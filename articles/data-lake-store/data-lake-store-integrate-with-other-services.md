---
title: "aaaIntegrating Data Lake Store com outros serviços do Azure | Microsoft Docs"
description: "Compreender a forma como a Data Lake Store integra-se com outros serviços do Azure"
documentationcenter: 
services: data-lake-store
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 48a5d1f4-3850-4c22-bbc4-6d1d394fba8a
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 839689f04623f8225884e7aa9c0b533a09323e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-data-lake-store-with-other-azure-services"></a>Integrating Data Lake Store with other Azure Services (Integrar o Data Lake Store noutros Serviços do Azure)
O Azure Data Lake Store pode ser utilizado em conjunto com outro serviços do Azure de tooenable uma vasta gama de cenários. Olá seguinte artigo apresenta uma lista de serviços de Olá Data Lake Store pode ser integrado.

## <a name="use-data-lake-store-with-azure-hdinsight"></a>Utilizar o Data Lake Store com o Azure HDInsight
Pode aprovisionar um [Azure HDInsight](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/) cluster que utiliza o Data Lake Store como armazenamento Olá compatível com HDFS. Nesta versão, para clusters do Hadoop e Storm no Windows e Linux, pode utilizar Data Lake Store apenas como um armazenamento adicional. Esses clusters continuar a utilizar armazenamento do Azure (WASB) como armazenamento de predefinido Olá. No entanto, para os clusters de HBase no Windows e Linux, pode utilizar Data Lake Store que o armazenamento de predefinido Olá, armazenamento adicional ou ambos.

Para obter instruções sobre como tooprovision um HDInsight cluster com o Data Lake Store, consulte:

* [Aprovisionar um cluster do HDInsight com o Data Lake Store utilizando o Portal do Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Aprovisionar um cluster do HDInsight com o Data Lake Store, como armazenamento de predefinido com o Azure PowerShell](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [Aprovisionar um cluster do HDInsight com o Data Lake Store, como armazenamento adicional com o Azure PowerShell](data-lake-store-hdinsight-hadoop-use-powershell.md)

## <a name="use-data-lake-store-with-azure-data-lake-analytics"></a>Utilizar o Data Lake Store do Azure Data Lake Analytics
[Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-overview.md) permite-lhe toowork com macrodados na escala da nuvem. Dinamicamente Aprovisiona recursos e permite-lhe fazer análises sobre terabytes ou até mesmo exabytes de dados que podem ser armazenados num número de origens de dados suportadas, um dos atributos que está a ser Data Lake Store. O Data Lake Analytics está otimizada especialmente toowork com o Azure Data Lake Store, fornecendo o nível mais elevado de Olá de desempenho, débito e paralelização para as suas cargas de trabalho de macrodados.

Para obter instruções sobre como toouse Data Lake Analytics com o Data Lake Store, consulte [introdução ao Data Lake Analytics com o Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md).

## <a name="use-data-lake-store-with-azure-data-factory"></a>Utilizar o Data Lake Store com o Azure Data Factory
Pode utilizar [do Azure Data Factory](https://azure.microsoft.com/services/data-factory/) tooingest dados de tabelas do Azure, SQL Database do Azure, o armazém de dados do Azure SQL, Blobs Storage do Azure e bases de dados no local. Uma primeira classe citizen no Olá ecossistema do Azure, Azure Data Factory pode ser utilizado tooorchestrate Olá ingestão de dados a partir destes tooAzure origem Data Lake Store.

Para obter instruções sobre como toouse do Azure Data Factory com o Data Lake Store, consulte o artigo [mover tooand de dados do Data Lake Store utilizando o Data Factory](../data-factory/data-factory-azure-datalake-connector.md).

## <a name="copy-data-from-azure-storage-blobs-into-data-lake-store"></a>Copiar dados de Blobs de armazenamento do Azure para o Data Lake Store
O Azure Data Lake Store fornece uma ferramenta da linha de comandos, AdlCopy, que lhe permite toocopy dados do Blob Storage do Azure para uma conta do Data Lake Store. Para obter mais informações, consulte [copiar dados de armazenamento de Blobs tooData arquivo Lake do Azure](data-lake-store-copy-data-azure-storage-blob.md).

## <a name="copy-data-between-azure-sql-database-and-data-lake-store"></a>Copiar dados entre SQL Database do Azure e a Data Lake Store
Pode utilizar o Apache Sqoop tooimport e exportar dados entre SQL Database do Azure e o Data Lake Store. Para obter mais informações, consulte [copiar dados entre o Data Lake Store e a SQL database do Azure utilizando o Sqoop](data-lake-store-data-transfer-sql-sqoop.md).

## <a name="use-data-lake-store-with-stream-analytics"></a>Utilizar o Data Lake Store Stream Analytics
Pode utilizar o Data Lake Store como um dos Olá produz dados toostore transmissão em fluxo utilizando o Azure Stream Analytics. Para obter mais informações, consulte [transmitir dados de Blob de armazenamento do Azure para o Data Lake Store utilizando o Azure Stream Analytics](data-lake-store-stream-analytics.md).

## <a name="use-data-lake-store-with-power-bi"></a>Utilizar o Data Lake Store com o Power BI
Pode utilizar os dados do Power BI tooimport a partir de um tooanalyze de conta do Data Lake Store e visualizar dados Olá. Para obter mais informações, consulte [analisar os dados no Data Lake Store através do Power BI](data-lake-store-power-bi.md).

## <a name="use-data-lake-store-with-data-catalog"></a>Utilizar o Data Lake Store com o catálogo de dados
Pode registar os dados do Data Lake Store para Olá Azure dados toomake Olá dados do catálogo Detetáveis em toda a organização Olá. Para obter mais informações consulte [registar dados do Data Lake Store no catálogo de dados do Azure](data-lake-store-with-data-catalog.md).

## <a name="use-data-lake-store-with-sql-server-integration-services-ssis"></a>Utilizar o Data Lake Store com o SQL Server Integration Services (SSIS)
Pode utilizar o Gestor de ligações do Azure Data Lake Store Olá SSIS tooconnect um pacote SSIS com o Azure Data Lake Store. Para obter mais informações, consulte [utilize Data Lake Store com SSIS](https://docs.microsoft.com/sql/integration-services/connection-manager/azure-data-lake-store-connection-manager).

## <a name="use-data-lake-store-with-sql-data-warehouse"></a>Utilizar o Data Lake Store com o SQL Data Warehouse
Pode utilizar dados de tooload PolyBase de Azure Data Lake Store para o SQL Data Warehouse. Para obter mais informações consulte [utilize Data Lake Store com o SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-load-from-azure-data-lake-store.md).

## <a name="see-also"></a>Consultar também
* [Descrição geral do Azure Data Lake Store](data-lake-store-overview.md)
* [Introdução ao Data Lake Store através do Portal](data-lake-store-get-started-portal.md)
* [Introdução ao Data Lake Store através do PowerShell](data-lake-store-get-started-powershell.md)  

