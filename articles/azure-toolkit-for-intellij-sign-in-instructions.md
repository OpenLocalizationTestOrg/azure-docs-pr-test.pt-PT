---
title: "aaaSign em instruções para Olá Toolkit do Azure para o IntelliJ | Microsoft Docs"
description: "Saiba como toosign no tooMicrosoft do Azure utilizando Olá Toolkit do Azure para o IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 2de781fc19267cce133b1e6456481497e165fce4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="65827-103">Início de sessão instruções para Olá Toolkit do Azure para o IntelliJ</span><span class="sxs-lookup"><span data-stu-id="65827-103">Sign-in instructions for hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="65827-104">Olá Toolkit do Azure para o IntelliJ fornece dois métodos para iniciar sessão tooyour conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="65827-104">hello Azure Toolkit for IntelliJ provides two methods for signing in tooyour Azure account:</span></span>

  * <span data-ttu-id="65827-105">**Interativo**: introduza as suas credenciais do Azure cada vez que iniciar sessão no tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="65827-105">**Interactive**: You enter your Azure credentials each time you sign in tooyour Azure account.</span></span>
  * <span data-ttu-id="65827-106">**Automatizada**: criar um ficheiro de credenciais que pode utilizar tooautomatically sessão tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="65827-106">**Automated**: You create a credentials file that you can use tooautomatically sign in tooyour Azure account.</span></span>

<span data-ttu-id="65827-107">Olá secções seguintes descrevem como toouse cada método.</span><span class="sxs-lookup"><span data-stu-id="65827-107">hello following sections describe how toouse each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a><span data-ttu-id="65827-108">Sessão interativamente tooyour conta do Azure</span><span class="sxs-lookup"><span data-stu-id="65827-108">Sign in tooyour Azure account interactively</span></span>

<span data-ttu-id="65827-109">toosign no tooAzure por introduzir manualmente as suas credenciais do Azure, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="65827-109">toosign in tooAzure by manually entering your Azure credentials, do hello following:</span></span>

1. <span data-ttu-id="65827-110">Abra o projeto com o IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="65827-110">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="65827-111">Clique em **ferramentas**, ponto demasiado**Azure**e, em seguida, clique em **Azure sessão**.</span><span class="sxs-lookup"><span data-stu-id="65827-111">Click **Tools**, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Olá comando IntelliJ Azure de sessão][I01]

3. <span data-ttu-id="65827-113">No Olá **Azure sessão** janela, selecione **interativo**e, em seguida, clique em **sessão**.</span><span class="sxs-lookup"><span data-stu-id="65827-113">In hello **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![Olá Azure sessão janela com interativo selecionado][I02]

4. <span data-ttu-id="65827-115">No Olá **Azure início de sessão** aparece a caixa de diálogo, introduza as suas credenciais do Azure e, em seguida, clique em **sessão**.</span><span class="sxs-lookup"><span data-stu-id="65827-115">In hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![janela de caixa de diálogo de início de sessão de Azure Olá][I03]

5. <span data-ttu-id="65827-117">No Olá **selecionar subscrições** caixa de diálogo, subscrições Olá Selecione se pretende toouse e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="65827-117">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![caixa de diálogo Selecionar subscrições Olá][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="65827-119">Terminar a sua conta do Azure depois de iniciar sessão interativamente</span><span class="sxs-lookup"><span data-stu-id="65827-119">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="65827-120">Depois de ter configurado a sua conta utilizando Olá precedente passos, irá ser automaticamente terminou sessão na sua conta do Azure, sempre que reiniciar o IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="65827-120">After you have configured your account by using hello preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="65827-121">No entanto, se quiser toosign fora da sua conta do Azure *sem* reiniciar o IntelliJ IDEA, Olá seguintes.</span><span class="sxs-lookup"><span data-stu-id="65827-121">However, if you want toosign out of your Azure account *without* restarting IntelliJ IDEA, do hello following.</span></span>

1. <span data-ttu-id="65827-122">No IntelliJ IDEA, no Olá **ferramentas** menu, ponto demasiado**Azure**e, em seguida, clique em **Azure terminar sessão**.</span><span class="sxs-lookup"><span data-stu-id="65827-122">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![Olá comando IntelliJ Azure terminar sessão][L01]

2. <span data-ttu-id="65827-124">No Olá **Azure terminar sessão** janela de confirmação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="65827-124">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![janela de Olá Azure terminar sessão confirmação][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a><span data-ttu-id="65827-126">Sessão automaticamente tooyour conta do Azure</span><span class="sxs-lookup"><span data-stu-id="65827-126">Sign in tooyour Azure account automatically</span></span>

<span data-ttu-id="65827-127">Esta secção explica como criar um ficheiro de credenciais que contenha os dados de principal de serviço.</span><span class="sxs-lookup"><span data-stu-id="65827-127">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="65827-128">Depois de concluir este processo, o Eclipse utiliza Olá credenciais ficheiro tooautomatically início de sessão que no tooAzure cada vez que abrir o projeto.</span><span class="sxs-lookup"><span data-stu-id="65827-128">After you have completed this process, Eclipse uses hello credentials file tooautomatically sign you in tooAzure each time you open your project.</span></span>

1. <span data-ttu-id="65827-129">Abra o projeto com o IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="65827-129">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="65827-130">No Olá **ferramentas** menu, ponto demasiado**Azure**e, em seguida, clique em **Azure sessão**.</span><span class="sxs-lookup"><span data-stu-id="65827-130">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Olá comando IntelliJ Azure de sessão][A01]

3. <span data-ttu-id="65827-132">No Olá **Azure sessão** janela, selecione **automatizada**e, em seguida, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="65827-132">In hello **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![Olá Azure sessão janela com automatizada selecionada][A02]

4. <span data-ttu-id="65827-134">No Olá **caixa de diálogo de início de sessão de Azure** janela, introduza as suas credenciais do Azure e, em seguida, clique em **sessão**.</span><span class="sxs-lookup"><span data-stu-id="65827-134">In hello **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![janela de caixa de diálogo de início de sessão de Azure Olá][A03]

5. <span data-ttu-id="65827-136">No Olá **criar ficheiros de autenticação** janela, subscrições Olá selecione que pretende toouse, escolha o seu diretório de destino e, em seguida, clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="65827-136">In hello **Create Authentication Files** window, select hello subscriptions that you want toouse, choose your destination directory, and then click **Start**.</span></span>

   ![janela de criar ficheiros de autenticação de Olá][A04]

6. <span data-ttu-id="65827-138">No Olá **o estado de criação de principais de serviço** caixa de diálogo, depois dos ficheiros foram criados com êxito, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="65827-138">In hello **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![Olá caixa de diálogo de estado de criação de principais de serviço][A05]

7. <span data-ttu-id="65827-140">No Olá **Azure sessão** janela, clique em **sessão**.</span><span class="sxs-lookup"><span data-stu-id="65827-140">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![Caixa de Diálogo Início de Sessão do Azure][A06]

8. <span data-ttu-id="65827-142">No Olá **selecionar subscrições** caixa de diálogo, subscrições Olá Selecione se pretende toouse e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="65827-142">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![caixa de diálogo Selecionar subscrições Olá][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="65827-144">Terminar a sua conta do Azure depois de iniciar sessão automaticamente</span><span class="sxs-lookup"><span data-stu-id="65827-144">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="65827-145">Depois de ter configurado a sua conta utilizando Olá precedente passos, Olá Azure Toolkit inicia a sessão tooyour sempre que reiniciar o IntelliJ IDEA de conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="65827-145">After you have configured your account by using hello preceding steps, hello Azure Toolkit automatically signs you in tooyour Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="65827-146">No entanto, toosign fora da sua conta do Azure e impedir Olá Azure Toolkit de iniciar sessão automaticamente, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="65827-146">However, toosign out of your Azure account and prevent hello Azure Toolkit from signing you in automatically, do hello following:</span></span>

1. <span data-ttu-id="65827-147">No IntelliJ IDEA, no Olá **ferramentas** menu, ponto demasiado**Azure**e, em seguida, clique em **Azure terminar sessão**.</span><span class="sxs-lookup"><span data-stu-id="65827-147">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![Olá comando IntelliJ Azure terminar sessão][L01]

2. <span data-ttu-id="65827-149">No Olá **Azure terminar sessão** janela de confirmação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="65827-149">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![janela de Olá Azure terminar sessão confirmação][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="65827-151">Inicie sessão no tooyour conta do Azure automaticamente utilizando um ficheiro de credenciais existentes</span><span class="sxs-lookup"><span data-stu-id="65827-151">Sign in tooyour Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="65827-152">Se assinar fora da sua conta do Azure quando estiver a utilizar o IntelliJ IDEA, tem de utilizar um início de sessão de tooautomatically de ficheiro de credenciais existentes no toohello conta.</span><span class="sxs-lookup"><span data-stu-id="65827-152">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file tooautomatically sign back in toohello account.</span></span> <span data-ttu-id="65827-153">tooconfigure Olá Toolkit do Azure para o Eclipse toouse um ficheiro de credenciais existentes, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="65827-153">tooconfigure hello Azure Toolkit for Eclipse toouse an existing credentials file, do hello following:</span></span>

1. <span data-ttu-id="65827-154">Abra o projeto com o IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="65827-154">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="65827-155">No Olá **ferramentas** menu, ponto demasiado**Azure**e, em seguida, clique em **Azure sessão**.</span><span class="sxs-lookup"><span data-stu-id="65827-155">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Olá comando IntelliJ Azure de sessão][A01]

3. <span data-ttu-id="65827-157">No Olá **Azure sessão** janela, selecione **automatizada**e, em seguida, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="65827-157">In hello **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![Olá Azure sessão janela com automatizada selecionada][A02]

4. <span data-ttu-id="65827-159">No Olá **selecionar ficheiro de autenticação** caixa de diálogo, selecione um ficheiro de credenciais criada anteriormente e, em seguida, clique em **selecione**.</span><span class="sxs-lookup"><span data-stu-id="65827-159">In hello **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![caixa de diálogo Selecionar ficheiro de autenticação Olá][A08]

5. <span data-ttu-id="65827-161">No Olá **Azure sessão** janela, clique em **sessão**.</span><span class="sxs-lookup"><span data-stu-id="65827-161">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![Olá Azure sessão janela com automatizada selecionada][A06]

6. <span data-ttu-id="65827-163">No Olá **selecionar subscrições** caixa de diálogo, subscrições Olá Selecione se pretende toouse e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="65827-163">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![caixa de diálogo Selecionar subscrições Olá][A07]

## <a name="next-steps"></a><span data-ttu-id="65827-165">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="65827-165">Next steps</span></span>
<span data-ttu-id="65827-166">Para mais informações sobre Olá Toolkits do Azure para Java IDEs, consulte Olá seguintes ligações:</span><span class="sxs-lookup"><span data-stu-id="65827-166">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="65827-167">[Toolkit do Azure do Eclipse]</span><span class="sxs-lookup"><span data-stu-id="65827-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="65827-168">[Novidades no Olá Toolkit de Azure do Eclipse]</span><span class="sxs-lookup"><span data-stu-id="65827-168">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="65827-169">[Instalar Olá Toolkit de Azure do Eclipse]</span><span class="sxs-lookup"><span data-stu-id="65827-169">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="65827-170">[Instruções de início de sessão para Olá Toolkit de Azure do Eclipse]</span><span class="sxs-lookup"><span data-stu-id="65827-170">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="65827-171">[Criar uma aplicação de web de Olá, mundo do Azure no Eclipse]</span><span class="sxs-lookup"><span data-stu-id="65827-171">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="65827-172">[Azure Toolkit para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="65827-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="65827-173">[Novidades no Olá Toolkit do Azure para o IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="65827-173">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="65827-174">[Instalar Olá Toolkit do Azure para o IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="65827-174">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="65827-175">*Início de sessão instruções para Olá Toolkit do Azure para o IntelliJ* (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="65827-175">*Sign-in instructions for hello Azure Toolkit for IntelliJ* (this article)</span></span>
  * <span data-ttu-id="65827-176">[Criar uma aplicação de web de Olá, mundo do Azure no IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="65827-176">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="65827-177">Para obter mais informações sobre como utilizar o Azure com Java, consulte Olá [Centro de programadores Java do Azure] e Olá [ferramentas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="65827-177">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Toolkit do Azure do Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit para IntelliJ]: ./azure-toolkit-for-intellij.md
[Criar uma aplicação de Web Olá mundo do Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Criar uma aplicação de web de Olá, mundo do Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalar Olá Toolkit de Azure do Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalar Olá Toolkit do Azure para o IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instruções de início de sessão para Olá Toolkit de Azure do Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novidades no Olá Toolkit de Azure do Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novidades no Olá Toolkit do Azure para o IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro de programadores Java do Azure]: https://azure.microsoft.com/develop/java/
[ferramentas de Java para Visual Studio Team Services]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
