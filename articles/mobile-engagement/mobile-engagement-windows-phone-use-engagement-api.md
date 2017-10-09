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
# <a name="how-toouse-hello-engagement-api-on-windows-phone-silverlight"></a>Como tooUse Olá o Engagement API no Windows Phone Silverlight
Este documento é um documento de toohello suplemento [como toointegrate Mobile Engagement na sua aplicação do Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md). Fornece na profundidade obter detalhes sobre como toouse Olá Engagement API tooreport as estatísticas da aplicação.

Se pretender apenas Engagement tooreport da sua aplicação sessões, atividades, as falhas e obter informações técnicas, em seguida, Olá mais simples é forma toomake todos os seus `PhoneApplicationPage` classes secundárias herdarem Olá `EngagementPage` classe.

Se quiser toodo mais, por exemplo, se precisar de eventos específicos de aplicação tooreport, erros e tarefas, ou se tiver tooreport as atividades da aplicação de forma diferente que Olá um implementado no Olá `EngagementPage` classes, em seguida, terá de toouse Olá Engagement API.

Olá Engagement API é fornecida pela Olá `EngagementAgent` classe. Pode aceder aos métodos toothose através de `EngagementAgent.Instance`.

Mesmo que o módulo de Olá de agente não foi inicializado, cada API de toohello chamada é deferida e será executada novamente quando o agente de Olá está disponível.

## <a name="engagement-concepts"></a>Conceitos de envolvimento
Olá seguintes partes refinar Olá conceitos do Mobile Engagement para a plataforma do Windows Phone Olá.

### <a name="session-and-activity"></a>`Session` e `Activity`
Um *atividade* é normalmente associadas uma página da aplicação Olá, que é toosay Olá *atividade* inicia quando página Olá é apresentada e para quando a página Olá está fechada: Este é o caso de Olá quando hello O engagement SDK está integrado utilizando Olá `EngagementPage` classe.

Mas *atividades* também pode ser controlado manualmente utilizando Olá o Engagement API. Isto permite que toosplit uma determinada página na várias sub partes tooget Olá, obter mais detalhes sobre a utilização desta página (por exemplo tooknown frequência e quanto as caixas de diálogo são utilizadas dentro desta página).

## <a name="reporting-activities"></a>Relatório de atividades
### <a name="user-starts-a-new-activity"></a>Utilizador inicia uma nova atividade
#### <a name="reference"></a>Referência
            void StartActivity(string name, Dictionary<object, object> extras = null)

Terá de toocall `StartActivity()` cada atividade de utilizador de Olá de hora é alterado. Olá primeira chamada toothis função inicia uma nova sessão de utilizador.

> [!IMPORTANT]
> Olá SDK automaticamente chamar o método de EndActivity de Olá, quando a aplicação Olá está fechada. Assim, recomenda-se vivamente método do toocall Olá StartActivity sempre que terminou a atividade de Olá de alteração de utilizador Olá e chamada de tooNEVER Olá método EndActivity, desde a chamar este método força Olá toobe de sessão atual.
> 
> 

#### <a name="example"></a>Exemplo
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a>Utilizador termina a atividade atual
#### <a name="reference"></a>Referência
            void EndActivity()

Terá de toocall `EndActivity()` , pelo menos, uma vez quando o utilizador Olá conclui a última atividade. Informa Olá irá expirar o Engagement SDK que utilizador Olá está atualmente inativa, e uma vez que a sessão de utilizador Olá tem toobe fechado Olá tempo limite da sessão (se chamar `StartActivity()` antes do tempo limite da sessão Olá expira, a sessão Olá simplesmente é continuado).

#### <a name="example"></a>Exemplo
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a>Tarefas de relatório
### <a name="start-a-job"></a>Iniciar uma tarefa
#### <a name="reference"></a>Referência
            void StartJob(string name, Dictionary<object, object> extras = null)

Pode utilizar tarefas certains tootrack de Olá durante um período de tempo.

#### <a name="example"></a>Exemplo
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a>Terminar uma tarefa
#### <a name="reference"></a>Referência
            void EndJob(string name)

Assim que uma tarefa controlada por uma tarefa foi terminada, deverá chamar o método de EndJob de Olá para esta tarefa, fornecendo o nome da tarefa Olá.

#### <a name="example"></a>Exemplo
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a>Eventos de relatório
Há três tipos de eventos:

* Eventos de autónomo
* Eventos da sessão
* Eventos de tarefas

### <a name="standalone-events"></a>Eventos de autónomo
#### <a name="reference"></a>Referência
            void SendEvent(string name, Dictionary<object, object> extras = null)

Podem ocorrer eventos de autónomo fora do contexto de Olá de uma sessão.

#### <a name="example"></a>Exemplo
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a>Eventos da sessão
#### <a name="reference"></a>Referência
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

Eventos da sessão são ações de Olá tooreport normalmente utilizadas realizadas por um utilizador durante a sua sessão.

#### <a name="example"></a>Exemplo
**Sem dados:**

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

**Com os dados:**

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a>Eventos de tarefas
#### <a name="reference"></a>Referência
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

Eventos de tarefas são ações de Olá de tooreport normalmente utilizadas realizadas por um utilizador durante uma tarefa.

#### <a name="example"></a>Exemplo
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a>Relatório de erros
Há três tipos de erros:

* Erros de autónomo
* Erros de sessão
* Erros de tarefas

### <a name="standalone-errors"></a>Erros de autónomo
#### <a name="reference"></a>Referência
            void SendError(string name, Dictionary<object, object> extras = null)

Erros de contrary toosession, autónomo erros podem ocorrer fora do contexto de Olá de uma sessão.

#### <a name="example"></a>Exemplo
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a>Erros de sessão
#### <a name="reference"></a>Referência
            void SendSessionError(string name, Dictionary<object, object> extras = null)

Erros de sessão são normalmente utilizadas tooreport Olá erros afetar utilizador Olá durante a sua sessão.

#### <a name="example"></a>Exemplo
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a>Erros de tarefas
#### <a name="reference"></a>Referência
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

Erros podem ser tooa relacionado com a tarefa em vez de ser relacionadas com toohello sessão do utilizador atual.

#### <a name="example"></a>Exemplo
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a>Relatório de falhas
agente de Olá fornece dois métodos toodeal com falhas.

### <a name="send-an-exception"></a>Enviar uma exceção
#### <a name="reference"></a>Referência
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a>Exemplo
Pode enviar uma exceção em qualquer altura ao chamar:

            EngagementAgent.Instance.SendCrash(aCatchedException);

Também pode utilizar uma sessão de envolvimento do parâmetro opcional tooterminate Olá em Olá mesmo tempo que o envio de falhas de Olá. por isso, chamar toodo:

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

Se, fazê-lo, sessão Olá e as tarefas serão fechadas depois de falhas de Olá a enviar.

### <a name="send-an-unhandled-exception"></a>Enviar uma exceção não processada
#### <a name="reference"></a>Referência
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

Também o engagement fornece um exceções toosend não processada do método. Isto é especialmente útil quando utilizada dentro de processador de eventos do Olá silverlight UnhandledException.

Este método irá **sempre** terminar sessão de envolvimento Olá e tarefas depois de a ser chamado.

#### <a name="example"></a>Exemplo
Pode utilizá-la tooimplement o seus próprios processador UnhandledException (especialmente se tiver desativado a funcionalidade do Engagement de relatórios de falhas automática Olá). Por exemplo, no Olá `Application_UnhandledException` método de Olá `App.xaml.cs` ficheiro:

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a>OnActivated
### <a name="reference"></a>Referência
            void OnActivated(ActivatedEventArgs e)

Quando o utilizador Olá navega reencaminhar, na direção oposta a uma aplicação, depois do evento de desativado de Olá é gerado, o sistema de operativo Olá tentará aplicação de Olá tooput num Estado dormant. Em seguida, da aplicação Olá é Tombstoning. Este processo é terminada uma aplicação, mas alguns dados sobre o estado de Olá da aplicação Olá e páginas individuais de Olá na aplicação Olá são preservados.

Tiver tooinsert `EngagementAgent.Instance.OnActivated(e)` no Olá `Application_Activated` método Olá do Olá App.xaml.cs ficheiro tooreset Engagement agente quando aplicação Olá foi Tombstoned.

### <a name="example"></a>Exemplo
            // Inside your App.xaml.cs file

            // Code tooexecute when hello application is activated (brought tooforeground)
            // This code will not execute when hello application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a>Id de dispositivo
            String GetDeviceId()

Pode obter o id de dispositivo do engagement Olá ao chamar este método.

## <a name="extras-parameters"></a>Parâmetros de Extras
Dados arbitrários podem ser anexado tooan evento, um erro, uma atividade ou uma tarefa. Estes dados podem ser estruturados utilizando um dicionário. As chaves e valores podem ser de qualquer tipo.

Dados extras são serializados se quiser tooinsert seu próprio tipo na extras terá tooadd um contrato de dados para este tipo.

### <a name="example"></a>Exemplo
Iremos criar uma nova classe "Pessoa".

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

Em seguida, iremos adicionar um `Person` tooan instância adicional.

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> Se o put outros tipos de objetos, certifique-se o método ToString () tooreturn implementada uma cadeia legível humana.
> 
> 

### <a name="limits"></a>Limites
#### <a name="keys"></a>Chaves
Cada chave no objeto de Olá tem de corresponder ao hello seguintes expressão regular:

`^[a-zA-Z][a-zA-Z_0-9]*$`

Significa que as chaves tem de começar com, pelo menos, uma letra, seguido de letras, dígitos ou carateres de sublinhado (\_).

#### <a name="size"></a>Tamanho
Extras estão limitadas demasiado**1024** carateres por chamada.

## <a name="reporting-application-information"></a>Informações de relatórios de aplicações
### <a name="reference"></a>Referência
            void SendAppInfo(Dictionary<object, object> appInfos)

Manualmente pode comunicar informações (ou quaisquer outras informações específicas da aplicação) utilizando Olá SendAppInfo() função de controlo.

Tenha em atenção que estas informações podem ser enviadas de forma incremental: apenas Olá valor mais recente para uma determinada chave será mantido para um determinado dispositivo. Como extras de evento, utilizar um dicionário\<objeto, objeto\> tooattach informations.

### <a name="example"></a>Exemplo
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a>Limites
#### <a name="keys"></a>Chaves
Cada chave no objeto de Olá tem de corresponder ao hello seguintes expressão regular:

`^[a-zA-Z][a-zA-Z_0-9]*$`

Significa que as chaves tem de começar com, pelo menos, uma letra, seguido de letras, dígitos ou carateres de sublinhado (\_).

#### <a name="size"></a>Tamanho
As informações da aplicação são limitadas demasiado**1024** carateres por chamada.

Olá anterior exemplo, Olá JSON enviado toohello servidor é 44 carateres de comprimento:

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a>Registo
### <a name="enable-logging"></a>Ativar o registo
Olá SDK pode ser configurado tooproduce registos de teste na consola do Olá IDE.
Estes registos não estão ativados por predefinição. toocustomize propriedade de Olá, atualização `EngagementAgent.Instance.TestLogEnabled` tooone do valor de Olá disponível a partir do Olá `EngagementTestLogLevel` enumeração, por exemplo:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
