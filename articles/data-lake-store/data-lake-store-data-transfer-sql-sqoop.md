---
title: dados de aaaCopy entre o Data Lake Store e a SQL database do Azure utilizando o Sqoop | Microsoft Docs
description: Utilizar o Sqoop toocopy dados entre SQL Database do Azure e a Data Lake Store
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3f914b2a-83cc-4950-b3f7-69c921851683
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: f58483455f0ebe9544673a1d5c5884f2721c800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a><span data-ttu-id="46355-103">Copiar dados entre o Data Lake Store e a SQL database do Azure utilizando o Sqoop</span><span class="sxs-lookup"><span data-stu-id="46355-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span></span>
<span data-ttu-id="46355-104">Saiba como toouse Apache Sqoop tooimport e exportar dados entre SQL Database do Azure e o Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="46355-104">Learn how toouse Apache Sqoop tooimport and export data between Azure SQL Database and Data Lake Store.</span></span>

## <a name="what-is-sqoop"></a><span data-ttu-id="46355-105">O que é Sqoop?</span><span class="sxs-lookup"><span data-stu-id="46355-105">What is Sqoop?</span></span>
<span data-ttu-id="46355-106">Aplicações de macrodados são uma opção natural para processamento de dados não estruturados e semiestruturados, tais como registos e ficheiros.</span><span class="sxs-lookup"><span data-stu-id="46355-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span></span> <span data-ttu-id="46355-107">No entanto, podem também existir um necessidade tooprocess estruturados os dados armazenados em bases de dados relacionais.</span><span class="sxs-lookup"><span data-stu-id="46355-107">However, there may also be a need tooprocess structured data that is stored in relational databases.</span></span>

<span data-ttu-id="46355-108">[O Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) é uma ferramenta concebida tootransfer dados entre bases de dados relacionais e um repositório de macrodados, tais como o Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="46355-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed tootransfer data between  relational databases and a big data repository, such as Data Lake Store.</span></span> <span data-ttu-id="46355-109">Pode utilizá-lo tooimport dados de um sistema de gestão de base de dados relacional (RDBMS), tais como SQL Database do Azure para o Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="46355-109">You can use it tooimport data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span></span> <span data-ttu-id="46355-110">Pode, em seguida, transformar e analisar dados de Olá utilizando cargas de trabalho de macrodados e, em seguida, exportar dados de Olá num RDBMS.</span><span class="sxs-lookup"><span data-stu-id="46355-110">You can then transform and analyze hello data using big data workloads and then export hello data back into an RDBMS.</span></span> <span data-ttu-id="46355-111">Neste tutorial, utilize uma base de dados do SQL do Azure como a base de dados relacional tooimport/exportação do.</span><span class="sxs-lookup"><span data-stu-id="46355-111">In this tutorial, you use an Azure SQL Database as your relational database tooimport/export from.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46355-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="46355-112">Prerequisites</span></span>
<span data-ttu-id="46355-113">Antes de começar este artigo, tem de ter o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="46355-113">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="46355-114">**Uma subscrição do Azure**.</span><span class="sxs-lookup"><span data-stu-id="46355-114">**An Azure subscription**.</span></span> <span data-ttu-id="46355-115">Consulte [Obter uma avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="46355-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="46355-116">**Uma conta do Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="46355-116">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="46355-117">Para obter instruções sobre como um, ver toocreate [introdução ao Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="46355-117">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="46355-118">**Cluster do HDInsight Azure** com acesso tooa conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="46355-118">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="46355-119">Consulte [criar um cluster do HDInsight com o Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="46355-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="46355-120">Este artigo pressupõe que tem um cluster do HDInsight com Linux com acesso de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="46355-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span></span>
* <span data-ttu-id="46355-121">**Base de Dados SQL do Azure**.</span><span class="sxs-lookup"><span data-stu-id="46355-121">**Azure SQL Database**.</span></span> <span data-ttu-id="46355-122">Para obter instruções sobre como um, ver toocreate [criar uma base de dados SQL do Azure](../sql-database/sql-database-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="46355-122">For instructions on how toocreate one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="46355-123">Aprende depressa com vídeos?</span><span class="sxs-lookup"><span data-stu-id="46355-123">Do you learn fast with videos?</span></span>
<span data-ttu-id="46355-124">[Veja este vídeo](https://mix.office.com/watch/1butcdjxmu114) sobre toocopy dados entre o Blobs Storage do Azure e utilizar o DistCp do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="46355-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="create-sample-tables-in-hello-azure-sql-database"></a><span data-ttu-id="46355-125">Criar tabelas de exemplo no Olá SQL Database do Azure</span><span class="sxs-lookup"><span data-stu-id="46355-125">Create sample tables in hello Azure SQL Database</span></span>
1. <span data-ttu-id="46355-126">toostart com, criar duas tabelas de exemplo Olá SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="46355-126">toostart with, create two sample tables in hello Azure SQL Database.</span></span> <span data-ttu-id="46355-127">Utilize [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) ou Visual Studio tooconnect toohello SQL Database do Azure e, em seguida, execute Olá seguintes consultas.</span><span class="sxs-lookup"><span data-stu-id="46355-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following queries.</span></span>

    <span data-ttu-id="46355-128">**Criar Table1**</span><span class="sxs-lookup"><span data-stu-id="46355-128">**Create Table1**</span></span>

        CREATE TABLE [dbo].[Table1](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO

    <span data-ttu-id="46355-129">**Criar tabela2**</span><span class="sxs-lookup"><span data-stu-id="46355-129">**Create Table2**</span></span>

        CREATE TABLE [dbo].[Table2](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO
2. <span data-ttu-id="46355-130">No **Table1**, adicionar alguns dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="46355-130">In **Table1**, add some sample data.</span></span> <span data-ttu-id="46355-131">Deixe **Table2** vazio.</span><span class="sxs-lookup"><span data-stu-id="46355-131">Leave **Table2** empty.</span></span> <span data-ttu-id="46355-132">Iremos importar dados a partir de **Table1** no Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="46355-132">We will import data from **Table1** into Data Lake Store.</span></span> <span data-ttu-id="46355-133">Em seguida, vamos exportar dados do Data Lake Store para **Table2**.</span><span class="sxs-lookup"><span data-stu-id="46355-133">Then, we will export data from Data Lake Store into **Table2**.</span></span> <span data-ttu-id="46355-134">Execute o seguinte fragmento de Olá.</span><span class="sxs-lookup"><span data-stu-id="46355-134">Run hello following snippet.</span></span>

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a><span data-ttu-id="46355-135">Sqoop de utilização de um cluster do HDInsight com acesso tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="46355-135">Use Sqoop from an HDInsight cluster with access tooData Lake Store</span></span>
<span data-ttu-id="46355-136">Um cluster do HDInsight já tem pacotes de Sqoop Olá disponíveis.</span><span class="sxs-lookup"><span data-stu-id="46355-136">An HDInsight cluster already has hello Sqoop packages available.</span></span> <span data-ttu-id="46355-137">Se tiver configurado Olá HDInsight cluster toouse Data Lake Store como um armazenamento adicional, pode utilizar o Sqoop (sem quaisquer alterações de configuração) tooimport/exportar dados entre uma base de dados relacional (neste exemplo, SQL Database do Azure) e uma Data Lake Store conta.</span><span class="sxs-lookup"><span data-stu-id="46355-137">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) tooimport/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span></span>

1. <span data-ttu-id="46355-138">Para este tutorial, iremos partem do princípio de que criou um cluster do Linux, pelo que deve utilizar o SSH tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="46355-138">For this tutorial, we assume you created a Linux cluster so you should use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="46355-139">Consulte [cluster de HDInsight baseado em Linux do Connect tooa](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="46355-139">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="46355-140">Certifique-se de que o se pode aceder a Olá conta do Data Lake Store do cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="46355-140">Verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="46355-141">Execute Olá seguintes comandos de linha de comandos do Olá SSH:</span><span class="sxs-lookup"><span data-stu-id="46355-141">Run hello following command from hello SSH prompt:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    <span data-ttu-id="46355-142">Isto deve fornecer uma lista de ficheiros/pastas Olá conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="46355-142">This should provide a list of files/folders in hello Data Lake Store account.</span></span>

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a><span data-ttu-id="46355-143">Importar dados do SQL Database do Azure para o Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="46355-143">Import data from Azure SQL Database into Data Lake Store</span></span>
1. <span data-ttu-id="46355-144">Navegue diretório toohello onde Sqoop pacotes estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="46355-144">Navigate toohello directory where Sqoop packages are available.</span></span> <span data-ttu-id="46355-145">Normalmente, esta será em `/usr/hdp/<version>/sqoop/bin`.</span><span class="sxs-lookup"><span data-stu-id="46355-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span></span>
2. <span data-ttu-id="46355-146">Importar os dados Olá **Table1** para Olá conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="46355-146">Import hello data from **Table1** into hello Data Lake Store account.</span></span> <span data-ttu-id="46355-147">Utilize Olá sintaxe:</span><span class="sxs-lookup"><span data-stu-id="46355-147">Use hello following syntax:</span></span>

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    <span data-ttu-id="46355-148">Tenha em atenção que **-base de dados--nome do servidor sql** marcador de posição representa o nome de hello do servidor de olá onde Olá SQL database do Azure está em execução.</span><span class="sxs-lookup"><span data-stu-id="46355-148">Note that **sql-database-server-name** placeholder represents hello name of hello server where hello Azure SQL database is running.</span></span> <span data-ttu-id="46355-149">**nome da base de dados SQL** marcador de posição representa o nome de base de dados real de Olá.</span><span class="sxs-lookup"><span data-stu-id="46355-149">**sql-database-name** placeholder represents hello actual database name.</span></span>

    <span data-ttu-id="46355-150">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="46355-150">For example,</span></span>


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. <span data-ttu-id="46355-151">Certifique-se de que Olá dos dados transferidos toohello conta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="46355-151">Verify that hello data has been transferred toohello Data Lake Store account.</span></span> <span data-ttu-id="46355-152">Execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="46355-152">Run hello following command:</span></span>

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    <span data-ttu-id="46355-153">Deverá ver Olá seguir saída.</span><span class="sxs-lookup"><span data-stu-id="46355-153">You should see hello following output.</span></span>


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    <span data-ttu-id="46355-154">Cada **parte-m -*** ficheiro corresponde tooa linha na tabela de origem Olá, **Table1**.</span><span class="sxs-lookup"><span data-stu-id="46355-154">Each **part-m-*** file corresponds tooa row in hello source table, **Table1**.</span></span> <span data-ttu-id="46355-155">Pode ver conteúdo Olá da peça de Olá - m-* ficheiros tooverify.</span><span class="sxs-lookup"><span data-stu-id="46355-155">You can view hello contents of hello part-m-* files tooverify.</span></span>


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a><span data-ttu-id="46355-156">Exportar dados do Data Lake Store numa SQL Database do Azure</span><span class="sxs-lookup"><span data-stu-id="46355-156">Export data from Data Lake Store into Azure SQL Database</span></span>
1. <span data-ttu-id="46355-157">Exportar dados de Olá do Data Lake Store conta toohello tabela vazia, **Table2**, no Olá SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="46355-157">Export hello data from Data Lake Store account toohello empty table, **Table2**, in hello Azure SQL Database.</span></span> <span data-ttu-id="46355-158">Utilize a sintaxe de Olá.</span><span class="sxs-lookup"><span data-stu-id="46355-158">Use hello following syntax.</span></span>

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    <span data-ttu-id="46355-159">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="46355-159">For example,</span></span>


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. <span data-ttu-id="46355-160">Certifique-se de que Olá dados foram carregadas toohello tabela de base de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="46355-160">Verify that hello data was uploaded toohello SQL Database table.</span></span> <span data-ttu-id="46355-161">Utilize [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) ou Visual Studio tooconnect toohello SQL Database do Azure e, em seguida, execute Olá seguindo a consulta.</span><span class="sxs-lookup"><span data-stu-id="46355-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following query.</span></span>

        SELECT * FROM TABLE2

    <span data-ttu-id="46355-162">Isto deve ter Olá seguinte saída.</span><span class="sxs-lookup"><span data-stu-id="46355-162">This should have hello following output.</span></span>

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a><span data-ttu-id="46355-163">Considerações sobre o desempenho ao utilizar o Sqoop</span><span class="sxs-lookup"><span data-stu-id="46355-163">Performance considerations while using Sqoop</span></span>

<span data-ttu-id="46355-164">Para sua Sqoop de otimização do desempenho da tarefa toocopy dados tooData Lake Store, consulte [documento de desempenho Sqoop](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span><span class="sxs-lookup"><span data-stu-id="46355-164">For performance tuning your Sqoop job toocopy data tooData Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span></span>

## <a name="see-also"></a><span data-ttu-id="46355-165">Consultar também</span><span class="sxs-lookup"><span data-stu-id="46355-165">See also</span></span>
* [<span data-ttu-id="46355-166">Copiar dados de armazenamento de Blobs tooData arquivo Lake do Azure</span><span class="sxs-lookup"><span data-stu-id="46355-166">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="46355-167">Secure data in Data Lake Store (Proteger dados no Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="46355-167">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="46355-168">Utilizar o Azure Data Lake Analytics com o Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="46355-168">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="46355-169">Use Azure HDInsight with Data Lake Store (Utilizar o Azure HDInsight com o Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="46355-169">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
