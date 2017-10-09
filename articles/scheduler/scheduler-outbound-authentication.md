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
# <a name="scheduler-outbound-authentication"></a>Autenticação de saída do agendador
Trabalhos do programador do poderão ter toocall saída tooservices que exija autenticação. Desta forma, um serviço chamado pode determinar se a tarefa do agendador de Olá pode aceder os recursos. Alguns destes serviços incluem outros serviços do Azure, em Salesforce.com, Facebook e Web sites personalizados segurados.

## <a name="adding-and-removing-authentication"></a>Adição e remoção de autenticação
Adicionar a tarefa de programador tooa de autenticação é simple – adicionar um elemento subordinado JSON `authentication` toohello `request` elemento quando criar ou atualizar uma tarefa. Os segredos transmitido serviço de agendador toohello num pedido PUT, correção ou POST – como parte do Olá `authentication` objeto – nunca são devolvidas em respostas. Nas respostas, as informações secretas estão definidas toonull ou podem ter um token pública que representa a entidade de Olá autenticado.

autenticação tooremove, PUT ou PATCH tarefa Olá explicitamente, definição Olá `authentication` toonull de objeto. Não irá ver quaisquer propriedades de autenticação na resposta.

Atualmente, Olá só são suportado tipos de autenticação são Olá `ClientCertificate` modelo (para utilização de certificados de cliente SSL/TLS Olá), Olá `Basic` modelo (para autenticação básica) e Olá `ActiveDirectoryOAuth` modelo (para o Active Directory OAuth autenticação).

## <a name="request-body-for-clientcertificate-authentication"></a>Corpo do pedido para a autenticação de ClientCertificate
Ao adicionar a autenticação utilizando Olá `ClientCertificate` modelo, especifique Olá seguintes elementos adicionais no corpo do pedido de Olá.  

| Elemento | Descrição |
|:--- |:--- |
| *autenticação (elemento principal)* |Objeto de autenticação para utilizar um certificado de cliente SSL. |
| *tipo* |Necessário. Tipo de autenticação. Para certificados de cliente SSL, Olá valor tem de ser `ClientCertificate`. |
| *PFX* |Necessário. Conteúdo do ficheiro PFX de Olá com codificação Base64. |
| *palavra-passe* |Necessário. Palavra-passe tooaccess Olá PFX o ficheiro. |

## <a name="response-body-for-clientcertificate-authentication"></a>Corpo de resposta para a autenticação de ClientCertificate
Quando é enviado um pedido com informações de autenticação, resposta Olá contém Olá seguintes elementos relacionados com a autenticação.

| Elemento | Descrição |
|:--- |:--- |
| *autenticação (elemento principal)* |Objeto de autenticação para utilizar um certificado de cliente SSL. |
| *tipo* |Tipo de autenticação. Para certificados de cliente SSL, o valor de Olá é `ClientCertificate`. |
| *certificateThumbprint* |Olá impressão digital do certificado de Olá. |
| *certificateSubjectName* |nome de hora distinto do requerente Olá do certificado de Olá. |
| *certificateExpiration* |Olá data de expiração Olá certificado. |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a>Exemplo de pedido REST para a autenticação de ClientCertificate
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

## <a name="sample-rest-response-for-clientcertificate-authentication"></a>Resposta REST de exemplo para a autenticação de ClientCertificate
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

## <a name="request-body-for-basic-authentication"></a>Corpo do pedido para a autenticação básica
Ao adicionar a autenticação utilizando Olá `Basic` modelo, especifique Olá seguintes elementos adicionais no corpo do pedido de Olá.

| Elemento | Descrição |
|:--- |:--- |
| *autenticação (elemento principal)* |Objeto de autenticação para utilizar a autenticação básica. |
| *tipo* |Necessário. Tipo de autenticação. Para a autenticação básica, Olá valor tem de ser `Basic`. |
| *nome de utilizador* |Necessário. Tooauthenticate de nome de utilizador. |
| *palavra-passe* |Necessário. Tooauthenticate de palavra-passe. |

## <a name="response-body-for-basic-authentication"></a>Corpo de resposta para a autenticação básica
Quando é enviado um pedido com informações de autenticação, resposta Olá contém Olá seguintes elementos relacionados com a autenticação.

| Elemento | Descrição |
|:--- |:--- |
| *autenticação (elemento principal)* |Objeto de autenticação para utilizar a autenticação básica. |
| *tipo* |Tipo de autenticação. Para a autenticação básica, o valor de Olá é `Basic`. |
| *nome de utilizador* |Olá autenticar o nome de utilizador. |

## <a name="sample-rest-request-for-basic-authentication"></a>Exemplo de pedido REST para a autenticação básica
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

## <a name="sample-rest-response-for-basic-authentication"></a>Resposta REST de exemplo para a autenticação básica
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

## <a name="request-body-for-activedirectoryoauth-authentication"></a>Corpo do pedido para a autenticação de ActiveDirectoryOAuth
Ao adicionar a autenticação utilizando Olá `ActiveDirectoryOAuth` modelo, especifique Olá seguintes elementos adicionais no corpo do pedido de Olá.

| Elemento | Descrição |
|:--- |:--- |
| *autenticação (elemento principal)* |Objeto de autenticação para utilizar a autenticação de ActiveDirectoryOAuth. |
| *tipo* |Necessário. Tipo de autenticação. Para a autenticação do ActiveDirectoryOAuth Olá valor tem de ser `ActiveDirectoryOAuth`. |
| *inquilino* |Necessário. Olá identificador de inquilino para o inquilino Olá do Azure AD. |
| *público-alvo* |Necessário. Isto é definido toohttps://management.core.windows.net/. |
| *ID de cliente* |Necessário. Forneça o identificador de cliente Olá para Olá aplicação do Azure AD. |
| *segredo* |Necessário. Segredo do cliente de Olá que está a solicitar o token de Olá. |

### <a name="determining-your-tenant-identifier"></a>Determinar o identificador do seu inquilino
Pode encontrar o identificador de inquilino Olá para o inquilino do Azure AD de Olá executando `Get-AzureAccount` no Azure PowerShell.

## <a name="response-body-for-activedirectoryoauth-authentication"></a>Corpo de resposta para a autenticação de ActiveDirectoryOAuth
Quando é enviado um pedido com informações de autenticação, resposta Olá contém Olá seguintes elementos relacionados com a autenticação.

| Elemento | Descrição |
|:--- |:--- |
| *autenticação (elemento principal)* |Objeto de autenticação para utilizar a autenticação de ActiveDirectoryOAuth. |
| *tipo* |Tipo de autenticação. Para a autenticação de ActiveDirectoryOAuth, o valor de Olá é `ActiveDirectoryOAuth`. |
| *inquilino* |Olá identificador de inquilino para o inquilino Olá do Azure AD. |
| *público-alvo* |Isto é definido toohttps://management.core.windows.net/. |
| *ID de cliente* |Olá identificador de cliente para a aplicação Olá do Azure AD. |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a>Exemplo de pedido REST para a autenticação de ActiveDirectoryOAuth
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

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a>Resposta REST de exemplo para a autenticação de ActiveDirectoryOAuth
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

## <a name="see-also"></a>Veja Também
 [O que é o Scheduler?](scheduler-intro.md)

 [Conceitos, terminologia e hierarquia de entidades do Azure Scheduler](scheduler-concepts-terms.md)

 [Começar a utilizar o agendador no Olá portal do Azure](scheduler-get-started-portal.md)

 [Planos e faturação no Azure Scheduler](scheduler-plans-billing.md)

 [Referência da API REST do Azure Scheduler](https://msdn.microsoft.com/library/mt629143)

 [Referência de cmdlets do PowerShell do Azure Scheduler](scheduler-powershell-reference.md)

 [Elevada disponibilidade e fiabilidade do Azure Scheduler](scheduler-high-availability-reliability.md)

 [Limites, predefinições e códigos de erro do Azure Scheduler](scheduler-limits-defaults-errors.md)

