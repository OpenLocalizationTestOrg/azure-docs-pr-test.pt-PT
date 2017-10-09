---
title: "desenvolvimento de ações de aaaScript com o HDInsight baseado em Linux - Azure | Microsoft Docs"
description: "Saiba como toouse Bash scripts toocustomize clusters do HDInsight baseado em Linux. funcionalidade de ação de script de Olá do HDInsight permite-lhe toorun scripts durante ou após a criação do cluster. Scripts podem ser utilizado toochange definições de configuração de cluster ou instalar software adicional."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a>Desenvolvimento de ações de script com o HDInsight

Saiba como utilizar o cluster do HDInsight Bash toocustomize scripts. Ações de script são uma forma toocustomize HDInsight durante ou após a criação do cluster.

> [!IMPORTANT]
> passos de Olá neste documento exigem um cluster do HDInsight que utiliza o Linux. Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior. Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).

## <a name="what-are-script-actions"></a>Quais são as ações de script

Ações de script são scripts de Bash Azure é executado na Olá cluster nós toomake as alterações de configuração ou instale o software. Uma ação de script é executada como raiz e fornece acesso total de nós de cluster toohello direitos.

Ações de script podem ser aplicadas através de Olá seguintes métodos:

| Utilize este método tooapply um script... | Durante a criação de cluster... | Num cluster em execução... |
| --- |:---:|:---:|
| Portal do Azure |✓ |✓ |
| Azure PowerShell |✓ |✓ |
| CLI do Azure |&nbsp; |✓ |
| SDK de .NET do HDInsight |✓ |✓ |
| Modelo Azure Resource Manager |✓ |&nbsp; |

Para obter mais informações sobre como utilizar estas ações de script de tooapply métodos, consulte [HDInsight personalizar clusters com ações de script](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="bestPracticeScripting"></a>Melhores práticas para o desenvolvimento do script

Quando desenvolver um script personalizado para um cluster do HDInsight, existem várias tookeep práticas melhor em mente:

* [Versão do destino Olá Hadoop](#bPS1)
* [Destino Olá versão do SO](#bps10)
* [Fornecer estável liga tooscript recursos](#bPS2)
* [Utilizar recursos previamente compilados](#bPS4)
* [Certifique-se de que o script de personalização do cluster Olá é idempotent](#bPS3)
* [Certifique-se de elevada disponibilidade da arquitetura de cluster Olá](#bPS5)
* [Configurar Olá componentes personalizados toouse Blob storage do Azure](#bPS6)
* [Escrever informações tooSTDOUT e STDERR](#bPS7)
* [Guardar ficheiros como ASCII com endings de linha de LF](#bps8)
* [Utilizar toorecover de lógica de repetição de erros transitórios](#bps9)

> [!IMPORTANT]
> Ações de script tem de concluir dentro de 60 minutos ou processo Olá falha. Durante o aprovisionamento de nó, executar script de Olá simultaneamente com outros processos de instalação e configuração. Disputa pelos recursos, tais como a largura de banda de CPU, tempo ou de rede pode fazer com que Olá script tootake mais toofinish que-lo no seu ambiente de desenvolvimento.

### <a name="bPS1"></a>Versão do destino Olá Hadoop

Versões diferentes do HDInsight têm versões diferentes dos serviços de Hadoop e componentes instalados. Se o script espera uma versão específica de um serviço ou componente, só deve utilizar o script de Olá com a versão de Olá do HDInsight que inclui os componentes de Olá necessário. Pode encontrar informações sobre versões de componentes incluídos com o HDInsight utilizando Olá [controlo de versões do HDInsight componente](hdinsight-component-versioning.md) documento.

### <a name="bps10"></a>Versão de SO de Olá de destino

HDInsight baseado em Linux baseia Olá distribuição Ubuntu Linux. Versões diferentes do HDInsight baseiam-se em diferentes versões do Ubuntu, que pode alterar a forma como se comporta seu script. Por exemplo, o HDInsight 3.4 e anterior baseiam-se em versões do Ubuntu que utilizam Upstart. Baseia-se no Ubuntu 16.04, que utiliza Systemd versão 3.5. Systemd e Upstart dependem comandos diferentes, pelo que o seu script deve ser escrito toowork com ambos.

Outra diferença importante entre HDInsight 3.4 e 3.5 é que `JAVA_HOME` agora pontos tooJava 8.

Pode verificar a versão de SO de Olá utilizando `lsb_release`. Olá código seguinte demonstra como toodetermine se hello do script está em execução no Ubuntu 14 ou 16:

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

Pode localizar o script de completo de Olá que contenha estes fragmentos em https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.

Para a versão de Olá do Ubuntu que é utilizado pelo HDInsight, consulte Olá [versão do componente de HDInsight](hdinsight-component-versioning.md) documento.

toounderstand Olá diferenças Systemd e Upstart, consulte [Systemd para utilizadores Upstart](https://wiki.ubuntu.com/SystemdForUpstartUsers).

### <a name="bPS2"></a>Fornecer estável liga tooscript recursos

Olá script e de recursos associados têm de permanecer disponíveis em toda a duração de Olá do cluster de Olá. Estes recursos são necessários se novos nós são adicionados toohello cluster durante operações de dimensionamento.

melhor prática de Olá é toodownload e arquivar tudo numa conta do Storage do Azure na sua subscrição.

> [!IMPORTANT]
> conta de armazenamento de Olá utilizada tem de ser Olá conta do storage predefinida para o cluster de Olá ou um contentor público só de leitura em qualquer outra conta de armazenamento.

Por exemplo, os exemplos de Olá fornecidos pela Microsoft são armazenados no Olá [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) conta de armazenamento. Este é um contentor público só de leitura mantido pela equipa do HDInsight Olá.

### <a name="bPS4"></a>Utilizar recursos previamente compilados

Olá tooreduce tempo demora toorun Olá script, evite operações compilam recursos a partir do código de origem. Por exemplo, a pré-compilar recursos e armazená-las num blob Storage do Azure de conta no Olá mesmo centro de dados como o HDInsight.

### <a name="bPS3"></a>Certifique-se de que o script de personalização do cluster Olá é idempotent

Scripts tem de ser idempotent. Se o script de Olá é executada várias vezes, deverá devolver Olá toohello cluster mesmo Estado de cada vez.

Por exemplo, um script que modifica os ficheiros de configuração deve não adicionar as entradas duplicadas se executada várias vezes.

### <a name="bPS5"></a>Certifique-se de elevada disponibilidade da arquitetura de cluster Olá

Clusters do HDInsight baseado em Linux fornecem dois nós principais que estão ativas num cluster de Olá e executam ações de script em ambos os nós. Se os componentes de Olá que instalar esperam apenas um nó principal, não instale componentes Olá em ambos os nós principais.

> [!IMPORTANT]
> Serviços fornecidos como parte do HDInsight são toofail concebida entre dois nós principais de Olá conforme necessário. Esta funcionalidade não é prolongada componentes toocustom instalados através de ações de script. Se necessitar de elevada disponibilidade de componentes personalizados, tem de implementar o seus próprios mecanismo de ativação pós-falha.

### <a name="bPS6"></a>Configurar Olá componentes personalizados toouse Blob storage do Azure

Os componentes que instalar num cluster de Olá poderão ter uma configuração predefinida, que utiliza armazenamento distribuído ficheiro sistema Hadoop (HDFS). O HDInsight utiliza o armazenamento do Azure ou para o Data Lake Store como armazenamento de predefinido Olá. Ambos fornecem um sistema de ficheiros compatíveis do HDFS que mantém os dados, mesmo se o cluster de Olá é eliminado. Poderá ser necessário componentes tooconfigure instalar toouse WASB ou ADL em vez do HDFS.

Na maioria das operações, não terá de sistema de ficheiros de Olá toospecify. Por exemplo, o seguinte Olá copia o ficheiro de giraph examples.jar de Olá do armazenamento de toocluster do sistema de ficheiros local Olá:

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

Neste exemplo, Olá `hdfs` comando utiliza o armazenamento de cluster predefinido de Olá transparente. Para algumas operações, poderá ser necessário toospecify Olá URI. Por exemplo, `adl:///example/jars` para o Data Lake Store ou `wasb:///example/jars` para armazenamento do Azure.

### <a name="bPS7"></a>Escrever informações tooSTDOUT e STDERR

HDInsight regista a saída do script que é escrito tooSTDOUT e STDERR. Pode ver estas informações através da web do Ambari Olá IU.

> [!NOTE]
> Ambari só está disponível se o cluster de Olá é criado com êxito. Se utilizar uma ação de script durante a criação do cluster e a criação falhar, consulte Olá secção de resolução de problemas [clusters do HDInsight de personalizar através da ação de script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) para outras formas de aceder a informações com sessão iniciada.

A maioria dos utilitários e pacotes de instalação já escrever informações tooSTDOUT e STDERR, no entanto, poderá pretender que o registo adicional tooadd. toosend texto tooSTDOUT, utilize `echo`. Por exemplo:

```bash
echo "Getting ready tooinstall Foo"
```

Por predefinição, `echo` envia Olá tooSTDOUT de cadeia. toodirect-tooSTDERR, adicionar `>&2` antes `echo`. Por exemplo:

```bash
>&2 echo "An error occurred installing Foo"
```

Isto redireciona informações escritas em vez disso, tooSTDOUT tooSTDERR (2). Para obter mais informações sobre o redirecionamento de e/s, consulte [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).

Para obter mais informações sobre a visualização de informações registadas pelas ações de script, consulte [clusters do HDInsight de personalizar através da ação de script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)

### <a name="bps8"></a>Guardar ficheiros como ASCII com endings de linha de LF

Scripts de bash devem ser armazenados em formato ASCII, com linhas terminadas por LF. Os ficheiros que são armazenados como UTF-8 ou utilizam CRLF como o fim de linha de Olá poderão falhar com Olá seguinte erro:

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <a name="bps9"></a>Utilizar toorecover de lógica de repetição de erros transitórios

Quando a transferência de ficheiros, instalando pacotes com apt get ou outras ações que transmitem dados através de Olá internet, a ação de Olá poderão falhar devido a erros de rede tootransient. Por exemplo, recurso remoto Olá que estão a comunicar com poderá estar em processo Olá falha de ativação pós-falha de nó tooa de cópia de segurança.

toomake os erros de script de tootransient resiliente, pode implementar a lógica de repetição. Olá seguinte função demonstra como tooimplement repetir lógica. Repetir a operação de Olá três vezes antes de falhar.

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

Olá exemplos seguintes demonstram como toouse esta função.

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <a name="helpermethods"></a>Métodos de programa auxiliar para scripts personalizados

Métodos de programa auxiliar de ação de script são utilitários que pode utilizar ao escrever scripts personalizados. Estes métodos estão contidos no[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script. Utilizar Olá seguir toodownload e utilizá-los como parte do seu script:

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

Olá programas de ajuda disponíveis para utilização no seu script a seguir:

| Utilização de programa auxiliar | Descrição |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |Transfere um ficheiro a partir do caminho do ficheiro especificado toohello Olá origem URI. Por predefinição, este não substituir ficheiro existente. |
| `untar_file TARFILE DESTDIR` |Extrai um ficheiro de tar (utilizando `-xf`) toohello diretório de destino. |
| `test_is_headnode` |Se executou num nó principal do cluster, 1 retorno; caso contrário, 0. |
| `test_is_datanode` |Se o nó atual Olá é um nó de dados (trabalho), devolver um 1; caso contrário, 0. |
| `test_is_first_datanode` |Se o nó atual Olá é os dados de primeiro Olá (trabalho) nó (denominado workernode0) devolver um 1; caso contrário, 0. |
| `get_headnodes` |Devolva o nome de domínio completamente qualificado Olá de Olá headnodes num cluster de Olá. Os nomes são delimitados por vírgulas. Uma cadeia vazia, é devolvida com o erro. |
| `get_primary_headnode` |Obtém o nome de domínio completamente qualificado Olá de headnode primário Olá. Uma cadeia vazia, é devolvida com o erro. |
| `get_secondary_headnode` |Obtém o nome de domínio completamente qualificado Olá de headnode secundário Olá. Uma cadeia vazia, é devolvida com o erro. |
| `get_primary_headnode_number` |Obtém o sufixo numérico Olá headnode primário Olá. Uma cadeia vazia, é devolvida com o erro. |
| `get_secondary_headnode_number` |Obtém o sufixo numérico Olá headnode secundário Olá. Uma cadeia vazia, é devolvida com o erro. |

## <a name="commonusage"></a>Padrões de utilização comuns

Esta secção fornece orientação na implementação de algumas das Olá comuns padrões de utilização que possam ser executadas ao escrever o seu próprio script personalizado.

### <a name="passing-parameters-tooa-script"></a>Os parâmetros a transmitir tooa script

Em alguns casos, o script pode necessitar de parâmetros. Por exemplo, poderá ter palavra-passe de administrador de Olá para cluster Olá quando utilizar Olá API de REST do Ambari.

Os parâmetros transmitidos toohello script são conhecidos como *parâmetros posicionais*e são atribuídos demasiado`$1` para o primeiro parâmetro Olá, `$2` para Olá segundo e, de modo-no. `$0`contém o nome de Olá do script Olá próprio.

Valores transmitidos toohello script como parâmetros devem estar entre símbolos por plicas ('). Se o fizer, assegura que Olá transmitido valor é tratado como um literal.

### <a name="setting-environment-variables"></a>Definir variáveis de ambiente

Definir uma variável de ambiente é realizado Olá a seguinte instrução:

    VARIABLENAME=value

Onde VARIABLENAME é o nome de Olá da variável de Olá. utilização de variáveis, de Olá tooaccess `$VARIABLENAME`. Por exemplo, tooassign um valor fornecido por um parâmetro posicional como uma variável de ambiente com o nome palavra-passe, teria de utilizar Olá a seguinte instrução:

    PASSWORD=$1

Depois, pode utilizar informações de toohello acesso subsequentes `$PASSWORD`.

Variáveis de ambiente definidas dentro do script Olá só existem no âmbito de Olá do script Olá. Em alguns casos, poderá ter de variáveis de ambiente em todo o sistema de tooadd serão mantidas após terminar o script de Olá. as variáveis de ambiente em todo o sistema tooadd, adicione a variável de Olá demasiado`/etc/environment`. Por exemplo, Olá a seguinte instrução adiciona `HADOOP_CONF_DIR`:

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>Toolocations acesso onde estão armazenados os scripts personalizados Olá

Scripts utilizadas toocustomize um cluster precisa toobe armazenado dos Olá seguintes localizações:

* Um __conta de armazenamento do Azure__ que está associado ao cluster Olá.

* Um __conta de armazenamento adicional__ associados ao cluster Olá.

* A __URI legível publicamente__. Por exemplo, um toodata URL armazenado no OneDrive, Dropbox ou outros ficheiros que aloja o serviço.

* Um __conta do Azure Data Lake Store__ que está associado ao cluster do HDInsight Olá. Para obter mais informações sobre como utilizar o Azure Data Lake Store com o HDInsight, consulte [criar um cluster do HDInsight com o Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

    > [!NOTE]
    > Olá serviço principal HDInsight utiliza tooaccess Data Lake Store tem de ter acesso de leitura toohello script.

Recursos utilizados pelo script de Olá também tem de ser publicamente disponíveis.

Armazenamento de ficheiros de Olá numa conta do Storage do Azure ou do Azure Data Lake Store fornece acesso rápido, como ambas no Olá rede do Azure.

> [!NOTE]
> Olá URI formato utilizado tooreference Olá script difere dependendo do serviço de Olá que está a ser utilizado. Para contas de armazenamento associadas ao cluster de HDInsight Olá, utilize `wasb://` ou `wasbs://`. Para os URIs legíveis publicamente, utilize `http://` ou `https://`. Para o Data Lake Store, utilize `adl://`.

### <a name="checking-hello-operating-system-version"></a>A verificar a versão do sistema operativo Olá

Versões diferentes do HDInsight dependem de versões específicas do Ubuntu. Poderão existir diferenças entre versões de SO que tem de verificar no script. Por exemplo, poderá ter tooinstall um binário que é uma versão de Ubuntu toohello associada.

versão de SO de Olá toocheck, utilize `lsb_release`. Por exemplo, Olá seguinte script demonstra como tooreference um tar específica de ficheiros, dependendo da versão do SO de Olá:

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <a name="deployScript"></a>Lista de verificação para implementar uma ação de script

Eis os passos de Olá que pegámos quando preparar toodeploy estes scripts:

* Colocar os ficheiros de Olá que contêm os scripts personalizados do Olá num local que esteja acessível a nós de cluster Olá durante a implementação. Por exemplo, Olá predefinido armazenamento Olá cluster. Ficheiros também podem ser armazenados nos serviços de alojamento legíveis publicamente.
* Certifique-se de que o script de Olá é impotent. Se o fizer, permite Olá script toobe executada várias vezes no Olá mesmo nó.
* Utilize Olá de tookeep um ficheiro temporário diretório /tmp dos ficheiros utilizados pelos scripts de Olá transferidos e, em seguida, limpe-los depois de tem executado scripts.
* Se as definições de nível de SO ou ficheiros de configuração de serviço do Hadoop são alterados, pretende toorestart HDInsight serviços.

## <a name="runScriptAction"></a>Como toorun uma ação de script

Pode utilizar o script ações toocustomize clusters do HDInsight utilizando Olá seguintes métodos:

* Portal do Azure
* Azure PowerShell
* Modelos do Azure Resource Manager
* Olá SDK .NET do HDInsight.

Para obter mais informações sobre como utilizar cada método, consulte [como toouse script ação](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="sampleScripts"></a>Exemplos de script personalizado

A Microsoft fornece scripts de exemplo tooinstall componentes num cluster do HDInsight. Consulte as seguintes ligações para mais ações de script de exemplo de Olá.

* [Instalar e utilizar Hue nos clusters do HDInsight](hdinsight-hadoop-hue-linux.md)
* [Instalar e utilizar Solr nos clusters do HDInsight](hdinsight-hadoop-solr-install-linux.md)
* [Instalar e utilizar Giraph nos clusters do HDInsight](hdinsight-hadoop-giraph-install-linux.md)
* [Instalar ou atualizar Mono nos clusters do HDInsight](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a>Resolução de problemas

Olá, são erros que poderá encontrar ao utilizar scripts que criou:

**Erro**: `$'\r': command not found`. Por vezes, seguido de `syntax error: unexpected end of file`.

*Causa*: Este erro é causado quando terminar de linhas de Olá num script com CRLF. Sistemas UNIX esperam LF apenas como o fim de linha de Olá.

Este problema ocorre frequentemente quando script Olá foi criado no ambiente do Windows, como CRLF é uma linha comuns final para muitos editores de texto no Windows.

*Resolução*: se for uma opção no seu editor de texto, selecione o formato Unix ou LF para o fim de linha de Olá. Também pode utilizar os seguintes comandos no Unix sistema toochange Olá CRLF tooan LF de Olá:

> [!NOTE]
> Olá comandos seguintes são quase equivalentes nessa Olá CRLF linha endings tooLF deve ser alterado. Selecione um com base no utilitários Olá disponíveis no seu sistema.

| Comando | Notas |
| --- | --- |
| `unix2dos -b INFILE` |ficheiro original Olá cópias de segurança com um. Extensão BAK |
| `tr -d '\r' < INFILE > OUTFILE` |OUTFILE contém uma versão com apenas os endings LF |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | Modifica o ficheiro de Olá diretamente |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |OUTFILE contém uma versão com apenas os endings LF. |

**Erro**: `line 1: #!/usr/bin/env: No such file or directory`.

*Causa*: Este erro ocorre quando hello script foi guardado como UTF-8 com uma marca de ordem de bytes (LM).

*Resolução*: guardar o ficheiro de Olá ou como ASCII ou UTF-8 sem um LM. Também pode utilizar os seguintes comandos num toocreate de sistema Linux ou Unix um ficheiro sem Olá LM de Olá:

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

Substitua `INFILE` com o ficheiro de Olá contendo Olá LM. `OUTFILE`deve ser um novo nome de ficheiro, que contém o script de Olá sem Olá LM.

## <a name="seeAlso"></a>Passos seguintes

* Saiba como demasiado[clusters do HDInsight de personalizar através da ação de script](hdinsight-hadoop-customize-cluster-linux.md)
* Olá utilize [referência do SDK .NET do HDInsight](https://msdn.microsoft.com/library/mt271028.aspx) toolearn mais sobre como criar aplicações de .NET que gerem o HDInsight
* Olá utilize [API de REST do HDInsight](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn como clusters toouse REST tooperform as ações de gestão no HDInsight.
