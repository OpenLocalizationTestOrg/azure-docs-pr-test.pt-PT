---
title: "aaaInstall tendência Micro segurança profunda numa VM | Microsoft Docs"
description: "Este artigo descreve como tooinstall e configurar a segurança de tendência Micro numa VM criada com o modelo de implementação clássica Olá no Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a><span data-ttu-id="f79a8-103">Como tooinstall e configurar a segurança avançada do tendência Micro como um serviço numa VM do Windows</span><span class="sxs-lookup"><span data-stu-id="f79a8-103">How tooinstall and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f79a8-104">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f79a8-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f79a8-105">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="f79a8-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f79a8-106">A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="f79a8-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="f79a8-107">Este artigo mostra como tooinstall e configurar a segurança avançada do tendência Micro como um serviço numa nova ou existente máquina virtual (VM) com o Windows Server.</span><span class="sxs-lookup"><span data-stu-id="f79a8-107">This article shows you how tooinstall and configure Trend Micro Deep Security as a Service on a new or existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="f79a8-108">Segurança avançada, como um serviço inclui proteção antimalware, uma firewall, um sistema de prevenção de intrusões e monitorização de integridade.</span><span class="sxs-lookup"><span data-stu-id="f79a8-108">Deep Security as a Service includes anti-malware protection, a firewall, an intrusion prevention system, and integrity monitoring.</span></span>

<span data-ttu-id="f79a8-109">Olá é instalado como uma extensão de segurança através de Olá agente da VM.</span><span class="sxs-lookup"><span data-stu-id="f79a8-109">hello client is installed as a security extension via hello VM Agent.</span></span> <span data-ttu-id="f79a8-110">Uma nova máquina virtual, instale Olá profunda de segurança de agente, como Olá que agente da VM é automaticamente criada pelo Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f79a8-110">On a new virtual machine, you install hello Deep Security Agent, as hello VM Agent is created automatically by hello Azure portal.</span></span>

<span data-ttu-id="f79a8-111">VM existente criada utilizando o portal clássico Olá, Olá Azure CLI ou PowerShell poderá não ter um agente VM.</span><span class="sxs-lookup"><span data-stu-id="f79a8-111">An existing VM created using hello classic portal, hello Azure CLI, or PowerShell might not have a VM agent.</span></span> <span data-ttu-id="f79a8-112">Para uma máquina virtual existente que não tem Olá agente da VM, tem de toodownload e instale-o primeiro.</span><span class="sxs-lookup"><span data-stu-id="f79a8-112">For an existing virtual machine that doesn't have hello VM Agent, you need toodownload and install it first.</span></span> <span data-ttu-id="f79a8-113">Este artigo abrange ambas as situações.</span><span class="sxs-lookup"><span data-stu-id="f79a8-113">This article covers both situations.</span></span>

<span data-ttu-id="f79a8-114">Se tiver uma subscrição atual de tendência Micro para uma solução no local, pode utilizá-lo toohelp proteger as máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="f79a8-114">If you have a current subscription from Trend Micro for an on-premises solution, you can use it toohelp protect your Azure virtual machines.</span></span> <span data-ttu-id="f79a8-115">Se ainda não estiver um cliente, pode inscrever-se para uma subscrição de avaliação.</span><span class="sxs-lookup"><span data-stu-id="f79a8-115">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="f79a8-116">Para obter mais informações sobre esta solução, consulte a mensagem de blogue de tendência Micro de Olá [Microsoft Azure VM extensão para a segurança do agente](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span><span class="sxs-lookup"><span data-stu-id="f79a8-116">For more information about this solution, see hello Trend Micro blog post [Microsoft Azure VM Agent Extension For Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span></span>

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a><span data-ttu-id="f79a8-117">Instalar uma nova VM Olá profunda de segurança de agente</span><span class="sxs-lookup"><span data-stu-id="f79a8-117">Install hello Deep Security Agent on a new VM</span></span>

<span data-ttu-id="f79a8-118">Olá [portal do Azure](http://portal.azure.com) permite-lhe instalar extensão de segurança de tendência Micro Olá quando utiliza uma imagem de Olá **Marketplace** toocreate Olá máquina.</span><span class="sxs-lookup"><span data-stu-id="f79a8-118">hello [Azure portal](http://portal.azure.com) lets you install hello Trend Micro security extension when you use an image from hello **Marketplace** toocreate hello virtual machine.</span></span> <span data-ttu-id="f79a8-119">Se estiver a criar uma máquina virtual individual, através do portal Olá é uma proteção de tooadd de forma fácil de tendência Micro.</span><span class="sxs-lookup"><span data-stu-id="f79a8-119">If you're creating a single virtual machine, using hello portal is an easy way tooadd protection from Trend Micro.</span></span>

<span data-ttu-id="f79a8-120">Através de uma entrada de Olá **Marketplace** abre um assistente que o ajuda a configurar a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="f79a8-120">Using an entry from hello **Marketplace** opens a wizard that helps you set up hello virtual machine.</span></span> <span data-ttu-id="f79a8-121">Utilizar Olá **definições** painel, o painel de terceiro Olá do Assistente de Olá, tooinstall Olá extensão de segurança de tendência Micro.</span><span class="sxs-lookup"><span data-stu-id="f79a8-121">You use hello **Settings** blade, hello third panel of hello wizard, tooinstall hello Trend Micro security extension.</span></span>  <span data-ttu-id="f79a8-122">Para instruções gerais, consulte [criar uma máquina virtual com o Windows hello portal do Azure](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="f79a8-122">For general instructions, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>

<span data-ttu-id="f79a8-123">Quando obtiver toohello **definições** Olá painel do Assistente de Olá, os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f79a8-123">When you get toohello **Settings** blade of hello wizard, do hello following steps:</span></span>

1. <span data-ttu-id="f79a8-124">Clique em **extensões**, em seguida, clique em **Adicionar extensão** no painel seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="f79a8-124">Click **Extensions**, then click **Add extension** in hello next pane.</span></span>

   ![Começar a adicionar a extensão de Olá][1]

2. <span data-ttu-id="f79a8-126">Selecione **profunda de segurança de agente** no Olá **novo recurso** painel.</span><span class="sxs-lookup"><span data-stu-id="f79a8-126">Select **Deep Security Agent** in hello **New resource** pane.</span></span> <span data-ttu-id="f79a8-127">No painel de agente de segurança avançada de Olá, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="f79a8-127">In hello Deep Security Agent pane, click **Create**.</span></span>

   ![Identificar o agente de segurança avançada][2]

3. <span data-ttu-id="f79a8-129">Introduza Olá **identificador de inquilino** e **palavra-passe de ativação de inquilino** para extensão Olá.</span><span class="sxs-lookup"><span data-stu-id="f79a8-129">Enter hello **Tenant Identifier** and **Tenant Activation Password** for hello extension.</span></span> <span data-ttu-id="f79a8-130">Opcionalmente, pode introduzir um **identificador de política de segurança**.</span><span class="sxs-lookup"><span data-stu-id="f79a8-130">Optionally, you can enter a **Security Policy Identifier**.</span></span> <span data-ttu-id="f79a8-131">Em seguida, clique em **OK** cliente de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="f79a8-131">Then, click **OK** tooadd hello client.</span></span>

   ![Forneça detalhes de extensão][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a><span data-ttu-id="f79a8-133">Instalar Olá profunda de segurança de agente numa VM existente</span><span class="sxs-lookup"><span data-stu-id="f79a8-133">Install hello Deep Security Agent on an existing VM</span></span>
<span data-ttu-id="f79a8-134">agente de Olá tooinstall numa VM existente, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f79a8-134">tooinstall hello agent on an existing VM, you need hello following items:</span></span>

* <span data-ttu-id="f79a8-135">módulo do Azure PowerShell Olá, versão 0.8.2 ou mais recente, instalada no seu computador local.</span><span class="sxs-lookup"><span data-stu-id="f79a8-135">hello Azure PowerShell module, version 0.8.2 or newer, installed on your local computer.</span></span> <span data-ttu-id="f79a8-136">Pode verificar a versão de Olá do Azure PowerShell que tenha instalado utilizando Olá **azure Get-Module | versão de formato tabela** comando.</span><span class="sxs-lookup"><span data-stu-id="f79a8-136">You can check hello version of Azure PowerShell that you have installed by using hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="f79a8-137">Para obter instruções e uma versão mais recente do toohello de ligação, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f79a8-137">For instructions and a link toohello latest version, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="f79a8-138">Inicie sessão com a subscrição do Azure tooyour `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="f79a8-138">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="f79a8-139">Olá agente da VM instalado na máquina de virtual de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="f79a8-139">hello VM Agent installed on hello target virtual machine.</span></span>

<span data-ttu-id="f79a8-140">Em primeiro lugar, certifique-se que Olá que agente da VM já se encontra instalado.</span><span class="sxs-lookup"><span data-stu-id="f79a8-140">First, verify that hello VM Agent is already installed.</span></span> <span data-ttu-id="f79a8-141">Preencha o nome do serviço de nuvem de Olá e nome da máquina virtual em seguida, execute Olá os seguintes comandos uma linha de comandos do PowerShell do Azure de nível de administrador.</span><span class="sxs-lookup"><span data-stu-id="f79a8-141">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="f79a8-142">Substitua tudo dentro de aspas Olá, incluindo Olá < e > carateres.</span><span class="sxs-lookup"><span data-stu-id="f79a8-142">Replace everything within hello quotes, including hello < and > characters.</span></span>

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

<span data-ttu-id="f79a8-143">Se não souber o serviço em nuvem Olá e nome da máquina virtual, execute **Get-AzureVM** toodisplay que informações para todos os Olá máquinas virtuais na sua subscrição atual.</span><span class="sxs-lookup"><span data-stu-id="f79a8-143">If you don't know hello cloud service and virtual machine name, run **Get-AzureVM** toodisplay that information for all hello virtual machines in your current subscription.</span></span>

<span data-ttu-id="f79a8-144">Se hello **escrita anfitrião** comando devolve **verdadeiro**, Olá agente VM está instalado.</span><span class="sxs-lookup"><span data-stu-id="f79a8-144">If hello **write-host** command returns **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="f79a8-145">Se devolver **falso**, consulte as instruções de Olá e toohello uma hiperligação Transferir Olá mensagem de blogue do Azure [extensões - parte 2 e o agente da VM](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span><span class="sxs-lookup"><span data-stu-id="f79a8-145">If it returns **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span></span>

<span data-ttu-id="f79a8-146">Se Olá agente VM está instalado, execute estes comandos.</span><span class="sxs-lookup"><span data-stu-id="f79a8-146">If hello VM Agent is installed, run these commands.</span></span>

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="f79a8-147">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f79a8-147">Next steps</span></span>
<span data-ttu-id="f79a8-148">Demora alguns minutos para Olá toostart de agente em execução quando é instalado.</span><span class="sxs-lookup"><span data-stu-id="f79a8-148">It takes a few minutes for hello agent toostart running when it is installed.</span></span> <span data-ttu-id="f79a8-149">Depois disso, terá de tooactivate segurança profunda na máquina virtual de Olá, para que possa ser gerido por um Gestor de segurança avançada.</span><span class="sxs-lookup"><span data-stu-id="f79a8-149">After that, you need tooactivate Deep Security on hello virtual machine so it can be managed by a Deep Security Manager.</span></span> <span data-ttu-id="f79a8-150">Olá seguintes artigos para obter instruções adicionais, consulte:</span><span class="sxs-lookup"><span data-stu-id="f79a8-150">See hello following articles for additional instructions:</span></span>

* <span data-ttu-id="f79a8-151">Artigo da tendência sobre esta solução, [Instant-On Cloud Security para o Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span><span class="sxs-lookup"><span data-stu-id="f79a8-151">Trend's article about this solution, [Instant-On Cloud Security for Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span></span>
* <span data-ttu-id="f79a8-152">A [script do Windows PowerShell de exemplo](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure Olá máquina</span><span class="sxs-lookup"><span data-stu-id="f79a8-152">A [sample Windows PowerShell script](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure hello virtual machine</span></span>
* <span data-ttu-id="f79a8-153">[Instruções](http://go.microsoft.com/fwlink/?LinkId=404099) de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="f79a8-153">[Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) for hello sample</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f79a8-154">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f79a8-154">Additional resources</span></span>
<span data-ttu-id="f79a8-155">[Como toolog na máquina de virtual tooa com o Windows Server]</span><span class="sxs-lookup"><span data-stu-id="f79a8-155">[How toolog on tooa virtual machine running Windows Server]</span></span>

<span data-ttu-id="f79a8-156">[Extensões de VM do Azure e funcionalidades]</span><span class="sxs-lookup"><span data-stu-id="f79a8-156">[Azure VM Extensions and features]</span></span>

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[Como toolog na máquina de virtual tooa com o Windows Server]:connect-logon.md
[Extensões de VM do Azure e funcionalidades]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
