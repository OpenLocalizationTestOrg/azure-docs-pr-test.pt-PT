---
title: "aaaSet segurança de um dispositivo Windows 10 com o Azure AD a partir das definições | Microsoft Docs"
description: "Explica como os utilizadores podem associar tooAzure AD através do menu de definições de Olá."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="e5114-103">Configurar um dispositivo Windows 10 com o Azure AD a partir das definições</span><span class="sxs-lookup"><span data-stu-id="e5114-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="e5114-104">Se já estiver a utilizar o Windows 7 ou Windows 8 e o computador ou dispositivo tiver sido atualizado tooWindows 10, pode participar tooAzure do Active Directory (Azure AD) através do menu de definições de Olá.</span><span class="sxs-lookup"><span data-stu-id="e5114-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded tooWindows 10, you can join tooAzure Active Directory (Azure AD) through hello Settings menu.</span></span>

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a><span data-ttu-id="e5114-105">toojoin tooAzure AD a partir do menu de definições de Olá</span><span class="sxs-lookup"><span data-stu-id="e5114-105">toojoin tooAzure AD from hello Settings menu</span></span>
1. <span data-ttu-id="e5114-106">De Olá **iniciar** menu, clique em Olá **definições** atalho.</span><span class="sxs-lookup"><span data-stu-id="e5114-106">From hello **Start** menu, click hello **Settings** charm.</span></span>
2. <span data-ttu-id="e5114-107">De **definições**, selecione **sistema**->**sobre**->**associação do Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="e5114-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="e5114-108"><center>
   ![Associação do Azure AD a partir do menu de definições de Olá](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center></span><span class="sxs-lookup"><span data-stu-id="e5114-108"><center>
![Join Azure AD from hello Settings menu](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="e5114-109">Clique em **continuar** na janela de mensagem de associação do Azure AD Olá.</span><span class="sxs-lookup"><span data-stu-id="e5114-109">Click **Continue** in hello Azure AD Join message window.</span></span>
   
   <span data-ttu-id="e5114-110"><center>
   ![Janela de mensagem de associação do Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png)</center></span><span class="sxs-lookup"><span data-stu-id="e5114-110"><center>
![Join Azure AD message window](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="e5114-111">Forneça as credenciais de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="e5114-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="e5114-112">Esta experiência de início de sessão irá incluir todos os passos de Olá são toocomplete necessária autenticação.</span><span class="sxs-lookup"><span data-stu-id="e5114-112">This sign-in experience will include all hello steps that are required toocomplete authentication.</span></span> <span data-ttu-id="e5114-113">Se fizer parte de um inquilino federado, o administrador irá fornecer-lhe experiência de Federação Olá que está alojada pela sua organização.</span><span class="sxs-lookup"><span data-stu-id="e5114-113">If you are part of a federated tenant, your administrator will provide you with hello federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="e5114-114"><center>
   ![Forneça as credenciais de início de sessão](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</center></span><span class="sxs-lookup"><span data-stu-id="e5114-114"><center>
![Provide sign-in credentials](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="e5114-115">Se a sua organização tiver configurado o multi-factor Authentication do Azure para efetuar a adesão tooAzure AD, forneça o segundo fator de Olá antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="e5114-115">If your organization has configured Azure Multi-Factor Authentication for joining tooAzure AD, provide hello second factor before proceeding.</span></span>
6. <span data-ttu-id="e5114-116">Clique em **aceitar** no Olá **permitir toobe este dispositivo gerido** ecrã.</span><span class="sxs-lookup"><span data-stu-id="e5114-116">Click **Accept** on hello **Allow this device toobe managed** screen.</span></span>
7. <span data-ttu-id="e5114-117">Deverá ver a mensagem de saudação "o dispositivo está agora associado tooyour organização no Azure AD".</span><span class="sxs-lookup"><span data-stu-id="e5114-117">You should see hello message "Your device is now joined tooyour organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="e5114-118">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="e5114-118">Additional information</span></span>
* [<span data-ttu-id="e5114-119">Saiba mais sobre os cenários de utilização da Associação do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5114-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="e5114-120">Ligar a dispositivos associados a domínios tooAzure AD para experiências do Windows 10</span><span class="sxs-lookup"><span data-stu-id="e5114-120">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="e5114-121">Configurar a Associação do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5114-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="e5114-122">Autenticar identidades sem palavras-passe através do Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="e5114-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)

