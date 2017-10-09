

## <a name="generate-hello-certificate-signing-request-file"></a>Gerar ficheiro de solicitação de assinatura de certificado Olá
Olá serviço Apple Push Notification (APNS) utiliza certificados tooauthenticate as notificações push. Siga estas instruções toocreate Olá push necessário certificado toosend e receber notificações. Para obter mais informações sobre estes conceitos, consulte oficial Olá [serviço Apple Push Notification](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentação.

Gerar ficheiro de assinatura de solicitação certificado (CSR) Olá, que é utilizado pela Apple toogenerate um certificado push assinado.

1. No Mac, execute Olá ferramenta de acesso de Keychain. Pode ser aberta a partir de Olá **utilitários** pasta ou Olá **outros** pasta no painel de arranque Olá.
2. Clique em **Acesso Keychain**, expanda **Assistente de Certificado** e, em seguida, clique em **Pedir um Certificado a uma Autoridade de Certificação...**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. Selecione o **endereço de correio eletrónico do utilizador** e **nome comum** , certifique-se de que **guardado toodisk** está selecionada e, em seguida, clique em **continuar**. Deixe Olá **endereço de correio eletrónico de AC** campo em branco, porque não é necessária.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. Escreva um nome para o ficheiro de assinatura de solicitação certificado (CSR) Olá no **guardar como**, selecione a localização de Olá **onde**, em seguida, clique em **guardar**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      Isto poupa ficheiro do Olá CSR na localização de Olá selecionada; localização de predefinida Olá é Olá ambiente de trabalho. Lembre-se a localização de Olá escolhida deste ficheiro.

Em seguida, irá registar a aplicação no Apple, ativar as notificações push e carregar este toocreate CSR exportado um certificado push.

## <a name="register-your-app-for-push-notifications"></a>Registar a aplicação para notificações push
toobe toosend capaz de push notificações tooan aplicação iOS, tem de registar a aplicação e Apple também registar-se as notificações push.  

1. Se ainda não registou a aplicação, navegue toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">Portal de aprovisionamento do iOS</a> na Olá Centro de programadores Apple, inicie sessão com o seu ID Apple, clique em **identificadores**, em seguida, clique em **IDs de aplicações** e, finalmente, clique em Olá  **+**  assinar tooregister uma nova aplicação.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. Atualizar Olá seguintes três campos para a nova aplicação e, em seguida, clique em **continuar**:
   
   * **Nome**: escreva um nome descritivo para a sua aplicação Olá **nome** campo no Olá **descrição do ID da aplicação** secção.
   * **Identificador do pacote**: em Olá **ID da aplicação explícito** secção, introduza um **identificador de pacote** no formulário de Olá `<Organization Identifier>.<Product Name>` tal como mencionado na Olá [distribuição de aplicações Guia](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8). Olá *identificador de organização* e *nome de produto* que utilizar têm de corresponder ao identificador de organização Olá e nome de produto que irá utilizar quando criar o projeto XCode. No Olá screeshot abaixo *NotificationHubs* é utilizado como um identificador da organização e *GetStarted* é utilizado como nome de produto Olá. Certificar-se de que corresponde a valores de Olá que irá utilizar no projeto XCode permitirá toouse Olá perfil de publicação correto com o XCode. 
   * **Notificações push**: verificação Olá **notificações Push** opção na Olá **serviços aplicacionais** secção.
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      Esta ação gera o ID da aplicação e pede-lhe que as informações de Olá tooconfirm. Clique em **registar** tooconfirm Olá novo ID de aplicação.
     
      Assim que clicar em **registar**, verá Olá **registo concluído** ecrã, conforme mostrado abaixo. Clique em **Concluído**.
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. No Olá Centro de programadores, em IDs de aplicações, localize o ID da aplicação Olá que acabou de criar e clique na respetiva linha.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      Clicar no ID da aplicação Olá apresentará os detalhes da aplicação Olá. Clique em Olá **editar** botão na parte inferior de Olá.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. Desloque-se toohello inferior do ecrã de Olá e clique em Olá **Criar certificado...**  botão na secção de Olá **certificado de SSL de Push de programação**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      Esta ação apresenta o Assistente de "Adicionar certificado iOS" Olá.
   
   > [!NOTE]
   > Este tutorial utiliza um certificado de programação. Olá mesmo processo é utilizado ao registar um certificado de produção. Basta certificar-se de que utiliza Olá mesmo tipo de certificado ao enviar notificações.
   > 
   > 
3. Clique em **Escolher ficheiro**, procure a localização de toohello onde guardou o ficheiro CSR Olá que criou na primeira tarefa de Olá, em seguida, clique em **gerar**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. Depois do certificado de Olá é criado pelo portal Olá, clique em Olá **transferir** botão e clique em **feito**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      Isto transfere o certificado de Olá e guarda-o tooyour computador na pasta transferências.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > Por predefinição, Olá transferido um certificado de desenvolvimento com o nome de ficheiro **aps_development.cer**.
   > 
   > 
5. Faça duplo clique em: certificado push transferido Olá **aps_development.cer**.
   
      Esta ação instala certificado novo Olá no Olá Keychain, como mostrado abaixo:
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > nome de Olá no seu certificado poderá ser diferente, mas esta terá o prefixo **Apple Development iOS Push Services:**.
   > 
   > 
6. No acesso Keychain, clique com botão direito Olá novo certificado push que criou no Olá **certificados** categoria. Clique em **exportar**, nome de ficheiro Olá, selecione Olá **. p12** formatar e, em seguida, clique em **guardar**.
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    Tome nota do nome de ficheiro Olá e localização do certificado. p12 exportado de Olá. Será utilizado tooenable autenticação com APNS.
   
   > [!NOTE]
   > Este tutorial mostra como criar um ficheiro QuickStart.p12. O nome do ficheiro e a localização poderão ser diferentes.
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a>Criar um perfil de aprovisionamento para a aplicação Olá
1. Novamente no Olá <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">Portal de aprovisionamento do iOS</a>, selecione **perfis de aprovisionamento**, selecione **todos os**e, em seguida, clique em Olá  **+**  botão toocreate um novo perfil. Isto inicia Olá **adicionar perfil de aprovisionamento do iOS** Assistente
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. Selecione **desenvolvimento de aplicações iOS** em **desenvolvimento** como tipo de perfil de aprovisionamento de Olá e clique em **continuar**. 
3. Em seguida, selecione o ID da aplicação Olá que acabou de criar Olá **ID da aplicação** na lista pendente e clique em **continuar**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. No Olá **selecionar certificados** ecrã, selecione o seu certificado de programação habitual utilizado para a assinatura de código e clique em **continuar**. Não se trata de certificado de push Olá que acabou de criar.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. Em seguida, selecione Olá **dispositivos** toouse para testar e clique em **continuar**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. Por fim, escolha um nome para o perfil de Olá no **nome do perfil**, clique em **gerar**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. Quando é criada Olá novo perfil de aprovisionamento clique toodownload-lo e instale-lo no seu computador de desenvolvimento do Xcode. Em seguida, clique em **Guardar**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
