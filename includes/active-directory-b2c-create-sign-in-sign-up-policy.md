tooenable início de sessão na sua aplicação, terá de política de toocreate um início de sessão. Esta política descreve experiências Olá consumidores passarão durante o início de sessão e receberão conteúdos Olá dos tokens Olá aplicação nos inícios de sessão com êxito.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Na secção de políticas de Olá das definições, selecione **políticas de inscrição ou início de sessão** e clique em **+ adicionar**.

![Selecione as políticas de inscrição ou início de sessão e clique no botão Adicionar](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

Introduza uma política **nome** para sua tooreference de aplicação. Por exemplo, introduza `SiUpIn`.

Selecione **Fornecedores de identidade** e selecione **Inscrição de e-mail**. Opcionalmente, também pode selecionar fornecedores de identidade social, se já estiverem configurados. Clique em **OK**.

![Selecione a inscrição de E-Mail como um fornecedor de identidade e clique no botão de Olá OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

Selecione **Atributos de inscrição**. Escolha atributos pretende toocollect do consumidor Olá durante a inscrição. Por exemplo, selecione **País/Região**, **Nome a Apresentar**, e **Código Postal**. Clique em **OK**.

![Selecione a alguns atributos e clique no botão de Olá OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

Selecione **Afirmações de aplicação**. Escolha afirmações que pretende devolvido em tokens de autorização de Olá enviadas a aplicação de back-tooyour depois de uma experiência de se inscrever ou iniciar sessão com êxito. Por exemplo, selecione **Nome a Apresentar**, **Fornecedor de Identidade**, **Código Postal**, **O utilizador é novo** e **ID de Objeto do Utilizador**.

![Selecione algumas afirmações de aplicação e clique no botão OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

Clique em **criar** política de Olá tooadd. política de Olá está listada como **B2C_1_SiUpIn**. Olá **B2C_1_** prefixo é o nome de toohello anexado.

Abrir a política de Olá selecionando **B2C_1_SiUpIn**. Verifique as definições de Olá especificadas na tabela de Olá, em seguida, clique em **executar agora**.

![Selecione a política e execute-a](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| Definição      | Valor  |
| ------------ | ------ |
| **Aplicações** | Aplicação Contoso B2C |
| **Selecionar o URL de resposta** | `https://localhost:44316/` |

É aberto um novo separador do browser e pode verificar a experiência de inscrição ou início de sessão consumidor Olá conforme configuradas.

> [!NOTE]
> Este ocupa tooa minuto para a criação de política e atualiza tootake efeito.
>