
Olá de exemplo anterior mostrou um padrão início de sessão, que necessita de Olá cliente toocontact ambas Olá identidade fornecedor e Olá back-end do Azure service sempre que inicia a aplicação Olá. Este método é ineficaz e podem ter problemas relacionados com a utilização se muitos clientes tente em simultâneo a aplicação de toostart. Uma abordagem de melhor é o token de autorização de Olá toocache devolvido pelo Olá serviço do Azure e tente toouse este primeiro antes de utilizar um fornecedor com base no início de sessão.

> [!NOTE]
> Pode colocar em cache o token de Olá emitido por Olá back-end do Azure service independentemente se estão a utilizar autenticação geridos pelo cliente ou serviço gerido. Este tutorial utiliza a autenticação de serviço gerido.
>
>

1. Abra o ficheiro ToDoActivity.java de Olá e adicione Olá seguir as instruções de importação:

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. Adicionar Olá seguintes membros toohello `ToDoActivity` classe.

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. No ficheiro ToDoActivity.java de Olá, adicionar Olá seguinte definição para Olá `cacheUserToken` método.

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    Este método armazena Olá ID de utilizador e o token num ficheiro preferência que está marcado como privado. Isto deve proteger o acesso toohello cache para que as outras aplicações no dispositivo Olá não dispõe de token de toohello de acesso. preferência de Olá é uma aplicação Olá. No entanto, se alguém obtiver o dispositivo de toohello de acesso, é possível que pode ganham acesso toohello token cache através de outros meios.

   > [!NOTE]
   > Pode proteger ainda mais token Olá com encriptação, se o token de acesso tooyour dados considerados altamente confidenciais e alguém obter dispositivo toohello de acesso. Uma solução completamente segura ultrapassa o âmbito de Olá deste tutorial, no entanto e depende dos requisitos de segurança.
   >
   >
4. No ficheiro ToDoActivity.java de Olá, adicionar Olá seguinte definição para Olá `loadUserTokenCache` método.

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
5. No Olá *ToDoActivity.java* de ficheiros, substitua Olá `authenticate` método com Olá método, o que utiliza uma cache de token a seguir. Alterar o fornecedor de início de sessão de Olá se quiser toouse uma conta diferente da Google.

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
6. Crie a autenticação de aplicação e o teste de Olá utilizando uma conta válida. Execute, pelo menos, duas vezes. Durante Olá executar pela primeira vez, deverá receber um aviso toosign no e criar a cache de token de Olá. Depois disso, cada execução tenta cache de token Olá tooload para autenticação. Não deve ser necessário toosign no.
