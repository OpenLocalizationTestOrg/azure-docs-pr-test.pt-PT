---
title: aaaCreate conta de utilizador do Azure AD | Microsoft Docs
description: "Este artigo descreve como de credencial toocreate uma conta de utilizador do Azure AD para runbooks na automatização do Azure tooauthenticate no Azure e Azure clássico."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: "utilizador do azure active directory, gestão do serviço do azure, conta de utilizador do azure ad"
ms.assetid: fcfe266d-b22e-4dfb-8272-adcab09fc0cf
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 7c6ed4182dbab074d0bc5da7057f74ad321d8884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-azure-classic-deployment-and-resource-manager"></a>Autenticar Runbooks com a implementação clássica do Azure e o Resource Manager
Este artigo descreve os passos de Olá que tem de efetuar tooconfigure uma conta de utilizador do Azure AD para runbooks de automatização do Azure em execução contra o modelo de implementação clássica do Azure ou recursos do Azure Resource Manager.  Embora isto continue toobe uma identidade de autenticação suportadas para o Gestor de recursos do Azure com runbooks, Olá recomendado método está a utilizar uma conta Run As do Azure.       

## <a name="create-a-new-azure-active-directory-user"></a>Criar um novo utilizador do Azure Active Directory
1. Inicie sessão no portal clássico do Azure toohello como um administrador de serviço para Olá pretende toomanage de subscrição do Azure.
2. Selecione **do Active Directory**e, em seguida, selecione o nome de Olá do diretório da organização.
3. Selecione Olá **utilizadores** separador e, em seguida, na área de comando Olá, selecione **adicionar utilizador**.
4. No Olá **diga-nos informações sobre este utilizador** página **tipo de utilizador**, selecione **novo utilizador na sua organização**.
5. Introduza um nome de utilizador.  
6. Selecione o nome de diretório de Olá que está associado a sua subscrição do Azure na página do Active Directory Olá.
7. No Olá **perfil de utilizador** , indique um primeiro e último nome, um nome amigável de utilizador e utilizador da Olá **funções** lista.  Não **Ative a Multi-Factor Authentication**.
8. Tenha em atenção o nome completo de Olá utilizador e palavra-passe temporária.
9. Selecione **Definições > Administradores > Adicionar**.
10. Escreva o nome de utilizador completo Olá do utilizador Olá que criou.
11. Selecione a subscrição de Olá que pretende que sejam Olá toomanage de utilizador.
12. Termine sessão no Azure e, em seguida, inicie sessão novamente com a conta de Olá que acabou de criar. Será palavra-passe do utilizador Olá toochange pedido.

## <a name="create-an-automation-account-in-azure-classic-portal"></a>Crie uma conta de Automatização no portal Clássico do Azure
Nesta secção, efetuar Olá os seguintes passos toocreate uma conta de automatização do Azure no portal do Azure para utilização de Olá com os runbooks gerir recursos de implementação clássico do Azure.  

> [!NOTE]
> As contas de automatização criadas com o portal clássico do Azure Olá podem ser geridas por Olá clássico do Azure e portal do Azure e um conjunto de cmdlets. Após criar a conta de Olá, não faz diferença como criar e gerir recursos na conta de Olá. Se estiver a planear toocontinue toouse Olá portal clássico do Azure, em seguida, deve utilizá-lo em vez de Olá toocreate portal do Azure, as contas de automatização.
> 
> 

1. Inicie sessão no portal clássico do Azure toohello como um administrador de serviço para Olá pretende toomanage de subscrição do Azure.
2. Selecione **Automatização**.
3. No Olá **automatização** página, selecione **criar uma conta de automatização**.
4. No Olá **criar uma conta de automatização** caixa, escreva um nome para a sua nova conta de automatização e selecione um **região** de Olá na lista pendente.  
5. Clique em **OK** tooaccept as suas definições e crie Olá conta.
6. Depois de criado, será listado no Olá **automatização** página.
7. Clique na conta de Olá e aparecerá a toohello página do Dashboard.  
8. Na página do Dashboard de automatização de Olá, selecione **ativos**.
9. No Olá **ativos** página, selecione **adicionar definições** localizado em Olá parte inferior da página Olá.
10. No Olá **adicionar definições** página, selecione **adicionar credencial**.
11. No Olá **definir credencial** página, selecione **credencial do Windows PowerShell** de Olá **tipo de credencial** pendente listar e forneça um nome para a credencial Olá.
12. No seguinte Olá **definir credencial** página tipo Olá nome de utilizador da conta de utilizador de Olá AD criada anteriormente no Olá **nome de utilizador** campo e Olá palavra-passe Olá **palavra-passe**e **Confirmar palavra-passe** campos. Clique em **OK** toosave as suas alterações.

## <a name="create-an-automation-account-in-hello-azure-portal"></a>Criar uma conta de automatização no portal do Azure de Olá
Nesta secção, execute Olá os seguintes passos toocreate uma conta de automatização do Azure no portal do Azure para utilização de Olá com os runbooks gerir recursos no modo Azure Resource Manager.  

1. Inicie sessão no toohello portal do Azure como um administrador de serviço para Olá pretende toomanage de subscrição do Azure.
2. Selecione **Contas de Automatização**.
3. No painel de contas de automatização de Olá, clique em **adicionar**.<br><br>![Adicionar Conta de Automatização](media/automation-create-aduser-account/add-automation-acct-properties.png)
4. No Olá **adicionar conta de automatização** painel, no Olá **nome** caixa escreva um nome para a sua nova conta de automatização.
5. Se tiver mais do que uma subscrição, especifique Olá um para a nova conta de Olá, bem como um novo ou existente **grupo de recursos** e num datacenter do Azure **localização**.
6. Selecione o valor de Olá **Sim** para Olá **criar Azure conta Run As** opção e clique em Olá **criar** botão.  
   
    > [!NOTE]
    > Se escolher o toonot criar Olá a conta Run As, selecionando a opção de Olá **não**, será apresentada uma mensagem de aviso no Olá **adicionar conta de automatização** painel.  Enquanto a conta de Olá é criada e atribuída toohello **contribuinte** função na subscrição Olá, não terá uma identidade de autenticação correspondente dentro do seu serviço de diretório de subscrições e, consequentemente, sem acesso recursos na sua subscrição.  Isto irá impedir que todos os runbooks que referenciam esta conta de ser capaz de tooauthenticate e executar tarefas relativamente aos recursos do Azure Resource Manager.
    > 
    >

    <br>![Adicionar Aviso de Conta de Automatização](media/automation-create-aduser-account/add-automation-acct-properties-error.png)<br>  
7. Enquanto o Azure cria a conta de automatização Olá, pode controlar o progresso de Olá em **notificações** menu Olá.

Quando a criação da credencial de Olá Olá estiver concluída, terá de toocreate Olá de tooassociate um recurso de credencial conta de automatização com Olá conta de utilizador do AD criada anteriormente.  Lembre-se que apenas criamos conta de automatização Olá e não está associada a uma identidade de autenticação.  Executar passos de Olá descritos em Olá [recursos no artigo de automatização do Azure da credencial](automation-credentials.md#creating-a-new-credential-asset) e introduza o valor de Olá para **username** no formato de Olá **domínio \ utilizador**.

## <a name="use-hello-credential-in-a-runbook"></a>Utilizar credencial de Olá num runbook
Pode obter credenciais Olá num runbook utilizando Olá [Get-AutomationPSCredential](http://msdn.microsoft.com/library/dn940015.aspx) atividade e, em seguida, utilizá-la com [Add-AzureAccount](http://msdn.microsoft.com/library/azure/dn722528.aspx) tooconnect tooyour subscrição do Azure. Se Olá credencial for um administrador de várias subscrições do Azure, em seguida, deve utilizar também [Select-AzureSubscription](http://msdn.microsoft.com/library/dn495203.aspx) toospecify Olá correto. É mostrado no exemplo de Olá abaixo do Windows PowerShell que, normalmente, será apresentada na parte superior de Olá da maioria dos runbooks de automatização do Azure.

    $cred = Get-AutomationPSCredential –Name "myuseraccount.onmicrosoft.com"
    Add-AzureAccount –Credential $cred
    Select-AzureSubscription –SubscriptionName "My Subscription"

Deve repetir estas linhas após qualquer [ponto de verificação](http://technet.microsoft.com/library/dn469257.aspx#bk_Checkpoints) no runbook. Se Olá runbook está suspenso e, em seguida, retoma noutra função de trabalho, em seguida, esta terá de autenticação de Olá tooperform novamente.

## <a name="next-steps"></a>Passos Seguintes
* Olá, reveja Olá vários tipos de runbook e os passos para criar os seus próprios runbooks do seguinte artigo [tipos de runbook da automatização do Azure](automation-runbook-types.md)

