1. Inicie sessão no Olá [Portal do Azure].
2. Clique em **+NOVO** > **Web + Móvel** > **Aplicação Móvel** e indique um nome para o back-end da Aplicação Móvel.
3. Para Olá **grupo de recursos**, selecione um grupo de recursos existente ou crie um novo (utilizando Olá o mesmo nome que a sua aplicação.) 
   
    Pode selecionar outro plano do Serviço de Aplicações ou criar um novo. Para obter mais informações sobre os planos de serviços aplicacionais e como toocreate um novo plano num preço diferente de camada e na localização pretendida, consulte [descrição geral dos planos do App Service do Azure](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
4. Para Olá **plano do App Service**, plano predefinido de Olá (no Olá [escalão Standard](https://azure.microsoft.com/pricing/details/app-service/)) está selecionado. Também pode selecionar um plano diferente ou [criar um novo](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan). Olá definições do plano de serviço de aplicações determinam Olá [localização, as funcionalidades, custos e recursos de computação](https://azure.microsoft.com/pricing/details/app-service/) associados à aplicação. 
   
    Depois de decidir o plano de Olá, clique em **criar**. Esta ação cria Olá back-end da aplicação móvel. 
5. No Olá **definições** painel Olá nova aplicação móvel back-end, clique em **início rápido** > sua plataforma de aplicação de cliente > **ligar uma base de dados**. 
   
    ![](./media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-data-connection.png)
6. No Olá **adicionar ligação de dados** painel, clique em **base de dados SQL** > **criar uma nova base de dados**, base de dados do tipo Olá **nome**, Escolha um escalão de preço, em seguida, clique em **servidor**.  Pode reutilizar esta nova base de dados. Se já tiver uma base de dados Olá mesma localização, pode escolher **utilizar uma base de dados existente**. utilização de Olá de uma base de dados numa localização diferente não é recomendada devido a custos de toobandwidth e latência superior.
   
    ![](./media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-db.png)
7. No Olá **novo servidor** painel, escreva um nome de servidor exclusivo no Olá **nome do servidor** campo, forneça um início de sessão e palavra-passe, verifique **servidor de tooaccess de serviços do azure permitir**e clique em **OK**. Esta ação cria a nova base de dados Olá.
8. Novamente no Olá **adicionar ligação de dados** painel, clique em **cadeia de ligação**, escreva os valores de início de sessão e palavra-passe Olá para a base de dados e clique em **OK**. Aguarde alguns minutos para Olá toobe de base de dados implementado com êxito antes de continuar.

<!-- URLs. -->
[Portal do Azure]: https://portal.azure.com/
