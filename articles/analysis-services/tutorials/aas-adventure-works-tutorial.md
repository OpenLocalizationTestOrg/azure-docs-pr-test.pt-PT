---
title: Tutorial do Azure Analysis Services da Adventure Works | Microsoft Docs
description: "Introdução ao tutorial da Adventure Works para o Azure Analysis Services"
services: analysis-services
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 01/08/2018
ms.author: owend
ms.openlocfilehash: 9b81e011d3e1ed23465bbd554a0c7376b432b585
ms.sourcegitcommit: 176c575aea7602682afd6214880aad0be6167c52
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/09/2018
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a>Azure Analysis Services- tutorial da Adventure Works

Este tutorial fornece lições sobre como criar e implementar um modelo de tabela no nível de compatibilidade 1400, ao utilizar o Visual Studio com o [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  

Se não estiver familiarizado com o Analysis Services e a modelagem de tabela, conclua este tutorial da forma mais rápida que lhe permita criar e implementar um modelo de tabela básico com o Visual Studio. Quando tiver definido os pré-requisitos, deve demorar entre duas a três horas para concluir.  
  
## <a name="what-you-learn"></a>O que irá aprender   
  
-   Como criar um novo projeto de modelo de tabela no **nível de compatibilidade 1400** no Visual Studio com SSDT.
  
-   Como importar dados de uma base de dados relacional para uma base de dados de área de trabalho de projeto de modelo de tabela.  
  
-   Como criar e gerir relações entre tabelas no modelo.  
  
-   Como criar colunas calculadas, medidas e indicadores-chave de desempenho que ajudam os utilizadores a analisar métricas comerciais críticas.  
  
-   Como criar e gerir perspectivas e hierarquias que ajudam os utilizadores a procurar mais facilmente os dados de modelo, fornecendo pontos de vista específicos das aplicações e dos negócios.  
  
-   Como criar partições que dividem dados de tabela em partes lógicas menores que podem ser processadas independentemente de outras partições.  
  
-   Como proteger dados e objetos de modelo, criando funções com membros de utilizador.  
  
-   Como implantar um modelo de tabela para um servidor **Azure Analysis Services** ou um servidor SQL Server 2017 Analysis Services local.  
  
## <a name="prerequisites"></a>Pré-requisitos  
Para concluir este tutorial, precisa de:  
  
-   Um servidor do Azure Analysis Services. Inscreva-se para uma [avaliação gratuita do Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) e [crie um servidor](../analysis-services-create-server.md). 

-   Um [Azure SQL Data Warehouse](../../sql-data-warehouse/create-data-warehouse-portal.md) com a **base de dados de exemplo AdventureWorksDW** ou um SQL Server Data Warehouse com a [base de dados de exemplo Adventure Works](http://go.microsoft.com/fwlink/?LinkID=335807).

    **Importante:** Se tiver instalado a base de dados de exemplo num SQL Server Data Warehouse no local e se estiver a implementar o seu modelo num servidor Azure Analysis Services, é necessário um [gateway de dados no local](../analysis-services-gateway.md).

-   A versão mais recente do [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx) para o Visual Studio.

-   Está instalada a versão mais recente do [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).    

-   Uma aplicação de cliente como [Power BI Desktop](https://powerbi.microsoft.com/desktop/) ou Excel. 

## <a name="scenario"></a>Cenário  
Este tutorial baseia-se em Adventure Works Cycles, uma empresa fictícia. A Adventure Works é uma grande empresa multinacional de fabrico que produz e distribui bicicletas, peças e acessórios para mercados comerciais na América do Norte, Europa e Ásia. A empresa emprega 500 funcionários. Além disso, a Adventure Works emprega várias equipas regionais de vendas em toda a sua base de mercado. O projeto é criar um modelo de tabela para que os utilizadores de vendas e marketing analisem os dados de vendas pela Internet na base de dados AdventureWorksDW.  
  
Para concluir o tutorial, deve concluir várias lições. Em cada lição, há tarefas. A conclusão de cada tarefa por ordem é necessária para concluir a lição. Numa lição específica podem existir várias tarefas que geram um resultado semelhante, mas a forma como conclui cada tarefa é ligeiramente diferente. Este método mostra que existe mais de uma forma para concluir uma tarefa e desafiamo-lo a usar as capacidades que assimilou nas lições e tarefas anteriores.  
  
A finalidade das lições é orientá-lo durante a criação de um modelo de tabela básico, utilizando muitas das funcionalidades incluídas no SSDT. Uma vez que cada lição é criada com base lição anterior, deverá concluir as lições por ordem.
  
Este tutorial não fornece lições sobre como gerir um servidor no portal do Azure, gerir um servidor ou base de dados, utilizar o SSMS ou utilizar uma aplicação de cliente para procurar dados de modelo. 


## <a name="lessons"></a>Lições  
Este tutorial inclui as seguintes lições:  
  
|Lição|Tempo estimado para concluir|  
|----------|------------------------------|  
|[1 - Criar um novo projeto de modelo em tabela](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)|10 minutos|  
|[2 - Obter dados](../tutorials/aas-lesson-2-get-data.md)|10 minutos|  
|[3 - Marcar como Tabela de Datas](../tutorials/aas-lesson-3-mark-as-date-table.md)|3 minutos|  
|[4 - Criar relações](../tutorials/aas-lesson-4-create-relationships.md)|10 minutos|  
|[5 - Criar colunas calculadas](../tutorials/aas-lesson-5-create-calculated-columns.md)|15 minutos|
|[6 - Criar medidas](../tutorials/aas-lesson-6-create-measures.md)|30 minutos|  
|[7 - Criar Indicadores Chave de Desempenho (KPI)](../tutorials/aas-lesson-7-create-key-performance-indicators.md)|15 minutos|  
|[8 - Criar perspetivas](../tutorials/aas-lesson-8-create-perspectives.md)|5 minutos|  
|[9 - Criar hierarquias](../tutorials/aas-lesson-9-create-hierarchies.md)|20 minutos|  
|[10 - Criar partições](../tutorials/aas-lesson-10-create-partitions.md)|15 minutos|  
|[11 - Criar funções](../tutorials/aas-lesson-11-create-roles.md)|15 minutos|  
|[12 - Analisar no Excel](../tutorials/aas-lesson-12-analyze-in-excel.md)|5 minutos| 
|[13 - Implementar](../tutorials/aas-lesson-13-deploy.md)|5 minutos|  
  
## <a name="supplemental-lessons"></a>Lições suplementares  
Estas lições não são necessárias para concluir o tutorial, mas podem ser úteis para compreender melhor a criação de modelos de tabelas avançados.  
  
|Lição|Tempo estimado para concluir|  
|----------|------------------------------|  
|[Linhas detalhadas](../tutorials/aas-supplemental-lesson-detail-rows.md)|10 minutos|
|[Segurança dinâmica](../tutorials/aas-supplemental-lesson-dynamic-security.md)|30 minutos|
|[Hierarquias desbalanceadas](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|20 minutos| 

  
## <a name="next-steps"></a>Passos seguintes  
Para começar, consulte [Lição 1: Criar um novo projeto de modelo de tabela](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
  
  

