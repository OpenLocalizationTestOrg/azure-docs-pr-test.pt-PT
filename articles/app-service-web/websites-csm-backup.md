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
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a>Utilize REST tooback cópias de segurança e restaurar as aplicações do App Service
> [!div class="op_single_selector"]
> * [PowerShell](../app-service/app-service-powershell-backup.md)
> * [API REST](websites-csm-backup.md)
> 
> 

[Aplicações do App Service](https://azure.microsoft.com/services/app-service/web/) pode ser feita como blobs no armazenamento do Azure. cópia de segurança de Olá pode também contêm bases de dados da aplicação Olá. Se a aplicação Olá é alguma vez acidentalmente eliminada ou se Olá aplicação necessidades toobe revertido versão anterior do tooa, pode ser restaurado a partir de qualquer cópia de segurança anterior. As cópias de segurança podem ser efetuadas em qualquer altura a pedido ou cópias de segurança podem ser agendadas em intervalos adequados.

Este artigo explica como toobackup e restauro de uma aplicação com a RESTful API pedidos. Se seria como toocreate e gerir cópias de segurança de aplicação graficamente através de Olá portal do Azure, consulte [cópia de segurança numa aplicação web no App Service do Azure](web-sites-backup.md)

<a name="gettingstarted"></a>

## <a name="getting-started"></a>Introdução
pedidos de toosend REST, terá de tooknow da sua aplicação **nome**, **grupo de recursos**, e **id de subscrição**. Estas informações podem ser encontradas clicando a sua aplicação no Olá **do serviço de aplicações** painel de Olá [portal do Azure](https://portal.azure.com). Para obter exemplos de Olá neste artigo, estamos a configurar Web site de Olá **backuprestoreapiexamples.azurewebsites.net**. Este é armazenado no grupo de recursos de predefinição-Web-WestUS Olá e está em execução numa subscrição com Olá ID 00001111-2222-3333-4444-555566667777.

![Informações do Web site de exemplo][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a>Cópia de segurança e restaurar a REST API
Abordaremos agora vários exemplos de como toouse Olá toobackup de REST API e restaurar uma aplicação. Cada exemplo inclui um corpo do pedido de URL e HTTP. URL do exemplo Olá contém os marcadores de posição encapsuladas chavetas, por exemplo, {id de subscrição}. Substitua os marcadores de posição de Olá Olá correspondente informações sobre a sua aplicação. Para referência, eis uma explicação de cada que aparece no URLs de exemplo de Olá marcador de posição.

* id de subscrição – ID da aplicação de Olá contentor do Olá subscrição do Azure
* recurso--nome do grupo – nome da aplicação de Olá Olá recursos grupo contentor
* nome – o nome da aplicação Olá
* id de cópia de segurança – ID da cópia de segurança de aplicação de Olá

Para obter documentação completa Olá de Olá API, incluindo vários parâmetros opcionais que podem ser incluídos no pedido HTTP de Olá, consulte o artigo Olá [Explorador de recursos do Azure](https://resources.azure.com/).

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a>Cópia de segurança de uma aplicação a pedido
tooback se uma aplicação imediatamente, enviar uma **POST** pedido demasiado**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ cópia de segurança /**.

Eis o URL de Olá aspeto utilizar nosso site de exemplo. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**

Forneça um objeto JSON no corpo de Olá do seu toospecify de pedido que toostore de toouse de conta de armazenamento Olá cópia de segurança. um objeto JSON Olá tem de ter uma propriedade chamada **storageAccountUrl**, que contém um [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) conceder acesso de escrita toohello Storage do Azure contentor que retém blob Olá de cópia de segurança. Se quiser tooback cópias de segurança das bases de dados, também tem de fornecer uma lista que contém nomes de Olá, tipos e cadeias de ligação de Olá bases de dados toobe uma cópia de segurança.

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

Uma cópia de segurança da aplicação Olá começa imediatamente quando é recebido Olá pedido. processo de cópia de segurança de Olá pode demorar um toocomplete muito tempo. Olá resposta de HTTP contém um ID que pode utilizar outro pedido toosee Olá do Estado da cópia de segurança de Olá. Eis um exemplo do corpo de Olá de pedido de tooour de resposta HTTP do Olá cópia de segurança.

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
> Mensagens de erro podem ser encontradas na propriedade de registo de Olá da Olá resposta de HTTP.
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a>Agendar cópias de segurança automáticas
Na adição toobacking se uma aplicação a pedido, também pode agendar uma cópia de segurança toohappen automaticamente.

### <a name="set-up-a-new-automatic-backup-schedule"></a>Configurar uma nova agenda de cópia de segurança automática
Enviar tooset de uma agenda de cópia de segurança, um **colocar** pedido demasiado**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config / cópia de segurança**.

Eis o aspeto Olá URL para o Web site nosso exemplo. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**

corpo do pedido Olá tem de ter um objeto JSON que especifica a configuração de cópia de segurança de Olá. Eis um exemplo com todos os parâmetros de Olá necessário.

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

Este exemplo configura Olá aplicação toobe automaticamente uma cópia de segurança a cada sete dias. Olá parâmetros **frequencyInterval** e **frequencyUnit** em conjunto determinam frequência hello cópias de segurança ocorrem. Os valores válidos para **frequencyUnit** são **hora** e **dia**. Por exemplo, tooback se uma aplicação a cada 12 horas, defina frequencyInterval too12 e frequencyUnit toohour.

Cópias de segurança antigas são automaticamente removidas da conta de armazenamento Olá. Pode controlar Olá antiguidade, as cópias de segurança podem ser através da definição Olá **retentionPeriodInDays** parâmetro. Se quiser tooalways ter, pelo menos, uma cópia de segurança guardada, independentemente de como antigo defini-lo como for, **keepAtLeastOneBackup** tootrue.

### <a name="get-hello-automatic-backup-schedule"></a>Obter a agenda de cópia de segurança automática Olá
da tooget uma aplicação configuração de cópia de segurança, enviar uma **POST** toohello URL de pedido **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ sites / {nome} / cópia de segurança/config/lista**.

o URL para o nosso site de exemplo Olá é **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a>Obter o estado de Olá de uma cópia de segurança
Dependendo de como grandes Olá aplicação é, uma cópia de segurança poderá demorar algum tempo toocomplete. As cópias de segurança poderão também falhar, o limite de tempo, ou parcialmente concluída com êxito. enviar estado de Olá toosee de cópias de segurança de todos os uma aplicação, um **obter** toohello URL de pedido **https://management.azure.com/subscriptions/ {id de subscrição} /resourceGroups/ {nome de grupo de recursos} /providers/ Microsoft.Web/sites/{name}/backups**.

Estado de Olá toosee de uma cópia de segurança específica, envie um URL de toohello pedido GET **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ { id de cópia de segurança}**.

Eis o aspeto Olá URL para o Web site nosso exemplo. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

corpo da resposta Olá contém um exemplo toothis da semelhante de objeto JSON.

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

Estado de Olá de uma cópia de segurança é um tipo enumerado. Segue-se cada Estado possíveis.

* 0 – em curso: cópia de segurança de Olá tiver sido iniciada mas ainda não foi concluído.
* 1 – falhou: cópia de segurança de Olá teve êxito.
* 2 – criada com êxito: Olá cópia de segurança foi concluída com êxito.
* 3 – ServiceHost: cópia de segurança de Olá não foi concluída no tempo e foi cancelada.
* 4 – criado: pedido de cópia de segurança de Olá é colocada na fila, mas não foi iniciado.
* 5 – ignorada: cópia de segurança de Olá não continuar devido a agenda de tooa acionar demasiadas cópias de segurança.
* 6 – PartiallySucceeded: cópia de segurança de Olá êxito, mas alguns ficheiros não foram efetuou cópia de segurança porque não foi possível ler. Normalmente, isto acontece porque um bloqueio exclusivo foi colocado em ficheiros Olá.
* 7 – DeleteInProgress: cópia de segurança de Olá foi pedida toobe eliminada, mas ainda não foi eliminada.
* 8 – DeleteFailed: não foi possível eliminar a cópia de segurança de Olá. Isto pode acontecer porque Olá URL de SAS que estava a cópia de segurança do toocreate utilizados Olá expirou.
* 9 – eliminados: cópia de segurança de Olá foi eliminada com êxito.

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a>Restaurar uma aplicação a partir de uma cópia de segurança
Se a aplicação foi eliminada, ou se quiser toorevert a versão anterior do tooa de aplicação, pode restaurar Olá aplicação a partir de uma cópia de segurança. tooinvoke um restauro, enviar uma **POST** toohello URL de pedido **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ as cópias de segurança / {id de cópia de segurança} / restaurar**.

Eis o aspeto Olá URL para o Web site nosso exemplo. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/Restore**

No corpo do pedido de Olá, envie um objeto JSON que contém as propriedades de Olá para a operação de restauro Olá. Eis um exemplo que contém todas as propriedades necessárias:

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

### <a name="restore-tooa-new-app"></a>Restaurar tooa nova aplicação
Por vezes, pode querer toocreate uma nova aplicação ao restaurar uma cópia de segurança, em vez de substituir uma aplicação já existente. toodo, alteração Olá pedido URL toopoint toohello nova aplicação que pretende toocreate e alterar Olá **substituir** propriedade no Olá JSON demasiado**falso**.

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a>Eliminar uma cópia de segurança da aplicação
Se quiser toodelete uma cópia de segurança, envie um **eliminar** toohello URL de pedido **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ sites / {nome} /backups/ {id de cópia de segurança}**.

Eis o aspeto Olá URL para o Web site nosso exemplo. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a>Gerir o URL de SAS de uma cópia de segurança
App Service do Azure tentará toodelete a cópia de segurança do armazenamento do Azure utilizando Olá URL de SAS que foi fornecido quando a cópia de segurança de Olá foi criada. Se este URL SAS já não é válido, a cópia de segurança de Olá não pode ser eliminada através de Olá REST API. No entanto, pode atualizar Olá SAS URL associado com uma cópia de segurança, enviando um **POST** toohello URL de pedido **/resourceGroups/ https://management.azure.com/subscriptions/ {id de subscrição} {nome de grupo de recursos} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.

Eis o aspeto Olá URL para o Web site nosso exemplo. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/List**

No corpo do pedido de Olá, envie um objeto JSON que contém Olá novo URL de SAS. Eis um exemplo.

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> Por motivos de segurança, Olá que SAs URL associado a uma cópia de segurança não é devolvido ao enviar um pedido GET para uma cópia de segurança específica. Se quiser Olá tooview SAS URL associado a uma cópia de segurança, envie um toohello de pedido POST mesmo URL acima. Inclua um objeto JSON vazio no corpo do pedido de Olá. resposta de Hello do servidor de Olá contém todas as informações da cópia de segurança, incluindo o respetivo URL SAS.
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
