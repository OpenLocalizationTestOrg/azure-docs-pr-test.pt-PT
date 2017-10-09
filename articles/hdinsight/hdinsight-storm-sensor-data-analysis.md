---
title: dados de sensores de aaaAnalyze com Apache Storm e HBase | Microsoft Docs
description: "Saiba como tooconnect tooApache Storm com uma rede virtual. Utilizar o Storm com dados de sensores do HBase tooprocess de um hub de eventos e visualizá-lo com D3.js."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a>Analisar dados de sensor com Apache Storm, o Hub de eventos e o HBase no HDInsight (Hadoop)

Saiba como toouse Apache Storm no HDInsight tooprocess dados de sensores do Hub de eventos do Azure. dados de Olá, em seguida, são armazenados no Apache HBase no HDInsight e visualizados utilizando D3.js.

modelo do Azure Resource Manager Olá utilizado neste documento demonstra como toocreate vários recursos do Azure num grupo de recursos. modelo de Olá cria uma rede Virtual do Azure, dois clusters do HDInsight (Storm e HBase) e uma aplicação Web do Azure. Uma implementação de node.js de um dashboard web em tempo real é automaticamente implementada toohello web app.

> [!NOTE]
> informações Olá este documento e o exemplo neste documento exigem HDInsight versão 3.6.
>
> Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior. Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).

## <a name="prerequisites"></a>Pré-requisitos

* Uma subscrição do Azure.
* [NODE.js](http://nodejs.org/): dashboard de web de Olá toopreview utilizados localmente no seu ambiente de desenvolvimento.
* [Java e Olá JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): utilizada topologia do Storm toodevelop Olá.
* [Maven](http://maven.apache.org/what-is-maven.html): projeto de Olá toobuild e compilação utilizados.
* [Git](http://git-scm.com/): projeto de Olá toodownload utilizado a partir do GitHub.
* Um **SSH** cliente: utilizada tooconnect toohello HDInsight baseado em Linux clusters. Para obter mais informações, veja [Utilizar SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).


> [!IMPORTANT]
> Não precisa de um cluster do HDInsight existente. passos de Olá neste documento criar Olá os seguintes recursos:
> 
> * Uma rede Virtual do Azure
> * Um cluster Storm no HDInsight (baseado em Linux, dois nós de trabalho)
> * O HBase no HDInsight cluster (baseado em Linux, dois nós de trabalho)
> * Uma aplicação Web do Azure que aloja o dashboard de web de Olá

## <a name="architecture"></a>Arquitetura

![diagrama da arquitetura](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

Neste exemplo consiste em Olá os seguintes componentes:

* **Os Hubs de eventos do Azure**: contém dados que são recolhidos dos sensores.
* **Storm no HDInsight**: fornece processamento em tempo real de dados a partir do Hub de eventos.
* **O HBase no HDInsight**: Fornece um arquivo de dados NoSQL persistente para os dados depois de ter sido processada pela Storm.
* **Serviço de rede Virtual do Azure**: permite as comunicações seguras entre Olá Storm no HDInsight e HBase nos clusters do HDInsight.
  
  > [!NOTE]
  > Uma rede virtual é necessária quando utilizar a API de cliente de Java HBase Olá. Não está exposta através de gateway de público Olá para clusters de HBase. Clusters de HBase instalar e Storm para Olá permite que a mesma rede virtual Olá cluster do Storm (ou qualquer outro sistema na rede virtual Olá) toodirectly aceder HBase através da API de cliente.

* **Web site do dashboard**: um dashboard de exemplo que gráficos de dados em tempo real.
  
  * Web site de Olá está implementada no Node.js.
  * [Socket.IO](http://socket.io/) é utilizado para comunicação em tempo real entre topologia do Storm Olá e site Olá.
    
    > [!NOTE]
    > A utilização de Socket.io para comunicação é um detalhe de implementação. Pode utilizar qualquer estrutura de comunicações, tais como WebSockets não processados ou SignalR.

  * [D3.js](http://d3js.org/) toograph utilizados Olá dados que é enviado toohello site.

> [!IMPORTANT]
> Dois clusters são necessárias, conforme não é não existe nenhum método suportado toocreate um cluster do HDInsight para Storm e HBase.

Olá topologia lê dados de Hub de eventos utilizando Olá [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) classe e escreve dados no HBase utilizando Olá [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) classe. Comunicação com o Web site de Olá é conseguida utilizando [socket.io client.java](https://github.com/nkzawa/socket.io-client.java).

Olá diagrama a seguir explica esquema Olá da topologia de Olá:

![diagrama da topologia](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> Este diagrama é uma visão simplificada de topologia de Olá. Para cada partição no seu Hub de eventos, é criada uma instância de cada componente. Estas instâncias são distribuídas entre os nós no cluster de Olá Olá e dados são encaminhados entre eles, da seguinte forma:
> 
> * Dados a partir do analisador de toohello Olá spout tem balanceamento de carga.
> * Dados de Olá parser toohello Dashboard e o HBase são agrupados por ID de dispositivo, para que as mensagens de Olá mesmo dispositivo sempre fluxo toohello mesmo componente.

### <a name="topology-components"></a>Componentes de topologia

* **Event Hub Spout**: spout Olá é fornecido como parte da versão do Apache Storm 0.10.0 e planos superiores.
  
  > [!NOTE]
  > spout de Hub de eventos de Olá utilizado neste exemplo requer um Storm no clusters do HDInsight versão 3.5 ou 3.6.

* **ParserBolt.java**: dados Olá que são emitidos por spout Olá for JSON não processado e, ocasionalmente mais do que um evento é emitido um momento. Este bolt lê dados de Olá emitidos por Olá spout e analisa a mensagem de JSON de saudação. bolt Olá, em seguida, emite dados Olá como uma cadeia de identificação contém vários campos.
* **DashboardBolt.java**: este componente demonstra como toouse Olá Socket.io biblioteca de clientes para os dados de toosend Java no dashboard de web de toohello em tempo real.
* **não hbase.yaml**: Olá utilizada quando executado no modo de local de definição de topologia. Não utilize componentes de HBase.
* **com hbase.yaml**: Olá utilizada ao executar a topologia de Olá no cluster de Olá de definição de topologia. Utilizar o HBase componentes.
* **Dev.Properties**: Olá informações de configuração para spout de Hub de eventos de Olá, bolt de HBase e componentes de dashboard.

## <a name="prepare-your-environment"></a>Preparar o ambiente

Antes de utilizar este exemplo, tem de criar um Hub de eventos do Azure, que topologia do Storm Olá lê a partir do.

### <a name="configure-event-hub"></a>Configurar o Hub de eventos

Hub de eventos é a origem de dados de Olá para este exemplo. Utilize os seguintes passos toocreate um Hub de eventos de Olá.

1. De Olá [portal do Azure](https://portal.azure.com), selecione **+ novo** -> **Internet das coisas** -> **Event Hubs**.
2. No Olá **criar espaço de nomes** secção, execute Olá seguintes tarefas:
   
   1. Introduza um **nome** para Olá espaço de nomes.
   2. Selecione um escalão de preço. **Básico** é suficiente para este exemplo.
   3. Selecione Olá Azure **subscrição** toouse.
   4. Selecione um grupo de recursos existente ou crie um novo.
   5. Selecione Olá **localização** para Olá Hub de eventos.
   6. Selecione **Pin toodashboard**e, em seguida, clique em **criar**.

3. Quando tiver concluído o processo de criação de Olá, é apresentada Olá informações de Hubs de eventos para o espaço de nomes. Aqui, selecione **+ adicionar Hub de eventos**. No Olá **criar o Hub de eventos** secção, introduza um nome de **sensordata**e, em seguida, selecione **criar**. Deixe Olá outros campos de valores predefinidos de Olá.
4. Hubs de eventos de Olá ver do seu espaço de nomes, selecione **Event Hubs**. Selecione Olá **sensordata** entrada.
5. A partir da Olá sensordata Hub de eventos, selecione **políticas de acesso partilhado**. Olá utilize **+ adicionar** Olá tooadd de hiperligação seguinte políticas:

    | Nome da política | afirmações |
    | ----- | ----- |
    | dispositivos | Enviar |
    | Storm | Escutar |

1. Selecione ambas as políticas e tome nota do Olá **chave primária** valor. Precisa de valor de Olá para ambas as políticas nos passos futuras.

## <a name="download-and-configure-hello-project"></a>Transferir e configurar o projeto de Olá

Utilize Olá seguir o projeto de Olá toodownload a partir do GitHub.

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

Após a conclusão do comando de Olá, tiver Olá seguir a estrutura de diretórios:

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> Este documento não passa nos detalhes de toofull de código Olá incluídos neste exemplo. No entanto, o código de Olá totalmente é comentado.

tooconfigure Olá projeto tooread do Hub de eventos, abra Olá `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` de ficheiros e adicionar o seu toohello de informações de Hub de eventos seguintes linhas:

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a>Compilar e testar localmente

> [!IMPORTANT]
> Com a topologia de Olá localmente requer um ambiente de desenvolvimento do Storm de trabalho. Para obter mais informações, consulte [configurar um ambiente de desenvolvimento do Storm](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) em Apache.org.

> [!WARNING]
> Se estiver a utilizar um ambiente de desenvolvimento do Windows, poderá receber um `java.io.IOException` ao executar localmente a topologia de Olá. Se assim for, deslocar-se na topologia de Olá toorunning no HDInsight.

Antes de testar, tem de começar Olá dashboard tooview Olá resultado topologia Olá e gerar dados toostore no Hub de eventos.

> [!IMPORTANT]
> componente de HBase Olá desta topologia não está ativo quando testar localmente. Olá Java API para o cluster de HBase Olá não pode ser acedido a partir de fora Olá Azure Virtual Network contém Olá clusters.

### <a name="start-hello-web-application"></a>Iniciar a aplicação web de Olá

1. Abra uma linha de comandos e mude de diretório demasiado`hdinsight-eventhub-example/dashboard`. Utilize Olá dependências Olá tooinstall de comando necessárias para a aplicação web de Olá os seguintes:
   
    ```bash
    npm install
    ```

2. Utilize Olá aplicação web do comando toostart Olá os seguintes:
   
    ```bash
    node server.js
    ```
   
    Verá uma mensagem toohello semelhante seguinte texto:
   
        Server listening at port 3000

3. Abra um browser e introduza `http://localhost:3000/` como endereço Olá. É apresentada uma página de toohello semelhante seguinte imagem:
   
    ![dashboard da Web](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    Deixe esta linha de comandos aberta. Depois de testar, utilize o servidor de web de Olá de toostop Ctrl-C.

### <a name="generate-data"></a>Gerar dados

> [!NOTE]
> Olá passos nesta secção utilizam o Node.js para que possa ser utilizados em qualquer plataforma. Para outros exemplos de idioma, consulte Olá `SendEvents` diretório.

1. Abra uma nova linha de comandos, shell ou terminal e altere os diretórios demasiado`hdinsight-eventhub-example/SendEvents/nodejs`. dependências de Olá tooinstall necessárias para a aplicação Olá, utilize Olá os seguintes comandos:

    ```bash
    npm install
    ```

2. Abra Olá `app.js` ficheiro num editor de texto e adicione Olá informações de Hub de eventos que obteve anteriormente:
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > Este exemplo assume que utilizou `sensordata` como nome de Olá do seu Hub de eventos. E que `devices` como nome de Olá da política de Olá que tenha um `Send` de afirmação.

3. Utilize os seguintes comandos tooinsert novo as entradas no Hub de eventos de Olá:
   
    ```bash
    node app.js
    ```
   
    Pode ver várias linhas de saída que contenham dados Olá enviados tooEvent Hub:
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-hello-topology"></a>Criar e iniciar a topologia de Olá

1. Abra uma nova linha de comandos e altere os diretórios demasiado`hdinsight-eventhub-example/TemperatureMonitor`. toobuild e pacote Olá topologia, utilize Olá os seguintes comandos: 

    ```bash
    mvn clean package
    ```

2. topologia de Olá toostart no modo local, Olá utilize os seguintes comandos:

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * `--local`topologia de Olá é iniciado no modo local.
    * `--filter`utiliza Olá `dev.properties` ficheiro toopopulate parâmetros na definição de topologia Olá.
    * `resources/no-hbase.yaml`utiliza Olá `no-hbase.yaml` definição de topologia.
 
   Depois de iniciada, a topologia de Olá lê entradas de Hub de eventos e envia-as dashboard toohello em execução no seu computador local. Deverá ver as linhas são apresentadas no dashboard de web de Olá, semelhante toohello seguinte imagem:
   
    ![dashboard com os dados](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. Enquanto dashboard Olá está em execução, utilizar Olá `node app.js` toosend novos dados tooEvent Hubs os passos de comando a partir de Olá anterior. Porque os valores de temperatura Olá aleatoriamente são gerados, gráfico de Olá deve atualizar tooshow alterações grande temperatura.
   
   > [!NOTE]
   > Tem de constar Olá **hdinsight-eventhub-exemplo/SendEvents/Nodejs** diretório quando utilizar Olá `node app.js` comando.

3. Depois de verificar que dashboard Olá atualizações, pare Olá topologia utilizando Ctrl + C. Pode utilizar o servidor local web do Ctrl + C toostop Olá também.

## <a name="create-a-storm-and-hbase-cluster"></a>Criar um cluster do Storm e HBase

Olá, os passos nesta utilização de secção um [modelo Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) toocreate um cluster de rede Virtual do Azure e um Storm e HBase na rede virtual Olá. modelo de Olá também cria uma aplicação Web do Azure e implementa uma cópia do dashboard de Olá para a mesma.

> [!NOTE]
> Uma rede virtual é utilizada para que a topologia de Olá em execução no cluster do Storm Olá pode comunicar diretamente com o cluster de HBase Olá Olá HBase Java API a utilizar.

modelo do Resource Manager Olá utilizado neste documento está localizado num contentor de blob público em **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.

1. Clique em Olá seguinte botão toosign no tooAzure e modelo do Resource Manager Olá aberta no Olá portal do Azure.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. De Olá **implementação personalizada** secção, introduza Olá os seguintes valores:
   
    ![Parâmetros do HDInsight](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * **Nome do Cluster de base**: este valor é utilizado como nome de base de Olá para clusters de Storm e HBase Olá. Por exemplo, introduzir **abc** cria um cluster do Storm com o nome **storm abc** e um cluster HBase com o nome **hbase abc**.
   * **Nome de utilizador de início de sessão do cluster**: nome de utilizador de admin Olá para clusters de Storm e HBase Olá.
   * **Palavra-passe de início de sessão do cluster**: palavra-passe utilizador de administrador de Olá para clusters de Storm e HBase Olá.
   * **Nome de utilizador SSH**: Olá toocreate de utilizador do SSH para clusters de Storm e HBase Olá.
   * **Palavra-passe SSH**: Olá palavra-passe do utilizador do SSH Olá para clusters de Storm e HBase Olá.
   * **Localização**: região Olá clusters Olá criados no.
     
     Clique em **OK** parâmetros de Olá toosave.

3. Olá utilize **Noções básicas** secção toocreate um grupo de recursos ou selecione um existente.
4. No Olá **localização do grupo de recursos** menu pendente, selecione Olá mesma localização que selecionou para Olá **localização** parâmetro Olá **definições** secção.
5. Leia Olá termos e condições e, em seguida, selecione **concordo toohello termos e condições indicadas acima**.
6. Por fim, verifique **Pin toodashboard** e, em seguida, selecione **Compra**. Demora cerca de 20 minutos toocreate clusters Olá.

Depois de tem sido criados recursos Olá, são apresentadas informações sobre o grupo de recursos de Olá.

![Grupo de recursos para vnet Olá e clusters](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> Tenha em atenção que os nomes de Olá dos clusters do HDInsight Olá são **storm BASENAME** e **hbase BASENAME**, onde BASENAME nome Olá fornecido toohello modelo. Utilize estes nomes num passo posterior ao ligar a toohello clusters. Também é tenha em atenção que Olá nome do site de dashboard Olá **basename dashboard**. Este valor é utilizado mais tarde neste documento.

## <a name="configure-hello-dashboard-bolt"></a>Configurar bolt de Dashboard Olá

toosend dashboard toohello dados implementado como uma aplicação web, tem de modificar Olá seguinte linha no Olá `dev.properties`ficheiro:

```yaml
dashboard.uri: http://localhost:3000
```

Alteração `http://localhost:3000` demasiado`http://BASENAME-dashboard.azurewebsites.net` e guarde o ficheiro de Olá. Substitua **BASENAME** com o nome de base Olá fornecido no passo anterior Olá. Também pode utilizar o grupo de recursos de Olá criado anteriormente tooselect Olá dashboard e vista Olá URL.

## <a name="create-hello-hbase-table"></a>Criar a tabela de HBase Olá

toostore dados no HBase, iremos tem primeiro de criar uma tabela. Pré-criar recursos de que necessita de Storm toowrite para, como a tentar toocreate recursos a partir de dentro de uma topologia do Storm podem resultar em várias instâncias ao tentar toocreate Olá mesmo recurso. Criar Olá recursos fora da topologia de Olá e utilizar o Storm para leitura/escrita e de análise.

1. Utilize o SSH tooconnect toohello cluster de HBase utilizando SSH Olá e palavra-passe que forneceu toohello modelo durante a criação do cluster. Por exemplo, se ligar utilizando Olá `ssh` comando, teria de utilizar Olá sintaxe:
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    Substitua `sshuser` com o nome de utilizador do SSH Olá que forneceu ao criar o cluster de Olá. Substitua `clustername` com o nome de cluster de HBase Olá.

2. Sessão SSH Olá, inicie o shell de HBase Olá.
   
    ```bash
    hbase shell
    ```
   
    Assim que a shell de Olá foi carregadas, verá um `hbase(main):001:0>` linha.

3. No Olá shell de HBase, introduza Olá comando toocreate o dados do sensor toostore Olá uma tabela a seguir:
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. Certifique-se de que essa tabela Olá foi criada utilizando Olá os seguintes comandos:
   
    ```hbase
    scan 'SensorData'
    ```
   
    Esta ação devolve informações toohello semelhante seguinte o exemplo, indicando que existem 0 linhas na tabela de Olá.
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. Introduza `exit` tooexit Olá shell de HBase:

## <a name="configure-hello-hbase-bolt"></a>Configurar bolt de HBase Olá

toowrite tooHBase do cluster do Storm Olá, tem de fornecer bolt de HBase Olá com detalhes de configuração de Olá do HBase cluster.

1. Utilize um dos Olá seguir o quórum do exemplos tooretrieve Olá Zookeeper para o cluster de HBase:

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > Substitua `your_HDInsight_cluster_name` com o nome de Olá de cluster do HDInsight. Para obter mais informações sobre como instalar Olá `jq` utilitário, consulte [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).
    >
    > Quando solicitado, introduza a palavra-passe de Olá para início de sessão do Olá HDInsight admin.

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > Substitua ' your_HDInsight_cluster_name com o nome de Olá de cluster do HDInsight. Quando solicitado, introduza a palavra-passe de Olá para início de sessão do Olá HDInsight admin.
    >
    > Este exemplo requer o Azure PowerShell. Para obter mais informações sobre como utilizar o Azure PowerShell, consulte [começar com o Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)

    informações de Olá devolvidas por estes exemplos são semelhante toohello seguinte texto:

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    Estas informações são utilizadas por toocommunicate do Storm com o cluster de HBase Olá.

2. Modificar Olá `dev.properties` de ficheiros e adicionar Olá Zookeeper quórum informações toohello seguinte linha:

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a>Criar pacote e implementar Olá solução tooHDInsight

No seu ambiente de desenvolvimento, utilize Olá os seguintes passos toodeploy Olá Storm topologia toohello cluster do storm.

1. De Olá `TemperatureMonitor` diretório seguinte de Olá utilize comandos tooperform uma nova compilação e cria um pacote JAR do seu projeto:
   
        mvn clean package
   
    Este comando cria um ficheiro denominado `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `destino ' diretório do seu projeto.

2. Olá do utilize scp tooupload `TemperatureMonitor-1.0-SNAPSHOT.jar` e `dev.properties` cluster do Storm de tooyour de ficheiros. No Olá seguinte o exemplo, substitua `sshuser` com o utilizador do SSH Olá que forneceu ao criar o cluster de Olá, e `clustername` com o nome de Olá do seu cluster do Storm. Quando lhe for pedido, introduza a palavra-passe de Olá para utilizador do SSH Olá.
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > Poderá demorar vários minutos ficheiros de Olá tooupload.

    Para obter mais informações sobre como utilizar Olá `scp` e `ssh` comandos com o HDInsight, consulte [utilizar o SSH com o HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)

3. Depois de terem sido carregado ficheiro Olá, ligue o cluster do Storm toohello utilizando SSH.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    Substitua `sshuser` com o nome de utilizador do SSH Olá. Substitua `clustername` com o nome de cluster do Storm Olá.

4. toostart Olá topologia, utilize Olá comando da sessão SSH Olá os seguintes:
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * `--remote`submete Olá topologia toohello serviço Nimbus, nós de supervisor toohello no cluster de Olá, distribui-lo.
    * `--filter`utiliza Olá `dev.properties` ficheiro toopopulate parâmetros na definição de topologia Olá.
    * `-R /with-hbase.yaml`utiliza Olá `with-hbase.yaml` topologia incluída no pacote de Olá.

5. Depois de é iniciado a topologia de Olá, abra um Web site toohello do browser publicado no Azure, em seguida, utilize Olá `node app.js` comando toosend dados tooEvent Hub. Deverá ver Olá web dashboard toodisplay Olá as informações de atualização.
   
    ![dashboard](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a>Ver os dados de HBase

Utilize os seguintes passos tooconnect tooHBase de Olá e certifique-se de que foi escritos dados Olá toohello tabela:

1. Utilize o SSH tooconnect toohello HBase cluster.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    Substitua `sshuser` com o nome de utilizador do SSH Olá. Substitua `clustername` com o nome de cluster de HBase Olá.

2. Sessão SSH Olá, inicie o shell de HBase Olá.
   
    ```bash
    hbase shell
    ```
   
    Assim que a shell de Olá foi carregadas, verá um `hbase(main):001:0>` linha.

3. Ver as linhas da tabela de Olá:
   
    ```hbase
    scan 'SensorData'
    ```
   
    Este comando devolve informações toohello semelhante seguir texto, com a indicação de que não há dados na tabela de Olá.
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > Esta operação de análise devolve um máximo de 10 linhas da tabela de Olá.

## <a name="delete-your-clusters"></a>Eliminar os clusters

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

clusters de Olá toodelete, de armazenamento e de aplicação web de uma só vez, elimine o grupo de recursos de Olá que contém-los.

## <a name="next-steps"></a>Passos seguintes

Para obter mais exemplos de topologias do Storm com o HDInsight, consulte [topologias de exemplo para Storm no HDInsight](hdinsight-storm-example-topology.md)

Para mais informações sobre o Apache Storm, consulte Olá [Apache Storm](https://storm.incubator.apache.org/) site.

Para obter mais informações sobre o HBase no HDInsight, consulte Olá [HBase com o HDInsight Overview](hdinsight-hbase-overview.md).

Para obter mais informações sobre Socket.io, consulte Olá [socket.io](http://socket.io/) site.

Para mais informações sobre D3.js, consulte [D3.js - documentos de orientada por dados](http://d3js.org/).

Para obter informações sobre como criar topologias em Java, consulte [topologias de Java desenvolver para o Apache Storm no HDInsight](hdinsight-storm-develop-java-topology.md).

Para obter informações sobre como criar topologias no .NET, consulte [desenvolver topologias c# para Apache Storm no HDInsight com o Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

[azure-portal]: https://portal.azure.com
