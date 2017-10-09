[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister a aplicação web, utilize definições de Olá especificadas na tabela de Olá.

![Definições de registo de exemplo para a nova aplicação Web](./media/active-directory-b2c-register-web-app/b2c-new-app-settings.png)

| Definição      | Valor da amostra  | Descrição                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Nome** | Aplicação Contoso B2C | Introduza um **nome** para aplicação Olá que descreve o tooconsumers de aplicação. | 
| **Incluir aplicação/API Web** | Sim | Selecione **Sim** para uma aplicação Web. |
| **Permitir fluxo implícito** | Sim | Selecione **Sim** se a sua aplicação utilizar o [Início de sessão OpenID Connect](../articles/active-directory-b2c/active-directory-b2c-reference-oidc.md) |
| **URL de resposta** | `https://localhost:44316` | Os URLs de resposta são pontos finais para onde o Azure AD B2C devolve quaisquer tokens que a aplicação solicite. Introduza [um](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-web-app-or-api-reply-url) **URL de resposta** adequado. Neste exemplo, a aplicação é local e está a escutar na porta 44316. |

Clique em **criar** tooregister a aplicação.

A aplicação recentemente registada é apresentada na lista de aplicações de Olá para o inquilino do B2C Olá. Selecione a aplicação web Olá lista. é apresentado o painel de propriedades da aplicação web Olá.

![Propriedades da aplicação Web](./media/active-directory-b2c-register-web-app/b2c-web-app-properties.png)

Tome nota dos Olá globalmente exclusivo **ID de cliente da aplicação**. Utilize o ID de Olá no código da aplicação.
