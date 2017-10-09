---
title: aaaAzure APIs de SDK do Mobile Engagement Web | Microsoft Docs
description: "Olá mais recentes atualizações e procedimentos para Olá Web SDK do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: ec1261d6ad573b8c3ad6d5f616ab7bbe560d6fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="0e9db-103">Utilizar Olá API do Azure Mobile Engagement numa aplicação web</span><span class="sxs-lookup"><span data-stu-id="0e9db-103">Use hello Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="0e9db-104">Este documento é um documento de toohello adição que indica como demasiado[integrar o Mobile Engagement numa aplicação web](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="0e9db-104">This document is an addition toohello document that tells you how too[integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="0e9db-105">Fornece detalhes aprofundados sobre como toouse Olá API do Azure Mobile Engagement tooreport as estatísticas da aplicação.</span><span class="sxs-lookup"><span data-stu-id="0e9db-105">It provides in-depth details about how toouse hello Azure Mobile Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="0e9db-106">Olá API do Mobile Engagement é fornecida pela Olá `engagement.agent` objeto.</span><span class="sxs-lookup"><span data-stu-id="0e9db-106">hello Mobile Engagement API is provided by hello `engagement.agent` object.</span></span> <span data-ttu-id="0e9db-107">Olá predefinição SDK Web do Azure Mobile Engagement alias `engagement`.</span><span class="sxs-lookup"><span data-stu-id="0e9db-107">hello default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="0e9db-108">Pode redefinir este alias de configuração do SDK Olá.</span><span class="sxs-lookup"><span data-stu-id="0e9db-108">You can redefine this alias from hello SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="0e9db-109">Conceitos do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="0e9db-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="0e9db-110">Olá seguintes partes refinar comuns [conceitos do Mobile Engagement](mobile-engagement-concepts.md) de plataforma web de Olá.</span><span class="sxs-lookup"><span data-stu-id="0e9db-110">hello following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for hello web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="0e9db-111">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="0e9db-111">`Session` and `Activity`</span></span>
<span data-ttu-id="0e9db-112">Se o utilizador Olá permanece inativo durante mais do que alguns segundos, entre duas atividades, hello sequência do utilizador de atividades está dividida em duas sessões distintas.</span><span class="sxs-lookup"><span data-stu-id="0e9db-112">If hello user stays idle for more than a few seconds between two activities, hello user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="0e9db-113">Estes alguns segundos são denominados Olá tempo limite da sessão.</span><span class="sxs-lookup"><span data-stu-id="0e9db-113">These few seconds are called hello session timeout.</span></span>

<span data-ttu-id="0e9db-114">Se a aplicação web não declara final Olá das atividades de utilizador por si só (por chamada Olá `engagement.agent.endActivity` função), servidor de Mobile Engagement Olá expira automaticamente Olá sessão de utilizador em três minutos depois de fechar a página de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="0e9db-114">If your web application doesn't declare hello end of user activities by itself (by calling hello `engagement.agent.endActivity` function), hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span> <span data-ttu-id="0e9db-115">Isto denomina-tempo limite de sessão do servidor Olá.</span><span class="sxs-lookup"><span data-stu-id="0e9db-115">This is called hello server session timeout.</span></span>

### `Crash`
<span data-ttu-id="0e9db-116">Relatórios automatizados de exceções de JavaScript não identificadas não estão criados por predefinição.</span><span class="sxs-lookup"><span data-stu-id="0e9db-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="0e9db-117">No entanto, pode reportar falhas manualmente utilizando Olá `sendCrash` funcionar (consulte a secção de Olá no relatório de falhas).</span><span class="sxs-lookup"><span data-stu-id="0e9db-117">However, you can report crashes manually by using hello `sendCrash` function (see hello section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="0e9db-118">Relatório de atividades</span><span class="sxs-lookup"><span data-stu-id="0e9db-118">Reporting activities</span></span>
<span data-ttu-id="0e9db-119">Atividade do utilizador de relatórios incluem quando um utilizador inicia uma nova atividade e, quando o utilizador Olá termina a atividade atual Olá.</span><span class="sxs-lookup"><span data-stu-id="0e9db-119">Reporting on user activity includes when a user starts a new activity, and when hello user ends hello current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="0e9db-120">Utilizador inicia uma nova atividade</span><span class="sxs-lookup"><span data-stu-id="0e9db-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="0e9db-121">Terá de toocall `startActivity()` cada atividade de utilizador de hora é alterado.</span><span class="sxs-lookup"><span data-stu-id="0e9db-121">You need toocall `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="0e9db-122">Olá primeira chamada toothis função inicia uma nova sessão de utilizador.</span><span class="sxs-lookup"><span data-stu-id="0e9db-122">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-hello-current-activity"></a><span data-ttu-id="0e9db-123">Utilizador termina a atividade atual Olá</span><span class="sxs-lookup"><span data-stu-id="0e9db-123">User ends hello current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="0e9db-124">Terá de toocall `endActivity()` , pelo menos, uma vez quando o utilizador de Olá for concluída, a última atividade dos mesmos.</span><span class="sxs-lookup"><span data-stu-id="0e9db-124">You need toocall `endActivity()` at least once when hello user finishes their last activity.</span></span> <span data-ttu-id="0e9db-125">Informa Olá Web SDK do Mobile Engagement que utilizador Olá está atualmente inativa, e que a sessão de utilizador Olá tem toobe fechada depois do tempo limite da sessão Olá expira.</span><span class="sxs-lookup"><span data-stu-id="0e9db-125">This informs hello Mobile Engagement Web SDK that hello user is currently idle, and that hello user session needs toobe closed after hello session timeout expires.</span></span> <span data-ttu-id="0e9db-126">Se chamar `startActivity()` antes do tempo limite da sessão Olá expira, a sessão de Olá simplesmente é retomada.</span><span class="sxs-lookup"><span data-stu-id="0e9db-126">If you call `startActivity()` before hello session timeout expires, hello session is simply resumed.</span></span>

<span data-ttu-id="0e9db-127">Porque não existe nenhuma chamada fiável para quando a janela do navegador de Olá está fechada, é frequentemente fim de Olá toocatch difícil ou impossível das atividades de utilizador dentro de um ambiente de web.</span><span class="sxs-lookup"><span data-stu-id="0e9db-127">Because there's no reliable call for when hello navigator window is closed, it's often difficult or impossible toocatch hello end of user activities inside a web environment.</span></span> <span data-ttu-id="0e9db-128">Por que motivo que é Olá Mobile Engagement server expira automaticamente sessão de utilizador de Olá dentro de três minutos após a página de aplicação Olá está fechada.</span><span class="sxs-lookup"><span data-stu-id="0e9db-128">That's why hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="0e9db-129">Eventos de relatório</span><span class="sxs-lookup"><span data-stu-id="0e9db-129">Reporting events</span></span>
<span data-ttu-id="0e9db-130">Eventos de relatório abrange eventos da sessão e eventos de autónomo.</span><span class="sxs-lookup"><span data-stu-id="0e9db-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="0e9db-131">Eventos da sessão</span><span class="sxs-lookup"><span data-stu-id="0e9db-131">Session events</span></span>
<span data-ttu-id="0e9db-132">Eventos da sessão são normalmente ações de Olá de tooreport utilizados realizadas por um utilizador durante a sessão do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="0e9db-132">Session events usually are used tooreport hello actions performed by a user during hello user's session.</span></span>

<span data-ttu-id="0e9db-133">**Exemplo sem dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="0e9db-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="0e9db-134">**Exemplo com dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="0e9db-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="0e9db-135">Eventos de autónomo</span><span class="sxs-lookup"><span data-stu-id="0e9db-135">Standalone events</span></span>
<span data-ttu-id="0e9db-136">Ao contrário de eventos da sessão, podem ocorrer eventos de autónomo fora Olá contexto de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="0e9db-136">Unlike session events, standalone events can occur outside hello context of a session.</span></span>

<span data-ttu-id="0e9db-137">Para tal, utilize ``engagement.agent.sendEvent`` em vez de ``engagement.agent.sendSessionEvent``.</span><span class="sxs-lookup"><span data-stu-id="0e9db-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="0e9db-138">Relatório de erros</span><span class="sxs-lookup"><span data-stu-id="0e9db-138">Reporting errors</span></span>
<span data-ttu-id="0e9db-139">Relatório de erros abrange erros de sessão e erros de autónomo.</span><span class="sxs-lookup"><span data-stu-id="0e9db-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="0e9db-140">Erros de sessão</span><span class="sxs-lookup"><span data-stu-id="0e9db-140">Session errors</span></span>
<span data-ttu-id="0e9db-141">Erros de sessão são, normalmente, erros de Olá tooreport utilizados que tem um impacto no utilizador Olá durante Olá da sessão de utilizador.</span><span class="sxs-lookup"><span data-stu-id="0e9db-141">Session errors usually are used tooreport hello errors that have an impact on hello user during hello user's session.</span></span>

<span data-ttu-id="0e9db-142">**Exemplo sem dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="0e9db-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="0e9db-143">**Exemplo com dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="0e9db-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="0e9db-144">Erros de autónomo</span><span class="sxs-lookup"><span data-stu-id="0e9db-144">Standalone errors</span></span>
<span data-ttu-id="0e9db-145">Ao contrário dos erros de sessão, podem ocorrer erros de autónomo fora Olá contexto de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="0e9db-145">Unlike session errors, standalone errors can occur outside hello context of a session.</span></span>

<span data-ttu-id="0e9db-146">Para tal, utilize `engagement.agent.sendError` em vez de `engagement.agent.sendSessionError`.</span><span class="sxs-lookup"><span data-stu-id="0e9db-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="0e9db-147">Tarefas de relatório</span><span class="sxs-lookup"><span data-stu-id="0e9db-147">Reporting jobs</span></span>
<span data-ttu-id="0e9db-148">Elaboração de relatórios em tarefas bastidores erros e eventos que ocorrem durante uma tarefa de relatórios e relatórios de falhas.</span><span class="sxs-lookup"><span data-stu-id="0e9db-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="0e9db-149">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="0e9db-149">**Example:**</span></span>

<span data-ttu-id="0e9db-150">Se quiser toomonitor um pedido de AJAX, utilizaria seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="0e9db-150">If you want toomonitor an AJAX request, you'd use hello following:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="0e9db-151">Relatório de erros durante a uma tarefa</span><span class="sxs-lookup"><span data-stu-id="0e9db-151">Reporting errors during a job</span></span>
<span data-ttu-id="0e9db-152">Erros podem ser tooa relacionado com a tarefa em vez de toohello sessão do utilizador atual.</span><span class="sxs-lookup"><span data-stu-id="0e9db-152">Errors can be related tooa running job instead of toohello current user session.</span></span>

<span data-ttu-id="0e9db-153">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="0e9db-153">**Example:**</span></span>

<span data-ttu-id="0e9db-154">Se quiser tooreport um erro se um pedido de AJAX falha:</span><span class="sxs-lookup"><span data-stu-id="0e9db-154">If you want tooreport an error if an AJAX request fails:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="0e9db-155">Eventos de relatório durante uma tarefa</span><span class="sxs-lookup"><span data-stu-id="0e9db-155">Reporting events during a job</span></span>
<span data-ttu-id="0e9db-156">Os eventos podem estar relacionado tooa executar tarefa em vez de sessão do utilizador atual toohello, thanks toohello `engagement.agent.sendJobEvent` função.</span><span class="sxs-lookup"><span data-stu-id="0e9db-156">Events can be related tooa running job instead of toohello current user session, thanks toohello `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="0e9db-157">Esta função funciona exatamente como `engagement.agent.sendJobError`.</span><span class="sxs-lookup"><span data-stu-id="0e9db-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="0e9db-158">Relatório de falhas</span><span class="sxs-lookup"><span data-stu-id="0e9db-158">Reporting crashes</span></span>
<span data-ttu-id="0e9db-159">Olá utilize `sendCrash` função tooreport falhas manualmente.</span><span class="sxs-lookup"><span data-stu-id="0e9db-159">Use hello `sendCrash` function tooreport crashes manually.</span></span>

<span data-ttu-id="0e9db-160">Olá `crashid` argumento é uma cadeia que identifica o tipo de Olá da falha.</span><span class="sxs-lookup"><span data-stu-id="0e9db-160">hello `crashid` argument is a string that identifies hello type of crash.</span></span>
<span data-ttu-id="0e9db-161">Olá `crash` argumento é, normalmente, o rastreio da pilha Olá de falhas de Olá como uma cadeia.</span><span class="sxs-lookup"><span data-stu-id="0e9db-161">hello `crash` argument usually is hello stack trace of hello crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="0e9db-162">Parâmetros adicionais</span><span class="sxs-lookup"><span data-stu-id="0e9db-162">Extra parameters</span></span>
<span data-ttu-id="0e9db-163">Pode anexar dados arbitrários tooan evento, erro, atividade ou tarefa.</span><span class="sxs-lookup"><span data-stu-id="0e9db-163">You can attach arbitrary data tooan event, error, activity, or job.</span></span>

<span data-ttu-id="0e9db-164">dados de Olá podem ser qualquer objeto JSON (mas não uma matriz nem um tipo primitivo).</span><span class="sxs-lookup"><span data-stu-id="0e9db-164">hello data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="0e9db-165">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="0e9db-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="0e9db-166">Limites</span><span class="sxs-lookup"><span data-stu-id="0e9db-166">Limits</span></span>
<span data-ttu-id="0e9db-167">Os limites que se aplicam tooextra parâmetros são nas áreas de Olá de expressões regulares para chaves, tipos de valor e tamanho.</span><span class="sxs-lookup"><span data-stu-id="0e9db-167">Limits that apply tooextra parameters are in hello areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="0e9db-168">Chaves</span><span class="sxs-lookup"><span data-stu-id="0e9db-168">Keys</span></span>
<span data-ttu-id="0e9db-169">Cada chave no objeto de Olá tem de corresponder ao hello seguintes expressão regular:</span><span class="sxs-lookup"><span data-stu-id="0e9db-169">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="0e9db-170">Isto significa que as chaves tem de começar com, pelo menos, uma letra, seguido de letras, dígitos ou carateres de sublinhado (\_).</span><span class="sxs-lookup"><span data-stu-id="0e9db-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="0e9db-171">Valores</span><span class="sxs-lookup"><span data-stu-id="0e9db-171">Values</span></span>
<span data-ttu-id="0e9db-172">Os valores são toostring limitada, o número e tipos booleanos.</span><span class="sxs-lookup"><span data-stu-id="0e9db-172">Values are limited toostring, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="0e9db-173">Tamanho</span><span class="sxs-lookup"><span data-stu-id="0e9db-173">Size</span></span>
<span data-ttu-id="0e9db-174">Extras estão limitadas too1, 024 carateres por chamada (após Olá Web SDK do Mobile Engagement codifica no JSON).</span><span class="sxs-lookup"><span data-stu-id="0e9db-174">Extras are limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="0e9db-175">Informações de relatórios de aplicações</span><span class="sxs-lookup"><span data-stu-id="0e9db-175">Reporting application information</span></span>
<span data-ttu-id="0e9db-176">Manualmente pode comunicar informações (ou outras informações específicas da aplicação) de controlo utilizando Olá `sendAppInfo()` função.</span><span class="sxs-lookup"><span data-stu-id="0e9db-176">You can manually report tracking information (or any other application-specific information) by using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="0e9db-177">Tenha em atenção que estas informações podem ser enviadas de forma incremental.</span><span class="sxs-lookup"><span data-stu-id="0e9db-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="0e9db-178">Apenas Olá valor mais recente para uma chave específica será mantido para um dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="0e9db-178">Only hello latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="0e9db-179">Como extras de eventos, pode utilizar qualquer JSON tooabstract aplicação as informações do objeto.</span><span class="sxs-lookup"><span data-stu-id="0e9db-179">Like event extras, you can use any JSON object tooabstract application information.</span></span> <span data-ttu-id="0e9db-180">Tenha em atenção que as matrizes ou objetos secundárias são tratados como cadeias simples (com a serialização do JSON).</span><span class="sxs-lookup"><span data-stu-id="0e9db-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="0e9db-181">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="0e9db-181">**Example:**</span></span>

<span data-ttu-id="0e9db-182">Eis um exemplo de código para sexo do utilizador Olá envio e a data de nascimento:</span><span class="sxs-lookup"><span data-stu-id="0e9db-182">Here is a code sample for sending hello user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="0e9db-183">Limites</span><span class="sxs-lookup"><span data-stu-id="0e9db-183">Limits</span></span>
<span data-ttu-id="0e9db-184">Os limites que se aplicam tooapplication informações são nas áreas de Olá de expressões regulares para chaves e tamanho.</span><span class="sxs-lookup"><span data-stu-id="0e9db-184">Limits that apply tooapplication information are in hello areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="0e9db-185">Chaves</span><span class="sxs-lookup"><span data-stu-id="0e9db-185">Keys</span></span>
<span data-ttu-id="0e9db-186">Cada chave no objeto de Olá tem de corresponder ao hello seguintes expressão regular:</span><span class="sxs-lookup"><span data-stu-id="0e9db-186">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="0e9db-187">Isto significa que as chaves tem de começar com, pelo menos, uma letra, seguido de letras, dígitos ou carateres de sublinhado (\_).</span><span class="sxs-lookup"><span data-stu-id="0e9db-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="0e9db-188">Tamanho</span><span class="sxs-lookup"><span data-stu-id="0e9db-188">Size</span></span>
<span data-ttu-id="0e9db-189">Informações sobre a aplicação é limitado too1, 024 carateres por chamada (após Olá Web SDK do Mobile Engagement codifica no JSON).</span><span class="sxs-lookup"><span data-stu-id="0e9db-189">Application information is limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="0e9db-190">Olá anterior exemplo, hello JSON enviadas toohello servidor é 44 carateres de comprimento:</span><span class="sxs-lookup"><span data-stu-id="0e9db-190">In hello preceding example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
