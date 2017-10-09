---
title: "aaaLog pedido de suporte para a série 8000 do StorSimple | Microsoft Docs"
description: "Saiba como toocreate um suporte de pedido e iniciar uma sessão de suporte no dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e1a3aa3c56e036c782c4fb502c477dc0feaa0ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a><span data-ttu-id="ca4ef-103">Contacte o suporte da Microsoft para do StorSimple</span><span class="sxs-lookup"><span data-stu-id="ca4ef-103">Contact Microsoft Support for your StorSimple</span></span>
<span data-ttu-id="ca4ef-104">Se tiver quaisquer problemas com a sua solução do Microsoft Azure StorSimple, pode criar um pedido de serviço para o suporte técnico.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-104">If you encounter any issues with your Microsoft Azure StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="ca4ef-105">Numa sessão com o seu engenheiro de suporte online, também poderá ser necessário toostart uma sessão de suporte no dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-105">In an online session with your support engineer, you may also need toostart a support session on your StorSimple device.</span></span> <span data-ttu-id="ca4ef-106">Este artigo explica como:</span><span class="sxs-lookup"><span data-stu-id="ca4ef-106">This article walks you through:</span></span>

* <span data-ttu-id="ca4ef-107">Como toocreate um suporte de pedidos.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-107">How toocreate a support request.</span></span>
* <span data-ttu-id="ca4ef-108">Como toostart uma sessão de suporte no Olá interface do Windows PowerShell do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-108">How toostart a support session in hello Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="ca4ef-109">Olá revisão [SLAs de suporte de série do StorSimple 8000 e informações](https://msdn.microsoft.com/library/mt433077.aspx) antes de criar um pedido de suporte.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-109">Review hello [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="ca4ef-110">Criar um pedido de suporte</span><span class="sxs-lookup"><span data-stu-id="ca4ef-110">Create a support request</span></span>
<span data-ttu-id="ca4ef-111">Execute os seguintes passos toocreate um pedido de suporte de Olá:</span><span class="sxs-lookup"><span data-stu-id="ca4ef-111">Perform hello following steps toocreate a support request:</span></span>

#### <a name="toocreate-a-support-request"></a><span data-ttu-id="ca4ef-112">toocreate um pedido de suporte</span><span class="sxs-lookup"><span data-stu-id="ca4ef-112">toocreate a support request</span></span>
1. <span data-ttu-id="ca4ef-113">No Olá [portal clássico do Azure](https://manage.windowsazure.com/), no Olá canto superior direito, clique em seu nome de conta e, em seguida, clique em **contactar o suporte da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-113">In hello [Azure classic portal](https://manage.windowsazure.com/), in hello upper right corner, click your account name and then click **Contact Microsoft Support**.</span></span>
   
    ![MS contacte o suporte através do ManagementPortal](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. <span data-ttu-id="ca4ef-115">Será redirecionado toohello novo portal do Azure (portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ca4ef-115">You will be redirected toohello new Azure portal (portal.azure.com).</span></span> <span data-ttu-id="ca4ef-116">Clique em Olá **novo pedido de suporte** mosaico.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-116">Click hello **New support request** tile.</span></span>
   
    ![MS contacte o suporte através do novo portal](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    <span data-ttu-id="ca4ef-118">No lado direito de Olá do ecrã de Olá, Olá **novo pedido de suporte** painel aparece.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-118">On hello right side of hello screen, hello **New support request** pane appears.</span></span> 
   
    ![Novo painel de pedido de suporte](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. <span data-ttu-id="ca4ef-120">No Olá **Noções básicas** caixa de diálogo, Olá concluir os seguintes:</span><span class="sxs-lookup"><span data-stu-id="ca4ef-120">In hello **Basics** dialog box, complete hello following:</span></span>                                
   
   1. <span data-ttu-id="ca4ef-121">De Olá **emitir tipo** na lista pendente, selecione **técnica**.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-121">From hello **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="ca4ef-122">Selecione um **subscrição** de Olá na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-122">Select a **Subscription** from hello drop-down list.</span></span>
   3. <span data-ttu-id="ca4ef-123">De Olá **serviço** na lista pendente, selecione **StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-123">From hello **Service** drop-down list, select **StorSimple**.</span></span> 
   4. <span data-ttu-id="ca4ef-124">Selecione um **plano de suporte** de Olá na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-124">Select a **Support plan** from hello drop-down list.</span></span> <span data-ttu-id="ca4ef-125">É necessário um tooenable do plano de suporte pago suporte técnico.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-125">You need a paid support plan tooenable Technical Support.</span></span>
4. <span data-ttu-id="ca4ef-126">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-126">Click **Next**.</span></span> <span data-ttu-id="ca4ef-127">Olá **problema** é apresentada a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-127">hello **Problem** dialog box appears.</span></span>
   
    ![Novo painel de pedido de suporte](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. <span data-ttu-id="ca4ef-129">No Olá **problema** caixa de diálogo, Olá concluir os seguintes:</span><span class="sxs-lookup"><span data-stu-id="ca4ef-129">In hello **Problem** dialog box, complete hello following:</span></span>
   
   1. <span data-ttu-id="ca4ef-130">Selecione um **gravidade** ao nível do Olá na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-130">Select a **Severity** level from hello drop-down list.</span></span>
   2. <span data-ttu-id="ca4ef-131">Selecione um **tipo de problema** de Olá na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-131">Select a **Problem type** from hello drop-down list.</span></span>
   3. <span data-ttu-id="ca4ef-132">Selecione um **categoria** de Olá na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-132">Select a **Category** from hello drop-down list.</span></span> 
   4. <span data-ttu-id="ca4ef-133">No Olá **detalhes** caixa, descreva resumidamente o seu problema.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-133">In hello **Details** box, briefly describe your issue.</span></span>
   5. <span data-ttu-id="ca4ef-134">No Olá **período de tempo** caixa, indique Olá data, hora e fuso horário que corresponde ao toohello ocorrência mais recente do seu problema.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-134">In hello **Time frame** box, indicate hello date, time, and time zone that corresponds toohello most recent occurrence of your issue.</span></span>
   6. <span data-ttu-id="ca4ef-135">Em **carregamento de ficheiros**, clique em pacote de suporte de tooyour ícone toobrowse Olá pasta.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-135">Under **File upload**, click hello folder icon toobrowse tooyour support package.</span></span>
   7. <span data-ttu-id="ca4ef-136">Selecione Olá **partilhar informações de diagnóstico** caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-136">Select hello **Share diagnostic information** check box.</span></span>
6. <span data-ttu-id="ca4ef-137">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-137">Click **Next**.</span></span> <span data-ttu-id="ca4ef-138">Olá **informações de contacto** é apresentada a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-138">hello **Contact information** dialog box appears.</span></span>
   
    ![Novo painel de pedido de suporte](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. <span data-ttu-id="ca4ef-140">Introduza as informações de contacto e selecione um método de contacto (telefone ou e-mail).</span><span class="sxs-lookup"><span data-stu-id="ca4ef-140">Enter your contact information and select a contact method (phone or email).</span></span> 
8. <span data-ttu-id="ca4ef-141">Selecione Olá **guardar alterações de contactos para futuros pedidos de suporte** caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-141">Select hello **Save contact changes for future support requests** check box.</span></span>
9. <span data-ttu-id="ca4ef-142">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-142">Click **Create**.</span></span>

<span data-ttu-id="ca4ef-143">Depois de ter submetido o pedido, um engenheiro de suporte irá contactá-lo logo que possível tooproceed com o seu pedido.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-143">After you have submitted your request, a Support engineer will contact you as soon as possible tooproceed with your request.</span></span>

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="ca4ef-144">Iniciar uma sessão de suporte no Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="ca4ef-144">Start a support session in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="ca4ef-145">tootroubleshoot os problemas que pode ocorrer com o dispositivo StorSimple Olá, terá de tooengage com a equipa do Olá Support da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-145">tootroubleshoot any issues that you might experience with hello StorSimple device, you will need tooengage with hello Microsoft Support team.</span></span> <span data-ttu-id="ca4ef-146">Support da Microsoft podem ter toouse um toolog de sessão de suporte no dispositivo tooyour.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-146">Microsoft Support may need toouse a support session toolog on tooyour device.</span></span> 

<span data-ttu-id="ca4ef-147">Execute o seguinte Olá passos toostart uma sessão de suporte:</span><span class="sxs-lookup"><span data-stu-id="ca4ef-147">Perform hello following steps toostart a support session:</span></span>

#### <a name="toostart-a-support-session"></a><span data-ttu-id="ca4ef-148">toostart uma sessão de suporte</span><span class="sxs-lookup"><span data-stu-id="ca4ef-148">toostart a support session</span></span>
1. <span data-ttu-id="ca4ef-149">Acesso Olá o dispositivo diretamente utilizando a consola de série de Olá ou através de uma sessão telnet a partir de um computador remoto.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-149">Access hello device directly by using hello serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="ca4ef-150">toodo, passos Olá siga [utilizar o PuTTY tooconnect toohello consola de série dispositivo](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="ca4ef-150">toodo this, follow hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="ca4ef-151">Na sessão de Olá que se abre, prima Olá **Enter** tooget chave numa linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-151">In hello session that opens, press hello **Enter** key tooget a command prompt.</span></span>
3. <span data-ttu-id="ca4ef-152">No menu da consola de série de Olá, selecione a opção 1, **iniciar sessão com acesso total**.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-152">In hello serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="ca4ef-153">Na linha de Olá, escreva Olá seguinte palavra-passe:</span><span class="sxs-lookup"><span data-stu-id="ca4ef-153">At hello prompt, type hello following password:</span></span> 
   
    `Password1`
5. <span data-ttu-id="ca4ef-154">Na linha de Olá, escreva Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="ca4ef-154">At hello prompt, type hello following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="ca4ef-155">Será apresentada uma cadeia encriptada tooyou.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-155">An encrypted string will be presented tooyou.</span></span> <span data-ttu-id="ca4ef-156">Copie esta cadeia para um editor de texto como o bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-156">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="ca4ef-157">Guarde esta cadeia e envie-num tooMicrosoft de mensagem de e-mail suporte.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-157">Save this string and send it in an email message tooMicrosoft Support.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ca4ef-158">Pode desativar o acesso de suporte executando `Disable-HcsSupportAccess`.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-158">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="ca4ef-159">o dispositivo StorSimple Olá também tentará toodisable suporte acesso 8 horas após a sessão de Olá foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-159">hello StorSimple device will also attempt toodisable support access 8 hours after hello session was initiated.</span></span> <span data-ttu-id="ca4ef-160">É uma melhor toochange de prática o dispositivo StorSimple credenciais depois de iniciar uma sessão de suporte.</span><span class="sxs-lookup"><span data-stu-id="ca4ef-160">It is a best practice toochange your StorSimple device credentials after initiating a support session.</span></span>
> 
> 

