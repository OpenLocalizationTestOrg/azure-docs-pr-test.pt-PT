---
title: "aaaScheduler autenticação de saída"
description: "Autenticação de saída do agendador"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 6707f82b-7e32-401b-a960-02aae7bb59cc
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2016
ms.author: deli
ms.openlocfilehash: ef713f4770b48d0a9176415e87c1042a823582e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-outbound-authentication"></a><span data-ttu-id="4f56b-103">Autenticação de saída do agendador</span><span class="sxs-lookup"><span data-stu-id="4f56b-103">Scheduler Outbound Authentication</span></span>
<span data-ttu-id="4f56b-104">Trabalhos do programador do poderão ter toocall saída tooservices que exija autenticação.</span><span class="sxs-lookup"><span data-stu-id="4f56b-104">Scheduler jobs may need toocall out tooservices that require authentication.</span></span> <span data-ttu-id="4f56b-105">Desta forma, um serviço chamado pode determinar se a tarefa do agendador de Olá pode aceder os recursos.</span><span class="sxs-lookup"><span data-stu-id="4f56b-105">This way, a called service can determine if hello Scheduler job can access its resources.</span></span> <span data-ttu-id="4f56b-106">Alguns destes serviços incluem outros serviços do Azure, em Salesforce.com, Facebook e Web sites personalizados segurados.</span><span class="sxs-lookup"><span data-stu-id="4f56b-106">Some of these services include other Azure services, Salesforce.com, Facebook, and secure custom websites.</span></span>

## <a name="adding-and-removing-authentication"></a><span data-ttu-id="4f56b-107">Adição e remoção de autenticação</span><span class="sxs-lookup"><span data-stu-id="4f56b-107">Adding and Removing Authentication</span></span>
<span data-ttu-id="4f56b-108">Adicionar a tarefa de programador tooa de autenticação é simple – adicionar um elemento subordinado JSON `authentication` toohello `request` elemento quando criar ou atualizar uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="4f56b-108">Adding authentication tooa Scheduler job is simple – add a JSON child element `authentication` toohello `request` element when creating or updating a job.</span></span> <span data-ttu-id="4f56b-109">Os segredos transmitido serviço de agendador toohello num pedido PUT, correção ou POST – como parte do Olá `authentication` objeto – nunca são devolvidas em respostas.</span><span class="sxs-lookup"><span data-stu-id="4f56b-109">Secrets passed toohello Scheduler service in a PUT, PATCH, or POST request – as part of hello `authentication` object – are never returned in responses.</span></span> <span data-ttu-id="4f56b-110">Nas respostas, as informações secretas estão definidas toonull ou podem ter um token pública que representa a entidade de Olá autenticado.</span><span class="sxs-lookup"><span data-stu-id="4f56b-110">In responses, secret information is set toonull or may have a public token that represents hello authenticated entity.</span></span>

<span data-ttu-id="4f56b-111">autenticação tooremove, PUT ou PATCH tarefa Olá explicitamente, definição Olá `authentication` toonull de objeto.</span><span class="sxs-lookup"><span data-stu-id="4f56b-111">tooremove authentication, PUT or PATCH hello job explicitly, setting hello `authentication` object toonull.</span></span> <span data-ttu-id="4f56b-112">Não irá ver quaisquer propriedades de autenticação na resposta.</span><span class="sxs-lookup"><span data-stu-id="4f56b-112">You will not see any authentication properties back in response.</span></span>

<span data-ttu-id="4f56b-113">Atualmente, Olá só são suportado tipos de autenticação são Olá `ClientCertificate` modelo (para utilização de certificados de cliente SSL/TLS Olá), Olá `Basic` modelo (para autenticação básica) e Olá `ActiveDirectoryOAuth` modelo (para o Active Directory OAuth autenticação).</span><span class="sxs-lookup"><span data-stu-id="4f56b-113">Currently, hello only supported authentication types are hello `ClientCertificate` model (for using hello SSL/TLS client certificates), hello `Basic` model (for Basic authentication), and hello `ActiveDirectoryOAuth` model (for Active Directory OAuth authentication.)</span></span>

## <a name="request-body-for-clientcertificate-authentication"></a><span data-ttu-id="4f56b-114">Corpo do pedido para a autenticação de ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="4f56b-114">Request Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="4f56b-115">Ao adicionar a autenticação utilizando Olá `ClientCertificate` modelo, especifique Olá seguintes elementos adicionais no corpo do pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="4f56b-115">When adding authentication using hello `ClientCertificate` model, specify hello following additional elements in hello request body.</span></span>  

| <span data-ttu-id="4f56b-116">Elemento</span><span class="sxs-lookup"><span data-stu-id="4f56b-116">Element</span></span> | <span data-ttu-id="4f56b-117">Descrição</span><span class="sxs-lookup"><span data-stu-id="4f56b-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4f56b-118">*autenticação (elemento principal)*</span><span class="sxs-lookup"><span data-stu-id="4f56b-118">*authentication (parent element)*</span></span> |<span data-ttu-id="4f56b-119">Objeto de autenticação para utilizar um certificado de cliente SSL.</span><span class="sxs-lookup"><span data-stu-id="4f56b-119">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="4f56b-120">*tipo*</span><span class="sxs-lookup"><span data-stu-id="4f56b-120">*type*</span></span> |<span data-ttu-id="4f56b-121">Necessário.</span><span class="sxs-lookup"><span data-stu-id="4f56b-121">Required.</span></span> <span data-ttu-id="4f56b-122">Tipo de autenticação. Para certificados de cliente SSL, Olá valor tem de ser `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="4f56b-122">Type of authentication.For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="4f56b-123">*PFX*</span><span class="sxs-lookup"><span data-stu-id="4f56b-123">*pfx*</span></span> |<span data-ttu-id="4f56b-124">Necessário.</span><span class="sxs-lookup"><span data-stu-id="4f56b-124">Required.</span></span> <span data-ttu-id="4f56b-125">Conteúdo do ficheiro PFX de Olá com codificação Base64.</span><span class="sxs-lookup"><span data-stu-id="4f56b-125">Base64-encoded contents of hello PFX file.</span></span> |
| <span data-ttu-id="4f56b-126">*palavra-passe*</span><span class="sxs-lookup"><span data-stu-id="4f56b-126">*password*</span></span> |<span data-ttu-id="4f56b-127">Necessário.</span><span class="sxs-lookup"><span data-stu-id="4f56b-127">Required.</span></span> <span data-ttu-id="4f56b-128">Palavra-passe tooaccess Olá PFX o ficheiro.</span><span class="sxs-lookup"><span data-stu-id="4f56b-128">Password tooaccess hello PFX file.</span></span> |

## <a name="response-body-for-clientcertificate-authentication"></a><span data-ttu-id="4f56b-129">Corpo de resposta para a autenticação de ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="4f56b-129">Response Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="4f56b-130">Quando é enviado um pedido com informações de autenticação, resposta Olá contém Olá seguintes elementos relacionados com a autenticação.</span><span class="sxs-lookup"><span data-stu-id="4f56b-130">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="4f56b-131">Elemento</span><span class="sxs-lookup"><span data-stu-id="4f56b-131">Element</span></span> | <span data-ttu-id="4f56b-132">Descrição</span><span class="sxs-lookup"><span data-stu-id="4f56b-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4f56b-133">*autenticação (elemento principal)*</span><span class="sxs-lookup"><span data-stu-id="4f56b-133">*authentication (parent element)*</span></span> |<span data-ttu-id="4f56b-134">Objeto de autenticação para utilizar um certificado de cliente SSL.</span><span class="sxs-lookup"><span data-stu-id="4f56b-134">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="4f56b-135">*tipo*</span><span class="sxs-lookup"><span data-stu-id="4f56b-135">*type*</span></span> |<span data-ttu-id="4f56b-136">Tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="4f56b-136">Type of authentication.</span></span> <span data-ttu-id="4f56b-137">Para certificados de cliente SSL, o valor de Olá é `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="4f56b-137">For SSL client certificates, hello value is `ClientCertificate`.</span></span> |
| <span data-ttu-id="4f56b-138">*certificateThumbprint*</span><span class="sxs-lookup"><span data-stu-id="4f56b-138">*certificateThumbprint*</span></span> |<span data-ttu-id="4f56b-139">Olá impressão digital do certificado de Olá.</span><span class="sxs-lookup"><span data-stu-id="4f56b-139">hello thumbprint of hello certificate.</span></span> |
| <span data-ttu-id="4f56b-140">*certificateSubjectName*</span><span class="sxs-lookup"><span data-stu-id="4f56b-140">*certificateSubjectName*</span></span> |<span data-ttu-id="4f56b-141">nome de hora distinto do requerente Olá do certificado de Olá.</span><span class="sxs-lookup"><span data-stu-id="4f56b-141">hello subject distinguished name of hello certificate.</span></span> |
| <span data-ttu-id="4f56b-142">*certificateExpiration*</span><span class="sxs-lookup"><span data-stu-id="4f56b-142">*certificateExpiration*</span></span> |<span data-ttu-id="4f56b-143">Olá data de expiração Olá certificado.</span><span class="sxs-lookup"><span data-stu-id="4f56b-143">hello expiration date of hello certificate.</span></span> |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a><span data-ttu-id="4f56b-144">Exemplo de pedido REST para a autenticação de ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="4f56b-144">Sample REST Request for ClientCertificate Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "clientcertificate",
          "password": "password",
          "pfx": "pfx key"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-clientcertificate-authentication"></a><span data-ttu-id="4f56b-145">Resposta REST de exemplo para a autenticação de ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="4f56b-145">Sample REST Response for ClientCertificate Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 858
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 56c7b40e-721a-437e-88e6-f68562a73aa8
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 1075219e-e879-4030-bc81-094e54fbabce
x-ms-routing-request-id: WESTUS:20160316T190424Z:1075219e-e879-4030-bc81-094e54fbabce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:04:23 GMT

{
  "id": "/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
  "type": "Microsoft.Scheduler/jobCollections/jobs",
  "name": "southeastasiajc/httpjob",
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "certificateThumbprint": "88105CG9DF9ADE75B835711D899296CB217D7055",
          "certificateExpiration": "2021-01-01T07:00:00Z",
          "certificateSubjectName": "CN=Scheduler Mgmt",
          "type": "ClientCertificate"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
    "status": {
      "nextExecutionTime": "2016-03-16T19:05:00Z",
      "executionCount": 0,
      "failureCount": 0,
      "faultedCount": 0
    }
  }
}
```

## <a name="request-body-for-basic-authentication"></a><span data-ttu-id="4f56b-146">Corpo do pedido para a autenticação básica</span><span class="sxs-lookup"><span data-stu-id="4f56b-146">Request Body for Basic Authentication</span></span>
<span data-ttu-id="4f56b-147">Ao adicionar a autenticação utilizando Olá `Basic` modelo, especifique Olá seguintes elementos adicionais no corpo do pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="4f56b-147">When adding authentication using hello `Basic` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="4f56b-148">Elemento</span><span class="sxs-lookup"><span data-stu-id="4f56b-148">Element</span></span> | <span data-ttu-id="4f56b-149">Descrição</span><span class="sxs-lookup"><span data-stu-id="4f56b-149">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4f56b-150">*autenticação (elemento principal)*</span><span class="sxs-lookup"><span data-stu-id="4f56b-150">*authentication (parent element)*</span></span> |<span data-ttu-id="4f56b-151">Objeto de autenticação para utilizar a autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="4f56b-151">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="4f56b-152">*tipo*</span><span class="sxs-lookup"><span data-stu-id="4f56b-152">*type*</span></span> |<span data-ttu-id="4f56b-153">Necessário.</span><span class="sxs-lookup"><span data-stu-id="4f56b-153">Required.</span></span> <span data-ttu-id="4f56b-154">Tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="4f56b-154">Type of authentication.</span></span> <span data-ttu-id="4f56b-155">Para a autenticação básica, Olá valor tem de ser `Basic`.</span><span class="sxs-lookup"><span data-stu-id="4f56b-155">For Basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="4f56b-156">*nome de utilizador*</span><span class="sxs-lookup"><span data-stu-id="4f56b-156">*username*</span></span> |<span data-ttu-id="4f56b-157">Necessário.</span><span class="sxs-lookup"><span data-stu-id="4f56b-157">Required.</span></span> <span data-ttu-id="4f56b-158">Tooauthenticate de nome de utilizador.</span><span class="sxs-lookup"><span data-stu-id="4f56b-158">Username tooauthenticate.</span></span> |
| <span data-ttu-id="4f56b-159">*palavra-passe*</span><span class="sxs-lookup"><span data-stu-id="4f56b-159">*password*</span></span> |<span data-ttu-id="4f56b-160">Necessário.</span><span class="sxs-lookup"><span data-stu-id="4f56b-160">Required.</span></span> <span data-ttu-id="4f56b-161">Tooauthenticate de palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="4f56b-161">Password tooauthenticate.</span></span> |

## <a name="response-body-for-basic-authentication"></a><span data-ttu-id="4f56b-162">Corpo de resposta para a autenticação básica</span><span class="sxs-lookup"><span data-stu-id="4f56b-162">Response Body for Basic Authentication</span></span>
<span data-ttu-id="4f56b-163">Quando é enviado um pedido com informações de autenticação, resposta Olá contém Olá seguintes elementos relacionados com a autenticação.</span><span class="sxs-lookup"><span data-stu-id="4f56b-163">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="4f56b-164">Elemento</span><span class="sxs-lookup"><span data-stu-id="4f56b-164">Element</span></span> | <span data-ttu-id="4f56b-165">Descrição</span><span class="sxs-lookup"><span data-stu-id="4f56b-165">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4f56b-166">*autenticação (elemento principal)*</span><span class="sxs-lookup"><span data-stu-id="4f56b-166">*authentication (parent element)*</span></span> |<span data-ttu-id="4f56b-167">Objeto de autenticação para utilizar a autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="4f56b-167">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="4f56b-168">*tipo*</span><span class="sxs-lookup"><span data-stu-id="4f56b-168">*type*</span></span> |<span data-ttu-id="4f56b-169">Tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="4f56b-169">Type of authentication.</span></span> <span data-ttu-id="4f56b-170">Para a autenticação básica, o valor de Olá é `Basic`.</span><span class="sxs-lookup"><span data-stu-id="4f56b-170">For Basic authentication, hello value is `Basic`.</span></span> |
| <span data-ttu-id="4f56b-171">*nome de utilizador*</span><span class="sxs-lookup"><span data-stu-id="4f56b-171">*username*</span></span> |<span data-ttu-id="4f56b-172">Olá autenticar o nome de utilizador.</span><span class="sxs-lookup"><span data-stu-id="4f56b-172">hello authenticated username.</span></span> |

## <a name="sample-rest-request-for-basic-authentication"></a><span data-ttu-id="4f56b-173">Exemplo de pedido REST para a autenticação básica</span><span class="sxs-lookup"><span data-stu-id="4f56b-173">Sample REST Request for Basic Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 562
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "basic",
          "username": "user",
          "password": "password"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-basic-authentication"></a><span data-ttu-id="4f56b-174">Resposta REST de exemplo para a autenticação básica</span><span class="sxs-lookup"><span data-stu-id="4f56b-174">Sample REST Response for Basic Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 701
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: a2dcb9cd-1aea-4887-8893-d81273a8cf04
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 7816f222-6ea7-468d-b919-e6ddebbd7e95
x-ms-routing-request-id: WESTUS:20160316T190506Z:7816f222-6ea7-468d-b919-e6ddebbd7e95
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:05:06 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "username":"user1",
               "type":"Basic"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "nextExecutionTime":"2016-03-16T19:06:00Z",
         "executionCount":0,
         "failureCount":0,
         "faultedCount":0
      }
   }
}
```

## <a name="request-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="4f56b-175">Corpo do pedido para a autenticação de ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="4f56b-175">Request Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="4f56b-176">Ao adicionar a autenticação utilizando Olá `ActiveDirectoryOAuth` modelo, especifique Olá seguintes elementos adicionais no corpo do pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="4f56b-176">When adding authentication using hello `ActiveDirectoryOAuth` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="4f56b-177">Elemento</span><span class="sxs-lookup"><span data-stu-id="4f56b-177">Element</span></span> | <span data-ttu-id="4f56b-178">Descrição</span><span class="sxs-lookup"><span data-stu-id="4f56b-178">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4f56b-179">*autenticação (elemento principal)*</span><span class="sxs-lookup"><span data-stu-id="4f56b-179">*authentication (parent element)*</span></span> |<span data-ttu-id="4f56b-180">Objeto de autenticação para utilizar a autenticação de ActiveDirectoryOAuth.</span><span class="sxs-lookup"><span data-stu-id="4f56b-180">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="4f56b-181">*tipo*</span><span class="sxs-lookup"><span data-stu-id="4f56b-181">*type*</span></span> |<span data-ttu-id="4f56b-182">Necessário.</span><span class="sxs-lookup"><span data-stu-id="4f56b-182">Required.</span></span> <span data-ttu-id="4f56b-183">Tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="4f56b-183">Type of authentication.</span></span> <span data-ttu-id="4f56b-184">Para a autenticação do ActiveDirectoryOAuth Olá valor tem de ser `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="4f56b-184">For ActiveDirectoryOAuth authentication, hello value must be `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="4f56b-185">*inquilino*</span><span class="sxs-lookup"><span data-stu-id="4f56b-185">*tenant*</span></span> |<span data-ttu-id="4f56b-186">Necessário.</span><span class="sxs-lookup"><span data-stu-id="4f56b-186">Required.</span></span> <span data-ttu-id="4f56b-187">Olá identificador de inquilino para o inquilino Olá do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f56b-187">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="4f56b-188">*público-alvo*</span><span class="sxs-lookup"><span data-stu-id="4f56b-188">*audience*</span></span> |<span data-ttu-id="4f56b-189">Necessário.</span><span class="sxs-lookup"><span data-stu-id="4f56b-189">Required.</span></span> <span data-ttu-id="4f56b-190">Isto é definido toohttps://management.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="4f56b-190">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="4f56b-191">*ID de cliente*</span><span class="sxs-lookup"><span data-stu-id="4f56b-191">*clientId*</span></span> |<span data-ttu-id="4f56b-192">Necessário.</span><span class="sxs-lookup"><span data-stu-id="4f56b-192">Required.</span></span> <span data-ttu-id="4f56b-193">Forneça o identificador de cliente Olá para Olá aplicação do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f56b-193">Provide hello client identifier for hello Azure AD application.</span></span> |
| <span data-ttu-id="4f56b-194">*segredo*</span><span class="sxs-lookup"><span data-stu-id="4f56b-194">*secret*</span></span> |<span data-ttu-id="4f56b-195">Necessário.</span><span class="sxs-lookup"><span data-stu-id="4f56b-195">Required.</span></span> <span data-ttu-id="4f56b-196">Segredo do cliente de Olá que está a solicitar o token de Olá.</span><span class="sxs-lookup"><span data-stu-id="4f56b-196">Secret of hello client that is requesting hello token.</span></span> |

### <a name="determining-your-tenant-identifier"></a><span data-ttu-id="4f56b-197">Determinar o identificador do seu inquilino</span><span class="sxs-lookup"><span data-stu-id="4f56b-197">Determining your Tenant Identifier</span></span>
<span data-ttu-id="4f56b-198">Pode encontrar o identificador de inquilino Olá para o inquilino do Azure AD de Olá executando `Get-AzureAccount` no Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4f56b-198">You can find hello tenant identifier for hello Azure AD tenant by running `Get-AzureAccount` in Azure PowerShell.</span></span>

## <a name="response-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="4f56b-199">Corpo de resposta para a autenticação de ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="4f56b-199">Response Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="4f56b-200">Quando é enviado um pedido com informações de autenticação, resposta Olá contém Olá seguintes elementos relacionados com a autenticação.</span><span class="sxs-lookup"><span data-stu-id="4f56b-200">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="4f56b-201">Elemento</span><span class="sxs-lookup"><span data-stu-id="4f56b-201">Element</span></span> | <span data-ttu-id="4f56b-202">Descrição</span><span class="sxs-lookup"><span data-stu-id="4f56b-202">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4f56b-203">*autenticação (elemento principal)*</span><span class="sxs-lookup"><span data-stu-id="4f56b-203">*authentication (parent element)*</span></span> |<span data-ttu-id="4f56b-204">Objeto de autenticação para utilizar a autenticação de ActiveDirectoryOAuth.</span><span class="sxs-lookup"><span data-stu-id="4f56b-204">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="4f56b-205">*tipo*</span><span class="sxs-lookup"><span data-stu-id="4f56b-205">*type*</span></span> |<span data-ttu-id="4f56b-206">Tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="4f56b-206">Type of authentication.</span></span> <span data-ttu-id="4f56b-207">Para a autenticação de ActiveDirectoryOAuth, o valor de Olá é `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="4f56b-207">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="4f56b-208">*inquilino*</span><span class="sxs-lookup"><span data-stu-id="4f56b-208">*tenant*</span></span> |<span data-ttu-id="4f56b-209">Olá identificador de inquilino para o inquilino Olá do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f56b-209">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="4f56b-210">*público-alvo*</span><span class="sxs-lookup"><span data-stu-id="4f56b-210">*audience*</span></span> |<span data-ttu-id="4f56b-211">Isto é definido toohttps://management.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="4f56b-211">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="4f56b-212">*ID de cliente*</span><span class="sxs-lookup"><span data-stu-id="4f56b-212">*clientId*</span></span> |<span data-ttu-id="4f56b-213">Olá identificador de cliente para a aplicação Olá do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f56b-213">hello client identifier for hello Azure AD application.</span></span> |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a><span data-ttu-id="4f56b-214">Exemplo de pedido REST para a autenticação de ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="4f56b-214">Sample REST Request for ActiveDirectoryOAuth Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 757
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "tenant":"microsoft.onmicrosoft.com",
          "audience":"https://management.core.windows.net/",
          "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
          "secret": "G6u071r8Gjw4V4KSibnb+VK4+tX399hkHaj7LOyHuj5=",
          "type":"ActiveDirectoryOAuth"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a><span data-ttu-id="4f56b-215">Resposta REST de exemplo para a autenticação de ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="4f56b-215">Sample REST Response for ActiveDirectoryOAuth Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 885
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 86d8e9fd-ac0d-4bed-9420-9baba1af3251
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
x-ms-routing-request-id: WESTUS:20160316T191003Z:5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:10:02 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "tenant":"microsoft.onmicrosoft.com",
               "audience":"https://management.core.windows.net/",
               "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
               "type":"ActiveDirectoryOAuth"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "lastExecutionTime":"2016-03-16T19:10:00.3762123Z",
         "nextExecutionTime":"2016-03-16T19:11:00Z",
         "executionCount":5,
         "failureCount":5,
         "faultedCount":1
      }
   }
}
```

## <a name="see-also"></a><span data-ttu-id="4f56b-216">Veja Também</span><span class="sxs-lookup"><span data-stu-id="4f56b-216">See Also</span></span>
 [<span data-ttu-id="4f56b-217">O que é o Scheduler?</span><span class="sxs-lookup"><span data-stu-id="4f56b-217">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="4f56b-218">Conceitos, terminologia e hierarquia de entidades do Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="4f56b-218">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="4f56b-219">Começar a utilizar o agendador no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4f56b-219">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="4f56b-220">Planos e faturação no Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="4f56b-220">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="4f56b-221">Referência da API REST do Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="4f56b-221">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="4f56b-222">Referência de cmdlets do PowerShell do Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="4f56b-222">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="4f56b-223">Elevada disponibilidade e fiabilidade do Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="4f56b-223">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="4f56b-224">Limites, predefinições e códigos de erro do Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="4f56b-224">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

