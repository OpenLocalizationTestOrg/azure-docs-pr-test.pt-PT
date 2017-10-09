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
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a>Windows VMSS e configuração de estado pretendido com modelos Azure Resource Manager
Este artigo descreve o modelo do Resource Manager Olá para Olá [processador de extensão de configuração de estado pretendido](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="template-example-for-a-windows-vm"></a>Exemplo de modelo para uma VM do Windows
Olá seguinte fragmento entra Olá secção de recurso de modelo de Olá.

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

## <a name="template-example-for-windows-vmss"></a>Exemplo de modelo para VMSS do Windows
Um nó VMSS tem uma secção de "Propriedades" com o Olá "VirtualMachineProfile". o atributo "extensionProfile". DSC é adicionado em "extensões". 

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

## <a name="detailed-settings-information"></a>Informações de definições detalhadas
Olá esquema seguinte é para Olá definições parte Olá extensão de DSC do Azure num modelo Azure Resource Manager.

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

## <a name="details"></a>Detalhes
| Nome da propriedade | Tipo | Descrição |
| --- | --- | --- |
| settings.wmfVersion |Cadeia |Especifica a versão de Olá do Olá Windows Management Framework que deve ser instalado na VM. Definir esta propriedade too'latest' instala Olá versão mais atualizada WMF. Olá atual apenas os valores possíveis para esta propriedade são **'4.0', '5.0', ' 5.0PP' e 'mais recente'**. Estes valores possíveis são tooupdates do requerente. valor predefinido de Olá é 'mais recente'. |
| Settings.Configuration.URL |Cadeia |Especifica a localização de URL de Olá do qual toodownload ficheiro zip de configuração de DSC. Se o URL Olá fornecido necessita de um token SAS para o acesso, terá de tooset Olá protectedSettings.configurationUrlSasToken toohello o valor da propriedade do seu token SAS. Esta propriedade é necessária se settings.configuration.script e/ou settings.configuration.function estiverem definidos. |
| Settings.Configuration.script |Cadeia |Especifica o nome de ficheiro Olá de script de Olá que contém uma definição de Olá da sua configuração de DSC. Este script tem de estar na pasta de raiz de Olá de Olá o ficheiro zip transferido a partir do URL de Olá especificado pela propriedade de configuration.url Olá. Esta propriedade é necessária se settings.configuration.url e/ou settings.configuration.script estiverem definidos. |
| Settings.Configuration.Function |Cadeia |Especifica o nome de Olá da sua configuração de DSC. configuração de Olá com o nome tem de estar contida no script de Olá definido pelo configuration.script. Esta propriedade é necessária se settings.configuration.url e/ou settings.configuration.function estiverem definidos. |
| settings.configurationArguments |Coleção |Define os parâmetros que gostaria de configuração de DSC toopass tooyour. Esta propriedade não está encriptada. |
| settings.configurationData.url |Cadeia |Especifica o URL de Olá do qual toodownload os dados de configuração (. psd1) ficheiro toouse como entrada para a sua configuração de DSC. Se o URL Olá fornecido necessita de um token SAS para o acesso, terá de tooset Olá protectedSettings.configurationDataUrlSasToken toohello o valor da propriedade do seu token SAS. |
| settings.privacy.dataEnabled |Cadeia |Ativa ou desativa a coleção de telemetria. Olá apenas os valores possíveis para esta propriedade são **'Ativar', 'Disable', ', ou $null**. Abandonar o fileparser esta propriedade em branco ou nulo permite telemetria. é o valor predefinido de Olá ". [Obter mais informações](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| settings.advancedOptions.downloadMappings |Coleção |Define as localizações alternativas a que partir do qual toodownload Olá WMF. [Obter mais informações](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| protectedSettings.configurationArguments |Coleção |Define os parâmetros que gostaria de configuração de DSC toopass tooyour. Esta propriedade está encriptada. |
| protectedSettings.configurationUrlSasToken |Cadeia |Especifica Olá SAS token tooaccess Olá URL definido pelo configuration.url. Esta propriedade está encriptada. |
| protectedSettings.configurationDataUrlSasToken |Cadeia |Especifica Olá SAS token tooaccess Olá URL definido pelo configurationData.url. Esta propriedade está encriptada. |

## <a name="settings-vs-protectedsettings"></a>Definições vs. ProtectedSettings
Todas as definições são guardadas num ficheiro de texto de definições num Olá VM.
Propriedades em "definições" são propriedades públicas porque estes não são encriptadas no ficheiro de texto de definições de Olá.
Propriedades em 'protectedSettings' são encriptadas com um certificado e não são apresentadas em texto simples neste ficheiro no Olá VM.

Se a configuração de Olá necessita de credenciais, podem ser incluídos no protectedSettings:

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

## <a name="example"></a>Exemplo
Olá exemplo seguinte deriva de Olá "Introdução" secção Olá [página Descrição geral de processador de extensão de DSC](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
Este exemplo utiliza modelos do Resource Manager, em vez de extensão de Olá toodeploy de cmdlets. Guardar a configuração de "IisInstall.ps1" Olá, colocar uma. ZIP ficheiro e ficheiro de Olá de carregamento num URL acessível. Este exemplo utiliza o blob storage do Azure, mas é toodownload possíveis. Ficheiros ZIP partir de qualquer localização arbitrário.

No modelo do Azure Resource Manager Olá, hello seguinte código dá instruções ao ficheiro correto do Olá VM toodownload Olá e executar a função de PowerShell adequada Olá:

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

## <a name="updating-from-hello-previous-format"></a>Atualização a partir do Olá formato anterior
Quaisquer definições no Olá anterior formato (que contém propriedades públicas do Olá ModulesUrl, ConfigurationFunction, SasToken ou propriedades) automaticamente adaptam formato atual toohello e executar de forma que funcionavam antes.

Olá seguir o esquema é o esquema de definições anteriores Olá comparada como:

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

Eis como formato anterior Olá feita formato atual toohello:

| Nome da propriedade | Anterior equivalente de esquema |
| --- | --- |
| settings.wmfVersion |definições. WMFVersion |
| Settings.Configuration.URL |definições. ModulesUrl |
| Settings.Configuration.script |Primeira parte das definições. ConfigurationFunction (antes de '\\\\') |
| Settings.Configuration.Function |Segunda parte das definições. ConfigurationFunction (depois de '\\\\') |
| settings.configurationArguments |definições. Propriedades |
| settings.configurationData.url |protectedSettings.DataBlobUri (sem SAS token) |
| settings.privacy.dataEnabled |definições. Privacy.DataEnabled |
| settings.advancedOptions.downloadMappings |definições. AdvancedOptions.DownloadMappings |
| protectedSettings.configurationArguments |protectedSettings.Properties |
| protectedSettings.configurationUrlSasToken |definições. SasToken |
| protectedSettings.configurationDataUrlSasToken |Token SAS de protectedSettings.DataBlobUri |

## <a name="troubleshooting---error-code-1100"></a>Resolução de problemas - o código de erro 1100
Código de erro 1100 indica que existe um problema com Olá extensão toohello DSC de intervenção do utilizador.
texto de Olá destes erros é variável e podem ser alterados.
Seguem-se alguns dos erros de Olá que poderá ter e como pode corrigi-los.

### <a name="invalid-values"></a>Valores inválidos
"Privacy.dataCollection é '{0}'. Olá apenas os valores possíveis são ', 'Enable' e 'Disable' ""WmfVersion é '{0}'. Apenas os valores possíveis são... e 'mais recente' "

Problema: Um valor fornecido não é permitido.

Solução: Alteração Olá valor inválido tooa valor válido. Consulte a tabela de Olá na seção de detalhes de Olá.

### <a name="invalid-url"></a>URL inválido
"ConfigurationData.url é '{0}'. Não é um URL válido""DataBlobUri é '{0}'. Não é um URL válido""Configuration.url é '{0}'. Não é um URL válido"

Problema: Um fornecidos no que URL não é válido.

Solução: Verifique todos os URLs de fornecido. Certifique-se de que todos os URLs resolver toovalid localizações que pode aceder a extensão de Olá no computador remoto Olá.

### <a name="invalid-configurationargument-type"></a>Tipo de ConfigurationArgument inválido
"ConfigurationArguments inválidos do tipo de {0}"

Problema: Olá ConfigurationArguments propriedade não é possível resolver o objeto de tabela hash tooa. 

Solução: Tornar a sua propriedade ConfigurationArguments uma tabela hash. Siga o formato de Olá fornecido no exemplo de que precede Olá. Tenha atenção para as aspas, vírgulas e chavetas.

### <a name="duplicate-configurationarguments"></a>ConfigurationArguments duplicado
"Encontrada argumentos duplicados '{0}' na configurationArguments público e protegido"

Problema: Olá ConfigurationArguments nas definições públicas e hello ConfigurationArguments nas definições protegidas conter propriedades com Olá mesmo nome.

Solução: Remova uma das propriedades duplicadas Olá.

### <a name="missing-properties"></a>Propriedades em falta
"Configuration.function requer que é especificado configuration.url ou configuration.module"

"Configuration.url requer que configuration.script é especificado"

"Configuration.script requer que configuration.url é especificado"

"Configuration.url requer que configuration.function é especificado"

"ConfigurationUrlSasToken requer que configuration.url é especificado"

"ConfigurationDataUrlSasToken requer que configurationData.url é especificado"

Problema: Uma propriedade definida tem outra propriedade que está em falta.

Soluções: 

* Fornece propriedade em falta Olá.
* Remova a propriedade de Olá que necessita de Olá de propriedade em falta.

## <a name="next-steps"></a>Passos Seguintes
Saiba mais sobre o DSC e conjuntos de dimensionamento de máquina virtual [utilizando a Máquina Virtual conjuntos de dimensionamento com Olá extensão de DSC do Azure](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)

Obter mais detalhes no [a gestão de credenciais seguras do DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Para obter mais informações sobre o processador de extensão de DSC do Azure Olá, consulte [o processador de extensão de configuração de estado pretendido do Azure introdução toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Para obter mais informações sobre o PowerShell DSC, [visitar o Centro de documentação do PowerShell Olá](https://msdn.microsoft.com/powershell/dsc/overview). 

