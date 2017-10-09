---
title: "aaaStore dados não estruturados com as funções do Azure e a base de dados do Cosmos"
description: "Armazenar dados não estruturados usando as funções do Azure e o Cosmos DB"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: "funções do azure, funções, processamento de eventos, Cosmos DB, computação dinâmica, arquitetura sem servidor"
ms.assetid: 
ms.service: functions
ms.devlang: csharp
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 48d6899c20d3e6f6b062725fca329972ead3c696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="store-unstructured-data-using-azure-functions-and-cosmos-db"></a>Armazenar dados não estruturados usando as funções do Azure e o Cosmos DB

[BD do Azure do Cosmos](https://azure.microsoft.com/services/cosmos-db/) é uma excelente forma toostore não estruturado e dados JSON. Combinado com funções do Azure, o Cosmos DB torna o armazenamento de dados rápido e fácil, sendo necessário menos códigos para armazenar dados numa base de dados relacional.

As funções do Azure, enlaces de entrada e de saída fornecem uma forma declarativa tooconnect tooexternal serviço de dados da sua função. Neste tópico, saiba como tooupdate um existente c# funcionar tooadd um enlace de saída que armazena dados não estruturados um documento de BD do Cosmos. 

![Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-cosmosdb.png)

## <a name="prerequisites"></a>Pré-requisitos

toocomplete neste tutorial:

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

## <a name="add-an-output-binding"></a>Adicionar um enlace de saída

1. Expanda a aplicação Function App e a função.

1. Selecione **integrar** e **+ nova saída**, que é em Olá principais lado direito da página Olá. Escolha **Azure Cosmos DB** e clique em **Selecionar**.

    ![Adicionar um enlace de saída do Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-add-new-output-binding.png)

3. Olá utilize **saída de base de dados do Azure Cosmos** definições conforme especificado na tabela de Olá: 

    ![Configurar o enlace de saída do Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-configure-cosmosdb-binding.png)

    | Definição      | Valor sugerido  | Descrição                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | **Nome do parâmetro do documento** | taskDocument | Nome que referencia o objeto de base de dados do Cosmos toohello no código. |
    | **Nome da base de dados** | taskDatabase | Nome de documentos de toosave de base de dados. |
    | **Nome da coleção** | TaskCollection | Nome da coleção de bases de dados do Cosmos DB. |
    | **Se for VERDADEIRO, cria a base de dados do Olá Cosmos base de dados e coleção** | Assinalado | coleção de Olá não já existe, pelo que criá-la. |

4. Selecione **novo** toohello seguinte **ligação de documento do Cosmos DB** etiqueta e selecione **+ criar nova**. 

5. Olá utilize **nova conta** definições conforme especificado na tabela de Olá: 

    ![Configurar a ligação ao Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-create-CosmosDB.png)

    | Definição      | Valor sugerido  | Descrição                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | **ID** | Nome da base de dados | ID exclusivo para a base de dados do Olá Cosmos DB  |
    | **API** | SQL (DocumentDB) | Selecione a API de base de dados de documento Olá.  |
    | **Subscrição** | Subscrição do Azure | Subscrição do Azure  |
    | **Grupo de Recursos** | myResourceGroup |  Utilize Olá grupo de recursos existente que contenha a aplicação de função. |
    | **Localização**  | WestEurope | Selecione uma localização perto tooeither a sua aplicação de função ou tooother aplicações que utilizam Olá documentos armazenados.  |

6. Clique em **OK** base de dados do toocreate Olá. Pode demorar alguns minutos toocreate Olá base de dados. Depois de criar a base de dados de Olá, cadeia de ligação de base de dados de Olá é armazenada como uma definição de aplicação de função. nome de Olá desta definição de aplicação é inserido no **ligação de conta de base de dados do Cosmos**. 
 
8. Depois de definir a cadeia de ligação de Olá, selecione **guardar** enlace de Olá toocreate.

## <a name="update-hello-function-code"></a>Atualizar o código de função Olá

Substitua Olá c# função código existente pelo Olá seguinte código:

```csharp
using System.Net;

public static HttpResponseMessage Run(HttpRequestMessage req, out object taskDocument, TraceWriter log)
{
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    string task = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "task", true) == 0)
        .Value;

    string duedate = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "duedate", true) == 0)
        .Value;

    taskDocument = new {
        name = name,
        duedate = duedate.ToString(),
        task = task
    };

    if (name != "" && task != "") {
        return req.CreateResponse(HttpStatusCode.OK);
    }
    else {
        return req.CreateResponse(HttpStatusCode.BadRequest);
    }
}

```
Este exemplo de código lê Olá pedido HTTP cadeias de consulta e atribui-las toofields no Olá `taskDocument` objeto. Olá `taskDocument` enlace envia dados de objeto Olá deste toobe de parâmetro de enlace armazenado na base de dados de documento vinculada de Olá. base de dados de Olá criada Olá pela primeira vez Olá função é executada.

## <a name="test-hello-function-and-database"></a>Função de Olá de teste e a base de dados

1. Expanda a janela de direito de Olá e selecione **teste**. Em **consulta**, clique em **+ Adicionar parâmetro** e adicione Olá seguinte cadeia de consulta de toohello parâmetros:

    + `name`
    + `task`
    + `duedate`

2. Clique em **Executar** e certifique-se de que é devolvido um estado 200.

    ![Configurar o enlace de saída do Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-test-function.png)

1. No Olá à esquerda do lado do Olá portal do Azure, expanda a barra de ícone de Olá, tipo `cosmos` na Olá procure campo e selecione **Azure Cosmos DB**.

    ![Procurar Olá serviço Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-search-cosmos-db.png)

2. Base de dados de Olá selecione que criou, em seguida, selecione **Explorador de dados**. Expanda Olá **coleções** nós, selecione o novo documento de Olá e confirme esse documento Olá contém os valores de cadeia de consulta, juntamente com alguns metadados adicionais. 

    ![Verifique a entrada no Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-verify-cosmosdb-output.png)

Adicionou com êxito um acionador HTTP do enlace tooyour que armazena dados não estruturados numa base de dados de base de dados do Cosmos.

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Passos seguintes

[!INCLUDE [functions-quickstart-next-steps](../../includes/functions-quickstart-next-steps.md)]

Para obter mais informações sobre a base de dados do enlace tooa Cosmos DB, consulte [enlaces de base de dados do Azure funções Cosmos](functions-bindings-documentdb.md).
