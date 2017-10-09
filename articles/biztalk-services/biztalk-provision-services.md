---
title: "aaaCreate BizTalk Services do Azure no portal do Azure de Olá | Microsoft Docs"
description: "Saiba como tooprovision ou criar os BizTalk Services do Azure no portal do Azure; de Olá MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a><span data-ttu-id="2bea5-103">Criar os BizTalk Services utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2bea5-103">Create BizTalk Services using hello Azure portal</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> <span data-ttu-id="2bea5-104">toosign no toohello portal do Azure, precisará de uma conta do Azure e subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bea5-104">toosign in toohello Azure portal, you need an Azure account and Azure subscription.</span></span> <span data-ttu-id="2bea5-105">Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="2bea5-105">If you don't have an account, you can create a free trial account within a few minutes.</span></span> <span data-ttu-id="2bea5-106">Veja [Avaliação Gratuita do Azure](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span><span class="sxs-lookup"><span data-stu-id="2bea5-106">See [Azure Free Trial](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span></span>


## <span data-ttu-id="2bea5-107"><a name="CreateService"></a>Criar um Serviço BizTalk</span><span class="sxs-lookup"><span data-stu-id="2bea5-107"><a name="CreateService"></a>Create a BizTalk Service</span></span>
<span data-ttu-id="2bea5-108">Dependendo da edição que escolher Olá, nem todas as definições do BizTalk Service poderão estar disponíveis.</span><span class="sxs-lookup"><span data-stu-id="2bea5-108">Depending on hello Edition you choose, not all BizTalk Service settings may be available.</span></span>

1. <span data-ttu-id="2bea5-109">Inicie sessão no toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="2bea5-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="2bea5-110">No painel de navegação inferior de Olá, selecione **novo**:</span><span class="sxs-lookup"><span data-stu-id="2bea5-110">In hello bottom navigation pane, select **NEW**:</span></span>  
   <span data-ttu-id="2bea5-111">![Selecione o botão novo Olá][NEWButton]</span><span class="sxs-lookup"><span data-stu-id="2bea5-111">![Select hello New button][NEWButton]</span></span>
3. <span data-ttu-id="2bea5-112">Selecione **SERVIÇOS APLICACIONAIS** > **BIZTALK SERVICE** > **CRIAÇÃO PERSONALIZADA**:</span><span class="sxs-lookup"><span data-stu-id="2bea5-112">Select **APP SERVICES** > **BIZTALK SERVICE** > **CUSTOM CREATE**:</span></span>  
   <span data-ttu-id="2bea5-113">![Selecionar Serviço BizTalk e Criação Personalizada][NewBizTalkService]</span><span class="sxs-lookup"><span data-stu-id="2bea5-113">![Select BizTalk Service and select Custom Create][NewBizTalkService]</span></span>
4. <span data-ttu-id="2bea5-114">Introduza as definições do BizTalk Service Olá:</span><span class="sxs-lookup"><span data-stu-id="2bea5-114">Enter hello BizTalk Service settings:</span></span>
   
    <table border="1">
    <tr>
    <td><span data-ttu-id="2bea5-115"><strong>Nome do Serviço BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="2bea5-115"><strong>BizTalk service name</strong></span></span></td>
    <td><span data-ttu-id="2bea5-116">Pode introduzir qualquer nome específico.</span><span class="sxs-lookup"><span data-stu-id="2bea5-116">You can enter any name but be specific.</span></span> <span data-ttu-id="2bea5-117">Alguns exemplos incluem:</span><span class="sxs-lookup"><span data-stu-id="2bea5-117">Some examples include:</span></span><br/><br/><span data-ttu-id="2bea5-118">
    <em>minhaempresa</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="2bea5-118">
    <em>mycompany</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="2bea5-119">
    <em>minhaaplicaçãominhaempresa</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="2bea5-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="2bea5-120">
    <em>minhaaplicação</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="2bea5-120">
    <em>myapplication</em>.biztalk.windows.net</span></span><br/><br/><span data-ttu-id="2bea5-121">". w" é automaticamente adicionado toohello nome que introduzir.</span><span class="sxs-lookup"><span data-stu-id="2bea5-121">".biztalk.windows.net" is automatically added toohello name you enter.</span></span> <span data-ttu-id="2bea5-122">Esta ação cria um URL que é utilizado tooaccess seu BizTalk Service, como <strong>https://<em>MinhaAplicação</em>. w</strong>.</span><span class="sxs-lookup"><span data-stu-id="2bea5-122">This creates a URL that is used tooaccess your BizTalk Service, like <strong>https://<em>myapplication</em>.biztalk.windows.net</strong>.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="2bea5-123"><strong>Edição</strong></span><span class="sxs-lookup"><span data-stu-id="2bea5-123"><strong>Edition</strong></span></span></td>
    <td><span data-ttu-id="2bea5-124">Se estiver na fase de teste/desenvolvimento Olá, escolha <strong>programador</strong>.</span><span class="sxs-lookup"><span data-stu-id="2bea5-124">If you are in hello testing/development phase, choose <strong>Developer</strong>.</span></span> <span data-ttu-id="2bea5-125">Se estiver na fase de produção Olá, utilize Olá <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: gráfico de edições</a> toodetermine se <strong>Premium</strong>, <strong>padrão</strong>, ou <strong>Basic</strong>Olá escolha correto para o seu cenário de negócio.</span><span class="sxs-lookup"><span data-stu-id="2bea5-125">If you are in hello production phase, use hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: Editions Chart</a> toodetermine if <strong>Premium</strong>, <strong>Standard</strong>, or <strong>Basic</strong> is hello correct choice for your business scenario.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="2bea5-126"><strong>Região</strong></span><span class="sxs-lookup"><span data-stu-id="2bea5-126"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="2bea5-127">Selecione Olá região geográfica toohost seu BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2bea5-127">Select hello geographic region toohost your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="2bea5-128"><strong>URL do domínio</strong></span><span class="sxs-lookup"><span data-stu-id="2bea5-128"><strong>Domain URL</strong></span></span></td>
    <td><span data-ttu-id="2bea5-129"><strong>Opcional</strong>.</span><span class="sxs-lookup"><span data-stu-id="2bea5-129"><strong>Optional</strong>.</span></span> <span data-ttu-id="2bea5-130">Por predefinição, o URL do domínio Olá é <em>Nomedobiztalkservice</em>. w.</span><span class="sxs-lookup"><span data-stu-id="2bea5-130">By default, hello domain URL is <em>YourBizTalkServiceName</em>.biztalk.windows.net.</span></span> <span data-ttu-id="2bea5-131">Também pode introduzir um domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="2bea5-131">A custom domain can also be entered.</span></span> <span data-ttu-id="2bea5-132">Por exemplo, se o seu domínio for <em>contoso</em>, pode introduzir:</span><span class="sxs-lookup"><span data-stu-id="2bea5-132">For example, if your domain is <em>contoso</em>, you can enter:</span></span> <br/><br/><span data-ttu-id="2bea5-133">
    <em>MinhaEmpresa</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="2bea5-133">
    <em>MyCompany</em>.contoso.com</span></span><br/><span data-ttu-id="2bea5-134">
    <em>MinhaAplicaçãoMinhaEmpresa</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="2bea5-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="2bea5-135">
    <em>MinhaAplicação</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="2bea5-135">
    <em>MyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="2bea5-136">
    <em>NomeDoBizTalkService</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="2bea5-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span></span><br/>
    </td>
    </tr>
    </table>
<span data-ttu-id="2bea5-137">Selecione a seta seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="2bea5-137">Select hello NEXT arrow.</span></span>
<span data-ttu-id="2bea5-138">5.</span><span class="sxs-lookup"><span data-stu-id="2bea5-138">5.</span></span> <span data-ttu-id="2bea5-139">Introduza Olá armazenamento e as definições de base de dados:</span><span class="sxs-lookup"><span data-stu-id="2bea5-139">Enter hello Storage and Database Settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="2bea5-140"><strong>Conta de armazenamento de monitorização/arquivo</strong></span><span class="sxs-lookup"><span data-stu-id="2bea5-140"><strong>Monitoring/Archiving storage account</strong></span></span></td>
    <td><span data-ttu-id="2bea5-141">Selecione uma conta de armazenamento existente ou crie uma nova.</span><span class="sxs-lookup"><span data-stu-id="2bea5-141">Select an existing storage account or create a new storage account.</span></span> <br/><br/><span data-ttu-id="2bea5-142">Se criar uma nova conta de armazenamento, introduza Olá <strong>nome da conta de armazenamento</strong>.</span><span class="sxs-lookup"><span data-stu-id="2bea5-142">If you create a new Storage account, enter hello <strong>Storage Account Name</strong>.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="2bea5-143"><strong>Base de dados de controlo</strong></span><span class="sxs-lookup"><span data-stu-id="2bea5-143"><strong>Tracking database</strong></span></span></td>
    <td><span data-ttu-id="2bea5-144">Se utilizar uma SQL Database do Azure existente, esta não poderá ser utilizada por mais nenhum BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2bea5-144">If you use an existing Azure SQL Database, it cannot be used by another BizTalk Service.</span></span> <span data-ttu-id="2bea5-145">Terá de nome de início de sessão de Olá e a palavra-passe introduzida quando esse servidor de base de dados SQL do Azure foi criado.</span><span class="sxs-lookup"><span data-stu-id="2bea5-145">You need hello login name and password entered when that Azure SQL Database Server was created.</span></span><br/><br/><span data-ttu-id="2bea5-146"><strong>Sugestão</strong> criar base de dados de controlo de Olá e conta de armazenamento de monitorização/arquivo na Olá mesma região como Olá BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2bea5-146"><strong>TIP</strong> Create hello Tracking database and Monitoring/Archiving storage account in hello same region as hello BizTalk Service.</span></span></td>
    </tr>
    </table>
<span data-ttu-id="2bea5-147">Selecione a seta seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="2bea5-147">Select hello NEXT arrow.</span></span>
<span data-ttu-id="2bea5-148">6.</span><span class="sxs-lookup"><span data-stu-id="2bea5-148">6.</span></span> <span data-ttu-id="2bea5-149">Introduza as definições de base de dados de Olá:</span><span class="sxs-lookup"><span data-stu-id="2bea5-149">Enter hello Database settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="2bea5-150"><strong>Nome</strong></span><span class="sxs-lookup"><span data-stu-id="2bea5-150"><strong>Name</strong></span></span></td>
    <td><span data-ttu-id="2bea5-151">Disponível quando <strong>criar uma nova instância de base de dados SQL</strong> está selecionado no ecrã anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="2bea5-151">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="2bea5-152">Introduza um toobe de nome de base de dados SQL utilizada pelo BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2bea5-152">Enter a SQL Database name toobe used by your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="2bea5-153"><strong>Servidor</strong></span><span class="sxs-lookup"><span data-stu-id="2bea5-153"><strong>Server</strong></span></span></td>
    <td><span data-ttu-id="2bea5-154">Disponível quando <strong>criar uma nova instância de base de dados SQL</strong> está selecionado no ecrã anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="2bea5-154">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="2bea5-155">Selecione um servidor da SQL Database existente ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="2bea5-155">Select an existing SQL Database Server or create a new SQL Database server.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="2bea5-156"><strong>Nome de início de sessão do servidor</strong></span><span class="sxs-lookup"><span data-stu-id="2bea5-156"><strong>Server login name</strong></span></span></td>
    <td><span data-ttu-id="2bea5-157">Introduza o nome de utilizador de início de sessão de Olá.</span><span class="sxs-lookup"><span data-stu-id="2bea5-157">Enter hello login user name.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="2bea5-158"><strong>Palavra-passe de início de sessão do servidor</strong></span><span class="sxs-lookup"><span data-stu-id="2bea5-158"><strong>Server login password</strong></span></span></td>
    <td><span data-ttu-id="2bea5-159">Introduza a palavra-passe de início de sessão de Olá.</span><span class="sxs-lookup"><span data-stu-id="2bea5-159">Enter hello login password.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="2bea5-160"><strong>Região</strong></span><span class="sxs-lookup"><span data-stu-id="2bea5-160"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="2bea5-161">Disponível quando selecionar <strong>Criar uma nova instância da Base de dados SQL</strong>.</span><span class="sxs-lookup"><span data-stu-id="2bea5-161">Available when <strong>Create a new SQL Database instance</strong> is selected.</span></span> <span data-ttu-id="2bea5-162">Selecione Olá região geográfica toohost a base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2bea5-162">Select hello geographic region toohost your SQL Database.</span></span></td>
    </tr>
    </table>

<span data-ttu-id="2bea5-163">Selecione o Assistente de Olá toocomplete do Olá marca de verificação.</span><span class="sxs-lookup"><span data-stu-id="2bea5-163">Select hello check mark toocomplete hello wizard.</span></span> <span data-ttu-id="2bea5-164">ícone de progresso Olá é apresentado:</span><span class="sxs-lookup"><span data-stu-id="2bea5-164">hello progress icon appears:</span></span>  
![O ícone de progresso é apresentado aquando da conclusão][ProgressComplete]

<span data-ttu-id="2bea5-166">Quando terminar, Olá BizTalk Service do Azure é criado e estará pronto para as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="2bea5-166">When complete, hello Azure BizTalk Service is created and ready for your applications.</span></span> <span data-ttu-id="2bea5-167">predefinições de Olá são suficientes.</span><span class="sxs-lookup"><span data-stu-id="2bea5-167">hello default settings are sufficient.</span></span> <span data-ttu-id="2bea5-168">Se pretender que as definições predefinidas da toochange Olá, selecione **BIZTALK SERVICES** no Olá painel de navegação esquerdo e, em seguida, selecione o seu BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2bea5-168">If you want toochange hello default settings, select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span> <span data-ttu-id="2bea5-169">Definições adicionais são apresentadas no Olá [separadores Dashboard, monitorização e dimensionamento](biztalk-dashboard-monitor-scale-tabs.md) na parte superior do Olá.</span><span class="sxs-lookup"><span data-stu-id="2bea5-169">Additional settings are displayed in hello [Dashboard, Monitor, and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md) at hello top.</span></span>

<span data-ttu-id="2bea5-170">Dependendo do Estado Olá de Olá BizTalk Service, existem algumas operações que não não possível concluir.</span><span class="sxs-lookup"><span data-stu-id="2bea5-170">Depending on hello state of hello BizTalk Service, there are some operations that cannot be completed.</span></span> <span data-ttu-id="2bea5-171">Para obter uma lista destas operações, visite demasiado[BizTalk Services gráfico de estado](biztalk-service-state-chart.md).</span><span class="sxs-lookup"><span data-stu-id="2bea5-171">For a list of these operations, go too[BizTalk Services State Chart](biztalk-service-state-chart.md).</span></span>

## <a name="post-provisioning-steps"></a><span data-ttu-id="2bea5-172">Passos pós-aprovisionamento</span><span class="sxs-lookup"><span data-stu-id="2bea5-172">Post-provisioning steps</span></span>
* [<span data-ttu-id="2bea5-173">Instalar o certificado de Olá num computador local</span><span class="sxs-lookup"><span data-stu-id="2bea5-173">Install hello certificate on a local computer</span></span>](#InstallCert)
* [<span data-ttu-id="2bea5-174">Adicionar um certificado pronto para produção</span><span class="sxs-lookup"><span data-stu-id="2bea5-174">Add a production-ready certificate</span></span>](#AddCert)
* [<span data-ttu-id="2bea5-175">Obter o espaço de nomes de controlo de acesso de Olá</span><span class="sxs-lookup"><span data-stu-id="2bea5-175">Get hello Access Control namespace</span></span>](#ACS)

#### <span data-ttu-id="2bea5-176"><a name="InstallCert"></a>Instalar o certificado de Olá num computador local</span><span class="sxs-lookup"><span data-stu-id="2bea5-176"><a name="InstallCert"></a>Install hello certificate on a local computer</span></span>
<span data-ttu-id="2bea5-177">Como parte do aprovisionamento do BizTalk Service, é criado um certificado autoassinado e associado à sua subscrição do BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2bea5-177">As part of BizTalk Service provisioning, a self-signed certificate is created and associated with your BizTalk Service subscription.</span></span> <span data-ttu-id="2bea5-178">Tem de transferir este certificado e instalá-lo em computadores a partir de onde se implementar aplicações do BizTalk Service ou enviar mensagens tooa ponto final do BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2bea5-178">You must download this certificate and install it on computers from where you either deploy BizTalk Service applications or send messages tooa BizTalk Service endpoint.</span></span>

1. <span data-ttu-id="2bea5-179">Inicie sessão no toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="2bea5-179">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="2bea5-180">Selecione **BIZTALK SERVICES** no Olá painel de navegação esquerdo e, em seguida, selecione a subscrição do BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2bea5-180">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service subscription.</span></span>
3. <span data-ttu-id="2bea5-181">Selecione Olá **Dashboard** separador.</span><span class="sxs-lookup"><span data-stu-id="2bea5-181">Select hello **Dashboard** tab.</span></span>
4. <span data-ttu-id="2bea5-182">Selecione **Transferir Certificado SSL**:</span><span class="sxs-lookup"><span data-stu-id="2bea5-182">Select **Download SSL Certificate**:</span></span>  
   <span data-ttu-id="2bea5-183">![Modificar o Certificado SSL][QuickGlance]</span><span class="sxs-lookup"><span data-stu-id="2bea5-183">![Modify SSL Certificate][QuickGlance]</span></span>
5. <span data-ttu-id="2bea5-184">Faça duplo clique Olá certificado e executar através de certificado do Olá assistente tooinstall Olá.</span><span class="sxs-lookup"><span data-stu-id="2bea5-184">Double-click hello certificate and run through hello wizard tooinstall hello certificate.</span></span> <span data-ttu-id="2bea5-185">Certifique-se instalar o certificado de Olá em Olá **autoridades de certificação de raiz fidedigna** armazenar.</span><span class="sxs-lookup"><span data-stu-id="2bea5-185">Make sure you install hello certificate under hello **Trusted Root Certificate Authorities** store.</span></span>

#### <span data-ttu-id="2bea5-186"><a name="AddCert"></a>Adicionar um certificado pronto para produção</span><span class="sxs-lookup"><span data-stu-id="2bea5-186"><a name="AddCert"></a>Add a production-ready certificate</span></span>
<span data-ttu-id="2bea5-187">Olá certificado autoassinado criado automaticamente quando criar os BizTalk Services destina-se em só a ambientes de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="2bea5-187">hello self-signed certificate that is automatically created when creating BizTalk Services is intended for use in development environments only.</span></span> <span data-ttu-id="2bea5-188">Para cenários de produção, substitua-o pelo certificado pronto para produção.</span><span class="sxs-lookup"><span data-stu-id="2bea5-188">For production scenarios, replace it with a production-ready certificate.</span></span>

1. <span data-ttu-id="2bea5-189">No Olá **Dashboard** separador, selecione **atualizar certificado SSL**.</span><span class="sxs-lookup"><span data-stu-id="2bea5-189">On hello **Dashboard** tab, select **Update SSL Certificate**.</span></span>
2. <span data-ttu-id="2bea5-190">Procurar o certificado SSL privado tooyour (*CertificateName*. pfx) que inclui o nome do seu BizTalk Service, introduza a palavra-passe de Olá e, em seguida, clique em marca de verificação Olá.</span><span class="sxs-lookup"><span data-stu-id="2bea5-190">Browse tooyour private SSL certificate (*CertificateName*.pfx) that includes your BizTalk Service name, enter hello password, and then click hello check mark.</span></span>

#### <span data-ttu-id="2bea5-191"><a name="ACS"></a>Obter o espaço de nomes de controlo de acesso de Olá</span><span class="sxs-lookup"><span data-stu-id="2bea5-191"><a name="ACS"></a>Get hello Access Control namespace</span></span>
1. <span data-ttu-id="2bea5-192">Inicie sessão no toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="2bea5-192">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="2bea5-193">Selecione **BIZTALK SERVICES** no Olá painel de navegação esquerdo e, em seguida, selecione o seu BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2bea5-193">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span>
3. <span data-ttu-id="2bea5-194">Na barra de tarefas Olá, selecione **informações de ligação**:</span><span class="sxs-lookup"><span data-stu-id="2bea5-194">In hello task bar, select **Connection Information**:</span></span>  
   <span data-ttu-id="2bea5-195">![Selecionar Informações de Ligação][ACSConnectInfo]</span><span class="sxs-lookup"><span data-stu-id="2bea5-195">![Select Connection Information][ACSConnectInfo]</span></span>
4. <span data-ttu-id="2bea5-196">Copie os valores do controlo de acesso de Olá.</span><span class="sxs-lookup"><span data-stu-id="2bea5-196">Copy hello Access Control values.</span></span>

<span data-ttu-id="2bea5-197">Quando implementa um projeto dos BizTalk Services a partir do Visual Studio, introduza este espaço de nomes do Controlo de Acesso.</span><span class="sxs-lookup"><span data-stu-id="2bea5-197">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="2bea5-198">espaço de nomes de controlo de acesso de Olá é criado automaticamente para o seu BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2bea5-198">hello Access Control namespace is automatically created for your BizTalk Service.</span></span>

<span data-ttu-id="2bea5-199">os valores do controlo de acesso de Olá podem ser utilizados com qualquer aplicação.</span><span class="sxs-lookup"><span data-stu-id="2bea5-199">hello Access Control values can be used with any application.</span></span> <span data-ttu-id="2bea5-200">Quando é criado BizTalk Services do Azure, este espaço de nomes do controlo de acesso controla a autenticação de Olá à sua implementação do BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2bea5-200">When Azure BizTalk Services is created, this Access Control namespace controls hello authentication with your BizTalk Service deployment.</span></span> <span data-ttu-id="2bea5-201">Selecione se pretende a subscrição de Olá toochange ou gerir o espaço de nomes de Olá, **do Active Directory** no Olá painel de navegação esquerdo e, em seguida, selecione o espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="2bea5-201">If you want toochange hello subscription or manage hello namespace, select **ACTIVE DIRECTORY** in hello left navigation pane and then select your namespace.</span></span> <span data-ttu-id="2bea5-202">barra de tarefas Olá lista as suas opções.</span><span class="sxs-lookup"><span data-stu-id="2bea5-202">hello task bar lists your options.</span></span>

<span data-ttu-id="2bea5-203">Ao clicar em **gerir** abre Olá Portal de gestão do controlo de acesso.</span><span class="sxs-lookup"><span data-stu-id="2bea5-203">Clicking **Manage** opens hello Access Control Management Portal.</span></span> <span data-ttu-id="2bea5-204">No Portal de gestão do controlo de acesso Olá, Olá BizTalk Service utiliza **identidades do serviço**:</span><span class="sxs-lookup"><span data-stu-id="2bea5-204">In hello Access Control Management Portal, hello BizTalk Service uses **Service identities**:</span></span>  
<span data-ttu-id="2bea5-205">![Identidades do serviço de ACS no Olá Portal de gestão do controlo de acesso][ACSServiceIdentities]</span><span class="sxs-lookup"><span data-stu-id="2bea5-205">![ACS Service Identities in hello Access Control Management Portal][ACSServiceIdentities]</span></span>

<span data-ttu-id="2bea5-206">Olá identidade de serviço de controlo de acesso é um conjunto de credenciais que permitem a aplicações ou tooauthenticate clientes diretamente com o controlo de acesso e receber um token.</span><span class="sxs-lookup"><span data-stu-id="2bea5-206">hello Access Control service identity is a set of credentials that allow applications or clients tooauthenticate directly with Access Control and receive a token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2bea5-207">Olá BizTalk Service utiliza **proprietário** para uma identidade de serviço predefinido Olá e Olá **palavra-passe** valor.</span><span class="sxs-lookup"><span data-stu-id="2bea5-207">hello BizTalk Service uses **Owner** for hello default service identity and hello **Password** value.</span></span> <span data-ttu-id="2bea5-208">Se utilizar o valor de chave simétrica Olá em vez de Olá valor de palavra-passe, hello erro seguinte pode ocorrer.</span><span class="sxs-lookup"><span data-stu-id="2bea5-208">If you use hello Symmetric Key value instead of hello Password value, hello following error may occur.</span></span><br/><br/><span data-ttu-id="2bea5-209">*Não foi possível ligar a conta de serviço de gestão do controlo de acesso de toohello com Olá especificada credenciais*</span><span class="sxs-lookup"><span data-stu-id="2bea5-209">*Could not connect toohello Access Control Management Service account with hello specified credentials*</span></span>
> 
> 

<span data-ttu-id="2bea5-210">Em [Gerir o Espaço de Nomes do ACS](https://msdn.microsoft.com/library/azure/hh674478.aspx), pode ver uma lista de algumas diretrizes e recomendações.</span><span class="sxs-lookup"><span data-stu-id="2bea5-210">[Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) lists some guidelines and recommendations.</span></span>

## <a name="requirements-explained"></a><span data-ttu-id="2bea5-211">Requisitos explicados</span><span class="sxs-lookup"><span data-stu-id="2bea5-211">Requirements explained</span></span>
<span data-ttu-id="2bea5-212">Estes requisitos não se aplicam toohello edição gratuita.</span><span class="sxs-lookup"><span data-stu-id="2bea5-212">These requirements do not apply toohello Free Edition.</span></span>

<table border="1">
<tr bgcolor="FAF9F9">
        <td><span data-ttu-id="2bea5-213"><strong>Do que precisa</strong></span><span class="sxs-lookup"><span data-stu-id="2bea5-213"><strong>What you need</strong></span></span></td>
        <td><span data-ttu-id="2bea5-214"><strong>Porque precisa</strong></span><span class="sxs-lookup"><span data-stu-id="2bea5-214"><strong>Why you need it</strong></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="2bea5-215">Subscrição do Azure</span><span class="sxs-lookup"><span data-stu-id="2bea5-215">Azure subscription</span></span></td>
<td><span data-ttu-id="2bea5-216">subscrição de Olá determina quem pode iniciar sessão no toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bea5-216">hello subscription determines who can sign in toohello Azure portal.</span></span> <span data-ttu-id="2bea5-217">o marcador de posição do Olá conta cria a subscrição de Olá em <a HREF="https://account.windowsazure.com/Subscriptions"> subscrições do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="2bea5-217">hello Account holder creates hello subscription at <a HREF="https://account.windowsazure.com/Subscriptions"> Azure Subscriptions</a>.</span></span>
<br/><br/>
<span data-ttu-id="2bea5-218">Olá conta do Azure pode ter várias subscrições e pode ser gerida por qualquer pessoa autorizada.</span><span class="sxs-lookup"><span data-stu-id="2bea5-218">hello Azure account can have multiple subscriptions and can be managed by anyone who is permitted.</span></span> <span data-ttu-id="2bea5-219">Por exemplo, o titular da conta do Azure cria uma subscrição designada <em>BizTalkServiceSubscription</em> e fornecem Olá administradores do BizTalk dentro da empresa (por exemplo, ContosoBTSAdmins@live.com) aceder à subscrição toothis.</span><span class="sxs-lookup"><span data-stu-id="2bea5-219">For example, your Azure account holder creates a subscription named <em>BizTalkServiceSubscription</em> and gives hello BizTalk Administrators within your company (for example, ContosoBTSAdmins@live.com) access toothis subscription.</span></span> <span data-ttu-id="2bea5-220">Neste cenário, os administradores do BizTalk Olá inicie sessão toohello portal do Azure e ter completos serviços do administrador direitos tooall Olá alojado na subscrição Olá, incluindo os BizTalk Services do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bea5-220">In this scenario, hello BizTalk Administrators sign in toohello Azure portal and have full Administrator rights tooall hello hosted services in hello subscription, including Azure BizTalk Services.</span></span> <span data-ttu-id="2bea5-221">Administradores do BizTalk Olá não são proprietários da conta do Azure de Olá, pelo que não tem acesso tooany as informações de faturação.</span><span class="sxs-lookup"><span data-stu-id="2bea5-221">hello BizTalk Administrators are not hello Azure account holders and therefore don't have access tooany billing information.</span></span>
<br/><br/><span data-ttu-id="2bea5-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Gerir subscrições e contas de armazenamento no portal do Azure de Olá</a> fornece mais informações.</span><span class="sxs-lookup"><span data-stu-id="2bea5-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577"> Manage Subscriptions and Storage Accounts in hello Azure portal</a> provides more information.</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="2bea5-223">Base de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="2bea5-223">Azure SQL Database</span></span></td>
<td><span data-ttu-id="2bea5-224">Armazena Olá tabelas, vistas e os procedimentos armazenados utilizados pelo BizTalk Service, incluindo dados de controlo de Olá de Olá.</span><span class="sxs-lookup"><span data-stu-id="2bea5-224">Stores hello tables, views, and stored procedures used by hello BizTalk Service, including hello Tracking data.</span></span>
<br/><br/>
<span data-ttu-id="2bea5-225">Quando cria um BizTalk Service, pode utilizar um Servidor SQL do Azure existente, uma SQL Database do Azure ou criar automaticamente um novo servidor ou base de dados.</span><span class="sxs-lookup"><span data-stu-id="2bea5-225">When you create a BizTalk Service, you can use an existing Azure SQL Server, Azure SQL Database, or automatically create a new Server or Database.</span></span>
<br/><br/>
<span data-ttu-id="2bea5-226">Olá escala de base de dados SQL é automaticamente configurado.</span><span class="sxs-lookup"><span data-stu-id="2bea5-226">hello SQL Database scale is automatically configured.</span></span> <span data-ttu-id="2bea5-227">Normalmente, dimensionamento do Olá predefinido é suficiente para um BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2bea5-227">Typically, hello default scale is sufficient for a BizTalk Service.</span></span> <span data-ttu-id="2bea5-228">Escala de Olá alteração terá impactos nos preços.</span><span class="sxs-lookup"><span data-stu-id="2bea5-228">Changing hello scale impacts pricing.</span></span> <span data-ttu-id="2bea5-229">Veja <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930">Contas e Faturação na Base de Dados SQL do Azure</a>
</span><span class="sxs-lookup"><span data-stu-id="2bea5-229">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
</span></span><br/><br/><span data-ttu-id="2bea5-230">
<strong>Notas</strong>
</span><span class="sxs-lookup"><span data-stu-id="2bea5-230">
<strong>Notes</strong>
</span></span><br/>
<ul>
<li> <span data-ttu-id="2bea5-231">Quando cria uma nova Base de Dados e um novo Servidor SQL do Azure, os Serviços do Azure são automaticamente ativados.</span><span class="sxs-lookup"><span data-stu-id="2bea5-231">When you create a new Azure SQL Server and Database, Azure Services is automatically enabled.</span></span> <span data-ttu-id="2bea5-232">Olá BizTalk Service requer os serviços do Azure ativada.</span><span class="sxs-lookup"><span data-stu-id="2bea5-232">hello BizTalk Service requires Azure Services be enabled.</span></span></li>
<li><span data-ttu-id="2bea5-233">Se criar uma nova base de dados do Azure SQL Server num servidor SQL do Azure existente, Olá regras de firewall de Olá Server não são alterados.</span><span class="sxs-lookup"><span data-stu-id="2bea5-233">If you create a new Azure SQL Database on an existing Azure SQL Server, hello firewall rules of hello Server are not changed.</span></span> <span data-ttu-id="2bea5-234">Como resultado, é possível a que outros serviços do Azure não são permitidos bases de dados do servidor de acesso toohello.</span><span class="sxs-lookup"><span data-stu-id="2bea5-234">As a result, it's possible other Azure Services are not allowed access toohello Server's databases.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="2bea5-235">Espaço de nomes do Controlo de Acesso do Azure</span><span class="sxs-lookup"><span data-stu-id="2bea5-235">Azure Access Control namespace</span></span></td>
<td><span data-ttu-id="2bea5-236">É autenticado com o BizTalk Services do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bea5-236">Authenticates with Azure BizTalk Services.</span></span> <span data-ttu-id="2bea5-237">Quando implementa um projeto dos BizTalk Services a partir do Visual Studio, introduza este espaço de nomes do Controlo de Acesso.</span><span class="sxs-lookup"><span data-stu-id="2bea5-237">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="2bea5-238">Quando cria um BizTalk Service, o espaço de nomes de controlo de acesso de Olá é criado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2bea5-238">When you create a BizTalk Service, hello Access Control namespace is automatically created.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="2bea5-239">Conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2bea5-239">Azure Storage account</span></span></td>
<td><span data-ttu-id="2bea5-240">Fornecem acesso tootables, blobs e filas utilizados pelo seu seguinte do BizTalk Service toosave Olá:</span><span class="sxs-lookup"><span data-stu-id="2bea5-240">Gives access tootables, blobs, and queues used by your BizTalk Service toosave hello following:</span></span>

<ul>
<li><span data-ttu-id="2bea5-241">Os ficheiros de registo Olá esse monitor BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2bea5-241">Log files that monitor hello BizTalk Service.</span></span> <span data-ttu-id="2bea5-242">Olá monitorização saída também é apresentada no Olá **monitorização** separador Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bea5-242">hello monitoring output is also displayed in hello **Monitoring** tab in hello Azure portal.</span></span></li>
<li><span data-ttu-id="2bea5-243">Ao criar um contrato X12 ou AS2 entre parceiros, pode ativar Olá arquivo funcionalidade toostore as propriedades da mensagem.</span><span class="sxs-lookup"><span data-stu-id="2bea5-243">When creating an X12 or AS2 agreement between partners, you can enable hello Archiving feature toostore message properties.</span></span> <span data-ttu-id="2bea5-244">Estes dados são guardados no Olá conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2bea5-244">This data is saved in hello Storage account.</span></span></li>
</ul>
<br/>
<span data-ttu-id="2bea5-245">Quando cria um BizTalk Service, pode utilizar uma Conta de armazenamento existente ou criar automaticamente uma nova.</span><span class="sxs-lookup"><span data-stu-id="2bea5-245">When you create a BizTalk Service, you can use an existing Storage account or automatically create a new Storage account.</span></span>
<br/><br/>
<span data-ttu-id="2bea5-246">as definições de armazenamento de predefinido Olá são suficientes para um BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2bea5-246">hello default Storage settings are sufficient for a BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="2bea5-247">Quando cria uma Conta de armazenamento, são criadas automaticamente uma Chave Primária e uma Chave Secundária.</span><span class="sxs-lookup"><span data-stu-id="2bea5-247">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="2bea5-248">Estas chaves controlam o acesso tooyour conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2bea5-248">These Keys control access tooyour Storage account.</span></span> <span data-ttu-id="2bea5-249">Olá BizTalk Service utiliza automaticamente Olá chave primária.</span><span class="sxs-lookup"><span data-stu-id="2bea5-249">hello BizTalk Service automatically uses hello Primary Key.</span></span>
<br/><br/>
<span data-ttu-id="2bea5-250">Para obter mais informações, veja <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">Armazenamento</a>.</span><span class="sxs-lookup"><span data-stu-id="2bea5-250">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a> for more information.</span></span>
</td>
</tr>

<tr>
<td><span data-ttu-id="2bea5-251">Certificado SSL privado</span><span class="sxs-lookup"><span data-stu-id="2bea5-251">SSL private certificate</span></span></td>
<td>
<span data-ttu-id="2bea5-252">Quando cria um BizTalk Service do Azure, também é criado um URL HTTPS com o nome do seu BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2bea5-252">When an Azure BizTalk Service is created, an HTTPS URL that includes your BizTalk Service name is also created.</span></span> <span data-ttu-id="2bea5-253">Este URL é configurada automaticamente toouse um certificado autoassinado do apenas de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="2bea5-253">This URL is automatically configured toouse a self-signed development-only certificate.</span></span> <span data-ttu-id="2bea5-254">Para a produção, precisa de um certificado SSL privado.</span><span class="sxs-lookup"><span data-stu-id="2bea5-254">For production, you need a private SSL certificate.</span></span>
<br/><br/><span data-ttu-id="2bea5-255">
<strong>Informações importantes sobre o Certificado SSL</strong>

</span><span class="sxs-lookup"><span data-stu-id="2bea5-255">
<strong>Important SSL Certificate Information</strong>

</span></span><ul>
<li><span data-ttu-id="2bea5-256">data de expiração do certificado Olá tem de ser inferior a cinco anos.</span><span class="sxs-lookup"><span data-stu-id="2bea5-256">hello certificate expiration date must be less than 5 years.</span></span></li>
<li><span data-ttu-id="2bea5-257">Todos os certificados privados requerem uma palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="2bea5-257">All private certificates require a password.</span></span> <span data-ttu-id="2bea5-258">Lembre-se desta palavra-passe e, como uma melhor prática, partilhe-a com os seus administradores.</span><span class="sxs-lookup"><span data-stu-id="2bea5-258">Know this password and as a best practice, share this password with your administrators.</span></span></li>
<li><span data-ttu-id="2bea5-259">Os certificados autoassinados são utilizados num ambiente de teste/desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="2bea5-259">Self-signed certificates are used in a test/development environment.</span></span> <span data-ttu-id="2bea5-260">Quando utilizar certificados autoassinados, importe o arquivo de certificados pessoais do Olá certificados tooyour e Olá arquivo de certificados de autoridades de certificação de raiz fidedigna.</span><span class="sxs-lookup"><span data-stu-id="2bea5-260">When using self-signed certificates, import hello certificate tooyour Personal certificate store and hello Trusted Root Certification Authorities certificate store.</span></span></li>
</ul>
<br/><span data-ttu-id="2bea5-261">Quando for enviada a autoridade de certificação de tooyour certificado pedido Olá produção, dê Olá seguintes propriedades do certificado:</span><span class="sxs-lookup"><span data-stu-id="2bea5-261">When sending hello production certificate request tooyour certification authority, give hello following certificate properties:</span></span>
<br/>

<ul>
<li><span data-ttu-id="2bea5-262"><strong>Utilização de Chave Avançada</strong>: no mínimo, os Serviços BizTalk do Azure requerem a Autenticação do Servidor.</span><span class="sxs-lookup"><span data-stu-id="2bea5-262"><strong>Enhanced Key Usage</strong>: At a minimum, Azure BizTalk Services requires Server Authentication.</span></span></li>
<li><span data-ttu-id="2bea5-263"><strong>Nome comum</strong>: introduza o nome de domínio completamente qualificado (FQDN) Olá do seu URL de serviço BizTalk do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bea5-263"><strong>Common Name</strong>: Enter hello fully qualified domain name (FQDN) of your Azure BizTalk Service URL.</span></span> <span data-ttu-id="2bea5-264">Veja <a HREF="#CreateService">Criar um BizTalk Service</a> neste artigo.</span><span class="sxs-lookup"><span data-stu-id="2bea5-264">See <a HREF="#CreateService">Create a BizTalk Service</a> in this article.</span></span></li>
</ul>
<br/>
<span data-ttu-id="2bea5-265">Um certificado novo ou diferentes pode ser adicionado depois da criação Olá BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2bea5-265">A new or different certificate can be added after hello BizTalk Service is created.</span></span>
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a><span data-ttu-id="2bea5-266">Ligações Híbridas</span><span class="sxs-lookup"><span data-stu-id="2bea5-266">Hybrid Connections</span></span>
<span data-ttu-id="2bea5-267">Quando cria um BizTalk Service do Azure, Olá **ligações híbridas** separador está disponível:</span><span class="sxs-lookup"><span data-stu-id="2bea5-267">When you create an Azure BizTalk Service, hello **Hybrid Connections** tab is available:</span></span>

![Separador Ligações Híbridas][HybridConnectionTab]

<span data-ttu-id="2bea5-269">As ligações híbridas são utilizada tooconnect um Azure site ou serviço móvel do Azure tooany no local recursos que utiliza uma porta TCP estática, como o SQL Server, MySQL, APIs da Web HTTP, os Mobile Services e a maioria dos serviços Web personalizados.</span><span class="sxs-lookup"><span data-stu-id="2bea5-269">Hybrid Connections are used tooconnect an Azure website or Azure mobile service tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, Mobile Services, and most custom Web Services.</span></span>  <span data-ttu-id="2bea5-270">As ligações híbridas e Olá BizTalk Adapter Service são diferentes.</span><span class="sxs-lookup"><span data-stu-id="2bea5-270">Hybrid Connections and hello BizTalk Adapter Service are different.</span></span> <span data-ttu-id="2bea5-271">Olá BizTalk Adapter Service é o sistema de linha de negócio (LOB) do tooconnect utilizados BizTalk Services do Azure tooan no local.</span><span class="sxs-lookup"><span data-stu-id="2bea5-271">hello BizTalk Adapter Service is used tooconnect Azure BizTalk Services tooan on-premises Line of Business (LOB) system.</span></span>

 <span data-ttu-id="2bea5-272">Consulte [ligações híbridas](integration-hybrid-connection-overview.md) toolearn mais, incluindo criar e gerir ligações híbridas.</span><span class="sxs-lookup"><span data-stu-id="2bea5-272">See [Hybrid Connections](integration-hybrid-connection-overview.md) toolearn more, including creating and managing Hybrid Connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bea5-273">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2bea5-273">Next steps</span></span>
<span data-ttu-id="2bea5-274">Agora que é criado um BizTalk Service, familiarize-se com Olá diferentes [BizTalk Services: separadores Dashboard, monitorização e dimensionamento](biztalk-dashboard-monitor-scale-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="2bea5-274">Now that a BizTalk Service is created, familiarize yourself with hello different [BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md).</span></span> <span data-ttu-id="2bea5-275">O BizTalk Service está pronto para as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="2bea5-275">Your BizTalk Service is ready for your applications.</span></span> <span data-ttu-id="2bea5-276">toostart criar aplicações, acedas demasiado[BizTalk Services do Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="2bea5-276">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="2bea5-277">Consultar também</span><span class="sxs-lookup"><span data-stu-id="2bea5-277">See also</span></span>
* [<span data-ttu-id="2bea5-278">Serviços BizTalk: Gráfico de Edições</span><span class="sxs-lookup"><span data-stu-id="2bea5-278">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)<br/>
* [<span data-ttu-id="2bea5-279">Serviços BizTalk: Gráfico de Estado</span><span class="sxs-lookup"><span data-stu-id="2bea5-279">BizTalk Services: State Chart</span></span>](biztalk-service-state-chart.md)<br/>
* [<span data-ttu-id="2bea5-280">Serviços BizTalk: Cópia de segurança e Restauro</span><span class="sxs-lookup"><span data-stu-id="2bea5-280">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)<br/>
* [<span data-ttu-id="2bea5-281">Serviços BizTalk: limitação</span><span class="sxs-lookup"><span data-stu-id="2bea5-281">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)<br/>
* [<span data-ttu-id="2bea5-282">Serviços BizTalk: Nome e Chave do Emissor</span><span class="sxs-lookup"><span data-stu-id="2bea5-282">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)<br/>
* [<span data-ttu-id="2bea5-283">Como posso começar a utilizar Olá SDK dos BizTalk Services do Azure</span><span class="sxs-lookup"><span data-stu-id="2bea5-283">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="2bea5-284">Ligações Híbridas</span><span class="sxs-lookup"><span data-stu-id="2bea5-284">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
