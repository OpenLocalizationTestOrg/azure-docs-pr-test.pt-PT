[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister a aplicação móvel ou nativa, utilizar definições de Olá especificadas na tabela de Olá.

![Definições de registo de exemplo para a nova aplicação móvel ou nativa](./media/active-directory-b2c-register-mobile-native-app/b2c-new-mobile-native-app-settings.png)

| Definição      | Valor da amostra  | Descrição                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Nome** | Aplicação Contoso B2C | Introduza um **nome** para aplicação Olá que descreve o tooconsumers de aplicação. |
| **Cliente nativo** | Sim | Selecione **Sim** para uma aplicação móvel ou nativa. |
| **URI de Redirecionamento Personalizado** | `com.onmicrosoft.contoso.appname://redirect/path` | Introduza um URI de redirecionamento com um esquema personalizado. Certifique-se de que escolhe um [bom URI de redirecionamento](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-native-application-redirect-uri) e não inclui caracteres especiais, como carateres de sublinhado. |

Clique em **criar** tooregister a aplicação.

A aplicação recentemente registada é apresentada na lista de aplicações de Olá para o inquilino do B2C Olá. Selecione a aplicação móvel ou nativa Olá lista. é apresentado o painel de propriedades da aplicação Olá.

![Propriedades da aplicação](./media/active-directory-b2c-register-mobile-native-app/b2c-mobile-native-app-properties.png)

Tome nota dos Olá globalmente exclusivo **ID de cliente da aplicação**. Utilize o ID de Olá no código da aplicação.

Se a sua aplicação nativa chamar uma API Web protegida pelo Azure AD B2C, efetue estes passos:
   1. Criar um segredo da aplicação por vai toohello **chaves** painel e clicar em Olá **gerar chave** botão. Tome nota dos Olá **chave da aplicação** valor. Utilize o valor de Olá como segredo da aplicação Olá no código da aplicação.
   2. Clique em **Acesso à API**, clique em **Adicionar** e selecione a API Web e os âmbitos (permissões).

> [!NOTE]
> Um **Segredo de Aplicação** é uma credencial de segurança importante e deve ser protegida devidamente.
> 
