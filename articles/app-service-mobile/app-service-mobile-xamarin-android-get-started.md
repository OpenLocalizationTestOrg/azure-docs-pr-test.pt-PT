---
title: "aaaGet iniciado com o Azure Mobile Apps para aplicações xamarin Android"
description: Siga este tutorial tooget iniciado a utilizar Mobile Apps do Azure para desenvolvimento de Xamarin Android
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 81649dd3-544f-40ff-b9b7-60c66d683e60
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 38710660d9328fe3c068efca972f76aa8b6e049b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinandroid-app"></a>Criar uma Aplicação Xamarin.Android
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Descrição geral
Este tutorial mostra como tooadd um back-end baseado na nuvem service aplicação xamarin. Android de tooa. Para obter mais informações, consulte [O que são Mobile Apps](app-service-mobile-value-prop.md).

Abaixo é uma captura de ecrã da aplicação Olá concluída:

![][0]

A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais de Mobile Apps para aplicações Xamarin.Android.

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, terá de Olá os seguintes pré-requisitos:

* Uma conta ativa do Azure. Se não tiver uma conta, inscreva-se uma versão de avaliação do Azure e obter cópias de segurança too10 livre Mobile Apps. Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* Visual Studio com Xamarin. Para obter instruções, consulte [Configuração e instalação do Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).

## <a name="create-an-azure-mobile-app-backend"></a>Criar um back-end da Aplicação Móvel do Azure
Siga estes passos toocreate um back-end de aplicação móvel.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

Acabou de aprovisionar um back-end da Aplicação Móvel do Azure que pode ser utilizado pelas suas aplicações cliente móveis. Em seguida, transferir um projeto de servidor para um simples "todo list" back-end e publicá-lo tooAzure.

## <a name="configure-hello-server-project"></a>Configurar o projeto de servidor Olá
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinandroid-app"></a>Transferir e executar a aplicação xamarin. Android de Olá
1. Em **transferir e executar o projeto xamarin. Android**, clique em Olá **transferir** botão.

      Guarde o computador local de tooyour ficheiro de projeto comprimido Olá e tome nota do local onde o guardou.
2. Olá prima **F5** projeto de Olá toobuild da chave e iniciar a aplicação Olá.
3. Na aplicação Olá, digite um texto significativo, tal como *tutorial Olá concluída* e, em seguida, clique em Olá **adicionar** botão.

    ![][10]

    Dados de pedido de Olá são inseridos na tabela TodoItem de Olá. Os itens armazenados na tabela de Olá são devolvidos pelo back-end de aplicação móvel de Olá e os dados são apresentados na lista de Olá.

   > [!NOTE]
   > Pode rever Olá código que acede ao seu tooquery de back-end da aplicação móvel e inserir dados, que se encontra no Olá ficheiro c# ToDoActivity.cs.
   >
   >

## <a name="next-steps"></a>Passos seguintes
* [Adicionar aplicação tooyour de Sincronização Offline](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [Adicionar autenticação tooyour aplicação](app-service-mobile-xamarin-android-get-started-users.md)
* [Adicionar a aplicação de xamarin. Android de tooyour de notificações push](app-service-mobile-xamarin-android-get-started-push.md)
* [Como toouse Olá geridos cliente para Mobile Apps do Azure](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
