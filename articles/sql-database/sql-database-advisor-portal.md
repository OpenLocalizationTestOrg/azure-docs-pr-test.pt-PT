---
title: "recomendações de desempenho de aaaApply - SQL Database do Azure | Microsoft Docs"
description: "Pode utilizar Olá toofind portal do Azure desempenho recomendações que podem otimizar o desempenho da SQL Database do Azure ou toocorrect algum problema identificado na sua carga de trabalho."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a>Localizar e aplicar as recomendações de desempenho

Pode utilizar Olá toofind portal do Azure desempenho recomendações que podem otimizar o desempenho da SQL Database do Azure ou toocorrect algum problema identificado na sua carga de trabalho. **Recomendação de desempenho** página no portal do Azure permite-lhe toofind Olá superior as recomendações com base no respetivo impacto potencial. 

## <a name="viewing-recommendations"></a>Recomendações de visualização

tooview e aplicar as recomendações de desempenho, precisa de Olá correto [controlo de acesso baseado em funções](../active-directory/role-based-access-control-what-is.md) permissões no Azure. **Leitor**, **contribuinte da BD SQL** permissões são necessárias tooview recomendações, e **proprietário**, **contribuinte da BD SQL** são necessárias permissões tooexecute quaisquer ações; Criar ou remova índices e cancelar a criação de índices.

Utilize Olá seguir as recomendações de desempenho de toofind passos no portal do Azure:

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).
2. Aceda demasiado**mais serviços** > **bases de dados SQL**e selecione a base de dados.
3. Navegue demasiado**recomendação de desempenho** tooview recomendações disponíveis para a base de dados selecionada Olá.

Recomendações de desempenho são shonw no Olá tabela toohello de semelhante mostrado na Olá figura a seguir:

![Recomendações](./media/sql-database-advisor-portal/recommendations.png)

Recomendações são ordenadas pelo respetivo potencial impacto no desempenho no Olá seguintes categorias:

| Impacto | Descrição |
|:--- |:--- |
| Elevado |Recomendações de elevado impacto devem fornecer o impacto no desempenho mais significativo Olá. |
| Médio |Impacto médio recomendações devem melhorar o desempenho, mas não substancialmente. |
| Baixo |Recomendações de impacto baixa devem fornecer um melhor desempenho sem, mas poderão não ser significativos melhoramentos. |


> [!NOTE]
> Base de dados SQL do Azure necessita toomonitor atividades com pelo menos um dia na ordem tooidentify algumas recomendações. Olá SQL Database do Azure pode otimizar mais facilmente para padrões de consulta consistente que pode para aleatórios bursts spotty da atividade. Se as recomendações não estão disponível corrently, Olá **recomendação de desempenho** página fornece uma mensagem explicar o motivo.
> 

Também pode ver o estado de Olá do histórico de operações Olá. Selecione uma recomendação ou estado toosee mais detalhes.

Eis um exemplo de recomendação "Criar índice" no Olá portal do Azure.

![Criar o índice](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a>Aplicar as recomendações
Base de dados SQL do Azure dá-lhe controlo total sobre a forma como as recomendações são ativada utilizando qualquer um dos Olá seguintes três opções: 

* Aplica recomendações individuais um cada vez.
* Ativar Olá tooautomatically otimização automática aplicar recomendações.
* tooimplement uma recomendação manualmente, execute Olá recomendado script T-SQL em relação a sua base de dados.

Selecione qualquer tooview recomendação os respectivos detalhes e, em seguida, clique em **Ver script** tooreview Olá obter detalhes exatos sobre como a recomendação de Olá é criada.

base de dados de Olá permanece online enquanto é aplicada a recomendação de Olá – utilizar a recomendação de desempenho ou a otimização automática nunca demora uma base de dados offline.

### <a name="apply-an-individual-recommendation"></a>Aplicar uma recomendação individuais
Pode rever e aceitar recomendações um cada vez.

1. No Olá **recomendações** painel, selecione uma recomendação.
2. No Olá **detalhes** painel clique **aplicar** botão.
   
    ![aplicar a recomendação](./media/sql-database-advisor-portal/apply.png)

Recomendação selecionada será aplicada na base de dados de Olá.

### <a name="removing-recommendations-from-hello-list"></a>A remover as recomendações da lista de Olá
Se a lista de recomendações contiver itens que pretende que o tooremove da lista de Olá, pode eliminar recomendação Olá:

1. Selecione uma recomendação na lista de Olá de **recomendações** detalhes de Olá tooopen.
2. Clique em **rejeitar** no Olá **detalhes** painel.

Se assim o desejar, pode adicionar itens rejeitados fazer uma cópia toohello **recomendações** lista:

1. No Olá **recomendações** painel clique **vista rejeitada**.
2. Selecione um item rejeitado Olá lista tooview os respetivos detalhes.
3. Opcionalmente, clique em **anular rejeitar** tooadd Olá índice back toohello principal lista de **recomendações**.


### <a name="enable-automatic-tuning"></a>Ativar o ajuste automático
Pode definir automaticamente recomendações de tooimplement Olá SQL Database do Azure. Como recomendações fiquem disponíveis automaticamente serão aplicadas. Como com todas as recomendações geridas pelo Olá serviço esteja de impacto no desempenho de Olá recomendação Olá negativo será revertido.

1. No Olá **recomendações** painel, clique em **Automate**:
   
    ![Definições do Advisor](./media/sql-database-advisor-portal/settings.png)
2. Selecione tooautomate ações:
   
    ![Recomendado índices](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a>Executar manualmente Olá recomendado script T-SQL
Selecione qualquer recomendação e, em seguida, clique em **Ver script**. Execute este script na sua base de dados toomanually aplicar a recomendação de Olá.

*Índices que são executados manualmente não são monitorizados e validados de impacto no desempenho pelo serviço de Olá* pelo que é sugerido que monitorizar estes índices após criação tooverify fornecer ganhos de desempenho e ajustar ou eliminá-los se necessário. Para obter detalhes sobre a criação de índices, consulte [criar índice (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).

### <a name="canceling-recommendations"></a>Cancelar recomendações
Recomendações que estão num **pendente**, **verificar**, ou **êxito** Estado pode ser cancelado. Recomendações com um Estado de **Executing** não pode ser cancelado.

1. Selecione uma recomendação Olá **otimização histórico** Olá de tooopen área **os detalhes das recomendações** painel.
2. Clique em **Cancelar** tooabort o processo de Olá aplicar a recomendação de Olá.

## <a name="monitoring-operations"></a>Operações de monitorização
Aplicar a recomendação não poderá acontecer instantaneamente. portal de Olá fornece detalhes sobre o estado de Olá de recomendação. Olá, são possíveis Estados que um índice pode ser:

| Estado | Descrição |
|:--- |:--- |
| Pendente |Aplica a recomendação comando foi recebido e está agendado para execução. |
| Executar |está a ser aplicada a recomendação de Olá. |
| A verificar |Recomendação foi aplicada com êxito e o serviço de Olá é medir vantagens Olá. |
| Êxito |Recomendação foi aplicada com êxito e tem sido medidos benefícios. |
| Erro |Ocorreu um erro durante o processo de Olá aplicar a recomendação de Olá. Isto pode ser um problema passageiro ou, possivelmente, uma tabela de toohello de alteração de esquema e scripts de Olá já não é válido. |
| A reversão |recomendação de Olá foi aplicada, mas foi considerado vvalidação não performant e está a ser revertida automaticamente. |
| Reverter |recomendação de Olá foi revertida. |

Clique uma recomendação de no processo do Olá lista toosee mais detalhes:

![Recomendado índices](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a>Reverter uma recomendação
Se utilizou a recomendação do Olá desempenho recomendações tooapply Olá (que significa que não foi executado manualmente script Olá T-SQL)-la automaticamente reverterá se localiza toobe de impacto do desempenho de Olá negativo. Se por alguma razão pretende simplesmente toorevert uma recomendação para fazer o seguinte de Olá:

1. Selecione uma recomendação aplicada com êxito na Olá **otimização histórico** área.
2. Clique em **reverter** no Olá **detalhes de recomendação** painel.

![Recomendado índices](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a>Impacto no desempenho das recomendações do índice de monitorização
Depois das recomendações são implementadas com êxito (atualmente, operações de índice e parametrizar recomendações de consultas só), pode clicar em **informações acerca das consultas** no tooopen de painel de detalhes de recomendação Olá [consulta Informações acerca do desempenho](sql-database-query-performance.md) e ver o impacto do desempenho Olá das suas consultas superiores.

![Impacto no desempenho do monitor](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a>Resumo
Base de dados SQL do Azure fornece recomendações para melhorar o desempenho de base de dados do SQL Server. Fornecendo scripts T-SQL, bem como individuais e totalmente-automático, obter um assistência útil para otimizar a base de dados e, em última análise melhorar o desempenho da consulta.

## <a name="next-steps"></a>Passos seguintes
Monitorizar as recomendações e continuar tooapply-los toorefine desempenho. Cargas de trabalho de base de dados são dinâmicas e alterar continuamente. Base de dados SQL do Azure irá prosseguir toomonitor e fornecer recomendações podem potencialmente melhorar o desempenho da base de dados. 

* Consulte [otimização automática](sql-database-automatic-tuning.md) toolearn mais informações sobre como Olá otimização automática na SQL Database do Azure.
* Consulte [recomendações de desempenho](sql-database-advisor.md) para uma descrição geral das recomendações de desempenho de SQL Database do Azure.
* Consulte [Query Performance Insight](sql-database-query-performance.md) toolearn sobre a visualização de impacto no desempenho de Olá das suas consultas superiores.

## <a name="additional-resources"></a>Recursos adicionais
* [O arquivo de consultas](https://msdn.microsoft.com/library/dn817826.aspx)
* [CRIAR O ÍNDICE](https://msdn.microsoft.com/library/ms188783.aspx)
* [Controlo de acesso baseado em funções](../active-directory/role-based-access-control-what-is.md)

