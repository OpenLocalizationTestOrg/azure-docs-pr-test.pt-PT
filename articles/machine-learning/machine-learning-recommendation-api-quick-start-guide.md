---
title: "Início rápido: Azure recomendações API do Machine Learning (ver. 1) | Microsoft Docs"
description: "Do Azure Machine Learning recomendações - guia de introdução"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 5bce1a4a-1ad6-473f-812b-84f800fdc09a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d8f98e85f723a1104cb169b26d797934140979f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="quick-start-guide-for-hello-machine-learning-recommendations-api-version-1"></a>Guia de introdução para Olá API do Machine Learning recomendações (versão 1)

> [!NOTE]
> Deve começar a utilizar Olá [recomendações API cognitivos serviço](https://www.microsoft.com/cognitive-services/recommendations-api) em vez de nesta versão. Olá serviço cognitivos recomendações irá substituir este serviço e todas as novas funcionalidades de Olá irão ser desenvolvidas não existe. Tem novas capacidades, como a criação de batches de suporte, melhor Explorador de API, uma experiência de inscrição/faturação superfície, mais consistente de API limpeza, etc.
>
> Saiba mais sobre [migrar toohello novo serviço cognitivos](http://aka.ms/recomigrate).
> 
> 

Este documento descreve como tooonboard toouse a aplicação ou serviço Microsoft Azure Machine Learning recomendações. Pode encontrar mais detalhes sobre Olá API de recomendações na Olá [galeria da Cortana Intelligence](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a>Descrição geral do geral
toouse recomendações do Azure Machine Learning, terá de Olá tootake os seguintes passos:

* Criar um modelo - um modelo é um contentor dos seus dados de utilização, dados do catálogo e modelo de recomendação Olá.
* Importar dados de catálogo - um catálogo contém informações de metadados em itens de Olá. 
* Importar dados de utilização - dados de utilização podem ser carregados uma de duas formas (ou ambos):
  * Através do carregamento de um ficheiro que contém dados de utilização de Olá.
  * Através do envio de eventos de aquisição de dados.
    Normalmente, pode carregar um ficheiro de utilização na ordem toobe capaz de toocreate um modelo de recomendação inicial (arranque de configuração) e utilizá-lo até que o sistema de Olá reúne dados suficientes utilizando o formato de aquisição de dados de Olá.
* Criar um modelo de recomendação - esta é uma operação assíncrona no qual Olá sistema recomendação demora todos os dados de utilização de Olá e cria um modelo de recomendação. Esta operação pode demorar alguns minutos ou várias horas, consoante Olá tamanho dos dados de Olá e Olá compilar parâmetros de configuração. Quando a acionar a compilação de Olá, receberá um ID de compilação. Utilizá-lo toocheck quando o processo de compilação de Olá terminou antes de iniciar tooconsume recomendações.
* Consuma recomendações - Get recomendações para um item específico ou a lista de itens.

Todos os passos de Olá acima são efetuados através de Olá API do Azure Machine Learning recomendações.  Pode transferir uma aplicação de exemplo que implementa cada um destes passos de Olá [Galeria bem.](http://1drv.ms/1xeO2F3)

## <a name="limitations"></a>Limitações
* Olá número máximo de modelos por subscrição é 10.
* Olá o número máximo de itens que pode conter um catálogo é 100 000.
* número máximo de Olá de pontos de utilização que são mantidos é ~ 5,000,000. Olá mais antigo será eliminado se novos serão carregados ou comunicados.
* tamanho máximo do Olá dos dados que podem ser enviados em POST (por exemplo, importar dados do catálogo, importar dados de utilização) é 200MB.
* Olá número de transações por segundo para uma compilação de modelo de recomendação que não está ativa é ~ 2TPS. Uma compilação de modelo de recomendação está ativa pode manter cópias de segurança too20TPS.

## <a name="integration"></a>Integração
### <a name="authentication"></a>Autenticação
Microsoft Azure Marketplace suporta qualquer um dos Olá método de autenticação básica ou de OAuth. Pode localizar facilmente Olá chaves de conta, navegando toohello chaves no marketplace, Olá em [definições da sua conta](https://datamarket.azure.com/account/keys). 

#### <a name="basic-authentication"></a>Autenticação básica
Adicione cabeçalho de autorização de Olá:

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

Converter tooBase64 (c#)

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

Converter tooBase64 (JavaScript)

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a>URI do serviço
URI de raiz de serviço Olá para Olá recomendações APIs do Azure Machine Learning é [aqui.](https://api.datamarket.azure.com/amla/recommendations/v2/)

URI do serviço completo Olá é expresso utilizando os elementos de especificação do OData Olá.

### <a name="api-version"></a>Versão de API
Cada chamada à API será de ter, no final de Olá, um parâmetro de consulta denominado apiVersion que deve ser definido demasiado "1.0".

### <a name="ids-are-case-sensitive"></a>Os iDs de são sensíveis a maiúsculas
IDs, devolvidos por qualquer um dos Olá APIs, são maiúsculas e minúsculas e devem ser utilizados como tal, ao transmitido como parâmetros subsequentes chamadas de API. Por exemplo, IDs de modelo e os IDs de catálogo diferenciam maiúsculas de minúsculas.

### <a name="create-a-model"></a>Criar um modelo
Criar um pedido de "Criar modelo de":

| Método de HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores válidos |
|:--- |:--- |
| modelName |Apenas letras (A-Z, a-z), números (0-9), hífenes (-) e caráter de sublinhado (_) são permitidos.<br>Comprimento máximo: 20 |
| apiVersion |1.0 |
|  | |
| Corpo do Pedido |NENHUM |

**Resposta**:

Código de estado HTTP: 200

* `feed/entry/content/properties/id`-Contém o ID de modelo Olá.
  Tenha em atenção que o ID de modelo de Olá maiúsculas e minúsculas.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-catalog-data"></a>Importar dados de catálogo
Se carregar várias catálogo ficheiros toohello mesmo modelo com várias chamadas, iremos irá inserir apenas Olá novos itens de catálogo. Itens existentes permanecerá com valores originais Olá.

| Método de HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de Olá (maiúsculas e minúsculas) |
| nome de ficheiro |Identificador de textual do catálogo de Olá.<br>Apenas letras (A-Z, a-z), números (0-9), hífenes (-) e caráter de sublinhado (_) são permitidos.<br>Comprimento máximo: 50 |
| apiVersion |1.0 |
|  | |
| Corpo do Pedido |Catálogo de dados. Formato:<br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th>Nome</th><th>Obrigatório</th><th>Tipo</th><th>Descrição</th></tr><tr><td>Id do item</td><td>Sim</td><td>Comprimento máximo, alfanumérico 50</td><td>Identificador exclusivo de um item</td></tr><tr><td>Nome do item</td><td>Sim</td><td>Comprimento máximo, alfanumérico 255</td><td>Nome do item</td></tr><tr><td>Categoria do item</td><td>Sim</td><td>Comprimento máximo, alfanumérico 255</td><td>Toowhich categoria que este item pertence (por exemplo, Cooking Books, Drama...)</td></tr><tr><td>Descrição</td><td>Não</td><td>Comprimento máximo, alfanumérico 4000</td><td>Descrição deste item</td></tr></table><br>Tamanho máximo do ficheiro é de 200MB.<br><br>Exemplo:<br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

**Resposta**:

Código de estado HTTP: 200

* `Feed\entry\content\properties\LineCount`-Aceite número de linhas.
* `Feed\entry\content\properties\ErrorCount`-Número de linhas que não foram inseridos devido a erro de tooan.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
          <subtitle type="text">Import catalog file</subtitle>
          <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:58:04Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">ImportCatalogFileEntity2</title>
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">4</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-usage-data"></a>Importar dados de utilização
#### <a name="uploading-a-file"></a>Carregar um ficheiro
Esta secção mostra como dados de utilização de tooupload utilizando um ficheiro. Pode chamar esta API várias vezes com dados de utilização. Todos os dados de utilização serão guardados para todas as chamadas.

| Método de HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de Olá (maiúsculas e minúsculas) |
| nome de ficheiro |Identificador de textual do catálogo de Olá.<br>Apenas letras (A-Z, a-z), números (0-9), hífenes (-) e caráter de sublinhado (_) são permitidos.<br>Comprimento máximo: 50 |
| apiVersion |1.0 |
|  | |
| Corpo do Pedido |Dados de utilização. Formato:<br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th>Nome</th><th>Obrigatório</th><th>Tipo</th><th>Descrição</th></tr><tr><td>Id de utilizador</td><td>Sim</td><td>Alfanumérica</td><td>Identificador exclusivo de um utilizador</td></tr><tr><td>Id do item</td><td>Sim</td><td>Comprimento máximo, alfanumérico 50</td><td>Identificador exclusivo de um item</td></tr><tr><td>Hora</td><td>Não</td><td>Data no formato: aaaa/MM/ddTHH (por exemplo, 2013/06/20T10:00:00)</td><td>Hora de dados</td></tr><tr><td>Evento</td><td>Não, se for fornecido, em seguida, também deve colocar data</td><td>Um dos seguintes Olá:<br>• Clique<br>• RecommendationClick<br>• AddShopCart<br>• RemoveShopCart<br>• Compra</td><td></td></tr></table><br>Tamanho máximo do ficheiro é de 200MB.<br><br>Exemplo:<br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

**Resposta**:

Código de estado HTTP: 200

* `Feed\entry\content\properties\LineCount`-Aceite número de linhas.
* `Feed\entry\content\properties\ErrorCount`-Número de linhas que não foram inseridos devido a erro de tooan.
* `Feed\entry\content\properties\FileId`-Identificador do ficheiro.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="using-data-acquisition"></a>Utilizar a aquisição de dados
Esta secção mostra como eventos toosend real tempo tooAzure Machine Learning as recomendações, normalmente, a partir do seu Web site.

| Método de HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores válidos |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| Corpo do pedido |Entrada de dados de eventos para cada evento pretende toosend. Deve enviar para hello mesma sessão de utilizador ou browser Olá mesmo ID no campo de SessionId Olá. (Consulte o exemplo de corpo de evento abaixo). |

* Exemplo para o evento 'Clique':
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* Exemplo para o evento 'RecommendationClick':
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* Exemplo para o evento 'AddShopCart':
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* Exemplo para o evento 'RemoveShopCart':
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RemoveShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* Exemplo para o evento 'Compra':
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
            <Name>Purchase</Name> 
            <PurchaseItems>
            <PurchaseItems>
                <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                <Count>3</Count>
            </PurchaseItems>
        </PurchaseItems>
        </EventData>
        </EventData>
        </Event>
* Exemplo a enviar 2 eventos, 'clique em' e 'AddShopCart':
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

**Resposta**: código de estado HTTP: 200

### <a name="build-a-recommendation-model"></a>Criar um modelo de recomendação
| Método de HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de Olá (maiúsculas e minúsculas) |
| userDescription |Identificador de textual do catálogo de Olá. Tenha em atenção que se utilizar os espaços de tem codificá-lo com o % 20 em vez disso. Consulte o exemplo acima.<br>Comprimento máximo: 50 |
| apiVersion |1.0 |
|  | |
| Corpo do Pedido |NENHUM |

**Resposta**:

Código de estado HTTP: 200

Esta é uma API assíncrona. Irá obter um ID de compilação como resposta. tooknow quando terminou compilação Olá, deve chamar a API de "Obter compilações do Estado de um modelo" Olá e localizar este ID de compilação na resposta Olá. Tenha em atenção que uma compilação pode demorar entre toohours minutos consoante o tamanho dos dados de Olá Olá.

Não é possível consumir recomendações até Olá criar termina.

Estado de compilação válido:

* Criar – modelo foi criado.
* Em fila – compilação do modelo foi acionada e é colocada na fila.
* Edifício – modelo está a ser criado.
* Êxito – compilação terminada com êxito.
* Erro-compilação terminou com uma falha.
* Compilação cancelada – foi cancelada.
* Cancelar – compilação que está a ser cancelada.

Tenha em atenção que compilação Olá que ID pode ser encontrado em Olá seguinte caminho:`Feed\entry\content\properties\Id`

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="get-build-status-of-a-model"></a>Obter o estado de compilação de um modelo
| Método de HTTP | URI |
|:--- |:--- |
| INTRODUÇÃO |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de Olá (maiúsculas e minúsculas) |
| onlyLastBuild |Indica se o tooreturn todas Olá criar histórico do modelo de Olá ou apenas Olá estado de compilação mais recente Olá. |
| apiVersion |1.0 |

**Resposta**:

Código de estado HTTP: 200

resposta Olá inclui uma entrada por compilação. Cada entrada tem Olá dados os seguintes:

* `feed/entry/content/properties/UserName`– O nome de utilizador de Olá.
* `feed/entry/content/properties/ModelName`– O nome do modelo de Olá.
* `feed/entry/content/properties/ModelId`– Identificador exclusivo modelo.
* `feed/entry/content/properties/IsDeployed`– Indica se a compilação de Olá é implementada (a.k.a. compilação do Active Directory).
* `feed/entry/content/properties/BuildId`– Crie Identificador exclusivo.
* `feed/entry/content/properties/BuildType`-Tipo de compilação de Olá.
* `feed/entry/content/properties/Status`– Estado de compilação. Pode ser um dos seguintes Olá: erro de criação, em fila, Canceling, cancelado, êxito
* `feed/entry/content/properties/StatusMessage`– Mensagem de estado detalhado (aplica-se apenas toospecific Estados).
* `feed/entry/content/properties/Progress`– Crie progresso (%).
* `feed/entry/content/properties/StartTime`– Hora de início de compilação.
* `feed/entry/content/properties/EndTime`– Hora de fim de compilação.
* `feed/entry/content/properties/ExecutionTime`– Crie duração.
* `feed/entry/content/properties/ProgressStep`– Detalhes sobre a fase de atual Olá que está a ser uma compilação em curso.

Estado de compilação válido:

* Criado – foi criada a entrada de pedido de compilação.
* Em fila – compilação pedido foi acionado e é colocada na fila.
* Edifício – compilação está em curso.
* Êxito – compilação terminada com êxito.
* Erro-compilação terminou com uma falha.
* Compilação cancelada – foi cancelada.
* Cancelar – compilação que está a ser cancelada.

Valores válidos para o tipo de compilação:

* Classificação - a posição da compilação. (Para a posição da compilação detalhes, consulte o documento de "Documentação de Machine Learning recomendação API" toohello.)
* Recomendação - compilação de recomendação.
* Fbt - comprou com frequência, em conjunto compilação.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get builds status of a model</subtitle>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetBuildsStatusEntity</title>
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
        <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
        <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
        <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
        <d:BuildId m:type="Edm.String">1000272</d:BuildId>
        <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
        <d:Status m:type="Edm.String">Success</d:Status>
        <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
        <d:Progress m:type="Edm.String">0</d:Progress>
        <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
        <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
        <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
        <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
        <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
      </m:properties>
     </content>
    </entry>
    </feed>


### <a name="get-recommendations"></a>Obtenha recomendações
| Método de HTTP | URI |
|:--- |:--- |
| INTRODUÇÃO |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de Olá (maiúsculas e minúsculas) |
| itemIds |Lista separada por vírgulas de Olá itens toorecommend para.<br>Comprimento máximo: 1024 |
| numberOfResults |Número de resultados necessários |
| includeMetatadata |Utilização futura, sempre falsa |
| apiVersion |1.0 |

**Resposta:**

Código de estado HTTP: 200

resposta Olá inclui uma entrada por item recomendada. Cada entrada tem Olá dados os seguintes:

* `Feed\entry\content\properties\Id`-ID do item recomendado.
* `Feed\entry\content\properties\Name`-Nome do item de Olá.
* `Feed\entry\content\properties\Rating`-Classificação recomendação Olá; número mais alto significa maior confiança.
* `Feed\entry\content\properties\Reasoning`-Raciocínio recomendação (por exemplo, explicações recomendação).

XML de OData

resposta de exemplo de Olá abaixo inclui 10 itens recomendados:

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="update-model"></a>Modelo de atualização
Pode atualizar a descrição do modelo Olá ou Olá ID de compilação do Active Directory.
*ID de compilação do Active Directory* -cada compilação para cada modelo tem um ID de compilação. ID de compilação do Active Directory Olá é compilação efetuada com êxito primeiro Olá de cada novo modelo. Depois de ter um ID de compilação do Active Directory e fazer compilações adicionais para Olá mesmo modelo, terá de tooexplicitly defini-lo como hello predefinido criar ID se pretender. Quando consumir recomendações, se não especificar ID de compilação de Olá que pretende que sejam toouse, Olá um será utilizado o predefinido automaticamente.

Este mecanismo permite-lhe - depois de ter um modelo de recomendação em produção - modelos novo toobuild e testá-los antes de promovê-los tooproduction.

| Método de HTTP | URI |
|:--- |:--- |
| COLOCAR |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores válidos |
|:--- |:--- |
| ID |Identificador exclusivo do modelo de Olá (maiúsculas e minúsculas) |
| apiVersion |1.0 |
|  | |
| Corpo do Pedido |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br>Tenha em atenção que a descrição de etiquetas de Olá XML e ActiveBuildId são opcionais. Se não pretender tooset descrição ou ActiveBuildId, remova etiqueta Olá de todo. |

**Resposta**:

Código de estado HTTP: 200

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a>Informações Legais
Este documento é fornecido "como-é". As informações e opiniões expressados neste documento, incluindo URLs e outras referências de Web site da Internet, podem ser alteradas sem aviso prévio. Alguns exemplos aqui demonstrados são fornecidos para apenas ilustração e são fictícios. Nenhuma associação ou ligação é intencional nem deve ser inferida. Este documento não fornece-lhe direitos de propriedade intelectual de tooany em qualquer produto da Microsoft. Pode copiar e utilizar este documento interna, para efeitos de consulta. © 2014 Microsoft. Todos os direitos reservados. 

