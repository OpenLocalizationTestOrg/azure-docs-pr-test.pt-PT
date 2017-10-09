---
title: "aaaGet iniciado o MFA do Azure na nuvem de Olá | Microsoft Docs"
description: "Este é Olá Microsoft Azure multi-factor authentication página que descreve como tooget ao Azure MFA na nuvem de Olá."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 6b2e6549-1a26-4666-9c4a-cbe5d64c4e66
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/24/2017
ms.author: kgremban
ms.openlocfilehash: a4aaf44bf08d96f2baad155072fdd6e0e727ce8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-in-hello-cloud"></a><span data-ttu-id="d45c1-103">Introdução ao Azure multi-factor Authentication na nuvem de Olá</span><span class="sxs-lookup"><span data-stu-id="d45c1-103">Getting started with Azure Multi-Factor Authentication in hello cloud</span></span>
<span data-ttu-id="d45c1-104">Este artigo explica como tooget iniciado utilizando a Azure multi-factor Authentication na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="d45c1-104">This article walks through how tooget started using Azure Multi-Factor Authentication in hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="d45c1-105">Olá seguinte documentação fornece informações sobre como os utilizadores tooenable utilizando Olá **Portal clássico do Azure**.</span><span class="sxs-lookup"><span data-stu-id="d45c1-105">hello following documentation provides information on how tooenable users using hello **Azure Classic Portal**.</span></span> <span data-ttu-id="d45c1-106">Se estiver à procura de informações sobre como tooset cópias de segurança do Azure multi-factor Authentication para os utilizadores do Office 365, consulte [configurar a multi-factor authentication para Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span><span class="sxs-lookup"><span data-stu-id="d45c1-106">If you are looking for information on how tooset up Azure Multi-Factor Authentication for O365 users, see [Set up multi-factor authentication for Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span></span>

![MFA na nuvem de Olá](./media/multi-factor-authentication-get-started-cloud/mfa_in_cloud.png)

## <a name="prerequisite"></a><span data-ttu-id="d45c1-108">Pré-requisito</span><span class="sxs-lookup"><span data-stu-id="d45c1-108">Prerequisite</span></span>
<span data-ttu-id="d45c1-109">[Inscreva-se uma subscrição do Azure](https://azure.microsoft.com/pricing/free-trial/) -se ainda não tiver uma subscrição do Azure, tem de cópia de segurança toosign numa.</span><span class="sxs-lookup"><span data-stu-id="d45c1-109">[Sign up for an Azure subscription](https://azure.microsoft.com/pricing/free-trial/) - If you do not already have an Azure subscription, you need toosign-up for one.</span></span> <span data-ttu-id="d45c1-110">Se estiver apenas a começar e a utilizar o MFA do Azure, pode utilizar uma subscrição de avaliação</span><span class="sxs-lookup"><span data-stu-id="d45c1-110">If you are just starting out and using Azure MFA you can use a trial subscription</span></span>

## <a name="enable-azure-multi-factor-authentication"></a><span data-ttu-id="d45c1-111">Ativar a Multi-Factor Authentication do Azure</span><span class="sxs-lookup"><span data-stu-id="d45c1-111">Enable Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="d45c1-112">Desde que os utilizadores têm de licenças que incluem o Azure multi-factor Authentication, não há nada que precisa de toodo tooturn na MFA do Azure.</span><span class="sxs-lookup"><span data-stu-id="d45c1-112">As long as your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="d45c1-113">Pode requerer a verificação de dois passos para cada utilizador.</span><span class="sxs-lookup"><span data-stu-id="d45c1-113">You can start requiring two-step verification on an individual user basis.</span></span> <span data-ttu-id="d45c1-114">licenças de Olá que ativar a MFA do Azure são:</span><span class="sxs-lookup"><span data-stu-id="d45c1-114">hello licenses that enable Azure MFA are:</span></span>
- <span data-ttu-id="d45c1-115">Multi-Factor Authentication do Azure</span><span class="sxs-lookup"><span data-stu-id="d45c1-115">Azure Multi-Factor Authentication</span></span>
- <span data-ttu-id="d45c1-116">Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="d45c1-116">Azure Active Directory Premium</span></span>
- <span data-ttu-id="d45c1-117">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="d45c1-117">Enterprise Mobility + Security</span></span>

<span data-ttu-id="d45c1-118">Se não tiver uma destas licenças três ou não tem suficiente toocover licenças todos os utilizadores que ok demasiado.</span><span class="sxs-lookup"><span data-stu-id="d45c1-118">If you don't have one of these three licenses, or you don't have enough licenses toocover all of your users, that's ok too.</span></span> <span data-ttu-id="d45c1-119">Apenas tiver toodo um passo adicional e [criar um fornecedor do multi-factor Auth](multi-factor-authentication-get-started-auth-provider.md) no seu diretório.</span><span class="sxs-lookup"><span data-stu-id="d45c1-119">You just have toodo an extra step and [Create a Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md) in your directory.</span></span>

## <a name="turn-on-two-step-verification-for-users"></a><span data-ttu-id="d45c1-120">Ativar a verificação de dois passos para os utilizadores</span><span class="sxs-lookup"><span data-stu-id="d45c1-120">Turn on two-step verification for users</span></span>

<span data-ttu-id="d45c1-121">Utilize um dos procedimentos de Olá listados no [como toorequire a verificação de dois passos para um utilizador ou grupo](multi-factor-authentication-get-started-user-states.md) toostart através do MFA do Azure.</span><span class="sxs-lookup"><span data-stu-id="d45c1-121">Use one of hello procedures listed in [How toorequire two-step verification for a user or group](multi-factor-authentication-get-started-user-states.md) toostart using Azure MFA.</span></span> <span data-ttu-id="d45c1-122">Pode escolher tooenforce a verificação de dois passos para todos os inícios de sessão ou pode criar a verificação de acesso condicional políticas toorequire apenas quando o é importante tooyou.</span><span class="sxs-lookup"><span data-stu-id="d45c1-122">You can choose tooenforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when it matters tooyou.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d45c1-123">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="d45c1-123">Next Steps</span></span>
<span data-ttu-id="d45c1-124">Agora que configurou Azure multi-factor Authentication na nuvem de Olá, pode configurar e configurar a sua implementação.</span><span class="sxs-lookup"><span data-stu-id="d45c1-124">Now that you have set up Azure Multi-Factor Authentication in hello cloud, you can configure and set up your deployment.</span></span> <span data-ttu-id="d45c1-125">Veja [Configuring Azure Multi-Factor Authentication (Configurar o Multi-Factor Authentication do Azure)](multi-factor-authentication-whats-next.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="d45c1-125">See [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) for more details.</span></span>

