---
title: aaaCreate um grupo de utilizadores no Azure Active Directory | Microsoft Docs
description: Como toocreate um grupo no Azure Active Directory e adicionar membros toohello grupo
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="e5447-103">Crie um grupo e adicionar membros no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e5447-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e5447-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e5447-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="e5447-105">Portal Clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="e5447-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="e5447-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5447-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="e5447-107">Este artigo explica como toocreate e preencher um novo grupo no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e5447-107">This article explains how toocreate and populate a new group in Azure Active Directory.</span></span> <span data-ttu-id="e5447-108">Utilize tarefas de gestão de tooperform um grupo, tais como atribuir licenças ou permissões tooa número de utilizadores ou dispositivos em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="e5447-108">Use a group tooperform management tasks such as assigning licenses or permissions tooa number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="e5447-109">Como crio um grupo?</span><span class="sxs-lookup"><span data-stu-id="e5447-109">How do I create a group?</span></span>
1. <span data-ttu-id="e5447-110">Inicie sessão no toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de Olá.</span><span class="sxs-lookup"><span data-stu-id="e5447-110">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="e5447-111">Selecione **mais serviços**, introduza **grupos de utilizadores e** no Olá caixa de texto e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="e5447-111">Select **More services**, enter **User and groups** in hello text box, and then select **Enter**.</span></span>

   ![Gestão de utilizadores de abertura](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="e5447-113">No Olá **utilizadores e grupos** painel, selecione **todos os grupos**.</span><span class="sxs-lookup"><span data-stu-id="e5447-113">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Painel de grupos de Olá de abertura](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="e5447-115">No Olá **utilizadores e grupos - todos os grupos** painel, selecione de Olá **adicionar** comando.</span><span class="sxs-lookup"><span data-stu-id="e5447-115">On hello **Users and groups - All groups** blade, select hello **Add** command.</span></span>

   ![Selecionar o comando de adicionar Olá](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="e5447-117">No Olá **grupo** painel, adicionar um nome e descrição para o grupo de Olá.</span><span class="sxs-lookup"><span data-stu-id="e5447-117">On hello **Group** blade, add a name and description for hello group.</span></span>
6. <span data-ttu-id="e5447-118">tooselect membros tooadd toohello grupo, selecione **atribuído** no Olá **tipo de associação** caixa e, em seguida, selecione **membros**.</span><span class="sxs-lookup"><span data-stu-id="e5447-118">tooselect members tooadd toohello group, select **Assigned** in hello **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="e5447-119">Para obter mais informações sobre como toomanage Olá associação de um grupo de forma dinâmica, consulte [utilizar toocreate de atributos avançadas de regras de associação ao grupo](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e5447-119">For more information about how toomanage hello membership of a group dynamically, see [Using attributes toocreate advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

   ![Selecionar Membros tooadd](./media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="e5447-121">No Olá **membros** painel, selecione uma ou mais utilizadores ou dispositivos grupo de toohello tooadd e Olá selecione **selecione** botão na parte inferior de Olá de Olá painel tooadd-los toohello grupo.</span><span class="sxs-lookup"><span data-stu-id="e5447-121">On hello **Members** blade, select one or more users or devices tooadd toohello group and select hello **Select** button at hello bottom of hello blade tooadd them toohello group.</span></span> <span data-ttu-id="e5447-122">Olá **utilizador** filtros caixa Olá apresentação com base na correspondência sua entrada tooany parte um nome de utilizador ou dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e5447-122">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="e5447-123">Não existem carateres universais são aceites na caixa de.</span><span class="sxs-lookup"><span data-stu-id="e5447-123">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="e5447-124">Quando acabar de adicionar membros toohello grupo, selecione **criar** no Olá **grupo** painel.</span><span class="sxs-lookup"><span data-stu-id="e5447-124">When you finish adding members toohello group, select **Create** on hello **Group** blade.</span></span>    

   ![Criar a confirmação de grupo](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a><span data-ttu-id="e5447-126">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e5447-126">Next steps</span></span>
<span data-ttu-id="e5447-127">Estes artigos fornecem informações adicionais acerca do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e5447-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="e5447-128">Consulte os grupos existentes</span><span class="sxs-lookup"><span data-stu-id="e5447-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="e5447-129">Gerir as definições de um grupo</span><span class="sxs-lookup"><span data-stu-id="e5447-129">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="e5447-130">Gerir os membros de um grupo</span><span class="sxs-lookup"><span data-stu-id="e5447-130">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="e5447-131">Gerir membros de um grupo</span><span class="sxs-lookup"><span data-stu-id="e5447-131">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="e5447-132">Gerir regras dinâmicas para os utilizadores de um grupo</span><span class="sxs-lookup"><span data-stu-id="e5447-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
