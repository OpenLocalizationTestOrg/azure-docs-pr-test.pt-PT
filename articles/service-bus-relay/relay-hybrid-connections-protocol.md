---
title: "Guia de protocolo de aaaAzure reencaminhamento híbrido ligações | Microsoft Docs"
description: "Guia de protocolo de ligações híbridas de reencaminhamento do Azure."
services: service-bus-relay
documentationcenter: na
author: clemensv
manager: timlt
editor: 
ms.assetid: 149f980c-3702-4805-8069-5321275bc3e8
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm;clemensv
ms.openlocfilehash: 2d145d919d606ae4722b063e1baf39fb845a600a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# Protocolo de ligações híbridas de reencaminhamento do Azure
Reencaminhamento do Azure é uma das pillars de capacidade chave Olá da plataforma do Service Bus do Azure de Olá. Olá novo *ligações híbridas* capacidade de reencaminhamento é uma evolução segura e protocolo open com base em HTTP e WebSockets. Este substitui o anterior Olá, igualmente denominado *BizTalk Services* funcionalidade que foi criada no foundation protocolo proprietário. integração de Olá de ligações híbridas para serviços de aplicações do Azure vai continuar toofunction como-é.

As ligações híbridas permite a comunicação de stream binário de bidirecionais entre duas aplicações de rede, durante os quais as partes de um ou ambos os podem residir atrás de firewalls ou dos NATs. Este artigo descreve as interações do lado do cliente de Olá com reencaminhamento de ligações híbridas Olá para ligação de clientes no serviço de escuta e funções do remetente e, como os serviços de escuta aceitarem novas ligações.

## Modelo de interação
reencaminhamento de ligações híbridas Olá liga-se duas partes, fornecendo um ponto de encontro Olá em nuvem do Azure que as entidades confiadoras podem detetar e ligar toofrom perspetiva da sua própria rede. Esse ponto de encontro é denominado "Ligação híbrida" neste e outra documentação na Olá APIs e também numa Olá portal do Azure. Olá ligações híbridas ponto final de serviço é referido tooas Olá "serviço" para rest Olá deste artigo. modelo de interação Olá leans no nomenclature Olá estabelecido pelo muitas outras APIs de rede.

Não há um serviço de escuta que primeiro indica ligações de entrada de toohandle de preparação e, subsequentemente, aceita-las à medida que chegam. Olá, no outro lado, existe uma ligação cliente que liga-se para o serviço de escuta de Olá, era esperado que toobe ligação aceite para estabelecer um caminho de comunicação bidirecional.
"Ligar", "Escuta," e "Aceitar" são Olá mesmo socket termos que encontrará na maior parte dos APIs.

Qualquer modelo de comunicação retransmitidas tem a efetuar ligações de saída para um ponto final de serviço, que faz com que Olá "serviço de escuta" também um "cliente" em utilização colloquial e também pode fazer com que outras sobrecargas terminologia de terceiros. terminologia preciso Olá que utilizamos, por conseguinte, para as ligações híbridas é o seguinte:

programas de Olá em ambos os lados de uma ligação são denominados "clientes", uma vez que são o serviço de toohello de clientes. Olá cliente que aguarda e aceita ligações é o "serviço de escuta", ou está consiga aceder tal toobe Olá "serviço de escuta função." Olá cliente que inicia uma nova ligação para um serviço de escuta através do serviço Olá denomina Olá ". o remetente", ou "função remetente".

### Interações do serviço de escuta
serviço de escuta de Olá tem quatro interações com o serviço de Olá; todos os detalhes de transmissão são descritos neste artigo na secção de referência de Olá.

#### Escutar
tooindicate serviço toohello preparação que um serviço de escuta está pronto tooaccept ligações, cria uma ligação de WebSocket saída. no handshake de ligação de Olá acarreta nome Olá de uma ligação híbrida configurado no espaço de nomes de reencaminhamento de Olá e um token de segurança que confers Olá "Escuta" correto esse nome.
Quando Olá WebSocket é aceite pelo serviço de Olá, registo Olá está concluído e Olá estabelecida web que websocket é mantida activa como Olá "canal de controlo" para ativar todas as interações subsequentes. o serviço de Olá permite cópias de segurança too25 em simultâneo os serviços de escuta numa ligação híbrida. Se existirem dois ou mais serviços de escuta Active Directory, ligações de entrada são equilibradas entre-los pela ordem aleatória; distribuição justa não é garantida.

#### Aceitar
Quando um remetente abre uma nova ligação no serviço de Olá, o serviço de Olá escolhe e notifica um dos serviços de escuta de Active Directory Olá no Olá da ligação híbrida. Esta notificação é enviada toohello escuta através do canal de controlo abra Olá como uma mensagem JSON que contêm Olá URL de ponto final de WebSocket de Olá Olá o serviço de escuta tem de ligar toofor ligação Olá a aceitar.

URL de Olá pode e tem de ser utilizada diretamente pelo serviço de escuta de Olá sem qualquer trabalho adicional.
informações de Olá codificado são apenas válida para um curto período de tempo, essencialmente, desde que o remetente Olá é disposto toowait Olá ligação toobe estabelecida ponto-a-ponto, mas a cópia de segurança tooa máximo de 30 segundos. URL de Olá só pode ser utilizado para a tentativa de uma ligação com êxito. Logo que Olá WebSocket ligação com Olá encontro que URL é estabelecido, toda a atividade adicional neste WebSocket é retransmitida do e o remetente de toohello, sem qualquer intervenção ou a interpretação pelo serviço de Olá.

#### Renovar
token de segurança de Olá que tem de ter o serviço de escuta do tooregister utilizados Olá e manter que o canal de controlo pode expirar enquanto o serviço de escuta de Olá está ativo. expiração do token Olá não afeta as ligações em curso, mas fazer com que toobe de canal de controlo de Olá ignorada pelo serviço de Olá em ou logo após momento Olá de expiração. a operação de "renovar" Olá é uma mensagem JSON que Olá escuta pode enviar token de Olá tooreplace associado de canal de controlo de Olá, para que hello canal de controlo pode ser mantida por períodos prolongados.

#### Ping
Se o canal de controlo de Olá permanece inativo durante muito tempo, intermediários na forma de Olá, tais como a carga balanceadores ou os NATs poderão remover ligação de TCP Olá. operação de "ping" Olá evita que enviando uma pequena quantidade de dados no canal de Olá que relembra todos os utilizadores numa rota de rede Olá essa ligação Olá destina-se toobe alive, e também serve como um teste "dinâmicos" para o serviço de escuta de Olá. Se Olá ping falhar, o canal de controlo de Olá deve ser considerada inutilizável e serviço de escuta de Olá deve voltar a ligar.

### Interação de remetente
remetente de Olá tem apenas uma única interação com o serviço de Olá: para estabelecer a ligação.

#### Ligar
a operação de "ligar" Olá abre um WebSocket num serviço Olá, fornecer Olá nome da ligação híbrida de Olá e (opcionalmente, mas necessário por predefinição), um token de segurança conferring permissão "Enviar" na cadeia de consulta Olá. serviço de Olá, em seguida, interage com o serviço de escuta de Olá Olá forma descrito anteriormente e serviço de escuta de Olá cria uma ligação de encontro que está associada este WebSocket. Depois de ter sido aceite Olá WebSocket, todas as interações adicionais em que WebSocket são com um serviço de escuta ligado.

### Interação resumo
resultado de Olá deste modelo de interação é que o cliente remetente Olá vem fora do handshake com um WebSocket "Limpar", que é que o serviço de escuta tooa ligado e que não necessita de nenhum preambles adicionais ou preparação. Este modelo permite praticamente qualquer existente WebSocket cliente implementação tooreadily tirar partido das Olá serviço ligações híbridas, fornecendo um URL construído corretamente na respetiva camada de cliente WebSocket.

Olá encontro ligação WebSocket Olá escuta obtém através da interação aceitar também está limpa e pode ser entregar tooany existente WebSocket implementação do servidor com algum abstração extra mínima que distingue entre "aceitar" operações no respetivo framework serviços de escuta de rede local e as ligações híbridas remoto "aceitam" operações.

## Referência do protocolo

Esta secção descreve os detalhes de Olá de interações de protocolo de Olá descritos anteriormente.

Todas as ligações de WebSocket que são efetuadas na porta 443 como uma atualização do 1.1 de HTTPS, o que é normalmente abstracted por alguns framework WebSocket ou API. A descrição aqui é mantida implementação independente, sem sugerindo uma arquitetura específica.

### Protocolo de serviço de escuta
protocolo de serviço de escuta de Olá é constituído por dois gestos de ligação e três operações de mensagem.

#### Ligação de canal de controlo do serviço de escuta
canal de controlo de Olá é aberta com criação de uma ligação de WebSocket para:

```
wss://{namespace-address}/$hc/{path}?sb-hc-action=...[&sb-hc-id=...]&sb-hc-token=...
```

Olá `namespace-address` é o nome de domínio completamente qualificado Olá de espaço de nomes do reencaminhamento do Azure Olá que anfitriões Olá da ligação híbrida, normalmente de forma Olá `{myname}.servicebus.windows.net`.

Opções de parâmetro de cadeia de consulta Olá são os seguintes.

| Parâmetro | Necessário | Descrição |
| --- | --- | --- |
| `sb-hc-action` |Sim |Para Olá de função Serviço de escuta de Olá parâmetro tem de ser **sb-hc-action = escuta** |
| `{path}` |Sim |caminho de espaço de nomes com codificação URL Olá de Olá pré-configurada tooregister da ligação híbrida neste serviço de escuta no. Esta expressão se toohello anexado fixo `$hc/` parte do caminho. |
| `sb-hc-token` |Sim\* |Olá serviço de escuta tem de fornecer um válido, com codificação URL Service Bus partilhado acesso Token para Olá espaço de nomes ou da ligação híbrida que confers Olá **escutar** à direita. |
| `sb-hc-id` |Não |Este ID fornecido pelo cliente opcional que permite que o rastreio de diagnóstico ponto-a-ponto. |

Se Olá ligação de WebSocket falhar devido a caminho de ligação híbrida toohello não a ser registado, ou um token inválido ou em falta ou alguns outros erros, comentários de erro Olá é fornecido com modelo de comentários de estado Olá regular HTTP 1.1. A descrição de estado contém um controlo-id de erro que pode ser comunicado ao pessoal de suporte do Azure:

| Código | Erro | Descrição |
| --- | --- | --- |
| 404 |Não foi encontrado |caminho de ligação híbrida Olá é inválido ou o URL de base de Olá tem um formato incorreto. |
| 401 |Não autorizado |token de segurança de Olá está em falta ou com formato incorreto ou é inválido. |
| 403 |Proibido |o token de segurança de Olá não é válido para este caminho para esta ação. |
| 500 |Erro interno |Ocorreu um erro no serviço de Olá. |

Se Olá ligação de WebSocket foi intencionalmente encerrado pelo serviço de Olá após esta foi inicialmente configurada, razão Olá para fazê-lo pelo que é comunicado utilizando um código de erro de protocolo de WebSocket adequado, juntamente com uma mensagem de erro descritivo também inclui um controlo ID. serviço de Olá irá não encerrar o canal de controlo sem encontrar uma condição de erro. Qualquer encerramento correto é controlado de cliente.

| Estado de WS | Descrição |
| --- | --- |
| 1001 |caminho de ligação híbrida Olá foi eliminado ou desativado. |
| 1008 |token de segurança de Olá expirou, se, por conseguinte, a política de autorização de Olá é violada. |
| 1011 |Ocorreu um erro no serviço de Olá. |

### Aceitar handshake
"aceitar" de Olá notificação é enviada através do canal de controlo anteriormente estabelecido pelo serviço de escuta do Olá serviço toohello como uma mensagem JSON num intervalo de texto de WebSocket. Não há nenhuma mensagem de toothis de resposta.

mensagem de saudação contém um objeto JSON com o nome "aceitar", que define Olá seguintes propriedades neste momento:

* **endereço** – Olá toobe de cadeia de URL utilizado para estabelecer Olá WebSocket toothe serviço tooaccept uma ligação recebida.
* **ID** – Olá Identificador exclusivo para esta ligação. Se o ID de Olá foi fornecido pelo cliente de remetente Olá, que é valor de remetente fornecido Olá, caso contrário, é um valor de gerada pelo sistema.
* **connectHeaders** – todos os cabeçalhos HTTP que foram fornecidos o ponto final de reencaminhamento de toohello pelo remetente Olá, que também inclui Olá protocolo de WebSocket seg e os cabeçalhos de extensões de WebSocket de seg.

#### Aceitar a mensagem

```json
{                                                           
    "accept" : {
        "address" : "wss://168.61.148.205:443/$hc/{path}?..."    
        "id" : "4cb542c3-047a-4d40-a19f-bdc66441e736",  
        "connectHeaders" : {                                         
            "Host" : "...",                                                
            "Sec-WebSocket-Protocol" : "...",                              
            "Sec-WebSocket-Extensions" : "..."                             
        }                                                            
     }                                                         
}
```

Olá endereço URL fornecido Olá mensagem JSON é utilizada pelo serviço de escuta de Olá para estabelecer hello WebSocket para aceitar ou rejeitar o socket de remetente Olá.

#### Ao aceitar o socket de Olá
tooaccept, o serviço de escuta de Olá estabelece um endereço de toohello fornecido de ligação de WebSocket.

Se Olá "aceitar" mensagem ativada uma `Sec-WebSocket-Protocol` cabeçalho, espera-se esse serviço de escuta de Olá só aceita Olá WebSocket se suporta esse protocolo. Além disso, define o cabeçalho de Olá como Olá que websocket é estabelecida.

Olá mesmo se aplica toohello `Sec-WebSocket-Extensions` cabeçalho. Se framework Olá suporta uma extensão, defini-lo deve Olá cabeçalho toohello do lado do servidor de resposta de Olá necessário `Sec-WebSocket-Extensions` handshake para extensão Olá.

URL de Olá podem ser utilizado como-destina-se estabelecer Olá aceitar o socket, mas contém os seguintes parâmetros:

| Parâmetro | Necessário | Descrição |
| --- | --- | --- |
| `sb-hc-action` |Sim |Para aceitar um socket, Olá parâmetro tem de ser`sb-hc-action=accept` |
| `{path}` |Sim |(consulte Olá seguir parágrafo) |
| `sb-hc-id` |Não |Ver descrição anterior **id**. |

`{path}`é o caminho de espaço de nomes com codificação URL Olá de Olá pré-configuradas da ligação híbrida no qual tooregister neste serviço de escuta. Esta expressão se toothe anexado fixo `$hc/` parte do caminho. 

Olá `path` expressão pode ser expandida com um sufixo e uma expressão de cadeia de consulta que se segue nome registado Olá após uma barra separating. Isto permite Olá remetente cliente toopass emissão argumentos toohello aceitar escuta quando não é possível tooinclude HTTP cabeçalhos. Olá expectativa é esse serviço de escuta de Olá framework analisa os parte de caminho fixo Olá e Olá nome registado do caminho e faz com que o resto Olá, possivelmente sem quaisquer argumentos de cadeia de consulta como prefixo `sb-`, aplicação toohello disponível para decidir se tooaccept Olá ligação.

Para obter mais informações, consulte Olá seguinte secção "Remetente protocolo".

Se houver um erro, o serviço de Olá pode responder a forma:

| Código | Erro | Descrição |
| --- | --- | --- |
| 403 |Proibido |Olá URL não é válido. |
| 500 |Erro interno |Ocorreu um erro no serviço de Olá |

Depois de estabelecida ligação Olá, servidor Olá encerra Olá WebSocket quando o remetente Olá WebSocket encerrado para baixo, ou com Olá seguinte estado:

| Estado de WS | Descrição |
| --- | --- |
| 1001 |cliente de remetente Olá encerra ligação Olá. |
| 1001 |caminho de ligação híbrida Olá foi eliminado ou desativado. |
| 1008 |token de segurança de Olá expirou, se, por conseguinte, a política de autorização de Olá é violada. |
| 1011 |Ocorreu um erro no serviço de Olá. |

#### Rejeitar socket Olá
Rejeitar socket Olá após inspecionar mensagem de "aceitar" Olá requer um handshake semelhante para que hello código de estado e a descrição de estado ao comunicar que o motivo da rejeição Olá possam circular volta toohello remetente.

Escolha de design de protocolo de Olá aqui é toouse um handshake de WebSocket (que é concebida tooend num Estado de erro definido), para que as implementações de cliente do serviço de escuta podem continuar toorely num cliente WebSocket e não precisa de utilizar um extra, bare cliente HTTP.

tooreject socket de Olá, cliente Olá assume o endereço de Olá URI da mensagem de "aceitar" Olá e acrescenta a cadeia de consulta dois parâmetros tooit, da seguinte forma:

| Param | Necessário | Descrição |
| --- | --- | --- |
| statusCode |Sim |Código de estado HTTP numérico. |
| StatusDescription |Sim |Razão legível humana da rejeição Olá. |

Olá que URI resultante é, em seguida, utilizado tooestablish uma ligação de WebSocket.

Quando concluir corretamente, este handshake intencionalmente ocorre uma falha com um código de erro HTTP 410, desde que foi estabelecida não WebSocket. Se algo não bate certo, Olá códigos a seguir descreve erro Olá:

| Código | Erro | Descrição |
| --- | --- | --- |
| 403 |Proibido |Olá URL não é válido. |
| 500 |Erro interno |Ocorreu um erro no serviço de Olá. |

### Renovação de token de serviço de escuta
Quando o token de serviço de escuta de Olá é sobre tooexpire, pode substituir, enviando um texto moldura toohello o serviço de mensagens através de canal de controlo de Olá estabelecida. A mensagem contém um objeto JSON chamado `renewToken`, que define Olá seguinte propriedade neste momento:

* **token** – um token de acesso de partilhado de barramento de serviço válido, com codificação URL para o espaço de nomes ou da ligação híbrida que confers Olá **escutar** à direita.

#### mensagem de renewToken

```json
{                                                                                                                                                                        
    "renewToken" : {                                                                                                                                                      
        "token" : "SharedAccessSignature sr=http%3a%2f%2fcontoso.servicebus.windows.net%2fhyco%2f&amp;sig=XXXXXXXXXX%3d&amp;se=1471633754&amp;skn=SasKeyName"  
    }                                                                                                                                                                     
}
```

Se a validação de token de Olá falhar, o acesso é negado e o serviço em nuvem Olá fecha o canal de controlo de Olá WebSocket com um erro. Caso contrário, não há nenhuma resposta.

| Estado de WS | Descrição |
| --- | --- |
| 1008 |token de segurança de Olá expirou, se, por conseguinte, a política de autorização de Olá é violada. |

## Protocolo de remetente
protocolo de remetente de Olá é um serviço de escuta é estabelecido de forma de toohello eficazmente idênticos.
o objetivo de Olá é transparência máxima de Olá ponto-a-ponto WebSocket. endereço de Olá ligar Olá toois que iguais do serviço de escuta de Olá, mas Olá "action" é diferente e o token tem uma permissão diferentes:

```
wss://{namespace-address}/$hc/{path}?sb-hc-action=...&sb-hc-id=...&sbc-hc-token=...
```

Olá *endereço de espaço de nomes* é o nome de domínio completamente qualificado Olá de espaço de nomes do reencaminhamento do Azure Olá que anfitriões Olá da ligação híbrida, normalmente de forma Olá `{myname}.servicebus.windows.net`.

pedido de Olá pode conter arbitrários Extras os cabeçalhos de HTTP, incluindo aqueles definido pela aplicação. Todos os fornecido o serviço de escuta do cabeçalhos fluxo toohello e pode ser encontrados no Olá `connectHeader` objeto do Olá **aceitar** mensagem de controlo.

Opções de parâmetro de cadeia de consulta Olá são os seguintes:

| Param | Necessário? | Descrição |
| --- | --- | --- |
| `sb-hc-action` |Sim |Para a função de remetente Olá, Olá parâmetro tem de ser `action=connect`. |
| `{path}` |Sim |(consulte Olá seguir parágrafo) |
| `sb-hc-token` |Sim\* |Olá serviço de escuta tem de fornecer um válido, com codificação URL Service Bus partilhado acesso Token para Olá espaço de nomes ou da ligação híbrida que confers Olá **enviar** à direita. |
| `sb-hc-id` |Não |Um ID opcional que permite o rastreio de diagnóstico ponto a ponto e é tornado disponível toohello escuta durante Olá aceitar handshake. |

Olá `{path}` é o caminho de espaço de nomes com codificação URL Olá de Olá pré-configuradas da ligação híbrida no qual tooregister neste serviço de escuta. Olá `path` expressão pode ser expandida com um sufixo e um toocommunicate de expressão de cadeia de consulta mais. Se Olá da ligação híbrida estiver registado no caminho de Olá `hyco`, Olá `path` expressão pode ser `hyco/suffix?param=value&...` seguido de parâmetros de cadeia de consulta de Olá definidos aqui. Uma expressão completa, em seguida, pode ser da seguinte forma:

```
wss://{namespace-address}/$hc/hyco/suffix?param=value&sb-hc-action=...[&sb-hc-id=...&]sbc-hc-token=...
```

Olá `path` expressão é transmitida através do serviço de escuta de toohello endereço Olá URI contido na mensagem de controlo "aceitar" Olá.

Se Olá ligação de WebSocket falhar devido um caminho de ligação híbrida toohello não registada, um token inválido ou em falta ou alguns outros erros, comentários de erro Olá é fornecido com modelo de comentários de estado Olá regular HTTP 1.1. A descrição de estado contém um erro de controlo ID que pode ser comunicada ao pessoal de suporte do Azure:

| Código | Erro | Descrição |
| --- | --- | --- |
| 404 |Não foi encontrado |caminho de ligação híbrida Olá é inválido ou o URL de base de Olá tem um formato incorreto. |
| 401 |Não autorizado |token de segurança de Olá está em falta ou com formato incorreto ou é inválido. |
| 403 |Proibido |o token de segurança de Olá não é válido para este caminho e para esta ação. |
| 500 |Erro interno |Ocorreu um erro no serviço de Olá. |

Se Olá ligação de WebSocket intencionalmente é encerrado pelo serviço de Olá depois de esta foi inicialmente configurada, razão Olá para fazê-lo, por isso, é comunicado utilizando um código de erro de protocolo de WebSocket adequado, juntamente com uma mensagem de erro descritivo também inclui um ID do controlo.

| Estado de WS | Descrição |
| --- | --- |
| 1000 |serviço de escuta de Olá encerrar socket Olá. |
| 1001 |caminho de ligação híbrida Olá foi eliminado ou desativado. |
| 1008 |token de segurança de Olá expirou, se, por conseguinte, a política de autorização de Olá é violada. |
| 1011 |Ocorreu um erro no serviço de Olá. |

## Passos seguintes
* [FAQ de Reencaminhamento](relay-faq.md)
* [Criar um espaço de nomes](relay-create-namespace-portal.md)
* [Introdução ao .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Introdução ao Node](relay-hybrid-connections-node-get-started.md)

