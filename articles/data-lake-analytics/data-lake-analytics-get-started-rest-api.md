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
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a><span data-ttu-id="76e36-103">Introdução ao Azure Data Lake Analytics com APIs REST</span><span class="sxs-lookup"><span data-stu-id="76e36-103">Get started with Azure Data Lake Analytics using REST APIs</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="76e36-104">Saiba como toouse WebHDFS REST APIs e APIs REST do Data Lake Analytics toomanage Data Lake Analytics contas, tarefas e de catálogo.</span><span class="sxs-lookup"><span data-stu-id="76e36-104">Learn how toouse WebHDFS REST APIs and Data Lake Analytics REST APIs toomanage Data Lake Analytics accounts, jobs, and catalog.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="76e36-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="76e36-105">Prerequisites</span></span>
* <span data-ttu-id="76e36-106">**Uma subscrição do Azure**.</span><span class="sxs-lookup"><span data-stu-id="76e36-106">**An Azure subscription**.</span></span> <span data-ttu-id="76e36-107">Veja [Obter versão de avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="76e36-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="76e36-108">**Criar uma Aplicação do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="76e36-108">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="76e36-109">Utilizar aplicações de análise do Data Lake de Olá aplicação tooauthenticate Olá do Azure AD com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76e36-109">You use hello Azure AD application tooauthenticate hello Data Lake Analytics application with Azure AD.</span></span> <span data-ttu-id="76e36-110">Existem diferentes abordagens tooauthenticate com o Azure AD, que são **autenticação de utilizador final** ou **autenticação de serviço a serviço**.</span><span class="sxs-lookup"><span data-stu-id="76e36-110">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="76e36-111">Para obter instruções e mais informações sobre como tooauthenticate, consulte [autenticar com o Data Lake Analytics com o Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="76e36-111">For instructions and more information on how tooauthenticate, see [Authenticate with Data Lake Analytics using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="76e36-112">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="76e36-112">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="76e36-113">Este artigo utiliza toodemonstrate cURL como chama o toomake REST API em relação a uma conta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="76e36-113">This article uses cURL toodemonstrate how toomake REST API calls against a Data Lake Analytics account.</span></span>

## <a name="authenticate-with-azure-active-directory"></a><span data-ttu-id="76e36-114">Autenticar com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="76e36-114">Authenticate with Azure Active Directory</span></span>
<span data-ttu-id="76e36-115">Existem dois métodos para autenticar no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="76e36-115">There are two methods for authenticating with Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="76e36-116">Autenticação de utilizador final (interativa)</span><span class="sxs-lookup"><span data-stu-id="76e36-116">End-user authentication (interactive)</span></span>
<span data-ttu-id="76e36-117">Utilizar este método, aplicação pede-lhe Olá utilizador toolog no e todas as operações de Olá são executadas no contexto de Olá do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="76e36-117">Using this method, application prompts hello user toolog in and all hello operations are performed in hello context of hello user.</span></span> 

<span data-ttu-id="76e36-118">Siga os passos seguintes para a autenticação interativa:</span><span class="sxs-lookup"><span data-stu-id="76e36-118">Follow these steps for interactive authentication:</span></span>

1. <span data-ttu-id="76e36-119">Através da sua aplicação, redireciona Olá utilizador toohello seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="76e36-119">Through your application, redirect hello user toohello following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="76e36-120">\<REDIRECT-URI > precisa de toobe codificado para utilização num URL.</span><span class="sxs-lookup"><span data-stu-id="76e36-120">\<REDIRECT-URI> needs toobe encoded for use in a URL.</span></span> <span data-ttu-id="76e36-121">Assim, para https://localhost, utilize `https%3A%2F%2Flocalhost`)</span><span class="sxs-lookup"><span data-stu-id="76e36-121">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="76e36-122">Para o objetivo de Olá deste tutorial, pode substituir os valores de marcador de posição de Olá no Olá URL acima e colá-lo na barra de endereço do browser.</span><span class="sxs-lookup"><span data-stu-id="76e36-122">For hello purpose of this tutorial, you can replace hello placeholder values in hello URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="76e36-123">Será redirecionado tooauthenticate utilizando o início de sessão do Azure.</span><span class="sxs-lookup"><span data-stu-id="76e36-123">You will be redirected tooauthenticate using your Azure login.</span></span> <span data-ttu-id="76e36-124">Depois de iniciar sessão com êxito, a resposta Olá é apresentada na barra de endereço do browser Olá.</span><span class="sxs-lookup"><span data-stu-id="76e36-124">Once you succesfully log in, hello response is displayed in hello browser's address bar.</span></span> <span data-ttu-id="76e36-125">resposta Olá estarão disponíveis na Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="76e36-125">hello response will be in hello following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="76e36-126">Capture o código de autorização de Olá na resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="76e36-126">Capture hello authorization code from hello response.</span></span> <span data-ttu-id="76e36-127">Para este tutorial, pode copiar o código de autorização de Olá a partir da barra de endereço Olá do browser da web de Olá e transmiti-lo no Olá POST pedido toohello ponto final de tokens, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="76e36-127">For this tutorial, you can copy hello authorization code from hello address bar of hello web browser and pass it in hello POST request toohello token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="76e36-128">Neste caso, Olá \<REDIRECT-URI > não tem de ser codificado.</span><span class="sxs-lookup"><span data-stu-id="76e36-128">In this case, hello \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="76e36-129">resposta Olá é um objeto JSON que contém um token de acesso (por exemplo, `"access_token": "<ACCESS_TOKEN>"`) e um token de atualização (por exemplo, `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="76e36-129">hello response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="76e36-130">A aplicação utiliza o token de acesso de Olá quando aceder ao Azure Data Lake Store e tooget de token de atualização de Olá outro token de acesso quando um token de acesso expira.</span><span class="sxs-lookup"><span data-stu-id="76e36-130">Your application uses hello access token when accessing Azure Data Lake Store and hello refresh token tooget another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="76e36-131">Quando o token de acesso de Olá expira, pode pedir um novo token de acesso utilizando o token de atualização de Olá, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="76e36-131">When hello access token expires, you can request a new access token using hello refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="76e36-132">Para obter mais informações sobre a autenticação de utilizador interativa, veja [Fluxo de concessão de códigos de autorização](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="76e36-132">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="76e36-133">Autenticação serviço a serviço (não interativa)</span><span class="sxs-lookup"><span data-stu-id="76e36-133">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="76e36-134">Utilizar este método, aplicação fornece as suas próprias credenciais tooperform Olá operações.</span><span class="sxs-lookup"><span data-stu-id="76e36-134">Using this method, application provides its own credentials tooperform hello operations.</span></span> <span data-ttu-id="76e36-135">Para tal, tem de emitir um pedido POST como Olá mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="76e36-135">For this, you must issue a POST request like hello one shown below:</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="76e36-136">saída de Olá deste pedido irá incluir um token de autorização (em falta por que `access-token` na saída de Olá abaixo) que irá transmitir subsequentemente com as chamadas de REST API.</span><span class="sxs-lookup"><span data-stu-id="76e36-136">hello output of this request will include an authorization token (denoted by `access-token` in hello output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="76e36-137">Guarde este token de autenticação num ficheiro de texto; irá precisar dele mais tarde neste artigo.</span><span class="sxs-lookup"><span data-stu-id="76e36-137">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="76e36-138">Este artigo utiliza Olá **não interativo** abordagem.</span><span class="sxs-lookup"><span data-stu-id="76e36-138">This article uses hello **non-interactive** approach.</span></span> <span data-ttu-id="76e36-139">Para obter mais informações sobre não interativa (chamadas serviço a serviço), consulte [chamadas tooservice utilizando as credenciais do serviço](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="76e36-139">For more information on non-interactive (service-to-service calls), see [Service tooservice calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="76e36-140">Criar uma conta de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="76e36-140">Create a Data Lake Analytics account</span></span>
<span data-ttu-id="76e36-141">Tem de criar um grupo de recursos do Azure e uma conta do Data Lake Store antes de poder criar uma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="76e36-141">You must create an Azure Resource group, and a Data Lake Store account before you can create a Data Lake Analytics account.</span></span>  <span data-ttu-id="76e36-142">Veja [Criar uma conta do Data Lake Store](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="76e36-142">See [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span></span>

<span data-ttu-id="76e36-143">Olá, como a seguir mostra de comando Curl toocreate uma conta:</span><span class="sxs-lookup"><span data-stu-id="76e36-143">hello following Curl command shows how toocreate an account:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

<span data-ttu-id="76e36-144">Substitua \< `REDACTED` \> com o token de autorização de Olá, \< `AzureSubscriptionID` \> com o seu ID de subscrição, \< `AzureResourceGroupName` \> com um recurso existente do Azure Nome do grupo, e \< `NewAzureDataLakeAnalyticsAccountName` \> com um novo nome de conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="76e36-144">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`NewAzureDataLakeAnalyticsAccountName`\> with a new Data Lake Analytics Account name.</span></span> <span data-ttu-id="76e36-145">payload de pedido de Olá para este comando está contido no Olá **CreateDatalakeAnalyticsAccountRequest.json** ficheiro que é fornecido para Olá `-d` parâmetro acima.</span><span class="sxs-lookup"><span data-stu-id="76e36-145">hello request payload for this command is contained in hello **CreateDatalakeAnalyticsAccountRequest.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="76e36-146">Olá conteúdo de Olá Input ficheiro assemelhar-se a seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="76e36-146">hello contents of hello input.json file resemble hello following:</span></span>

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


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a><span data-ttu-id="76e36-147">Listar as contas Data Lake Analytics numa subscrição</span><span class="sxs-lookup"><span data-stu-id="76e36-147">List Data Lake Analytics accounts in a subscription</span></span>
<span data-ttu-id="76e36-148">Olá seguinte comando Curl mostra como toolist contas numa subscrição:</span><span class="sxs-lookup"><span data-stu-id="76e36-148">hello following Curl command shows how toolist accounts in a subscription:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

<span data-ttu-id="76e36-149">Substitua \< `REDACTED` \> com o token de autorização de Olá, \< `AzureSubscriptionID` \> com o ID de subscrição.</span><span class="sxs-lookup"><span data-stu-id="76e36-149">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID.</span></span> <span data-ttu-id="76e36-150">saída de Olá é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="76e36-150">hello output is similar to:</span></span>

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

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="76e36-151">Obter informações sobre uma conta do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="76e36-151">Get information about a Data Lake Analytics account</span></span>
<span data-ttu-id="76e36-152">Olá, como a seguir mostra de comando Curl tooget uma informações da conta:</span><span class="sxs-lookup"><span data-stu-id="76e36-152">hello following Curl command shows how tooget an account information:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

<span data-ttu-id="76e36-153">Substitua \< `REDACTED` \> com o token de autorização de Olá, \< `AzureSubscriptionID` \> com o seu ID de subscrição, \< `AzureResourceGroupName` \> com um recurso existente do Azure Nome do grupo, e \< `DataLakeAnalyticsAccountName` \> com o nome de Olá de uma conta existente do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="76e36-153">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="76e36-154">saída de Olá é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="76e36-154">hello output is similar to:</span></span>

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

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a><span data-ttu-id="76e36-155">Listar os Data Lake Stores de uma conta do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="76e36-155">List Data Lake Stores of a Data Lake Analytics account</span></span>
<span data-ttu-id="76e36-156">Olá seguinte comando Curl mostra como toolist Data Lake armazena de uma conta:</span><span class="sxs-lookup"><span data-stu-id="76e36-156">hello following Curl command shows how toolist Data Lake Stores of an account:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

<span data-ttu-id="76e36-157">Substitua \< `REDACTED` \> com o token de autorização de Olá, \< `AzureSubscriptionID` \> com o seu ID de subscrição, \< `AzureResourceGroupName` \> com um recurso existente do Azure Nome do grupo, e \< `DataLakeAnalyticsAccountName` \> com o nome de Olá de uma conta existente do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="76e36-157">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="76e36-158">saída de Olá é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="76e36-158">hello output is similar to:</span></span>

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

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="76e36-159">Submeter tarefas U-SQL</span><span class="sxs-lookup"><span data-stu-id="76e36-159">Submit U-SQL jobs</span></span>
<span data-ttu-id="76e36-160">Olá a seguir mostra de comando Curl como tarefa toosubmit U-SQL:</span><span class="sxs-lookup"><span data-stu-id="76e36-160">hello following Curl command shows how toosubmit a U-SQL job:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

<span data-ttu-id="76e36-161">Substitua \< `REDACTED` \> com o token de autorização de Olá, \< `DataLakeAnalyticsAccountName` \> com o nome de Olá de uma conta existente do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="76e36-161">Replace \<`REDACTED`\> with hello authorization token, \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="76e36-162">payload de pedido de Olá para este comando está contido no Olá **SubmitADLAJob.json** ficheiro que é fornecido para Olá `-d` parâmetro acima.</span><span class="sxs-lookup"><span data-stu-id="76e36-162">hello request payload for this command is contained in hello **SubmitADLAJob.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="76e36-163">Olá conteúdo de Olá Input ficheiro assemelhar-se a seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="76e36-163">hello contents of hello input.json file resemble hello following:</span></span>

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

<span data-ttu-id="76e36-164">saída de Olá é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="76e36-164">hello output is similar to:</span></span>

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


## <a name="list-u-sql-jobs"></a><span data-ttu-id="76e36-165">Listar tarefas U-SQL</span><span class="sxs-lookup"><span data-stu-id="76e36-165">List U-SQL jobs</span></span>
<span data-ttu-id="76e36-166">Olá a seguir mostra de comando Curl como tarefas toolist U-SQL:</span><span class="sxs-lookup"><span data-stu-id="76e36-166">hello following Curl command shows how toolist U-SQL jobs:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

<span data-ttu-id="76e36-167">Substitua \< `REDACTED` \> com o token de autorização de Olá, e \< `DataLakeAnalyticsAccountName` \> com o nome de Olá de uma conta existente do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="76e36-167">Replace \<`REDACTED`\> with hello authorization token, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> 

<span data-ttu-id="76e36-168">saída de Olá é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="76e36-168">hello output is similar to:</span></span>

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


## <a name="get-catalog-items"></a><span data-ttu-id="76e36-169">Obter itens de catálogo</span><span class="sxs-lookup"><span data-stu-id="76e36-169">Get catalog items</span></span>
<span data-ttu-id="76e36-170">Olá seguinte comando Curl mostra como bases de dados do tooget Olá de Olá catálogo:</span><span class="sxs-lookup"><span data-stu-id="76e36-170">hello following Curl command shows how tooget hello databases from hello catalog:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

<span data-ttu-id="76e36-171">saída de Olá é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="76e36-171">hello output is similar to:</span></span>

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a><span data-ttu-id="76e36-172">Consultar também</span><span class="sxs-lookup"><span data-stu-id="76e36-172">See also</span></span>
* <span data-ttu-id="76e36-173">toosee uma consulta mais complexa, consulte [analisar registos de site utilizando o Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="76e36-173">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="76e36-174">tooget iniciado a desenvolver aplicações U-SQL, consulte [desenvolver scripts SQL-U utilizando ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="76e36-174">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="76e36-175">toolearn U-SQL, consulte [introdução à linguagem de Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="76e36-175">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="76e36-176">Para tarefas de gestão, veja [Manage Azure Data Lake Analytics using Azure portal (Gerir o Azure Data Lake Analytics com o Portal do Azure)](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="76e36-176">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="76e36-177">tooget descrição geral do Data Lake Analytics, consulte [descrição geral do Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="76e36-177">tooget an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="76e36-178">toosee Olá mesmo tutorial, utilizando outras ferramentas, clique em seletores de separador Olá no Olá parte superior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="76e36-178">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>

