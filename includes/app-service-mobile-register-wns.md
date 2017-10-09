
1. No Explorador de soluções do Visual Studio, clique no projeto de aplicação da loja Windows hello e clique em **arquivo** > **associar aplicação Olá arquivo**.

    ![Associar aplicação à loja Windows](./media/app-service-mobile-register-wns/notification-hub-associate-win8-app.png)
2. No Assistente de Olá, clique em **seguinte**e inicie sessão com a sua conta Microsoft. Escreva um nome para a sua aplicação no **reservar um novo nome de aplicação**e, em seguida, clique em **reserva**.
3. Depois de registo de aplicação Olá é o nome da aplicação nova criada com êxito, selecione Olá, clique em **seguinte**e, em seguida, clique em **associar**. Esta ação adiciona Olá necessário loja Windows registo informações toohello manifesto da aplicação.
4. Repita os passos 1 e 3 para o projeto de aplicação da loja Windows Phone Olá utilizando Olá registo mesmo que criou anteriormente para a aplicação da loja Windows hello.  
5. Procurar toohello [Windows Dev Center](https://dev.windows.com/en-us/overview)e inicie sessão com a sua conta Microsoft. Clique em registo de nova aplicação Olá no **as minhas aplicações**e, em seguida, expanda **serviços** > **notificações Push**.
6. No Olá **notificações Push** página, clique em **site dos Serviços Live** em **Push notificação serviços Windows (WNS) e as Mobile Apps do Microsoft Azure**. Tome nota dos valores de Olá de Olá **SID do pacote** e Olá *atual* valor **segredo da aplicação**. 

    ![Definição de aplicação no Centro de programadores Olá](./media/app-service-mobile-register-wns/mobile-services-win8-app-push-auth.png)

   > [!IMPORTANT]
   > segredo da aplicação Olá e o SID do pacote são credenciais de segurança importantes. Não partilhe estes valores com ninguém e não os distribua com a aplicação.
   >
   >
