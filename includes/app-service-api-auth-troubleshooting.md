A maioria dos erros de autenticação de tempo de Olá resulta de definições de configuração inconsistentes ou incorretos. Aqui estão algumas sugestões específicos para toocheck coisas.

* Certifique-se de que não tenha perder Olá **guardar** botão em qualquer lugar. Isto é frequentemente toodo fácil, não sendo resultado Olá que que irá ser observar valores corretos Olá numa página de portal, mas, na verdade, não foram guardadas no Olá ambiente do Azure ou a aplicação do Azure AD.
* Para as definições configuradas na Olá **definições da aplicação** painel de Olá portal do Azure, certifique-se de que Olá correto de aplicação API ou aplicação web foi selecionada quando as definições de Olá foram introduzidas.  Certifique-se de que as definições de Olá foram introduzidas como também **as definições de aplicação** e não **cadeias de ligação**, uma vez que o formato de Olá de secções de Olá dois é semelhante.
* Autenticação tooa JavaScript front-end, transferência Olá manifesto novamente tooverify que `oauth2AllowImplicitFlow` foi alterada com êxito demasiado`true`.
* Certifique-se de que utilizou HTTPS independentemente do local onde configurou URLs:
  
  * No código de projeto
  * No CORS
  * Nas definições de aplicação de ambiente do Azure para cada aplicação API e a aplicação web
  * Nas definições de aplicação do Azure AD.
    
    Tenha em atenção que se copiar o URL de uma aplicação API a partir do portal de Olá, muitas vezes tem `http://` e tiver toomanually alterá-la demasiado`https://`.
* Certifique-se de que as alterações de código foram implementadas com êxito. Por exemplo, uma solução de vários projeto é possível toochange um projeto de código e acidentalmente escolha uma das Olá outras pessoas quando pretende alteração de Olá toodeploy.
* Certifique-se de que vai tooHTTPS URLs no browser, não os URLs de HTTP. Por predefinição, o Visual Studio cria publicar perfis com HTTP URLs e que é o que abre no browser Olá depois de implementar um projeto.
* Para autenticação tooa JavaScript front-end, certifique-se de que está corretamente configurada CORS na aplicação de API de Olá Olá chamadas de código JavaScript. Em caso de dúvida sobre se o problema de Olá está relacionado com a CORS, tente "*" como Olá permitido URL de origem. 
* Para um JavaScript front-end, abra tooget de separador de consola de ferramentas de programador do seu browser obter mais informações de erro e examine a pedidos HTTP na Olá rede. No entanto, poderá enganosa mensagens de erro de consola. Se receber uma mensagem a indicar um erro CORS, o problema real Olá poderá autenticação. Pode verificar se é este Olá caso executando a aplicação Olá com autenticação temporariamente temporariamente desativada.
* Para uma aplicação .NET API, certifique-se estão a obter a maior quantidade informações em mensagens de erro possível definindo [customErrors modo tooOff](../articles/app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remoteview).
* Para uma aplicação .NET API, inicie um [sessão de depuração remota](../articles/app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug)e examine a valores de Olá das variáveis de Olá que são transmitidos toocode que utiliza a ADAL tooacquire um token de portador, ou um código que verifica as afirmações com o ID de principal de serviço de Olá esperado Tenha em atenção que o seu código pode recolher valores de configuração a partir de várias origens diferentes, pelo que é possível toofind surpresas desta forma. Por exemplo, se de que escreveu `ida:ClientId` como `ida:ClientID` quando configurar as definições de ambiente de App Service do Azure, o código de Olá poderá obter Olá `ida:ClientId` valor está à procura do ficheiro Web. config de Olá, a ignorar a definição de serviço de aplicações do Azure Olá. 
* Se as coisas não funcionam numa janela do Internet Explorer normal, uma existente início de sessão pode estar a interferir; Tente InPrivate e tente Chrome ou o Firefox.

