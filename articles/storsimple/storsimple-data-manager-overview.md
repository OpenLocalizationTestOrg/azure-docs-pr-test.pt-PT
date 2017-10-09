---
title: "Descrição geral do Gestor de dados do Azure StorSimple aaaMicrosoft | Microsoft Docs"
description: "Fornece uma descrição geral de Olá serviço StorSimple Manager de dados (pré-visualização privada)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 5d29f7d26be9f2b36857526bdea770d991cece6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a><span data-ttu-id="08229-103">Descrição geral do Gestor de dados do StorSimple (pré-visualização privada)</span><span class="sxs-lookup"><span data-stu-id="08229-103">StorSimple Data Manager overview (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="08229-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="08229-104">Overview</span></span>

<span data-ttu-id="08229-105">Microsoft Azure StorSimple é uma solução de armazenamento de nuvem híbrida endereços Olá complexidades de dados não estruturados normalmente associadas a partilhas de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="08229-105">Microsoft Azure StorSimple is a hybrid cloud storage solution that addresses hello complexities of unstructured data commonly associated with file shares.</span></span> <span data-ttu-id="08229-106">StorSimple utiliza armazenamento na nuvem como uma extensão de Olá solução no local e automaticamente as camadas de dados através de armazenamento do Olá no local e na nuvem.</span><span class="sxs-lookup"><span data-stu-id="08229-106">StorSimple uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="08229-107">Integrado proteção de dados no local e na nuvem instantâneos, elimina a necessidade de Olá de uma infraestrutura de armazenamento sprawling.</span><span class="sxs-lookup"><span data-stu-id="08229-107">Integrated data protection, with local and cloud snapshots, eliminates hello need for a sprawling storage infrastructure.</span></span> <span data-ttu-id="08229-108">Arquivo e recuperação após desastre é também totalmente integrada com a nuvem Olá a agir como uma localização fora das instalações.</span><span class="sxs-lookup"><span data-stu-id="08229-108">Archival and disaster recovery is also seamless with hello cloud acting as an offsite location.</span></span>

<span data-ttu-id="08229-109">serviço de transformação de dados Olá que iremos introduzir neste documento, permite-lhe tooseamlessly acesso Olá StorSimple dados na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="08229-109">hello data transformation service that we are introducing in this document, allows you tooseamlessly access hello StorSimple data in hello cloud.</span></span> <span data-ttu-id="08229-110">Este serviço fornece dados de tooextract APIs do StorSimple e apresente-tooother Azure serviços nos formatos que podem ser prontamente consumidos.</span><span class="sxs-lookup"><span data-stu-id="08229-110">This service provides APIs tooextract data from StorSimple and present it tooother Azure services in formats that can be readily consumed.</span></span> <span data-ttu-id="08229-111">formatos de Olá suportados nesta pré-visualização são blobs do Azure e os recursos de Media Services do Azure.</span><span class="sxs-lookup"><span data-stu-id="08229-111">hello formats supported in this preview are Azure blobs and Azure Media Services assets.</span></span> <span data-ttu-id="08229-112">Esta transformação permite-lhe tooeasily durante a transmissão dos serviços, tais como dados de toooperate Media Services do Azure, Azure HDInsight, do Azure Machine Learning e da Azure Search no dispositivo de no local de série 8000 do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="08229-112">This transformation enables you tooeasily wire up services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search toooperate data on StorSimple 8000 series on-premises device.</span></span>

<span data-ttu-id="08229-113">Um diagrama de blocos de alto nível que ilustra isto é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="08229-113">A high-level block diagram illustrating this is shown below.</span></span>

![Diagrama de alto nível](./media//storsimple-data-manager-overview/high-level-diagram.png)

<span data-ttu-id="08229-115">Este documento explica como pode inscrever para uma versão de pré-visualização privada deste serviço.</span><span class="sxs-lookup"><span data-stu-id="08229-115">This document explains how you can sign up for a private preview of this service.</span></span> <span data-ttu-id="08229-116">Também explica como pode utilizar aplicações de toowrite este serviço que utilizam dados StorSimple e outros serviços do Azure na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="08229-116">It also explains how you can use this service toowrite applications that use StorSimple data and other Azure services in hello cloud.</span></span>

## <a name="sign-up-for-data-manager-preview"></a><span data-ttu-id="08229-117">Inscrever-se para a pré-visualização do Gestor de dados</span><span class="sxs-lookup"><span data-stu-id="08229-117">Sign up for Data Manager preview</span></span>
<span data-ttu-id="08229-118">Antes de se inscrever no serviço do Gestor de dados de Olá, reveja Olá os seguintes pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="08229-118">Before you sign up for hello Data Manager service, review hello following prerequisites.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="08229-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="08229-119">Prerequisites</span></span>

<span data-ttu-id="08229-120">Neste exercício parte do princípio de que tem</span><span class="sxs-lookup"><span data-stu-id="08229-120">This exercise assumes that you have</span></span>
* <span data-ttu-id="08229-121">Uma subscrição do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="08229-121">an active Azure subscription.</span></span>
* <span data-ttu-id="08229-122">acesso tooa registado o dispositivo de série 8000 do StorSimple</span><span class="sxs-lookup"><span data-stu-id="08229-122">access tooa registered StorSimple 8000 series device</span></span>
* <span data-ttu-id="08229-123">Olá todas as chaves associadas ao dispositivo de série de Olá 8000 do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="08229-123">all hello keys associated with hello StorSimple 8000 series device.</span></span>

### <a name="sign-up"></a><span data-ttu-id="08229-124">Inscrever-se</span><span class="sxs-lookup"><span data-stu-id="08229-124">Sign up</span></span>

<span data-ttu-id="08229-125">Olá StorSimple Manager de dados está em pré-visualização privada.</span><span class="sxs-lookup"><span data-stu-id="08229-125">hello StorSimple Data Manager is in private preview.</span></span> <span data-ttu-id="08229-126">Execute Olá toosign passos para uma versão de pré-visualização privada deste serviço os seguintes:</span><span class="sxs-lookup"><span data-stu-id="08229-126">Perform hello following steps toosign up for a private preview of this service:</span></span>

1.  <span data-ttu-id="08229-127">Inicie sessão no Olá portal do Azure com a extensão do Gestor de dados do StorSimple Olá em: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span><span class="sxs-lookup"><span data-stu-id="08229-127">Log into hello Azure portal with hello StorSimple Data Manager extension at: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span></span> <span data-ttu-id="08229-128">Utilize o toolog de credenciais do Azure no.</span><span class="sxs-lookup"><span data-stu-id="08229-128">Use your Azure credentials toolog in.</span></span>

2.  <span data-ttu-id="08229-129">Clique em Olá  **+**  ícone toocreate um serviço.</span><span class="sxs-lookup"><span data-stu-id="08229-129">Click hello **+** icon toocreate a service.</span></span> <span data-ttu-id="08229-130">Clique em **armazenamento** e, em seguida, clique em **ver todos os** no painel de Olá que se abre.</span><span class="sxs-lookup"><span data-stu-id="08229-130">Click **Storage** and then click **See All** in hello blade that opens up.</span></span>

    ![Ícone de Gestor de dados do StorSimple pesquisa](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. <span data-ttu-id="08229-132">Pode ver o ícone de Gestor de dados do StorSimple Olá.</span><span class="sxs-lookup"><span data-stu-id="08229-132">You see hello StorSimple Data Manager icon.</span></span>

    ![Selecione o ícone do Gestor de dados do StorSimple](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. <span data-ttu-id="08229-134">Clique em Gestor de dados do StorSimple ícone e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="08229-134">Click StorSimple Data Manager icon and then click **Create**.</span></span> <span data-ttu-id="08229-135">Escolha a subscrição de Olá que pretende tooenable para pré-visualização privada Olá e, em seguida, clique em **inscrever-me!**</span><span class="sxs-lookup"><span data-stu-id="08229-135">Pick hello subscription that you want tooenable for hello private preview and then click **Sign me up!**</span></span>

    ![Inscrever-me](./media/storsimple-data-manager-overview/sign-me-up.png)

5. <span data-ttu-id="08229-137">Esta ação envia um pedido tooonboard.</span><span class="sxs-lookup"><span data-stu-id="08229-137">This sends a request tooonboard you.</span></span> <span data-ttu-id="08229-138">Iremos carregar, logo que possível.</span><span class="sxs-lookup"><span data-stu-id="08229-138">We will onboard you as soon as possible.</span></span> <span data-ttu-id="08229-139">Depois de ativar a sua subscrição, pode criar um serviço StorSimple Manager de dados.</span><span class="sxs-lookup"><span data-stu-id="08229-139">After your subscription is enabled, you can create a StorSimple Data Manager service.</span></span>

6. <span data-ttu-id="08229-140">tooeasily aceder ao serviço StorSimple Manager de dados Olá, clique em Olá ícone de estrela toopin-tooyour Favoritos.</span><span class="sxs-lookup"><span data-stu-id="08229-140">tooeasily access hello StorSimple Data Manager service, click hello star icon toopin it tooyour favorites.</span></span>

    ![Gestores de dados do StorSimple de acesso](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a><span data-ttu-id="08229-142">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="08229-142">Next steps</span></span>

<span data-ttu-id="08229-143">[Utilize a IU do Gestor de dados de StorSimple tootransform os dados](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="08229-143">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
