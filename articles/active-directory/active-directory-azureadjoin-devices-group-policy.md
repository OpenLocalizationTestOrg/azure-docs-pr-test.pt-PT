---
title: "ocorre no aaaConnect dispositivos associados a domínios tooAzure AD para o Windows 10 | Microsoft Docs"
description: "Explica como os administradores podem configurar a rede empresarial de associados a um domínio toohello toobe política de grupo tooenable dispositivos."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 9766aa702352dea2ecad3a9a0bdf8d3286ee6d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a><span data-ttu-id="3e330-103">Ligar a dispositivos associados a domínios tooAzure AD para experiências do Windows 10</span><span class="sxs-lookup"><span data-stu-id="3e330-103">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>
<span data-ttu-id="3e330-104">Associação a um domínio é que as organizações de forma tradicional Olá ligou dispositivos for work para Olá últimos 15 anos e muito mais.</span><span class="sxs-lookup"><span data-stu-id="3e330-104">Domain join is hello traditional way organizations have connected devices for work for hello last 15 years and more.</span></span> <span data-ttu-id="3e330-105">Ativou toosign de utilizadores nos dispositivos tootheir utilizando o respetivo trabalho do Windows Server Active Directory (Active Directory) ou contas profissional e permitido IT toofully gerirem estes dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3e330-105">It has enabled users toosign in tootheir devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT toofully manage these devices.</span></span> <span data-ttu-id="3e330-106">As organizações dependem normalmente imaging métodos tooprovision dispositivos toousers e geralmente, utilizar o System Center Configuration Manager (SCCM) ou de política de grupo toomanage-los.</span><span class="sxs-lookup"><span data-stu-id="3e330-106">Organizations typically rely on imaging methods tooprovision devices toousers and generally use System Center Configuration Manager (SCCM) or Group Policy toomanage them.</span></span>


<span data-ttu-id="3e330-107">Associação a um domínio no Windows 10 fornece-lhe Olá depois de ligar dispositivos tooAzure do Active Directory (Azure AD) os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="3e330-107">Domain join in Windows 10 provides you with hello following benefits after you connect devices tooAzure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="3e330-108">Único início de sessão (SSO) tooAzure AD recursos a partir de qualquer lugar</span><span class="sxs-lookup"><span data-stu-id="3e330-108">Single sign-on (SSO) tooAzure AD resources from anywhere</span></span>
* <span data-ttu-id="3e330-109">Aceder à empresa toohello loja Windows através da utilização de trabalho ou escola contas (não existe nenhuma conta Microsoft necessária)</span><span class="sxs-lookup"><span data-stu-id="3e330-109">Access toohello enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="3e330-110">Empresarial compatível roaming de definições de utilizador em todos os dispositivos através da utilização de contas profissionais ou escolares (não existe nenhuma conta Microsoft necessária)</span><span class="sxs-lookup"><span data-stu-id="3e330-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="3e330-111">Autenticação forte e conveniente início de sessão para contas profissionais ou escolares com o Windows Hello para empresas e o Windows Hello</span><span class="sxs-lookup"><span data-stu-id="3e330-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="3e330-112">Capacidade toorestrict aceder apenas toodevices que estão em conformidade com as definições de política de grupo organizacional do dispositivo</span><span class="sxs-lookup"><span data-stu-id="3e330-112">Ability toorestrict access only toodevices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e330-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3e330-113">Prerequisites</span></span>
<span data-ttu-id="3e330-114">Associação a um domínio continua toobe útil.</span><span class="sxs-lookup"><span data-stu-id="3e330-114">Domain join continues toobe useful.</span></span> <span data-ttu-id="3e330-115">No entanto, tooget vantagens de Olá do Azure AD do SSO, roaming das definições com ou escola contas e aceder à loja de tooWindows com trabalho profissional ou escolar contas, é necessário Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="3e330-115">However, tooget hello Azure AD benefits of SSO, roaming of settings with work or school accounts, and access tooWindows Store with work or school accounts, you will need hello following:</span></span>

* <span data-ttu-id="3e330-116">Subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e330-116">Azure AD subscription</span></span>
* <span data-ttu-id="3e330-117">Azure AD Connect tooextend Olá no local diretório tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="3e330-117">Azure AD Connect tooextend hello on-premises directory tooAzure AD</span></span>
* <span data-ttu-id="3e330-118">Política de que definiu tooconnect dispositivos associados a domínios tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="3e330-118">Policy that's set tooconnect domain-joined devices tooAzure AD</span></span>
* <span data-ttu-id="3e330-119">Compilação do Windows 10 (compilação 10551 ou mais recente) para dispositivos</span><span class="sxs-lookup"><span data-stu-id="3e330-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="3e330-120">tooenable Windows Hello para empresas e o Windows Hello, também terá de seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="3e330-120">tooenable Windows Hello for Business and Windows Hello, you will also need hello following:</span></span>

- <span data-ttu-id="3e330-121">**Infraestrutura de chaves públicas (PKI)** para emissão de certificados de utilizador.</span><span class="sxs-lookup"><span data-stu-id="3e330-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="3e330-122">**System Center Configuration Manager Current Branch** -terá tooinstall versão 1606 ou melhor.</span><span class="sxs-lookup"><span data-stu-id="3e330-122">**System Center Configuration Manager Current Branch** - You need tooinstall version 1606 or better.</span></span>  
<span data-ttu-id="3e330-123">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="3e330-123">For more information, see:</span></span> 
    - [<span data-ttu-id="3e330-124">Documentação do System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="3e330-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="3e330-125">Blogue da equipa do System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="3e330-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="3e330-126">Windows Hello para definições da empresa no System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="3e330-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="3e330-127">Como um requisito de implementação de PKI toohello alternativa, pode fazê-lo seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="3e330-127">As an alternative toohello PKI deployment requirement, you can do hello following:</span></span>

* <span data-ttu-id="3e330-128">Ter alguns controladores de domínio com o Windows Server 2016 Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="3e330-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="3e330-129">acesso condicional tooenable, pode criar definições de política de grupo que permitem o acesso a dispositivos associados a toodomain com sem implementações adicionais.</span><span class="sxs-lookup"><span data-stu-id="3e330-129">tooenable conditional access, you can create Group Policy settings that allow access toodomain-joined devices with no additional deployments.</span></span> <span data-ttu-id="3e330-130">controlo de acesso de toomanage com base na conformidade de dispositivo Olá, terá de seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="3e330-130">toomanage access control based on compliance of hello device, you will need hello following:</span></span>

* <span data-ttu-id="3e330-131">System Center Configuration Manager Current Branch (1606 ou posterior) para Windows Hello para cenários de negócios</span><span class="sxs-lookup"><span data-stu-id="3e330-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="3e330-132">Instruções de implementação</span><span class="sxs-lookup"><span data-stu-id="3e330-132">Deployment instructions</span></span>

<span data-ttu-id="3e330-133">toodeploy, siga passos de Olá apresentados na [como tooconfigure o registo automático do Windows associados a um domínio dispositivos com o Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="3e330-133">toodeploy, follow hello steps listed in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="3e330-134">Passo seguinte</span><span class="sxs-lookup"><span data-stu-id="3e330-134">Next step</span></span>
* [<span data-ttu-id="3e330-135">Windows 10 para empresa Olá: dispositivos de toouse formas de trabalho</span><span class="sxs-lookup"><span data-stu-id="3e330-135">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="3e330-136">Expandir nuvem dispositivos de tooWindows 10 capacidades através da associação do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e330-136">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="3e330-137">Saiba mais sobre os cenários de utilização da Associação do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e330-137">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="3e330-138">Ligar a dispositivos associados a domínios tooAzure AD para experiências do Windows 10</span><span class="sxs-lookup"><span data-stu-id="3e330-138">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="3e330-139">Configurar a Associação do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e330-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

