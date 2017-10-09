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
# <a name="custom-script-extension-for-windows"></a>Extensão de Script personalizado para o Windows

Olá extensão de Script personalizado transfere e executa os scripts em máquinas virtuais do Azure. Esta extensão é útil para configuração de implementação de post, instalação de software ou qualquer outra configuração / tarefas de gestão. Scripts podem ser transferidos a partir do armazenamento do Azure ou do GitHub, ou fornecidos toohello do portal do Azure em tempo de execução de extensão. Olá a extensão de Script personalizado se integra com modelos Azure Resource Manager e também pode ser executado utilizando Olá CLI do Azure, o PowerShell, o portal do Azure ou o Olá API de REST de Máquina Virtual do Azure.

Este documento fornece detalhes sobre como utilizar o toouse Olá extensão de Script personalizado Olá módulo Azure PowerShell, os modelos Azure Resource Manager e detalhes de resolução de problemas de passos em sistemas Windows.

## <a name="prerequisites"></a>Pré-requisitos

### <a name="operating-system"></a>Sistema Operativo

Olá extensão de Script personalizado para o Windows pode ser executado no Windows Server 2008 R2, 2012, 2012 R2 e 2016 versões.

### <a name="script-location"></a>Localização do script

script de Olá tem toobe armazenado no Blob storage do Azure ou qualquer outra localização acessível através de um URL válido.

### <a name="internet-connectivity"></a>Conectividade Internet

Olá extensão de Script personalizado para o Windows necessita de máquina virtual de destino que Olá é toohello ligado à internet. 

## <a name="extension-schema"></a>Esquema de extensão

Olá seguinte JSON mostra esquema Olá para Olá extensão de Script personalizado. extensão de Olá requer uma localização de script (Storage do Azure ou noutro local de URL válido) e um tooexecute de comando. Se utilizar o Storage do Azure como origem do script Olá, uma chave de conta e o nome da conta de armazenamento do Azure é necessária. Estes itens devem ser tratados como dados confidenciais e especificados na configuração de definição protegido Olá extensões. Dados de definição de extensão protegido de VM do Azure é encriptados e desencriptados apenas na máquina de virtual de destino Olá.

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

### <a name="property-values"></a>Valores de propriedade

| Nome | Valor / exemplo |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| Fabricante | Microsoft.Compute |
| tipo | extensões |
| typeHandlerVersion | 1.9 |
| fileUris (por exemplo) | https://RAW.githubusercontent.com/Microsoft/DotNet-Core-Sample-Templates/Master/DotNet-Core-Music-Windows/scripts/configure-Music-App.ps1 |
| commandToExecute (por exemplo) | PowerShell sem restrições - ExecutionPolicy - configurar-música-app.ps1 de ficheiros |
| storageAccountName (por exemplo) | examplestorageacct |
| storageAccountKey (por exemplo) | TmJK/1N3AbAZ3q / + hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg = = |

**Tenha em atenção** -estes nomes de propriedade são sensíveis a maiúsculas e minúsculas. Utilize nomes de Olá, como mostrado acima tooavoid problemas de implementação.

## <a name="template-deployment"></a>Implementação de modelos

Extensões VM do Azure podem ser implementadas com modelos Azure Resource Manager. esquema JSON Olá descrita na secção anterior Olá pode ser utilizada numa Olá de toorun de modelo Azure Resource Manager extensão de Script personalizado durante uma implementação de modelo Azure Resource Manager. Um modelo de exemplo inclui Olá extensão de Script personalizado pode ser encontrada aqui, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="powershell-deployment"></a>Implementação de PowerShell

Olá `Set-AzureRmVMCustomScriptExtension` comando pode ser utilizado tooadd Olá Script personalizado extensão tooan máquina virtual existente. Para obter mais informações, consulte [conjunto AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a>Resolver problemas e suporte

### <a name="troubleshoot"></a>Resolução de problemas

Dados sobre o estado de Olá das implementações de extensão de podem ser obtidos a partir da Olá portal do Azure e utilizando o módulo do Azure PowerShell Olá. Estado da implementação de Olá toosee das extensões para uma determinada VM, execute Olá os seguintes comandos.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Execução de extensão de saída é iniciada toofiles encontrado em Olá seguindo diretório do Olá máquina virtual de destino.
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

Olá especificar os ficheiros são transferidos para Olá seguindo o diretório do Olá máquina virtual de destino.
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
onde `<n>` é um número inteiro decimal que pode ser alterada entre execuções de extensão de Olá.  Olá `1.*` valor corresponde à atual real, Olá `typeHandlerVersion` valor da extensão de Olá.  Por exemplo, poderia ser diretório real Olá `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.  

Ao executar Olá `commandToExecute` comando, a extensão de Olá ter definirá neste diretório (por exemplo, `...\Downloads\2`) como diretório de trabalho atual Olá. Esta utilização de Olá permite dos ficheiros de Olá caminhos relativos toolocate transferidos através do Olá `fileURIs` propriedade. Consulte a tabela de Olá abaixo para obter exemplos.

Uma vez que o caminho de transferência absoluto de Olá pode variar devido ao longo do tempo, é melhor tooopt para caminhos de script/ficheiro relativo no Olá `commandToExecute` string, sempre que possível. Por exemplo:
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

Informações de caminho depois de segmento URI primeiro Olá é mantido para os ficheiros transferidos através do Olá `fileUris` lista de propriedades.  Conforme mostrado na tabela de Olá abaixo, os ficheiros transferidos estão mapeados numa estrutura de Olá do transferência subdiretórios tooreflect de Olá `fileUris` valores.  

#### <a name="examples-of-downloaded-files"></a>Exemplos de ficheiros transferidos

| URI no fileUris | Caminho relativo de localização de transferência | Localização de transferência absoluto * |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

\*Como acima, os caminhos de diretório absoluto de Olá serão alterado ao longo da duração de Olá de Olá VM, mas não uma execução única da extensão CustomScript Olá.

### <a name="support"></a>Suporte

Se precisar de mais ajuda, a qualquer altura neste artigo, pode contactar Olá especialistas do Azure no Olá [fóruns do MSDN Azure e Stack Overflow] (https://azure.microsoft.com/en-us/support/forums/). Em alternativa, pode ficheiro um incidente de suporte do Azure. Aceda toohello [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione o suporte de Get. Para obter informações sobre como utilizar o suporte do Azure, leia o artigo Olá [suporte do Microsoft Azure FAQ](https://azure.microsoft.com/en-us/support/faq/).
