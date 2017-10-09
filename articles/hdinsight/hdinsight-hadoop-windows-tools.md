---
title: aaaUse um PC Windows com o Hadoop no HDInsight - Azure | Microsoft Docs
description: "Trabalhar a partir de um PC do Windows no Hadoop no HDInsight. Gerir clusters e de consulta com ferramentas do PowerShell, o Visual Studio e Linux. Desenvolva soluções de macrodados com o .NET."
services: hdinsight
keywords: hadoop no windows, o hadoop para o windows
author: cjgronlund
manager: jhubbard
ms.author: cgronlun
ms.date: 05/17/2017
ms.topic: article
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 7c93f16e93349c0b8fb1abd55320c2c172b93aa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="work-in-hello-hadoop-ecosystem-on-hdinsight-from-a-windows-pc"></a>Trabalhar em Olá ecossistema do Hadoop no HDInsight a partir de um PC com Windows

Saiba mais sobre o desenvolvimento e as opções de gestão no Olá Windows PC para trabalhar no ecossistema do Hadoop Olá no HDInsight. 

HDInsight baseia-se no Apache Hadoop e componentes do Hadoop, tecnologias de open source desenvolvidos no Linux. HDInsight versão 3.4 e superior utiliza Olá distribuição Ubuntu Linux como Olá subjacente SO para o cluster de Olá. No entanto, pode trabalhar com o HDInsight partir de um cliente Windows ou o ambiente de desenvolvimento do Windows.

## <a name="use-powershell-for-deployment-and-management-tasks"></a>Utilizar o PowerShell para implementação e gestão de tarefas
O Azure PowerShell é um ambiente de script que pode utilizar toocontrol e automatizar tarefas de implementação e gestão no HDInsight a partir do Windows.

Exemplos de tarefas que pode fazer com o PowerShell:

* [Criar clusters com o PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [Executar consultas do Hive com o PowerShell](hdinsight-hadoop-use-hive-powershell.md)
* [Gerir clusters com o PowerShell](hdinsight-administer-use-powershell.md)

Siga os passos demasiado[instalar e configurar o Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) versão mais recente do tooget Olá. Se tiver scripts que tenham toobe modificado toouse Olá novos cmdlets do Azure Resource Manager, consulte [migrar tooAzure ferramentas de desenvolvimento baseadas no Resource Manager para clusters do HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).

## <a name="utilities-you-can-run-in-a-browser"></a>Utilitários que pode ser executado num browser
Olá seguintes utilitários tem uma IU da web do que é executado num browser:
* **[Shell de nuvem do Azure (pré-visualização)](https://docs.microsoft.com/azure/cloud-shell/quickstart)**  é uma shell interativa e da linha de comandos que é executado no seu browser e Olá, a partir do portal do Azure.
* **[IU da Web do Ambari](hdinsight-hadoop-manage-ambari.md)**  é um gestão e monitorização utilitário disponível no Olá portal do Azure que pode ser utilizados toomanage diferentes tipos de tarefas, tais como:
    * [Utilizar Ambari com Olá REST API](hdinsight-hadoop-manage-ambari-rest-api.md)
    * [Vista Ambari Hive](hdinsight-hadoop-use-hive-ambari-view.md)
    * [Tez vista Ambari](hdinsight-debug-ambari-tez-view.md)

## <a name="data-lake-hadoop-tools-for-visual-studio"></a>N (Hadoop) do Data Lake Tools para Visual Studio
Utilizar as ferramentas do Data Lake para Visual Studio toodeploy e gerir topologias do Storm. Ferramentas do Data Lake também instala Olá SCP.NET SDK, que lhe permite toodevelop topologias de C# com o Visual Studio.

Antes de ir toohello seguir exemplos, [instale e tente ferramentas do Data Lake para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md). 

Exemplos de tarefas que pode fazer com o Visual Studio e as ferramentas do Data Lake para Visual Studio:
* [Implementar e gerir topologias Storm a partir do Visual Studio](hdinsight-storm-deploy-monitor-topology-linux.md)
* [Desenvolver topologias c# para Storm com o Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md). bits de Olá incluem modelos de exemplo para topologias Storm pode ligar toodatabases, tais como a base de dados do Azure Cosmos e a SQL Database.

## <a name="visual-studio-and-hello-net-sdk"></a>Visual Studio e Olá .NET SDK 

Pode utilizar o Visual Studio com clusters de toomanage Olá SDK do .NET e desenvolver aplicações de macrodados. Pode utilizar outros IDEs para Olá seguintes tarefas, mas os exemplos são mostrados no Visual Studio.

Exemplos de tarefas que pode fazer com Olá SDK do .NET no Visual Studio:
* [Criar clusters e trabalhar no HDInsight a partir de uma aplicação do .NET Framework](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* [Executar consultas do Hive com Olá .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md)
* [Utilizar funções definidas pelo utilizador c# com o Hive e do Pig de transmissão em fluxo do Hadoop](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

> Sugestão Se estiver a executar as soluções de .NET com clusters do HDInsight baseados em Windows, é uma boa altura tooplan uma migração baseada em tooLinux clusters. Para obter mais informações, consulte [solução .NET migrar para o HDInsight baseado em Windows HDInsight baseado em tooLinux](hdinsight-hadoop-migrate-dotnet-to-linux.md).

## <a name="intellij-idea-and-eclipse-ide-for-spark-clusters"></a>Intellij IDEA e IDE Eclipse para clusters do Spark
Ambos [Intellij IDEA](https://www.jetbrains.com/idea/download) e Olá [Eclipse IDE](https://www.eclipse.org/downloads/) pode ser utilizado para:
* Desenvolver e submeter uma aplicação do Scala Spark num cluster do HDInsight Spark.
* Aceder a recursos de cluster do Spark.
* Desenvolver e executar uma aplicação do Scala Spark localmente.

Estes artigos mostram como: 
* Intellij IDEA: [aplicações do Spark de criar utilizando Olá Toolkit do Azure para o plug-in Intellij e Olá Scala SDK.](hdinsight-apache-spark-intellij-tool-plugin.md)
* Eclipse IDE ou Scala IDE para o Eclipse: [Olá Toolkit do Azure para o Eclipse e de aplicações do Spark criar](hdinsight-apache-spark-eclipse-tool-plugin.md) 


## <a name="notebooks-on-spark-for-data-scientists"></a>Blocos de notas no Spark cientistas de dados 
Clusters do Apache Spark no HDInsight incluem blocos de notas do Zeppelin e kernels que podem ser utilizados com blocos de notas do Jupyter. 

* [Saiba como toouse kernels no Spark clusters com as aplicações do Spark de tootest de blocos de notas do Jupyter](hdinsight-apache-spark-zeppelin-notebook.md)
* [Saiba como notas do Zeppelin toouse no Spark clusters tarefas de Spark toorun](hdinsight-apache-spark-jupyter-notebook-kernels.md) 


## <a name="run-linux-based-tools-and-technologies-on-windows"></a>Executar ferramentas baseadas em Linux e as tecnologias no Windows

Se encontrar uma situação em que tem de utilizar uma ferramenta ou tecnologia que só está disponível no Linux, considere Olá seguintes opções:

* **Bash (beta) no Windows 10** fornece um subsistema de Linux no Windows. Bash permite-lhe toodirectly executar utilitários de Linux sem ter toomaintain uma instalação de Linux dedicada. [Instalar e executar beta de Bash Olá no Windows 10](https://msdn.microsoft.com/commandline/wsl/install_guide)
* **Docker para Windows** fornece acesso toomany baseado em Linux ferramentas e pode ser executada diretamente a partir do Windows. Por exemplo, pode utilizar o cliente do Docker toorun Olá Beeline para do Hive diretamente a partir do Windows. Pode também utilizar o Docker toorun um bloco de notas do Jupyter local e ligar remotamente tooSpark no HDInsight. [Introdução ao Docker para Windows](https://docs.docker.com/docker-for-windows/)
* **[MobaXTerm](http://mobaxterm.mobatek.net/)**  permite-lhe o sistema de ficheiros do toographically procurar Olá cluster através de uma ligação SSH.

## <a name="next-steps"></a>Passos seguintes
Se a nova tooworking em clusters baseados em Linux, consulte Olá siga artigos:
* [Configurar Hadoop, Kafka, Spark ou outros clusters](hdinsight-hadoop-provision-linux-clusters.md)
* [Sugestões para clusters do HDInsight no Linux](hdinsight-hadoop-linux-information.md)