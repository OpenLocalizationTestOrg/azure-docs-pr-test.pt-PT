---
title: "aaaDesired modelo de Gestor de recursos de configuração de estado | Microsoft Docs"
description: "Definição de modelo do Resource Manager para a configuração de estado pretendido no Azure com exemplos e resolução de problemas"
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: b5402e5a-1768-4075-8c19-b7f7402687af
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: fc47ac149b1179d9305797eaa8ed8a83c0958c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a><span data-ttu-id="dd661-103">Windows VMSS e configuração de estado pretendido com modelos Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dd661-103">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>
<span data-ttu-id="dd661-104">Este artigo descreve o modelo do Resource Manager Olá para Olá [processador de extensão de configuração de estado pretendido](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd661-104">This article describes hello Resource Manager template for hello [Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="template-example-for-a-windows-vm"></a><span data-ttu-id="dd661-105">Exemplo de modelo para uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="dd661-105">Template example for a Windows VM</span></span>
<span data-ttu-id="dd661-106">Olá seguinte fragmento entra Olá secção de recurso de modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="dd661-106">hello following snippet goes into hello Resource section of hello template.</span></span>

```json
            "name": "Microsoft.Powershell.DSC",
            "type": "extensions",
             "location": "[resourceGroup().location]",
             "apiVersion": "2015-06-15",
             "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "dscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }

```

## <a name="template-example-for-windows-vmss"></a><span data-ttu-id="dd661-107">Exemplo de modelo para VMSS do Windows</span><span class="sxs-lookup"><span data-stu-id="dd661-107">Template example for Windows VMSS</span></span>
<span data-ttu-id="dd661-108">Um nó VMSS tem uma secção de "Propriedades" com o Olá "VirtualMachineProfile". o atributo "extensionProfile".</span><span class="sxs-lookup"><span data-stu-id="dd661-108">A VMSS node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="dd661-109">DSC é adicionado em "extensões".</span><span class="sxs-lookup"><span data-stu-id="dd661-109">DSC is added under "extensions".</span></span> 

```json
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": true,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
        }
```

## <a name="detailed-settings-information"></a><span data-ttu-id="dd661-110">Informações de definições detalhadas</span><span class="sxs-lookup"><span data-stu-id="dd661-110">Detailed Settings Information</span></span>
<span data-ttu-id="dd661-111">Olá esquema seguinte é para Olá definições parte Olá extensão de DSC do Azure num modelo Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dd661-111">hello following schema is for hello settings portion of hello Azure DSC extension in an Azure Resource Manager template.</span></span>

```json

"settings": {
  "wmfVersion": "latest",
  "configuration": {
    "url": "http://validURLToConfigLocation",
    "script": "ConfigurationScript.ps1",
    "function": "ConfigurationFunction"
  },
  "configurationArguments": {
    "argument1": "Value1",
    "argument2": "Value2"
  },
  "configurationData": {
    "url": "https://foo.psd1"
  },
  "privacy": {
    "dataCollection": "enable"
  },
  "advancedOptions": {
    "downloadMappings": {
      "customWmfLocation": "http://myWMFlocation"
    }
  } 
},
"protectedSettings": {
  "configurationArguments": {
    "parameterOfTypePSCredential1": {
      "userName": "UsernameValue1",
      "password": "PasswordValue1"
    },
    "parameterOfTypePSCredential2": {
      "userName": "UsernameValue2",
      "password": "PasswordValue2"
    }
  },
  "configurationUrlSasToken": "?g!bber1sht0k3n",
  "configurationDataUrlSasToken": "?dataAcC355T0k3N"
}

```

## <a name="details"></a><span data-ttu-id="dd661-112">Detalhes</span><span class="sxs-lookup"><span data-stu-id="dd661-112">Details</span></span>
| <span data-ttu-id="dd661-113">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="dd661-113">Property Name</span></span> | <span data-ttu-id="dd661-114">Tipo</span><span class="sxs-lookup"><span data-stu-id="dd661-114">Type</span></span> | <span data-ttu-id="dd661-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="dd661-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd661-116">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="dd661-116">settings.wmfVersion</span></span> |<span data-ttu-id="dd661-117">Cadeia</span><span class="sxs-lookup"><span data-stu-id="dd661-117">string</span></span> |<span data-ttu-id="dd661-118">Especifica a versão de Olá do Olá Windows Management Framework que deve ser instalado na VM.</span><span class="sxs-lookup"><span data-stu-id="dd661-118">Specifies hello version of hello Windows Management Framework that should be installed on your VM.</span></span> <span data-ttu-id="dd661-119">Definir esta propriedade too'latest' instala Olá versão mais atualizada WMF.</span><span class="sxs-lookup"><span data-stu-id="dd661-119">Setting this property too'latest' installs hello most updated version of WMF.</span></span> <span data-ttu-id="dd661-120">Olá atual apenas os valores possíveis para esta propriedade são **'4.0', '5.0', ' 5.0PP' e 'mais recente'**.</span><span class="sxs-lookup"><span data-stu-id="dd661-120">hello only current possible values for this property are **'4.0', '5.0', '5.0PP', and 'latest'**.</span></span> <span data-ttu-id="dd661-121">Estes valores possíveis são tooupdates do requerente.</span><span class="sxs-lookup"><span data-stu-id="dd661-121">These possible values are subject tooupdates.</span></span> <span data-ttu-id="dd661-122">valor predefinido de Olá é 'mais recente'.</span><span class="sxs-lookup"><span data-stu-id="dd661-122">hello default value is 'latest'.</span></span> |
| <span data-ttu-id="dd661-123">Settings.Configuration.URL</span><span class="sxs-lookup"><span data-stu-id="dd661-123">settings.configuration.url</span></span> |<span data-ttu-id="dd661-124">Cadeia</span><span class="sxs-lookup"><span data-stu-id="dd661-124">string</span></span> |<span data-ttu-id="dd661-125">Especifica a localização de URL de Olá do qual toodownload ficheiro zip de configuração de DSC.</span><span class="sxs-lookup"><span data-stu-id="dd661-125">Specifies hello URL location from which toodownload your DSC configuration zip file.</span></span> <span data-ttu-id="dd661-126">Se o URL Olá fornecido necessita de um token SAS para o acesso, terá de tooset Olá protectedSettings.configurationUrlSasToken toohello o valor da propriedade do seu token SAS.</span><span class="sxs-lookup"><span data-stu-id="dd661-126">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationUrlSasToken property toohello value of your SAS token.</span></span> <span data-ttu-id="dd661-127">Esta propriedade é necessária se settings.configuration.script e/ou settings.configuration.function estiverem definidos.</span><span class="sxs-lookup"><span data-stu-id="dd661-127">This property is required if settings.configuration.script and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="dd661-128">Settings.Configuration.script</span><span class="sxs-lookup"><span data-stu-id="dd661-128">settings.configuration.script</span></span> |<span data-ttu-id="dd661-129">Cadeia</span><span class="sxs-lookup"><span data-stu-id="dd661-129">string</span></span> |<span data-ttu-id="dd661-130">Especifica o nome de ficheiro Olá de script de Olá que contém uma definição de Olá da sua configuração de DSC.</span><span class="sxs-lookup"><span data-stu-id="dd661-130">Specifies hello file name of hello script that contains hello definition of your DSC configuration.</span></span> <span data-ttu-id="dd661-131">Este script tem de estar na pasta de raiz de Olá de Olá o ficheiro zip transferido a partir do URL de Olá especificado pela propriedade de configuration.url Olá.</span><span class="sxs-lookup"><span data-stu-id="dd661-131">This script must be in hello root folder of hello zip file downloaded from hello URL specified by hello configuration.url property.</span></span> <span data-ttu-id="dd661-132">Esta propriedade é necessária se settings.configuration.url e/ou settings.configuration.script estiverem definidos.</span><span class="sxs-lookup"><span data-stu-id="dd661-132">This property is required if settings.configuration.url and/or settings.configuration.script are defined.</span></span> |
| <span data-ttu-id="dd661-133">Settings.Configuration.Function</span><span class="sxs-lookup"><span data-stu-id="dd661-133">settings.configuration.function</span></span> |<span data-ttu-id="dd661-134">Cadeia</span><span class="sxs-lookup"><span data-stu-id="dd661-134">string</span></span> |<span data-ttu-id="dd661-135">Especifica o nome de Olá da sua configuração de DSC.</span><span class="sxs-lookup"><span data-stu-id="dd661-135">Specifies hello name of your DSC configuration.</span></span> <span data-ttu-id="dd661-136">configuração de Olá com o nome tem de estar contida no script de Olá definido pelo configuration.script.</span><span class="sxs-lookup"><span data-stu-id="dd661-136">hello configuration named must be contained in hello script defined by configuration.script.</span></span> <span data-ttu-id="dd661-137">Esta propriedade é necessária se settings.configuration.url e/ou settings.configuration.function estiverem definidos.</span><span class="sxs-lookup"><span data-stu-id="dd661-137">This property is required if settings.configuration.url and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="dd661-138">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="dd661-138">settings.configurationArguments</span></span> |<span data-ttu-id="dd661-139">Coleção</span><span class="sxs-lookup"><span data-stu-id="dd661-139">Collection</span></span> |<span data-ttu-id="dd661-140">Define os parâmetros que gostaria de configuração de DSC toopass tooyour.</span><span class="sxs-lookup"><span data-stu-id="dd661-140">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="dd661-141">Esta propriedade não está encriptada.</span><span class="sxs-lookup"><span data-stu-id="dd661-141">This property is not encrypted.</span></span> |
| <span data-ttu-id="dd661-142">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="dd661-142">settings.configurationData.url</span></span> |<span data-ttu-id="dd661-143">Cadeia</span><span class="sxs-lookup"><span data-stu-id="dd661-143">string</span></span> |<span data-ttu-id="dd661-144">Especifica o URL de Olá do qual toodownload os dados de configuração (. psd1) ficheiro toouse como entrada para a sua configuração de DSC.</span><span class="sxs-lookup"><span data-stu-id="dd661-144">Specifies hello URL from which toodownload your configuration data (.psd1) file toouse as input for your DSC configuration.</span></span> <span data-ttu-id="dd661-145">Se o URL Olá fornecido necessita de um token SAS para o acesso, terá de tooset Olá protectedSettings.configurationDataUrlSasToken toohello o valor da propriedade do seu token SAS.</span><span class="sxs-lookup"><span data-stu-id="dd661-145">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationDataUrlSasToken property toohello value of your SAS token.</span></span> |
| <span data-ttu-id="dd661-146">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="dd661-146">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="dd661-147">Cadeia</span><span class="sxs-lookup"><span data-stu-id="dd661-147">string</span></span> |<span data-ttu-id="dd661-148">Ativa ou desativa a coleção de telemetria.</span><span class="sxs-lookup"><span data-stu-id="dd661-148">Enables or disables telemetry collection.</span></span> <span data-ttu-id="dd661-149">Olá apenas os valores possíveis para esta propriedade são **'Ativar', 'Disable', ', ou $null**.</span><span class="sxs-lookup"><span data-stu-id="dd661-149">hello only possible values for this property are **'Enable', 'Disable', '', or $null**.</span></span> <span data-ttu-id="dd661-150">Abandonar o fileparser esta propriedade em branco ou nulo permite telemetria.</span><span class="sxs-lookup"><span data-stu-id="dd661-150">Leaving this property blank or null enables telemetry.</span></span> <span data-ttu-id="dd661-151">é o valor predefinido de Olá ".</span><span class="sxs-lookup"><span data-stu-id="dd661-151">hello default value is ''.</span></span> [<span data-ttu-id="dd661-152">Obter mais informações</span><span class="sxs-lookup"><span data-stu-id="dd661-152">More Information</span></span>](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| <span data-ttu-id="dd661-153">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="dd661-153">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="dd661-154">Coleção</span><span class="sxs-lookup"><span data-stu-id="dd661-154">Collection</span></span> |<span data-ttu-id="dd661-155">Define as localizações alternativas a que partir do qual toodownload Olá WMF.</span><span class="sxs-lookup"><span data-stu-id="dd661-155">Defines alternate locations from which toodownload hello WMF.</span></span> [<span data-ttu-id="dd661-156">Obter mais informações</span><span class="sxs-lookup"><span data-stu-id="dd661-156">More Information</span></span>](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| <span data-ttu-id="dd661-157">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="dd661-157">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="dd661-158">Coleção</span><span class="sxs-lookup"><span data-stu-id="dd661-158">Collection</span></span> |<span data-ttu-id="dd661-159">Define os parâmetros que gostaria de configuração de DSC toopass tooyour.</span><span class="sxs-lookup"><span data-stu-id="dd661-159">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="dd661-160">Esta propriedade está encriptada.</span><span class="sxs-lookup"><span data-stu-id="dd661-160">This property is encrypted.</span></span> |
| <span data-ttu-id="dd661-161">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="dd661-161">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="dd661-162">Cadeia</span><span class="sxs-lookup"><span data-stu-id="dd661-162">string</span></span> |<span data-ttu-id="dd661-163">Especifica Olá SAS token tooaccess Olá URL definido pelo configuration.url.</span><span class="sxs-lookup"><span data-stu-id="dd661-163">Specifies hello SAS token tooaccess hello URL defined by configuration.url.</span></span> <span data-ttu-id="dd661-164">Esta propriedade está encriptada.</span><span class="sxs-lookup"><span data-stu-id="dd661-164">This property is encrypted.</span></span> |
| <span data-ttu-id="dd661-165">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="dd661-165">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="dd661-166">Cadeia</span><span class="sxs-lookup"><span data-stu-id="dd661-166">string</span></span> |<span data-ttu-id="dd661-167">Especifica Olá SAS token tooaccess Olá URL definido pelo configurationData.url.</span><span class="sxs-lookup"><span data-stu-id="dd661-167">Specifies hello SAS token tooaccess hello URL defined by configurationData.url.</span></span> <span data-ttu-id="dd661-168">Esta propriedade está encriptada.</span><span class="sxs-lookup"><span data-stu-id="dd661-168">This property is encrypted.</span></span> |

## <a name="settings-vs-protectedsettings"></a><span data-ttu-id="dd661-169">Definições vs. ProtectedSettings</span><span class="sxs-lookup"><span data-stu-id="dd661-169">Settings vs. ProtectedSettings</span></span>
<span data-ttu-id="dd661-170">Todas as definições são guardadas num ficheiro de texto de definições num Olá VM.</span><span class="sxs-lookup"><span data-stu-id="dd661-170">All settings are saved in a settings text file on hello VM.</span></span>
<span data-ttu-id="dd661-171">Propriedades em "definições" são propriedades públicas porque estes não são encriptadas no ficheiro de texto de definições de Olá.</span><span class="sxs-lookup"><span data-stu-id="dd661-171">Properties under 'settings' are public properties because they are not encrypted in hello settings text file.</span></span>
<span data-ttu-id="dd661-172">Propriedades em 'protectedSettings' são encriptadas com um certificado e não são apresentadas em texto simples neste ficheiro no Olá VM.</span><span class="sxs-lookup"><span data-stu-id="dd661-172">Properties under 'protectedSettings' are encrypted with a certificate and are not shown in plain text in this file on hello VM.</span></span>

<span data-ttu-id="dd661-173">Se a configuração de Olá necessita de credenciais, podem ser incluídos no protectedSettings:</span><span class="sxs-lookup"><span data-stu-id="dd661-173">If hello configuration needs credentials, they can be included in protectedSettings:</span></span>

```json
"protectedSettings": {
    "configurationArguments": {
        "parameterOfTypePSCredential1": {
               "userName": "UsernameValue1",
               "password": "PasswordValue1"
        }
    }
}
```

## <a name="example"></a><span data-ttu-id="dd661-174">Exemplo</span><span class="sxs-lookup"><span data-stu-id="dd661-174">Example</span></span>
<span data-ttu-id="dd661-175">Olá exemplo seguinte deriva de Olá "Introdução" secção Olá [página Descrição geral de processador de extensão de DSC](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd661-175">hello following example derives from hello "Getting Started" section of hello [DSC Extension Handler Overview page](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
<span data-ttu-id="dd661-176">Este exemplo utiliza modelos do Resource Manager, em vez de extensão de Olá toodeploy de cmdlets.</span><span class="sxs-lookup"><span data-stu-id="dd661-176">This example uses Resource Manager templates instead of cmdlets toodeploy hello extension.</span></span> <span data-ttu-id="dd661-177">Guardar a configuração de "IisInstall.ps1" Olá, colocar uma. ZIP ficheiro e ficheiro de Olá de carregamento num URL acessível.</span><span class="sxs-lookup"><span data-stu-id="dd661-177">Save hello "IisInstall.ps1" configuration, place it in a .ZIP file, and upload hello file in an accessible URL.</span></span> <span data-ttu-id="dd661-178">Este exemplo utiliza o blob storage do Azure, mas é toodownload possíveis. Ficheiros ZIP partir de qualquer localização arbitrário.</span><span class="sxs-lookup"><span data-stu-id="dd661-178">This example uses Azure blob storage, but it is possible toodownload .ZIP files from any arbitrary location.</span></span>

<span data-ttu-id="dd661-179">No modelo do Azure Resource Manager Olá, hello seguinte código dá instruções ao ficheiro correto do Olá VM toodownload Olá e executar a função de PowerShell adequada Olá:</span><span class="sxs-lookup"><span data-stu-id="dd661-179">In hello Azure Resource Manager template, hello following code instructs hello VM toodownload hello correct file and run hello appropriate PowerShell function:</span></span>

```json
"settings": {
    "configuration": {
        "url": "https://demo.blob.core.windows.net/",
        "script": "IisInstall.ps1",
        "function": "IISInstall"
    }
    } 
},
"protectedSettings": {
    "configurationUrlSasToken": "odLPL/U1p9lvcnp..."
}
```

## <a name="updating-from-hello-previous-format"></a><span data-ttu-id="dd661-180">Atualização a partir do Olá formato anterior</span><span class="sxs-lookup"><span data-stu-id="dd661-180">Updating from hello Previous Format</span></span>
<span data-ttu-id="dd661-181">Quaisquer definições no Olá anterior formato (que contém propriedades públicas do Olá ModulesUrl, ConfigurationFunction, SasToken ou propriedades) automaticamente adaptam formato atual toohello e executar de forma que funcionavam antes.</span><span class="sxs-lookup"><span data-stu-id="dd661-181">Any settings in hello previous format (containing hello public properties ModulesUrl, ConfigurationFunction, SasToken, or Properties) automatically adapt toohello current format and run just as they did before.</span></span>

<span data-ttu-id="dd661-182">Olá seguir o esquema é o esquema de definições anteriores Olá comparada como:</span><span class="sxs-lookup"><span data-stu-id="dd661-182">hello following schema is what hello previous settings schema looked like:</span></span>

```json
"settings": {
    "WMFVersion": "latest",
    "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
    "SasToken": "SAS Token if ModulesUrl points tooprivate Azure Blob Storage",
    "ConfigurationFunction": "ConfigurationScript.ps1\\ConfigurationFunction",
    "Properties":  {
        "ParameterToConfigurationFunction1":  "Value1",
        "ParameterToConfigurationFunction2":  "Value2",
        "ParameterOfTypePSCredential1": {
            "UserName": "UsernameValue1",
            "Password": "PrivateSettingsRef:Key1" 
        },
        "ParameterOfTypePSCredential2": {
            "UserName": "UsernameValue2",
            "Password": "PrivateSettingsRef:Key2"
        }
    }
},
"protectedSettings": { 
    "Items": {
        "Key1": "PasswordValue1",
        "Key2": "PasswordValue2"
    },
    "DataBlobUri": "https://UrlToConfigurationDataWithOptionalSasToken.psd1"
}
```

<span data-ttu-id="dd661-183">Eis como formato anterior Olá feita formato atual toohello:</span><span class="sxs-lookup"><span data-stu-id="dd661-183">Here's how hello previous format adapts toohello current format:</span></span>

| <span data-ttu-id="dd661-184">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="dd661-184">Property Name</span></span> | <span data-ttu-id="dd661-185">Anterior equivalente de esquema</span><span class="sxs-lookup"><span data-stu-id="dd661-185">Previous Schema Equivalent</span></span> |
| --- | --- |
| <span data-ttu-id="dd661-186">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="dd661-186">settings.wmfVersion</span></span> |<span data-ttu-id="dd661-187">definições. WMFVersion</span><span class="sxs-lookup"><span data-stu-id="dd661-187">settings.WMFVersion</span></span> |
| <span data-ttu-id="dd661-188">Settings.Configuration.URL</span><span class="sxs-lookup"><span data-stu-id="dd661-188">settings.configuration.url</span></span> |<span data-ttu-id="dd661-189">definições. ModulesUrl</span><span class="sxs-lookup"><span data-stu-id="dd661-189">settings.ModulesUrl</span></span> |
| <span data-ttu-id="dd661-190">Settings.Configuration.script</span><span class="sxs-lookup"><span data-stu-id="dd661-190">settings.configuration.script</span></span> |<span data-ttu-id="dd661-191">Primeira parte das definições. ConfigurationFunction (antes de '\\\\')</span><span class="sxs-lookup"><span data-stu-id="dd661-191">First part of settings.ConfigurationFunction (before '\\\\')</span></span> |
| <span data-ttu-id="dd661-192">Settings.Configuration.Function</span><span class="sxs-lookup"><span data-stu-id="dd661-192">settings.configuration.function</span></span> |<span data-ttu-id="dd661-193">Segunda parte das definições. ConfigurationFunction (depois de '\\\\')</span><span class="sxs-lookup"><span data-stu-id="dd661-193">Second part of settings.ConfigurationFunction (after '\\\\')</span></span> |
| <span data-ttu-id="dd661-194">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="dd661-194">settings.configurationArguments</span></span> |<span data-ttu-id="dd661-195">definições. Propriedades</span><span class="sxs-lookup"><span data-stu-id="dd661-195">settings.Properties</span></span> |
| <span data-ttu-id="dd661-196">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="dd661-196">settings.configurationData.url</span></span> |<span data-ttu-id="dd661-197">protectedSettings.DataBlobUri (sem SAS token)</span><span class="sxs-lookup"><span data-stu-id="dd661-197">protectedSettings.DataBlobUri (without SAS token)</span></span> |
| <span data-ttu-id="dd661-198">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="dd661-198">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="dd661-199">definições. Privacy.DataEnabled</span><span class="sxs-lookup"><span data-stu-id="dd661-199">settings.Privacy.DataEnabled</span></span> |
| <span data-ttu-id="dd661-200">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="dd661-200">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="dd661-201">definições. AdvancedOptions.DownloadMappings</span><span class="sxs-lookup"><span data-stu-id="dd661-201">settings.AdvancedOptions.DownloadMappings</span></span> |
| <span data-ttu-id="dd661-202">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="dd661-202">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="dd661-203">protectedSettings.Properties</span><span class="sxs-lookup"><span data-stu-id="dd661-203">protectedSettings.Properties</span></span> |
| <span data-ttu-id="dd661-204">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="dd661-204">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="dd661-205">definições. SasToken</span><span class="sxs-lookup"><span data-stu-id="dd661-205">settings.SasToken</span></span> |
| <span data-ttu-id="dd661-206">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="dd661-206">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="dd661-207">Token SAS de protectedSettings.DataBlobUri</span><span class="sxs-lookup"><span data-stu-id="dd661-207">SAS token from protectedSettings.DataBlobUri</span></span> |

## <a name="troubleshooting---error-code-1100"></a><span data-ttu-id="dd661-208">Resolução de problemas - o código de erro 1100</span><span class="sxs-lookup"><span data-stu-id="dd661-208">Troubleshooting - Error Code 1100</span></span>
<span data-ttu-id="dd661-209">Código de erro 1100 indica que existe um problema com Olá extensão toohello DSC de intervenção do utilizador.</span><span class="sxs-lookup"><span data-stu-id="dd661-209">Error Code 1100 indicates that there is a problem with hello user input toohello DSC extension.</span></span>
<span data-ttu-id="dd661-210">texto de Olá destes erros é variável e podem ser alterados.</span><span class="sxs-lookup"><span data-stu-id="dd661-210">hello text of these errors is variable and may change.</span></span>
<span data-ttu-id="dd661-211">Seguem-se alguns dos erros de Olá que poderá ter e como pode corrigi-los.</span><span class="sxs-lookup"><span data-stu-id="dd661-211">Here are some of hello errors you may run into and how you can fix them.</span></span>

### <a name="invalid-values"></a><span data-ttu-id="dd661-212">Valores inválidos</span><span class="sxs-lookup"><span data-stu-id="dd661-212">Invalid Values</span></span>
<span data-ttu-id="dd661-213">"Privacy.dataCollection é '{0}'.</span><span class="sxs-lookup"><span data-stu-id="dd661-213">"Privacy.dataCollection is '{0}'.</span></span> <span data-ttu-id="dd661-214">Olá apenas os valores possíveis são ', 'Enable' e 'Disable' ""WmfVersion é '{0}'.</span><span class="sxs-lookup"><span data-stu-id="dd661-214">hello only possible values are '', 'Enable', and 'Disable'" "WmfVersion is '{0}'.</span></span> <span data-ttu-id="dd661-215">Apenas os valores possíveis são...</span><span class="sxs-lookup"><span data-stu-id="dd661-215">Only possible values are …</span></span> <span data-ttu-id="dd661-216">e 'mais recente' "</span><span class="sxs-lookup"><span data-stu-id="dd661-216">and 'latest'"</span></span>

<span data-ttu-id="dd661-217">Problema: Um valor fornecido não é permitido.</span><span class="sxs-lookup"><span data-stu-id="dd661-217">Problem: A provided value is not allowed.</span></span>

<span data-ttu-id="dd661-218">Solução: Alteração Olá valor inválido tooa valor válido.</span><span class="sxs-lookup"><span data-stu-id="dd661-218">Solution: Change hello invalid value tooa valid value.</span></span> <span data-ttu-id="dd661-219">Consulte a tabela de Olá na seção de detalhes de Olá.</span><span class="sxs-lookup"><span data-stu-id="dd661-219">See hello table in hello Details section.</span></span>

### <a name="invalid-url"></a><span data-ttu-id="dd661-220">URL inválido</span><span class="sxs-lookup"><span data-stu-id="dd661-220">Invalid URL</span></span>
<span data-ttu-id="dd661-221">"ConfigurationData.url é '{0}'.</span><span class="sxs-lookup"><span data-stu-id="dd661-221">"ConfigurationData.url is '{0}'.</span></span> <span data-ttu-id="dd661-222">Não é um URL válido""DataBlobUri é '{0}'.</span><span class="sxs-lookup"><span data-stu-id="dd661-222">This is not a valid URL" "DataBlobUri is '{0}'.</span></span> <span data-ttu-id="dd661-223">Não é um URL válido""Configuration.url é '{0}'.</span><span class="sxs-lookup"><span data-stu-id="dd661-223">This is not a valid URL" "Configuration.url is '{0}'.</span></span> <span data-ttu-id="dd661-224">Não é um URL válido"</span><span class="sxs-lookup"><span data-stu-id="dd661-224">This is not a valid URL"</span></span>

<span data-ttu-id="dd661-225">Problema: Um fornecidos no que URL não é válido.</span><span class="sxs-lookup"><span data-stu-id="dd661-225">Problem: A provided URL is not valid.</span></span>

<span data-ttu-id="dd661-226">Solução: Verifique todos os URLs de fornecido.</span><span class="sxs-lookup"><span data-stu-id="dd661-226">Solution: Check all your provided URLs.</span></span> <span data-ttu-id="dd661-227">Certifique-se de que todos os URLs resolver toovalid localizações que pode aceder a extensão de Olá no computador remoto Olá.</span><span class="sxs-lookup"><span data-stu-id="dd661-227">Make sure all URLs resolve toovalid locations that hello extension can access on hello remote machine.</span></span>

### <a name="invalid-configurationargument-type"></a><span data-ttu-id="dd661-228">Tipo de ConfigurationArgument inválido</span><span class="sxs-lookup"><span data-stu-id="dd661-228">Invalid ConfigurationArgument Type</span></span>
<span data-ttu-id="dd661-229">"ConfigurationArguments inválidos do tipo de {0}"</span><span class="sxs-lookup"><span data-stu-id="dd661-229">"Invalid configurationArguments type {0}"</span></span>

<span data-ttu-id="dd661-230">Problema: Olá ConfigurationArguments propriedade não é possível resolver o objeto de tabela hash tooa.</span><span class="sxs-lookup"><span data-stu-id="dd661-230">Problem: hello ConfigurationArguments property cannot resolve tooa Hashtable object.</span></span> 

<span data-ttu-id="dd661-231">Solução: Tornar a sua propriedade ConfigurationArguments uma tabela hash.</span><span class="sxs-lookup"><span data-stu-id="dd661-231">Solution: Make your ConfigurationArguments property a Hashtable.</span></span> <span data-ttu-id="dd661-232">Siga o formato de Olá fornecido no exemplo de que precede Olá.</span><span class="sxs-lookup"><span data-stu-id="dd661-232">Follow hello format provided in hello preceeding example.</span></span> <span data-ttu-id="dd661-233">Tenha atenção para as aspas, vírgulas e chavetas.</span><span class="sxs-lookup"><span data-stu-id="dd661-233">Watch out for quotes, commas, and braces.</span></span>

### <a name="duplicate-configurationarguments"></a><span data-ttu-id="dd661-234">ConfigurationArguments duplicado</span><span class="sxs-lookup"><span data-stu-id="dd661-234">Duplicate ConfigurationArguments</span></span>
<span data-ttu-id="dd661-235">"Encontrada argumentos duplicados '{0}' na configurationArguments público e protegido"</span><span class="sxs-lookup"><span data-stu-id="dd661-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments"</span></span>

<span data-ttu-id="dd661-236">Problema: Olá ConfigurationArguments nas definições públicas e hello ConfigurationArguments nas definições protegidas conter propriedades com Olá mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="dd661-236">Problem: hello ConfigurationArguments in public settings and hello ConfigurationArguments in protected settings contain properties with hello same name.</span></span>

<span data-ttu-id="dd661-237">Solução: Remova uma das propriedades duplicadas Olá.</span><span class="sxs-lookup"><span data-stu-id="dd661-237">Solution: Remove one of hello duplicate properties.</span></span>

### <a name="missing-properties"></a><span data-ttu-id="dd661-238">Propriedades em falta</span><span class="sxs-lookup"><span data-stu-id="dd661-238">Missing Properties</span></span>
<span data-ttu-id="dd661-239">"Configuration.function requer que é especificado configuration.url ou configuration.module"</span><span class="sxs-lookup"><span data-stu-id="dd661-239">"Configuration.function requires that configuration.url or configuration.module is specified"</span></span>

<span data-ttu-id="dd661-240">"Configuration.url requer que configuration.script é especificado"</span><span class="sxs-lookup"><span data-stu-id="dd661-240">"Configuration.url requires that configuration.script is specified"</span></span>

<span data-ttu-id="dd661-241">"Configuration.script requer que configuration.url é especificado"</span><span class="sxs-lookup"><span data-stu-id="dd661-241">"Configuration.script requires that configuration.url is specified"</span></span>

<span data-ttu-id="dd661-242">"Configuration.url requer que configuration.function é especificado"</span><span class="sxs-lookup"><span data-stu-id="dd661-242">"Configuration.url requires that configuration.function is specified"</span></span>

<span data-ttu-id="dd661-243">"ConfigurationUrlSasToken requer que configuration.url é especificado"</span><span class="sxs-lookup"><span data-stu-id="dd661-243">"ConfigurationUrlSasToken requires that configuration.url is specified"</span></span>

<span data-ttu-id="dd661-244">"ConfigurationDataUrlSasToken requer que configurationData.url é especificado"</span><span class="sxs-lookup"><span data-stu-id="dd661-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified"</span></span>

<span data-ttu-id="dd661-245">Problema: Uma propriedade definida tem outra propriedade que está em falta.</span><span class="sxs-lookup"><span data-stu-id="dd661-245">Problem: A defined property needs another property that is missing.</span></span>

<span data-ttu-id="dd661-246">Soluções:</span><span class="sxs-lookup"><span data-stu-id="dd661-246">Solutions:</span></span> 

* <span data-ttu-id="dd661-247">Fornece propriedade em falta Olá.</span><span class="sxs-lookup"><span data-stu-id="dd661-247">Provide hello missing property.</span></span>
* <span data-ttu-id="dd661-248">Remova a propriedade de Olá que necessita de Olá de propriedade em falta.</span><span class="sxs-lookup"><span data-stu-id="dd661-248">Remove hello property that needs hello missing property.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd661-249">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="dd661-249">Next Steps</span></span>
<span data-ttu-id="dd661-250">Saiba mais sobre o DSC e conjuntos de dimensionamento de máquina virtual [utilizando a Máquina Virtual conjuntos de dimensionamento com Olá extensão de DSC do Azure](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span><span class="sxs-lookup"><span data-stu-id="dd661-250">Learn about DSC and virtual machine scale sets in [Using Virtual Machine Scale Sets with hello Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span></span>

<span data-ttu-id="dd661-251">Obter mais detalhes no [a gestão de credenciais seguras do DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd661-251">Find more details on [DSC's secure credential management](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="dd661-252">Para obter mais informações sobre o processador de extensão de DSC do Azure Olá, consulte [o processador de extensão de configuração de estado pretendido do Azure introdução toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd661-252">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="dd661-253">Para obter mais informações sobre o PowerShell DSC, [visitar o Centro de documentação do PowerShell Olá](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="dd661-253">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

