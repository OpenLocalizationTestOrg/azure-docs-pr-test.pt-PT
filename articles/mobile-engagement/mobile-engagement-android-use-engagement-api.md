---
title: "aaaHow tooUse Olá Engagement API no Android"
description: "SDK Android mais recente - como tooUse Olá o Engagement API no Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 09b62659-82ae-4a55-8784-fca0b6b22eaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: article
ms.date: 07/25/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e0b2d484616c0c7874e77c5283d94c3063949ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-android"></a><span data-ttu-id="4a193-103">Como tooUse Olá o Engagement API no Android</span><span class="sxs-lookup"><span data-stu-id="4a193-103">How tooUse hello Engagement API on Android</span></span>
<span data-ttu-id="4a193-104">Este documento é um documento de toohello suplemento [opções avançadas de relatórios para o Android SDK do Mobile Engagement](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="4a193-104">This document is an add-on toohello document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span></span> <span data-ttu-id="4a193-105">Fornece na profundidade obter detalhes sobre como toouse Olá Engagement API tooreport as estatísticas da aplicação.</span><span class="sxs-lookup"><span data-stu-id="4a193-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="4a193-106">Tenha em atenção que, se quiser apenas o Engagement tooreport da sua aplicação sessões, atividades, as falhas e obter informações técnicas, em seguida, hello forma mais simples é toomake todos os seus `Activity` classes secundárias herdarem Olá correspondente `EngagementActivity` classe.</span><span class="sxs-lookup"><span data-stu-id="4a193-106">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Activity` sub-classes inherit from hello corresponding `EngagementActivity` class.</span></span>

<span data-ttu-id="4a193-107">Se quiser toodo mais, por exemplo, se precisar de eventos específicos de aplicação tooreport, erros e tarefas, ou se tiver tooreport as atividades da aplicação de forma diferente que Olá um implementado no Olá `EngagementActivity` classes, em seguida, terá de toouse Olá Engagement API.</span><span class="sxs-lookup"><span data-stu-id="4a193-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementActivity` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="4a193-108">Olá Engagement API é fornecida pela Olá `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="4a193-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="4a193-109">Uma instância desta classe pode ser obtida ao chamar Olá `EngagementAgent.getInstance(Context)` método estático (tenha em atenção que Olá `EngagementAgent` objeto devolvido é um singleton).</span><span class="sxs-lookup"><span data-stu-id="4a193-109">An instance of this class can be retrieved by calling hello `EngagementAgent.getInstance(Context)` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="4a193-110">Conceitos de envolvimento</span><span class="sxs-lookup"><span data-stu-id="4a193-110">Engagement concepts</span></span>
<span data-ttu-id="4a193-111">Olá seguintes partes refinar Olá comuns [conceitos do Mobile Engagement](mobile-engagement-concepts.md), para a plataforma Android Olá.</span><span class="sxs-lookup"><span data-stu-id="4a193-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for hello Android platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="4a193-112">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="4a193-112">`Session` and `Activity`</span></span>
<span data-ttu-id="4a193-113">Se o utilizador Olá permanece mais do que alguns segundos de inatividade entre duas *atividades*, em seguida, a sequência de *atividades* é dividida em duas distintos *sessões*.</span><span class="sxs-lookup"><span data-stu-id="4a193-113">If hello user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*.</span></span> <span data-ttu-id="4a193-114">Estes alguns segundos são denominados Olá "tempo limite de sessão".</span><span class="sxs-lookup"><span data-stu-id="4a193-114">These few seconds are called hello "session timeout".</span></span>

<span data-ttu-id="4a193-115">Um *atividade* é normalmente associadas um ecrã da aplicação Olá, que é toosay Olá *atividade* inicia quando o ecrã de Olá é apresentado e para quando o ecrã de Olá está fechado: Este é Olá caso quando Olá Engagement SDK é integrado utilizando Olá `EngagementActivity` classes.</span><span class="sxs-lookup"><span data-stu-id="4a193-115">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementActivity` classes.</span></span>

<span data-ttu-id="4a193-116">Mas *atividades* também pode ser controlado manualmente utilizando Olá o Engagement API.</span><span class="sxs-lookup"><span data-stu-id="4a193-116">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="4a193-117">Isto permite que toosplit um ecrã específico na várias sub partes tooget Olá, obter mais detalhes sobre a utilização deste ecrã (por exemplo tooknown frequência e quanto as caixas de diálogo são utilizadas dentro este ecrã).</span><span class="sxs-lookup"><span data-stu-id="4a193-117">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="4a193-118">Relatório de atividades</span><span class="sxs-lookup"><span data-stu-id="4a193-118">Reporting Activities</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4a193-119">Não precisa de tooreport atividades, como descrito nesta secção se estiver a utilizar Olá `EngagementActivity` classe e o respetivos variantes conforme explicado no Olá como tooIntegrate o Engagement num documento do Android.</span><span class="sxs-lookup"><span data-stu-id="4a193-119">You don't need tooreport activities like described in this section if you are using hello `EngagementActivity` class and its variants as explained in hello How tooIntegrate Engagement on Android document.</span></span>
> 
> 

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="4a193-120">Utilizador inicia uma nova atividade</span><span class="sxs-lookup"><span data-stu-id="4a193-120">User starts a new Activity</span></span>
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

<span data-ttu-id="4a193-121">Terá de toocall `startActivity()` cada atividade de utilizador de Olá de hora é alterado.</span><span class="sxs-lookup"><span data-stu-id="4a193-121">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="4a193-122">Olá primeira chamada toothis função inicia uma nova sessão de utilizador.</span><span class="sxs-lookup"><span data-stu-id="4a193-122">hello first call toothis function starts a new user session.</span></span>

<span data-ttu-id="4a193-123">Olá melhor local toocall, esta função é em cada atividade `onResume` chamada de retorno.</span><span class="sxs-lookup"><span data-stu-id="4a193-123">hello best place toocall this function is on each activity `onResume` callback.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="4a193-124">Utilizador termina a atividade atual</span><span class="sxs-lookup"><span data-stu-id="4a193-124">User ends his current Activity</span></span>
            EngagementAgent.getInstance(this).endActivity();

<span data-ttu-id="4a193-125">Terá de toocall `endActivity()` , pelo menos, uma vez quando o utilizador Olá conclui a última atividade.</span><span class="sxs-lookup"><span data-stu-id="4a193-125">You need toocall `endActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="4a193-126">Informa Olá irá expirar o Engagement SDK que utilizador Olá está atualmente inativa, e uma vez que a sessão de utilizador Olá tem toobe fechado Olá tempo limite da sessão (se chamar `startActivity()` antes do tempo limite da sessão Olá expira, a sessão Olá simplesmente é retomado).</span><span class="sxs-lookup"><span data-stu-id="4a193-126">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `startActivity()` before hello session timeout expires, hello session is simply resumed).</span></span>

<span data-ttu-id="4a193-127">Olá melhor local toocall, esta função é em cada atividade `onPause` chamada de retorno.</span><span class="sxs-lookup"><span data-stu-id="4a193-127">hello best place toocall this function is on each activity `onPause` callback.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="4a193-128">Eventos de relatório</span><span class="sxs-lookup"><span data-stu-id="4a193-128">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="4a193-129">Eventos da sessão</span><span class="sxs-lookup"><span data-stu-id="4a193-129">Session events</span></span>
<span data-ttu-id="4a193-130">Eventos da sessão são ações de Olá tooreport normalmente utilizadas realizadas por um utilizador durante a sua sessão.</span><span class="sxs-lookup"><span data-stu-id="4a193-130">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="4a193-131">**Exemplo sem dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="4a193-131">**Example without extra data:**</span></span>

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

<span data-ttu-id="4a193-132">**Exemplo com dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="4a193-132">**Example with extra data:**</span></span>

            public MyActivity extends EngagementActivity {
              [...]
              @Override
              public boolean onMenuItemSelected(int featureId, MenuItem item) {
                Bundle extras = new Bundle();
                extras.putInt("id", item.getItemId());
                getEngagementAgent().sendSessionEvent("menu_selected", extras);
              }
              [...]
            }

### <a name="standalone-events"></a><span data-ttu-id="4a193-133">Eventos de autónomo</span><span class="sxs-lookup"><span data-stu-id="4a193-133">Standalone Events</span></span>
<span data-ttu-id="4a193-134">Eventos de contrary toosession, podem ocorrer eventos de autónomo fora do contexto de Olá de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="4a193-134">Contrary toosession events, standalone events can occur outside of hello context of a session.</span></span>

<span data-ttu-id="4a193-135">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="4a193-135">**Example:**</span></span>

<span data-ttu-id="4a193-136">Suponha que pretende que os eventos de tooreport ocorrer quando é acionado um recetor difusão:</span><span class="sxs-lookup"><span data-stu-id="4a193-136">Suppose you want tooreport events occurring when a broadcast receiver is triggered:</span></span>

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a><span data-ttu-id="4a193-137">Relatório de erros</span><span class="sxs-lookup"><span data-stu-id="4a193-137">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="4a193-138">Erros de sessão</span><span class="sxs-lookup"><span data-stu-id="4a193-138">Session errors</span></span>
<span data-ttu-id="4a193-139">Erros de sessão são normalmente utilizadas tooreport Olá erros afetar utilizador Olá durante a sua sessão.</span><span class="sxs-lookup"><span data-stu-id="4a193-139">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="4a193-140">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="4a193-140">**Example:**</span></span>

            /** hello user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* hello user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a><span data-ttu-id="4a193-141">Erros de autónomo</span><span class="sxs-lookup"><span data-stu-id="4a193-141">Standalone errors</span></span>
<span data-ttu-id="4a193-142">Erros de contrary toosession, autónomo erros podem ocorrer fora do contexto de Olá de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="4a193-142">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

<span data-ttu-id="4a193-143">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="4a193-143">**Example:**</span></span>

<span data-ttu-id="4a193-144">Olá exemplo seguinte mostra como tooreport erro sempre que a memória de Olá fica baixa no telemóvel Olá durante o processo de aplicação está em execução.</span><span class="sxs-lookup"><span data-stu-id="4a193-144">hello following example shows how tooreport an error whenever hello memory becomes low on hello phone while your application process is running.</span></span>

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a><span data-ttu-id="4a193-145">Tarefas de relatório</span><span class="sxs-lookup"><span data-stu-id="4a193-145">Reporting Jobs</span></span>
### <a name="example"></a><span data-ttu-id="4a193-146">Exemplo</span><span class="sxs-lookup"><span data-stu-id="4a193-146">Example</span></span>
<span data-ttu-id="4a193-147">Suponha que pretende que a duração de Olá tooreport do processo de início de sessão:</span><span class="sxs-lookup"><span data-stu-id="4a193-147">Suppose you want tooreport hello duration of your login process:</span></span>

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="4a193-148">Relatório de erros durante a uma tarefa</span><span class="sxs-lookup"><span data-stu-id="4a193-148">Report Errors during a Job</span></span>
<span data-ttu-id="4a193-149">Erros podem ser tooa relacionado com a tarefa em vez de ser relacionadas com toohello sessão do utilizador atual.</span><span class="sxs-lookup"><span data-stu-id="4a193-149">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="4a193-150">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="4a193-150">**Example:**</span></span>

<span data-ttu-id="4a193-151">Suponha que pretende tooreport um erro durante a iniciar sessão no processo:</span><span class="sxs-lookup"><span data-stu-id="4a193-151">Suppose you want tooreport an error during you login process:</span></span>

<span data-ttu-id="4a193-152">[...] signIn void público (contexto contexto,...) {</span><span class="sxs-lookup"><span data-stu-id="4a193-152">[...] public void signIn(Context context, ...) {</span></span>

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try toosign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report hello error tooEngagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="4a193-153">Eventos de relatório durante uma tarefa</span><span class="sxs-lookup"><span data-stu-id="4a193-153">Reporting Events during a job</span></span>
<span data-ttu-id="4a193-154">Eventos podem ser tooa relacionado com a tarefa em vez de ser relacionadas com toohello sessão do utilizador atual.</span><span class="sxs-lookup"><span data-stu-id="4a193-154">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="4a193-155">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="4a193-155">**Example:**</span></span>

<span data-ttu-id="4a193-156">Suponha que temos uma rede social e Utilizamos um tarefa tooreport Olá tempo total durante o qual Olá utilizador é o servidor de toohello ligado.</span><span class="sxs-lookup"><span data-stu-id="4a193-156">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="4a193-157">utilizador Olá pode permanecer ligado em segundo plano, mesmo quando ele está a utilizar outra aplicação ou quando está suspenso phone Olá, pelo que não existe nenhuma sessão.</span><span class="sxs-lookup"><span data-stu-id="4a193-157">hello user can stay connected in background even when he's using another application or when hello phone is sleeping, so there is no session.</span></span>

<span data-ttu-id="4a193-158">utilizador Olá pode receber mensagens dos seus amigos, este é um evento de tarefa.</span><span class="sxs-lookup"><span data-stu-id="4a193-158">hello user can receive messages from his friends, this is a job event.</span></span>

            [...]
            public void signin(Context context, ...) {
              [...Sign in code...]
              EngagementAgent.getInstance(context).startJob("connection", null);
            }
            [...]
            public void signout(Context context) {
              [...Sign out code...]
              EngagementAgent.getInstance(context).endJob("connection");
            }
            [...]
            public void onMessageReceived(Context context) {
              [...Notify in status bar...]
              EngagementAgent.getInstance(context).sendJobEvent("message_received", "connection", null);
            }
            [...]

## <a name="extra-parameters"></a><span data-ttu-id="4a193-159">Parâmetros adicionais</span><span class="sxs-lookup"><span data-stu-id="4a193-159">Extra parameters</span></span>
<span data-ttu-id="4a193-160">Dados arbitrários podem ser anexado tooevents, erros, atividades e tarefas.</span><span class="sxs-lookup"><span data-stu-id="4a193-160">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="4a193-161">Estes dados podem ser estruturados, utiliza a classe de pacote do Android (na realidade, funciona como parâmetros adicionais no Android pendentes).</span><span class="sxs-lookup"><span data-stu-id="4a193-161">This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents).</span></span> <span data-ttu-id="4a193-162">Tenha em atenção que um grupo pode conter matrizes ou outro instâncias de pacote.</span><span class="sxs-lookup"><span data-stu-id="4a193-162">Note that a Bundle can contain arrays or another Bundle instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4a193-163">Se o put nos parâmetros parcelable ou serializáveis, certifique-se os seus `toString()` método é implementado tooreturn uma cadeia legível por humanos.</span><span class="sxs-lookup"><span data-stu-id="4a193-163">If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented tooreturn a human-readable string.</span></span> <span data-ttu-id="4a193-164">Classes serializáveis que contêm campos não transitórios que não são serializáveis tornará falhas Android quando irá chamar`bundle.putSerializable("key",value);`</span><span class="sxs-lookup"><span data-stu-id="4a193-164">Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`</span></span>
> 
> [!WARNING]
> <span data-ttu-id="4a193-165">Não são suportadas matrizes dispersas nos parâmetros adicionais, ou seja, não irá ser serializada como uma matriz.</span><span class="sxs-lookup"><span data-stu-id="4a193-165">Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array.</span></span> <span data-ttu-id="4a193-166">Deverá convertê-los em matrizes padrão antes de a utilizar nos parâmetros adicionais.</span><span class="sxs-lookup"><span data-stu-id="4a193-166">You should convert them into standard arrays before using it in extra parameters.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="4a193-167">Exemplo</span><span class="sxs-lookup"><span data-stu-id="4a193-167">Example</span></span>
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="4a193-168">Limites</span><span class="sxs-lookup"><span data-stu-id="4a193-168">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="4a193-169">Chaves</span><span class="sxs-lookup"><span data-stu-id="4a193-169">Keys</span></span>
<span data-ttu-id="4a193-170">Cada chave no Olá `Bundle` tem de corresponder ao hello seguintes expressão regular:</span><span class="sxs-lookup"><span data-stu-id="4a193-170">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="4a193-171">Significa que as chaves tem de começar com, pelo menos, uma letra, seguido de letras, dígitos ou carateres de sublinhado (\_).</span><span class="sxs-lookup"><span data-stu-id="4a193-171">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="4a193-172">Tamanho</span><span class="sxs-lookup"><span data-stu-id="4a193-172">Size</span></span>
<span data-ttu-id="4a193-173">Extras estão limitadas demasiado**1024** carateres por chamada (uma vez codificados em JSON pelo serviço de envolvimento Olá).</span><span class="sxs-lookup"><span data-stu-id="4a193-173">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="4a193-174">Olá anterior exemplo, Olá JSON enviado toohello servidor é 58 carateres de comprimento:</span><span class="sxs-lookup"><span data-stu-id="4a193-174">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="4a193-175">Informações de relatórios de aplicações</span><span class="sxs-lookup"><span data-stu-id="4a193-175">Reporting Application Information</span></span>
<span data-ttu-id="4a193-176">Pode comunicar manualmente controlo informações (ou quaisquer outras informações específicas da aplicação) utilizando Olá `sendAppInfo()` função.</span><span class="sxs-lookup"><span data-stu-id="4a193-176">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="4a193-177">Tenha em atenção que estas informações podem ser enviadas de forma incremental: apenas Olá valor mais recente para uma determinada chave será mantido para um determinado dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4a193-177">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="4a193-178">Como extras de evento, Olá classe de pacote utilizados tooabstract informações da aplicação, tenha em atenção que as matrizes ou subplano bundles será tratada como cadeias simples (com a serialização do JSON).</span><span class="sxs-lookup"><span data-stu-id="4a193-178">Like event extras, hello Bundle class is used tooabstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).</span></span>

### <a name="example"></a><span data-ttu-id="4a193-179">Exemplo</span><span class="sxs-lookup"><span data-stu-id="4a193-179">Example</span></span>
<span data-ttu-id="4a193-180">Eis um género de utilizador de toosend de exemplo de código e a data de nascimento:</span><span class="sxs-lookup"><span data-stu-id="4a193-180">Here is a code sample toosend user gender and birthdate:</span></span>

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="4a193-181">Limites</span><span class="sxs-lookup"><span data-stu-id="4a193-181">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="4a193-182">Chaves</span><span class="sxs-lookup"><span data-stu-id="4a193-182">Keys</span></span>
<span data-ttu-id="4a193-183">Cada chave no Olá `Bundle` tem de corresponder ao hello seguintes expressão regular:</span><span class="sxs-lookup"><span data-stu-id="4a193-183">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="4a193-184">Significa que as chaves tem de começar com, pelo menos, uma letra, seguido de letras, dígitos ou carateres de sublinhado (\_).</span><span class="sxs-lookup"><span data-stu-id="4a193-184">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="4a193-185">Tamanho</span><span class="sxs-lookup"><span data-stu-id="4a193-185">Size</span></span>
<span data-ttu-id="4a193-186">As informações da aplicação são limitadas demasiado**1024** carateres por chamada (uma vez codificados em JSON pelo serviço de envolvimento Olá).</span><span class="sxs-lookup"><span data-stu-id="4a193-186">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="4a193-187">Olá anterior exemplo, Olá JSON enviado toohello servidor é 44 carateres de comprimento:</span><span class="sxs-lookup"><span data-stu-id="4a193-187">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"expiration":"2016-12-07","status":"premium"}
