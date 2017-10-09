---
title: aaaReplace um controlador de StorSimple EBOD | Microsoft Docs
description: Explica como tooremove e substitua um ou ambos os controladores EBOD num dispositivo StorSimple 8600.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8cbfa507-1a56-4e24-99dd-7db9abd3b850
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 5d29de2ee30bfdd70910050eee5cfa1d293d444f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="18589-103">Substituir um controlador EBOD no dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="18589-103">Replace an EBOD controller on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="18589-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="18589-104">Overview</span></span>
<span data-ttu-id="18589-105">Este tutorial explica como tooreplace um módulo de controlador EBOD defeituoso no seu dispositivo do Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="18589-105">This tutorial explains how tooreplace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="18589-106">um módulo de controlador EBOD tooreplace, tem de:</span><span class="sxs-lookup"><span data-stu-id="18589-106">tooreplace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="18589-107">Remover Olá defeituoso EBOD controlador</span><span class="sxs-lookup"><span data-stu-id="18589-107">Remove hello faulty EBOD controller</span></span>
* <span data-ttu-id="18589-108">Instalar um novo controlador EBOD</span><span class="sxs-lookup"><span data-stu-id="18589-108">Install a new EBOD controller</span></span>

<span data-ttu-id="18589-109">Considere Olá seguintes informações antes de começar:</span><span class="sxs-lookup"><span data-stu-id="18589-109">Consider hello following information before you begin:</span></span>

* <span data-ttu-id="18589-110">Módulos EBOD em branco tem de ser inseridos em todas as ranhuras de não utilizadas.</span><span class="sxs-lookup"><span data-stu-id="18589-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="18589-111">inclusão de Olá não será esporádico corretamente se uma ranhura é deixada aberta.</span><span class="sxs-lookup"><span data-stu-id="18589-111">hello enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="18589-112">controlador EBOD Olá é frequente-swappable e pode ser removido ou substituído.</span><span class="sxs-lookup"><span data-stu-id="18589-112">hello EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="18589-113">Não remova um módulo falhado até ter uma substituição.</span><span class="sxs-lookup"><span data-stu-id="18589-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="18589-114">Quando inicia o processo de substituição de Olá, deve ser concluído dentro de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="18589-114">When you initiate hello replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="18589-115">Antes de tentar tooremove ou substituir qualquer componente do StorSimple, certifique-se de que revê Olá [convenções de ícone de segurança](storsimple-safety.md#safety-icon-conventions) e outros [precauções de segurança](storsimple-safety.md).</span><span class="sxs-lookup"><span data-stu-id="18589-115">Before attempting tooremove or replace any StorSimple component, make sure that you review hello [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>
> 
> 

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="18589-116">Remover um controlador EBOD</span><span class="sxs-lookup"><span data-stu-id="18589-116">Remove an EBOD controller</span></span>
<span data-ttu-id="18589-117">Antes de Olá Falha ao substituir o módulo de controlador EBOD no dispositivo StorSimple, certifique-se de que Olá outro módulo de controlador EBOD está ativa e em execução.</span><span class="sxs-lookup"><span data-stu-id="18589-117">Before replacing hello failed EBOD controller module in your StorSimple device, make sure that hello other EBOD controller module is active and running.</span></span> <span data-ttu-id="18589-118">Olá procedimento e tabela seguintes explicam como tooremove Olá módulo de controlador EBOD.</span><span class="sxs-lookup"><span data-stu-id="18589-118">hello following procedure and table explain how tooremove hello EBOD controller module.</span></span>

#### <a name="tooremove-an-ebod-module"></a><span data-ttu-id="18589-119">tooremove um módulo EBOD</span><span class="sxs-lookup"><span data-stu-id="18589-119">tooremove an EBOD module</span></span>
1. <span data-ttu-id="18589-120">Abra Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="18589-120">Open hello Azure classic portal.</span></span>
2. <span data-ttu-id="18589-121">Navegue demasiado**dispositivos** > **manutenção** > **estado do Hardware**e certifique-se de que o estado de Olá de Olá GUIADO para Olá EBOD Active Directory módulo de controlador é verde e Olá LED para o módulo de controlador EBOD Olá falhada é vermelho.</span><span class="sxs-lookup"><span data-stu-id="18589-121">Navigate too**Devices** > **Maintenance** > **Hardware Status**, and verify that hello status of hello LED for hello active EBOD controller module is green and hello LED for hello failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="18589-122">Localize o módulo de controlador EBOD Olá falhada Olá back of dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="18589-122">Locate hello failed EBOD controller module at hello back of hello device.</span></span>
4. <span data-ttu-id="18589-123">Remova os cabos de Olá ligar o controlador de toohello Olá EBOD controlador módulo antes de tirar o módulo EBOD Olá fora do sistema de Olá.</span><span class="sxs-lookup"><span data-stu-id="18589-123">Remove hello cables that connect hello EBOD controller module toohello controller before taking hello EBOD module out of hello system.</span></span>
5. <span data-ttu-id="18589-124">Tome nota da porta SAS exata de Olá da Olá EBOD controlador módulo que foi ligado toohello controlador.</span><span class="sxs-lookup"><span data-stu-id="18589-124">Make a note of hello exact SAS port of hello EBOD controller module that was connected toohello controller.</span></span> <span data-ttu-id="18589-125">Será necessário toorestore de configuração Olá system toothis depois de as substituir o módulo EBOD Olá.</span><span class="sxs-lookup"><span data-stu-id="18589-125">You will be required toorestore hello system toothis configuration after you replace hello EBOD module.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="18589-126">Normalmente, esta será a porta A, que é denominada como **alojar na** no Olá diagrama a seguir.</span><span class="sxs-lookup"><span data-stu-id="18589-126">Typically, this will be Port A, which is labeled as **Host in** in hello following diagram.</span></span>
   > 
   > 
   
    ![Controlador Backplane de EBOD](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="18589-128">**Figura 1** módulo do Back EBOD</span><span class="sxs-lookup"><span data-stu-id="18589-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="18589-129">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="18589-129">Label</span></span> | <span data-ttu-id="18589-130">Descrição</span><span class="sxs-lookup"><span data-stu-id="18589-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="18589-131">1</span><span class="sxs-lookup"><span data-stu-id="18589-131">1</span></span> |<span data-ttu-id="18589-132">Falhas LED</span><span class="sxs-lookup"><span data-stu-id="18589-132">Fault LED</span></span> |
   | <span data-ttu-id="18589-133">2</span><span class="sxs-lookup"><span data-stu-id="18589-133">2</span></span> |<span data-ttu-id="18589-134">Energia LED</span><span class="sxs-lookup"><span data-stu-id="18589-134">Power LED</span></span> |
   | <span data-ttu-id="18589-135">3</span><span class="sxs-lookup"><span data-stu-id="18589-135">3</span></span> |<span data-ttu-id="18589-136">Conectores SAS</span><span class="sxs-lookup"><span data-stu-id="18589-136">SAS connectors</span></span> |
   | <span data-ttu-id="18589-137">4</span><span class="sxs-lookup"><span data-stu-id="18589-137">4</span></span> |<span data-ttu-id="18589-138">SAS LEDs</span><span class="sxs-lookup"><span data-stu-id="18589-138">SAS LEDs</span></span> |
   | <span data-ttu-id="18589-139">5</span><span class="sxs-lookup"><span data-stu-id="18589-139">5</span></span> |<span data-ttu-id="18589-140">Portas série fábrica apenas para utilização</span><span class="sxs-lookup"><span data-stu-id="18589-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="18589-141">6</span><span class="sxs-lookup"><span data-stu-id="18589-141">6</span></span> |<span data-ttu-id="18589-142">Porta (anfitrião do)</span><span class="sxs-lookup"><span data-stu-id="18589-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="18589-143">7</span><span class="sxs-lookup"><span data-stu-id="18589-143">7</span></span> |<span data-ttu-id="18589-144">Porta B (anfitrião de saída)</span><span class="sxs-lookup"><span data-stu-id="18589-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="18589-145">8</span><span class="sxs-lookup"><span data-stu-id="18589-145">8</span></span> |<span data-ttu-id="18589-146">Porta C (apenas para utilização de fábrica)</span><span class="sxs-lookup"><span data-stu-id="18589-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="18589-147">Instalar um novo controlador EBOD</span><span class="sxs-lookup"><span data-stu-id="18589-147">Install a new EBOD controller</span></span>
<span data-ttu-id="18589-148">Olá procedimento e tabela seguintes explicam como tooinstall um módulo de controlador EBOD no dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="18589-148">hello following procedure and table explain how tooinstall an EBOD controller module in your StorSimple device.</span></span>

#### <a name="tooinstall-an-ebod-controller"></a><span data-ttu-id="18589-149">tooinstall um controlador EBOD</span><span class="sxs-lookup"><span data-stu-id="18589-149">tooinstall an EBOD controller</span></span>
1. <span data-ttu-id="18589-150">Verifique o dispositivo EBOD Olá para danos, especialmente toohello conector de interface.</span><span class="sxs-lookup"><span data-stu-id="18589-150">Check hello EBOD device for damage, especially toohello interface connector.</span></span> <span data-ttu-id="18589-151">Não instale o novo controlador de EBOD Olá se qualquer pins são bent.</span><span class="sxs-lookup"><span data-stu-id="18589-151">Do not install hello new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="18589-152">Com as bloqueios simultâneos de Olá no Olá abra posição, o módulo de Olá gradualmente no bastidor Olá até os bloqueios simultâneos de Olá envolvimento.</span><span class="sxs-lookup"><span data-stu-id="18589-152">With hello latches in hello open position, slide hello module into hello enclosure until hello latches engage.</span></span>
   
    ![Instalar o controlador de EBOD](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="18589-154">**Figura 2** módulo de controlador instalar Olá EBOD</span><span class="sxs-lookup"><span data-stu-id="18589-154">**Figure 2**  Installing hello EBOD controller module</span></span>
3. <span data-ttu-id="18589-155">Bloqueio temporário de Olá fechar.</span><span class="sxs-lookup"><span data-stu-id="18589-155">Close hello latch.</span></span> <span data-ttu-id="18589-156">Deve ouvir um clique como bloqueio temporário de Olá envolva.</span><span class="sxs-lookup"><span data-stu-id="18589-156">You should hear a click as hello latch engages.</span></span>
   
    ![Ao libertar o bloqueio temporário EBOD](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="18589-158">**Figura 3** fechar bloqueio temporário do módulo EBOD Olá</span><span class="sxs-lookup"><span data-stu-id="18589-158">**Figure 3**  Closing hello EBOD module latch</span></span>
4. <span data-ttu-id="18589-159">Restabeleça a ligação de cabos de Olá.</span><span class="sxs-lookup"><span data-stu-id="18589-159">Reconnect hello cables.</span></span> <span data-ttu-id="18589-160">Utilize a configuração exata de Olá que estava presente antes de substituição de Olá.</span><span class="sxs-lookup"><span data-stu-id="18589-160">Use hello exact configuration that was present before hello replacement.</span></span> <span data-ttu-id="18589-161">Consulte Olá diagrama a seguir e na tabela para obter detalhes sobre como os cabos de Olá tooconnect.</span><span class="sxs-lookup"><span data-stu-id="18589-161">See hello following diagram and table for details about how tooconnect hello cables.</span></span>
   
    ![Instalar os cabos do dispositivo 4U de energia](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="18589-163">**Figura 4**.</span><span class="sxs-lookup"><span data-stu-id="18589-163">**Figure 4**.</span></span> <span data-ttu-id="18589-164">Cabos de restabelecer a ligação</span><span class="sxs-lookup"><span data-stu-id="18589-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="18589-165">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="18589-165">Label</span></span> | <span data-ttu-id="18589-166">Descrição</span><span class="sxs-lookup"><span data-stu-id="18589-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="18589-167">1</span><span class="sxs-lookup"><span data-stu-id="18589-167">1</span></span> |<span data-ttu-id="18589-168">Inclusão principal</span><span class="sxs-lookup"><span data-stu-id="18589-168">Primary enclosure</span></span> |
   | <span data-ttu-id="18589-169">2</span><span class="sxs-lookup"><span data-stu-id="18589-169">2</span></span> |<span data-ttu-id="18589-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="18589-170">PCM 0</span></span> |
   | <span data-ttu-id="18589-171">3</span><span class="sxs-lookup"><span data-stu-id="18589-171">3</span></span> |<span data-ttu-id="18589-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="18589-172">PCM 1</span></span> |
   | <span data-ttu-id="18589-173">4</span><span class="sxs-lookup"><span data-stu-id="18589-173">4</span></span> |<span data-ttu-id="18589-174">Controlador 0</span><span class="sxs-lookup"><span data-stu-id="18589-174">Controller 0</span></span> |
   | <span data-ttu-id="18589-175">5</span><span class="sxs-lookup"><span data-stu-id="18589-175">5</span></span> |<span data-ttu-id="18589-176">Controlador 1</span><span class="sxs-lookup"><span data-stu-id="18589-176">Controller 1</span></span> |
   | <span data-ttu-id="18589-177">6</span><span class="sxs-lookup"><span data-stu-id="18589-177">6</span></span> |<span data-ttu-id="18589-178">Controlador EBOD 0</span><span class="sxs-lookup"><span data-stu-id="18589-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="18589-179">7</span><span class="sxs-lookup"><span data-stu-id="18589-179">7</span></span> |<span data-ttu-id="18589-180">Controlador EBOD 1</span><span class="sxs-lookup"><span data-stu-id="18589-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="18589-181">8</span><span class="sxs-lookup"><span data-stu-id="18589-181">8</span></span> |<span data-ttu-id="18589-182">Inclusão EBOD</span><span class="sxs-lookup"><span data-stu-id="18589-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="18589-183">9</span><span class="sxs-lookup"><span data-stu-id="18589-183">9</span></span> |<span data-ttu-id="18589-184">Unidades de distribuição de energia</span><span class="sxs-lookup"><span data-stu-id="18589-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="18589-185">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="18589-185">Next steps</span></span>
<span data-ttu-id="18589-186">Saiba mais sobre [substituição de componente de hardware do StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="18589-186">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

