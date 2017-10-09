---
title: conceitos do Engagement aaaMobile | Microsoft Docs
description: Conceitos do Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8d19abd1-0a6c-4772-9fa5-5e99980ac5da
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 5aa7f28c00cd641a36a6e040c6b13d802ea6ae41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-concepts"></a>Conceitos do Azure Mobile Engagement
O Mobile Engagement define alguns plataformas tooall suportado comuns conceitos. Este artigo descreve brevemente esses conceitos.

Este artigo é um bom ponto de partida se for novo tooMobile Engagement. Também Certifique-se de que tooread Olá documentação toohello específico plataforma que estiver a utilizar, conforme que tal irá refinar os conceitos de Olá descritos neste artigo com mais detalhes e exemplos, bem como limitações possíveis.

## <a name="devices-and-users"></a>Dispositivos e utilizadores
O Mobile Engagement identifica os utilizadores através da geração de um identificador exclusivo para cada dispositivo. Este identificador é designado identificador do dispositivo hello (ou `deviceid`). Este é gerado de tal forma que todas as aplicações em execução Olá mesmo partilha dispositivo Olá o mesmo identificador de dispositivo.

Implicitamente, tal significa que o Mobile Engagement considera que um dispositivo toobelong tooexactly um utilizador e, portanto, os utilizadores e dispositivos são conceitos equivalentes.

## <a name="sessions-and-activities"></a>Sessões e atividades
Uma sessão é uma utilização da aplicação Olá realizada por um utilizador, de utilizador do Olá tempo Olá começa a utilizá-la, até Olá termina.

Uma atividade corresponde a uma utilização de uma determinada parte secundária da aplicação Olá realizada por um utilizador (é normalmente um ecrã, mas pode ser qualquer caráter adequado toohello aplicação).

Um utilizador pode realizar apenas uma atividade de cada vez.

Uma atividade é identificada por um nome (limitado too64 carateres) e, opcionalmente, pode incorporar alguns dados adicionais (no limite de Olá de 1024 bytes).

As sessões são automaticamente calculadas a partir da sequência de Olá das atividades realizadas pelos utilizadores. Uma sessão é iniciada quando o utilizador Olá começa a primeira atividade e termina quando este conclui a última atividade. Isto significa que uma sessão não precisa de toobe explicitamente iniciada ou interrompida. Em vez disso, as atividades são explicitamente iniciadas ou interrompidas. Se nenhuma atividade for comunicada, nenhuma sessão será comunicada.

## <a name="events"></a>Eventos
Os eventos são utilizados tooreport ações instantâneas (como botão premido ou artigos lidos por utilizadores).

Um evento pode ser relacionado toohello sessão atual, tooa executar tarefa, ou pode ser um evento autónomo.

Um evento é identificado por um nome (limitado too64 carateres) e, opcionalmente, pode incorporar alguns dados adicionais (no limite de Olá de 1024 bytes).

## <a name="error"></a>Erro
Erros são problemas de tooreport utilizado corretamente detetados pela aplicação Olá (por exemplo, ações incorretas do utilizador, ou falhas de chamada de API).

Um erro pode ser relacionado toohello sessão atual, tooa executar tarefa, ou pode ser um erro autónomo.

Um erro é identificado por um nome (limitado too64 carateres) e, opcionalmente, pode incorporar alguns dados adicionais (no limite de Olá de 1024 bytes).

## <a name="job"></a>Tarefa
As tarefas são utilizadas tooreport ações com uma duração (como a duração de chamadas à API, mostra a hora dos anúncios, duração das tarefas em segundo plano ou duração das ações do utilizador).

Uma tarefa não é tooa relacionados sessão, porque pode ser executada uma tarefa em segundo plano, Olá, sem qualquer interação do utilizador.

Uma tarefa é identificada por um nome (limitado too64 carateres) e, opcionalmente, pode incorporar alguns dados adicionais (no limite de Olá de 1024 bytes).

## <a name="crash"></a>Falha de sistema
As falhas são emitidas automaticamente pelo Olá aplicação do Mobile Engagement SDK tooreport falhas onde problemas não detetados pela aplicação Olá torná-lo de falhas.

## <a name="application-information"></a>Informações da aplicação
As informações da aplicação (ou as informações da aplicação) é utilizado tootag utilizadores, ou seja, tooassociate alguns utilizadores toohello de dados de uma aplicação (isto é semelhante tooweb cookies, exceto que as informações de aplicação são armazenadas no lado do servidor de Olá na plataforma do Azure Mobile Engagement Olá).

As informações da aplicação podem ser registadas utilizando Olá API do SDK do Mobile Engagement ou utilizando a plataforma de Mobile Engagement Olá API do dispositivo.

As informações da aplicação são um dispositivo de tooa associados do par chave/valor. chave de Olá é o nome de Olá Olá informações da aplicação (limitado too64 letras ASCII [a-zA-Z], números [0-9] e carateres de sublinhado [_]). o valor de Olá (too1024 limitado carateres) pode ser qualquer cadeia, número inteiro, data (AAAA-MM-dd) ou booleano (VERDADEIRO ou FALSO).

Qualquer número de informações da aplicação pode ser associados tooa dispositivo, dentro dos limites de Olá definidos pelos termos dos preços do Mobile Engagement Olá. Numa determinada chave, o Mobile Engagement apenas mantém um registo dos Olá conjunto de valores mais recente (nenhum histórico). Definir ou alterar o valor de Olá das informações da aplicação força o Mobile Engagement toore-avaliar os critérios de audiência definidos nesta aplicação as informações (se aplicável), o que significa que as informações da aplicação podem ser utilizados tootrigger pushes de em tempo real.

## <a name="extra-data"></a>Dados adicionais
Dados adicionais (ou extras) são alguns dados arbitrários que podem ser anexados tooevents, erros, atividades e tarefas.

Extras estão estruturados do mesmo modo tooJSON objetos: são compostos uma árvore de pares chave/valor. As chaves estão limitadas too64 letras de ASCII [a-zA-Z], números [0-9] e carateres de sublinhado [_]) e Olá o tamanho total dos extras é carateres too1024 limitado (uma vez codificados em JSON pelo Olá SDK do Mobile Engagement).

árvore completa de Olá de pares chave/valor é armazenado como um objeto JSON. Contudo, só Olá primeiro nível das chaves/valores é decomposed toobe diretamente acessível toosome avançadas funções como segmentos (por exemplo, pode facilmente definir um segmento denominado "SciFi ventoinhas", que é feito de todos os utilizadores ter enviado a eventos de Olá, pelo menos, 10 vezes com o nome "content_viewed" com extra chave Olá "tipo_conteúdo" definido toohello valor "scifi" no Olá último mês). Recomenda-se, por conseguinte, altamente Step-by-toosend apenas extras constituídos por listas simples de pares chave/valor utilizando valores escalares (por exemplo, cadeias, datas, números inteiros ou booleano).

## <a name="next-steps"></a>Passos seguintes
* [Descrição geral do SDK do Universal do Windows para o Azure Mobile Engagement](mobile-engagement-windows-store-sdk-overview.md)
* [Descrição geral do SDK do Windows Phone Silverlight para o Azure Mobile Engagement](mobile-engagement-windows-phone-sdk-overview.md)
* [SDK do iOS do Azure Mobile Engagement](mobile-engagement-ios-sdk-overview.md)
* [SDK do Android do Azure Mobile Engagement](mobile-engagement-android-sdk-overview.md)

