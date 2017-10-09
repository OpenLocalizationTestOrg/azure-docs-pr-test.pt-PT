<span data-ttu-id="3dd42-101">perfil de tooenable edição na sua aplicação, terá de toocreate um perfil de política de edição.</span><span class="sxs-lookup"><span data-stu-id="3dd42-101">tooenable profile editing on your application, you will need toocreate a profile editing policy.</span></span> <span data-ttu-id="3dd42-102">Esta política descreve as experiências de Olá consumidores passarão durante perfil editar e Olá conteúdo tokens que receberão uma aplicação Olá após a conclusão com êxito.</span><span class="sxs-lookup"><span data-stu-id="3dd42-102">This policy describes hello experiences that consumers will go through during profile editing and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="3dd42-103">Na secção de políticas de Olá das definições, selecione **perfil editar políticas** e clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3dd42-103">In hello policies section of settings, select **Profile editing policies** and click **+ Add**.</span></span>

![Selecione o perfil editar políticas e clique no botão Adicionar de Olá](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

<span data-ttu-id="3dd42-105">Introduza uma política **nome** para sua tooreference de aplicação.</span><span class="sxs-lookup"><span data-stu-id="3dd42-105">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="3dd42-106">Por exemplo, introduza `SiPe`.</span><span class="sxs-lookup"><span data-stu-id="3dd42-106">For example, enter `SiPe`.</span></span>

<span data-ttu-id="3dd42-107">Selecione **Fornecedores de identidade** e selecione **Início de Sessão da Conta Local**.</span><span class="sxs-lookup"><span data-stu-id="3dd42-107">Select **Identity providers** and check **Local Account Signin**.</span></span> <span data-ttu-id="3dd42-108">Opcionalmente, também pode selecionar fornecedores de identidade social, se já estiverem configurados.</span><span class="sxs-lookup"><span data-stu-id="3dd42-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="3dd42-109">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3dd42-109">Click **OK**.</span></span>

![Selecione o início de sessão de conta Local como um fornecedor de identidade e clique no botão de Olá OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

<span data-ttu-id="3dd42-111">Selecione **Atributos do perfil**.</span><span class="sxs-lookup"><span data-stu-id="3dd42-111">Select **Profile attributes**.</span></span> <span data-ttu-id="3dd42-112">Escolha os consumidores de Olá atributos podem ver e editar no respetivo perfil.</span><span class="sxs-lookup"><span data-stu-id="3dd42-112">Choose attributes hello consumer can view and edit in their profile.</span></span> <span data-ttu-id="3dd42-113">Por exemplo, selecione **País/Região**, **Nome a Apresentar**, e **Código Postal**.</span><span class="sxs-lookup"><span data-stu-id="3dd42-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="3dd42-114">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3dd42-114">Click **OK**.</span></span>

![Selecione a alguns atributos e clique no botão de Olá OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

<span data-ttu-id="3dd42-116">Selecione **Afirmações de aplicação**.</span><span class="sxs-lookup"><span data-stu-id="3dd42-116">Select **Application claims**.</span></span> <span data-ttu-id="3dd42-117">Escolha afirmações que pretende devolvido em tokens de autorização de Olá enviadas a aplicação de back-tooyour depois de uma experiência de edição de perfis com êxito.</span><span class="sxs-lookup"><span data-stu-id="3dd42-117">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful profile editing experience.</span></span> <span data-ttu-id="3dd42-118">Por exemplo, selecione **Nome a Apresentar**, **Código Postal**.</span><span class="sxs-lookup"><span data-stu-id="3dd42-118">For example, select **Display Name**, **Postal Code**.</span></span>

![Selecione algumas afirmações de aplicação e clique no botão OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

<span data-ttu-id="3dd42-120">Clique em **criar** política de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="3dd42-120">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="3dd42-121">política de Olá está listada como **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="3dd42-121">hello policy is listed as **B2C_1_SiPe**.</span></span> <span data-ttu-id="3dd42-122">Olá **B2C_1_** prefixo é o nome de toohello anexado.</span><span class="sxs-lookup"><span data-stu-id="3dd42-122">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="3dd42-123">Abrir a política de Olá selecionando **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="3dd42-123">Open hello policy by selecting **B2C_1_SiPe**.</span></span> <span data-ttu-id="3dd42-124">Verifique as definições de Olá especificadas na tabela de Olá, em seguida, clique em **executar agora**.</span><span class="sxs-lookup"><span data-stu-id="3dd42-124">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Selecione a política e execute-a](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| <span data-ttu-id="3dd42-126">Definição</span><span class="sxs-lookup"><span data-stu-id="3dd42-126">Setting</span></span>      | <span data-ttu-id="3dd42-127">Valor</span><span class="sxs-lookup"><span data-stu-id="3dd42-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="3dd42-128">**Aplicações**</span><span class="sxs-lookup"><span data-stu-id="3dd42-128">**Applications**</span></span> | <span data-ttu-id="3dd42-129">Aplicação Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="3dd42-129">Contoso B2C app</span></span> |
| <span data-ttu-id="3dd42-130">**Selecionar o URL de resposta**</span><span class="sxs-lookup"><span data-stu-id="3dd42-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="3dd42-131">É aberto um novo separador do browser e pode verificar perfil Olá experiência de consumidor de edição, tal como foi configurada.</span><span class="sxs-lookup"><span data-stu-id="3dd42-131">A new browser tab opens, and you can verify hello profile editing consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="3dd42-132">Este ocupa tooa minuto para a criação de política e atualiza tootake efeito.</span><span class="sxs-lookup"><span data-stu-id="3dd42-132">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>