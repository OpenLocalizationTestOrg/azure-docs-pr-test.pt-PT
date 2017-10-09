---
title: "Olá aaaModify dados 0 definições num dispositivo StorSimple | Microsoft Docs"
description: "Saiba como toouse do Windows PowerShell para StorSimple tooreconfigure Olá interface rede DATA 0 no dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 58e3d509-f425-4a7f-b650-d496a7c85193
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: caec51c3344d953299253301c2a0d7577d553c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-device"></a><span data-ttu-id="34888-103">Modificar definições da interface de rede 0 de dados de Olá no dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="34888-103">Modify hello DATA 0 network interface settings on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="34888-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="34888-104">Overview</span></span>
<span data-ttu-id="34888-105">O dispositivo Microsoft Azure StorSimple possui seis interfaces de rede, a partir dos dados 0 tooDATA 5.</span><span class="sxs-lookup"><span data-stu-id="34888-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 tooDATA 5.</span></span> <span data-ttu-id="34888-106">Olá dados 0 interface é sempre configurada através da interface do Windows PowerShell Olá ou consola de série de Olá e é automaticamente ativado para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="34888-106">hello DATA 0 interface is always configured through hello Windows PowerShell interface or hello serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="34888-107">Tenha em atenção que não é possível configurar interface rede DATA 0 através de Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="34888-107">Note that you cannot configure DATA 0 network interface through hello Azure classic portal.</span></span> 

<span data-ttu-id="34888-108">Olá dados 0 interface de rede pela primeira vez é configurada através do Assistente de configuração de Olá durante a implementação inicial de dispositivo do StorSimple Olá.</span><span class="sxs-lookup"><span data-stu-id="34888-108">hello DATA 0 interface is first configured through hello setup wizard during initial deployment of hello StorSimple device.</span></span> <span data-ttu-id="34888-109">Quando o dispositivo de Olá está num modo operacional, poderá ser necessário tooreconfigure dados 0 definições.</span><span class="sxs-lookup"><span data-stu-id="34888-109">When hello device is in an operational mode, you may need tooreconfigure DATA 0 settings.</span></span> <span data-ttu-id="34888-110">Este tutorial fornece dois métodos toomodify dados 0 as definições de rede, tanto através do Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="34888-110">This tutorial provides two methods toomodify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="34888-111">Depois de ler este tutorial, será capaz de:</span><span class="sxs-lookup"><span data-stu-id="34888-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="34888-112">Modificar dados 0 definição através do Assistente de configuração de Olá de rede</span><span class="sxs-lookup"><span data-stu-id="34888-112">Modify DATA 0 network setting through hello setup wizard</span></span>
* <span data-ttu-id="34888-113">Modificar as definições de rede 0 de dados através de Olá `Set-HcsNetInterface` cmdlet</span><span class="sxs-lookup"><span data-stu-id="34888-113">Modify DATA 0 network settings through hello `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="34888-114">Modificar as definições de rede 0 de dados através do Assistente de configuração</span><span class="sxs-lookup"><span data-stu-id="34888-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="34888-115">Pode reconfigurar as definições de rede 0 de dados através da interface do Windows PowerShell toohello do dispositivo StorSimple a ligar e iniciar uma sessão de Assistente de configuração.</span><span class="sxs-lookup"><span data-stu-id="34888-115">You can reconfigure DATA 0 network settings by connecting toohello Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="34888-116">Efetuar Olá passos toomodify dados 0 os seguintes definições:</span><span class="sxs-lookup"><span data-stu-id="34888-116">Perform hello following steps toomodify DATA 0 settings:</span></span>

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="34888-117">definições de rede 0 toomodify dados através do Assistente de configuração</span><span class="sxs-lookup"><span data-stu-id="34888-117">toomodify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="34888-118">No menu da consola de série de Olá, selecione a opção 1, **iniciar sessão com acesso total**.</span><span class="sxs-lookup"><span data-stu-id="34888-118">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="34888-119">Quando lhe for pedido fornecer Olá **palavra-passe de administrador do dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="34888-119">When prompted provide hello **device administrator password**.</span></span> <span data-ttu-id="34888-120">palavra-passe predefinida de Olá é `Password1`.</span><span class="sxs-lookup"><span data-stu-id="34888-120">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="34888-121">Na linha de comandos Olá, escreva:</span><span class="sxs-lookup"><span data-stu-id="34888-121">At hello command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="34888-122">Um Assistente de configuração irá aparecer toohelp configurar Olá dados 0 interface do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="34888-122">A setup wizard will appear toohelp you configure hello DATA 0 interface of your device.</span></span> <span data-ttu-id="34888-123">Forneça novos valores para o endereço IP Olá, o gateway e máscara de rede.</span><span class="sxs-lookup"><span data-stu-id="34888-123">Provide new values for hello IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="34888-124">Olá fixo controladores IPs terá toobe reconfigurado através de Olá **configurar** página do dispositivo StorSimple Olá Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="34888-124">hello fixed controllers IPs will need toobe reconfigured through hello **Configure** page of hello StorSimple device in hello Azure classic portal.</span></span> <span data-ttu-id="34888-125">Para mais informações, visite demasiado[modificar interfaces de rede](storsimple-modify-device-config.md#modify-network-interfaces).</span><span class="sxs-lookup"><span data-stu-id="34888-125">For more information, go too[Modify network interfaces](storsimple-modify-device-config.md#modify-network-interfaces).</span></span>
> 
> 

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="34888-126">Modificar as definições de rede 0 de dados através do cmdlet Set-HcsNetInterface</span><span class="sxs-lookup"><span data-stu-id="34888-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="34888-127">Tooreconfigure uma maneira alternativa DATA 0 é de interface de rede através da utilização de Olá de Olá `Set-HcsNetInterface` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="34888-127">An alternate way tooreconfigure DATA 0 network interface is through hello use of  hello `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="34888-128">Olá cmdlet é executado a partir da interface do Windows PowerShell Olá do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="34888-128">hello cmdlet is executed from hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="34888-129">Quando utilizar este procedimento, controlador Olá IPs fixo também pode ser configurado aqui.</span><span class="sxs-lookup"><span data-stu-id="34888-129">When using this procedure, hello controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="34888-130">Efetuar Olá passos toomodify Olá dados 0 os seguintes definições:</span><span class="sxs-lookup"><span data-stu-id="34888-130">Perform hello following steps toomodify hello DATA 0 settings:</span></span> 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="34888-131">definições de rede 0 toomodify dados através do cmdlet Olá HcsNetInterface conjunto</span><span class="sxs-lookup"><span data-stu-id="34888-131">toomodify DATA 0 network settings through hello Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="34888-132">No menu da consola de série de Olá, selecione a opção 1, **iniciar sessão com acesso total**.</span><span class="sxs-lookup"><span data-stu-id="34888-132">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="34888-133">Quando lhe for pedido forneça a palavra-passe de administrador de dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="34888-133">When prompted provide hello device administrator password.</span></span> <span data-ttu-id="34888-134">palavra-passe predefinida de Olá é `Password1`.</span><span class="sxs-lookup"><span data-stu-id="34888-134">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="34888-135">Na linha de comandos Olá, escreva:</span><span class="sxs-lookup"><span data-stu-id="34888-135">At hello command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="34888-136">Entre parênteses Retos Olá angled, escreva Olá os seguintes valores para os dados 0:</span><span class="sxs-lookup"><span data-stu-id="34888-136">In hello angled brackets, type hello following values for DATA 0:</span></span>
   
   * <span data-ttu-id="34888-137">Endereço IPv4</span><span class="sxs-lookup"><span data-stu-id="34888-137">IPv4 address</span></span>
   * <span data-ttu-id="34888-138">Gateway de IPv4</span><span class="sxs-lookup"><span data-stu-id="34888-138">IPv4 gateway</span></span>
   * <span data-ttu-id="34888-139">Máscara de sub-rede IPv4</span><span class="sxs-lookup"><span data-stu-id="34888-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="34888-140">Endereço IPv4 fixo para o controlador 0</span><span class="sxs-lookup"><span data-stu-id="34888-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="34888-141">Endereço IPv4 fixo para o controlador 1</span><span class="sxs-lookup"><span data-stu-id="34888-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="34888-142">Para obter mais informações sobre a utilização de Olá deste cmdlet, visite demasiado[do Windows PowerShell para StorSimple referência de cmdlet](https://technet.microsoft.com/library/dn688161.aspx).</span><span class="sxs-lookup"><span data-stu-id="34888-142">For more information on hello use of this cmdlet, go too[Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="34888-143">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="34888-143">Next steps</span></span>
* <span data-ttu-id="34888-144">tooconfigure interfaces de rede que não sejam dados 0, pode utilizar Olá [Configurar página no portal clássico do Azure de Olá](storsimple-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="34888-144">tooconfigure network interfaces other than DATA 0, you can use hello [Configure page in hello Azure classic portal](storsimple-modify-device-config.md).</span></span> 
* <span data-ttu-id="34888-145">Se ocorrer algum problema quando configurar as interfaces de rede, consulte demasiado[resolver problemas de implementação](storsimple-troubleshoot-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="34888-145">If you experience any issues when configuring your network interfaces, refer too[Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>

