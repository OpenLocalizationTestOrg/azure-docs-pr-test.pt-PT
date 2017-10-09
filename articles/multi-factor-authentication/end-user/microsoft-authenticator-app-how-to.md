---
title: "aplicação de autenticador aaaMicrosoft para telemóveis | Microsoft Docs"
description: "Saiba como tooupgrade toohello versão mais recente do Azure Authenticator."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: d895d92d89613cbafd9fc09d4ff4810cbf25652e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="c70bf-103">Introdução à aplicação do Microsoft Authenticator Olá</span><span class="sxs-lookup"><span data-stu-id="c70bf-103">Get started with hello Microsoft Authenticator app</span></span>
<span data-ttu-id="c70bf-104">Olá aplicação Authenticator da Microsoft fornece um nível adicional de segurança na sua conta escolar ou profissional (por exemplo, bsimon@contoso.com) ou a sua conta Microsoft (por exemplo, bsimon@outlook.com).</span><span class="sxs-lookup"><span data-stu-id="c70bf-104">hello Microsoft Authenticator app provides an additional level of security in your work or school account (for example, bsimon@contoso.com) or your Microsoft account (for example, bsimon@outlook.com).</span></span>

<span data-ttu-id="c70bf-105">Olá aplicação funciona de uma das seguintes formas:</span><span class="sxs-lookup"><span data-stu-id="c70bf-105">hello app works in one of two ways:</span></span>

* <span data-ttu-id="c70bf-106">**Notificação**.</span><span class="sxs-lookup"><span data-stu-id="c70bf-106">**Notification**.</span></span> <span data-ttu-id="c70bf-107">aplicação Olá pode ajudar a impedir o acesso não autorizado tooaccounts e parar as transações fraudulentas ao enviar uma notificação tooyour smartphone ou tablet.</span><span class="sxs-lookup"><span data-stu-id="c70bf-107">hello app can help prevent unauthorized access tooaccounts and stop fraudulent transactions by pushing a notification tooyour smartphone or tablet.</span></span> <span data-ttu-id="c70bf-108">Basta ver notificação Olá e se esta for legítima, selecionar **verifique**.</span><span class="sxs-lookup"><span data-stu-id="c70bf-108">Simply view hello notification, and if it's legitimate, select **Verify**.</span></span> <span data-ttu-id="c70bf-109">Caso contrário, pode selecionar **negar**.</span><span class="sxs-lookup"><span data-stu-id="c70bf-109">Otherwise, you can select **Deny**.</span></span> 
* <span data-ttu-id="c70bf-110">**Código de verificação**.</span><span class="sxs-lookup"><span data-stu-id="c70bf-110">**Verification code**.</span></span> <span data-ttu-id="c70bf-111">aplicação Olá pode ser utilizada como um software token toogenerate um código de verificação de OAuth.</span><span class="sxs-lookup"><span data-stu-id="c70bf-111">hello app can be used as a software token toogenerate an OAuth verification code.</span></span> <span data-ttu-id="c70bf-112">Depois de introduzir o nome de utilizador e palavra-passe, introduza código Olá fornecido pela aplicação Olá no ecrã de início de sessão Olá.</span><span class="sxs-lookup"><span data-stu-id="c70bf-112">After you enter your username and password, you enter hello code provided by hello app into hello sign-in screen.</span></span> <span data-ttu-id="c70bf-113">código de verificação Olá fornece uma segunda forma de autenticação.</span><span class="sxs-lookup"><span data-stu-id="c70bf-113">hello verification code provides a second form of authentication.</span></span>

<span data-ttu-id="c70bf-114">aplicação do Microsoft Authenticator Olá substitui Olá do Azure Authenticator.</span><span class="sxs-lookup"><span data-stu-id="c70bf-114">hello Microsoft Authenticator app replaces hello Azure Authenticator app.</span></span> <span data-ttu-id="c70bf-115">Olá do Azure Authenticator ainda funciona, mas se decidir toomove toohello Microsoft Authenticator nova aplicação, este artigo pode ajudá-lo.</span><span class="sxs-lookup"><span data-stu-id="c70bf-115">hello Azure Authenticator app still works, but if you decide toomove toohello new Microsoft Authenticator app, this article can assist you.</span></span>  

## <a name="opt-in-for-two-step-verification"></a><span data-ttu-id="c70bf-116">Optar por verificação de dois passos</span><span class="sxs-lookup"><span data-stu-id="c70bf-116">Opt in for two-step verification</span></span>

<span data-ttu-id="c70bf-117">aplicação do Microsoft Authenticator Olá não funciona por si só.</span><span class="sxs-lookup"><span data-stu-id="c70bf-117">hello Microsoft Authenticator app doesn't work by itself.</span></span> <span data-ttu-id="c70bf-118">Configure cada um dos seus tooprompt de contas para um segundo método de verificação depois de iniciar sessão com o nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="c70bf-118">Configure each of your accounts tooprompt you for a second verification method after you sign in with your username and password.</span></span> 

<span data-ttu-id="c70bf-119">Para uma conta escolar ou profissional, não normalmente obtiver toochoose esta funcionalidade para si próprio.</span><span class="sxs-lookup"><span data-stu-id="c70bf-119">For a work or school account, you don't usually get toochoose this feature for yourself.</span></span> <span data-ttu-id="c70bf-120">Em vez disso, um administrador de segurança de optar por participar ativamente em seu nome e, em seguida, notifica-o tooregister métodos de verificação para a sua conta.</span><span class="sxs-lookup"><span data-stu-id="c70bf-120">Instead, a security administrator opts in on your behalf and then notifies you tooregister verification methods for your account.</span></span> <span data-ttu-id="c70bf-121">Se este cenário aplica-se tooyou, saiba mais em [que Azure multi-factor Authentication significa para me permitir](multi-factor-authentication-end-user.md).</span><span class="sxs-lookup"><span data-stu-id="c70bf-121">If this scenario applies tooyou, learn more in [What does Azure Multi-Factor Authentication mean for me](multi-factor-authentication-end-user.md).</span></span>

<span data-ttu-id="c70bf-122">Para uma conta pessoal, terá de tooset se a verificação de dois passos para si próprio.</span><span class="sxs-lookup"><span data-stu-id="c70bf-122">For a personal account, you need tooset up two-step verification for yourself.</span></span> <span data-ttu-id="c70bf-123">Se tiver uma conta Microsoft, estão disponíveis nesses passos [sobre a verificação de dois passos](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span><span class="sxs-lookup"><span data-stu-id="c70bf-123">If you have a Microsoft account, those steps are available in [About two-step verification](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span></span> 

<span data-ttu-id="c70bf-124">Também pode utilizar Olá Microsoft Authenticator com contas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="c70bf-124">You can also use hello Microsoft Authenticator with non-Microsoft accounts.</span></span> <span data-ttu-id="c70bf-125">Pode chamar funcionalidade Olá de algo diferente de verificação em dois passos, mas deve ser capaz de toofind-lo com as definições de segurança ou início de sessão.</span><span class="sxs-lookup"><span data-stu-id="c70bf-125">They may call hello feature something other than two-step verification, but you should be able toofind it under security or sign-in settings.</span></span> 

## <a name="install-hello-app"></a><span data-ttu-id="c70bf-126">Instalar aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="c70bf-126">Install hello app</span></span>
<span data-ttu-id="c70bf-127">aplicação do Microsoft Authenticator Olá está disponível para [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), e [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span><span class="sxs-lookup"><span data-stu-id="c70bf-127">hello Microsoft Authenticator app is available for [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), and [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span></span>

## <a name="add-accounts-toohello-app"></a><span data-ttu-id="c70bf-128">Adicionar contas toohello aplicação</span><span class="sxs-lookup"><span data-stu-id="c70bf-128">Add accounts toohello app</span></span>
<span data-ttu-id="c70bf-129">Para cada conta que pretende que a aplicação de Microsoft Authenticator tooadd toohello, utilize um dos Olá os seguintes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="c70bf-129">For each account that you want tooadd toohello Microsoft Authenticator app, use one of hello following procedures:</span></span>

### <a name="add-a-personal-microsoft-account-toohello-app"></a><span data-ttu-id="c70bf-130">Adicionar uma aplicação toohello da conta Microsoft pessoal</span><span class="sxs-lookup"><span data-stu-id="c70bf-130">Add a personal Microsoft account toohello app</span></span>

<span data-ttu-id="c70bf-131">Para uma conta Microsoft pessoal (um que utilize toosign no tooOutlook.com, Xbox, Skype, etc.), tudo tiver toodo é inicie sessão na conta tooyour na aplicação do Microsoft Authenticator Olá.</span><span class="sxs-lookup"><span data-stu-id="c70bf-131">For a personal Microsoft account (one that you use toosign in tooOutlook.com, Xbox, Skype, etc.), all you have toodo is sign in tooyour account in hello Microsoft Authenticator app.</span></span>

### <a name="add-a-work-or-school-account-toohello-app-using-hello-qr-code-scanner"></a><span data-ttu-id="c70bf-132">Adicionar um trabalho ou escola utilizando scanner de código Olá QR toohello aplicação da conta</span><span class="sxs-lookup"><span data-stu-id="c70bf-132">Add a work or school account toohello app using hello QR code scanner</span></span>
1. <span data-ttu-id="c70bf-133">Visite o ecrã de definições de verificação de segurança toohello.</span><span class="sxs-lookup"><span data-stu-id="c70bf-133">Go toohello security verification settings screen.</span></span>  <span data-ttu-id="c70bf-134">Para obter informações sobre como tooget toothis ecrã, consulte [alterar as definições de segurança](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span><span class="sxs-lookup"><span data-stu-id="c70bf-134">For information on how tooget toothis screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span></span>
2. <span data-ttu-id="c70bf-135">Olá caixa de verificação-demasiado junto**aplicação de autenticação** , em seguida, selecione **configurar**.</span><span class="sxs-lookup"><span data-stu-id="c70bf-135">Check hello box next too**Authenticator app** then select **Configure**.</span></span>

    ![botão de configurar Olá no ecrã de definições de verificação de segurança de Olá](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="c70bf-137">Isto apresenta um ecrã com um código QR no mesmo.</span><span class="sxs-lookup"><span data-stu-id="c70bf-137">This brings up a screen with a QR code on it.</span></span>

    ![Ecrã fornece código Olá QR](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="c70bf-139">Aplicação do Microsoft Authenticator Olá aberta.</span><span class="sxs-lookup"><span data-stu-id="c70bf-139">Open hello Microsoft Authenticator app.</span></span> <span data-ttu-id="c70bf-140">No Olá **contas** ecrã, selecione  **+** e, em seguida, especifique que pretende que o tooadd uma conta escolar ou profissional.</span><span class="sxs-lookup"><span data-stu-id="c70bf-140">On hello **accounts** screen, select **+**, and then specify that you want tooadd a work or school account.</span></span>
4. <span data-ttu-id="c70bf-141">Utilizar Olá câmara tooscan Olá QR código e, em seguida, selecione **feito** ecrã de código tooclose Olá QR.</span><span class="sxs-lookup"><span data-stu-id="c70bf-141">Use hello camera tooscan hello QR code, and then select **Done** tooclose hello QR code screen.</span></span>

    <span data-ttu-id="c70bf-142">Se a câmara não está a funcionar corretamente, pode [introduzir manualmente o código de Olá QR e o URL](#add-an-account-to-the-app-manually).</span><span class="sxs-lookup"><span data-stu-id="c70bf-142">If your camera is not working properly, you can [enter hello QR code and URL manually](#add-an-account-to-the-app-manually).</span></span>

5. <span data-ttu-id="c70bf-143">Quando a aplicação Olá mostra o nome da sua conta com um código de seis dígitos por baixo, terminar.</span><span class="sxs-lookup"><span data-stu-id="c70bf-143">When hello app shows your account name with a six-digit code underneath it, you're done.</span></span> 

    ![Ecrã de contas](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-manually"></a><span data-ttu-id="c70bf-145">Adicionar uma aplicação da conta toohello manualmente</span><span class="sxs-lookup"><span data-stu-id="c70bf-145">Add an account toohello app manually</span></span>
1. <span data-ttu-id="c70bf-146">Visite o ecrã de definições de verificação de segurança toohello.</span><span class="sxs-lookup"><span data-stu-id="c70bf-146">Go toohello security verification settings screen.</span></span>  <span data-ttu-id="c70bf-147">Para obter informações sobre como tooget toothis ecrã, consulte [alterar as definições de segurança](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="c70bf-147">For information on how tooget toothis screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>
2. <span data-ttu-id="c70bf-148">Selecione **configurar**.</span><span class="sxs-lookup"><span data-stu-id="c70bf-148">Select **Configure**.</span></span>

    ![botão de configurar Olá no ecrã de definições de verificação de segurança de Olá](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="c70bf-150">Isto apresenta um ecrã com um código QR no mesmo.</span><span class="sxs-lookup"><span data-stu-id="c70bf-150">This brings up a screen with a QR code on it.</span></span>  <span data-ttu-id="c70bf-151">Tenha em atenção Olá código e o URL.</span><span class="sxs-lookup"><span data-stu-id="c70bf-151">Note hello code and URL.</span></span>

    ![Ecrã fornece código Olá QR e o URL](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="c70bf-153">Aplicação do Microsoft Authenticator Olá aberta.</span><span class="sxs-lookup"><span data-stu-id="c70bf-153">Open hello Microsoft Authenticator app.</span></span> <span data-ttu-id="c70bf-154">No Olá **contas** ecrã, selecione  **+** e, em seguida, especifique que pretende que o tooadd uma conta escolar ou profissional.</span><span class="sxs-lookup"><span data-stu-id="c70bf-154">On hello **accounts** screen, select **+**, and then specify that you want tooadd a work or school account.</span></span>

4. <span data-ttu-id="c70bf-155">Em detetor de Olá, selecione **introduzir manualmente o código**.</span><span class="sxs-lookup"><span data-stu-id="c70bf-155">In hello scanner, select **enter code manually**.</span></span>

    ![Ecrã de análise de um código QR](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. <span data-ttu-id="c70bf-157">Introduza o código de Olá e o URL de Olá nas caixas adequadas do Olá na aplicação Olá, em seguida, selecione **concluir**.</span><span class="sxs-lookup"><span data-stu-id="c70bf-157">Enter hello code and hello URL in hello appropriate boxes in hello app, then select **Finish**.</span></span>

    ![Ecrã para introduzir o código e o URL](./media/authenticator-app-how-to/manual.png)

6. <span data-ttu-id="c70bf-159">Quando a aplicação Olá mostra o nome da sua conta com um código de seis dígitos por baixo, terminar.</span><span class="sxs-lookup"><span data-stu-id="c70bf-159">When hello app shows your account name with a six-digit code underneath it, you're done.</span></span>

    ![Ecrã de contas](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-using-touch-id"></a><span data-ttu-id="c70bf-161">Adicionar uma aplicação da conta toohello utilizar o Touch ID</span><span class="sxs-lookup"><span data-stu-id="c70bf-161">Add an account toohello app using Touch ID</span></span>
<span data-ttu-id="c70bf-162">aplicação do Microsoft Authenticator Olá no iOS suporta Touch ID.</span><span class="sxs-lookup"><span data-stu-id="c70bf-162">hello Microsoft Authenticator app on iOS supports Touch ID.</span></span>  <span data-ttu-id="c70bf-163">Multi-factor Authentication do Azure permite que as organizações toorequire um PIN para dispositivos.</span><span class="sxs-lookup"><span data-stu-id="c70bf-163">Azure Multi-Factor Authentication allows organizations toorequire a PIN for devices.</span></span> <span data-ttu-id="c70bf-164">Com o Touch ID, utilizadores do iOS não precisam de tooenter um PIN.</span><span class="sxs-lookup"><span data-stu-id="c70bf-164">With Touch ID, iOS users don’t need tooenter a PIN.</span></span> <span data-ttu-id="c70bf-165">Em vez disso, pode analisar a respetiva impressão digital e selecione **aprovar**.</span><span class="sxs-lookup"><span data-stu-id="c70bf-165">Instead, they can scan their fingerprint and select **Approve**.</span></span>

<span data-ttu-id="c70bf-166">Configurar o Touch ID com o Microsoft Authenticator é simple.</span><span class="sxs-lookup"><span data-stu-id="c70bf-166">Setting up Touch ID with Microsoft Authenticator is simple.</span></span> <span data-ttu-id="c70bf-167">Conclua um desafio de verificação normal com um PIN.</span><span class="sxs-lookup"><span data-stu-id="c70bf-167">You complete a normal verification challenge with a PIN.</span></span> <span data-ttu-id="c70bf-168">Se o dispositivo suporta Touch ID, Microsoft Authenticator define-automaticamente para essa conta.</span><span class="sxs-lookup"><span data-stu-id="c70bf-168">If your device supports Touch ID, Microsoft Authenticator sets it up automatically for that account.</span></span>

![Verificação da configuração de Touch ID](./media/authenticator-app-how-to/touchid1.png)

<span data-ttu-id="c70bf-170">A partir do que ponto reencaminhar, quando estiver necessário tooverify o início de sessão, selecione a notificação push de Olá recebido e analisar a sua impressão digital em vez de introduzir o PIN.</span><span class="sxs-lookup"><span data-stu-id="c70bf-170">From that point forward, when you're required tooverify your sign-in, you select hello received push notification and scan your fingerprint instead of entering your PIN.</span></span>

![Notificação Push](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-hello-app-when-you-sign-in"></a><span data-ttu-id="c70bf-172">Utilizar a aplicação Olá quando iniciar sessão</span><span class="sxs-lookup"><span data-stu-id="c70bf-172">Use hello app when you sign in</span></span>

<span data-ttu-id="c70bf-173">Assim que a conta é adicionada toohello aplicação, poderá ser pedido toodo um toomake de verificação de teste se de que tudo foi corretamente configurado.</span><span class="sxs-lookup"><span data-stu-id="c70bf-173">Once your account is added toohello app, you may be prompted toodo a test verification toomake sure everything was configured correctly.</span></span> <span data-ttu-id="c70bf-174">Depois disso, está concluído!</span><span class="sxs-lookup"><span data-stu-id="c70bf-174">After that, you're done!</span></span> <span data-ttu-id="c70bf-175">Não precisa de toodo há mais alguma coisa até hello próxima vez que iniciar sessão.</span><span class="sxs-lookup"><span data-stu-id="c70bf-175">You don't need toodo anything else until hello next time you sign in.</span></span>

<span data-ttu-id="c70bf-176">Se tiver escolhido toouse códigos de verificação na aplicação Olá, iniciar toosee-las na Olá home page.</span><span class="sxs-lookup"><span data-stu-id="c70bf-176">If you chose toouse verification codes in hello app, you start toosee them on hello home page.</span></span> <span data-ttu-id="c70bf-177">Se alterar a cada 30 segundos para que tenham sempre um novo código quando precisa de uma.</span><span class="sxs-lookup"><span data-stu-id="c70bf-177">They change every 30 seconds so that you always have a new code when you need one.</span></span> <span data-ttu-id="c70bf-178">Mas não precisa de toodo nada com as mesmas até a iniciar sessão e são tooenter pedido um código de verificação.</span><span class="sxs-lookup"><span data-stu-id="c70bf-178">But you don't need toodo anything with them until you sign in and are prompted tooenter a verification code.</span></span>  
