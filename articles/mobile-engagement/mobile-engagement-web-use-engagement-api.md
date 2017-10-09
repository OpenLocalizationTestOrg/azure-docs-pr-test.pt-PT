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
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a>Utilizar Olá API do Azure Mobile Engagement numa aplicação web
Este documento é um documento de toohello adição que indica como demasiado[integrar o Mobile Engagement numa aplicação web](mobile-engagement-web-integrate-engagement.md). Fornece detalhes aprofundados sobre como toouse Olá API do Azure Mobile Engagement tooreport as estatísticas da aplicação.

Olá API do Mobile Engagement é fornecida pela Olá `engagement.agent` objeto. Olá predefinição SDK Web do Azure Mobile Engagement alias `engagement`. Pode redefinir este alias de configuração do SDK Olá.

## <a name="mobile-engagement-concepts"></a>Conceitos do Mobile Engagement
Olá seguintes partes refinar comuns [conceitos do Mobile Engagement](mobile-engagement-concepts.md) de plataforma web de Olá.

### <a name="session-and-activity"></a>`Session` e `Activity`
Se o utilizador Olá permanece inativo durante mais do que alguns segundos, entre duas atividades, hello sequência do utilizador de atividades está dividida em duas sessões distintas. Estes alguns segundos são denominados Olá tempo limite da sessão.

Se a aplicação web não declara final Olá das atividades de utilizador por si só (por chamada Olá `engagement.agent.endActivity` função), servidor de Mobile Engagement Olá expira automaticamente Olá sessão de utilizador em três minutos depois de fechar a página de aplicação Olá. Isto denomina-tempo limite de sessão do servidor Olá.

### `Crash`
Relatórios automatizados de exceções de JavaScript não identificadas não estão criados por predefinição. No entanto, pode reportar falhas manualmente utilizando Olá `sendCrash` funcionar (consulte a secção de Olá no relatório de falhas).

## <a name="reporting-activities"></a>Relatório de atividades
Atividade do utilizador de relatórios incluem quando um utilizador inicia uma nova atividade e, quando o utilizador Olá termina a atividade atual Olá.

### <a name="user-starts-a-new-activity"></a>Utilizador inicia uma nova atividade
    engagement.agent.startActivity("MyUserActivity");

Terá de toocall `startActivity()` cada atividade de utilizador de hora é alterado. Olá primeira chamada toothis função inicia uma nova sessão de utilizador.

### <a name="user-ends-hello-current-activity"></a>Utilizador termina a atividade atual Olá
    engagement.agent.endActivity();

Terá de toocall `endActivity()` , pelo menos, uma vez quando o utilizador de Olá for concluída, a última atividade dos mesmos. Informa Olá Web SDK do Mobile Engagement que utilizador Olá está atualmente inativa, e que a sessão de utilizador Olá tem toobe fechada depois do tempo limite da sessão Olá expira. Se chamar `startActivity()` antes do tempo limite da sessão Olá expira, a sessão de Olá simplesmente é retomada.

Porque não existe nenhuma chamada fiável para quando a janela do navegador de Olá está fechada, é frequentemente fim de Olá toocatch difícil ou impossível das atividades de utilizador dentro de um ambiente de web. Por que motivo que é Olá Mobile Engagement server expira automaticamente sessão de utilizador de Olá dentro de três minutos após a página de aplicação Olá está fechada.

## <a name="reporting-events"></a>Eventos de relatório
Eventos de relatório abrange eventos da sessão e eventos de autónomo.

### <a name="session-events"></a>Eventos da sessão
Eventos da sessão são normalmente ações de Olá de tooreport utilizados realizadas por um utilizador durante a sessão do utilizador Olá.

**Exemplo sem dados adicionais:**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

**Exemplo com dados adicionais:**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a>Eventos de autónomo
Ao contrário de eventos da sessão, podem ocorrer eventos de autónomo fora Olá contexto de uma sessão.

Para tal, utilize ``engagement.agent.sendEvent`` em vez de ``engagement.agent.sendSessionEvent``.

## <a name="reporting-errors"></a>Relatório de erros
Relatório de erros abrange erros de sessão e erros de autónomo.

### <a name="session-errors"></a>Erros de sessão
Erros de sessão são, normalmente, erros de Olá tooreport utilizados que tem um impacto no utilizador Olá durante Olá da sessão de utilizador.

**Exemplo sem dados adicionais:**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

**Exemplo com dados adicionais:**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a>Erros de autónomo
Ao contrário dos erros de sessão, podem ocorrer erros de autónomo fora Olá contexto de uma sessão.

Para tal, utilize `engagement.agent.sendError` em vez de `engagement.agent.sendSessionError`.

## <a name="reporting-jobs"></a>Tarefas de relatório
Elaboração de relatórios em tarefas bastidores erros e eventos que ocorrem durante uma tarefa de relatórios e relatórios de falhas.

**Exemplo:**

Se quiser toomonitor um pedido de AJAX, utilizaria seguinte Olá:

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

### <a name="reporting-errors-during-a-job"></a>Relatório de erros durante a uma tarefa
Erros podem ser tooa relacionado com a tarefa em vez de toohello sessão do utilizador atual.

**Exemplo:**

Se quiser tooreport um erro se um pedido de AJAX falha:

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

### <a name="reporting-events-during-a-job"></a>Eventos de relatório durante uma tarefa
Os eventos podem estar relacionado tooa executar tarefa em vez de sessão do utilizador atual toohello, thanks toohello `engagement.agent.sendJobEvent` função.

Esta função funciona exatamente como `engagement.agent.sendJobError`.

### <a name="reporting-crashes"></a>Relatório de falhas
Olá utilize `sendCrash` função tooreport falhas manualmente.

Olá `crashid` argumento é uma cadeia que identifica o tipo de Olá da falha.
Olá `crash` argumento é, normalmente, o rastreio da pilha Olá de falhas de Olá como uma cadeia.

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a>Parâmetros adicionais
Pode anexar dados arbitrários tooan evento, erro, atividade ou tarefa.

dados de Olá podem ser qualquer objeto JSON (mas não uma matriz nem um tipo primitivo).

**Exemplo:**

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a>Limites
Os limites que se aplicam tooextra parâmetros são nas áreas de Olá de expressões regulares para chaves, tipos de valor e tamanho.

#### <a name="keys"></a>Chaves
Cada chave no objeto de Olá tem de corresponder ao hello seguintes expressão regular:

    ^[a-zA-Z][a-zA-Z_0-9]*

Isto significa que as chaves tem de começar com, pelo menos, uma letra, seguido de letras, dígitos ou carateres de sublinhado (\_).

#### <a name="values"></a>Valores
Os valores são toostring limitada, o número e tipos booleanos.

#### <a name="size"></a>Tamanho
Extras estão limitadas too1, 024 carateres por chamada (após Olá Web SDK do Mobile Engagement codifica no JSON).

## <a name="reporting-application-information"></a>Informações de relatórios de aplicações
Manualmente pode comunicar informações (ou outras informações específicas da aplicação) de controlo utilizando Olá `sendAppInfo()` função.

Tenha em atenção que estas informações podem ser enviadas de forma incremental. Apenas Olá valor mais recente para uma chave específica será mantido para um dispositivo específico.

Como extras de eventos, pode utilizar qualquer JSON tooabstract aplicação as informações do objeto. Tenha em atenção que as matrizes ou objetos secundárias são tratados como cadeias simples (com a serialização do JSON).

**Exemplo:**

Eis um exemplo de código para sexo do utilizador Olá envio e a data de nascimento:

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a>Limites
Os limites que se aplicam tooapplication informações são nas áreas de Olá de expressões regulares para chaves e tamanho.

#### <a name="keys"></a>Chaves
Cada chave no objeto de Olá tem de corresponder ao hello seguintes expressão regular:

    ^[a-zA-Z][a-zA-Z_0-9]*

Isto significa que as chaves tem de começar com, pelo menos, uma letra, seguido de letras, dígitos ou carateres de sublinhado (\_).

#### <a name="size"></a>Tamanho
Informações sobre a aplicação é limitado too1, 024 carateres por chamada (após Olá Web SDK do Mobile Engagement codifica no JSON).

Olá anterior exemplo, hello JSON enviadas toohello servidor é 44 carateres de comprimento:

    {"birthdate":"1983-12-07","gender":"female"}
