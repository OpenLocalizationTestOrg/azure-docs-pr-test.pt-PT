---
title: aaaAzure Cosmos DB Node.js API, SDK & recursos | Microsoft Docs
description: "Saiba tudo sobre Olá Node.js API e SDK, incluindo as datas de versão, datas de extinção e as alterações efetuadas entre cada versão do Olá SDK Node.js do Azure Cosmos DB."
services: cosmos-db
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d450b9a9ea7b0f4717ddae8940121fc458ea3744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a>Azure SDK Node.js do Cosmos DB: Notas de versão e recursos
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [Feed de alteração de .NET](documentdb-sdk-dotnet-changefeed.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.js](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/documentdb/)
> * [Fornecedor de Recursos REST](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td>**Transferir o SDK**</td><td>[NPM](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td>**Documentação da API**</td><td>[Documentação de referência de API node.js](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td>**Instruções de instalação do SDK**</td><td>[Instruções de instalação](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td>**Contribuir tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td>**Amostras**</td><td>[Exemplos de código do node.js](documentdb-nodejs-samples.md)</td></tr>

<tr><td>**Tutorial de introdução**</td><td>[Introdução ao hello Node.js SDK](documentdb-nodejs-get-started.md)</td></tr>

<tr><td>**Tutorial de aplicação Web**</td><td>[Criar uma aplicação de web do Node.js utilizando o Azure Cosmos DB](documentdb-nodejs-application.md)</td></tr>

<tr><td>**Plataforma suportada atual**</td><td> 
[V6. x do node.js](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[NODE.js v4.2.0](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[NODE.js v0.12](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
[NODE.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</td></tr>
</table></br>

## <a name="release-notes"></a>Notas de versão

### <a name="1.12.2"/>1.12.2</a>
*   documentação de npm for corrigida.

### <a name="1.12.1"/>1.12.1</a>
* Corrigido um erro no executeStoredProcedure onde documentos envolvidos tinham carateres Unicode especiais (LS, PS).
* Corrigido um erro no processamento de documentos com a chave de partição Olá carateres Unicode.
* Suporte fixo para criação de coleções com suporte de dados de nome de Olá. Problema de Github #114.
* Suporte fixo para o token de autorização de permissão. Problema de Github #178.

### <a name="1.12.0"/>1.12.0</a>
* Foi adicionado suporte para um novo [nível de consistência](consistency-levels.md) chamado ConsistentPrefix.
* Suporte adicionado para UriFactory.
* Corrigido um erro de suporte de Unicode. Problema de GitHub #171.

### <a name="1.11.0"/>1.11.0</a>
* Suporte adicionado Olá para consultas de agregação (CONTAGEM, MIN, MAX, soma e média).
* Opção de Olá foram adicionadas para controlar o grau de paralelismo para entre consultas de partição.
* Opção de Olá adicionado para desativar a verificação de SSL quando em execução contra o emulador de BD do Cosmos do Azure.
* Lowered débito mínimo em coleções particionadas de 10,100 RU/s too2500 RU/s.
* Erros de hora token do continuação Olá fixo para a coleção de partições únicas. Problema de Github #107.
* Erros de executeStoredProcedure Olá fixo processar 0 como param único. Problema de Github #155.

### <a name="1.10.2"/>1.10.2</a>
* Versão do agente de utilizador fixo cabeçalho tooinclude Olá SDK.
* Limpeza de código secundárias.

### <a name="1.10.1"/>1.10.1</a>
* Quando utilizar Olá SDK tootarget Olá emulator(hostname=localhost) a desativar a verificação de SSL.
* Suporte adicionado para ativar o registo de script durante a execução do procedimento armazenado.

### <a name="1.10.0"/>1.10.0</a>
* Suporte adicionado para entre consultas paralelas de partição.
* Suporte adicionado para consultas de parte superior/ORDER BY para coleções particionadas.

### <a name="1.9.0"/>1.9.0</a>
* Suporte de política de repetição adicionado para pedidos otimizados. (Pedidos otimizados recebem uma pedido taxa demasiado grande exceção, o código de erro 429.) Por predefinição, base de dados do Azure Cosmos repete nove vezes para cada pedido quando for detetado o código de erro 429, para respeitar o tempo de retryAfter Olá no cabeçalho de resposta de Olá. Um período de tempo do intervalo de repetição fixo pode agora ser definido como parte da Olá RetryOptions propriedade no objecto de ConnectionPolicy Olá se pretender que o tempo de retryAfter tooignore Olá devolvido pelo servidor entre repetições Olá. BD do Azure do Cosmos aguarda agora um máximo de 30 segundos para cada pedido que está a ser limitado (independentemente da contagem de repetições) e devolve a resposta de Olá com o código de erro 429. Neste momento também pode ser substituído na Olá RetryOptions propriedade ConnectionPolicy objeto.
* BD do cosmos devolve agora x-ms-limitação--contagem de repetições e x-ms-throttle-retry-wait-time-ms como cabeçalhos de resposta de Olá em cada limitação do pedido toodenote Olá Repetir contagem e Olá cumulativo tempo do pedido Olá aguardaram entre repetições Olá.
* foi adicionado Olá RetryOptions classe, a exposição de propriedade de RetryOptions Olá na classe de ConnectionPolicy Olá que pode ser utilizado toooverride algumas das predefinido Olá as opções de repetição.

### <a name="1.8.0"/>1.8.0</a>
* Suporte adicionado Olá para contas de multirregião base de dados.

### <a name="1.7.0"/>1.7.0</a>
* Olá adicionado suporte para a funcionalidade de tooLive(TTL) de tempo para documentos.

### <a name="1.6.0"/>1.6.0</a>
* Implementado [particionada coleções](partition-data.md) e [níveis de desempenho definido pelo utilizador](performance-levels.md).

### <a name="1.5.6"/>1.5.6</a>
* Erros de RangePartitionResolver.resolveForRead fixo onde não foi devolver ligações devido tooa concat incorreto de resultados.

### <a name="1.5.5"/>1.5.5</a>
* Corrigido hashParitionResolver resolveForRead(): quando nenhuma chave de partição fornecido foi gerar exceção, em vez de devolver uma lista de todas as ligações registadas.

### <a name="1.5.4"/>1.5.4</a>
* Corrige o problema [#100](https://github.com/Azure/azure-documentdb-node/issues/100) -agente dedicado de HTTPS: evitar modificar agente global de Olá para fins de BD do Cosmos do Azure. Utilize um agente dedicado para todos os pedidos do lib Olá.

### <a name="1.5.3"/>1.5.3</a>
* Corrige o problema [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - corretamente processar travessões no ID de suporte de dados.

### <a name="1.5.2"/>1.5.2</a>
* Corrige o problema [#95](https://github.com/Azure/azure-documentdb-node/issues/95) -EventEmitter escuta fuga de aviso.

### <a name="1.5.1"/>1.5.1</a>
* Corrige o problema [#92](https://github.com/Azure/azure-documentdb-node/issues/90) -mudar o nome de pasta Hash toohash para sistemas de maiúsculas e minúsculas.

### <a name="1.5.0"/>1.5.0</a>
* Suporte de fragmentação de implementar, adicionando as resoluções de hash & ntervalo de datas da partição.

### <a name="1.4.0"/>1.4.0</a>
* Implemente Upsert. Novo upsertXXX os métodos no documentClient.

### <a name="1.3.0"/>1.3.0</a>
* Ignorado toobring números de versão em alinhamento com outros SDKs.

### <a name="1.2.2"/>1.2.2</a>
* Divisão Q promete repositório de toonew wrapper.
* Atualize o ficheiro de toopackage para registo de npm.

### <a name="1.2.1"/>1.2.1</a>
* Implementa o ID de encaminhamento com base.
* Corrige o problema [#49](https://github.com/Azure/azure-documentdb-node/issues/49) -propriedade atual está em conflito com current () do método.

### <a name="1.2.0"/>1.2.0</a>
* Suporte adicionado para o índice de Geoespacial.
* Valida a propriedade id de todos os recursos. Os IDs de recursos não podem conter?, /, # &#47; &#47; carateres nem terminar com um espaço.
* Adiciona tooResourceResponse de "progresso de transformação de índice" do novo cabeçalho.

### <a name="1.1.0"/>1.1.0</a>
* Implementa a política de indexação V2.

### <a name="1.0.3"/>1.0.3</a>
* Problema [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - implementado eslint grunt configurações de núcleos de Olá e promessa SDK.

### <a name="1.0.2"/>1.0.2</a>
* Problema [#45](https://github.com/Azure/azure-documentdb-node/issues/45) -Promises wrapper não inclui um cabeçalho com o erro.

### <a name="1.0.1"/>1.0.1</a>
* Implementado tooquery de capacidade para conflitos adicionando readConflicts, readConflictAsync e queryConflicts.
* Documentação da API atualizada.
* Problema [#41](https://github.com/Azure/azure-documentdb-node/issues/41) -client.createDocumentAsync erro.

### <a name="1.0.0"/>1.0.0</a>
* GA SDK.

## <a name="release--retirement-dates"></a>Datas de extinção & versão
A Microsoft disponibiliza notificação, pelo menos, **12 meses** previamente extinguir um SDK na ordem toosmooth Olá transição tooa/suportada mais recente versão.

Apenas são adicionadas novas funcionalidades e a funcionalidade e otimizações o atual toohello SDK, como tal, é recomendado que lhe toohello sempre atualização mais recente versão do SDK antecipadamente quanto possível.

Qualquer pedido tooCosmos BD utilizando um SDK extinto é rejeitadas pelo serviço de Olá.

<br/>

| Versão | Data da versão | Data de retirada |
| --- | --- | --- |
| [1.12.2](#1.12.2) |10 de Agosto de 2017 |--- |
| [1.12.1](#1.12.1) |10 de Agosto de 2017 |--- |
| [1.12.0](#1.12.0) |10 de maio de 2017 |--- |
| [1.11.0](#1.11.0) |16 de Março de 2017 |--- |
| [1.10.2](#1.10.2) |27 de Janeiro de 2017 |--- |
| [1.10.1](#1.10.1) |22 de Dezembro de 2016 |--- |
| [1.10.0](#1.10.0) |03 de Outubro de 2016 |--- |
| [1.9.0](#1.9.0) |07 de Julho de 2016 |--- |
| [1.8.0](#1.8.0) |14 de Junho de 2016 |--- |
| [1.7.0](#1.7.0) |26 de Abril de 2016 |--- |
| [1.6.0](#1.6.0) |29 de Março de 2016 |--- |
| [1.5.6](#1.5.6) |08 de Março de 2016 |--- |
| [1.5.5](#1.5.5) |02 de Fevereiro de 2016 |--- |
| [1.5.4](#1.5.4) |01 de Fevereiro de 2016 |--- |
| [1.5.2](#1.5.2) |26 de Janeiro de 2016 |--- |
| [1.5.2](#1.5.2) |22 de Janeiro de 2016 |--- |
| [1.5.1](#1.5.1) |4 de Janeiro de 2016 |--- |
| [1.5.0](#1.5.0) |31 de Dezembro de 2015 |--- |
| [1.4.0](#1.4.0) |06 de Outubro de 2015 |--- |
| [1.3.0](#1.3.0) |06 de Outubro de 2015 |--- |
| [1.2.2](#1.2.2) |10 de Setembro de 2015 |--- |
| [1.2.1](#1.2.1) |15 de Agosto de 2015 |--- |
| [1.2.0](#1.2.0) |05 de Agosto de 2015 |--- |
| [1.1.0](#1.1.0) |09 de Julho de 2015 |--- |
| [1.0.3](#1.0.3) |04 de Junho de 2015 |--- |
| [1.0.2](#1.0.2) |23 de Maio de 2015 |--- |
| [1.0.1](#1.0.1) |15 de Maio de 2015 |--- |
| [1.0.0](#1.0.0) |08 de Abril de 2015 |--- |

## <a name="faq"></a>FAQ
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Consultar também
toolearn mais informações sobre a base de dados do Cosmos, consulte [base de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página do serviço.

