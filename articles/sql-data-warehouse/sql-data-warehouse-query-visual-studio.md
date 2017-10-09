---
title: "aaaConnect tooAzure do armazém de dados do SQL Server - VSTS | Microsoft Docs"
description: Consultar o SQL Data Warehouse com o Visual Studio.
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a>Ligar tooSQL do armazém de dados com o Visual Studio e SSDT
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Utilize o Visual Studio tooquery Azure SQL Data Warehouse em apenas alguns minutos. Este método utiliza a extensão do SQL Server Data Tools (SSDT) Olá no Visual Studio. 

## <a name="prerequisites"></a>Pré-requisitos
toouse neste tutorial, precisa de:

* Um SQL Data Warehouse existente. toocreate um, consulte [criar um SQL Data Warehouse][Create a SQL Data Warehouse].
* SSDT para Visual Studio. Se tiver o Visual Studio, provavelmente já os tem. Para obter instruções e opções de instalação, veja [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT] (Instalar o Visual Studio e o SSDT).
* Olá nome de servidor SQL completamente qualificado. toofind esta, consulte [ligar tooSQL do armazém de dados][Connect tooSQL Data Warehouse].

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1. Ligar tooyour SQL Data Warehouse
1. Abra o Visual Studio 2013 ou 2015.
2. Abra o SQL Server Object Explorer. toodo este, selecione **vista** > **SQL Server Object Explorer**.
   
    ![SQL Server Object Explorer][1]
3. Clique em Olá **adicionar SQL Server** ícone.
   
    ![Adicionar SQL Server][2]
4. Preencha os campos de Olá na janela de tooServer Olá ligar.
   
    ![Ligar tooServer][3]
   
   * **Nome do servidor**. Introduza Olá **nome do servidor** que identificou anteriormente.
   * **Autenticação**. Selecione **Autenticação do SQL Server** ou **Autenticação Integrada do Active Directory**.
   * **Nome de Utilizador** e **Palavra-passe**. Introduza o nome de utilizador e a palavra-passe, se a Autenticação do SQL Server tiver sido selecionada acima.
   * Clique em **Ligar**.
5. tooexplore, expanda o servidor de SQL do Azure. Pode ver as bases de dados de Olá associadas ao servidor de Olá. Expanda AdventureWorksDW tabelas de Olá toosee na sua base de dados de exemplo.
   
    ![Explorar AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a>2. Executar uma consulta de exemplo
Agora que uma ligação foi estabelecida tooyour base de dados, vamos escrever uma consulta.

1. Clique com o botão direito do rato na base de dados no SQL Server Object Explorer.
2. Selecione **Nova Consulta**. É aberta uma nova janela de consulta.
   
    ![Nova consulta][5]
3. Copie esta consulta TSQL para a janela de consulta Olá:
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Execute consulta Olá. toodo, clique seta de Olá verde ou utilize Olá seguir atalho: `CTRL` + `SHIFT` + `E`.
   
    ![Executar consulta][6]
5. Observe os resultados da consulta Olá. Neste exemplo, a tabela do Olá FactInternetSales tem 60398 linhas.
   
    ![Resultados da consulta][7]

## <a name="next-steps"></a>Passos seguintes
Agora que pode ligar e consultar, experimente [visualizar Olá dados com o PowerBI][visualizing hello data with PowerBI].

tooconfigure o ambiente para a autenticação do Azure Active Directory, consulte [autenticar tooSQL do armazém de dados][Authenticate tooSQL Data Warehouse].

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
