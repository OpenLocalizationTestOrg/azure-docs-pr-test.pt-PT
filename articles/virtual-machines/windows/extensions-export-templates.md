---
title: "os grupos de recursos do Azure que contêm as extensões de VM de aaaExporting | Microsoft Docs"
description: "Exporte os modelos do Resource Manager, que incluem as extensões de máquina virtual."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: cdbc2030988a19fe68429e8733dc60536c264abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a>Exportar os grupos de recursos que contêm as extensões de VM

Grupos de recursos do Azure podem ser exportados para um novo modelo do Resource Manager que pode, em seguida, voltar a implementar. Olá processo de exportação interpreta recursos existentes e cria um modelo do Resource Manager que quando implementado resulta num grupo de recursos semelhantes. Quando utilizar a opção de exportação de grupo de recursos de Olá em relação a um grupo de recursos que contém as extensões de Máquina Virtual, vários toobe de necessidade de itens considerada como compatibilidade de extensão e protegido definições.

Suportado de detalhes deste documento como funciona o processo de exportação do grupo de recursos de Olá sobre extensões de máquina virtual, incluindo uma lista de extensões e protegida de detalhes sobre o processamento de dados.

## <a name="supported-virtual-machine-extensions"></a>Extensões de Máquina Virtual suportadas

Estão disponíveis várias extensões de Máquina Virtual. Nem todas as extensões podem ser exportadas para um modelo do Resource Manager utilizando a funcionalidade de "Scripts de automatização" Olá. Se não for suportada uma extensão da máquina virtual, é necessário toobe manualmente colocado no modelo exportado Olá.

Olá seguintes extensões podem ser exportadas com funcionalidade de script de automatização Olá.

| Extensão ||||
|---|---|---|---|
| Cópia de segurança Acronis | Agente do Datadog Windows | SO de aplicação de patches para Linux | Linux de instantâneos VM
| Cópia de segurança Acronis Linux | Extensão de docker | Agente de puppet |
| Informações de BG | Extensão DSC | Informações do site 24x7 Apm |
| BMC CTM agente Linux | Dynatrace Linux | Servidor do site 24x7 Linux |
| BMC CTM agente Windows | Dynatrace Windows | Servidor do site 24x7 Windows |
| Cliente chef | HPE segurança aplicação Defender | DSA Micro tendência |
| Script personalizado | Antimalware de IaaS | Tendência Micro DSA Linux |
| Extensão de Script Personalizado | Diagnóstico do IaaS | Acesso VM para Linux |
| Script personalizado para Linux | Cliente de Chef do Linux | Acesso VM para Linux |
| Agente do Linux Datadog | Diagnóstico do Linux | Instantâneo VM |

## <a name="export-hello-resource-group"></a>Exportar Olá grupo de recursos

tooexport um grupo de recursos a um modelo reutilizável, Olá concluir os seguintes passos:

1. A iniciar sessão toohello portal do Azure
2. No Hub Menu Olá, clique em grupos de recursos
3. Selecione o grupo de recursos do destino de Olá da lista de Olá
4. No painel do grupo de recursos de Olá, clique em scripts de automatização

![Exportação de modelo](./media/extensions-export-templates/template-export.png)

Olá script do Azure Resource Manager automatizações produz um modelo do Resource Manager, um ficheiro de parâmetros e vários scripts de implementação de exemplo, tais como o PowerShell e da CLI do Azure. Neste momento, modelo exportado Olá pode ser transferido com o botão Transferir Olá, adicionado como uma nova biblioteca do modelo de toohello do modelo ou implementada novamente com Olá botão implementar.

## <a name="configure-protected-settings"></a>Configurar as definições de protegido

Várias extensões de máquina virtual do Azure incluem uma configuração de definições protegido, encripta os dados confidenciais, tais como as credenciais e cadeias de configuração. Definições protegidas não são exportadas com script de automatização Olá. Se precisam de definições necessárias, protegidas toobe voltar no Olá exportados transformada em modelo.

### <a name="step-1---remove-template-parameter"></a>Passo 1 - Remove parâmetro de modelo

Quando Olá que grupo de recursos é exportado, um parâmetro único modelo é criado tooprovide toohello um valor exportado definições protegidas. Este parâmetro pode ser removido. parâmetro de Olá tooremove, examine a lista de parâmetros de Olá e eliminar parâmetro Olá de exemplo JSON toothis semelhante.

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a>Passo 2 - Get protegidos propriedades das definições

Uma vez que cada definição protegidos tem um conjunto de propriedades necessárias, uma lista destas propriedades necessário toobe recolhido. Cada um dos parâmetros de configuração de definições protegido de Olá pode ser encontrado na Olá [esquema de Gestor de recursos do Azure no GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json). Este esquema inclui apenas os conjuntos de parâmetros de Olá para extensões de Olá listadas na secção Descrição geral de Olá deste documento. 

De dentro do repositório de esquema Olá, procure extensão Olá assim o desejar, para este exemplo `IaaSDiagnostics`. Uma vez Olá extensões `protectedSettings` objeto foi localizado, tome nota de cada um dos parâmetros. No exemplo de Olá de Olá `IaasDiagnostic` extensão, Olá requer os parâmetros são `storageAccountName`, `storageAccountKey`, e `storageAccountEndPoint`.

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-hello-protected-configuration"></a>Passo 3 - recriar a configuração de Olá protegido

No modelo exportado de Olá, procure `protectedSettings` e substitua Olá exportado protegido definir o objeto com um novo, o que inclui os parâmetros de extensão de Olá necessário e um valor para cada um deles.

No exemplo de Olá de Olá `IaasDiagnostic` extensão, nova configuração de definição protegido Olá teria aspeto Olá seguinte exemplo:

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

recurso de extensão final Olá procura toohello semelhante seguinte o exemplo de JSON:

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

Se utilizar valores de propriedade de tooprovide de parâmetros de modelo, estes têm toobe criado. Quando criar os parâmetros do modelo para definir valores de protegidas, certifique-se de que toouse Olá `SecureString` parâmetro de tipo para que os valores confidenciais são protegidos. Para obter mais informações sobre como utilizar parâmetros, consulte [modelos Authoring Azure Resource Manager](../../resource-group-authoring-templates.md).

No exemplo de Olá de Olá `IaasDiagnostic` extensão, seria possível criar Olá seguir os parâmetros na secção de parâmetros de Olá de modelo do Resource Manager Olá.

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

Neste momento, o modelo de Olá pode ser implementado com qualquer método de implementação do modelo.
