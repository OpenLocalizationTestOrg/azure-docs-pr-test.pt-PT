---
title: "implementação do Mobile Engagement aaaAzure para a aplicação de jogos"
description: "Tooimplement de cenário de aplicação de jogos do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a>Implementar o Mobile Engagement com a aplicação de jogos
## <a name="overview"></a>Descrição geral
Um arranque de jogos tem de iniciar uma aplicação de jogos de role-play/estratégia de fishing com base. jogos de Olá foi configurado e em execução durante 6 meses. Este jogo enorme concluído com êxito e tem milhões de transferências e se o período de retenção do Olá é tooother muito elevada em comparação com arranque jogos aplicações. A reunião de revisão trimestral Olá, intervenientes concordarem que precisam tooincrease média de receitas por utilizador (ARPU). Pacotes de no jogo Premium estão disponíveis como ofertas especiais. Estes pacotes de jogos permitem aspecto de Olá tooupgrade de utilizadores e o desempenho da respetiva linhas fishing e lures ou tackles no jogo Olá. No entanto, as vendas do pacote são muito baixos. Para decidirem experiência de cliente de Olá tooanalyze primeiro com uma ferramenta de análise e, em seguida, toodevelop utilizando um envolvimento programa tooincrease vendas avançadas segmentação.

Com base no Olá [Azure Mobile Engagement – guia de introdução com melhores práticas](mobile-engagement-getting-started-best-practices.md) criem uma estratégia de envolvimento.

## <a name="objectives-and-kpis"></a>Objetivos e KPIs
Principais intervenientes para jogo Olá cumpram. Todos os concorda com um objetivo de principal - vendas de pacote premium tooincrease por 15%. Criarem toomeasure indicadores do negócio chave de desempenho (KPIs) e unidade neste objetivo

* O nível do jogo Olá estes pacotes adquiridos?
* O que é receitas Olá por utilizador, por sessão, por semana e por mês?
* Quais são os tipos de compra favorito Olá?

Parte 1 de Olá [guia de introdução](mobile-engagement-getting-started-best-practices.md) explica como toodefine Olá objetivos e KPIs. 

Com Olá que KPIs de empresas agora definidas, Olá Mobile produto Manager cria e retenção de tendências de utilizador novo toodetermine KPIs de envolvimento.

* Monitorizar a retenção e utilize em Olá intervalos os seguintes: diariamente, a cada 2 dias, semanalmente, mensalmente e todos os 3 meses
* Contagens de utilizadores do Active Directory
* classificação da aplicação Olá no Olá armazenar

Com base na recomendações da equipa de TI de Olá, Olá KPIs técnicos a seguir foram adicionado Olá tooanswer seguintes perguntas:

* O que é o meu caminho de utilizador (visitada, a qual página quanto tempo que o utilizador dedica nela)
* Número de falhas ou erros que encontrou por sessão
* Quais as versões de SO executam os meus utilizadores?
* O que é o tamanho médio de Olá do ecrã para os meus utilizadores?
* Que tipo de ligação à internet dispõe os meus utilizadores?

Para cada KPI Olá Mobile produto Manager Especifica dados Olá que precisa e onde está localizado no respetivo manual de comunicação social.

## <a name="engagement-program-and-integration"></a>Programa de envolvimento e a integração
Antes de criar um programa de envolvimento avançadas, Olá Director do projeto de Mobile responsável pela projeto Olá deve ter uma compreensão profunda sobre como e quando os produtos são consumidos pelos utilizadores de Olá.

Depois de 3 meses, Olá Director do projeto de Mobile recolheu suficiente tooenhance dados STA vendas de notificação push na aplicação. Ele aprende que:

* Compra primeiro Olá geralmente ocorre ao nível de Olá 14. Para 90% nesses casos, compra de Olá destina-se a nova weapons legendary $3.
* No 80% nesses casos, os utilizadores que efetuou uma compra, continuar com o produto Olá e tornar mais adquire.
* Os utilizadores que passaram a nível de Olá 20, iniciar toospend mais de 10 $/ semana.
* Os utilizadores tendem a pacotes de premium toobuy nível 16, 24 e 32.

Obrigado analysis toothis Olá Director do projeto de Mobile decide toocreate push específicos notificação sequências tooincrease no vendas da aplicação. Ele cria três sequências de push que ele chama: bem-vindo programa, o programa de vendas e o programa inativa. Para obter mais informações consulte toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
