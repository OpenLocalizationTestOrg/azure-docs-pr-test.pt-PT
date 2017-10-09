---
title: "aaaException processamento & cenário de registo de erro - Azure Logic Apps | Microsoft Docs"
description: "Descreve um caso de utilização real sobre o processamento de exceções avançadas e registo de erros para o Azure Logic Apps"
keywords: 
services: logic-apps
author: hedidin
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 63b0b843-f6b0-4d9a-98d0-17500be17385
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/29/2016
ms.author: LADocs; b-hoedid
ms.openlocfilehash: e893a7b652254dca7b8a82398e8afd571f6ccd25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a><span data-ttu-id="bd363-103">Cenário: Processamento de exceções e registo de erros para aplicações lógicas</span><span class="sxs-lookup"><span data-stu-id="bd363-103">Scenario: Exception handling and error logging for logic apps</span></span>

<span data-ttu-id="bd363-104">Este cenário descreve como expandir o processamento de exceções uma lógica aplicação toobetter suporte.</span><span class="sxs-lookup"><span data-stu-id="bd363-104">This scenario describes how you can extend a logic app toobetter support exception handling.</span></span> <span data-ttu-id="bd363-105">Tiver utilizámos uma pergunta de Olá tooanswer caso utilize reais: "Aplicações lógicas do Azure suporta exceções e processamento de erros?"</span><span class="sxs-lookup"><span data-stu-id="bd363-105">We've used a real-life use case tooanswer hello question: "Does Azure Logic Apps support exception and error handling?"</span></span>

> [!NOTE]
> <span data-ttu-id="bd363-106">esquema de Azure Logic Apps atual Olá fornece um modelo padrão para respostas de ação.</span><span class="sxs-lookup"><span data-stu-id="bd363-106">hello current Azure Logic Apps schema provides a standard template for action responses.</span></span> <span data-ttu-id="bd363-107">Este modelo inclui validação interna e respostas de erros devolvidas por uma aplicação API.</span><span class="sxs-lookup"><span data-stu-id="bd363-107">This template includes both internal validation and error responses returned from an API app.</span></span>

## <a name="scenario-and-use-case-overview"></a><span data-ttu-id="bd363-108">Descrição geral de cenário de cenário e utilização</span><span class="sxs-lookup"><span data-stu-id="bd363-108">Scenario and use case overview</span></span>

<span data-ttu-id="bd363-109">Eis o bloco de Olá como caso de utilização de Olá para este cenário:</span><span class="sxs-lookup"><span data-stu-id="bd363-109">Here's hello story as hello use case for this scenario:</span></span> 

<span data-ttu-id="bd363-110">Uma organização de cuidados de saúde bem conhecida-na parte toodevelop uma solução do Azure que criaria um portal patient através do Microsoft Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="bd363-110">A well-known healthcare organization engaged us toodevelop an Azure solution that would create a patient portal by using Microsoft Dynamics CRM Online.</span></span> <span data-ttu-id="bd363-111">São necessários os registos de sessão toosend entre o portal de patient Dynamics CRM Online Olá e da Salesforce.</span><span class="sxs-lookup"><span data-stu-id="bd363-111">They needed toosend appointment records between hello Dynamics CRM Online patient portal and Salesforce.</span></span> <span data-ttu-id="bd363-112">Iremos foram-lhe pedidos toouse Olá [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) padrão para todas as patient registos.</span><span class="sxs-lookup"><span data-stu-id="bd363-112">We were asked toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard for all patient records.</span></span>

<span data-ttu-id="bd363-113">projeto de Olá tinha dois requisitos principais:</span><span class="sxs-lookup"><span data-stu-id="bd363-113">hello project had two major requirements:</span></span>  

* <span data-ttu-id="bd363-114">Registos toolog método enviados a partir de Olá portal Dynamics CRM Online</span><span class="sxs-lookup"><span data-stu-id="bd363-114">A method toolog records sent from hello Dynamics CRM Online portal</span></span>
* <span data-ttu-id="bd363-115">Uma forma tooview quaisquer erros que ocorreram dentro do fluxo de trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="bd363-115">A way tooview any errors that occurred within hello workflow</span></span>

> [!TIP]
> <span data-ttu-id="bd363-116">Para um vídeo de alto nível sobre este projeto, consulte [grupo de utilizadores de integração](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "grupo de utilizadores de integração").</span><span class="sxs-lookup"><span data-stu-id="bd363-116">For a high-level video about this project, see [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span></span>

## <a name="how-we-solved-hello-problem"></a><span data-ttu-id="bd363-117">Como é resolvido o problema de Olá</span><span class="sxs-lookup"><span data-stu-id="bd363-117">How we solved hello problem</span></span>

<span data-ttu-id="bd363-118">Escolhemos [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") como um repositório para registos de registo e o erro de Olá (Cosmos DB refere-se toorecords como documentos).</span><span class="sxs-lookup"><span data-stu-id="bd363-118">We chose [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") As a repository for hello log and error records (Cosmos DB refers toorecords as documents).</span></span> <span data-ttu-id="bd363-119">Uma vez Azure Logic Apps tem um modelo padrão para todas as respostas, seria não temos toocreate um esquema personalizado.</span><span class="sxs-lookup"><span data-stu-id="bd363-119">Because Azure Logic Apps has a standard template for all responses, we would not have toocreate a custom schema.</span></span> <span data-ttu-id="bd363-120">Foi possível criar uma aplicação API demasiado**inserir** e **consulta** para registos de erro e registo.</span><span class="sxs-lookup"><span data-stu-id="bd363-120">We could create an API app too**Insert** and **Query** for both error and log records.</span></span> <span data-ttu-id="bd363-121">Iremos também definir um esquema para cada aplicação de API de Olá.</span><span class="sxs-lookup"><span data-stu-id="bd363-121">We could also define a schema for each within hello API app.</span></span>  

<span data-ttu-id="bd363-122">Outro requisito necessário foi toopurge registos após uma data determinada.</span><span class="sxs-lookup"><span data-stu-id="bd363-122">Another requirement was toopurge records after a certain date.</span></span> <span data-ttu-id="bd363-123">Cosmos DB tem uma propriedade denominada [tempo tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "tempo tooLive") (TTL), que permitido nos tooset um **tempo tooLive** valor para cada registo ou a coleção.</span><span class="sxs-lookup"><span data-stu-id="bd363-123">Cosmos DB has a property called [Time tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time tooLive") (TTL), which allowed us tooset a **Time tooLive** value for each record or collection.</span></span> <span data-ttu-id="bd363-124">Esta capacidade eliminado o aperto Olá necessidade toomanually eliminar os registos na base de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bd363-124">This capability eliminated hello need toomanually delete records in Cosmos DB.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd363-125">toocomplete neste tutorial, precisa de toocreate uma base de dados de base de dados do Cosmos e duas coleções (registo e erros).</span><span class="sxs-lookup"><span data-stu-id="bd363-125">toocomplete this tutorial, you need toocreate a Cosmos DB database and two collections (Logging and Errors).</span></span>

## <a name="create-hello-logic-app"></a><span data-ttu-id="bd363-126">Criar aplicação de lógica de Olá</span><span class="sxs-lookup"><span data-stu-id="bd363-126">Create hello logic app</span></span>

<span data-ttu-id="bd363-127">Step-by-Olá primeiro passo é a aplicação de lógica de Olá toocreate e aplicação Olá aberta no Designer de aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="bd363-127">hello first step is toocreate hello logic app and open hello app in Logic App Designer.</span></span> <span data-ttu-id="bd363-128">Neste exemplo, estamos a utilizar aplicações lógicas de principal-subordinado.</span><span class="sxs-lookup"><span data-stu-id="bd363-128">In this example, we are using parent-child logic apps.</span></span> <span data-ttu-id="bd363-129">Vamos assumir já criou principal Olá e vai toocreate uma aplicação de lógica de subordinados.</span><span class="sxs-lookup"><span data-stu-id="bd363-129">Let's assume that we have already created hello parent and are going toocreate one child logic app.</span></span>

<span data-ttu-id="bd363-130">Vamos começar porque, vamos registo de Olá toolog provenientes de Dynamics CRM Online, na parte superior do Olá.</span><span class="sxs-lookup"><span data-stu-id="bd363-130">Because we are going toolog hello record coming out of Dynamics CRM Online, let's start at hello top.</span></span> <span data-ttu-id="bd363-131">Iremos tem de utilizar um **pedido** acionar porque a aplicação de lógica de principal de Olá aciona menor.</span><span class="sxs-lookup"><span data-stu-id="bd363-131">We must use a **Request** trigger because hello parent logic app triggers this child.</span></span>

### <a name="logic-app-trigger"></a><span data-ttu-id="bd363-132">Acionador de aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="bd363-132">Logic app trigger</span></span>

<span data-ttu-id="bd363-133">Estamos a utilizar um **pedido** acionar conforme mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="bd363-133">We are using a **Request** trigger as shown in hello following example:</span></span>

```` json
"triggers": {
        "request": {
          "type": "request",
          "kind": "http",
          "inputs": {
            "schema": {
              "properties": {
                "CRMid": {
                  "type": "string"
                },
                "recordType": {
                  "type": "string"
                },
                "salesforceID": {
                  "type": "string"
                },
                "update": {
                  "type": "boolean"
                }
              },
              "required": [
                "CRMid",
                "recordType",
                "salesforceID",
                "update"
              ],
              "type": "object"
            }
          }
        }
      },

````


## <a name="steps"></a><span data-ttu-id="bd363-134">Passos</span><span class="sxs-lookup"><span data-stu-id="bd363-134">Steps</span></span>

<span data-ttu-id="bd363-135">Iremos tem de iniciar a origem de Olá (pedido) do registo patient Olá do portal de Dynamics CRM Online Olá.</span><span class="sxs-lookup"><span data-stu-id="bd363-135">We must log hello source (request) of hello patient record from hello Dynamics CRM Online portal.</span></span>

1. <span data-ttu-id="bd363-136">Iremos tem de obter um novo registo de sessão do Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="bd363-136">We must get a new appointment record from Dynamics CRM Online.</span></span>

   <span data-ttu-id="bd363-137">acionador Olá feitos CRM fornece-nos com Olá **CRM PatentId**, **tipo de registo**, **novo ou atualizar o registo** (novo ou atualizar o valor booleano), e  **SalesforceId**.</span><span class="sxs-lookup"><span data-stu-id="bd363-137">hello trigger coming from CRM provides us with hello **CRM PatentId**, **record type**, **New or Updated Record** (new or update Boolean value), and **SalesforceId**.</span></span> <span data-ttu-id="bd363-138">Olá **SalesforceId** pode ser nulo porque só é utilizada para uma atualização.</span><span class="sxs-lookup"><span data-stu-id="bd363-138">hello **SalesforceId** can be null because it's only used for an update.</span></span>
   <span data-ttu-id="bd363-139">Vamos obter registos CRM Olá utilizando Olá CRM **PatientID** e Olá **tipo de registo**.</span><span class="sxs-lookup"><span data-stu-id="bd363-139">We get hello CRM record by using hello CRM **PatientID** and hello **Record Type**.</span></span>

2. <span data-ttu-id="bd363-140">Em seguida, temos tooadd nossa aplicação de API do DocumentDB **InsertLogEntry** operação conforme mostrado aqui no Designer de aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="bd363-140">Next, we need tooadd our DocumentDB API app **InsertLogEntry** operation as shown here in Logic App Designer.</span></span>

   <span data-ttu-id="bd363-141">**Inserir entrada de registo**</span><span class="sxs-lookup"><span data-stu-id="bd363-141">**Insert log entry**</span></span>

   ![Inserir entrada de registo](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   <span data-ttu-id="bd363-143">**Inserir entrada de erro**</span><span class="sxs-lookup"><span data-stu-id="bd363-143">**Insert error entry**</span></span>

   ![Inserir entrada de registo](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   <span data-ttu-id="bd363-145">**A verificação para criar registo falha**</span><span class="sxs-lookup"><span data-stu-id="bd363-145">**Check for create record failure**</span></span>

   ![Condição](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a><span data-ttu-id="bd363-147">Código de origem da aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="bd363-147">Logic app source code</span></span>

> [!NOTE]
> <span data-ttu-id="bd363-148">Olá exemplos a seguir é apenas exemplos.</span><span class="sxs-lookup"><span data-stu-id="bd363-148">hello following examples are samples only.</span></span> <span data-ttu-id="bd363-149">Olá, porque este tutorial baseiam-se uma implementação agora na produção, valor de um **origem nó** pode não apresentar as propriedades que estão relacionado tooscheduling uma sessão. ></span><span class="sxs-lookup"><span data-stu-id="bd363-149">Because this tutorial is based on an implementation now in production, hello value of a **Source Node** might not display properties that are related tooscheduling an appointment.></span></span> 

### <a name="logging"></a><span data-ttu-id="bd363-150">Registo</span><span class="sxs-lookup"><span data-stu-id="bd363-150">Logging</span></span>

<span data-ttu-id="bd363-151">Olá seguinte código de aplicação de lógica de exemplo mostra como toohandle registo.</span><span class="sxs-lookup"><span data-stu-id="bd363-151">hello following logic app code sample shows how toohandle logging.</span></span>

#### <a name="log-entry"></a><span data-ttu-id="bd363-152">Entrada de registo</span><span class="sxs-lookup"><span data-stu-id="bd363-152">Log entry</span></span>

<span data-ttu-id="bd363-153">Eis o código de origem do Olá logic app para inserir uma entrada de registo.</span><span class="sxs-lookup"><span data-stu-id="bd363-153">Here is hello logic app source code for inserting a log entry.</span></span>

``` json
"InsertLogEntry": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "date": "@{outputs('Gets_NewPatientRecord')['headers']['Date']}",
            "operation": "New Patient",
            "patientId": "@{triggerBody()['CRMid']}",
            "providerId": "@{triggerBody()['providerID']}",
            "source": "@{outputs('Gets_NewPatientRecord')['headers']}"
        },
        "method": "post",
        "uri": "https://.../api/Log"
        },
        "runAfter":    {
            "Gets_NewPatientecord": ["Succeeded"]
        }
}
```

#### <a name="log-request"></a><span data-ttu-id="bd363-154">Pedido de registo</span><span class="sxs-lookup"><span data-stu-id="bd363-154">Log request</span></span>

<span data-ttu-id="bd363-155">Eis a mensagem de pedido de registo de Olá publicada a aplicação de API toohello.</span><span class="sxs-lookup"><span data-stu-id="bd363-155">Here is hello log request message posted toohello API app.</span></span>

``` json
    {
    "uri": "https://.../api/Log",
    "method": "post",
    "body": {
        "date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "operation": "New Patient",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "providerId": "",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}"
        }
    }

```


#### <a name="log-response"></a><span data-ttu-id="bd363-156">Resposta de registo</span><span class="sxs-lookup"><span data-stu-id="bd363-156">Log response</span></span>

<span data-ttu-id="bd363-157">Eis a mensagem de resposta de registo Olá da aplicação de API de Olá.</span><span class="sxs-lookup"><span data-stu-id="bd363-157">Here is hello log response message from hello API app.</span></span>

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:32:17 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "964",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "ttl": 2592000,
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0_1465597937",
        "_rid": "XngRAOT6IQEHAAAAAAAAAA==",
        "_self": "dbs/XngRAA==/colls/XngRAOT6IQE=/docs/XngRAOT6IQEHAAAAAAAAAA==/",
        "_ts": 1465597936,
        "_etag": "/"0400fc2f-0000-0000-0000-575b3ff00000/"",
        "patientID": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:56Z",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}",
        "operation": "New Patient",
        "salesforceId": "",
        "expired": false
    }
}

```

<span data-ttu-id="bd363-158">Agora vamos ver os passos de processamento de erros de Olá.</span><span class="sxs-lookup"><span data-stu-id="bd363-158">Now let's look at hello error handling steps.</span></span>

### <a name="error-handling"></a><span data-ttu-id="bd363-159">Processamento de erros</span><span class="sxs-lookup"><span data-stu-id="bd363-159">Error handling</span></span>

<span data-ttu-id="bd363-160">Olá exemplo de código da aplicação de lógica seguinte mostra como pode implementar o processamento de erros.</span><span class="sxs-lookup"><span data-stu-id="bd363-160">hello following logic app code sample shows how you can implement error handling.</span></span>

#### <a name="create-error-record"></a><span data-ttu-id="bd363-161">Criar registo de erro</span><span class="sxs-lookup"><span data-stu-id="bd363-161">Create error record</span></span>

<span data-ttu-id="bd363-162">Eis o código de origem do Olá lógica aplicação para criar um registo de erro.</span><span class="sxs-lookup"><span data-stu-id="bd363-162">Here is hello logic app source code for creating an error record.</span></span>

``` json
"actions": {
    "CreateErrorRecord": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "action": "New_Patient",
            "isError": true,
            "crmId": "@{triggerBody()['CRMid']}",
            "patientID": "@{triggerBody()['CRMid']}",
            "message": "@{body('Create_NewPatientRecord')['message']}",
            "providerId": "@{triggerBody()['providerId']}",
            "severity": 4,
            "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
            "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
            "salesforceId": "",
            "update": false
        },
        "method": "post",
        "uri": "https://.../api/CrMtoSfError"
        },
        "runAfter":
        {
            "Create_NewPatientRecord": ["Failed" ]
        }
    }
}             
```

#### <a name="insert-error-into-cosmos-db--request"></a><span data-ttu-id="bd363-163">Erro de inserção na base de dados do Cosmos – pedido</span><span class="sxs-lookup"><span data-stu-id="bd363-163">Insert error into Cosmos DB--request</span></span>

``` json

{
    "uri": "https://.../api/CrMtoSfError",
    "method": "post",
    "body": {
        "action": "New_Patient",
        "isError": true,
        "crmId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "providerId": "",
        "severity": 4,
        "salesforceId": "",
        "update": false,
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MasterID_mp__c/":/"/",/"C_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"ONY_ID__c/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "statusCode": "400"
    }
}
```

#### <a name="insert-error-into-cosmos-db--response"></a><span data-ttu-id="bd363-164">Inserir o erro na base de dados do Cosmos - resposta</span><span class="sxs-lookup"><span data-stu-id="bd363-164">Insert error into Cosmos DB--response</span></span>

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:57 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "1561",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0-1465597917",
        "_rid": "sQx2APhVzAA8AAAAAAAAAA==",
        "_self": "dbs/sQx2AA==/colls/sQx2APhVzAA=/docs/sQx2APhVzAA8AAAAAAAAAA==/",
        "_ts": 1465597912,
        "_etag": "/"0c00eaac-0000-0000-0000-575b3fdc0000/"",
        "prescriberId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:57.3651027Z",
        "action": "New_Patient",
        "salesforceId": "",
        "update": false,
        "body": "CRM failed toocomplete task: Message: duplicate value found: CRM_HUB_ID__c duplicates value on record with id: 001U000001c83gK",
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/":/"DO - Degree level is DO/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MterID_mp__c/":/"/",/"Medicis_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"XXXXXXX/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "code": 400,
        "errors": null,
        "isError": true,
        "severity": 4,
        "notes": null,
        "resolved": 0
        }
}
```

#### <a name="salesforce-error-response"></a><span data-ttu-id="bd363-165">Resposta de erro do Salesforce</span><span class="sxs-lookup"><span data-stu-id="bd363-165">Salesforce error response</span></span>

``` json
{
    "statusCode": 400,
    "headers": {
        "Pragma": "no-cache",
        "x-ms-request-id": "3e8e4884-288e-4633-972c-8271b2cc912c",
        "X-Content-Type-Options": "nosniff",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "Set-Cookie": "ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1",
        "Server": "Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "205",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "status": 400,
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "source": "Salesforce.Common",
        "errors": []
    }
}

```

### <a name="return-hello-response-back-tooparent-logic-app"></a><span data-ttu-id="bd363-166">Devolver a aplicação de lógica de back-tooparent de resposta de Olá</span><span class="sxs-lookup"><span data-stu-id="bd363-166">Return hello response back tooparent logic app</span></span>

<span data-ttu-id="bd363-167">Depois de obter resposta Olá, pode passar resposta Olá aplicação de lógica de principal toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="bd363-167">After you get hello response, you can pass hello response back toohello parent logic app.</span></span>

#### <a name="return-success-response-tooparent-logic-app"></a><span data-ttu-id="bd363-168">Devolver a aplicação de lógica de tooparent de resposta de êxito</span><span class="sxs-lookup"><span data-stu-id="bd363-168">Return success response tooparent logic app</span></span>

``` json
"SuccessResponse": {
    "runAfter":
        {
            "UpdateNew_CRMPatientResponse": ["Succeeded"]
        },
    "inputs": {
        "body": {
            "status": "Success"
    },
    "headers": {
    "    Content-type": "application/json",
        "x-ms-date": "@utcnow()"
    },
    "statusCode": 200
    },
    "type": "Response"
}
```

#### <a name="return-error-response-tooparent-logic-app"></a><span data-ttu-id="bd363-169">Devolver a aplicação de lógica de tooparent de resposta de erro</span><span class="sxs-lookup"><span data-stu-id="bd363-169">Return error response tooparent logic app</span></span>

``` json
"ErrorResponse": {
    "runAfter":
        {
            "Create_NewPatientRecord": ["Failed"]
        },
    "inputs": {
        "body": {
            "status": "BadRequest"
        },
        "headers": {
            "Content-type": "application/json",
            "x-ms-date": "@utcnow()"
        },
        "statusCode": 400
    },
    "type": "Response"
}

```


## <a name="cosmos-db-repository-and-portal"></a><span data-ttu-id="bd363-170">Portal e do repositório do cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bd363-170">Cosmos DB repository and portal</span></span>

<span data-ttu-id="bd363-171">A nossa solução adicionada capacidades com [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span><span class="sxs-lookup"><span data-stu-id="bd363-171">Our solution added capabilities with [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span></span>

### <a name="error-management-portal"></a><span data-ttu-id="bd363-172">Portal de gestão de erro</span><span class="sxs-lookup"><span data-stu-id="bd363-172">Error management portal</span></span>

<span data-ttu-id="bd363-173">erros de Olá tooview, pode criar um registos de erro do MVC web app toodisplay Olá da base de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bd363-173">tooview hello errors, you can create an MVC web app toodisplay hello error records from Cosmos DB.</span></span> <span data-ttu-id="bd363-174">Olá **lista**, **detalhes**, **editar**, e **eliminar** operations estão incluído na versão atual do Olá.</span><span class="sxs-lookup"><span data-stu-id="bd363-174">hello **List**, **Details**, **Edit**, and **Delete** operations are included in hello current version.</span></span>

> [!NOTE]
> <span data-ttu-id="bd363-175">Editar operação: Cosmos DB substitui documento Olá de todo.</span><span class="sxs-lookup"><span data-stu-id="bd363-175">Edit operation: Cosmos DB replaces hello entire document.</span></span> <span data-ttu-id="bd363-176">Olá registos mostrados na Olá **lista** e **detalhe** as vistas são apenas exemplos.</span><span class="sxs-lookup"><span data-stu-id="bd363-176">hello records shown in hello **List** and **Detail** views are samples only.</span></span> <span data-ttu-id="bd363-177">Não são registos de sessão patient real.</span><span class="sxs-lookup"><span data-stu-id="bd363-177">They are not actual patient appointment records.</span></span>

<span data-ttu-id="bd363-178">Seguem-se exemplos de nossa aplicação MVC detalhes criados com Olá anteriormente descrito abordagem.</span><span class="sxs-lookup"><span data-stu-id="bd363-178">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="error-management-list"></a><span data-ttu-id="bd363-179">Lista de gestão de erros</span><span class="sxs-lookup"><span data-stu-id="bd363-179">Error management list</span></span>
![Lista de erros](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a><span data-ttu-id="bd363-181">Vista de detalhes do erro gestão</span><span class="sxs-lookup"><span data-stu-id="bd363-181">Error management detail view</span></span>
![Detalhes do Erro](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a><span data-ttu-id="bd363-183">Portal de gestão do registo</span><span class="sxs-lookup"><span data-stu-id="bd363-183">Log management portal</span></span>

<span data-ttu-id="bd363-184">os registos de Olá tooview, também foi criada uma aplicação web MVC.</span><span class="sxs-lookup"><span data-stu-id="bd363-184">tooview hello logs, we also created an MVC web app.</span></span> <span data-ttu-id="bd363-185">Seguem-se exemplos de nossa aplicação MVC detalhes criados com Olá anteriormente descrito abordagem.</span><span class="sxs-lookup"><span data-stu-id="bd363-185">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="sample-log-detail-view"></a><span data-ttu-id="bd363-186">Vista de detalhes de registo de exemplo</span><span class="sxs-lookup"><span data-stu-id="bd363-186">Sample log detail view</span></span>
![Vista de detalhes de registo](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a><span data-ttu-id="bd363-188">Detalhes da aplicação API</span><span class="sxs-lookup"><span data-stu-id="bd363-188">API app details</span></span>

#### <a name="logic-apps-exception-management-api"></a><span data-ttu-id="bd363-189">API de gestão de exceção de aplicações do lógica</span><span class="sxs-lookup"><span data-stu-id="bd363-189">Logic Apps exception management API</span></span>

<span data-ttu-id="bd363-190">A nossa aplicação de API de gestão do open source Azure Logic Apps exceção fornece uma funcionalidade, conforme descrito aqui – existem dois controladores:</span><span class="sxs-lookup"><span data-stu-id="bd363-190">Our open-source Azure Logic Apps exception management API app provides functionality as described here - there are two controllers:</span></span>

* <span data-ttu-id="bd363-191">**ErrorController** insere um registo de erro (documento) numa coleção do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="bd363-191">**ErrorController** inserts an error record (document) in a DocumentDB collection.</span></span>
* <span data-ttu-id="bd363-192">**LogController** insere um registo (documento) numa coleção do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="bd363-192">**LogController** Inserts a log record (document) in a DocumentDB collection.</span></span>

> [!TIP]
> <span data-ttu-id="bd363-193">Utilizam os dois controladores `async Task<dynamic>` operações, permitindo tooresolve operações em runtime, para que possa criar Olá esquema DocumentDB no corpo de Olá de operação de Olá.</span><span class="sxs-lookup"><span data-stu-id="bd363-193">Both controllers use `async Task<dynamic>` operations, allowing operations tooresolve at runtime, so we can create hello DocumentDB schema in hello body of hello operation.</span></span> 
> 

<span data-ttu-id="bd363-194">Todos os documentos no DocumentDB tem de ter um ID exclusivo.</span><span class="sxs-lookup"><span data-stu-id="bd363-194">Every document in DocumentDB must have a unique ID.</span></span> <span data-ttu-id="bd363-195">Estamos a utilizar `PatientId` e adicionar um timestamp que é converter o valor de timestamp tooa Unix (double).</span><span class="sxs-lookup"><span data-stu-id="bd363-195">We are using `PatientId` and adding a timestamp that is converted tooa Unix timestamp value (double).</span></span> <span data-ttu-id="bd363-196">Iremos truncar valor fracional de Olá valor tooremove Olá.</span><span class="sxs-lookup"><span data-stu-id="bd363-196">We truncate hello value tooremove hello fractional value.</span></span>

<span data-ttu-id="bd363-197">Pode ver o código de origem Olá do nosso controlador Erro API [a partir do GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span><span class="sxs-lookup"><span data-stu-id="bd363-197">You can view hello source code of our error controller API [from GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span></span>

<span data-ttu-id="bd363-198">Chamamos Olá API a partir de uma aplicação lógica, utilizando Olá sintaxe:</span><span class="sxs-lookup"><span data-stu-id="bd363-198">We call hello API from a logic app by using hello following syntax:</span></span>

``` json
 "actions": {
        "CreateErrorRecord": {
          "metadata": {
            "apiDefinitionUrl": "https://.../swagger/docs/v1",
            "swaggerSource": "website"
          },
          "type": "Http",
          "inputs": {
            "body": {
              "action": "New_Patient",
              "isError": true,
              "crmId": "@{triggerBody()['CRMid']}",
              "prescriberId": "@{triggerBody()['CRMid']}",
              "message": "@{body('Create_NewPatientRecord')['message']}",
              "salesforceId": "@{triggerBody()['salesforceID']}",
              "severity": 4,
              "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
              "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
              "update": false
            },
            "method": "post",
            "uri": "https://.../api/CrMtoSfError"
          },
          "runAfter": {
              "Create_NewPatientRecord": ["Failed"]
            }
        }
 }
```

<span data-ttu-id="bd363-199">Olá expressão no Olá anterior exemplo de código verificações para Olá *Create_NewPatientRecord* estado **falha**.</span><span class="sxs-lookup"><span data-stu-id="bd363-199">hello expression in hello preceding code sample checks for hello *Create_NewPatientRecord* status of **Failed**.</span></span>

## <a name="summary"></a><span data-ttu-id="bd363-200">Resumo</span><span class="sxs-lookup"><span data-stu-id="bd363-200">Summary</span></span>

* <span data-ttu-id="bd363-201">Pode facilmente implementar registo e erros numa aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="bd363-201">You can easily implement logging and error handling in a logic app.</span></span>
* <span data-ttu-id="bd363-202">Pode utilizar o DocumentDB como repositório de Olá para registos de erro e de registo (documentos).</span><span class="sxs-lookup"><span data-stu-id="bd363-202">You can use DocumentDB as hello repository for log and error records (documents).</span></span>
* <span data-ttu-id="bd363-203">Pode utilizar MVC toocreate um registo de portal toodisplay e registos de erro.</span><span class="sxs-lookup"><span data-stu-id="bd363-203">You can use MVC toocreate a portal toodisplay log and error records.</span></span>

### <a name="source-code"></a><span data-ttu-id="bd363-204">Código de origem</span><span class="sxs-lookup"><span data-stu-id="bd363-204">Source code</span></span>

<span data-ttu-id="bd363-205">código de origem Olá para gestão de exceções de Logic Apps aplicação API de Olá está disponível neste [repositório do GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "API de gestão de exceção de aplicação lógica").</span><span class="sxs-lookup"><span data-stu-id="bd363-205">hello source code for hello Logic Apps exception management API application is available in this [GitHub repository](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App Exception Management API").</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd363-206">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="bd363-206">Next steps</span></span>

* [<span data-ttu-id="bd363-207">Ver mais cenários e exemplos de aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="bd363-207">View more logic app examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="bd363-208">Saiba mais sobre a monitorização de aplicações lógicas</span><span class="sxs-lookup"><span data-stu-id="bd363-208">Learn about monitoring logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="bd363-209">Criar modelos de implementação automática para as logic apps</span><span class="sxs-lookup"><span data-stu-id="bd363-209">Create automated deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
