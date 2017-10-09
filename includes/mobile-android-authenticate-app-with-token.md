
<span data-ttu-id="bc59a-101">Olá de exemplo anterior mostrou um padrão início de sessão, que necessita de Olá cliente toocontact ambas Olá identidade fornecedor e Olá back-end do Azure service sempre que inicia a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="bc59a-101">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello back-end Azure service every time hello app starts.</span></span> <span data-ttu-id="bc59a-102">Este método é ineficaz e podem ter problemas relacionados com a utilização se muitos clientes tente em simultâneo a aplicação de toostart.</span><span class="sxs-lookup"><span data-stu-id="bc59a-102">This method is inefficient, and you can have usage-related issues if many customers try toostart your app simultaneously.</span></span> <span data-ttu-id="bc59a-103">Uma abordagem de melhor é o token de autorização de Olá toocache devolvido pelo Olá serviço do Azure e tente toouse este primeiro antes de utilizar um fornecedor com base no início de sessão.</span><span class="sxs-lookup"><span data-stu-id="bc59a-103">A better approach is toocache hello authorization token returned by hello Azure service, and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="bc59a-104">Pode colocar em cache o token de Olá emitido por Olá back-end do Azure service independentemente se estão a utilizar autenticação geridos pelo cliente ou serviço gerido.</span><span class="sxs-lookup"><span data-stu-id="bc59a-104">You can cache hello token issued by hello back-end Azure service regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="bc59a-105">Este tutorial utiliza a autenticação de serviço gerido.</span><span class="sxs-lookup"><span data-stu-id="bc59a-105">This tutorial uses service-managed authentication.</span></span>
>
>

1. <span data-ttu-id="bc59a-106">Abra o ficheiro ToDoActivity.java de Olá e adicione Olá seguir as instruções de importação:</span><span class="sxs-lookup"><span data-stu-id="bc59a-106">Open hello ToDoActivity.java file and add hello following import statements:</span></span>

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. <span data-ttu-id="bc59a-107">Adicionar Olá seguintes membros toohello `ToDoActivity` classe.</span><span class="sxs-lookup"><span data-stu-id="bc59a-107">Add hello following members toohello `ToDoActivity` class.</span></span>

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. <span data-ttu-id="bc59a-108">No ficheiro ToDoActivity.java de Olá, adicionar Olá seguinte definição para Olá `cacheUserToken` método.</span><span class="sxs-lookup"><span data-stu-id="bc59a-108">In hello ToDoActivity.java file, add hello following definition for hello `cacheUserToken` method.</span></span>

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    <span data-ttu-id="bc59a-109">Este método armazena Olá ID de utilizador e o token num ficheiro preferência que está marcado como privado.</span><span class="sxs-lookup"><span data-stu-id="bc59a-109">This method stores hello user ID and token in a preference file that is marked private.</span></span> <span data-ttu-id="bc59a-110">Isto deve proteger o acesso toohello cache para que as outras aplicações no dispositivo Olá não dispõe de token de toohello de acesso.</span><span class="sxs-lookup"><span data-stu-id="bc59a-110">This should protect access toohello cache so that other apps on hello device do not have access toohello token.</span></span> <span data-ttu-id="bc59a-111">preferência de Olá é uma aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="bc59a-111">hello preference is sandboxed for hello app.</span></span> <span data-ttu-id="bc59a-112">No entanto, se alguém obtiver o dispositivo de toohello de acesso, é possível que pode ganham acesso toohello token cache através de outros meios.</span><span class="sxs-lookup"><span data-stu-id="bc59a-112">However, if someone gains access toohello device, it is possible that they may gain access toohello token cache through other means.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bc59a-113">Pode proteger ainda mais token Olá com encriptação, se o token de acesso tooyour dados considerados altamente confidenciais e alguém obter dispositivo toohello de acesso.</span><span class="sxs-lookup"><span data-stu-id="bc59a-113">You can further protect hello token with encryption, if token access tooyour data is considered highly sensitive and someone may gain access toohello device.</span></span> <span data-ttu-id="bc59a-114">Uma solução completamente segura ultrapassa o âmbito de Olá deste tutorial, no entanto e depende dos requisitos de segurança.</span><span class="sxs-lookup"><span data-stu-id="bc59a-114">A completely secure solution is beyond hello scope of this tutorial, however, and depends on your security requirements.</span></span>
   >
   >
4. <span data-ttu-id="bc59a-115">No ficheiro ToDoActivity.java de Olá, adicionar Olá seguinte definição para Olá `loadUserTokenCache` método.</span><span class="sxs-lookup"><span data-stu-id="bc59a-115">In hello ToDoActivity.java file, add hello following definition for hello `loadUserTokenCache` method.</span></span>

        private boolean loadUserTokenCache(MobileServiceClient client)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            String userId = prefs.getString(USERIDPREF, null);
            if (userId == null)
                return false;
            String token = prefs.getString(TOKENPREF, null);
            if (token == null)
                return false;

            MobileServiceUser user = new MobileServiceUser(userId);
            user.setAuthenticationToken(token);
            client.setCurrentUser(user);

            return true;
        }
5. <span data-ttu-id="bc59a-116">No Olá *ToDoActivity.java* de ficheiros, substitua Olá `authenticate` método com Olá método, o que utiliza uma cache de token a seguir.</span><span class="sxs-lookup"><span data-stu-id="bc59a-116">In hello *ToDoActivity.java* file, replace hello `authenticate` method with hello following method, which uses a token cache.</span></span> <span data-ttu-id="bc59a-117">Alterar o fornecedor de início de sessão de Olá se quiser toouse uma conta diferente da Google.</span><span class="sxs-lookup"><span data-stu-id="bc59a-117">Change hello login provider if you want toouse an account other than Google.</span></span>

        private void authenticate() {
            // We first try tooload a token cache if one exists.
            if (loadUserTokenCache(mClient))
            {
                createTable();
            }
            // If we failed tooload a token cache, login and create a token cache
            else
            {
                // Login using hello Google provider.    
                ListenableFuture<MobileServiceUser> mLogin = mClient.login(MobileServiceAuthenticationProvider.Google);

                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        createAndShowDialog("You must log in. Login Required", "Error");
                    }           
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        createAndShowDialog(String.format(
                                "You are now logged in - %1$2s",
                                user.getUserId()), "Success");
                        cacheUserToken(mClient.getCurrentUser());
                        createTable();    
                    }
                });
            }
        }
6. <span data-ttu-id="bc59a-118">Crie a autenticação de aplicação e o teste de Olá utilizando uma conta válida.</span><span class="sxs-lookup"><span data-stu-id="bc59a-118">Build hello app and test authentication using a valid account.</span></span> <span data-ttu-id="bc59a-119">Execute, pelo menos, duas vezes.</span><span class="sxs-lookup"><span data-stu-id="bc59a-119">Run it at least twice.</span></span> <span data-ttu-id="bc59a-120">Durante Olá executar pela primeira vez, deverá receber um aviso toosign no e criar a cache de token de Olá.</span><span class="sxs-lookup"><span data-stu-id="bc59a-120">During hello first run, you should receive a prompt toosign in and create hello token cache.</span></span> <span data-ttu-id="bc59a-121">Depois disso, cada execução tenta cache de token Olá tooload para autenticação.</span><span class="sxs-lookup"><span data-stu-id="bc59a-121">After that, each run attempts tooload hello token cache for authentication.</span></span> <span data-ttu-id="bc59a-122">Não deve ser necessário toosign no.</span><span class="sxs-lookup"><span data-stu-id="bc59a-122">You should not be required toosign in.</span></span>
