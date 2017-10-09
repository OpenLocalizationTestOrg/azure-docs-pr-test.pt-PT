---
title: "a compressão do ficheiro de aaaTroubleshooting na CDN do Azure | Microsoft Docs"
description: "Resolva problemas com a compressão do ficheiro de CDN do Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a>Resolver problemas de compressão de ficheiros CDN
Este artigo ajuda-o a resolver problemas com [compressão do ficheiro CDN](cdn-improve-performance.md).

Se precisar de mais ajuda, a qualquer altura neste artigo, pode contactar Olá especialistas do Azure no [Olá MSDN Azure e Olá Stack Overflow fóruns](https://azure.microsoft.com/support/forums/). Em alternativa, pode também ficheiro um incidente de suporte do Azure. Aceda toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e clique em **obter suporte**.

## <a name="symptom"></a>Sintoma
A compressão para o ponto final está ativada, mas os ficheiros estão a ser devolvidos descomprimidos.

> [!TIP]
> toocheck se os ficheiros estão a ser devolvidos comprimidos, é preciso toouse uma ferramenta como [Fiddler](http://www.telerik.com/fiddler) ou do seu browser [ferramentas de programador](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).  Verificação de cabeçalhos de resposta de Olá HTTP devolveu o CDN em cache conteúdos.  Se houver um cabeçalho com o nome `Content-Encoding` com um valor de **gzip**, **bzip2**, ou **deflate**, o conteúdo é comprimido.
> 
> ![Cabeçalho de codificação de conteúdo](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a>Causa
Existem várias causas possíveis, incluindo:

* Olá pedida não é elegível para compressão de conteúdo.
* Compressão não está ativada para Olá ficheiro tipo pedido.
* pedido HTTP Olá não inclui um cabeçalho de pedir um tipo de compressão válido.

## <a name="troubleshooting-steps"></a>Passos de resolução de problemas
> [!TIP]
> Como implementar novo pontos finais, as alterações de configuração da CDN tomar algumas toopropagate tempo através da rede Olá.  Normalmente, as alterações sejam aplicadas dentro de 90 minutos.  Se este for Olá pela primeira vez que tiver configurado a compressão para o ponto final CDN, deve considerar a aguardar toobe 1-2 horas se as definições de compressão Olá terem sido propagados toohello POPs. 
> 
> 

### <a name="verify-hello-request"></a>Verifique se o pedido de Olá
Em primeiro lugar, iremos deve efetuar uma verificação rápida sanity pedido Olá.  Pode utilizar o seu browser [ferramentas de programador](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview Olá pedidos efetuados.

* Certifique-se de que está a ser enviado o pedido de Olá URL de ponto final de tooyour `<endpointname>.azureedge.net`e não a sua origem.
* Certifique-se de que o pedido de Olá contém um **codificação de aceitar** cabeçalho e Olá valor para essa cabeçalho contém **gzip**, **deflate**, ou **bzip2** .

> [!NOTE]
> **CDN do Azure da Akamai** perfis suporte apenas **gzip** codificação.
> 
> 

![Cabeçalhos de pedido CDN](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a>Verifique as definições de compressão (perfil de Standard CDN)
> [!NOTE]
> Este passo aplica-se apenas se o perfil de CDN é uma **CDN do Azure Standard da Verizon** ou **CDN do Azure Standard da Akamai** perfil. 
> 
> 

Navegue tooyour no ponto final em Olá [portal do Azure](https://portal.azure.com) e clique em Olá **configurar** botão.

* Certifique-se de que a compressão está ativada.
* Verifique se o tipo de MIME Olá Olá conteúdo toobe comprimido está incluído na lista de Olá dos formatos comprimidos.

![Definições de compressão de CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a>Verifique as definições de compressão (perfil de Premium CDN)
> [!NOTE]
> Este passo aplica-se apenas se o perfil de CDN é uma **CDN do Azure Premium da Verizon** perfil.
> 
> 

Navegue tooyour no ponto final em Olá [portal do Azure](https://portal.azure.com) e clique em Olá **gerir** botão.  portal suplementar Olá irá abrir.  Paire sobre Olá **HTTP grande** separador, em seguida, paire sobre Olá **definições da Cache** flyout.  Clique em **compressão**. 

* Certifique-se de que a compressão está ativada.
* Certifique-se Olá **tipos de ficheiro** lista contém uma lista separada por vírgulas (sem espaços) de tipos de MIME.
* Verifique se o tipo de MIME Olá Olá conteúdo toobe comprimido está incluído na lista de Olá dos formatos comprimidos.

![Definições de compressão CDN premium](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a>Certifique-se de que o conteúdo de Olá é colocado em cache
> [!NOTE]
> Este passo aplica-se apenas se o perfil de CDN é uma **CDN do Azure da Verizon** perfil (Standard ou Premium).
> 
> 

Utilizar ferramentas de programador do seu browser, verifique o ficheiro a Olá da tooensure de cabeçalhos de resposta de Olá é colocado em cache na região de olá onde está a ser pedida.

* Verifique Olá **servidor** cabeçalho de resposta.  cabeçalho de Olá deve ter o formato de Olá **Platform (servidor/POP ID)**, como mostrado no seguinte exemplo de Olá.
* Verifique Olá **X-Cache** cabeçalho de resposta.  deve ler o cabeçalho de Olá **ACESSOS**.  

![Cabeçalhos de resposta CDN](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a>Certifique-se de que o ficheiro de Olá cumpre os requisitos de tamanho de Olá
> [!NOTE]
> Este passo aplica-se apenas se o perfil de CDN é uma **CDN do Azure da Verizon** perfil (Standard ou Premium).
> 
> 

toobe elegível para compressão, um ficheiro tem de cumprir os requisitos de tamanho de Olá:

* Maior do que 128 bytes.
* Menor que 1 MB.

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a>Verificar a solicitação de Olá no servidor de origem Olá para um **através de** cabeçalho
Olá **através de** cabeçalho de HTTP indica o servidor de web de toohello Olá pedido está a ser transferida por um servidor proxy.  Os servidores web do Microsoft IIS por predefinição não comprimir respostas quando Olá pedido contém um **através de** cabeçalho.  toooverride este comportamento, efetue Olá seguinte:

* **IIS 6**: [definir HcNoCompressionForProxies = "FALSE" nas propriedades de Metabase do IIS Olá](https://msdn.microsoft.com/library/ms525390.aspx)
* **IIS 7 e até**: [definidas **noCompressionForHttp10** e **noCompressionForProxies** tooFalse numa configuração de servidor Olá](http://www.iis.net/configreference/system.webserver/httpcompression)

