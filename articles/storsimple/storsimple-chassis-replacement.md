---
title: "chassis de aaaReplace no dispositivo de série 8000 do StorSimple | Microsoft Docs"
description: "Descreve como tooremove e substitua Olá chassis para o seu inclusão principal do StorSimple ou a inclusão EBOD."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 537659ed-4c46-49c1-b1e4-186262f2542d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: f8576d63520a6f7d3267180d2a68d4fc38fd48fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a><span data-ttu-id="0af23-103">Substitua o chassis Olá no dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="0af23-103">Replace hello chassis on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="0af23-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="0af23-104">Overview</span></span>
<span data-ttu-id="0af23-105">Este tutorial explica como tooremove e substituir um chassis de um dispositivo de série 8000 do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0af23-105">This tutorial explains how tooremove and replace a chassis in a StorSimple 8000 series device.</span></span> <span data-ttu-id="0af23-106">modelo de Olá StorSimple 8100 é um dispositivo de inclusão único (chassis), enquanto Olá 8600 é um dispositivo de inclusão dupla (dois chassis).</span><span class="sxs-lookup"><span data-stu-id="0af23-106">hello StorSimple 8100 model is a single enclosure device (one chassis), whereas hello 8600 is a dual enclosure device (two chassis).</span></span> <span data-ttu-id="0af23-107">Para um modelo de 8600, existem dois chassis potencialmente poderá falhar num dispositivo Olá: Olá chassis para inclusão principal Olá ou chassis Olá para Olá bastidor EBOD.</span><span class="sxs-lookup"><span data-stu-id="0af23-107">For an 8600 model, there are potentially two chassis that could fail in hello device: hello chassis for hello primary enclosure or hello chassis for hello EBOD enclosure.</span></span>

<span data-ttu-id="0af23-108">Em ambos os casos, o chassis de substituição de Olá que é enviada pela Microsoft está vazio.</span><span class="sxs-lookup"><span data-stu-id="0af23-108">In either case, hello replacement chassis that is shipped by Microsoft is empty.</span></span> <span data-ttu-id="0af23-109">Sem energia e arrefecimento módulos do (PCMs), módulos de controlador, unidades de disco de estado sólido (SSDs), unidades de disco rígido (HDDs) ou EBOD módulos será incluídos.</span><span class="sxs-lookup"><span data-stu-id="0af23-109">No Power and Cooling Modules (PCMs), controller modules, solid state disk drives (SSDs), hard disk drives (HDDs), or EBOD modules will be included.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0af23-110">Antes de remover e de substituir chassis Olá, reveja as informações de segurança de Olá na [substituição de componente de hardware do StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="0af23-110">Before removing and replacing hello chassis, review hello safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-hello-chassis"></a><span data-ttu-id="0af23-111">Remover chassis Olá</span><span class="sxs-lookup"><span data-stu-id="0af23-111">Remove hello chassis</span></span>
<span data-ttu-id="0af23-112">Efetue Olá chassis de Olá tooremove de passos a seguir no dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0af23-112">Perform hello following steps tooremove hello chassis on your StorSimple device.</span></span>

#### <a name="tooremove-a-chassis"></a><span data-ttu-id="0af23-113">tooremove um chassis</span><span class="sxs-lookup"><span data-stu-id="0af23-113">tooremove a chassis</span></span>
1. <span data-ttu-id="0af23-114">Certifique-se de que o dispositivo StorSimple Olá é encerrado e desligado de todas as fontes de alimentação Olá.</span><span class="sxs-lookup"><span data-stu-id="0af23-114">Make sure that hello StorSimple device is shut down and disconnected from all hello power sources.</span></span>
2. <span data-ttu-id="0af23-115">Remova todos os rede Olá e cabos SAS, se aplicável.</span><span class="sxs-lookup"><span data-stu-id="0af23-115">Remove all hello network and SAS cables, if applicable.</span></span>
3. <span data-ttu-id="0af23-116">Remova unidade de Olá bastidor Olá.</span><span class="sxs-lookup"><span data-stu-id="0af23-116">Remove hello unit from hello rack.</span></span>
4. <span data-ttu-id="0af23-117">Remova a cada uma das unidades de Olá e tenha em atenção as ranhuras Olá partir da qual são removidos.</span><span class="sxs-lookup"><span data-stu-id="0af23-117">Remove each of hello drives and note hello slots from which they are removed.</span></span> <span data-ttu-id="0af23-118">Para obter mais informações, consulte [remover a unidade de disco Olá](storsimple-disk-drive-replacement.md#remove-the-disk-drive).</span><span class="sxs-lookup"><span data-stu-id="0af23-118">For more information, see [Remove hello disk drive](storsimple-disk-drive-replacement.md#remove-the-disk-drive).</span></span>
5. <span data-ttu-id="0af23-119">Remova Olá bastidor EBOD (se se tratar de chassis Olá que falharam), módulos de controlador Olá EBOD.</span><span class="sxs-lookup"><span data-stu-id="0af23-119">On hello EBOD enclosure (if this is hello chassis that failed), remove hello EBOD controller modules.</span></span> <span data-ttu-id="0af23-120">Para obter mais informações, consulte [remover um controlador EBOD](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller).</span><span class="sxs-lookup"><span data-stu-id="0af23-120">For more information, see [Remove an EBOD controller](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller).</span></span> 
   
    <span data-ttu-id="0af23-121">Olá inclusão principal (se se tratar de chassis Olá que falharam), remover controladores de Olá e tenha em atenção as ranhuras Olá partir da qual são removidos.</span><span class="sxs-lookup"><span data-stu-id="0af23-121">On hello primary enclosure (if this is hello chassis that failed), remove hello controllers and note hello slots from which they are removed.</span></span> <span data-ttu-id="0af23-122">Para obter mais informações, consulte [remover um controlador](storsimple-controller-replacement.md#remove-a-controller).</span><span class="sxs-lookup"><span data-stu-id="0af23-122">For more information, see [Remove a controller](storsimple-controller-replacement.md#remove-a-controller).</span></span>

## <a name="install-hello-chassis"></a><span data-ttu-id="0af23-123">Instalar o chassis Olá</span><span class="sxs-lookup"><span data-stu-id="0af23-123">Install hello chassis</span></span>
<span data-ttu-id="0af23-124">Efetue Olá chassis de Olá tooinstall de passos a seguir no dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0af23-124">Perform hello following steps tooinstall hello chassis on your StorSimple device.</span></span>

#### <a name="tooinstall-a-chassis"></a><span data-ttu-id="0af23-125">tooinstall um chassis</span><span class="sxs-lookup"><span data-stu-id="0af23-125">tooinstall a chassis</span></span>
1. <span data-ttu-id="0af23-126">Chassis de Olá num bastidor Olá de montagem.</span><span class="sxs-lookup"><span data-stu-id="0af23-126">Mount hello chassis in hello rack.</span></span> <span data-ttu-id="0af23-127">Para obter mais informações, consulte [montar em Bastidor os cabos do 8100 StorSimple dispositivo](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) ou [montar em Bastidor os cabos do 8600 StorSimple dispositivo](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="0af23-127">For more information, see [Rack-mount your StorSimple 8100 device](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) or [Rack-mount your StorSimple 8600 device](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span></span>
2. <span data-ttu-id="0af23-128">Depois de chassis Olá está montado num bastidor Olá, instale módulos de controlador Olá Olá posições mesmo tenham sido anteriormente instalados no.</span><span class="sxs-lookup"><span data-stu-id="0af23-128">After hello chassis is mounted in hello rack, install hello controller modules in hello same positions that they were previously installed in.</span></span>
3. <span data-ttu-id="0af23-129">Instalação Olá unidades no Olá mesmo posições e ranhuras que anteriormente foram instalados no.</span><span class="sxs-lookup"><span data-stu-id="0af23-129">Install hello drives in hello same positions and slots that they were previously installed in.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0af23-130">Recomendamos que instale Olá SSDs no ranhuras Olá primeiro e, em seguida, instale Olá HDDs.</span><span class="sxs-lookup"><span data-stu-id="0af23-130">We recommend that you install hello SSDs in hello slots first, and then install hello HDDs.</span></span>
   > 
   > 
4. <span data-ttu-id="0af23-131">Com Olá dispositivo montado num bastidor Olá e componentes de Olá instalados, ligar as fontes de alimentação adequada de toohello do dispositivo e ativar Olá de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="0af23-131">With hello device mounted in hello rack and hello components installed, connect your device toohello appropriate power sources, and turn on hello device.</span></span> <span data-ttu-id="0af23-132">Para obter mais informações, consulte [instalar os cabos do dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) ou [instalar os cabos do dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="0af23-132">For details, see [Cable your StorSimple 8100 device](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) or [Cable your StorSimple 8600 device](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0af23-133">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0af23-133">Next steps</span></span>
<span data-ttu-id="0af23-134">Saiba mais sobre [substituição de componente de hardware do StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="0af23-134">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

