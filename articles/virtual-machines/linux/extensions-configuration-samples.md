---
title: "configuração de aaaSample para extensões de VM com Linux | Microsoft Docs"
description: "Configuração de exemplo para a criação de modelos com extensões para VMs com Linux"
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4f50e6b2-fce0-41ef-823d-df433957601a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/13/2016
ms.author: kundanap
ms.openlocfilehash: bc19b8d7d6fdb1783be99ec7fdd5cde5e1f8ca80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="linux-vm-extension-configuration-samples"></a>Exemplos de configuração das extensões de VM com Linux
> [!div class="op_single_selector"]
> * [PowerShell – modelo](../windows/extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> * [CLI - modelo](../windows/extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

Este artigo fornece uma configuração de exemplo para a configuração de extensões de VM do Azure para VMs com Linux.

toolearn mais informações sobre estas extensões clique aqui: [descrição geral de extensões de VM do Azure.](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

toolearn mais informações sobre a criação de modelos de extensão clique aqui: [criação de modelos de extensão.](../windows/extensions-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

Este artigo apresenta uma lista de valores de configuração esperado para algumas das Olá extensões de Linux.

## <a name="sample-template-snippet-for-vm-extensions"></a>Fragmento de modelo de exemplo para extensões de VM.
fragmento de modelo de Olá para implementar a procura de extensões seguinte forma:

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "autoUpgradeMinorVersion":true,
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

## <a name="sample-template-snippet-for-vm-extensions-with-vm-scale-sets"></a>Fragmento de modelo de exemplo para extensões de VM com conjuntos de dimensionamento de VM.
          {
           "type":"Microsoft.Compute/virtualMachineScaleSets",
          ....
                 "extensionProfile":{
                 "extensions":[
                   {
                     "name":"extension Name",
                     "properties":{
                       "publisher":"Publisher Namespace",
                       "type":"extension Name",
                       "typeHandlerVersion":"extension version",
                       "autoUpgradeMinorVersion":true,
                       "settings":{
                       // Extension specific configuration goes in here.
                       }
                     }
                    }
                  }
                }

Antes de implementar a extensão de Olá. Verifique a versão mais recente da extensão Olá e substituir typeHandlerVersion"Olá" com a versão atual mais recente de Olá.

Resto do artigo Olá fornece configurações de exemplo para extensões de VM do Linux.

### <a name="cloudlink-securevm-agent"></a>CloudLink SecureVM agente
          {
            "publisher": "CloudLinkEMC.SecureVM",
            "type": "CloudLinkSecureVMLinuxAgent",
            "typeHandlerVersion": "4.0",
            "settings": {
              "CloudLinkCenter" : "specify valid IP/FQDN tooCloudLinkCenter"
            }
          }

### <a name="customscript-extension-for-linux"></a>Extensão CustomScript para Linux.
    {
        "publisher": " Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "http: //Yourstorageaccount.blob.core.windows.net/customscriptfiles/start.ps1"
            ],
            "commandToExecute": "powershell.exe-ExecutionPolicyUnrestricted-Filestart.ps1"
        }
    }


### <a name="datadog-agent"></a>Agente de Datadog
        {
          "publisher": "Datadog.Agent",
          "type": "DatadogLinuxAgent",
          "typeHandlerVersion": "0.4",
          "settings": {
            "api_key" : "API Key from https://app.datadoghq.com/account/settings#api"
          }
        }

### <a name="chef-agent"></a>Agente de chef
        {
          "publisher": "Chef.Bootstrap.WindowsAzure",
          "type": "CentosChefClient|LinuxChefClient",
          "typeHandlerVersion": "1210.12",
          "settings": {
            "validation_key" : " Validation key",
            "client_rb" : "client_rb file",
            "runlist" : "Optional runlist"
          }
        }

### <a name="vm-access-extension-password-reset"></a>Extensão de acesso VM (reposição de palavra-passe)
Para o esquema atualizada Consulte toohello [VMAccessForLinux documentação](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess)

        {
          "publisher": "Microsoft.OSTCExtensions",
          "type": "VMAccessForLinux",
          "typeHandlerVersion": "1.2",
          "protectedSettings": {
            "username": "(required, string) hello name of hello user",
            "password": "(optional, string) hello password of hello user",
            "reset_ssh": "(optional, boolean) whether or not reset hello ssh",
            "ssh_key": "(optional, string) hello public key of hello user, base64 encoded pem",
            "remove_user": "(optional, string) hello user name tooremove"
          }
        }

### <a name="os-patching"></a>Aplicação de patches de SO
Para o esquema atualizada Consulte toohello [OSPatching documentação](https://github.com/Azure/azure-linux-extensions/tree/master/OSPatching)

        {
        "publisher": "Microsoft.OSTCExtensions",
        "type": "OSPatchingForLinux",
        "typeHandlerVersion": "2.9",
        "Settings": {
          "disabled": false,
          "stop": false,
          "rebootAfterPatch": "RebootIfNeed|Required|NotRequired|Auto",
          "category": "Important|ImportantAndRecommended",
          "installDuration": "<hr:min>",
          "oneoff": false,
          "intervalOfWeeks": "<number>",
          "dayOfWeek": "Sunday|Monday|Tuesday|Wednesday|Thursday|Friday|Saturday|Everyday",
          "startTime": "<hr:min>",
          "vmStatusTest": {
              "local": false,
              "idleTestScript": "<path_to_idletestscript>",
              "healthyTestScript": "<path_to_healthytestscript>"
          }
        }
        }

### <a name="docker-extension"></a>Extensão de docker
Para o esquema atualizada Consulte toohello [documentação da extensão de Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md#1-configuration-schema)

        {
          "publisher": "Microsoft.Azure.Extensions ",
          "type": "DockerExtension ",
          "typeHandlerVersion": "1.0",
          "Settings": {
            "docker":{
                "port": "2376",
                "options": ["-D", "--dns=8.8.8.8"]
            },
            "compose": {
                "cache" : {
                    "image" : "memcached",
                    "ports" : ["11211:11211"]
                },
                "blog": {
                    "image": "ghost",
                    "ports": ["80:2368"]
                }
            }
            }
        }

        ### Linux Diagnostics Extension
        {
        "storageAccountName": "storage account tooreceive data",
        "storageAccountKey": "key of hello account",
        "perfCfg": [
        {
            "query": "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
            "table": "LinuxMemory"
        }
        ],
        "fileCfg": [
        {
            "file": "/var/log/mysql.err",
            "table": "mysqlerr"
        }
        ]
        }

Nos exemplos de Olá acima, substitua o número de versão Olá número da versão mais recente Olá.

Segue-se um modelo VM completo para criar uma VM com Linux com uma extensão:

[Extensão de Script personalizado numa VM com Linux](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

