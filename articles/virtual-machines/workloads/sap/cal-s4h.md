---
title: aaaDeploy SAP S/4HANA ou BW/4HANA numa VM do Azure | Microsoft Docs
description: Implementar SAP S/4HANA ou BW/4HANA numa VM do Azure
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a><span data-ttu-id="7074f-103">Implementar SAP S/4HANA ou BW/4HANA no Azure</span><span class="sxs-lookup"><span data-stu-id="7074f-103">Deploy SAP S/4HANA or BW/4HANA on Azure</span></span>
<span data-ttu-id="7074f-104">Este artigo descreve como toodeploy S/4HANA no Azure utilizando Olá biblioteca de aplicação de nuvem do SAP (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="7074f-104">This article describes how toodeploy S/4HANA on Azure by using hello SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="7074f-105">toodeploy outras soluções baseadas em SAP HANA, tais como BW/4HANA, siga Olá mesmos passos.</span><span class="sxs-lookup"><span data-stu-id="7074f-105">toodeploy other SAP HANA-based solutions, such as BW/4HANA, follow hello same steps.</span></span>

> [!NOTE]
<span data-ttu-id="7074f-106">Para mais informações sobre Olá SAP CAL, visite toohello [biblioteca de aplicação de nuvem do SAP](https://cal.sap.com/) Web site.</span><span class="sxs-lookup"><span data-stu-id="7074f-106">For more information about hello SAP CAL, go toohello [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="7074f-107">SAP também tem um blogue sobre Olá [SAP nuvem aplicação biblioteca 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="7074f-107">SAP also has a blog about hello [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span>

> [!NOTE]
<span data-ttu-id="7074f-108">Além disso como de 29 de Maio de 2017, pode utilizar o modelo de implementação Azure Resource Manager Olá toohello preferencial menos implementação clássica modelo toodeploy Olá SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="7074f-108">As of May 29, 2017, you can use hello Azure Resource Manager deployment model in addition toohello less-preferred classic deployment model toodeploy hello SAP CAL.</span></span> <span data-ttu-id="7074f-109">Recomendamos que utilize o modelo de implementação Resource Manager novo Olá e ignorar o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="7074f-109">We recommend that you use hello new Resource Manager deployment model and disregard hello classic deployment model.</span></span>

## <a name="step-by-step-process-toodeploy-hello-solution"></a><span data-ttu-id="7074f-110">Solução do passo a passo do processo toodeploy Olá</span><span class="sxs-lookup"><span data-stu-id="7074f-110">Step-by-step process toodeploy hello solution</span></span>

<span data-ttu-id="7074f-111">Olá sequência das capturas de ecrã a seguir mostra como toodeploy S/4HANA no Azure utilizando Olá SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="7074f-111">hello following sequence of screenshots shows you how toodeploy S/4HANA on Azure by using hello SAP CAL.</span></span> <span data-ttu-id="7074f-112">processo de Olá funciona Olá mesma forma para outras soluções, tais como BW/4HANA.</span><span class="sxs-lookup"><span data-stu-id="7074f-112">hello process works hello same way for other solutions, such as BW/4HANA.</span></span>

<span data-ttu-id="7074f-113">Olá **soluções** página mostra algumas das Olá soluções baseadas em CAL de SAP HANA disponíveis no Azure.</span><span class="sxs-lookup"><span data-stu-id="7074f-113">hello **Solutions** page shows some of hello SAP CAL HANA-based solutions available on Azure.</span></span> <span data-ttu-id="7074f-114">**SAP S/4HANA 1610 FPS01, Fully-Activated aplicação** na linha de média de Olá:</span><span class="sxs-lookup"><span data-stu-id="7074f-114">**SAP S/4HANA 1610 FPS01, Fully-Activated Appliance** is in hello middle row:</span></span>

![Soluções de CAL SAP](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a><span data-ttu-id="7074f-116">Criar uma conta no Olá SAP CAL</span><span class="sxs-lookup"><span data-stu-id="7074f-116">Create an account in hello SAP CAL</span></span>
1. <span data-ttu-id="7074f-117">toosign no toohello SAP CAL para Olá pela primeira vez, utilize o SAP-utilizador ou outro utilizador registado com o SAP.</span><span class="sxs-lookup"><span data-stu-id="7074f-117">toosign in toohello SAP CAL for hello first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="7074f-118">Em seguida, defina uma conta do SAP CAL que é utilizada por aplicações de toodeploy SAP CAL Olá no Azure.</span><span class="sxs-lookup"><span data-stu-id="7074f-118">Then define an SAP CAL account that is used by hello SAP CAL toodeploy appliances on Azure.</span></span> <span data-ttu-id="7074f-119">Na definição da conta de Olá, tem de:</span><span class="sxs-lookup"><span data-stu-id="7074f-119">In hello account definition, you need to:</span></span>

    <span data-ttu-id="7074f-120">a.</span><span class="sxs-lookup"><span data-stu-id="7074f-120">a.</span></span> <span data-ttu-id="7074f-121">Selecione o modelo de implementação de Olá no Azure (Gestor de recursos ou clássico).</span><span class="sxs-lookup"><span data-stu-id="7074f-121">Select hello deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="7074f-122">b.</span><span class="sxs-lookup"><span data-stu-id="7074f-122">b.</span></span> <span data-ttu-id="7074f-123">Introduza a sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="7074f-123">Enter your Azure subscription.</span></span> <span data-ttu-id="7074f-124">Uma conta do SAP CAL pode ser atribuída a subscrição de tooone apenas.</span><span class="sxs-lookup"><span data-stu-id="7074f-124">An SAP CAL account can be assigned tooone subscription only.</span></span> <span data-ttu-id="7074f-125">Se precisar de mais do que uma subscrição, terá de toocreate outra conta do SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="7074f-125">If you need more than one subscription, you need toocreate another SAP CAL account.</span></span>

    <span data-ttu-id="7074f-126">c.</span><span class="sxs-lookup"><span data-stu-id="7074f-126">c.</span></span> <span data-ttu-id="7074f-127">Dê Olá SAP CAL permissão toodeploy na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="7074f-127">Give hello SAP CAL permission toodeploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="7074f-128">Olá passos seguintes mostram como uma conta de toocreate uma CAL SAP para implementações do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7074f-128">hello next steps show how toocreate an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="7074f-129">Se já tiver uma conta do SAP CAL que é o modelo de implementação clássica toohello ligado, *necessário* toofollow toocreate estes passos uma nova conta do SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="7074f-129">If you already have an SAP CAL account that is linked toohello classic deployment model, you *need* toofollow these steps toocreate a new SAP CAL account.</span></span> <span data-ttu-id="7074f-130">nova conta do SAP CAL Olá tem toodeploy no modelo do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="7074f-130">hello new SAP CAL account needs toodeploy in hello Resource Manager model.</span></span>

2. <span data-ttu-id="7074f-131">Crie uma nova conta do SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="7074f-131">Create a new SAP CAL account.</span></span> <span data-ttu-id="7074f-132">Olá **contas** página mostra três opções para o Azure:</span><span class="sxs-lookup"><span data-stu-id="7074f-132">hello **Accounts** page shows three choices for Azure:</span></span> 

    <span data-ttu-id="7074f-133">a.</span><span class="sxs-lookup"><span data-stu-id="7074f-133">a.</span></span> <span data-ttu-id="7074f-134">**Microsoft Azure (clássica)** é o modelo de implementação clássica Olá e já não é preferencial.</span><span class="sxs-lookup"><span data-stu-id="7074f-134">**Microsoft Azure (classic)** is hello classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="7074f-135">b.</span><span class="sxs-lookup"><span data-stu-id="7074f-135">b.</span></span> <span data-ttu-id="7074f-136">**Microsoft Azure** é Olá novo modelo de implementação de Gestor de recursos.</span><span class="sxs-lookup"><span data-stu-id="7074f-136">**Microsoft Azure** is hello new Resource Manager deployment model.</span></span>

    <span data-ttu-id="7074f-137">c.</span><span class="sxs-lookup"><span data-stu-id="7074f-137">c.</span></span> <span data-ttu-id="7074f-138">**O Microsoft Azure operado pela 21Vianet** é uma opção na China que utiliza o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="7074f-138">**Windows Azure operated by 21Vianet** is an option in China that uses hello classic deployment model.</span></span>

    <span data-ttu-id="7074f-139">Selecione toodeploy no modelo do Resource Manager Olá, **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="7074f-139">toodeploy in hello Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Detalhes de conta do CAL SAP](./media/cal-s4h/s4h-pic-2a.png)

3. <span data-ttu-id="7074f-141">Introduza Olá Azure **ID de subscrição** que pode ser encontrado no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7074f-141">Enter hello Azure **Subscription ID** that can be found on hello Azure portal.</span></span>

   ![Contas de CAL SAP](./media/cal-s4h/s4h-pic3c.png)

4. <span data-ttu-id="7074f-143">tooauthorize Olá SAP CAL toodeploy para Olá subscrição do Azure definidos, clique em **autorizar**.</span><span class="sxs-lookup"><span data-stu-id="7074f-143">tooauthorize hello SAP CAL toodeploy into hello Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="7074f-144">Olá seguir página é apresentada no separador do browser Olá:</span><span class="sxs-lookup"><span data-stu-id="7074f-144">hello following page appears in hello browser tab:</span></span>

   ![Início de sessão dos serviços de nuvem do Internet Explorer](./media/cal-s4h/s4h-pic4c.png)

5. <span data-ttu-id="7074f-146">Se mais do que um utilizador estiver listado, escolha Olá conta Microsoft à qual está ligado toobe Olá coadministrador do Olá subscrição do Azure que selecionou.</span><span class="sxs-lookup"><span data-stu-id="7074f-146">If more than one user is listed, choose hello Microsoft account that is linked toobe hello coadministrator of hello Azure subscription you selected.</span></span> <span data-ttu-id="7074f-147">Olá seguir página é apresentada no separador do browser Olá:</span><span class="sxs-lookup"><span data-stu-id="7074f-147">hello following page appears in hello browser tab:</span></span>

   ![Confirmação de serviços de nuvem do Internet Explorer](./media/cal-s4h/s4h-pic5a.png)

6. <span data-ttu-id="7074f-149">Clique em **aceitar**.</span><span class="sxs-lookup"><span data-stu-id="7074f-149">Click **Accept**.</span></span> <span data-ttu-id="7074f-150">Se a autorização de Olá for bem-sucedida, Olá definição de conta do SAP CAL apresenta novamente.</span><span class="sxs-lookup"><span data-stu-id="7074f-150">If hello authorization is successful, hello SAP CAL account definition displays again.</span></span> <span data-ttu-id="7074f-151">Após um curto período de tempo, uma mensagem confirma que o processo de autorização de Olá foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="7074f-151">After a short time, a message confirms that hello authorization process was successful.</span></span>

7. <span data-ttu-id="7074f-152">Olá tooassign recém-criado SAP CAL conta de utilizador do tooyour, introduza o **ID de utilizador** no Olá caixa de texto Olá direito e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7074f-152">tooassign hello newly created SAP CAL account tooyour user, enter your **User ID** in hello text box on hello right and click **Add**.</span></span>

   ![Associação de conta toouser](./media/cal-s4h/s4h-pic8a.png)

8. <span data-ttu-id="7074f-154">Clique em sua conta com o utilizador Olá que utilize toosign toohello SAP CAL, de tooassociate **revisão**.</span><span class="sxs-lookup"><span data-stu-id="7074f-154">tooassociate your account with hello user that you use toosign in toohello SAP CAL, click **Review**.</span></span> 
 
9. <span data-ttu-id="7074f-155">associação de Olá toocreate entre o utilizador e a conta do SAP CAL Olá recentemente criado, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="7074f-155">toocreate hello association between your user and hello newly created SAP CAL account, click **Create**.</span></span>

   ![Associação de conta do utilizador tooSAP CAL](./media/cal-s4h/s4h-pic9b.png)

<span data-ttu-id="7074f-157">Criou com êxito uma conta do SAP CAL que é capaz de:</span><span class="sxs-lookup"><span data-stu-id="7074f-157">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="7074f-158">Utilize o modelo de implementação do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="7074f-158">Use hello Resource Manager deployment model.</span></span>
- <span data-ttu-id="7074f-159">Implemente sistemas SAP na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="7074f-159">Deploy SAP systems into your Azure subscription.</span></span>

<span data-ttu-id="7074f-160">Agora pode começar a toodeploy S/4HANA na sua subscrição de utilizador no Azure.</span><span class="sxs-lookup"><span data-stu-id="7074f-160">Now you can start toodeploy S/4HANA into your user subscription in Azure.</span></span>

> [!NOTE]
<span data-ttu-id="7074f-161">Antes de continuar, determine se tem de quotas de núcleo do Azure para as VMs do Azure série H.</span><span class="sxs-lookup"><span data-stu-id="7074f-161">Before you continue, determine whether you have Azure core quotas for Azure H-Series VMs.</span></span> <span data-ttu-id="7074f-162">Momento Olá, Olá SAP CAL utiliza H série VMs do Azure toodeploy algumas das soluções de SAP HANA baseado Olá.</span><span class="sxs-lookup"><span data-stu-id="7074f-162">At hello moment, hello SAP CAL uses H-Series VMs of Azure toodeploy some of hello SAP HANA-based solutions.</span></span> <span data-ttu-id="7074f-163">A subscrição do Azure poderá não ter quaisquer quotas de núcleos de série de H para série H.</span><span class="sxs-lookup"><span data-stu-id="7074f-163">Your Azure subscription might not have any H-Series core quotas for H-Series.</span></span> <span data-ttu-id="7074f-164">Se assim for, poderá ser necessário toocontact suporte do Azure tooget uma quota de núcleos de série de H, pelo menos, 16.</span><span class="sxs-lookup"><span data-stu-id="7074f-164">If so, you might need toocontact Azure support tooget a quota of at least 16 H-Series cores.</span></span>

> [!NOTE]
<span data-ttu-id="7074f-165">Ao implementar uma solução no Azure em Olá SAP CAL, poderá achar que pode escolher apenas uma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="7074f-165">When you deploy a solution on Azure in hello SAP CAL, you might find that you can choose only one Azure region.</span></span> <span data-ttu-id="7074f-166">toodeploy em regiões do Azure que não sejam Olá um sugerida pelo Olá SAP CAL, precisa de toopurchase uma subscrição de CAL do SAP.</span><span class="sxs-lookup"><span data-stu-id="7074f-166">toodeploy into Azure regions other than hello one suggested by hello SAP CAL, you need toopurchase a CAL subscription from SAP.</span></span> <span data-ttu-id="7074f-167">Também poderá ter tooopen uma mensagem com o SAP toohave sua toodeliver de conta ativada de CAL para regiões do Azure que não sejam Olá aqueles inicialmente sugeridos.</span><span class="sxs-lookup"><span data-stu-id="7074f-167">You also might need tooopen a message with SAP toohave your CAL account enabled toodeliver into Azure regions other than hello ones initially suggested.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="7074f-168">Implementar uma solução</span><span class="sxs-lookup"><span data-stu-id="7074f-168">Deploy a solution</span></span>

<span data-ttu-id="7074f-169">Eis como implementar uma solução de Olá **soluções** página do Olá SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="7074f-169">Let's deploy a solution from hello **Solutions** page of hello SAP CAL.</span></span> <span data-ttu-id="7074f-170">Olá SAP CAL tem duas sequências toodeploy:</span><span class="sxs-lookup"><span data-stu-id="7074f-170">hello SAP CAL has two sequences toodeploy:</span></span>

- <span data-ttu-id="7074f-171">Uma sequência básica que utiliza uma página toodefine Olá sistema toobe implementado</span><span class="sxs-lookup"><span data-stu-id="7074f-171">A basic sequence that uses one page toodefine hello system toobe deployed</span></span>
- <span data-ttu-id="7074f-172">Uma sequência avançada que dá-lhe algumas opções em tamanhos de VM</span><span class="sxs-lookup"><span data-stu-id="7074f-172">An advanced sequence that gives you certain choices on VM sizes</span></span> 

<span data-ttu-id="7074f-173">Iremos demonstrar Olá toodeployment de caminho básico aqui.</span><span class="sxs-lookup"><span data-stu-id="7074f-173">We demonstrate hello basic path toodeployment here.</span></span>

1. <span data-ttu-id="7074f-174">No Olá **detalhes da conta** página, tem de:</span><span class="sxs-lookup"><span data-stu-id="7074f-174">On hello **Account Details** page, you need to:</span></span>

    <span data-ttu-id="7074f-175">a.</span><span class="sxs-lookup"><span data-stu-id="7074f-175">a.</span></span> <span data-ttu-id="7074f-176">Selecione uma conta do SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="7074f-176">Select an SAP CAL account.</span></span> <span data-ttu-id="7074f-177">(Utilizar uma conta que seja toodeploy associado com o modelo de implementação do Resource Manager Olá.)</span><span class="sxs-lookup"><span data-stu-id="7074f-177">(Use an account that is associated toodeploy with hello Resource Manager deployment model.)</span></span>

    <span data-ttu-id="7074f-178">b.</span><span class="sxs-lookup"><span data-stu-id="7074f-178">b.</span></span> <span data-ttu-id="7074f-179">Introduza uma instância **nome**.</span><span class="sxs-lookup"><span data-stu-id="7074f-179">Enter an instance **Name**.</span></span>

    <span data-ttu-id="7074f-180">c.</span><span class="sxs-lookup"><span data-stu-id="7074f-180">c.</span></span> <span data-ttu-id="7074f-181">Selecione um Azure **região**.</span><span class="sxs-lookup"><span data-stu-id="7074f-181">Select an Azure **Region**.</span></span> <span data-ttu-id="7074f-182">Olá SAP CAL sugere uma região.</span><span class="sxs-lookup"><span data-stu-id="7074f-182">hello SAP CAL suggests a region.</span></span> <span data-ttu-id="7074f-183">Se precisar de outra região do Azure e não tiver uma subscrição de SAP CAL, precisa de subscrição de tooorder um CAL com SAP.</span><span class="sxs-lookup"><span data-stu-id="7074f-183">If you need another Azure region and you don't have an SAP CAL subscription, you need tooorder a CAL subscription with SAP.</span></span>

    <span data-ttu-id="7074f-184">d.</span><span class="sxs-lookup"><span data-stu-id="7074f-184">d.</span></span> <span data-ttu-id="7074f-185">Introduza um mestre **palavra-passe** para a solução de Olá de nove ou oito carateres.</span><span class="sxs-lookup"><span data-stu-id="7074f-185">Enter a master **Password** for hello solution of eight or nine characters.</span></span> <span data-ttu-id="7074f-186">palavra-passe de Olá é utilizada para os administradores de Olá dos componentes diferentes Olá.</span><span class="sxs-lookup"><span data-stu-id="7074f-186">hello password is used for hello administrators of hello different components.</span></span>

   ![Modo de CAL Basic SAP: Criar uma instância](./media/cal-s4h/s4h-pic10a.png)

2. <span data-ttu-id="7074f-188">Clique em **criar**e na caixa de mensagem de Olá que aparece, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="7074f-188">Click **Create**, and in hello message box that appears, click **OK**.</span></span>

   ![CAL de SAP suportado tamanhos de VM](./media/cal-s4h/s4h-pic10b.png)

3. <span data-ttu-id="7074f-190">No Olá **chave privada** caixa de diálogo, clique em **arquivo** toostore chave privada de Olá no Olá SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="7074f-190">In hello **Private Key** dialog box, click **Store** toostore hello private key in hello SAP CAL.</span></span> <span data-ttu-id="7074f-191">proteção de palavra-passe toouse para a chave privada de Olá, clique em **transferir**.</span><span class="sxs-lookup"><span data-stu-id="7074f-191">toouse password protection for hello private key, click **Download**.</span></span> 

   ![Chave privada de CAL SAP](./media/cal-s4h/s4h-pic10c.png)

4. <span data-ttu-id="7074f-193">Olá leitura SAP CAL **aviso** de mensagens e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="7074f-193">Read hello SAP CAL **Warning** message, and click **OK**.</span></span>

   ![Aviso de CAL SAP](./media/cal-s4h/s4h-pic10d.png)

    <span data-ttu-id="7074f-195">Agora a implementação de Olá ocorre.</span><span class="sxs-lookup"><span data-stu-id="7074f-195">Now hello deployment takes place.</span></span> <span data-ttu-id="7074f-196">Após algum tempo, dependendo da complexidade da solução de Olá (Olá SAP CAL fornece uma estimativa) e o tamanho Olá Olá estado é mostrado como Active Directory e pronto a utilizar.</span><span class="sxs-lookup"><span data-stu-id="7074f-196">After some time, depending on hello size and complexity of hello solution (hello SAP CAL provides an estimate), hello status is shown as active and ready for use.</span></span>

5. <span data-ttu-id="7074f-197">as máquinas virtuais de Olá toofind recolhidas com Olá outros recursos associados num grupo de recursos, visite toohello portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="7074f-197">toofind hello virtual machines collected with hello other associated resources in one resource group, go toohello Azure portal:</span></span> 

   ![Objetos de SAP CAL implementados no portal novo Olá](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. <span data-ttu-id="7074f-199">No portal de SAP CAL Olá, é apresentado o estado de Olá como **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7074f-199">On hello SAP CAL portal, hello status appears as **Active**.</span></span> <span data-ttu-id="7074f-200">tooconnect toohello solução, clique em **Connect**.</span><span class="sxs-lookup"><span data-stu-id="7074f-200">tooconnect toohello solution, click **Connect**.</span></span> <span data-ttu-id="7074f-201">Os diferentes componentes do diferentes opções tooconnect toohello são implementados dentro desta solução.</span><span class="sxs-lookup"><span data-stu-id="7074f-201">Different options tooconnect toohello different components are deployed within this solution.</span></span>

   ![Instâncias de CAL SAP](./media/cal-s4h/active_solution.png)

7. <span data-ttu-id="7074f-203">Antes de poder utilizar um dos Olá opções tooconnect toohello implementado sistemas, clique em **guia de introdução**.</span><span class="sxs-lookup"><span data-stu-id="7074f-203">Before you can use one of hello options tooconnect toohello deployed systems, click **Getting Started Guide**.</span></span> 

   ![Ligar toohello instância](./media/cal-s4h/connect_to_solution.png)

    <span data-ttu-id="7074f-205">os nomes de documentação Olá hello utilizadores para cada um dos métodos de conectividade Olá.</span><span class="sxs-lookup"><span data-stu-id="7074f-205">hello documentation names hello users for each of hello connectivity methods.</span></span> <span data-ttu-id="7074f-206">Olá palavras-passe para esses utilizadores são definidas toohello mestre palavra-passe que definiu no início de Olá do processo de implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="7074f-206">hello passwords for those users are set toohello master password you defined at hello beginning of hello deployment process.</span></span> <span data-ttu-id="7074f-207">Na documentação de Olá, outros mais funcionais utilizadores são listados com as palavras-passe, que pode utilizar toosign no toohello implementado o sistema.</span><span class="sxs-lookup"><span data-stu-id="7074f-207">In hello documentation, other more functional users are listed with their passwords, which you can use toosign in toohello deployed system.</span></span> 

    <span data-ttu-id="7074f-208">Por exemplo, se utilizar Olá SAP GUI que está pré-instalado na máquina de ambiente de trabalho remoto do Windows hello, Olá sistema S/4 poderá ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="7074f-208">For example, if you use hello SAP GUI that's preinstalled on hello Windows Remote Desktop machine, hello S/4 system might look like this:</span></span>

   ![SM50 no Olá pré-instalado SAP GUI](./media/cal-s4h/gui_sm50.png)

    <span data-ttu-id="7074f-210">Ou, se utilizar Olá DBACockpit, instância de Olá poderá ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="7074f-210">Or if you use hello DBACockpit, hello instance might look like this:</span></span>

   ![SM50 no Olá DBACockpit SAP GUI](./media/cal-s4h/dbacockpit.png)

<span data-ttu-id="7074f-212">Dentro de algumas horas, um dispositivo de SAP S/4 bom estado de funcionamento é implementado no Azure.</span><span class="sxs-lookup"><span data-stu-id="7074f-212">Within a few hours, a healthy SAP S/4 appliance is deployed in Azure.</span></span>

<span data-ttu-id="7074f-213">Se comprou a uma subscrição de SAP CAL, SAP suporta totalmente implementações através de Olá SAP CAL no Azure.</span><span class="sxs-lookup"><span data-stu-id="7074f-213">If you bought an SAP CAL subscription, SAP fully supports deployments through hello SAP CAL on Azure.</span></span> <span data-ttu-id="7074f-214">fila de suporte de Olá é BC-VCM-CAL.</span><span class="sxs-lookup"><span data-stu-id="7074f-214">hello support queue is BC-VCM-CAL.</span></span>







