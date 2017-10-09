---
title: aaaManage sua primeira API na API Management do Azure | Microsoft Docs
description: "Saiba como toocreate APIs, adicionar operações e começar a utilizar com a API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a><span data-ttu-id="cd22b-103">Gerir a sua primeira API na API Management do Azure</span><span class="sxs-lookup"><span data-stu-id="cd22b-103">Manage your first API in Azure API Management</span></span>
## <span data-ttu-id="cd22b-104"><a name="overview"> </a>Descrição geral</span><span class="sxs-lookup"><span data-stu-id="cd22b-104"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="cd22b-105">Este guia mostra como tooquickly começar a utilizar a API Management do Azure e efetuar a primeira chamada de API.</span><span class="sxs-lookup"><span data-stu-id="cd22b-105">This guide shows you how tooquickly get started in using Azure API Management and make your first API call.</span></span>

## <span data-ttu-id="cd22b-106"><a name="concepts"> </a>O que é a Gestão de API do Azure?</span><span class="sxs-lookup"><span data-stu-id="cd22b-106"><a name="concepts"> </a>What is Azure API Management?</span></span>
<span data-ttu-id="cd22b-107">Pode utilizar qualquer back-end de API Management do Azure tootake e iniciar um programa de API totalmente funcional com base no mesmo.</span><span class="sxs-lookup"><span data-stu-id="cd22b-107">You can use Azure API Management tootake any backend and launch a full-fledged API program based on it.</span></span>

<span data-ttu-id="cd22b-108">Os cenários comuns incluem:</span><span class="sxs-lookup"><span data-stu-id="cd22b-108">Common scenarios include:</span></span>

* <span data-ttu-id="cd22b-109">**Proteção da infraestrutura móvel** mediante o controlo de acesso com chaves de API, prevenção de ataques DoS através da utilização de limitação ou utilização de políticas de segurança avançadas como a validação de token JWT.</span><span class="sxs-lookup"><span data-stu-id="cd22b-109">**Securing mobile infrastructure** by gating access with API keys, preventing DOS attacks by using throttling, or using advanced security policies like JWT token validation.</span></span>
* <span data-ttu-id="cd22b-110">**Ativação de ecossistemas de parceiros ISV** , oferecendo integração rápida dos parceiros através de programação de Olá portal e a criação de um toodecouple fachada de API de implementações internas que não são ripe para consumo de parceiro.</span><span class="sxs-lookup"><span data-stu-id="cd22b-110">**Enabling ISV partner ecosystems** by offering fast partner onboarding through hello developer portal and building an API facade toodecouple from internal implementations that are not ripe for partner consumption.</span></span>
* <span data-ttu-id="cd22b-111">**Executar um programa de API interno** por oferecer uma localização centralizada para Olá organização toocommunicate sobre a disponibilidade de Olá e mais recentes alterações tooAPIs, controlo de acesso com base em contas organizacionais, todos os com base num canal seguro entre Olá gateway da API e Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="cd22b-111">**Running an internal API program** by offering a centralized location for hello organization toocommunicate about hello availability and latest changes tooAPIs, gating access based on organizational accounts, all based on a secured channel between hello API gateway and hello backend.</span></span>

<span data-ttu-id="cd22b-112">sistema de Olá é constituído por Olá os seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="cd22b-112">hello system is made up of hello following components:</span></span>

* <span data-ttu-id="cd22b-113">Olá **gateway da API** é o ponto final de Olá que:</span><span class="sxs-lookup"><span data-stu-id="cd22b-113">hello **API gateway** is hello endpoint that:</span></span>
  
  * <span data-ttu-id="cd22b-114">Aceita as chamadas de API e encaminha-os de back-ends de tooyour.</span><span class="sxs-lookup"><span data-stu-id="cd22b-114">Accepts API calls and routes them tooyour backends.</span></span>
  * <span data-ttu-id="cd22b-115">Verifica as chaves de API, os tokens JWT, os certificados e outras credenciais.</span><span class="sxs-lookup"><span data-stu-id="cd22b-115">Verifies API keys, JWT tokens, certificates, and other credentials.</span></span>
  * <span data-ttu-id="cd22b-116">Impõe quotas de utilização e limites de velocidade.</span><span class="sxs-lookup"><span data-stu-id="cd22b-116">Enforces usage quotas and rate limits.</span></span>
  * <span data-ttu-id="cd22b-117">Transforma a API no momento de Olá sem modificações no código.</span><span class="sxs-lookup"><span data-stu-id="cd22b-117">Transforms your API on hello fly without code modifications.</span></span>
  * <span data-ttu-id="cd22b-118">Coloca em cache as respostas de back-end, quando estão configuradas.</span><span class="sxs-lookup"><span data-stu-id="cd22b-118">Caches backend responses where set up.</span></span>
  * <span data-ttu-id="cd22b-119">Regista metadados de chamadas para fins de análise.</span><span class="sxs-lookup"><span data-stu-id="cd22b-119">Logs call metadata for analytics purposes.</span></span>
* <span data-ttu-id="cd22b-120">Olá **portal do publicador** é a interface administrativa olá onde configurou o seu programa de API.</span><span class="sxs-lookup"><span data-stu-id="cd22b-120">hello **publisher portal** is hello administrative interface where you set up your API program.</span></span> <span data-ttu-id="cd22b-121">Utilize-o para:</span><span class="sxs-lookup"><span data-stu-id="cd22b-121">Use it to:</span></span>
  
  * <span data-ttu-id="cd22b-122">Definir ou importar o esquema de API.</span><span class="sxs-lookup"><span data-stu-id="cd22b-122">Define or import API schema.</span></span>
  * <span data-ttu-id="cd22b-123">Integrar APIs em produtos.</span><span class="sxs-lookup"><span data-stu-id="cd22b-123">Package APIs into products.</span></span>
  * <span data-ttu-id="cd22b-124">Configure políticas como quotas ou transformações nas APIs de Olá.</span><span class="sxs-lookup"><span data-stu-id="cd22b-124">Set up policies like quotas or transformations on hello APIs.</span></span>
  * <span data-ttu-id="cd22b-125">Obter conhecimentos aprofundados a partir da análise.</span><span class="sxs-lookup"><span data-stu-id="cd22b-125">Get insights from analytics.</span></span>
  * <span data-ttu-id="cd22b-126">Gerir utilizadores.</span><span class="sxs-lookup"><span data-stu-id="cd22b-126">Manage users.</span></span>
* <span data-ttu-id="cd22b-127">Olá **portal do programador** serve como Olá principal presença na web para os programadores, onde podem:</span><span class="sxs-lookup"><span data-stu-id="cd22b-127">hello **developer portal** serves as hello main web presence for developers, where they can:</span></span>
  
  * <span data-ttu-id="cd22b-128">Ler a documentação da API.</span><span class="sxs-lookup"><span data-stu-id="cd22b-128">Read API documentation.</span></span>
  * <span data-ttu-id="cd22b-129">Experimente uma API através da consola interativa Olá.</span><span class="sxs-lookup"><span data-stu-id="cd22b-129">Try out an API via hello interactive console.</span></span>
  * <span data-ttu-id="cd22b-130">Criar uma conta e subscrever tooget API chaves.</span><span class="sxs-lookup"><span data-stu-id="cd22b-130">Create an account and subscribe tooget API keys.</span></span>
  * <span data-ttu-id="cd22b-131">Aceder a análises sobre a sua própria utilização.</span><span class="sxs-lookup"><span data-stu-id="cd22b-131">Access analytics on their own usage.</span></span>

## <span data-ttu-id="cd22b-132"><a name="create-service-instance"> </a>Criar uma instância da Gestão de API</span><span class="sxs-lookup"><span data-stu-id="cd22b-132"><a name="create-service-instance"> </a>Create an API Management instance</span></span>
> [!NOTE]
> <span data-ttu-id="cd22b-133">toocomplete neste tutorial, precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd22b-133">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="cd22b-134">Se não tiver uma conta, pode criar uma conta gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="cd22b-134">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="cd22b-135">Para obter mais detalhes, consulte [Azure Free Trial (Avaliação Gratuita do Azure)][Azure Free Trial].</span><span class="sxs-lookup"><span data-stu-id="cd22b-135">For details, see [Azure Free Trial][Azure Free Trial].</span></span>
> 
> 

<span data-ttu-id="cd22b-136">Olá primeiro passo para trabalhar com a API Management é toocreate uma instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="cd22b-136">hello first step in working with API Management is toocreate a service instance.</span></span> <span data-ttu-id="cd22b-137">Inicie sessão no toohello [Portal do Azure] [ Azure Portal] e clique em **novo**, **Web + móvel**, **API Management**.</span><span class="sxs-lookup"><span data-stu-id="cd22b-137">Sign in toohello [Azure Portal][Azure Portal] and click **New**, **Web + Mobile**, **API Management**.</span></span>

![Nova instância da API Management][api-management-create-instance-menu]

<span data-ttu-id="cd22b-139">Para **nome**, especifique um toouse de nome de subdomínio exclusivo para o URL do serviço Olá.</span><span class="sxs-lookup"><span data-stu-id="cd22b-139">For **Name**, specify a unique sub-domain name toouse for hello service URL.</span></span>

<span data-ttu-id="cd22b-140">Escolha Olá pretendido **subscrição**, **grupo de recursos** e **localização** para a instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="cd22b-140">Choose hello desired **Subscription**, **Resource group** and **Location** for your service instance.</span></span>

<span data-ttu-id="cd22b-141">Introduza **Contoso Lda.** para Olá **nome da organização**e introduza o seu endereço de e-mail no Olá **E-Mail do administrador** campo.</span><span class="sxs-lookup"><span data-stu-id="cd22b-141">Enter **Contoso Ltd.** for hello **Organization Name**, and enter your email address in hello **Administrator E-Mail** field.</span></span>

> [!NOTE]
> <span data-ttu-id="cd22b-142">Este endereço de correio eletrónico é utilizado para obter notificações do sistema de gestão de API de Olá.</span><span class="sxs-lookup"><span data-stu-id="cd22b-142">This email address is used for notifications from hello API Management system.</span></span> <span data-ttu-id="cd22b-143">Para obter mais informações, consulte [como tooconfigure notificações e modelos de e-mail na API Management do Azure][How tooconfigure notifications and email templates in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="cd22b-143">For more information, see [How tooconfigure notifications and email templates in Azure API Management][How tooconfigure notifications and email templates in Azure API Management].</span></span>
> 
> 

![Novo serviço da API Management][api-management-create-instance-step1]

<span data-ttu-id="cd22b-145">As instâncias do serviço de API Management estão disponíveis em três camadas: Programador, Standard e Premium.</span><span class="sxs-lookup"><span data-stu-id="cd22b-145">API Management service instances are available in three tiers: Developer, Standard, and Premium.</span></span>

> [!NOTE]
> <span data-ttu-id="cd22b-146">Olá camada de programador destina-se a desenvolvimento, teste e piloto programas de API em que a elevada disponibilidade não é uma preocupação.</span><span class="sxs-lookup"><span data-stu-id="cd22b-146">hello Developer Tier is for development, testing, and pilot API programs where high availability is not a concern.</span></span> <span data-ttu-id="cd22b-147">No Olá padrão e camadas Premium, pode dimensionar a sua toohandle de contagem de unidade reservada mais tráfego.</span><span class="sxs-lookup"><span data-stu-id="cd22b-147">In hello Standard and Premium tiers, you can scale your reserved unit count toohandle more traffic.</span></span> <span data-ttu-id="cd22b-148">camadas de Olá Standard e Premium fornecem o serviço de gestão de API com Olá mais potência de processamento e o desempenho.</span><span class="sxs-lookup"><span data-stu-id="cd22b-148">hello Standard and Premium tiers provide your API Management service with hello most processing power and performance.</span></span> <span data-ttu-id="cd22b-149">Pode concluir este tutorial utilizando qualquer camada.</span><span class="sxs-lookup"><span data-stu-id="cd22b-149">You can complete this tutorial by using any tier.</span></span> <span data-ttu-id="cd22b-150">Para obter mais informações sobre as camadas de Gestão de API, consulte [Preços da Gestão de API][API Management pricing].</span><span class="sxs-lookup"><span data-stu-id="cd22b-150">For more information about API Management tiers, see [API Management pricing][API Management pricing].</span></span>
> 
> 

<span data-ttu-id="cd22b-151">Clique em **criar** toostart aprovisionamento a instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="cd22b-151">Click **Create** toostart provisioning your service instance.</span></span>

![Novo serviço da API Management][api-management-instance-created]

<span data-ttu-id="cd22b-153">Uma vez criada a instância de serviço Olá, o passo seguinte Olá é toocreate ou importar uma API.</span><span class="sxs-lookup"><span data-stu-id="cd22b-153">Once hello service instance is created, hello next step is toocreate or import an API.</span></span>

## <span data-ttu-id="cd22b-154"><a name="create-api"> </a>Importar uma API</span><span class="sxs-lookup"><span data-stu-id="cd22b-154"><a name="create-api"> </a>Import an API</span></span>
<span data-ttu-id="cd22b-155">Uma API consiste num conjunto de operações que podem ser invocadas a partir de uma aplicação cliente.</span><span class="sxs-lookup"><span data-stu-id="cd22b-155">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="cd22b-156">Operações de API são efetuados tooexisting web.</span><span class="sxs-lookup"><span data-stu-id="cd22b-156">API operations are proxied tooexisting web services.</span></span>

<span data-ttu-id="cd22b-157">Pode criar APIs (e adicionar operações) manualmente ou pode importá-las.</span><span class="sxs-lookup"><span data-stu-id="cd22b-157">APIs can be created (and operations can be added) manually, or they can be imported.</span></span> <span data-ttu-id="cd22b-158">Neste tutorial, iremos importar Olá API para um serviço de web de Calculadora exemplo fornecido pela Microsoft e alojado no Azure.</span><span class="sxs-lookup"><span data-stu-id="cd22b-158">In this tutorial, we will import hello API for a sample calculator web service provided by Microsoft and hosted on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="cd22b-159">Para obter orientações sobre como criar uma API e adição manual de operações, consulte [como toocreate APIs](api-management-howto-create-apis.md) e [como tooadd operações tooan API](api-management-howto-add-operations.md).</span><span class="sxs-lookup"><span data-stu-id="cd22b-159">For guidance on creating an API and manually adding operations, see [How toocreate APIs](api-management-howto-create-apis.md) and [How tooadd operations tooan API](api-management-howto-add-operations.md).</span></span>
> 
> 

<span data-ttu-id="cd22b-160">As APIs são configuradas a partir do portal do publicador Olá.</span><span class="sxs-lookup"><span data-stu-id="cd22b-160">APIs are configured from hello publisher portal.</span></span> <span data-ttu-id="cd22b-161">tooreach, clique em **portal do publicador** da barra de ferramentas do Olá serviço.</span><span class="sxs-lookup"><span data-stu-id="cd22b-161">tooreach it, click **Publisher portal** from hello service toolbar.</span></span>

![Portal do publicador][api-management-management-console]

<span data-ttu-id="cd22b-163">Calculadora de Olá tooimport API, clique em **APIs** de Olá **API Management** menu Olá à esquerda e, em seguida, clique em **API de importação**.</span><span class="sxs-lookup"><span data-stu-id="cd22b-163">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![Botão Importar API][api-management-import-api]

<span data-ttu-id="cd22b-165">Execute os seguintes passos tooconfigure Olá API de calculadora de Olá:</span><span class="sxs-lookup"><span data-stu-id="cd22b-165">Perform hello following steps tooconfigure hello calculator API:</span></span>

1. <span data-ttu-id="cd22b-166">Clique em **de URL**, introduza **http://calcapi.cloudapp.net/calcapi.json** para Olá **URL de documento de especificação** texto caixa e clique em Olá **Swagger**  botão de opção.</span><span class="sxs-lookup"><span data-stu-id="cd22b-166">Click **From URL**, enter **http://calcapi.cloudapp.net/calcapi.json** into hello **Specification document URL** text box, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="cd22b-167">Tipo **calc** para Olá **sufixo do URL da API Web** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="cd22b-167">Type **calc** into hello **Web API URL suffix** text box.</span></span>
3. <span data-ttu-id="cd22b-168">Clique na Olá **produtos (opcionais)** caixa e escolha **Starter**.</span><span class="sxs-lookup"><span data-stu-id="cd22b-168">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="cd22b-169">Clique em **guardar** tooimport Olá API.</span><span class="sxs-lookup"><span data-stu-id="cd22b-169">Click **Save** tooimport hello API.</span></span>

![Adicionar nova API][api-management-import-new-api]

> [!NOTE]
> <span data-ttu-id="cd22b-171">A **API Management** suporta atualmente a versão 1.2 e 2.0 do documento Swagger para importação.</span><span class="sxs-lookup"><span data-stu-id="cd22b-171">**API Management** currently supports both 1.2 and 2.0 version of Swagger document for import.</span></span> <span data-ttu-id="cd22b-172">Embora a [Especificação Swagger 2.0](http://swagger.io/specification) declare que as propriedades `host`, `basePath` e `schemes` são opcionais, o documento Swagger 2.0 **DEVE** conter essas propriedades; caso contrário, não será importado.</span><span class="sxs-lookup"><span data-stu-id="cd22b-172">Make sure that, even though [Swagger 2.0 specification](http://swagger.io/specification) declares that `host`, `basePath`, and `schemes` properties are optional, your Swagger 2.0 document **MUST** contain those properties; otherwise it won't get imported.</span></span> 
> 
> 

<span data-ttu-id="cd22b-173">Depois de Olá API for importada, hello página de resumo para a API de Olá é apresentada no portal do publicador Olá.</span><span class="sxs-lookup"><span data-stu-id="cd22b-173">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

![Resumo da API][api-management-imported-api-summary]

<span data-ttu-id="cd22b-175">Olá secção API tem vários separadores.</span><span class="sxs-lookup"><span data-stu-id="cd22b-175">hello API section has several tabs.</span></span> <span data-ttu-id="cd22b-176">Olá **resumo** separador apresenta métricas e informações sobre Olá API básicas.</span><span class="sxs-lookup"><span data-stu-id="cd22b-176">hello **Summary** tab displays basic metrics and information about hello API.</span></span> <span data-ttu-id="cd22b-177">Olá [definições](api-management-howto-create-apis.md#configure-api-settings) separador utilizada tooview e editar Olá configuração é para uma API.</span><span class="sxs-lookup"><span data-stu-id="cd22b-177">hello [Settings](api-management-howto-create-apis.md#configure-api-settings) tab is used tooview and edit hello configuration for an API.</span></span> <span data-ttu-id="cd22b-178">Olá [operações](api-management-howto-add-operations.md) separador é operações Olá toomanage utilizados da API.</span><span class="sxs-lookup"><span data-stu-id="cd22b-178">hello [Operations](api-management-howto-add-operations.md) tab is used toomanage hello API's operations.</span></span> <span data-ttu-id="cd22b-179">Olá **segurança** separador pode ser tooconfigure utilizada a autenticação de gateway para o servidor de back-end Olá, utilizando a autenticação básica ou [autenticação de certificados mútuos](api-management-howto-mutual-certificates.md)e tooconfigure [ autorização do utilizador através da utilização de OAuth 2.0](api-management-howto-oauth2.md).</span><span class="sxs-lookup"><span data-stu-id="cd22b-179">hello **Security** tab can be used tooconfigure gateway authentication for hello backend server by using Basic authentication or [mutual certificate authentication](api-management-howto-mutual-certificates.md), and tooconfigure [user authorization by using OAuth 2.0](api-management-howto-oauth2.md).</span></span>  <span data-ttu-id="cd22b-180">Olá **problemas** separador é problemas de tooview utilizados comunicados pelos programadores Olá que estão a utilizar as suas APIs.</span><span class="sxs-lookup"><span data-stu-id="cd22b-180">hello **Issues** tab is used tooview issues reported by hello developers who are using your APIs.</span></span> <span data-ttu-id="cd22b-181">Olá **produtos** separador é produtos de Olá tooconfigure utilizados que contêm esta API.</span><span class="sxs-lookup"><span data-stu-id="cd22b-181">hello **Products** tab is used tooconfigure hello products that contain this API.</span></span>

<span data-ttu-id="cd22b-182">Por predefinição, cada instância daAPI Management é fornecida com dois produtos de exemplo:</span><span class="sxs-lookup"><span data-stu-id="cd22b-182">By default, each API Management instance comes with two sample products:</span></span>

* <span data-ttu-id="cd22b-183">**Inicial**</span><span class="sxs-lookup"><span data-stu-id="cd22b-183">**Starter**</span></span>
* <span data-ttu-id="cd22b-184">**Ilimitado**</span><span class="sxs-lookup"><span data-stu-id="cd22b-184">**Unlimited**</span></span>

<span data-ttu-id="cd22b-185">Neste tutorial, Olá API de calculadora básica foi adicionada toohello produto de arranque quando Olá API foi importada.</span><span class="sxs-lookup"><span data-stu-id="cd22b-185">In this tutorial, hello Basic Calculator API was added toohello Starter product when hello API was imported.</span></span>

<span data-ttu-id="cd22b-186">Na ordem toomake chamadas tooan API, os programadores têm primeiro de subscrever tooa produto que lhes dá acesso tooit.</span><span class="sxs-lookup"><span data-stu-id="cd22b-186">In order toomake calls tooan API, developers must first subscribe tooa product that gives them access tooit.</span></span> <span data-ttu-id="cd22b-187">Os programadores podem subscrever tooproducts no portal de programador hello, ou os administradores podem subscrever tooproducts os programadores no portal do publicador Olá.</span><span class="sxs-lookup"><span data-stu-id="cd22b-187">Developers can subscribe tooproducts in hello developer portal, or administrators can subscribe developers tooproducts in hello publisher portal.</span></span> <span data-ttu-id="cd22b-188">É um administrador, uma vez que criou instância da API Management Olá no Olá passos anteriores no tutorial Olá, pelo que já são tooevery subscrito produto por predefinição.</span><span class="sxs-lookup"><span data-stu-id="cd22b-188">You are an administrator since you created hello API Management instance in hello previous steps in hello tutorial, so you are already subscribed tooevery product by default.</span></span>

## <span data-ttu-id="cd22b-189"><a name="call-operation"></a>Chamar uma operação a partir do portal de programador Olá</span><span class="sxs-lookup"><span data-stu-id="cd22b-189"><a name="call-operation"> </a>Call an operation from hello developer portal</span></span>
<span data-ttu-id="cd22b-190">As operações podem ser chamadas diretamente a partir do portal do programador Olá, que fornece uma maneira conveniente tooview e operações de Olá de uma API de teste.</span><span class="sxs-lookup"><span data-stu-id="cd22b-190">Operations can be called directly from hello developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="cd22b-191">Este passo do tutorial, irá chamar Olá API de calculadora básica **adicionar dois números inteiros** operação.</span><span class="sxs-lookup"><span data-stu-id="cd22b-191">In this tutorial step, you will call hello Basic Calculator API's **Add two integers** operation.</span></span> <span data-ttu-id="cd22b-192">Clique em **portal do programador** a partir do menu de Olá em Olá principais direita do portal do publicador Olá.</span><span class="sxs-lookup"><span data-stu-id="cd22b-192">Click **Developer portal** from hello menu at hello top right of hello publisher portal.</span></span>

![Portal do programador][api-management-developer-portal-menu]

<span data-ttu-id="cd22b-194">Clique em **APIs** do menu superior Olá e, em seguida, clique em **calculadora básica** toosee Olá operações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="cd22b-194">Click **APIs** from hello top menu, and then click **Basic Calculator** toosee hello available operations.</span></span>

![Portal do programador][api-management-developer-portal-calc-api]

<span data-ttu-id="cd22b-196">Tenha em atenção as descrições de exemplo de Olá e os parâmetros que foram importados juntamente com Olá API e operações, que proporcionam documentação para programadores de Olá que irá utilizar esta operação.</span><span class="sxs-lookup"><span data-stu-id="cd22b-196">Note hello sample descriptions and parameters that were imported along with hello API and operations, providing documentation for hello developers that will use this operation.</span></span> <span data-ttu-id="cd22b-197">Estas descrições também podem ser adicionadas quando as operações são adicionadas manualmente.</span><span class="sxs-lookup"><span data-stu-id="cd22b-197">These descriptions can also be added when operations are added manually.</span></span>

<span data-ttu-id="cd22b-198">Olá toocall **adicionar dois números inteiros** operação, clique em **experimente**.</span><span class="sxs-lookup"><span data-stu-id="cd22b-198">toocall hello **Add two integers** operation, click **Try it**.</span></span>

![Experimente][api-management-developer-portal-calc-api-console]

<span data-ttu-id="cd22b-200">Pode introduzir alguns valores para parâmetros de Olá ou mantenha as predefinições de Olá e, em seguida, clique em **enviar**.</span><span class="sxs-lookup"><span data-stu-id="cd22b-200">You can enter some values for hello parameters or keep hello defaults, and then click **Send**.</span></span>

![HTTP Get][api-management-invoke-get]

<span data-ttu-id="cd22b-202">Após uma operação ser invocada, o portal do programador Olá apresenta Olá **estado de resposta**, Olá **cabeçalhos de resposta**e quaisquer **conteúdo da resposta**.</span><span class="sxs-lookup"><span data-stu-id="cd22b-202">After an operation is invoked, hello developer portal displays hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![Resposta][api-management-invoke-get-response]

## <span data-ttu-id="cd22b-204"><a name="view-analytics"> </a>Ver análise</span><span class="sxs-lookup"><span data-stu-id="cd22b-204"><a name="view-analytics"> </a>View analytics</span></span>
<span data-ttu-id="cd22b-205">análise de tooview da calculadora básica, comutador back toohello portal do publicador ao selecionar **gerir** a partir do menu de Olá em Olá principais à direita do portal de programador Olá.</span><span class="sxs-lookup"><span data-stu-id="cd22b-205">tooview analytics for Basic Calculator, switch back toohello publisher portal by selecting **Manage** from hello menu at hello top right of hello developer portal.</span></span>

![Gerir][api-management-manage-menu]

<span data-ttu-id="cd22b-207">Olá vista predefinida para o portal do publicador Olá é Olá **Dashboard**, que fornece uma descrição geral da sua instância da API Management.</span><span class="sxs-lookup"><span data-stu-id="cd22b-207">hello default view for hello publisher portal is hello **Dashboard**, which provides an overview of your API Management instance.</span></span>

![Dashboard][api-management-dashboard]

<span data-ttu-id="cd22b-209">Rato de Olá paire sobre gráfico Olá para **calculadora básica** toosee métricas específicas de Olá da utilização de Olá do Olá API para um determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="cd22b-209">Hover hello mouse over hello chart for **Basic Calculator** toosee hello specific metrics for hello usage of hello API for a given time period.</span></span>

> [!NOTE]
> <span data-ttu-id="cd22b-210">Se não vir quaisquer linhas no gráfico, mudar o portal do Programador de back-toohello e efetue algumas chamadas à API de Olá, aguarde alguns instantes e, em seguida, voltar toohello dashboard.</span><span class="sxs-lookup"><span data-stu-id="cd22b-210">If you don't see any lines on your chart, switch back toohello developer portal and make some calls into hello API, wait a few moments, and then come back toohello dashboard.</span></span>
> 
> 

<span data-ttu-id="cd22b-211">Clique em **ver detalhes** tooview Olá página de resumo Olá API, incluindo uma versão maior das métricas de Olá apresentado.</span><span class="sxs-lookup"><span data-stu-id="cd22b-211">Click **View Details** tooview hello summary page for hello API, including a larger version of hello displayed metrics.</span></span>

![Análise][api-management-mouse-over]

![Resumo][api-management-api-summary-metrics]

<span data-ttu-id="cd22b-214">Para métricas e relatórios detalhados, clique em **análise** de Olá **API Management** menu Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="cd22b-214">For detailed metrics and reports, click **Analytics** from hello **API Management** menu on hello left.</span></span>

![Descrição geral][api-management-analytics-overview]

<span data-ttu-id="cd22b-216">Olá **análise** secção tem Olá seguintes quatro separadores:</span><span class="sxs-lookup"><span data-stu-id="cd22b-216">hello **Analytics** section has hello following four tabs:</span></span>

* <span data-ttu-id="cd22b-217">**Rapidamente** fornece utilização global e métricas de estado de funcionamento, bem como Olá principais programadores, principais produtos, as principais APIs e operações superiores.</span><span class="sxs-lookup"><span data-stu-id="cd22b-217">**At a glance** provides overall usage and health metrics, as well as hello top developers, top products, top APIs, and top operations.</span></span>
* <span data-ttu-id="cd22b-218">**Utilização** fornece uma visão detalhada das chamadas à API e da largura de banda, incluindo uma representação geográfica.</span><span class="sxs-lookup"><span data-stu-id="cd22b-218">**Usage** provides an in-depth look at API calls and bandwidth, including a geographical representation.</span></span>
* <span data-ttu-id="cd22b-219">**Estado de funcionamento** concentra-se em códigos de estado, taxas de êxito de colocação em cache, tempos de resposta e tempos de resposta da API e do serviço.</span><span class="sxs-lookup"><span data-stu-id="cd22b-219">**Health** focuses on status codes, cache success rates, response times, and API and service response times.</span></span>
* <span data-ttu-id="cd22b-220">**Atividade** fornece relatórios detalhados sobre a atividade específica do Olá por programador, produto, API e operação.</span><span class="sxs-lookup"><span data-stu-id="cd22b-220">**Activity** provides reports that drill down on hello specific activity by developer, product, API, and operation.</span></span>

## <span data-ttu-id="cd22b-221"><a name="next-steps"> </a>Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="cd22b-221"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="cd22b-222">Saiba como demasiado[proteger a sua API com limites de velocidade](api-management-howto-product-with-rules.md).</span><span class="sxs-lookup"><span data-stu-id="cd22b-222">Learn how too[Protect your API with rate limits](api-management-howto-product-with-rules.md).</span></span>

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
