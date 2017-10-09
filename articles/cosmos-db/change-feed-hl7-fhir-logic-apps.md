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
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="0a4f5-104">Notificar patients das alterações de registo de saúde HL7 FHIR com Logic Apps e a base de dados do Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="0a4f5-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="0a4f5-105">Azure Edidin de Howard MVP recentemente foi contactado por uma organização de cuidados de saúde que pretendia tooadd nova funcionalidade tootheir patient portal.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted tooadd new functionality tootheir patient portal.</span></span> <span data-ttu-id="0a4f5-106">Se necessitar de toosend notificações toopatients respetivo registo de estado de funcionamento foi atualizado e necessárias patients toobe toosubscribe capaz de toothese atualizações.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-106">They needed toosend notifications toopatients when their health record was updated, and they needed patients toobe able toosubscribe toothese updates.</span></span> 

<span data-ttu-id="0a4f5-107">Este artigo acompanha-o através da solução de feed de notificação de alteração de Olá criada para esta organização de cuidados de saúde utilizando a BD do Cosmos do Azure, as Logic Apps e o Service Bus.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-107">This article walks through hello change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="0a4f5-108">Requisitos do projeto</span><span class="sxs-lookup"><span data-stu-id="0a4f5-108">Project requirements</span></span>
- <span data-ttu-id="0a4f5-109">Fornecedores de enviam a arquitetura de documento consolidado Clinical HL7 (C-CDA) documentos no formato XML.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="0a4f5-110">Documentos C CDA abranger praticamente cada tipo de documento clinical, incluindo documentos clinical como histories famílias e registos de immunization, bem como administrativos, fluxo de trabalho e os documentos financeiros.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="0a4f5-111">Documentos C CDA são convertidos demasiado[HL7 FHIR recursos](http://hl7.org/fhir/2017Jan/resourcelist.html) no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-111">C-CDA documents are converted too[HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="0a4f5-112">Documentos de recurso FHIR modificados são enviados por correio eletrónico no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="0a4f5-113">Fluxo de trabalho da solução</span><span class="sxs-lookup"><span data-stu-id="0a4f5-113">Solution workflow</span></span> 

<span data-ttu-id="0a4f5-114">Um nível elevado, o projeto Olá necessário Olá os seguintes passos de fluxo de trabalho:</span><span class="sxs-lookup"><span data-stu-id="0a4f5-114">At a high level, hello project required hello following workflow steps:</span></span> 
1. <span data-ttu-id="0a4f5-115">Converta os recursos de tooFHIR C CDA documentos.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-115">Convert C-CDA documents tooFHIR resources.</span></span>
2. <span data-ttu-id="0a4f5-116">Execute o acionador recorrente de consulta para obter recursos FHIR modificados.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="0a4f5-117">Chame uma aplicação personalizada, FhirNotificationApi, tooconnect tooAzure Cosmos DB e consulta para documentos novos ou modificados.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-117">Call a custom app, FhirNotificationApi, tooconnect tooAzure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="0a4f5-118">Guarde a fila do Service Bus Olá resposta tootoohello.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-118">Save hello response tootoohello Service Bus queue.</span></span>
4. <span data-ttu-id="0a4f5-119">Consulta para novas mensagens na fila do Service Bus Olá.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-119">Poll for new messages in hello Service Bus queue.</span></span>
5. <span data-ttu-id="0a4f5-120">Envie toopatients de notificações de correio eletrónico.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-120">Send email notifications toopatients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="0a4f5-121">Arquitetura de solução</span><span class="sxs-lookup"><span data-stu-id="0a4f5-121">Solution architecture</span></span>
<span data-ttu-id="0a4f5-122">Esta solução requer três Olá de toomeet Logic Apps acima requisitos e fluxo de trabalho de solução de Olá concluída.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-122">This solution requires three Logic Apps toomeet hello above requirements and complete hello solution workflow.</span></span> <span data-ttu-id="0a4f5-123">as logic apps de três Olá são:</span><span class="sxs-lookup"><span data-stu-id="0a4f5-123">hello three logic apps are:</span></span>
1. <span data-ttu-id="0a4f5-124">**Aplicação de mapeamento de FHIR HL7**: recebe o documento de HL7 C-CDA Olá, transforma-toohello FHIR recursos e guarda-o tooAzure BD do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-124">**HL7-FHIR-Mapping app**: Receives hello HL7 C-CDA document, transforms it toohello FHIR Resource, then saves it tooAzure Cosmos DB.</span></span>
2. <span data-ttu-id="0a4f5-125">**Aplicação EHR**: consulta o repositório de Azure Cosmos DB FHIR Olá e guarda a fila do Service Bus Olá resposta tooa.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-125">**EHR app**: Queries hello Azure Cosmos DB FHIR repository and saves hello response tooa Service Bus queue.</span></span> <span data-ttu-id="0a4f5-126">Esta aplicação lógica utiliza um [aplicação API](#api-app) tooretrieve novas e alteradas documentos.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-126">This logic app uses an [API app](#api-app) tooretrieve new and changed documents.</span></span>
3. <span data-ttu-id="0a4f5-127">**Aplicação de notificação de processo**: envia uma notificação de correio eletrónico com documentos de recursos FHIR Olá no corpo de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-127">**Process notification app**: Sends an email notification with hello FHIR resource documents in hello body.</span></span>

![Olá três Logic Apps utilizada nesta solução de cuidados de saúde HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a><span data-ttu-id="0a4f5-129">Serviços do Azure utilizados na solução de Olá</span><span class="sxs-lookup"><span data-stu-id="0a4f5-129">Azure services used in hello solution</span></span>

#### <a name="azure-cosmos-db-documentdb-api"></a><span data-ttu-id="0a4f5-130">DocumentDB do Azure Cosmos DB API</span><span class="sxs-lookup"><span data-stu-id="0a4f5-130">Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="0a4f5-131">BD do Azure do Cosmos é o repositório de Olá para recursos FHIR Olá, conforme mostrado no Olá figura a seguir.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-131">Azure Cosmos DB is hello repository for hello FHIR resources as shown in hello following figure.</span></span>

![conta de base de dados do Azure Cosmos Olá utilizada neste tutorial de cuidados de saúde HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="0a4f5-133">Aplicações Lógicas</span><span class="sxs-lookup"><span data-stu-id="0a4f5-133">Logic Apps</span></span>
<span data-ttu-id="0a4f5-134">As Logic Apps lidar com o processo de fluxo de trabalho de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-134">Logic Apps handle hello workflow process.</span></span> <span data-ttu-id="0a4f5-135">Olá capturas de ecrã seguintes mostram Olá as Logic apps criadas para esta solução.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-135">hello following screenshots show hello Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="0a4f5-136">**Aplicação de mapeamento de FHIR HL7**: receber o documento de HL7 C-CDA Olá e transformá-los recursos FHIR tooan utilizando Olá Enterprise Integration Pack para aplicações lógicas.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-136">**HL7-FHIR-Mapping app**: Receive hello HL7 C-CDA document and transform it tooan FHIR resource using hello Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="0a4f5-137">Olá Enterprise Integration Pack processa Olá mapeamento da Olá recursos de tooFHIR C CDA.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-137">hello Enterprise Integration Pack handles hello mapping from hello C-CDA tooFHIR resources.</span></span>

    ![Olá aplicação lógica utilizada registos de cuidados de saúde tooreceive HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="0a4f5-139">**Aplicação EHR**: consultar o repositório de Azure Cosmos DB FHIR Olá e guarde Olá resposta tooa barramento de serviço fila.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-139">**EHR app**: Query hello Azure Cosmos DB FHIR repository and save hello response tooa Service Bus queue.</span></span> <span data-ttu-id="0a4f5-140">código de Olá Olá GetNewOrModifiedFHIRDocuments aplicação está abaixo.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-140">hello code for hello GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![Olá aplicação lógica utilizada tooquery BD do Cosmos do Azure](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="0a4f5-142">**Aplicação de notificação de processo**: enviar uma notificação de correio eletrónico com documentos de recursos FHIR Olá no corpo de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-142">**Process notification app**: Send an email notification with hello FHIR resource documents in hello body.</span></span>

    ![Olá aplicação lógica que envia correio eletrónico patient com recurso de HL7 FHIR Olá no corpo de Olá](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="0a4f5-144">Service Bus</span><span class="sxs-lookup"><span data-stu-id="0a4f5-144">Service Bus</span></span>
<span data-ttu-id="0a4f5-145">Olá seguinte figura mostra Olá patients fila.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-145">hello following figure shows hello patients queue.</span></span> <span data-ttu-id="0a4f5-146">Olá valor de propriedade da etiqueta é utilizada para o assunto do e-mail Olá.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-146">hello Tag property value is used for hello email subject.</span></span>

![Olá utilizado neste tutorial HL7 FHIR de fila do Service Bus](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="0a4f5-148">Aplicação API</span><span class="sxs-lookup"><span data-stu-id="0a4f5-148">API app</span></span>
<span data-ttu-id="0a4f5-149">Uma aplicação API liga tooAzure Cosmos DB e consultas para novos ou modificados documentos FHIR por tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-149">An API app connects tooAzure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="0a4f5-150">Esta aplicação tem um controlador, **FhirNotificationApi** com uma única operação **GetNewOrModifiedFhirDocuments**, consulte [origem para a aplicação API](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="0a4f5-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="0a4f5-151">Estamos a utilizar Olá [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) classe a partir de Olá Cosmos BD do DocumentDB .NET API do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-151">We are using hello [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from hello Azure Cosmos DB DocumentDB .NET API.</span></span> <span data-ttu-id="0a4f5-152">Para obter mais informações, consulte Olá [alteração feed artigo](change-feed.md).</span><span class="sxs-lookup"><span data-stu-id="0a4f5-152">For more information, see hello [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="0a4f5-153">Operação GetNewOrModifiedFhirDocuments</span><span class="sxs-lookup"><span data-stu-id="0a4f5-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="0a4f5-154">**Entradas**</span><span class="sxs-lookup"><span data-stu-id="0a4f5-154">**Inputs**</span></span>
- <span data-ttu-id="0a4f5-155">DatabaseId</span><span class="sxs-lookup"><span data-stu-id="0a4f5-155">DatabaseId</span></span>
- <span data-ttu-id="0a4f5-156">CollectionId</span><span class="sxs-lookup"><span data-stu-id="0a4f5-156">CollectionId</span></span>
- <span data-ttu-id="0a4f5-157">Nome de tipo de recurso de FHIR HL7</span><span class="sxs-lookup"><span data-stu-id="0a4f5-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="0a4f5-158">Valor booleano: Iniciar a partir do início</span><span class="sxs-lookup"><span data-stu-id="0a4f5-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="0a4f5-159">INT: Número de documentos devolvidos</span><span class="sxs-lookup"><span data-stu-id="0a4f5-159">Int: Number of documents returned</span></span>

<span data-ttu-id="0a4f5-160">**Saídas**</span><span class="sxs-lookup"><span data-stu-id="0a4f5-160">**Outputs**</span></span>
- <span data-ttu-id="0a4f5-161">Êxito: Código de estado: resposta 200,: lista de documentos (matriz JSON)</span><span class="sxs-lookup"><span data-stu-id="0a4f5-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="0a4f5-162">Falha: Código de estado: respostas 404,: "não existem documentos encontrado para '*nome de recurso '* tipo de recurso"</span><span class="sxs-lookup"><span data-stu-id="0a4f5-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="0a4f5-163">**Origem da aplicação Olá API**</span><span class="sxs-lookup"><span data-stu-id="0a4f5-163">**Source for hello API app**</span></span>

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

### <a name="testing-hello-fhirnotificationapi"></a><span data-ttu-id="0a4f5-164">Testar Olá FhirNotificationApi</span><span class="sxs-lookup"><span data-stu-id="0a4f5-164">Testing hello FhirNotificationApi</span></span> 

<span data-ttu-id="0a4f5-165">Olá imagem seguinte demonstra como swagger foi utilizado tootootest Olá [FhirNotificationApi](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="0a4f5-165">hello following image demonstrates how swagger was used tootootest hello [FhirNotificationApi](#api-app-source).</span></span>

![o ficheiro Swagger Olá utilizado a aplicação de API de Olá tootest](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="0a4f5-167">Dashboard do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0a4f5-167">Azure portal dashboard</span></span>

<span data-ttu-id="0a4f5-168">Olá imagem a seguir mostra todos os Olá serviços do Azure para esta solução em execução no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-168">hello following image shows all of hello Azure services for this solution running in hello Azure portal.</span></span>

![Olá portal do Azure que mostra todos os serviços de Olá utilizados neste tutorial HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="0a4f5-170">Resumo</span><span class="sxs-lookup"><span data-stu-id="0a4f5-170">Summary</span></span>

- <span data-ttu-id="0a4f5-171">Aprendeu a que a base de dados do Azure Cosmos tem suppport nativo para as notificações para novas ou documentos contidos e como é fácil toouse.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is toouse.</span></span> 
- <span data-ttu-id="0a4f5-172">Ao tirar partido das Logic Apps, pode criar fluxos de trabalho sem escrever qualquer código.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="0a4f5-173">Utilização da distribuição de Olá toohandle de filas do Service Bus do Azure para documentos de HL7 FHIR Olá.</span><span class="sxs-lookup"><span data-stu-id="0a4f5-173">Using Azure Service Bus Queues toohandle hello distribution for hello HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a4f5-174">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0a4f5-174">Next steps</span></span>
<span data-ttu-id="0a4f5-175">Para obter mais informações sobre a BD do Cosmos do Azure, consulte Olá [home page da base de dados do Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="0a4f5-175">For more information about Azure Cosmos DB, see hello [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="0a4f5-176">Para obter mais informaiton sobre Logic Apps, consulte [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="0a4f5-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


