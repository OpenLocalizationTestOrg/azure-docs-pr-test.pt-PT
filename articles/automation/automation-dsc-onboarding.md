---
title: "aaaOnboarding máquinas para gestão pelo Automation DSC do Azure | Microsoft Docs"
description: "Como toosetup máquinas para gestão com o Automation DSC do Azure"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: ef15801fec2ffea4ba62dcba2fbe9af09268e424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a><span data-ttu-id="49ac9-103">Máquinas de integração de gestão do Automation DSC do Azure</span><span class="sxs-lookup"><span data-stu-id="49ac9-103">Onboarding machines for management by Azure Automation DSC</span></span>

## <a name="why-manage-machines-with-azure-automation-dsc"></a><span data-ttu-id="49ac9-104">Por que motivo gerir máquinas com o Automation DSC do Azure?</span><span class="sxs-lookup"><span data-stu-id="49ac9-104">Why manage machines with Azure Automation DSC?</span></span>

<span data-ttu-id="49ac9-105">Como [configuração de estado pretendido do PowerShell](https://technet.microsoft.com/library/dn249912.aspx), a configuração de estado pretendido do Azure Automation é um serviço de gestão de configuração de simples, mas poderosa, para nós de DSC (máquinas virtuais e físicas) no Centro de dados qualquer nuvem ou no local.</span><span class="sxs-lookup"><span data-stu-id="49ac9-105">Like [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is a simple, yet powerful, configuration management service for DSC nodes (physical and virtual machines) in any cloud or on-premises datacenter.</span></span> <span data-ttu-id="49ac9-106">Permite que escalabilidade entre milhares de máquinas forma rápida e fácil de uma localização central e segura.</span><span class="sxs-lookup"><span data-stu-id="49ac9-106">It enables scalability across thousands of machines quickly and easily from a central, secure location.</span></span> <span data-ttu-id="49ac9-107">Pode carregar facilmente máquinas, atribua-as configurações declarativas e ver relatórios, que mostra cada computador do que especificou o estado de compatibilidade toohello assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="49ac9-107">You can easily onboard machines, assign them declarative configurations, and view reports showing each machine's compliance toohello desired state you specified.</span></span> <span data-ttu-id="49ac9-108">camada de gestão do Azure Automation DSC Olá é tooDSC camada de gestão de automatização do Azure que Olá é tooPowerShell scripting.</span><span class="sxs-lookup"><span data-stu-id="49ac9-108">hello Azure Automation DSC management layer is tooDSC what hello Azure Automation management layer is tooPowerShell scripting.</span></span> <span data-ttu-id="49ac9-109">Por outras palavras, de Olá mesma maneira que a automatização do Azure ajuda-o a gerir os scripts do PowerShell, também o ajuda a gerir configurações de DSC.</span><span class="sxs-lookup"><span data-stu-id="49ac9-109">In other words, in hello same way that Azure Automation helps you manage PowerShell scripts, it also helps you manage DSC configurations.</span></span> <span data-ttu-id="49ac9-110">toolearn mais informações sobre os benefícios de Olá da utilização do Automation DSC do Azure, consulte [descrição geral do Azure Automation DSC](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="49ac9-110">toolearn more about hello benefits of using Azure Automation DSC, see [Azure Automation DSC overview](automation-dsc-overview.md).</span></span>

<span data-ttu-id="49ac9-111">Automation DSC do Azure pode ser utilizado toomanage uma variedade de máquinas:</span><span class="sxs-lookup"><span data-stu-id="49ac9-111">Azure Automation DSC can be used toomanage a variety of machines:</span></span>

* <span data-ttu-id="49ac9-112">Máquinas virtuais do Azure (clássica)</span><span class="sxs-lookup"><span data-stu-id="49ac9-112">Azure virtual machines (classic)</span></span>
* <span data-ttu-id="49ac9-113">Máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="49ac9-113">Azure virtual machines</span></span>
* <span data-ttu-id="49ac9-114">Máquinas virtuais Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="49ac9-114">Amazon Web Services (AWS) virtual machines</span></span>
* <span data-ttu-id="49ac9-115">Windows físico virtual máquinas no local, ou numa nuvem diferente do Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="49ac9-115">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>
* <span data-ttu-id="49ac9-116">Linux físico virtual máquinas no local, no Azure ou numa nuvem diferente do Azure</span><span class="sxs-lookup"><span data-stu-id="49ac9-116">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="49ac9-117">Além disso, se não estiver pronta toomanage configuração da máquina da nuvem Olá, DSC de automatização do Azure também pode ser utilizado como um ponto final só de relatório.</span><span class="sxs-lookup"><span data-stu-id="49ac9-117">In addition, if you are not ready toomanage machine configuration from hello cloud, Azure Automation DSC can also be used as a report-only endpoint.</span></span> <span data-ttu-id="49ac9-118">Isto permite configuração pretendida do tooset (emitir) através do DSC no local e ver detalhes relatórios avançados de conformidade de nó com Olá pretendido estado na automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="49ac9-118">This allows you tooset (push) desired configuration through DSC on-premises and view rich reporting details on node compliance with hello desired state in Azure Automation.</span></span>

<span data-ttu-id="49ac9-119">Olá seguintes secções descrevem como pode carregar cada tipo de máquina tooAzure DSC de automatização.</span><span class="sxs-lookup"><span data-stu-id="49ac9-119">hello following sections outline how you can onboard each type of machine tooAzure Automation DSC.</span></span>

## <a name="azure-virtual-machines-classic"></a><span data-ttu-id="49ac9-120">Máquinas virtuais do Azure (clássica)</span><span class="sxs-lookup"><span data-stu-id="49ac9-120">Azure virtual machines (classic)</span></span>

<span data-ttu-id="49ac9-121">Com o DSC de automatização do Azure, pode facilmente carregar virtual machines do Azure (clássica) para gestão de configuração utilizando o Olá portal do Azure ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49ac9-121">With Azure Automation DSC, you can easily onboard Azure virtual machines (classic) for configuration management using either hello Azure portal, or PowerShell.</span></span> <span data-ttu-id="49ac9-122">Em definições avançadas de Olá e sem um administrador ter tooremote para Olá VM, Olá extensão de configuração de estado pretendido do Azure VM regista Olá VM no Automation DSC do Azure.</span><span class="sxs-lookup"><span data-stu-id="49ac9-122">Under hello hood, and without an administrator having tooremote into hello VM, hello Azure VM Desired State Configuration extension registers hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="49ac9-123">Uma vez que Olá extensão de configuração de estado pretendido do Azure VM é executado no modo assíncrono, passos tootrack progresso dela ou resolver problemas são fornecidos na Olá [ **integração de máquina virtual do Azure de resolução de problemas** ](#troubleshooting-azure-virtual-machine-onboarding)secção abaixo.</span><span class="sxs-lookup"><span data-stu-id="49ac9-123">Since hello Azure VM Desired State Configuration extension runs asynchronously, steps tootrack its progress or troubleshoot it are provided in hello [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="49ac9-124">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="49ac9-124">Azure portal</span></span>

<span data-ttu-id="49ac9-125">No Olá [portal do Azure](http://portal.azure.com/), clique em **procurar** -> **máquinas virtuais (clássicas)**.</span><span class="sxs-lookup"><span data-stu-id="49ac9-125">In hello [Azure portal](http://portal.azure.com/), click **Browse** -> **Virtual machines (classic)**.</span></span> <span data-ttu-id="49ac9-126">Selecione Olá VM do Windows que pretende tooonboard.</span><span class="sxs-lookup"><span data-stu-id="49ac9-126">Select hello Windows VM you want tooonboard.</span></span> <span data-ttu-id="49ac9-127">No painel de dashboard da máquina virtual Olá, clique em **todas as definições** -> **extensões** -> **adicionar**  ->   **Automation DSC do Azure** -> **criar**.</span><span class="sxs-lookup"><span data-stu-id="49ac9-127">On hello virtual machine's dashboard blade, click **All settings** -> **Extensions** -> **Add** -> **Azure Automation DSC** -> **Create**.</span></span> <span data-ttu-id="49ac9-128">Introduza Olá [valores de Gestor de configuração Local do PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) necessários para o caso de utilização, chave de registo da sua conta de automatização e URL de registo e, opcionalmente, um toohello de tooassign de configuração de nó VM.</span><span class="sxs-lookup"><span data-stu-id="49ac9-128">Enter hello [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, your Automation account's registration key and registration URL, and optionally a node configuration tooassign toohello VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

<span data-ttu-id="49ac9-129">URL de registo de Olá toofind e a chave para a máquina Olá tooonboard de conta de automatização de Olá, consulte Olá [ **Secure registo** ](#secure-registration) secção abaixo.</span><span class="sxs-lookup"><span data-stu-id="49ac9-129">toofind hello registration URL and key for hello Automation account tooonboard hello machine to, see hello [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="49ac9-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="49ac9-130">PowerShell</span></span>

```powershell
# log in tooboth Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in hello name of a Node Configuration in Azure Automation DSC, for this VM tooconform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use hello DSC extension tooonboard hello VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a><span data-ttu-id="49ac9-131">Máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="49ac9-131">Azure virtual machines</span></span>

<span data-ttu-id="49ac9-132">Automation DSC do Azure permite carregar facilmente máquinas virtuais do Azure para a gestão de configuração, utilizando o portal do Azure de Olá, modelos Azure Resource Manager ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49ac9-132">Azure Automation DSC lets you easily onboard Azure virtual machines for configuration management, using either hello Azure portal, Azure Resource Manager templates, or PowerShell.</span></span> <span data-ttu-id="49ac9-133">Em definições avançadas de Olá e sem um administrador ter tooremote para Olá VM, Olá extensão de configuração de estado pretendido do Azure VM regista Olá VM no Automation DSC do Azure.</span><span class="sxs-lookup"><span data-stu-id="49ac9-133">Under hello hood, and without an administrator having tooremote into hello VM, hello Azure VM Desired State Configuration extension registers hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="49ac9-134">Uma vez que Olá extensão de configuração de estado pretendido do Azure VM é executado no modo assíncrono, passos tootrack progresso dela ou resolver problemas são fornecidos na Olá [ **integração de máquina virtual do Azure de resolução de problemas** ](#troubleshooting-azure-virtual-machine-onboarding)secção abaixo.</span><span class="sxs-lookup"><span data-stu-id="49ac9-134">Since hello Azure VM Desired State Configuration extension runs asynchronously, steps tootrack its progress or troubleshoot it are provided in hello [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="49ac9-135">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="49ac9-135">Azure portal</span></span>

<span data-ttu-id="49ac9-136">No Olá [portal do Azure](https://portal.azure.com/), navegue até toohello conta de automatização do Azure onde pretende que as máquinas virtuais de tooonboard.</span><span class="sxs-lookup"><span data-stu-id="49ac9-136">In hello [Azure portal](https://portal.azure.com/), navigate toohello Azure Automation account where you want tooonboard virtual machines.</span></span> <span data-ttu-id="49ac9-137">No painel de conta de automatização de Olá, clique em **nós de DSC** -> **adicionar a VM do Azure**.</span><span class="sxs-lookup"><span data-stu-id="49ac9-137">On hello Automation account dashboard, click **DSC Nodes** -> **Add Azure VM**.</span></span>

<span data-ttu-id="49ac9-138">Em **selecionar máquinas virtuais tooonboard**, selecione um ou mais Azure virtual máquinas tooonboard.</span><span class="sxs-lookup"><span data-stu-id="49ac9-138">Under **Select virtual machines tooonboard**, select one or more Azure virtual machines tooonboard.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

<span data-ttu-id="49ac9-139">Em **configurar dados de registo**, introduza Olá [valores de Gestor de configuração Local do PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) necessários para o caso de utilização e opcionalmente um toohello de tooassign de configuração de nó VM.</span><span class="sxs-lookup"><span data-stu-id="49ac9-139">Under **Configure registration data**, enter hello [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, and optionally a node configuration tooassign toohello VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="49ac9-140">Modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="49ac9-140">Azure Resource Manager templates</span></span>

<span data-ttu-id="49ac9-141">Máquinas virtuais do Azure pode ser implementadas e simplificar tooAzure Automation DSC através de modelos Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="49ac9-141">Azure virtual machines can be deployed and onboarded tooAzure Automation DSC via Azure Resource Manager templates.</span></span> <span data-ttu-id="49ac9-142">Consulte [configurar uma VM através de extensão de DSC e Automation DSC do Azure](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) para um modelo de exemplo que onboards um tooAzure VM existente DSC de automatização.</span><span class="sxs-lookup"><span data-stu-id="49ac9-142">See [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) for an example template that onboards an existing VM tooAzure Automation DSC.</span></span> <span data-ttu-id="49ac9-143">toofind Olá chave e o registo do URL de registo tomada como entrada neste modelo, consulte Olá [ **Secure registo** ](#secure-registration) secção abaixo.</span><span class="sxs-lookup"><span data-stu-id="49ac9-143">toofind hello registration key and registration URL taken as input in this template, see hello [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="49ac9-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="49ac9-144">PowerShell</span></span>

<span data-ttu-id="49ac9-145">Olá [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet pode ser utilizado tooonboard máquinas virtuais Olá portal do Azure através do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49ac9-145">hello [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet can be used tooonboard virtual machines in hello Azure portal via PowerShell.</span></span>

## <a name="amazon-web-services-aws-virtual-machines"></a><span data-ttu-id="49ac9-146">Máquinas virtuais Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="49ac9-146">Amazon Web Services (AWS) virtual machines</span></span>

<span data-ttu-id="49ac9-147">Pode carregar facilmente máquinas de virtuais Amazon Web Services para a gestão de configuração ao utilizar Olá AWS DSC Toolkit de Automation DSC do Azure.</span><span class="sxs-lookup"><span data-stu-id="49ac9-147">You can easily onboard Amazon Web Services virtual machines for configuration management by Azure Automation DSC using hello AWS DSC Toolkit.</span></span> <span data-ttu-id="49ac9-148">Pode saber mais sobre o toolkit de Olá [aqui](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span><span class="sxs-lookup"><span data-stu-id="49ac9-148">You can learn more about hello toolkit [here](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span></span>

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a><span data-ttu-id="49ac9-149">Windows físico virtual máquinas no local, ou numa nuvem diferente do Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="49ac9-149">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>

<span data-ttu-id="49ac9-150">Máquinas do Windows no local e as máquinas do Windows em nuvens não do Azure (por exemplo, Amazon Web Services) também podem ser integrado tooAzure DSC de automatização, desde que têm acesso de saída toohello à internet, através de alguns passos simples:</span><span class="sxs-lookup"><span data-stu-id="49ac9-150">On-premises Windows machines and Windows machines in non-Azure clouds (such as Amazon Web Services) can also be onboarded tooAzure Automation DSC, as long as they have outbound access toohello internet, via a few simple steps:</span></span>

1. <span data-ttu-id="49ac9-151">Certifique-se de que versão mais recente de Olá do [WMF 5](http://aka.ms/wmf5latest) está instalado em máquinas de Olá pretende tooonboard tooAzure DSC de automatização.</span><span class="sxs-lookup"><span data-stu-id="49ac9-151">Make sure hello latest version of [WMF 5](http://aka.ms/wmf5latest) is installed on hello machines you want tooonboard tooAzure Automation DSC.</span></span>
2. <span data-ttu-id="49ac9-152">Siga as indicações Olá secção [ **gerar DSC metaconfigurations** ](#generating-dsc-metaconfigurations) abaixo toogenerate uma pasta que contém Olá necessário metaconfigurations de DSC.</span><span class="sxs-lookup"><span data-stu-id="49ac9-152">Follow hello directions in section [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) below toogenerate a folder containing hello needed DSC metaconfigurations.</span></span>
3. <span data-ttu-id="49ac9-153">Aplica remotamente Olá PowerShell DSC configuração meta toohello as máquinas que pretende tooonboard.</span><span class="sxs-lookup"><span data-stu-id="49ac9-153">Remotely apply hello PowerShell DSC metaconfiguration toohello machines you want tooonboard.</span></span> <span data-ttu-id="49ac9-154">**Este comando é executado a partir de máquina de Olá tem de ter a versão mais recente do Olá do [WMF 5](http://aka.ms/wmf5latest) instalado**:</span><span class="sxs-lookup"><span data-stu-id="49ac9-154">**hello machine this command is run from must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed**:</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. <span data-ttu-id="49ac9-155">Se não é possível aplicar Olá PowerShell DSC metaconfigurations remotamente, copie a pasta de metaconfigurations de Olá do passo 2 para cada máquina tooonboard.</span><span class="sxs-lookup"><span data-stu-id="49ac9-155">If you cannot apply hello PowerShell DSC metaconfigurations remotely, copy hello metaconfigurations folder from step 2 onto each machine tooonboard.</span></span> <span data-ttu-id="49ac9-156">Em seguida, chame **conjunto DscLocalConfigurationManager** localmente em cada máquina tooonboard.</span><span class="sxs-lookup"><span data-stu-id="49ac9-156">Then call **Set-DscLocalConfigurationManager** locally on each machine tooonboard.</span></span>
5. <span data-ttu-id="49ac9-157">Utilizar Olá portal do Azure ou os cmdlets, verifique se Olá máquinas tooonboard agora aparecem como nós de DSC registado na sua conta de automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="49ac9-157">Using hello Azure portal or cmdlets, check that hello machines tooonboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a><span data-ttu-id="49ac9-158">Linux físico virtual máquinas no local, no Azure ou numa nuvem diferente do Azure</span><span class="sxs-lookup"><span data-stu-id="49ac9-158">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="49ac9-159">As máquinas no local Linux, computadores Linux no Azure, e computadores Linux no Azure não nuvens também podem ser integrado tooAzure DSC de automatização, desde que têm acesso de saída toohello à internet, através de alguns passos simples:</span><span class="sxs-lookup"><span data-stu-id="49ac9-159">On-premises Linux machines, Linux machines in Azure, and Linux machines in non-Azure clouds can also be onboarded tooAzure Automation DSC, as long as they have outbound access toohello internet, via a few simple steps:</span></span>

1. <span data-ttu-id="49ac9-160">Certifique-se de que versão mais recente de Olá do [PowerShell configuração de estado pretendido para Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) está instalado em máquinas de Olá pretende tooonboard tooAzure DSC de automatização.</span><span class="sxs-lookup"><span data-stu-id="49ac9-160">Make sure hello latest version of [PowerShell Desired State Configuration for Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is installed on hello machines you want tooonboard tooAzure Automation DSC.</span></span>
2. <span data-ttu-id="49ac9-161">Se Olá [predefinições do Gestor de configuração Local do PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) corresponder ao seu caso de utilização e pretender tooonboard máquinas tais que estes **ambos** solicitar a partir e comunicar tooAzure DSC de automatização:</span><span class="sxs-lookup"><span data-stu-id="49ac9-161">If hello [PowerShell DSC Local Configuration Manager defaults](https://msdn.microsoft.com/powershell/dsc/metaconfig4) match your use case, and you want tooonboard machines such that they **both** pull from and report tooAzure Automation DSC:</span></span>

   + <span data-ttu-id="49ac9-162">Na máquina tooonboard tooAzure Automation DSC cada Linux, utilize tooonboard Register.py Olá predefinições do Gestor de configuração Local do PowerShell DSC a utilizar:</span><span class="sxs-lookup"><span data-stu-id="49ac9-162">On each Linux machine tooonboard tooAzure Automation DSC, use Register.py tooonboard using hello PowerShell DSC Local Configuration Manager defaults:</span></span>

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + <span data-ttu-id="49ac9-163">toofind Olá chave e o registo do URL de registo para a sua conta de automatização, consulte Olá [ **Secure registo** ](#secure-registration) secção abaixo.</span><span class="sxs-lookup"><span data-stu-id="49ac9-163">toofind hello registration key and registration URL for your Automation account, see hello [**Secure registration**](#secure-registration) section below.</span></span>

     <span data-ttu-id="49ac9-164">Se hello predefinições do Gestor de configuração Local do PowerShell DSC **fazer** **não** corresponder ao seu caso de utilização ou se quiser tooonboard máquinas de forma a que estes apenas comunicam tooAzure DSC de automatização, mas não solicitar a configuração ou de módulos do PowerShell a partir do mesmo, siga os passos 3 a 6.</span><span class="sxs-lookup"><span data-stu-id="49ac9-164">If hello PowerShell DSC Local Configuration Manager defaults **do** **not** match your use case, or you want tooonboard machines such that they only report tooAzure Automation DSC, but do not pull configuration or PowerShell modules from it,  follow steps 3 - 6.</span></span> <span data-ttu-id="49ac9-165">Caso contrário, avance diretamente toostep 6.</span><span class="sxs-lookup"><span data-stu-id="49ac9-165">Otherwise, proceed directly toostep 6.</span></span>

3. <span data-ttu-id="49ac9-166">Siga as indicações de Olá Olá [ **gerar DSC metaconfigurations** ](#generating-dsc-metaconfigurations) secção abaixo toogenerate uma pasta que contém Olá necessário metaconfigurations de DSC.</span><span class="sxs-lookup"><span data-stu-id="49ac9-166">Follow hello directions in hello [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) section below toogenerate a folder containing hello needed DSC metaconfigurations.</span></span>
4. <span data-ttu-id="49ac9-167">Aplicar remotamente Olá PowerShell DSC configuração meta toohello as máquinas que pretende tooonboard:</span><span class="sxs-lookup"><span data-stu-id="49ac9-167">Remotely apply hello PowerShell DSC metaconfiguration toohello machines you want tooonboard:</span></span>

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

<span data-ttu-id="49ac9-168">Este comando é executado a partir de máquina de Olá tem de ter a versão mais recente do Olá do [WMF 5](http://aka.ms/wmf5latest) instalado.</span><span class="sxs-lookup"><span data-stu-id="49ac9-168">hello machine this command is run from must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>

1. <span data-ttu-id="49ac9-169">Se não é possível aplicar Olá PowerShell DSC metaconfigurations remotamente, tooonboard cada computador Linux, copie a máquina de toothat correspondente do Olá configuração meta da pasta de Olá no passo 5 na máquina de Linux Olá.</span><span class="sxs-lookup"><span data-stu-id="49ac9-169">If you cannot apply hello PowerShell DSC metaconfigurations remotely, for each Linux machine tooonboard, copy hello metaconfiguration corresponding toothat machine from hello folder in step 5 onto hello Linux machine.</span></span> <span data-ttu-id="49ac9-170">Em seguida, chame `SetDscLocalConfigurationManager.py` localmente em cada computador Linux que pretende tooonboard tooAzure DSC de automatização:</span><span class="sxs-lookup"><span data-stu-id="49ac9-170">Then call `SetDscLocalConfigurationManager.py` locally on each Linux machine you want tooonboard tooAzure Automation DSC:</span></span>

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. <span data-ttu-id="49ac9-171">Utilizar Olá portal do Azure ou os cmdlets, verifique se Olá máquinas tooonboard agora aparecem como nós de DSC registado na sua conta de automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="49ac9-171">Using hello Azure portal or cmdlets, check that hello machines tooonboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="generating-dsc-metaconfigurations"></a><span data-ttu-id="49ac9-172">Gerar DSC metaconfigurations</span><span class="sxs-lookup"><span data-stu-id="49ac9-172">Generating DSC metaconfigurations</span></span>

<span data-ttu-id="49ac9-173">toogenerically carregar qualquer máquina tooAzure DSC de automatização, um [configuração meta do DSC](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) pode ser gerada que, quando aplicada, diz ao agente Olá DSC no Olá máquina toopull de e/ou relatório tooAzure DSC de automatização.</span><span class="sxs-lookup"><span data-stu-id="49ac9-173">toogenerically onboard any machine tooAzure Automation DSC, a [DSC metaconfiguration](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) can be generated that, when applied, tells hello DSC agent on hello machine toopull from and/or report tooAzure Automation DSC.</span></span> <span data-ttu-id="49ac9-174">DSC metaconfigurations para Automation DSC do Azure pode ser gerada através de uma configuração de DSC do PowerShell, ou Olá cmdlets do PowerShell de automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="49ac9-174">DSC metaconfigurations for Azure Automation DSC can be generated using either a PowerShell DSC configuration, or hello Azure Automation PowerShell cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="49ac9-175">DSC metaconfigurations conter Olá segredos necessários tooonboard uma conta de automatização para a gestão de tooan máquina.</span><span class="sxs-lookup"><span data-stu-id="49ac9-175">DSC metaconfigurations contain hello secrets needed tooonboard a machine tooan Automation account for management.</span></span> <span data-ttu-id="49ac9-176">Certifique-se de que tooproperly proteger qualquer metaconfigurations DSC que criar ou eliminá-los após a utilização.</span><span class="sxs-lookup"><span data-stu-id="49ac9-176">Make sure tooproperly protect any DSC metaconfigurations you create, or delete them after use.</span></span>

### <a name="using-a-dsc-configuration"></a><span data-ttu-id="49ac9-177">Utilizar uma configuração de DSC</span><span class="sxs-lookup"><span data-stu-id="49ac9-177">Using a DSC Configuration</span></span>

1. <span data-ttu-id="49ac9-178">Abra Olá ISE do PowerShell como administrador num computador do ambiente local.</span><span class="sxs-lookup"><span data-stu-id="49ac9-178">Open hello PowerShell ISE as an administrator in a machine in your local environment.</span></span> <span data-ttu-id="49ac9-179">máquina Olá tem de ter a versão mais recente do Olá do [WMF 5](http://aka.ms/wmf5latest) instalado.</span><span class="sxs-lookup"><span data-stu-id="49ac9-179">hello machine must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>
2. <span data-ttu-id="49ac9-180">Copie Olá seguir o script localmente.</span><span class="sxs-lookup"><span data-stu-id="49ac9-180">Copy hello following script locally.</span></span> <span data-ttu-id="49ac9-181">Este script contém uma configuração de DSC do PowerShell para criar metaconfigurations e tookick um comando desativar a criação de configuração meta Olá.</span><span class="sxs-lookup"><span data-stu-id="49ac9-181">This script contains a PowerShell DSC configuration for creating metaconfigurations, and a command tookick off hello metaconfiguration creation.</span></span>

    ```powershell
    # hello DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create hello metaconfigurations
    # TODO: edit hello below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM tooonboard>', '<some other VM tooonboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set too$True toohave machines only report tooAA DSC but not pull from it
    }

    # Use PowerShell splatting toopass parameters toohello DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. <span data-ttu-id="49ac9-182">Preencha chave de registo Olá e o URL para a sua conta de automatização, bem como os nomes de Olá de Olá máquinas tooonboard.</span><span class="sxs-lookup"><span data-stu-id="49ac9-182">Fill in hello registration key and URL for your Automation account, as well as hello names of hello machines tooonboard.</span></span> <span data-ttu-id="49ac9-183">Todos os outros parâmetros são opcionais.</span><span class="sxs-lookup"><span data-stu-id="49ac9-183">All other parameters are optional.</span></span> <span data-ttu-id="49ac9-184">toofind Olá chave e o registo do URL de registo para a sua conta de automatização, consulte Olá [ **Secure registo** ](#secure-registration) secção abaixo.</span><span class="sxs-lookup"><span data-stu-id="49ac9-184">toofind hello registration key and registration URL for your Automation account, see hello [**Secure registration**](#secure-registration) section below.</span></span>
4. <span data-ttu-id="49ac9-185">Se pretender Olá máquinas tooreport DSC Estado informações tooAzure DSC de automatização, mas não solicitar a configuração ou de módulos do PowerShell, defina Olá **ReportOnly** tootrue de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="49ac9-185">If you want hello machines tooreport DSC status information tooAzure Automation DSC, but not pull configuration or PowerShell modules, set hello **ReportOnly** parameter tootrue.</span></span>
5. <span data-ttu-id="49ac9-186">Execute script de Olá.</span><span class="sxs-lookup"><span data-stu-id="49ac9-186">Run hello script.</span></span> <span data-ttu-id="49ac9-187">Agora, deve ter uma pasta denominada **DscMetaConfigs** no seu diretório de trabalho, que contém Olá PowerShell DSC metaconfigurations para Olá máquinas tooonboard (como administrador):</span><span class="sxs-lookup"><span data-stu-id="49ac9-187">You should now have a folder called **DscMetaConfigs** in your working directory, containing hello PowerShell DSC metaconfigurations for hello machines tooonboard (as an administrator):</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a><span data-ttu-id="49ac9-188">Utilizar cmdlets de automatização do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="49ac9-188">Using hello Azure Automation cmdlets</span></span>

<span data-ttu-id="49ac9-189">Se as predefinições do Gestor de configuração Local do PowerShell DSC de Olá corresponder ao seu caso de utilização e pretende tooonboard máquinas para que possam tanto solicitar a partir e comunicam tooAzure DSC de automatização, Olá cmdlets de automatização do Azure fornecem um método simplificado de gerar Olá DSC metaconfigurations necessário:</span><span class="sxs-lookup"><span data-stu-id="49ac9-189">If hello PowerShell DSC Local Configuration Manager defaults match your use case, and you want tooonboard machines such that they both pull from and report tooAzure Automation DSC, hello Azure Automation cmdlets provide a simplified method of generating hello DSC metaconfigurations needed:</span></span>

1. <span data-ttu-id="49ac9-190">Abra a consola do PowerShell Olá ou o ISE do PowerShell como administrador numa máquina no seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="49ac9-190">Open hello PowerShell console or PowerShell ISE as an administrator in a machine in your local environment.</span></span>
2. <span data-ttu-id="49ac9-191">Ligar através do Gestor de recursos de tooAzure **Add-AzureRmAccount**</span><span class="sxs-lookup"><span data-stu-id="49ac9-191">Connect tooAzure Resource Manager using **Add-AzureRmAccount**</span></span>
3. <span data-ttu-id="49ac9-192">Transferir Olá PowerShell DSC metaconfigurations para máquinas de Olá pretende tooonboard de Olá automatização conta toowhich pretende tooonboard nós:</span><span class="sxs-lookup"><span data-stu-id="49ac9-192">Download hello PowerShell DSC metaconfigurations for hello machines you want tooonboard from hello Automation account toowhich you want tooonboard nodes:</span></span>

    ```powershell
    # Define hello parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # hello name of hello ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # hello name of hello Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # hello names of hello computers that hello meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting toopass parameters toohello Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. <span data-ttu-id="49ac9-193">Agora, deve ter uma pasta denominada ***DscMetaConfigs***, que contém Olá PowerShell DSC metaconfigurations para Olá máquinas tooonboard (como administrador):</span><span class="sxs-lookup"><span data-stu-id="49ac9-193">You should now have a folder called ***DscMetaConfigs***, containing hello PowerShell DSC metaconfigurations for hello machines tooonboard (as an administrator):</span></span>
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a><span data-ttu-id="49ac9-194">Registo seguro</span><span class="sxs-lookup"><span data-stu-id="49ac9-194">Secure registration</span></span>

<span data-ttu-id="49ac9-195">Máquinas podem integrar com segurança tooan conta de automatização do Azure através do protocolo de registo do Olá WMF 5 DSC, que permite que um nó tooauthenticate tooa PowerShell DSC V2 solicitar ou relatórios servidor DSC (incluindo o Automation DSC do Azure).</span><span class="sxs-lookup"><span data-stu-id="49ac9-195">Machines can securely onboard tooan Azure Automation account through hello WMF 5 DSC registration protocol, which allows a DSC node tooauthenticate tooa PowerShell DSC V2 Pull or Reporting server (including Azure Automation DSC).</span></span> <span data-ttu-id="49ac9-196">nó Olá regista o servidor de toohello num **URL de registo**, autenticação utilizando um **chave de registo**.</span><span class="sxs-lookup"><span data-stu-id="49ac9-196">hello node registers toohello server at a **Registration URL**, authenticating using a **Registration key**.</span></span> <span data-ttu-id="49ac9-197">Durante o registo no nó de Olá DSC e servidor de solicitação do DSC/relatórios negociar um certificado exclusivo para este toouse do nó para autenticação toohello pós-o registo do servidor.</span><span class="sxs-lookup"><span data-stu-id="49ac9-197">During registration, hello DSC node and DSC Pull/Reporting server negotiate a unique certificate for this node toouse for authentication toohello server post-registration.</span></span> <span data-ttu-id="49ac9-198">Este processo impede que nós de integrado de representar um que outro, por exemplo, se um nó for comprometido e comportam de forma maliciosa.</span><span class="sxs-lookup"><span data-stu-id="49ac9-198">This process prevents onboarded nodes from impersonating one another, such as if a node is compromised and behaving maliciously.</span></span> <span data-ttu-id="49ac9-199">Após o registo, a chave de registo Olá não é utilizado para autenticação novamente e é eliminado do nó de Olá.</span><span class="sxs-lookup"><span data-stu-id="49ac9-199">After registration, hello Registration key is not used for authentication again, and is deleted from hello node.</span></span>

<span data-ttu-id="49ac9-200">Pode obter informações de Olá necessárias para o protocolo de registo de Olá DSC de Olá **gerir chaves** painel no portal de pré-visualização do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="49ac9-200">You can get hello information required for hello DSC registration protocol from hello **Manage Keys** blade in hello Azure preview portal.</span></span> <span data-ttu-id="49ac9-201">Abrir este painel clicando no ícone chave Olá no Olá **Essentials** painel para Olá conta de automatização.</span><span class="sxs-lookup"><span data-stu-id="49ac9-201">Open this blade by clicking hello key icon on hello **Essentials** panel for hello Automation account.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* <span data-ttu-id="49ac9-202">URL de registo é o campo de URL de Olá no painel de gerir chaves de Olá.</span><span class="sxs-lookup"><span data-stu-id="49ac9-202">Registration URL is hello URL field in hello Manage Keys blade.</span></span>
* <span data-ttu-id="49ac9-203">Chave de registo é Olá chave de acesso primária ou secundária a chave de acesso no painel de gerir chaves de Olá.</span><span class="sxs-lookup"><span data-stu-id="49ac9-203">Registration key is hello Primary Access Key or Secondary Access Key in hello Manage Keys blade.</span></span> <span data-ttu-id="49ac9-204">A chave pode ser utilizada.</span><span class="sxs-lookup"><span data-stu-id="49ac9-204">Either key can be used.</span></span>

<span data-ttu-id="49ac9-205">Para segurança adicional, chaves de acesso primária e secundária Olá de uma conta de automatização podem ser novamente geradas em qualquer altura (no Olá **gerir chaves** painel) registos de nó futuras tooprevent utilizando chaves anteriores.</span><span class="sxs-lookup"><span data-stu-id="49ac9-205">For added security, hello primary and secondary access keys of an Automation account can be regenerated at any time (on hello **Manage Keys** blade) tooprevent future node registrations using previous keys.</span></span>

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a><span data-ttu-id="49ac9-206">Resolução de problemas de integração da máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="49ac9-206">Troubleshooting Azure virtual machine onboarding</span></span>

<span data-ttu-id="49ac9-207">Automation DSC do Azure permite-lhe facilmente Windows VMs do Azure para gestão de configuração.</span><span class="sxs-lookup"><span data-stu-id="49ac9-207">Azure Automation DSC lets you easily onboard Azure Windows VMs for configuration management.</span></span> <span data-ttu-id="49ac9-208">Definições avançadas de Olá, Olá extensão de configuração de estado pretendido do Azure VM é utilizada tooregister Olá VM com o Automation DSC do Azure.</span><span class="sxs-lookup"><span data-stu-id="49ac9-208">Under hello hood, hello Azure VM Desired State Configuration extension is used tooregister hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="49ac9-209">Uma vez que Olá extensão de configuração de estado pretendido do Azure VM é executado no modo assíncrono, ao controlar o progresso e a execução de resolução de problemas podem ser importantes.</span><span class="sxs-lookup"><span data-stu-id="49ac9-209">Since hello Azure VM Desired State Configuration extension runs asynchronously, tracking its progress and troubleshooting its execution may be important.</span></span>

> [!NOTE]
> <span data-ttu-id="49ac9-210">Qualquer método de integração tooAzure uma VM do Windows Azure Automation DSC que utiliza a extensão de configuração de estado pretendido do Azure VM Olá pode demorar até tooan hora para Olá nó tooshow cópias de segurança, tal como registado na automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="49ac9-210">Any method of onboarding an Azure Windows VM tooAzure Automation DSC that uses hello Azure VM Desired State Configuration extension could take up tooan hour for hello node tooshow up as registered in Azure Automation.</span></span> <span data-ttu-id="49ac9-211">Isto acontece devido toohello instalação do Windows Management Framework 5.0 Olá VM pela extensão de DSC da VM do Azure Olá, que é necessário tooonboard Olá VM tooAzure DSC de automatização.</span><span class="sxs-lookup"><span data-stu-id="49ac9-211">This is due toohello installation of Windows Management Framework 5.0 on hello VM by hello Azure VM DSC extension, which is required tooonboard hello VM tooAzure Automation DSC.</span></span>

<span data-ttu-id="49ac9-212">Estado de Olá tootroubleshoot ou de vista de Olá extensão de configuração de estado pretendido do Azure VM, no portal do Azure de Olá navegue toohello VM que está a ser integrado, em seguida, clique em->- **todas as definições** -> **extensões**   ->  **DSC**.</span><span class="sxs-lookup"><span data-stu-id="49ac9-212">tootroubleshoot or view hello status of hello Azure VM Desired State Configuration extension, in hello Azure portal navigate toohello VM being onboarded, then click -> **All settings** -> **Extensions** -> **DSC**.</span></span> <span data-ttu-id="49ac9-213">Para obter mais detalhes, pode clicar em **ver o estado detalhado**.</span><span class="sxs-lookup"><span data-stu-id="49ac9-213">For more details, you can click **View detailed status**.</span></span>

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a><span data-ttu-id="49ac9-214">Expiração do certificado e o novo registo</span><span class="sxs-lookup"><span data-stu-id="49ac9-214">Certificate expiration and reregistration</span></span>

<span data-ttu-id="49ac9-215">Depois de registar uma máquina como um nó de DSC no Automation DSC do Azure, existem vários motivos por que razão poderá ser necessário tooreregister esse nó Olá futura:</span><span class="sxs-lookup"><span data-stu-id="49ac9-215">After registering a machine as a DSC node in Azure Automation DSC, there are a number of reasons why you may need tooreregister that node in hello future:</span></span>

* <span data-ttu-id="49ac9-216">Depois de registar, cada nó negoceia automaticamente um certificado exclusivo para a autenticação expira após um ano.</span><span class="sxs-lookup"><span data-stu-id="49ac9-216">After registering, each node automatically negotiates a unique certificate for authentication that expires after one year.</span></span> <span data-ttu-id="49ac9-217">Atualmente, Olá protocolo de registo do PowerShell DSC não é possível renovar automaticamente certificados quando estes estão prestes a expirar, por isso terá de nós de Olá tooreregister após o tempo de um ano.</span><span class="sxs-lookup"><span data-stu-id="49ac9-217">Currently, hello PowerShell DSC registration protocol cannot automatically renew certificates when they are nearing expiration, so you need tooreregister hello nodes after a year's time.</span></span> <span data-ttu-id="49ac9-218">Antes de ao registar novamente, certifique-se de que cada nó está a executar Windows Management Framework 5.0 RTM.</span><span class="sxs-lookup"><span data-stu-id="49ac9-218">Before reregistering, ensure that each node is running Windows Management Framework 5.0 RTM.</span></span> <span data-ttu-id="49ac9-219">Se o certificado de autenticação de um nó expira e nó Olá não é reregistered, nó Olá toocommunicate não é possível com a automatização do Azure e será marcado como 'Unresponsive.'</span><span class="sxs-lookup"><span data-stu-id="49ac9-219">If a node's authentication certificate expires, and hello node is not reregistered, hello node will be unable toocommunicate with Azure Automation and will be marked 'Unresponsive.'</span></span> <span data-ttu-id="49ac9-220">O novo registo efetuada 90 dias ou menor da hora de expiração do certificado hello, ou em qualquer momento após a hora de expiração do certificado de Olá, irá resultar num novo certificado a ser gerado e utilizado.</span><span class="sxs-lookup"><span data-stu-id="49ac9-220">Reregistration performed 90 days or less from hello certificate expiration time, or at any point after hello certificate expiration time, will result in a new certificate being generated and used.</span></span>
* <span data-ttu-id="49ac9-221">toochange qualquer [valores de Gestor de configuração Local do PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) que foram definidas durante o registo inicial do nó de Olá, tais como ConfigurationMode.</span><span class="sxs-lookup"><span data-stu-id="49ac9-221">toochange any [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) that were set during initial registration of hello node, such as ConfigurationMode.</span></span> <span data-ttu-id="49ac9-222">Atualmente, estes valores de agente do DSC só podem ser alterados através do novo registo.</span><span class="sxs-lookup"><span data-stu-id="49ac9-222">Currently, these DSC agent values can only be changed through reregistration.</span></span> <span data-ttu-id="49ac9-223">uma exceção de Olá é Olá configuração do nó atribuído nó toohello – Isto pode ser alterado no Automation DSC do Azure diretamente.</span><span class="sxs-lookup"><span data-stu-id="49ac9-223">hello one exception is hello Node Configuration assigned toohello node -- this can be changed in Azure Automation DSC directly.</span></span>

<span data-ttu-id="49ac9-224">O novo registo pode ser efetuado no Olá mesma forma que registou nó Olá inicialmente, utilizando qualquer um dos métodos de integração de Olá descrita neste documento.</span><span class="sxs-lookup"><span data-stu-id="49ac9-224">Reregistration can be performed in hello same way you registered hello node initially, using any of hello onboarding methods described in this document.</span></span> <span data-ttu-id="49ac9-225">Não é necessário toounregister um nó do DSC da automatização do Azure antes de ao registar novamente-lo.</span><span class="sxs-lookup"><span data-stu-id="49ac9-225">You do not need toounregister a node from Azure Automation DSC before reregistering it.</span></span>

## <a name="related-articles"></a><span data-ttu-id="49ac9-226">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="49ac9-226">Related Articles</span></span>

* [<span data-ttu-id="49ac9-227">Descrição geral do DSC da automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="49ac9-227">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="49ac9-228">Cmdlets do DSC da automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="49ac9-228">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="49ac9-229">Preços do DSC da automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="49ac9-229">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)
