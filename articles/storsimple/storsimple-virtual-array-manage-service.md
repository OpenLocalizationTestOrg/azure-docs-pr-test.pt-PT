---
title: "aaaDeploy serviço Gestor de dispositivos do StorSimple | Microsoft Docs"
description: "Explica como toocreate e delete hello do serviço StorSimple Manager de dispositivos no portal do Azure de Olá e descreve como toomanage Olá chave de registo do serviço."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="21902-103">Implementar o serviço do Gestor de dispositivos do StorSimple Olá matriz Virtual StorSimple</span><span class="sxs-lookup"><span data-stu-id="21902-103">Deploy hello StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="21902-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="21902-104">Overview</span></span>

<span data-ttu-id="21902-105">Olá serviço Gestor de dispositivos do StorSimple é executado no Microsoft Azure e liga toomultiple StorSimple dispositivos.</span><span class="sxs-lookup"><span data-stu-id="21902-105">hello StorSimple Device Manager service runs in Microsoft Azure and connects toomultiple StorSimple devices.</span></span> <span data-ttu-id="21902-106">Depois de criar serviço Olá, pode utilizá-lo dispositivos Olá toomanage Olá Microsoft Azure portal em execução num browser.</span><span class="sxs-lookup"><span data-stu-id="21902-106">After you create hello service, you can use it toomanage hello devices from hello Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="21902-107">Isto permite-lhe toomonitor todos os dispositivos de Olá que estão ligado toohello Gestor de dispositivos do StorSimple service a partir de uma única localização central, deste modo, minimizando o fardo administrativo.</span><span class="sxs-lookup"><span data-stu-id="21902-107">This allows you toomonitor all hello devices that are connected toohello StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="21902-108">Olá comuns tarefas relacionadas tooa serviço StorSimple Manager de dispositivos são:</span><span class="sxs-lookup"><span data-stu-id="21902-108">hello common tasks related tooa StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="21902-109">Criar um serviço</span><span class="sxs-lookup"><span data-stu-id="21902-109">Create a service</span></span>
* <span data-ttu-id="21902-110">Eliminar um serviço</span><span class="sxs-lookup"><span data-stu-id="21902-110">Delete a service</span></span>
* <span data-ttu-id="21902-111">Obter a chave de registo do serviço de Olá</span><span class="sxs-lookup"><span data-stu-id="21902-111">Get hello service registration key</span></span>
* <span data-ttu-id="21902-112">Regenerar a chave de registo do serviço de Olá</span><span class="sxs-lookup"><span data-stu-id="21902-112">Regenerate hello service registration key</span></span>

<span data-ttu-id="21902-113">Este tutorial descreve como tooperform de Olá tarefas anteriores.</span><span class="sxs-lookup"><span data-stu-id="21902-113">This tutorial describes how tooperform each of hello preceding tasks.</span></span> <span data-ttu-id="21902-114">informações de Olá contidas neste artigo são aplicável apenas tooStorSimple Virtual as matrizes.</span><span class="sxs-lookup"><span data-stu-id="21902-114">hello information contained in this article is applicable only tooStorSimple Virtual Arrays.</span></span> <span data-ttu-id="21902-115">Para obter mais informações sobre série 8000 do StorSimple, visite demasiado[implementar um serviço StorSimple Manager](storsimple-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="21902-115">For more information on StorSimple 8000 series, go too[deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="21902-116">Criar um serviço</span><span class="sxs-lookup"><span data-stu-id="21902-116">Create a service</span></span>

<span data-ttu-id="21902-117">toocreate um serviço, terá de toohave:</span><span class="sxs-lookup"><span data-stu-id="21902-117">toocreate a service, you need toohave:</span></span>

* <span data-ttu-id="21902-118">Uma subscrição com um Enterprise Agreement</span><span class="sxs-lookup"><span data-stu-id="21902-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="21902-119">Uma conta de armazenamento do Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="21902-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="21902-120">Olá, as informações de faturação que são utilizadas para gestão de acesso</span><span class="sxs-lookup"><span data-stu-id="21902-120">hello billing information that is used for access management</span></span>

<span data-ttu-id="21902-121">Também pode escolher toogenerate uma conta de armazenamento ao criar o serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="21902-121">You can also choose toogenerate a storage account when you create hello service.</span></span>

<span data-ttu-id="21902-122">Um único serviço pode gerir vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="21902-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="21902-123">No entanto, um dispositivo não pode abranger vários serviços.</span><span class="sxs-lookup"><span data-stu-id="21902-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="21902-124">Uma grande empresa pode ter vários toowork de instâncias de serviço com diferentes subscrições, as organizações ou até mesmo as localizações de implementação.</span><span class="sxs-lookup"><span data-stu-id="21902-124">A large enterprise can have multiple service instances toowork with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="21902-125">Terá de instâncias separadas de dispositivos de série do Gestor de dispositivos do StorSimple serviço toomanage 8000 do StorSimple e matrizes Virtual StorSimple.</span><span class="sxs-lookup"><span data-stu-id="21902-125">You need separate instances of StorSimple Device Manager service toomanage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="21902-126">Efetue Olá os seguintes passos toocreate um serviço.</span><span class="sxs-lookup"><span data-stu-id="21902-126">Perform hello following steps toocreate a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="21902-127">Eliminar um serviço</span><span class="sxs-lookup"><span data-stu-id="21902-127">Delete a service</span></span>

<span data-ttu-id="21902-128">Antes de eliminar um serviço, certifique-se de que não existem dispositivos ligados a estiver a utilizar.</span><span class="sxs-lookup"><span data-stu-id="21902-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="21902-129">Se o serviço de Olá está a ser utilizado, desative dispositivos Olá ligado.</span><span class="sxs-lookup"><span data-stu-id="21902-129">If hello service is in use, deactivate hello connected devices.</span></span> <span data-ttu-id="21902-130">Olá desativar operação irá sever ligação Olá entre dispositivos de Olá e o serviço de Olá, mas manter os dados do dispositivo Olá na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="21902-130">hello deactivate operation will sever hello connection between hello device and hello service, but preserve hello device data in hello cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21902-131">Depois de um serviço é eliminado, não é possível reverter a operação de Olá.</span><span class="sxs-lookup"><span data-stu-id="21902-131">After a service is deleted, hello operation cannot be reversed.</span></span> <span data-ttu-id="21902-132">Terá de qualquer dispositivo que estava a utilizar o serviço de Olá toobe antes de poder ser utilizada com outro serviço de reposição de fábrica.</span><span class="sxs-lookup"><span data-stu-id="21902-132">Any device that was using hello service will need toobe factory reset before it can be used with another service.</span></span> <span data-ttu-id="21902-133">Neste cenário, os dados locais Olá no dispositivo Olá, bem como a configuração de Olá, serão perdidas.</span><span class="sxs-lookup"><span data-stu-id="21902-133">In this scenario, hello local data on hello device, as well as hello configuration, will be lost.</span></span>
 

<span data-ttu-id="21902-134">Efetue Olá os seguintes passos toodelete um serviço.</span><span class="sxs-lookup"><span data-stu-id="21902-134">Perform hello following steps toodelete a service.</span></span>

#### <a name="toodelete-a-service"></a><span data-ttu-id="21902-135">toodelete um serviço</span><span class="sxs-lookup"><span data-stu-id="21902-135">toodelete a service</span></span>

1. <span data-ttu-id="21902-136">Aceda demasiado**todos os recursos**.</span><span class="sxs-lookup"><span data-stu-id="21902-136">Go too**All resources**.</span></span> <span data-ttu-id="21902-137">Pesquisa para o seu serviço do Gestor de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="21902-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="21902-138">Selecione o serviço de Olá pretende toodelete.</span><span class="sxs-lookup"><span data-stu-id="21902-138">Select hello service that you wish toodelete.</span></span>
   
    ![Selecione toodelete de serviço](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="21902-140">Aceda tooyour serviço dashboard tooensure existem não existem dispositivos ligados toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="21902-140">Go tooyour service dashboard tooensure there are no devices connected toohello service.</span></span> <span data-ttu-id="21902-141">Se não houver nenhuma dispositivos registados com este serviço, verá também um efeito de toohello de mensagem de faixa.</span><span class="sxs-lookup"><span data-stu-id="21902-141">If there are no devices registered with this service, you will also see a banner message toohello effect.</span></span> <span data-ttu-id="21902-142">Clique em **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="21902-142">Click **Delete**.</span></span>
   
    ![Eliminar o serviço](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="21902-144">Quando lhe for pedido para confirmação, clique em **Sim** na notificação de confirmação de Olá.</span><span class="sxs-lookup"><span data-stu-id="21902-144">When prompted for confirmation, click **Yes** in hello confirmation notification.</span></span> 
   
    ![Confirmar eliminação do serviço](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="21902-146">Pode demorar alguns minutos para Olá serviço toobe eliminado.</span><span class="sxs-lookup"><span data-stu-id="21902-146">It may take a few minutes for hello service toobe deleted.</span></span> <span data-ttu-id="21902-147">Depois de Olá serviço é eliminado com êxito, será notificado.</span><span class="sxs-lookup"><span data-stu-id="21902-147">After hello service is successfully deleted, you will be notified.</span></span>
   
    ![Eliminação do serviço concluída com êxito](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="21902-149">lista de Olá de serviços será atualizada.</span><span class="sxs-lookup"><span data-stu-id="21902-149">hello list of services will be refreshed.</span></span>

 ![Lista atualizada de serviços](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a><span data-ttu-id="21902-151">Obter a chave de registo do serviço de Olá</span><span class="sxs-lookup"><span data-stu-id="21902-151">Get hello service registration key</span></span>
<span data-ttu-id="21902-152">Depois de ter criado com êxito um serviço, terá de tooregister serviço Olá no dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="21902-152">After you have successfully created a service, you will need tooregister your StorSimple device with hello service.</span></span> <span data-ttu-id="21902-153">tooregister primeiro dispositivo StorSimple, será necessário Olá chave de registo do serviço.</span><span class="sxs-lookup"><span data-stu-id="21902-153">tooregister your first StorSimple device, you will need hello service registration key.</span></span> <span data-ttu-id="21902-154">tooregister dispositivos adicionais com um serviço StorSimple, terá de chave de registo Olá e Olá serviço chave de encriptação dados (que é gerado no primeiro dispositivo de Olá durante o registo).</span><span class="sxs-lookup"><span data-stu-id="21902-154">tooregister additional devices with an existing StorSimple service, you will need both hello registration key and hello service data encryption key (which is generated on hello first device during registration).</span></span> <span data-ttu-id="21902-155">Para obter mais informações sobre a chave de encriptação de dados de serviço Olá, consulte [segurança do StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="21902-155">For more information about hello service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="21902-156">Pode obter a chave de registo Olá acedendo Olá **chaves** painel para o seu serviço.</span><span class="sxs-lookup"><span data-stu-id="21902-156">You can get hello registration key by accessing hello **Keys** blade for your service.</span></span>

<span data-ttu-id="21902-157">Efetue Olá chave de registo de serviço de Olá tooget passos a seguir.</span><span class="sxs-lookup"><span data-stu-id="21902-157">Perform hello following steps tooget hello service registration key.</span></span>

#### <a name="tooget-hello-service-registration-key"></a><span data-ttu-id="21902-158">chave de registo do serviço de Olá tooget</span><span class="sxs-lookup"><span data-stu-id="21902-158">tooget hello service registration key</span></span>
1. <span data-ttu-id="21902-159">No Olá **Gestor de dispositivos do StorSimple** painel, vá demasiado**gestão &gt;**  **chaves**.</span><span class="sxs-lookup"><span data-stu-id="21902-159">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![Painel de chaves](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="21902-161">No Olá **chaves** aparece do painel, uma chave de registo do serviço.</span><span class="sxs-lookup"><span data-stu-id="21902-161">In hello **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="21902-162">Copie a chave de registo de Olá com ícone de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="21902-162">Copy hello registration key using hello copy icon.</span></span> 

<span data-ttu-id="21902-163">Manter a chave de registo do serviço de Olá numa localização segura.</span><span class="sxs-lookup"><span data-stu-id="21902-163">Keep hello service registration key in a safe location.</span></span> <span data-ttu-id="21902-164">Terá esta chave, bem como chave de encriptação de dados de serviço Olá, tooregister dispositivos adicionais com este serviço.</span><span class="sxs-lookup"><span data-stu-id="21902-164">You will need this key, as well as hello service data encryption key, tooregister additional devices with this service.</span></span> <span data-ttu-id="21902-165">Depois de obter a chave de registo do serviço de Olá, terá de tooconfigure o dispositivo através do Olá do Windows PowerShell para StorSimple interface.</span><span class="sxs-lookup"><span data-stu-id="21902-165">After obtaining hello service registration key, you will need tooconfigure your device through hello Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-hello-service-registration-key"></a><span data-ttu-id="21902-166">Regenerar a chave de registo do serviço de Olá</span><span class="sxs-lookup"><span data-stu-id="21902-166">Regenerate hello service registration key</span></span>
<span data-ttu-id="21902-167">Precisa de tooregenerate uma chave de registo do serviço se for necessário tooperform rotação da chave ou se a lista de Olá dos administradores de serviço foi alterada.</span><span class="sxs-lookup"><span data-stu-id="21902-167">You will need tooregenerate a service registration key if you are required tooperform key rotation or if hello list of service administrators has changed.</span></span> <span data-ttu-id="21902-168">Quando voltar a gerar chave Olá, a nova chave de Olá é utilizado apenas para registar dispositivos subsequentes.</span><span class="sxs-lookup"><span data-stu-id="21902-168">When you regenerate hello key, hello new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="21902-169">dispositivos de Olá que já foram registados não são afetados por este processo.</span><span class="sxs-lookup"><span data-stu-id="21902-169">hello devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="21902-170">Efetue Olá os seguintes passos tooregenerate uma chave de registo do serviço.</span><span class="sxs-lookup"><span data-stu-id="21902-170">Perform hello following steps tooregenerate a service registration key.</span></span>

#### <a name="tooregenerate-hello-service-registration-key"></a><span data-ttu-id="21902-171">chave de registo do serviço de Olá tooregenerate</span><span class="sxs-lookup"><span data-stu-id="21902-171">tooregenerate hello service registration key</span></span>
1. <span data-ttu-id="21902-172">No Olá **Gestor de dispositivos do StorSimple** painel, vá demasiado**gestão &gt;**  **chaves**.</span><span class="sxs-lookup"><span data-stu-id="21902-172">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![Painel de chaves](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="21902-174">No Olá **chaves** painel, clique em **regenerar**.</span><span class="sxs-lookup"><span data-stu-id="21902-174">In hello **Keys** blade, click **Regenerate**.</span></span>
   
   ![Clique em voltar a gerar](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="21902-176">No Olá **chave de registo do serviço de voltar a gerar** painel, reveja Olá necessária ação ao hello chaves são regeneradas.</span><span class="sxs-lookup"><span data-stu-id="21902-176">In hello **Regenerate service registration key** blade, review hello action required when hello keys are regenerated.</span></span> <span data-ttu-id="21902-177">Todos os dispositivos subsequentes Olá registados com este serviço irão utilizar a nova chave de registo Olá.</span><span class="sxs-lookup"><span data-stu-id="21902-177">All hello subsequent devices that are registered with this service will use hello new registration key.</span></span> <span data-ttu-id="21902-178">Clique em **regenerar** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="21902-178">Click **Regenerate** tooconfirm.</span></span> <span data-ttu-id="21902-179">Será notificado depois de concluída a registo Olá.</span><span class="sxs-lookup"><span data-stu-id="21902-179">You will be notified after hello registration is complete.</span></span>
   
   ![Confirme a regeneração da chave](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="21902-181">Será apresentada uma nova chave de registo do serviço.</span><span class="sxs-lookup"><span data-stu-id="21902-181">A new service registration key will appear.</span></span>
   
    ![Confirme a regeneração da chave](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="21902-183">Copie esta chave e guarde-a para registar os novos dispositivos com este serviço.</span><span class="sxs-lookup"><span data-stu-id="21902-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21902-184">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="21902-184">Next steps</span></span>
* <span data-ttu-id="21902-185">Saiba como demasiado[começar](storsimple-virtual-array-deploy1-portal-prep.md) com uma matriz de Virtual StorSimple.</span><span class="sxs-lookup"><span data-stu-id="21902-185">Learn how too[get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="21902-186">Saiba como demasiado[administrar o dispositivo StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="21902-186">Learn how too[administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>

