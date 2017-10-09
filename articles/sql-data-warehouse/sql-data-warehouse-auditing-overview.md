---
title: aaaAuditing no Azure SQL Data Warehouse | Microsoft Docs
description: "Introdução ao Azure SQL Data Warehouse de auditoria"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 08/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 948de74fa052ef206cf1aa65c0d81f084b18cb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a>Auditoria no armazém de dados SQL do Azure
> [!div class="op_single_selector"]
> * [Auditoria](sql-data-warehouse-auditing-overview.md)
> * [Deteção de ameaças](sql-data-warehouse-security-threat-detection.md)
> 
> 

Auditoria de SQL Data Warehouse permite-lhe toorecord eventos no registo de auditoria de tooan a base de dados na sua conta do Storage do Azure. Auditoria pode ajudar a manter a conformidade de regulamentação, compreender a atividade de base de dados e obter informações sobre discrepâncias e anomalias que poderão indicar preocupações para a empresa ou suspeitas de violação de segurança. Auditoria de SQL Data Warehouse também integra-se com o Microsoft Power BI para desagregar relatórios e análise.

As ferramentas de auditoria ativarem e facilitam as normas de toocompliance aderência, mas não garantir a compatibilidade. Para obter mais informações sobre o Azure programas que conformidade de padrões de suporte, consulte Olá <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Centro de fidedignidade do Azure</a>.

* [Noções básicas de auditoria de base de dados]
* [Configurar a auditoria da base de dados]
* [Analisar registos de auditoria e relatórios]

## <a id="subheading-1"></a>Noções básicas de auditoria da base de dados de armazém de dados do SQL do Azure
Auditoria de base de dados do SQL Data Warehouse permite-lhe:

* **Manter** um registo de auditoria de eventos selecionados. Pode definir categorias de base de dados ações toobe auditada.
* **Relatório** na atividade de base de dados. Pode utilizar relatórios pré-configurados e tooget um dashboard a trabalhar rapidamente com atividade e o relatório de eventos.
* **Analisar** relatórios. Pode encontrar eventos suspeitos, atividade invulgar e tendências.

Pode configurar a auditoria para Olá seguintes categorias de evento:

**SQL simples** e **parametrizadas SQL** para que Olá registos de auditoria recolhidos são classificados como  

* **Acesso toodata**
* **Alterações do esquema (DDL)**
* **Alterações de dados (DML)**
* **Contas, funções e permissões (DCL)**
* **Procedimento armazenado**, **início de sessão** e, **transação gestão**.

Para cada categoria de evento de auditoria de **êxito** e **falha** operações configuradas em separado.

Para obter mais informações sobre atividades de Olá e os eventos auditados, consulte Olá <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">referência de formatos de registo de auditoria (transferência de ficheiro do documento)</a>.

Os registos de auditoria são armazenados na sua conta do storage do Azure. Pode definir um período de retenção do registo de auditoria.

Uma política de auditoria pode ser definida para uma base de dados específica ou como uma política de servidor de predefinição. Uma política de auditoria do servidor predefinido aplica-se tooall bases de dados num servidor, que não dispõe de uma substituição da base de dados auditoria política específica definida.

Antes de configurar a auditoria de auditoria de verificação se estiver a utilizar um ["Clientes de nível inferior."](sql-data-warehouse-auditing-downlevel-clients.md)

## <a id="subheading-2"></a>Configurar a auditoria da base de dados
1. Iniciar Olá <a href="https://portal.azure.com" target="_blank">portal do Azure</a>.
2. Aceda toohello **definições** painel de Olá pretende tooaudit do SQL Data Warehouse. No Olá **definições** painel, selecione **deteção de ameaças e auditoria**.
   
    ![][1]
3. Em seguida, ativar a auditoria clicando Olá **ON** botão.
   
    ![][3]
4. No painel Configuração de auditoria de Olá, selecione **detalhes armazenamento** painel de armazenamento de registos de auditoria de Olá tooopen. Selecione Olá conta de armazenamento do Azure onde serão guardados registos e Olá período de retenção. 
>[!TIP]
>Olá utilize mesma conta de armazenamento para todos os Olá de tooget auditada bases de dados mais fora Olá pré-configurados relatórios de modelos.
   
    ![][4]
5. Clique em Olá **OK** configuração de detalhes do botão toosave Olá armazenamento.
6. Em **registo pelo evento**, clique em **êxito** e **falha** toolog todos os eventos, ou escolha categorias de eventos individuais.
7. Se estiver a configurar auditoria para uma base de dados, poderá ser necessário a cadeia de ligação de Olá tooalter do seu tooensure cliente auditoria de dados é capturado corretamente. Verifique Olá [modificar FDQN de servidor na cadeia de ligação de Olá](sql-data-warehouse-auditing-downlevel-clients.md) tópico para ligações de cliente de nível inferior.
8. Clique em **OK**.

## <a id="subheading-3"></a>Analisar registos de auditoria e relatórios
Os registos de auditoria são agregados de uma coleção de tabelas de arquivo com um **SQLDBAuditLogs** prefixo no Olá que escolheu durante a configuração de conta de armazenamento do Azure. Pode ver ficheiros de registo utilizando uma ferramenta como <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Explorador de armazenamento do Azure</a>.

Um modelo de relatório do dashboard pré-configurada está disponível como uma <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">transferível folha de cálculo do Excel</a> toohelp analisar rapidamente os dados de registo. modelo de Olá toouse nos seus registos de auditoria, terá de Excel 2013 ou posterior e o Power Query, que pode transferir <a href="http://www.microsoft.com/download/details.aspx?id=39379">aqui</a>.

modelo de Olá tem dados de exemplo fictícias no mesmo e, pode configurar Power Query tooimport o registo de auditoria diretamente a partir da sua conta do storage do Azure.

## <a id="subheading-4"></a>Regeneração da chave de armazenamento
Na produção, é provável toorefresh o armazenamento de chaves periodicamente. Ao atualizar as suas chaves, terá de política de Olá toosave. processo de Olá é o seguinte:

1. No Olá auditoria painel de configuração (descrito acima em auditoria secção de configuração de Olá) comutador Olá **chave de acesso de armazenamento** de *primário* demasiado*secundário* e  **GUARDAR**.

   ![][4]
2. Painel de configuração de armazenamento toohello aceda e **regenerar** Olá *chave de acesso primária*.
3. Voltar atrás toohello auditoria painel de configuração, o comutador Olá **chave de acesso de armazenamento** de *secundário* demasiado*primário* e prima **guardar**.
4. Voltar atrás toohello armazenamento IU e **regenerar** Olá *chave de acesso secundária* (como preparação para Olá chaves seguintes atualização ciclo.

## <a id="subheading-5"></a>Automatização (do PowerShell/REST API)
Também pode configurar a auditoria no Azure SQL Data Warehouse, utilizando Olá seguintes ferramentas de automatização:

* **Cmdlets do PowerShell**:

   * [Get-AzureRMSqlDatabaseAuditingPolicy][101]
   * [Get-AzureRMSqlServerAuditingPolicy][102]
   * [Remover AzureRMSqlDatabaseAuditing][103]
   * [Remover AzureRMSqlServerAuditing][104]
   * [Conjunto AzureRMSqlDatabaseAuditingPolicy][105]
   * [Conjunto AzureRMSqlServerAuditingPolicy][106]
   * [Utilize AzureRMSqlServerAuditingPolicy][107]

<!--Anchors-->
[Noções básicas de auditoria de base de dados]: #subheading-1
[Configurar a auditoria da base de dados]: #subheading-2
[Analisar registos de auditoria e relatórios]: #subheading-3


<!--Image references-->
[1]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->
[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy