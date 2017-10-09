### <a name="server-auth"></a>Como: autenticar com um fornecedor (Fluxo de Servidor)
toohave Mobile Apps gerir o processo de autenticação de Olá na sua aplicação, tem de registar a aplicação com o seu fornecedor de identidade. Em seguida, no seu serviço de aplicações do Azure, terá de ID da aplicação Olá tooconfigure e o segredo fornecida pelo seu fornecedor.
Para obter mais informações, consulte o tutorial Olá [adicionar autenticação tooyour aplicação](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).

Depois de ter registado o fornecedor de identidade, chamar Olá `.login()` método com o nome de Olá do seu fornecedor. Por exemplo, toologin com o Facebook utilizar Olá seguinte código:

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

os valores válidos de Olá para o fornecedor de Olá são 'aad', 'facebook', 'google', 'microsoftaccount' e 'twitter'.

> [!NOTE]
> A Autenticação da Google não funciona atualmente através do Fluxo de Servidor.  tooauthenticate com o Google, tem de utilizar um [método de fluxo de cliente](#client-auth).

Neste caso, o App Service do Azure gere o fluxo de autenticação de Olá OAuth 2.0.  Apresenta a página de início de sessão de Olá do fornecedor selecionado Olá e gera um token de autenticação do serviço de aplicações após o início de sessão com êxito com o fornecedor de identidade Olá. função de início de sessão de Olá, quando terminar, devolve um objeto JSON que expõe Olá ID de utilizador e do serviço de aplicações token de autenticação em campos de userId e authenticationToken Olá, respetivamente. Este token pode ser colocado em cache e reutilizado até expirar.

###<a name="client-auth"></a>Como: autenticar com um fornecedor (Fluxo de Cliente)

A aplicação pode também independentemente contacte o fornecedor de identidade Olá e, em seguida, fornecer Olá devolvido tooyour token do serviço de aplicações para autenticação. Este fluxo de cliente permite-lhe tooprovide uma experiência de início de sessão único para utilizadores ou dados de utilizador adicionais de tooretrieve do fornecedor de identidade Olá.

#### <a name="social-authentication-basic-example"></a>Exemplo básico de Autenticação nas Redes Sociais

Este exemplo utiliza o SDK cliente do Facebook para autenticação:

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
Este exemplo assume que token Olá fornecida pelo fornecedor respetivos Olá SDK é armazenado na variável de token de Olá.

#### <a name="microsoft-account-example"></a>Exemplo da Conta Microsoft

Olá exemplo utiliza os seguintes Olá Live SDK, que suporta single-sign-on para aplicações da loja Windows, utilizando Account Microsoft:

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

Neste exemplo obtém um token de estabelecer a ligação em direto, que é fornecido tooyour do serviço de aplicações ao chamar a função de início de sessão de Olá.

###<a name="auth-getinfo"></a>Como: obter informações sobre o utilizador Olá autenticado

as informações de autenticação de Olá podem ser obtidas Olá `/.auth/me` ponto final utilizando um HTTP chamar com qualquer biblioteca AJAX.  Certifique-se de que definiu Olá `X-ZUMO-AUTH` token de autenticação de tooyour do cabeçalho.  Olá token de autenticação é armazenada na `client.currentUser.mobileServiceAuthenticationToken`.  Por exemplo, toouse Olá obtenção API:

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

A obtenção está disponível como [um pacote de npm](https://www.npmjs.com/package/whatwg-fetch) ou para transferência de browser a partir do [CDNJS](https://cdnjs.com/libraries/fetch). Pode também utilizar jQuery ou outros API de AJAX toofetch Olá as informações.  Os dados são recebidos como um objeto JSON.
