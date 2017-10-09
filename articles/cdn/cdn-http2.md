---
title: suporte de aaaHTTP/2 na CDN do Azure | Microsoft Docs
description: Saiba mais sobre o suporte HTTP/2 e CDN.
services: cdn
documentationcenter: 
author: lichard
manager: erikre
editor: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: 2e5e5345e8cf5c40e080ebf18b4f13a239a5aac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="http2-support-in-azure-cdn"></a>Suporte HTTP/2 na CDN do Azure

HTTP/2 é tooHTTP/1.1\ uma revisão principal. Fornece mais rapidamente do desempenho da web, tempo de resposta reduzida e melhorada experiência do utilizador, mantendo os métodos HTTP familiares Olá, códigos de estado e semântica. Apesar de HTTP/2 toowork concebida com HTTP e HTTPS, muitos browsers do cliente suportam apenas HTTP/2 sobre TLS.

###<a name="http2-benefits"></a>Vantagens HTTP/2

benefícios Olá de HTTP/2 incluem:

*   **Multiplexação e simultaneidade**

    Utilizar HTTP 1.1, vários tornar vários pedidos de recursos requer várias ligações TCP e cada ligação tem uma tolerância de desempenho associada ao mesmo. HTTP/2 permite vários recursos toobe, pedida numa única ligação TCP.

*   **Compressão de cabeçalho**

    Através da compressão de cabeçalhos de Olá HTTP servidos recursos, hora de transmissão de Olá é significativamente reduzida.

*   **Dependências de sequência**

    Dependências de sequência permitem ao cliente Olá tooindicate toohello servidor que recursos tem prioridade.


##<a name="http2-browser-support"></a>Suporte de browsers HTTP/2

Todos os browsers principais Olá tem implementada HTTP/2 suporte das respetivas versões atuais. Browsers suportados não serão automaticamente contingência tooHTTP/1.1.

|Browser|Versão mínima|
|-------------|------------|
|Microsoft Edge| 12|
|Google Chrome| 43|
|Mozilla Firefox| 38|
|Opera| 32|
|Safari| 9|

##<a name="enabling-http2-support-in-azure-cdn"></a>Ativar o suporte HTTP/2 na CDN do Azure

Atualmente está ativo para o suporte HTTP/2 **CDN do Azure da Akamai** e **CDN do Azure da Verizon** perfis. Nenhuma ação adicional é necessária de clientes.

##<a name="next-steps"></a>Passos Seguintes

vantagens de Olá toosee de HTTP/2 em ação, consulte [esta demonstração da Akamai](https://http2.akamai.com/demo).

toolearn mais informações sobre HTTP/2, visite Olá os seguintes recursos:

*   [Home page de especificação de HTTP/2](https://http2.github.io/)
*   [Oficial HTTP/2 FAQ](https://http2.github.io/faq/)
*   [Informações da Akamai HTTP/2](https://http2.akamai.com/)

toolearn mais informações sobre as funcionalidades disponíveis da CDN do Azure, consulte Olá [descrição geral da CDN do Azure](https://azure.microsoft.com/documentation/articles/cdn-overview/).
