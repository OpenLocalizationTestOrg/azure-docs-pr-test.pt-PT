---
title: API de Python do Cosmos DB, aaaAzure SDK & recursos | Microsoft Docs
description: "Saiba tudo sobre Olá Python API e SDK, incluindo as datas de versão, datas de extinção e as alterações efetuadas entre cada versão do Olá SDK Python do Azure Cosmos DB."
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a>SDK de Python Cosmos BD do Azure: Notas de versão e recursos
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

<tr><td>**Transferir o SDK**</td><td>[PyPI](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td>**Documentação da API**</td><td>[Documentação de referência da API de Python](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td>**Instruções de instalação do SDK**</td><td>[Instruções de instalação do Python SDK](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td>**Contribuir tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td>**Introdução**</td><td>[Introdução ao hello Python SDK](documentdb-python-application.md)</td></tr>

<tr><td>**Plataforma suportada atual**</td><td>[Python 2.7](https://www.python.org/downloads/) e [Python 3.5](https://www.python.org/downloads/)</td></tr>
</table></br>

## <a name="release-notes"></a>Notas de versão
### <a name="a-name220220"></a><a name="2.2.0"/>2.2.0
* Suporte adicionado para um novo nível de consistência chamado ConsistentPrefix.


### <a name="a-name210210"></a><a name="2.1.0"/>2.1.0
* Suporte adicionado para consultas de agregação (CONTAGEM, MIN, MAX, soma e média).
* Adicionar uma opção para desativar a verificação de SSL quando em execução contra o emulador de BD do Cosmos.
* Remover a restrição de Olá do módulo de pedidos dependentes toobe 2.10.0 exatamente.
* Lowered débito mínimo em coleções particionadas de 10,100 RU/s too2500 RU/s.
* Suporte adicionado para ativar o registo de script durante a execução do procedimento armazenado.
* Versão de REST API demasiado bumped'2017-01-19' com esta versão.

### <a name="a-name201201"></a><a name="2.0.1"/>2.0.1
* Efetuou alterações editoriais toodocumentation comentários.

### <a name="a-name200200"></a><a name="2.0.0"/>2.0.0
* Suporte adicionado para o Python 3.5.
* Suporte adicionado para utilizar um módulo de pedidos de agrupamento de ligações.
* Adicionado suporte para a consistência de sessão.
* Suporte adicionado para consultas de parte superior/ORDERBY para coleções particionadas.

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* Suporte de política de repetição adicionado para pedidos otimizados. (Pedidos otimizados recebem uma pedido taxa demasiado grande exceção, o código de erro 429.) Por predefinição, base de dados do Azure Cosmos repete nove vezes para cada pedido quando for detetado o código de erro 429, para respeitar o tempo de retryAfter Olá no cabeçalho de resposta de Olá. Um período de tempo do intervalo de repetição fixo pode agora ser definido como parte da Olá RetryOptions propriedade no objecto de ConnectionPolicy Olá se pretender que o tempo de retryAfter tooignore Olá devolvido pelo servidor entre repetições Olá. BD do Azure do Cosmos aguarda agora um máximo de 30 segundos para cada pedido que está a ser limitado (independentemente da contagem de repetições) e devolve a resposta de Olá com o código de erro 429. Neste momento também pode ser substituída no Olá RetryOptions propriedade ConnectionPolicy objeto.
* BD do cosmos devolve agora x-ms-limitação--contagem de repetições e x-ms-throttle-retry-wait-time-ms como cabeçalhos de resposta de Olá em cada limitação do pedido toodenote Olá Repetir contagem e Olá cummulative tempo do pedido Olá aguardaram entre repetições Olá.
* Classe de RetryPolicy Olá removido propriedade correspondente da Olá (retry_policy) exposta na classe de document_client Olá e introduzidas em vez disso, uma classe de RetryOptions exposição de propriedade de RetryOptions Olá na classe ConnectionPolicy que pode ser utilizado toooverride Alguns dos predefinido Olá as opções de repetição.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Suporte adicionado Olá para contas de multirregião base de dados.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Olá adicionado suporte para a funcionalidade de tooLive(TTL) de tempo para documentos.

### <a name="a-name161161"></a><a name="1.6.1"/>1.6.1
* Correções de erros relacionados com o lado tooserver tooallow carateres especiais no caminho de partitionkey de criação de partições.

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* Implementado [particionada coleções](partition-data.md) e [níveis de desempenho definido pelo utilizador](performance-levels.md). 

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Adicionar Hash & intervalo de partição resoluções tooassist com as aplicações de fragmentação através de várias partições.

### <a name="a-name142142"></a><a name="1.4.2"/>1.4.2
* Implemente Upsert. Novos métodos de UpsertXXX adicionado toosupport Upsert funcionalidade.
* ID de implementar baseado Routing. Sem alterações de API públicas, todas as alterações internas.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Índice de Geoespacial suporta.
* Valida a propriedade id de todos os recursos. Os IDs de recursos não podem conter?, /, #, \, carateres nem terminar com um espaço.
* Adiciona tooResourceResponse de "progresso de transformação de índice" do novo cabeçalho.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Implementa a política de indexação V2.

### <a name="a-name101101"></a><a name="1.0.1"/>1.0.1
* Suporta a ligação de proxy.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* GA SDK.

## <a name="release--retirement-dates"></a>Versão & extinção datas
A Microsoft vai fornecer pelo menos notificação **12 meses** previamente extinguir um SDK na ordem toosmooth Olá transição tooa/suportada mais recente versão.

Apenas são adicionadas novas funcionalidades e a funcionalidade e otimizações o atual toohello SDK, como tal, é recomendado que lhe toohello sempre atualização mais recente versão do SDK antecipadamente quanto possível. 

Qualquer tooCosmos pedido BD utilizando um SDK extinto serão rejeitadas pelo serviço de Olá.

> [!WARNING]
> Todas as versões do Olá SDK do Azure DocumentDB para tooversion anterior Python **1.0.0** serão descontinuados no **29 de Fevereiro de 2016**. 
> 
> 

<br/>

| Versão | Data da versão | Data de retirada |
| --- | --- | --- |
| [2.2.0](#2.2.0) |10 de maio de 2017 |--- |
| [2.1.0](#2.1.0) |01 de Maio de 2017 |--- |
| [2.0.1](#2.0.1) |30 de Outubro de 2016 |--- |
| [2.0.0](#2.0.0) |29 de Setembro de 2016 |--- |
| [1.9.0](#1.9.0) |07 de Julho de 2016 |--- |
| [1.8.0](#1.8.0) |14 de Junho de 2016 |--- |
| [1.7.0](#1.7.0) |26 de Abril de 2016 |--- |
| [1.6.1](#1.6.1) |08 de Abril de 2016 |--- |
| [1.6.0](#1.6.0) |29 de Março de 2016 |--- |
| [1.5.0](#1.5.0) |03 de Janeiro de 2016 |--- |
| [1.4.2](#1.4.2) |06 de Outubro de 2015 |--- |
| [1.4.1](#1.4.1) |06 de Outubro de 2015 |--- |
| [1.2.0](#1.2.0) |06 de Agosto de 2015 |--- |
| [1.1.0](#1.1.0) |09 de Julho de 2015 |--- |
| [1.0.1](#1.0.1) |25 de Maio de 2015 |--- |
| [1.0.0](#1.0.0) |07 de Abril de 2015 |--- |
| 0.9.4-prelease |14 de Janeiro de 2015 |29 de Fevereiro de 2016 |
| 0.9.3-prelease |09 de Dezembro de 2014 |29 de Fevereiro de 2016 |
| 0.9.2-prelease |25 de Novembro de 2014 |29 de Fevereiro de 2016 |
| 0.9.1-prelease |23 de Setembro de 2014 |29 de Fevereiro de 2016 |
| 0.9.0-prelease |21 de Agosto de 2014 |29 de Fevereiro de 2016 |

## <a name="faq"></a>FAQ
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Consultar também
toolearn mais informações sobre a base de dados do Cosmos, consulte [base de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página do serviço. 

