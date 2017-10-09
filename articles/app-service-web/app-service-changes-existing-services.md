---
title: "aaaAzure do serviço de aplicações e o respetivo impacto nos serviços do Azure existentes"
description: "Explica como Olá novo serviço de aplicações do Azure e as respetivas funcionalidades afetam existentes serviços no Azure."
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a>Serviço de Aplicações do Azure e serviços do Azure existentes
Este artigo descreve Olá alterações tooexisting Azure services como parte da Olá alteração toobring em conjunto vários serviços do Azure para [App Service do Azure](https://azure.microsoft.com/services/app-service/), uma nova oferta integrada.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a>Descrição geral
[App Service do Azure](https://azure.microsoft.com/services/app-service/) é um serviço de nuvem novos e únicos que permite aos programadores toocreate web apps e móveis para qualquer plataforma e de qualquer dispositivo. Serviço de aplicações é que uma solução integrada concebida toostreamline repetido funções de codificação, integrar com sistemas de SaaS e enterprise e automatizar processos empresariais ao satisfazer as suas necessidades de segurança, escalabilidade e fiabilidade.

Serviço de aplicações reúne Olá seguir existente do Azure serviços - [sites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), e [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) numa única combinado serviço, enquanto adicionar novas capacidades poderosas.  Serviço de aplicações permite-lhe Olá toohost os seguintes tipos de aplicações:

* Aplicações Web
* Mobile Apps
* Aplicações API
* Aplicações Lógicas

Olá tabela seguinte explica como existente do Azure serviços mapeiam tooApp serviço e Olá tipos de aplicações disponíveis dentro da mesma.

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%">Serviço do Azure existente</th>
<th align="left", style="width:10%">Serviço de Aplicações do Azure</th>
<th align="left", style="width:80%">O que foi alterado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Web Sites do Azure</td>
<td align="left">Aplicações Web</td>
<td align="left"><li>Para Web sites do Azure, o serviço de aplicações é estritamente limitado toochanging Olá nome sites tooWeb aplicações.
<p><li>Todas as instâncias existentes de Web sites estão agora Web Apps no App Service.</p>
<p><li>Pode aceder ao seus sites existentes através de Olá <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Portal do Azure</a>, onde poderá encontrar todos os sites existentes em <em>Web Apps</em>.</p>
<p><li><em>Planear o alojamento de Web</em> está agora <em>plano do App Service</em>. Um <em>plano do App Service</em> pode alojar qualquer tipo de aplicação de serviço de aplicações, tais como aplicações Web, móveis, lógicas ou API.</p>
<p><li>Serviço Web Apps do App do Azure em geral é disponibilidade.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/web/">Saiba mais sobre as aplicações Web</a>.</p></td>
</tr>
<tr class="even">
<td align="left">Serviços Móveis do Azure</td>
<td align="left">Mobile Apps</td>
<td align="left"><p><li>Mobile Services continuar toobe disponível como um serviço autónomo e permanecem totalmente suportados.</p>
<p><li>As Mobile Apps é um tipo de aplicação no App Service, integra-se a todas as funcionalidades de Olá do Mobile Services e muito mais.</p>
<p><li>É fácil demasiado<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrar a partir dos Mobile Services tooMobile aplicações</a>.</p>
<p><li>Como parte do serviço de aplicações, as Mobile Apps obter novas capacidades para além dos Mobile Services, tais como a integração no local e sistemas de SaaS, ranhuras, WebJobs, opções de dimensionamento melhor e mais de teste.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/mobile/">Saiba mais sobre as Mobile Apps</a>.</p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">Aplicações API</td>
<td align="left">
<p><li>As API Apps é um novo tipo de aplicação no App Service permite-lhe criar e consumir APIs na nuvem de Olá facilmente.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/api/">Saiba mais sobre API Apps</a>.</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">Aplicações Lógicas</td>
<td align="left">
<p><li>As Logic Apps é um novo tipo de aplicação no App Service permite-lhe automatizar facilmente os processos de negócios.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/logic/">Saiba mais sobre Logic Apps</a>.</p></td>
</tr>
<tr class="odd">
<td align="left">Serviços BizTalk do Azure</td>
<td align="left">BizTalk API Apps</td>
<td align="left">
<li><p>BizTalk Services continuar toobe disponível como um serviço autónomo e permanecem totalmente suportados.</p>
<li><p>Todos os Olá capacidades do BizTalk Services estão integradas no serviço de aplicações como API Apps ativar utilizadores tooperform enterprise integração de aplicações e cenários de integração de B2B com qualquer um dos tipos de aplicação Olá no App Service.</p>
<li><p>Com as Logic Apps, agora pode automatizar os processos de negócios através de um visual conceber experiência toocreate fluxos de trabalho.</p></td>
</tr>
</tbody>
</table>

toolearn mais, visite [documentação do App Service](https://azure.microsoft.com/documentation/services/app-service/).

