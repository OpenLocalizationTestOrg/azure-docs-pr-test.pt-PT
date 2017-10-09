---
title: "portal de inscrição do serviço de aaaSelf para colaboração B2B do Azure Active Directory do | Microsoft Docs"
description: "Colaboração do Azure Active Directory B2B suporta as relações entre empresas ao permitir o acesso de tooselectively de parceiros de negócio a aplicações empresariais"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: c78920ecf812f7efc06a8b54b1fff834c32904f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a><span data-ttu-id="687b9-103">Portal self-service para inscrição de colaboração B2B do Azure AD</span><span class="sxs-lookup"><span data-stu-id="687b9-103">Self-service portal for Azure AD B2B collaboration sign-up</span></span>

<span data-ttu-id="687b9-104">Os clientes podem fazer muito com funcionalidades incorporadas Olá expostas através do nosso administrador de TI [portal do Azure](https://portal.azure.com) e no nosso [painel de acesso de aplicação](https://myapps.microsoft.com) para os utilizadores finais.</span><span class="sxs-lookup"><span data-stu-id="687b9-104">Customers can do a lot with hello built-in features that are exposed through our IT admin [Azure portal](https://portal.azure.com) and our [Application Access Panel](https://myapps.microsoft.com) for end users.</span></span> <span data-ttu-id="687b9-105">Mas estamos também em atenção de que as empresas necessitam de fluxo de trabalho do toocustomize Olá integração para B2B utilizadores toofit as necessidades da sua organização.</span><span class="sxs-lookup"><span data-stu-id="687b9-105">But we are also aware that businesses need toocustomize hello onboarding workflow for B2B users toofit their organization’s needs.</span></span> <span data-ttu-id="687b9-106">Podem fazê-lo com [nossa API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span><span class="sxs-lookup"><span data-stu-id="687b9-106">They can do that with [our API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span></span>

<span data-ttu-id="687b9-107">Em discussões com os nossos clientes, vemos um comuns tem de aumentar a segurança acima de todos os outros.</span><span class="sxs-lookup"><span data-stu-id="687b9-107">In discussions with our customers, we see one common need rise up above all others.</span></span> <span data-ttu-id="687b9-108">Olá inviting organização poderá não saber antecedência que Olá colaboradores externos individuais são que precisa de aceder a recursos de tootheir.</span><span class="sxs-lookup"><span data-stu-id="687b9-108">hello inviting organization may not know ahead of time who hello individual external collaborators are who need access tootheir resources.</span></span> <span data-ttu-id="687b9-109">Pretendessem uma forma para os utilizadores de empresas demasiado inscrevem-se com um conjunto de políticas que Olá inviting controlos da organização.</span><span class="sxs-lookup"><span data-stu-id="687b9-109">They wanted a way for users from partner companies too sign themselves up with a set of policies that hello inviting organization controls.</span></span> <span data-ttu-id="687b9-110">Este cenário é possível através do nosso APIs, pelo que iremos publicado um projeto no Github que criou apenas que: [projeto do Github de exemplo](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span><span class="sxs-lookup"><span data-stu-id="687b9-110">This scenario is possible through our APIs,  so we published a project on Github that did just that: [sample Github project](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

<span data-ttu-id="687b9-111">Nosso projeto Github demonstra como as organizações podem utilizar os APIs e fornecer uma capacidade de inscrição baseadas em políticas, self-service para os respetivos parceiros confiadores, com regras que determinam aplicações Olá que poderem aceder ao.</span><span class="sxs-lookup"><span data-stu-id="687b9-111">Our Github project demonstrates how organizations can use our APIs, and provide a policy-based, self-service sign-up capability for their trusted partners, with rules that determine hello apps they can access.</span></span> <span data-ttu-id="687b9-112">Os utilizadores do parceiro podem obter acesso tooresources quando precisam, de forma segura, sem necessidade de Olá inviting organização toomanually carregá-los.</span><span class="sxs-lookup"><span data-stu-id="687b9-112">Partner users can get access tooresources when they need them, securely, without requiring hello inviting organization toomanually onboard them.</span></span> <span data-ttu-id="687b9-113">Pode facilmente implementar o projeto de Olá para uma subscrição do Azure à sua escolha.</span><span class="sxs-lookup"><span data-stu-id="687b9-113">You can easily deploy hello project into an Azure subscription of your choice.</span></span>

## <a name="as-is-code"></a><span data-ttu-id="687b9-114">Como-é código</span><span class="sxs-lookup"><span data-stu-id="687b9-114">As-is code</span></span>

<span data-ttu-id="687b9-115">Lembre-se de que este código é disponibilizado como a utilização de toodemonstrate um exemplo de convite de Olá do Azure Active Directory B2B API.</span><span class="sxs-lookup"><span data-stu-id="687b9-115">Remember that this code is made available as a sample toodemonstrate usage of hello Azure Active Directory B2B invitation API.</span></span> <span data-ttu-id="687b9-116">Deve ser personalizada pela sua equipa de desenvolvimento ou de um parceiro e deve ser revisto antes de ser implementado num cenário de produção.</span><span class="sxs-lookup"><span data-stu-id="687b9-116">It should be customized by your dev team or a partner, and should be reviewed before being deployed in a production scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="687b9-117">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="687b9-117">Next steps</span></span>

<span data-ttu-id="687b9-118">Consulte os nossos outros artigos sobre a colaboração B2B do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="687b9-118">Browse our other articles on Azure AD B2B collaboration:</span></span>
* [<span data-ttu-id="687b9-119">O que é a colaboração B2B do Azure AD?</span><span class="sxs-lookup"><span data-stu-id="687b9-119">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="687b9-120">Como é que os administradores de Azure Active Directory adicionar utilizadores de colaboração do B2B?</span><span class="sxs-lookup"><span data-stu-id="687b9-120">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="687b9-121">Como é que os infotrabalhadores adicionar utilizadores de colaboração do B2B?</span><span class="sxs-lookup"><span data-stu-id="687b9-121">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="687b9-122">elementos de Olá de Olá e-mail de convite de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="687b9-122">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="687b9-123">Resgate de convite de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="687b9-123">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="687b9-124">Licenciamento e colaboração do Azure AD B2B</span><span class="sxs-lookup"><span data-stu-id="687b9-124">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="687b9-125">Resolução de problemas de colaboração B2B do Azure Active Directory do</span><span class="sxs-lookup"><span data-stu-id="687b9-125">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="687b9-126">Colaboração do Azure Active Directory B2B perguntas mais frequentes (FAQ)</span><span class="sxs-lookup"><span data-stu-id="687b9-126">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="687b9-127">Autenticação multifator para os utilizadores da colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="687b9-127">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="687b9-128">Adicionar utilizadores de colaboração B2B sem um convite</span><span class="sxs-lookup"><span data-stu-id="687b9-128">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="687b9-129">Índice de Artigos da Gestão da Aplicação no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="687b9-129">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)