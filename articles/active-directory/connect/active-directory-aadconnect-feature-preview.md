---
title: "Do Azure AD Connect: As funcionalidades pré-visualização | Microsoft Docs"
description: "Este tópico descreve em mais funcionalidades de detalhe que estão na pré-visualização no Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a><span data-ttu-id="8c63a-103">Obter mais detalhes sobre as funcionalidades em pré-visualização</span><span class="sxs-lookup"><span data-stu-id="8c63a-103">More details about features in preview</span></span>
<span data-ttu-id="8c63a-104">Este tópico descreve como toouse as funcionalidades atualmente em pré-visualização.</span><span class="sxs-lookup"><span data-stu-id="8c63a-104">This topic describes how toouse features currently in preview.</span></span>

## <a name="group-writeback"></a><span data-ttu-id="8c63a-105">Repetição de escrita do grupo</span><span class="sxs-lookup"><span data-stu-id="8c63a-105">Group writeback</span></span>
<span data-ttu-id="8c63a-106">opção de Olá para repetição de escrita do grupo em funcionalidades opcionais permite-lhe toowriteback **grupos do Office 365** tooa floresta com o Exchange instalado.</span><span class="sxs-lookup"><span data-stu-id="8c63a-106">hello option for group writeback in optional features allows you toowriteback **Office 365 Groups** tooa forest with Exchange installed.</span></span> <span data-ttu-id="8c63a-107">Este é um grupo que é controlado sempre na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="8c63a-107">This is a group that is always mastered in hello cloud.</span></span> <span data-ttu-id="8c63a-108">Se tiver o Exchange no local, em seguida, pode escrever novamente este grupos tooon local para que os utilizadores com uma caixa de correio do Exchange no local podem enviar e receber e-mails destes grupos.</span><span class="sxs-lookup"><span data-stu-id="8c63a-108">If you have Exchange on-premises, then you can write back these groups tooon-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span></span>

<span data-ttu-id="8c63a-109">Mais informações sobre grupos do Office 365 e como toouse-los podem ser encontrados [aqui](http://aka.ms/O365g).</span><span class="sxs-lookup"><span data-stu-id="8c63a-109">More information about Office 365 Groups and how toouse them can be found [here](http://aka.ms/O365g).</span></span>

<span data-ttu-id="8c63a-110">Um grupo do Office 365 é representado como um grupo de distribuição no local do AD DS.</span><span class="sxs-lookup"><span data-stu-id="8c63a-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span></span> <span data-ttu-id="8c63a-111">O servidor do Exchange no local tem de ser no Exchange 2013 atualização cumulativa 8 (lançada em Março de 2015) ou o Exchange 2016 toorecognize este novo tipo de grupo.</span><span class="sxs-lookup"><span data-stu-id="8c63a-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 toorecognize this new group type.</span></span>

<span data-ttu-id="8c63a-112">**Notas durante a pré-visualização de Olá**</span><span class="sxs-lookup"><span data-stu-id="8c63a-112">**Notes during hello preview**</span></span>

* <span data-ttu-id="8c63a-113">atributo de livro de endereços de Olá não for preenchido atualmente em pré-visualização Olá.</span><span class="sxs-lookup"><span data-stu-id="8c63a-113">hello address book attribute is currently not populated in hello preview.</span></span> <span data-ttu-id="8c63a-114">Sem este atributo, o grupo de Olá não estiver visível na Olá GAL.</span><span class="sxs-lookup"><span data-stu-id="8c63a-114">Without this attribute, hello group is not visible in hello GAL.</span></span> <span data-ttu-id="8c63a-115">Olá toopopulate de forma mais fácil este atributo é toouse Olá do Exchange PowerShell cmdlet `update-recipient`.</span><span class="sxs-lookup"><span data-stu-id="8c63a-115">hello easiest way toopopulate this attribute is toouse hello Exchange PowerShell cmdlet `update-recipient`.</span></span>
* <span data-ttu-id="8c63a-116">Só é florestas com o esquema do Exchange de Olá são destinos válidos para grupos.</span><span class="sxs-lookup"><span data-stu-id="8c63a-116">Only forests with hello Exchange schema are valid targets for groups.</span></span> <span data-ttu-id="8c63a-117">Não se foi detetado nenhum Exchange, em seguida, repetição de escrita do grupo não é possível tooenable.</span><span class="sxs-lookup"><span data-stu-id="8c63a-117">If no Exchange was detected, then group writeback is not possible tooenable.</span></span>
* <span data-ttu-id="8c63a-118">Apenas floresta única organização implementações do Exchange são atualmente suportadas.</span><span class="sxs-lookup"><span data-stu-id="8c63a-118">Only single-forest Exchange organization deployments are currently supported.</span></span> <span data-ttu-id="8c63a-119">Se tiver mais do que um Exchange organização no local, em seguida, terá de uma solução de GALSync no local para estes grupos tooappear sua noutras florestas.</span><span class="sxs-lookup"><span data-stu-id="8c63a-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups tooappear in your other forests.</span></span>
* <span data-ttu-id="8c63a-120">funcionalidade de repetição de escrita do grupo de Olá não processa os grupos de segurança ou grupos de distribuição.</span><span class="sxs-lookup"><span data-stu-id="8c63a-120">hello Group writeback feature does not handle security groups or distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="8c63a-121">Uma subscrição tooAzure AD Premium é necessário para a repetição de escrita do grupo.</span><span class="sxs-lookup"><span data-stu-id="8c63a-121">A subscription tooAzure AD Premium is required for group writeback.</span></span>
> 
>

## <a name="user-writeback"></a><span data-ttu-id="8c63a-122">Repetição de escrita do utilizador</span><span class="sxs-lookup"><span data-stu-id="8c63a-122">User writeback</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8c63a-123">Olá funcionalidade de pré-visualização de repetição de escrita do utilizador foi removida no Olá Agosto de 2015 update tooAzure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8c63a-123">hello user writeback preview feature was removed in hello August 2015 update tooAzure AD Connect.</span></span> <span data-ttu-id="8c63a-124">Se tiver ativado o-lo, deve desativar esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="8c63a-124">If you have enabled it, then you should disable this feature.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="8c63a-125">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8c63a-125">Next steps</span></span>
<span data-ttu-id="8c63a-126">Continuar a [instalação personalizada do Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="8c63a-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

<span data-ttu-id="8c63a-127">Saiba mais sobre como [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="8c63a-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
