---
title: aaaGet iniciado utilizando a REST API do Data Lake Analytics | Microsoft Docs
description: "Utilizar operações de tooperform WebHDFS REST APIs no Data Lake Analytics"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 5e133d92-baaa-44c9-890c-ab2d85c91122
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: jgao
ms.openlocfilehash: a0b13d521821fd2d74716cc52485585feb7c51b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a>Introdução ao Azure Data Lake Analytics com APIs REST
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Saiba como toouse WebHDFS REST APIs e APIs REST do Data Lake Analytics toomanage Data Lake Analytics contas, tarefas e de catálogo. 

## <a name="prerequisites"></a>Pré-requisitos
* **Uma subscrição do Azure**. Veja [Obter versão de avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Criar uma Aplicação do Azure Active Directory**. Utilizar aplicações de análise do Data Lake de Olá aplicação tooauthenticate Olá do Azure AD com o Azure AD. Existem diferentes abordagens tooauthenticate com o Azure AD, que são **autenticação de utilizador final** ou **autenticação de serviço a serviço**. Para obter instruções e mais informações sobre como tooauthenticate, consulte [autenticar com o Data Lake Analytics com o Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).
* [cURL](http://curl.haxx.se/). Este artigo utiliza toodemonstrate cURL como chama o toomake REST API em relação a uma conta de Data Lake Analytics.

## <a name="authenticate-with-azure-active-directory"></a>Autenticar com o Azure Active Directory
Existem dois métodos para autenticar no Azure Active Directory.

### <a name="end-user-authentication-interactive"></a>Autenticação de utilizador final (interativa)
Utilizar este método, aplicação pede-lhe Olá utilizador toolog no e todas as operações de Olá são executadas no contexto de Olá do utilizador Olá. 

Siga os passos seguintes para a autenticação interativa:

1. Através da sua aplicação, redireciona Olá utilizador toohello seguinte URL:
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<REDIRECT-URI > precisa de toobe codificado para utilização num URL. Assim, para https://localhost, utilize `https%3A%2F%2Flocalhost`)
   > 
   > 
   
    Para o objetivo de Olá deste tutorial, pode substituir os valores de marcador de posição de Olá no Olá URL acima e colá-lo na barra de endereço do browser. Será redirecionado tooauthenticate utilizando o início de sessão do Azure. Depois de iniciar sessão com êxito, a resposta Olá é apresentada na barra de endereço do browser Olá. resposta Olá estarão disponíveis na Olá seguinte formato:
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. Capture o código de autorização de Olá na resposta Olá. Para este tutorial, pode copiar o código de autorização de Olá a partir da barra de endereço Olá do browser da web de Olá e transmiti-lo no Olá POST pedido toohello ponto final de tokens, conforme mostrado abaixo:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > Neste caso, Olá \<REDIRECT-URI > não tem de ser codificado.
   > 
   > 
3. resposta Olá é um objeto JSON que contém um token de acesso (por exemplo, `"access_token": "<ACCESS_TOKEN>"`) e um token de atualização (por exemplo, `"refresh_token": "<REFRESH_TOKEN>"`). A aplicação utiliza o token de acesso de Olá quando aceder ao Azure Data Lake Store e tooget de token de atualização de Olá outro token de acesso quando um token de acesso expira.
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. Quando o token de acesso de Olá expira, pode pedir um novo token de acesso utilizando o token de atualização de Olá, conforme mostrado abaixo:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

Para obter mais informações sobre a autenticação de utilizador interativa, veja [Fluxo de concessão de códigos de autorização](https://msdn.microsoft.com/library/azure/dn645542.aspx).

### <a name="service-to-service-authentication-non-interactive"></a>Autenticação serviço a serviço (não interativa)
Utilizar este método, aplicação fornece as suas próprias credenciais tooperform Olá operações. Para tal, tem de emitir um pedido POST como Olá mostrado abaixo: 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

saída de Olá deste pedido irá incluir um token de autorização (em falta por que `access-token` na saída de Olá abaixo) que irá transmitir subsequentemente com as chamadas de REST API. Guarde este token de autenticação num ficheiro de texto; irá precisar dele mais tarde neste artigo.

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

Este artigo utiliza Olá **não interativo** abordagem. Para obter mais informações sobre não interativa (chamadas serviço a serviço), consulte [chamadas tooservice utilizando as credenciais do serviço](https://msdn.microsoft.com/library/azure/dn645543.aspx).

## <a name="create-a-data-lake-analytics-account"></a>Criar uma conta de Data Lake Analytics
Tem de criar um grupo de recursos do Azure e uma conta do Data Lake Store antes de poder criar uma conta do Data Lake Analytics.  Veja [Criar uma conta do Data Lake Store](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).

Olá, como a seguir mostra de comando Curl toocreate uma conta:

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

Substitua \< `REDACTED` \> com o token de autorização de Olá, \< `AzureSubscriptionID` \> com o seu ID de subscrição, \< `AzureResourceGroupName` \> com um recurso existente do Azure Nome do grupo, e \< `NewAzureDataLakeAnalyticsAccountName` \> com um novo nome de conta do Data Lake Analytics. payload de pedido de Olá para este comando está contido no Olá **CreateDatalakeAnalyticsAccountRequest.json** ficheiro que é fornecido para Olá `-d` parâmetro acima. Olá conteúdo de Olá Input ficheiro assemelhar-se a seguinte Olá:

    {  
        "location": "East US 2",  
        "name": "myadla1004",  
        "tags": {},  
        "properties": {  
            "defaultDataLakeStoreAccount": "my1004store",  
            "dataLakeStoreAccounts": [  
                {  
                    "name": "my1004store"  
                }     
            ]
        }  
    }  


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a>Listar as contas Data Lake Analytics numa subscrição
Olá seguinte comando Curl mostra como toolist contas numa subscrição:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

Substitua \< `REDACTED` \> com o token de autorização de Olá, \< `AzureSubscriptionID` \> com o ID de subscrição. saída de Olá é semelhante a:

    {
        "value": [
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla0831.azuredatalakeanalytics.net",
                "accountId": "21e74660-0941-4880-ae72-b143c2615ea9",
                "creationTime": "2016-09-01T12:49:12.7451428Z",
                "lastModifiedTime": "2016-09-01T12:49:12.7451428Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla0831rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla0831",
            "name": "myadla0831",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            },
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla1004.azuredatalakeanalytics.net",
                "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
                "creationTime": "2016-10-04T20:46:42.287147Z",
                "lastModifiedTime": "2016-10-04T20:46:42.287147Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
            "name": "myadla1004",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            }
        ]
    }

## <a name="get-information-about-a-data-lake-analytics-account"></a>Obter informações sobre uma conta do Data Lake Analytics
Olá, como a seguir mostra de comando Curl tooget uma informações da conta:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

Substitua \< `REDACTED` \> com o token de autorização de Olá, \< `AzureSubscriptionID` \> com o seu ID de subscrição, \< `AzureResourceGroupName` \> com um recurso existente do Azure Nome do grupo, e \< `DataLakeAnalyticsAccountName` \> com o nome de Olá de uma conta existente do Data Lake Analytics. saída de Olá é semelhante a:

    {
        "properties": {
            "defaultDataLakeStoreAccount": "my1004store",
            "dataLakeStoreAccounts": [
            {
                "properties": {
                "suffix": "azuredatalakestore.net"
                },
                "name": "my1004store"
            }
            ],
            "provisioningState": "Creating",
            "state": null,
            "endpoint": null,
            "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
            "creationTime": null,
            "lastModifiedTime": null
        },
        "location": "East US 2",
        "tags": {},
        "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
        "name": "myadla1004",
        "type": "Microsoft.DataLakeAnalytics/accounts"
    }

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a>Listar os Data Lake Stores de uma conta do Data Lake Analytics
Olá seguinte comando Curl mostra como toolist Data Lake armazena de uma conta:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

Substitua \< `REDACTED` \> com o token de autorização de Olá, \< `AzureSubscriptionID` \> com o seu ID de subscrição, \< `AzureResourceGroupName` \> com um recurso existente do Azure Nome do grupo, e \< `DataLakeAnalyticsAccountName` \> com o nome de Olá de uma conta existente do Data Lake Analytics. saída de Olá é semelhante a:

    {
        "value": [
            {
            "properties": {
                "suffix": "azuredatalakestore.net"
            },
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004/dataLakeStoreAccounts/my1004store",
            "name": "my1004store",
            "type": "Microsoft.DataLakeAnalytics/accounts/dataLakeStoreAccounts"
            }
        ]
    }

## <a name="submit-u-sql-jobs"></a>Submeter tarefas U-SQL
Olá a seguir mostra de comando Curl como tarefa toosubmit U-SQL:

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

Substitua \< `REDACTED` \> com o token de autorização de Olá, \< `DataLakeAnalyticsAccountName` \> com o nome de Olá de uma conta existente do Data Lake Analytics. payload de pedido de Olá para este comando está contido no Olá **SubmitADLAJob.json** ficheiro que é fornecido para Olá `-d` parâmetro acima. Olá conteúdo de Olá Input ficheiro assemelhar-se a seguinte Olá:

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "properties": {
            "type": "USql",
            "script": "@searchlog =\n    EXTRACT UserId          int,\n            Start           DateTime,\n            Region          string,\n            Query          
        string,\n            Duration        int?,\n            Urls            string,\n            ClickedUrls     string\n    FROM \"/Samples/Data/SearchLog.tsv\"\n    US
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    too\"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

saída de Olá é semelhante a:

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "myadl@SPI",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "2016-10-05T13:54:59.9871859+00:00",
        "state": "Compiling",
        "result": "Succeeded",
        "stateAuditRecords": [
            {
            "newState": "New",
            "timeStamp": "2016-10-05T13:54:59.9871859+00:00",
            "details": "userName:myadl@SPI;submitMachine:N/A"
            }
        ],
        "properties": {
            "owner": "myadl@SPI",
            "resources": [],
            "runtimeVersion": "default",
            "rootProcessNodeId": "00000000-0000-0000-0000-000000000000",
            "algebraFilePath": "adl://myadls0831.azuredatalakestore.net/system/jobservice/jobs/Usql/2016/10/05/13/54/8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a/algebra.xml",
            "compileMode": "Semantic",
            "errorSource": "Unknown",
            "totalCompilationTime": "PT0S",
            "totalPausedTime": "PT0S",
            "totalQueuedTime": "PT0S",
            "totalRunningTime": "PT0S",
            "type": "USql"
        }
    }


## <a name="list-u-sql-jobs"></a>Listar tarefas U-SQL
Olá a seguir mostra de comando Curl como tarefas toolist U-SQL:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

Substitua \< `REDACTED` \> com o token de autorização de Olá, e \< `DataLakeAnalyticsAccountName` \> com o nome de Olá de uma conta existente do Data Lake Analytics. 

saída de Olá é semelhante a:

    {
    "value": [
        {
        "jobId": "65cf1691-9dbe-43cd-90ed-1cafbfb406fb",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someone@microsoft.com",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:46:53 GMT",
        "startTime": "Wed, 05 Oct 2016 13:47:33 GMT",
        "endTime": "Wed, 05 Oct 2016 13:48:07 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        },
        {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someoneadl@SPI",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:54:59 GMT",
        "startTime": "Wed, 05 Oct 2016 13:55:43 GMT",
        "endTime": "Wed, 05 Oct 2016 13:56:11 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        }
    ],
    "nextLink": null,
    "count": null
    }


## <a name="get-catalog-items"></a>Obter itens de catálogo
Olá seguinte comando Curl mostra como bases de dados do tooget Olá de Olá catálogo:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

saída de Olá é semelhante a:

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a>Consultar também
* toosee uma consulta mais complexa, consulte [analisar registos de site utilizando o Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).
* tooget iniciado a desenvolver aplicações U-SQL, consulte [desenvolver scripts SQL-U utilizando ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* toolearn U-SQL, consulte [introdução à linguagem de Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).
* Para tarefas de gestão, veja [Manage Azure Data Lake Analytics using Azure portal (Gerir o Azure Data Lake Analytics com o Portal do Azure)](data-lake-analytics-manage-use-portal.md).
* tooget descrição geral do Data Lake Analytics, consulte [descrição geral do Azure Data Lake Analytics](data-lake-analytics-overview.md).
* toosee Olá mesmo tutorial, utilizando outras ferramentas, clique em seletores de separador Olá no Olá parte superior da página Olá.

