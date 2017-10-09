---
title: "aaaNext passos para utilizar grupos de gestão de acesso | Microsoft Docs"
description: "Avançadas como-para gerir grupos de segurança e como toouse o recurso do tooa toomanage acesso estes grupos."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 44350a3c-8ea1-4da1-aaac-7fc53933dd21
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4fd55f893290fac3551a130f29bd12709cf551e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="37797-103">Gerir proprietários de um grupo</span><span class="sxs-lookup"><span data-stu-id="37797-103">Managing owners for a group</span></span>
<span data-ttu-id="37797-104">Após um proprietário de recursos tem atribuída a grupo do acesso tooa recursos tooan do Azure AD, associação de Olá do grupo de Olá é gerida pelo proprietário do grupo Olá.</span><span class="sxs-lookup"><span data-stu-id="37797-104">Once a resource owner has assigned access tooa resource tooan Azure AD group, hello membership of hello group is managed by hello group owner.</span></span> <span data-ttu-id="37797-105">proprietário do recurso Olá eficazmente delega Olá permissão tooassign utilizadores toohello toohello proprietário do recurso do grupo de Olá.</span><span class="sxs-lookup"><span data-stu-id="37797-105">hello resource owner effectively delegates hello permission tooassign users toohello resource toohello owner of hello group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37797-106">A Microsoft recomenda que gere o Azure AD através de Olá [Centro de administração do Azure AD](https://aad.portal.azure.com) no Olá portal do Azure em vez de utilizar Olá portal clássico do Azure referenciado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="37797-106">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 

## <a name="assigning-group-ownership"></a><span data-ttu-id="37797-107">Atribuir propriedade do grupo</span><span class="sxs-lookup"><span data-stu-id="37797-107">Assigning group ownership</span></span>
<span data-ttu-id="37797-108">**tooadd um grupo de tooa proprietário**</span><span class="sxs-lookup"><span data-stu-id="37797-108">**tooadd an owner tooa group**</span></span>

1. <span data-ttu-id="37797-109">No Olá [portal clássico do Azure](https://manage.windowsazure.com), selecione **do Active Directory**e, em seguida, abra o diretório da sua organização.</span><span class="sxs-lookup"><span data-stu-id="37797-109">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="37797-110">Selecione Olá **grupos** separador e grupo, em seguida, abra Olá que pretende que os proprietários de tooadd.</span><span class="sxs-lookup"><span data-stu-id="37797-110">Select hello **Groups** tab, and then open hello group that you want tooadd owners to.</span></span>
3. <span data-ttu-id="37797-111">Selecione **adicionar proprietários**.</span><span class="sxs-lookup"><span data-stu-id="37797-111">Select **Add Owners**.</span></span>
4. <span data-ttu-id="37797-112">No Olá **adicionar proprietários** página, o utilizador Olá Selecione se pretende tooadd como proprietário Olá deste grupo e, certifique-se de que este nome é adicionado toohello **selecionados** painel.</span><span class="sxs-lookup"><span data-stu-id="37797-112">On hello **Add owners** page, select hello user that you want tooadd as hello owner of this group, and make sure this name is added toohello **Selected** pane.</span></span>

<span data-ttu-id="37797-113">**tooremove um proprietário de um grupo**</span><span class="sxs-lookup"><span data-stu-id="37797-113">**tooremove an owner from a group**</span></span>

1. <span data-ttu-id="37797-114">No Olá [portal clássico do Azure](https://manage.windowsazure.com), selecione **do Active Directory**e, em seguida, abra o diretório da sua organização.</span><span class="sxs-lookup"><span data-stu-id="37797-114">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="37797-115">Selecione Olá **grupos** separador e, em seguida, abra Olá grupo que pretende tooremove um proprietário de.</span><span class="sxs-lookup"><span data-stu-id="37797-115">Select hello **Groups** tab, and then open hello group that you want tooremove an owner from.</span></span>
3. <span data-ttu-id="37797-116">Selecione Olá **proprietários** separador.</span><span class="sxs-lookup"><span data-stu-id="37797-116">Select hello **Owners** tab.</span></span>
4. <span data-ttu-id="37797-117">Proprietário de Olá Selecione se pretende tooremove deste grupo e, em seguida, selecione **remover**.</span><span class="sxs-lookup"><span data-stu-id="37797-117">Select hello owner that you want tooremove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="37797-118">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="37797-118">Additional information</span></span>
<span data-ttu-id="37797-119">Estes artigos fornecem informações adicionais acerca do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="37797-119">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="37797-120">Gerir o acesso tooresources com grupos do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37797-120">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="37797-121">Cmdlets do Azure Active Directory para configurar definições de grupo</span><span class="sxs-lookup"><span data-stu-id="37797-121">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="37797-122">Índice de Artigos da Gestão da Aplicação no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37797-122">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="37797-123">O que é o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="37797-123">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="37797-124">Integrar as identidades no local ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37797-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
