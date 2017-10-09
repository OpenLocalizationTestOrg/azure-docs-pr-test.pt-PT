---
title: os dados pessoais aaaProtect com controlos de identidades e acessos do Azure | Microsoft Docs
description: Utilizar toohelp de controlos de identidades e acessos do Azure pode protege os seus dados pessoais
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a><span data-ttu-id="ed8b2-103">Azure Active Directory e o multi-factor Authentication: proteger os dados pessoais com controlos de identidades e acessos</span><span class="sxs-lookup"><span data-stu-id="ed8b2-103">Azure Active Directory and Multi-Factor Authentication: Protect personal data with identity and access controls</span></span>

<span data-ttu-id="ed8b2-104">Este artigo fornece informações e procedimentos que pode utilizar os dados pessoais tooprotect utilizar os serviços e funcionalidades de segurança do Azure Active Directory e o multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-104">This article provides information and procedures you can use tooprotect personal data using Azure Active Directory and Multi-factor authentication security features and services.</span></span>

## <a name="scenario"></a><span data-ttu-id="ed8b2-105">Cenário</span><span class="sxs-lookup"><span data-stu-id="ed8b2-105">Scenario</span></span>

<span data-ttu-id="ed8b2-106">Uma empresa de grande cruise headquartered no Olá dos Estados Unidos, está a expandir as respetivas itineraries de toooffer operações no Mediterranean Olá, Adriatic e Baltic seas, bem como Olá território Isles.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="ed8b2-107">toosupport os esforços obteve várias linhas cruise mais pequenas com base em (Itália), na Alemanha, Dinamarca e Olá U.K.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-107">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="ed8b2-108">empresa Olá utiliza os dados empresariais do Microsoft Azure toostore na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="ed8b2-109">Isto inclui informações pessoais tais como nomes, endereços, números de telefone e informações de cartão de crédito da respetiva base de cliente global.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="ed8b2-110">Também inclui informações de recursos humanos tradicionais, como endereços, números de telefone, os números de identificação de dedução dos impostos e médicas informações sobre os funcionários da empresa em todas as localizações.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-110">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="ed8b2-111">linha de cruise Olá mantém também uma grande base de dados de membros de programa reward e loyalty que inclui as relações de tootrack informações pessoais com clientes atuais e anteriores.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-111">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="ed8b2-112">Empresariais aos funcionários acesso Olá rede de armazenamento da empresa Olá escritórios remotos e agentes levar localizados em torno Olá mundo ter toosome aceder a recursos empresariais.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-112">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="ed8b2-113">Declaração do problema</span><span class="sxs-lookup"><span data-stu-id="ed8b2-113">Problem statement</span></span>

<span data-ttu-id="ed8b2-114">empresa Olá deve proteger a privacidade de Olá dos dados pessoais dos clientes e dos empregados de atacantes pesquisa toouse comprometido identidades toogain acesso.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-114">hello company must protect hello privacy of customers’ and employees’ personal data from attackers seeking toouse compromised identities toogain access.</span></span> <span data-ttu-id="ed8b2-115">Eles também tem de garantir que toopersonal de acesso a dados por utilizadores legítimos estão restringidos apenas a quem será necessário toodo as respetivas tarefas.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-115">They also must ensure that access toopersonal data by legitimate users is restricted to only those who need it toodo their jobs.</span></span>

## <a name="company-goal"></a><span data-ttu-id="ed8b2-116">Objetivo da empresa</span><span class="sxs-lookup"><span data-stu-id="ed8b2-116">Company goal</span></span>

<span data-ttu-id="ed8b2-117">Objetivo da empresa Olá é tooensure aceder a dados toopersonal é estritamente controlada.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-117">hello company’s goal is tooensure that access toopersonal data is strictly controlled.</span></span> <span data-ttu-id="ed8b2-118">É essencial que as identidades dos utilizadores com aceder a dados toopersonal estar protegido por autenticação forte.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-118">It is essential that identities of users with access toopersonal data be protected by strong authentication.</span></span> <span data-ttu-id="ed8b2-119">Uma política do [menor privilégio] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) tem de ser imposta para que os utilizadores legítimos tem apenas Olá nível de acesso que precisam e não existem mais.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-119">A policy of [least privilege] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) must be enforced so that legitimate users have only hello level of  access they need, and no more.</span></span>

## <a name="solutions"></a><span data-ttu-id="ed8b2-120">Soluções</span><span class="sxs-lookup"><span data-stu-id="ed8b2-120">Solutions</span></span>

<span data-ttu-id="ed8b2-121">Microsoft Azure fornece ferramentas de gestão de identidades e acesso de controlo de empresas de toohelp quem tem acesso tooresources que contêm dados pessoais.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-121">Microsoft Azure provides identity and access management tools toohelp companies control who has access tooresources that contain personal data.</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="ed8b2-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed8b2-122">Azure Active Directory</span></span>

<span data-ttu-id="ed8b2-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) gere as identidades e controla o acesso tooAzure, bem como outro no local e outros recursos na nuvem, dados e aplicações.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) manages identities and controls access tooAzure as well as other on-premises and other cloud resources, data, and applications.</span></span> <span data-ttu-id="ed8b2-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) ajuda os administradores do Azure toominimize Olá diversas pessoas que têm acesso toocertain informações tais como os dados pessoais.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) helps Azure administrators toominimize hello number of people who have access toocertain information such as personal data.</span></span> <span data-ttu-id="ed8b2-125">Permite-lhes toodiscover, restringir e monitorizar as identidades privilegiadas e o respetivos acesso tooresources tooassign temporário, just (JIT) direitos administrativos tooeligible utilizadores e.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-125">It enables them toodiscover, restrict, and monitor privileged identities and their access tooresources, and tooassign temporary, Just-In-Time (JIT) administrative rights tooeligible users.</span></span> <span data-ttu-id="ed8b2-126">Também fornece informações sobre os utilizadores que possuem os privilégios administrativos AAD.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-126">It also provides insight into those who have AAD administrative privileges.</span></span>

<span data-ttu-id="ed8b2-127">as atividades de Olá envolvidas na utilizando AAD PIM incluem:</span><span class="sxs-lookup"><span data-stu-id="ed8b2-127">hello activities involved in using AAD PIM include:</span></span>

- <span data-ttu-id="ed8b2-128">Ativar o Privileged Identity Management para o seu diretório</span><span class="sxs-lookup"><span data-stu-id="ed8b2-128">Enabling Privileged Identity Management for your directory</span></span>

- <span data-ttu-id="ed8b2-129">Utilizando informações importantes de Privileged Identity Management admin dashboard toosee num instante</span><span class="sxs-lookup"><span data-stu-id="ed8b2-129">Using Privileged Identity Management admin dashboard toosee important information at a glance</span></span>

- <span data-ttu-id="ed8b2-130">Gestão de identidades Olá privilegiado (administradores) através da adição ou remoção de função de tooeach administradores permanentes ou elegíveis</span><span class="sxs-lookup"><span data-stu-id="ed8b2-130">Managing hello privileged identities (administrators) by adding or removing permanent or eligible administrators tooeach role</span></span>

- <span data-ttu-id="ed8b2-131">Configurar definições de ativação de função Olá</span><span class="sxs-lookup"><span data-stu-id="ed8b2-131">Configuring hello role activation settings</span></span>

- <span data-ttu-id="ed8b2-132">Ativar funções</span><span class="sxs-lookup"><span data-stu-id="ed8b2-132">Activating roles</span></span>

- <span data-ttu-id="ed8b2-133">Rever a actividade de função</span><span class="sxs-lookup"><span data-stu-id="ed8b2-133">Reviewing role activity</span></span>

#### <a name="how-do-i-enable-aad-pim"></a><span data-ttu-id="ed8b2-134">Como ativar a PIM do AAD?</span><span class="sxs-lookup"><span data-stu-id="ed8b2-134">How do I enable AAD PIM?</span></span>

<span data-ttu-id="ed8b2-135">toostart PIM a utilizar para o seu diretório, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed8b2-135">toostart using PIM for your directory, do hello following:</span></span>

1. <span data-ttu-id="ed8b2-136">Inicie sessão no toohello portal do Azure como um administrador global do seu diretório.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-136">Sign in toohello Azure portal as a global administrator of your directory.</span></span>

2. <span data-ttu-id="ed8b2-137">Se a sua organização tiver mais do que um diretório, selecione o seu nome de utilizador no canto direito superior Olá de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-137">If your organization has more than one directory, select your username in hello upper right-hand corner of hello Azure portal.</span></span> <span data-ttu-id="ed8b2-138">Selecione o diretório de olá onde utilizará o Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-138">Select hello directory where you will use Azure AD Privileged Identity Management.</span></span>

3. <span data-ttu-id="ed8b2-139">Selecione **mais serviços** e utilizar Olá **filtro** toosearch de caixa de texto para o Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-139">Select **More services** and use hello **Filter** textbox toosearch for Azure AD Privileged Identity Management.</span></span>

4. <span data-ttu-id="ed8b2-140">Verifique **Pin toodashboard** e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-140">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="ed8b2-141">é aberto o Olá aplicação Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-141">hello Privileged Identity Management application opens.</span></span>

<span data-ttu-id="ed8b2-142">Depois de configurada do Azure AD Privileged Identity Management, consulte painel de navegação de Olá sempre que abrir a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-142">Once Azure AD Privileged Identity Management is set up, you see hello navigation blade whenever you open hello application.</span></span>

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

<span data-ttu-id="ed8b2-143">Para obter mais informações e instruções sobre como começar a PIM do AAD, consulte [começar a utilizar o Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span><span class="sxs-lookup"><span data-stu-id="ed8b2-143">For more information and instructions on getting started with AAD PIM, see [Start Using Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span></span>

### <a name="azure-role-based-access-control"></a><span data-ttu-id="ed8b2-144">Controlo de acesso baseado em funções do Azure</span><span class="sxs-lookup"><span data-stu-id="ed8b2-144">Azure Role-based Access Control</span></span>

<span data-ttu-id="ed8b2-145">[Controlo de acesso baseado em funções do Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) ajuda os administradores do Azure gerir aceder a recursos tooAzure Ativando Olá concessão de permissões de acesso com base na função de utilizador Olá atribuído.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-145">[Azure Role-Based Access Control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) helps Azure administrators manage access tooAzure resources by enabling hello granting of access based on hello user’s assigned role.</span></span> <span data-ttu-id="ed8b2-146">Pode segregar funções dentro de uma equipa e conceder apenas Olá quantidade de acesso toousers, grupos e aplicações que precisam de tooperform as respetivas tarefas.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-146">You can segregate duties within a team and grant only hello amount of access toousers, groups and applications that they need tooperform their jobs.</span></span>

<span data-ttu-id="ed8b2-147">Acesso baseado em funções pode ser concedido toousers utilizando Olá portal do Azure, as ferramentas da linha de comandos do Azure ou APIs de gestão do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-147">Role-based access can be granted toousers using hello Azure portal, Azure Command-Line tools or Azure Management APIs.</span></span>

<span data-ttu-id="ed8b2-148">Para mais informações sobre noções básicas do RBAC do Azure, consulte [introdução ao controlo de acesso baseado em funções na Olá Portal do Azure.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span><span class="sxs-lookup"><span data-stu-id="ed8b2-148">For more information about Azure RBAC basics, see [Get started with Role-Based Access Control in hello Azure Portal.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span></span>

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a><span data-ttu-id="ed8b2-149">Como gerir o RBAC do Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed8b2-149">How do I manage Azure RBAC with PowerShell?</span></span>

<span data-ttu-id="ed8b2-150">Pode utilizar o PowerShell cmdlets toomanage RBAC do Azure, incluindo Olá seguintes tarefas de gestão:</span><span class="sxs-lookup"><span data-stu-id="ed8b2-150">You can use PowerShell cmdlets toomanage Azure RBAC, including hello following management tasks:</span></span>

- <span data-ttu-id="ed8b2-151">Lista de funções</span><span class="sxs-lookup"><span data-stu-id="ed8b2-151">List roles</span></span>

- <span data-ttu-id="ed8b2-152">Ver quem tem acesso</span><span class="sxs-lookup"><span data-stu-id="ed8b2-152">See who has access</span></span>

- <span data-ttu-id="ed8b2-153">Conceder acesso</span><span class="sxs-lookup"><span data-stu-id="ed8b2-153">Grant access</span></span>

- <span data-ttu-id="ed8b2-154">Remover o acesso</span><span class="sxs-lookup"><span data-stu-id="ed8b2-154">Remove access</span></span>

- <span data-ttu-id="ed8b2-155">Criar uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="ed8b2-155">Create a custom role</span></span>

- <span data-ttu-id="ed8b2-156">Obter as ações de um fornecedor de recursos</span><span class="sxs-lookup"><span data-stu-id="ed8b2-156">Get Actions for a Resource Provider</span></span>

- <span data-ttu-id="ed8b2-157">Modificar uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="ed8b2-157">Modify a custom role</span></span>

- <span data-ttu-id="ed8b2-158">Eliminar uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="ed8b2-158">Delete a custom role</span></span>

- <span data-ttu-id="ed8b2-159">Lista de funções personalizadas</span><span class="sxs-lookup"><span data-stu-id="ed8b2-159">List custom roles</span></span>

<span data-ttu-id="ed8b2-160">Para obter instruções sobre como toomanage RBAC do Azure com o PowerShell, consulte o artigo [baseada em funções gerir acesso com o Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span><span class="sxs-lookup"><span data-stu-id="ed8b2-160">For instructions on how toomanage Azure RBAC with PowerShell, see [Manage Role-based Access with Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span></span>

### <a name="azure-multi-factor-authentication"></a><span data-ttu-id="ed8b2-161">Multi-Factor Authentication do Azure</span><span class="sxs-lookup"><span data-stu-id="ed8b2-161">Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="ed8b2-162">[Multi-factor Authentication do Azure](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) é uma solução de verificação de dois passos que ajuda a salvaguardar acesso toodata e aplicações, cumprindo o pedido do utilizador para um processo de início de sessão simple.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-162">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) is a two-step verification solution that helps safeguard access toodata and applications, while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="ed8b2-163">Oferece autenticação forte através de vários métodos de verificação, incluindo chamada telefónica, mensagem de texto ou verificação de aplicação móvel.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-163">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

<span data-ttu-id="ed8b2-164">toodeploy MFA na Olá em nuvem do Azure, terá de toofirst ativá-la e, em seguida, ative a verificação em dois passos para os utilizadores.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-164">toodeploy MFA in hello Azure cloud, you need toofirst enable it and then turn on two-step verification for users.</span></span>

#### <a name="how-do-i-enable-azure-toouse-mfa"></a><span data-ttu-id="ed8b2-165">Como ativar a toouse do Azure MFA?</span><span class="sxs-lookup"><span data-stu-id="ed8b2-165">How do I enable Azure toouse MFA?</span></span>

<span data-ttu-id="ed8b2-166">Se os utilizadores têm de licenças que incluem o Azure multi-factor Authentication, não há nada que precisa de toodo tooturn na MFA do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-166">If your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="ed8b2-167">Caso contrário, terá de toocreate um fornecedor de multi-Factor Auth no seu diretório.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-167">If not, you need toocreate a Multi-Factor Auth provider in your directory.</span></span> <span data-ttu-id="ed8b2-168">toodo isto, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="ed8b2-168">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="ed8b2-169">Selecione **do Active Directory** no Olá portal clássico do Azure (com sessão iniciado como administrador).</span><span class="sxs-lookup"><span data-stu-id="ed8b2-169">Select **Active Directory** in hello Azure classic portal (logged on as an administrator).</span></span>

2. <span data-ttu-id="ed8b2-170">Selecione **fornecedores do multi-factor Authentication.**</span><span class="sxs-lookup"><span data-stu-id="ed8b2-170">Select **Multi-Factor Authentication Providers.**</span></span>

3. <span data-ttu-id="ed8b2-171">Selecione **novo,** e, em **serviços aplicacionais,** selecione **fornecedor do multi-factor Auth.**</span><span class="sxs-lookup"><span data-stu-id="ed8b2-171">Select **New,** and then under **App Services,** select **Multi-Factor Auth Provider.**</span></span>

4. <span data-ttu-id="ed8b2-172">Selecione **criação rápida.**</span><span class="sxs-lookup"><span data-stu-id="ed8b2-172">Select **Quick Create.**</span></span>

5. <span data-ttu-id="ed8b2-173">Preencha o campo de nome de Olá e selecione um modelo de utilização (por autenticação ou por utilizador ativado).</span><span class="sxs-lookup"><span data-stu-id="ed8b2-173">Fill in hello name field and select a usage model (per authentication or per enabled user).</span></span>

6. <span data-ttu-id="ed8b2-174">Designa um diretório com que Olá fornecedor de MFA está associado.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-174">Designate a directory with which hello MFA Provider is associated.</span></span>

7. <span data-ttu-id="ed8b2-175">Clique em Olá **criar** botão.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-175">Click hello **Create** button.</span></span>

![](media/protect-personal-data-identity-access-controls/quick-create.png)

<span data-ttu-id="ed8b2-176">Para obter mais instruções sobre como toomanage o fornecedor do multi-factor Auth, consulte [introdução de um fornecedor do multi-factor Auth do Azure.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span><span class="sxs-lookup"><span data-stu-id="ed8b2-176">For more instructions on how toomanage your Multi-Factor Auth Provider, see [Getting Started with an Azure Multi-Factor Auth Provider.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span></span>

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a><span data-ttu-id="ed8b2-177">Como ativar verificação em dois passos para os utilizadores?</span><span class="sxs-lookup"><span data-stu-id="ed8b2-177">How do I turn on two-step verification for users?</span></span>

<span data-ttu-id="ed8b2-178">Pode impor a verificação de dois passos para todos os inícios de sessão ou pode criar a verificação de acesso condicional políticas toorequire apenas quando aplicam condições específicas.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-178">You can enforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when specific conditions apply.</span></span>

<span data-ttu-id="ed8b2-179">Ativar a MFA do Azure, alterando os Estados de utilizador é a abordagem tradicional de Olá para exigir a verificação de dois passos.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-179">Enabling Azure MFA by changing user states is hello traditional approach for requiring two-step verification.</span></span> <span data-ttu-id="ed8b2-180">Todos os utilizadores de Olá que ativar terão Olá tooperform a verificação de requisito mesmo sempre iniciar sessão.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-180">All hello users that you enable will have hello same requirement tooperform two-step verification every time they sign in.</span></span> <span data-ttu-id="ed8b2-181">Ativar um utilizador substitui quaisquer políticas de acesso condicional que podem afetar esse utilizador.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-181">Enabling a user overrides any conditional access policies that may affect that user.</span></span>

<span data-ttu-id="ed8b2-182">Ativar a MFA do Azure com uma política de acesso condicional é uma abordagem mais flexível para exigir a verificação de dois passos.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-182">Enabling Azure MFA with a conditional access policy is a more flexible approach for requiring two-step verification.</span></span> <span data-ttu-id="ed8b2-183">Pode criar políticas de acesso condicional que se aplicam toogroups, bem como os utilizadores individuais.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-183">You can create conditional access policies that apply toogroups as well as individual users.</span></span> <span data-ttu-id="ed8b2-184">Grupos de alto risco podem ser especificados mais restrições de grupos de baixo risco, ou pode ser necessário apenas para aplicações na nuvem de alto risco e ignorada para baixo risco aqueles verificação em dois passos.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-184">High-risk groups can be given more restrictions than low-risk groups, or two-step verification can be required only for high-risk cloud apps and skipped for low-risk ones.</span></span> <span data-ttu-id="ed8b2-185">No entanto, o acesso condicional é uma funcionalidade paga do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-185">However, conditional access is a paid feature of Azure Active Directory.</span></span>

<span data-ttu-id="ed8b2-186">tooenable MFA alterando o estado do utilizador, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="ed8b2-186">tooenable MFA by changing user state, do hello following:</span></span>

1. <span data-ttu-id="ed8b2-187">Inicie sessão no toohello portal do Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-187">Sign in toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="ed8b2-188">Aceda demasiado**do Azure Active Directory \> utilizadores e grupos \> todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-188">Go too**Azure Active Directory \> Users and groups \> All users**.</span></span>
3. <span data-ttu-id="ed8b2-189">Selecione **multi-factor Authentication**.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-189">Select **Multi-Factor Authentication**.</span></span>
4. <span data-ttu-id="ed8b2-190">Localizar Olá utilizador que pretende que tooenable para MFA do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-190">Find hello user that you want tooenable for Azure MFA.</span></span> <span data-ttu-id="ed8b2-191">Poderá ser necessário toochange Olá vista na parte superior do Olá.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-191">You may need toochange hello view at hello top.</span></span>
5. <span data-ttu-id="ed8b2-192">Verifique o nome de Olá caixa seguinte toohello do utilizador.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-192">Check hello box next toohello user’s name.</span></span>
6. <span data-ttu-id="ed8b2-193">Olá direita, em passos rápidos, escolha **ativar**.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-193">On hello right, under quick steps, choose **Enable**.</span></span>

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. <span data-ttu-id="ed8b2-194">Confirme a sua selecção na janela de pop-up Olá que é aberta.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-194">Confirm your selection in hello pop-up window that opens.</span></span>  <span data-ttu-id="ed8b2-195">Os utilizadores para o qual o MFA tiver sido ativada serão pedidos tooregister Olá vez seguinte que iniciar sessão.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-195">Users for whom MFA has been enabled will be asked tooregister hello next time they sign in.</span></span>

<span data-ttu-id="ed8b2-196">tooenable MFA do Azure com uma política de acesso condicional, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="ed8b2-196">tooenable Azure MFA with a conditional access policy, do hello following:</span></span>

1. <span data-ttu-id="ed8b2-197">Inicie sessão no toohello portal do Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-197">Sign in toohello Azure portal as an administrator.</span></span>

2. <span data-ttu-id="ed8b2-198">Aceda demasiado**do Azure Active Directory \> acesso condicional**.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-198">Go too**Azure Active Directory \> Conditional access**.</span></span>

3. <span data-ttu-id="ed8b2-199">Selecione **nova política**.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-199">Select **New policy**.</span></span>

4. <span data-ttu-id="ed8b2-200">Em **atribuições**, selecione **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-200">Under **Assignments**, select **Users and groups**.</span></span> <span data-ttu-id="ed8b2-201">Olá utilize **incluir** e **excluir** separadores toospecify quais os utilizadores e grupos será gerido pela política de Olá.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-201">Use hello **Include** and     **Exclude** tabs toospecify which users and groups will be managed by hello policy.</span></span>

5. <span data-ttu-id="ed8b2-202">Em **atribuições**, selecione **aplicações em nuvem.**</span><span class="sxs-lookup"><span data-stu-id="ed8b2-202">Under **Assignments**, select **Cloud apps.**</span></span> <span data-ttu-id="ed8b2-203">Escolha demasiado**incluem todas as aplicações em nuvem**.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-203">Choose too**include All cloud apps**.</span></span>
6.  <span data-ttu-id="ed8b2-204">Em **controlos de acesso**, selecione **conceder**.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-204">Under **Access controls**, select **Grant**.</span></span> <span data-ttu-id="ed8b2-205">Escolha **requer autenticação multifator**.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-205">Choose **Require multi-factor authentication**.</span></span>
7.  <span data-ttu-id="ed8b2-206">Ativar **ativar política de** demasiado**no** e, em seguida, selecione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="ed8b2-206">Turn **Enable policy** too**On** and then select **Save**.</span></span>

<span data-ttu-id="ed8b2-207">Para obter informações sobre como tooconfigure MFA do Azure definições tooset configurar alertas de fraude, criar uma omissão de uso individual, utilizar mensagens de voz personalizadas, configurar a colocação em cache, especificar IPs fidedignos, criar palavras-passe de aplicação, ativar a MFA para dispositivos que os utilizadores de confiança e selecione a memorizar métodos de verificação, consulte [configurar definições de autenticação de multi-factor do Azure.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span><span class="sxs-lookup"><span data-stu-id="ed8b2-207">For information on how tooconfigure Azure MFA settings tooset up fraud alerts, create a one-time bypass, use custom voice messages, configure caching, specify trusted IPs, create app passwords, enable remembering MFA for devices that users trust, and select verification methods, see [Configure Azure Multi-Factor Authentication Settings.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed8b2-208">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ed8b2-208">Next steps</span></span>

- [<span data-ttu-id="ed8b2-209">Proteger o acesso privilegiado no Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed8b2-209">Securing privileged access in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [<span data-ttu-id="ed8b2-210">Perguntas mais frequentes sobre o Multi-Factor Authentication do Azure</span><span class="sxs-lookup"><span data-stu-id="ed8b2-210">Frequently asked questions about Azure Multi-Factor Authentication</span></span>](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [<span data-ttu-id="ed8b2-211">Resolução de problemas de controlo de acesso baseado em funções</span><span class="sxs-lookup"><span data-stu-id="ed8b2-211">Role-based Access Control troubleshooting</span></span>](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [<span data-ttu-id="ed8b2-212">Proteção de identidade do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed8b2-212">Azure Active Directory Identity Protection</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
