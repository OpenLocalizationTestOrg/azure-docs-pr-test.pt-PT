---
title: problemas de desempenho de aaaTroubleshoot e otimizar a base de dados | Microsoft Docs
description: "Aplicar as recomendações de desempenho tooyour base de dados SQL, bem como lear como toogain informações sobre Olá desempenho das consultas de Olá em execução na sua base de dados"
metakeywords: azure sql database performance monitoring recommendation
services: sql-database
documentationcenter: 
manager: jhubbard
author: jan-eng
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,monitor & tune
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: janeng
ms.openlocfilehash: e948d30ac74eecf45420d5d77ef55e3c0b6f3f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a>Resolver problemas de desempenho e otimizar a base de dados

Os índices em falta e as consultas mal otimizadas são razões comuns para um desempenho fraco da base de dados. Neste tutorial que aprende a:
> [!div class="checklist"]
> * Reveja, aplicam-se e reverter as recomendações de melhoramento de desempenho
> * Localizar consultas com uma utilização intensiva de recursos
> * Localizar consultas de execução longa

> Precisa de uma carga de trabalho contínua na base de dados com problemas de desempenho – falta um índice, por exemplo tooreceive uma recomendação.
>

## <a name="log-in-toohello-azure-portal"></a>Início de sessão toohello portal do Azure

Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).

## <a name="review-and-apply-a-recommendation"></a>Rever e aplicar uma recomendação

Siga estes passos tooapply uma recomendação do sistema de Olá da base de dados:

1. Clique em Olá **recomendações de desempenho** menu no painel da base de dados de Olá.

    ![recomendação de desempenho](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. Na lista de Olá recomendações, selecione uma recomendação de Active Directory. Neste exemplo, criar índice.

    ![Selecione a recomendação](./media/sql-database-performance-tutorial/create_index.png)

3. Aplicar a recomendação de Olá clicando Olá **aplicar** botão. Opcionalmente, reveja os detalhes de recomendação Olá e ver script Olá T-SQL demasiado ser executado ao clicar no **ver Script** botão.

    ![aplicar a recomendação](./media/sql-database-performance-tutorial/apply.png)

4. [Opcional] Ative a otimização automática para toobe recomendações aplicada automaticamente.

    ![auto Otimização](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a>Reverter uma recomendação

Olá Database Advisor monitoriza cada recomendação implementada. Se uma recomendação não melhorar a carga de trabalho Olá, serão automaticamente revertido. Reverter manualmente uma recomendação é possíveis, mas não necessariamente na maioria dos casos. toorevert uma recomendação:

1. Visite o menu de recomendações de desempenho toohello e selecione uma das recomendações de Olá aplicada.

    ![Selecione a recomendação](./media/sql-database-performance-tutorial/select.png)

2. Na vista de detalhes de Olá, clique em **reverter**.

    ![reverter recomendação](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a>Localizar a consulta de Olá que consome Olá maioria dos recursos

Siga estas consultas de Olá passos toofind Olá a consumir mais recursos:

1. Clique em Olá **Query Performance Insight** menu no painel da base de dados de Olá.

    ![informações acerca das consultas](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. Selecione um tipo de recurso.

    ![informações acerca das consultas](./media/sql-database-performance-tutorial/select_resource_type.png)

3. Selecione Olá primeira consulta numa tabela Olá.

    ![informações acerca das consultas](./media/sql-database-performance-tutorial/select_query.png)

4. Reveja os detalhes de consulta Olá.

    ![informações acerca das consultas](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a>Encontrar Olá mais longo, consulta em execução

1. Aceda tooQuery Performance Insight e selecione Olá **consultas de execução longa** separador.

    ![informações acerca das consultas](./media/sql-database-performance-tutorial/long_running.png)

3. Selecione Olá primeira consulta numa tabela Olá.

    ![informações acerca das consultas](./media/sql-database-performance-tutorial/select_first_query.png)

4. Reveja os detalhes de consulta Olá.

    ![informações acerca das consultas](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a>Passos seguintes 
Os índices em falta e as consultas mal otimizadas são razões comuns para um desempenho fraco da base de dados. Neste tutorial, que aprendeu a:
> [!div class="checklist"]
> * Reveja, aplicam-se e reverter as recomendações de melhoramento de desempenho
> * Localizar consultas com uma utilização intensiva de recursos
> * Localizar consultas de execução longa

[Sugestões de otimização de desempenho de base de dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
