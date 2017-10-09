
1. Abra o projeto de Olá no Android Studio.

2. No **Explorador de projeto** no Android Studio, abra o ficheiro ToDoActivity.java de Olá e adicione Olá seguir as instruções de importação:

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. Adicionar Olá seguinte método toohello **ToDoActivity** classe:

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

    Este código cria um Olá toohandle de método processo de autenticação da Google. Uma caixa de diálogo apresenta Olá ID de utilizador de Olá autenticado. Só pode prosseguir numa autenticação com êxito.

    > [!NOTE]
    > Se estiver a utilizar um fornecedor de identidade que não seja o Google, altere o valor de Olá transmitido toohello **início de sessão** tooone de método de Olá os seguintes valores: _MicrosoftAccount_, _Facebook_, _Twitter_, ou _windowsazureactivedirectory_.

4. No Olá **onCreate** método, adicione Olá seguinte linha de código depois código Olá que cria uma instância Olá `MobileServiceClient` objeto.

        authenticate();

    Esta chamada inicia o processo de autenticação de Olá.

5. Mover Olá restantes código após `authenticate();` no Olá **onCreate** tooa método novo **createTable** método:

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

6. tooensure redirecionamento funciona conforme esperado, adicionar Olá seguinte fragmento de _RedirectUrlActivity_ too_AndroidManifest.xml_:

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. Adicione redirectUriScheme too_build.gradle_ da sua aplicação Android.

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

8. Adicione com.android.support:customtabs:23.0.1 toohello dependências no seu gradle:

      dependências {/ /... Compilar 'com.android.support:customtabs:23.0.1'}

9. De Olá **executar** menu, clique em **executar a aplicação** toostart Olá aplicação e inicie sessão com o fornecedor de identidade que escolheu.

> [!WARNING]
> Olá esquema de URL mencionado diferencia maiúsculas de minúsculas.  Certifique-se de que todas as ocorrências de `{url_scheme_of_you_app}` utilize Olá mesmo maiúsculas e minúsculas.

Quando com êxito tem sessão iniciada, aplicação Olá deverão ser executadas sem erros, e deve ser tooquery capaz de serviço de back-end de Olá e tornar toodata de atualizações.
