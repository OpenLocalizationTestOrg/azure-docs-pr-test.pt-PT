---
title: "aaaHow tooUse Olá Engagement API no Windows Phone Silverlight"
description: "Como tooUse Olá o Engagement API no Windows Phone Silverlight"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ae2ba2e8-f75b-4dee-a164-a7dd65d35a23
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1e84be95cc910be7f1227b4ae60eb483a1939284
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-phone-silverlight"></a><span data-ttu-id="3c158-103">Como tooUse Olá o Engagement API no Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="3c158-103">How tooUse hello Engagement API on Windows Phone Silverlight</span></span>
<span data-ttu-id="3c158-104">Este documento é um documento de toohello suplemento [como toointegrate Mobile Engagement na sua aplicação do Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="3c158-104">This document is an add-on toohello document [How toointegrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md).</span></span> <span data-ttu-id="3c158-105">Fornece na profundidade obter detalhes sobre como toouse Olá Engagement API tooreport as estatísticas da aplicação.</span><span class="sxs-lookup"><span data-stu-id="3c158-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="3c158-106">Se pretender apenas Engagement tooreport da sua aplicação sessões, atividades, as falhas e obter informações técnicas, em seguida, Olá mais simples é forma toomake todos os seus `PhoneApplicationPage` classes secundárias herdarem Olá `EngagementPage` classe.</span><span class="sxs-lookup"><span data-stu-id="3c158-106">If you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="3c158-107">Se quiser toodo mais, por exemplo, se precisar de eventos específicos de aplicação tooreport, erros e tarefas, ou se tiver tooreport as atividades da aplicação de forma diferente que Olá um implementado no Olá `EngagementPage` classes, em seguida, terá de toouse Olá Engagement API.</span><span class="sxs-lookup"><span data-stu-id="3c158-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="3c158-108">Olá Engagement API é fornecida pela Olá `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="3c158-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="3c158-109">Pode aceder aos métodos toothose através de `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="3c158-109">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="3c158-110">Mesmo que o módulo de Olá de agente não foi inicializado, cada API de toohello chamada é deferida e será executada novamente quando o agente de Olá está disponível.</span><span class="sxs-lookup"><span data-stu-id="3c158-110">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="3c158-111">Conceitos de envolvimento</span><span class="sxs-lookup"><span data-stu-id="3c158-111">Engagement concepts</span></span>
<span data-ttu-id="3c158-112">Olá seguintes partes refinar Olá conceitos do Mobile Engagement para a plataforma do Windows Phone Olá.</span><span class="sxs-lookup"><span data-stu-id="3c158-112">hello following parts refine hello Mobile Engagement Concepts for hello Windows Phone platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="3c158-113">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="3c158-113">`Session` and `Activity`</span></span>
<span data-ttu-id="3c158-114">Um *atividade* é normalmente associadas uma página da aplicação Olá, que é toosay Olá *atividade* inicia quando página Olá é apresentada e para quando a página Olá está fechada: Este é o caso de Olá quando hello O engagement SDK está integrado utilizando Olá `EngagementPage` classe.</span><span class="sxs-lookup"><span data-stu-id="3c158-114">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="3c158-115">Mas *atividades* também pode ser controlado manualmente utilizando Olá o Engagement API.</span><span class="sxs-lookup"><span data-stu-id="3c158-115">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="3c158-116">Isto permite que toosplit uma determinada página na várias sub partes tooget Olá, obter mais detalhes sobre a utilização desta página (por exemplo tooknown frequência e quanto as caixas de diálogo são utilizadas dentro desta página).</span><span class="sxs-lookup"><span data-stu-id="3c158-116">This allows toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknown how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="3c158-117">Relatório de atividades</span><span class="sxs-lookup"><span data-stu-id="3c158-117">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="3c158-118">Utilizador inicia uma nova atividade</span><span class="sxs-lookup"><span data-stu-id="3c158-118">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="3c158-119">Referência</span><span class="sxs-lookup"><span data-stu-id="3c158-119">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="3c158-120">Terá de toocall `StartActivity()` cada atividade de utilizador de Olá de hora é alterado.</span><span class="sxs-lookup"><span data-stu-id="3c158-120">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="3c158-121">Olá primeira chamada toothis função inicia uma nova sessão de utilizador.</span><span class="sxs-lookup"><span data-stu-id="3c158-121">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c158-122">Olá SDK automaticamente chamar o método de EndActivity de Olá, quando a aplicação Olá está fechada.</span><span class="sxs-lookup"><span data-stu-id="3c158-122">hello SDK automatically call hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="3c158-123">Assim, recomenda-se vivamente método do toocall Olá StartActivity sempre que terminou a atividade de Olá de alteração de utilizador Olá e chamada de tooNEVER Olá método EndActivity, desde a chamar este método força Olá toobe de sessão atual.</span><span class="sxs-lookup"><span data-stu-id="3c158-123">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user change, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="3c158-124">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3c158-124">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="3c158-125">Utilizador termina a atividade atual</span><span class="sxs-lookup"><span data-stu-id="3c158-125">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="3c158-126">Referência</span><span class="sxs-lookup"><span data-stu-id="3c158-126">Reference</span></span>
            void EndActivity()

<span data-ttu-id="3c158-127">Terá de toocall `EndActivity()` , pelo menos, uma vez quando o utilizador Olá conclui a última atividade.</span><span class="sxs-lookup"><span data-stu-id="3c158-127">You need toocall `EndActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="3c158-128">Informa Olá irá expirar o Engagement SDK que utilizador Olá está atualmente inativa, e uma vez que a sessão de utilizador Olá tem toobe fechado Olá tempo limite da sessão (se chamar `StartActivity()` antes do tempo limite da sessão Olá expira, a sessão Olá simplesmente é continuado).</span><span class="sxs-lookup"><span data-stu-id="3c158-128">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `StartActivity()` before hello session timeout expires, hello session is simply continued).</span></span>

#### <a name="example"></a><span data-ttu-id="3c158-129">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3c158-129">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="3c158-130">Tarefas de relatório</span><span class="sxs-lookup"><span data-stu-id="3c158-130">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="3c158-131">Iniciar uma tarefa</span><span class="sxs-lookup"><span data-stu-id="3c158-131">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="3c158-132">Referência</span><span class="sxs-lookup"><span data-stu-id="3c158-132">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="3c158-133">Pode utilizar tarefas certains tootrack de Olá durante um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="3c158-133">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="3c158-134">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3c158-134">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="3c158-135">Terminar uma tarefa</span><span class="sxs-lookup"><span data-stu-id="3c158-135">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="3c158-136">Referência</span><span class="sxs-lookup"><span data-stu-id="3c158-136">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="3c158-137">Assim que uma tarefa controlada por uma tarefa foi terminada, deverá chamar o método de EndJob de Olá para esta tarefa, fornecendo o nome da tarefa Olá.</span><span class="sxs-lookup"><span data-stu-id="3c158-137">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="3c158-138">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3c158-138">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="3c158-139">Eventos de relatório</span><span class="sxs-lookup"><span data-stu-id="3c158-139">Reporting Events</span></span>
<span data-ttu-id="3c158-140">Há três tipos de eventos:</span><span class="sxs-lookup"><span data-stu-id="3c158-140">There is three types of events :</span></span>

* <span data-ttu-id="3c158-141">Eventos de autónomo</span><span class="sxs-lookup"><span data-stu-id="3c158-141">Standalone events</span></span>
* <span data-ttu-id="3c158-142">Eventos da sessão</span><span class="sxs-lookup"><span data-stu-id="3c158-142">Session events</span></span>
* <span data-ttu-id="3c158-143">Eventos de tarefas</span><span class="sxs-lookup"><span data-stu-id="3c158-143">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="3c158-144">Eventos de autónomo</span><span class="sxs-lookup"><span data-stu-id="3c158-144">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="3c158-145">Referência</span><span class="sxs-lookup"><span data-stu-id="3c158-145">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="3c158-146">Podem ocorrer eventos de autónomo fora do contexto de Olá de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="3c158-146">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="3c158-147">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3c158-147">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="3c158-148">Eventos da sessão</span><span class="sxs-lookup"><span data-stu-id="3c158-148">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="3c158-149">Referência</span><span class="sxs-lookup"><span data-stu-id="3c158-149">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="3c158-150">Eventos da sessão são ações de Olá tooreport normalmente utilizadas realizadas por um utilizador durante a sua sessão.</span><span class="sxs-lookup"><span data-stu-id="3c158-150">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="3c158-151">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3c158-151">Example</span></span>
<span data-ttu-id="3c158-152">**Sem dados:**</span><span class="sxs-lookup"><span data-stu-id="3c158-152">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="3c158-153">**Com os dados:**</span><span class="sxs-lookup"><span data-stu-id="3c158-153">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="3c158-154">Eventos de tarefas</span><span class="sxs-lookup"><span data-stu-id="3c158-154">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="3c158-155">Referência</span><span class="sxs-lookup"><span data-stu-id="3c158-155">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="3c158-156">Eventos de tarefas são ações de Olá de tooreport normalmente utilizadas realizadas por um utilizador durante uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="3c158-156">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="3c158-157">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3c158-157">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="3c158-158">Relatório de erros</span><span class="sxs-lookup"><span data-stu-id="3c158-158">Reporting Errors</span></span>
<span data-ttu-id="3c158-159">Há três tipos de erros:</span><span class="sxs-lookup"><span data-stu-id="3c158-159">There is three types of errors :</span></span>

* <span data-ttu-id="3c158-160">Erros de autónomo</span><span class="sxs-lookup"><span data-stu-id="3c158-160">Standalone errors</span></span>
* <span data-ttu-id="3c158-161">Erros de sessão</span><span class="sxs-lookup"><span data-stu-id="3c158-161">Session errors</span></span>
* <span data-ttu-id="3c158-162">Erros de tarefas</span><span class="sxs-lookup"><span data-stu-id="3c158-162">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="3c158-163">Erros de autónomo</span><span class="sxs-lookup"><span data-stu-id="3c158-163">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="3c158-164">Referência</span><span class="sxs-lookup"><span data-stu-id="3c158-164">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="3c158-165">Erros de contrary toosession, autónomo erros podem ocorrer fora do contexto de Olá de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="3c158-165">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="3c158-166">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3c158-166">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="3c158-167">Erros de sessão</span><span class="sxs-lookup"><span data-stu-id="3c158-167">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="3c158-168">Referência</span><span class="sxs-lookup"><span data-stu-id="3c158-168">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="3c158-169">Erros de sessão são normalmente utilizadas tooreport Olá erros afetar utilizador Olá durante a sua sessão.</span><span class="sxs-lookup"><span data-stu-id="3c158-169">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="3c158-170">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3c158-170">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="3c158-171">Erros de tarefas</span><span class="sxs-lookup"><span data-stu-id="3c158-171">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="3c158-172">Referência</span><span class="sxs-lookup"><span data-stu-id="3c158-172">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="3c158-173">Erros podem ser tooa relacionado com a tarefa em vez de ser relacionadas com toohello sessão do utilizador atual.</span><span class="sxs-lookup"><span data-stu-id="3c158-173">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="3c158-174">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3c158-174">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="3c158-175">Relatório de falhas</span><span class="sxs-lookup"><span data-stu-id="3c158-175">Reporting Crashes</span></span>
<span data-ttu-id="3c158-176">agente de Olá fornece dois métodos toodeal com falhas.</span><span class="sxs-lookup"><span data-stu-id="3c158-176">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="3c158-177">Enviar uma exceção</span><span class="sxs-lookup"><span data-stu-id="3c158-177">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="3c158-178">Referência</span><span class="sxs-lookup"><span data-stu-id="3c158-178">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="3c158-179">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3c158-179">Example</span></span>
<span data-ttu-id="3c158-180">Pode enviar uma exceção em qualquer altura ao chamar:</span><span class="sxs-lookup"><span data-stu-id="3c158-180">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="3c158-181">Também pode utilizar uma sessão de envolvimento do parâmetro opcional tooterminate Olá em Olá mesmo tempo que o envio de falhas de Olá.</span><span class="sxs-lookup"><span data-stu-id="3c158-181">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="3c158-182">por isso, chamar toodo:</span><span class="sxs-lookup"><span data-stu-id="3c158-182">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="3c158-183">Se, fazê-lo, sessão Olá e as tarefas serão fechadas depois de falhas de Olá a enviar.</span><span class="sxs-lookup"><span data-stu-id="3c158-183">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="3c158-184">Enviar uma exceção não processada</span><span class="sxs-lookup"><span data-stu-id="3c158-184">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="3c158-185">Referência</span><span class="sxs-lookup"><span data-stu-id="3c158-185">Reference</span></span>
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

<span data-ttu-id="3c158-186">Também o engagement fornece um exceções toosend não processada do método.</span><span class="sxs-lookup"><span data-stu-id="3c158-186">Engagement also provides a method toosend unhandled exceptions.</span></span> <span data-ttu-id="3c158-187">Isto é especialmente útil quando utilizada dentro de processador de eventos do Olá silverlight UnhandledException.</span><span class="sxs-lookup"><span data-stu-id="3c158-187">This is especially useful when used inside hello silverlight UnhandledException event handler.</span></span>

<span data-ttu-id="3c158-188">Este método irá **sempre** terminar sessão de envolvimento Olá e tarefas depois de a ser chamado.</span><span class="sxs-lookup"><span data-stu-id="3c158-188">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="3c158-189">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3c158-189">Example</span></span>
<span data-ttu-id="3c158-190">Pode utilizá-la tooimplement o seus próprios processador UnhandledException (especialmente se tiver desativado a funcionalidade do Engagement de relatórios de falhas automática Olá).</span><span class="sxs-lookup"><span data-stu-id="3c158-190">You can use it tooimplement your own UnhandledException handler (especially if you have disabled hello automatic crash reporting feature of Engagement).</span></span> <span data-ttu-id="3c158-191">Por exemplo, no Olá `Application_UnhandledException` método de Olá `App.xaml.cs` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="3c158-191">For example, in hello `Application_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a><span data-ttu-id="3c158-192">OnActivated</span><span class="sxs-lookup"><span data-stu-id="3c158-192">OnActivated</span></span>
### <a name="reference"></a><span data-ttu-id="3c158-193">Referência</span><span class="sxs-lookup"><span data-stu-id="3c158-193">Reference</span></span>
            void OnActivated(ActivatedEventArgs e)

<span data-ttu-id="3c158-194">Quando o utilizador Olá navega reencaminhar, na direção oposta a uma aplicação, depois do evento de desativado de Olá é gerado, o sistema de operativo Olá tentará aplicação de Olá tooput num Estado dormant.</span><span class="sxs-lookup"><span data-stu-id="3c158-194">When hello user navigates forward, away from an application, after hello Deactivated event is raised, hello operating system will attempt tooput hello application into a dormant state.</span></span> <span data-ttu-id="3c158-195">Em seguida, da aplicação Olá é Tombstoning.</span><span class="sxs-lookup"><span data-stu-id="3c158-195">Then, hello application is Tombstoning.</span></span> <span data-ttu-id="3c158-196">Este processo é terminada uma aplicação, mas alguns dados sobre o estado de Olá da aplicação Olá e páginas individuais de Olá na aplicação Olá são preservados.</span><span class="sxs-lookup"><span data-stu-id="3c158-196">In this process an application is terminated but some data about hello state of hello application and hello individual pages within hello application is preserved.</span></span>

<span data-ttu-id="3c158-197">Tiver tooinsert `EngagementAgent.Instance.OnActivated(e)` no Olá `Application_Activated` método Olá do Olá App.xaml.cs ficheiro tooreset Engagement agente quando aplicação Olá foi Tombstoned.</span><span class="sxs-lookup"><span data-stu-id="3c158-197">You have tooinsert `EngagementAgent.Instance.OnActivated(e)` in hello `Application_Activated` method from hello App.xaml.cs file tooreset hello Engagement Agent when hello application has been Tombstoned.</span></span>

### <a name="example"></a><span data-ttu-id="3c158-198">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3c158-198">Example</span></span>
            // Inside your App.xaml.cs file

            // Code tooexecute when hello application is activated (brought tooforeground)
            // This code will not execute when hello application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a><span data-ttu-id="3c158-199">Id de dispositivo</span><span class="sxs-lookup"><span data-stu-id="3c158-199">Device Id</span></span>
            String GetDeviceId()

<span data-ttu-id="3c158-200">Pode obter o id de dispositivo do engagement Olá ao chamar este método.</span><span class="sxs-lookup"><span data-stu-id="3c158-200">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="3c158-201">Parâmetros de Extras</span><span class="sxs-lookup"><span data-stu-id="3c158-201">Extras parameters</span></span>
<span data-ttu-id="3c158-202">Dados arbitrários podem ser anexado tooan evento, um erro, uma atividade ou uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="3c158-202">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="3c158-203">Estes dados podem ser estruturados utilizando um dicionário.</span><span class="sxs-lookup"><span data-stu-id="3c158-203">These data can be structured using a dictionary.</span></span> <span data-ttu-id="3c158-204">As chaves e valores podem ser de qualquer tipo.</span><span class="sxs-lookup"><span data-stu-id="3c158-204">Keys and values can be of any type.</span></span>

<span data-ttu-id="3c158-205">Dados extras são serializados se quiser tooinsert seu próprio tipo na extras terá tooadd um contrato de dados para este tipo.</span><span class="sxs-lookup"><span data-stu-id="3c158-205">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="3c158-206">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3c158-206">Example</span></span>
<span data-ttu-id="3c158-207">Iremos criar uma nova classe "Pessoa".</span><span class="sxs-lookup"><span data-stu-id="3c158-207">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Engagement.Agent
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

<span data-ttu-id="3c158-208">Em seguida, iremos adicionar um `Person` tooan instância adicional.</span><span class="sxs-lookup"><span data-stu-id="3c158-208">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="3c158-209">Se o put outros tipos de objetos, certifique-se o método ToString () tooreturn implementada uma cadeia legível humana.</span><span class="sxs-lookup"><span data-stu-id="3c158-209">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="3c158-210">Limites</span><span class="sxs-lookup"><span data-stu-id="3c158-210">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="3c158-211">Chaves</span><span class="sxs-lookup"><span data-stu-id="3c158-211">Keys</span></span>
<span data-ttu-id="3c158-212">Cada chave no objeto de Olá tem de corresponder ao hello seguintes expressão regular:</span><span class="sxs-lookup"><span data-stu-id="3c158-212">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="3c158-213">Significa que as chaves tem de começar com, pelo menos, uma letra, seguido de letras, dígitos ou carateres de sublinhado (\_).</span><span class="sxs-lookup"><span data-stu-id="3c158-213">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="3c158-214">Tamanho</span><span class="sxs-lookup"><span data-stu-id="3c158-214">Size</span></span>
<span data-ttu-id="3c158-215">Extras estão limitadas demasiado**1024** carateres por chamada.</span><span class="sxs-lookup"><span data-stu-id="3c158-215">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="3c158-216">Informações de relatórios de aplicações</span><span class="sxs-lookup"><span data-stu-id="3c158-216">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="3c158-217">Referência</span><span class="sxs-lookup"><span data-stu-id="3c158-217">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="3c158-218">Manualmente pode comunicar informações (ou quaisquer outras informações específicas da aplicação) utilizando Olá SendAppInfo() função de controlo.</span><span class="sxs-lookup"><span data-stu-id="3c158-218">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="3c158-219">Tenha em atenção que estas informações podem ser enviadas de forma incremental: apenas Olá valor mais recente para uma determinada chave será mantido para um determinado dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3c158-219">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="3c158-220">Como extras de evento, utilizar um dicionário\<objeto, objeto\> tooattach informations.</span><span class="sxs-lookup"><span data-stu-id="3c158-220">Like event extras, use a Dictionary\<object, object\> tooattach informations.</span></span>

### <a name="example"></a><span data-ttu-id="3c158-221">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3c158-221">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="3c158-222">Limites</span><span class="sxs-lookup"><span data-stu-id="3c158-222">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="3c158-223">Chaves</span><span class="sxs-lookup"><span data-stu-id="3c158-223">Keys</span></span>
<span data-ttu-id="3c158-224">Cada chave no objeto de Olá tem de corresponder ao hello seguintes expressão regular:</span><span class="sxs-lookup"><span data-stu-id="3c158-224">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="3c158-225">Significa que as chaves tem de começar com, pelo menos, uma letra, seguido de letras, dígitos ou carateres de sublinhado (\_).</span><span class="sxs-lookup"><span data-stu-id="3c158-225">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="3c158-226">Tamanho</span><span class="sxs-lookup"><span data-stu-id="3c158-226">Size</span></span>
<span data-ttu-id="3c158-227">As informações da aplicação são limitadas demasiado**1024** carateres por chamada.</span><span class="sxs-lookup"><span data-stu-id="3c158-227">Application information are limited too**1024** characters per call.</span></span>

<span data-ttu-id="3c158-228">Olá anterior exemplo, Olá JSON enviado toohello servidor é 44 carateres de comprimento:</span><span class="sxs-lookup"><span data-stu-id="3c158-228">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a><span data-ttu-id="3c158-229">Registo</span><span class="sxs-lookup"><span data-stu-id="3c158-229">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="3c158-230">Ativar o registo</span><span class="sxs-lookup"><span data-stu-id="3c158-230">Enable Logging</span></span>
<span data-ttu-id="3c158-231">Olá SDK pode ser configurado tooproduce registos de teste na consola do Olá IDE.</span><span class="sxs-lookup"><span data-stu-id="3c158-231">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="3c158-232">Estes registos não estão ativados por predefinição.</span><span class="sxs-lookup"><span data-stu-id="3c158-232">These logs are not activated by default.</span></span> <span data-ttu-id="3c158-233">toocustomize propriedade de Olá, atualização `EngagementAgent.Instance.TestLogEnabled` tooone do valor de Olá disponível a partir do Olá `EngagementTestLogLevel` enumeração, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3c158-233">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
