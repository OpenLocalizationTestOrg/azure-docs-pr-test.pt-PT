---
title: Suporte de partilha (CORS) de recursos de origem aaaCross | Microsoft Docs
description: "Saiba como suporte de CORS tooenable para Olá dos serviços de armazenamento do Microsoft Azure."
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: carmonm
editor: tysonn
ms.assetid: a0229595-5b64-4898-b8d6-fa2625ea6887
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 2/22/2017
ms.author: cbrooks
ms.openlocfilehash: 0a6ec3bf6999c5faa7f0912dc2a47921aa01d3d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="cross-origin-resource-sharing-cors-support-for-hello-azure-storage-services"></a>Suporte de partilha de recursos de várias origens (CORS) para Olá dos serviços de armazenamento do Azure
A partir da versão 2013-08-15, serviços do storage do Azure Olá suportam a partilha de recursos de várias origens (CORS) para serviços Blob, tabela, fila e ficheiro de Olá. CORS é uma funcionalidade HTTP que permite uma aplicação web em execução recursos de tooaccess de domínio com um no outro domínio. Browsers da Web implementam uma restrição de segurança denominada [política da mesma origem](http://www.w3.org/Security/wiki/Same_Origin_Policy) impede que uma página web a partir de APIs chamadas num domínio diferente; CORS fornece uma forma segura tooallow um domínio (domínio de origem Olá) toocall APIs noutro domínio. Consulte Olá [especificação de CORS](http://www.w3.org/TR/cors/) para obter detalhes sobre CORS.

Pode definir as regras CORS individualmente para cada um dos Olá serviços de armazenamento, chamando [definir propriedades de serviço Blob](https://msdn.microsoft.com/library/hh452235.aspx), [definir propriedades de serviço fila](https://msdn.microsoft.com/library/hh452232.aspx), e [definir propriedades do serviço tabela](https://msdn.microsoft.com/library/hh452240.aspx). Depois de definir as regras CORS Olá para o serviço de Olá, em seguida, um pedido autenticado corretamente realizado em serviço Olá de outro domínio será avaliado toodetermine se é permitido em conformidade com as regras de toohello que especificou.

> [!NOTE]
> Tenha em atenção que CORS não é um mecanismo de autenticação. Qualquer pedido efetuado em relação a um recurso de armazenamento, quando ativar a CORS tem de ter uma assinatura de uma autenticação adequada ou têm de ser efetuado em relação a um recurso público.
> 
> 

## <a name="understanding-cors-requests"></a>Noções sobre pedidos CORS
Um pedido de CORS de um domínio de origem pode ser composto por duas pedidos separados:

* Um pedido prévia, que consulta as restrições de CORS Olá impostas pelo serviço de Olá. pedido de verificação prévia de Olá é necessário, a menos que o método de pedido de Olá um [método simples](http://www.w3.org/TR/cors/), que significa que GET, HEAD ou POST.
* pedido real de Olá, efetuado relativamente aos recursos de Olá assim o desejar.

### <a name="preflight-request"></a>Pedido de verificação prévia
pedido de verificação prévia Olá consultas Olá restrições de CORS que foram estabelecidas pelo proprietário da conta Olá Olá para serviço de armazenamento. browser da web Hello (ou outros agentes de utilizador) envia um pedido de opções que inclui os cabeçalhos de pedido de Olá, domínio método e origem. serviço de armazenamento Olá avalia operação Olá pretendido com base num conjunto de regras CORS que especificar os domínios de origem, métodos de pedido de pré-configurado e cabeçalhos de pedido podem ser especificados num pedido real contra um recurso de armazenamento.

Se CORS está ativada para o serviço de Olá e existe uma regra CORS que corresponde ao pedido de verificação prévia de Olá, serviço Olá responde com o código de estado 200 (OK) e inclui os cabeçalhos de controlo de acesso de Olá necessária na resposta Olá.

Se CORS não está ativada para o serviço de Olá ou pedido de verificação prévia de Olá não corresponde a nenhuma regra CORS, o serviço Olá responderá com o código de estado 403 (proibido).

Se Olá opções pedido não contém hello necessários cabeçalhos CORS (Olá origem e cabeçalhos de pedido-método de acesso-controlo), o serviço de Olá responderá com o código de estado 400 (pedido incorreto).

Tenha em atenção que um pedido de verificação prévia é avaliado em comparação com o serviço de Olá (Blob, fila e tabela) e não em relação aos Olá recurso requerido. tem de ter ativada ao proprietário da conta Olá CORS como parte das propriedades de serviço de conta Olá por ordem para Olá pedido toosucceed.

### <a name="actual-request"></a>Pedido real
Depois de pedido de verificação prévia de Olá é aceite e é devolvida a resposta Olá, browser Olá irá emitir o pedido real de Olá contra recursos de armazenamento Olá. browser de Olá irá negar o pedido real Olá imediatamente se hello prévia pedido foi rejeitado.

pedido real Olá é tratado como normal pedido contra o serviço de armazenamento Olá. presença de Olá de cabeçalho de origem Olá indica que o pedido Olá é um pedido CORS e serviço Olá irá verificar Olá correspondente as regras CORS. Se for encontrada uma correspondência, cabeçalhos de Olá controlo de acesso são adicionados toohello resposta e enviados toohello back-cliente. Se não for encontrada uma correspondência, cabeçalhos de controlo de acesso CORS Olá não são devolvidos.

## <a name="enabling-cors-for-hello-azure-storage-services"></a>Ativar o CORS para serviços de armazenamento do Azure Olá
As regras CORS são definidas ao nível de serviço Olá, pelo que precisa tooenable ou desativar a CORS para cada serviço (Blob, fila e tabela) em separado. Por predefinição, a CORS está desativada para cada serviço. tooenable CORS, terá de propriedades de serviço apropriado tooset Olá utilizando a versão 2013-08-15 ou posterior e adicione as propriedades do serviço toohello de regras de CORS. Para obter detalhes sobre como tooenable ou desativar a CORS para um serviço e como tooset CORS regras,. Consulte demasiado[definir propriedades de serviço Blob](https://msdn.microsoft.com/library/hh452235.aspx), [definir propriedades de serviço fila](https://msdn.microsoft.com/library/hh452232.aspx), e [Definir tabela Propriedades do serviço](https://msdn.microsoft.com/library/hh452240.aspx).

Eis um exemplo de uma única regra CORS, especificado através de uma operação definir propriedades de serviço:

```xml
<Cors>    
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com, http://www.fabrikam.com</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <AllowedHeaders>x-ms-meta-data*,x-ms-meta-target*,x-ms-meta-abc</AllowedHeaders>
        <ExposedHeaders>x-ms-meta-*</ExposedHeaders>
        <MaxAgeInSeconds>200</MaxAgeInSeconds>
    </CorsRule>
<Cors>
```

Cada elemento incluído Olá CORS regra é descrito abaixo:

* **AllowedOrigins**: os domínios de origem Olá permitidos toomake um pedido de armazenamento de Olá service através de CORS. domínio de origem Olá é domínio Olá do qual Olá pedido tem origem. Tenha em atenção que a origem de Olá tem de ser uma correspondência exata sensível com origem Olá que idade do utilizador de Olá envia toohello serviço. Também pode utilizar o caráter universal de Olá ' *' tooallow todos os pedidos de toomake de domínios de origem através de CORS. No exemplo de Olá acima, Olá domínios [http://www.contoso.com](http://www.contoso.com) e [http://www.fabrikam.com](http://www.fabrikam.com) possa fazer pedidos contra serviço Olá utilizando a CORS.
* **AllowedMethods**: métodos Olá (verbos de pedido HTTP) pode utilizar esse domínio de origem Olá para um pedido CORS. No exemplo de Olá acima, são permitidos apenas pedidos PUT e GET.
* **AllowedHeaders**: cabeçalhos de pedido de Olá pode especificar esse domínio de origem Olá Olá CORS pedido. No exemplo de Olá acima, todos os cabeçalhos de metadados a partir x-ms-meta-data, x-ms-meta-destino e x-ms-meta-abc são permitidos. Tenha em atenção que caráter universal de Olá ' *' indica que o início qualquer cabeçalho com Olá especificado prefixo é permitido.
* **ExposedHeaders**: Olá cabeçalhos de resposta que podem ser enviados no pedido CORS do Olá resposta toohello e expostos pelo emissor do Olá browser toohello pedido. Exemplo de Olá acima, o browser Olá é instruído tooexpose partir qualquer cabeçalho x-ms-meta.
* **MaxAgeInSeconds**: tempo de quantidade máxima de Olá que um browser deve colocar em cache pedidos de opções de verificação prévia Olá.

Olá dos serviços de armazenamento do Azure suportam a especificação de cabeçalhos com prefixo para ambos os Olá **AllowedHeaders** e **ExposedHeaders** elementos. tooallow uma categoria dos cabeçalhos, pode especificar uma categoria de toothat prefixo comuns. Por exemplo, especificar *x-ms-meta** como um cabeçalho com prefixo estabelece uma regra que corresponde a todos os cabeçalhos que começam com x-ms-meta.

Olá seguintes limitações aplicam-se tooCORS regras:

* Pode especificar cópia de segurança toofive regras CORS por serviço de armazenamento (Blob, tabela e fila).
* tamanho máximo do Olá de todas as definições CORS da regras no pedido de Olá, excluindo as etiquetas XML, não deve ter mais de 2 KB.
* comprimento de Olá de um cabeçalho permitido, cabeçalho exposto ou origem permitida não deve exceder 256 carateres.
* Cabeçalhos permitidos e expostos cabeçalhos podem ser:
  * Cabeçalhos literais, onde o nome de cabeçalho exato de Olá for fornecido, tais como **x-ms-meta-processados**. Um máximo de 64 cabeçalhos literais pode ser especificado no pedido de Olá.
  * Cabeçalhos, onde um prefixo de cabeçalho de Olá for fornecido, tais como o prefixo **x-ms-meta-data***. Especificar um prefixo desta forma permite ou expõe qualquer cabeçalho que comece com Olá fornecido prefixo. Um máximo de dois cabeçalhos com prefixo pode ser especificado no pedido de Olá.
* Olá métodos (ou verbos HTTP) especificado no Olá **AllowedMethods** elemento deve ter métodos toohello suportados pelo serviço de armazenamento do Azure APIs. Métodos suportados são DELETE, GET, HEAD, intercalação, POST, as opções e PUT.

## <a name="understanding-cors-rule-evaluation-logic"></a>Compreender a lógica de avaliação da regra CORS
Quando um serviço de armazenamento recebe um pedido de verificação prévia ou real, avalia esse pedido com base nas regras CORS Olá que ter estabelecida para o serviço de Olá através de operação de definir propriedades de serviço apropriado Olá. As regras CORS são avaliadas por ordem de Olá em que foram definidas no corpo do pedido de Olá de Olá operação definir propriedades de serviço.

As regras CORS são avaliadas da seguinte forma:

1. Em primeiro lugar, o domínio de origem Olá de pedido de Olá é verificado com domínios Olá listados para Olá **AllowedOrigins** elemento. Se o domínio de origem Olá está incluído na lista de Olá ou todos os domínios são permitidos com um caráter universal Olá ' *', em seguida, as regras continua de avaliação. Se o domínio de origem Olá não estiver incluído, em seguida, Olá pedido falha.
2. Em seguida, o método hello (ou o verbo HTTP) do pedido de Olá é verificado com métodos de Olá apresentados por Olá **AllowedMethods** elemento. Se o método de Olá está incluído na lista de Olá, avaliação de regras prossegue; caso contrário, em seguida, o pedido de Olá falhar.
3. Se o pedido de Olá corresponde a uma regra no respetivo domínio de origem e o respetivo método, essa regra é selecionado tooprocess Olá pedido e não existem regras adicionais são avaliadas. Antes do pedido de Olá pode ter êxito, no entanto, quaisquer cabeçalhos especificados num pedido de Olá são verificados relativamente contra cabeçalhos Olá listados no Olá **AllowedHeaders** elemento. Se os cabeçalhos de Olá enviados não corresponderem Olá permitido cabeçalhos, o pedido de Olá falha.

Uma vez que as regras de Olá são processadas pela ordem de Olá estiverem presentes no corpo do pedido de Olá, recomendadas as melhores práticas que especifique as regras de mais restritivas Olá com respeitem tooorigins primeiro na lista de Olá, para que estes são avaliadas primeiro. Especifique as regras que são menos restritivas – por exemplo, um tooallow regra todas as origens – no fim de Olá da lista de Olá.

### <a name="example--cors-rules-evaluation"></a>Exemplo-avaliação de regras de CORS
Olá exemplo seguinte mostra um corpo do pedido parcial para regras CORS de tooset uma operação Olá dos serviços de armazenamento. Consulte [definir propriedades de serviço Blob](https://msdn.microsoft.com/library/hh452235.aspx), [definir propriedades de serviço fila](https://msdn.microsoft.com/library/hh452232.aspx), e [definir propriedades de serviço tabela](https://msdn.microsoft.com/library/hh452240.aspx) para obter detalhes sobre como construir o pedido de Olá.

```xml
<Cors>
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com</AllowedOrigins>
        <AllowedMethods>PUT,HEAD</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-blob-content-type, x-ms-blob-content-disposition</AllowedHeaders>
    </CorsRule>
    <CorsRule>
        <AllowedOrigins>*</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-blob-content-type, x-ms-blob-content-disposition</AllowedHeaders>
    </CorsRule>
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com</AllowedOrigins>
        <AllowedMethods>GET</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-client-request-id</AllowedHeaders>
    </CorsRule>
</Cors>
```

Em seguida, considere Olá CORS pedidos os seguintes:

| Pedir |  |  | Resposta |  |
| --- | --- | --- | --- | --- |
| **Método** |**Origem** |**Cabeçalhos de pedido** |**Correspondência de regra** |**Resultado** |
| **COLOCAR** |http://www.contoso.com |x-ms-BLOBs-tipo de conteúdo |Primeira regra |Êxito |
| **INTRODUÇÃO** |http://www.contoso.com |x-ms-BLOBs-tipo de conteúdo |Segunda regra |Êxito |
| **INTRODUÇÃO** |http://www.contoso.com |x-ms-client-request-id |Segunda regra |Falha |

primeiro pedido efetuado Olá corresponde à primeira regra de Olá – domínio de origem Olá corresponde ao Olá permitido origens, o método de Olá corresponde Olá permitido métodos e cabeçalho de Olá corresponde Olá permitido cabeçalhos – e, por isso, é concluída com êxito.

pedido de segundo Olá não corresponde a primeira regra de Olá porque o método Olá não corresponde ao hello permitido métodos. No entanto, corresponde a segunda regra de Olá, pelo que será efetuada com êxito.

pedido de terceiro Olá corresponde a segunda regra de Olá no respetivo domínio de origem e o método, pelo que não existem regras adicionais são avaliadas. No entanto, Olá *cabeçalho x-ms-client-request-id* não é permitido pelo segunda regra de Olá, pelo que o pedido de Olá falha, não obstante facto Olá que semântica de Olá de regra terceira Olá seria tenham permitido-toosucceed.

> [!NOTE]
> Embora este exemplo mostra uma regra menos restritiva antes de um mais restritivo, em geral Olá melhor prática é regras mais restritivas do toolist Olá primeiro.
> 
> 

## <a name="understanding-how-hello-vary-header-is-set"></a>Compreender a forma como o cabeçalho Vary de Olá está definido
Olá *Vary* cabeçalho é um cabeçalho HTTP/1.1 padrão constituída por um conjunto de campos de cabeçalho de pedido aconselhe processo agente de utilizador do browser ou de Olá sobre critérios de Olá que foram selecionados por Olá servidor tooprocess Olá pedido. Olá *Vary* cabeçalho é essencialmente utilizado para a colocação em cache por proxies, browsers e CDNs, que utilizá-lo toodetermine como resposta Olá deve ser colocados em cache. Para obter mais informações, consulte especificação Olá para Olá [cabeçalho Vary](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).

Quando o browser Olá ou outro agente de utilizador Olá coloca resposta em cache de um pedido CORS, o domínio de origem Olá é colocado em cache, como Olá permitido origem. Quando um segundo problemas de domínio Olá mesmo pedido para um recurso de armazenamento enquanto cache Olá está ativa, o agente de utilizador de Olá obtém o domínio de origem em cache de Olá. domínio de segundo Olá não corresponde ao domínio em cache Olá, para que o pedido de Olá falhar quando caso contrário será bem sucedida. Em certos casos, o armazenamento de Azure define o cabeçalho Vary de Olá demasiado**origem** tooinstruct Olá utilizador toosend Olá subsequente CORS pedido toohello serviço do agente quando Olá pedir domínio difere do Olá em cache de origem.

Define o armazenamento do Azure Olá *Vary* cabeçalho demasiado**origem** para os pedidos GET/HEAD reais no Olá seguintes casos:

* Quando o pedido de Olá origem corresponde exatamente ao hello permitida origem definida por uma regra CORS. toobe uma correspondência exata, regra CORS Olá não pode incluir um caráter universal ' * ' carateres.
* Não existe nenhuma origem de pedido de Olá correspondente da regra, mas CORS está ativada para o serviço de armazenamento Olá.

No caso de olá onde um pedido GET/HEAD corresponde a uma regra CORS que permite que todas as origens, resposta Olá indica que todas as origens são permitidas e cache de agente de utilizador Olá irá permitir que os pedidos subsequentes de qualquer domínio de origem enquanto cache Olá está ativa.

Note que dos pedidos de utilização de métodos diferentes de GET/HEAD, serviços de armazenamento Olá serão não definida cabeçalho Vary de Olá, uma vez que os métodos de toothese respostas não estão em cache por agentes de utilizador.

Olá seguinte tabela indica o Azure como armazenamento responderá a pedidos de tooGET/HEAD com base no Olá anteriormente mencionadas casos:

| Pedir | Definição de conta e o resultado da avaliação da regra |  |  | Resposta |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Cabeçalho de origem presente no pedido** |**CORS regra (s) especificado para este serviço** |**Existe uma regra correspondente que permite que todas as origens (*)** |**Existe uma regra correspondente para a correspondência exata de origem** |**Resposta inclui tooOrigin de conjunto de cabeçalho Vary** |**Resposta inclui acesso controlo-permitido-origens: "*"** |**Resposta inclui acesso-controlo-expostos-cabeçalhos** |
| Não |Não |Não |Não |Não |Não |Não |
| Não |Sim |Não |Não |Sim |Não |Não |
| Não |Sim |Sim |Não |Não |Sim |Sim |
| Sim |Não |Não |Não |Não |Não |Não |
| Sim |Sim |Não |Sim |Sim |Não |Sim |
| Sim |Sim |Não |Não |Sim |Não |Não |
| Sim |Sim |Sim |Não |Não |Sim |Sim |

## <a name="billing-for-cors-requests"></a>Faturação para pedidos CORS
Os pedidos com êxito prévias são faturadas se tiver ativado o CORS para qualquer um dos serviços de armazenamento Olá para a sua conta (chamando [definir propriedades de serviço Blob](https://msdn.microsoft.com/library/hh452235.aspx), [definir propriedades de serviço fila](https://msdn.microsoft.com/library/hh452232.aspx), ou [ Definir as propriedades do serviço tabela](https://msdn.microsoft.com/library/hh452240.aspx)). toominimize encargos, considere definir Olá **MaxAgeInSeconds** elemento no seu CORS regras valor grande tooa para que hello agente de utilizador coloca em cache pedidos de Olá.

Pedidos de verificação prévias sem não serão cobrados.

## <a name="next-steps"></a>Passos seguintes
[Definir as propriedades de serviço Blob](https://msdn.microsoft.com/library/hh452235.aspx)

[Definir as propriedades do serviço fila](https://msdn.microsoft.com/library/hh452232.aspx)

[Definir as propriedades do serviço tabela](https://msdn.microsoft.com/library/hh452240.aspx)

[Especificação de partilha de recursos de várias origens de W3C](http://www.w3.org/TR/cors/)

