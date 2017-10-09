---
title: "Descrição geral de aaaRedirect para Gateway de aplicação do Azure | Microsoft Docs"
description: "Saiba mais sobre a capacidade de redirecionamento Olá no Gateway de aplicação do Azure"
services: application-gateway
documentationcenter: na
author: amsriva
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/18/2017
ms.author: amsriva
ms.openlocfilehash: 7149e3bd000d336c51995fb0e90f971b4d9ba2be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-redirect-overview"></a>Descrição geral de redirecionamento do Gateway de aplicação

Um cenário comum para muitas aplicações web é toosupport automática HTTP tooHTTPS redirecionamento tooensure que toda a comunicação entre aplicações e os seus utilizadores ocorre através de um caminho encriptado. No passado, Olá, os clientes utilizou técnicas, como criar um conjunto de back-end dedicado cujo objetivo único é pedidos tooredirect recebe no tooHTTPS HTTP.  Gateway de aplicação já suporta tráfego de tooredirect capacidade em Olá Gateway de aplicação. Isto simplifica a configuração da aplicação, otimiza a utilização de recursos de Olá e suporta novos cenários de redirecionamento, incluindo global e com base no caminho de redirecionamento. O suporte de redirecionamento do Gateway de aplicação não está limitado tooHTTP -> redirecionamento HTTPS individualmente. Este é um mecanismo de redirecionamento genérico, que permite o redirecionamento de tráfego recebido na entidade Serviço de escuta de tooanother de um serviço de escuta no Gateway de aplicação. Também suporta redirecionamento tooan externo site bem. Suporte de redirecionamento do Gateway de aplicação oferece Olá seguintes capacidades:

1. Redirecionamento global do serviço de escuta de tooanother de um serviço de escuta no Olá Gateway. Isto permite que o redirecionamento de HTTP tooHTTPS num site.
2. Com base no caminho de redirecionamento. Este tipo de redirecionamento de permite o redirecionamento de HTTP tooHTTPS apenas na área de um site específico, por exemplo uma área de carrinho de compras em falta por que/carrinho / *.
3. Redireciona tooexternal site.

![redirecionar](./media/application-gateway-redirect-overview/redirect.png)

Com esta alteração, os clientes teria toocreate um novo objeto de configuração de redirecionamento, o que especifica o serviço de escuta de destino de Olá ou redirecionamento de toowhich site externo, se pretendido. o elemento de configuração de Olá também suporta tooenable opções acrescentar o caminho URI Olá e consulta cadeia toohello redirecionado URL. Os clientes também poderia escolher se o redirecionamento é um temporário (código de estado HTTP 302) ou um redirecionamento permanente (código de estado HTTP 301). Uma vez criada esta configuração de redirecionamento é toohello ligado ao serviço de escuta de origem através de uma nova regra. Quando utilizar uma regra básica, Olá redirecionamento configuração está associada um serviço de escuta de origem e um redirecionamento global. Quando é utilizada uma regra com base no caminho, a configuração de redirecionamento de Olá está definida no mapa de caminho de URL Olá e, por conseguinte, só se aplica a área de caminho específico toohello de um site.

### <a name="next-steps"></a>Passos seguintes

[Configurar redirecionamento de URL num gateway de aplicação](application-gateway-configure-redirect-powershell.md)
