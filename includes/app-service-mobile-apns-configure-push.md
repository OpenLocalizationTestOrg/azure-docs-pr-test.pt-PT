

1. No Mac, inicie **acesso Keychain**. No Olá deixado barra de navegação, em **categoria**, abra **certificados My**. Localizar o certificado SSL Olá que transferiu na secção anterior Olá e indicar o respetivo conteúdo. Selecione apenas Olá certificado (selecionar chave privada Olá), e [exportá-lo](https://support.apple.com/kb/PH20122?locale=en_US).
2. No Olá [portal do Azure](https://portal.azure.com/), clique em **Procurar tudo** > **serviços aplicacionais**e clique em seu back-end do Mobile Apps. Em **definições**, clique em **Push do serviço de aplicações**e, em seguida, clique em seu nome de hub de notificação. Aceda demasiado**serviços de notificação Push da Apple** > **carregar certificado**. Carregar ficheiro. p12 Olá, selecionar Olá correto **modo** (dependendo se o certificado de cliente SSL, do anteriormente é produção ou sandbox). Guarde as alterações.

O serviço está agora configurado toowork com notificações push no iOS.

[1]: ./media/app-service-mobile-apns-configure-push/mobile-push-notification-hub.png
