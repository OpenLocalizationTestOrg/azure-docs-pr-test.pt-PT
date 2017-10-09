<span data-ttu-id="fd4ae-101">tooenable início de sessão na sua aplicação, terá de política de toocreate um início de sessão.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-101">tooenable sign-in on your application, you will need toocreate a sign-in policy.</span></span> <span data-ttu-id="fd4ae-102">Esta política descreve experiências Olá consumidores passarão durante o início de sessão e receberão conteúdos Olá dos tokens Olá aplicação nos inícios de sessão com êxito.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-102">This policy describes hello experiences that consumers will go through during sign-in and hello contents of tokens that hello application will receive on successful sign-ins.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="fd4ae-103">Na secção de políticas de Olá das definições, selecione **políticas de inscrição ou início de sessão** e clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-103">In hello policies section of settings, select **Sign-up or sign-in policies** and click **+ Add**.</span></span>

![Selecione as políticas de inscrição ou início de sessão e clique no botão Adicionar](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

<span data-ttu-id="fd4ae-105">Introduza uma política **nome** para sua tooreference de aplicação.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-105">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="fd4ae-106">Por exemplo, introduza `SiUpIn`.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-106">For example, enter `SiUpIn`.</span></span>

<span data-ttu-id="fd4ae-107">Selecione **Fornecedores de identidade** e selecione **Inscrição de e-mail**.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-107">Select **Identity providers** and check **Email signup**.</span></span> <span data-ttu-id="fd4ae-108">Opcionalmente, também pode selecionar fornecedores de identidade social, se já estiverem configurados.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="fd4ae-109">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-109">Click **OK**.</span></span>

![Selecione a inscrição de E-Mail como um fornecedor de identidade e clique no botão de Olá OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

<span data-ttu-id="fd4ae-111">Selecione **Atributos de inscrição**.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-111">Select **Sign-up attributes**.</span></span> <span data-ttu-id="fd4ae-112">Escolha atributos pretende toocollect do consumidor Olá durante a inscrição.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-112">Choose attributes you want toocollect from hello consumer during sign-up.</span></span> <span data-ttu-id="fd4ae-113">Por exemplo, selecione **País/Região**, **Nome a Apresentar**, e **Código Postal**.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="fd4ae-114">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-114">Click **OK**.</span></span>

![Selecione a alguns atributos e clique no botão de Olá OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

<span data-ttu-id="fd4ae-116">Selecione **Afirmações de aplicação**.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-116">Select **Application claims**.</span></span> <span data-ttu-id="fd4ae-117">Escolha afirmações que pretende devolvido em tokens de autorização de Olá enviadas a aplicação de back-tooyour depois de uma experiência de se inscrever ou iniciar sessão com êxito.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-117">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful sign-up or sign-in experience.</span></span> <span data-ttu-id="fd4ae-118">Por exemplo, selecione **Nome a Apresentar**, **Fornecedor de Identidade**, **Código Postal**, **O utilizador é novo** e **ID de Objeto do Utilizador**.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-118">For example, select **Display Name**, **Identity Provider**, **Postal Code**, **User is new** and **User's Object ID**.</span></span>

![Selecione algumas afirmações de aplicação e clique no botão OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

<span data-ttu-id="fd4ae-120">Clique em **criar** política de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-120">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="fd4ae-121">política de Olá está listada como **B2C_1_SiUpIn**.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-121">hello policy is listed as **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="fd4ae-122">Olá **B2C_1_** prefixo é o nome de toohello anexado.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-122">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="fd4ae-123">Abrir a política de Olá selecionando **B2C_1_SiUpIn**.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-123">Open hello policy by selecting **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="fd4ae-124">Verifique as definições de Olá especificadas na tabela de Olá, em seguida, clique em **executar agora**.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-124">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Selecione a política e execute-a](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| <span data-ttu-id="fd4ae-126">Definição</span><span class="sxs-lookup"><span data-stu-id="fd4ae-126">Setting</span></span>      | <span data-ttu-id="fd4ae-127">Valor</span><span class="sxs-lookup"><span data-stu-id="fd4ae-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="fd4ae-128">**Aplicações**</span><span class="sxs-lookup"><span data-stu-id="fd4ae-128">**Applications**</span></span> | <span data-ttu-id="fd4ae-129">Aplicação Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="fd4ae-129">Contoso B2C app</span></span> |
| <span data-ttu-id="fd4ae-130">**Selecionar o URL de resposta**</span><span class="sxs-lookup"><span data-stu-id="fd4ae-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="fd4ae-131">É aberto um novo separador do browser e pode verificar a experiência de inscrição ou início de sessão consumidor Olá conforme configuradas.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-131">A new browser tab opens, and you can verify hello sign-up or sign-in consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="fd4ae-132">Este ocupa tooa minuto para a criação de política e atualiza tootake efeito.</span><span class="sxs-lookup"><span data-stu-id="fd4ae-132">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>