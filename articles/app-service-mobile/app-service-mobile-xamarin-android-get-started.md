---
title: "Introdução às Mobile Apps do Azure para aplicações Xamarin.Android"
description: "Siga este tutorial para começar a utilizar Mobile Apps do Azure para desenvolvimento do Xamarin.Android"
services: app-service\mobile
documentationcenter: xamarin
author: conceptdev
manager: crdun
editor: 
ms.assetid: 81649dd3-544f-40ff-b9b7-60c66d683e60
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: crdun
ms.openlocfilehash: abc4fa4129a596c3f3304dc37af3a9b659f45473
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/04/2018
---
# <a name="create-a-xamarinandroid-app"></a>Criar uma Aplicação Xamarin.Android
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Descrição geral
Este tutorial mostra como adicionar um serviço de back-end baseado na nuvem a uma aplicação Xamarin.Android. Para obter mais informações, consulte [O que são Mobile Apps](app-service-mobile-value-prop.md).

Abaixo é exibida uma captura de ecrã da aplicação concluída:

![][0]

A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais de Mobile Apps para aplicações Xamarin.Android.

## <a name="prerequisites"></a>Pré-requisitos
Para concluir este tutorial, precisa dos seguintes pré-requisitos:

* Uma conta ativa do Azure. Se não tiver uma conta, inscreva-se para uma versão de avaliação do Azure e obtenha até 10 Aplicações Móveis gratuitas. Para obter mais detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* Visual Studio com Xamarin. Para obter instruções, consulte [Configuração e instalação do Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).

## <a name="create-an-azure-mobile-app-backend"></a>Criar um back-end da Aplicação Móvel do Azure
Siga estes passos para criar um back-end da Aplicação Móvel.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

Acabou de aprovisionar um back-end da Aplicação Móvel do Azure que pode ser utilizado pelas suas aplicações cliente móveis. Em seguida, transfira um projeto de servidor para um back-end simples de uma “lista de tarefas” e publique-o no Azure.

## <a name="configure-the-server-project"></a>Configurar o projeto de servidor
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinandroid-app"></a>Transferir e executar a aplicação Xamarin.Android
1. Em **Transferir e executar o projeto Xamarin.Android**, clique no botão **Transferir**.

      Guarde o ficheiro de projeto comprimido no computador local e tome nota do local onde o guardou.
2. Prima a tecla **F5** para compilar o projeto e iniciar a aplicação.
3. Na aplicação, digite um texto significativo, tal como *Concluir o tutorial*, e clique no botão **Adicionar**.

    ![][10]

    Os dados do pedido são inseridos na tabela TodoItem. Os itens armazenados na tabela são devolvidos pelo back-end da aplicação móvel e os dados são apresentados na lista.

   > [!NOTE]
   > Pode rever o código que acede ao seu back-end da aplicação móvel para consultar e inserir dados (presente no ficheiro ToDoActivity.cs c#).
   >
   >

## <a name="next-steps"></a>Passos seguintes
* [Adicionar Sincronização Offline à sua aplicação](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [Adicionar autenticação à aplicação ](app-service-mobile-xamarin-android-get-started-users.md)
* [Adicionar notificações push à aplicação Xamarin.Android](app-service-mobile-xamarin-android-get-started-push.md)
* [Como utilizar o cliente gerido para Mobile Apps do Azure](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
