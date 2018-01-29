# <a name="call-the-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a>Chamar o Microsoft Graph API a partir de uma aplicação de página de JavaScript única (SPA)

Este guia demonstra como uma aplicação JavaScript página única (SPA) pode iniciar sessão no trabalhos pessoais, e contas escolares, obter um token de acesso e chamar outras APIs que necessitam de tokens de acesso do ponto final v2 do Azure Active Directory ou o Microsoft Graph API.

### <a name="how-this-guide-works"></a>Como funciona este guia

![Como funciona a aplicação de exemplo gerada por este guia](media/active-directory-develop-guidedsetup-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a>Mais Informações

A aplicação de exemplo criada por este guia permite uma SPA JavaScript consultar a Graph API do Microsoft ou uma API Web que aceita tokens de ponto final do Azure Active Directory v2. Para este cenário, depois de um utilizador inicia sessão, um token de acesso pedido e adicionar a pedidos de HTTP através do cabeçalho de autorização. Aquisição do token e renovação são processadas pela biblioteca de autenticação do Microsoft (MSAL).

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a>Bibliotecas

Este guia utiliza a biblioteca seguinte:

|Biblioteca|Descrição|
|---|---|
|[msal.js](https://github.com/AzureAD/microsoft-authentication-library-for-js)|Biblioteca de autenticação da Microsoft para a pré-visualização de JavaScript|

> [!NOTE]
> *msal.js* destinos o *ponto final do Azure Active Directory v2* -permite que o pessoais, profissional e escolar contas iniciar sessão e adquirir tokens. O *ponto final do Azure Active Directory v2* tem [algumas limitações](..\articles\active-directory\develop\active-directory-v2-limitations.md). Se estiver interessado apenas em contas profissional e escolar, utilize *adal.js* e *V1 endpoint*. Para compreender as diferenças entre os pontos finais de v1 e v2 ler o [v1 v2 comparação](..\articles\active-directory\develop\active-directory-v2-compare.md).

<!--end-collapse-->
