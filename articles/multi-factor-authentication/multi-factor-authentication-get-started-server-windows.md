---
title: "aaaWindows autenticação e o servidor MFA do Azure | Microsoft Docs"
description: "Esta é Olá multi-factor authentication página que irá ajudar a implementar a autenticação do Windows e o servidor do Azure multi-factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a><span data-ttu-id="13401-103">Autenticação do Windows e Servidor Multi-Factor Authentication do Azure</span><span class="sxs-lookup"><span data-stu-id="13401-103">Windows Authentication and Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="13401-104">Utilize a secção autenticação do Windows hello hello do servidor multi-factor Authentication Azure tooenable e configurar a autenticação do Windows para aplicações.</span><span class="sxs-lookup"><span data-stu-id="13401-104">Use hello Windows Authentication section of hello Azure Multi-Factor Authentication Server tooenable and configure Windows authentication for applications.</span></span> <span data-ttu-id="13401-105">Antes de configurar a autenticação do Windows, mantenha Olá lista em consideração os seguintes:</span><span class="sxs-lookup"><span data-stu-id="13401-105">Before you set up Windows Authentication, keep hello following list in mind:</span></span>

* <span data-ttu-id="13401-106">Após a configuração, reinicie Olá Azure multi-factor Authentication para o efeito de tootake de serviços de Terminal.</span><span class="sxs-lookup"><span data-stu-id="13401-106">After setup, reboot hello Azure Multi-Factor Authentication for Terminal Services tootake effect.</span></span>
* <span data-ttu-id="13401-107">Se estiver marcada "Correspondência de utilizador exigir autenticação multi-factor do Azure" e não estiver na lista de utilizadores Olá, não será capaz de toolog numa máquina Olá após o reinício.</span><span class="sxs-lookup"><span data-stu-id="13401-107">If ‘Require Azure Multi-Factor Authentication user match’ is checked and you are not in hello user list, you will not be able toolog into hello machine after reboot.</span></span>
* <span data-ttu-id="13401-108">Fidedigno que IPs é depende se a aplicação Olá pode fornecer Olá IP do cliente com a autenticação de Olá.</span><span class="sxs-lookup"><span data-stu-id="13401-108">Trusted IPs is dependent on whether hello application can provide hello client IP with hello authentication.</span></span> <span data-ttu-id="13401-109">Atualmente, apenas os Serviços de Terminal são suportados.</span><span class="sxs-lookup"><span data-stu-id="13401-109">Currently only Terminal Services is supported.</span></span>  

> [!NOTE]
> <span data-ttu-id="13401-110">Esta funcionalidade não é suportado toosecure os serviços de Terminal no Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="13401-110">This feature is not supported toosecure Terminal Services on Windows Server 2012 R2.</span></span>

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a><span data-ttu-id="13401-111">toosecure uma aplicação com a autenticação do Windows, Olá utilize procedimento a seguir.</span><span class="sxs-lookup"><span data-stu-id="13401-111">toosecure an application with Windows Authentication, use hello following procedure.</span></span>
1. <span data-ttu-id="13401-112">No hello do servidor multi-factor Authentication Azure clique Olá ícone autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="13401-112">In hello Azure Multi-Factor Authentication Server click hello Windows Authentication icon.</span></span>
   <span data-ttu-id="13401-113">![Autenticação do Windows](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span><span class="sxs-lookup"><span data-stu-id="13401-113">![Windows Authentication](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span></span>
2. <span data-ttu-id="13401-114">Verifique Olá **ativar a autenticação do Windows** caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="13401-114">Check hello **Enable Windows Authentication** checkbox.</span></span> <span data-ttu-id="13401-115">Por predefinição, esta caixa está desmarcada.</span><span class="sxs-lookup"><span data-stu-id="13401-115">By default, this box is unchecked.</span></span>
3. <span data-ttu-id="13401-116">separador de aplicações de Olá permite Olá administrador tooconfigure uma ou mais aplicações para autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="13401-116">hello Applications tab allows hello administrator tooconfigure one or more applications for Windows Authentication.</span></span>
4. <span data-ttu-id="13401-117">Selecione um servidor ou a aplicação – especificar se a aplicação e do Olá está ativada.</span><span class="sxs-lookup"><span data-stu-id="13401-117">Select a server or application – specify whether hello server/application is enabled.</span></span> <span data-ttu-id="13401-118">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="13401-118">Click **OK**.</span></span>
5. <span data-ttu-id="13401-119">Clique em **Adicionar...**</span><span class="sxs-lookup"><span data-stu-id="13401-119">Click **Add…**</span></span>
6. <span data-ttu-id="13401-120">separador IPs fidedignos de Olá permite-lhe tooskip sessões de Azure multi-factor Authentication do Windows provenientes de IPs específicos.</span><span class="sxs-lookup"><span data-stu-id="13401-120">hello Trusted IPs tab allows you tooskip Azure Multi-Factor Authentication for Windows sessions originating from specific IPs.</span></span> <span data-ttu-id="13401-121">Por exemplo, se os funcionários utilizarem a aplicação Olá Olá escritório e em casa, pode decidir que não pretende que os telefones toquem para o Azure multi-factor Authentication, office Olá.</span><span class="sxs-lookup"><span data-stu-id="13401-121">For example, if employees use hello application from hello office and from home, you may decide you don't want their phones ringing for Azure Multi-Factor Authentication while at hello office.</span></span> <span data-ttu-id="13401-122">Para tal, tem de especificar a sub-rede do escritório Olá como entrada de IPs fidedignos.</span><span class="sxs-lookup"><span data-stu-id="13401-122">For this, you would specify hello office subnet as Trusted IPs entry.</span></span>
7. <span data-ttu-id="13401-123">Clique em **Adicionar...**</span><span class="sxs-lookup"><span data-stu-id="13401-123">Click **Add…**</span></span>
8. <span data-ttu-id="13401-124">Selecione **IP único** se gostaria tooskip um único endereço IP.</span><span class="sxs-lookup"><span data-stu-id="13401-124">Select **Single IP** if you would like tooskip a single IP address.</span></span>
9. <span data-ttu-id="13401-125">Selecione **intervalo IP** se gostaria tooskip um intervalo IP completo.</span><span class="sxs-lookup"><span data-stu-id="13401-125">Select **IP Range** if you would like tooskip an entire IP range.</span></span> <span data-ttu-id="13401-126">Por exemplo, 10.63.193.1-10.63.193.100.</span><span class="sxs-lookup"><span data-stu-id="13401-126">Example 10.63.193.1-10.63.193.100.</span></span>
10. <span data-ttu-id="13401-127">Selecione **sub-rede** se gostaria toospecify um intervalo de IPs utilizando a notação de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="13401-127">Select **Subnet** if you would like toospecify a range of IPs using subnet notation.</span></span> <span data-ttu-id="13401-128">Introduza o IP inicial da sub-rede Olá e escolha Olá máscara de rede adequada Olá na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="13401-128">Enter hello subnet's starting IP and pick hello appropriate netmask from hello drop-down list.</span></span>
11. <span data-ttu-id="13401-129">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="13401-129">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13401-130">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="13401-130">Next steps</span></span>

- [<span data-ttu-id="13401-131">Configurar aplicações de VPN de terceiros para o Servidor de MFA do Azure</span><span class="sxs-lookup"><span data-stu-id="13401-131">Configure third-party VPN appliances for Azure MFA Server</span></span>](multi-factor-authentication-advanced-vpn-configurations.md)

- [<span data-ttu-id="13401-132">Aumentar a sua infraestrutura de autenticação existente com Olá extensão NPS para o Azure MFA</span><span class="sxs-lookup"><span data-stu-id="13401-132">Augment your existing authentication infrastructure with hello NPS extension for Azure MFA</span></span>](multi-factor-authentication-nps-extension.md)
