---
title: "aaaEnable ou desativar a monitorização de VM do Azure"
description: "Descreve como tooEnable ou desativar a monitorização de VM do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a><span data-ttu-id="31042-103">Ativar ou desativar a monitorização de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="31042-103">Enable or Disable Azure VM Monitoring</span></span>

<span data-ttu-id="31042-104">Esta secção descreve como tooenable ou desativar a monitorização em Virtual máquinas em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="31042-104">This section describes how tooenable or disable monitoring on Virtual machines running on Azure.</span></span> <span data-ttu-id="31042-105">Pode ativar ou desativar a monitorização utilizando o portal de Olá ou Interface de linha de comandos do Azure para Mac, Linux e Windows (Olá CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="31042-105">You can enable or disable monitoring using hello portal or Azure Command-line Interface for Mac, Linux, and Windows (hello Azure CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31042-106">Este documento descreve a versão 2.3 de Olá extensão diagnóstico de Linux, o que foi preterido.</span><span class="sxs-lookup"><span data-stu-id="31042-106">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="31042-107">Versão 2.3 será suportada até 30 de Junho de 2018.</span><span class="sxs-lookup"><span data-stu-id="31042-107">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="31042-108">Versão 3.0 do Olá que extensão de diagnóstico do Linux em vez disso, pode ser ativada.</span><span class="sxs-lookup"><span data-stu-id="31042-108">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="31042-109">Para obter mais informações, consulte [Olá documentação](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="31042-109">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a><span data-ttu-id="31042-110">Ativar / desativar a monitorização Olá através do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="31042-110">Enable / Disable Monitoring through hello Azure portal</span></span>

<span data-ttu-id="31042-111">Pode ativar a monitorização da sua VM do Azure, que fornecem dados sobre a instância em períodos de 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="31042-111">You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods.</span></span> <span data-ttu-id="31042-112">(aplicam alterações de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="31042-112">(storage changes apply).</span></span> <span data-ttu-id="31042-113">Dados de diagnóstico detalhadas, em seguida, estão disponíveis para Olá VM em gráficos de portal Olá ou através de Olá API.</span><span class="sxs-lookup"><span data-stu-id="31042-113">Detailed diagnostics data is then available for hello VM in hello portal graphs or through hello API.</span></span> <span data-ttu-id="31042-114">Por predefinição, o portal do Azure permite a monitorização baseadas em anfitrião de um conjunto limitado de métricas.</span><span class="sxs-lookup"><span data-stu-id="31042-114">By default, Azure portal enables host-based monitoring of a limited set of metrics.</span></span> <span data-ttu-id="31042-115">Pode ativar a monitorização de métricas de dentro de uma VM ao hello que VM está em execução ou em estado de paragem.</span><span class="sxs-lookup"><span data-stu-id="31042-115">You can enable monitoring of metrics from within a VM while hello VM is running or in stopped state.</span></span>

* <span data-ttu-id="31042-116">Abra Olá Azure portal em [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="31042-116">Open hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
* <span data-ttu-id="31042-117">No Olá deixado de navegação, clique em máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="31042-117">In hello left navigation, click Virtual machines.</span></span>
* <span data-ttu-id="31042-118">Em Olá máquinas de virtuais de lista, selecione uma instância em execução ou parada.</span><span class="sxs-lookup"><span data-stu-id="31042-118">In hello list Virtual machines, select a running or stopped instance.</span></span> <span data-ttu-id="31042-119">é aberto o painel do Olá "Máquina Virtual".</span><span class="sxs-lookup"><span data-stu-id="31042-119">hello "Virtual machine" blade opens.</span></span>
* <span data-ttu-id="31042-120">Clique em todas as definições.</span><span class="sxs-lookup"><span data-stu-id="31042-120">Click All settings.</span></span>
* <span data-ttu-id="31042-121">Clique em diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="31042-121">Click Diagnostics.</span></span>
* <span data-ttu-id="31042-122">Alterar Estado tooOn ou terminar a sessão.</span><span class="sxs-lookup"><span data-stu-id="31042-122">Change status tooOn or Off.</span></span> <span data-ttu-id="31042-123">Também pode escolher neste nível de Olá do painel de detalhes que gostaria de tooenable para a máquina virtual de monitorização.</span><span class="sxs-lookup"><span data-stu-id="31042-123">You can also pick in this blade hello level of monitoring details you would like tooenable for your virtual machine.</span></span>

![Ativar / desativar a monitorização através de Olá portal do Azure.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a><span data-ttu-id="31042-125">Ativar / desativar a monitorização com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="31042-125">Enable / Disable Monitoring with Azure CLI</span></span>

<span data-ttu-id="31042-126">tooenable monitorização para uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="31042-126">tooenable monitoring for an Azure VM.</span></span>

* <span data-ttu-id="31042-127">Crie um ficheiro (com o nome como PrivateConfig.json):</span><span class="sxs-lookup"><span data-stu-id="31042-127">Create a file (named such as PrivateConfig.json):</span></span>

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* <span data-ttu-id="31042-128">Ative a extensão de Olá através da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="31042-128">Enable hello extension via Azure CLI.</span></span>

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

<span data-ttu-id="31042-129">Para obter mais informações, consulte [utilizando a extensão de diagnóstico do Linux tooMonitor Linux VM dados de desempenho e diagnóstico](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="31042-129">For more information, see [Using Linux Diagnostic Extension tooMonitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
