---
title: aaaGet iniciado com o Azure Mobile Engagement para xamarin. Android
description: "Saiba como toouse Azure Mobile Engagement com notificações Push para aplicações xamarin. Android e de análise."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 9d584fea8e8153d511258cf9b6f87f31dac6aeca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a>Introdução ao Azure Mobile Engagement para Aplicações Xamarin.Android
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tópico mostra como toouse Azure Mobile Engagement toounderstand a utilização da aplicação e como toosend push a utilizadores de toosegmented de notificações de uma aplicação xamarin. Android.
Este tutorial demonstra Olá cenário de difusão simples utilizando o Mobile Engagement. Aqui, vai criar uma aplicação Xamarin.Android em branco que recolhe dados básicos e recebe notificações push através Google Cloud Messaging (GCM).

> [!NOTE]
> serviço de Azure Mobile Engagement Olá será descontinuado Março de 2018 e está, atualmente, apenas os clientes de tooexisting disponíveis. Para obter mais informações, veja [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Este tutorial requer o seguinte Olá:

* [Xamarin Studio](http://xamarin.com/studio). Também pode utilizar o Visual Studio com Xamarin, mas este tutorial utiliza o Xamarin Studio. Para obter instruções de instalação, consulte [Configuração e Instalação do Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).
* [SDK Xamarin do Mobile Engagement](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> toocomplete neste tutorial, tem de ter uma conta do Azure Active Directory. Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).
> 
> 

## <a id="setup-azme"></a>Configurar o Mobile Engagement para a aplicação Android
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Ligar o back-end da aplicação toohello Mobile Engagement
Este tutorial apresenta uma "integração básica", que é definida de Olá mínima necessária toocollect dados e enviar uma notificação push. 

Iremos criar uma aplicação básica com a integração do Xamarin Studio toodemonstrate Olá.

### <a name="create-a-new-xamarinandroid-project"></a>Criar um novo projeto Xamarin.Android
1. Iniciar **Xamarin Studio** aceda demasiado**ficheiro** -> **novo** -> **solução** 
   
    ![][1]
2. Selecione **aplicação Android** , em seguida, certifique-se de idioma Olá selecionado **c#** e clique em **seguinte**.
   
    ![][2]
3. Preencha Olá **nome da aplicação** e Olá **identificador de organização**. Certifique-se de que toocheckmark **serviços Google Play** e, em seguida, clique em **seguinte**. 
   
    ![][3]
4. Olá atualização **nome do projeto**, **nome da solução** e **localização** se necessário e clique em **criar**.
   
    ![][4]

Xamarin Studio criará a aplicação Olá na qual iremos integrar o Mobile Engagement. 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Ligar o back-end da aplicação tooMobile Engagement
1. Clique com o botão direito do rato em Olá **pacotes** pasta nas janelas solução de Olá e selecione **adicionar pacotes...**
   
    ![][5]
2. Procure Olá **SDK Xamarin do Microsoft Azure Mobile Engagement** e adicioná-la tooyour solução.  
   
    ![][6]
3. Abra **mainactivity. cs** e adicione Olá seguintes instruções de utilização:
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. No Olá `OnCreate` método, adicione Olá seguinte ligação de Olá tooinitialize com back-end do Mobile Engagement. Certifique-se de que tooadd sua **ConnectionString**. 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a>Adicionar permissões e uma declaração de serviço
1. Abra Olá **Manifest.xml** ficheiro na pasta de propriedades de Olá. Selecione o separador origem para que a origem XML Olá diretamente de atualização.
2. Adicione estas permissões toohello Manifest.xml (que pode ser encontrado na Olá **propriedades** pasta) do projeto imediatamente antes ou depois Olá `<application>` etiquetas:
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. Adicione o seguinte Olá entre Olá `<application>` e `</application>` etiquetas de serviço do agente toodeclare Olá:
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. No código de Olá que acabou de colar, substitua `"<Your application name>"` na etiqueta Olá. Isto é apresentado no Olá **definições** menu onde os utilizadores podem ver os serviços em execução no dispositivo Olá. Por exemplo, pode adicionar palavra Olá "Serviço" nessa etiqueta.

### <a name="send-a-screen-toomobile-engagement"></a>Enviar um ecrã tooMobile Engagement
Na ordem toostart envio de dados e garantir Olá utilizadores estão ativos, terá de enviar, pelo menos, um ecrã o toohello Mobile Engagement backend. Para fazê-lo-certifique-se de que Olá `MainActivity` herda `EngagementActivity` em vez de `Activity`.

    public class MainActivity : EngagementActivity

Em alternativa, se não for possível herdar de `EngagementActivity`, deve adicionar os métodos `.StartActivity` e `.EndActivity` em `OnResume` e `OnPause`, respetivamente.  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <a id="monitor"></a>Ligar a aplicação com a monitorização em tempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Ativar as notificações push e mensagens na aplicação
O Mobile Engagement permite-lhe toointeract com e ALCANÇAR os seus utilizadores com notificações push e mensagens no contexto de Olá das campanhas na aplicação. Este módulo é designado alcance no portal de Mobile Engagement Olá.
Olá secções a seguir configura a aplicação tooreceive-los.

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
