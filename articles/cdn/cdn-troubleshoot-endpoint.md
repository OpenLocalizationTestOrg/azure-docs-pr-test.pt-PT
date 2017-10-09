---
title: "pontos finais da CDN do Azure aaaTroubleshooting devolução de estado 404 | Microsoft Docs"
description: "Resolver problemas de 404 códigos de resposta com pontos finais da CDN do Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: b588a1eb-ab69-4fc7-ae4d-157c3e46f4a8
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 450bfbd641c869cfd88169a12c4b69819eaa7c26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-endpoints-returning-404-statuses"></a>Resolução de problemas em pontos finais da CDN que devolvem estados 404
Este artigo ajuda-o a resolver problemas com [pontos finais da CDN](cdn-create-new-endpoint.md) devolver 404 erros.

Se precisar de mais ajuda, a qualquer altura neste artigo, pode contactar Olá especialistas do Azure no [Olá MSDN Azure e Olá Stack Overflow fóruns](https://azure.microsoft.com/support/forums/). Em alternativa, pode também ficheiro um incidente de suporte do Azure. Aceda toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e clique em **obter suporte**.

## <a name="symptom"></a>Sintoma
Criou um perfil da CDN e um ponto final, mas o conteúdo não parece estar toobe disponível no Olá CDN.  Utilizadores que tentam tooaccess conteúdo através de Olá CDN URL receber os códigos de estado de HTTP 404. 

## <a name="cause"></a>Causa
Existem várias causas possíveis, incluindo:

* origem do ficheiro de Olá não está visível toohello CDN
* ponto final de Olá configurada incorretamente, provocando Olá CDN toolook no local incorreto Olá
* anfitrião de Olá está a rejeitar o cabeçalho de anfitrião Olá de Olá CDN
* ponto final de Olá não registou a tempo toopropagate ao longo de Olá CDN

## <a name="troubleshooting-steps"></a>Passos de resolução de problemas
> [!IMPORTANT]
> Depois de criar um ponto final de CDN, este não imediatamente estará disponível para utilização, como demora algum tempo para Olá registo toopropagate através de Olá CDN.  Para <b>CDN do Azure da Akamai</b> perfis, propagação normalmente concluída num minuto.  Para os perfis <b>CDN do Azure da Verizon</b>, a propagação normalmente fica concluída no prazo de 90 minutos, mas em certos casos pode demorar mais tempo.  Se concluir o passo de Olá deste documento e ainda estamos a preparar 404 respostas, considere a aguardar alguns toocheck de horas antes de abrir um pedido de suporte.
> 
> 

### <a name="check-hello-origin-file"></a>Verifique o ficheiro de origem Olá
Em primeiro lugar, deve verificar Olá esse ficheiro Olá queremos em cache está disponível no nosso origem e é acessível publicamente.  Olá toodo forma mais rápida, que é um browser de tooopen numa sessão em privado ou Incognito e procurar diretamente o ficheiro de toohello.  Apenas escreva ou cole o URL de Olá na caixa de endereço Olá e ver se que resulta num ficheiro de Olá esperado.  Neste exemplo, vou toouse um ficheiro tiver uma conta de armazenamento do Azure, acessível em `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`.  Como pode ver, passa com êxito o teste de Olá.

![Êxito!](./media/cdn-troubleshoot-endpoint/cdn-origin-file.png)

> [!WARNING]
> Enquanto é Olá mais rápida e tooverify de forma mais fácil o ficheiro estiver publicamente disponível, algumas configurações de rede na sua organização poderia conceder Olá ilusão que este ficheiro é publicamente disponível quando é, na verdade, apenas visíveis toousers da sua (da rede mesmo que está alojado no Azure).  Se tiver um browser externo a partir da qual pode testar, como um dispositivo móvel que não está ligada a rede da organização tooyour ou uma máquina virtual no Azure, que será melhor.
> 
> 

### <a name="check-hello-origin-settings"></a>Verifique as definições de origem Olá
Agora que tiver confirmado que iremos ficheiro Olá é publicamente disponível na Olá internet, mas deve verificar as nossas definições de origem.  No Olá [Portal do Azure](https://portal.azure.com), procure o perfil da CDN tooyour e clique em ponto final de Olá que está a resolução de problemas.  No Olá resultante **Endpoint** painel, clique em origem Olá.  

![Painel de ponto final com origem realçada](./media/cdn-troubleshoot-endpoint/cdn-endpoint.png)

Olá **origem** é apresentado o painel. 

![Painel de origem](./media/cdn-troubleshoot-endpoint/cdn-origin-settings.png)

#### <a name="origin-type-and-hostname"></a>Tipo de origem e nome de anfitrião
Certifique-se Olá **tipo de origem** estão corretas e, certifique-se Olá **nome de anfitrião de origem**.  A minha exemplo `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, Olá hostname parte Olá URL é `cdndocdemo.blob.core.windows.net`.  Como pode ver na captura de ecrã Olá, isto está correto.  Para armazenamento do Azure, aplicação Web e origens de serviço em nuvem, Olá **nome de anfitrião de origem** campo é uma lista pendente, pelo que não temos tooworry sobre spelling-la corretamente.  No entanto, se estiver a utilizar uma origem personalizado, é *absolutamente essencial* seu nome do anfitrião está escrito corretamente!

#### <a name="http-and-https-ports"></a>Portas HTTP e HTTPS
Olá outro toocheck coisa aqui é o **HTTP** e **portas HTTPS**.  Na maioria dos casos, 80 e 443 estão corretas e que vai necessitar sem alterações.  No entanto, se o servidor de origem Olá está à escuta numa porta diferente, que terá de toobe representado aqui.  Se não tiver a certeza, observe apenas Olá URL para o ficheiro de origem.  Olá HTTP e especificações de HTTPS, especifique as portas 80 e 443 como Olá predefinições. No meu URL `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, uma porta não for especificada, pelo que é assumida predefinição Olá 443 e as minhas definições estão corretas.  

No entanto, diga Olá URL para o ficheiro de origem que testada anteriormente é `http://www.contoso.com:8080/file.txt`.  Olá nota `:8080` no fim de Olá do segmento do nome de anfitrião de Olá.  Que indica a porta do Olá browser toouse `8080` tooconnect toohello web servidor `www.contoso.com`, pelo que terá tooenter 8080 no Olá **porta HTTP** campo.  É importante toonote que estas definições de porta afetam apenas as portas Olá o ponto final utiliza tooretrieve informações da origem de Olá.

> [!NOTE]
> **CDN do Azure da Akamai** pontos finais não permitem Olá TCP intervalo de portas completo para origens.  Para obter uma lista das portas de origem que não são permitidas, consulte [Portas de Origem Permitidas do Azure CDN da Akamai](https://msdn.microsoft.com/library/mt757337.aspx).  
> 
> 

### <a name="check-hello-endpoint-settings"></a>Verifique as definições de ponto final de Olá
Novamente no Olá **Endpoint** painel, clique em Olá **configurar** botão.

![Painel de ponto final com o botão Configurar realçado](./media/cdn-troubleshoot-endpoint/cdn-endpoint-configure-button.png)

Olá do ponto final **configurar** é apresentado o painel.

![Configurar o painel](./media/cdn-troubleshoot-endpoint/cdn-configure.png)

#### <a name="protocols"></a>Protocolos
Para **protocolos**, certifique-se de que o protocolo de Olá que está a ser utilizado por clientes de Olá está selecionado.  Olá mesmo protocolo utilizado pelo cliente de Olá será Olá um utilizado tooaccess de origem Olá, pelo que é importante toohave portas de origem de Olá configuradas corretamente na secção anterior Olá.  ponto final de Olá só escuta Olá HTTP e HTTPS portas predefinidas (80 e 443), independentemente das portas de origem Olá.

Vamos voltar tooour exemplo hipotético com `http://www.contoso.com:8080/file.txt`.  Como irá lembrar, Contoso especificado `8080` como as respetivas HTTP de porta, mas vamos também partem do princípio de que o especificado `44300` como a respetiva porta HTTPS.  Se um ponto final com o nome criadas `contoso`, seria o respetivo nome de anfitrião de ponto final CDN `contoso.azureedge.net`.  Um pedido para `http://contoso.azureedge.net/file.txt` é um pedido HTTP pelo ponto final de Olá teria de utilizar HTTP na porta 8080 tooretrieve a origem de Olá.  Um pedido seguro através de HTTPS, `https://contoso.azureedge.net/file.txt`, causaria Olá endpoint toouse HTTPS na porta 44300 quando obter Olá ficheiro a partir da origem de Olá.

#### <a name="origin-host-header"></a>Cabeçalho de anfitrião de origem
Olá **cabeçalho de anfitrião de origem** é o valor do cabeçalho de anfitrião de Olá enviado toohello origem com cada pedido.  Na maioria dos casos, isto deve ser Olá mesmo como Olá **nome de anfitrião de origem** foi verificado anteriormente.  Um valor incorreto neste campo, geralmente, não irá fazer com que devolvem 404 Estados, mas é provável toocause outros Estados 4xx, dependendo de origem que Olá espera.

#### <a name="origin-path"></a>Caminho de origem
Por último, deve verificar a nossa **caminho de origem**.  Por predefinição, está em branco.  Só deve utilizar este campo se pretender que o âmbito de Olá toonarrow dos recursos de origem alojadas Olá pretende toomake disponível no Olá CDN.  

Por exemplo, no meu ponto final, posso pretendia todos os recursos no meu toobe de conta de armazenamento disponível, para que posso deixado **caminho de origem** em branco.  Isto significa que um pedido demasiado`https://cdndocdemo.azureedge.net/publicblob/lorem.txt` resulta numa ligação de ponto final do meu demasiado`cdndocdemo.core.windows.net` que solicita `/publicblob/lorem.txt`.  Da mesma forma, um pedido para `https://cdndocdemo.azureedge.net/donotcache/status.png` resulta no pedido de ponto final de Olá `/donotcache/status.png` da origem de Olá.

Mas e se não quiser toouse Olá CDN para cada caminho no meu origem?  Diga I apenas pretendia tooexpose Olá `publicblob` caminho.  Se introduzo */publicblob* na minha **caminho de origem** campo, o que fará com que Olá endpoint tooinsert */publicblob* antes de todos os pedidos efetuados toohello origem.  Isto significa que esse pedido Olá para `https://cdndocdemo.azureedge.net/publicblob/lorem.txt` agora irá demorar, na verdade, Olá pedido parte URL Olá, `/publicblob/lorem.txt`e de acréscimo `/publicblob` toohello início. Isto resulta num pedido para `/publicblob/publicblob/lorem.txt` da origem de Olá.  Se o caminho não resolve tooan real do ficheiro, origem Olá irá devolver um estado 404.  Olá correto URL tooretrieve lorem.txt neste exemplo, na verdade, seria `https://cdndocdemo.azureedge.net/lorem.txt`.  Tenha em atenção que não incluímos Olá */publicblob* caminho, porque parte do pedido de Olá de Olá URL é `/lorem.txt` e adiciona o ponto final de Olá `/publicblob`, resultando num `/publicblob/lorem.txt` a ser pedido Olá transmitido toohello origem .

