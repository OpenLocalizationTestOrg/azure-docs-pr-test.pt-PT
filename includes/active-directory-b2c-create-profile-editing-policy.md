perfil de tooenable edição na sua aplicação, terá de toocreate um perfil de política de edição. Esta política descreve as experiências de Olá consumidores passarão durante perfil editar e Olá conteúdo tokens que receberão uma aplicação Olá após a conclusão com êxito.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Na secção de políticas de Olá das definições, selecione **perfil editar políticas** e clique em **+ adicionar**.

![Selecione o perfil editar políticas e clique no botão Adicionar de Olá](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

Introduza uma política **nome** para sua tooreference de aplicação. Por exemplo, introduza `SiPe`.

Selecione **Fornecedores de identidade** e selecione **Início de Sessão da Conta Local**. Opcionalmente, também pode selecionar fornecedores de identidade social, se já estiverem configurados. Clique em **OK**.

![Selecione o início de sessão de conta Local como um fornecedor de identidade e clique no botão de Olá OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

Selecione **Atributos do perfil**. Escolha os consumidores de Olá atributos podem ver e editar no respetivo perfil. Por exemplo, selecione **País/Região**, **Nome a Apresentar**, e **Código Postal**. Clique em **OK**.

![Selecione a alguns atributos e clique no botão de Olá OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

Selecione **Afirmações de aplicação**. Escolha afirmações que pretende devolvido em tokens de autorização de Olá enviadas a aplicação de back-tooyour depois de uma experiência de edição de perfis com êxito. Por exemplo, selecione **Nome a Apresentar**, **Código Postal**.

![Selecione algumas afirmações de aplicação e clique no botão OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

Clique em **criar** política de Olá tooadd. política de Olá está listada como **B2C_1_SiPe**. Olá **B2C_1_** prefixo é o nome de toohello anexado.

Abrir a política de Olá selecionando **B2C_1_SiPe**. Verifique as definições de Olá especificadas na tabela de Olá, em seguida, clique em **executar agora**.

![Selecione a política e execute-a](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| Definição      | Valor  |
| ------------ | ------ |
| **Aplicações** | Aplicação Contoso B2C |
| **Selecionar o URL de resposta** | `https://localhost:44316/` |

É aberto um novo separador do browser e pode verificar perfil Olá experiência de consumidor de edição, tal como foi configurada.

> [!NOTE]
> Este ocupa tooa minuto para a criação de política e atualiza tootake efeito.
>