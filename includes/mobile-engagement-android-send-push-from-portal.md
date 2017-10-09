### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>Conceda o Mobile Engagement acesso tooyour chave de API do GCM
tooallow Mobile Engagement toosend as notificações push em seu nome, terá de toogrant aceder a tooyour chave de API. Isto é feito ao configurar e introduzir a chave no portal de Mobile Engagement Olá.

1. Do seu Portal clássico do Azure, certifique-se de que está na aplicação de Olá que estamos a utilizar para este projeto e, em seguida, clique em Olá **iniciar** botão na parte inferior de Olá:
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. Em seguida, clique em Olá **definições** -> **Push nativo** secção tooenter a chave do GCM:
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. Clique em Olá **editar** ícone à frente do **chave de API** no Olá **definições de GCM** secção conforme mostrado abaixo:
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. No pop-up de Olá, cole Olá chave do servidor GCM que obteve anteriormente e, em seguida, clique em **Ok**.
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <a id="send"></a>Enviar uma aplicação de tooyour de notificação
Iremos agora criar uma campanha de notificações push simples que envia uma aplicação de tooour de notificação push.

1. Navegue toohello **ALCANÇAR** separador no portal do Mobile Engagement.
2. Clique em **novo anúncio** toocreate sua campanha de notificações push.
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. Configure o primeiro campo de Olá da campanha com Olá os seguintes passos:
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    a. Dê um nome à campanha.
   
    b. Selecione Olá **tipo de entrega** como *notificação do sistema -> simples*: Este é o tipo de notificação push Android simples do Olá que inclui um título e uma pequena linha de texto.
   
    c. Selecione **hora de entrega** como *sempre* tooallow Olá aplicação tooreceive uma notificação se a aplicação Olá é iniciada ou não.
   
    d. No Olá de tipo de texto de notificação de Olá **título** que será em negrito no push Olá.
   
    e. Em seguida, escreva a **Mensagem**
4. Desloque-se para baixo e, na Olá **conteúdo** secção, selecione **apenas notificação**.
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. Terminar possíveis de campanha mais básica Olá definição. Agora, desloque para baixo novamente e clique em Olá **criar** botão toosave sua campanha.
6. Último passo: clique em **ativar** tooactivate as notificações de push de toosend campanha.
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

