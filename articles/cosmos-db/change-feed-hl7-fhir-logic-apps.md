---
title: aaaChange feed recursos HL7 FHIR - base de dados do Azure Cosmos | Microsoft Docs
description: "Saiba como tooset se alterar as notificações para HL7 FHIR patient saúde os registos com Azure Logic Apps, a base de dados do Azure Cosmos e o Service Bus."
keywords: HL7 fhir
services: cosmos-db
author: hedidin
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 0d25c11f-9197-419a-aa19-4614c6ab2d06
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: b-hoedid
ms.openlocfilehash: d2809bf5c6d8c193c49438d20684c56caea646bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a>Notificar patients das alterações de registo de saúde HL7 FHIR com Logic Apps e a base de dados do Azure Cosmos

Azure Edidin de Howard MVP recentemente foi contactado por uma organização de cuidados de saúde que pretendia tooadd nova funcionalidade tootheir patient portal. Se necessitar de toosend notificações toopatients respetivo registo de estado de funcionamento foi atualizado e necessárias patients toobe toosubscribe capaz de toothese atualizações. 

Este artigo acompanha-o através da solução de feed de notificação de alteração de Olá criada para esta organização de cuidados de saúde utilizando a BD do Cosmos do Azure, as Logic Apps e o Service Bus. 

## <a name="project-requirements"></a>Requisitos do projeto
- Fornecedores de enviam a arquitetura de documento consolidado Clinical HL7 (C-CDA) documentos no formato XML. Documentos C CDA abranger praticamente cada tipo de documento clinical, incluindo documentos clinical como histories famílias e registos de immunization, bem como administrativos, fluxo de trabalho e os documentos financeiros. 
- Documentos C CDA são convertidos demasiado[HL7 FHIR recursos](http://hl7.org/fhir/2017Jan/resourcelist.html) no formato JSON.
- Documentos de recurso FHIR modificados são enviados por correio eletrónico no formato JSON.

## <a name="solution-workflow"></a>Fluxo de trabalho da solução 

Um nível elevado, o projeto Olá necessário Olá os seguintes passos de fluxo de trabalho: 
1. Converta os recursos de tooFHIR C CDA documentos.
2. Execute o acionador recorrente de consulta para obter recursos FHIR modificados. 
2. Chame uma aplicação personalizada, FhirNotificationApi, tooconnect tooAzure Cosmos DB e consulta para documentos novos ou modificados.
3. Guarde a fila do Service Bus Olá resposta tootoohello.
4. Consulta para novas mensagens na fila do Service Bus Olá.
5. Envie toopatients de notificações de correio eletrónico.

## <a name="solution-architecture"></a>Arquitetura de solução
Esta solução requer três Olá de toomeet Logic Apps acima requisitos e fluxo de trabalho de solução de Olá concluída. as logic apps de três Olá são:
1. **Aplicação de mapeamento de FHIR HL7**: recebe o documento de HL7 C-CDA Olá, transforma-toohello FHIR recursos e guarda-o tooAzure BD do Cosmos.
2. **Aplicação EHR**: consulta o repositório de Azure Cosmos DB FHIR Olá e guarda a fila do Service Bus Olá resposta tooa. Esta aplicação lógica utiliza um [aplicação API](#api-app) tooretrieve novas e alteradas documentos.
3. **Aplicação de notificação de processo**: envia uma notificação de correio eletrónico com documentos de recursos FHIR Olá no corpo de Olá.

![Olá três Logic Apps utilizada nesta solução de cuidados de saúde HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a>Serviços do Azure utilizados na solução de Olá

#### <a name="azure-cosmos-db-documentdb-api"></a>DocumentDB do Azure Cosmos DB API
BD do Azure do Cosmos é o repositório de Olá para recursos FHIR Olá, conforme mostrado no Olá figura a seguir.

![conta de base de dados do Azure Cosmos Olá utilizada neste tutorial de cuidados de saúde HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a>Aplicações Lógicas
As Logic Apps lidar com o processo de fluxo de trabalho de Olá. Olá capturas de ecrã seguintes mostram Olá as Logic apps criadas para esta solução. 


1. **Aplicação de mapeamento de FHIR HL7**: receber o documento de HL7 C-CDA Olá e transformá-los recursos FHIR tooan utilizando Olá Enterprise Integration Pack para aplicações lógicas. Olá Enterprise Integration Pack processa Olá mapeamento da Olá recursos de tooFHIR C CDA.

    ![Olá aplicação lógica utilizada registos de cuidados de saúde tooreceive HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. **Aplicação EHR**: consultar o repositório de Azure Cosmos DB FHIR Olá e guarde Olá resposta tooa barramento de serviço fila. código de Olá Olá GetNewOrModifiedFHIRDocuments aplicação está abaixo.

    ![Olá aplicação lógica utilizada tooquery BD do Cosmos do Azure](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. **Aplicação de notificação de processo**: enviar uma notificação de correio eletrónico com documentos de recursos FHIR Olá no corpo de Olá.

    ![Olá aplicação lógica que envia correio eletrónico patient com recurso de HL7 FHIR Olá no corpo de Olá](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a>Service Bus
Olá seguinte figura mostra Olá patients fila. Olá valor de propriedade da etiqueta é utilizada para o assunto do e-mail Olá.

![Olá utilizado neste tutorial HL7 FHIR de fila do Service Bus](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a>Aplicação API
Uma aplicação API liga tooAzure Cosmos DB e consultas para novos ou modificados documentos FHIR por tipo de recurso. Esta aplicação tem um controlador, **FhirNotificationApi** com uma única operação **GetNewOrModifiedFhirDocuments**, consulte [origem para a aplicação API](#api-app-source).

Estamos a utilizar Olá [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) classe a partir de Olá Cosmos BD do DocumentDB .NET API do Azure. Para obter mais informações, consulte Olá [alteração feed artigo](change-feed.md). 

##### <a name="getnewormodifiedfhirdocuments-operation"></a>Operação GetNewOrModifiedFhirDocuments

**Entradas**
- DatabaseId
- CollectionId
- Nome de tipo de recurso de FHIR HL7
- Valor booleano: Iniciar a partir do início
- INT: Número de documentos devolvidos

**Saídas**
- Êxito: Código de estado: resposta 200,: lista de documentos (matriz JSON)
- Falha: Código de estado: respostas 404,: "não existem documentos encontrado para '*nome de recurso '* tipo de recurso"

<a id="api-app-source"></a>

**Origem da aplicação Olá API**

```C#

    using System.Collections.Generic;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Threading.Tasks;
    using System.Web.Http;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Swashbuckle.Swagger.Annotations;
    using TRex.Metadata;
    
    namespace FhirNotificationApi.Controllers
    {
        /// <summary>
        ///     FHIR Resource Type Controller
        /// </summary>
        /// <seealso cref="System.Web.Http.ApiController" />
        public class FhirResourceTypeController : ApiController
        {
            /// <summary>
            ///     Gets hello new or modified FHIR documents from Last Run Date 
            ///     or create date of hello collection
            /// </summary>
            /// <param name="databaseId"></param>
            /// <param name="collectionId"></param>
            /// <param name="resourceType"></param>
            /// <param name="startfromBeginning"></param>
            /// <param name="maximumItemCount">-1 returns all (default)</param>
            /// <returns></returns>
            [Metadata("Get New or Modified FHIR Documents",
                "Query for new or modifed FHIR Documents By Resource Type " +
                "from Last Run Date or Begining of Collection creation"
            )]
            [SwaggerResponse(HttpStatusCode.OK, type: typeof(Task<dynamic>))]
            [SwaggerResponse(HttpStatusCode.NotFound, "No New or Modifed Documents found")]
            [SwaggerOperation("GetNewOrModifiedFHIRDocuments")]
            public async Task<dynamic> GetNewOrModifiedFhirDocuments(
                [Metadata("Database Id", "Database Id")] string databaseId,
                [Metadata("Collection Id", "Collection Id")] string collectionId,
                [Metadata("Resource Type", "FHIR resource type name")] string resourceType,
                [Metadata("Start from Beginning ", "Change Feed Option")] bool startfromBeginning,
                [Metadata("Maximum Item Count", "Number of documents returned. '-1 returns all' (default)")] int maximumItemCount = -1
            )
            {
                var collectionLink = UriFactory.CreateDocumentCollectionUri(databaseId, collectionId);
    
                var context = new DocumentDbContext();  
    
                var docs = new List<dynamic>();
    
                var partitionKeyRanges = new List<PartitionKeyRange>();
                FeedResponse<PartitionKeyRange> pkRangesResponse;
    
                do
                {
                    pkRangesResponse = await context.Client.ReadPartitionKeyRangeFeedAsync(collectionLink);
                    partitionKeyRanges.AddRange(pkRangesResponse);
                } while (pkRangesResponse.ResponseContinuation != null);
    
                foreach (var pkRange in partitionKeyRanges)
                {
                    var changeFeedOptions = new ChangeFeedOptions
                    {
                        StartFromBeginning = startfromBeginning,
                        RequestContinuation = null,
                        MaxItemCount = maximumItemCount,
                        PartitionKeyRangeId = pkRange.Id
                    };
    
                    using (var query = context.Client.CreateDocumentChangeFeedQuery(collectionLink, changeFeedOptions))
                    {
                        do
                        {
                            if (query != null)
                            {
                                var results = await query.ExecuteNextAsync<dynamic>().ConfigureAwait(false);
                                if (results.Count > 0)
                                    docs.AddRange(results.Where(doc => doc.resourceType == resourceType));
                            }
                            else
                            {
                                throw new HttpResponseException(new HttpResponseMessage(HttpStatusCode.NotFound));
                            }
                        } while (query.HasMoreResults);
                    }
                }
                if (docs.Count > 0)
                    return docs;
                var msg = new StringContent("No documents found for " + resourceType + " Resource");
                var response = new HttpResponseMessage
                {
                    StatusCode = HttpStatusCode.NotFound,
                    Content = msg
                };
                return response;
            }
        }
    }
    
```

### <a name="testing-hello-fhirnotificationapi"></a>Testar Olá FhirNotificationApi 

Olá imagem seguinte demonstra como swagger foi utilizado tootootest Olá [FhirNotificationApi](#api-app-source).

![o ficheiro Swagger Olá utilizado a aplicação de API de Olá tootest](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a>Dashboard do portal do Azure

Olá imagem a seguir mostra todos os Olá serviços do Azure para esta solução em execução no Olá portal do Azure.

![Olá portal do Azure que mostra todos os serviços de Olá utilizados neste tutorial HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a>Resumo

- Aprendeu a que a base de dados do Azure Cosmos tem suppport nativo para as notificações para novas ou documentos contidos e como é fácil toouse. 
- Ao tirar partido das Logic Apps, pode criar fluxos de trabalho sem escrever qualquer código.
- Utilização da distribuição de Olá toohandle de filas do Service Bus do Azure para documentos de HL7 FHIR Olá.

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre a BD do Cosmos do Azure, consulte Olá [home page da base de dados do Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/). Para obter mais informaiton sobre Logic Apps, consulte [Logic Apps](https://azure.microsoft.com/services/logic-apps/).


