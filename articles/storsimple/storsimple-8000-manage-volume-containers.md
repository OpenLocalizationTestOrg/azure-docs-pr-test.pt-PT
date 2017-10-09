---
title: "aaaManage os contentores de volume do StorSimple no dispositivo de série de Olá 8000 do StorSimple | Microsoft Docs"
description: "Explica como pode utilizar Olá Gestor de dispositivos do StorSimple contentores de volume do serviço página tooadd, modificarem ou eliminar um contentor de volume."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="05dff-103">Utilize contentores de volume de StorSimple serviço toomanage Olá Gestor de dispositivos do StorSimple</span><span class="sxs-lookup"><span data-stu-id="05dff-103">Use hello StorSimple Device Manager service toomanage StorSimple volume containers</span></span>

## <a name="overview"></a><span data-ttu-id="05dff-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="05dff-104">Overview</span></span>
<span data-ttu-id="05dff-105">Este tutorial explica como toouse Olá toocreate de serviço do Gestor de dispositivos do StorSimple e gerir contentores de volume do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="05dff-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="05dff-106">Um contentor de volume no dispositivo Microsoft Azure StorSimple contém um ou mais volumes que partilham a conta de armazenamento, a encriptação e definições de consumo de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="05dff-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="05dff-107">Um dispositivo pode ter vários contentores de volume para todos os seus volumes.</span><span class="sxs-lookup"><span data-stu-id="05dff-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="05dff-108">Um contentor de volume possui Olá seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="05dff-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="05dff-109">**Volumes** – Olá camadas ou afixado localmente volumes do StorSimple que estão contidas dentro do contentor de volume Olá.</span><span class="sxs-lookup"><span data-stu-id="05dff-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> 
* <span data-ttu-id="05dff-110">**Encriptação** – uma chave de encriptação pode ser definida para cada contentor de volume.</span><span class="sxs-lookup"><span data-stu-id="05dff-110">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="05dff-111">Esta chave é utilizada para encriptar dados Olá que são enviados a partir da nuvem toohello dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="05dff-111">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="05dff-112">Uma chave do nível military AES 256 bits é utilizada com a chave de utilizador introduzido Olá.</span><span class="sxs-lookup"><span data-stu-id="05dff-112">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="05dff-113">toosecure os dados, recomendamos que ativar sempre a encriptação de armazenamento de nuvem.</span><span class="sxs-lookup"><span data-stu-id="05dff-113">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="05dff-114">**Conta de armazenamento** – Olá conta de armazenamento do Azure que seja utilizado toostore Olá dados.</span><span class="sxs-lookup"><span data-stu-id="05dff-114">**Storage account** – hello Azure storage account that is used toostore hello data.</span></span> <span data-ttu-id="05dff-115">Todos os volumes de Olá que residem num contentor de volume partilham esta conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="05dff-115">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="05dff-116">Pode escolher uma conta de armazenamento a partir de uma lista existente ou crie uma nova conta ao criar o contentor de volume Olá e, em seguida, especifique as credenciais de acesso de Olá para essa conta.</span><span class="sxs-lookup"><span data-stu-id="05dff-116">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="05dff-117">**Largura de banda da nuvem** – Olá largura de banda consumida pelo dispositivo Olá quando estão a ser enviados dados de Olá de dispositivo Olá toohello nuvem.</span><span class="sxs-lookup"><span data-stu-id="05dff-117">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="05dff-118">Pode impor um controlo de largura de banda, especificando um valor entre 1 e 1000 Mbps quando cria este contentor.</span><span class="sxs-lookup"><span data-stu-id="05dff-118">You can enforce a bandwidth control by specifying a value between 1 Mbps and 1,000 Mbps when you create this container.</span></span> <span data-ttu-id="05dff-119">Se quiser Olá dispositivo tooconsume largura de banda disponível, defina este campo demasiado**ilimitada**.</span><span class="sxs-lookup"><span data-stu-id="05dff-119">If you want hello device tooconsume all available bandwidth, set this field too**Unlimited**.</span></span> <span data-ttu-id="05dff-120">Também pode criar e aplicar uma largura de banda modelo tooallocate da largura de banda com base numa agenda.</span><span class="sxs-lookup"><span data-stu-id="05dff-120">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

<span data-ttu-id="05dff-121">Olá procedimentos seguintes explicam como toouse Olá StorSimple **contentores de Volume** Olá do painel toocomplete seguintes operações comuns:</span><span class="sxs-lookup"><span data-stu-id="05dff-121">hello following procedures explain how toouse hello StorSimple **Volume containers** blade toocomplete hello following common operations:</span></span>

* <span data-ttu-id="05dff-122">Adicionar um contentor de volume</span><span class="sxs-lookup"><span data-stu-id="05dff-122">Add a volume container</span></span>
* <span data-ttu-id="05dff-123">Modificar um contentor de volume</span><span class="sxs-lookup"><span data-stu-id="05dff-123">Modify a volume container</span></span>
* <span data-ttu-id="05dff-124">Eliminar um contentor de volume</span><span class="sxs-lookup"><span data-stu-id="05dff-124">Delete a volume container</span></span>

## <a name="add-a-volume-container"></a><span data-ttu-id="05dff-125">Adicionar um contentor de volume</span><span class="sxs-lookup"><span data-stu-id="05dff-125">Add a volume container</span></span>
<span data-ttu-id="05dff-126">Efetue Olá os seguintes passos tooadd um contentor de volume.</span><span class="sxs-lookup"><span data-stu-id="05dff-126">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="05dff-127">Modificar um contentor de volume</span><span class="sxs-lookup"><span data-stu-id="05dff-127">Modify a volume container</span></span>
<span data-ttu-id="05dff-128">Efetue Olá os seguintes passos toomodify um contentor de volume.</span><span class="sxs-lookup"><span data-stu-id="05dff-128">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="05dff-129">Eliminar um contentor de volume</span><span class="sxs-lookup"><span data-stu-id="05dff-129">Delete a volume container</span></span>
<span data-ttu-id="05dff-130">Um contentor de volume possui volumes dentro do mesmo.</span><span class="sxs-lookup"><span data-stu-id="05dff-130">A volume container has volumes within it.</span></span> <span data-ttu-id="05dff-131">Pode ser eliminado apenas se todos os volumes de Olá nele contidos são eliminados primeiro.</span><span class="sxs-lookup"><span data-stu-id="05dff-131">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="05dff-132">Efetue Olá os seguintes passos toodelete um contentor de volume.</span><span class="sxs-lookup"><span data-stu-id="05dff-132">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="05dff-133">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="05dff-133">Next steps</span></span>
* <span data-ttu-id="05dff-134">Saiba mais sobre [gerir volumes do StorSimple](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="05dff-134">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span> 
* <span data-ttu-id="05dff-135">Saiba mais sobre [utilizando Olá tooadminister de serviço do Gestor de dispositivos do StorSimple com o dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="05dff-135">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

