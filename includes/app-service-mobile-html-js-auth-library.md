### <span data-ttu-id="0f725-101"><a name="server-auth"></a>Como: autenticar com um fornecedor (Fluxo de Servidor)</span><span class="sxs-lookup"><span data-stu-id="0f725-101"><a name="server-auth"></a>How to: Authenticate with a provider (Server Flow)</span></span>
<span data-ttu-id="0f725-102">toohave Mobile Apps gerir o processo de autenticação de Olá na sua aplicação, tem de registar a aplicação com o seu fornecedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="0f725-102">toohave Mobile Apps manage hello authentication process in your app, you must register your app with your identity provider.</span></span> <span data-ttu-id="0f725-103">Em seguida, no seu serviço de aplicações do Azure, terá de ID da aplicação Olá tooconfigure e o segredo fornecida pelo seu fornecedor.</span><span class="sxs-lookup"><span data-stu-id="0f725-103">Then in your Azure App Service, you need tooconfigure hello application ID and secret provided by your provider.</span></span>
<span data-ttu-id="0f725-104">Para obter mais informações, consulte o tutorial Olá [adicionar autenticação tooyour aplicação](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="0f725-104">For more information, see hello tutorial [Add authentication tooyour app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span></span>

<span data-ttu-id="0f725-105">Depois de ter registado o fornecedor de identidade, chamar Olá `.login()` método com o nome de Olá do seu fornecedor.</span><span class="sxs-lookup"><span data-stu-id="0f725-105">Once you have registered your identity provider, call hello `.login()` method with hello name of your provider.</span></span> <span data-ttu-id="0f725-106">Por exemplo, toologin com o Facebook utilizar Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="0f725-106">For example, toologin with Facebook use hello following code:</span></span>

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

<span data-ttu-id="0f725-107">os valores válidos de Olá para o fornecedor de Olá são 'aad', 'facebook', 'google', 'microsoftaccount' e 'twitter'.</span><span class="sxs-lookup"><span data-stu-id="0f725-107">hello valid values for hello provider are 'aad', 'facebook', 'google', 'microsoftaccount', and 'twitter'.</span></span>

> [!NOTE]
> <span data-ttu-id="0f725-108">A Autenticação da Google não funciona atualmente através do Fluxo de Servidor.</span><span class="sxs-lookup"><span data-stu-id="0f725-108">Google Authentication does not currently work via Server Flow.</span></span>  <span data-ttu-id="0f725-109">tooauthenticate com o Google, tem de utilizar um [método de fluxo de cliente](#client-auth).</span><span class="sxs-lookup"><span data-stu-id="0f725-109">tooauthenticate with Google, you must use a [client-flow method](#client-auth).</span></span>

<span data-ttu-id="0f725-110">Neste caso, o App Service do Azure gere o fluxo de autenticação de Olá OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="0f725-110">In this case, Azure App Service manages hello OAuth 2.0 authentication flow.</span></span>  <span data-ttu-id="0f725-111">Apresenta a página de início de sessão de Olá do fornecedor selecionado Olá e gera um token de autenticação do serviço de aplicações após o início de sessão com êxito com o fornecedor de identidade Olá.</span><span class="sxs-lookup"><span data-stu-id="0f725-111">It displays hello login page of hello selected provider and generates an App Service authentication token after successful login with hello identity provider.</span></span> <span data-ttu-id="0f725-112">função de início de sessão de Olá, quando terminar, devolve um objeto JSON que expõe Olá ID de utilizador e do serviço de aplicações token de autenticação em campos de userId e authenticationToken Olá, respetivamente.</span><span class="sxs-lookup"><span data-stu-id="0f725-112">hello login function, when complete, returns a JSON object that exposes both hello user ID and App Service authentication token in hello userId and authenticationToken fields, respectively.</span></span> <span data-ttu-id="0f725-113">Este token pode ser colocado em cache e reutilizado até expirar.</span><span class="sxs-lookup"><span data-stu-id="0f725-113">This token can be cached and reused until it expires.</span></span>

###<span data-ttu-id="0f725-114"><a name="client-auth"></a>Como: autenticar com um fornecedor (Fluxo de Cliente)</span><span class="sxs-lookup"><span data-stu-id="0f725-114"><a name="client-auth"></a>How to: Authenticate with a provider (Client Flow)</span></span>

<span data-ttu-id="0f725-115">A aplicação pode também independentemente contacte o fornecedor de identidade Olá e, em seguida, fornecer Olá devolvido tooyour token do serviço de aplicações para autenticação.</span><span class="sxs-lookup"><span data-stu-id="0f725-115">Your app can also independently contact hello identity provider and then provide hello returned token tooyour App Service for authentication.</span></span> <span data-ttu-id="0f725-116">Este fluxo de cliente permite-lhe tooprovide uma experiência de início de sessão único para utilizadores ou dados de utilizador adicionais de tooretrieve do fornecedor de identidade Olá.</span><span class="sxs-lookup"><span data-stu-id="0f725-116">This client flow enables you tooprovide a single sign-in experience for users or tooretrieve additional user data from hello identity provider.</span></span>

#### <a name="social-authentication-basic-example"></a><span data-ttu-id="0f725-117">Exemplo básico de Autenticação nas Redes Sociais</span><span class="sxs-lookup"><span data-stu-id="0f725-117">Social Authentication basic example</span></span>

<span data-ttu-id="0f725-118">Este exemplo utiliza o SDK cliente do Facebook para autenticação:</span><span class="sxs-lookup"><span data-stu-id="0f725-118">This example uses Facebook client SDK for authentication:</span></span>

```
client.login(
     "facebook",
     {"access_token": token})
.done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});

```
<span data-ttu-id="0f725-119">Este exemplo assume que token Olá fornecida pelo fornecedor respetivos Olá SDK é armazenado na variável de token de Olá.</span><span class="sxs-lookup"><span data-stu-id="0f725-119">This example assumes that hello token provided by hello respective provider SDK is stored in hello token variable.</span></span>

#### <a name="microsoft-account-example"></a><span data-ttu-id="0f725-120">Exemplo da Conta Microsoft</span><span class="sxs-lookup"><span data-stu-id="0f725-120">Microsoft Account example</span></span>

<span data-ttu-id="0f725-121">Olá exemplo utiliza os seguintes Olá Live SDK, que suporta single-sign-on para aplicações da loja Windows, utilizando Account Microsoft:</span><span class="sxs-lookup"><span data-stu-id="0f725-121">hello following example uses hello Live SDK, which supports single-sign-on for Windows Store apps by using Microsoft Account:</span></span>

```
WL.login({ scope: "wl.basic"}).then(function (result) {
      client.login(
            "microsoftaccount",
            {"authenticationToken": result.session.authentication_token})
      .done(function(results){
            alert("You are now logged in as: " + results.userId);
      },
      function(error){
            alert("Error: " + err);
      });
});

```

<span data-ttu-id="0f725-122">Neste exemplo obtém um token de estabelecer a ligação em direto, que é fornecido tooyour do serviço de aplicações ao chamar a função de início de sessão de Olá.</span><span class="sxs-lookup"><span data-stu-id="0f725-122">This example gets a token from Live Connect, which is supplied tooyour App Service by calling hello login function.</span></span>

###<span data-ttu-id="0f725-123"><a name="auth-getinfo"></a>Como: obter informações sobre o utilizador Olá autenticado</span><span class="sxs-lookup"><span data-stu-id="0f725-123"><a name="auth-getinfo"></a>How to: Obtain information about hello authenticated user</span></span>

<span data-ttu-id="0f725-124">as informações de autenticação de Olá podem ser obtidas Olá `/.auth/me` ponto final utilizando um HTTP chamar com qualquer biblioteca AJAX.</span><span class="sxs-lookup"><span data-stu-id="0f725-124">hello authentication information can be retrieved from hello `/.auth/me` endpoint using an HTTP call with any AJAX library.</span></span>  <span data-ttu-id="0f725-125">Certifique-se de que definiu Olá `X-ZUMO-AUTH` token de autenticação de tooyour do cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="0f725-125">Ensure you set hello `X-ZUMO-AUTH` header tooyour authentication token.</span></span>  <span data-ttu-id="0f725-126">Olá token de autenticação é armazenada na `client.currentUser.mobileServiceAuthenticationToken`.</span><span class="sxs-lookup"><span data-stu-id="0f725-126">hello authentication token is stored in `client.currentUser.mobileServiceAuthenticationToken`.</span></span>  <span data-ttu-id="0f725-127">Por exemplo, toouse Olá obtenção API:</span><span class="sxs-lookup"><span data-stu-id="0f725-127">For example, toouse hello fetch API:</span></span>

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // hello user object contains hello claims for hello authenticated user
    });
```

<span data-ttu-id="0f725-128">A obtenção está disponível como [um pacote de npm](https://www.npmjs.com/package/whatwg-fetch) ou para transferência de browser a partir do [CDNJS](https://cdnjs.com/libraries/fetch).</span><span class="sxs-lookup"><span data-stu-id="0f725-128">Fetch is available as [an npm package](https://www.npmjs.com/package/whatwg-fetch) or for browser download from [CDNJS](https://cdnjs.com/libraries/fetch).</span></span> <span data-ttu-id="0f725-129">Pode também utilizar jQuery ou outros API de AJAX toofetch Olá as informações.</span><span class="sxs-lookup"><span data-stu-id="0f725-129">You could also use jQuery or another AJAX API toofetch hello information.</span></span>  <span data-ttu-id="0f725-130">Os dados são recebidos como um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="0f725-130">Data is received as a JSON object.</span></span>
