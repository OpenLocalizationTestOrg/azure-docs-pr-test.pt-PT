---
title: "aaaGet começar teste em produção para aplicações Web"
description: "Saiba mais sobre Olá teste na funcionalidade de produção (Sugestão) nas Web Apps do Azure App Service."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 4623468d-886e-4203-8012-8f86deb2790b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: cephalin
ms.openlocfilehash: 2ddbd532ffe2a4f3e07fd386d9741a3fde3639ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-test-in-production-for-web-apps"></a>Introdução ao teste na produção para Aplicações Web
Testar na produção, ou em direto-testar a sua aplicação web utilizando o tráfego de cliente em direto, é uma estratégia de teste que os programadores de aplicações cada vez mais integram os seus [desenvolvimento seja ágil](https://en.wikipedia.org/wiki/Agile_software_development) metodologia. Permite-lhe qualidade de Olá tootest das suas aplicações com o tráfego de utilizador em direto no seu ambiente de produção, como dados de toosynthesized oposição num ambiente de teste. Resultariam da exposição seus novos utilizadores tooreal da aplicação, pode ser informado sobre problemas reais de Olá que a aplicação poderá enfrentam assim que for implementado. Pode verificar a funcionalidade de Olá, o desempenho e o valor das atualizações de aplicação contra volume Olá, a velocidade e a variedade de tráfego de utilizador reais, que nunca pode aproximada num ambiente de teste.

## <a name="traffic-routing-in-app-service-web-apps"></a>Tráfego de encaminhamento na Web Apps do App Service
Com o encaminhamento de tráfego de Olá funcionalidade em [App Service do Azure](http://go.microsoft.com/fwlink/?LinkId=529714), pode direcionar uma parte do utilizador em direto tráfego tooone ou mais [ranhuras de implementação](web-sites-staged-publishing.md)e, em seguida, analise a sua aplicação com [aplicação do Azure Insights](/services/application-insights/) ou [Azure HDInsight](/services/hdinsight/), ou uma ferramenta de terceiros, como [New Relic](/marketplace/partners/newrelic/newrelic/) toovalidate a alteração. Por exemplo, pode implementar Olá os seguintes cenários com o serviço de aplicações:

* Detetar erros funcionais ou identificar estrangulamentos de desempenho na sua implementação de todo o toosite anterior de atualizações
* Efetuar o "teste controlada flights" das alterações ao medir as métricas de utilização na aplicação de beta Olá
* Gradualmente atualizem tooa nova atualização e transições fazer uma cópia para baixo a versão atual do toohello se ocorrer um erro 
* Otimizar os resultados de negócios da sua aplicação executando [A / B testa](https://en.wikipedia.org/wiki/A/B_testing) ou [testes multivariate](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) em várias ranhuras de implementação

### <a name="requirements-for-using-traffic-routing-in-web-apps"></a>Requisitos para utilizar o encaminhamento de tráfego nas Web Apps
* A aplicação web tem de executar **padrão** ou **Premium** camada, conforme necessário para vários blocos de implementação.
* Na ordem toowork corretamente, o encaminhamento de tráfego necessita de toobe cookies ativada no browser dos utilizadores Olá. Encaminhamento de tráfego utiliza cookies toopin uma ranhura de implementação do cliente browser tooa para a sessão de cliente do Olá vida Olá.
* Encaminhamento de tráfego suporta cenários avançados de sugestão através de cmdlets do PowerShell do Azure.

## <a name="route-traffic-segment-tooa-deployment-slot"></a>Ranhura de implementação de tooa de segmento de tráfego de rotas
No nível básico Olá, cada cenário de sugestão, encaminhar uma percentagem predefinida do seu bloco de implementação de não produção de tooa de tráfego em direto. toodo passos de Olá, siga abaixo:

> [!NOTE]
> Olá passos aqui descritos pressupõe que já tem um [ranhura de implementação de não produção](web-sites-staged-publishing.md) e esse Olá pretendido conteúdo de aplicação web já está [implementado](web-sites-deploy.md) tooit.
> 
> 

1. Iniciar sessão Olá [Portal do Azure](https://portal.azure.com/).
2. No painel da sua aplicação web, clique em **definições** > **o encaminhamento de tráfego**.
   ![](./media/app-service-web-test-in-production/01-traffic-routing.png)
3. Ranhura de Olá selecione que pretende que percentagem do tooroute tráfego tooand Olá do tráfego total de Olá pretendidos ao nível, em seguida, clique em **guardar**.
   
    ![](./media/app-service-web-test-in-production/02-select-slot.png)
4. Painel do bloco de implementação toohello aceda. Deverá ver agora a ser encaminhado tooit de tráfego em direto.
   
    ![](./media/app-service-web-test-in-production/03-traffic-routed.png)

Depois de configurar o encaminhamento de tráfego, Olá especificar a percentagem de clientes serão aleatoriamente encaminhadas tooyour ranhura de não produção. No entanto, é importante toonote assim que um cliente estiver ranhura específico tooa automaticamente encaminhadas, a ranhura de "afixado" toothat para vida Olá dessa sessão de cliente. Isto feito através de uma sessão de utilizador do cookie toopin Olá. Se inspecionar os pedidos HTTP de Olá, irá encontrar um `TipMix` cookie em cada pedido subsequente.

![](./media/app-service-web-test-in-production/04-tip-cookie.png)

## <a name="force-client-requests-tooa-specific-slot"></a>Forçar ranhura específico do tooa de pedidos de cliente
Na adição tooautomatic o encaminhamento de tráfego, o serviço de aplicações é ranhura do tooroute capaz de pedidos tooa específico. Isto é útil quando pretender que o seu tooopt capaz de toobe utilizadores- ou a ativamente da sua aplicação beta. toodo isto, utilize Olá `x-ms-routing-name` parâmetro de consulta.

tooreroute utilizadores tooa ranhura específica a utilizar `x-ms-routing-name`, tem de se certificar de que ranhura Olá já foi adicionada a lista de encaminhamento de tráfego toohello. Uma vez que pretendem tooroute tooa ranhura explicitamente, não interessa Olá real encaminhamento percentagem de definir. Se quiser, pode craft uma "ligação beta" que os utilizadores podem clicar tooaccess Olá aplicação beta.

![](./media/app-service-web-test-in-production/06-enable-x-ms-routing-name.png)

### <a name="opt-users-out-of-beta-app"></a>Optar ativamente por participar utilizadores fora da aplicação de beta
optar ativamente por participar toolet utilizadores fora da sua aplicação beta, por exemplo, pode colocar esta ligação na sua página web:

    <a href="<webappname>.azurewebsites.net/?x-ms-routing-name=self">Go back tooproduction app</a>

Olá cadeia `x-ms-routing-name=self` Especifica a ranhura de produção Olá. Assim hello ligação de Olá do acesso de browser do cliente, não só é redirecionado-toohello ranhura de produção, mas todos os pedidos subsequentes irão conter Olá `x-ms-routing-name=self` cookie que pins ranhura de produção do Olá sessão toohello.

![](./media/app-service-web-test-in-production/05-access-production-slot.png)

### <a name="opt-users-in-toobeta-app"></a>Optar ativamente por utilizadores na aplicação toobeta
utilizadores de toolet optar ativamente por participar na aplicação de beta tooyour, conjunto Olá mesmo consultar o nome do parâmetro toohello da ranhura de produção não Olá, por exemplo:

        <webappname>.azurewebsites.net/?x-ms-routing-name=staging

## <a name="more-resources"></a>Mais recursos
* [Configurar ambientes para web apps no App Service do Azure de teste](web-sites-staged-publishing.md)
* [Implementar uma aplicação complexa previsibilidade no Azure](app-service-deploy-complex-application-predictably.md)
* [Desenvolvimento de software seja ágil App Service do Azure](app-service-agile-software-development.md)
* [Utilizar eficazmente os ambientes de DevOps para as suas aplicações web](app-service-web-staged-publishing-realworld-scenarios.md)

