---
title: "Implementação de aplicação com extensões de Máquina Virtual de aaaAutomating | Microsoft Docs"
description: "Tutorial do DotNet núcleos de Máquina Virtual do Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 79c91304-6c1b-4354-a185-fecc129b139d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6d52537fbd4e935f19d3864def11484f519f8598
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="46431-103">Implementação de aplicação com modelos Azure Resource Manager para VMs do Windows</span><span class="sxs-lookup"><span data-stu-id="46431-103">Application deployment with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="46431-104">Depois de tem identificados e convertidos de um modelo de implementação de todos os requisitos de infraestrutura do Azure, implementação de aplicação real Olá tem toobe resolvido.</span><span class="sxs-lookup"><span data-stu-id="46431-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, hello actual application deployment needs toobe addressed.</span></span> <span data-ttu-id="46431-105">Implementação de aplicação aqui faz referência binários da aplicação real Olá tooinstalling para recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="46431-105">Application deployment here is referring tooinstalling hello actual application binaries onto Azure resources.</span></span> <span data-ttu-id="46431-106">Para o exemplo de arquivo de música Olá, .net Core e o IIS necessita toobe instalado e configurado em cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="46431-106">For hello Music Store sample, .Net Core and IIS need toobe installed and configured on each virtual machine.</span></span> <span data-ttu-id="46431-107">Olá loja de música binários necessário toobe instalado na máquina virtual de Olá e Olá base de dados do arquivo de música previamente criada.</span><span class="sxs-lookup"><span data-stu-id="46431-107">hello Music Store binaries need toobe installed onto hello virtual machine, and hello Music Store database pre-created.</span></span>

<span data-ttu-id="46431-108">Este documento fornece detalhes sobre como extensões de Máquina Virtual podem automatizar a aplicação de implementação e configuração tooAzure máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="46431-108">This document details how Virtual Machine extensions can automate application deployment and configuration tooAzure virtual machines.</span></span> <span data-ttu-id="46431-109">Todas as dependências e configurações exclusivas são realçadas.</span><span class="sxs-lookup"><span data-stu-id="46431-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="46431-110">Para uma experiência otimizada Olá, pré-implemente uma instância de trabalho, juntamente com o modelo do Azure Resource Manager Olá e Olá solução tooyour subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="46431-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="46431-111">modelo completo Olá pode ser encontrado aqui – [implementação de arquivo de música em Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="46431-111">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="46431-112">Script de configuração</span><span class="sxs-lookup"><span data-stu-id="46431-112">Configuration script</span></span>
<span data-ttu-id="46431-113">Extensões de máquina virtual são programas especializados que executar em relação a automatização de configuração de tooprovide de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="46431-113">Virtual Machine extensions are specialized programs that execute against virtual machines tooprovide configuration automation.</span></span> <span data-ttu-id="46431-114">As extensões estão disponíveis para vários fins específicos, tais como o software antivírus, a configuração de registo e a configuração de Docker.</span><span class="sxs-lookup"><span data-stu-id="46431-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="46431-115">Olá a extensão de Script personalizado pode ser utilizado toorun qualquer script em relação a uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="46431-115">hello Custom Script extension can be used toorun any script against a virtual machine.</span></span> <span data-ttu-id="46431-116">Exemplo do arquivo de música Olá, está a funcionar toohello script personalizado extensão tooconfigure Olá máquinas virtuais do Windows e instalar a aplicação da loja de música Olá.</span><span class="sxs-lookup"><span data-stu-id="46431-116">With hello Music Store sample, it is up toohello custom script extension tooconfigure hello Windows virtual machines and install hello Music Store application.</span></span>

<span data-ttu-id="46431-117">Antes de com detalhes sobre como as extensões de máquina virtual são declaradas num modelo Azure Resource Manager, examine o script de Olá que está a ser executado.</span><span class="sxs-lookup"><span data-stu-id="46431-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine hello script that is run.</span></span> <span data-ttu-id="46431-118">Este script configura Olá Windows máquina virtual toohost hello aplicação da loja de música.</span><span class="sxs-lookup"><span data-stu-id="46431-118">This script configures hello Windows virtual machine toohost hello Music Store application.</span></span> <span data-ttu-id="46431-119">Quando executada, o script de Olá instala software todos os necessário, instalar aplicação da loja de música Olá do controlo de origem e preparar Olá base de dados.</span><span class="sxs-lookup"><span data-stu-id="46431-119">When run, hello script installs all needed software, install hello Music store application from source control, and prepare hello database.</span></span> 

> <span data-ttu-id="46431-120">Este exemplo está para efeitos de demonstração.</span><span class="sxs-lookup"><span data-stu-id="46431-120">This sample is for demonstration purposes.</span></span>

```PowerShell
<#
    .SYNOPSIS
        Downloads and configures .Net Core Music Store application sample across IIS and Azure SQL DB.
#>

Param (
    [string]$user,
    [string]$password,
    [string]$sqlserver
)

# Firewall
netsh advfirewall firewall add rule name="http" dir=in action=allow protocol=TCP localport=80

# Folders
New-Item -ItemType Directory c:\temp
New-Item -ItemType Directory c:\music

# Install iis
Install-WindowsFeature web-server -IncludeManagementTools

# Install dot.net core sdk
Invoke-WebRequest http://go.microsoft.com/fwlink/?LinkID=615460 -outfile c:\temp\vc_redistx64.exe
Start-Process c:\temp\vc_redistx64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkID=809122 -outfile c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe
Start-Process c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkId=817246 -outfile c:\temp\DotNetCore.WindowsHosting.exe
Start-Process c:\temp\DotNetCore.WindowsHosting.exe -ArgumentList '/quiet' -Wait

# Download music app
Invoke-WebRequest  https://github.com/Microsoft/dotnet-core-sample-templates/raw/master/dotnet-core-music-windows/music-app/music-store-azure-demo-pub.zip -OutFile c:\temp\musicstore.zip
Expand-Archive C:\temp\musicstore.zip c:\music

# Azure SQL connection sting in environment variable
[Environment]::SetEnvironmentVariable("Data:DefaultConnection:ConnectionString", "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30",[EnvironmentVariableTarget]::Machine)

# Pre-create database
$env:Data:DefaultConnection:ConnectionString = "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30"
Start-Process 'C:\Program Files\dotnet\dotnet.exe' -ArgumentList 'c:\music\MusicStore.dll'

# Configure iis
Remove-WebSite -Name "Default Web Site"
Set-ItemProperty IIS:\AppPools\DefaultAppPool\ managedRuntimeVersion ""
New-Website -Name "MusicStore" -Port 80 -PhysicalPath C:\music\ -ApplicationPool DefaultAppPool
& iisreset
```

## <a name="vm-script-extension"></a><span data-ttu-id="46431-121">Extensão de Script VM</span><span class="sxs-lookup"><span data-stu-id="46431-121">VM Script Extension</span></span>
<span data-ttu-id="46431-122">Extensões de VM podem ser executadas em relação a uma máquina virtual no momento da compilação, incluindo o recurso de extensão de Olá num modelo do Azure Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="46431-122">VM Extensions can be run against a virtual machine at build time by including hello extension resource in hello Azure Resource Manager template.</span></span> <span data-ttu-id="46431-123">extensão de Olá pode ser adicionado com o Assistente de Visual Studio adicionar recursos Olá ou por inserir o modelo de Olá JSON válido.</span><span class="sxs-lookup"><span data-stu-id="46431-123">hello extension can be added with hello Visual Studio Add Resource wizard, or by inserting valid JSON into hello template.</span></span> <span data-ttu-id="46431-124">Olá recursos de extensão de Script é aninhada Olá recurso de Máquina Virtual Isto pode ser visto no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="46431-124">hello Script Extension resource is nested inside hello Virtual Machine resource; this can be seen in hello following example.</span></span>

<span data-ttu-id="46431-125">Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [extensão de Script de VM](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span><span class="sxs-lookup"><span data-stu-id="46431-125">Follow this link toosee hello JSON sample within hello Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span></span> 

<span data-ttu-id="46431-126">Observe que, Olá abaixo JSON Olá script é armazenado no GitHub.</span><span class="sxs-lookup"><span data-stu-id="46431-126">Notice in hello below JSON that hello script is stored in GitHub.</span></span> <span data-ttu-id="46431-127">Este script também pode ser armazenado no Blob storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="46431-127">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="46431-128">Além disso, os modelos Azure Resource Manager permitem Olá script execução cadeia toobe construída de forma a que os valores de parâmetros de modelo podem ser utilizados como parâmetros para a execução do script.</span><span class="sxs-lookup"><span data-stu-id="46431-128">Also, Azure Resource Manager templates allow hello script execution string toobe constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="46431-129">Neste caso, os dados são fornecidos quando implementar modelos de Olá e estes valores podem ser utilizados ao executar o script de Olá.</span><span class="sxs-lookup"><span data-stu-id="46431-129">In this case data is provided when deploying hello templates, and these values can then be used when executing hello script.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
  }
}
```

<span data-ttu-id="46431-130">Conforme mencionado, é também possível toostore sua personalizado de scripts no Blob storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="46431-130">As mentioned above, it is also possible toostore your custom scripts in Azure Blob storage.</span></span> <span data-ttu-id="46431-131">Existem duas opções para armazenar recursos de script de Olá no armazenamento de BLOBs torne Olá público de contentor/script e siga Olá mesmo abordar conforme apresentado acima, ou também podem ser mantido no armazenamento de BLOBs privada que requeiram tooprovide Olá storageAccountName e storageAccountKey toohello CustomScriptExtension definição do recurso.</span><span class="sxs-lookup"><span data-stu-id="46431-131">There are two options for storing hello script resources in blob storage; either make hello container/script public and follow hello same approach as above, or it can also be kept in private blob storage which requires you tooprovide hello storageAccountName and storageAccountKey toohello CustomScriptExtension resource definition.</span></span>

<span data-ttu-id="46431-132">No exemplo Olá abaixo podemos ter decorrido um passo adicional.</span><span class="sxs-lookup"><span data-stu-id="46431-132">In hello example below we have gone a step further.</span></span> <span data-ttu-id="46431-133">Embora seja nome de conta de armazenamento de Olá tooprovide possíveis e a chave como um parâmetro ou variável durante a implementação, os modelos do Resource Manager fornecem Olá `listKeys` função que pode obter a conta de armazenamento Olá chave através de programação e insira-o no toohello modelo para si no momento da implementação.</span><span class="sxs-lookup"><span data-stu-id="46431-133">While it is possible tooprovide hello storage account name and key as a parameter or variable during deployment, Resource Manager templates provide hello `listKeys` function that can obtain hello storage account key programmatically and insert it in toohello template for you at deployment time.</span></span>

<span data-ttu-id="46431-134">Exemplo de Olá CustomScriptExtension definição do recurso abaixo, nosso script personalizado já foi carregado tooan denominada conta do storage do Azure `mystorageaccount9999` qual existe noutro grupo de recursos chamado `mysa999rgname`.</span><span class="sxs-lookup"><span data-stu-id="46431-134">In hello example CustomScriptExtension resource definition below, our custom script has already been uploaded tooan Azure storage account called `mystorageaccount9999` which exists in another Resource Group called `mysa999rgname`.</span></span> <span data-ttu-id="46431-135">Quando é implementar um modelo que contém este recurso, Olá `listKeys` função através de programação obtém a chave de conta do storage Olá Olá conta de armazenamento `mystorageaccount9999` no grupo de recursos de Olá `mysa999rgname` e insere-o no modelo de toohello para-nos.</span><span class="sxs-lookup"><span data-stu-id="46431-135">When we deploy a template containing this resource, hello `listKeys` function programmatically obtains hello storage account key for hello storage account `mystorageaccount9999` in hello Resource Group `mysa999rgname` and inserts it in toohello template for us.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://mystorageaccount9999.blob.core.windows.net/container/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]",
      "storageAccountName": "mystorageaccount9999",
      "storageAccountKey": "[listKeys(resourceId('mysa999rgname','Microsoft.Storage/storageAccounts', mystorageaccount9999), '2015-06-15').key1]"
    }
  }
}
```

<span data-ttu-id="46431-136">benefício de principais de Olá desta abordagem é que não requer toochange o modelo ou parâmetros de implementação no evento Olá de Olá armazenamento o alterar chave da conta.</span><span class="sxs-lookup"><span data-stu-id="46431-136">hello main benefit of this approach is that it does not require you toochange your template or deployment parameters in hello event of hello storage account key changing.</span></span>

<span data-ttu-id="46431-137">Para obter mais informações sobre como utilizar a extensão de script personalizado Olá, consulte [extensões de script personalizado com modelos do Resource Manager](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="46431-137">For more information on using hello custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="46431-138">Passo seguinte</span><span class="sxs-lookup"><span data-stu-id="46431-138">Next Step</span></span>
<hr>

[<span data-ttu-id="46431-139">Explorar os modelos do Gestor de recursos do Azure mais</span><span class="sxs-lookup"><span data-stu-id="46431-139">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

