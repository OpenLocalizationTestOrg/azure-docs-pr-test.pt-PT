---
title: "controlo de acesso baseado em aaaRole na automatização do Azure | Microsoft Docs"
description: "O controlo de acesso baseado em funções (RBAC) permite uma gestão de acesso para os recursos do Azure. Este artigo descreve como tooset configurar o RBAC na automatização do Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: "rbac de automatização, controlo de acesso baseado em funções , rbac do azure"
ms.assetid: 04b5625e-0ee8-4b5b-85cd-7734c1b3d4a3
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 051438e44d0c5c514d6dbaac5a312344ee311cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-in-azure-automation"></a>Controlo de acesso baseado em funções na Automatização do Azure
## <a name="role-based-access-control"></a>Controlo de acesso baseado em funções
O controlo de acesso baseado em funções (RBAC) permite uma gestão de acesso para os recursos do Azure. Utilizar [RBAC](../active-directory/role-based-access-control-configure.md), pode segregar funções na sua equipa e conceder apenas Olá quantidade de acesso toousers, grupos e aplicações que precisam de tooperform as respetivas tarefas. Acesso baseado em funções pode ser concedido toousers utilizando Olá portal do Azure, as ferramentas da linha de comandos do Azure ou APIs de gestão do Azure.

## <a name="rbac-in-automation-accounts"></a>RBAC em Contas de Automatização
Na automatização do Azure, é concedido acesso ao atribuir Olá toousers de funções RBAC adequada, grupos e aplicações em Olá âmbito da conta de automatização. Seguintes são Olá funções incorporadas suportadas por uma conta de automatização:  

| **Função** | **Descrição** |
|:--- |:--- |
| Proprietário |função de proprietário de Olá permite tooall aceder a recursos e ações dentro de uma conta de automatização, incluindo fornecer acesso tooother utilizadores, grupos e aplicações toomanage Olá conta de automatização. |
| Contribuinte |função de contribuinte Olá permite-lhe toomanage tudo, exceto modificar outro utilizador aceder à conta de automatização de tooan de permissões. |
| Leitor |função de leitor de Olá permite-lhe tooview todos os recursos de Olá uma automatização conta, mas não é possível efetuar quaisquer alterações. |
| Operador de Automatização |função de operador de automatização Olá permite-lhe tooperform de tarefas operacionais, tais como iniciar, parar, suspender, retomar e agendar tarefas. Esta função é útil se pretender tooprotect seus recursos da conta de automatização como recursos de credenciais e runbooks de ser visualização ou modificação, mas ainda permite que os membros da sua organização tooexecute estes runbooks. |
| Administrador de Acesso de Utilizador |função de administrador de acesso de utilizador Olá permite-lhe toomanage utilizador acesso tooAzure as contas de automatização. |

> [!NOTE]
> Não é possível conceder acesso direitos tooa runbook ou runbooks específicos, apenas toohello recursos e ações dentro Olá conta de automatização.  
> 
> 

Neste artigo, ajudá-lhe como tooset configurar o RBAC na automatização do Azure. Mas, primeiro, vamos tirar uma próximo observar Olá permissões individuais concedida toohello Contribuidor, leitor, operador de automatização e administrador de acesso de utilizador para que possamos ter uma boa compreensão antes de conceder a alguém direitos toohello conta de automatização.  Caso contrário, poderão resultar em consequências involuntárias ou indesejáveis.     

## <a name="contributor-role-permissions"></a>Permissões de Função de Contribuidor
Olá tabela seguinte apresenta Olá ações específicas que podem ser efetuadas pela função de contribuinte Olá na automatização.

| **Tipo de Recurso** | **Leitura** | **Escrita** | **Eliminar** | **Outras Ações** |
|:--- |:--- |:--- |:--- |:--- |
| Adicionar Conta de Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Recurso de Certificado de Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Recurso de Ligação de Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Recurso de Tipo de Ligação de Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Recurso de Credenciais de Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Recurso de Agenda da Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Recurso de Variável de Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Configuração do Estado Pretendido de Automatização | | | |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |
| Tipo de Recurso da Função de Trabalho de Runbook Híbrida |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Tarefa de Automatização do Azure |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |
| Fluxo de Trabalho de Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Plano de Trabalho da Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Módulo de Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Runbook da Automatização do Azure |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |
| Rascunho do Runbook da Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |
| Tarefa de Teste de Rascunho do Runbook de Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |
| Webhook de automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |

## <a name="reader-role-permissions"></a>Permissões de função de leitor
Olá tabela seguinte apresenta Olá ações específicas que podem ser efetuadas pela função de leitor de Olá na automatização.

| **Tipo de Recurso** | **Leitura** | **Escrita** | **Eliminar** | **Outras Ações** |
|:--- |:--- |:--- |:--- |:--- |
| Administrador de subscrição clássica |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Bloqueio de gestão |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Permissão |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Operações de fornecedor |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Atribuição de função |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Definição de função |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="automation-operator-role-permissions"></a>Permissões de função do Operador de Automatização
Olá tabela seguinte apresenta Olá ações específicas que podem ser efetuadas pela função de operador de automatização de Olá na automatização.

| **Tipo de Recurso** | **Leitura** | **Escrita** | **Eliminar** | **Outras Ações** |
|:--- |:--- |:--- |:--- |:--- |
| Adicionar Conta de Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Recurso de Certificado de Automatização | | | | |
| Recurso de Ligação de Automatização | | | | |
| Recurso de Tipo de Ligação de Automatização | | | | |
| Recurso de Credenciais de Automatização | | | | |
| Recurso de Agenda da Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | |
| Recurso de Variável de Automatização | | | | |
| Configuração do Estado Pretendido de Automatização | | | | |
| Tipo de Recurso da Função de Trabalho de Runbook Híbrida | | | | |
| Tarefa de Automatização do Azure |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |
| Fluxo de Trabalho de Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Plano de Trabalho da Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | |
| Módulo de Automatização | | | | |
| Runbook da Automatização do Azure |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Rascunho do Runbook da Automatização | | | | |
| Tarefa de Teste de Rascunho do Runbook de Automatização | | | | |
| Webhook de automatização | | | | |

Para obter mais detalhes, Olá [ações de operador de automatização](../active-directory/role-based-access-built-in-roles.md#automation-operator) listas Olá ações suportadas pela função de operador de automatização Olá na conta de automatização Olá e os respetivos recursos.

## <a name="user-access-administrator-role-permissions"></a>Permissões da função Administrador de Acesso de Utilizador
Olá tabela seguinte apresenta Olá ações específicas que podem ser efetuadas pela função de administrador de acesso de utilizador de Olá na automatização.

| **Tipo de Recurso** | **Leitura** | **Escrita** | **Eliminar** | **Outras Ações** |
|:--- |:--- |:--- |:--- |:--- |
| Adicionar Conta de Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Recurso de Certificado de Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Recurso de Ligação de Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Recurso de Tipo de Ligação de Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Recurso de Credenciais de Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Recurso de Agenda da Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Recurso de Variável de Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Configuração do Estado Pretendido de Automatização | | | | |
| Tipo de Recurso da Função de Trabalho de Runbook Híbrida |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Tarefa de Automatização do Azure |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Fluxo de Trabalho de Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Plano de Trabalho da Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Módulo de Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Runbook da Automatização do Azure |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Rascunho do Runbook da Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Tarefa de Teste de Rascunho do Runbook de Automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Webhook de automatização |![Estado Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="configure-rbac-for-your-automation-account-using-azure-portal"></a>Configurar o RBAC para a sua Conta de Automatização com o Portal do Azure
1. Inicie sessão no toohello [Portal do Azure](https://portal.azure.com/) e abra a sua conta de automatização a partir do painel de contas de automatização Olá.  
2. Clique em Olá **acesso** controlo ao hello canto superior direito. Esta ação abre Olá **utilizadores** painel onde pode adicionar novo toomanage de utilizadores, grupos e aplicações a conta de automatização e das funções existentes vista que podem ser configuradas para Olá conta de automatização.  
   
   ![Botão de acesso](media/automation-role-based-access-control/automation-01-access-button.png)  

> [!NOTE]
> **Os administradores da subscrição** já existe como utilizador do Olá predefinido. grupo do Active Directory do Olá subscrição admins inclui administradores de serviço de Olá e coadministradores para a sua subscrição do Azure. Olá, admin serviço é proprietário de Olá da sua subscrição do Azure e os respetivos recursos e irá ter função de proprietário Olá herdada para as contas de automatização Olá demasiado. Isto significa que o acesso de Olá **herdado** para **administradores e coadministradores de serviço** de uma subscrição e a respetiva **atribuído** para Olá todos os outros utilizadores. Clique em **administradores da subscrição** tooview mais detalhes sobre as respetivas permissões.  
> 
> 

### <a name="add-a-new-user-and-assign-a-role"></a>Adicionar um novo utilizador e atribuir uma função
1. No painel de utilizadores Olá, clique em **adicionar** tooopen Olá **painel adicionar acesso** onde pode adicionar um utilizador, grupo ou aplicação e atribuir uma função toothem.  
   
   ![Adicionar utilizador](media/automation-role-based-access-control/automation-02-add-user.png)  
2. Selecione uma função Olá lista de funções disponíveis. Vamos escolher Olá **leitor** função, mas pode escolher qualquer uma das Olá funções incorporadas disponíveis que suporte a uma conta de automatização ou qualquer função personalizada que pode ter definido.  
   
   ![Selecionar função](media/automation-role-based-access-control/automation-03-select-role.png)  
3. Clique em **adicionar utilizadores** tooopen Olá **adicionar utilizadores** painel. Se tiver adicionado quaisquer utilizadores, grupos ou aplicações toomanage sua subscrição, em seguida, os utilizadores estão listados e pode selecioná-los tooadd acesso. Se não existirem quaisquer utilizadores listados ou se estiver interessado na adição de utilizador de Olá não estiver listado, em seguida, clique em **convidar** tooopen Olá **convidar um convidado** painel, onde pode convidar um utilizador com uma conta Microsoft válida endereço de correio eletrónico, tais como o Outlook.com, OneDrive ou Xbox Live Ids. Depois de introduzir o endereço de correio eletrónico Olá do utilizador Olá, clique em **selecione** tooadd Olá utilizador e, em seguida, clique em **OK**. 
   
   ![Adicionar utilizadores](media/automation-role-based-access-control/automation-04-add-users.png)  
   
   Agora deverá ver o utilizador Olá adicionado toohello **utilizadores** painel com Olá **leitor** função atribuída.  
   
   ![Listar utilizadores](media/automation-role-based-access-control/automation-05-list-users.png)  
   
   Também pode atribuir um utilizador de Olá toohello uma função **funções** painel. 
4. Clique em **funções** de Olá de tooopen de painel de utilizadores Olá **painel funções**. A partir deste painel, pode ver o nome de Olá da função de Olá, número de Olá de utilizadores e grupos atribuídos toothat função.
   
    ![Atribuir função a partir do painel de utilizadores](media/automation-role-based-access-control/automation-06-assign-role-from-users-blade.png)  
   
   > [!NOTE]
   > Controlo de acesso baseado em funções só pode ser definido ao nível da conta de automatização de Olá e não em qualquer recurso abaixo Olá conta de automatização.
   > 
   > 
   
    Pode atribuir mais do que um utilizador de tooa de função, grupo ou aplicação. Por exemplo, se adicionamos Olá **operador de automatização** função juntamente com Olá **função leitor** toohello utilizador, em seguida, que podem ver todos os recursos de automatização de Olá, bem como executar tarefas de runbook Olá. Pode expandir a lista pendente de Olá tooview uma lista de funções atribuídas toohello utilizador.  
   
    ![Ver várias funções](media/automation-role-based-access-control/automation-07-view-multiple-roles.png)  

### <a name="remove-a-user"></a>Remover um utilizador
Pode remover a permissão de acesso de Olá para um utilizador que não está a gerir Olá conta de automatização ou que já não trabalha para a organização Olá. Seguintes são Olá passos tooremove um utilizador: 

1. De Olá **utilizadores** painel, atribuição de função Olá Selecione se pretende tooremove.
2. Clique em Olá **remover** botão no painel de detalhes de atribuição de Olá.
3. Clique em **Sim** tooconfirm remoção. 
   
   ![Remover utilizadores](media/automation-role-based-access-control/automation-08-remove-users.png)  

## <a name="role-assigned-user"></a>Utilizador com Função Atribuída
Quando uma função de tooa atribuída ao utilizador inicia sessão tootheir conta de automatização, podem agora ver conta do Olá proprietário listada na lista de Olá de **diretórios predefinidos**. Na conta de automatização que tenha sido adicionados da Olá de tooview a ordem, tem de trocar Olá predefinido diretório toohello diretório predefinido do proprietário.  

![Diretório predefinido](media/automation-role-based-access-control/automation-09-default-directory-in-role-assigned-user.png)  

### <a name="user-experience-for-automation-operator-role"></a>Experiência de utilizador para a função de operador de Automatização
Quando um utilizador, que é atribuído a vistas de função de operador de automatização toohello são atribuídas a conta de automatização de Olá, estes requisitos podem apenas lista de Olá de vista de runbooks, tarefas de runbook e agendas criadas no Olá conta de automatização, mas não é possível ver a respetiva definição. Estes podem iniciar, parar, suspender, retomar ou agendar a tarefa de runbook Olá. utilizador Olá não terá acesso tooother recursos de automatização, tais como configurações, grupos de trabalho híbrida ou nós de DSC.  

![Não existem tooresourcres de acesso](media/automation-role-based-access-control/automation-10-no-access-to-resources.png)  

Quando o utilizador Olá clica no runbook Olá, hello comandos tooview Olá origem ou editar o runbook Olá não são fornecidos como função de operador de automatização Olá não permite o acesso toothem.  

![Nenhum runbook tooedit de acesso](media/automation-role-based-access-control/automation-11-no-access-to-edit-runbook.png)  

utilizador Olá terão acesso tooview e toocreate agendas, mas não terão acesso tooany outro tipo de recurso.  

![Não existem tooassets de acesso](media/automation-role-based-access-control/automation-12-no-access-to-assets.png)  

Este utilizador também não tem acesso tooview Olá webhooks associados a um runbook

![Não existem toowebhooks de acesso](media/automation-role-based-access-control/automation-13-no-access-to-webhooks.png)  

## <a name="configure-rbac-for-your-automation-account-using-azure-powershell"></a>Configurar o RBAC para a sua Conta de Automatização com o Azure PowerShell
Acesso baseado em funções também pode ser configurado tooan conta de automatização utilizando Olá seguintes [cmdlets Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md).

• [Get-AzureRmRoleDefinition](https://msdn.microsoft.com/library/mt603792.aspx) lista todas as funções do RBAC que estão disponíveis no Azure Active Directory. Pode utilizar este comando juntamente com Olá **nome** toolist propriedade Olá todas as ações que podem ser efetuadas pela função específica.  
    **Exemplo:**  
    ![Obter a definição de função](media/automation-role-based-access-control/automation-14-get-azurerm-role-definition.png)  

• [Get-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt619413.aspx) listas atribuições de funções de RBAC do Azure AD no Olá especificado âmbito. Sem quaisquer parâmetros, este comando devolve todas as atribuições de função Olá efetuadas sob Olá subscrição. Olá utilize **ExpandPrincipalGroups** atribuições de acesso do parâmetro toolist para Olá especificados de utilizador, bem como grupos de Olá Olá utilizador faz parte.  
    **Exemplo:** seguinte de Olá utilize comando toolist todos os utilizadores de Olá e as respetivas funções dentro de uma conta de automatização.

    Get-AzureRMRoleAssignment -scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>” 

![Obter a atribuição de função](media/automation-role-based-access-control/automation-15-get-azurerm-role-assignment.png)

• [New-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603580.aspx) tooassign acesso toousers, grupos e aplicações tooa determinado âmbito.  
    **Exemplo:** seguinte de Olá utilize comando função de "Operador de automatização" Olá tooassign de um utilizador no âmbito da conta de automatização de Olá.

    New-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish toogrant access> -RoleDefinitionName "Automation operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”  

![Nova atribuição de função](media/automation-role-based-access-control/automation-16-new-azurerm-role-assignment.png)

• Utilize [Remove-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603781.aspx) tooremove acesso de um utilizador especificado, grupo ou aplicação num determinado âmbito.  
    **Exemplo:** seguinte de Olá utilize comando utilizador de Olá tooremove da função de "Operador de automatização" Olá no Olá âmbito da conta de automatização.

    Remove-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish tooremove> -RoleDefinitionName "Automation Operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”

No Olá acima exemplos, substitua **sessão Id**, **Id de subscrição**, **nome do grupo de recursos** e **nome da conta de automatização** com o Detalhes da conta. Escolha **Sim** quando lhe for pedido tooconfirm antes de continuar tooremove atribuição de função de utilizador.   

## <a name="next-steps"></a>Passos Seguintes
* Para informações sobre diferentes formas tooconfigure RBAC de automatização do Azure, consulte demasiado[gerir o RBAC com o Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md).
* Para obter detalhes sobre diferentes formas toostart um runbook, consulte [iniciar um runbook](automation-starting-a-runbook.md)
* Para obter informações sobre os tipos de runbook diferente, consulte demasiado[tipos de runbook da automatização do Azure](automation-runbook-types.md)

