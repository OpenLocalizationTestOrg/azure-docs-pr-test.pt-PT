tooenable início de sessão na sua aplicação, terá de política de toocreate um início de sessão. Esta política descreve experiências Olá consumidores passarão durante o início de sessão e receberão conteúdos Olá dos tokens Olá aplicação nos inícios de sessão com êxito.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)] Clique em **Políticas de início de sessão**.

Clique em **+ adicionar** , Olá parte superior do painel de Olá.

Olá **nome** determina o nome de política de início de sessão de Olá utilizado pela sua aplicação. Por exemplo, introduza **SiIn**.

Clique em **Fornecedores de identidade** e selecione **Início de Sessão da Conta Local**. Opcionalmente, também pode selecionar fornecedores de identidade social, se já estiverem configurados. Clique em **OK**.

Clique em **Afirmações de aplicação**. Aqui pode escolher as afirmações que pretende que sejam devolvidos em tokens de Olá enviados aplicação de back-tooyour depois de uma experiência de início de sessão com êxito. Por exemplo, selecione **Nome a Apresentar**, **Fornecedor de Identidade**, **Código Postal** e **ID de Objeto do Utilizador**. Clique em **OK**.

Clique em **Criar**. Tenha em atenção que a política de Olá acabou de criar é apresentada como **B2C_1_SiIn** (Olá **B2C\_1\_**  fragmento é automaticamente adicionado) no Olá **início de sessão políticas**painel.

Abrir a política de Olá clicando **B2C_1_SiIn**.

Selecione **Contoso B2C app** no Olá **aplicações** pendente e `https://localhost:44321/` no Olá **resposta URL / URI de redirecionamento** pendente.

Clique em **Executar agora**. É aberto um novo separador do browser e o utilizador pode executar através de experiência de consumidor Olá do início de sessão na sua aplicação.

> [!NOTE]
> Este ocupa tooa minuto para a criação de política e atualiza tootake efeito.
>