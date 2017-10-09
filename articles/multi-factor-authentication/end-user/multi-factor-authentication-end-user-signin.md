---
title: "aaaAzure MFA inicie sessão com a verificação de dois passos | Microsoft Docs"
description: "Esta página será fornecem orientações sobre onde toogo toosee Olá vários início de sessão métodos disponíveis com a MFA do Azure."
keywords: "autenticação de utilizador, o início de sessão experiência, início de sessão com o telemóvel, início de sessão com o telefone do escritório"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a><span data-ttu-id="7a9ea-104">Olá início de sessão experiência com multi-factor Authentication do Azure</span><span class="sxs-lookup"><span data-stu-id="7a9ea-104">hello sign-in experience with Azure Multi-Factor Authentication</span></span>
> [!NOTE]
> <span data-ttu-id="7a9ea-105">objetivo Olá este artigo é toowalk através de uma experiência de início de sessão normal.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-105">hello purpose of this article is toowalk through a typical sign-in experience.</span></span> <span data-ttu-id="7a9ea-106">Para obter ajuda com início de sessão, ou tootroubleshoot problemas, consulte [problemas com o Azure multi-factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="7a9ea-106">For help with signing in, or tootroubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

## <a name="what-will-your-sign-in-experience-be"></a><span data-ttu-id="7a9ea-107">O que será a experiência de início de sessão?</span><span class="sxs-lookup"><span data-stu-id="7a9ea-107">What will your sign-in experience be?</span></span>
<span data-ttu-id="7a9ea-108">A experiência de início de sessão é diferente consoante aquilo que escolher toouse como o segundo fator: uma chamada telefónica, uma aplicação de autenticação ou textos.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-108">Your sign-in experience differs depending on what you choose toouse as your second factor: a phone call, an authentication app, or texts.</span></span> <span data-ttu-id="7a9ea-109">Escolha a opção de Olá que melhor descreve o que fazer:</span><span class="sxs-lookup"><span data-stu-id="7a9ea-109">Choose hello option that best describes what you are doing:</span></span>

| <span data-ttu-id="7a9ea-110">Como pode iniciar sessão?</span><span class="sxs-lookup"><span data-stu-id="7a9ea-110">How do you sign in?</span></span> | 
| --- |
| [<span data-ttu-id="7a9ea-111">Com um telefone de escritório ou mobile da toomy de chamada telefónica</span><span class="sxs-lookup"><span data-stu-id="7a9ea-111">With a phone call toomy mobile or office phone</span></span>](#signing-in-with-a-phone-call) |
| [<span data-ttu-id="7a9ea-112">Com um telemóvel de toomy de texto</span><span class="sxs-lookup"><span data-stu-id="7a9ea-112">With a text toomy mobile phone</span></span>](#signing-in-with-a-text-message)
| [<span data-ttu-id="7a9ea-113">Notificações da aplicação do Microsoft Authenticator Olá</span><span class="sxs-lookup"><span data-stu-id="7a9ea-113">With notifications from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [<span data-ttu-id="7a9ea-114">Com códigos de verificação da aplicação do Microsoft Authenticator Olá</span><span class="sxs-lookup"><span data-stu-id="7a9ea-114">With verification codes from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [<span data-ttu-id="7a9ea-115">Com um método alternativo, porque o meu método preferido não é possível utilizar neste momento</span><span class="sxs-lookup"><span data-stu-id="7a9ea-115">With an alternate method, because I can't use my preferred method right now</span></span>](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a><span data-ttu-id="7a9ea-116">Iniciar sessão com uma chamada telefónica</span><span class="sxs-lookup"><span data-stu-id="7a9ea-116">Signing in with a phone call</span></span>
<span data-ttu-id="7a9ea-117">Olá informações a seguir descreve a experiência de verificação de dois passos Olá com chamada tooyour móveis ou de telefone do escritório.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-117">hello following information describes hello two-step verification experience with a call tooyour mobile or office phone.</span></span>

1. <span data-ttu-id="7a9ea-118">Inicie sessão no tooan aplicação ou serviço como o Office 365, utilizando o seu nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-118">Sign in tooan application or service such as Office 365 using your username and password.</span></span>  
2. <span data-ttu-id="7a9ea-119">Microsoft chama a.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-119">Microsoft calls you.</span></span>  
3. <span data-ttu-id="7a9ea-120">Responder phone Olá e prima a tecla de # Olá.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-120">Answer hello phone and hit hello # key.</span></span>  

## <a name="signing-in-with-a-text-message"></a><span data-ttu-id="7a9ea-121">Iniciar sessão com uma mensagem de texto</span><span class="sxs-lookup"><span data-stu-id="7a9ea-121">Signing in with a text message</span></span>
<span data-ttu-id="7a9ea-122">Olá informações a seguir descreve a experiência de verificação de dois passos Olá com um texto mensagem tooyour telemóvel:</span><span class="sxs-lookup"><span data-stu-id="7a9ea-122">hello following information describes hello two-step verification experience with a text message tooyour mobile phone:</span></span>

1. <span data-ttu-id="7a9ea-123">Inicie sessão no tooan aplicação ou serviço como o Office 365, utilizando o seu nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-123">Sign in tooan application or service such as Office 365 using your username and password.</span></span> 
2. <span data-ttu-id="7a9ea-124">Microsoft envia uma mensagem de texto que contém um código de número.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-124">Microsoft sends you a text message that contains a number code.</span></span> 
3. <span data-ttu-id="7a9ea-125">Introduza o código de Olá na caixa de Olá fornecida na página de início de sessão Olá.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-125">Enter hello code in hello box provided on hello sign-in page.</span></span> 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="7a9ea-126">Iniciar sessão com a aplicação do Microsoft Authenticator Olá</span><span class="sxs-lookup"><span data-stu-id="7a9ea-126">Signing in with hello Microsoft Authenticator app</span></span> 
<span data-ttu-id="7a9ea-127">Olá seguintes informações descrevem Olá experiência de utilização da aplicação do Microsoft Authenticator Olá para verificações de validação em dois passos.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-127">hello following information describes hello experience of using hello Microsoft Authenticator app for two-step verifications.</span></span> <span data-ttu-id="7a9ea-128">Existem duas formas diferentes o toouse Olá aplicação.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-128">There are two different ways toouse hello app.</span></span> <span data-ttu-id="7a9ea-129">Pode receber notificações push no seu dispositivo ou pode abrir Olá aplicação tooget um código de verificação.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-129">You can receive push notifications on your device, or you can open hello app tooget a verification code.</span></span>

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a><span data-ttu-id="7a9ea-130">toosign com uma notificação da aplicação do Microsoft Authenticator Olá</span><span class="sxs-lookup"><span data-stu-id="7a9ea-130">toosign in with a notification from hello Microsoft Authenticator app</span></span>
1. <span data-ttu-id="7a9ea-131">Inicie sessão no tooan aplicação ou serviço como o Office 365, utilizando o seu nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-131">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="7a9ea-132">Microsoft envia uma aplicação de Microsoft Authenticator toohello notificação no seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-132">Microsoft sends a notification toohello Microsoft Authenticator app on your device.</span></span>

  ![Microsoft envia a notificação](./media/multi-factor-authentication-end-user-signin/notify.png)

3. <span data-ttu-id="7a9ea-134">Notificação de Olá aberto no seu telemóvel e selecione Olá **verifique** chave.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-134">Open hello notification on your phone and select hello **Verify** key.</span></span> <span data-ttu-id="7a9ea-135">Se a sua empresa necessita de um PIN, introduza-o aqui.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-135">If your company requires a PIN, enter it here.</span></span>
4. <span data-ttu-id="7a9ea-136">Agora que deve ser iniciou sessão.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-136">You should now be signed in.</span></span>

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="7a9ea-137">toosign utilizando um código de verificação com a aplicação do Microsoft Authenticator Olá</span><span class="sxs-lookup"><span data-stu-id="7a9ea-137">toosign in using a verification code with hello Microsoft Authenticator app</span></span>

<span data-ttu-id="7a9ea-138">Se utilizar códigos de verificação de tooget de aplicações Microsoft Authenticator Olá, em seguida, quando abre a aplicação Olá verá um número em nome da sua conta.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-138">If you use hello Microsoft Authenticator app tooget verification codes, then when you open hello app you see a number under your account name.</span></span> <span data-ttu-id="7a9ea-139">Este número altera a cada 30 segundos para que não utilize Olá igual número duas vezes.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-139">This number changes every 30 seconds so that you don't use hello same number twice.</span></span> <span data-ttu-id="7a9ea-140">Quando estiver a pedido para um código de verificação, abra a aplicação Olá e utilizar qualquer número atualmente é apresentado.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-140">When you're asked for a verification code, open hello app and use whatever number is currently displayed.</span></span> 

1. <span data-ttu-id="7a9ea-141">Inicie sessão no tooan aplicação ou serviço como o Office 365, utilizando o seu nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-141">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="7a9ea-142">Microsoft pede-lhe um código de verificação.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-142">Microsoft prompts you for a verification code.</span></span>

  ![Introduza o código de verificação](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. <span data-ttu-id="7a9ea-144">Abra a aplicação do Microsoft Authenticator Olá no seu telemóvel e introduza o código de Olá na caixa de olá onde está a iniciar sessão.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-144">Open hello Microsoft Authenticator app on your phone and enter hello code in hello box where you are signing in.</span></span>

## <a name="signing-in-with-an-alternate-method"></a><span data-ttu-id="7a9ea-145">Iniciar sessão com um método alternativo</span><span class="sxs-lookup"><span data-stu-id="7a9ea-145">Signing in with an alternate method</span></span>
<span data-ttu-id="7a9ea-146">Por vezes, não tem o telefone Olá ou dispositivos que configurou como método de verificação preferida.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-146">Sometimes you don't have hello phone or device that you set up as your preferred verification method.</span></span> <span data-ttu-id="7a9ea-147">Esta situação é a razão pela qual recomendamos que configure métodos de cópia de segurança para a sua conta.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-147">This situation is why we recommend that you set up backup methods for your account.</span></span> <span data-ttu-id="7a9ea-148">Olá secção seguinte mostra como toosign com um método alternativo quando o método principal pode não estar disponível.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-148">hello following section shows you how toosign in with an alternate method when your primary method may not be available.</span></span>

1. <span data-ttu-id="7a9ea-149">Inicie sessão no tooan aplicação ou serviço como o Office 365, utilizando o seu nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-149">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="7a9ea-150">Selecione **utilizar outra opção de verificação**.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-150">Select **Use a different verification option**.</span></span> <span data-ttu-id="7a9ea-151">Consulte as opções de verificação diferente com base no número que configurou.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-151">You see different verification options based on how many you have setup.</span></span>
3. <span data-ttu-id="7a9ea-152">Escolha um método alternativo e iniciar sessão.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-152">Choose an alternate method and sign in.</span></span>

  ![Utilize o método alternativo](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a><span data-ttu-id="7a9ea-154">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7a9ea-154">Next steps</span></span>

<span data-ttu-id="7a9ea-155">Se tiver problemas em iniciar sessão com a verificação de dois passos, obter mais informações em [problemas com o Azure multi-factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="7a9ea-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

<span data-ttu-id="7a9ea-156">Saiba como demasiado[gerir as definições da verificação de dois passos](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="7a9ea-156">Learn how too[Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>

<span data-ttu-id="7a9ea-157">Saiba como demasiado[introdução à aplicação do Microsoft Authenticator Olá](microsoft-authenticator-app-how-to.md) para que possa utilizar notificações toosign, em vez de textos e chamadas telefónicas.</span><span class="sxs-lookup"><span data-stu-id="7a9ea-157">Find out how too[Get started with hello Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications toosign in, instead of texts and phone calls.</span></span> 
