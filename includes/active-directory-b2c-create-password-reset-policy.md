tooenable palavras-passe detalhadas repor na sua aplicação, terá de toocreate uma política de reposição de palavra-passe. Tenha em atenção essa palavra-passe de todo o inquilino de Olá repor opção especificada [aqui](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md). Esta política descreve experiências Olá consumidores Olá passarão durante a reposição de palavra-passe e receberão conteúdos Olá dos tokens Olá aplicação após a conclusão com êxito.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Na secção de políticas de Olá das definições, selecione **políticas de reposição de palavra-passe** e clique em **+ adicionar**.

![Selecione as políticas de inscrição ou início de sessão e clique no botão Adicionar de Olá](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

Introduza uma política **nome** para sua tooreference de aplicação. Por exemplo, introduza `SSPR`.

Selecione **Fornecedores de identidade** e **Repor a palavra-passe com o endereço de e-mail**. Clique em **OK**.

![Selecione a repor a palavra-passe utilizando o endereço de e-mail como um fornecedor de identidade e clique no botão de Olá OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

Selecione **Afirmações de aplicação**. Escolha afirmações que pretende devolvido em tokens de autorização de Olá enviadas aplicação de back-tooyour depois de reposição de uma palavra-passe com êxito. Por exemplo, selecione **ID de Objeto do Utilizador**.

![Selecione algumas afirmações de aplicação e clique no botão OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

Clique em **criar** política de Olá tooadd. política de Olá está listada como **B2C_1_SSPR**. Olá **B2C_1_** prefixo é o nome de toohello anexado.

Abrir a política de Olá selecionando **B2C_1_SSPR**. Verifique as definições de Olá especificadas na tabela de Olá, em seguida, clique em **executar agora**.

![Selecione a política e execute-a](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| Definição      | Valor  |
| ------------ | ------ |
| **Aplicações** | Aplicação Contoso B2C |
| **Selecionar o URL de resposta** | `https://localhost:44316/` |

É aberto um novo separador do browser e verificar a experiência de consumidor na sua aplicação de reposição de palavra-passe de Olá.

> [!NOTE]
> Este ocupa tooa minuto para a criação de política e atualiza tootake efeito.
>
