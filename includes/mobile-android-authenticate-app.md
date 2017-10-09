
1. <span data-ttu-id="578ae-101">Abra o projeto de Olá no Android Studio.</span><span class="sxs-lookup"><span data-stu-id="578ae-101">Open hello project in Android Studio.</span></span>

2. <span data-ttu-id="578ae-102">No **Explorador de projeto** no Android Studio, abra o ficheiro ToDoActivity.java de Olá e adicione Olá seguir as instruções de importação:</span><span class="sxs-lookup"><span data-stu-id="578ae-102">In **Project Explorer** in Android Studio, open hello ToDoActivity.java file and add hello following import statements:</span></span>

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. <span data-ttu-id="578ae-103">Adicionar Olá seguinte método toohello **ToDoActivity** classe:</span><span class="sxs-lookup"><span data-stu-id="578ae-103">Add hello following method toohello **ToDoActivity** class:</span></span>

        // You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
        public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

        private void authenticate() {
            // Login using hello Google provider.
            mClient.login("Google", "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
        }

        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent data) {
            // When request completes
            if (resultCode == RESULT_OK) {
                // Check hello request code matches hello one we send in hello login request
                if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
                    MobileServiceActivityResult result = mClient.onActivityResult(data);
                    if (result.isLoggedIn()) {
                        // login succeeded
                        createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                        createTable();
                    } else {
                        // login failed, check hello error message
                        String errorMessage = result.getErrorMessage();
                        createAndShowDialog(errorMessage, "Error");
                    }
                }
            }
        }

    <span data-ttu-id="578ae-104">Este código cria um Olá toohandle de método processo de autenticação da Google.</span><span class="sxs-lookup"><span data-stu-id="578ae-104">This code creates a method toohandle hello Google authentication process.</span></span> <span data-ttu-id="578ae-105">Uma caixa de diálogo apresenta Olá ID de utilizador de Olá autenticado.</span><span class="sxs-lookup"><span data-stu-id="578ae-105">A dialog displays hello ID of hello authenticated user.</span></span> <span data-ttu-id="578ae-106">Só pode prosseguir numa autenticação com êxito.</span><span class="sxs-lookup"><span data-stu-id="578ae-106">You can only proceed on a successful authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="578ae-107">Se estiver a utilizar um fornecedor de identidade que não seja o Google, altere o valor de Olá transmitido toohello **início de sessão** tooone de método de Olá os seguintes valores: _MicrosoftAccount_, _Facebook_, _Twitter_, ou _windowsazureactivedirectory_.</span><span class="sxs-lookup"><span data-stu-id="578ae-107">If you are using an identity provider other than Google, change hello value passed toohello **login** method tooone of hello following values: _MicrosoftAccount_, _Facebook_, _Twitter_, or _windowsazureactivedirectory_.</span></span>

4. <span data-ttu-id="578ae-108">No Olá **onCreate** método, adicione Olá seguinte linha de código depois código Olá que cria uma instância Olá `MobileServiceClient` objeto.</span><span class="sxs-lookup"><span data-stu-id="578ae-108">In hello **onCreate** method, add hello following line of code after hello code that instantiates hello `MobileServiceClient` object.</span></span>

        authenticate();

    <span data-ttu-id="578ae-109">Esta chamada inicia o processo de autenticação de Olá.</span><span class="sxs-lookup"><span data-stu-id="578ae-109">This call starts hello authentication process.</span></span>

5. <span data-ttu-id="578ae-110">Mover Olá restantes código após `authenticate();` no Olá **onCreate** tooa método novo **createTable** método:</span><span class="sxs-lookup"><span data-stu-id="578ae-110">Move hello remaining code after `authenticate();` in hello **onCreate** method tooa new **createTable** method:</span></span>

        private void createTable() {

            // Get hello table instance toouse.
            mToDoTable = mClient.getTable(ToDoItem.class);

            mTextNewToDo = (EditText) findViewById(R.id.textNewToDo);

            // Create an adapter toobind hello items with hello view.
            mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
            ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
            listViewToDo.setAdapter(mAdapter);

            // Load hello items from Azure.
            refreshItemsFromTable();
        }

6. <span data-ttu-id="578ae-111">tooensure redirecionamento funciona conforme esperado, adicionar Olá seguinte fragmento de _RedirectUrlActivity_ too_AndroidManifest.xml_:</span><span class="sxs-lookup"><span data-stu-id="578ae-111">tooensure redirection works as expected, add hello following snippet of _RedirectUrlActivity_ too_AndroidManifest.xml_:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. <span data-ttu-id="578ae-112">Adicione redirectUriScheme too_build.gradle_ da sua aplicação Android.</span><span class="sxs-lookup"><span data-stu-id="578ae-112">Add redirectUriScheme too_build.gradle_ of your Android application.</span></span>

        android {
            buildTypes {
                release {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
                debug {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
            }
        }

8. <span data-ttu-id="578ae-113">Adicione com.android.support:customtabs:23.0.1 toohello dependências no seu gradle:</span><span class="sxs-lookup"><span data-stu-id="578ae-113">Add com.android.support:customtabs:23.0.1 toohello dependencies in your build.gradle:</span></span>

      <span data-ttu-id="578ae-114">dependências {/ /... Compilar 'com.android.support:customtabs:23.0.1'}</span><span class="sxs-lookup"><span data-stu-id="578ae-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span></span>

9. <span data-ttu-id="578ae-115">De Olá **executar** menu, clique em **executar a aplicação** toostart Olá aplicação e inicie sessão com o fornecedor de identidade que escolheu.</span><span class="sxs-lookup"><span data-stu-id="578ae-115">From hello **Run** menu, click **Run app** toostart hello app and sign in with your chosen identity provider.</span></span>

> [!WARNING]
> <span data-ttu-id="578ae-116">Olá esquema de URL mencionado diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="578ae-116">hello URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="578ae-117">Certifique-se de que todas as ocorrências de `{url_scheme_of_you_app}` utilize Olá mesmo maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="578ae-117">Ensure that all occurrences of `{url_scheme_of_you_app}` use hello same case.</span></span>

<span data-ttu-id="578ae-118">Quando com êxito tem sessão iniciada, aplicação Olá deverão ser executadas sem erros, e deve ser tooquery capaz de serviço de back-end de Olá e tornar toodata de atualizações.</span><span class="sxs-lookup"><span data-stu-id="578ae-118">When you are successfully signed in, hello app should run without errors, and you should be able tooquery hello back-end service and make updates toodata.</span></span>
