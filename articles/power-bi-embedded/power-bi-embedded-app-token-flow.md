---
title: "aaaAuthenticating e autorização com Power BI Embedded"
description: "Autenticação e autorização com Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a><span data-ttu-id="6b976-103">Autenticação e autorização com Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="6b976-103">Authenticating and authorizing with Power BI Embedded</span></span>

<span data-ttu-id="6b976-104">Olá serviço Power BI Embedded utiliza **chaves** e **Tokens de aplicação** para autenticação e autorização, em vez de autenticação de utilizador final explícita.</span><span class="sxs-lookup"><span data-stu-id="6b976-104">hello Power BI Embedded service uses **Keys** and **App Tokens** for authentication and authorization, instead of explicit end-user authentication.</span></span> <span data-ttu-id="6b976-105">Neste modelo, a sua aplicação gere autenticação e autorização para os utilizadores finais.</span><span class="sxs-lookup"><span data-stu-id="6b976-105">In this model, your application manages authentication and authorization for your end-users.</span></span> <span data-ttu-id="6b976-106">Quando for necessário, a sua aplicação cria e envia os Tokens de aplicação Olá que diz ao nosso serviço toorender Olá relatório pedido.</span><span class="sxs-lookup"><span data-stu-id="6b976-106">When necessary, your app creates and sends hello App Tokens that tells our service toorender hello requested report.</span></span> <span data-ttu-id="6b976-107">Esta estrutura não requer o toouse de aplicação do Azure Active Directory para autenticação de utilizador e a autorização, embora ainda possa.</span><span class="sxs-lookup"><span data-stu-id="6b976-107">This design doesn't require your app toouse Azure Active Directory for user authentication and authorization, although you still can.</span></span>

## <a name="two-ways-tooauthenticate"></a><span data-ttu-id="6b976-108">Duas formas tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="6b976-108">Two ways tooauthenticate</span></span>

<span data-ttu-id="6b976-109">**Chave** -pode utilizar as chaves para todas as chamadas da API de REST do Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="6b976-109">**Key** -  You can use keys for all Power BI Embedded REST API calls.</span></span> <span data-ttu-id="6b976-110">podem encontrar chaves Olá Olá **portal do Azure** ao clicar no **todas as definições** e, em seguida, **chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="6b976-110">hello keys can be found in hello **Azure portal** by clicking on **All settings** and then **Access keys**.</span></span> <span data-ttu-id="6b976-111">Trate sempre a sua chave como se fosse uma palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="6b976-111">Always treat your key as if it were a password.</span></span> <span data-ttu-id="6b976-112">Estas chaves tem toomake permissões chamar qualquer API de REST de uma coleção de área de trabalho específica.</span><span class="sxs-lookup"><span data-stu-id="6b976-112">These keys have permissions toomake any REST API call on a particular workspace collection.</span></span>

<span data-ttu-id="6b976-113">toouse uma chave de uma chamada REST, adicione Olá cabeçalho de autorização os seguintes:</span><span class="sxs-lookup"><span data-stu-id="6b976-113">toouse a key on a REST call, add hello following authorization header:</span></span>            

    Authorization: AppKey {your key}

<span data-ttu-id="6b976-114">**Token de aplicação** -tokens de aplicação são utilizados para todos os pedidos embedding.</span><span class="sxs-lookup"><span data-stu-id="6b976-114">**App token** - App tokens are used for all embedding requests.</span></span> <span data-ttu-id="6b976-115">Estiverem toobe concebida executar lado do cliente, pelo que estes restritos tooa único relatório e de melhores práticas tooset uma hora de expiração.</span><span class="sxs-lookup"><span data-stu-id="6b976-115">They’re designed toobe run client-side, so they're restricted tooa single report and it’s best practice tooset an expiration time.</span></span>

<span data-ttu-id="6b976-116">Os tokens de aplicação são um JWT (JSON Web Token) que esteja assinado por uma das suas chaves.</span><span class="sxs-lookup"><span data-stu-id="6b976-116">App tokens are a JWT (JSON Web Token) that is signed by one of your keys.</span></span>

<span data-ttu-id="6b976-117">O token de aplicação pode conter Olá afirmações os seguintes:</span><span class="sxs-lookup"><span data-stu-id="6b976-117">Your app token can contain hello following claims:</span></span>

| <span data-ttu-id="6b976-118">Afirmação</span><span class="sxs-lookup"><span data-stu-id="6b976-118">Claim</span></span> | <span data-ttu-id="6b976-119">Descrição</span><span class="sxs-lookup"><span data-stu-id="6b976-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6b976-120">**ver**</span><span class="sxs-lookup"><span data-stu-id="6b976-120">**ver**</span></span> |<span data-ttu-id="6b976-121">versão de Olá do token da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="6b976-121">hello version of hello app token.</span></span> <span data-ttu-id="6b976-122">0.2.0 é a versão atual do Olá.</span><span class="sxs-lookup"><span data-stu-id="6b976-122">0.2.0 is hello current version.</span></span> |
| <span data-ttu-id="6b976-123">**aud**</span><span class="sxs-lookup"><span data-stu-id="6b976-123">**aud**</span></span> |<span data-ttu-id="6b976-124">Olá destina-se o destinatário do token de Olá.</span><span class="sxs-lookup"><span data-stu-id="6b976-124">hello intended recipient of hello token.</span></span> <span data-ttu-id="6b976-125">Para utilização do Power BI Embedded: "https://analysis.windows.net/powerbi/api".</span><span class="sxs-lookup"><span data-stu-id="6b976-125">For Power BI Embedded use: “https://analysis.windows.net/powerbi/api”.</span></span> |
| <span data-ttu-id="6b976-126">**ISS**</span><span class="sxs-lookup"><span data-stu-id="6b976-126">**iss**</span></span> |<span data-ttu-id="6b976-127">Uma cadeia que indica que a aplicação Olá que emitiu o token de Olá.</span><span class="sxs-lookup"><span data-stu-id="6b976-127">A string indicating hello application which issued hello token.</span></span> |
| <span data-ttu-id="6b976-128">**tipo**</span><span class="sxs-lookup"><span data-stu-id="6b976-128">**type**</span></span> |<span data-ttu-id="6b976-129">tipo de Olá de token de aplicação que está a ser criada.</span><span class="sxs-lookup"><span data-stu-id="6b976-129">hello type of app token which is being created.</span></span> <span data-ttu-id="6b976-130">Tipo de Olá só suportada atual é **incorporar**.</span><span class="sxs-lookup"><span data-stu-id="6b976-130">Current hello only supported type is **embed**.</span></span> |
| <span data-ttu-id="6b976-131">**WCN**</span><span class="sxs-lookup"><span data-stu-id="6b976-131">**wcn**</span></span> |<span data-ttu-id="6b976-132">Token de Olá de nome de coleção de área de trabalho está a ser emitido para.</span><span class="sxs-lookup"><span data-stu-id="6b976-132">Workspace collection name hello token is being issued for.</span></span> |
| <span data-ttu-id="6b976-133">**WID**</span><span class="sxs-lookup"><span data-stu-id="6b976-133">**wid**</span></span> |<span data-ttu-id="6b976-134">Token de Olá de ID de área de trabalho está a ser emitidos para.</span><span class="sxs-lookup"><span data-stu-id="6b976-134">Workspace ID hello token is being issued for.</span></span> |
| <span data-ttu-id="6b976-135">**RID**</span><span class="sxs-lookup"><span data-stu-id="6b976-135">**rid**</span></span> |<span data-ttu-id="6b976-136">Token de Olá de ID do relatório está a ser emitidos para.</span><span class="sxs-lookup"><span data-stu-id="6b976-136">Report ID hello token is being issued for.</span></span> |
| <span data-ttu-id="6b976-137">**nome de utilizador** (opcional)</span><span class="sxs-lookup"><span data-stu-id="6b976-137">**username** (optional)</span></span> |<span data-ttu-id="6b976-138">Utilizado com RLS, esta é uma cadeia que pode ajudar a identificar o utilizador Olá ao aplicar regras RLS.</span><span class="sxs-lookup"><span data-stu-id="6b976-138">Used with RLS, this is a string that can help identify hello user when applying RLS rules.</span></span> |
| <span data-ttu-id="6b976-139">**funções** (opcional)</span><span class="sxs-lookup"><span data-stu-id="6b976-139">**roles** (optional)</span></span> |<span data-ttu-id="6b976-140">Uma cadeia que contém Olá funções tooselect ao aplicar regras de segurança de nível de linha.</span><span class="sxs-lookup"><span data-stu-id="6b976-140">A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="6b976-141">Se a transmitir mais de uma função, deve ser transmitidas como uma matriz de sting.</span><span class="sxs-lookup"><span data-stu-id="6b976-141">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="6b976-142">**SCP** (opcional)</span><span class="sxs-lookup"><span data-stu-id="6b976-142">**scp** (optional)</span></span> |<span data-ttu-id="6b976-143">Uma cadeia contendo âmbitos de permissões de Olá.</span><span class="sxs-lookup"><span data-stu-id="6b976-143">A string containing hello permissions scopes.</span></span> <span data-ttu-id="6b976-144">Se a transmitir mais de uma função, deve ser transmitidas como uma matriz de sting.</span><span class="sxs-lookup"><span data-stu-id="6b976-144">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="6b976-145">**EXP** (opcional)</span><span class="sxs-lookup"><span data-stu-id="6b976-145">**exp** (optional)</span></span> |<span data-ttu-id="6b976-146">Indica o tempo de Olá no qual Olá token irá expirar.</span><span class="sxs-lookup"><span data-stu-id="6b976-146">Indicates hello time in which hello token will expire.</span></span> <span data-ttu-id="6b976-147">Estas devem ser transmitidas como carimbos de Unix.</span><span class="sxs-lookup"><span data-stu-id="6b976-147">These should be passed in as Unix timestamps.</span></span> |
| <span data-ttu-id="6b976-148">**NBF** (opcional)</span><span class="sxs-lookup"><span data-stu-id="6b976-148">**nbf** (optional)</span></span> |<span data-ttu-id="6b976-149">Indica o tempo de Olá que Olá token começa a ser válido.</span><span class="sxs-lookup"><span data-stu-id="6b976-149">Indicates hello time in which hello token starts being valid.</span></span> <span data-ttu-id="6b976-150">Estas devem ser transmitidas como carimbos de Unix.</span><span class="sxs-lookup"><span data-stu-id="6b976-150">These should be passed in as Unix timestamps.</span></span> |

<span data-ttu-id="6b976-151">Um token de aplicação de exemplo irá ter este aspeto:</span><span class="sxs-lookup"><span data-stu-id="6b976-151">A sample app token will look like this:</span></span>

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

<span data-ttu-id="6b976-152">Quando descodificar, irá procurar algo semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="6b976-152">When decoded, it will look something like this:</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

<span data-ttu-id="6b976-153">Existem métodos disponíveis dentro de Olá SDKs que o facilitar a criação de apptokens.</span><span class="sxs-lookup"><span data-stu-id="6b976-153">There are methods available within hello SDKs that make creation of apptokens easier.</span></span> <span data-ttu-id="6b976-154">Por exemplo, para o .NET pode examinar Olá [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) classe e Olá [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) métodos.</span><span class="sxs-lookup"><span data-stu-id="6b976-154">For example, for .NET you can look at hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) class and hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methods.</span></span>

<span data-ttu-id="6b976-155">Para o .NET SDK Olá, pode fazer referência demasiado[âmbitos](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span><span class="sxs-lookup"><span data-stu-id="6b976-155">For hello .NET SDK, you can refer too[Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span></span>

## <a name="scopes"></a><span data-ttu-id="6b976-156">âmbitos</span><span class="sxs-lookup"><span data-stu-id="6b976-156">Scopes</span></span>

<span data-ttu-id="6b976-157">Quando a utilização de tokens de incorporação, poderá pretender toorestrict utilização dos recursos de Olá que conceder acesso.</span><span class="sxs-lookup"><span data-stu-id="6b976-157">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="6b976-158">Por este motivo, pode gerar um token com permissões com âmbito definido.</span><span class="sxs-lookup"><span data-stu-id="6b976-158">For this reason, you can generate a token with scoped permissions.</span></span>

<span data-ttu-id="6b976-159">Olá seguem-se âmbitos disponíveis de Olá para Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="6b976-159">hello following are hello available scopes for Power BI Embedded.</span></span>

|<span data-ttu-id="6b976-160">Âmbito</span><span class="sxs-lookup"><span data-stu-id="6b976-160">Scope</span></span>|<span data-ttu-id="6b976-161">Descrição</span><span class="sxs-lookup"><span data-stu-id="6b976-161">Description</span></span>|
|---|---|
|<span data-ttu-id="6b976-162">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="6b976-162">Dataset.Read</span></span>|<span data-ttu-id="6b976-163">Fornece a permissão tooread Olá especificado o conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="6b976-163">Provides permission tooread hello specified dataset.</span></span>|
|<span data-ttu-id="6b976-164">Dataset.Write</span><span class="sxs-lookup"><span data-stu-id="6b976-164">Dataset.Write</span></span>|<span data-ttu-id="6b976-165">Fornece a permissão toowrite toohello especificado conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="6b976-165">Provides permission toowrite toohello specified dataset.</span></span>|
|<span data-ttu-id="6b976-166">Dataset.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="6b976-166">Dataset.ReadWrite</span></span>|<span data-ttu-id="6b976-167">Fornece a permissão tooread e escrita toohello especificado conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="6b976-167">Provides permission tooread and write toohello specificed dataset.</span></span>|
|<span data-ttu-id="6b976-168">Report.Read</span><span class="sxs-lookup"><span data-stu-id="6b976-168">Report.Read</span></span>|<span data-ttu-id="6b976-169">Fornece a permissão tooview Olá especificado relatório.</span><span class="sxs-lookup"><span data-stu-id="6b976-169">Provides permission tooview hello specified report.</span></span>|
|<span data-ttu-id="6b976-170">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="6b976-170">Report.ReadWrite</span></span>|<span data-ttu-id="6b976-171">Fornece a permissão tooview e editar Olá relatório especificado.</span><span class="sxs-lookup"><span data-stu-id="6b976-171">Provides permission tooview and edit hello specified report.</span></span>|
|<span data-ttu-id="6b976-172">Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="6b976-172">Workspace.Report.Create</span></span>|<span data-ttu-id="6b976-173">Fornece um novo relatório no Olá especificado de permissão toocreate área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6b976-173">Provides permission toocreate a new report within hello specified workspace.</span></span>|
|<span data-ttu-id="6b976-174">Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="6b976-174">Workspace.Report.Copy</span></span>|<span data-ttu-id="6b976-175">Fornece um relatório existente no Olá especificado de permissão tooclone área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6b976-175">Provides permission tooclone an existing report within hello specified workspace.</span></span>|

<span data-ttu-id="6b976-176">Pode fornecer vários âmbitos utilizando um espaço entre os âmbitos de Olá semelhante Olá seguinte.</span><span class="sxs-lookup"><span data-stu-id="6b976-176">You can supply multiple scopes by using a space between hello scopes like hello following.</span></span>

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

<span data-ttu-id="6b976-177">**Afirmações necessárias - âmbitos**</span><span class="sxs-lookup"><span data-stu-id="6b976-177">**Required claims - scopes**</span></span>

<span data-ttu-id="6b976-178">SCP: {scopesClaim} scopesClaim pode ser uma cadeia ou matriz de cadeias, salientar Olá permitido permissões tooworkspace recursos (relatório, conjunto de dados, etc.)</span><span class="sxs-lookup"><span data-stu-id="6b976-178">scp: {scopesClaim} scopesClaim can be either a string or array of strings, noting hello allowed permissions tooworkspace resources (Report, Dataset, etc.)</span></span>

<span data-ttu-id="6b976-179">Um token descodificado, com âmbitos definido, seria ter um aspeto semelhante toohello seguinte.</span><span class="sxs-lookup"><span data-stu-id="6b976-179">A decoded token, with scopes defined, would look similar toohello following.</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a><span data-ttu-id="6b976-180">Operações e âmbitos</span><span class="sxs-lookup"><span data-stu-id="6b976-180">Operations and scopes</span></span>

|<span data-ttu-id="6b976-181">Operação</span><span class="sxs-lookup"><span data-stu-id="6b976-181">Operation</span></span>|<span data-ttu-id="6b976-182">Recurso de destino</span><span class="sxs-lookup"><span data-stu-id="6b976-182">Target resource</span></span>|<span data-ttu-id="6b976-183">Permissões de token</span><span class="sxs-lookup"><span data-stu-id="6b976-183">Token permissions</span></span>|
|---|---|---|
|<span data-ttu-id="6b976-184">Crie um novo relatório com base num conjunto de dados de (na memória).</span><span class="sxs-lookup"><span data-stu-id="6b976-184">Create (in-memory) a new report based on a dataset.</span></span>|<span data-ttu-id="6b976-185">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="6b976-185">Dataset</span></span>|<span data-ttu-id="6b976-186">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="6b976-186">Dataset.Read</span></span>|
|<span data-ttu-id="6b976-187">Criar um novo relatório com base num conjunto de dados de (na memória) e guarde o relatório de Olá.</span><span class="sxs-lookup"><span data-stu-id="6b976-187">Create (in-memory) a new report based on a dataset and save hello report.</span></span>|<span data-ttu-id="6b976-188">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="6b976-188">Dataset</span></span>|<span data-ttu-id="6b976-189">* Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="6b976-189">* Dataset.Read</span></span><br><span data-ttu-id="6b976-190">* Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="6b976-190">* Workspace.Report.Create</span></span>|
|<span data-ttu-id="6b976-191">Visualize e explore/Editar (na memória) um relatório existente.</span><span class="sxs-lookup"><span data-stu-id="6b976-191">View and explore/edit (in-memory) an existing report.</span></span> <span data-ttu-id="6b976-192">Report.Read implica Dataset.Read.</span><span class="sxs-lookup"><span data-stu-id="6b976-192">Report.Read implies Dataset.Read.</span></span> <span data-ttu-id="6b976-193">Isto permitirá não permissões toosave edições.</span><span class="sxs-lookup"><span data-stu-id="6b976-193">This will not allow permissions toosave edits.</span></span>|<span data-ttu-id="6b976-194">Relatório</span><span class="sxs-lookup"><span data-stu-id="6b976-194">Report</span></span>|<span data-ttu-id="6b976-195">Report.Read</span><span class="sxs-lookup"><span data-stu-id="6b976-195">Report.Read</span></span>|
|<span data-ttu-id="6b976-196">Editar e guardar um relatório existente.</span><span class="sxs-lookup"><span data-stu-id="6b976-196">Edit and save an existing report.</span></span>|<span data-ttu-id="6b976-197">Relatório</span><span class="sxs-lookup"><span data-stu-id="6b976-197">Report</span></span>|<span data-ttu-id="6b976-198">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="6b976-198">Report.ReadWrite</span></span>|
|<span data-ttu-id="6b976-199">Guarde uma cópia de um relatório (Guardar como).</span><span class="sxs-lookup"><span data-stu-id="6b976-199">Save a copy of a report (Save As).</span></span>|<span data-ttu-id="6b976-200">Relatório</span><span class="sxs-lookup"><span data-stu-id="6b976-200">Report</span></span>|<span data-ttu-id="6b976-201">* Report.Read</span><span class="sxs-lookup"><span data-stu-id="6b976-201">* Report.Read</span></span><br><span data-ttu-id="6b976-202">* Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="6b976-202">* Workspace.Report.Copy</span></span>|

## <a name="heres-how-hello-flow-works"></a><span data-ttu-id="6b976-203">Eis como funciona o fluxo de Olá</span><span class="sxs-lookup"><span data-stu-id="6b976-203">Here's how hello flow works</span></span>
1. <span data-ttu-id="6b976-204">Copie a aplicação de tooyour de chaves de API Olá.</span><span class="sxs-lookup"><span data-stu-id="6b976-204">Copy hello API keys tooyour application.</span></span> <span data-ttu-id="6b976-205">Pode obter chaves Olá em **Portal do Azure**.</span><span class="sxs-lookup"><span data-stu-id="6b976-205">You can get hello keys in **Azure Portal**.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. <span data-ttu-id="6b976-206">Token de asserções uma afirmação e tem um período de tempo de expiração.</span><span class="sxs-lookup"><span data-stu-id="6b976-206">Token asserts a claim and has an expiration time.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. <span data-ttu-id="6b976-207">Token obtém assinado com chaves de acesso da API.</span><span class="sxs-lookup"><span data-stu-id="6b976-207">Token gets signed with an API access keys.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. <span data-ttu-id="6b976-208">O utilizador solicita tooview um relatório.</span><span class="sxs-lookup"><span data-stu-id="6b976-208">User requests tooview a report.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. <span data-ttu-id="6b976-209">Token é validado com um chaves de acesso da API.</span><span class="sxs-lookup"><span data-stu-id="6b976-209">Token is validated with an API access keys.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. <span data-ttu-id="6b976-210">Power BI Embedded, envia um toouser de relatório.</span><span class="sxs-lookup"><span data-stu-id="6b976-210">Power BI Embedded sends a report toouser.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

<span data-ttu-id="6b976-211">Depois de **Power BI Embedded** envia um utilizador de toohello do relatório, utilizador de Olá pode ver o relatório de Olá na sua aplicação personalizada.</span><span class="sxs-lookup"><span data-stu-id="6b976-211">After **Power BI Embedded** sends a report toohello user, hello user can view hello report in your custom app.</span></span> <span data-ttu-id="6b976-212">Por exemplo, se importar Olá [exemplo analisar PBIX de dados de vendas](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), aplicação de web de exemplo de Olá deverá ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="6b976-212">For example, if you imported hello [Analyzing Sales Data PBIX sample](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a><span data-ttu-id="6b976-213">Veja Também</span><span class="sxs-lookup"><span data-stu-id="6b976-213">See Also</span></span>

[<span data-ttu-id="6b976-214">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="6b976-214">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="6b976-215">Introdução ao exemplo do Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="6b976-215">Get started with Microsoft Power BI Embedded sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="6b976-216">Cenários comuns do Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="6b976-216">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="6b976-217">Introdução ao Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="6b976-217">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)  
[<span data-ttu-id="6b976-218">Repositório de Git do PowerBI CSharp</span><span class="sxs-lookup"><span data-stu-id="6b976-218">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
<span data-ttu-id="6b976-219">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="6b976-219">More questions?</span></span> [<span data-ttu-id="6b976-220">Tente Olá da Comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="6b976-220">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

