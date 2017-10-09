---
title: aaaDedicated grupos no Azure Active Directory | Microsoft Docs
description: "Descrição geral de como dedicado de grupos de trabalho no Azure Active Directory e como são criados."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="2b278-103">Grupos dedicados no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b278-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="2b278-104">No Azure Active Directory (Azure AD), funcionalidade de grupos dedicados Olá cria e povoa automaticamente a associação de grupos do Azure AD predefinido.</span><span class="sxs-lookup"><span data-stu-id="2b278-104">In Azure Active Directory (Azure AD), hello dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="2b278-105">Não não possível adicionar membros dos grupos dedicados ou removida utilizando hello do Azure clássicos portal, cmdlets do Windows PowerShell, ou através de programação.</span><span class="sxs-lookup"><span data-stu-id="2b278-105">Members of dedicated groups cannot be added or removed using hello Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="2b278-106">Grupos dedicados requerem que está atribuída uma licença do Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="2b278-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="2b278-107">administrador de Olá que gere a regra de Olá num grupo</span><span class="sxs-lookup"><span data-stu-id="2b278-107">hello administrator who manages hello rule on a group</span></span>
> * <span data-ttu-id="2b278-108">todos os utilizadores que estão selecionados por Olá regra toobe um membro do grupo de Olá</span><span class="sxs-lookup"><span data-stu-id="2b278-108">all users who are selected by hello rule toobe a member of hello group</span></span>
>
>

<span data-ttu-id="2b278-109">**grupos de tooenable dedicado**</span><span class="sxs-lookup"><span data-stu-id="2b278-109">**tooenable dedicated groups**</span></span>

1. <span data-ttu-id="2b278-110">No Olá [portal clássico do Azure](https://manage.windowsazure.com), selecione **do Active Directory**e, em seguida, abra o diretório da sua organização.</span><span class="sxs-lookup"><span data-stu-id="2b278-110">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="2b278-111">Selecione Olá **grupos** separador e grupo, em seguida, abra Olá pretende tooedit.</span><span class="sxs-lookup"><span data-stu-id="2b278-111">Select hello **Groups** tab, and then open hello group you want tooedit.</span></span>
3. <span data-ttu-id="2b278-112">Selecione Olá **configurar** separador e, em seguida, defina **ative os grupos dedicados** demasiado**Sim**.</span><span class="sxs-lookup"><span data-stu-id="2b278-112">Select hello **Configure** tab, and then set **Enable Dedicated Groups** too**Yes**.</span></span>

<span data-ttu-id="2b278-113">Depois de Olá ativar grupos dedicados comutador está definido demasiado**Sim**, pode ativar a mais Olá diretório tooautomatically criar grupo dedicado de todos os utilizadores Olá por definição Olá **ativar "Todos os utilizadores" grupo** comutador demasiado**Sim**.</span><span class="sxs-lookup"><span data-stu-id="2b278-113">Once hello Enable Dedicated Groups switch is set too**Yes**, you can further enable hello directory tooautomatically create hello All Users dedicated group by setting hello **Enable “All Users” Group** switch too**Yes**.</span></span> <span data-ttu-id="2b278-114">Em seguida, também pode editar nome Olá deste grupo dedicado, introduzindo-Olá **nome a apresentar para "Todos os utilizadores" grupo** campo.</span><span class="sxs-lookup"><span data-stu-id="2b278-114">You can then also edit hello name of this dedicated group by typing it in hello **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="2b278-115">pode ser utilizado o grupo de todos os utilizadores Olá tooassign Olá mesmo permissões tooall Olá os utilizadores no seu diretório.</span><span class="sxs-lookup"><span data-stu-id="2b278-115">hello All Users group can be used tooassign hello same permissions tooall hello users in your directory.</span></span> <span data-ttu-id="2b278-116">Por exemplo, pode conceder todos os utilizadores na sua tooa de acesso de diretório aplicação SaaS através da atribuição de acesso para Olá todos os utilizadores dedicados grupo toothis aplicação.</span><span class="sxs-lookup"><span data-stu-id="2b278-116">For example, you can grant all users in your directory access tooa SaaS application by assigning access for hello All Users dedicated group toothis application.</span></span>

<span data-ttu-id="2b278-117">grupo de todos os utilizadores Olá dedicado inclui todos os utilizadores no diretório de Olá, incluindo utilizadores externos e de convidados.</span><span class="sxs-lookup"><span data-stu-id="2b278-117">hello dedicated All Users group includes all users in hello directory, including guests and external users.</span></span> <span data-ttu-id="2b278-118">Se precisar de um grupo que exclui os utilizadores externos, em seguida, pode conseguir isto ao criar um grupo com uma regra dinâmica baseadas em atributos como seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="2b278-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as hello following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="2b278-119">Para um grupo que exclua todos os convidados, utilize uma regra, como o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="2b278-119">For a group that excludes all Guests, use a rule such as hello following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="2b278-120">toolearn sobre como toocreate *avançadas* regras (regras que podem conter várias comparações) para filiação dinâmica em grupos, consulte [utilizar toocreate de atributos avançadas regras](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="2b278-120">toolearn about how toocreate *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes toocreate advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="2b278-121">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2b278-121">Next steps</span></span>
<span data-ttu-id="2b278-122">Estes artigos fornecem informações adicionais acerca do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2b278-122">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="2b278-123">Gerir o acesso tooresources com grupos do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b278-123">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="2b278-124">Índice de Artigos da Gestão da Aplicação no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b278-124">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="2b278-125">O que é o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2b278-125">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="2b278-126">Integrar as identidades no local ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b278-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
