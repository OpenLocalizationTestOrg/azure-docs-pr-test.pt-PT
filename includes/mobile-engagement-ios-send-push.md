### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a>Conceda acesso tooyour certificado Push tooMobile Engagement
tooallow Mobile Engagement toosend notificações Push em seu nome, terá de toogrant aceder a tooyour certificado. Isto é feito ao configurar e introduzir o certificado no portal de Mobile Engagement Olá. Não se esqueça de obter o certificado .p12 conforme explicado na [Documentação da Apple](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6).

1. Navegue tooyour portal de Mobile Engagement. Certifique-se de que está na Olá correto e, em seguida, clique em Olá **iniciar** botão na parte inferior de Olá:
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. Clique em Olá **definições** página no Portal do Engagement. Clique na Olá **Push nativo** secção tooupload o certificado p12:
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. Selecione o p12, carregue-o e escreva a palavra-passe:
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <a id="send"></a>Enviar uma aplicação de tooyour de notificação
Iremos agora criar uma campanha de notificação Push simples que vai enviar uma aplicação de tooour push:

1. Navegue toohello **alcançar** separador no portal do Mobile Engagement.
2. Clique em **novo anúncio** toocreate a campanha push.
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. Configurar os campos de primeiro Olá da sua campanha:
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * Forneça um **Nome** para a campanha. 
   * Selecione Olá **hora de entrega** como **apenas fora da aplicação**: Este é Olá Apple push notification tipo simples que inclui algum texto.
   * Texto da notificação Olá, escreva primeiro Olá **título** que será a primeira linha de Olá no push Olá.
   * Em seguida, escreva o **mensagem** que será a segunda linha de Olá
4. Desloque para baixo e, no Olá secção de conteúdo selecione **apenas notificação**
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. Terminar a campanha mais básica do Olá definição. Agora, desloque para baixo e clique em **criar** botão toosave sua campanha de notificações push. 
6. Por fim, clique em **ativar** toosend notificações de push. 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. Poderá receber a notificação de Olá no seu dispositivo iOS no Centro de notificações de Olá semelhante Olá seguinte:
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. Se tiver um Apple Watch emparelhado com este dispositivo iOS, em seguida, verá Olá notificação no seu Apple Watch:
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

