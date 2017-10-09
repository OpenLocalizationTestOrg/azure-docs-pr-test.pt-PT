

## <a name="generate-hello-certificate-signing-request-file"></a><span data-ttu-id="169b3-101">Gerar ficheiro de solicitação de assinatura de certificado Olá</span><span class="sxs-lookup"><span data-stu-id="169b3-101">Generate hello Certificate Signing Request file</span></span>
<span data-ttu-id="169b3-102">Olá serviço Apple Push Notification (APNS) utiliza certificados tooauthenticate as notificações push.</span><span class="sxs-lookup"><span data-stu-id="169b3-102">hello Apple Push Notification Service (APNS) uses certificates tooauthenticate your push notifications.</span></span> <span data-ttu-id="169b3-103">Siga estas instruções toocreate Olá push necessário certificado toosend e receber notificações.</span><span class="sxs-lookup"><span data-stu-id="169b3-103">Follow these instructions toocreate hello necessary push certificate toosend and receive notifications.</span></span> <span data-ttu-id="169b3-104">Para obter mais informações sobre estes conceitos, consulte oficial Olá [serviço Apple Push Notification](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentação.</span><span class="sxs-lookup"><span data-stu-id="169b3-104">For more information on these concepts see hello official [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentation.</span></span>

<span data-ttu-id="169b3-105">Gerar ficheiro de assinatura de solicitação certificado (CSR) Olá, que é utilizado pela Apple toogenerate um certificado push assinado.</span><span class="sxs-lookup"><span data-stu-id="169b3-105">Generate hello Certificate Signing Request (CSR) file, which is used by Apple toogenerate a signed push certificate.</span></span>

1. <span data-ttu-id="169b3-106">No Mac, execute Olá ferramenta de acesso de Keychain.</span><span class="sxs-lookup"><span data-stu-id="169b3-106">On your Mac, run hello Keychain Access tool.</span></span> <span data-ttu-id="169b3-107">Pode ser aberta a partir de Olá **utilitários** pasta ou Olá **outros** pasta no painel de arranque Olá.</span><span class="sxs-lookup"><span data-stu-id="169b3-107">It can be opened from hello **Utilities** folder or hello **Other** folder on hello launch pad.</span></span>
2. <span data-ttu-id="169b3-108">Clique em **Acesso Keychain**, expanda **Assistente de Certificado** e, em seguida, clique em **Pedir um Certificado a uma Autoridade de Certificação...**</span><span class="sxs-lookup"><span data-stu-id="169b3-108">Click **Keychain Access**, expand **Certificate Assistant**, then click **Request a Certificate from a Certificate Authority...**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. <span data-ttu-id="169b3-109">Selecione o **endereço de correio eletrónico do utilizador** e **nome comum** , certifique-se de que **guardado toodisk** está selecionada e, em seguida, clique em **continuar**.</span><span class="sxs-lookup"><span data-stu-id="169b3-109">Select your **User Email Address** and **Common Name** , make sure that **Saved toodisk** is selected, and then click **Continue**.</span></span> <span data-ttu-id="169b3-110">Deixe Olá **endereço de correio eletrónico de AC** campo em branco, porque não é necessária.</span><span class="sxs-lookup"><span data-stu-id="169b3-110">Leave hello **CA Email Address** field blank as it is not required.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. <span data-ttu-id="169b3-111">Escreva um nome para o ficheiro de assinatura de solicitação certificado (CSR) Olá no **guardar como**, selecione a localização de Olá **onde**, em seguida, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="169b3-111">Type a name for hello Certificate Signing Request (CSR) file in **Save As**, select hello location in **Where**, then click **Save**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      <span data-ttu-id="169b3-112">Isto poupa ficheiro do Olá CSR na localização de Olá selecionada; localização de predefinida Olá é Olá ambiente de trabalho.</span><span class="sxs-lookup"><span data-stu-id="169b3-112">This saves hello CSR file in hello selected location; hello default location is in hello Desktop.</span></span> <span data-ttu-id="169b3-113">Lembre-se a localização de Olá escolhida deste ficheiro.</span><span class="sxs-lookup"><span data-stu-id="169b3-113">Remember hello location chosen for this file.</span></span>

<span data-ttu-id="169b3-114">Em seguida, irá registar a aplicação no Apple, ativar as notificações push e carregar este toocreate CSR exportado um certificado push.</span><span class="sxs-lookup"><span data-stu-id="169b3-114">Next, you will register your app with Apple, enable push notifications, and upload this exported CSR toocreate a push certificate.</span></span>

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="169b3-115">Registar a aplicação para notificações push</span><span class="sxs-lookup"><span data-stu-id="169b3-115">Register your app for push notifications</span></span>
<span data-ttu-id="169b3-116">toobe toosend capaz de push notificações tooan aplicação iOS, tem de registar a aplicação e Apple também registar-se as notificações push.</span><span class="sxs-lookup"><span data-stu-id="169b3-116">toobe able toosend push notifications tooan iOS app, you must register your application with Apple and also register for push notifications.</span></span>  

1. <span data-ttu-id="169b3-117">Se ainda não registou a aplicação, navegue toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">Portal de aprovisionamento do iOS</a> na Olá Centro de programadores Apple, inicie sessão com o seu ID Apple, clique em **identificadores**, em seguida, clique em **IDs de aplicações** e, finalmente, clique em Olá  **+**  assinar tooregister uma nova aplicação.</span><span class="sxs-lookup"><span data-stu-id="169b3-117">If you have not already registered your app, navigate toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a> at hello Apple Developer Center, log on with your Apple ID, click **Identifiers**, then click **App IDs**, and finally click on hello **+** sign tooregister a new app.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. <span data-ttu-id="169b3-118">Atualizar Olá seguintes três campos para a nova aplicação e, em seguida, clique em **continuar**:</span><span class="sxs-lookup"><span data-stu-id="169b3-118">Update hello following three fields for your new app and then click **Continue**:</span></span>
   
   * <span data-ttu-id="169b3-119">**Nome**: escreva um nome descritivo para a sua aplicação Olá **nome** campo no Olá **descrição do ID da aplicação** secção.</span><span class="sxs-lookup"><span data-stu-id="169b3-119">**Name**: Type a descriptive name for your app in hello **Name** field in hello **App ID Description** section.</span></span>
   * <span data-ttu-id="169b3-120">**Identificador do pacote**: em Olá **ID da aplicação explícito** secção, introduza um **identificador de pacote** no formulário de Olá `<Organization Identifier>.<Product Name>` tal como mencionado na Olá [distribuição de aplicações Guia](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span><span class="sxs-lookup"><span data-stu-id="169b3-120">**Bundle Identifier**: Under hello **Explicit App ID** section, enter a **Bundle Identifier** in hello form `<Organization Identifier>.<Product Name>` as mentioned in hello [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span></span> <span data-ttu-id="169b3-121">Olá *identificador de organização* e *nome de produto* que utilizar têm de corresponder ao identificador de organização Olá e nome de produto que irá utilizar quando criar o projeto XCode.</span><span class="sxs-lookup"><span data-stu-id="169b3-121">hello *Organization Identifier* and *Product Name* you use must match hello organization identifier and product name you will use when you create your XCode project.</span></span> <span data-ttu-id="169b3-122">No Olá screeshot abaixo *NotificationHubs* é utilizado como um identificador da organização e *GetStarted* é utilizado como nome de produto Olá.</span><span class="sxs-lookup"><span data-stu-id="169b3-122">In hello screeshot below *NotificationHubs* is used as a organization idenitifier and *GetStarted* is used as hello product name.</span></span> <span data-ttu-id="169b3-123">Certificar-se de que corresponde a valores de Olá que irá utilizar no projeto XCode permitirá toouse Olá perfil de publicação correto com o XCode.</span><span class="sxs-lookup"><span data-stu-id="169b3-123">Making sure this matches hello values you will use in your XCode project will allow you toouse hello correct publishing profile with XCode.</span></span> 
   * <span data-ttu-id="169b3-124">**Notificações push**: verificação Olá **notificações Push** opção na Olá **serviços aplicacionais** secção.</span><span class="sxs-lookup"><span data-stu-id="169b3-124">**Push Notifications**: Check hello **Push Notifications** option in hello **App Services** section, .</span></span>
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      <span data-ttu-id="169b3-125">Esta ação gera o ID da aplicação e pede-lhe que as informações de Olá tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="169b3-125">This generates your App ID and requests you tooconfirm hello information.</span></span> <span data-ttu-id="169b3-126">Clique em **registar** tooconfirm Olá novo ID de aplicação.</span><span class="sxs-lookup"><span data-stu-id="169b3-126">Click **Register** tooconfirm hello new App ID.</span></span>
     
      <span data-ttu-id="169b3-127">Assim que clicar em **registar**, verá Olá **registo concluído** ecrã, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="169b3-127">Once you click **Register**, you will see hello **Registration complete** screen, as shown below.</span></span> <span data-ttu-id="169b3-128">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="169b3-128">Click **Done**.</span></span>
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. <span data-ttu-id="169b3-129">No Olá Centro de programadores, em IDs de aplicações, localize o ID da aplicação Olá que acabou de criar e clique na respetiva linha.</span><span class="sxs-lookup"><span data-stu-id="169b3-129">In hello Developer Center, under App IDs, locate hello app ID that you just created, and click on its row.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      <span data-ttu-id="169b3-130">Clicar no ID da aplicação Olá apresentará os detalhes da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="169b3-130">Clicking on hello app ID will display hello app details.</span></span> <span data-ttu-id="169b3-131">Clique em Olá **editar** botão na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="169b3-131">Click hello **Edit** button at hello bottom.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. <span data-ttu-id="169b3-132">Desloque-se toohello inferior do ecrã de Olá e clique em Olá **Criar certificado...**  botão na secção de Olá **certificado de SSL de Push de programação**.</span><span class="sxs-lookup"><span data-stu-id="169b3-132">Scroll toohello bottom of hello screen, and click hello **Create Certificate...** button under hello section **Development Push SSL Certificate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      <span data-ttu-id="169b3-133">Esta ação apresenta o Assistente de "Adicionar certificado iOS" Olá.</span><span class="sxs-lookup"><span data-stu-id="169b3-133">This displays hello "Add iOS Certificate" assistant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="169b3-134">Este tutorial utiliza um certificado de programação.</span><span class="sxs-lookup"><span data-stu-id="169b3-134">This tutorial uses a development certificate.</span></span> <span data-ttu-id="169b3-135">Olá mesmo processo é utilizado ao registar um certificado de produção.</span><span class="sxs-lookup"><span data-stu-id="169b3-135">hello same process is used when registering a production certificate.</span></span> <span data-ttu-id="169b3-136">Basta certificar-se de que utiliza Olá mesmo tipo de certificado ao enviar notificações.</span><span class="sxs-lookup"><span data-stu-id="169b3-136">Just make sure that you use hello same certificate type when sending notifications.</span></span>
   > 
   > 
3. <span data-ttu-id="169b3-137">Clique em **Escolher ficheiro**, procure a localização de toohello onde guardou o ficheiro CSR Olá que criou na primeira tarefa de Olá, em seguida, clique em **gerar**.</span><span class="sxs-lookup"><span data-stu-id="169b3-137">Click **Choose File**, browse toohello location where you saved hello CSR file that you created in hello first task, then click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. <span data-ttu-id="169b3-138">Depois do certificado de Olá é criado pelo portal Olá, clique em Olá **transferir** botão e clique em **feito**.</span><span class="sxs-lookup"><span data-stu-id="169b3-138">After hello certificate is created by hello portal, click hello **Download** button, and click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      <span data-ttu-id="169b3-139">Isto transfere o certificado de Olá e guarda-o tooyour computador na pasta transferências.</span><span class="sxs-lookup"><span data-stu-id="169b3-139">This downloads hello certificate and saves it tooyour computer in your Downloads folder.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > <span data-ttu-id="169b3-140">Por predefinição, Olá transferido um certificado de desenvolvimento com o nome de ficheiro **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="169b3-140">By default, hello downloaded file a development certificate is named **aps_development.cer**.</span></span>
   > 
   > 
5. <span data-ttu-id="169b3-141">Faça duplo clique em: certificado push transferido Olá **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="169b3-141">Double-click hello downloaded push certificate **aps_development.cer**.</span></span>
   
      <span data-ttu-id="169b3-142">Esta ação instala certificado novo Olá no Olá Keychain, como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="169b3-142">This installs hello new certificate in hello Keychain, as shown below:</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > <span data-ttu-id="169b3-143">nome de Olá no seu certificado poderá ser diferente, mas esta terá o prefixo **Apple Development iOS Push Services:**.</span><span class="sxs-lookup"><span data-stu-id="169b3-143">hello name in your certificate might be different, but it will be prefixed with **Apple Development iOS Push Services:**.</span></span>
   > 
   > 
6. <span data-ttu-id="169b3-144">No acesso Keychain, clique com botão direito Olá novo certificado push que criou no Olá **certificados** categoria.</span><span class="sxs-lookup"><span data-stu-id="169b3-144">In Keychain Access, right-click hello new push certificate that you created in hello **Certificates** category.</span></span> <span data-ttu-id="169b3-145">Clique em **exportar**, nome de ficheiro Olá, selecione Olá **. p12** formatar e, em seguida, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="169b3-145">Click **Export**, name hello file, select hello **.p12** format, and then click **Save**.</span></span>
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    <span data-ttu-id="169b3-146">Tome nota do nome de ficheiro Olá e localização do certificado. p12 exportado de Olá.</span><span class="sxs-lookup"><span data-stu-id="169b3-146">Make a note of hello file name and location of hello exported .p12 certificate.</span></span> <span data-ttu-id="169b3-147">Será utilizado tooenable autenticação com APNS.</span><span class="sxs-lookup"><span data-stu-id="169b3-147">It will be used tooenable authentication with APNS.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="169b3-148">Este tutorial mostra como criar um ficheiro QuickStart.p12.</span><span class="sxs-lookup"><span data-stu-id="169b3-148">This tutorial creates a QuickStart.p12 file.</span></span> <span data-ttu-id="169b3-149">O nome do ficheiro e a localização poderão ser diferentes.</span><span class="sxs-lookup"><span data-stu-id="169b3-149">Your file name and location might be different.</span></span>
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a><span data-ttu-id="169b3-150">Criar um perfil de aprovisionamento para a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="169b3-150">Create a provisioning profile for hello app</span></span>
1. <span data-ttu-id="169b3-151">Novamente no Olá <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">Portal de aprovisionamento do iOS</a>, selecione **perfis de aprovisionamento**, selecione **todos os**e, em seguida, clique em Olá  **+**  botão toocreate um novo perfil.</span><span class="sxs-lookup"><span data-stu-id="169b3-151">Back in hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, select **Provisioning Profiles**, select **All**, and then click hello **+** button toocreate a new profile.</span></span> <span data-ttu-id="169b3-152">Isto inicia Olá **adicionar perfil de aprovisionamento do iOS** Assistente</span><span class="sxs-lookup"><span data-stu-id="169b3-152">This launches hello **Add iOS Provisiong Profile** Wizard</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. <span data-ttu-id="169b3-153">Selecione **desenvolvimento de aplicações iOS** em **desenvolvimento** como tipo de perfil de aprovisionamento de Olá e clique em **continuar**.</span><span class="sxs-lookup"><span data-stu-id="169b3-153">Select **iOS App Development** under **Development** as hello provisiong profile type, and click **Continue**.</span></span> 
3. <span data-ttu-id="169b3-154">Em seguida, selecione o ID da aplicação Olá que acabou de criar Olá **ID da aplicação** na lista pendente e clique em **continuar**</span><span class="sxs-lookup"><span data-stu-id="169b3-154">Next, select hello app ID you just created from hello **App ID** drop-down list, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. <span data-ttu-id="169b3-155">No Olá **selecionar certificados** ecrã, selecione o seu certificado de programação habitual utilizado para a assinatura de código e clique em **continuar**.</span><span class="sxs-lookup"><span data-stu-id="169b3-155">In hello **Select certificates** screen, select your usual development certificate used for code signing, and click **Continue**.</span></span> <span data-ttu-id="169b3-156">Não se trata de certificado de push Olá que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="169b3-156">This is not hello push certificate you just created.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. <span data-ttu-id="169b3-157">Em seguida, selecione Olá **dispositivos** toouse para testar e clique em **continuar**</span><span class="sxs-lookup"><span data-stu-id="169b3-157">Next, select hello **Devices** toouse for testing, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. <span data-ttu-id="169b3-158">Por fim, escolha um nome para o perfil de Olá no **nome do perfil**, clique em **gerar**.</span><span class="sxs-lookup"><span data-stu-id="169b3-158">Finally, pick a name for hello profile in **Profile Name**, click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. <span data-ttu-id="169b3-159">Quando é criada Olá novo perfil de aprovisionamento clique toodownload-lo e instale-lo no seu computador de desenvolvimento do Xcode.</span><span class="sxs-lookup"><span data-stu-id="169b3-159">When hello new provisioning profile is created click toodownload it and install it on your Xcode development machine.</span></span> <span data-ttu-id="169b3-160">Em seguida, clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="169b3-160">Then click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
