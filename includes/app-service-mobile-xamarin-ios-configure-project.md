#### <a name="configure-hello-ios-project-in-xamarin-studio"></a>Configurar o projeto do iOS Olá no Xamarin Studio
1. No Xamarin.Studio, abra **Info. plist**e atualização Olá **identificador de pacote** com Olá agrupar ID que criou anteriormente com o ID de aplicação nova.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. Desloque para baixo demasiado**modos em segundo plano**. Selecione Olá **ativar modos de em segundo plano** caixa e Olá **notificações remotas** caixa.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. Faça duplo clique em projeto no Olá solução painel tooopen **opções do projeto**.
4. Em **criar**, escolha **iOS assinatura do pacote**e selecione Olá identidade correspondente e perfil de aprovisionamento acabou de configurar para este projeto.

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   Isto garante que projeto Olá utiliza o novo perfil de Olá para assinatura de código. Para Olá oficial Xamarin aprovisionamento de dispositivos documentação, consulte [aprovisionamento de dispositivos de Xamarin].

#### <a name="configure-hello-ios-project-in-visual-studio"></a>Configurar o projeto do iOS Olá no Visual Studio
1. No Visual Studio, clique no projeto Olá e, em seguida, clique em **propriedades**.
2. Nas páginas de propriedades de Olá, clique em Olá **iOS aplicação** separador e atualização Olá **identificador** com o ID de Olá que criou anteriormente.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. No Olá **iOS assinatura do pacote** separador identidade correspondente Olá selecione e aprovisionamento de conjunto de perfis apenas cópias de segurança para este projeto.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    Isto garante que projeto Olá utiliza o novo perfil de Olá para assinatura de código. Para Olá oficial Xamarin aprovisionamento de dispositivos documentação, consulte [aprovisionamento de dispositivos de Xamarin].
4. Faça duplo clique em ficheiro info. plist tooopen-lo e, em seguida, ativar **RemoteNotifications** em **modos em segundo plano**.

[aprovisionamento de dispositivos de Xamarin]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/
