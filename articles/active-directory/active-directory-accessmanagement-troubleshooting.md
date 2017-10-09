---
title: "aaaTroubleshooting a filiação dinâmica para grupos | Microsoft Docs"
description: "Sugestões de resolução de problemas para a filiação dinâmica para grupos no Azure AD."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="31d7b-103">Resolver problemas de associações dinâmicas a grupos</span><span class="sxs-lookup"><span data-stu-id="31d7b-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="31d7b-104">**Posso configurar uma regra num grupo, mas não associações for atualizadas no grupo de Olá**</span><span class="sxs-lookup"><span data-stu-id="31d7b-104">**I configured a rule on a group but no memberships get updated in hello group**</span></span><br/><span data-ttu-id="31d7b-105">Certifique-se de que Olá **ativar gestão de grupo delegada** definição está definida demasiado**Sim** no Olá **configurar** separador. Irá ver esta definição apenas se tem sessão iniciada como um toowhom utilizador uma licença do Azure Active Directory Premium está atribuído.</span><span class="sxs-lookup"><span data-stu-id="31d7b-105">Verify that hello **Enable delegated group management** setting is set too**Yes** in hello **Configure** tab. You will see this setting only if you are signed in as a user toowhom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="31d7b-106">Verifique os valores de Olá para atributos de utilizador na regra Olá: existem utilizadores que satisfazem Olá regra?</span><span class="sxs-lookup"><span data-stu-id="31d7b-106">Verify hello values for user attributes on hello rule: are there users that satisfy hello rule?</span></span>

<span data-ttu-id="31d7b-107">**Posso configurado uma regra, mas agora membros existentes de Olá da regra de Olá são removidos**</span><span class="sxs-lookup"><span data-stu-id="31d7b-107">**I configured a rule, but now hello existing members of hello rule are removed**</span></span><br/><span data-ttu-id="31d7b-108">Este comportamento está previsto.</span><span class="sxs-lookup"><span data-stu-id="31d7b-108">This is expected behavior.</span></span> <span data-ttu-id="31d7b-109">Membros existentes do grupo de Olá são removidos quando uma regra está ativada ou alterada.</span><span class="sxs-lookup"><span data-stu-id="31d7b-109">Existing members of hello group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="31d7b-110">são adicionados utilizadores de Olá devolvidos de avaliação da regra de Olá como grupo de toohello de membros.</span><span class="sxs-lookup"><span data-stu-id="31d7b-110">hello users returned from evaluation of hello rule are added as members toohello group.</span></span>     

<span data-ttu-id="31d7b-111">**Não consigo ver associação mudar instantly quando adicionar ou alterar uma regra, por que motivo não?**</span><span class="sxs-lookup"><span data-stu-id="31d7b-111">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="31d7b-112">Avaliação da associação dedicada é feita periodicamente num processo em segundo plano assíncronas.</span><span class="sxs-lookup"><span data-stu-id="31d7b-112">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="31d7b-113">Quanto Olá processo demora é determinado pelo número de Olá de utilizadores no seu diretório e Olá o tamanho do grupo de Olá criado no seguimento da regra de Olá.</span><span class="sxs-lookup"><span data-stu-id="31d7b-113">How long hello process takes is determined by hello number of users in your directory and hello size of hello group created as a result of hello rule.</span></span> <span data-ttu-id="31d7b-114">Normalmente, diretórios com pequeno número de utilizadores verão as alterações de associação de grupo Olá em menos de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="31d7b-114">Typically, directories with small numbers of users will see hello group membership changes in less than a few minutes.</span></span> <span data-ttu-id="31d7b-115">Diretórios com um grande número de utilizadores podem demorar 30 minutos ou mais toopopulate.</span><span class="sxs-lookup"><span data-stu-id="31d7b-115">Directories with a large number of users can take 30 minutes or longer toopopulate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="31d7b-116">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="31d7b-116">Next steps</span></span>
<span data-ttu-id="31d7b-117">Estes artigos fornecem informações adicionais acerca do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="31d7b-117">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="31d7b-118">Gerir o acesso tooresources com grupos do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31d7b-118">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="31d7b-119">Índice de Artigos da Gestão da Aplicação no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31d7b-119">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="31d7b-120">O que é o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="31d7b-120">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="31d7b-121">Integrar as identidades no local ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31d7b-121">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
