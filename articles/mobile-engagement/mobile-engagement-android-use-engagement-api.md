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
# <a name="how-toouse-hello-engagement-api-on-android"></a>Como tooUse Olá o Engagement API no Android
Este documento é um documento de toohello suplemento [opções avançadas de relatórios para o Android SDK do Mobile Engagement](mobile-engagement-android-advanced-reporting.md). Fornece na profundidade obter detalhes sobre como toouse Olá Engagement API tooreport as estatísticas da aplicação.

Tenha em atenção que, se quiser apenas o Engagement tooreport da sua aplicação sessões, atividades, as falhas e obter informações técnicas, em seguida, hello forma mais simples é toomake todos os seus `Activity` classes secundárias herdarem Olá correspondente `EngagementActivity` classe.

Se quiser toodo mais, por exemplo, se precisar de eventos específicos de aplicação tooreport, erros e tarefas, ou se tiver tooreport as atividades da aplicação de forma diferente que Olá um implementado no Olá `EngagementActivity` classes, em seguida, terá de toouse Olá Engagement API.

Olá Engagement API é fornecida pela Olá `EngagementAgent` classe. Uma instância desta classe pode ser obtida ao chamar Olá `EngagementAgent.getInstance(Context)` método estático (tenha em atenção que Olá `EngagementAgent` objeto devolvido é um singleton).

## <a name="engagement-concepts"></a>Conceitos de envolvimento
Olá seguintes partes refinar Olá comuns [conceitos do Mobile Engagement](mobile-engagement-concepts.md), para a plataforma Android Olá.

### <a name="session-and-activity"></a>`Session` e `Activity`
Se o utilizador Olá permanece mais do que alguns segundos de inatividade entre duas *atividades*, em seguida, a sequência de *atividades* é dividida em duas distintos *sessões*. Estes alguns segundos são denominados Olá "tempo limite de sessão".

Um *atividade* é normalmente associadas um ecrã da aplicação Olá, que é toosay Olá *atividade* inicia quando o ecrã de Olá é apresentado e para quando o ecrã de Olá está fechado: Este é Olá caso quando Olá Engagement SDK é integrado utilizando Olá `EngagementActivity` classes.

Mas *atividades* também pode ser controlado manualmente utilizando Olá o Engagement API. Isto permite que toosplit um ecrã específico na várias sub partes tooget Olá, obter mais detalhes sobre a utilização deste ecrã (por exemplo tooknown frequência e quanto as caixas de diálogo são utilizadas dentro este ecrã).

## <a name="reporting-activities"></a>Relatório de atividades
> [!IMPORTANT]
> Não precisa de tooreport atividades, como descrito nesta secção se estiver a utilizar Olá `EngagementActivity` classe e o respetivos variantes conforme explicado no Olá como tooIntegrate o Engagement num documento do Android.
> 
> 

### <a name="user-starts-a-new-activity"></a>Utilizador inicia uma nova atividade
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

Terá de toocall `startActivity()` cada atividade de utilizador de Olá de hora é alterado. Olá primeira chamada toothis função inicia uma nova sessão de utilizador.

Olá melhor local toocall, esta função é em cada atividade `onResume` chamada de retorno.

### <a name="user-ends-his-current-activity"></a>Utilizador termina a atividade atual
            EngagementAgent.getInstance(this).endActivity();

Terá de toocall `endActivity()` , pelo menos, uma vez quando o utilizador Olá conclui a última atividade. Informa Olá irá expirar o Engagement SDK que utilizador Olá está atualmente inativa, e uma vez que a sessão de utilizador Olá tem toobe fechado Olá tempo limite da sessão (se chamar `startActivity()` antes do tempo limite da sessão Olá expira, a sessão Olá simplesmente é retomado).

Olá melhor local toocall, esta função é em cada atividade `onPause` chamada de retorno.

## <a name="reporting-events"></a>Eventos de relatório
### <a name="session-events"></a>Eventos da sessão
Eventos da sessão são ações de Olá tooreport normalmente utilizadas realizadas por um utilizador durante a sua sessão.

**Exemplo sem dados adicionais:**

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

**Exemplo com dados adicionais:**

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

### <a name="standalone-events"></a>Eventos de autónomo
Eventos de contrary toosession, podem ocorrer eventos de autónomo fora do contexto de Olá de uma sessão.

**Exemplo:**

Suponha que pretende que os eventos de tooreport ocorrer quando é acionado um recetor difusão:

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a>Relatório de erros
### <a name="session-errors"></a>Erros de sessão
Erros de sessão são normalmente utilizadas tooreport Olá erros afetar utilizador Olá durante a sua sessão.

**Exemplo:**

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

### <a name="standalone-errors"></a>Erros de autónomo
Erros de contrary toosession, autónomo erros podem ocorrer fora do contexto de Olá de uma sessão.

**Exemplo:**

Olá exemplo seguinte mostra como tooreport erro sempre que a memória de Olá fica baixa no telemóvel Olá durante o processo de aplicação está em execução.

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a>Tarefas de relatório
### <a name="example"></a>Exemplo
Suponha que pretende que a duração de Olá tooreport do processo de início de sessão:

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

### <a name="report-errors-during-a-job"></a>Relatório de erros durante a uma tarefa
Erros podem ser tooa relacionado com a tarefa em vez de ser relacionadas com toohello sessão do utilizador atual.

**Exemplo:**

Suponha que pretende tooreport um erro durante a iniciar sessão no processo:

[...] signIn void público (contexto contexto,...) {

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

### <a name="reporting-events-during-a-job"></a>Eventos de relatório durante uma tarefa
Eventos podem ser tooa relacionado com a tarefa em vez de ser relacionadas com toohello sessão do utilizador atual.

**Exemplo:**

Suponha que temos uma rede social e Utilizamos um tarefa tooreport Olá tempo total durante o qual Olá utilizador é o servidor de toohello ligado. utilizador Olá pode permanecer ligado em segundo plano, mesmo quando ele está a utilizar outra aplicação ou quando está suspenso phone Olá, pelo que não existe nenhuma sessão.

utilizador Olá pode receber mensagens dos seus amigos, este é um evento de tarefa.

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

## <a name="extra-parameters"></a>Parâmetros adicionais
Dados arbitrários podem ser anexado tooevents, erros, atividades e tarefas.

Estes dados podem ser estruturados, utiliza a classe de pacote do Android (na realidade, funciona como parâmetros adicionais no Android pendentes). Tenha em atenção que um grupo pode conter matrizes ou outro instâncias de pacote.

> [!IMPORTANT]
> Se o put nos parâmetros parcelable ou serializáveis, certifique-se os seus `toString()` método é implementado tooreturn uma cadeia legível por humanos. Classes serializáveis que contêm campos não transitórios que não são serializáveis tornará falhas Android quando irá chamar`bundle.putSerializable("key",value);`
> 
> [!WARNING]
> Não são suportadas matrizes dispersas nos parâmetros adicionais, ou seja, não irá ser serializada como uma matriz. Deverá convertê-los em matrizes padrão antes de a utilizar nos parâmetros adicionais.
> 
> 

### <a name="example"></a>Exemplo
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a>Limites
#### <a name="keys"></a>Chaves
Cada chave no Olá `Bundle` tem de corresponder ao hello seguintes expressão regular:

`^[a-zA-Z][a-zA-Z_0-9]*`

Significa que as chaves tem de começar com, pelo menos, uma letra, seguido de letras, dígitos ou carateres de sublinhado (\_).

#### <a name="size"></a>Tamanho
Extras estão limitadas demasiado**1024** carateres por chamada (uma vez codificados em JSON pelo serviço de envolvimento Olá).

Olá anterior exemplo, Olá JSON enviado toohello servidor é 58 carateres de comprimento:

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>Informações de relatórios de aplicações
Pode comunicar manualmente controlo informações (ou quaisquer outras informações específicas da aplicação) utilizando Olá `sendAppInfo()` função.

Tenha em atenção que estas informações podem ser enviadas de forma incremental: apenas Olá valor mais recente para uma determinada chave será mantido para um determinado dispositivo.

Como extras de evento, Olá classe de pacote utilizados tooabstract informações da aplicação, tenha em atenção que as matrizes ou subplano bundles será tratada como cadeias simples (com a serialização do JSON).

### <a name="example"></a>Exemplo
Eis um género de utilizador de toosend de exemplo de código e a data de nascimento:

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a>Limites
#### <a name="keys"></a>Chaves
Cada chave no Olá `Bundle` tem de corresponder ao hello seguintes expressão regular:

`^[a-zA-Z][a-zA-Z_0-9]*`

Significa que as chaves tem de começar com, pelo menos, uma letra, seguido de letras, dígitos ou carateres de sublinhado (\_).

#### <a name="size"></a>Tamanho
As informações da aplicação são limitadas demasiado**1024** carateres por chamada (uma vez codificados em JSON pelo serviço de envolvimento Olá).

Olá anterior exemplo, Olá JSON enviado toohello servidor é 44 carateres de comprimento:

            {"expiration":"2016-12-07","status":"premium"}
