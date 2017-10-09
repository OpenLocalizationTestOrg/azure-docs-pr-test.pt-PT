---
title: "aaaUse REST tooback cópias de segurança e restaurar as aplicações do App Service"
description: "Saiba como toouse RESTful API chama tooback cópias de segurança e restaurar uma aplicação no App Service do Azure"
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: f94d0aea-edc1-43ab-9b51-ea7375859276
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: f77bdfc7de1626d04d8d0c0e8979231ae1ced81a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a><span data-ttu-id="2637b-103">Utilize REST tooback cópias de segurança e restaurar as aplicações do App Service</span><span class="sxs-lookup"><span data-stu-id="2637b-103">Use REST tooback up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2637b-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2637b-104">PowerShell</span></span>](../app-service/app-service-powershell-backup.md)
> * [<span data-ttu-id="2637b-105">API REST</span><span class="sxs-lookup"><span data-stu-id="2637b-105">REST API</span></span>](websites-csm-backup.md)
> 
> 

<span data-ttu-id="2637b-106">[Aplicações do App Service](https://azure.microsoft.com/services/app-service/web/) pode ser feita como blobs no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2637b-106">[App Service apps](https://azure.microsoft.com/services/app-service/web/) can be backed up as blobs in Azure storage.</span></span> <span data-ttu-id="2637b-107">cópia de segurança de Olá pode também contêm bases de dados da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="2637b-107">hello backup can also contain hello app’s databases.</span></span> <span data-ttu-id="2637b-108">Se a aplicação Olá é alguma vez acidentalmente eliminada ou se Olá aplicação necessidades toobe revertido versão anterior do tooa, pode ser restaurado a partir de qualquer cópia de segurança anterior.</span><span class="sxs-lookup"><span data-stu-id="2637b-108">If hello app is ever accidentally deleted, or if hello app needs toobe reverted tooa previous version, it can be restored from any previous backup.</span></span> <span data-ttu-id="2637b-109">As cópias de segurança podem ser efetuadas em qualquer altura a pedido ou cópias de segurança podem ser agendadas em intervalos adequados.</span><span class="sxs-lookup"><span data-stu-id="2637b-109">Backups can be done at any time on demand, or backups can be scheduled at suitable intervals.</span></span>

<span data-ttu-id="2637b-110">Este artigo explica como toobackup e restauro de uma aplicação com a RESTful API pedidos.</span><span class="sxs-lookup"><span data-stu-id="2637b-110">This article explains how toobackup and restore an app with RESTful API requests.</span></span> <span data-ttu-id="2637b-111">Se seria como toocreate e gerir cópias de segurança de aplicação graficamente através de Olá portal do Azure, consulte [cópia de segurança numa aplicação web no App Service do Azure](web-sites-backup.md)</span><span class="sxs-lookup"><span data-stu-id="2637b-111">If you would like toocreate and manage app backups graphically through hello Azure portal, see [Back up a web app in Azure App Service](web-sites-backup.md)</span></span>

<a name="gettingstarted"></a>

## <a name="getting-started"></a><span data-ttu-id="2637b-112">Introdução</span><span class="sxs-lookup"><span data-stu-id="2637b-112">Getting Started</span></span>
<span data-ttu-id="2637b-113">pedidos de toosend REST, terá de tooknow da sua aplicação **nome**, **grupo de recursos**, e **id de subscrição**. Estas informações podem ser encontradas clicando a sua aplicação no Olá **do serviço de aplicações** painel de Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2637b-113">toosend REST requests, you need tooknow your app’s **name**, **resource group**, and **subscription id**. This information can be found by clicking your app in hello **App Service** blade of hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2637b-114">Para obter exemplos de Olá neste artigo, estamos a configurar Web site de Olá **backuprestoreapiexamples.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="2637b-114">For hello examples in this article, we are configuring hello website **backuprestoreapiexamples.azurewebsites.net**.</span></span> <span data-ttu-id="2637b-115">Este é armazenado no grupo de recursos de predefinição-Web-WestUS Olá e está em execução numa subscrição com Olá ID 00001111-2222-3333-4444-555566667777.</span><span class="sxs-lookup"><span data-stu-id="2637b-115">It is stored in hello Default-Web-WestUS resource group and is running on a subscription with hello ID 00001111-2222-3333-4444-555566667777.</span></span>

![Informações do Web site de exemplo][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a><span data-ttu-id="2637b-117">Cópia de segurança e restaurar a REST API</span><span class="sxs-lookup"><span data-stu-id="2637b-117">Backup and restore REST API</span></span>
<span data-ttu-id="2637b-118">Abordaremos agora vários exemplos de como toouse Olá toobackup de REST API e restaurar uma aplicação.</span><span class="sxs-lookup"><span data-stu-id="2637b-118">We will now cover several examples of how toouse hello REST API toobackup and restore an app.</span></span> <span data-ttu-id="2637b-119">Cada exemplo inclui um corpo do pedido de URL e HTTP.</span><span class="sxs-lookup"><span data-stu-id="2637b-119">Each example includes a URL and HTTP request body.</span></span> <span data-ttu-id="2637b-120">URL do exemplo Olá contém os marcadores de posição encapsuladas chavetas, por exemplo, {id de subscrição}.</span><span class="sxs-lookup"><span data-stu-id="2637b-120">hello sample URL contains placeholders wrapped in curly braces, such as {subscription-id}.</span></span> <span data-ttu-id="2637b-121">Substitua os marcadores de posição de Olá Olá correspondente informações sobre a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="2637b-121">Replace hello placeholders with hello corresponding information for your app.</span></span> <span data-ttu-id="2637b-122">Para referência, eis uma explicação de cada que aparece no URLs de exemplo de Olá marcador de posição.</span><span class="sxs-lookup"><span data-stu-id="2637b-122">For reference, here is an explanation of each placeholder that appears in hello example URLs.</span></span>

* <span data-ttu-id="2637b-123">id de subscrição – ID da aplicação de Olá contentor do Olá subscrição do Azure</span><span class="sxs-lookup"><span data-stu-id="2637b-123">subscription-id – ID of hello Azure subscription containing hello app</span></span>
* <span data-ttu-id="2637b-124">recurso--nome do grupo – nome da aplicação de Olá Olá recursos grupo contentor</span><span class="sxs-lookup"><span data-stu-id="2637b-124">resource-group-name – Name of hello resource group containing hello app</span></span>
* <span data-ttu-id="2637b-125">nome – o nome da aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="2637b-125">name – Name of hello app</span></span>
* <span data-ttu-id="2637b-126">id de cópia de segurança – ID da cópia de segurança de aplicação de Olá</span><span class="sxs-lookup"><span data-stu-id="2637b-126">backup-id – ID of hello app backup</span></span>

<span data-ttu-id="2637b-127">Para obter documentação completa Olá de Olá API, incluindo vários parâmetros opcionais que podem ser incluídos no pedido HTTP de Olá, consulte o artigo Olá [Explorador de recursos do Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2637b-127">For hello complete documentation of hello API, including several optional parameters that can be included in hello HTTP request, see hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a><span data-ttu-id="2637b-128">Cópia de segurança de uma aplicação a pedido</span><span class="sxs-lookup"><span data-stu-id="2637b-128">Backup an app on demand</span></span>
<span data-ttu-id="2637b-129">tooback se uma aplicação imediatamente, enviar uma **POST** pedido demasiado**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ cópia de segurança /**.</span><span class="sxs-lookup"><span data-stu-id="2637b-129">tooback up an app immediately, send a **POST** request too**https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.</span></span>

<span data-ttu-id="2637b-130">Eis o URL de Olá aspeto utilizar nosso site de exemplo.</span><span class="sxs-lookup"><span data-stu-id="2637b-130">Here is what hello URL looks like using our example website.</span></span> <span data-ttu-id="2637b-131">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span><span class="sxs-lookup"><span data-stu-id="2637b-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span></span>

<span data-ttu-id="2637b-132">Forneça um objeto JSON no corpo de Olá do seu toospecify de pedido que toostore de toouse de conta de armazenamento Olá cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="2637b-132">Supply a JSON object in hello body of your request toospecify which storage account toouse toostore hello backup.</span></span> <span data-ttu-id="2637b-133">um objeto JSON Olá tem de ter uma propriedade chamada **storageAccountUrl**, que contém um [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) conceder acesso de escrita toohello Storage do Azure contentor que retém blob Olá de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="2637b-133">hello JSON object must have a property named **storageAccountUrl**, which holds a [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) granting write access toohello Azure Storage container that holds hello backup blob.</span></span> <span data-ttu-id="2637b-134">Se quiser tooback cópias de segurança das bases de dados, também tem de fornecer uma lista que contém nomes de Olá, tipos e cadeias de ligação de Olá bases de dados toobe uma cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="2637b-134">If you want tooback up your databases, you must also supply a list containing hello names, types, and connection strings of hello databases toobe backed up.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        “databases”: [
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”,
                "connectionString": "<your database connection string>"
            }
        ]
    }
}
```

<span data-ttu-id="2637b-135">Uma cópia de segurança da aplicação Olá começa imediatamente quando é recebido Olá pedido.</span><span class="sxs-lookup"><span data-stu-id="2637b-135">A backup of hello app begins immediately when hello request is received.</span></span> <span data-ttu-id="2637b-136">processo de cópia de segurança de Olá pode demorar um toocomplete muito tempo.</span><span class="sxs-lookup"><span data-stu-id="2637b-136">hello backup process may take a long time toocomplete.</span></span> <span data-ttu-id="2637b-137">Olá resposta de HTTP contém um ID que pode utilizar outro pedido toosee Olá do Estado da cópia de segurança de Olá.</span><span class="sxs-lookup"><span data-stu-id="2637b-137">hello HTTP response contains an ID that you can use in another request toosee hello status of hello backup.</span></span> <span data-ttu-id="2637b-138">Eis um exemplo do corpo de Olá de pedido de tooour de resposta HTTP do Olá cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="2637b-138">Here is an example of hello body of hello HTTP response tooour backup request.</span></span>

```
{
    "id": "/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples",
    "name": " backuprestoreapiexamples ",
    "type": "Microsoft.Web/sites",
    "location": "WestUS",
    "properties":    {
        "id": 1,
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        "blobName": “backup_201509291825.zip”,
        "name": "backup_201509291825",
        "status": 4,
        "sizeInBytes": 0,
        "created": "2015-09-29T18:25:26.3992707Z",
        "log": null,
        "databases": [
            {
                "databaseType": "SqlAzure",
                "name": "MyDatabase1",
                "connectionString": "<your database connection string>"
            }
        ],
        "scheduled": false,
        "correlationId": "ea730f4d-dd06-4f7f-a090-9aa09k662h36",
    }
}
```

> [!NOTE]
> <span data-ttu-id="2637b-139">Mensagens de erro podem ser encontradas na propriedade de registo de Olá da Olá resposta de HTTP.</span><span class="sxs-lookup"><span data-stu-id="2637b-139">Error messages can be found in hello log property of hello HTTP response.</span></span>
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a><span data-ttu-id="2637b-140">Agendar cópias de segurança automáticas</span><span class="sxs-lookup"><span data-stu-id="2637b-140">Schedule automatic backups</span></span>
<span data-ttu-id="2637b-141">Na adição toobacking se uma aplicação a pedido, também pode agendar uma cópia de segurança toohappen automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2637b-141">In addition toobacking up an app on demand, you can also schedule a backup toohappen automatically.</span></span>

### <a name="set-up-a-new-automatic-backup-schedule"></a><span data-ttu-id="2637b-142">Configurar uma nova agenda de cópia de segurança automática</span><span class="sxs-lookup"><span data-stu-id="2637b-142">Set up a new automatic backup schedule</span></span>
<span data-ttu-id="2637b-143">Enviar tooset de uma agenda de cópia de segurança, um **colocar** pedido demasiado**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config / cópia de segurança**.</span><span class="sxs-lookup"><span data-stu-id="2637b-143">tooset up a backup schedule, send a **PUT** request too**https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.</span></span>

<span data-ttu-id="2637b-144">Eis o aspeto Olá URL para o Web site nosso exemplo.</span><span class="sxs-lookup"><span data-stu-id="2637b-144">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="2637b-145">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span><span class="sxs-lookup"><span data-stu-id="2637b-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span></span>

<span data-ttu-id="2637b-146">corpo do pedido Olá tem de ter um objeto JSON que especifica a configuração de cópia de segurança de Olá.</span><span class="sxs-lookup"><span data-stu-id="2637b-146">hello request body must have a JSON object that specifies hello backup configuration.</span></span> <span data-ttu-id="2637b-147">Eis um exemplo com todos os parâmetros de Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="2637b-147">Here is an example with all hello required parameters.</span></span>

```
{
    "location": "WestUS",
    "properties": // Represents an app restore request
    {
        "backupSchedule": { // Required for automatically scheduled backups
            "frequencyInterval": "7",
            "frequencyUnit": "Day",
            "keepAtLeastOneBackup": "True",
            "retentionPeriodInDays": "10",
        },
        "enabled": "True", // Must be set tootrue tooenable automatic backups
        "name": “mysitebackup”,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

<span data-ttu-id="2637b-148">Este exemplo configura Olá aplicação toobe automaticamente uma cópia de segurança a cada sete dias.</span><span class="sxs-lookup"><span data-stu-id="2637b-148">This example configures hello app toobe automatically backed up every seven days.</span></span> <span data-ttu-id="2637b-149">Olá parâmetros **frequencyInterval** e **frequencyUnit** em conjunto determinam frequência hello cópias de segurança ocorrem.</span><span class="sxs-lookup"><span data-stu-id="2637b-149">hello parameters **frequencyInterval** and **frequencyUnit** together determine how often hello backups happen.</span></span> <span data-ttu-id="2637b-150">Os valores válidos para **frequencyUnit** são **hora** e **dia**.</span><span class="sxs-lookup"><span data-stu-id="2637b-150">Valid values for **frequencyUnit** are **hour** and **day**.</span></span> <span data-ttu-id="2637b-151">Por exemplo, tooback se uma aplicação a cada 12 horas, defina frequencyInterval too12 e frequencyUnit toohour.</span><span class="sxs-lookup"><span data-stu-id="2637b-151">For example, tooback up an app every 12 hours, set frequencyInterval too12 and frequencyUnit toohour.</span></span>

<span data-ttu-id="2637b-152">Cópias de segurança antigas são automaticamente removidas da conta de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="2637b-152">Old backups are automatically removed from hello storage account.</span></span> <span data-ttu-id="2637b-153">Pode controlar Olá antiguidade, as cópias de segurança podem ser através da definição Olá **retentionPeriodInDays** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="2637b-153">You can control how old hello backups can be by setting hello **retentionPeriodInDays** parameter.</span></span> <span data-ttu-id="2637b-154">Se quiser tooalways ter, pelo menos, uma cópia de segurança guardada, independentemente de como antigo defini-lo como for, **keepAtLeastOneBackup** tootrue.</span><span class="sxs-lookup"><span data-stu-id="2637b-154">If you want tooalways have at least one backup saved, regardless of how old it is, set **keepAtLeastOneBackup** tootrue.</span></span>

### <a name="get-hello-automatic-backup-schedule"></a><span data-ttu-id="2637b-155">Obter a agenda de cópia de segurança automática Olá</span><span class="sxs-lookup"><span data-stu-id="2637b-155">Get hello automatic backup schedule</span></span>
<span data-ttu-id="2637b-156">da tooget uma aplicação configuração de cópia de segurança, enviar uma **POST** toohello URL de pedido **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ sites / {nome} / cópia de segurança/config/lista**.</span><span class="sxs-lookup"><span data-stu-id="2637b-156">tooget an app’s backup configuration, send a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.</span></span>

<span data-ttu-id="2637b-157">o URL para o nosso site de exemplo Olá é **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span><span class="sxs-lookup"><span data-stu-id="2637b-157">hello URL for our example site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span></span>

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a><span data-ttu-id="2637b-158">Obter o estado de Olá de uma cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="2637b-158">Get hello status of a backup</span></span>
<span data-ttu-id="2637b-159">Dependendo de como grandes Olá aplicação é, uma cópia de segurança poderá demorar algum tempo toocomplete.</span><span class="sxs-lookup"><span data-stu-id="2637b-159">Depending on how large hello app is, a backup may take a while toocomplete.</span></span> <span data-ttu-id="2637b-160">As cópias de segurança poderão também falhar, o limite de tempo, ou parcialmente concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="2637b-160">Backups might also fail, time out, or partially succeed.</span></span> <span data-ttu-id="2637b-161">enviar estado de Olá toosee de cópias de segurança de todos os uma aplicação, um **obter** toohello URL de pedido **https://management.azure.com/subscriptions/ {id de subscrição} /resourceGroups/ {nome de grupo de recursos} /providers/ Microsoft.Web/sites/{name}/backups**.</span><span class="sxs-lookup"><span data-stu-id="2637b-161">toosee hello status of all an app’s backups, send a **GET** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.</span></span>

<span data-ttu-id="2637b-162">Estado de Olá toosee de uma cópia de segurança específica, envie um URL de toohello pedido GET **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ { id de cópia de segurança}**.</span><span class="sxs-lookup"><span data-stu-id="2637b-162">toosee hello status of a specific backup, send a GET request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="2637b-163">Eis o aspeto Olá URL para o Web site nosso exemplo.</span><span class="sxs-lookup"><span data-stu-id="2637b-163">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="2637b-164">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="2637b-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<span data-ttu-id="2637b-165">corpo da resposta Olá contém um exemplo toothis da semelhante de objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="2637b-165">hello response body contains a JSON object similar toothis example.</span></span>

```
{
    "properties":  {
        "id": 1,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl",
        "blobName": "backup_201509291734.zip",
        "name": "backup_201509291734",
        "status": 2,
        "sizeInBytes": 151973,
        "created": "2015-09-29T17:34:57.2091605",
        "scheduled": false,
        "lastRestoreTimeStamp": null,
        "finishedTimeStamp": "2015-09-29T17:35:11.3293602",
        "correlationId": "2379fc13-418a-4b9c-920d-d06e73c5028d",
        "websiteSizeInBytes": 209920
    }
}
```

<span data-ttu-id="2637b-166">Estado de Olá de uma cópia de segurança é um tipo enumerado.</span><span class="sxs-lookup"><span data-stu-id="2637b-166">hello status of a backup is an enumerated type.</span></span> <span data-ttu-id="2637b-167">Segue-se cada Estado possíveis.</span><span class="sxs-lookup"><span data-stu-id="2637b-167">Here is every possible state.</span></span>

* <span data-ttu-id="2637b-168">0 – em curso: cópia de segurança de Olá tiver sido iniciada mas ainda não foi concluído.</span><span class="sxs-lookup"><span data-stu-id="2637b-168">0 – InProgress: hello backup has been started but has not yet completed.</span></span>
* <span data-ttu-id="2637b-169">1 – falhou: cópia de segurança de Olá teve êxito.</span><span class="sxs-lookup"><span data-stu-id="2637b-169">1 – Failed: hello backup was unsuccessful.</span></span>
* <span data-ttu-id="2637b-170">2 – criada com êxito: Olá cópia de segurança foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="2637b-170">2 – Succeeded: hello backup completed successfully.</span></span>
* <span data-ttu-id="2637b-171">3 – ServiceHost: cópia de segurança de Olá não foi concluída no tempo e foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="2637b-171">3 – TimedOut: hello backup did not finish in time and was canceled.</span></span>
* <span data-ttu-id="2637b-172">4 – criado: pedido de cópia de segurança de Olá é colocada na fila, mas não foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="2637b-172">4 – Created: hello backup request is queued but has not been started.</span></span>
* <span data-ttu-id="2637b-173">5 – ignorada: cópia de segurança de Olá não continuar devido a agenda de tooa acionar demasiadas cópias de segurança.</span><span class="sxs-lookup"><span data-stu-id="2637b-173">5 – Skipped: hello backup did not proceed due tooa schedule triggering too many backups.</span></span>
* <span data-ttu-id="2637b-174">6 – PartiallySucceeded: cópia de segurança de Olá êxito, mas alguns ficheiros não foram efetuou cópia de segurança porque não foi possível ler.</span><span class="sxs-lookup"><span data-stu-id="2637b-174">6 – PartiallySucceeded: hello backup succeeded, but some files were not backed up because they could not be read.</span></span> <span data-ttu-id="2637b-175">Normalmente, isto acontece porque um bloqueio exclusivo foi colocado em ficheiros Olá.</span><span class="sxs-lookup"><span data-stu-id="2637b-175">This usually happens because an exclusive lock was placed on hello files.</span></span>
* <span data-ttu-id="2637b-176">7 – DeleteInProgress: cópia de segurança de Olá foi pedida toobe eliminada, mas ainda não foi eliminada.</span><span class="sxs-lookup"><span data-stu-id="2637b-176">7 – DeleteInProgress: hello backup has been requested toobe deleted, but has not yet been deleted.</span></span>
* <span data-ttu-id="2637b-177">8 – DeleteFailed: não foi possível eliminar a cópia de segurança de Olá.</span><span class="sxs-lookup"><span data-stu-id="2637b-177">8 – DeleteFailed: hello backup could not be deleted.</span></span> <span data-ttu-id="2637b-178">Isto pode acontecer porque Olá URL de SAS que estava a cópia de segurança do toocreate utilizados Olá expirou.</span><span class="sxs-lookup"><span data-stu-id="2637b-178">This might happen because hello SAS URL that was used toocreate hello backup has expired.</span></span>
* <span data-ttu-id="2637b-179">9 – eliminados: cópia de segurança de Olá foi eliminada com êxito.</span><span class="sxs-lookup"><span data-stu-id="2637b-179">9 – Deleted: hello backup was deleted successfully.</span></span>

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a><span data-ttu-id="2637b-180">Restaurar uma aplicação a partir de uma cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="2637b-180">Restore an app from a backup</span></span>
<span data-ttu-id="2637b-181">Se a aplicação foi eliminada, ou se quiser toorevert a versão anterior do tooa de aplicação, pode restaurar Olá aplicação a partir de uma cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="2637b-181">If your app has been deleted, or if you want toorevert your app tooa previous version, you can restore hello app from a backup.</span></span> <span data-ttu-id="2637b-182">tooinvoke um restauro, enviar uma **POST** toohello URL de pedido **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ as cópias de segurança / {id de cópia de segurança} / restaurar**.</span><span class="sxs-lookup"><span data-stu-id="2637b-182">tooinvoke a restore, send a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.</span></span>

<span data-ttu-id="2637b-183">Eis o aspeto Olá URL para o Web site nosso exemplo.</span><span class="sxs-lookup"><span data-stu-id="2637b-183">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="2637b-184">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/Restore**</span><span class="sxs-lookup"><span data-stu-id="2637b-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span></span>

<span data-ttu-id="2637b-185">No corpo do pedido de Olá, envie um objeto JSON que contém as propriedades de Olá para a operação de restauro Olá.</span><span class="sxs-lookup"><span data-stu-id="2637b-185">In hello request body, send a JSON object that contains hello properties for hello restore operation.</span></span> <span data-ttu-id="2637b-186">Eis um exemplo que contém todas as propriedades necessárias:</span><span class="sxs-lookup"><span data-stu-id="2637b-186">Here is an example containing all required properties:</span></span>

```
{
    "location": "WestUS",
    "properties":
    {
        "blobName": "backup_201509280431.zip",
        "databases": [ // Not required unless you’re restoring databases
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”
        }],
        "overwrite": "true",
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl" // SAS URL toostorage container containing your website backup
    }
}
```

### <a name="restore-tooa-new-app"></a><span data-ttu-id="2637b-187">Restaurar tooa nova aplicação</span><span class="sxs-lookup"><span data-stu-id="2637b-187">Restore tooa new app</span></span>
<span data-ttu-id="2637b-188">Por vezes, pode querer toocreate uma nova aplicação ao restaurar uma cópia de segurança, em vez de substituir uma aplicação já existente.</span><span class="sxs-lookup"><span data-stu-id="2637b-188">Sometimes you might want toocreate a new app when you restore a backup, instead of overwriting an already existing app.</span></span> <span data-ttu-id="2637b-189">toodo, alteração Olá pedido URL toopoint toohello nova aplicação que pretende toocreate e alterar Olá **substituir** propriedade no Olá JSON demasiado**falso**.</span><span class="sxs-lookup"><span data-stu-id="2637b-189">toodo this, change hello request URL toopoint toohello new app you want toocreate, and change hello **overwrite** property in hello JSON too**false**.</span></span>

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a><span data-ttu-id="2637b-190">Eliminar uma cópia de segurança da aplicação</span><span class="sxs-lookup"><span data-stu-id="2637b-190">Delete an app backup</span></span>
<span data-ttu-id="2637b-191">Se quiser toodelete uma cópia de segurança, envie um **eliminar** toohello URL de pedido **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ sites / {nome} /backups/ {id de cópia de segurança}**.</span><span class="sxs-lookup"><span data-stu-id="2637b-191">If you would like toodelete a backup, send a **DELETE** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="2637b-192">Eis o aspeto Olá URL para o Web site nosso exemplo.</span><span class="sxs-lookup"><span data-stu-id="2637b-192">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="2637b-193">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="2637b-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a><span data-ttu-id="2637b-194">Gerir o URL de SAS de uma cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="2637b-194">Manage a backup’s SAS URL</span></span>
<span data-ttu-id="2637b-195">App Service do Azure tentará toodelete a cópia de segurança do armazenamento do Azure utilizando Olá URL de SAS que foi fornecido quando a cópia de segurança de Olá foi criada.</span><span class="sxs-lookup"><span data-stu-id="2637b-195">Azure App Service will attempt toodelete your backup from Azure Storage using hello SAS URL that was provided when hello backup was created.</span></span> <span data-ttu-id="2637b-196">Se este URL SAS já não é válido, a cópia de segurança de Olá não pode ser eliminada através de Olá REST API.</span><span class="sxs-lookup"><span data-stu-id="2637b-196">If this SAS URL is no longer valid, hello backup cannot be deleted through hello REST API.</span></span> <span data-ttu-id="2637b-197">No entanto, pode atualizar Olá SAS URL associado com uma cópia de segurança, enviando um **POST** toohello URL de pedido **/resourceGroups/ https://management.azure.com/subscriptions/ {id de subscrição} {nome de grupo de recursos} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span><span class="sxs-lookup"><span data-stu-id="2637b-197">However, you can update hello SAS URL associated with a backup by sending a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span></span>

<span data-ttu-id="2637b-198">Eis o aspeto Olá URL para o Web site nosso exemplo.</span><span class="sxs-lookup"><span data-stu-id="2637b-198">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="2637b-199">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/List**</span><span class="sxs-lookup"><span data-stu-id="2637b-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span></span>

<span data-ttu-id="2637b-200">No corpo do pedido de Olá, envie um objeto JSON que contém Olá novo URL de SAS.</span><span class="sxs-lookup"><span data-stu-id="2637b-200">In hello request body, send a JSON object that contains hello new SAS URL.</span></span> <span data-ttu-id="2637b-201">Eis um exemplo.</span><span class="sxs-lookup"><span data-stu-id="2637b-201">Here is an example.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> <span data-ttu-id="2637b-202">Por motivos de segurança, Olá que SAs URL associado a uma cópia de segurança não é devolvido ao enviar um pedido GET para uma cópia de segurança específica.</span><span class="sxs-lookup"><span data-stu-id="2637b-202">For security reasons, hello SAS URL associated with a backup is not returned when sending a GET request for a specific backup.</span></span> <span data-ttu-id="2637b-203">Se quiser Olá tooview SAS URL associado a uma cópia de segurança, envie um toohello de pedido POST mesmo URL acima.</span><span class="sxs-lookup"><span data-stu-id="2637b-203">If you want tooview hello SAS URL associated with a backup, send a POST request toohello same URL above.</span></span> <span data-ttu-id="2637b-204">Inclua um objeto JSON vazio no corpo do pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="2637b-204">Include an empty JSON object in hello request body.</span></span> <span data-ttu-id="2637b-205">resposta de Hello do servidor de Olá contém todas as informações da cópia de segurança, incluindo o respetivo URL SAS.</span><span class="sxs-lookup"><span data-stu-id="2637b-205">hello response from hello server contains all of that backup’s information, including its SAS URL.</span></span>
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
