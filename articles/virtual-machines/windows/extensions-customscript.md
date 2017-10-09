---
title: "aaaAzure extensão de Script personalizado para Windows | Microsoft Docs"
description: "Automatizar tarefas de configuração de VM do Windows utilizando a extensão de Script personalizado Olá"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f4181fee-7a9d-4a1c-b517-52956f5b7fa1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/16/2017
ms.author: nepeters
ms.openlocfilehash: 97e065242e9fed116ee20b074f4e302a0cd10585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows"></a><span data-ttu-id="6bb44-103">Extensão de Script personalizado para o Windows</span><span class="sxs-lookup"><span data-stu-id="6bb44-103">Custom Script Extension for Windows</span></span>

<span data-ttu-id="6bb44-104">Olá extensão de Script personalizado transfere e executa os scripts em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="6bb44-104">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="6bb44-105">Esta extensão é útil para configuração de implementação de post, instalação de software ou qualquer outra configuração / tarefas de gestão.</span><span class="sxs-lookup"><span data-stu-id="6bb44-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="6bb44-106">Scripts podem ser transferidos a partir do armazenamento do Azure ou do GitHub, ou fornecidos toohello do portal do Azure em tempo de execução de extensão.</span><span class="sxs-lookup"><span data-stu-id="6bb44-106">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span> <span data-ttu-id="6bb44-107">Olá a extensão de Script personalizado se integra com modelos Azure Resource Manager e também pode ser executado utilizando Olá CLI do Azure, o PowerShell, o portal do Azure ou o Olá API de REST de Máquina Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="6bb44-107">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="6bb44-108">Este documento fornece detalhes sobre como utilizar o toouse Olá extensão de Script personalizado Olá módulo Azure PowerShell, os modelos Azure Resource Manager e detalhes de resolução de problemas de passos em sistemas Windows.</span><span class="sxs-lookup"><span data-stu-id="6bb44-108">This document details how toouse hello Custom Script Extension using hello Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bb44-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6bb44-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="6bb44-110">Sistema Operativo</span><span class="sxs-lookup"><span data-stu-id="6bb44-110">Operating System</span></span>

<span data-ttu-id="6bb44-111">Olá extensão de Script personalizado para o Windows pode ser executado no Windows Server 2008 R2, 2012, 2012 R2 e 2016 versões.</span><span class="sxs-lookup"><span data-stu-id="6bb44-111">hello Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="6bb44-112">Localização do script</span><span class="sxs-lookup"><span data-stu-id="6bb44-112">Script Location</span></span>

<span data-ttu-id="6bb44-113">script de Olá tem toobe armazenado no Blob storage do Azure ou qualquer outra localização acessível através de um URL válido.</span><span class="sxs-lookup"><span data-stu-id="6bb44-113">hello script needs toobe stored in Azure Blob storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="6bb44-114">Conectividade Internet</span><span class="sxs-lookup"><span data-stu-id="6bb44-114">Internet Connectivity</span></span>

<span data-ttu-id="6bb44-115">Olá extensão de Script personalizado para o Windows necessita de máquina virtual de destino que Olá é toohello ligado à internet.</span><span class="sxs-lookup"><span data-stu-id="6bb44-115">hello Custom Script Extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="6bb44-116">Esquema de extensão</span><span class="sxs-lookup"><span data-stu-id="6bb44-116">Extension schema</span></span>

<span data-ttu-id="6bb44-117">Olá seguinte JSON mostra esquema Olá para Olá extensão de Script personalizado.</span><span class="sxs-lookup"><span data-stu-id="6bb44-117">hello following JSON shows hello schema for hello Custom Script Extension.</span></span> <span data-ttu-id="6bb44-118">extensão de Olá requer uma localização de script (Storage do Azure ou noutro local de URL válido) e um tooexecute de comando.</span><span class="sxs-lookup"><span data-stu-id="6bb44-118">hello extension requires a script location (Azure Storage or other location with valid URL), and a command tooexecute.</span></span> <span data-ttu-id="6bb44-119">Se utilizar o Storage do Azure como origem do script Olá, uma chave de conta e o nome da conta de armazenamento do Azure é necessária.</span><span class="sxs-lookup"><span data-stu-id="6bb44-119">If using Azure Storage as hello script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="6bb44-120">Estes itens devem ser tratados como dados confidenciais e especificados na configuração de definição protegido Olá extensões.</span><span class="sxs-lookup"><span data-stu-id="6bb44-120">These items should be treated as sensitive data and specified in hello extensions protected setting configuration.</span></span> <span data-ttu-id="6bb44-121">Dados de definição de extensão protegido de VM do Azure é encriptados e desencriptados apenas na máquina de virtual de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="6bb44-121">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span>

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
        "typeHandlerVersion": "1.9",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "script location"
            ]
        },
        "protectedSettings": {
            "commandToExecute": "myExecutionCommand",
            "storageAccountName": "myStorageAccountName",
            "storageAccountKey": "myStorageAccountKey"
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="6bb44-122">Valores de propriedade</span><span class="sxs-lookup"><span data-stu-id="6bb44-122">Property values</span></span>

| <span data-ttu-id="6bb44-123">Nome</span><span class="sxs-lookup"><span data-stu-id="6bb44-123">Name</span></span> | <span data-ttu-id="6bb44-124">Valor / exemplo</span><span class="sxs-lookup"><span data-stu-id="6bb44-124">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="6bb44-125">apiVersion</span><span class="sxs-lookup"><span data-stu-id="6bb44-125">apiVersion</span></span> | <span data-ttu-id="6bb44-126">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="6bb44-126">2015-06-15</span></span> |
| <span data-ttu-id="6bb44-127">Fabricante</span><span class="sxs-lookup"><span data-stu-id="6bb44-127">publisher</span></span> | <span data-ttu-id="6bb44-128">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="6bb44-128">Microsoft.Compute</span></span> |
| <span data-ttu-id="6bb44-129">tipo</span><span class="sxs-lookup"><span data-stu-id="6bb44-129">type</span></span> | <span data-ttu-id="6bb44-130">extensões</span><span class="sxs-lookup"><span data-stu-id="6bb44-130">extensions</span></span> |
| <span data-ttu-id="6bb44-131">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="6bb44-131">typeHandlerVersion</span></span> | <span data-ttu-id="6bb44-132">1.9</span><span class="sxs-lookup"><span data-stu-id="6bb44-132">1.9</span></span> |
| <span data-ttu-id="6bb44-133">fileUris (por exemplo)</span><span class="sxs-lookup"><span data-stu-id="6bb44-133">fileUris (e.g)</span></span> | <span data-ttu-id="6bb44-134">https://RAW.githubusercontent.com/Microsoft/DotNet-Core-Sample-Templates/Master/DotNet-Core-Music-Windows/scripts/configure-Music-App.ps1</span><span class="sxs-lookup"><span data-stu-id="6bb44-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="6bb44-135">commandToExecute (por exemplo)</span><span class="sxs-lookup"><span data-stu-id="6bb44-135">commandToExecute (e.g)</span></span> | <span data-ttu-id="6bb44-136">PowerShell sem restrições - ExecutionPolicy - configurar-música-app.ps1 de ficheiros</span><span class="sxs-lookup"><span data-stu-id="6bb44-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |
| <span data-ttu-id="6bb44-137">storageAccountName (por exemplo)</span><span class="sxs-lookup"><span data-stu-id="6bb44-137">storageAccountName (e.g)</span></span> | <span data-ttu-id="6bb44-138">examplestorageacct</span><span class="sxs-lookup"><span data-stu-id="6bb44-138">examplestorageacct</span></span> |
| <span data-ttu-id="6bb44-139">storageAccountKey (por exemplo)</span><span class="sxs-lookup"><span data-stu-id="6bb44-139">storageAccountKey (e.g)</span></span> | <span data-ttu-id="6bb44-140">TmJK/1N3AbAZ3q / + hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg = =</span><span class="sxs-lookup"><span data-stu-id="6bb44-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span></span> |

<span data-ttu-id="6bb44-141">**Tenha em atenção** -estes nomes de propriedade são sensíveis a maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="6bb44-141">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="6bb44-142">Utilize nomes de Olá, como mostrado acima tooavoid problemas de implementação.</span><span class="sxs-lookup"><span data-stu-id="6bb44-142">Use hello names as seen above tooavoid deployment issues.</span></span>

## <a name="template-deployment"></a><span data-ttu-id="6bb44-143">Implementação de modelos</span><span class="sxs-lookup"><span data-stu-id="6bb44-143">Template deployment</span></span>

<span data-ttu-id="6bb44-144">Extensões VM do Azure podem ser implementadas com modelos Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6bb44-144">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="6bb44-145">esquema JSON Olá descrita na secção anterior Olá pode ser utilizada numa Olá de toorun de modelo Azure Resource Manager extensão de Script personalizado durante uma implementação de modelo Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6bb44-145">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="6bb44-146">Um modelo de exemplo inclui Olá extensão de Script personalizado pode ser encontrada aqui, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="6bb44-146">A sample template that includes hello Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="6bb44-147">Implementação de PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bb44-147">PowerShell deployment</span></span>

<span data-ttu-id="6bb44-148">Olá `Set-AzureRmVMCustomScriptExtension` comando pode ser utilizado tooadd Olá Script personalizado extensão tooan máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="6bb44-148">hello `Set-AzureRmVMCustomScriptExtension` command can be used tooadd hello Custom Script extension tooan existing virtual machine.</span></span> <span data-ttu-id="6bb44-149">Para obter mais informações, consulte [conjunto AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="6bb44-149">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="6bb44-150">Resolver problemas e suporte</span><span class="sxs-lookup"><span data-stu-id="6bb44-150">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="6bb44-151">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="6bb44-151">Troubleshoot</span></span>

<span data-ttu-id="6bb44-152">Dados sobre o estado de Olá das implementações de extensão de podem ser obtidos a partir da Olá portal do Azure e utilizando o módulo do Azure PowerShell Olá.</span><span class="sxs-lookup"><span data-stu-id="6bb44-152">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="6bb44-153">Estado da implementação de Olá toosee das extensões para uma determinada VM, execute Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="6bb44-153">toosee hello deployment state of extensions for a given VM, run hello following command.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="6bb44-154">Execução de extensão de saída é iniciada toofiles encontrado em Olá seguindo diretório do Olá máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="6bb44-154">Extension execution output is logged toofiles found under hello following directory on hello target virtual machine.</span></span>
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="6bb44-155">Olá especificar os ficheiros são transferidos para Olá seguindo o diretório do Olá máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="6bb44-155">hello specified files are downloaded into hello following directory on hello target virtual machine.</span></span>
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
<span data-ttu-id="6bb44-156">onde `<n>` é um número inteiro decimal que pode ser alterada entre execuções de extensão de Olá.</span><span class="sxs-lookup"><span data-stu-id="6bb44-156">where `<n>` is a decimal integer which may change between executions of hello extension.</span></span>  <span data-ttu-id="6bb44-157">Olá `1.*` valor corresponde à atual real, Olá `typeHandlerVersion` valor da extensão de Olá.</span><span class="sxs-lookup"><span data-stu-id="6bb44-157">hello `1.*` value matches hello actual, current `typeHandlerVersion` value of hello extension.</span></span>  <span data-ttu-id="6bb44-158">Por exemplo, poderia ser diretório real Olá `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span><span class="sxs-lookup"><span data-stu-id="6bb44-158">For example, hello actual directory could be `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span></span>  

<span data-ttu-id="6bb44-159">Ao executar Olá `commandToExecute` comando, a extensão de Olá ter definirá neste diretório (por exemplo, `...\Downloads\2`) como diretório de trabalho atual Olá.</span><span class="sxs-lookup"><span data-stu-id="6bb44-159">When executing hello `commandToExecute` command, hello extension will have set this directory (e.g., `...\Downloads\2`) as hello current working directory.</span></span> <span data-ttu-id="6bb44-160">Esta utilização de Olá permite dos ficheiros de Olá caminhos relativos toolocate transferidos através do Olá `fileURIs` propriedade.</span><span class="sxs-lookup"><span data-stu-id="6bb44-160">This enables hello use of relative paths toolocate hello files downloaded via hello `fileURIs` property.</span></span> <span data-ttu-id="6bb44-161">Consulte a tabela de Olá abaixo para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="6bb44-161">See hello table below for examples.</span></span>

<span data-ttu-id="6bb44-162">Uma vez que o caminho de transferência absoluto de Olá pode variar devido ao longo do tempo, é melhor tooopt para caminhos de script/ficheiro relativo no Olá `commandToExecute` string, sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="6bb44-162">Since hello absolute download path may vary over time, it is better tooopt for relative script/file paths in hello `commandToExecute` string, whenever possible.</span></span> <span data-ttu-id="6bb44-163">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6bb44-163">For example:</span></span>
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

<span data-ttu-id="6bb44-164">Informações de caminho depois de segmento URI primeiro Olá é mantido para os ficheiros transferidos através do Olá `fileUris` lista de propriedades.</span><span class="sxs-lookup"><span data-stu-id="6bb44-164">Path information after hello first URI segment is retained for files downloaded via hello `fileUris` property list.</span></span>  <span data-ttu-id="6bb44-165">Conforme mostrado na tabela de Olá abaixo, os ficheiros transferidos estão mapeados numa estrutura de Olá do transferência subdiretórios tooreflect de Olá `fileUris` valores.</span><span class="sxs-lookup"><span data-stu-id="6bb44-165">As shown in hello table below, downloaded files are mapped into download subdirectories tooreflect hello structure of hello `fileUris` values.</span></span>  

#### <a name="examples-of-downloaded-files"></a><span data-ttu-id="6bb44-166">Exemplos de ficheiros transferidos</span><span class="sxs-lookup"><span data-stu-id="6bb44-166">Examples of Downloaded Files</span></span>

| <span data-ttu-id="6bb44-167">URI no fileUris</span><span class="sxs-lookup"><span data-stu-id="6bb44-167">URI in fileUris</span></span> | <span data-ttu-id="6bb44-168">Caminho relativo de localização de transferência</span><span class="sxs-lookup"><span data-stu-id="6bb44-168">Relative downloaded location</span></span> | <span data-ttu-id="6bb44-169">Localização de transferência absoluto *</span><span class="sxs-lookup"><span data-stu-id="6bb44-169">Absolute downloaded location *</span></span> |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

<span data-ttu-id="6bb44-170">\*Como acima, os caminhos de diretório absoluto de Olá serão alterado ao longo da duração de Olá de Olá VM, mas não uma execução única da extensão CustomScript Olá.</span><span class="sxs-lookup"><span data-stu-id="6bb44-170">\* As above, hello absolute directory paths will change over hello lifetime of hello VM, but not within a single execution of hello CustomScript extension.</span></span>

### <a name="support"></a><span data-ttu-id="6bb44-171">Suporte</span><span class="sxs-lookup"><span data-stu-id="6bb44-171">Support</span></span>

<span data-ttu-id="6bb44-172">Se precisar de mais ajuda, a qualquer altura neste artigo, pode contactar Olá especialistas do Azure no Olá [fóruns do MSDN Azure e Stack Overflow] (https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="6bb44-172">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums] (https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="6bb44-173">Em alternativa, pode ficheiro um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="6bb44-173">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="6bb44-174">Aceda toohello [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione o suporte de Get.</span><span class="sxs-lookup"><span data-stu-id="6bb44-174">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="6bb44-175">Para obter informações sobre como utilizar o suporte do Azure, leia o artigo Olá [suporte do Microsoft Azure FAQ](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="6bb44-175">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
