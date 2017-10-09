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
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a><span data-ttu-id="f3001-103">Exportar os grupos de recursos que contêm as extensões de VM</span><span class="sxs-lookup"><span data-stu-id="f3001-103">Exporting Resource Groups that contain VM extensions</span></span>

<span data-ttu-id="f3001-104">Grupos de recursos do Azure podem ser exportados para um novo modelo do Resource Manager que pode, em seguida, voltar a implementar.</span><span class="sxs-lookup"><span data-stu-id="f3001-104">Azure Resource Groups can be exported into a new Resource Manager template that can then be redeployed.</span></span> <span data-ttu-id="f3001-105">Olá processo de exportação interpreta recursos existentes e cria um modelo do Resource Manager que quando implementado resulta num grupo de recursos semelhantes.</span><span class="sxs-lookup"><span data-stu-id="f3001-105">hello export process interprets existing resources, and creates a Resource Manager template that when deployed results in a similar Resource Group.</span></span> <span data-ttu-id="f3001-106">Quando utilizar a opção de exportação de grupo de recursos de Olá em relação a um grupo de recursos que contém as extensões de Máquina Virtual, vários toobe de necessidade de itens considerada como compatibilidade de extensão e protegido definições.</span><span class="sxs-lookup"><span data-stu-id="f3001-106">When using hello Resource Group export option against a Resource Group containing Virtual Machine extensions, several items need toobe considered such as extension compatibility and protected settings.</span></span>

<span data-ttu-id="f3001-107">Suportado de detalhes deste documento como funciona o processo de exportação do grupo de recursos de Olá sobre extensões de máquina virtual, incluindo uma lista de extensões e protegida de detalhes sobre o processamento de dados.</span><span class="sxs-lookup"><span data-stu-id="f3001-107">This document details how hello Resource Group export process works regarding virtual machine extensions, including a list of supported extensions, and details on handling secured data.</span></span>

## <a name="supported-virtual-machine-extensions"></a><span data-ttu-id="f3001-108">Extensões de Máquina Virtual suportadas</span><span class="sxs-lookup"><span data-stu-id="f3001-108">Supported Virtual Machine Extensions</span></span>

<span data-ttu-id="f3001-109">Estão disponíveis várias extensões de Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="f3001-109">Many Virtual Machine extensions are available.</span></span> <span data-ttu-id="f3001-110">Nem todas as extensões podem ser exportadas para um modelo do Resource Manager utilizando a funcionalidade de "Scripts de automatização" Olá.</span><span class="sxs-lookup"><span data-stu-id="f3001-110">Not all extensions can be exported into a Resource Manager template using hello “Automation Script” feature.</span></span> <span data-ttu-id="f3001-111">Se não for suportada uma extensão da máquina virtual, é necessário toobe manualmente colocado no modelo exportado Olá.</span><span class="sxs-lookup"><span data-stu-id="f3001-111">If a virtual machine extension is not supported, it needs toobe manually placed back into hello exported template.</span></span>

<span data-ttu-id="f3001-112">Olá seguintes extensões podem ser exportadas com funcionalidade de script de automatização Olá.</span><span class="sxs-lookup"><span data-stu-id="f3001-112">hello following extensions can be exported with hello automation script feature.</span></span>

| <span data-ttu-id="f3001-113">Extensão</span><span class="sxs-lookup"><span data-stu-id="f3001-113">Extension</span></span> ||||
|---|---|---|---|
| <span data-ttu-id="f3001-114">Cópia de segurança Acronis</span><span class="sxs-lookup"><span data-stu-id="f3001-114">Acronis Backup</span></span> | <span data-ttu-id="f3001-115">Agente do Datadog Windows</span><span class="sxs-lookup"><span data-stu-id="f3001-115">Datadog Windows Agent</span></span> | <span data-ttu-id="f3001-116">SO de aplicação de patches para Linux</span><span class="sxs-lookup"><span data-stu-id="f3001-116">OS Patching For Linux</span></span> | <span data-ttu-id="f3001-117">Linux de instantâneos VM</span><span class="sxs-lookup"><span data-stu-id="f3001-117">VM Snapshot Linux</span></span>
| <span data-ttu-id="f3001-118">Cópia de segurança Acronis Linux</span><span class="sxs-lookup"><span data-stu-id="f3001-118">Acronis Backup Linux</span></span> | <span data-ttu-id="f3001-119">Extensão de docker</span><span class="sxs-lookup"><span data-stu-id="f3001-119">Docker Extension</span></span> | <span data-ttu-id="f3001-120">Agente de puppet</span><span class="sxs-lookup"><span data-stu-id="f3001-120">Puppet Agent</span></span> |
| <span data-ttu-id="f3001-121">Informações de BG</span><span class="sxs-lookup"><span data-stu-id="f3001-121">Bg Info</span></span> | <span data-ttu-id="f3001-122">Extensão DSC</span><span class="sxs-lookup"><span data-stu-id="f3001-122">DSC Extension</span></span> | <span data-ttu-id="f3001-123">Informações do site 24x7 Apm</span><span class="sxs-lookup"><span data-stu-id="f3001-123">Site 24x7 Apm Insight</span></span> |
| <span data-ttu-id="f3001-124">BMC CTM agente Linux</span><span class="sxs-lookup"><span data-stu-id="f3001-124">BMC CTM Agent Linux</span></span> | <span data-ttu-id="f3001-125">Dynatrace Linux</span><span class="sxs-lookup"><span data-stu-id="f3001-125">Dynatrace Linux</span></span> | <span data-ttu-id="f3001-126">Servidor do site 24x7 Linux</span><span class="sxs-lookup"><span data-stu-id="f3001-126">Site 24x7 Linux Server</span></span> |
| <span data-ttu-id="f3001-127">BMC CTM agente Windows</span><span class="sxs-lookup"><span data-stu-id="f3001-127">BMC CTM Agent Windows</span></span> | <span data-ttu-id="f3001-128">Dynatrace Windows</span><span class="sxs-lookup"><span data-stu-id="f3001-128">Dynatrace Windows</span></span> | <span data-ttu-id="f3001-129">Servidor do site 24x7 Windows</span><span class="sxs-lookup"><span data-stu-id="f3001-129">Site 24x7 Windows Server</span></span> |
| <span data-ttu-id="f3001-130">Cliente chef</span><span class="sxs-lookup"><span data-stu-id="f3001-130">Chef Client</span></span> | <span data-ttu-id="f3001-131">HPE segurança aplicação Defender</span><span class="sxs-lookup"><span data-stu-id="f3001-131">HPE Security Application Defender</span></span> | <span data-ttu-id="f3001-132">DSA Micro tendência</span><span class="sxs-lookup"><span data-stu-id="f3001-132">Trend Micro DSA</span></span> |
| <span data-ttu-id="f3001-133">Script personalizado</span><span class="sxs-lookup"><span data-stu-id="f3001-133">Custom Script</span></span> | <span data-ttu-id="f3001-134">Antimalware de IaaS</span><span class="sxs-lookup"><span data-stu-id="f3001-134">IaaS Antimalware</span></span> | <span data-ttu-id="f3001-135">Tendência Micro DSA Linux</span><span class="sxs-lookup"><span data-stu-id="f3001-135">Trend Micro DSA Linux</span></span> |
| <span data-ttu-id="f3001-136">Extensão de Script Personalizado</span><span class="sxs-lookup"><span data-stu-id="f3001-136">Custom Script Extension</span></span> | <span data-ttu-id="f3001-137">Diagnóstico do IaaS</span><span class="sxs-lookup"><span data-stu-id="f3001-137">IaaS Diagnostics</span></span> | <span data-ttu-id="f3001-138">Acesso VM para Linux</span><span class="sxs-lookup"><span data-stu-id="f3001-138">VM Access For Linux</span></span> |
| <span data-ttu-id="f3001-139">Script personalizado para Linux</span><span class="sxs-lookup"><span data-stu-id="f3001-139">Custom Script for Linux</span></span> | <span data-ttu-id="f3001-140">Cliente de Chef do Linux</span><span class="sxs-lookup"><span data-stu-id="f3001-140">Linux Chef Client</span></span> | <span data-ttu-id="f3001-141">Acesso VM para Linux</span><span class="sxs-lookup"><span data-stu-id="f3001-141">VM Access For Linux</span></span> |
| <span data-ttu-id="f3001-142">Agente do Linux Datadog</span><span class="sxs-lookup"><span data-stu-id="f3001-142">Datadog Linux Agent</span></span> | <span data-ttu-id="f3001-143">Diagnóstico do Linux</span><span class="sxs-lookup"><span data-stu-id="f3001-143">Linux Diagnostic</span></span> | <span data-ttu-id="f3001-144">Instantâneo VM</span><span class="sxs-lookup"><span data-stu-id="f3001-144">VM Snapshot</span></span> |

## <a name="export-hello-resource-group"></a><span data-ttu-id="f3001-145">Exportar Olá grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f3001-145">Export hello Resource Group</span></span>

<span data-ttu-id="f3001-146">tooexport um grupo de recursos a um modelo reutilizável, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f3001-146">tooexport a Resource Group into a reusable template, complete hello following steps:</span></span>

1. <span data-ttu-id="f3001-147">A iniciar sessão toohello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f3001-147">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="f3001-148">No Hub Menu Olá, clique em grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="f3001-148">On hello Hub Menu, click Resource Groups</span></span>
3. <span data-ttu-id="f3001-149">Selecione o grupo de recursos do destino de Olá da lista de Olá</span><span class="sxs-lookup"><span data-stu-id="f3001-149">Select hello target resource group from hello list</span></span>
4. <span data-ttu-id="f3001-150">No painel do grupo de recursos de Olá, clique em scripts de automatização</span><span class="sxs-lookup"><span data-stu-id="f3001-150">In hello Resource Group blade, click Automation Script</span></span>

![Exportação de modelo](./media/extensions-export-templates/template-export.png)

<span data-ttu-id="f3001-152">Olá script do Azure Resource Manager automatizações produz um modelo do Resource Manager, um ficheiro de parâmetros e vários scripts de implementação de exemplo, tais como o PowerShell e da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3001-152">hello Azure Resource Manager automations script produces a Resource Manager template, a parameters file, and several sample deployment scripts such as PowerShell and Azure CLI.</span></span> <span data-ttu-id="f3001-153">Neste momento, modelo exportado Olá pode ser transferido com o botão Transferir Olá, adicionado como uma nova biblioteca do modelo de toohello do modelo ou implementada novamente com Olá botão implementar.</span><span class="sxs-lookup"><span data-stu-id="f3001-153">At this point, hello exported template can be downloaded using hello download button, added as a new template toohello template library, or redeployed using hello deploy button.</span></span>

## <a name="configure-protected-settings"></a><span data-ttu-id="f3001-154">Configurar as definições de protegido</span><span class="sxs-lookup"><span data-stu-id="f3001-154">Configure protected settings</span></span>

<span data-ttu-id="f3001-155">Várias extensões de máquina virtual do Azure incluem uma configuração de definições protegido, encripta os dados confidenciais, tais como as credenciais e cadeias de configuração.</span><span class="sxs-lookup"><span data-stu-id="f3001-155">Many Azure virtual machine extensions include a protected settings configuration, that encrypts sensitive data such as credentials and configuration strings.</span></span> <span data-ttu-id="f3001-156">Definições protegidas não são exportadas com script de automatização Olá.</span><span class="sxs-lookup"><span data-stu-id="f3001-156">Protected settings are not exported with hello automation script.</span></span> <span data-ttu-id="f3001-157">Se precisam de definições necessárias, protegidas toobe voltar no Olá exportados transformada em modelo.</span><span class="sxs-lookup"><span data-stu-id="f3001-157">If necessary, protected settings need toobe reinserted into hello exported templated.</span></span>

### <a name="step-1---remove-template-parameter"></a><span data-ttu-id="f3001-158">Passo 1 - Remove parâmetro de modelo</span><span class="sxs-lookup"><span data-stu-id="f3001-158">Step 1 - Remove template parameter</span></span>

<span data-ttu-id="f3001-159">Quando Olá que grupo de recursos é exportado, um parâmetro único modelo é criado tooprovide toohello um valor exportado definições protegidas.</span><span class="sxs-lookup"><span data-stu-id="f3001-159">When hello Resource Group is exported, a single template parameter is created tooprovide a value toohello exported protected settings.</span></span> <span data-ttu-id="f3001-160">Este parâmetro pode ser removido.</span><span class="sxs-lookup"><span data-stu-id="f3001-160">This parameter can be removed.</span></span> <span data-ttu-id="f3001-161">parâmetro de Olá tooremove, examine a lista de parâmetros de Olá e eliminar parâmetro Olá de exemplo JSON toothis semelhante.</span><span class="sxs-lookup"><span data-stu-id="f3001-161">tooremove hello parameter, look through hello parameter list and delete hello parameter that looks similar toothis JSON example.</span></span>

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a><span data-ttu-id="f3001-162">Passo 2 - Get protegidos propriedades das definições</span><span class="sxs-lookup"><span data-stu-id="f3001-162">Step 2 - Get protected settings properties</span></span>

<span data-ttu-id="f3001-163">Uma vez que cada definição protegidos tem um conjunto de propriedades necessárias, uma lista destas propriedades necessário toobe recolhido.</span><span class="sxs-lookup"><span data-stu-id="f3001-163">Because each protected setting has a set of required properties, a list of these properties need toobe gathered.</span></span> <span data-ttu-id="f3001-164">Cada um dos parâmetros de configuração de definições protegido de Olá pode ser encontrado na Olá [esquema de Gestor de recursos do Azure no GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span><span class="sxs-lookup"><span data-stu-id="f3001-164">Each parameter of hello protected settings configuration can be found in hello [Azure Resource Manager schema on GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span></span> <span data-ttu-id="f3001-165">Este esquema inclui apenas os conjuntos de parâmetros de Olá para extensões de Olá listadas na secção Descrição geral de Olá deste documento.</span><span class="sxs-lookup"><span data-stu-id="f3001-165">This schema only includes hello parameter sets for hello extensions listed in hello overview section of this document.</span></span> 

<span data-ttu-id="f3001-166">De dentro do repositório de esquema Olá, procure extensão Olá assim o desejar, para este exemplo `IaaSDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="f3001-166">From within hello schema repository, search for hello desired extension, for this example `IaaSDiagnostics`.</span></span> <span data-ttu-id="f3001-167">Uma vez Olá extensões `protectedSettings` objeto foi localizado, tome nota de cada um dos parâmetros.</span><span class="sxs-lookup"><span data-stu-id="f3001-167">Once hello extensions `protectedSettings` object has been located, take note of each parameter.</span></span> <span data-ttu-id="f3001-168">No exemplo de Olá de Olá `IaasDiagnostic` extensão, Olá requer os parâmetros são `storageAccountName`, `storageAccountKey`, e `storageAccountEndPoint`.</span><span class="sxs-lookup"><span data-stu-id="f3001-168">In hello example of hello `IaasDiagnostic` extension, hello require parameters are `storageAccountName`, `storageAccountKey`, and `storageAccountEndPoint`.</span></span>

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

### <a name="step-3---re-create-hello-protected-configuration"></a><span data-ttu-id="f3001-169">Passo 3 - recriar a configuração de Olá protegido</span><span class="sxs-lookup"><span data-stu-id="f3001-169">Step 3 - Re-create hello protected configuration</span></span>

<span data-ttu-id="f3001-170">No modelo exportado de Olá, procure `protectedSettings` e substitua Olá exportado protegido definir o objeto com um novo, o que inclui os parâmetros de extensão de Olá necessário e um valor para cada um deles.</span><span class="sxs-lookup"><span data-stu-id="f3001-170">On hello exported template, search for `protectedSettings` and replace hello exported protected setting object with a new one that includes hello required extension parameters and a value for each one.</span></span>

<span data-ttu-id="f3001-171">No exemplo de Olá de Olá `IaasDiagnostic` extensão, nova configuração de definição protegido Olá teria aspeto Olá seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="f3001-171">In hello example of hello `IaasDiagnostic` extension, hello new protected setting configuration would look like hello following example:</span></span>

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

<span data-ttu-id="f3001-172">recurso de extensão final Olá procura toohello semelhante seguinte o exemplo de JSON:</span><span class="sxs-lookup"><span data-stu-id="f3001-172">hello final extension resource looks similar toohello following JSON example:</span></span>

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

<span data-ttu-id="f3001-173">Se utilizar valores de propriedade de tooprovide de parâmetros de modelo, estes têm toobe criado.</span><span class="sxs-lookup"><span data-stu-id="f3001-173">If using template parameters tooprovide property values, these need toobe created.</span></span> <span data-ttu-id="f3001-174">Quando criar os parâmetros do modelo para definir valores de protegidas, certifique-se de que toouse Olá `SecureString` parâmetro de tipo para que os valores confidenciais são protegidos.</span><span class="sxs-lookup"><span data-stu-id="f3001-174">When creating template parameters for protected setting values, make sure toouse hello `SecureString` parameter type so that sensitive values are secured.</span></span> <span data-ttu-id="f3001-175">Para obter mais informações sobre como utilizar parâmetros, consulte [modelos Authoring Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f3001-175">For more information on using parameters, see [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="f3001-176">No exemplo de Olá de Olá `IaasDiagnostic` extensão, seria possível criar Olá seguir os parâmetros na secção de parâmetros de Olá de modelo do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="f3001-176">In hello example of hello `IaasDiagnostic` extension, hello following parameters would be created in hello parameters section of hello Resource Manager template.</span></span>

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

<span data-ttu-id="f3001-177">Neste momento, o modelo de Olá pode ser implementado com qualquer método de implementação do modelo.</span><span class="sxs-lookup"><span data-stu-id="f3001-177">At this point, hello template can be deployed using any template deployment method.</span></span>
