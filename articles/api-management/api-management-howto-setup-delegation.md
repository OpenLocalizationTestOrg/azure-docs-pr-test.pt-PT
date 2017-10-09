---
title: "aaaHow toodelegate utilizador produto e registo de subscrição"
description: "Saiba como toodelegate utilizador registo e o produto da subscrição tooa de terceiros na API Management do Azure."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a><span data-ttu-id="4d295-103">Como toodelegate de subscrição de produto e registo de utilizador</span><span class="sxs-lookup"><span data-stu-id="4d295-103">How toodelegate user registration and product subscription</span></span>
<span data-ttu-id="4d295-104">Delegação permite-lhe toouse seu Web site existente para processar tooproducts de início de sessão-na/sessão-up e uma subscrição de programador como opposed toousing Olá uma funcionalidade incorporada no portal de programador Olá.</span><span class="sxs-lookup"><span data-stu-id="4d295-104">Delegation allows you toouse your existing website for handling developer sign-in/sign-up and subscription tooproducts as opposed toousing hello built-in functionality in hello developer portal.</span></span> <span data-ttu-id="4d295-105">Isto permite que os dados de utilizador do Web site tooown Olá e efetuar a validação de Olá destes passos de uma forma personalizada.</span><span class="sxs-lookup"><span data-stu-id="4d295-105">This enables your website tooown hello user data and perform hello validation of these steps in a custom way.</span></span>

## <span data-ttu-id="4d295-106"><a name="delegate-signin-up"></a>Delegating programador início de sessão e inscrição</span><span class="sxs-lookup"><span data-stu-id="4d295-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="4d295-107">toodelegate programador tooyour de início de sessão e inscrição Web site existente, terá de toocreate um ponto final de delegação especial no seu site que age como Olá ponto de entrada para esse pedido de iniciadas a partir do portal do programador Olá API Management.</span><span class="sxs-lookup"><span data-stu-id="4d295-107">toodelegate developer sign-in and sign-up tooyour existing website you will need toocreate a special delegation endpoint on your site that acts as hello entry-point for any such request initiated from hello API Management developer portal.</span></span>

<span data-ttu-id="4d295-108">fluxo de trabalho final Olá será o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4d295-108">hello final workflow will be as follows:</span></span>

1. <span data-ttu-id="4d295-109">Programador clica na ligação de início de sessão ou inscrição de Olá em Olá portal do Programador de API Management</span><span class="sxs-lookup"><span data-stu-id="4d295-109">Developer clicks on hello sign-in or sign-up link at hello API Management developer portal</span></span>
2. <span data-ttu-id="4d295-110">Browser é o ponto final de delegação toohello redirecionada</span><span class="sxs-lookup"><span data-stu-id="4d295-110">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="4d295-111">Ponto final de delegação no return redireciona tooor apresenta IU perguntar utilizador toosign ou no inscrição</span><span class="sxs-lookup"><span data-stu-id="4d295-111">Delegation endpoint in return redirects tooor presents UI asking user toosign-in or sign-up</span></span>
4. <span data-ttu-id="4d295-112">Com êxito, o utilizador Olá é redirecionada toohello back-API Management programador portal página iniciadas a partir do</span><span class="sxs-lookup"><span data-stu-id="4d295-112">On success, hello user is redirected back toohello API Management developer portal page they started from</span></span>

<span data-ttu-id="4d295-113">toobegin, vamos primeiro tooroute de gestão de API de configuração pedidos através do seu ponto final de delegação.</span><span class="sxs-lookup"><span data-stu-id="4d295-113">toobegin, let's first set-up API Management tooroute requests via your delegation endpoint.</span></span> <span data-ttu-id="4d295-114">No portal do publicador da API Management Olá, clique em **segurança** e, em seguida, clique em Olá **delegação** separador. Clique em Olá caixa de verificação tooenable 'Delegate início de sessão e inscrição'.</span><span class="sxs-lookup"><span data-stu-id="4d295-114">In hello API Management publisher portal, click on **Security** and then click hello **Delegation** tab. Click hello checkbox tooenable 'Delegate sign-in & sign-up'.</span></span>

![Página de delegação][api-management-delegation-signin-up]

* <span data-ttu-id="4d295-116">Decidir que Olá URL do seu ponto final de delegação especial será e introduza-o no Olá **URL de ponto final de delegação** campo.</span><span class="sxs-lookup"><span data-stu-id="4d295-116">Decide what hello URL of your special delegation endpoint will be and enter it in hello **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="4d295-117">Dentro do Olá **chave de autenticação de delegação** campo introduza um segredo que será utilizado toocompute tooyou uma assinatura fornecida para verificação tooensure que Olá pedido realmente for proveniente de API Management do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d295-117">Within hello **Delegation authentication key** field enter a secret that will be used toocompute a signature provided tooyou for verification tooensure that hello request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="4d295-118">Pode clicar em Olá **gerar** botão toohave gestão de API gerar aleatoriamente uma chave para si.</span><span class="sxs-lookup"><span data-stu-id="4d295-118">You can click hello **generate** button toohave API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="4d295-119">Agora tem toocreate Olá **ponto final de delegação**.</span><span class="sxs-lookup"><span data-stu-id="4d295-119">Now you need toocreate hello **delegation endpoint**.</span></span> <span data-ttu-id="4d295-120">Tooperform é tem um número de ações:</span><span class="sxs-lookup"><span data-stu-id="4d295-120">It has tooperform a number of actions:</span></span>

1. <span data-ttu-id="4d295-121">Receba um pedido no Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="4d295-121">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="4d295-122">*http://www.yourwebsite.com/apimdelegation?Operation=SignIn&returnUrl= {URL da página de origem} & salt = {cadeia} & sig = {cadeia}*</span><span class="sxs-lookup"><span data-stu-id="4d295-122">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="4d295-123">Parâmetros de consulta para o caso de início de sessão / inscrição Olá:</span><span class="sxs-lookup"><span data-stu-id="4d295-123">Query parameters for hello sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="4d295-124">**operação**: identifica o tipo de pedido de delegação é - só pode ser **SignIn** neste caso,</span><span class="sxs-lookup"><span data-stu-id="4d295-124">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="4d295-125">**returnUrl**: Olá URL da página olá onde o utilizador Olá clicado numa ligação de início de sessão ou inscrição</span><span class="sxs-lookup"><span data-stu-id="4d295-125">**returnUrl**: hello URL of hello page where hello user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="4d295-126">**Salt**: uma cadeia de salt especial utilizada para um hash de segurança de computação</span><span class="sxs-lookup"><span data-stu-id="4d295-126">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="4d295-127">**SIG**: um toobe de hash de segurança calculada utilizado para comparação tooyour própria hash calculado</span><span class="sxs-lookup"><span data-stu-id="4d295-127">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="4d295-128">Certifique-se de que esse pedido Olá for proveniente de API Management do Azure (opcional, mas vivamente recomendado de segurança)</span><span class="sxs-lookup"><span data-stu-id="4d295-128">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="4d295-129">Computação um hash HMAC SHA512 de uma cadeia com base no Olá **returnUrl** e **salt** parâmetros de consulta ([código de exemplo fornecido abaixo]):</span><span class="sxs-lookup"><span data-stu-id="4d295-129">Compute an HMAC-SHA512 hash of a string based on hello **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="4d295-130">HMAC (**salt** + '\n' + **returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="4d295-130">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="4d295-131">Comparar Olá acima-hash calculado toohello valor Olá **sig** parâmetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="4d295-131">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="4d295-132">Se correspondem aos hashes de dois Olá, mover no passo seguinte toohello, caso contrário negar o pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="4d295-132">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="4d295-133">Certifique-se de que estão a receber um pedido de início de sessão na/início de sessão-cópia de segurança: Olá **operação** parâmetro de consulta será definido demasiado "**SignIn**".</span><span class="sxs-lookup"><span data-stu-id="4d295-133">Verify that you are receiving a request for sign-in/sign-up: hello **operation** query parameter will be set too"**SignIn**".</span></span>
4. <span data-ttu-id="4d295-134">Presente Olá utilizador com IU toosign ou no inscrição</span><span class="sxs-lookup"><span data-stu-id="4d295-134">Present hello user with UI toosign-in or sign-up</span></span>
5. <span data-ttu-id="4d295-135">Se o utilizador Olá é a assinatura de segurança tem toocreate uma conta correspondente para os mesmos na API Management.</span><span class="sxs-lookup"><span data-stu-id="4d295-135">If hello user is signing-up you have toocreate a corresponding account for them in API Management.</span></span> <span data-ttu-id="4d295-136">[Criar um utilizador] com Olá API de REST de gestão de API.</span><span class="sxs-lookup"><span data-stu-id="4d295-136">[Create a user] with hello API Management REST API.</span></span> <span data-ttu-id="4d295-137">Ao fazê-lo, certifique-se de que definiu toohello de ID de utilizador Olá mesmo está no arquivo de utilizador ou ID de tooan pode manter controlar dos.</span><span class="sxs-lookup"><span data-stu-id="4d295-137">When doing so, ensure that you set hello user ID toohello same it is in your user store or tooan ID that you can keep track of.</span></span>
6. <span data-ttu-id="4d295-138">Quando o utilizador de Olá é autenticado com êxito:</span><span class="sxs-lookup"><span data-stu-id="4d295-138">When hello user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="4d295-139">[pedir um token de sessão único (SSO)] através de Olá API de REST de gestão de API</span><span class="sxs-lookup"><span data-stu-id="4d295-139">[request a single-sign-on (SSO) token] via hello API Management REST API</span></span>
   * <span data-ttu-id="4d295-140">acrescente um toohello de parâmetro de consulta returnUrl URL SSO recebidos da chamada de API de Olá acima:</span><span class="sxs-lookup"><span data-stu-id="4d295-140">append a returnUrl query parameter toohello SSO URL you have received from hello API call above:</span></span>
     
     > <span data-ttu-id="4d295-141">Por exemplo, https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span><span class="sxs-lookup"><span data-stu-id="4d295-141">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="4d295-142">Olá utilizador toohello acima foram produzido URL de redirecionamento</span><span class="sxs-lookup"><span data-stu-id="4d295-142">redirect hello user toohello above produced URL</span></span>

<span data-ttu-id="4d295-143">Na adição toohello **SignIn** operação, também pode efetuar a gestão de conta ao seguir os passos anteriores Olá e utilizando um dos Olá seguintes operações.</span><span class="sxs-lookup"><span data-stu-id="4d295-143">In addition toohello **SignIn** operation, you can also perform account management by following hello previous steps and using one of hello following operations.</span></span>

* <span data-ttu-id="4d295-144">**ChangePassword**</span><span class="sxs-lookup"><span data-stu-id="4d295-144">**ChangePassword**</span></span>
* <span data-ttu-id="4d295-145">**ChangeProfile**</span><span class="sxs-lookup"><span data-stu-id="4d295-145">**ChangeProfile**</span></span>
* <span data-ttu-id="4d295-146">**CloseAccount**</span><span class="sxs-lookup"><span data-stu-id="4d295-146">**CloseAccount**</span></span>

<span data-ttu-id="4d295-147">Tem de passar Olá seguir os parâmetros de consulta para operações de gestão de conta.</span><span class="sxs-lookup"><span data-stu-id="4d295-147">You must pass hello following query parameters for account management operations.</span></span>

* <span data-ttu-id="4d295-148">**operação**: identifica o tipo de pedido de delegação é (ChangePassword, ChangeProfile ou CloseAccount)</span><span class="sxs-lookup"><span data-stu-id="4d295-148">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="4d295-149">**userId**: id de utilizador de Olá de Olá conta toomanage</span><span class="sxs-lookup"><span data-stu-id="4d295-149">**userId**: hello user id of hello account toomanage</span></span>
* <span data-ttu-id="4d295-150">**Salt**: uma cadeia de salt especial utilizada para um hash de segurança de computação</span><span class="sxs-lookup"><span data-stu-id="4d295-150">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="4d295-151">**SIG**: um toobe de hash de segurança calculada utilizado para comparação tooyour própria hash calculado</span><span class="sxs-lookup"><span data-stu-id="4d295-151">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>

## <span data-ttu-id="4d295-152"><a name="delegate-product-subscription"></a>Delegar a subscrição do produto</span><span class="sxs-lookup"><span data-stu-id="4d295-152"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="4d295-153">Delegar a subscrição de produto funciona da mesma forma toodelegating utilizador início de sessão/cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="4d295-153">Delegating product subscription works similarly toodelegating user sign-in/-up.</span></span> <span data-ttu-id="4d295-154">fluxo de trabalho final Olá seria o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4d295-154">hello final workflow would be as follows:</span></span>

1. <span data-ttu-id="4d295-155">Programador seleciona um produto no portal de Programador de API Management Olá e clica no botão de subscrever Olá</span><span class="sxs-lookup"><span data-stu-id="4d295-155">Developer selects a product in hello API Management developer portal and clicks on hello Subscribe button</span></span>
2. <span data-ttu-id="4d295-156">Browser é o ponto final de delegação toohello redirecionada</span><span class="sxs-lookup"><span data-stu-id="4d295-156">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="4d295-157">Ponto final de delegação efetua os passos de subscrição necessário produto - esta é a cópia de segurança tooyou e poderá entail redirecionar informações de faturação, colocar questões adicionais, ou simplesmente armazenar informações de Olá e que não requerem qualquer ação do utilizador o toorequest da página de tooanother</span><span class="sxs-lookup"><span data-stu-id="4d295-157">Delegation endpoint performs required product subscription steps - this is up tooyou and may entail redirecting tooanother page toorequest billing information, asking additional questions, or simply storing hello information and not requiring any user action</span></span>

<span data-ttu-id="4d295-158">tooenable Olá funcionalidade, Olá **delegação** página clique **delegar a subscrição de produto**.</span><span class="sxs-lookup"><span data-stu-id="4d295-158">tooenable hello functionality, on hello **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="4d295-159">Em seguida, certifique-se de ponto final de delegação Olá efetua Olá seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="4d295-159">Then ensure hello delegation endpoint performs hello following actions:</span></span>

1. <span data-ttu-id="4d295-160">Receba um pedido no Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="4d295-160">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="4d295-161">*http://www.yourwebsite.com/apimdelegation?Operation= {operação} & productId = {toosubscribe de produto para} & userId = {efetuar o pedido de utilizador} & salt = {cadeia} & sig = {cadeia}*</span><span class="sxs-lookup"><span data-stu-id="4d295-161">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product toosubscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="4d295-162">Parâmetros de consulta para o caso de subscrição de produto Olá:</span><span class="sxs-lookup"><span data-stu-id="4d295-162">Query parameters for hello product subscription case:</span></span>
   
   * <span data-ttu-id="4d295-163">**operação**: identifica o tipo de pedido de delegação é.</span><span class="sxs-lookup"><span data-stu-id="4d295-163">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="4d295-164">Para a subscrição de produto pedidos Olá válido opções são:</span><span class="sxs-lookup"><span data-stu-id="4d295-164">For product subscription requests hello valid options are:</span></span>
     * <span data-ttu-id="4d295-165">"Subscrever": fornecidos de um pedido toosubscribe Olá utilizador tooa fornecido produto com o ID (ver abaixo)</span><span class="sxs-lookup"><span data-stu-id="4d295-165">"Subscribe": a request toosubscribe hello user tooa given product with provided ID (see below)</span></span>
     * <span data-ttu-id="4d295-166">"Anular a subscrição": toounsubscribe um pedido um utilizador de um produto</span><span class="sxs-lookup"><span data-stu-id="4d295-166">"Unsubscribe": a request toounsubscribe a user from a product</span></span>
     * <span data-ttu-id="4d295-167">"Renovar": uma toorenew requst uma subscrição (por exemplo, que pode ser expira)</span><span class="sxs-lookup"><span data-stu-id="4d295-167">"Renew": a requst toorenew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="4d295-168">**productId**: Olá ID de utilizador do Olá produto Olá pedida toosubscribe para</span><span class="sxs-lookup"><span data-stu-id="4d295-168">**productId**: hello ID of hello product hello user requested toosubscribe to</span></span>
   * <span data-ttu-id="4d295-169">**userId**: Olá ID de utilizador de Olá para o qual o pedido de Olá é efetuado</span><span class="sxs-lookup"><span data-stu-id="4d295-169">**userId**: hello ID of hello user for whom hello request is made</span></span>
   * <span data-ttu-id="4d295-170">**Salt**: uma cadeia de salt especial utilizada para um hash de segurança de computação</span><span class="sxs-lookup"><span data-stu-id="4d295-170">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="4d295-171">**SIG**: um toobe de hash de segurança calculada utilizado para comparação tooyour própria hash calculado</span><span class="sxs-lookup"><span data-stu-id="4d295-171">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="4d295-172">Certifique-se de que esse pedido Olá for proveniente de API Management do Azure (opcional, mas vivamente recomendado de segurança)</span><span class="sxs-lookup"><span data-stu-id="4d295-172">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="4d295-173">Computação um SHA512 HMAC de uma cadeia com base no Olá **productId**, **userId** e **salt** parâmetros de consulta:</span><span class="sxs-lookup"><span data-stu-id="4d295-173">Compute an HMAC-SHA512 of a string based on hello **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="4d295-174">HMAC (**salt** + '\n' + **productId** + '\n' + **userId**)</span><span class="sxs-lookup"><span data-stu-id="4d295-174">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="4d295-175">Comparar Olá acima-hash calculado toohello valor Olá **sig** parâmetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="4d295-175">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="4d295-176">Se correspondem aos hashes de dois Olá, mover no passo seguinte toohello, caso contrário negar o pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="4d295-176">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="4d295-177">Efetuar qualquer processamento de subscrição de produto com base no tipo de Olá da operação pedida no **operação** -por exemplo, de faturação, mais perguntas, etc.</span><span class="sxs-lookup"><span data-stu-id="4d295-177">Perform any product subscription processing based on hello type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="4d295-178">Com êxito subscrever o produto de toohello Olá utilizador no seu lado, subscrever produtos de gestão de API do Olá utilizador toohello por [Olá chamar a REST API para a subscrição de produto].</span><span class="sxs-lookup"><span data-stu-id="4d295-178">On successfully subscribing hello user toohello product on your side, subscribe hello user toohello API Management product by [calling hello REST API for product subscription].</span></span>

## <span data-ttu-id="4d295-179"><a name="delegate-example-code"></a> Código de exemplo</span><span class="sxs-lookup"><span data-stu-id="4d295-179"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="4d295-180">Estes exemplos mostram de código como tootake Olá *chave de validação de delegação*, que está definido no ecrã de delegação de Olá do portal do publicador Olá, toocreate um HMAC que, em seguida, é utilizada a assinatura de Olá toovalidate, comprovar a respetiva validade Olá Olá returnUrl transmitido.</span><span class="sxs-lookup"><span data-stu-id="4d295-180">These code samples show how tootake hello *delegation validation key*, which is set in hello Delegation screen of hello publisher portal, toocreate a HMAC which is then used toovalidate hello signature, proving hello validity of hello passed returnUrl.</span></span> <span data-ttu-id="4d295-181">Olá mesmo código funciona para Olá productId e userId com ligeiras modificação.</span><span class="sxs-lookup"><span data-stu-id="4d295-181">hello same code works for hello productId and userId with slight modification.</span></span>

<span data-ttu-id="4d295-182">**C# hash de código toogenerate do returnUrl**</span><span class="sxs-lookup"><span data-stu-id="4d295-182">**C# code toogenerate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

<span data-ttu-id="4d295-183">**NodeJS código hash toogenerate de returnUrl**</span><span class="sxs-lookup"><span data-stu-id="4d295-183">**NodeJS code toogenerate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="4d295-184">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4d295-184">Next steps</span></span>
<span data-ttu-id="4d295-185">Para obter mais informações sobre delegação, consulte Olá seguir as vídeo.</span><span class="sxs-lookup"><span data-stu-id="4d295-185">For more information on delegation, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[pedir um token de sessão único (SSO)]: http://go.microsoft.com/fwlink/?LinkId=507409
[criar um utilizador]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[Olá chamar a REST API para a subscrição de produto]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[código de exemplo fornecido abaixo]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
