---
title: "máquinas virtuais do Azure de aaaConnect tooLog Analytics | Microsoft Docs"
description: "Para o Windows e Linux máquinas virtuais em execução no Azure, Olá recomendado forma de registos recolhidos e métricas é através da instalação da extensão de VM do Azure de análise de registo Olá. Pode utilizar Olá portal do Azure ou do PowerShell tooinstall Olá extensão da máquina virtual de análise de registos em VMs do Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: ca39e586-a6af-42fe-862e-80978a58d9b1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: richrund
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac96c242d03ed3a22ca96368e5a8cc53f9a993db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a><span data-ttu-id="0f6ff-104">Ligar máquinas virtuais do Azure tooLog análise com um agente de análise de registos</span><span class="sxs-lookup"><span data-stu-id="0f6ff-104">Connect Azure virtual machines tooLog Analytics with a Log Analytics agent</span></span>

<span data-ttu-id="0f6ff-105">Para computadores Windows e Linux, Olá recomendado método para recolher registos e as métricas é pela instalação do agente de análise de registos de Olá.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-105">For Windows and Linux computers, hello recommended method for collecting logs and metrics is by installing hello Log Analytics agent.</span></span>

<span data-ttu-id="0f6ff-106">Olá mais fácil forma tooinstall Olá análise de registos do agente máquinas virtuais do Azure é através de Olá extensão de VM de análise do registo.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-106">hello easiest way tooinstall hello Log Analytics agent on Azure virtual machines is through hello Log Analytics VM Extension.</span></span>  <span data-ttu-id="0f6ff-107">Utilizando a extensão de Olá simplifica o processo de instalação de Olá e configura automaticamente Olá agente toosend dados toohello Log Analytics área de trabalho que especificar.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-107">Using hello extension simplifies hello installation process and automatically configures hello agent toosend data toohello Log Analytics workspace that you specify.</span></span> <span data-ttu-id="0f6ff-108">agente de Olá também atualizada automaticamente, assegurando que tem Step-by-Olá mais recentes funcionalidades e correções.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-108">hello agent is also upgraded automatically, ensuring that you have hello latest features and fixes.</span></span>

<span data-ttu-id="0f6ff-109">Para máquinas virtuais do Windows, ativar Olá *Microsoft Monitoring Agent* extensão da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-109">For Windows virtual machines, you enable hello *Microsoft Monitoring Agent* virtual machine extension.</span></span>
<span data-ttu-id="0f6ff-110">Para máquinas virtuais do Linux, ativar Olá *OMS agente para Linux* extensão da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-110">For Linux virtual machines, you enable hello *OMS Agent For Linux* virtual machine extension.</span></span>

<span data-ttu-id="0f6ff-111">Saiba mais sobre [extensões de máquina virtual do Azure](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e Olá [agente Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0f6ff-111">Learn more about [Azure virtual machine extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and hello [Linux agent](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="0f6ff-112">Quando utilizar coleção baseada no agente para dados de registo, tem de configurar [origens de dados de análise de registos](log-analytics-data-sources.md) toospecify Olá registos e as métricas que pretende que o toocollect.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-112">When you use agent-based collection for log data, you must configure [data sources in Log Analytics](log-analytics-data-sources.md) toospecify hello logs and metrics that you want toocollect.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0f6ff-113">Se configurar dados de registo do Log Analytics tooindex utilizando [diagnóstico do Azure](log-analytics-azure-storage.md), e configurar Olá toocollect agente de Olá mesmo inicia sessão, em seguida, Olá registos são recolhidos duas vezes.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-113">If you configure Log Analytics tooindex log data by using [Azure diagnostics](log-analytics-azure-storage.md), and you configure hello agent toocollect hello same logs, then hello logs are collected twice.</span></span> <span data-ttu-id="0f6ff-114">São-lhe cobrados para ambas as origens de dados.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-114">You are charged for both data sources.</span></span> <span data-ttu-id="0f6ff-115">Se tiver o agente de Olá instalado, recolher dados de registo utilizando o agente de Olá só - não configurar dados de registo de toocollect de análise de registos de diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-115">If you have hello agent installed, then collect log data by using only hello agent - don't configure Log Analytics toocollect log data from Azure diagnostics.</span></span>
>
>

<span data-ttu-id="0f6ff-116">Existem três formas de fácil extensão da máquina virtual tooenable Olá análise de registos:</span><span class="sxs-lookup"><span data-stu-id="0f6ff-116">There are three easy ways tooenable hello Log Analytics virtual machine extension:</span></span>

* <span data-ttu-id="0f6ff-117">Ao utilizar Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0f6ff-117">By using hello Azure portal</span></span>
* <span data-ttu-id="0f6ff-118">Ao utilizar o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f6ff-118">By using Azure PowerShell</span></span>
* <span data-ttu-id="0f6ff-119">Ao utilizar um modelo Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0f6ff-119">By using an Azure Resource Manager template</span></span>

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a><span data-ttu-id="0f6ff-120">Ativar a extensão VM Olá na Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0f6ff-120">Enable hello VM extension in hello Azure portal</span></span>
<span data-ttu-id="0f6ff-121">Pode instalar o agente de Olá para análise de registos e ligar Olá máquina virtual do Azure, que é executada no utilizando Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0f6ff-121">You can install hello agent for Log Analytics and connect hello Azure virtual machine that it runs on by using hello [Azure portal](https://portal.azure.com).</span></span>

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a><span data-ttu-id="0f6ff-122">tooinstall Olá agente da análise de registos e ligue-se a área de trabalho do Log Analytics do Olá máquina virtual tooa</span><span class="sxs-lookup"><span data-stu-id="0f6ff-122">tooinstall hello Log Analytics agent and connect hello virtual machine tooa Log Analytics workspace</span></span>
1. <span data-ttu-id="0f6ff-123">Inicie sessão em Olá [portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0f6ff-123">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="0f6ff-124">Selecione **procurar** no Olá à esquerda do lado do Olá portal e, em seguida, aceda demasiado**análise de registos (OMS)** e selecioná-lo.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-124">Select **Browse** on hello left side of hello portal, and then go too**Log Analytics (OMS)** and select it.</span></span>
3. <span data-ttu-id="0f6ff-125">Na lista de áreas de trabalho de análise de registos, selecione Olá uma que pretenda toouse com Olá VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-125">In your list of Log Analytics workspaces, select hello one that you want toouse with hello Azure VM.</span></span>  
   ![Áreas de trabalho do OMS](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. <span data-ttu-id="0f6ff-127">Em **gestão de análise de registo**, selecione **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-127">Under **Log analytics management**, select **Virtual machines**.</span></span>  
   <span data-ttu-id="0f6ff-128">![Máquinas virtuais](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span><span class="sxs-lookup"><span data-stu-id="0f6ff-128">![Virtual machines](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span></span>
5. <span data-ttu-id="0f6ff-129">Na lista de Olá de **máquinas virtuais**, selecione Olá máquina virtual no qual pretende que o agente de Olá tooinstall.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-129">In hello list of **Virtual machines**, select hello virtual machine on which you want tooinstall hello agent.</span></span> <span data-ttu-id="0f6ff-130">Olá **estado de ligação do OMS** para Olá VM indica que é **não ligado**.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-130">hello **OMS connection status** for hello VM indicates that it is **Not connected**.</span></span>  
   <span data-ttu-id="0f6ff-131">![VM não ligado](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span><span class="sxs-lookup"><span data-stu-id="0f6ff-131">![VM not connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span></span>
6. <span data-ttu-id="0f6ff-132">Nos detalhes de Olá para a máquina virtual, selecione **Connect**.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-132">In hello details for your virtual machine, select **Connect**.</span></span> <span data-ttu-id="0f6ff-133">agente de Olá é automaticamente instalado e configurado para a área de trabalho de análise de registos.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-133">hello agent is automatically installed and configured for your Log Analytics workspace.</span></span> <span data-ttu-id="0f6ff-134">Este processo demora alguns minutos, durante o período de tempo é Olá estado da ligação do OMS *ligar...*</span><span class="sxs-lookup"><span data-stu-id="0f6ff-134">This process takes a few minutes, during which time hello OMS Connection status is *Connecting...*</span></span>  
   <span data-ttu-id="0f6ff-135">![Ligar a VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span><span class="sxs-lookup"><span data-stu-id="0f6ff-135">![Connect VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span></span>
7. <span data-ttu-id="0f6ff-136">Depois de instalar e ligar o agente de Olá, Olá **ligação OMS** estado será atualizado tooshow **esta área de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-136">After you install and connect hello agent, hello **OMS connection** status will be updated tooshow **This workspace**.</span></span>  
   <span data-ttu-id="0f6ff-137">![Ligado](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span><span class="sxs-lookup"><span data-stu-id="0f6ff-137">![Connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span></span>

## <a name="enable-hello-vm-extension-using-powershell"></a><span data-ttu-id="0f6ff-138">Ativar a extensão VM de Olá através do PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f6ff-138">Enable hello VM extension using PowerShell</span></span>
<span data-ttu-id="0f6ff-139">Quando configurar a máquina virtual utilizando o PowerShell, terá de tooprovide Olá **workspaceId** e **workspaceKey**.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-139">When you configure your virtual machine by using PowerShell, you need tooprovide hello **workspaceId** and **workspaceKey**.</span></span> <span data-ttu-id="0f6ff-140">os nomes de propriedade de Olá na sua configuração de json são **maiúsculas e minúsculas**.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-140">hello property names in your json configuration are **case-sensitive**.</span></span>

<span data-ttu-id="0f6ff-141">Pode encontrar Olá Id e a chave no Olá **definições** página do portal do OMS hello, ou do PowerShell conforme mostrado no Olá anterior exemplo.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-141">You can find hello Id and key on hello **Settings** page of hello OMS portal, or by using PowerShell as shown in hello preceding example.</span></span>

![ID da área de trabalho e a chave primária](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

<span data-ttu-id="0f6ff-143">Existem diferentes comandos para máquinas virtuais clássicas do Azure e as máquinas virtuais do Gestor de recursos.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-143">There are different commands for Azure classic virtual machines and Resource Manager virtual machines.</span></span> <span data-ttu-id="0f6ff-144">Seguem-se exemplos de clássica e Resource Manager máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-144">Following are examples for both classic and Resource Manager virtual machines.</span></span>

<span data-ttu-id="0f6ff-145">Para as máquinas virtuais clássicas, utilize Olá seguinte o exemplo do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0f6ff-145">For classic virtual machines, use hello following PowerShell example:</span></span>

```PowerShell
Add-AzureAccount

$workspaceId = "enter workspace ID here"
$workspaceKey = "enter workspace key here"
$hostedService = "enter hosted service here"

$vm = Get-AzureVM –ServiceName $hostedService

# For Windows VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'MicrosoftMonitoringAgent' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose

# For Linux VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'OmsAgentForLinux' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose
```

<span data-ttu-id="0f6ff-146">Para VMs do Gestor de recursos com Linux utilizando Olá seguir CLI</span><span class="sxs-lookup"><span data-stu-id="0f6ff-146">For Resource Manager Linux VMs using hello following CLI</span></span>
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

<span data-ttu-id="0f6ff-147">Para máquinas de virtuais do Gestor de recursos, utilize Olá seguinte o exemplo do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0f6ff-147">For Resource Manager virtual machines, use hello following PowerShell example:</span></span>

```PowerShell
Login-AzureRMAccount
Select-AzureRMSubscription -SubscriptionId "**"

$workspaceName = "your workspace name"
$VMresourcegroup = "**"
$VMresourcename = "**"

$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq $workspaceName})

if ($workspace.Name -ne $workspaceName)
{
    Write-Error "Unable toofind OMS Workspace $workspaceName. Do you need toorun Select-AzureRMSubscription?"
}

$workspaceId = $workspace.CustomerId
$workspaceKey = (Get-AzureRmOperationalInsightsWorkspaceSharedKeys -ResourceGroupName $workspace.ResourceGroupName -Name $workspace.Name).PrimarySharedKey

$vm = Get-AzureRmVM -ResourceGroupName $VMresourcegroup -Name $VMresourcename
$location = $vm.Location

# For Windows VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'MicrosoftMonitoringAgent' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'MicrosoftMonitoringAgent' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"

# For Linux VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'OmsAgentForLinux' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'OmsAgentForLinux' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"


```


## <a name="deploy-hello-vm-extension-using-a-template"></a><span data-ttu-id="0f6ff-148">Implementar a extensão da VM Olá através de um modelo</span><span class="sxs-lookup"><span data-stu-id="0f6ff-148">Deploy hello VM extension using a template</span></span>
<span data-ttu-id="0f6ff-149">Ao utilizar o Azure Resource Manager, pode criar um modelo (no formato JSON) que define a implementação de Olá e configuração da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-149">By using Azure Resource Manager, you can create a template (in JSON format) that defines hello deployment and configuration of your application.</span></span> <span data-ttu-id="0f6ff-150">Este modelo é conhecido como um modelo do Resource Manager e fornece uma implementação de toodefine de forma declarativa.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-150">This template is known as a Resource Manager template and provides a declarative way toodefine deployment.</span></span> <span data-ttu-id="0f6ff-151">Ao utilizar um modelo, que pode implementar a aplicação durante todo o ciclo de vida Olá repetidamente e ter a confiança de que os recursos estão a ser implementados num estado consistente.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-151">By using a template, you can repeatedly deploy your application throughout hello app lifecycle and have confidence that your resources are being deployed in a consistent state.</span></span>

<span data-ttu-id="0f6ff-152">Ao incluir o agente de análise de registos de Olá como parte do seu modelo do Resource Manager, pode certificar-se de que cada máquina virtual é a área de trabalho de análise de registos de tooyour de tooreport previamente configurada.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-152">By including hello Log Analytics agent as part of your Resource Manager template, you can ensure that each virtual machine is pre-configured tooreport tooyour Log Analytics workspace.</span></span>

<span data-ttu-id="0f6ff-153">Para mais informações sobre modelos do Resource Manager, consulte [modelos Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0f6ff-153">For more information about Resource Manager templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="0f6ff-154">Segue-se um exemplo de um modelo do Resource Manager que é utilizado para implementar uma máquina virtual que está a executar o Windows com Olá extensão do Microsoft Monitoring Agent instalada.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-154">Following is an example of a Resource Manager template that's used for deploying a virtual machine that's running Windows with hello Microsoft Monitoring Agent extension installed.</span></span> <span data-ttu-id="0f6ff-155">Este é um modelo de máquinas típicos, com Olá seguintes adições:</span><span class="sxs-lookup"><span data-stu-id="0f6ff-155">This template is a typical virtual machine template, with hello following additions:</span></span>

* <span data-ttu-id="0f6ff-156">parâmetros workspaceId e workspaceName</span><span class="sxs-lookup"><span data-stu-id="0f6ff-156">workspaceId and workspaceName parameters</span></span>
* <span data-ttu-id="0f6ff-157">Secção de extensão do recurso Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="0f6ff-157">Microsoft.EnterpriseCloud.Monitoring resource extension section</span></span>
* <span data-ttu-id="0f6ff-158">Saídas toolook Olá workspaceId e workspaceSharedKey</span><span class="sxs-lookup"><span data-stu-id="0f6ff-158">Outputs toolook up hello workspaceId and workspaceSharedKey</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for hello Virtual Machine."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Password for hello Virtual Machine."
      }
    },
    "dnsLabelPrefix": {
       "type": "string",
       "metadata": {
          "description": "DNS Label for hello Public IP. Must be lowercase. It should match with hello following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error."
       }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "OMS workspace ID"
      }
    },
    "workspaceName": {
      "type": "string",
      "metadata": {
         "description": "OMS workspace name"
      }
    },
    "windowsOSVersion": {
      "type": "string",
      "defaultValue": "2012-R2-Datacenter",
      "allowedValues": [
        "2008-R2-SP1",
        "2012-Datacenter",
        "2012-R2-Datacenter",
        "Windows-Server-Technical-Preview"
      ],
      "metadata": {
        "description": "hello Windows version for hello VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter, Windows-Server-Technical-Preview."
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]",
    "apiVersion": "2015-06-15",
    "imagePublisher": "MicrosoftWindowsServer",
    "imageOffer": "WindowsServer",
    "OSDiskName": "osdiskforwindowssimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyWindowsVM",
    "vmSize": "Standard_DS1",
    "virtualNetworkName": "MyVNET",
    "resourceId": "[resourceGroup().id]",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "[variables('apiVersion')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "accountType": "[variables('storageAccountType')]"
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsLabelPrefix')]"
        }
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[variables('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[variables('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
              },
              "subnet": {
                "id": "[variables('subnetRef')]"
              }
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[variables('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": {
          "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
          "computername": "[variables('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('windowsOSVersion')]",
            "version": "latest"
          },
          "osDisk": {
            "name": "osdisk",
            "vhd": {
              "uri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        },
        "diagnosticsProfile": {
          "bootDiagnostics": {
             "enabled": "true",
             "storageUri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net')]"
          }
        }
      },
      "resources": [
        {
          "type": "extensions",
          "name": "Microsoft.EnterpriseCloud.Monitoring",
          "apiVersion": "[variables('apiVersion')]",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
          ],
          "properties": {
            "publisher": "Microsoft.EnterpriseCloud.Monitoring",
            "type": "MicrosoftMonitoringAgent",
            "typeHandlerVersion": "1.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "workspaceId": "[parameters('workspaceId')]"
            },
            "protectedSettings": {
              "workspaceKey": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspaceName')), '2015-03-20').primarySharedKey]"
            }
          }
        }
      ]
    }
  ],
  "outputs": {
      "sharedKeyOutput": {
         "value": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').primarySharedKey]",
         "type": "string"
      },
      "workspaceIdOutput": {
         "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').customerId]",
        "type" : "string"
      }
  }
}
```

<span data-ttu-id="0f6ff-159">Pode implementar um modelo através da utilização de Olá seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0f6ff-159">You can deploy a template by using hello following PowerShell command:</span></span>

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a><span data-ttu-id="0f6ff-160">Extensão de VM de análise do registo de Olá de resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="0f6ff-160">Troubleshooting hello Log Analytics VM extension</span></span>
<span data-ttu-id="0f6ff-161">Normalmente, receberá uma mensagem quando coisas não funcionam, do portal do Azure ou o Azure powershell.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-161">Usually you receive a message when things don't work, from either Azure portal or Azure powershell.</span></span>

1. <span data-ttu-id="0f6ff-162">Inicie sessão em Olá [portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0f6ff-162">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="0f6ff-163">Localize Olá VM e abra os detalhes VM.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-163">Find hello VM and open VM details.</span></span>
3. <span data-ttu-id="0f6ff-164">Clique em **extensões** toocheck se a extensão do OMS está ativada ou não.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-164">Click **Extensions** toocheck if OMS extension is enabled or not.</span></span>

   ![Vista de extensão de VM](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. <span data-ttu-id="0f6ff-166">Clique em Olá *MicrosoftMonitoringAgent*(Windows) ou *OmsAgentForLinux*(Linux) extensão e vista de detalhes.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-166">Click hello *MicrosoftMonitoringAgent*(Windows) or *OmsAgentForLinux*(Linux) extension and view details.</span></span> 

   ![Detalhes da extensão de VM](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a><span data-ttu-id="0f6ff-168">Resolução de problemas de máquinas virtuais do Windows</span><span class="sxs-lookup"><span data-stu-id="0f6ff-168">Troubleshooting Windows Virtual Machines</span></span>
<span data-ttu-id="0f6ff-169">Se hello *Microsoft Monitoring Agent* extensão de agente da VM não está a instalar ou relatórios, pode realizar Olá problema de Olá tootroubleshoot de passos a seguir.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-169">If hello *Microsoft Monitoring Agent* VM agent extension is not installing or reporting, you can perform hello following steps tootroubleshoot hello issue.</span></span>

1. <span data-ttu-id="0f6ff-170">Verifique se o agente de VM do Azure de Olá está instalado e a funcionar corretamente utilizando Olá os passos em [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span><span class="sxs-lookup"><span data-stu-id="0f6ff-170">Check if hello Azure VM agent is installed and working correctly by using hello steps in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span></span>
   * <span data-ttu-id="0f6ff-171">Também pode rever o ficheiro de registo do agente VM Olá`C:\WindowsAzure\logs\WaAppAgent.log`</span><span class="sxs-lookup"><span data-stu-id="0f6ff-171">You can also review hello VM agent log file `C:\WindowsAzure\logs\WaAppAgent.log`</span></span>
   * <span data-ttu-id="0f6ff-172">Se o registo de Olá não existir, o agente da VM Olá não está instalado.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-172">If hello log does not exist, hello VM agent is not installed.</span></span>
     * [<span data-ttu-id="0f6ff-173">Instalar Olá agente da VM do Azure em VMs clássicas</span><span class="sxs-lookup"><span data-stu-id="0f6ff-173">Install hello Azure VM Agent on classic VMs</span></span>](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. <span data-ttu-id="0f6ff-174">Confirme Olá Microsoft Monitoring Agent está a executar tarefas de heartbeat de extensão utilizando Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="0f6ff-174">Confirm hello Microsoft Monitoring Agent extension heartbeat task is running using hello following steps:</span></span>
   * <span data-ttu-id="0f6ff-175">Inicie sessão na máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="0f6ff-175">Log in toohello virtual machine</span></span>
   * <span data-ttu-id="0f6ff-176">Abra o Programador de tarefas e determinar Olá `update_azureoperationalinsight_agent_heartbeat` tarefas</span><span class="sxs-lookup"><span data-stu-id="0f6ff-176">Open task scheduler and find hello `update_azureoperationalinsight_agent_heartbeat` task</span></span>
   * <span data-ttu-id="0f6ff-177">Certifique-se tarefas de Olá está ativada e está em execução a cada minuto</span><span class="sxs-lookup"><span data-stu-id="0f6ff-177">Confirm hello task is enabled and is running every one minute</span></span>
   * <span data-ttu-id="0f6ff-178">Verifique o ficheiro de registo de heartbeat de Olá na`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span><span class="sxs-lookup"><span data-stu-id="0f6ff-178">Check hello heartbeat logfile in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span></span>
3. <span data-ttu-id="0f6ff-179">Consulte Olá ficheiros de registo de extensão VM de agente de monitorização da Microsoft no`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span><span class="sxs-lookup"><span data-stu-id="0f6ff-179">Review hello Microsoft Monitoring Agent VM extension log files in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span></span>
4. <span data-ttu-id="0f6ff-180">Certifique-se a máquina virtual de Olá pode executar scripts do PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f6ff-180">Ensure hello virtual machine can run PowerShell scripts</span></span>
5. <span data-ttu-id="0f6ff-181">Certifique-se de que as permissões num C:\Windows\temp ainda não foram alteradas</span><span class="sxs-lookup"><span data-stu-id="0f6ff-181">Ensure permissions on C:\Windows\temp haven’t been changed</span></span>
6. <span data-ttu-id="0f6ff-182">Ver o estado de Olá de Olá Microsoft Monitoring Agent escrevendo Olá os seguintes comandos numa janela elevada do PowerShell na máquina virtual de Olá`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span><span class="sxs-lookup"><span data-stu-id="0f6ff-182">View hello status of hello Microsoft Monitoring Agent by typing hello following command in an elevated PowerShell window on hello virtual machine `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span></span>
7. <span data-ttu-id="0f6ff-183">Consulte Olá ficheiros de registo do programa de configuração de Microsoft Monitoring Agent no`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span><span class="sxs-lookup"><span data-stu-id="0f6ff-183">Review hello Microsoft Monitoring Agent setup log files in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span></span>

<span data-ttu-id="0f6ff-184">Para obter mais informações, consulte [resolução de problemas de extensões do Windows](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0f6ff-184">For more information, see [troubleshooting Windows extensions](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="troubleshooting-linux-virtual-machines"></a><span data-ttu-id="0f6ff-185">Resolução de problemas de máquinas virtuais do Linux</span><span class="sxs-lookup"><span data-stu-id="0f6ff-185">Troubleshooting Linux Virtual Machines</span></span>
<span data-ttu-id="0f6ff-186">Se hello *agente do OMS para Linux* extensão de agente da VM não está a instalar ou relatórios, pode realizar Olá problema de Olá tootroubleshoot de passos a seguir.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-186">If hello *OMS Agent for Linux* VM agent extension is not installing or reporting, you can perform hello following steps tootroubleshoot hello issue.</span></span>

1. <span data-ttu-id="0f6ff-187">Se o estado da extensão Olá é *desconhecido* verificar se o agente da VM do Azure de Olá está instalado e a funcionar corretamente, revendo o ficheiro de registo do agente VM Olá`/var/log/waagent.log`</span><span class="sxs-lookup"><span data-stu-id="0f6ff-187">If hello extension status is *Unknown* check if hello Azure VM agent is installed and working correctly by reviewing hello VM agent log file `/var/log/waagent.log`</span></span>
   * <span data-ttu-id="0f6ff-188">Se o registo de Olá não existir, o agente da VM Olá não está instalado.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-188">If hello log does not exist, hello VM agent is not installed.</span></span>
   * [<span data-ttu-id="0f6ff-189">Instalar o agente da VM do Azure de Olá em VMs do Linux</span><span class="sxs-lookup"><span data-stu-id="0f6ff-189">Install hello Azure VM Agent on Linux VMs</span></span>](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="0f6ff-190">Para outros Estados mau estado de funcionamento, reveja Olá agente do OMS para a extensão de VM com Linux ficheiros de registo `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` e`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span><span class="sxs-lookup"><span data-stu-id="0f6ff-190">For other unhealthy statuses, review hello OMS Agent for Linux VM extension logs files in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` and `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span></span>
3. <span data-ttu-id="0f6ff-191">Se o estado da extensão Olá está em bom estado, mas não estão a ser carregados dados reveja Olá agente do OMS para ficheiros de registo de Linux`/var/opt/microsoft/omsagent/log/omsagent.log`</span><span class="sxs-lookup"><span data-stu-id="0f6ff-191">If hello extension status is healthy, but data is not being uploaded review hello OMS Agent for Linux log files in `/var/opt/microsoft/omsagent/log/omsagent.log`</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f6ff-192">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0f6ff-192">Next steps</span></span>
* <span data-ttu-id="0f6ff-193">Configurar [origens de dados de análise de registos](log-analytics-data-sources.md) toospecify Olá toocollect métricas e registos.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-193">Configure [data sources in Log Analytics](log-analytics-data-sources.md) toospecify hello logs and metrics toocollect.</span></span>
* <span data-ttu-id="0f6ff-194">toogather dados provenientes de máquinas virtuais [soluções de análise de registos de adicionar de Olá soluções galeria](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="0f6ff-194">toogather data from virtual machines [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
* <span data-ttu-id="0f6ff-195">[Recolher dados, utilizando o Azure Diagnostics](log-analytics-azure-storage.md) para outros recursos que estão em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="0f6ff-195">[Collect data by using Azure Diagnostics](log-analytics-azure-storage.md) for other resources that are running in Azure.</span></span>

<span data-ttu-id="0f6ff-196">Para computadores que não estão no Azure, pode instalar o agente de análise de registos de Olá utilizando métodos de Olá descritas Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="0f6ff-196">For computers that are not in Azure, you can install hello Log Analytics agent by using hello methods that are described in hello following articles:</span></span>

* [<span data-ttu-id="0f6ff-197">Ligar tooLog de computadores Windows análise</span><span class="sxs-lookup"><span data-stu-id="0f6ff-197">Connect Windows computers tooLog Analytics</span></span>](log-analytics-windows-agents.md)
* [<span data-ttu-id="0f6ff-198">Ligar tooLog de computadores Linux análise</span><span class="sxs-lookup"><span data-stu-id="0f6ff-198">Connect Linux computers tooLog Analytics</span></span>](log-analytics-linux-agents.md)
