---
title: "aaaDeploy uma aplicação no conjunto de dimensionamento da máquina virtual do Azure | Microsoft Docs"
description: "Saiba toodeploy uma aplicação de dimensionamento automático simples numa escala de máquina virtual definida utilizando um modelo Azure Resource Manager."
services: virtual-machine-scale-sets
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 6fccc310312cabfcdddfcbcd2d154fc5cc440417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-autoscaling-app-using-a-template"></a><span data-ttu-id="e5ed3-103">Implementar uma aplicação de dimensionamento automático através de um modelo</span><span class="sxs-lookup"><span data-stu-id="e5ed3-103">Deploy an autoscaling app using a template</span></span>

<span data-ttu-id="e5ed3-104">[Modelos Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) é uma excelente forma toodeploy grupos de recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way toodeploy groups of related resources.</span></span> <span data-ttu-id="e5ed3-105">Este tutorial baseia-se [implementar um conjunto de dimensionamento simples](virtual-machine-scale-sets-mvss-start.md) e descreve como toodeploy uma aplicação de dimensionamento automático simples numa escala definido de utilizando um modelo Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-105">This tutorial builds on [Deploy a simple scale set](virtual-machine-scale-sets-mvss-start.md) and describes how toodeploy a simple autoscaling application on a scale set using an Azure Resource Manager template.</span></span>  <span data-ttu-id="e5ed3-106">Também pode configurar com o PowerShell, o CLI ou o portal de Olá de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-106">You can also set up autoscaling using PowerShell, CLI, or hello portal.</span></span> <span data-ttu-id="e5ed3-107">Para obter mais informações, consulte [Descrição geral do dimensionamento automático](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e5ed3-107">For more information, see [Autoscale overview](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

## <a name="two-quickstart-templates"></a><span data-ttu-id="e5ed3-108">Dois modelos de início rápido</span><span class="sxs-lookup"><span data-stu-id="e5ed3-108">Two quickstart templates</span></span>
<span data-ttu-id="e5ed3-109">Quando implementa um conjunto de dimensionamento, instala o novo software numa plataforma de imagens que usa uma [extensão de VM](../virtual-machines/virtual-machines-windows-extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="e5ed3-109">When you deploy a scale set you can install new software on a platform image using a [VM Extension](../virtual-machines/virtual-machines-windows-extensions-features.md).</span></span> <span data-ttu-id="e5ed3-110">Uma extensão de VM é uma pequena aplicação que fornece tarefas de configuração e automação de pós-implementação em máquinas virtuais do Azure, tais como implementar uma aplicação.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-110">A VM extension is a small application that provides post-deployment configuration and automation tasks on Azure virtual machines, such as deploying an app.</span></span> <span data-ttu-id="e5ed3-111">Dois modelos de outro exemplo são fornecidos na [/azure-guia de introdução-modelos do Azure](https://github.com/Azure/azure-quickstart-templates) que mostram como toodeploy uma aplicação de dimensionamento automático para uma escala definido utilizando extensões VM.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-111">Two different sample templates are provided in [Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) which show how toodeploy an autoscaling application onto a scale set using VM extensions.</span></span>

### <a name="python-http-server-on-linux"></a><span data-ttu-id="e5ed3-112">Servidor de HTTP do Python no Linux</span><span class="sxs-lookup"><span data-stu-id="e5ed3-112">Python HTTP server on Linux</span></span>
<span data-ttu-id="e5ed3-113">Olá [servidor de HTTP de Python no Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) modelo de exemplo implementa uma aplicação de dimensionamento automático simples em execução num conjunto de dimensionamento do Linux.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-113">hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) sample template deploys a simple autoscaling application running on a Linux scale set.</span></span>  <span data-ttu-id="e5ed3-114">[Bottle](http://bottlepy.org/docs/dev/), um Python web framework e um servidor HTTP simple são implementadas em cada VM em escala Olá definida utilizando um script personalizado extensão da VM.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-114">[Bottle](http://bottlepy.org/docs/dev/), a Python web framework, and a simple HTTP server are deployed on each VM in hello scale set using a custom script VM extension.</span></span> <span data-ttu-id="e5ed3-115">escala de Olá Definir escalas quando a utilização da CPU média em todas as VMs é maior do que 60% e reduz horizontalmente para baixo, quando a utilização da CPU média Olá é inferior a 30%.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-115">hello scale set scales up when average CPU utilization across all VMs is greater than 60% and scales down when hello average CPU utilization is less than 30%.</span></span>

<span data-ttu-id="e5ed3-116">Além disso toohello conjunto de dimensionamento de recurso, hello *azuredeploy. JSON* modelo de exemplo também declara rede virtual, o endereço IP público, o Balanceador de carga e recursos de definições de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-116">In addition toohello scale set resource, hello *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span>  <span data-ttu-id="e5ed3-117">Para obter mais informações sobre como criar esses recursos num modelo, consulte [Conjunto de dimensionamento do Linux escala automática](virtual-machine-scale-sets-linux-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="e5ed3-117">For more information on creating these resources in a template, see [Linux scale set with autoscale](virtual-machine-scale-sets-linux-autoscale.md).</span></span>

<span data-ttu-id="e5ed3-118">No Olá *azuredeploy. JSON* modelo, Olá `extensionProfile` propriedade Olá `Microsoft.Compute/virtualMachineScaleSets` recurso Especifica uma extensão de script personalizado.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-118">In hello *azuredeploy.json* template, hello `extensionProfile` property of hello `Microsoft.Compute/virtualMachineScaleSets` resource specifies a custom script extension.</span></span> <span data-ttu-id="e5ed3-119">`fileUris`Especifica a localização de script(s) Olá.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-119">`fileUris` specifies hello script(s) location.</span></span> <span data-ttu-id="e5ed3-120">Neste caso, dois ficheiros: *workserver.py*, que define um servidor HTTP simple, e *installserver.sh*, que instala o Bottle e inicia Olá servidor de HTTP.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-120">In this case, two files: *workserver.py*, which defines a simple HTTP server, and *installserver.sh*, which installs Bottle and starts hello HTTP server.</span></span> <span data-ttu-id="e5ed3-121">`commandToExecute`Especifica Olá comando toorun depois do conjunto de dimensionamento de Olá foi implementado.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-121">`commandToExecute` specifies hello command toorun after hello scale set has been deployed.</span></span>

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "lapextension",
                "properties": {
                  "publisher": "Microsoft.Azure.Extensions",
                  "type": "CustomScript",
                  "typeHandlerVersion": "2.0",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "fileUris": [
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
                    ],
                    "commandToExecute": "bash installserver.sh"
                  }
                }
              }
            ]
          }
```

### <a name="aspnet-mvc-application-on-windows"></a><span data-ttu-id="e5ed3-122">Aplicação ASP.NET MVC no Windows</span><span class="sxs-lookup"><span data-stu-id="e5ed3-122">ASP.NET MVC application on Windows</span></span>
<span data-ttu-id="e5ed3-123">Olá [aplicação MVC do ASP.NET no Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) modelo de exemplo implementa uma aplicação ASP.NET MVC simples em execução no IIS no conjunto de dimensionamento do Windows.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-123">hello [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) sample template deploys a simple ASP.NET MVC app running in IIS on Windows scale set.</span></span>  <span data-ttu-id="e5ed3-124">IIS e Olá aplicação MVC são implementadas através de Olá [PowerShell estado configuração pretendido (DSC)](virtual-machine-scale-sets-dsc.md) extensão da VM.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-124">IIS and hello MVC app are deployed using hello [PowerShell desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) VM extension.</span></span>  <span data-ttu-id="e5ed3-125">escala de Olá configurar escalas (na instância de VM a uma hora) quando a utilização da CPU é superior a 50% para 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-125">hello scale set scales up (on VM instance at a time) when CPU utilization is greater than 50% for 5 minutes.</span></span> 

<span data-ttu-id="e5ed3-126">Além disso toohello conjunto de dimensionamento de recurso, hello *azuredeploy. JSON* modelo de exemplo também declara rede virtual, o endereço IP público, o Balanceador de carga e recursos de definições de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-126">In addition toohello scale set resource, hello *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span> <span data-ttu-id="e5ed3-127">Este modelo também demonstra a atualização da aplicação.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-127">This template also demonstrates application upgrade.</span></span>  <span data-ttu-id="e5ed3-128">Para obter mais informações sobre como criar esses recursos num modelo, consulte [Conjunto de dimensionamento do Windows com escala automática](virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="e5ed3-128">For more information on creating these resources in a template, see [Windows scale set with autoscale](virtual-machine-scale-sets-windows-autoscale.md).</span></span>

<span data-ttu-id="e5ed3-129">No Olá *azuredeploy. JSON* modelo, Olá `extensionProfile` propriedade Olá `Microsoft.Compute/virtualMachineScaleSets` recurso Especifica um [configuração de estado pretendido (DSC)](virtual-machine-scale-sets-dsc.md) extensão que instala o IIS e uma predefinição aplicação Web a partir de um pacote de WebDeploy.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-129">In hello *azuredeploy.json* template, hello `extensionProfile` property of hello `Microsoft.Compute/virtualMachineScaleSets` resource specifies a [desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) extension which installs IIS and a default web app from a WebDeploy package.</span></span>  <span data-ttu-id="e5ed3-130">Olá *IISInstall.ps1* script instala o IIS na máquina virtual de Olá e se encontra no Olá *DSC* pasta.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-130">hello *IISInstall.ps1* script installs IIS on hello virtual machine and is found in hello *DSC* folder.</span></span>  <span data-ttu-id="e5ed3-131">aplicação de web MVC Olá se encontra no Olá *WebDeploy* pasta.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-131">hello MVC web app is found in hello *WebDeploy* folder.</span></span>  <span data-ttu-id="e5ed3-132">script de instalação do Olá caminhos toohello e aplicação de web de Olá são definidos no Olá `powershelldscZip` e `webDeployPackage` parâmetros Olá *azuredeploy.parameters.json* ficheiro.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-132">hello paths toohello install script and hello web app are defined in hello `powershelldscZip` and `webDeployPackage` parameters in hello *azuredeploy.parameters.json* file.</span></span> 

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Powershell.DSC",
                "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.9",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('powershelldscUpdateTagVersion')]",
                  "settings": {
                    "configuration": {
                      "url": "[variables('powershelldscZipFullPath')]",
                      "script": "IISInstall.ps1",
                      "function": "InstallIIS"
                    },
                    "configurationArguments": {
                      "nodeName": "localhost",
                      "WebDeployPackagePath": "[variables('webDeployPackageFullPath')]"
                    }
                  }
                }
              }
            ]
          }
```

## <a name="deploy-hello-template"></a><span data-ttu-id="e5ed3-133">Implementar a modelo Olá</span><span class="sxs-lookup"><span data-stu-id="e5ed3-133">Deploy hello template</span></span>
<span data-ttu-id="e5ed3-134">Olá toodeploy da forma mais simples do Olá [servidor de HTTP de Python no Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) ou [aplicação MVC do ASP.NET no Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) modelo é toouse Olá **implementar tooAzure** botão encontrado no Olá nos ficheiros Leia-me de Olá no GitHub.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-134">hello simplest way toodeploy hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) template is toouse hello **Deploy tooAzure** button found in hello in hello readme files in GitHub.</span></span>  <span data-ttu-id="e5ed3-135">Também pode utilizar o PowerShell ou a CLI do Azure modelos de exemplo de Olá toodeploy.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-135">You can also use PowerShell or Azure CLI toodeploy hello sample templates.</span></span>

### <a name="powershell"></a><span data-ttu-id="e5ed3-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5ed3-136">PowerShell</span></span>
<span data-ttu-id="e5ed3-137">Olá cópia [servidor de HTTP de Python no Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) ou [aplicação MVC do ASP.NET no Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) ficheiros Olá GitHub repositório tooa pasta no computador local.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-137">Copy hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) files from hello GitHub repo tooa folder on your local computer.</span></span>  <span data-ttu-id="e5ed3-138">Abra Olá *azuredeploy.parameters.json* de ficheiros e atualização Olá os valores predefinidos de Olá `vmssName`, `adminUsername`, e `adminPassword` parâmetros.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-138">Open hello *azuredeploy.parameters.json* file and update hello default values of hello `vmssName`, `adminUsername`, and `adminPassword` parameters.</span></span> <span data-ttu-id="e5ed3-139">Guardar Olá seguinte script do PowerShell demasiado*deploy.ps1* no Olá mesma pasta que Olá *azuredeploy. JSON* modelo.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-139">Save hello following PowerShell script too*deploy.ps1* in hello same folder as hello *azuredeploy.json* template.</span></span> <span data-ttu-id="e5ed3-140">Olá de modelo executar de exemplo de Olá toodeploy *deploy.ps1* script a partir de uma janela de comando do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e5ed3-140">toodeploy hello sample template run hello *deploy.ps1* script from a PowerShell command window.</span></span>

```powershell
param(
 [Parameter(Mandatory=$True)]
 [string]
 $subscriptionId,

 [Parameter(Mandatory=$True)]
 [string]
 $resourceGroupName,

 [string]
 $resourceGroupLocation,

 [Parameter(Mandatory=$True)]
 [string]
 $deploymentName,

 [string]
 $templateFilePath = "template.json",

 [string]
 $parametersFilePath = "parameters.json"
)

<#
.SYNOPSIS
    Registers RPs
#>
Function RegisterRP {
    Param(
        [string]$ResourceProviderNamespace
    )

    Write-Host "Registering resource provider '$ResourceProviderNamespace'";
    Register-AzureRmResourceProvider -ProviderNamespace $ResourceProviderNamespace;
}

#******************************************************************************
# Script body
# Execution begins here
#******************************************************************************
$ErrorActionPreference = "Stop"

# sign in
Write-Host "Logging in...";
Login-AzureRmAccount;

# select subscription
Write-Host "Selecting subscription '$subscriptionId'";
Select-AzureRmSubscription -SubscriptionID $subscriptionId;

# Register RPs
$resourceProviders = @("microsoft.compute","microsoft.insights","microsoft.network");
if($resourceProviders.length) {
    Write-Host "Registering resource providers"
    foreach($resourceProvider in $resourceProviders) {
        RegisterRP($resourceProvider);
    }
}

#Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $resourceGroupName -ErrorAction SilentlyContinue
if(!$resourceGroup)
{
    Write-Host "Resource group '$resourceGroupName' does not exist. toocreate a new resource group, please enter a location.";
    if(!$resourceGroupLocation) {
        $resourceGroupLocation = Read-Host "resourceGroupLocation";
    }
    Write-Host "Creating resource group '$resourceGroupName' in location '$resourceGroupLocation'";
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else{
    Write-Host "Using existing resource group '$resourceGroupName'";
}

# Start hello deployment
Write-Host "Starting deployment...";
if(Test-Path $parametersFilePath) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath -TemplateParameterFile $parametersFilePath;
} else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath;
}
```

### <a name="azure-cli"></a><span data-ttu-id="e5ed3-141">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e5ed3-141">Azure CLI</span></span>
```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely toocause confusing bugs when looping arrays or arguments (e.g. $@)

usage() { echo "Usage: $0 -i <subscriptionId> -g <resourceGroupName> -n <deploymentName> -l <resourceGroupLocation>" 1>&2; exit 1; }

declare subscriptionId=""
declare resourceGroupName=""
declare deploymentName=""
declare resourceGroupLocation=""

# Initialize parameters specified from command line
while getopts ":i:g:n:l:" arg; do
    case "${arg}" in
        i)
            subscriptionId=${OPTARG}
            ;;
        g)
            resourceGroupName=${OPTARG}
            ;;
        n)
            deploymentName=${OPTARG}
            ;;
        l)
            resourceGroupLocation=${OPTARG}
            ;;
        esac
done
shift $((OPTIND-1))

#Prompt for parameters is some required parameters are missing
if [[ -z "$subscriptionId" ]]; then
    echo "Subscription Id:"
    read subscriptionId
    [[ "${subscriptionId:?}" ]]
fi

if [[ -z "$resourceGroupName" ]]; then
    echo "ResourceGroupName:"
    read resourceGroupName
    [[ "${resourceGroupName:?}" ]]
fi

if [[ -z "$deploymentName" ]]; then
    echo "DeploymentName:"
    read deploymentName
fi

if [[ -z "$resourceGroupLocation" ]]; then
    echo "Enter a location below toocreate a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file toobe used
templateFilePath="template.json"

if [ ! -f "$templateFilePath" ]; then
    echo "$templateFilePath not found"
    exit 1
fi

#parameter file path
parametersFilePath="parameters.json"

if [ ! -f "$parametersFilePath" ]; then
    echo "$parametersFilePath not found"
    exit 1
fi

if [ -z "$subscriptionId" ] || [ -z "$resourceGroupName" ] || [ -z "$deploymentName" ]; then
    echo "Either one of subscriptionId, resourceGroupName, deploymentName is empty"
    usage
fi

#login tooazure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set hello default subscription id
az account set --name $subscriptionId

set +e

#Check for existing RG
az group show $resourceGroupName 1> /dev/null

if [ $? != 0 ]; then
    echo "Resource group with name" $resourceGroupName "could not be found. Creating new resource group.."
    set -e
    (
        set -x
        az group create --name $resourceGroupName --location $resourceGroupLocation 1> /dev/null
    )
    else
    echo "Using existing resource group..."
fi

#Start deployment
echo "Starting deployment..."
(
    set -x
    az group deployment create --name $deploymentName --resource-group $resourceGroupName --template-file $templateFilePath --parameters $parametersFilePath
)

if [ $?  == 0 ];
 then
    echo "Template has been successfully deployed"
fi
```

## <a name="next-steps"></a><span data-ttu-id="e5ed3-142">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e5ed3-142">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
