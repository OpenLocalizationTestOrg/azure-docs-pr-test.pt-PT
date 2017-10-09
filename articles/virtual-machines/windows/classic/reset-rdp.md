---
title: "aaaReset Olá palavra-passe ou a configuração de ambiente de trabalho remoto numa VM do Windows no Azure | Microsoft Docs"
description: "Saiba como tooreset uma palavra-passe de conta ou serviços de ambiente de trabalho remoto numa VM do Windows criada utilizando Olá clássico implementação modelo utilizando Olá portal do Azure ou do Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 1721a91fc6c89b46df74e76dfcf918b1c4c77a4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a><span data-ttu-id="435cb-103">Como o serviço de ambiente de trabalho remoto de Olá tooreset ou a palavra-passe de início de sessão numa Windows VM criados utilizando o modelo de implementação clássica Olá</span><span class="sxs-lookup"><span data-stu-id="435cb-103">How tooreset hello Remote Desktop service or its login password in a Windows VM created using hello Classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="435cb-104">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="435cb-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="435cb-105">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="435cb-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="435cb-106">A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="435cb-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="435cb-107">Também pode [executar estes passos para VMs criadas com o modelo de implementação do Resource Manager Olá](../reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="435cb-107">You can also [perform these steps for VMs created with hello Resource Manager deployment model](../reset-rdp.md).</span></span>

<span data-ttu-id="435cb-108">Se não conseguir ligar a máquina virtual (VM) do tooa Windows, pode repor a palavra-passe de administrador local do Olá ou reponha Olá configuração do serviço de ambiente de trabalho remoto.</span><span class="sxs-lookup"><span data-stu-id="435cb-108">If you can't connect tooa Windows virtual machine (VM), you can reset hello local administrator password or reset hello Remote Desktop service configuration.</span></span> <span data-ttu-id="435cb-109">Pode utilizar qualquer um dos Olá extensão de acesso de VM do Azure portal ou Olá na palavra-passe do Azure PowerShell tooreset Olá.</span><span class="sxs-lookup"><span data-stu-id="435cb-109">You can use either hello Azure portal or hello VM Access extension in Azure PowerShell tooreset hello password.</span></span>

## <a name="ways-tooreset-configuration-or-credentials"></a><span data-ttu-id="435cb-110">Configuração de tooreset formas ou credenciais</span><span class="sxs-lookup"><span data-stu-id="435cb-110">Ways tooreset configuration or credentials</span></span>
<span data-ttu-id="435cb-111">Pode repor os serviços de ambiente de trabalho remoto e as credenciais de diversas formas, consoante as suas necessidades:</span><span class="sxs-lookup"><span data-stu-id="435cb-111">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="435cb-112">Repor utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="435cb-112">Reset using hello Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="435cb-113">Repor com o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="435cb-113">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="435cb-114">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="435cb-114">Azure portal</span></span>
<span data-ttu-id="435cb-115">Pode utilizar Olá [portal do Azure](https://portal.azure.com) tooreset Olá serviço de ambiente de trabalho remoto.</span><span class="sxs-lookup"><span data-stu-id="435cb-115">You can use hello [Azure portal](https://portal.azure.com) tooreset hello Remote Desktop service.</span></span> <span data-ttu-id="435cb-116">menu do portal Olá tooexpand, clique em barras Olá três no canto superior esquerdo Olá e, em seguida, clique em **máquinas virtuais (clássicas)**:</span><span class="sxs-lookup"><span data-stu-id="435cb-116">tooexpand hello portal menu, click hello three bars in hello upper left corner and then click **Virtual machines (classic)**:</span></span>

![Navegue para a VM do Azure](./media/reset-rdp/Portal-Select-Classic-VM.png)

<span data-ttu-id="435cb-118">Selecione a máquina virtual do Windows e, em seguida, clique em **repor remoto...** . hello seguinte caixa de diálogo é apresentada a configuração de ambiente de trabalho remoto de Olá tooreset:</span><span class="sxs-lookup"><span data-stu-id="435cb-118">Select your Windows virtual machine and then click **Reset Remote...**. hello following dialog appears tooreset hello Remote Desktop configuration:</span></span>

![Página de configuração reposição RDP](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

<span data-ttu-id="435cb-120">Pode também repô Olá nome de utilizador e palavra-passe da conta de administrador local Olá.</span><span class="sxs-lookup"><span data-stu-id="435cb-120">You can also reset hello username and password of hello local administrator account.</span></span> <span data-ttu-id="435cb-121">A VM, clique em **suporte + resolução de problemas** > **Repor palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="435cb-121">From your VM, click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="435cb-122">é apresentado o painel de reposição de palavra-passe Olá:</span><span class="sxs-lookup"><span data-stu-id="435cb-122">hello password reset blade is displayed:</span></span>

![Página de reposição de palavra-passe](./media/reset-rdp/Portal-PW-Reset-Windows.png)

<span data-ttu-id="435cb-124">Depois de introduzir Olá novo nome de utilizador e a palavra-passe, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="435cb-124">After you enter hello new user name and password, click **Save**.</span></span>

## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="435cb-125">Extensão VMAccess e PowerShell</span><span class="sxs-lookup"><span data-stu-id="435cb-125">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="435cb-126">Certifique-se de que Olá que agente VM está instalado na máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="435cb-126">Make sure hello VM Agent is installed on hello virtual machine.</span></span> <span data-ttu-id="435cb-127">Olá extensão VMAccess não necessita de toobe instalado para poder utilizá-lo, desde que Olá agente VM está disponível.</span><span class="sxs-lookup"><span data-stu-id="435cb-127">hello VMAccess extension doesn't need toobe installed before you can use it, as long as hello VM Agent is available.</span></span> <span data-ttu-id="435cb-128">Certifique-se de que Olá que agente da VM já estiver instalado utilizando Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="435cb-128">Verify that hello VM Agent is already installed by using hello following command.</span></span> <span data-ttu-id="435cb-129">(Substituir "myCloudService" e "myVM" por nomes de Olá do seu serviço em nuvem e a VM, respetivamente.</span><span class="sxs-lookup"><span data-stu-id="435cb-129">(Replace "myCloudService" and "myVM" by hello names of your cloud service and your VM, respectively.</span></span> <span data-ttu-id="435cb-130">Pode obter estes nomes executando `Get-AzureVM` sem quaisquer parâmetros.)</span><span class="sxs-lookup"><span data-stu-id="435cb-130">You can learn these names by running `Get-AzureVM` without any parameters.)</span></span>

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="435cb-131">Se hello **escrita anfitrião** comando apresenta **verdadeiro**, Olá agente VM está instalado.</span><span class="sxs-lookup"><span data-stu-id="435cb-131">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="435cb-132">Se apresenta **falso**, consulte as instruções de Olá e toohello uma hiperligação Transferir Olá [extensões - parte 2 e o agente da VM](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) mensagem de blogue do Azure.</span><span class="sxs-lookup"><span data-stu-id="435cb-132">If it displays **False**, see hello instructions and a link toohello download in hello [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blog post.</span></span>

<span data-ttu-id="435cb-133">Se criou a máquina virtual de Olá através do portal Olá, verifique se `$vm.GetInstance().ProvisionGuestAgent` devolve **verdadeiro**.</span><span class="sxs-lookup"><span data-stu-id="435cb-133">If you created hello virtual machine by using hello portal, check whether `$vm.GetInstance().ProvisionGuestAgent` returns **True**.</span></span> <span data-ttu-id="435cb-134">Caso contrário, pode configurá-lo ao utilizar este comando:</span><span class="sxs-lookup"><span data-stu-id="435cb-134">If not, you can set it by using this command:</span></span>

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

<span data-ttu-id="435cb-135">Este comando impede Olá seguinte erro ao executar o Olá **conjunto AzureVMExtension** comando nos passos seguintes Olá: "Aprovisionar o agente convidado deve ser ativado no objeto VM Olá antes de definir a extensão de acesso de VM do IaaS."</span><span class="sxs-lookup"><span data-stu-id="435cb-135">This command prevents hello following error when you're running hello **Set-AzureVMExtension** command in hello next steps: “Provision Guest Agent must be enabled on hello VM object before setting IaaS VM Access Extension.”</span></span>

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="435cb-136">**Repor palavra-passe de conta de administrador local Olá**</span><span class="sxs-lookup"><span data-stu-id="435cb-136">**Reset hello local administrator account password**</span></span>
<span data-ttu-id="435cb-137">Criar uma credencial de início de sessão com o nome de conta de administrador local Olá atual e uma palavra-passe nova e, em seguida, execute Olá `Set-AzureVMAccessExtension` da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="435cb-137">Create a sign-in credential with hello current local administrator account name and a new password, and then run hello `Set-AzureVMAccessExtension` as follows.</span></span>

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

<span data-ttu-id="435cb-138">Se escrever um nome diferente conta atual de Olá, Olá extensão VMAccess muda o nome de conta de administrador local Olá, atribui a conta de toothat Olá palavras-passe e emite um ambiente de trabalho remoto fim de sessão. Se a conta de administrador local Olá estiver desativada, Olá extensão VMAccess ativa o mesmo.</span><span class="sxs-lookup"><span data-stu-id="435cb-138">If you type a different name than hello current account, hello VMAccess extension renames hello local administrator account, assigns hello password toothat account, and issues a Remote Desktop sign-out. If hello local administrator account is disabled, hello VMAccess extension enables it.</span></span>

<span data-ttu-id="435cb-139">Estes comandos também repor a configuração do serviço de ambiente de trabalho remoto de Olá.</span><span class="sxs-lookup"><span data-stu-id="435cb-139">These commands also reset hello Remote Desktop service configuration.</span></span>

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="435cb-140">**Repor a configuração do serviço de ambiente de trabalho remoto de Olá**</span><span class="sxs-lookup"><span data-stu-id="435cb-140">**Reset hello Remote Desktop service configuration**</span></span>
<span data-ttu-id="435cb-141">tooreset Olá ambiente de trabalho remoto a configuração do serviço, executar Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="435cb-141">tooreset hello Remote Desktop service configuration, run hello following command:</span></span>

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

<span data-ttu-id="435cb-142">Olá extensão VMAccess executa dois comandos na máquina virtual de Olá:</span><span class="sxs-lookup"><span data-stu-id="435cb-142">hello VMAccess extension runs two commands on hello virtual machine:</span></span>

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

<span data-ttu-id="435cb-143">Este comando activa grupo Firewall do Windows incorporado Olá que permita o tráfego recebido do ambiente de trabalho remoto, que utiliza a porta TCP 3389.</span><span class="sxs-lookup"><span data-stu-id="435cb-143">This command enables hello built-in Windows Firewall group that allows incoming Remote Desktop traffic, which uses TCP port 3389.</span></span>

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

<span data-ttu-id="435cb-144">Este comando define Olá fDenyTSConnections registo valor too0, ativação de ligações de ambiente de trabalho remoto.</span><span class="sxs-lookup"><span data-stu-id="435cb-144">This command sets hello fDenyTSConnections registry value too0, enabling Remote Desktop connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="435cb-145">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="435cb-145">Next steps</span></span>
<span data-ttu-id="435cb-146">Se não responde Olá extensão de acesso de VM do Azure e são palavra-passe do tooreset não é possível Olá, pode [reposição Olá Windows palavra-passe local offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="435cb-146">If hello Azure VM access extension does not respond and you are unable tooreset hello password, you can [reset hello local Windows password offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="435cb-147">Este método é um processo mais avançado e requer que tooconnect Olá disco rígido virtual Olá problemática VM tooanother VM.</span><span class="sxs-lookup"><span data-stu-id="435cb-147">This method is a more advanced process and requires you tooconnect hello virtual hard disk of hello problematic VM tooanother VM.</span></span> <span data-ttu-id="435cb-148">Siga os passos de Olá documentados neste artigo pela primeira vez e apenas a tentativa de método de reposição de palavra-passe offline Olá como último recurso.</span><span class="sxs-lookup"><span data-stu-id="435cb-148">Follow hello steps documented in this article first, and only attempt hello offline password reset method as a last resort.</span></span>

[<span data-ttu-id="435cb-149">Extensões VM do Azure e funcionalidades</span><span class="sxs-lookup"><span data-stu-id="435cb-149">Azure VM extensions and features</span></span>](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="435cb-150">Ligar tooan máquina virtual do Azure com RDP ou SSH</span><span class="sxs-lookup"><span data-stu-id="435cb-150">Connect tooan Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="435cb-151">Resolver problemas de ambiente de trabalho remoto ligações tooa baseados em Windows máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="435cb-151">Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine</span></span>](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

