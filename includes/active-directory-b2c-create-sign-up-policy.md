tooenable inscrição na sua aplicação, terá de toocreate uma política de inscrição. Esta política descreve as experiências de Olá que os consumidores percorrer durante a inscrição e recebe conteúdo Olá tokens Olá aplicação nos ups de início de sessão com êxito.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Clique em **Políticas de inscrição**.

Clique em **+ adicionar** , Olá parte superior do painel de Olá.

Olá **nome** determina o nome da política de inscrição de Olá utilizado pela sua aplicação. Por exemplo, introduza **SiUp**.

Clique em **Fornecedores de identidade** e selecione **Inscrição de e-mail**. Opcionalmente, também pode selecionar fornecedores de identidade social, se já estiverem configurados. Clique em **OK**.

Clique em **Atributos de inscrição**. Aqui, escolher os atributos que pretende que toocollect do consumidor Olá durante a inscrição. Por exemplo, selecione **País/Região**, **Nome a Apresentar**, e **Código Postal**. Clique em **OK**.

Clique em **Afirmações de aplicação**. Aqui pode escolher as afirmações que pretende que sejam devolvidos em tokens de Olá enviados aplicação de back-tooyour depois de uma experiência de inscrição com êxito. Por exemplo, selecione **Nome a Apresentar**, **Fornecedor de Identidade**, **Código Postal**, **O utilizador é novo** e **ID de Objeto do Utilizador**.

Clique em **Criar**. política de Olá criada aparece como **B2C_1_SiUp** (Olá **B2C\_1\_**  fragmento é automaticamente adicionado) no Olá **políticas de inscrição** painel.

Abrir a política de Olá clicando **B2C_1_SiUp**.

Selecione **Contoso B2C app** no Olá **aplicações** pendente e `https://localhost:44321/` no Olá **resposta URL / URI de redirecionamento** pendente.

Clique em **Executar agora**. Abre-se de um novo separador do browser e o utilizador pode executar através de experiência de consumidor Olá de inscrever-se para a sua aplicação.

> [!NOTE]
> Este ocupa tooa minuto para a criação de política e atualiza tootake efeito.
>