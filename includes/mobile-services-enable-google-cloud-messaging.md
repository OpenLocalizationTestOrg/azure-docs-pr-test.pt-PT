
1. <span data-ttu-id="d0d77-101">Navegue toohello [Google Cloud Console](https://console.developers.google.com/project), inicie sessão com as credenciais da conta Google.</span><span class="sxs-lookup"><span data-stu-id="d0d77-101">Navigate toohello [Google Cloud Console](https://console.developers.google.com/project), sign in with your Google account credentials.</span></span> 
2. <span data-ttu-id="d0d77-102">Clique em **Criar Projeto**, escreva um nome de projeto e, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d0d77-102">Click **Create Project**, type a project name, then click **Create**.</span></span> <span data-ttu-id="d0d77-103">Se solicitado, realizar Olá verificação por SMS e clique em **criar** novamente.</span><span class="sxs-lookup"><span data-stu-id="d0d77-103">If requested, carry out hello SMS Verification, and click **Create** again.</span></span>
   
    ![Criar novo projeto](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     <span data-ttu-id="d0d77-105">Escreva o novo **Nome do projeto** e clique em **Criar projeto**.</span><span class="sxs-lookup"><span data-stu-id="d0d77-105">Type in your new **Project name** and click **Create project**.</span></span>
3. <span data-ttu-id="d0d77-106">Clique em Olá **utilitários e mais** botão e, em seguida, clique em **informações do projeto**.</span><span class="sxs-lookup"><span data-stu-id="d0d77-106">Click hello **Utilities and More** button and then click **Project Information**.</span></span> <span data-ttu-id="d0d77-107">Tome nota do Olá **número do projeto**.</span><span class="sxs-lookup"><span data-stu-id="d0d77-107">Make a note of hello **Project Number**.</span></span> <span data-ttu-id="d0d77-108">Terá de tooset este valor como Olá `SenderId` variável na aplicação de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="d0d77-108">You will need tooset this value as hello `SenderId` variable in hello client app.</span></span>
   
    ![Utilitários e muito mais](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. <span data-ttu-id="d0d77-110">Olá projeto em dashboard, **APIs móveis**, clique em **Google Cloud Messaging**, na página seguinte Olá, clique em **ativar API** e aceite os termos de Olá de serviço.</span><span class="sxs-lookup"><span data-stu-id="d0d77-110">In hello project dashboard, under **Mobile APIs**, click **Google Cloud Messaging**, then on hello next page click **Enable API** and accept hello terms of service.</span></span> 
   
    ![Ativar o GCM](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![Ativar o GCM](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. <span data-ttu-id="d0d77-113">No dashboard do projeto de Olá, clique em **credenciais** > **criar credencial** > **chave de API**.</span><span class="sxs-lookup"><span data-stu-id="d0d77-113">In hello project dashboard, Click **Credentials** > **Create Credential** > **API Key**.</span></span> 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. <span data-ttu-id="d0d77-114">Em **Criar uma nova chave**, clique em **Chave de servidor**, escreva um nome para a chave e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d0d77-114">In **Create a new key**, click **Server key**, type a name for your key, then click **Create**.</span></span>
7. <span data-ttu-id="d0d77-115">Tome nota do Olá **chave de API** valor.</span><span class="sxs-lookup"><span data-stu-id="d0d77-115">Make a note of hello **API KEY** value.</span></span>
   
    <span data-ttu-id="d0d77-116">Irá utilizar este tooenable de valor de chave de API tooauthenticate do Azure com o GCM e enviar notificações push em nome da aplicação.</span><span class="sxs-lookup"><span data-stu-id="d0d77-116">You will use this API key value tooenable Azure tooauthenticate with GCM and send push notifications on behalf of your app.</span></span>

