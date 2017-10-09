---
title: "Atualizações aaaInstall numa matriz Virtual StorSimple | Microsoft Docs"
description: "Descreve como toouse Olá matriz Virtual StorSimple web IU tooapply atualizações através do método de portal e correção de Olá"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7f1b1e7d-04d0-4ca2-9dbb-77077ff19bb9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/07/2016
ms.author: alkohli
ms.openlocfilehash: 10af0f52abb75a5b41562704194157f0d35710bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a><span data-ttu-id="ba65b-103">Instalar atualizações na sua matriz de Virtual StorSimple</span><span class="sxs-lookup"><span data-stu-id="ba65b-103">Install Updates on your StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="ba65b-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="ba65b-104">Overview</span></span>
<span data-ttu-id="ba65b-105">Este artigo descreve Olá passos tooinstall necessárias atualizações na sua matriz Virtual StorSimple através da IU da web local Olá e via Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba65b-105">This article describes hello steps required tooinstall updates on your StorSimple Virtual Array via hello local web UI and via hello Azure classic portal.</span></span> <span data-ttu-id="ba65b-106">É necessário tooapply software tookeep atualizações ou correções a matriz de Virtual StorSimple atualizado.</span><span class="sxs-lookup"><span data-stu-id="ba65b-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="ba65b-107">Tenha em atenção que a instalar uma atualização ou correção reinicia o seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ba65b-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="ba65b-108">Dado que Olá matriz Virtual StorSimple é um dispositivo de nó único, qualquer e/s em curso é interrompido e período de indisponibilidade ocorre com o seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ba65b-108">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="ba65b-109">Antes de aplicar uma atualização, recomendamos que tome volumes Olá ou partilhas offline no Olá alojam primeiro e, em seguida, Olá dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ba65b-109">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="ba65b-110">Isto minimiza qualquer possibilidade de danos nos dados.</span><span class="sxs-lookup"><span data-stu-id="ba65b-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba65b-111">Se estiver a executar a atualização 0.1 ou versões de software DG, tem de utilizar o método de correção Olá através de Olá local web IU tooinstall atualização 0.3.</span><span class="sxs-lookup"><span data-stu-id="ba65b-111">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall update 0.3.</span></span> <span data-ttu-id="ba65b-112">Se estiver a executar a atualização 0,2, recomendamos que instale as atualizações de Olá através de Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba65b-112">If you are running Update 0.2, we recommend that you install hello updates via hello Azure classic portal.</span></span>
> 
> 

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="ba65b-113">Utilize Olá local IU da web</span><span class="sxs-lookup"><span data-stu-id="ba65b-113">Use hello local web UI</span></span>
<span data-ttu-id="ba65b-114">Existem dois passos, ao utilizar a IU da web local Olá:</span><span class="sxs-lookup"><span data-stu-id="ba65b-114">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="ba65b-115">Transferir a atualização de Olá ou da correção de Olá</span><span class="sxs-lookup"><span data-stu-id="ba65b-115">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="ba65b-116">Instalar a atualização de Olá ou da correção de Olá</span><span class="sxs-lookup"><span data-stu-id="ba65b-116">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="ba65b-117">Transferir a atualização de Olá ou da correção de Olá</span><span class="sxs-lookup"><span data-stu-id="ba65b-117">Download hello update or hello hotfix</span></span>
<span data-ttu-id="ba65b-118">Efetue Olá seguintes passos toodownload Olá atualização de software de Olá catálogo Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="ba65b-118">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="ba65b-119">toodownload Olá Olá de atualização ou correção</span><span class="sxs-lookup"><span data-stu-id="ba65b-119">toodownload hello update or hello hotfix</span></span>
1. <span data-ttu-id="ba65b-120">Inicie o Internet Explorer e navegue demasiado[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ba65b-120">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="ba65b-121">Se esta for a primeira vez utilizando Olá catálogo Microsoft Update neste computador, clique em **instalar** quando pedido tooinstall hello do suplemento do catálogo Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="ba65b-121">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
3. <span data-ttu-id="ba65b-122">Na caixa de pesquisa de Olá de Olá catálogo Microsoft Update, introduza o número de Base de dados de conhecimento (KB) Olá de correção de Olá que pretende toodownload.</span><span class="sxs-lookup"><span data-stu-id="ba65b-122">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="ba65b-123">Introduza **3182061** para atualização 0.3 e, em seguida, clique em **pesquisa**.</span><span class="sxs-lookup"><span data-stu-id="ba65b-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="ba65b-124">Olá listagem de correção é apresentado, por exemplo, **StorSimple Virtual matriz atualização 0.3**.</span><span class="sxs-lookup"><span data-stu-id="ba65b-124">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![Catálogo de pesquisa](./media/storsimple-ova-install-update-01/download1.png)
4. <span data-ttu-id="ba65b-126">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ba65b-126">Click **Add**.</span></span> <span data-ttu-id="ba65b-127">atualização de Olá está adicionada toohello cesto.</span><span class="sxs-lookup"><span data-stu-id="ba65b-127">hello update is added toohello basket.</span></span>
5. <span data-ttu-id="ba65b-128">Clique em **Ver Cesto**.</span><span class="sxs-lookup"><span data-stu-id="ba65b-128">Click **View Basket**.</span></span>
6. <span data-ttu-id="ba65b-129">Clique em **Transferir**.</span><span class="sxs-lookup"><span data-stu-id="ba65b-129">Click **Download**.</span></span> <span data-ttu-id="ba65b-130">Especifique ou **procurar** tooa localização local onde pretende Olá transfere tooappear.</span><span class="sxs-lookup"><span data-stu-id="ba65b-130">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="ba65b-131">Olá as atualizações são transferidas toohello especificada a localização e colocada numa subpasta com o mesmo nome como atualização Olá de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba65b-131">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="ba65b-132">pasta de Olá também pode ser copiado tooa partilha de rede que seja acessível a partir do dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="ba65b-132">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>
7. <span data-ttu-id="ba65b-133">Abra Olá copiados pasta, deverá ver um ficheiro de pacote do Microsoft Update autónomo `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="ba65b-133">Open hello copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="ba65b-134">Este ficheiro é utilizado tooinstall Olá atualização ou correção.</span><span class="sxs-lookup"><span data-stu-id="ba65b-134">This file is used tooinstall hello update or hotfix.</span></span>

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="ba65b-135">Instalar a atualização de Olá ou da correção de Olá</span><span class="sxs-lookup"><span data-stu-id="ba65b-135">Install hello update or hello hotfix</span></span>
<span data-ttu-id="ba65b-136">Instalação de atualização ou correção toohello anterior, certifique-se de que tem Olá atualização ou correção de Olá transferido localmente no seu anfitrião ou acessível através de uma partilha de rede.</span><span class="sxs-lookup"><span data-stu-id="ba65b-136">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="ba65b-137">Utilizar atualizações de tooinstall este método num dispositivo com GA ou atualização 0.1 versões de software.</span><span class="sxs-lookup"><span data-stu-id="ba65b-137">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="ba65b-138">Este procedimento assume inferior toocomplete de 2 minutos.</span><span class="sxs-lookup"><span data-stu-id="ba65b-138">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="ba65b-139">Execute o seguinte Olá passos tooinstall Olá atualização ou correção.</span><span class="sxs-lookup"><span data-stu-id="ba65b-139">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="ba65b-140">tooinstall Olá atualização ou correção de Olá</span><span class="sxs-lookup"><span data-stu-id="ba65b-140">tooinstall hello update or hello hotfix</span></span>
1. <span data-ttu-id="ba65b-141">Olá local IU da web, aceda demasiado**manutenção** > **atualização de Software**.</span><span class="sxs-lookup"><span data-stu-id="ba65b-141">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![atualizar o dispositivo](./media/storsimple-ova-install-update-01/update1m.png)
2. <span data-ttu-id="ba65b-143">No **caminho do ficheiro de atualização**, introduza o nome de ficheiro Olá para atualização Olá ou Olá correção.</span><span class="sxs-lookup"><span data-stu-id="ba65b-143">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="ba65b-144">Também pode procurar ficheiro de instalação de atualização ou correção toohello se colocado numa partilha de rede.</span><span class="sxs-lookup"><span data-stu-id="ba65b-144">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="ba65b-145">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="ba65b-145">Click **Apply**.</span></span>
   
    ![atualizar o dispositivo](./media/storsimple-ova-install-update-01/update2m.png)
3. <span data-ttu-id="ba65b-147">É apresentado um aviso.</span><span class="sxs-lookup"><span data-stu-id="ba65b-147">A warning is displayed.</span></span> <span data-ttu-id="ba65b-148">Este é um dispositivo de nó único, depois de Olá atualização ser aplicada, Olá dispositivo for reiniciado e existe um período de indisponibilidade.</span><span class="sxs-lookup"><span data-stu-id="ba65b-148">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="ba65b-149">Clique Olá ícone de verificação.</span><span class="sxs-lookup"><span data-stu-id="ba65b-149">Click hello check icon.</span></span>
   
   ![atualizar o dispositivo](./media/storsimple-ova-install-update-01/update3m.png)
4. <span data-ttu-id="ba65b-151">inicia a atualização de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba65b-151">hello update starts.</span></span> <span data-ttu-id="ba65b-152">Depois do dispositivo de Olá foi atualizado com êxito, esta reiniciar.</span><span class="sxs-lookup"><span data-stu-id="ba65b-152">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="ba65b-153">Olá IU local não está acessível desta duração.</span><span class="sxs-lookup"><span data-stu-id="ba65b-153">hello local UI is not accessible in this duration.</span></span>
   
    ![atualizar o dispositivo](./media/storsimple-ova-install-update-01/update5m.png)
5. <span data-ttu-id="ba65b-155">Após a conclusão do reinício Olá, é direcionado toohello **sessão** página.</span><span class="sxs-lookup"><span data-stu-id="ba65b-155">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="ba65b-156">tooverify que atualizou o software de dispositivos de Olá, no Olá local IU da web do, aceda demasiado**manutenção** > **atualização de Software**.</span><span class="sxs-lookup"><span data-stu-id="ba65b-156">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="ba65b-157">Olá apresentada a versão de software deve estar **10.0.0.0.0.10288.0** para atualização 0.3.</span><span class="sxs-lookup"><span data-stu-id="ba65b-157">hello displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ba65b-158">Estamos a versões de software Olá de relatório de forma ligeiramente diferente na IU da web local Olá e Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba65b-158">We report hello software versions in a slightly different way in hello local web UI and hello Azure classic portal.</span></span> <span data-ttu-id="ba65b-159">Por exemplo, Olá relatórios de IU da local web **10.0.0.0.0.10288** e Olá relatórios de portais clássicos do Azure **10.0.10288.0** para Olá mesma versão.</span><span class="sxs-lookup"><span data-stu-id="ba65b-159">For example, hello local web UI reports **10.0.0.0.0.10288** and hello Azure classic portal reports **10.0.10288.0** for hello same version.</span></span> 
   > 
   > 
   
    ![atualizar o dispositivo](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-hello-azure-classic-portal"></a><span data-ttu-id="ba65b-161">Utilizar Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="ba65b-161">Use hello Azure classic portal</span></span>
<span data-ttu-id="ba65b-162">Se executar a atualização 0,2, recomendamos que instale atualizações através de Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba65b-162">If running Update 0.2, we recommend that you install updates through hello Azure classic portal.</span></span> <span data-ttu-id="ba65b-163">procedimento portal Olá requer Olá utilizador tooscan, transferir e, em seguida, instalar atualizações de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba65b-163">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="ba65b-164">Este procedimento assume toocomplete cerca de 7 minutos.</span><span class="sxs-lookup"><span data-stu-id="ba65b-164">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="ba65b-165">Execute o seguinte Olá passos tooinstall Olá atualização ou correção.</span><span class="sxs-lookup"><span data-stu-id="ba65b-165">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

<span data-ttu-id="ba65b-166">Olá após a instalação estiver concluída (conforme indicado pelo Estado de tarefa a 100%), aceda demasiado**dispositivos > manutenção > as atualizações de Software**.</span><span class="sxs-lookup"><span data-stu-id="ba65b-166">After hello installation is complete (as indicated by job status at 100 %), go too**Devices > Maintenance > Software Updates**.</span></span> <span data-ttu-id="ba65b-167">versão do software Olá apresentado deve ser 10.0.10288.0.</span><span class="sxs-lookup"><span data-stu-id="ba65b-167">hello displayed software version should be 10.0.10288.0.</span></span>

![atualizar o dispositivo](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a><span data-ttu-id="ba65b-169">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ba65b-169">Next steps</span></span>
<span data-ttu-id="ba65b-170">Saiba mais sobre [administrar a matriz de Virtual StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="ba65b-170">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

