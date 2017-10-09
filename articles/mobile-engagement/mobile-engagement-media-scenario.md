---
title: "implementação do Mobile Engagement aaaAzure para a aplicação do suporte de dados"
description: "Tooimplement de cenário de aplicação do suporte de dados do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48201cc8-4e04-485c-a8dc-d6406d23f3ed
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 6a495eb790993a30d5c03802aa9e6404fea983d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-media-app"></a>Implementar o Engagement móvel com suporte de dados de aplicação
## <a name="overview"></a>Descrição geral
O João é um Gestor de projeto móveis para uma empresa de grande de suporte de dados. Ele executada recentemente uma nova aplicação que tem uma contagem de transferência muito elevada. Ele atingiu os objetivos para transferência no entanto, ainda a devolver em Investment(ROI) por utilizador não cumpre os requisitos. 

O João já identificou a razão pela qual o ROI está demasiado baixo. Os utilizadores deixar de utilizar a aplicação após apenas 2 semanas com frequência e a maior parte dos mesmos nunca voltar atrás. John retenção de Olá tooincrease da sua aplicação.

Após alguns testes iniciais, ele tem aprendidas quando ele envolva os seus utilizadores com notificações push, estes tendem toocontinue utilizando a aplicação. Também os utilizadores que foram inativos, muitas vezes, irão devolver toohello aplicação consoante as notificações, envia-os. O João decide tooinvest em algum tipo de programa de envolvimento para a aplicação que utiliza a filtragem avançados com notificações push.

O João tem recentemente leitura Olá [Azure Mobile Engagement – guia de introdução com melhores práticas](mobile-engagement-getting-started-best-practices.md) e decidiu recomendações de Olá tooimplement do guia de Olá.

## <a name="objectives-and-kpis"></a>Objetivos e KPIs
Principais intervenientes para a aplicação de João cumpram. Empresas é gerada a partir de anúncios como utilizadores consumam o suporte de dados. Aumento conteúdo consumido por utilizador, o João aumenta as receitas. Todos os concordarem num objetivo principal: tooincrease vendas de anúncios em 25%. Criarem toomeasure indicadores do negócio chave de desempenho (KPIs) e unidade neste objetivo

* Número de anúncios clicado por utilizador
* Quantas páginas de artigo visitada (por utilizador / por sessão / por semana / por mês...)
* Quais são as categorias favoritas

Com base na reunião de João com principais intervenientes ele definiu os KPIs de empresas. Ele segue parte 1 de Olá [Azure Mobile Engagement – guia de introdução com melhores práticas](mobile-engagement-getting-started-best-practices.md). 

Em seguida, ele cria Olá tooensure KPIs de envolvimento que objetivos são atingidos os seguintes:

* Monitorizar a retenção em Olá intervalos os seguintes: diárias, semanais, bissemanais e mensais.
* Contagens de utilizadores ativos
* classificação da aplicação Olá na aplicação Olá armazena

Com base na recomendações da equipa de TI de Olá, Olá KPIs técnicos a seguir foram adicionado Olá tooanswer seguintes perguntas:

* O que é o meu caminho de utilizador (visitada, a página de que quantidade de tempo de que os utilizadores passam no mesmo)
* Número de falhas ou erros que encontrou por sessão?
* Quais as versões de SO executam os meus utilizadores?
* O que é o tamanho médio de Olá do ecrã para os meus utilizadores?
* Que tipo de ligações à internet dispõe os meus utilizadores?

Para cada KPI, ele classifica os dados de Olá necessários e ele regista-lo numa localização correta do Olá do seu manual de comunicação social.

## <a name="engagement-program-and-integration"></a>Programa de envolvimento e a integração
Agora que o João concluiu a definir os KPIs, ele começa a fase de estratégia de envolvimento por definir os seus objetivos e 4 programas de envolvimento:![][1]

Em seguida, João fica mais profundo por com detalhes sobre as notificações push para cada programa. Notificação push são definidos por cinco elementos:

1. Objetivo: o que é o objetivo de notificação de Olá Olá
2. Como irá ser atingido o objetivo de Olá
3. Destino: que receberão uma notificação de Olá?
4. Conteúdo: Qual é a utilização de expressões Olá e formato Olá de notificação de Olá (no App/Out de aplicação)
5. Quando: o que é Olá melhor momento toosend esta notificação push
   
    ![][2]

Para obter mais informações consulte toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks).

Toocollect e escreve a plano de etiquetas jointly com a solução de Olá IT equipa tooimplement de acordo com toohello parte 2 Olá documento técnico que o João utiliza toodefine da secção de destino que ele tem de dados. Depois de 1 semana de implementação e testes de aceitação de utilizadores, João por fim, pode iniciar os programas.

## <a name="program-results"></a>Resultados de programa
4 meses mais tarde, o João consulta os desempenhos de programas. Olá programa de boas-vindas e Olá semanal programa estão a cumprir os objetivos. diminui o número de Olá de utilizador com sessão apenas uma, estão a ser utilizadas mais funcionalidades da aplicação Olá e número de Olá de ligações por semana tem duplicada.

Olá **programa inativa** está a ajudar João compreender tendencies de utilizador. Parece que 15% de utilizadores Inativos Olá voltar toohello aplicação. No entanto a maior parte dos mesmos não permanecem ativos mais de 1 mês. O João foresees uma potencial otimização desta sequência com notificações adicionais e expandir as opções de conteúdo.

Olá **detetar programa** não funciona corretamente. Aumenta cruzada vender mas insuficiente tooreach os seus objetivos. O João identifica que ele não tem suficiente dados toomake relevantes filtragem e de propor conteúdo apropriado. Ele para este programa e centra-se no envio de "notificações editorial push" com o Azure Mobile Engagement. As journalists já tem um notificações de push CMS solução toosend e que não pretendem toochange.

O João decide toouse Olá API de alcance que é uma API de REST de HTTP que permite a gestão de campanhas de alcance sem que tenha toouse AZME Web interface. Com esta abordagem João pode recolher dados de Olá ele precisa e permitir que os escritores tookeep utilizando Olá CMS solução.

tooensure funcionalidade funciona corretamente, o João pede-lhe IT equipa toobe vigilant no Olá seguintes pontos:

1. **Sistemas operativos** : todos os têm as suas próprias regras tooadministrate as notificações push, para que o João decide toolist todos os casos e verifica se Olá APIs processá-lo.
   Por exemplo: O sistema de Android push permite visão geral que não é o caso de Olá com iOS.
2. **Período de tempo**: João pretende uma API, o que definir período de tempo de Olá e um toocampaigns de fim. John toopreserve utilizadores de qualquer notificação acontece bombing.
3. **Categorias**: equipa de Marketing prepara o modelo para cada tipo de alerta. O João pergunta categorias de tooset equipa IT dentro Olá API.

Após alguns testes João é satisfeito. Obrigado toothis API, journalists podem ainda enviar notificações push com os respetivos CMS e do Azure Mobile Engagement recolhe todos os dados comportamentais para os mesmos

Depois destes 4 primeiro meses, resultados refletem uma confiança de desempenho e fornecem geral boa para João e a placa, ROI por utilizador aumenta por 15% e vendas móveis representam 17.5% do totais vendas, um aumento de 7.5% em apenas quatro meses.

<!--Image references-->
[1]: ./media/mobile-engagement-media-scenario/engagement-strategy.png
[2]: ./media/mobile-engagement-media-scenario/push-scenarios.png

<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
