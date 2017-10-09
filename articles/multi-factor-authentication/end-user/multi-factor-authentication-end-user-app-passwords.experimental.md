---
title: "aaaHow toouse palavras-passe de aplicação no Azure MFA? | Microsoft Docs"
description: "Esta página irá ajudar os utilizadores a compreenderem quais são as palavras-passe de aplicação e o que são utilizados para com regard tooAzure MFA."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 3afa2003d8e87576f035bf9440a1dba67bd85f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a><span data-ttu-id="095c8-104">Quais são palavras-passe de aplicação no Azure multi-factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="095c8-104">What are App Passwords in Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="095c8-105">Determinadas aplicações não baseadas no browser, como o cliente de e-mail nativa de Apple Olá que utiliza o Exchange Active Sync, atualmente não suportam autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="095c8-105">Certain non-browser apps, such as hello Apple native email client that uses Exchange Active Sync, currently do not support multi-factor authentication.</span></span> <span data-ttu-id="095c8-106">Autenticação multifator é ativada por utilizador.</span><span class="sxs-lookup"><span data-stu-id="095c8-106">Multi-factor authentication is enabled per user.</span></span>  <span data-ttu-id="095c8-107">Isto significa que um utilizador não é possível utilizar a autenticação multifator se:</span><span class="sxs-lookup"><span data-stu-id="095c8-107">This means that a user can't use multi-factor authentication if:</span></span>

- <span data-ttu-id="095c8-108">utilizador Olá foi ativada para autenticação multifator</span><span class="sxs-lookup"><span data-stu-id="095c8-108">hello user has been enabled for multi-factor authentication</span></span>
- <span data-ttu-id="095c8-109">utilizador Olá está a tentar toouse uma aplicação não baseadas no browser.</span><span class="sxs-lookup"><span data-stu-id="095c8-109">hello user is trying toouse a non-browser app.</span></span>

<span data-ttu-id="095c8-110">Uma palavra-passe de aplicação permite Olá utilizador toouse Olá aplicação.</span><span class="sxs-lookup"><span data-stu-id="095c8-110">An app password allows hello user toouse hello app.</span></span>

<span data-ttu-id="095c8-111">Assim que tiver uma palavra-passe de aplicação, utilize-o em vez da palavra-passe original com estas aplicações não baseadas no browser.</span><span class="sxs-lookup"><span data-stu-id="095c8-111">Once you have an app password, you use it in place of your original password with these non-browser apps.</span></span> <span data-ttu-id="095c8-112">Ao registar para a verificação de dois passos, está a informar Microsoft não toolet qualquer pessoa iniciar sessão com a sua palavra-passe se estes também não é possível efetuar a verificação de segundo Olá.</span><span class="sxs-lookup"><span data-stu-id="095c8-112">When you register for two-step verification, you're telling Microsoft not toolet anyone sign in with your password if they can't also perform hello second verification.</span></span> <span data-ttu-id="095c8-113">cliente de e-mail nativo Olá Apple no seu telemóvel não pode iniciar sessão como porque não é possível pedir a verificação.</span><span class="sxs-lookup"><span data-stu-id="095c8-113">hello Apple native email client on your phone can't sign in as you because it can't ask for two-step verification.</span></span> <span data-ttu-id="095c8-114">Olá solução toothis problema é toocreate uma mais segura palavra-passe de aplicação não utilizar diárias.</span><span class="sxs-lookup"><span data-stu-id="095c8-114">hello solution toothis problem is toocreate a more secure app password that you don't use day-to-day.</span></span> <span data-ttu-id="095c8-115">As palavras-passe de aplicação são apenas para essas aplicações que não suportem a verificação de dois passos.</span><span class="sxs-lookup"><span data-stu-id="095c8-115">App passwords are only for those apps that can't support two-step verification.</span></span> <span data-ttu-id="095c8-116">Utilize Olá palavra-passe para que as aplicações podem ignorar multi-factor authentication e continuar toowork.</span><span class="sxs-lookup"><span data-stu-id="095c8-116">Use hello app password so that apps can bypass multi-factor authentication and continue toowork.</span></span>


> [!NOTE]
> <span data-ttu-id="095c8-117">Clientes do Office 2013 (incluindo o Outlook) suportam o novo protocolos de autenticação e pode ser utilizado com verificação de dois passos.</span><span class="sxs-lookup"><span data-stu-id="095c8-117">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span></span> <span data-ttu-id="095c8-118">As palavras-passe de aplicação não são necessárias para utilização com clientes do Office 2013.</span><span class="sxs-lookup"><span data-stu-id="095c8-118">App passwords are not required for use with Office 2013 clients.</span></span>  <span data-ttu-id="095c8-119">Para obter mais informações, consulte [Office 2013 autenticação moderna pré-visualização pública anunciada](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span><span class="sxs-lookup"><span data-stu-id="095c8-119">For more information, see [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span></span>


## <a name="how-toouse-app-passwords"></a><span data-ttu-id="095c8-120">Como toouse palavras-passe de aplicação</span><span class="sxs-lookup"><span data-stu-id="095c8-120">How toouse app passwords</span></span>
<span data-ttu-id="095c8-121">Seguem-se algumas tooknow coisas sobre palavras-passe de aplicação:</span><span class="sxs-lookup"><span data-stu-id="095c8-121">Here are some things tooknow about app passwords:</span></span>

* <span data-ttu-id="095c8-122">Não crie as suas próprias palavras-passe de aplicação.</span><span class="sxs-lookup"><span data-stu-id="095c8-122">You don't create your own app passwords.</span></span> <span data-ttu-id="095c8-123">São geradas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="095c8-123">They are automatically generated.</span></span>
* <span data-ttu-id="095c8-124">Atualmente não há um limite de 40 palavras-passe por utilizador.</span><span class="sxs-lookup"><span data-stu-id="095c8-124">Currently there is a limit of 40 passwords per user.</span></span> 
* <span data-ttu-id="095c8-125">Se tentar toocreate uma palavra-passe de aplicação após ter atingido o limite de Olá, terá de toodelete uma das suas palavras-passe de aplicação existentes antes de criar um novo.</span><span class="sxs-lookup"><span data-stu-id="095c8-125">If you try toocreate an app password after you have reached hello limit, you'll have toodelete one of your existing app passwords before you create a new one.</span></span>
* <span data-ttu-id="095c8-126">Utilize uma palavra-passe por dispositivo, não por aplicação.</span><span class="sxs-lookup"><span data-stu-id="095c8-126">Use one app password per device, not per application.</span></span> <span data-ttu-id="095c8-127">Por exemplo, pode criar uma palavra-passe de aplicação para o seu computador portátil e utilizar essa palavra-passe de aplicação para todas as aplicações desse portátil.</span><span class="sxs-lookup"><span data-stu-id="095c8-127">For example, you can create one app password for your laptop and use that app password for all of your applications on that laptop.</span></span> <span data-ttu-id="095c8-128">Em seguida, crie uma segunda toouse de palavra-passe de aplicação para todas as suas aplicações no seu ambiente de trabalho.</span><span class="sxs-lookup"><span data-stu-id="095c8-128">Then, create a second app password toouse for all your apps on your desktop.</span></span> 
* <span data-ttu-id="095c8-129">É-lhe dada uma Olá de palavra-passe de aplicação pela primeira vez a que registar para a verificação de dois passos.</span><span class="sxs-lookup"><span data-stu-id="095c8-129">You are given one app password hello first time you register for two-step verification.</span></span>  <span data-ttu-id="095c8-130">Se precisar de adicionais, pode criá-los.</span><span class="sxs-lookup"><span data-stu-id="095c8-130">If you need additional ones, you can create them.</span></span>



## <a name="creating-and-deleting-app-passwords"></a><span data-ttu-id="095c8-131">Criar e eliminar as palavras-passe de aplicação</span><span class="sxs-lookup"><span data-stu-id="095c8-131">Creating and deleting app passwords</span></span>
<span data-ttu-id="095c8-132">Durante a sua inicial início de sessão, é-lhe dada uma palavra-passe de aplicação que pode utilizar.</span><span class="sxs-lookup"><span data-stu-id="095c8-132">During your initial sign-in, you are given an app password that you can use.</span></span>  <span data-ttu-id="095c8-133">Também pode criar e eliminar as palavras-passe de aplicação mais tarde.</span><span class="sxs-lookup"><span data-stu-id="095c8-133">You can also create and delete app passwords later on.</span></span> <span data-ttu-id="095c8-134">Como eliminar palavras-passe de aplicação depende de como utilizar a autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="095c8-134">How you delete app passwords depends on how you use multi-factor authentication.</span></span> <span data-ttu-id="095c8-135">Olá resposta seguintes questões de toodetermine onde deve passar toomanage palavras-passe de aplicação:</span><span class="sxs-lookup"><span data-stu-id="095c8-135">Answer hello following questions toodetermine where you should go toomanage app passwords:</span></span> 

1. <span data-ttu-id="095c8-136">Utiliza a verificação da sua conta Microsoft pessoal?</span><span class="sxs-lookup"><span data-stu-id="095c8-136">Do you use two-step verification for your personal Microsoft account?</span></span> <span data-ttu-id="095c8-137">Se Sim, devem consultar toohello [palavras-passe de aplicação e a verificação de dois passos](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) artigo para obter ajuda.</span><span class="sxs-lookup"><span data-stu-id="095c8-137">If yes, you should refer toohello [App passwords and two-step verification](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article for help.</span></span> <span data-ttu-id="095c8-138">Se não, continue tooquestion dois.</span><span class="sxs-lookup"><span data-stu-id="095c8-138">If no, continue tooquestion two.</span></span>

2. <span data-ttu-id="095c8-139">OK, pelo que utilizar a verificação de dois passos para a sua conta escolar ou profissional.</span><span class="sxs-lookup"><span data-stu-id="095c8-139">Ok, so you use two-step verification for your work or school account.</span></span> <span data-ttu-id="095c8-140">A utilizar toosign tooOffice 365 aplicações?</span><span class="sxs-lookup"><span data-stu-id="095c8-140">Do you use it toosign in tooOffice 365 apps?</span></span> <span data-ttu-id="095c8-141">Se Sim, deve consultar demasiado[criar uma palavra-passe de aplicação para o Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) para obter ajuda.</span><span class="sxs-lookup"><span data-stu-id="095c8-141">If yes, you should refer too[Create an app password for Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) for help.</span></span> <span data-ttu-id="095c8-142">Se não, continue tooquestion três.</span><span class="sxs-lookup"><span data-stu-id="095c8-142">If no, continue tooquestion three.</span></span> 

3. <span data-ttu-id="095c8-143">Utiliza a verificação com o Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="095c8-143">Do you use two-step verification with Microsoft Azure?</span></span> <span data-ttu-id="095c8-144">Se Sim, continuar toohello [gerir palavras-passe de aplicação no portal do Azure de Olá](#manage-app-passwords-in-the-Azure-portal) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="095c8-144">If yes, continue toohello [Manage app passwords in hello Azure portal](#manage-app-passwords-in-the-Azure-portal) section of this article.</span></span> <span data-ttu-id="095c8-145">Se não, continue tooquestion quatro.</span><span class="sxs-lookup"><span data-stu-id="095c8-145">If no, continue tooquestion four.</span></span>

4. <span data-ttu-id="095c8-146">Não tem a certeza, quando utiliza a verificação de dois passos?</span><span class="sxs-lookup"><span data-stu-id="095c8-146">Not sure where you use two-step verification?</span></span> <span data-ttu-id="095c8-147">Continuar toohello [gerir palavras-passe de aplicação com o portal de MyApps Olá](#manage-app-passwords-with-the-myapps-portal) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="095c8-147">Continue toohello [Manage app passwords with hello MyApps portal](#manage-app-passwords-with-the-myapps-portal) section of this article.</span></span> 


## <a name="manage-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="095c8-148">Gerir palavras-passe de aplicação no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="095c8-148">Manage app passwords in hello Azure portal</span></span>
<span data-ttu-id="095c8-149">Se utilizar a verificação com o Azure, quer palavras-passe de aplicação de toocreate através de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="095c8-149">If you use two-step verification with Azure, you want toocreate app passwords through hello Azure portal.</span></span>

### <a name="toocreate-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="095c8-150">palavras-passe de aplicação de toocreate no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="095c8-150">toocreate app passwords in hello Azure portal</span></span>
1. <span data-ttu-id="095c8-151">Inicie sessão no toohello portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="095c8-151">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="095c8-152">Na parte superior do Olá, o nome de utilizador com o botão direito e selecione a verificação de segurança adicional.</span><span class="sxs-lookup"><span data-stu-id="095c8-152">At hello top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="095c8-153">Na página de proofup Olá, na parte superior do Olá, selecione as palavras-passe de aplicação</span><span class="sxs-lookup"><span data-stu-id="095c8-153">On hello proofup page, at hello top, select app passwords</span></span>
4. <span data-ttu-id="095c8-154">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="095c8-154">Click **Create**.</span></span>
5. <span data-ttu-id="095c8-155">Introduza um nome para a palavra-passe de aplicação de Olá e clique em **seguinte**</span><span class="sxs-lookup"><span data-stu-id="095c8-155">Enter a name for hello app password and click **Next**</span></span>
6. <span data-ttu-id="095c8-156">Copie a área de transferência do Olá aplicação palavra-passe toohello e cole-o sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="095c8-156">Copy hello app password toohello clipboard and paste it into your app.</span></span>
   
   ![Nuvem](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="toodelete-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="095c8-158">palavras-passe de aplicação de toodelete no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="095c8-158">toodelete app passwords in hello Azure portal</span></span>
1. <span data-ttu-id="095c8-159">Inicie sessão no toohello portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="095c8-159">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="095c8-160">Na parte superior do Olá, o nome de utilizador com o botão direito e selecione a verificação de segurança adicional.</span><span class="sxs-lookup"><span data-stu-id="095c8-160">At hello top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="095c8-161">Na parte superior de Olá, verificação de segurança tooadditional seguinte, selecione **palavras-passe de aplicação.**</span><span class="sxs-lookup"><span data-stu-id="095c8-161">At hello top, next tooadditional security verification, select **app passwords.**</span></span>
4. <span data-ttu-id="095c8-162">Seguinte toohello palavra-passe que pretende toodelete, selecione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="095c8-162">Next toohello app password you want toodelete, select **Delete**.</span></span>
5. <span data-ttu-id="095c8-163">Confirmar eliminação de Olá clicando **Sim**.</span><span class="sxs-lookup"><span data-stu-id="095c8-163">Confirm hello deletion by clicking **yes**.</span></span>
6. <span data-ttu-id="095c8-164">Assim que a palavra-passe de aplicação de Olá é eliminado, pode clicar em **fechar**.</span><span class="sxs-lookup"><span data-stu-id="095c8-164">Once hello app password is deleted, you can click **close**.</span></span>


## <a name="manage-app-passwords-with-hello-myapps-portal"></a><span data-ttu-id="095c8-165">Gerir palavras-passe de aplicação com o portal do Olá MyApps.</span><span class="sxs-lookup"><span data-stu-id="095c8-165">Manage app passwords with hello MyApps portal.</span></span>
<span data-ttu-id="095c8-166">Se não tem a certeza de como utilizar a autenticação multifator, em seguida, pode sempre criar e eliminar palavras-passe de aplicação através do portal Olá myapps.</span><span class="sxs-lookup"><span data-stu-id="095c8-166">If you are not sure how you use multi-factor authentication, then you can always create and delete app passwords through hello myapps portal.</span></span>

### <a name="toocreate-an-app-password-using-hello-myapps-portal"></a><span data-ttu-id="095c8-167">uma palavra-passe de aplicação através de toocreate Olá Myapps portal</span><span class="sxs-lookup"><span data-stu-id="095c8-167">toocreate an app password using hello Myapps portal</span></span>
1. <span data-ttu-id="095c8-168">A iniciar sessão demasiado[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="095c8-168">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="095c8-169">Clique no seu nome no canto superior Olá direito e selecione **perfil**.</span><span class="sxs-lookup"><span data-stu-id="095c8-169">Click your name at hello top right, and choose **Profile**.</span></span>
3. <span data-ttu-id="095c8-170">Selecione **verificação adicional de segurança**.</span><span class="sxs-lookup"><span data-stu-id="095c8-170">Select **Additional Security Verification**.</span></span>
   <span data-ttu-id="095c8-171">![Selecione verificação adicional de segurança - captura de ecrã](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span><span class="sxs-lookup"><span data-stu-id="095c8-171">![Select additional security verification - screenshot](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span></span>

4. <span data-ttu-id="095c8-172">Selecione **palavras-passe de aplicação**.</span><span class="sxs-lookup"><span data-stu-id="095c8-172">Select **app passwords**.</span></span>
   <span data-ttu-id="095c8-173">![Selecione as palavras-passe de aplicação - captura de ecrã](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span><span class="sxs-lookup"><span data-stu-id="095c8-173">![Select app passwords - screenshot](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span></span>

5. <span data-ttu-id="095c8-174">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="095c8-174">Click **Create**.</span></span>
6. <span data-ttu-id="095c8-175">Introduza um nome para a palavra-passe de aplicação de Olá e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="095c8-175">Enter a name for hello app password and click **Next**.</span></span>
7. <span data-ttu-id="095c8-176">Copie a área de transferência do Olá aplicação palavra-passe toohello e cole-o sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="095c8-176">Copy hello app password toohello clipboard and paste it into your app.</span></span>
   <span data-ttu-id="095c8-177">![Criar uma palavra-passe de aplicação](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span><span class="sxs-lookup"><span data-stu-id="095c8-177">![Create an app password](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span></span>

### <a name="toodelete-an-app-password-using-hello-myapps-portal"></a><span data-ttu-id="095c8-178">uma palavra-passe de aplicação através de toodelete Olá Myapps portal</span><span class="sxs-lookup"><span data-stu-id="095c8-178">toodelete an app password using hello Myapps portal</span></span>
1. <span data-ttu-id="095c8-179">A iniciar sessão demasiado[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="095c8-179">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="095c8-180">Na parte superior do Olá, selecione o perfil.</span><span class="sxs-lookup"><span data-stu-id="095c8-180">At hello top, select profile.</span></span>
3. <span data-ttu-id="095c8-181">Selecione **verificação adicional de segurança**.</span><span class="sxs-lookup"><span data-stu-id="095c8-181">Select **Additional Security Verification**.</span></span>

   ![Selecione verificação adicional de segurança - captura de ecrã](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. <span data-ttu-id="095c8-183">Selecione **palavras-passe de aplicação**.</span><span class="sxs-lookup"><span data-stu-id="095c8-183">Select **app passwords**.</span></span>

   ![Selecione as palavras-passe de aplicação - captura de ecrã](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. <span data-ttu-id="095c8-185">Clique em seguinte toohello palavra-passe que pretende toodelete, **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="095c8-185">Next toohello app password you want toodelete, click **Delete**.</span></span>

   ![Eliminar uma palavra-passe de aplicação](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. <span data-ttu-id="095c8-187">Confirmar que pretende que toodelete essa palavra-passe clicando **Sim**.</span><span class="sxs-lookup"><span data-stu-id="095c8-187">Confirm that you want toodelete that password by clicking **yes**.</span></span>
7. <span data-ttu-id="095c8-188">Assim que a palavra-passe de aplicação de Olá é eliminado, pode clicar em **fechar**.</span><span class="sxs-lookup"><span data-stu-id="095c8-188">Once hello app password is deleted, you can click **close**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="095c8-189">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="095c8-189">Next steps</span></span>

- [<span data-ttu-id="095c8-190">Gerir as definições da verificação de dois passos</span><span class="sxs-lookup"><span data-stu-id="095c8-190">Manage your two-step verification settings</span></span>](multi-factor-authentication-end-user-manage-settings.md)

- <span data-ttu-id="095c8-191">Experimentar Olá [aplicação Microsoft Authenticator](microsoft-authenticator-app-how-to.md) tooverify os inícios de sessão com as notificações de aplicação, em vez de textos ou chamadas a receber.</span><span class="sxs-lookup"><span data-stu-id="095c8-191">Try out hello [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) tooverify your sign-ins with app notifications, instead of receiving texts or calls.</span></span> 
