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
# <a name="deploy-an-autoscaling-app-using-a-template"></a>Implementar uma aplicação de dimensionamento automático através de um modelo

[Modelos Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) é uma excelente forma toodeploy grupos de recursos relacionados. Este tutorial baseia-se [implementar um conjunto de dimensionamento simples](virtual-machine-scale-sets-mvss-start.md) e descreve como toodeploy uma aplicação de dimensionamento automático simples numa escala definido de utilizando um modelo Azure Resource Manager.  Também pode configurar com o PowerShell, o CLI ou o portal de Olá de dimensionamento automático. Para obter mais informações, consulte [Descrição geral do dimensionamento automático](virtual-machine-scale-sets-autoscale-overview.md).

## <a name="two-quickstart-templates"></a>Dois modelos de início rápido
Quando implementa um conjunto de dimensionamento, instala o novo software numa plataforma de imagens que usa uma [extensão de VM](../virtual-machines/virtual-machines-windows-extensions-features.md). Uma extensão de VM é uma pequena aplicação que fornece tarefas de configuração e automação de pós-implementação em máquinas virtuais do Azure, tais como implementar uma aplicação. Dois modelos de outro exemplo são fornecidos na [/azure-guia de introdução-modelos do Azure](https://github.com/Azure/azure-quickstart-templates) que mostram como toodeploy uma aplicação de dimensionamento automático para uma escala definido utilizando extensões VM.

### <a name="python-http-server-on-linux"></a>Servidor de HTTP do Python no Linux
Olá [servidor de HTTP de Python no Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) modelo de exemplo implementa uma aplicação de dimensionamento automático simples em execução num conjunto de dimensionamento do Linux.  [Bottle](http://bottlepy.org/docs/dev/), um Python web framework e um servidor HTTP simple são implementadas em cada VM em escala Olá definida utilizando um script personalizado extensão da VM. escala de Olá Definir escalas quando a utilização da CPU média em todas as VMs é maior do que 60% e reduz horizontalmente para baixo, quando a utilização da CPU média Olá é inferior a 30%.

Além disso toohello conjunto de dimensionamento de recurso, hello *azuredeploy. JSON* modelo de exemplo também declara rede virtual, o endereço IP público, o Balanceador de carga e recursos de definições de dimensionamento automático.  Para obter mais informações sobre como criar esses recursos num modelo, consulte [Conjunto de dimensionamento do Linux escala automática](virtual-machine-scale-sets-linux-autoscale.md).

No Olá *azuredeploy. JSON* modelo, Olá `extensionProfile` propriedade Olá `Microsoft.Compute/virtualMachineScaleSets` recurso Especifica uma extensão de script personalizado. `fileUris`Especifica a localização de script(s) Olá. Neste caso, dois ficheiros: *workserver.py*, que define um servidor HTTP simple, e *installserver.sh*, que instala o Bottle e inicia Olá servidor de HTTP. `commandToExecute`Especifica Olá comando toorun depois do conjunto de dimensionamento de Olá foi implementado.

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

### <a name="aspnet-mvc-application-on-windows"></a>Aplicação ASP.NET MVC no Windows
Olá [aplicação MVC do ASP.NET no Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) modelo de exemplo implementa uma aplicação ASP.NET MVC simples em execução no IIS no conjunto de dimensionamento do Windows.  IIS e Olá aplicação MVC são implementadas através de Olá [PowerShell estado configuração pretendido (DSC)](virtual-machine-scale-sets-dsc.md) extensão da VM.  escala de Olá configurar escalas (na instância de VM a uma hora) quando a utilização da CPU é superior a 50% para 5 minutos. 

Além disso toohello conjunto de dimensionamento de recurso, hello *azuredeploy. JSON* modelo de exemplo também declara rede virtual, o endereço IP público, o Balanceador de carga e recursos de definições de dimensionamento automático. Este modelo também demonstra a atualização da aplicação.  Para obter mais informações sobre como criar esses recursos num modelo, consulte [Conjunto de dimensionamento do Windows com escala automática](virtual-machine-scale-sets-windows-autoscale.md).

No Olá *azuredeploy. JSON* modelo, Olá `extensionProfile` propriedade Olá `Microsoft.Compute/virtualMachineScaleSets` recurso Especifica um [configuração de estado pretendido (DSC)](virtual-machine-scale-sets-dsc.md) extensão que instala o IIS e uma predefinição aplicação Web a partir de um pacote de WebDeploy.  Olá *IISInstall.ps1* script instala o IIS na máquina virtual de Olá e se encontra no Olá *DSC* pasta.  aplicação de web MVC Olá se encontra no Olá *WebDeploy* pasta.  script de instalação do Olá caminhos toohello e aplicação de web de Olá são definidos no Olá `powershelldscZip` e `webDeployPackage` parâmetros Olá *azuredeploy.parameters.json* ficheiro. 

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

## <a name="deploy-hello-template"></a>Implementar a modelo Olá
Olá toodeploy da forma mais simples do Olá [servidor de HTTP de Python no Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) ou [aplicação MVC do ASP.NET no Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) modelo é toouse Olá **implementar tooAzure** botão encontrado no Olá nos ficheiros Leia-me de Olá no GitHub.  Também pode utilizar o PowerShell ou a CLI do Azure modelos de exemplo de Olá toodeploy.

### <a name="powershell"></a>PowerShell
Olá cópia [servidor de HTTP de Python no Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) ou [aplicação MVC do ASP.NET no Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) ficheiros Olá GitHub repositório tooa pasta no computador local.  Abra Olá *azuredeploy.parameters.json* de ficheiros e atualização Olá os valores predefinidos de Olá `vmssName`, `adminUsername`, e `adminPassword` parâmetros. Guardar Olá seguinte script do PowerShell demasiado*deploy.ps1* no Olá mesma pasta que Olá *azuredeploy. JSON* modelo. Olá de modelo executar de exemplo de Olá toodeploy *deploy.ps1* script a partir de uma janela de comando do PowerShell.

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

### <a name="azure-cli"></a>CLI do Azure
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

## <a name="next-steps"></a>Passos seguintes

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
