
1. Clique em Olá **serviços aplicacionais** botão, selecione o seu back-end do Mobile Apps, selecione **início rápido**e, em seguida, selecione a plataforma de cliente (em iOS, Android, Xamarin, Cordova).

    ![Portal do Azure com Início Rápido de Aplicações Móveis realçado][quickstart]

2. Se não estiver configurada uma ligação de base de dados, crie um, Olá seguinte:

    ![Portal do Azure com as aplicações de Mobile Connect toodatabase][connect]

    a. Crie uma base de dados SQL e o servidor novos.

    ![Portal do Azure com Aplicações Móveis criar base de dados e servidor novos][server]

    b. Aguarde até que a ligação de dados de Olá é criada com êxito.

    ![Notificação do portal do Azure de criação com êxito de ligação de dados][notification]

    c. A ligação de dados tem de ser bem-sucedida.

    ![Notificação do portal do Azure, "Já tem uma ligação de dados"][already-connection]

3. Em **2. Criar uma API de tabela**, selecione Node.js em **Linguagem do back-end**. 
 
4. Aceite a confirmação de Olá e, em seguida, selecione **criar tabela TodoItem**.  
    Esta ação cria uma nova tabela de itens pendentes na base de dados. 

    >[!IMPORTANT]
    > Mudar um tooNode.js de back-end existente substitui todos os conteúdos. toocreate um back-end de .NET em vez disso, consulte [funcione com o servidor de back-end de .NET de Olá SDK para Mobile Apps][instructions].

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
