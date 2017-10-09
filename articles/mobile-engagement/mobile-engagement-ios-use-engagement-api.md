---
title: "aaaHow tooUse Olá Engagement API no iOS"
description: "SDK - mais recente do iOS como tooUse Olá o Engagement API no iOS"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1fb4509e-3804-46c1-949f-1cf727f91f9f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 7fb9b95ad319cf3b1e2de81b5d6aee5b30266069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-ios"></a><span data-ttu-id="cb67f-103">Como tooUse Olá o Engagement API no iOS</span><span class="sxs-lookup"><span data-stu-id="cb67f-103">How tooUse hello Engagement API on iOS</span></span>
<span data-ttu-id="cb67f-104">Este documento é um documento de toohello suplemento como tooIntegrate o Engagement no iOS: fornece na profundidade obter detalhes sobre como toouse Olá Engagement API tooreport as estatísticas da aplicação.</span><span class="sxs-lookup"><span data-stu-id="cb67f-104">This document is an add-on toohello document How tooIntegrate Engagement on iOS: it provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="cb67f-105">Tenha em atenção que o se pretender que apenas Engagement tooreport da sua aplicação sessões, atividades, as falhas e obter informações técnicas, em seguida, hello mais simples é forma toomake todos os seus custom `UIViewController` objetos herdarem Olá correspondente `EngagementViewController` classe .</span><span class="sxs-lookup"><span data-stu-id="cb67f-105">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your custom `UIViewController` objects inherit from hello corresponding `EngagementViewController` class.</span></span>

<span data-ttu-id="cb67f-106">Se quiser toodo mais, por exemplo, se precisar de eventos específicos de aplicação tooreport, erros e tarefas, ou se tiver tooreport as atividades da aplicação de forma diferente que Olá um implementado no Olá `EngagementViewController` classes, em seguida, terá de toouse Olá Engagement API.</span><span class="sxs-lookup"><span data-stu-id="cb67f-106">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementViewController` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="cb67f-107">Olá Engagement API é fornecida pela Olá `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="cb67f-107">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="cb67f-108">Uma instância desta classe pode ser obtida ao chamar Olá `[EngagementAgent shared]` método estático (tenha em atenção que Olá `EngagementAgent` objeto devolvido é um singleton).</span><span class="sxs-lookup"><span data-stu-id="cb67f-108">An instance of this class can be retrieved by calling hello `[EngagementAgent shared]` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

<span data-ttu-id="cb67f-109">Antes de quaisquer chamadas à API, hello `EngagementAgent` objeto tem de ser inicializado ao chamar o método de Olá`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span><span class="sxs-lookup"><span data-stu-id="cb67f-109">Before any API calls, hello `EngagementAgent` object must be initialized by calling hello method `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="cb67f-110">Conceitos de envolvimento</span><span class="sxs-lookup"><span data-stu-id="cb67f-110">Engagement concepts</span></span>
<span data-ttu-id="cb67f-111">Olá seguintes partes refinar Olá comuns [conceitos do Mobile Engagement](mobile-engagement-concepts.md) para a plataforma de iOS Olá.</span><span class="sxs-lookup"><span data-stu-id="cb67f-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for hello iOS platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="cb67f-112">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="cb67f-112">`Session` and `Activity`</span></span>
<span data-ttu-id="cb67f-113">Um *atividade* é normalmente associadas um ecrã da aplicação Olá, que é toosay Olá *atividade* inicia quando o ecrã de Olá é apresentado e para quando o ecrã de Olá está fechado: Este é Olá caso quando Olá Engagement SDK é integrado utilizando Olá `EngagementViewController` classes.</span><span class="sxs-lookup"><span data-stu-id="cb67f-113">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementViewController` classes.</span></span>

<span data-ttu-id="cb67f-114">Mas *atividades* também pode ser controlado manualmente utilizando Olá o Engagement API.</span><span class="sxs-lookup"><span data-stu-id="cb67f-114">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="cb67f-115">Isto permite que toosplit um ecrã específico na várias sub partes tooget Olá, obter mais detalhes sobre a utilização deste ecrã (por exemplo tooknown frequência e quanto as caixas de diálogo são utilizadas dentro este ecrã).</span><span class="sxs-lookup"><span data-stu-id="cb67f-115">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="cb67f-116">Relatório de atividades</span><span class="sxs-lookup"><span data-stu-id="cb67f-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="cb67f-117">Utilizador inicia uma nova atividade</span><span class="sxs-lookup"><span data-stu-id="cb67f-117">User starts a new Activity</span></span>
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

<span data-ttu-id="cb67f-118">Terá de toocall `startActivity()` cada atividade de utilizador de Olá de hora é alterado.</span><span class="sxs-lookup"><span data-stu-id="cb67f-118">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="cb67f-119">Olá primeira chamada toothis função inicia uma nova sessão de utilizador.</span><span class="sxs-lookup"><span data-stu-id="cb67f-119">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="cb67f-120">Utilizador termina a atividade atual</span><span class="sxs-lookup"><span data-stu-id="cb67f-120">User ends his current Activity</span></span>
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> <span data-ttu-id="cb67f-121">Deve **nunca** chamar esta função por si, exceto se quiser toosplit uma utilização da sua aplicação para várias sessões: uma chamada de função toothis terminaria Olá imediatamente, a sessão atual deste modo, uma chamada subsequente demasiado`startActivity()`seria iniciar uma sessão de novo.</span><span class="sxs-lookup"><span data-stu-id="cb67f-121">You should **NEVER** call this function by yourself, except if you want toosplit one use of your application into several sessions: a call toothis function would end hello current session immediately, so, a subsequent call too`startActivity()` would start a new session.</span></span> <span data-ttu-id="cb67f-122">Esta função é chamada automaticamente por Olá SDK quando a aplicação está fechada.</span><span class="sxs-lookup"><span data-stu-id="cb67f-122">This function is automatically called by hello SDK when your application is closed.</span></span>
> 
> 

## <a name="reporting-events"></a><span data-ttu-id="cb67f-123">Eventos de relatório</span><span class="sxs-lookup"><span data-stu-id="cb67f-123">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="cb67f-124">Eventos da sessão</span><span class="sxs-lookup"><span data-stu-id="cb67f-124">Session events</span></span>
<span data-ttu-id="cb67f-125">Eventos da sessão são ações de Olá tooreport normalmente utilizadas realizadas por um utilizador durante a sua sessão.</span><span class="sxs-lookup"><span data-stu-id="cb67f-125">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="cb67f-126">**Exemplo sem dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="cb67f-126">**Example without extra data:**</span></span>

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:nil];
            ...
       }
       [...]
    }

<span data-ttu-id="cb67f-127">**Exemplo com dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="cb67f-127">**Example with extra data:**</span></span>

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        NSMutableDictionary* extras = [NSMutableDictionary dictionary];
        [extras setObject:[NSNumber numberWithInt:toInterfaceOrientation] forKey:@"to_orientation_id"];
        [extras setObject:[NSNumber numberWithDouble:duration] forKey:@"duration"];
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:extras];
            ...
       }
       [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="cb67f-128">Eventos de autónomo</span><span class="sxs-lookup"><span data-stu-id="cb67f-128">Standalone events</span></span>
<span data-ttu-id="cb67f-129">Eventos de contrary toosession, autónomo eventos podem ser utilizados fora do contexto de Olá de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="cb67f-129">Contrary toosession events, standalone events can be used outside of hello context of a session.</span></span>

<span data-ttu-id="cb67f-130">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="cb67f-130">**Example:**</span></span>

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a><span data-ttu-id="cb67f-131">Relatório de erros</span><span class="sxs-lookup"><span data-stu-id="cb67f-131">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="cb67f-132">Erros de sessão</span><span class="sxs-lookup"><span data-stu-id="cb67f-132">Session errors</span></span>
<span data-ttu-id="cb67f-133">Erros de sessão são normalmente utilizadas tooreport Olá erros afetar utilizador Olá durante a sua sessão.</span><span class="sxs-lookup"><span data-stu-id="cb67f-133">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="cb67f-134">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="cb67f-134">**Example:**</span></span>

    /** hello user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* hello user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="cb67f-135">Erros de autónomo</span><span class="sxs-lookup"><span data-stu-id="cb67f-135">Standalone errors</span></span>
<span data-ttu-id="cb67f-136">Contrary toosession erros, erros autónomo podem ser utilizados fora do contexto de Olá de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="cb67f-136">Contrary toosession errors, standalone errors can be used outside of hello context of a session.</span></span>

<span data-ttu-id="cb67f-137">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="cb67f-137">**Example:**</span></span>

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a><span data-ttu-id="cb67f-138">Tarefas de relatório</span><span class="sxs-lookup"><span data-stu-id="cb67f-138">Reporting Jobs</span></span>
<span data-ttu-id="cb67f-139">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="cb67f-139">**Example:**</span></span>

<span data-ttu-id="cb67f-140">Suponha que pretende que a duração de Olá tooreport do processo de início de sessão:</span><span class="sxs-lookup"><span data-stu-id="cb67f-140">Suppose you want tooreport hello duration of your login process:</span></span>

    [...]
    -(void)signIn
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      [... sign in ...]

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    }
    [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="cb67f-141">Relatório de erros durante a uma tarefa</span><span class="sxs-lookup"><span data-stu-id="cb67f-141">Report Errors during a Job</span></span>
<span data-ttu-id="cb67f-142">Erros podem ser tooa relacionado com a tarefa em vez de ser relacionadas com toohello sessão do utilizador atual.</span><span class="sxs-lookup"><span data-stu-id="cb67f-142">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="cb67f-143">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="cb67f-143">**Example:**</span></span>

<span data-ttu-id="cb67f-144">Suponha que pretende tooreport um erro durante o processo de início de sessão:</span><span class="sxs-lookup"><span data-stu-id="cb67f-144">Suppose you want tooreport an error during your login process:</span></span>

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try toosign in */
        NSError* error = nil;
        [self trySigin:&error];
        success = error == nil;

        /* If an error occured report it */
        if(!success)
        {
          [[EngagementAgent shared] sendJobError:@"sign_in_error"
                         jobName:@"sign_in"
                          extras:[NSDictionary dictionaryWithObject:[error localizedDescription] forKey:@"error"]];

          /* Retry after a moment */
          [NSThread sleepForTimeInterval:20];
        }
      }

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    };
    [...]

### <a name="events-during-a-job"></a><span data-ttu-id="cb67f-145">Eventos durante uma tarefa</span><span class="sxs-lookup"><span data-stu-id="cb67f-145">Events during a job</span></span>
<span data-ttu-id="cb67f-146">Eventos podem ser tooa relacionado com a tarefa em vez de ser relacionadas com toohello sessão do utilizador atual.</span><span class="sxs-lookup"><span data-stu-id="cb67f-146">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="cb67f-147">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="cb67f-147">**Example:**</span></span>

<span data-ttu-id="cb67f-148">Suponha que temos uma rede social e Utilizamos um tarefa tooreport Olá tempo total durante o qual Olá utilizador é o servidor de toohello ligado.</span><span class="sxs-lookup"><span data-stu-id="cb67f-148">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="cb67f-149">utilizador Olá pode receber mensagens dos seus amigos, este é um evento de tarefa.</span><span class="sxs-lookup"><span data-stu-id="cb67f-149">hello user can receive messages from his friends, this is a job event.</span></span>

    [...]
    - (void) signin
    {
      [...Sign in code...]
      [[EngagementAgent shared] startJob:@"connection" extras:nil];
    }
    [...]
    - (void) signout
    {
      [...Sign out code...]
      [[EngagementAgent shared] endJob:@"connection"];
    }
    [...]
    - (void) onMessageReceived
    {
      [...Notify user...]
      [[EngagementAgent shared] sendJobEvent:@"connection" jobName:@"message_received" extras:nil];
    }
    [...]

## <a name="extra-parameters"></a><span data-ttu-id="cb67f-150">Parâmetros adicionais</span><span class="sxs-lookup"><span data-stu-id="cb67f-150">Extra parameters</span></span>
<span data-ttu-id="cb67f-151">Dados arbitrários podem ser anexado tooevents, erros, atividades e tarefas.</span><span class="sxs-lookup"><span data-stu-id="cb67f-151">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="cb67f-152">Estes dados podem ser estruturados, utiliza a classe de NSDictionary do iOS.</span><span class="sxs-lookup"><span data-stu-id="cb67f-152">This data can be structured, it uses iOS's NSDictionary class.</span></span>

<span data-ttu-id="cb67f-153">Tenha em atenção que podem conter extras `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` ou outros `NSDictionary` instâncias.</span><span class="sxs-lookup"><span data-stu-id="cb67f-153">Note that extras can contain `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` or other `NSDictionary` instances.</span></span>

> [!NOTE]
> <span data-ttu-id="cb67f-154">Olá parâmetro adicional é serializado no JSON.</span><span class="sxs-lookup"><span data-stu-id="cb67f-154">hello extra parameter is serialized in JSON.</span></span> <span data-ttu-id="cb67f-155">Se quiser toopass diferentes objetos que Olá aqueles descrito acima, tem de implementar Olá seguinte método na sua classe:</span><span class="sxs-lookup"><span data-stu-id="cb67f-155">If you want toopass different objects than hello ones described above, you must implement hello following method in your class:</span></span>
> 
> <span data-ttu-id="cb67f-156">-(NSString*) JSONRepresentation;</span><span class="sxs-lookup"><span data-stu-id="cb67f-156">-(NSString*)JSONRepresentation;</span></span>
> 
> <span data-ttu-id="cb67f-157">método de Olá deve devolver uma representação JSON do seu objeto.</span><span class="sxs-lookup"><span data-stu-id="cb67f-157">hello method should return a JSON representation of your object.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="cb67f-158">Exemplo</span><span class="sxs-lookup"><span data-stu-id="cb67f-158">Example</span></span>
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a><span data-ttu-id="cb67f-159">Limites</span><span class="sxs-lookup"><span data-stu-id="cb67f-159">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="cb67f-160">Chaves</span><span class="sxs-lookup"><span data-stu-id="cb67f-160">Keys</span></span>
<span data-ttu-id="cb67f-161">Cada chave no Olá `NSDictionary` tem de corresponder ao hello seguintes expressão regular:</span><span class="sxs-lookup"><span data-stu-id="cb67f-161">Each key in hello `NSDictionary` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="cb67f-162">Significa que as chaves tem de começar com, pelo menos, uma letra, seguido de letras, dígitos ou carateres de sublinhado (\_).</span><span class="sxs-lookup"><span data-stu-id="cb67f-162">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="cb67f-163">Tamanho</span><span class="sxs-lookup"><span data-stu-id="cb67f-163">Size</span></span>
<span data-ttu-id="cb67f-164">Extras estão limitadas demasiado**1024** carateres por chamada (uma vez codificados em JSON pelo agente de envolvimento Olá).</span><span class="sxs-lookup"><span data-stu-id="cb67f-164">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement agent).</span></span>

<span data-ttu-id="cb67f-165">Olá anterior exemplo, Olá JSON enviado toohello servidor é 58 carateres de comprimento:</span><span class="sxs-lookup"><span data-stu-id="cb67f-165">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="cb67f-166">Informações de relatórios de aplicações</span><span class="sxs-lookup"><span data-stu-id="cb67f-166">Reporting Application Information</span></span>
<span data-ttu-id="cb67f-167">Pode comunicar manualmente controlo informações (ou quaisquer outras informações específicas da aplicação) utilizando Olá `sendAppInfo:` função.</span><span class="sxs-lookup"><span data-stu-id="cb67f-167">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo:` function.</span></span>

<span data-ttu-id="cb67f-168">Tenha em atenção que estas informações podem ser enviadas de forma incremental: apenas Olá valor mais recente para uma determinada chave será mantido para um determinado dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cb67f-168">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="cb67f-169">Como extras de evento, hello `NSDictionary` classe é utilizada tooabstract informações da aplicação, tenha em atenção que as matrizes ou dicionários secundárias serão tratados como cadeias simples (com a serialização do JSON).</span><span class="sxs-lookup"><span data-stu-id="cb67f-169">Like event extras, hello `NSDictionary` class is used tooabstract application information, note that arrays or sub-dictionaries will be treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="cb67f-170">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="cb67f-170">**Example:**</span></span>

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a><span data-ttu-id="cb67f-171">Limites</span><span class="sxs-lookup"><span data-stu-id="cb67f-171">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="cb67f-172">Chaves</span><span class="sxs-lookup"><span data-stu-id="cb67f-172">Keys</span></span>
<span data-ttu-id="cb67f-173">Cada chave no Olá `NSDictionary` tem de corresponder ao hello seguintes expressão regular:</span><span class="sxs-lookup"><span data-stu-id="cb67f-173">Each key in hello `NSDictionary` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="cb67f-174">Significa que as chaves tem de começar com, pelo menos, uma letra, seguido de letras, dígitos ou carateres de sublinhado (\_).</span><span class="sxs-lookup"><span data-stu-id="cb67f-174">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="cb67f-175">Tamanho</span><span class="sxs-lookup"><span data-stu-id="cb67f-175">Size</span></span>
<span data-ttu-id="cb67f-176">As informações da aplicação são limitadas demasiado**1024** carateres por chamada (uma vez codificados em JSON pelo agente de envolvimento Olá).</span><span class="sxs-lookup"><span data-stu-id="cb67f-176">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement agent).</span></span>

<span data-ttu-id="cb67f-177">Olá anterior exemplo, Olá JSON enviado toohello servidor é 44 carateres de comprimento:</span><span class="sxs-lookup"><span data-stu-id="cb67f-177">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
