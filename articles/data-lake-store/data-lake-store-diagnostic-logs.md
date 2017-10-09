---
title: "os registos de diagnóstico aaaViewing para o Azure Data Lake Store | Microsoft Docs"
description: "Compreender como toosetup e acesso os registos de diagnóstico para o Azure Data Lake Store "
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 11fbf7f517f97abdcaf809c1ebeeb51424ab2c1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a>Aceder a registos de diagnóstico para o Azure Data Lake Store
Saiba mais sobre como o registo de diagnóstico tooenable para a sua conta do Data Lake Store e o modo de registo de tooview Olá recolhidos para a sua conta.

As organizações podem ativar o registo de diagnóstico para os respetivos Azure Data Lake Store conta toocollect dados acesso os registos de auditoria que fornece informações como a lista de utilizadores que acedem aos dados Olá frequência Olá de acesso aos dados, a quantidade de dados são armazenados em Olá a conta, etc.

## <a name="prerequisites"></a>Pré-requisitos
* **Uma subscrição do Azure**. Consulte [Obter uma avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Conta do Azure Data Lake Store**. Siga as instruções de Olá em [introdução ao Azure Data Lake Store utilizando o Portal do Azure de Olá](data-lake-store-get-started-portal.md).

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a>Ativar o registo de diagnóstico para a sua conta do Data Lake Store
1. Inicie sessão no novo toohello [Portal do Azure](https://portal.azure.com).
2. Abra a sua conta do Data Lake Store e, no painel de conta do Data Lake Store, clique em **definições**e, em seguida, clique em **registos de diagnóstico**.
3. No Olá **registos de diagnóstico** painel, clique em **ative os diagnósticos**.

    ![Ativar o registo de diagnóstico](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "ativar registos de diagnóstico")

3. No Olá **diagnóstico** painel, tornar Olá seguir o registo de diagnóstico de tooconfigure de alterações.
   
    ![Ativar o registo de diagnóstico](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "ativar registos de diagnóstico")
   
   * Definir **estado** demasiado**no** tooenable registo de diagnóstico.
   * Pode escolher dados toostore/processe Olá formas diferentes.
     
        * Selecione a opção de Olá demasiado**arquivar a conta de armazenamento tooa** toostore regista tooan conta de armazenamento do Azure. Utilize esta opção se pretende que os dados de Olá tooarchive que serão processado de lote numa data posterior. Se selecionar esta opção tem de fornecer uma conta de armazenamento do Azure toosave Olá os registos.
        
        * Selecione a opção de Olá demasiado**hub de eventos do fluxo tooan** toostream registo dados tooan Hub de eventos do Azure. Provavelmente irá utilizar esta opção se tiver um processamento a jusante de pipeline de registos de entrada tooanalyze em tempo real. Se selecionar esta opção, tem de fornecer detalhes de Olá para Olá Hub de eventos do Azure que pretende toouse.

        * Selecione a opção de Olá demasiado**enviar tooLog análise** toouse Olá dados de registo do Log Analytics do Azure service tooanalyze Olá gerado. Se selecionar esta opção, tem de fornecer Olá os detalhes da área de trabalho do Olá Operations Management Suite que seria utilizar Olá efetuar análise de registos.
     
   * Especifique se pretende que os registos de auditoria tooget ou registos de pedidos ou ambos.
   * Especifique o número de Olá de dias para o qual os dados de Olá devem ser mantidos. Retenção só é aplicável se estiver a utilizar dados de registo de tooarchive de conta de armazenamento do Azure.
   * Clique em **Guardar**.

Assim que tiver ativado as definições de diagnóstico, pode ver Olá inicia sessão no Olá **os registos de diagnóstico** separador.

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a>Ver registos de diagnóstico para a sua conta do Data Lake Store
Existem duas formas tooview Olá registar dados para a sua conta do Data Lake Store.

* Da conta de Data Lake Store Olá visualizar definições
* Da conta de armazenamento do Azure de olá onde estão armazenados os dados de Olá

### <a name="using-hello-data-lake-store-settings-view"></a>Utilizar Olá ver de definições de arquivo Data Lake
1. Da sua conta do Data Lake Store **definições** painel, clique em **os registos de diagnóstico**.
   
    ![Registo de diagnóstico de vista](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "ver registos de diagnóstico") 
2. No Olá **os registos de diagnóstico** painel, deverá ver registos de Olá categorizados pelo **registos de auditoria** e **pedido registos**.
   
   * Registos de pedidos capturam todos os pedidos de API efetuados no Olá conta do Data Lake Store.
   * Registos de auditoria são semelhantes toorequest registos mas fornece uma repartição das operações de Olá a ser efetuada numa conta do Data Lake Store Olá muito mais detalhada. Por exemplo, uma chamada de API de carregamento único nos registos de pedido poderá resultar em várias operações de "Acrescentar" nos registos de auditoria Olá.
3. Clique em Olá **transferir** ligação em cada registo de entrada toodownload Olá registos.

### <a name="from-hello-azure-storage-account-that-contains-log-data"></a>De Olá conta de armazenamento do Azure que contém dados de registo
1. Abra o painel de conta de armazenamento do Azure Olá associado ao Data Lake Store para o registo e, em seguida, clique em Blobs. Olá **serviço Blob** painel apresenta uma lista de dois contentores.
   
    ![Registo de diagnóstico de vista](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "ver registos de diagnóstico")
   
   * contentor de Olá **insights-registos de auditoria** contém registos de auditoria Olá.
   * contentor de Olá **pedidos de registos insights** contém registos de Olá de pedidos.
2. Dentro destes contentores Olá registos são armazenados em Olá seguir a estrutura.
   
    ![Registo de diagnóstico de vista](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "ver registos de diagnóstico")
   
    Por exemplo, pode ser o caminho completo de Olá tooan registo de auditoria`https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`
   
    Similary, foi possível Olá caminho completo tooa pedido registo`https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`

## <a name="understand-hello-structure-of-hello-log-data"></a>Compreender a estrutura de Olá Olá de dados de registo
Olá registos de auditoria e pedido são num formato JSON. Nesta secção, observe a estrutura de Olá de JSON para o pedido e registos de auditoria.

### <a name="request-logs"></a>Registos de pedido
Eis uma entrada de exemplo no registo do Olá pedido formatada em JSON. Cada blob tem um objeto de raiz denominado **registos** que contém uma matriz de objetos de registo.

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a>Esquema de registo de pedido
| Nome | Tipo | Descrição |
| --- | --- | --- |
| hora |Cadeia |Olá timestamp (em UTC) do registo de Olá |
| resourceId |Cadeia |Olá ID do recurso de Olá que demorou a operação de colocar em |
| categoria |Cadeia |categoria do registo de Olá. Por exemplo, **pedidos**. |
| operationName |Cadeia |Nome da operação de Olá que tem sessão iniciada. Por exemplo, getfilestatus. |
| resultType |Cadeia |Estado da operação de Olá, por exemplo, 200 Olá. |
| callerIpAddress |Cadeia |endereço IP Hello do cliente de Olá efetuar Olá pedido |
| correlationId |Cadeia |Olá id do registo de Olá que pode ser utilizado toogroup em conjunto um conjunto de entradas de registo relacionados |
| identidade |Objeto |identidade de Olá que gerou o registo de Olá |
| propriedades |JSON |Consulte abaixo para obter detalhes |

#### <a name="request-log-properties-schema"></a>Esquema de propriedades de registo de pedido
| Nome | Tipo | Descrição |
| --- | --- | --- |
| httpMethod |Cadeia |Olá HTTP método utilizado para a operação de Olá. Por exemplo, GET. |
| Caminho |Cadeia |Olá caminho Olá operação estava efetuada numa |
| RequestContentLength |Int |comprimento do conteúdo do pedido HTTP de Olá Olá |
| clientRequestId |Cadeia |Olá Id que identifica exclusivamente este pedido |
| StartTime |Cadeia |hora de Olá no pedido de Olá que Olá recebido do servidor |
| endTime |Cadeia |tempo de Olá no qual Olá servidor enviou uma resposta |

### <a name="audit-logs"></a>Registos de auditoria
Eis uma entrada de exemplo no registo de auditoria formatada em JSON Olá. Cada blob tem um objeto de raiz denominado **registos** que contém uma matriz de objetos de registo

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a>Esquema de registo de auditoria
| Nome | Tipo | Descrição |
| --- | --- | --- |
| hora |Cadeia |Olá timestamp (em UTC) do registo de Olá |
| resourceId |Cadeia |Olá ID do recurso de Olá que demorou a operação de colocar em |
| categoria |Cadeia |categoria do registo de Olá. Por exemplo, **auditoria**. |
| operationName |Cadeia |Nome da operação de Olá que tem sessão iniciada. Por exemplo, getfilestatus. |
| resultType |Cadeia |Estado da operação de Olá, por exemplo, 200 Olá. |
| correlationId |Cadeia |Olá id do registo de Olá que pode ser utilizado toogroup em conjunto um conjunto de entradas de registo relacionados |
| identidade |Objeto |identidade de Olá que gerou o registo de Olá |
| propriedades |JSON |Consulte abaixo para obter detalhes |

#### <a name="audit-log-properties-schema"></a>Esquema de propriedades de registo de auditoria
| Nome | Tipo | Descrição |
| --- | --- | --- |
| StreamName |Cadeia |Olá caminho Olá operação estava efetuada numa |

## <a name="samples-tooprocess-hello-log-data"></a>Dados de registo do amostras tooprocess Olá
O Azure Data Lake Store fornece um exemplo sobre como tooprocess e analisar dados de registo Olá. Pode encontrar o exemplo de Olá em [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample). 

## <a name="see-also"></a>Consultar também
* [Descrição geral do Azure Data Lake Store](data-lake-store-overview.md)
* [Secure data in Data Lake Store (Proteger dados no Data Lake Store)](data-lake-store-secure-data.md)

