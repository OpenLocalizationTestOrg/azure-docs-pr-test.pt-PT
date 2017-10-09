---
title: "aaaManage acesso tooAzure faturação a utilização de funções | Microsoft Docs"
description: 
services: 
documentationcenter: 
author: vikramdesai01
manager: vikdesai
editor: 
tags: billing
ms.assetid: e4c4d136-2826-4938-868f-a7e67ff6b025
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: vikdesai
ms.openlocfilehash: 5937fac5ffa5ca204eb03a1dcbc5e800b3d5eb74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-toobilling-information-for-azure-using-role-based-access-control"></a>Gerir acesso toobilling informações para o Azure utilizando o controlo de acesso baseado em funções

Pode conceder acesso para o Azure toomembers de informações de faturação da sua equipa atribuindo um Olá seguir a subscrição de tooyour de funções de utilizador: administrador da conta, administrador de serviço, coadministrador, proprietário, Contribuidor, leitor, leitor e de faturação. Seria têm acesso toobilling informações no Olá [portal do Azure](https://portal.azure.com/), e podem utilizar Olá [APIs de faturação](billing-usage-rate-card-overview.md) tooprogrammatically obter faturas (uma vez optado por participar) e detalhes de utilização. Para obter mais informações sobre quem pode conceder funções e que funções podem fazer com que, consulte [funções no Azure RBAC](../active-directory/role-based-access-built-in-roles.md).

## <a name="opt-in"></a>Permitir que os utilizadores adicionais tooaccess faturas

Olá administrador da conta tem optar ativamente por participar no utilizando Olá [portal do Azure](https://portal.azure.com/) permitir acesso tooinvoices para outros utilizadores e através de API.

1. Como hello administrador da conta, selecione a sua subscrição do Olá [painel subscrições](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) no portal do Azure.

1. Selecione **faturas** e, em seguida, **aceder tooinvoices**.

    ![Captura de ecrã mostra como toodelegate aceder tooinvoices](./media/billing-manage-access/AA-optin.png)

1. Ativar **no** acesso Olá seguido de guardar as alterações de Olá, os utilizadores tooallow subscrição funções âmbito toodownload fatura.

    ![Captura de ecrã mostra-desativar toodelegate acesso tooinvoice](./media/billing-manage-access/AA-optinAllow.png)

Aceitar permite que o administrador de serviço, coadministrador, proprietário, Contribuidor, leitor e faturação leitor no faturas PDF do Olá subscrição toodownload no Olá portal do Azure. No entanto, faturas anteriores Dezembro de 2016 estão disponível toohello apenas o administrador de conta por agora.

Olá conta administrador também pode configurar faturas toohave enviadas por e-mail. toolearn mais, consulte [obter da sua fatura no e-mail](billing-download-azure-invoice-daily-usage-date.md).

## <a name="adding-users-toohello-billing-reader-role"></a>Adicionar a função de leitor de faturação de toohello de utilizadores

função de leitor de faturação Olá tem acesso só de leitura toosubscription as informações de faturação no portal do Azure e não tooservices acesso como VMs e as contas de armazenamento. Atribuir toosomeone de função de leitor de faturação Olá que necessita de aceder às informações de faturação de subscrição de toohello, mas não Olá capacidade toomanage Azure serviços. Esta função é adequada para os utilizadores numa organização que efetuar apenas financeiro e de custo de gestão de subscrições do Azure.

1. Selecione a sua subscrição do Olá [painel subscrições](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) no portal do Azure.

1. Selecione **(IAM) do controlo de acesso** e, em seguida, clique em **adicionar**.

    ![Captura de ecrã mostra IAM no painel de subscrição de Olá](./media/billing-manage-access/select-iam.PNG)

1. Escolha **faturação leitor** no Olá **selecionar uma função** página.

    ![Captura de ecrã mostra o leitor de faturação na vista de pop-up Olá](./media/billing-manage-access/select-roles.PNG)

1. Tipo de correio eletrónico Olá utilizador Olá pretende tooinvite, em seguida, clique em **OK** convite de Olá toosend.

    ![Captura de ecrã que mostra tooenter e-mail tooinvite alguém](./media/billing-manage-access/add-user.PNG)

1. Siga as instruções em toolog de e-mail de convite de Olá na como um leitor de faturação.

    ![Captura de ecrã que mostra que Olá leitor de faturação pode ver no portal do Azure](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> funcionalidade de leitor de faturação Olá está em pré-visualização e ainda não suporta subscrições de empresa (EA) ou de nuvens não global.

## <a name="adding-users-tooother-roles"></a>Adicionar utilizadores tooother funções

Os utilizadores nas outras funções, tais como proprietário ou contribuinte, podem aceder a informações de faturação não apenas, mas, bem como os serviços do Azure. toomanage destas funções, consulte [adicionar ou alterar funções de administrador do Azure que gerem serviços ou de subscrição de Olá](billing-add-change-azure-subscription-administrator.md).

## <a name="who-can-access-hello-account-centerhttpsaccountwindowsazurecom"></a>Quem pode aceder a Olá [Centro de contas](https://account.windowsazure.com)?

Olá apenas a conta de administrador pode iniciar sessão no Centro de contas toohello. Olá administrador de conta é proprietário legal do Olá da subscrição Olá. Por predefinição, Olá quem inscreveu no ou comprou Olá subscrição do Azure é Olá administrador de conta, a menos que Olá [propriedade de subscrição foi transferida](billing-subscription-transfer.md) toosomebody pessoa. Olá administrador da conta pode criar subscrições, cancelar subscrições, alterar o endereço para faturação Olá para uma subscrição e gerir políticas de acesso para a subscrição de Olá.

## <a name="need-help-contact-support"></a>Precisa de ajuda? Contacte o suporte.

Se ainda tiver mais perguntas, [contacte o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.
