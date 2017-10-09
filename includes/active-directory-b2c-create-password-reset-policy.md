<span data-ttu-id="42311-101">tooenable palavras-passe detalhadas repor na sua aplicação, terá de toocreate uma política de reposição de palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="42311-101">tooenable fine-grained password reset on your application, you will need toocreate a password reset policy.</span></span> <span data-ttu-id="42311-102">Tenha em atenção essa palavra-passe de todo o inquilino de Olá repor opção especificada [aqui](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span><span class="sxs-lookup"><span data-stu-id="42311-102">Note that hello tenant-wide password reset option specified [here](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span></span> <span data-ttu-id="42311-103">Esta política descreve experiências Olá consumidores Olá passarão durante a reposição de palavra-passe e receberão conteúdos Olá dos tokens Olá aplicação após a conclusão com êxito.</span><span class="sxs-lookup"><span data-stu-id="42311-103">This policy describes hello experiences that hello consumers will go through during password reset and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="42311-104">Na secção de políticas de Olá das definições, selecione **políticas de reposição de palavra-passe** e clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="42311-104">In hello policies section of settings, select **Password reset policies** and click **+ Add**.</span></span>

![Selecione as políticas de inscrição ou início de sessão e clique no botão Adicionar de Olá](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

<span data-ttu-id="42311-106">Introduza uma política **nome** para sua tooreference de aplicação.</span><span class="sxs-lookup"><span data-stu-id="42311-106">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="42311-107">Por exemplo, introduza `SSPR`.</span><span class="sxs-lookup"><span data-stu-id="42311-107">For example, enter `SSPR`.</span></span>

<span data-ttu-id="42311-108">Selecione **Fornecedores de identidade** e **Repor a palavra-passe com o endereço de e-mail**.</span><span class="sxs-lookup"><span data-stu-id="42311-108">Select **Identity providers** and check **Reset password using email address**.</span></span> <span data-ttu-id="42311-109">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="42311-109">Click **OK**.</span></span>

![Selecione a repor a palavra-passe utilizando o endereço de e-mail como um fornecedor de identidade e clique no botão de Olá OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

<span data-ttu-id="42311-111">Selecione **Afirmações de aplicação**.</span><span class="sxs-lookup"><span data-stu-id="42311-111">Select **Application claims**.</span></span> <span data-ttu-id="42311-112">Escolha afirmações que pretende devolvido em tokens de autorização de Olá enviadas aplicação de back-tooyour depois de reposição de uma palavra-passe com êxito.</span><span class="sxs-lookup"><span data-stu-id="42311-112">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful password reset experience.</span></span> <span data-ttu-id="42311-113">Por exemplo, selecione **ID de Objeto do Utilizador**.</span><span class="sxs-lookup"><span data-stu-id="42311-113">For example, select **User's Object ID**.</span></span>

![Selecione algumas afirmações de aplicação e clique no botão OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

<span data-ttu-id="42311-115">Clique em **criar** política de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="42311-115">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="42311-116">política de Olá está listada como **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="42311-116">hello policy is listed as **B2C_1_SSPR**.</span></span> <span data-ttu-id="42311-117">Olá **B2C_1_** prefixo é o nome de toohello anexado.</span><span class="sxs-lookup"><span data-stu-id="42311-117">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="42311-118">Abrir a política de Olá selecionando **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="42311-118">Open hello policy by selecting **B2C_1_SSPR**.</span></span> <span data-ttu-id="42311-119">Verifique as definições de Olá especificadas na tabela de Olá, em seguida, clique em **executar agora**.</span><span class="sxs-lookup"><span data-stu-id="42311-119">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Selecione a política e execute-a](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| <span data-ttu-id="42311-121">Definição</span><span class="sxs-lookup"><span data-stu-id="42311-121">Setting</span></span>      | <span data-ttu-id="42311-122">Valor</span><span class="sxs-lookup"><span data-stu-id="42311-122">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="42311-123">**Aplicações**</span><span class="sxs-lookup"><span data-stu-id="42311-123">**Applications**</span></span> | <span data-ttu-id="42311-124">Aplicação Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="42311-124">Contoso B2C app</span></span> |
| <span data-ttu-id="42311-125">**Selecionar o URL de resposta**</span><span class="sxs-lookup"><span data-stu-id="42311-125">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="42311-126">É aberto um novo separador do browser e verificar a experiência de consumidor na sua aplicação de reposição de palavra-passe de Olá.</span><span class="sxs-lookup"><span data-stu-id="42311-126">A new browser tab opens, and you can verify hello password reset consumer experience in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="42311-127">Este ocupa tooa minuto para a criação de política e atualiza tootake efeito.</span><span class="sxs-lookup"><span data-stu-id="42311-127">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>
