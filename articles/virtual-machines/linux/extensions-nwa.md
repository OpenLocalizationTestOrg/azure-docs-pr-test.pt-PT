---
title: "aaaAzure extensão da máquina virtual de agente do observador de rede para Linux | Microsoft Docs"
description: "Implemente Olá agente do observador de rede na máquina de virtual com Linux utilizando uma extensão da máquina virtual."
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a><span data-ttu-id="791f7-103">Extensão da máquina virtual de agente do observador de rede para Linux</span><span class="sxs-lookup"><span data-stu-id="791f7-103">Network Watcher Agent virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="791f7-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="791f7-104">Overview</span></span>

<span data-ttu-id="791f7-105">[Observador de rede do Azure](https://review.docs.microsoft.com/en-us/azure/network-watcher/) é um serviço de monitorização, diagnóstico e análise de desempenho de rede que permite a monitorização de redes do Azure.</span><span class="sxs-lookup"><span data-stu-id="791f7-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="791f7-106">Olá extensão da máquina virtual de agente do observador de rede é um requisito para algumas das funcionalidades de observador de rede Olá em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="791f7-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="791f7-107">Isto inclui capturar o tráfego de rede a pedido e outras funcionalidades avançadas.</span><span class="sxs-lookup"><span data-stu-id="791f7-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="791f7-108">Olá de detalhes deste documento suportado plataformas e opções de implementação para Olá extensão da máquina virtual de agente do observador de rede para Linux.</span><span class="sxs-lookup"><span data-stu-id="791f7-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="791f7-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="791f7-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="791f7-110">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="791f7-110">Operating system</span></span>

<span data-ttu-id="791f7-111">Olá extensão de agente do observador de rede pode ser executada relativamente a estes distribuições do Linux:</span><span class="sxs-lookup"><span data-stu-id="791f7-111">hello Network Watcher Agent extension can be run against these Linux distributions:</span></span>

| <span data-ttu-id="791f7-112">Distribuição</span><span class="sxs-lookup"><span data-stu-id="791f7-112">Distribution</span></span> | <span data-ttu-id="791f7-113">Versão</span><span class="sxs-lookup"><span data-stu-id="791f7-113">Version</span></span> |
|---|---|
| <span data-ttu-id="791f7-114">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="791f7-114">Ubuntu</span></span> | <span data-ttu-id="791f7-115">16.04 LTS, 14.04 LTS e 12.04 LTS</span><span class="sxs-lookup"><span data-stu-id="791f7-115">16.04 LTS, 14.04 LTS and 12.04 LTS</span></span> |
| <span data-ttu-id="791f7-116">Debian</span><span class="sxs-lookup"><span data-stu-id="791f7-116">Debian</span></span> | <span data-ttu-id="791f7-117">7 e 8</span><span class="sxs-lookup"><span data-stu-id="791f7-117">7 and 8</span></span> |
| <span data-ttu-id="791f7-118">RedHat</span><span class="sxs-lookup"><span data-stu-id="791f7-118">RedHat</span></span> | <span data-ttu-id="791f7-119">6 e 7. x</span><span class="sxs-lookup"><span data-stu-id="791f7-119">6.x and 7.x</span></span> |
| <span data-ttu-id="791f7-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="791f7-120">Oracle Linux</span></span> | <span data-ttu-id="791f7-121">7 x</span><span class="sxs-lookup"><span data-stu-id="791f7-121">7x</span></span> |
| <span data-ttu-id="791f7-122">SUSE</span><span class="sxs-lookup"><span data-stu-id="791f7-122">Suse</span></span> | <span data-ttu-id="791f7-123">11 e 12</span><span class="sxs-lookup"><span data-stu-id="791f7-123">11 and 12</span></span> |
| <span data-ttu-id="791f7-124">OpenSuse</span><span class="sxs-lookup"><span data-stu-id="791f7-124">OpenSuse</span></span> | <span data-ttu-id="791f7-125">7.0</span><span class="sxs-lookup"><span data-stu-id="791f7-125">7.0</span></span> |
| <span data-ttu-id="791f7-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="791f7-126">CentOS</span></span> | <span data-ttu-id="791f7-127">7.0</span><span class="sxs-lookup"><span data-stu-id="791f7-127">7.0</span></span> |

<span data-ttu-id="791f7-128">Tenha em atenção que CoreOS não é suportado neste momento.</span><span class="sxs-lookup"><span data-stu-id="791f7-128">Note that CoreOS is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="791f7-129">Conectividade Internet</span><span class="sxs-lookup"><span data-stu-id="791f7-129">Internet connectivity</span></span>

<span data-ttu-id="791f7-130">Algumas das funcionalidades do agente do observador de rede de Olá requer uma máquina virtual de destino que Olá toohello ligado à Internet.</span><span class="sxs-lookup"><span data-stu-id="791f7-130">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="791f7-131">Sem ligações de saída Olá capacidade tooestablish algumas das funcionalidades do agente do observador de rede de Olá podem avaria ou ficar indisponíveis.</span><span class="sxs-lookup"><span data-stu-id="791f7-131">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="791f7-132">Para obter mais detalhes, consulte Olá [documentação de observador de rede](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span><span class="sxs-lookup"><span data-stu-id="791f7-132">For more details, please see hello [Network Watcher documentation](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="791f7-133">Esquema de extensão</span><span class="sxs-lookup"><span data-stu-id="791f7-133">Extension schema</span></span>

<span data-ttu-id="791f7-134">Olá seguinte JSON mostra esquema Olá para Olá extensão de agente do observador de rede.</span><span class="sxs-lookup"><span data-stu-id="791f7-134">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="791f7-135">extensão de Olá nem requer nem suporta as definições fornecido pelo utilizador neste momento e baseia-se na sua configuração predefinida.</span><span class="sxs-lookup"><span data-stu-id="791f7-135">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentLinux",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="791f7-136">Valores de propriedade</span><span class="sxs-lookup"><span data-stu-id="791f7-136">Property values</span></span>

| <span data-ttu-id="791f7-137">Nome</span><span class="sxs-lookup"><span data-stu-id="791f7-137">Name</span></span> | <span data-ttu-id="791f7-138">Valor / exemplo</span><span class="sxs-lookup"><span data-stu-id="791f7-138">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="791f7-139">apiVersion</span><span class="sxs-lookup"><span data-stu-id="791f7-139">apiVersion</span></span> | <span data-ttu-id="791f7-140">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="791f7-140">2015-06-15</span></span> |
| <span data-ttu-id="791f7-141">Fabricante</span><span class="sxs-lookup"><span data-stu-id="791f7-141">publisher</span></span> | <span data-ttu-id="791f7-142">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="791f7-142">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="791f7-143">tipo</span><span class="sxs-lookup"><span data-stu-id="791f7-143">type</span></span> | <span data-ttu-id="791f7-144">NetworkWatcherAgentLinux</span><span class="sxs-lookup"><span data-stu-id="791f7-144">NetworkWatcherAgentLinux</span></span> |
| <span data-ttu-id="791f7-145">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="791f7-145">typeHandlerVersion</span></span> | <span data-ttu-id="791f7-146">1.4</span><span class="sxs-lookup"><span data-stu-id="791f7-146">1.4</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="791f7-147">Implementação de modelos</span><span class="sxs-lookup"><span data-stu-id="791f7-147">Template deployment</span></span>

<span data-ttu-id="791f7-148">Extensões VM do Azure podem ser implementadas com modelos Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="791f7-148">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="791f7-149">esquema JSON Olá descrita na secção anterior Olá pode ser utilizada numa Olá de toorun de modelo Azure Resource Manager extensão de agente do observador de rede durante uma implementação de modelo Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="791f7-149">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="azure-cli-deployment"></a><span data-ttu-id="791f7-150">Implementação da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="791f7-150">Azure CLI deployment</span></span>

<span data-ttu-id="791f7-151">Olá CLI do Azure pode ser utilizado toodeploy Olá VM de agente do observador de rede extensão tooan máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="791f7-151">hello Azure CLI can be used toodeploy hello Network Watcher Agent VM extension tooan existing virtual machine.</span></span>

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="791f7-152">Resolução de problemas e suporte</span><span class="sxs-lookup"><span data-stu-id="791f7-152">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="791f7-153">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="791f7-153">Troubleshooting</span></span>

<span data-ttu-id="791f7-154">Dados sobre o estado de Olá das implementações de extensão de podem ser obtidos a partir da Olá portal do Azure e utilizando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="791f7-154">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="791f7-155">Estado de implementação de Olá toosee das extensões para uma determinada VM, execute Olá utilizando o comando a seguir Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="791f7-155">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

<span data-ttu-id="791f7-156">Execução de extensão de saída é iniciada toofiles encontrado no Olá seguinte diretório:</span><span class="sxs-lookup"><span data-stu-id="791f7-156">Extension execution output is logged toofiles found in hello following directory:</span></span>

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a><span data-ttu-id="791f7-157">Suporte</span><span class="sxs-lookup"><span data-stu-id="791f7-157">Support</span></span>

<span data-ttu-id="791f7-158">Se precisar de mais ajuda, a qualquer altura neste artigo, pode consulte a documentação do toohello observador de rede ou contactar Olá Azure peritos em Olá [fóruns do MSDN Azure e Stack Overflow](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="791f7-158">If you need more help at any point in this article, you can refer toohello Network Watcher documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="791f7-159">Em alternativa, pode ficheiro um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="791f7-159">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="791f7-160">Aceda toohello [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione o suporte de Get.</span><span class="sxs-lookup"><span data-stu-id="791f7-160">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="791f7-161">Para obter informações sobre como utilizar o suporte do Azure, leia o artigo Olá [suporte do Microsoft Azure FAQ](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="791f7-161">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
