[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister web API, utilize definições de Olá especificadas na tabela de Olá.

![Definições de registo de exemplo para a nova API Web](./media/active-directory-b2c-register-web-api/b2c-new-web-api-settings.png)

| Definição      | Valor da amostra  | Descrição                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Nome** | API Contoso B2C | Introduza um **nome** para aplicação Olá que descreve o tooconsumers de API. | 
| **Incluir aplicação/API Web** | Sim | Selecione **Sim** para uma API Web. |
| **Permitir fluxo implícito** | Sim | Selecione **Sim** se a sua aplicação utilizar o [Início de sessão OpenID Connect](../articles/active-directory-b2c/active-directory-b2c-reference-oidc.md) |
| **URL de resposta** | `https://localhost:44316/` | Os URLs de resposta são pontos finais para onde o Azure AD B2C devolve quaisquer tokens que a aplicação solicite. Introduza [um](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-web-app-or-api-reply-url) **URL de resposta** adequado. Neste exemplo, a API Web é local e está a escutar na porta 44316. |
| **URI do ID da Aplicação** | api | Olá URI de ID de aplicação é o identificador de Olá utilizado para a API web. Olá identificador completo do URI, incluindo o domínio de Olá é gerado por si. |

Clique em **criar** tooregister a aplicação.

A aplicação recentemente registada é apresentada na lista de aplicações de Olá para o inquilino do B2C Olá. Selecione a API web de lista de Olá. é apresentado o painel de propriedade Olá da API.

![Propriedades da API Web](./media/active-directory-b2c-register-web-api/b2c-web-api-properties.png)

Tome nota dos Olá globalmente exclusivo **ID de cliente da aplicação**. Utilize o ID de Olá no código da aplicação.
