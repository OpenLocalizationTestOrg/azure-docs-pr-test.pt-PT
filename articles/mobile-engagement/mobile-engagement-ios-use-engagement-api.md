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
# <a name="how-toouse-hello-engagement-api-on-ios"></a>Como tooUse Olá o Engagement API no iOS
Este documento é um documento de toohello suplemento como tooIntegrate o Engagement no iOS: fornece na profundidade obter detalhes sobre como toouse Olá Engagement API tooreport as estatísticas da aplicação.

Tenha em atenção que o se pretender que apenas Engagement tooreport da sua aplicação sessões, atividades, as falhas e obter informações técnicas, em seguida, hello mais simples é forma toomake todos os seus custom `UIViewController` objetos herdarem Olá correspondente `EngagementViewController` classe .

Se quiser toodo mais, por exemplo, se precisar de eventos específicos de aplicação tooreport, erros e tarefas, ou se tiver tooreport as atividades da aplicação de forma diferente que Olá um implementado no Olá `EngagementViewController` classes, em seguida, terá de toouse Olá Engagement API.

Olá Engagement API é fornecida pela Olá `EngagementAgent` classe. Uma instância desta classe pode ser obtida ao chamar Olá `[EngagementAgent shared]` método estático (tenha em atenção que Olá `EngagementAgent` objeto devolvido é um singleton).

Antes de quaisquer chamadas à API, hello `EngagementAgent` objeto tem de ser inicializado ao chamar o método de Olá`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`

## <a name="engagement-concepts"></a>Conceitos de envolvimento
Olá seguintes partes refinar Olá comuns [conceitos do Mobile Engagement](mobile-engagement-concepts.md) para a plataforma de iOS Olá.

### <a name="session-and-activity"></a>`Session` e `Activity`
Um *atividade* é normalmente associadas um ecrã da aplicação Olá, que é toosay Olá *atividade* inicia quando o ecrã de Olá é apresentado e para quando o ecrã de Olá está fechado: Este é Olá caso quando Olá Engagement SDK é integrado utilizando Olá `EngagementViewController` classes.

Mas *atividades* também pode ser controlado manualmente utilizando Olá o Engagement API. Isto permite que toosplit um ecrã específico na várias sub partes tooget Olá, obter mais detalhes sobre a utilização deste ecrã (por exemplo tooknown frequência e quanto as caixas de diálogo são utilizadas dentro este ecrã).

## <a name="reporting-activities"></a>Relatório de atividades
### <a name="user-starts-a-new-activity"></a>Utilizador inicia uma nova atividade
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

Terá de toocall `startActivity()` cada atividade de utilizador de Olá de hora é alterado. Olá primeira chamada toothis função inicia uma nova sessão de utilizador.

### <a name="user-ends-his-current-activity"></a>Utilizador termina a atividade atual
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> Deve **nunca** chamar esta função por si, exceto se quiser toosplit uma utilização da sua aplicação para várias sessões: uma chamada de função toothis terminaria Olá imediatamente, a sessão atual deste modo, uma chamada subsequente demasiado`startActivity()`seria iniciar uma sessão de novo. Esta função é chamada automaticamente por Olá SDK quando a aplicação está fechada.
> 
> 

## <a name="reporting-events"></a>Eventos de relatório
### <a name="session-events"></a>Eventos da sessão
Eventos da sessão são ações de Olá tooreport normalmente utilizadas realizadas por um utilizador durante a sua sessão.

**Exemplo sem dados adicionais:**

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

**Exemplo com dados adicionais:**

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

### <a name="standalone-events"></a>Eventos de autónomo
Eventos de contrary toosession, autónomo eventos podem ser utilizados fora do contexto de Olá de uma sessão.

**Exemplo:**

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a>Relatório de erros
### <a name="session-errors"></a>Erros de sessão
Erros de sessão são normalmente utilizadas tooreport Olá erros afetar utilizador Olá durante a sua sessão.

**Exemplo:**

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

### <a name="standalone-errors"></a>Erros de autónomo
Contrary toosession erros, erros autónomo podem ser utilizados fora do contexto de Olá de uma sessão.

**Exemplo:**

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a>Tarefas de relatório
**Exemplo:**

Suponha que pretende que a duração de Olá tooreport do processo de início de sessão:

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

### <a name="report-errors-during-a-job"></a>Relatório de erros durante a uma tarefa
Erros podem ser tooa relacionado com a tarefa em vez de ser relacionadas com toohello sessão do utilizador atual.

**Exemplo:**

Suponha que pretende tooreport um erro durante o processo de início de sessão:

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

### <a name="events-during-a-job"></a>Eventos durante uma tarefa
Eventos podem ser tooa relacionado com a tarefa em vez de ser relacionadas com toohello sessão do utilizador atual.

**Exemplo:**

Suponha que temos uma rede social e Utilizamos um tarefa tooreport Olá tempo total durante o qual Olá utilizador é o servidor de toohello ligado. utilizador Olá pode receber mensagens dos seus amigos, este é um evento de tarefa.

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

## <a name="extra-parameters"></a>Parâmetros adicionais
Dados arbitrários podem ser anexado tooevents, erros, atividades e tarefas.

Estes dados podem ser estruturados, utiliza a classe de NSDictionary do iOS.

Tenha em atenção que podem conter extras `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` ou outros `NSDictionary` instâncias.

> [!NOTE]
> Olá parâmetro adicional é serializado no JSON. Se quiser toopass diferentes objetos que Olá aqueles descrito acima, tem de implementar Olá seguinte método na sua classe:
> 
> -(NSString*) JSONRepresentation;
> 
> método de Olá deve devolver uma representação JSON do seu objeto.
> 
> 

### <a name="example"></a>Exemplo
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a>Limites
#### <a name="keys"></a>Chaves
Cada chave no Olá `NSDictionary` tem de corresponder ao hello seguintes expressão regular:

`^[a-zA-Z][a-zA-Z_0-9]*`

Significa que as chaves tem de começar com, pelo menos, uma letra, seguido de letras, dígitos ou carateres de sublinhado (\_).

#### <a name="size"></a>Tamanho
Extras estão limitadas demasiado**1024** carateres por chamada (uma vez codificados em JSON pelo agente de envolvimento Olá).

Olá anterior exemplo, Olá JSON enviado toohello servidor é 58 carateres de comprimento:

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>Informações de relatórios de aplicações
Pode comunicar manualmente controlo informações (ou quaisquer outras informações específicas da aplicação) utilizando Olá `sendAppInfo:` função.

Tenha em atenção que estas informações podem ser enviadas de forma incremental: apenas Olá valor mais recente para uma determinada chave será mantido para um determinado dispositivo.

Como extras de evento, hello `NSDictionary` classe é utilizada tooabstract informações da aplicação, tenha em atenção que as matrizes ou dicionários secundárias serão tratados como cadeias simples (com a serialização do JSON).

**Exemplo:**

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a>Limites
#### <a name="keys"></a>Chaves
Cada chave no Olá `NSDictionary` tem de corresponder ao hello seguintes expressão regular:

`^[a-zA-Z][a-zA-Z_0-9]*`

Significa que as chaves tem de começar com, pelo menos, uma letra, seguido de letras, dígitos ou carateres de sublinhado (\_).

#### <a name="size"></a>Tamanho
As informações da aplicação são limitadas demasiado**1024** carateres por chamada (uma vez codificados em JSON pelo agente de envolvimento Olá).

Olá anterior exemplo, Olá JSON enviado toohello servidor é 44 carateres de comprimento:

    {"birthdate":"1983-12-07","gender":"female"}
