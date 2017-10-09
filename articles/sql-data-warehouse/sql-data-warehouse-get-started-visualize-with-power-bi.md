---
title: aaaVisualize dados do SQL Data Warehouse com o Power BI Microsoft Azure
description: Visualizar dados do SQL Data Warehouse com o Power BI
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: d7fb89d1-da1d-4788-a111-68d0e3fda799
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 0425cf5abe7bc001b2a41df4d09bf5f2e42527e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-data-with-power-bi"></a>Visualizar dados com o Power BI
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Este tutorial mostra como toouse Power BI tooconnect tooSQL do armazém de dados e criar algumas visualizações básicas.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
toostep com este tutorial, precisa de:

* Um SQL Data Warehouse pré-carregado com a base de dados do Olá AdventureWorksDW. tooprovision esta, consulte [criar um SQL Data Warehouse] [ Create a SQL Data Warehouse] e escolha os dados de exemplo de Olá tooload. Se já tiver um armazém de dados, mas não tiver dados de exemplo, pode [carregar dados de exemplo manualmente][load sample data manually].

## <a name="1-connect-tooyour-database"></a>1. Ligar a base de dados tooyour
tooopen Power BI e ligar a base de dados do tooyour AdventureWorksDW:

1. Inicie sessão em Olá [portal do Azure][Azure portal].
2. Clique em **Bases de dados SQL** e selecione a sua base de dados AdventureWorks do SQL Data Warehouse.
   
    ![Localizar a base de dados][1]
3. Clique no botão 'Abrir no Power BI' de Olá.
   
    ![Botão do Power BI][2]
4. Agora, deverá ver a página de ligação de armazém de dados do SQL Server Olá apresentar o seu endereço de web de base de dados. Clique em seguinte.
   
    ![Ligação ao Power BI][3]
5. Introduza o nome de utilizador do Azure SQL server e a palavra-passe e será a base de dados do SQL Data Warehouse tooyour completamente ligado.
   
    ![Início de sessão no Power BI][4]
6. Assim que o se se inscreveu no Power BI, clique em conjunto de dados no painel esquerdo Olá Olá AdventureWorksDW. Esta ação irá abrir a base de dados de Olá.
   
    ![No Power BI, abrir AdventureWorksDW][5]

## <a name="2-create-a-report"></a>2. Criar um relatório
Está agora prontos toouse Power BI tooanalyze os dados de exemplo AdventureWorksDW. análise de Olá tooperform, a AdventureWorksDW tem uma vista denominada AggregateSales. Esta vista contém algumas das métricas principais de Olá para analisar as vendas Olá da empresa Olá.

1. toocreate um mapa do montante de vendas em conformidade com o código de toopostal, no painel direito de campos de Olá, clique em Olá tooexpand de vista AggregateSales-lo. Clique em Olá PostalCode e SalesAmount colunas tooselect-los.
   
    ![No Power BI, selecionar AggregateSales][6]
   
    O Power BI reconhece automaticamente estes dados geográficos e coloca-os num mapa para si.
   
    ![Mapa do Power BI][7]
2. Este passo cria um gráfico de barras que mostra a quantidade de vendas por receitas de cliente. toocreate este toohello aceda expandido vista AggregateSales. Clique no campo SalesAmount Olá. Arraste Olá receitas de cliente campo toohello esquerda e solte-o no eixo.
   
    ![No Power BI, selecionar eixo][8]
   
    Iremos movidos gráfico de barras Olá através de Olá esquerda.
   
    ![Barra do Power BI][9]
3. Este passo cria um gráfico de linhas que mostra o montante de vendas por data de encomenda. toocreate este toohello aceda expandido vista AggregateSales. Clique em SalesAmount e OrderDate. Na coluna visualizações de Olá clique ícone de gráfico de linhas de Olá; Este é o primeiro ícone de Olá na segunda linha de Olá em visualizações.
   
    ![No Power BI, selecionar gráfico de linhas][10]
   
    Tem agora um relatório que mostra as três visualizações diferentes dos dados de Olá.
   
    ![Linha do Power BI][11]

Pode guardar o seu progresso em qualquer altura, clicando em **Ficheiro** e selecionando **Guardar**.

## <a name="next-steps"></a>Passos seguintes
Agora que iremos toowarm algum tempo cópias de segurança com dados de exemplo de Olá, consulte como demasiado[desenvolver][develop], [carregar][load], ou [ migrar][migrate]. Ou observe Olá [Web site do Power BI][Power BI website].

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-find-database.png
[2]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-button.png
[3]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-connect-to-azure.png
[4]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-sign-in.png
[5]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-open-adventureworks.png
[6]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-aggregatesales.png
[7]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-map.png
[8]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-chooseaxis.png
[9]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-bar.png
[10]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-prepare-line.png
[11]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-line.png
[12]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-save.png

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[connecting tooSQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
