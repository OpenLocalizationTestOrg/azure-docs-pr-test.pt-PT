---
title: "aaaAzure Toolkit para o IntelliJ - aplicações de depuração remota no HDInsight Spark | Microsoft Docs"
description: "Saiba como utilizar as ferramentas do HDInsight na Azure Toolkit para IntelliJ tooremotely depuração aplicações em execução em clusters do HDInsight Spark através de vpn."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a>Utilize o Toolkit do Azure para aplicações de toodebug IntelliJ remotamente no Spark do HDInsight através de VPN

Recomendamos a forma de Olá de depuração applicaltion spark remotamente através de ssh. Para obter instruções, consulte [remotamente depurar aplicações do Spark num cluster do HDInsight com o Toolkit do Azure para o IntelliJ através de SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).

Este artigo fornece orientação passo a passo sobre como toouse hello as ferramentas do HDInsight na Azure Toolkit para o IntelliJ toosubmit uma tarefa do Spark no cluster do HDInsight Spark e, em seguida, depurá-lo remotamente a partir do seu computador de secretária. toodo por isso, tem de efetuar Olá seguindo os passos de alto nível:

1. Crie um site para site ou ponto a site Virtual Network do Azure. Olá passos neste documento partem do princípio de que utiliza uma rede de site para site.
2. Crie um cluster do Spark no Azure HDInsight que faz parte de Olá site a site Rede Virtual do Azure.
3. Verifique a conectividade de Olá entre Olá cluster headnode e ambiente de trabalho.
4. Criar uma aplicação de Scala no IntelliJ IDEA e configurá-la para depuração remota.
5. Execute e depurar a aplicação Olá.

## <a name="prerequisites"></a>Pré-requisitos
* Uma subscrição do Azure. Consulte [Obter uma avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Um cluster do Apache Spark no HDInsight. Para obter instruções, consulte [clusters do Apache Spark criar no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Kit de desenvolvimento Java Oracle. Pode instalar a [aqui](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* IntelliJ IDEA. Este artigo utiliza a versão 2017.1. Pode instalar a [aqui](https://www.jetbrains.com/idea/download/).
* Ferramentas do HDInsight no Toolkit do Azure para o IntelliJ. As ferramentas do HDInsight para o IntelliJ estão disponíveis como parte da Olá Toolkit do Azure para o IntelliJ. Para obter instruções sobre como tooinstall Olá Toolkit do Azure, consulte [instalar Olá Toolkit do Azure para o IntelliJ](../azure-toolkit-for-intellij-installation.md).
* Registo para a sua subscrição do Azure de IntelliJ IDEA. Siga as instruções de Olá [aqui](hdinsight-apache-spark-intellij-tool-plugin.md).
* Ao executar a aplicação de Spark Scala para depuração remota num computador Windows, poderá obter uma exceção, conforme explicado no [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) que ocorre devido a falta de tooa WinUtils.exe no Windows. toowork em torno este erro, tem de [transferir Olá executável a partir daqui](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) como localização de tooa **C:\WinUtils\bin**. Em seguida, tem de adicionar uma variável de ambiente **HADOOP_HOME** e defina o valor de Olá da variável de Olá demasiado**C\WinUtils**.

## <a name="step-1-create-an-azure-virtual-network"></a>Passo 1: Criar uma Azure Virtual Network
Siga as instruções de Olá do Olá abaixo ligações toocreate uma Azure Virtual Network e, em seguida, verifique a conectividade de Olá entre o ambiente de trabalho Olá e a rede Virtual do Azure.

* [Criar uma VNet com uma ligação de VPN de site a site através do Portal do Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [Criar uma VNet com uma ligação de VPN de site para site com o PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [Configurar uma rede virtual de ligação de ponto a site tooa através do PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a>Passo 2: Criar um cluster do Spark do HDInsight
Também deve criar um cluster do Apache Spark no Azure HDInsight que faz parte de Olá Azure Virtual Network que criou. Utilize as informações de Olá disponíveis em [baseado em Linux criar clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Como parte da configuração opcional, selecione Olá Azure Virtual Network que criou no passo anterior Olá.

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a>Passo 3: Verificar a conectividade de Olá entre Olá cluster headnode e ambiente de trabalho
1. Obter o endereço IP Olá Olá headnode. Abra a IU do Ambari para cluster Olá. No painel do cluster de Olá, clique em **Dashboard**.

    ![Localizar headnode IP](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. Olá IU do Ambari, a partir do canto superior direito de Olá, clique em **anfitriões**.

    ![Localizar headnode IP](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. Deverá ver uma lista de nós de zookeeper, nós de trabalho e headnodes. Olá headnodes ter Olá **hn*** prefixo. Clique em headnode primeiro Olá.

    ![Localizar headnode IP](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. Em Olá parte inferior da página Olá que se abre, de Olá **resumo** caixa, endereço IP de Olá de cópia de Olá headnode e nome de anfitrião Olá.

    ![Localizar headnode IP](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. Incluem o endereço IP Olá e nome de anfitrião Olá do Olá headnode toohello **anfitriões** ficheiro no computador de Olá de onde pretende toorun e remotamente as tarefas de Spark Olá de depuração. Isto permitirá toocommunicate com headnode Olá utilizando o endereço IP Olá, bem como Olá nome do anfitrião.

   1. Abra um bloco de notas com permissões elevadas. No menu de ficheiro Olá, clique em **abra** e, em seguida, navegue até toohello localização do ficheiro de anfitriões de Olá. Num computador Windows, é `C:\Windows\System32\Drivers\etc\hosts`.
   2. Adicionar Olá seguir toohello **anfitriões** ficheiro.

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. O computador de Olá que ligado toohello Azure Virtual Network é utilizado pelo cluster do HDInsight Olá, certifique-se de que consegue enviar pings para ambos os headnodes Olá utilizando o endereço IP Olá, bem como o hostname Olá.
7. SSH no Olá cluster headnode utilizar instruções Olá em [Connect tooan cluster do HDInsight utilizando SSH](hdinsight-hadoop-linux-use-ssh-unix.md). De Olá cluster headnode, executar um ping endereço IP de Olá do computador de secretária Olá. Deve testar a conectividade tooboth Olá IP endereços atribuídos toohello computador, um para ligação de rede Olá e Olá para Olá Azure Virtual Network Olá computador está ligado.
8. Repita os passos de Olá para Olá, bem como outra headnode.

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a>Passo 4: Criar uma aplicação de Spark Scala utilizando as ferramentas do HDInsight Olá no Toolkit do Azure para o IntelliJ e configurá-la para depuração remota
1. Inicie o IntelliJ IDEA e criar um novo projeto. Na caixa de diálogo de projeto novo do Olá, certifique-Olá seguintes opções e, em seguida, clique em **seguinte**.

    ![Criar aplicações do Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * No painel esquerdo Olá, selecione **HDInsight**.
   * No painel direito Olá, selecione **Spark no HDInsight (Scala)**.
   * Clique em **Seguinte**.
2. Na próxima janela de Olá, forneça Olá os detalhes do projeto e, em seguida, clique em **concluir**.  
   - Forneça um nome de projeto e a localização do projeto.
   - Para **projeto SDK**, utilize Java 1.8 para o cluster do spark 2. x, Java 1.7 para um cluster do spark 1. x.
   - Para **Spark versão**, Assistente de criação do projeto Scala integra-se a versão correta para o SDK do Spark e Scala SDK. Se a versão de cluster do spark Olá for inferior 2.0, escolha spark 1. x. Caso contrário, deve selecionar spark2.x. Este exemplo utiliza Spark2.0.2 (Scala 2.11.8).
       ![Criar aplicações do Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)
  
3. projeto de Spark Olá criará automaticamente um artefacto para si. artefactos de Olá toosee, siga estes passos.

   1. De Olá **ficheiro** menu, clique em **estrutura do projeto**.
   2. No Olá **estrutura do projeto** caixa de diálogo, clique em **artefactos** toosee Olá predefinido artefacto que é criado.
   ![Criar JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)

      Também pode criar os seus artefactos bly clicando no Olá  **+**  ícone, realçado na imagem de Olá acima.

4. Adicione bibliotecas tooyour projeto. tooadd uma biblioteca, clique no nome do projeto Olá na árvore de projeto Olá e, em seguida, clique em **abra as definições do módulo**. No Olá **estrutura do projeto** caixa de diálogo, a partir do painel esquerdo do Olá, clique em **bibliotecas**, clique o símbolo de Olá (+) e, em seguida, clique em **do Maven**.

    ![Adicionar a biblioteca](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    No Olá **transferir biblioteca do repositório Maven** diálogo caixa, procurar e adicionar Olá seguintes bibliotecas.

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. Cópia `yarn-site.xml` e `core-site.xml` de Olá headnode do cluster e adicione-toohello projeto. Utilize Olá os seguintes ficheiros de Olá toocopy de comandos. Pode utilizar [Cygwin](https://cygwin.com/install.html) seguinte de Olá toorun `scp` comandos toocopy ficheiros Olá Olá headnodes de cluster.

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    Porque já foi adicionado o Olá cluster headnode IP endereços e nomes de anfitrião fo Olá ficheiro hosts no ambiente de trabalho Olá, podemos utilizar Olá **scp** comandos no Olá seguinte forma.

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    Adicione o projeto de tooyour estes ficheiros ao copiá-las em Olá **/src** pasta na sua árvore de projeto, por exemplo `<your project directory>\src`.
6. Olá atualização `core-site.xml` Olá toomake seguir as alterações.

   1. `core-site.xml`inclui uma conta de armazenamento de chaves toohello Olá encriptado associada ao cluster Olá. No Olá `core-site.xml` que adicionou toohello projeto, substituir Olá chave encriptada com a chave de armazenamento real Olá associado à conta do storage predefinida Olá. Consulte [gerir as chaves de acesso de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. Remover Olá seguintes entradas de Olá `core-site.xml`.

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. Guarde o ficheiro de Olá.
7. Adicione classe de principal de Olá para a sua aplicação. De Olá **Explorador de projeto**, faça duplo clique **src**, ponto demasiado**novo**e, em seguida, clique em **Scala classe**.

    ![Adicione o código de origem](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. No Olá **criar uma nova classe de Scala** diálogo caixa, forneça um nome para **tipo** selecione **objeto**e, em seguida, clique em **OK**.

    ![Adicione o código de origem](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. No Olá `MyClusterAppMain.scala` de ficheiros, cole Olá seguinte código. Este código cria o contexto de Spark Olá e inicia uma `executeJob` método Olá `SparkSample` objeto.

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. Repita os passos 8 e 9 acima tooadd chamado um novo objeto de Scala `SparkSample`. classe de toothis adicionar Olá seguinte código. Este código lê dados de Olá de Olá HVAC.csv (disponível em todos os clusters do HDInsight Spark), obtém linhas Olá que têm apenas um dígito na coluna seventh Olá Olá CSV e escreve saída Olá demasiado**/HVACOut** em predefinido Olá contentor de armazenamento Olá cluster.

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. Repita os passos 8 e 9 acima tooadd uma nova classe denominada `RemoteClusterDebugging`. Esta classe implementa Olá Spark teste arquitetura que é utilizada para depuração de aplicações. Adicionar Olá seguinte código toohello `RemoteClusterDebugging` classe.

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     Alguns pontos importantes toonote aqui:

   * Para `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, certifique-se Olá assemblagem Spark JAR no armazenamento de cluster Olá no caminho especificado Olá.
   * Para `setJars`, especifique a localização olá onde será criada jar do artefacto de Olá. Normalmente, é `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.
12. No Olá `RemoteClusterDebugging` classe, faça duplo clique Olá `test` palavra-chave e selecione **criar configuração de RemoteClusterDebugging**.

    ![Criar configuração remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. Na caixa de diálogo Olá, forneça um nome para a configuração de Olá e selecione Olá **testar tipo** como **nome para o teste**. Deixe todos os outros valores como predefinição, clique em **aplicar**e, em seguida, clique em **OK**.

    ![Criar configuração remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. Deverá ver uma **remoto execute** configuração pendente na barra de menus Olá.

    ![Criar configuração remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a>Passo 5: Executar a aplicação Olá no modo de depuração
1. No projeto IntelliJ IDEA, abra `SparkSample.scala` e criar um rdd1 too'val seguinte do ponto de interrupção '. No menu de pop-up de Olá para criar um ponto de interrupção, selecione **linha na função executeJob**.

    ![Adicionar um ponto de interrupção](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. Clique em Olá **depurar executar** toohello seguinte botão **remoto execute** configuração pendente toostart execução da aplicação Olá.

    ![Executar o programa de Olá no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. Quando a execução do programa Olá atinge o ponto de interrupção Olá, deverá ver uma **depurador** separador Olá inferior painel.

    ![Executar o programa de Olá no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. Clique em Olá (**+**) ícone tooadd uma veja conforme mostrado na imagem de Olá abaixo.

    ![Executar o programa de Olá no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    Aqui, porque a aplicação Olá quebrou antes de variável de Olá `rdd1` foi criado, utilizando este veja é possível ver o que são Olá primeiro 5 linhas na variável Olá `rdd`. Prima **ENTER**.

    ![Executar o programa de Olá no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    O que vê na imagem de Olá acima é no tempo de execução, pode consultar terrabytes de dados e de depuração como avança de ser a aplicação. Por exemplo, no resultado de Olá mostrado na imagem de Olá acima, pode ver essa Olá primeira linha da saída de Olá é um cabeçalho. Com base nisso, pode modificar a linha de cabeçalho do aplicação código tooskip Olá se necessário.
5. Agora pode clicar em Olá **retomar programa** tooproceed ícone com a sua aplicação em execução.

    ![Executar o programa de Olá no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. Se a aplicação Olá for concluída com êxito, deve ver um resultado semelhante Olá seguinte.

    ![Executar o programa de Olá no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <a name="seealso"></a>Ver também
* [Descrição geral: Apache Spark no Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Demonstração
* Criar projeto Scala (vídeo): [criar aplicações do Spark Scala](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* Depuração remota (vídeo): [Toolkit do Azure de utilização para o IntelliJ toodebug aplicações do Spark remotamente num Cluster do HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>Cenários
* [Spark com BI: Efetuar uma análise de dados interativa com o Spark no HDInsight com ferramentas do BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark com Machine Learning: Utilizar o Spark no HDInsight para analisar a temperatura do edifício com dados de AVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark com Machine Learning: utilizar o Spark no HDInsight toopredict inspeções alimentares](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Transmissão em Fluxo do Spark: Utilizar o Spark no HDInsight para criar aplicações de transmissão em fluxo em tempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análise de registos de sites com o Spark no HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Criar e executar aplicações
* [Criar uma aplicação autónoma com o Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Executar tarefas remotamente num cluster do Spark com o Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Ferramentas e extensões
* [Utilize as ferramentas do HDInsight no Toolkit do Azure para o IntelliJ toocreate e submeter aplicações do Spark scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utilize o Toolkit do Azure para aplicações do Spark toodebug IntelliJ remotamente através de SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Utilize as ferramentas do HDInsight para o IntelliJ com Hortonworks Sandbox](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Utilize as ferramentas do HDInsight Toolkit do Azure para aplicações do Spark Eclipse toocreate](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Utilizar blocos de notas do Zeppelin com um cluster do Spark no HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponíveis para o bloco de notas do Jupyter no cluster do Spark para o HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Utilizar pacotes externos com blocos de notas do Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalar o Jupyter no seu computador e ligue tooan cluster do HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gerir recursos
* [Gerir os recursos de cluster do Apache Spark Olá no Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Controlar e depurar tarefas em execução num cluster do Apache Spark do HDInsight](hdinsight-apache-spark-job-debugging.md)
