---
title: "aaaUse da automatização do Azure toovertically dimensionar as máquinas virtuais do Windows | Microsoft Docs"
description: "Aumentar verticalmente Máquina Virtual do Windows nos alertas do toomonitoring resposta com a automatização do Azure"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4f964713-fb67-4bcc-8246-3431452ddf7d
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: kasing
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 24d07f3e2e217668f18676e6d6873be4f9770349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-windows-vms-with-azure-automation"></a><span data-ttu-id="d429d-103">Aumentar verticalmente VMs do Windows com a automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="d429d-103">Vertically scale Windows VMs with Azure Automation</span></span>

<span data-ttu-id="d429d-104">Dimensionamento vertical é o processo de Olá de aumente ou diminua recursos Olá de uma máquina numa carga de trabalho de toohello de resposta.</span><span class="sxs-lookup"><span data-stu-id="d429d-104">Vertical scaling is hello process of increasing or decreasing hello resources of a machine in response toohello workload.</span></span> <span data-ttu-id="d429d-105">No Azure Isto pode ser efetuado ao alterar o tamanho de Olá de Olá Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="d429d-105">In Azure this can be accomplished by changing hello size of hello Virtual Machine.</span></span> <span data-ttu-id="d429d-106">Isto pode ajudar nos seguintes cenários de Olá</span><span class="sxs-lookup"><span data-stu-id="d429d-106">This can help in hello following scenarios</span></span>

* <span data-ttu-id="d429d-107">Se Olá Máquina Virtual não está a ser utilizada com frequência, pode redimensioná-lo para baixo tooa tooreduce de tamanho mais pequeno os custos mensais</span><span class="sxs-lookup"><span data-stu-id="d429d-107">If hello Virtual Machine is not being used frequently, you can resize it down tooa smaller size tooreduce your monthly costs</span></span>
* <span data-ttu-id="d429d-108">Se Olá Máquina Virtual está a ter um pico de carga, pode ser redimensionado tooa maior tamanho tooincrease a capacidade</span><span class="sxs-lookup"><span data-stu-id="d429d-108">If hello Virtual Machine is seeing a peak load, it can be resized tooa larger size tooincrease its capacity</span></span>

<span data-ttu-id="d429d-109">Descrição de Olá para Olá passos tooaccomplish trata como abaixo</span><span class="sxs-lookup"><span data-stu-id="d429d-109">hello outline for hello steps tooaccomplish this is as below</span></span>

1. <span data-ttu-id="d429d-110">O programa de configuração da automatização do Azure tooaccess as máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="d429d-110">Setup Azure Automation tooaccess your Virtual Machines</span></span>
2. <span data-ttu-id="d429d-111">Importar Olá runbooks de escala Vertical de automatização do Azure para a sua subscrição</span><span class="sxs-lookup"><span data-stu-id="d429d-111">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="d429d-112">Adicionar um runbook de tooyour do webhook</span><span class="sxs-lookup"><span data-stu-id="d429d-112">Add a webhook tooyour runbook</span></span>
4. <span data-ttu-id="d429d-113">Adicionar um alerta tooyour Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="d429d-113">Add an alert tooyour Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="d429d-114">Devido ao tamanho de Olá de Olá primeira Máquina Virtual, tamanhos de Olá pode ser ampliada, poderá ser limitado devido a disponibilidade de toohello de Olá outros tamanhos de cluster Olá atual Máquina Virtual está implementada no.</span><span class="sxs-lookup"><span data-stu-id="d429d-114">Because of hello size of hello first Virtual Machine, hello sizes it can be scaled to, may be limited due toohello availability of hello other sizes in hello cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="d429d-115">No Olá publicar runbooks de automatização utilizados neste artigo, vamos asseguramos neste caso e dimensionar apenas dentro do Olá abaixo pares de tamanho VM.</span><span class="sxs-lookup"><span data-stu-id="d429d-115">In hello published automation runbooks used in this article we take care of this case and only scale within hello below VM size pairs.</span></span> <span data-ttu-id="d429d-116">Isto significa que uma Máquina Virtual de Standard_D1v2 subitamente não irá ser escalado para cima tooStandard_G5 ou ampliada baixo tooBasic_A0.</span><span class="sxs-lookup"><span data-stu-id="d429d-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up tooStandard_G5 or scaled down tooBasic_A0.</span></span>
> 
> | <span data-ttu-id="d429d-117">Dimensionamento par de tamanhos de VM</span><span class="sxs-lookup"><span data-stu-id="d429d-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="d429d-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="d429d-118">Basic_A0</span></span> |<span data-ttu-id="d429d-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="d429d-119">Basic_A4</span></span> |
> | <span data-ttu-id="d429d-120">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="d429d-120">Standard_A0</span></span> |<span data-ttu-id="d429d-121">Standard_A4</span><span class="sxs-lookup"><span data-stu-id="d429d-121">Standard_A4</span></span> |
> | <span data-ttu-id="d429d-122">Standard_A5</span><span class="sxs-lookup"><span data-stu-id="d429d-122">Standard_A5</span></span> |<span data-ttu-id="d429d-123">Standard_A7</span><span class="sxs-lookup"><span data-stu-id="d429d-123">Standard_A7</span></span> |
> | <span data-ttu-id="d429d-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="d429d-124">Standard_A8</span></span> |<span data-ttu-id="d429d-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="d429d-125">Standard_A9</span></span> |
> | <span data-ttu-id="d429d-126">Standard_A10</span><span class="sxs-lookup"><span data-stu-id="d429d-126">Standard_A10</span></span> |<span data-ttu-id="d429d-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="d429d-127">Standard_A11</span></span> |
> | <span data-ttu-id="d429d-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="d429d-128">Standard_D1</span></span> |<span data-ttu-id="d429d-129">Standard_D4</span><span class="sxs-lookup"><span data-stu-id="d429d-129">Standard_D4</span></span> |
> | <span data-ttu-id="d429d-130">Standard_D11</span><span class="sxs-lookup"><span data-stu-id="d429d-130">Standard_D11</span></span> |<span data-ttu-id="d429d-131">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="d429d-131">Standard_D14</span></span> |
> | <span data-ttu-id="d429d-132">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="d429d-132">Standard_DS1</span></span> |<span data-ttu-id="d429d-133">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="d429d-133">Standard_DS4</span></span> |
> | <span data-ttu-id="d429d-134">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="d429d-134">Standard_DS11</span></span> |<span data-ttu-id="d429d-135">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="d429d-135">Standard_DS14</span></span> |
> | <span data-ttu-id="d429d-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="d429d-136">Standard_D1v2</span></span> |<span data-ttu-id="d429d-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="d429d-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="d429d-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="d429d-138">Standard_D11v2</span></span> |<span data-ttu-id="d429d-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="d429d-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="d429d-140">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="d429d-140">Standard_G1</span></span> |<span data-ttu-id="d429d-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="d429d-141">Standard_G5</span></span> |
> | <span data-ttu-id="d429d-142">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="d429d-142">Standard_GS1</span></span> |<span data-ttu-id="d429d-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="d429d-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a><span data-ttu-id="d429d-144">O programa de configuração da automatização do Azure tooaccess as máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="d429d-144">Setup Azure Automation tooaccess your Virtual Machines</span></span>
<span data-ttu-id="d429d-145">Olá primeira coisa que precisa de toodo é criar uma conta de automatização do Azure que irá alojar Olá runbooks utilizados tooscale uma Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="d429d-145">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale a Virtual Machine.</span></span> <span data-ttu-id="d429d-146">Recentemente o serviço de automatização Olá introduzida Olá "Conta Run As" funcionalidade que permite configurar Olá Principal de serviço para executar automaticamente Olá runbooks em nome de utilizador Olá muito fácil.</span><span class="sxs-lookup"><span data-stu-id="d429d-146">Recently hello Automation service introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on hello user's behalf very easy.</span></span> <span data-ttu-id="d429d-147">Pode ler mais sobre este artigo Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="d429d-147">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="d429d-148">Autenticar Runbooks com a conta Run As do Azure</span><span class="sxs-lookup"><span data-stu-id="d429d-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="d429d-149">Importar Olá runbooks de escala Vertical de automatização do Azure para a sua subscrição</span><span class="sxs-lookup"><span data-stu-id="d429d-149">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="d429d-150">Olá runbooks que são necessários para aumentar verticalmente a sua máquina Virtual já são publicados no Olá Galeria de Runbooks de automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="d429d-150">hello runbooks that are needed for Vertically Scaling your Virtual Machine are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="d429d-151">Terá de tooimport-los na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="d429d-151">You will need tooimport them into your subscription.</span></span> <span data-ttu-id="d429d-152">Pode saber como tooimport runbooks. o lendo Olá seguinte artigo.</span><span class="sxs-lookup"><span data-stu-id="d429d-152">You can learn how tooimport runbooks by reading hello following article.</span></span>

* [<span data-ttu-id="d429d-153">Galleries módulos e Runbooks de automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="d429d-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="d429d-154">Olá runbooks que necessitam de toobe importado são apresentados na imagem de Olá abaixo</span><span class="sxs-lookup"><span data-stu-id="d429d-154">hello runbooks that need toobe imported are shown in hello image below</span></span>

![Importar runbooks](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="d429d-156">Adicionar um runbook de tooyour do webhook</span><span class="sxs-lookup"><span data-stu-id="d429d-156">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="d429d-157">Assim que tiver de importar runbooks Olá terá tooadd webhook toohello runbook pelo que pode ser acionada por um alerta de uma Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="d429d-157">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="d429d-158">detalhes de Olá de criar um webhook de Runbook podem ser lidos aqui</span><span class="sxs-lookup"><span data-stu-id="d429d-158">hello details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="d429d-159">Webhooks de automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="d429d-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="d429d-160">Certifique-se que copiar Olá webhook antes de fechar a caixa de diálogo do Olá webhook como irá precisar na secção seguinte, Olá.</span><span class="sxs-lookup"><span data-stu-id="d429d-160">Make sure you copy hello webhook before closing hello webhook dialog as you will need this in hello next section.</span></span>

## <a name="add-an-alert-tooyour-virtual-machine"></a><span data-ttu-id="d429d-161">Adicionar um alerta tooyour Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="d429d-161">Add an alert tooyour Virtual Machine</span></span>
1. <span data-ttu-id="d429d-162">Selecione as definições da Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="d429d-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="d429d-163">Selecione "Regras de alerta"</span><span class="sxs-lookup"><span data-stu-id="d429d-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="d429d-164">Selecione "Adicionar alerta"</span><span class="sxs-lookup"><span data-stu-id="d429d-164">Select "Add alert"</span></span>
4. <span data-ttu-id="d429d-165">Selecione um alerta de Olá toofire métrica no</span><span class="sxs-lookup"><span data-stu-id="d429d-165">Select a metric toofire hello alert on</span></span>
5. <span data-ttu-id="d429d-166">Selecione uma condição que quando cumprido irá causar Olá toofire de alerta</span><span class="sxs-lookup"><span data-stu-id="d429d-166">Select a condition, which when fulfilled will cause hello alert toofire</span></span>
6. <span data-ttu-id="d429d-167">Selecione um limiar para a condição de Olá no passo 5.</span><span class="sxs-lookup"><span data-stu-id="d429d-167">Select a threshold for hello condition in Step 5.</span></span> <span data-ttu-id="d429d-168">toobe cumprido</span><span class="sxs-lookup"><span data-stu-id="d429d-168">toobe fulfilled</span></span>
7. <span data-ttu-id="d429d-169">Selecionar um período de ativação pós-falha que Olá irá verificar o serviço de monitorização para a condição de Olá e limiar de passos 5 & 6</span><span class="sxs-lookup"><span data-stu-id="d429d-169">Select a period over which hello monitoring service will check for hello condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="d429d-170">Cole no webhook Olá que copiou na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="d429d-170">Paste in hello webhook you copied from hello previous section.</span></span>

![Adicionar o alerta tooVirtual máquina 1](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Adicionar o alerta tooVirtual Machine 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

