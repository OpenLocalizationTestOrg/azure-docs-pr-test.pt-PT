
1. Navegue toohello [Google Cloud Console](https://console.developers.google.com/project), inicie sessão com as credenciais da conta Google. 
2. Clique em **Criar Projeto**, escreva um nome de projeto e, em seguida, clique em **Criar**. Se solicitado, realizar Olá verificação por SMS e clique em **criar** novamente.
   
    ![Criar novo projeto](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     Escreva o novo **Nome do projeto** e clique em **Criar projeto**.
3. Clique em Olá **utilitários e mais** botão e, em seguida, clique em **informações do projeto**. Tome nota do Olá **número do projeto**. Terá de tooset este valor como Olá `SenderId` variável na aplicação de cliente Olá.
   
    ![Utilitários e muito mais](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. Olá projeto em dashboard, **APIs móveis**, clique em **Google Cloud Messaging**, na página seguinte Olá, clique em **ativar API** e aceite os termos de Olá de serviço. 
   
    ![Ativar o GCM](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![Ativar o GCM](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. No dashboard do projeto de Olá, clique em **credenciais** > **criar credencial** > **chave de API**. 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. Em **Criar uma nova chave**, clique em **Chave de servidor**, escreva um nome para a chave e clique em **Criar**.
7. Tome nota do Olá **chave de API** valor.
   
    Irá utilizar este tooenable de valor de chave de API tooauthenticate do Azure com o GCM e enviar notificações push em nome da aplicação.

