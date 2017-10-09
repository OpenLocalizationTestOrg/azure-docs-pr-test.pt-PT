## <a name="create-hello-webapi-project"></a><span data-ttu-id="1a733-101">Criar Olá end WebAPI projeto</span><span class="sxs-lookup"><span data-stu-id="1a733-101">Create hello WebAPI Project</span></span>
<span data-ttu-id="1a733-102">Será criado um novo back-end de ASP.NET WebAPI end nas secções Olá que se seguem e terá três objetivos principais:</span><span class="sxs-lookup"><span data-stu-id="1a733-102">A new ASP.NET WebAPI backend will be created in hello sections that follow and it will have three main purposes:</span></span>

1. <span data-ttu-id="1a733-103">**Os clientes em autenticação**: o processador de mensagens será adicionado pedidos de cliente tooauthenticate posteriores e o utilizador de Olá associar com pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="1a733-103">**Authenticating Clients**: A message handler will be added later tooauthenticate client requests and associate hello user with hello request.</span></span>
2. <span data-ttu-id="1a733-104">**Registos de notificação de cliente**: mais tarde, irá adicionar um controlador toohandle novos registos para um notificações de tooreceive de dispositivo do cliente.</span><span class="sxs-lookup"><span data-stu-id="1a733-104">**Client Notification Registrations**: Later, you will add a controller toohandle new registrations for a client device tooreceive notifications.</span></span> <span data-ttu-id="1a733-105">Olá nome de utilizador autenticado será automaticamente adicionada toohello registo como um [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span><span class="sxs-lookup"><span data-stu-id="1a733-105">hello authenticated user name will automatically be added toohello registration as a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span></span>
3. <span data-ttu-id="1a733-106">**Enviar notificações tooClients**: posterior, também irá adicionar um controlador tooprovide uma forma de um utilizador de tootrigger toodevices um push segura e clientes associados a tag de Olá.</span><span class="sxs-lookup"><span data-stu-id="1a733-106">**Sending Notifications tooClients**: Later, you will also add a controller tooprovide a way for a user tootrigger a secure push toodevices and clients associated with hello tag.</span></span> 

<span data-ttu-id="1a733-107">Olá, os passos seguintes mostra como toocreate Olá novo back-end de ASP.NET WebAPI end:</span><span class="sxs-lookup"><span data-stu-id="1a733-107">hello following steps show how toocreate hello new ASP.NET WebAPI backend:</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="1a733-108">Se estiver a utilizar o Visual Studio 2015 ou anterior, antes de começar este tutorial, certifique-se que instalou a versão mais recente do Olá do Olá Gestor de pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="1a733-108">If you are using Visual Studio 2015 or earlier, before starting this tutorial, please ensure that you have installed hello latest version of hello NuGet Package Manager.</span></span> <span data-ttu-id="1a733-109">toocheck, início Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1a733-109">toocheck, start Visual Studio.</span></span> <span data-ttu-id="1a733-110">De Olá **ferramentas** menu, clique em **extensões e atualizações**.</span><span class="sxs-lookup"><span data-stu-id="1a733-110">From hello **Tools** menu, click **Extensions and Updates**.</span></span> <span data-ttu-id="1a733-111">Procurar **Gestor de pacotes NuGet** para a sua versão do Visual Studio e certifique-se de que tem a versão mais recente Olá.</span><span class="sxs-lookup"><span data-stu-id="1a733-111">Search for **NuGet Package Manager** for your version of Visual Studio, and make sure you have hello latest version.</span></span> <span data-ttu-id="1a733-112">Se não estiver, desinstale e reinstale Olá Gestor de pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="1a733-112">If not, please uninstall, then reinstall hello NuGet Package Manager.</span></span>
> 
> ![][B4]
> 
> [!NOTE]
> <span data-ttu-id="1a733-113">Certifique-se de que instalou o Visual Studio do Olá [Azure SDK](https://azure.microsoft.com/downloads/) para a implementação de Web site.</span><span class="sxs-lookup"><span data-stu-id="1a733-113">Make sure you have installed hello Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) for website deployment.</span></span>
> 
> 

1. <span data-ttu-id="1a733-114">Inicie o Visual Studio ou o Visual Studio Express.</span><span class="sxs-lookup"><span data-stu-id="1a733-114">Start Visual Studio or Visual Studio Express.</span></span> <span data-ttu-id="1a733-115">Clique em **Explorador de servidores** e iniciar sessão tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a733-115">Click **Server Explorer** and sign in tooyour Azure account.</span></span> <span data-ttu-id="1a733-116">Visual Studio terá de sessão em recursos de web site Olá toocreate na sua conta.</span><span class="sxs-lookup"><span data-stu-id="1a733-116">Visual Studio will need you signed in toocreate hello web site resources on your account.</span></span>
2. <span data-ttu-id="1a733-117">No Visual Studio, clique em **ficheiro**, em seguida, clique em **novo**, em seguida, **projeto**, expanda **modelos**, **Visual c#**, em seguida, clique em **Web** e **aplicação Web ASP.NET**, nome do tipo Olá **AppBackend**e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="1a733-117">In Visual Studio, click **File**, then click **New**, then **Project**, expand **Templates**, **Visual C#**, then click **Web** and **ASP.NET Web Application**, type hello name **AppBackend**, and then click **OK**.</span></span> 
   
    ![][B1]
3. <span data-ttu-id="1a733-118">No Olá **novo projeto ASP.NET** caixa de diálogo, clique em **Web API**, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="1a733-118">In hello **New ASP.NET Project** dialog, click **Web API**, then click **OK**.</span></span>
   
    ![][B2]
4. <span data-ttu-id="1a733-119">No Olá **configurar aplicação da Web do Microsoft Azure** caixa de diálogo, escolha uma subscrição e um **plano do App Service** que já criou.</span><span class="sxs-lookup"><span data-stu-id="1a733-119">In hello **Configure Microsoft Azure Web App** dialog, choose a subscription, and an **App Service plan** you have already created.</span></span> <span data-ttu-id="1a733-120">Também pode optar por **criar um novo plano do app service** e criar uma caixa de diálogo de Olá.</span><span class="sxs-lookup"><span data-stu-id="1a733-120">You can also choose **Create a new app service plan** and create one from hello dialog.</span></span> <span data-ttu-id="1a733-121">Não precisa de uma base de dados para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="1a733-121">You do not need a database for this tutorial.</span></span> <span data-ttu-id="1a733-122">Assim que tiver selecionado o plano do app service, clique em **OK** projeto de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="1a733-122">Once you have selected your app service plan, click **OK** toocreate hello project.</span></span>
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a><span data-ttu-id="1a733-123">Autenticação de clientes toohello back-end WebAPI</span><span class="sxs-lookup"><span data-stu-id="1a733-123">Authenticating Clients toohello WebAPI Backend</span></span>
<span data-ttu-id="1a733-124">Nesta secção, irá criar uma nova classe de processador de mensagens com o nome **AuthenticationTestHandler** para Olá novo back-end.</span><span class="sxs-lookup"><span data-stu-id="1a733-124">In this section, you will create a new message handler class named **AuthenticationTestHandler** for hello new backend.</span></span> <span data-ttu-id="1a733-125">Esta classe é derivada de [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) e adicionado como um processador de mensagens, pelo que pode processar todos os pedidos entra de back-end de Olá.</span><span class="sxs-lookup"><span data-stu-id="1a733-125">This class is derived from [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) and added as a message handler so it can process all requests coming into hello backend.</span></span> 

1. <span data-ttu-id="1a733-126">No Explorador de soluções, faça duplo clique Olá **AppBackend** do projeto, clique em **adicionar**, em seguida, clique em **classe**.</span><span class="sxs-lookup"><span data-stu-id="1a733-126">In Solution Explorer, right-click hello **AppBackend** project, click **Add**, then click **Class**.</span></span> <span data-ttu-id="1a733-127">Nome da nova classe de Olá **AuthenticationTestHandler.cs**e clique em **adicionar** classe de Olá toogenerate.</span><span class="sxs-lookup"><span data-stu-id="1a733-127">Name hello new class **AuthenticationTestHandler.cs**, and click **Add** toogenerate hello class.</span></span> <span data-ttu-id="1a733-128">Esta classe será utilizado tooauthenticate utilizadores utilizando o *autenticação básica* de simplicidade.</span><span class="sxs-lookup"><span data-stu-id="1a733-128">This class will be used tooauthenticate users using *Basic Authentication* for simplicity.</span></span> <span data-ttu-id="1a733-129">Tenha em atenção que a sua aplicação pode utilizar qualquer esquema de autenticação.</span><span class="sxs-lookup"><span data-stu-id="1a733-129">Note that your app can use any authentication scheme.</span></span>
2. <span data-ttu-id="1a733-130">No AuthenticationTestHandler.cs, adicione o seguinte de Olá `using` instruções:</span><span class="sxs-lookup"><span data-stu-id="1a733-130">In AuthenticationTestHandler.cs, add hello following `using` statements:</span></span>
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. <span data-ttu-id="1a733-131">No AuthenticationTestHandler.cs, substituindo Olá `AuthenticationTestHandler` definição de classe com Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="1a733-131">In AuthenticationTestHandler.cs, replacing hello `AuthenticationTestHandler` class definition with hello following code.</span></span> 
   
    <span data-ttu-id="1a733-132">Este processador autorizará pedido Olá quando Olá seguintes três condições se verificarem todas as:</span><span class="sxs-lookup"><span data-stu-id="1a733-132">This handler will authorize hello request when hello following three conditions are all true:</span></span>
   
   * <span data-ttu-id="1a733-133">pedido de Olá incluído um *autorização* cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="1a733-133">hello request included an *Authorization* header.</span></span> 
   * <span data-ttu-id="1a733-134">pedido de Olá utiliza *básico* autenticação.</span><span class="sxs-lookup"><span data-stu-id="1a733-134">hello request uses *basic* authentication.</span></span> 
   * <span data-ttu-id="1a733-135">cadeia de nome de utilizador Olá e a cadeia de palavra-passe de Olá são Olá mesma cadeia.</span><span class="sxs-lookup"><span data-stu-id="1a733-135">hello user name string and hello password string are hello same string.</span></span>
     
     <span data-ttu-id="1a733-136">Caso contrário, o pedido de Olá será rejeitado.</span><span class="sxs-lookup"><span data-stu-id="1a733-136">Otherwise, hello request will be rejected.</span></span> <span data-ttu-id="1a733-137">Esta não é uma verdadeira abordagem de autenticação e autorização.</span><span class="sxs-lookup"><span data-stu-id="1a733-137">This is not a true authentication and authorization approach.</span></span> <span data-ttu-id="1a733-138">É apenas um exemplo muito simples para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="1a733-138">It is just a very simple example for this tutorial.</span></span>
     
     <span data-ttu-id="1a733-139">Se a mensagem de pedido de saudação é autenticada e autorizada por Olá `AuthenticationTestHandler`, utilizador de autenticação básica Olá será anexado toohello pedido atual no Olá [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span><span class="sxs-lookup"><span data-stu-id="1a733-139">If hello request message is authenticated and authorized by hello `AuthenticationTestHandler`, then hello basic authentication user will be attached toohello current request on hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span></span> <span data-ttu-id="1a733-140">Informações do utilizador no Olá HttpContext serão utilizadas por outro controlador (RegisterController) tooadd posterior um [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello pedido de registo de notificação.</span><span class="sxs-lookup"><span data-stu-id="1a733-140">User information in hello HttpContext will be used by another controller (RegisterController) later tooadd a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello notification registration request.</span></span>
     
       <span data-ttu-id="1a733-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span><span class="sxs-lookup"><span data-stu-id="1a733-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span></span>
     
               if (authorizationHeader != null && authorizationHeader
                   .StartsWith("Basic ", StringComparison.InvariantCultureIgnoreCase))
               {
                   string authorizationUserAndPwdBase64 =
                       authorizationHeader.Substring("Basic ".Length);
                   string authorizationUserAndPwd = Encoding.Default
                       .GetString(Convert.FromBase64String(authorizationUserAndPwdBase64));
                   string user = authorizationUserAndPwd.Split(':')[0];
                   string password = authorizationUserAndPwd.Split(':')[1];
     
                   if (verifyUserAndPwd(user, password))
                   {
                       // Attach hello new principal object toohello current HttpContext object
                       HttpContext.Current.User =
                           new GenericPrincipal(new GenericIdentity(user), new string[0]);
                       System.Threading.Thread.CurrentPrincipal =
                           System.Web.HttpContext.Current.User;
                   }
                   else return Unauthorized();
               }
               else return Unauthorized();
     
               return base.SendAsync(request, cancellationToken);
           }
     
           private bool verifyUserAndPwd(string user, string password)
           {
               // This is not a real authentication scheme.
               return user == password;
           }
     
           private Task<HttpResponseMessage> Unauthorized()
           {
               var response = new HttpResponseMessage(HttpStatusCode.Forbidden);
               var tsc = new TaskCompletionSource<HttpResponseMessage>();
               tsc.SetResult(response);
               return tsc.Task;
           }
       <span data-ttu-id="1a733-142">}</span><span class="sxs-lookup"><span data-stu-id="1a733-142">}</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="1a733-143">**Nota de segurança**: Olá `AuthenticationTestHandler` classe não fornecer autenticação verdadeira.</span><span class="sxs-lookup"><span data-stu-id="1a733-143">**Security Note**: hello `AuthenticationTestHandler` class does not provide true authentication.</span></span> <span data-ttu-id="1a733-144">É utilizado toomimic apenas a autenticação básica e não é segura.</span><span class="sxs-lookup"><span data-stu-id="1a733-144">It is used only toomimic basic authentication and is not secure.</span></span> <span data-ttu-id="1a733-145">Tem de implementar um mecanismo de autenticação segura nos seus serviços e aplicações de produção.</span><span class="sxs-lookup"><span data-stu-id="1a733-145">You must implement a secure authentication mechanism in your production applications and services.</span></span>                
     > 
     > 
4. <span data-ttu-id="1a733-146">Adicionar Olá seguinte código no final Olá Olá `Register` método Olá **App_Start/WebApiConfig.cs** o processador de mensagens de Olá classe tooregister:</span><span class="sxs-lookup"><span data-stu-id="1a733-146">Add hello following code at hello end of hello `Register` method in hello **App_Start/WebApiConfig.cs** class tooregister hello message handler:</span></span>
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. <span data-ttu-id="1a733-147">Guarde as alterações.</span><span class="sxs-lookup"><span data-stu-id="1a733-147">Save your changes.</span></span>

## <a name="registering-for-notifications-using-hello-webapi-backend"></a><span data-ttu-id="1a733-148">A registar notificações utilizando Olá back-end WebAPI</span><span class="sxs-lookup"><span data-stu-id="1a733-148">Registering for Notifications using hello WebAPI Backend</span></span>
<span data-ttu-id="1a733-149">Nesta secção, iremos adicionar que um novo back-end toohandle do controlador toohello end WebAPI pedidos tooregister um utilizador e dispositivo para as notificações com a biblioteca de cliente de Olá para os notification hubs.</span><span class="sxs-lookup"><span data-stu-id="1a733-149">In this section, we will add a new controller toohello WebAPI backend toohandle requests tooregister a user and device for notifications using hello client library for notification hubs.</span></span> <span data-ttu-id="1a733-150">controlador Olá irá adicionar uma etiqueta de utilizador para o utilizador Olá que foi autenticado e anexado toohello HttpContext por Olá `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="1a733-150">hello controller will add a user tag for hello user that was authenticated and attached toohello HttpContext by hello `AuthenticationTestHandler`.</span></span> <span data-ttu-id="1a733-151">etiqueta de Olá terão o formato de cadeia Olá, `"username:<actual username>"`.</span><span class="sxs-lookup"><span data-stu-id="1a733-151">hello tag will have hello string format, `"username:<actual username>"`.</span></span>

1. <span data-ttu-id="1a733-152">No Explorador de soluções, faça duplo clique Olá **AppBackend** projeto e, em seguida, clique em **gerir pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1a733-152">In Solution Explorer, right-click hello **AppBackend** project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="1a733-153">No lado esquerdo Olá, clique em **Online**e procure **notificationhubs** no Olá **pesquisa** caixa.</span><span class="sxs-lookup"><span data-stu-id="1a733-153">On hello left-hand side, click **Online**, and search for **Microsoft.Azure.NotificationHubs** in hello **Search** box.</span></span>
3. <span data-ttu-id="1a733-154">Na lista de resultados de Olá, clique em **os Notification Hubs do Microsoft Azure**e, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="1a733-154">In hello results list, click **Microsoft Azure Notification Hubs**, and then click **Install**.</span></span> <span data-ttu-id="1a733-155">Concluir a instalação de Olá, em seguida, feche a janela do Gestor de pacotes de NuGet de Olá.</span><span class="sxs-lookup"><span data-stu-id="1a733-155">Complete hello installation, then close hello NuGet package manager window.</span></span>
   
    <span data-ttu-id="1a733-156">Esta ação adiciona uma referência toohello SDK dos Notification Hubs do Azure utilizando Olá <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet do Microsoft Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="1a733-156">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="1a733-157">Iremos agora criar um novo ficheiro de classe que representa a ligação de Olá com o notification hub utilizado toosend notificações.</span><span class="sxs-lookup"><span data-stu-id="1a733-157">We will now create a new class file that represents hello connection with notification hub used toosend notifications.</span></span> <span data-ttu-id="1a733-158">No Explorador de soluções Olá, faça duplo clique Olá **modelos** pasta, clique em **adicionar**, em seguida, clique em **classe**.</span><span class="sxs-lookup"><span data-stu-id="1a733-158">In hello Solution Explorer, right-click hello **Models** folder, click **Add**, then click **Class**.</span></span> <span data-ttu-id="1a733-159">Nome da nova classe de Olá **Notifications.cs**, em seguida, clique em **adicionar** classe de Olá toogenerate.</span><span class="sxs-lookup"><span data-stu-id="1a733-159">Name hello new class **Notifications.cs**, then click **Add** toogenerate hello class.</span></span> 
   
    ![][B6]
5. <span data-ttu-id="1a733-160">No Notifications.cs, adicione o seguinte de Olá `using` declaração, Olá parte superior do ficheiro de Olá:</span><span class="sxs-lookup"><span data-stu-id="1a733-160">In Notifications.cs, add hello following `using` statement at hello top of hello file:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
6. <span data-ttu-id="1a733-161">Substitua Olá `Notifications` definição com o seguinte Olá de classe, certifique-se tooreplace Olá dois marcadores de posição pelo cadeia de ligação de Olá (com acesso total) para o seu hub de notificação e Olá nome do hub (disponível em [Portal clássico do Azure ](http://manage.windowsazure.com)):</span><span class="sxs-lookup"><span data-stu-id="1a733-161">Replace hello `Notifications` class definition with hello following and make sure tooreplace hello two placeholders with hello connection string (with full access) for your notification hub, and hello hub name (available at [Azure Classic Portal](http://manage.windowsazure.com)):</span></span>
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. <span data-ttu-id="1a733-162">Em seguida, vamos criar um controlador novo com o nome **RegisterController**.</span><span class="sxs-lookup"><span data-stu-id="1a733-162">Next we will create a new controller named **RegisterController**.</span></span> <span data-ttu-id="1a733-163">No Explorador de soluções, faça duplo clique Olá **controladores** pasta, em seguida, clique em **adicionar**, em seguida, clique em **controlador**.</span><span class="sxs-lookup"><span data-stu-id="1a733-163">In Solution Explorer, right-click hello **Controllers** folder, then click **Add**, then click **Controller**.</span></span> <span data-ttu-id="1a733-164">Clique em Olá **controlador no Web API 2 – vazio** item e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1a733-164">Click hello **Web API 2 Controller -- Empty** item, and then click **Add**.</span></span> <span data-ttu-id="1a733-165">Nome da nova classe de Olá **RegisterController**e, em seguida, clique em **adicionar** novamente o controlador de Olá toogenerate.</span><span class="sxs-lookup"><span data-stu-id="1a733-165">Name hello new class **RegisterController**, and then click **Add** again toogenerate hello controller.</span></span>
   
    ![][B7]
   
    ![][B8]
8. <span data-ttu-id="1a733-166">No RegisterController.cs, adicione o seguinte de Olá `using` instruções:</span><span class="sxs-lookup"><span data-stu-id="1a733-166">In RegisterController.cs, add hello following `using` statements:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. <span data-ttu-id="1a733-167">Adicionar Olá seguinte código dentro de Olá `RegisterController` definição de classe.</span><span class="sxs-lookup"><span data-stu-id="1a733-167">Add hello following code inside hello `RegisterController` class definition.</span></span> <span data-ttu-id="1a733-168">Tenha em atenção que neste código, iremos adicionar uma etiqueta de utilizador para o utilizador Olá é anexado toohello HttpContext.</span><span class="sxs-lookup"><span data-stu-id="1a733-168">Note that in this code, we add a user tag for hello user this is attached toohello HttpContext.</span></span> <span data-ttu-id="1a733-169">utilizador Olá foi autenticado e anexado toohello HttpContext pelo filtro de mensagem de Olá adicionámos, `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="1a733-169">hello user was authenticated and attached toohello HttpContext by hello message filter we added, `AuthenticationTestHandler`.</span></span> <span data-ttu-id="1a733-170">Também pode adicionar tooverify verificações opcional que Olá utilizador tem direitos tooregister para Olá pedida etiquetas.</span><span class="sxs-lookup"><span data-stu-id="1a733-170">You can also add optional checks tooverify that hello user has rights tooregister for hello requested tags.</span></span>
   
        private NotificationHubClient hub;
   
        public RegisterController()
        {
            hub = Notifications.Instance.Hub;
        }
   
        public class DeviceRegistration
        {
            public string Platform { get; set; }
            public string Handle { get; set; }
            public string[] Tags { get; set; }
        }
   
        // POST api/register
        // This creates a registration id
        public async Task<string> Post(string handle = null)
        {
            string newRegistrationId = null;
   
            // make sure there are no existing registrations for this push handle (used for iOS and Android)
            if (handle != null)
            {
                var registrations = await hub.GetRegistrationsByChannelAsync(handle, 100);
   
                foreach (RegistrationDescription registration in registrations)
                {
                    if (newRegistrationId == null)
                    {
                        newRegistrationId = registration.RegistrationId;
                    }
                    else
                    {
                        await hub.DeleteRegistrationAsync(registration);
                    }
                }
            }
   
            if (newRegistrationId == null) 
                newRegistrationId = await hub.CreateRegistrationIdAsync();
   
            return newRegistrationId;
        }
   
        // PUT api/register/5
        // This creates or updates a registration (with provided channelURI) at hello specified id
        public async Task<HttpResponseMessage> Put(string id, DeviceRegistration deviceUpdate)
        {
            RegistrationDescription registration = null;
            switch (deviceUpdate.Platform)
            {
                case "mpns":
                    registration = new MpnsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "wns":
                    registration = new WindowsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "apns":
                    registration = new AppleRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "gcm":
                    registration = new GcmRegistrationDescription(deviceUpdate.Handle);
                    break;
                default:
                    throw new HttpResponseException(HttpStatusCode.BadRequest);
            }
   
            registration.RegistrationId = id;
            var username = HttpContext.Current.User.Identity.Name;
   
            // add check if user is allowed tooadd these tags
            registration.Tags = new HashSet<string>(deviceUpdate.Tags);
            registration.Tags.Add("username:" + username);
   
            try
            {
                await hub.CreateOrUpdateRegistrationAsync(registration);
            }
            catch (MessagingException e)
            {
                ReturnGoneIfHubResponseIsGone(e);
            }
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        // DELETE api/register/5
        public async Task<HttpResponseMessage> Delete(string id)
        {
            await hub.DeleteRegistrationAsync(id);
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        private static void ReturnGoneIfHubResponseIsGone(MessagingException e)
        {
            var webex = e.InnerException as WebException;
            if (webex.Status == WebExceptionStatus.ProtocolError)
            {
                var response = (HttpWebResponse)webex.Response;
                if (response.StatusCode == HttpStatusCode.Gone)
                    throw new HttpRequestException(HttpStatusCode.Gone.ToString());
            }
        }
10. <span data-ttu-id="1a733-171">Guarde as alterações.</span><span class="sxs-lookup"><span data-stu-id="1a733-171">Save your changes.</span></span>

## <a name="sending-notifications-from-hello-webapi-backend"></a><span data-ttu-id="1a733-172">Enviar notificações de Olá back-end WebAPI</span><span class="sxs-lookup"><span data-stu-id="1a733-172">Sending Notifications from hello WebAPI Backend</span></span>
<span data-ttu-id="1a733-173">Nesta secção, pode adiciona um novo controlador que expõe uma forma de dispositivos de cliente toosend uma notificação com base na etiqueta de nome de utilizador de Olá utilizando a biblioteca de gestão de serviço do Azure Notification Hubs no Olá back-end de ASP.NET WebAPI.</span><span class="sxs-lookup"><span data-stu-id="1a733-173">In this section you add a new controller that exposes a way for client devices toosend a notification based on hello username tag using Azure Notification Hubs Service Management Library in hello ASP.NET WebAPI backend.</span></span>

1. <span data-ttu-id="1a733-174">Crie outro controlador novo com o nome **NotificationsController**.</span><span class="sxs-lookup"><span data-stu-id="1a733-174">Create another new controller named **NotificationsController**.</span></span> <span data-ttu-id="1a733-175">Criá-la Olá mesma forma que criou Olá **RegisterController** na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="1a733-175">Create it hello same way you created hello **RegisterController** in hello previous section.</span></span>
2. <span data-ttu-id="1a733-176">No NotificationsController.cs, adicione o seguinte de Olá `using` instruções:</span><span class="sxs-lookup"><span data-stu-id="1a733-176">In NotificationsController.cs, add hello following `using` statements:</span></span>
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. <span data-ttu-id="1a733-177">Adicionar Olá seguinte método toohello **NotificationsController** classe.</span><span class="sxs-lookup"><span data-stu-id="1a733-177">Add hello following method toohello **NotificationsController** class.</span></span>
   
    <span data-ttu-id="1a733-178">Este código de enviar um tipo de notificação com base no serviço de notificação de plataforma (PNS) de Olá `pns` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="1a733-178">This code send a notification type based on hello Platform Notification Service (PNS) `pns` parameter.</span></span> <span data-ttu-id="1a733-179">Olá valor `to_tag` é utilizado tooset Olá *username* tag na mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="1a733-179">hello value of `to_tag` is used tooset hello *username* tag on hello message.</span></span> <span data-ttu-id="1a733-180">Esta etiqueta tem de corresponder a uma etiqueta de nome de utilizador de um registo de hub de notificação ativo.</span><span class="sxs-lookup"><span data-stu-id="1a733-180">This tag must match a username tag of an active notification hub registration.</span></span> <span data-ttu-id="1a733-181">mensagem de notificação de saudação é retirada da corpo Olá de pedido POST Olá e formatada para o destino de Olá PNS.</span><span class="sxs-lookup"><span data-stu-id="1a733-181">hello notification message is pulled from hello body of hello POST request and formatted for hello target PNS.</span></span> 
   
    <span data-ttu-id="1a733-182">Dependendo do serviço de notificação de plataforma (PNS) que os dispositivos suportados utilizam notificações de tooreceive Olá, diferentes notificações são suportadas com diferentes formatos.</span><span class="sxs-lookup"><span data-stu-id="1a733-182">Depending on hello Platform Notification Service (PNS) that your supported devices use tooreceive notifications, different notifications are supported using different formats.</span></span> <span data-ttu-id="1a733-183">Por exemplo, em dispositivos Windows, pode utilizar uma [notificação de alerta com WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) que não seja diretamente suportada por outro PNS.</span><span class="sxs-lookup"><span data-stu-id="1a733-183">For example on Windows devices, you could use a [toast notification with WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) that isn't directly supported by another PNS.</span></span> <span data-ttu-id="1a733-184">Planear toosupport pelo seu back-end seria necessita de notificação de Olá tooformat para uma notificação suportada para Olá PNS dos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="1a733-184">So your backend would need tooformat hello notification into a supported notification for hello PNS of devices you plan toosupport.</span></span> <span data-ttu-id="1a733-185">Em seguida, utilize Olá envio adequado API no Olá [NotificationHubClient classe](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span><span class="sxs-lookup"><span data-stu-id="1a733-185">Then use hello appropriate send API on hello [NotificationHubClient class](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span></span>
   
        public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag)
        {
            var user = HttpContext.Current.User.Identity.Name;
            string[] userTag = new string[2];
            userTag[0] = "username:" + to_tag;
            userTag[1] = "from:" + user;
   
            Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;
            HttpStatusCode ret = HttpStatusCode.InternalServerError;
   
            switch (pns.ToLower())
            {
                case "wns":
                    // Windows 8.1 / Windows Phone 8.1
                    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" + 
                                "From " + user + ": " + message + "</text></binding></visual></toast>";
                    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
                    break;
                case "apns":
                    // iOS
                    var alert = "{\"aps\":{\"alert\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(alert, userTag);
                    break;
                case "gcm":
                    // Android
                    var notif = "{ \"data\" : {\"message\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendGcmNativeNotificationAsync(notif, userTag);
                    break;
            }
   
            if (outcome != null)
            {
                if (!((outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Abandoned) ||
                    (outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Unknown)))
                {
                    ret = HttpStatusCode.OK;
                }
            }
   
            return Request.CreateResponse(ret);
        }
4. <span data-ttu-id="1a733-186">Prima **F5** toorun Olá aplicação e tooensure Olá precisão do seu trabalho até ao momento.</span><span class="sxs-lookup"><span data-stu-id="1a733-186">Press **F5** toorun hello application and tooensure hello accuracy of your work so far.</span></span> <span data-ttu-id="1a733-187">aplicação Olá deve iniciar um browser e apresentar a home page do Olá ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1a733-187">hello app should launch a web browser and display hello ASP.NET home page.</span></span> 

## <a name="publish-hello-new-webapi-backend"></a><span data-ttu-id="1a733-188">Publicar Olá novo back-end WebAPI</span><span class="sxs-lookup"><span data-stu-id="1a733-188">Publish hello new WebAPI Backend</span></span>
1. <span data-ttu-id="1a733-189">Agora iremos implementar esta tooan de aplicação Web site do Azure na ordem toomake-lo acessível a partir de todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="1a733-189">Now we will deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="1a733-190">Clique com o botão direito no Olá **AppBackend** projeto e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="1a733-190">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="1a733-191">Selecione **Serviço de Aplicações do Microsoft Azure** como o destino da publicação e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="1a733-191">Select **Microsoft Azure App Service** as your publish target and click **Publish**.</span></span> <span data-ttu-id="1a733-192">Esta ação abre Olá criar App Service caixa de diálogo, que ajuda a criar todos os Olá recursos do Azure necessários toorun Olá aplicação web do ASP.NET no Azure.</span><span class="sxs-lookup"><span data-stu-id="1a733-192">This opens hello Create App Service dialog, which helps you create all hello necessary Azure resources toorun hello ASP.NET web app in Azure.</span></span>

    ![][B15]
3. <span data-ttu-id="1a733-193">No Olá **criar App Service** caixa de diálogo, selecione a sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a733-193">In hello **Create App Service** dialog, select your Azure account.</span></span> <span data-ttu-id="1a733-194">Clique em **Alterar Tipo** e selecione **Aplicação Web**.</span><span class="sxs-lookup"><span data-stu-id="1a733-194">Click **Change Type** and select **Web App**.</span></span> <span data-ttu-id="1a733-195">Manter Olá **nome da aplicação Web** Olá indicado e selecione **subscrição**, **grupo de recursos**, e **plano do App Service**.</span><span class="sxs-lookup"><span data-stu-id="1a733-195">Keep hello **Web App Name** given and select hello **Subscription**, **Resource Group**, and **App Service Plan**.</span></span>  <span data-ttu-id="1a733-196">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1a733-196">Click **Create**.</span></span>

4. <span data-ttu-id="1a733-197">Tome nota do Olá **URL do Site** propriedade no Olá **resumo** secção.</span><span class="sxs-lookup"><span data-stu-id="1a733-197">Make a note of hello **Site URL** property in hello **Summary** section.</span></span> <span data-ttu-id="1a733-198">Iremos dar toothis URL como o *ponto final de back-end* mais à frente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="1a733-198">We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="1a733-199">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="1a733-199">Click **Publish**.</span></span>

5. <span data-ttu-id="1a733-200">Após a conclusão do Assistente de Olá, publica Olá ASP.NET web app tooAzure e, em seguida, inicia Olá aplicação no browser predefinido de Olá.</span><span class="sxs-lookup"><span data-stu-id="1a733-200">Once hello wizard completes, it publishes hello ASP.NET web app tooAzure, and then launches hello app in hello default browser.</span></span>  <span data-ttu-id="1a733-201">A aplicação estará visualizável no Serviço de Aplicações do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a733-201">Your application will be viewable in Azure App Services.</span></span>

<span data-ttu-id="1a733-202">URL de Olá utiliza Olá nome da aplicação web que especificou anteriormente, com Olá formato http://<app_name>.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="1a733-202">hello URL uses hello web app name that you specified earlier, with hello format http://<app_name>.azurewebsites.net.</span></span>

[B1]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push1.png
[B2]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push2.png
[B3]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push3.png
[B4]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push4.png
[B5]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push5.png
[B6]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push6.png
[B7]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push7.png
[B8]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push8.png
[B14]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push14.png
[B15]: ./media/notification-hubs-aspnet-backend-notifyusers/publish-to-app-service.png
[B16]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users16.PNG
[B18]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users18.PNG
