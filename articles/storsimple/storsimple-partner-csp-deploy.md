---
title: "aaaMicrosoft Azure StorSimple e descrição geral de programa do fornecedor de soluções de nuvem | Microsoft Docs"
description: "Uma descrição geral sobre Olá StorSimple e o CSP para parceiros do StorSimple."
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
ms.date: 02/08/2017
ms.author: alkohli
ms.openlocfilehash: b5d999f2fbb9a27e7404ff454957b29dbef56af6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a><span data-ttu-id="760b7-103">Implementar matriz Virtual StorSimple para o programa de fornecedor de solução em nuvem</span><span class="sxs-lookup"><span data-stu-id="760b7-103">Deploy StorSimple Virtual Array for Cloud Solution Provider Program</span></span>

## <a name="overview"></a><span data-ttu-id="760b7-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="760b7-104">Overview</span></span>

<span data-ttu-id="760b7-105">Matriz Virtual StorSimple pode ser implementado por parceiros de fornecedor de solução em nuvem (CSP) Olá para os seus clientes.</span><span class="sxs-lookup"><span data-stu-id="760b7-105">StorSimple Virtual Array can be deployed by hello Cloud Solution Provider (CSP) partners for their customers.</span></span> <span data-ttu-id="760b7-106">Um parceiro CSP pode criar um serviço do Gestor de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="760b7-106">A CSP partner can create a StorSimple Device Manager service.</span></span> <span data-ttu-id="760b7-107">Este serviço, em seguida, pode ser utilizado toodeploy e gerir matriz Virtual StorSimple e Olá partilhas, volumes e as cópias de segurança associados.</span><span class="sxs-lookup"><span data-stu-id="760b7-107">This service can then be used toodeploy and manage StorSimple Virtual Array and hello associated shares, volumes, and backups.</span></span>

<span data-ttu-id="760b7-108">Este artigo descreve como um parceiro CSP pode adicionar um cliente ou uma nova subscrição tooan existente e, em seguida, criar um serviço toodeploy uma matriz de Virtual StorSimple no CSP.</span><span class="sxs-lookup"><span data-stu-id="760b7-108">This article describes how a CSP partner can add a customer or a new subscription tooan existing customer and then create a service toodeploy a StorSimple Virtual Array in CSP.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="760b7-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="760b7-109">Prerequisites</span></span>

<span data-ttu-id="760b7-110">Antes de começar, certifique-se de que:</span><span class="sxs-lookup"><span data-stu-id="760b7-110">Before you begin, ensure that:</span></span>

- <span data-ttu-id="760b7-111">Estão inscritos no programa CSP Olá.</span><span class="sxs-lookup"><span data-stu-id="760b7-111">You are enrolled under hello CSP program.</span></span>
- <span data-ttu-id="760b7-112">Tiver válido [Centro de parceiros](http://partnercenter.microsoft.com/) credenciais de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="760b7-112">You have valid [Partner Center](http://partnercenter.microsoft.com/) login credentials.</span></span> <span data-ttu-id="760b7-113">credenciais de Olá permitem-lhe toosign em novos clientes do toohello parceiro portal tooadd, procurar clientes ou navegue tooa a conta de cliente a partir do dashboard de parceiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="760b7-113">hello credentials enable you toosign in toohello Partner portal tooadd new customers, search for customers, or navigate tooa customer account from hello Partner dashboard.</span></span> <span data-ttu-id="760b7-114">Olá CSP pode funcionar como um administrador do StorSimple em nome do cliente de Olá no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="760b7-114">hello CSP can function as a StorSimple administrator on behalf of hello customer in hello Azure portal.</span></span>
                             
## <a name="add-a-customer"></a><span data-ttu-id="760b7-115">Adicionar um cliente</span><span class="sxs-lookup"><span data-stu-id="760b7-115">Add a customer</span></span>

<span data-ttu-id="760b7-116">Se adicionar um cliente, é automaticamente criada uma subscrição.</span><span class="sxs-lookup"><span data-stu-id="760b7-116">If you add a customer, a subscription is automatically created.</span></span> <span data-ttu-id="760b7-117">tooadd um cliente (e criar automaticamente uma subscrição), efetuar Olá os seguintes passos no portal de parceiros de Olá.</span><span class="sxs-lookup"><span data-stu-id="760b7-117">tooadd a customer (and automatically create a subscription), perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="760b7-118">Aceda toohello [Centro de parceiros](http://partnercenter.microsoft.com/) e inicie sessão com as suas credenciais CSP.</span><span class="sxs-lookup"><span data-stu-id="760b7-118">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="760b7-119">Clique em **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="760b7-119">Click **Dashboard**.</span></span>

     ![Dashboard do Centro de parceiros](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="760b7-121">No Olá painel esquerdo, clique em **clientes**.</span><span class="sxs-lookup"><span data-stu-id="760b7-121">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="760b7-122">No Olá painel direito, clique em **adicionar clientes**.</span><span class="sxs-lookup"><span data-stu-id="760b7-122">In hello right-pane, click **Add customers**.</span></span> <span data-ttu-id="760b7-123">Introduza os detalhes de hello do cliente de Olá.</span><span class="sxs-lookup"><span data-stu-id="760b7-123">Enter hello details of hello customer.</span></span> <span data-ttu-id="760b7-124">Clique em **seguinte: subscrições** toocreate uma subscrição do cliente.</span><span class="sxs-lookup"><span data-stu-id="760b7-124">Click **Next: Subscriptions** toocreate a customer subscription.</span></span>

    ![Adicionar cliente](./media/storsimple-partner-csp-deploy/image2.png)

3.  <span data-ttu-id="760b7-126">Selecione **Microsoft Azure** oferecem.</span><span class="sxs-lookup"><span data-stu-id="760b7-126">Select **Microsoft Azure** offer.</span></span> <span data-ttu-id="760b7-127">Parte inferior do toohello de deslocamento da página Olá e clique em **revisão**.</span><span class="sxs-lookup"><span data-stu-id="760b7-127">Scroll toohello bottom of hello page and click **Review**.</span></span>

    ![Reveja as informações de subscrição](./media/storsimple-partner-csp-deploy/image3.png)
                              
4. <span data-ttu-id="760b7-129">Reveja as informações de Olá e clique em **submeter**.</span><span class="sxs-lookup"><span data-stu-id="760b7-129">Review hello information and click **Submit**.</span></span>

    ![Submeter subscrição](./media/storsimple-partner-csp-deploy/image4.png)

5. <span data-ttu-id="760b7-131">Guarde informações de confirmação de Olá para consulta futura.</span><span class="sxs-lookup"><span data-stu-id="760b7-131">Save hello confirmation information for future reference.</span></span>

    ![Guardar confirmação](./media/storsimple-partner-csp-deploy/image5.png)

6. <span data-ttu-id="760b7-133">Localizar ou navegue até ao cliente toohello que acabou de adicionar.</span><span class="sxs-lookup"><span data-stu-id="760b7-133">Find or navigate toohello customer you just added.</span></span> <span data-ttu-id="760b7-134">Clique em Olá **nome da empresa** toodrill para baixo para detalhes de Olá.</span><span class="sxs-lookup"><span data-stu-id="760b7-134">Click hello **Company name** toodrill down into hello details.</span></span>

    ![Pesquisa de cliente de Olá](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="760b7-136">No Olá painel esquerdo, selecione **gestão de serviço**.</span><span class="sxs-lookup"><span data-stu-id="760b7-136">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="760b7-137">No Olá painel direito, em **administrar serviços**, clique em **Microsoft Azure Management Portal** toosign na como um administrador do Azure para o seu cliente.</span><span class="sxs-lookup"><span data-stu-id="760b7-137">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![Inicie sessão no portal de tooAzure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="760b7-139">toocreate um Gestor de dispositivos do StorSimple, clique em **+ novo** e procure ou navegue demasiado**série de dispositivo Virtual StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="760b7-139">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="760b7-140">Para mais informações, visite demasiado[implementar um serviço do Gestor de dispositivos do StorSimple](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="760b7-140">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Criar o serviço do Gestor de dispositivos do StorSimple](./media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a><span data-ttu-id="760b7-142">Adicionar uma subscrição</span><span class="sxs-lookup"><span data-stu-id="760b7-142">Add a subscription</span></span>

<span data-ttu-id="760b7-143">Em alguns casos, poderá ter um cliente existente e tem de tooadd uma subscrição.</span><span class="sxs-lookup"><span data-stu-id="760b7-143">In some instances, you may have an existing customer, and you need tooadd a subscription.</span></span> <span data-ttu-id="760b7-144">tooadd um subscrição tooan cliente existente, execute Olá os seguintes passos no portal de parceiros de Olá.</span><span class="sxs-lookup"><span data-stu-id="760b7-144">tooadd a subscription tooan existing customer, perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="760b7-145">Aceda toohello [Centro de parceiros](http://partnercenter.microsoft.com/) e inicie sessão com as suas credenciais CSP.</span><span class="sxs-lookup"><span data-stu-id="760b7-145">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="760b7-146">Clique em **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="760b7-146">Click **Dashboard**.</span></span>

     ![Dashboard do Centro de parceiros](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="760b7-148">No Olá painel esquerdo, clique em **clientes**.</span><span class="sxs-lookup"><span data-stu-id="760b7-148">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="760b7-149">Localizar ou navegue até ao cliente toohello que pretende tooadd uma subscrição.</span><span class="sxs-lookup"><span data-stu-id="760b7-149">Find or navigate toohello customer you want tooadd a subscription to.</span></span> <span data-ttu-id="760b7-150">Clique em Olá ![ícone de verificação de expansão](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) linha de Olá tooexpand ícone para o nome da empresa Olá para o seu cliente.</span><span class="sxs-lookup"><span data-stu-id="760b7-150">Click hello ![Expand check icon](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) icon tooexpand hello row for hello company name for your customer.</span></span> <span data-ttu-id="760b7-151">Nos detalhes de Olá, clique em **adicionar subscrições**.</span><span class="sxs-lookup"><span data-stu-id="760b7-151">In hello details, click **Add subscriptions**.</span></span>

    ![Clientes](./media/storsimple-partner-csp-deploy/image10.png)

3. <span data-ttu-id="760b7-153">Verifique **Microsoft Azure** para Olá **principais ofertas** na subscrição Olá e clique em **submeter**.</span><span class="sxs-lookup"><span data-stu-id="760b7-153">Check **Microsoft Azure** for hello **Top offers** in hello subscription and click **Submit**.</span></span> <span data-ttu-id="760b7-154">Esta ação cria uma nova subscrição.</span><span class="sxs-lookup"><span data-stu-id="760b7-154">This creates a new subscription.</span></span>

    ![Adicionar nova subscrição](./media/storsimple-partner-csp-deploy/image11.png)

6. <span data-ttu-id="760b7-156">Depois de criar uma nova subscrição, clique em **< – clientes** no Olá painel esquerdo tooreturn toohello **clientes** página.</span><span class="sxs-lookup"><span data-stu-id="760b7-156">After a new subscription is created, click **<-- Customers** in hello left-pane tooreturn toohello **Customers** page.</span></span> <span data-ttu-id="760b7-157">Pesquisa de cliente Olá para o qual acabou de criar uma subscrição.</span><span class="sxs-lookup"><span data-stu-id="760b7-157">Search for hello customer for whom you just created a subscription.</span></span> <span data-ttu-id="760b7-158">Clique em Olá **nome da empresa** toodrill para baixo para detalhes de Olá.</span><span class="sxs-lookup"><span data-stu-id="760b7-158">Click hello **Company name** toodrill down into hello details.</span></span>

    ![Pesquisa de cliente de Olá](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="760b7-160">No Olá painel esquerdo, selecione **gestão de serviço**.</span><span class="sxs-lookup"><span data-stu-id="760b7-160">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="760b7-161">No Olá painel direito, em **administrar serviços**, clique em **Microsoft Azure Management Portal** toosign na como um administrador do Azure para o seu cliente.</span><span class="sxs-lookup"><span data-stu-id="760b7-161">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![Inicie sessão no portal de tooAzure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="760b7-163">toocreate um Gestor de dispositivos do StorSimple, clique em **+ novo** e procure ou navegue demasiado**série de dispositivo Virtual StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="760b7-163">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="760b7-164">Para mais informações, visite demasiado[implementar um serviço do Gestor de dispositivos do StorSimple](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="760b7-164">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Criar o serviço do Gestor de dispositivos do StorSimple](./media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a><span data-ttu-id="760b7-166">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="760b7-166">Next steps</span></span>

- <span data-ttu-id="760b7-167">Se tiver mais perguntas sobre Olá StorSimple no CSP, aceda demasiado[StorSimple no CSP: Perguntas mais frequentes](storsimple-partner-csp-faq.md).</span><span class="sxs-lookup"><span data-stu-id="760b7-167">If you have more questions regarding hello StorSimple in CSP, go too[StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md).</span></span>
- <span data-ttu-id="760b7-168">Se estiver pronto toodeploy do StorSimple, aceda demasiado[implementar a sua StorSimple no CSP](storsimple-partner-csp-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="760b7-168">If you are ready toodeploy your StorSimple, go too[Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md).</span></span>
