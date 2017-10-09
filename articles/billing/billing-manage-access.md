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
# <a name="manage-access-toobilling-information-for-azure-using-role-based-access-control"></a><span data-ttu-id="bf6fd-102">Gerir acesso toobilling informações para o Azure utilizando o controlo de acesso baseado em funções</span><span class="sxs-lookup"><span data-stu-id="bf6fd-102">Manage access toobilling information for Azure using role-based access control</span></span>

<span data-ttu-id="bf6fd-103">Pode conceder acesso para o Azure toomembers de informações de faturação da sua equipa atribuindo um Olá seguir a subscrição de tooyour de funções de utilizador: administrador da conta, administrador de serviço, coadministrador, proprietário, Contribuidor, leitor, leitor e de faturação.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-103">You can grant access for Azure billing information toomembers of your team by assigning one of hello following user roles tooyour subscription: Account Administrator, Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader.</span></span> <span data-ttu-id="bf6fd-104">Seria têm acesso toobilling informações no Olá [portal do Azure](https://portal.azure.com/), e podem utilizar Olá [APIs de faturação](billing-usage-rate-card-overview.md) tooprogrammatically obter faturas (uma vez optado por participar) e detalhes de utilização.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-104">They would have access toobilling information in hello [Azure portal](https://portal.azure.com/), and they can use hello [Billing APIs](billing-usage-rate-card-overview.md) tooprogrammatically get invoices (once opted-in) and usage details.</span></span> <span data-ttu-id="bf6fd-105">Para obter mais informações sobre quem pode conceder funções e que funções podem fazer com que, consulte [funções no Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="bf6fd-105">For more information about who can grant roles, and which roles can do what, see [Roles in Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span></span>

## <span data-ttu-id="bf6fd-106"><a name="opt-in"></a>Permitir que os utilizadores adicionais tooaccess faturas</span><span class="sxs-lookup"><span data-stu-id="bf6fd-106"><a name="opt-in"></a> Allowing additional users tooaccess invoices</span></span>

<span data-ttu-id="bf6fd-107">Olá administrador da conta tem optar ativamente por participar no utilizando Olá [portal do Azure](https://portal.azure.com/) permitir acesso tooinvoices para outros utilizadores e através de API.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-107">hello Account Administrator must opt in using hello [Azure portal](https://portal.azure.com/) allow access tooinvoices for other users and via API.</span></span>

1. <span data-ttu-id="bf6fd-108">Como hello administrador da conta, selecione a sua subscrição do Olá [painel subscrições](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-108">As hello Account Administrator, select your subscription from hello [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="bf6fd-109">Selecione **faturas** e, em seguida, **aceder tooinvoices**.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-109">Select **Invoices** and then **Access tooinvoices**.</span></span>

    ![Captura de ecrã mostra como toodelegate aceder tooinvoices](./media/billing-manage-access/AA-optin.png)

1. <span data-ttu-id="bf6fd-111">Ativar **no** acesso Olá seguido de guardar as alterações de Olá, os utilizadores tooallow subscrição funções âmbito toodownload fatura.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-111">Turn **On** hello access followed by saving hello changes, tooallow users in subscription scoped roles toodownload invoice.</span></span>

    ![Captura de ecrã mostra-desativar toodelegate acesso tooinvoice](./media/billing-manage-access/AA-optinAllow.png)

<span data-ttu-id="bf6fd-113">Aceitar permite que o administrador de serviço, coadministrador, proprietário, Contribuidor, leitor e faturação leitor no faturas PDF do Olá subscrição toodownload no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-113">Opting in allows Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader on hello subscription toodownload PDF invoices in hello Azure portal.</span></span> <span data-ttu-id="bf6fd-114">No entanto, faturas anteriores Dezembro de 2016 estão disponível toohello apenas o administrador de conta por agora.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-114">However, invoices older than December 2016 are available only toohello Account Administrator for now.</span></span>

<span data-ttu-id="bf6fd-115">Olá conta administrador também pode configurar faturas toohave enviadas por e-mail.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-115">hello Account Administrator can also configure toohave invoices sent via email.</span></span> <span data-ttu-id="bf6fd-116">toolearn mais, consulte [obter da sua fatura no e-mail](billing-download-azure-invoice-daily-usage-date.md).</span><span class="sxs-lookup"><span data-stu-id="bf6fd-116">toolearn more, see [Get your invoice in email](billing-download-azure-invoice-daily-usage-date.md).</span></span>

## <a name="adding-users-toohello-billing-reader-role"></a><span data-ttu-id="bf6fd-117">Adicionar a função de leitor de faturação de toohello de utilizadores</span><span class="sxs-lookup"><span data-stu-id="bf6fd-117">Adding users toohello Billing Reader role</span></span>

<span data-ttu-id="bf6fd-118">função de leitor de faturação Olá tem acesso só de leitura toosubscription as informações de faturação no portal do Azure e não tooservices acesso como VMs e as contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-118">hello Billing Reader role has read-only access toosubscription billing information in Azure portal, and no access tooservices such as VMs and storage accounts.</span></span> <span data-ttu-id="bf6fd-119">Atribuir toosomeone de função de leitor de faturação Olá que necessita de aceder às informações de faturação de subscrição de toohello, mas não Olá capacidade toomanage Azure serviços.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-119">Assign hello Billing Reader role toosomeone that needs access toohello subscription billing information but not hello ability toomanage Azure services.</span></span> <span data-ttu-id="bf6fd-120">Esta função é adequada para os utilizadores numa organização que efetuar apenas financeiro e de custo de gestão de subscrições do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-120">This role is appropriate for users in an organization who only perform financial and cost management for Azure subscriptions.</span></span>

1. <span data-ttu-id="bf6fd-121">Selecione a sua subscrição do Olá [painel subscrições](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-121">Select your subscription from hello [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="bf6fd-122">Selecione **(IAM) do controlo de acesso** e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-122">Select **Access control (IAM)** and then click **Add**.</span></span>

    ![Captura de ecrã mostra IAM no painel de subscrição de Olá](./media/billing-manage-access/select-iam.PNG)

1. <span data-ttu-id="bf6fd-124">Escolha **faturação leitor** no Olá **selecionar uma função** página.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-124">Choose **Billing Reader** in hello **Select a role** page.</span></span>

    ![Captura de ecrã mostra o leitor de faturação na vista de pop-up Olá](./media/billing-manage-access/select-roles.PNG)

1. <span data-ttu-id="bf6fd-126">Tipo de correio eletrónico Olá utilizador Olá pretende tooinvite, em seguida, clique em **OK** convite de Olá toosend.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-126">Type hello email for hello user you want tooinvite, then click **OK** toosend hello invitation.</span></span>

    ![Captura de ecrã que mostra tooenter e-mail tooinvite alguém](./media/billing-manage-access/add-user.PNG)

1. <span data-ttu-id="bf6fd-128">Siga as instruções em toolog de e-mail de convite de Olá na como um leitor de faturação.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-128">Follow instructions in hello invite email toolog in as a Billing Reader.</span></span>

    ![Captura de ecrã que mostra que Olá leitor de faturação pode ver no portal do Azure](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> <span data-ttu-id="bf6fd-130">funcionalidade de leitor de faturação Olá está em pré-visualização e ainda não suporta subscrições de empresa (EA) ou de nuvens não global.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-130">hello Billing Reader feature is in preview, and does not yet support enterprise (EA) subscriptions or non-global clouds.</span></span>

## <a name="adding-users-tooother-roles"></a><span data-ttu-id="bf6fd-131">Adicionar utilizadores tooother funções</span><span class="sxs-lookup"><span data-stu-id="bf6fd-131">Adding users tooother roles</span></span>

<span data-ttu-id="bf6fd-132">Os utilizadores nas outras funções, tais como proprietário ou contribuinte, podem aceder a informações de faturação não apenas, mas, bem como os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-132">Users in other roles, such as Owner or Contributor, can access not just billing information, but Azure services as well.</span></span> <span data-ttu-id="bf6fd-133">toomanage destas funções, consulte [adicionar ou alterar funções de administrador do Azure que gerem serviços ou de subscrição de Olá](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="bf6fd-133">toomanage these roles, see [Add or change Azure administrator roles that manage hello subscription or services](billing-add-change-azure-subscription-administrator.md).</span></span>

## <a name="who-can-access-hello-account-centerhttpsaccountwindowsazurecom"></a><span data-ttu-id="bf6fd-134">Quem pode aceder a Olá [Centro de contas](https://account.windowsazure.com)?</span><span class="sxs-lookup"><span data-stu-id="bf6fd-134">Who can access hello [Account Center](https://account.windowsazure.com)?</span></span>

<span data-ttu-id="bf6fd-135">Olá apenas a conta de administrador pode iniciar sessão no Centro de contas toohello.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-135">Only hello Account Administrator can log in toohello Account center.</span></span> <span data-ttu-id="bf6fd-136">Olá administrador de conta é proprietário legal do Olá da subscrição Olá.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-136">hello Account Administrator is hello legal owner of hello subscription.</span></span> <span data-ttu-id="bf6fd-137">Por predefinição, Olá quem inscreveu no ou comprou Olá subscrição do Azure é Olá administrador de conta, a menos que Olá [propriedade de subscrição foi transferida](billing-subscription-transfer.md) toosomebody pessoa.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-137">By default, hello person who signed up for or bought hello Azure subscription is hello Account Administrator, unless hello [subscription ownership was transferred](billing-subscription-transfer.md) toosomebody else.</span></span> <span data-ttu-id="bf6fd-138">Olá administrador da conta pode criar subscrições, cancelar subscrições, alterar o endereço para faturação Olá para uma subscrição e gerir políticas de acesso para a subscrição de Olá.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-138">hello Account Administrator can create subscriptions, cancel subscriptions, change hello billing address for a subscription, and manage access policies for hello subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="bf6fd-139">Precisa de ajuda?</span><span class="sxs-lookup"><span data-stu-id="bf6fd-139">Need help?</span></span> <span data-ttu-id="bf6fd-140">Contacte o suporte.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-140">Contact support.</span></span>

<span data-ttu-id="bf6fd-141">Se ainda tiver mais perguntas, [contacte o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.</span><span class="sxs-lookup"><span data-stu-id="bf6fd-141">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
