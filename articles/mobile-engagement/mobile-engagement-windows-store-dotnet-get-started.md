---
title: "aaaGet ao Windows Universal aplicações do Azure Mobile Engagement"
description: "Saiba como toouse Azure Mobile Engagement com notificações push e de análise para aplicações universais do Windows."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a>Introdução ao Azure Mobile Engagement para Aplicações Universais do Windows
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tópico mostra como toouse Azure Mobile Engagement toounderstand a utilização da aplicação e enviar push a utilizadores de toosegmented de notificações de uma aplicação Universal do Windows.
Este tutorial demonstra Olá cenário de difusão simples utilizando o Mobile Engagement. Irá criar uma Aplicação Universal do Windows em branco que recolhe dados de utilização de aplicação básicas e recebe notificações push através do Serviço de Notificações do Windows (WNS).

> [!NOTE]
> serviço de Azure Mobile Engagement Olá será descontinuado Março de 2018 e está, atualmente, apenas os clientes de tooexisting disponíveis. Para obter mais informações, veja [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

## <a name="prerequisites"></a>Pré-requisitos
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a>Configurar o Mobile Engagement para a aplicação Universal do Windows
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Ligar o back-end da aplicação toohello Mobile Engagement
Este tutorial apresenta uma "integração básica," que é definida de Olá mínima necessária toocollect dados e enviar uma notificação push. a documentação da integração completa Olá pode ser encontrada na Olá [integração do SDK do Mobile Engagement Windows Universal](mobile-engagement-windows-store-sdk-overview.md).

Criar uma aplicação básica com a integração do Visual Studio toodemonstrate Olá.

### <a name="create-a-windows-universal-app-project"></a>Criar um projeto da Aplicação Universal do Windows
Olá seguintes passos assumem Olá utilização do Visual Studio 2015 apesar dos passos de Olá serem semelhantes em versões anteriores do Visual Studio.

1. Inicie o Visual Studio e em Olá **home page** ecrã, selecione **novo projeto**.
2. No pop-up de Olá, selecione **Windows** -> **Universal** -> **aplicação em branco (Universal Windows)**. Preencha aplicação Olá **nome** e **nome da solução**e, em seguida, clique em **OK**.

    ![][1]

Acabou de criar um projeto de aplicação Universal do Windows no qual, em seguida, integrar Olá Azure Mobile Engagement SDK.

### <a name="connect-your-app-toomobile-engagement-backend"></a>Ligar o back-end da aplicação tooMobile Engagement
1. Instalar Olá [microsoftazure. Mobileengagement] pacote Nuget do seu projeto. Se tiver como objetivo as plataformas Windows e Windows Phone, terá de toodo isto para ambos os projetos. Para o Windows 8. x e Windows Phone 8.1, Olá mesmos Nuget pacote locais Olá corretos binários específicos da plataforma em cada projeto.
2. Abra **Package. appxmanifest** e certifique-se de que Olá seguir capacidade está adicionada aí:

        Internet (Client)

    ![][2]
3. Agora copie a cadeia de ligação de Olá que copiou anteriormente para a sua aplicação de Mobile Engagement e cole-o no Olá `Resources\EngagementConfiguration.xml` ficheiros, entre Olá `<connectionString>` e `</connectionString>` etiquetas:

    ![][3]

    > [!TIP]
    > Se a sua Aplicação visar as plataformas Windows e Windows Phone, deve criar ainda duas Aplicações Mobile Engagement – uma para cada plataforma suportada. Ter duas aplicações assegura que pode criar a segmentação correta do público-alvo de Olá e pode enviar notificações adequadamente segmentadas para cada plataforma.

    > [!IMPORTANT]
    > NuGet automaticamente não copiar recursos do SDK Olá na sua aplicação UWP do Windows 10. Tiver toodo-lo manualmente os seguintes passos de Olá que apareçam (readme.txt) quando o pacote Nuget de Olá está instalado.  

1. No Olá `App.xaml.cs` ficheiro:

    a. Adicionar Olá `using` instrução:

            using Microsoft.Azure.Engagement;

    b. Adicione um método que inicializa Olá o Engagement:

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    c. Inicializar Olá SDK no Olá **OnLaunched** método:

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    c. Insira o seguinte Olá na Olá **OnActivated** método e adicione o método de Olá se não estiver já presente:

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <a id="monitor"></a>Ativar a monitorização em tempo real
toostart envio de dados e garantir que os utilizadores de Olá estão ativos, terá de enviar, pelo menos, um ecrã (atividade) o toohello Mobile Engagement backend.

1. No Olá **MainPage.xaml.cs**, adicione Olá seguinte `using` instrução:

    utilizar o Microsoft.Azure.Engagement.Overlay;
2. Alterar a classe base do Olá de **MainPage** de **página** demasiado**EngagementPageOverlay**:

        class MainPage : EngagementPageOverlay
3. No Olá `MainPage.xaml` ficheiro:

    a. Adicione declarações de espaços de nomes de tooyour:

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    b. Substitua Olá **página** no nome de etiqueta XML Olá com **engagement: EngagementPageOverlay**

> [!IMPORTANT]
> Se a sua página substitui Olá `OnNavigatedTo` método, ser toocall se `base.OnNavigatedTo(e)`. Caso contrário, não foi reportada atividade Olá `EngagementPage` chamadas `StartActivity` dentro respetivo `OnNavigatedTo` método). Isto é especialmente importante num projeto Windows Phone onde Olá predefinido modelo tem um `OnNavigatedTo` método.
>
> Para **aplicações universais do Windows 10**, utilizar o método de Olá recomendado na Olá "recomendado método: Sobrecarga as classes de página" secção [avançadas de relatórios com Olá SDK Windows Universal do aplicações Engagement](mobile-engagement-windows-store-advanced-reporting.md) , em vez de Olá um mencionados acima.

## <a id="monitor"></a>Ligar a aplicação com a monitorização em tempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Ativar as notificações push e mensagens na aplicação
O Mobile Engagement permite-lhe toointeract e alcançar os seus utilizadores com notificações push e mensagens no contexto de Olá das campanhas na aplicação. Este módulo é designado alcance no portal de Mobile Engagement Olá.
Olá secções seguintes configuram a aplicação tooreceive-los.

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a>Ativar a sua aplicação tooreceive notificações Push do WNS
1. No Olá `Package.appxmanifest` ficheiro no Olá **aplicação** separador em **notificações**, defina **com capacidade de alerta:** demasiado**Sim**

    ![][5]

### <a name="initialize-hello-reach-sdk"></a>Inicializar Olá ALCANÇAR SDK
No `App.xaml.cs`, chamar **EngagementReach.Instance.Init(e);** no Olá **InitEngagement** função imediatamente após a inicialização do agente Olá:

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

Está pronto toosend um alerta. A seguir, vamos confirmar que realizou corretamente esta integração básica.

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a>Conceda acesso tooMobile Engagement toosend notificações
1. Abra o [Dev Center da Loja Windows] no seu browser, inicie sessão e crie uma conta, se necessário.
2. Clique em **Dashboard** Olá superior direita canto e, em seguida, clique em **criar uma nova aplicação** no menu de Olá painel esquerdo.

    ![][9]
3. Crie a sua aplicação ao reservar o respetivo nome.

    ![][10]
4. Quando tiver sido criada a aplicação Olá, navegue até demasiado**serviços -> notificações Push** no menu esquerdo Olá.

    ![][11]
5. No Olá de secção notificações Push, clique em Olá **site dos Serviços Live** ligação.

    ![][12]
6. Navegue toohello secção de credenciais de Push. Certifique-se de que está em Olá **as definições de aplicação** secção e, em seguida, copie o **SID do pacote** e **segredo do cliente**

    ![][13]
7. Navegue toohello **definições** do portal do Mobile Engagement e clique em Olá **Push nativo** secção Olá esquerda. Em seguida, clique em Olá **editar** botão tooenter sua **identificador de segurança do pacote (SID)** e os seus **chave secreta** conforme mostrado:

    ![][6]
8. Por fim, certifique-se de que associou a sua aplicação do Visual Studio a esta aplicação criada numa loja de aplicações de Olá. Clique em **Associar a Aplicação à Loja** no Visual Studio.

    ![][7]

## <a id="send"></a>Enviar uma aplicação de tooyour de notificação
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

Se estiver a executar a aplicação de Olá, verá uma notificação na aplicação. caso contrário, se a aplicação Olá estiver fechada, verá uma notificação de alerta.
Se vir uma notificação na aplicação, mas não uma notificação de alerta e Olá aplicação estiver a executar no modo de depuração no Visual Studio, em seguida, tente **eventos de ciclo de vida -> suspender** no Olá barra de ferramentas tooensure essa aplicação Olá é suspenso. Se clicou no botão de Home Olá durante a depuração da aplicação Olá no Visual Studio, em seguida, não fica sempre suspensa e consulte notificação Olá como na aplicação, não aparecer como uma notificação de alerta.  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[microsoftazure. Mobileengagement]: http://go.microsoft.com/?linkid=9864592
[Dev Center da Loja Windows]: https://dev.windows.com
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
