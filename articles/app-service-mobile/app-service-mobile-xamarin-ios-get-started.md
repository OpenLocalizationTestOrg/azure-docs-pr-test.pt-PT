---
title: "aaaGet começar a utilizar Mobile Apps do Azure App Service para aplicações xamarin. IOS | Microsoft Docs"
description: "Siga este tutorial tooget começar a utilizar Mobile Apps para o desenvolvimento de xamarin. IOS."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: syntaxc4
ms.openlocfilehash: 524c5ac4d8a29d7cb858f74132aad5d6e2201d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinios-app"></a>Criar uma aplicação Xamarin.iOS
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Descrição geral
Este tutorial mostra como tooadd um back-end baseado na nuvem serviço de aplicações móveis do tooa xamarin. IOS utilizando um back-end de aplicação móvel do Azure.  Pode criar tanto um novo back-end da aplicação móvel assim como uma simples aplicação Xamarin.iOS de uma *Lista de tarefas* que armazena dados da aplicação no Azure.

A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais do xamarin. IOS sobre como utilizar a funcionalidade de aplicações móveis Olá no App Service do Azure.

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, terá de Olá os seguintes pré-requisitos:

* Uma conta ativa do Azure. Se não tiver uma conta, inscreva-se uma versão de avaliação do Azure e obter cópias de segurança too10 mobile apps gratuitas que pode continuar a utilizar mesmo após o final da avaliação. Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* Visual Studio com Xamarin. Para obter instruções, consulte [Configuração e instalação do Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).
* Um Mac com Xcode v7.0 ou posterior e Xamarin Studio Community instalado. Consulte [Configuração e instalação do Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) e [Configuração, instalação e verificações para utilizadores Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).

## <a name="create-an-azure-mobile-app-backend"></a>Criar um back-end da Aplicação Móvel do Azure
Siga estes passos toocreate um back-end de aplicação móvel.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a>Configurar o projeto de servidor Olá
Acabou de aprovisionar um back-end da Aplicação Móvel do Azure que pode ser utilizado pelas suas aplicações cliente móveis. Em seguida, transferir um projeto de servidor para um simples "todo list" back-end e publicá-lo tooAzure.

Siga os seguintes passos tooconfigure Olá servidor projeto toouse de Olá ou Olá Node.js ou .NET back-end.

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a>Transferir e executar a aplicação xamarin. IOS de Olá
1. Abra Olá [portal do Azure] numa janela do browser.
2. No painel de definições de Olá da aplicação móvel, clique em **começar** > **xamarin. IOS**. No passo 3, clique em **Criar uma nova aplicação**, se a opção ainda não estiver selecionada.  Em seguida clique em Olá **transferir** botão.

      Uma aplicação cliente que estabelece ligação back-end móvel tooyour é transferida. Guarde o ficheiro de projeto comprimido Olá para o seu computador local e tome nota do local onde o guardou.
3. Extraia o projeto de Olá que transferiu e, em seguida, abra-o no Xamarin Studio (ou Visual Studio).

    ![][9]

    ![][8]
4. Prima o projeto de Olá Olá F5 toobuild chave e iniciar a aplicação de Olá no emulador do iPhone Olá.
5. Na aplicação Olá, digite um texto significativo, tal como *saiba Xamarin*e, em seguida, clique em Olá  **+**  botão.

    ![][10]

    Dados de pedido de Olá são inseridos na tabela TodoItem de Olá. Os itens armazenados na tabela de Olá são devolvidos pelo back-end de aplicação móvel de Olá, e os dados são apresentados na lista de Olá.

> [!NOTE]
> Pode rever Olá código que acede ao seu tooquery de back-end da aplicação móvel e inserir dados no Olá ficheiro QSTodoService.cs c#.
>
>

## <a name="next-steps"></a>Passos seguintes
* [Adicionar aplicação tooyour de Sincronização Offline](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [Adicionar autenticação tooyour aplicação](app-service-mobile-xamarin-ios-get-started-users.md)
* [Adicionar a aplicação de xamarin. Android de tooyour de notificações push](app-service-mobile-xamarin-ios-get-started-push.md)
* [Como toouse Olá geridos cliente para Mobile Apps do Azure](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
[portal do Azure]: https://portal.azure.com/
