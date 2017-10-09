---
title: "Sincronização do Azure AD Connect: Ativar Reciclagem AD | Microsoft Docs"
description: "Este tópico recomenda a utilização de Olá da funcionalidade de reciclagem do AD com o Azure AD Connect."
services: active-directory
keywords: "Reciclagem do AD, a eliminação acidental, âncora de origem"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a><span data-ttu-id="b04ca-104">Sincronização do Azure AD Connect: Ativar Reciclagem do AD</span><span class="sxs-lookup"><span data-stu-id="b04ca-104">Azure AD Connect sync: Enable AD recycle bin</span></span>
<span data-ttu-id="b04ca-105">Recomenda-se que ative a funcionalidade de reciclagem Olá AD para os diretórios de Active Directory no local, que são sincronizado tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="b04ca-105">It is recommended that you enable hello AD Recycle Bin feature for your on-premises Active Directories, which are synchronized tooAzure AD.</span></span> 

<span data-ttu-id="b04ca-106">Caso o tenha eliminado acidentalmente um local objeto de utilizador do AD e restaure-la utilizando a funcionalidade de Olá, Azure AD restaura objeto de utilizador do Azure AD de Olá correspondente.</span><span class="sxs-lookup"><span data-stu-id="b04ca-106">If you accidentally deleted an on-premises AD user object and restore it using hello feature, Azure AD restores hello corresponding Azure AD user object.</span></span>  <span data-ttu-id="b04ca-107">Para obter informações sobre a funcionalidade de reciclagem Olá AD, consulte tooarticle [descrição geral do cenário para restaurar eliminar objetos do Active Directory](https://technet.microsoft.com/library/dd379542.aspx).</span><span class="sxs-lookup"><span data-stu-id="b04ca-107">For information about hello AD Recycle Bin feature, refer tooarticle [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx).</span></span>

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a><span data-ttu-id="b04ca-108">Benefícios da ativação Olá AD Reciclagem</span><span class="sxs-lookup"><span data-stu-id="b04ca-108">Benefits of enabling hello AD recycle bin</span></span>
<span data-ttu-id="b04ca-109">Esta funcionalidade ajuda-o com o restauro de objetos de utilizador do Azure AD, Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="b04ca-109">This feature helps with restoring Azure AD user objects by doing hello following:</span></span>

* <span data-ttu-id="b04ca-110">Caso o tenha eliminado acidentalmente um local objeto de utilizador do AD, objeto de utilizador do Azure AD correspondente Olá será eliminado no Olá próximo ciclo de sincronização.</span><span class="sxs-lookup"><span data-stu-id="b04ca-110">If you accidentally deleted an on-premises AD user object, hello corresponding Azure AD user object will be deleted in hello next sync cycle.</span></span> <span data-ttu-id="b04ca-111">Por predefinição, do Azure AD mantém o objeto de utilizador do Azure AD Olá eliminado no estado de eliminação de forma recuperável durante 30 dias.</span><span class="sxs-lookup"><span data-stu-id="b04ca-111">By default, Azure AD keeps hello deleted Azure AD user object in soft-deleted state for 30 days.</span></span>

* <span data-ttu-id="b04ca-112">Se tiver no local ativada a funcionalidade de reciclagem do AD, pode restaurar Olá eliminado no local o objeto de utilizador do AD sem alterar o valor de âncora de origem.</span><span class="sxs-lookup"><span data-stu-id="b04ca-112">If you have on-premises AD Recycle Bin feature enabled, you can restore hello deleted on-premises AD user object without changing its Source Anchor value.</span></span> <span data-ttu-id="b04ca-113">Quando Olá recuperados no local o objeto de utilizador do AD está sincronizado tooAzure AD, do Azure AD irá restaurar Olá correspondente eliminados de forma recuperável objeto de utilizador do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b04ca-113">When hello recovered on-premises AD user object is synchronized tooAzure AD, Azure AD will restore hello corresponding soft-deleted Azure AD user object.</span></span> <span data-ttu-id="b04ca-114">Para obter informações sobre o atributo âncora de origem, consulte tooarticle [do Azure AD Connect: conceitos de Design](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span><span class="sxs-lookup"><span data-stu-id="b04ca-114">For information about Source Anchor attribute, refer tooarticle [Azure AD Connect: Design concepts](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span></span>

* <span data-ttu-id="b04ca-115">Se não tiver no local AD reciclar funcionalidade de reciclagem ativada, poderá ser necessário toocreate um AD utilizador objeto tooreplace Olá objeto eliminado.</span><span class="sxs-lookup"><span data-stu-id="b04ca-115">If you do not have on-premises AD Recycle Bin feature enabled, you may be required toocreate an AD user object tooreplace hello deleted object.</span></span> <span data-ttu-id="b04ca-116">Se serviço sincronização do Azure AD Connect toouse configurado gerado pelo sistema AD atributo (por exemplo, ObjectGuid) para o atributo de âncora de origem Olá, hello acabada de criar objeto de utilizador do AD será não ter Olá mesmo valor de âncora de origem como Olá eliminou o objeto de utilizador do AD.</span><span class="sxs-lookup"><span data-stu-id="b04ca-116">If Azure AD Connect Synchronization Service is configured toouse system-generated AD attribute (such as ObjectGuid) for hello Source Anchor attribute, hello newly created AD user object will not have hello same Source Anchor value as hello deleted AD user object.</span></span> <span data-ttu-id="b04ca-117">Quando Olá criado recentemente AD para o objeto de utilizador é sincronizado tooAzure AD, do Azure AD cria um novo objeto de utilizador do Azure AD em vez de restaurar o objeto de utilizador do Azure AD Olá eliminados de forma recuperável.</span><span class="sxs-lookup"><span data-stu-id="b04ca-117">When hello newly created AD user object is synchronized tooAzure AD, Azure AD creates a new Azure AD user object instead of restoring hello soft-deleted Azure AD user object.</span></span>

> [!NOTE]
> <span data-ttu-id="b04ca-118">Por predefinição, do Azure AD mantém eliminar objetos de utilizador do Azure AD no estado de eliminação de forma recuperável durante 30 dias antes de estes sejam eliminados permanentemente.</span><span class="sxs-lookup"><span data-stu-id="b04ca-118">By default, Azure AD keeps deleted Azure AD user objects in soft-deleted state for 30 days before they are permanently deleted.</span></span> <span data-ttu-id="b04ca-119">No entanto, os administradores podem acelerar a eliminação de Olá desses objetos.</span><span class="sxs-lookup"><span data-stu-id="b04ca-119">However, administrators can accelerate hello deletion of such objects.</span></span> <span data-ttu-id="b04ca-120">Depois de objetos de Olá são eliminados definitivamente, já não podem ser recuperados, mesmo quando no local é ativada a funcionalidade de reciclagem do AD.</span><span class="sxs-lookup"><span data-stu-id="b04ca-120">Once hello objects are permanently deleted, they can no longer be recovered, even if on-premises AD Recycle Bin feature is enabled.</span></span>



## <a name="next-steps"></a><span data-ttu-id="b04ca-121">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b04ca-121">Next steps</span></span>
<span data-ttu-id="b04ca-122">**Tópicos de descrição geral**</span><span class="sxs-lookup"><span data-stu-id="b04ca-122">**Overview topics**</span></span>

* [<span data-ttu-id="b04ca-123">Sincronização do Azure AD Connect: Noções e personalizar a sincronização</span><span class="sxs-lookup"><span data-stu-id="b04ca-123">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="b04ca-124">Integrar as identidades no local ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b04ca-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
