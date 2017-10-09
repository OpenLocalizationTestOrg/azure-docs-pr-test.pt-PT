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
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a>Início de sessão instruções para Olá Toolkit do Azure para o IntelliJ

Olá Toolkit do Azure para o IntelliJ fornece dois métodos para iniciar sessão tooyour conta do Azure:

  * **Interativo**: introduza as suas credenciais do Azure cada vez que iniciar sessão no tooyour conta do Azure.
  * **Automatizada**: criar um ficheiro de credenciais que pode utilizar tooautomatically sessão tooyour conta do Azure.

Olá secções seguintes descrevem como toouse cada método.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a>Sessão interativamente tooyour conta do Azure

toosign no tooAzure por introduzir manualmente as suas credenciais do Azure, Olá seguintes:

1. Abra o projeto com o IntelliJ IDEA.

2. Clique em **ferramentas**, ponto demasiado**Azure**e, em seguida, clique em **Azure sessão**.

   ![Olá comando IntelliJ Azure de sessão][I01]

3. No Olá **Azure sessão** janela, selecione **interativo**e, em seguida, clique em **sessão**.

   ![Olá Azure sessão janela com interativo selecionado][I02]

4. No Olá **Azure início de sessão** aparece a caixa de diálogo, introduza as suas credenciais do Azure e, em seguida, clique em **sessão**.

   ![janela de caixa de diálogo de início de sessão de Azure Olá][I03]

5. No Olá **selecionar subscrições** caixa de diálogo, subscrições Olá Selecione se pretende toouse e, em seguida, clique em **OK**.

   ![caixa de diálogo Selecionar subscrições Olá][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a>Terminar a sua conta do Azure depois de iniciar sessão interativamente

Depois de ter configurado a sua conta utilizando Olá precedente passos, irá ser automaticamente terminou sessão na sua conta do Azure, sempre que reiniciar o IntelliJ IDEA. No entanto, se quiser toosign fora da sua conta do Azure *sem* reiniciar o IntelliJ IDEA, Olá seguintes.

1. No IntelliJ IDEA, no Olá **ferramentas** menu, ponto demasiado**Azure**e, em seguida, clique em **Azure terminar sessão**.

   ![Olá comando IntelliJ Azure terminar sessão][L01]

2. No Olá **Azure terminar sessão** janela de confirmação, clique em **Sim**.

   ![janela de Olá Azure terminar sessão confirmação][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a>Sessão automaticamente tooyour conta do Azure

Esta secção explica como criar um ficheiro de credenciais que contenha os dados de principal de serviço. Depois de concluir este processo, o Eclipse utiliza Olá credenciais ficheiro tooautomatically início de sessão que no tooAzure cada vez que abrir o projeto.

1. Abra o projeto com o IntelliJ IDEA.

2. No Olá **ferramentas** menu, ponto demasiado**Azure**e, em seguida, clique em **Azure sessão**.

   ![Olá comando IntelliJ Azure de sessão][A01]

3. No Olá **Azure sessão** janela, selecione **automatizada**e, em seguida, clique em **novo**.

   ![Olá Azure sessão janela com automatizada selecionada][A02]

4. No Olá **caixa de diálogo de início de sessão de Azure** janela, introduza as suas credenciais do Azure e, em seguida, clique em **sessão**.

   ![janela de caixa de diálogo de início de sessão de Azure Olá][A03]

5. No Olá **criar ficheiros de autenticação** janela, subscrições Olá selecione que pretende toouse, escolha o seu diretório de destino e, em seguida, clique em **iniciar**.

   ![janela de criar ficheiros de autenticação de Olá][A04]

6. No Olá **o estado de criação de principais de serviço** caixa de diálogo, depois dos ficheiros foram criados com êxito, clique em **OK**.

   ![Olá caixa de diálogo de estado de criação de principais de serviço][A05]

7. No Olá **Azure sessão** janela, clique em **sessão**.

   ![Caixa de Diálogo Início de Sessão do Azure][A06]

8. No Olá **selecionar subscrições** caixa de diálogo, subscrições Olá Selecione se pretende toouse e, em seguida, clique em **OK**.

   ![caixa de diálogo Selecionar subscrições Olá][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a>Terminar a sua conta do Azure depois de iniciar sessão automaticamente

Depois de ter configurado a sua conta utilizando Olá precedente passos, Olá Azure Toolkit inicia a sessão tooyour sempre que reiniciar o IntelliJ IDEA de conta do Azure. No entanto, toosign fora da sua conta do Azure e impedir Olá Azure Toolkit de iniciar sessão automaticamente, Olá a seguir:

1. No IntelliJ IDEA, no Olá **ferramentas** menu, ponto demasiado**Azure**e, em seguida, clique em **Azure terminar sessão**.

   ![Olá comando IntelliJ Azure terminar sessão][L01]

2. No Olá **Azure terminar sessão** janela de confirmação, clique em **Sim**.

   ![janela de Olá Azure terminar sessão confirmação][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a>Inicie sessão no tooyour conta do Azure automaticamente utilizando um ficheiro de credenciais existentes

Se assinar fora da sua conta do Azure quando estiver a utilizar o IntelliJ IDEA, tem de utilizar um início de sessão de tooautomatically de ficheiro de credenciais existentes no toohello conta. tooconfigure Olá Toolkit do Azure para o Eclipse toouse um ficheiro de credenciais existentes, Olá seguintes:

1. Abra o projeto com o IntelliJ IDEA.

2. No Olá **ferramentas** menu, ponto demasiado**Azure**e, em seguida, clique em **Azure sessão**.

   ![Olá comando IntelliJ Azure de sessão][A01]

3. No Olá **Azure sessão** janela, selecione **automatizada**e, em seguida, clique em **procurar**.

   ![Olá Azure sessão janela com automatizada selecionada][A02]

4. No Olá **selecionar ficheiro de autenticação** caixa de diálogo, selecione um ficheiro de credenciais criada anteriormente e, em seguida, clique em **selecione**.

   ![caixa de diálogo Selecionar ficheiro de autenticação Olá][A08]

5. No Olá **Azure sessão** janela, clique em **sessão**.

   ![Olá Azure sessão janela com automatizada selecionada][A06]

6. No Olá **selecionar subscrições** caixa de diálogo, subscrições Olá Selecione se pretende toouse e, em seguida, clique em **OK**.

   ![caixa de diálogo Selecionar subscrições Olá][A07]

## <a name="next-steps"></a>Passos seguintes
Para mais informações sobre Olá Toolkits do Azure para Java IDEs, consulte Olá seguintes ligações:

* [Toolkit do Azure do Eclipse]
  * [Novidades no Olá Toolkit de Azure do Eclipse]
  * [Instalar Olá Toolkit de Azure do Eclipse]
  * [Instruções de início de sessão para Olá Toolkit de Azure do Eclipse]
  * [Criar uma aplicação de web de Olá, mundo do Azure no Eclipse]
* [Azure Toolkit para IntelliJ]
  * [Novidades no Olá Toolkit do Azure para o IntelliJ]
  * [Instalar Olá Toolkit do Azure para o IntelliJ]
  * *Início de sessão instruções para Olá Toolkit do Azure para o IntelliJ* (Este artigo)
  * [Criar uma aplicação de web de Olá, mundo do Azure no IntelliJ]

Para obter mais informações sobre como utilizar o Azure com Java, consulte Olá [Centro de programadores Java do Azure] e Olá [ferramentas de Java para Visual Studio Team Services].

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
