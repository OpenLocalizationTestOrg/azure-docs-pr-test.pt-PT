---
title: aaaUse Apache Storm com o Power BI - Azure HDInsight | Microsoft Docs
description: "Crie um relatório do Power BI com dados de uma topologia de c# em execução num cluster do Apache Storm no HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a>Utilizar dados de toovisualize do Power BI a partir de uma topologia do Apache Storm

Power BI permite-lhe toovisually apresenta dados como relatórios. Este documento fornece um exemplo de como toouse Apache Storm no HDInsight toogenerate dados para o Power BI.

> [!NOTE]
> Olá passos neste documento dependem de um ambiente de desenvolvimento do Windows com o Visual Studio. projeto compilado Olá pode ser o cluster de HDInsight baseado em Linux tooa submetido. Apenas clusters baseados em Linux criados após 10/28/2016 suporte SCP.NET topologias.
>
> toouse uma topologia de c# com um cluster baseado em Linux, atualização Olá pacote Microsoft.SCP.Net.SDK NuGet utilizado pelo seu tooversion projeto 0.10.0.6 ou superior. versão de Olá do pacote de Olá também tem de corresponder à versão principal do Olá do Storm instalado no HDInsight. Por exemplo, o Storm nas versões 3.3 e 3.4 do HDInsight utilizam a versão 0.10.x do Storm, enquanto o HDInsight 3.5 utiliza o Storm 1.0.x.
>
> Topologias de c# em clusters baseados em Linux tem de utilizar o .NET 4.5 e utilizar Mono toorun num cluster do HDInsight Olá. A maioria dos aspetos funcionam. No entanto, deve verificar Olá [Mono compatibilidade](http://www.mono-project.com/docs/about-mono/compatibility/) documento para incompatibilidades potenciais.
>
> Para uma versão de Java deste projeto, que funciona com o HDInsight baseado em Windows ou baseado em Linux, consulte [processar eventos provenientes dos Hubs de eventos do Azure com o Storm no HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="prerequisites"></a>Pré-requisitos

* Um utilizador do Azure Active Directory com [Power BI](https://powerbi.com) acesso.
* Um cluster do HDInsight. Para obter mais informações, consulte [introdução ao Storm no HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

  > [!IMPORTANT]
  > Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior. Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).

* Visual Studio (uma das seguintes versões de Olá)

  * Visual Studio 2012 com [atualização 4](http://www.microsoft.com/download/details.aspx?id=39305)
  * Visual Studio 2013 com [atualização 4](http://www.microsoft.com/download/details.aspx?id=44921) ou [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * Visual Studio 2017 (qualquer edição)

* Olá ferramentas do HDInsight para Visual Studio: consulte [começar a utilizar as ferramentas do HDInsight Olá para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) para obter informações sobre as informações da instalação.

## <a name="how-it-works"></a>Como funciona

Este exemplo contém uma topologia de C# que aleatoriamente gera dados de registo de serviços de informação Internet (IIS). Estes dados, em seguida, são escritos tooa base de dados SQL e a partir daí é toogenerate utilizados relatórios no Power BI.

Olá ficheiros implementar Olá funcionalidade principal deste exemplo a seguir:

* **SqlAzureBolt.cs**: escreve informações produzidas Olá Storm topologia tooSQL da base de dados.
* **IISLogsTable.sql**: Olá Transact-SQL instruções utilizadas toogenerate Olá base de dados que Olá dados são armazenados no.

> [!WARNING]
> Crie tabela Olá na base de dados do SQL Server antes de iniciar a topologia de Olá no cluster do HDInsight.

## <a name="download-hello-example"></a>Transferir o exemplo de Olá

Transferir Olá [exemplo HDInsight c# Storm Power BI](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi). toodownload, quer bifurcação/clone-o utilizando [git](http://git-scm.com/), ou utilize Olá **transferir** toodownload ligação um. zip do arquivo de Olá.

## <a name="create-a-database"></a>Criar uma base de dados

1. toocreate uma base de dados, utilize os passos de Olá Olá [tutorial de base de dados SQL](../sql-database/sql-database-get-started.md) documento.

2. Base de dados do Connect toohello pela seguinte Olá os passos em Olá [ligar tooa base de dados SQL com o Visual Studio](../sql-database/sql-database-connect-query.md) documento.

3. No Object Explorer, base de dados de Olá com o botão direito e selecione **nova consulta**. Cole conteúdo Olá Olá **IISLogsTable.sql** ficheiros incluídos no Olá transferidas projeto na janela de consulta Olá e, em seguida, utilize Ctrl + Shift + consulta de Olá I tooexecute. Deverá receber uma mensagem que Olá comandos foi concluídos com êxito.

## <a name="configure-hello-sample"></a>Configurar o exemplo de Olá

1. De Olá [portal do Azure](https://portal.azure.com), selecione a base de dados do SQL Server. De Olá **Essentials** secção Olá SQL painel base de dados, selecione **Mostrar cadeias de ligação de base de dados**. Na lista de Olá que aparece, copie Olá **ADO.NET (autenticação do SQL Server)** informações.

2. Exemplo de Olá abrir no Visual Studio. De **Explorador de soluções**, abra Olá **App. config** de ficheiros e, em seguida, localize Olá seguir entrada:

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    Substitua Olá **# # TOBEFILLED # #** valor com a cadeia de ligação de base de dados de Olá copiou no passo anterior Olá. Substitua **{sua\_username}** e **{sua\_palavra-passe}** com Olá nome de utilizador e palavra-passe para a base de dados de Olá.

3. Guarde e feche ficheiros Olá.

## <a name="deploy-hello-sample"></a>Implementar o exemplo de Olá

1. De **Explorador de soluções**, contexto Olá **StormToSQL** projeto e selecione **submeter tooStorm no HDInsight**. Cluster do HDInsight Olá selecione de Olá **Cluster do Storm** caixa de diálogo de lista pendente.

   > [!NOTE]
   > Poderá demorar alguns segundos para Olá **Cluster do Storm** toopopulate pendente com nomes de servidor.
   >
   > Se lhe for solicitado, introduza as credenciais de início de sessão Olá para a sua subscrição do Azure. Se tiver mais do que uma subscrição, inicie sessão toohello que contenha o seu cluster Storm no HDInsight.

2. Quando foi submetida topologia Olá, Olá __Visualizador de topologia__ aparece. tooview esta topologia, a entrada de SqlAzureWriterTopology Olá selecione na lista de Olá.

    ![topologias de Olá, com topologia Olá selecionado](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    Pode utilizar estas informações de toosee vista na topologia de Olá ou faça duplo clique num componente do entrada (por exemplo, Olá SqlAzureBolt) toosee informações tooa específico numa topologia de Olá.

3. Depois de Olá topologia tem foi executada para alguns minutos, janela de consulta SQL de retorno toohello utilizou toocreate Olá da base de dados. Substitua as instruções existente Olá Olá seguinte consulta:

        select * from iislogs;

    Utilize Ctrl + Shift + consulta de Olá I tooexecute e deverá receber resultados toohello semelhante, os seguintes dados:

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    Estes dados tem sido escritos da topologia do Storm Olá.

## <a name="create-a-report"></a>Criar um relatório

1. Ligar toohello [conector da SQL Database do Azure](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) para o Power BI. 

2. Dentro do **bases de dados**, selecione **obter**.

3. Selecione **SQL Database do Azure**e, em seguida, selecione **Connect**.

    > [!NOTE]
    > Poderá ser pedido toodownload Olá Power BI Desktop toocontinue. Se assim for, utilize Olá tooconnect passos a seguir:
    >
    > 1. Abra o ambiente de trabalho do Power BI e selecione __obter dados__.
    > 2 selecione __Azure__e, em seguida, __SQL database do Azure__.

4. Introduza Olá informações tooconnect tooyour SQL Database do Azure. Pode encontrar estas informações visitando Olá [portal do Azure](https://portal.azure.com) e selecionando a base de dados do SQL Server.

   > [!NOTE]
   > Também pode definir o intervalo de atualização de Olá e filtros personalizados utilizando **ativar opções avançadas** de Olá ligar a caixa de diálogo.

5. Depois de se ligar, verá um novo conjunto de dados com Olá que mesmo nome como base de dados de Olá à. Selecione toobegin de conjunto de dados de Olá conceber um relatório.

6. De **campos**, expanda Olá **IISLOGS** entrada. toocreate um relatório que apresenta uma lista de Olá URI stems, selecionar Olá caixa de verificação **URISTEM**.

    ![Criar um relatório](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. Em seguida, arraste **método** toohello relatório. Olá de toolist de atualizações de relatório Olá stems e método HTTP correspondente Olá utilizada para Olá pedido de HTTP.

    ![adicionar dados de método Olá](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. De Olá **visualizações** coluna, selecione de Olá **campos** ícone e, em seguida, selecione Olá seta para baixo junto demasiado**método** no Olá **valores**secção. Selecione toodisplay tiverem sido acedida uma contagem de quantas vezes um URI, **contagem**.

    ![Contagem de tooa dos métodos de alteração](./media/hdinsight-storm-power-bi-topology/count.png)

9. Em seguida, selecione Olá **gráfico de colunas Stacked** toochange como Olá informações a apresentar.

    ![A alteração gráficos empilhados de tooa](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. relatório de Olá toosave, selecione **guardar** e introduza um nome para o relatório de Olá.

## <a name="stop-hello-topology"></a>Parar a topologia de Olá

topologia de Olá continua toorun até pará-la ou eliminar Olá Storm num cluster do HDInsight. toostop Olá topologia, execute Olá os seguintes passos:

1. No Visual Studio, devolver o Visualizador de topologia toohello e selecione a topologia de Olá.

2. Selecione Olá **Kill** topologia do botão toostop Olá.

    ![Kill botão na topologia de Olá resumo](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Elimina o cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Passos seguintes

Neste documento, aprendeu como toosend dados a partir de um tooSQL de topologia do Storm base de dados, em seguida, visualize os dados de Olá através do Power BI. Para obter informações sobre como toowork com outras tecnologias do Azure a utilizar o Storm no HDInsight, consulte Olá seguintes documentos:

* [Topologias de exemplo para Storm no HDInsight](hdinsight-storm-example-topology.md)
