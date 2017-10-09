---
title: "aaaOMS extensão da máquina virtual do Azure para Linux | Microsoft Docs"
description: "Implemente o agente do OMS Olá na máquina de virtual com Linux utilizando uma extensão da máquina virtual."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a><span data-ttu-id="32010-103">Extensão da máquina virtual OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="32010-103">OMS virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="32010-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="32010-104">Overview</span></span>

<span data-ttu-id="32010-105">Operations Management Suite (OMS) fornece capacidades de remediação de monitorização, alertas e alertas na nuvem e no local ativos.</span><span class="sxs-lookup"><span data-stu-id="32010-105">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="32010-106">Olá extensão da máquina virtual de agente do OMS para Linux é publicado e suportado pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="32010-106">hello OMS Agent virtual machine extension for Linux is published and supported by Microsoft.</span></span> <span data-ttu-id="32010-107">a extensão de Olá instala o agente do OMS Olá em máquinas virtuais do Azure e inscreve máquinas virtuais para uma área de trabalho existente do OMS.</span><span class="sxs-lookup"><span data-stu-id="32010-107">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="32010-108">Olá de detalhes deste documento suportado plataformas, as configurações e opções de implementação para Olá extensão da máquina virtual OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="32010-108">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32010-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="32010-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="32010-110">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="32010-110">Operating system</span></span>

<span data-ttu-id="32010-111">Olá extensão de agente do OMS pode ser executada relativamente a estes distribuições do Linux.</span><span class="sxs-lookup"><span data-stu-id="32010-111">hello OMS Agent extension can be run against these Linux distributions.</span></span>

| <span data-ttu-id="32010-112">Distribuição</span><span class="sxs-lookup"><span data-stu-id="32010-112">Distribution</span></span> | <span data-ttu-id="32010-113">Versão</span><span class="sxs-lookup"><span data-stu-id="32010-113">Version</span></span> |
|---|---|
| <span data-ttu-id="32010-114">CentOS Linux</span><span class="sxs-lookup"><span data-stu-id="32010-114">CentOS Linux</span></span> | <span data-ttu-id="32010-115">5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="32010-115">5, 6, and 7</span></span> |
| <span data-ttu-id="32010-116">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="32010-116">Oracle Linux</span></span> | <span data-ttu-id="32010-117">5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="32010-117">5, 6, and 7</span></span> |
| <span data-ttu-id="32010-118">Red Hat Enterprise Linux Server</span><span class="sxs-lookup"><span data-stu-id="32010-118">Red Hat Enterprise Linux Server</span></span> | <span data-ttu-id="32010-119">5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="32010-119">5, 6 and 7</span></span> |
| <span data-ttu-id="32010-120">Debian GNU/Linux</span><span class="sxs-lookup"><span data-stu-id="32010-120">Debian GNU/Linux</span></span> | <span data-ttu-id="32010-121">6, 7 e 8</span><span class="sxs-lookup"><span data-stu-id="32010-121">6, 7, and 8</span></span> |
| <span data-ttu-id="32010-122">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="32010-122">Ubuntu</span></span> | <span data-ttu-id="32010-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="32010-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span></span> |
| <span data-ttu-id="32010-124">Servidor Linux Empresarial SUSE</span><span class="sxs-lookup"><span data-stu-id="32010-124">SUSE Linux Enterprise Server</span></span> | <span data-ttu-id="32010-125">11 e 12</span><span class="sxs-lookup"><span data-stu-id="32010-125">11 and 12</span></span> |

### <a name="internet-connectivity"></a><span data-ttu-id="32010-126">Conectividade Internet</span><span class="sxs-lookup"><span data-stu-id="32010-126">Internet connectivity</span></span>

<span data-ttu-id="32010-127">Olá Linux na extensão do agente do OMS requer a máquina virtual de destino que Olá é toohello ligado à internet.</span><span class="sxs-lookup"><span data-stu-id="32010-127">hello OMS Agent extension for Linux requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="32010-128">Esquema de extensão</span><span class="sxs-lookup"><span data-stu-id="32010-128">Extension schema</span></span>

<span data-ttu-id="32010-129">Olá seguinte JSON mostra esquema Olá para Olá extensão de agente do OMS.</span><span class="sxs-lookup"><span data-stu-id="32010-129">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="32010-130">extensão de Olá requer Olá área de trabalho ID e a área de trabalho chave a partir da área de trabalho do OMS do destino de Olá; Estes valores podem ser encontrados no portal do OMS Olá.</span><span class="sxs-lookup"><span data-stu-id="32010-130">hello extension requires hello workspace ID and workspace key from hello target OMS workspace; these values can be found in hello OMS portal.</span></span> <span data-ttu-id="32010-131">Porque a chave da área de trabalho de Olá deve ser tratado como dados confidenciais, devem ser armazenado numa configuração de definição protegido.</span><span class="sxs-lookup"><span data-stu-id="32010-131">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="32010-132">Dados de definição de extensão protegido de VM do Azure é encriptados e desencriptados apenas na máquina de virtual de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="32010-132">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="32010-133">Tenha em atenção que **workspaceId** e **workspaceKey** diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="32010-133">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a><span data-ttu-id="32010-134">Valores de propriedade</span><span class="sxs-lookup"><span data-stu-id="32010-134">Property values</span></span>

| <span data-ttu-id="32010-135">Nome</span><span class="sxs-lookup"><span data-stu-id="32010-135">Name</span></span> | <span data-ttu-id="32010-136">Valor / exemplo</span><span class="sxs-lookup"><span data-stu-id="32010-136">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="32010-137">apiVersion</span><span class="sxs-lookup"><span data-stu-id="32010-137">apiVersion</span></span> | <span data-ttu-id="32010-138">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="32010-138">2015-06-15</span></span> |
| <span data-ttu-id="32010-139">Fabricante</span><span class="sxs-lookup"><span data-stu-id="32010-139">publisher</span></span> | <span data-ttu-id="32010-140">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="32010-140">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="32010-141">tipo</span><span class="sxs-lookup"><span data-stu-id="32010-141">type</span></span> | <span data-ttu-id="32010-142">OmsAgentForLinux</span><span class="sxs-lookup"><span data-stu-id="32010-142">OmsAgentForLinux</span></span> |
| <span data-ttu-id="32010-143">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="32010-143">typeHandlerVersion</span></span> | <span data-ttu-id="32010-144">1.4</span><span class="sxs-lookup"><span data-stu-id="32010-144">1.4</span></span> |
| <span data-ttu-id="32010-145">workspaceId (por exemplo)</span><span class="sxs-lookup"><span data-stu-id="32010-145">workspaceId (e.g)</span></span> | <span data-ttu-id="32010-146">6f680a37-00c6-41C7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="32010-146">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="32010-147">workspaceKey (por exemplo)</span><span class="sxs-lookup"><span data-stu-id="32010-147">workspaceKey (e.g)</span></span> | <span data-ttu-id="32010-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI + rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ = =</span><span class="sxs-lookup"><span data-stu-id="32010-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="32010-149">Implementação de modelos</span><span class="sxs-lookup"><span data-stu-id="32010-149">Template deployment</span></span>

<span data-ttu-id="32010-150">Extensões VM do Azure podem ser implementadas com modelos Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="32010-150">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="32010-151">Os modelos são ideais quando implementar um ou mais máquinas virtuais que necessitam de configuração de implementação de post, tais como tooOMS de integração.</span><span class="sxs-lookup"><span data-stu-id="32010-151">Templates are ideal when deploying one or more virtual machines that require post deployment configuration such as onboarding tooOMS.</span></span> <span data-ttu-id="32010-152">Um modelo de Gestor de recursos de exemplo que inclui a extensão da VM de agente do OMS Olá pode ser encontrado no Olá [Galeria de início rápido de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span><span class="sxs-lookup"><span data-stu-id="32010-152">A sample Resource Manager template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span></span> 

<span data-ttu-id="32010-153">configuração de JSON Olá para uma extensão de máquina virtual pode ser aninhada Olá recurso de máquina virtual ou colocada na raiz de Olá ou de nível superior de um modelo do Resource Manager JSON.</span><span class="sxs-lookup"><span data-stu-id="32010-153">hello JSON configuration for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="32010-154">a colocação da configuração de JSON Olá Olá afeta valor Olá Olá recursos nome e tipo.</span><span class="sxs-lookup"><span data-stu-id="32010-154">hello placement of hello JSON configuration affects hello value of hello resource name and type.</span></span> <span data-ttu-id="32010-155">Para obter mais informações, consulte [definir nome e tipo para recursos subordinados](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="32010-155">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="32010-156">Olá exemplo que se segue parte do princípio de extensão do OMS Olá é aninhada Olá recurso de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="32010-156">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="32010-157">Quando o aninhamento de recursos de extensão de Olá, Olá JSON é colocada na Olá `"resources": []` objeto de máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="32010-157">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

<span data-ttu-id="32010-158">Quando colocar extensão Olá JSON na raiz de Olá de modelo de Olá, nome do recurso Olá inclui uma máquina virtual do referência toohello principal e tipo de Olá reflete configuração aninhada Olá.</span><span class="sxs-lookup"><span data-stu-id="32010-158">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span>  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a><span data-ttu-id="32010-159">Implementação da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="32010-159">Azure CLI deployment</span></span>

<span data-ttu-id="32010-160">Olá CLI do Azure pode ser utilizado toodeploy Olá VM de agente do OMS extensão tooan máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="32010-160">hello Azure CLI can be used toodeploy hello OMS Agent VM extension tooan existing virtual machine.</span></span> <span data-ttu-id="32010-161">Substitua a chave OMS de Olá e o ID do OMS com os da sua área de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="32010-161">Replace hello OMS key and OMS ID with those from your OMS workspace.</span></span> 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="32010-162">Resolver problemas e suporte</span><span class="sxs-lookup"><span data-stu-id="32010-162">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="32010-163">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="32010-163">Troubleshoot</span></span>

<span data-ttu-id="32010-164">Dados sobre o estado de Olá das implementações de extensão de podem ser obtidos a partir da Olá portal do Azure e utilizando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="32010-164">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="32010-165">Estado de implementação de Olá toosee das extensões para uma determinada VM, execute Olá utilizando o comando a seguir Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="32010-165">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="32010-166">Execução de extensão de saída é toohello registado os seguintes ficheiros:</span><span class="sxs-lookup"><span data-stu-id="32010-166">Extension execution output is logged toohello following file:</span></span>

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a><span data-ttu-id="32010-167">Códigos de erro e os respetivos significados</span><span class="sxs-lookup"><span data-stu-id="32010-167">Error codes and their meanings</span></span>

| <span data-ttu-id="32010-168">Código de erro</span><span class="sxs-lookup"><span data-stu-id="32010-168">Error Code</span></span> | <span data-ttu-id="32010-169">Significado</span><span class="sxs-lookup"><span data-stu-id="32010-169">Meaning</span></span> | <span data-ttu-id="32010-170">Ação possíveis</span><span class="sxs-lookup"><span data-stu-id="32010-170">Possible Action</span></span> |
| :---: | --- | --- |
| <span data-ttu-id="32010-171">10</span><span class="sxs-lookup"><span data-stu-id="32010-171">10</span></span> | <span data-ttu-id="32010-172">VM já se encontra ligado tooan área de trabalho do OMS</span><span class="sxs-lookup"><span data-stu-id="32010-172">VM is already connected tooan OMS workspace</span></span> | <span data-ttu-id="32010-173">tooconnect Olá VM toohello área de trabalho especificada no esquema de extensão de Olá, defina stopOnMultipleConnections toofalse nas definições de públicas ou remova esta propriedade.</span><span class="sxs-lookup"><span data-stu-id="32010-173">tooconnect hello VM toohello workspace specified in hello extension schema, set stopOnMultipleConnections toofalse in public settings or remove this property.</span></span> <span data-ttu-id="32010-174">Esta VM obtém cobrada depois de cada área de trabalho está ligado a um.</span><span class="sxs-lookup"><span data-stu-id="32010-174">This VM gets billed once for each workspace it is connected to.</span></span> |
| <span data-ttu-id="32010-175">11</span><span class="sxs-lookup"><span data-stu-id="32010-175">11</span></span> | <span data-ttu-id="32010-176">Configuração inválida fornecida toohello extensão</span><span class="sxs-lookup"><span data-stu-id="32010-176">Invalid config provided toohello extension</span></span> | <span data-ttu-id="32010-177">Siga Olá precedente exemplos tooset todos os valores de propriedade necessários para a implementação.</span><span class="sxs-lookup"><span data-stu-id="32010-177">Follow hello preceding examples tooset all property values necessary for deployment.</span></span> |
| <span data-ttu-id="32010-178">12</span><span class="sxs-lookup"><span data-stu-id="32010-178">12</span></span> | <span data-ttu-id="32010-179">Gestor de pacotes de dpkg Olá está bloqueado</span><span class="sxs-lookup"><span data-stu-id="32010-179">hello dpkg package manager is locked</span></span> | <span data-ttu-id="32010-180">Certifique-se de que todos os dpkg operações de atualização na máquina de Olá tiver concluído e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="32010-180">Make sure all dpkg update operations on hello machine have finished and retry.</span></span> |
| <span data-ttu-id="32010-181">20</span><span class="sxs-lookup"><span data-stu-id="32010-181">20</span></span> | <span data-ttu-id="32010-182">Ativar chamado prematuramente</span><span class="sxs-lookup"><span data-stu-id="32010-182">Enable called prematurely</span></span> | <span data-ttu-id="32010-183">[Olá atualização agente Linux do Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello versão mais recente disponível.</span><span class="sxs-lookup"><span data-stu-id="32010-183">[Update hello Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello latest available version.</span></span> |
| <span data-ttu-id="32010-184">51</span><span class="sxs-lookup"><span data-stu-id="32010-184">51</span></span> | <span data-ttu-id="32010-185">Esta extensão não é suportada no sistema de operativo Olá da VM</span><span class="sxs-lookup"><span data-stu-id="32010-185">This extension is not supported on hello VM's operation system</span></span> | |
| <span data-ttu-id="32010-186">55</span><span class="sxs-lookup"><span data-stu-id="32010-186">55</span></span> | <span data-ttu-id="32010-187">Não é possível ligar o serviço do Microsoft Operations Management Suite toohello</span><span class="sxs-lookup"><span data-stu-id="32010-187">Cannot connect toohello Microsoft Operations Management Suite service</span></span> | <span data-ttu-id="32010-188">Verifique se Olá sistema tem acesso à Internet ou que foi fornecido um proxy HTTP válido.</span><span class="sxs-lookup"><span data-stu-id="32010-188">Check that hello system either has Internet access, or that a valid HTTP proxy has been provided.</span></span> <span data-ttu-id="32010-189">Além disso, verifique a correção de Olá do ID da área de trabalho Olá.</span><span class="sxs-lookup"><span data-stu-id="32010-189">Additionally, check hello correctness of hello workspace ID.</span></span> |

<span data-ttu-id="32010-190">Informações adicionais de resolução de problemas podem ser encontradas no Olá [guia de resolução de problemas do OMS agente para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span><span class="sxs-lookup"><span data-stu-id="32010-190">Additional troubleshooting information can be found on hello [OMS-Agent-for-Linux Troubleshooting Guide](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span></span>

### <a name="support"></a><span data-ttu-id="32010-191">Suporte</span><span class="sxs-lookup"><span data-stu-id="32010-191">Support</span></span>

<span data-ttu-id="32010-192">Se precisar de mais ajuda, a qualquer altura neste artigo, pode contactar Olá especialistas do Azure no Olá [fóruns do MSDN Azure e Stack Overflow](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="32010-192">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="32010-193">Em alternativa, pode ficheiro um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="32010-193">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="32010-194">Aceda toohello [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione o suporte de Get.</span><span class="sxs-lookup"><span data-stu-id="32010-194">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="32010-195">Para obter informações sobre como utilizar o suporte do Azure, leia o artigo Olá [suporte do Microsoft Azure FAQ](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="32010-195">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
