---
title: "aaaAdd proprietários e os utilizadores no Azure DevTest Labs | Microsoft Docs"
description: "Adicionar utilizadores e proprietários no Azure DevTest Labs utilizando Olá portal do Azure ou o PowerShell"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a>Adicionar utilizadores e proprietários no Azure DevTest Labs
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

O acesso no Azure DevTest Labs é controlado pelo [controlo de acesso em funções do Azure (RBAC)](../active-directory/role-based-access-control-what-is.md). Utilizar o RBAC, pode segregar funções na sua equipa no *funções* onde conceder apenas Olá quantidade de acesso necessários toousers tooperform as respetivas tarefas. Três destas funções do RBAC são *proprietário*, *DevTest Labs utilizador*, e *contribuinte*. Neste artigo, saiba o que ações podem ser efetuadas em cada um dos Olá três principais funções do RBAC. A partir daí, saiba como laboratório do tooadd utilizadores tooa - ambos através de Olá portal e através de um script do PowerShell e como os utilizadores de tooadd no Olá ao nível da subscrição.

## <a name="actions-that-can-be-performed-in-each-role"></a>Ações que podem ser executadas em cada função
Existem três funções principais que pode atribuir um utilizador:

* Proprietário
* DevTest Labs utilizador
* Contribuinte

Olá tabela que se segue ilustra as ações de Olá que podem ser efetuadas pelos utilizadores em cada uma destas funções:

| **Podem efetuar ações os utilizadores com esta função** | **DevTest Labs utilizador** | **Proprietário** | **Contribuinte** |
| --- | --- | --- | --- |
| **Tarefas de laboratório** | | | |
| Adicionar o laboratório de tooa de utilizadores |Não |Sim |Não |
| Atualizar as definições de custos |Não |Sim |Sim |
| **Tarefas de base de VM** | | | |
| Adicionar e remover imagens personalizadas |Não |Sim |Sim |
| Adicionar, atualizar e eliminar as fórmulas |Sim |Sim |Sim |
| Imagens da lista branca Azure Marketplace |Não |Sim |Sim |
| **Tarefas VM** | | | |
| Criar VMs |Sim |Sim |Sim |
| Iniciar, parar e eliminar as VMs |Apenas as VMs criadas por utilizador Olá |Sim |Sim |
| Atualizar as políticas de VM |Não |Sim |Sim |
| Adicionar/remover discos de dados do VMs |Apenas as VMs criadas por utilizador Olá |Sim |Sim |
| **Tarefas de artefactos** | | | |
| Adicionar e remover repositórios de artefactos |Não |Sim |Sim |
| Aplicam-se de artefactos |Sim |Sim |Sim |

> [!NOTE]
> Quando um utilizador cria uma VM, esse utilizador é atribuído automaticamente toohello **proprietário** função de Olá criada a VM.
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a>Adicionar um proprietário ou o utilizador ao nível de laboratório de Olá
Os proprietários e os utilizadores podem ser adicionados ao nível do laboratório Olá através de Olá portal do Azure. Isto inclui os utilizadores externos com um [conta Microsoft (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).
Olá, os seguintes passos guiá-lo através do processo de Olá de adição de um laboratório de tooa proprietário ou utilizador no Azure DevTest Labs:

1. Inicie sessão no toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de Olá.
3. Na lista de Olá de laboratórios, selecione laboratório pretendido Olá.
4. No painel do laboratório de Olá, selecione **configuração**. 
5. No Olá **configuração** painel, selecione **utilizadores**.
6. No Olá **utilizadores** painel, selecione **+ adicionar**.
   
    ![Adicionar utilizador](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. No Olá **selecionar uma função** painel, a função pretendida Olá selecione. Olá secção [ações que podem ser executadas em cada função](#actions-that-can-be-performed-in-each-role) listas Olá várias ações que podem ser efetuadas pelos utilizadores nas funções de proprietário, utilizador de DevTest e contribuinte Olá.
8. No Olá **adicionar utilizadores** painel, introduza o endereço de correio eletrónico Olá ou nome de utilizador de Olá pretende tooadd na função Olá que especificou. Se não é possível localizar o utilizador Olá, uma mensagem de erro explica problema Olá. Se Olá utilizador for encontrado, esse utilizador é listado e seleccionado. 
9. Selecione **selecione**.
10. Selecione **OK** tooclose Olá **adicionar acesso** painel.
11. Quando regressar toohello **utilizadores** painel, Olá utilizador foi adicionado.  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a>Adicionar um laboratório de tooa utilizador externo através do PowerShell
Além disso tooadding utilizadores Olá portal do Azure, pode adicionar um laboratório de tooyour de utilizador externo utilizando um script do PowerShell. Olá simplesmente seguinte o exemplo, modificar os valores de parâmetros de Olá em Olá **valores toochange** comentário.
Pode obter Olá `subscriptionId`, `labResourceGroup`, e `labName` valores a partir do painel de laboratório Olá no Olá portal do Azure.

> [!NOTE]
> script de exemplo de Olá parte do princípio de que Olá especificado utilizador foi adicionado como um toohello de convidado do Active Directory e irá falhar se não for esse caso de Olá. tooadd um utilizador não se encontra na Olá laboratório de tooa do Active Directory, utilize Olá tooassign portal do Azure Olá tooa a função de utilizador, conforme ilustrado na secção de Olá, [adicionar um proprietário ou o utilizador ao nível de laboratório de Olá](#add-an-owner-or-user-at-the-lab-level).   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a>Adicionar um proprietário ou o utilizador ao nível da subscrição de Olá
Permissões do Azure são propagadas do âmbito de toochild âmbito principal no Azure. Por conseguinte, os proprietários de uma subscrição do Azure que contém laboratórios são automaticamente os proprietários desses laboratórios. Também possuem Olá VMs e outros recursos criados por utilizadores do laboratório de Olá e Olá serviço Azure DevTest Labs. 

Pode adicionar o laboratório de tooa proprietários adicionais através do painel do laboratório de Olá no Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). No entanto, Olá Adicionar âmbito do proprietário da administração é mais restritos ao âmbito do proprietário da subscrição Olá. Por exemplo, Olá adicionada proprietários não têm acesso total toosome Olá de recursos de que são criados na subscrição Olá por Olá serviço DevTest Labs. 

tooadd tooan um proprietário subscrição do Azure, siga estes passos:

1. Inicie sessão no toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecione **mais serviços**e, em seguida, selecione **subscrições** da lista de Olá.
3. Selecione a subscrição de Olá assim o desejar.
4. Selecione **acesso** ícone. 
   
    ![Utilizadores de acesso](./media/devtest-lab-add-devtest-user/access-users.png)
5. No Olá **utilizadores** painel, selecione **adicionar**.
   
    ![Adicionar utilizador](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. No Olá **selecionar uma função** painel, selecione **proprietário**.
7. No Olá **adicionar utilizadores** painel, introduza o endereço de correio eletrónico Olá ou nome de utilizador de Olá pretende tooadd como um proprietário. Se não é possível localizar o utilizador Olá, receberá uma mensagem de erro explicar problema Olá. Se for encontrado o utilizador Olá, esse utilizador é apresentado em Olá **utilizador** caixa de texto.
8. Selecione o nome de utilizador localizado Olá.
9. Selecione **selecione**.
10. Selecione **OK** tooclose Olá **adicionar acesso** painel.
11. Quando regressar toohello **utilizadores** painel, Olá utilizador foi adicionado como um proprietário. Este utilizador é agora um proprietário de quaisquer laboratórios criado pertencentes a esta subscrição e, por conseguinte, ser capaz de tooperform tarefas de proprietário. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

