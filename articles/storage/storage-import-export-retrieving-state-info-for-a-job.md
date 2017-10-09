---
title: "informações de estado de aaaRetrieving para uma tarefa de importação/exportação do Azure | Microsoft Docs"
description: "Saiba como tooobtain Estado informações para as tarefas do serviço de importação/exportação do Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 22d7e5f0-94da-49b4-a1ac-dd4c14a423c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: muralikk
ms.openlocfilehash: cbc35660519573d92f641924ac0025c9e577d69b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="retrieving-state-information-for-an-importexport-job"></a>A obtenção de informações de estado para uma tarefa de importação/exportação
Pode chamar Olá [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operação tooretrieve sobre ambos importar e exportar tarefas. informações de Olá devolvidas incluem:

-   estado atual Olá da tarefa de Olá.

-   percentagem de aproximado Olá que cada tarefa foi concluída.

-   Estado de Olá atual de cada unidade.

-   URIs para blobs que contém os registos de erros e informações de registo verboso (se estiver ativada).

Olá secções seguintes explicam as informações de Olá devolvidas pelo Olá `Get Job` operação.

## <a name="job-states"></a>Estados de tarefa
tabela de Olá e diagrama de estado de Olá abaixo descrevem Olá Estados que uma tarefa passa através de durante o ciclo de vida. estado atual do Olá da tarefa de Olá pode ser determinado ao chamar Olá `Get Job` operação.

![JobStates](./media/storage-import-export-retrieving-state-info-for-a-job/JobStates.png "JobStates")

Olá tabela seguinte descreve cada Estado de uma tarefa pode pass-through.

|Estado da tarefa|Descrição|
|---------------|-----------------|
|`Creating`|Depois de chamar a operação de colocar a tarefa de Olá, é criada uma tarefa e o estado estiver definido demasiado`Creating`. Enquanto a tarefa de Olá está em Olá `Creating` Estado, Olá serviço importar/exportar assume Olá unidades não foram fornecidos toohello Centro de dados. Uma tarefa pode permanecer na Olá `Creating` estado para cima tootwo semanas, após o qual é automaticamente eliminado pelo serviço de Olá.<br /><br /> Se chamar a operação de propriedades da tarefa de atualização de Olá enquanto a tarefa de Olá está em Olá `Creating` Estado, a tarefa de Olá permanece no Olá `Creating` estado e Olá tempo limite de intervalo é de reposição tootwo semanas.|
|`Shipping`|Depois de enviar o pacote, deve chamar Olá atualizar propriedades da tarefa operação Olá estado de atualização de tarefa Olá demasiado`Shipping`. Estado de envio de Olá pode ser definido apenas se hello `DeliveryPackage` (postal carrier e número de controlo) e Olá `ReturnAddress` propriedades foram definidas para a tarefa de Olá.<br /><br /> tarefa de Olá permanecerá no estado de envio de Olá para cópia de segurança tootwo semanas. Se duas semanas passaram e Olá unidades não foram recebidas, operadores de serviço de importação/exportação Olá serão notificados.|
|`Received`|Depois de todas as unidades foram recebidas no Centro de dados de Olá, irá definir estado da tarefa Olá toohello Estado Received.|
|`Transferring`|Depois de unidades de Olá foram recebidas no Centro de dados de Olá e pelo menos uma unidade começou a processar, estado da tarefa Olá será definido toohello `Transferring` estado. Consulte Olá `Drive States` secção abaixo para obter informações detalhadas.|
|`Packaging`|Depois de todas as unidades concluiu o processamento, tarefa Olá será colocada no Olá `Packaging` até Olá unidades são fornecidos toohello back-cliente de estado.|
|`Completed`|Depois de todas as unidades de terem sido fornecidos back toohello cliente, se a tarefa de Olá tiver sido concluída sem erros, em seguida, a tarefa de Olá será definida toohello `Completed` estado. Olá tarefa será eliminada automaticamente após 90 dias no Olá `Completed` estado.|
|`Closed`|Depois de todas as unidades de terem sido fornecidos back toohello cliente, se tiverem sido erros durante o processamento de Olá da tarefa de Olá, em seguida, a tarefa de Olá será definida toohello `Closed` estado. Olá tarefa será eliminada automaticamente após 90 dias no Olá `Closed` estado.|

Pode cancelar uma tarefa apenas em determinados Estados. Uma tarefa cancelada ignore o passo de cópia de dados de Olá mas, caso contrário, segue Olá mesmo transições de estado como uma tarefa que não foi cancelada.

Olá seguinte tabela descreve os erros que podem ocorrer para cada Estado da tarefa, bem como o efeito de Olá na tarefa de Olá quando ocorre um erro.

|Estado da tarefa|Evento|Resolução / próximos passos|
|---------------|-----------|------------------------------|
|`Creating or Undefined`|Chegaram uma ou mais unidades para uma tarefa, mas não está em Olá tarefa de Olá `Shipping` Estado ou há um registo da tarefa de Olá no serviço de Olá.|equipa de operações do serviço de importação/exportação Olá irá tentar toocontact Olá cliente toocreate ou actualizar a tarefa de Olá com a tarefa de informações necessárias toomove Olá reencaminhar.<br /><br /> Se a equipa de operações do Olá cliente de Olá toocontact não é possível no prazo de duas semanas, a equipa de operações de Olá tentará tooreturn Olá unidades.<br /><br /> Olá durante o evento que não podem ser devolvidas Olá unidades e não é possível aceder ao cliente de Olá, unidades Olá irão ser destruídas de forma segura nos 90 dias.<br /><br /> Tenha em atenção que não é possível processar uma tarefa, até que o respetivo estado é atualizado demasiado`Shipping`.|
|`Shipping`|pacote de Olá para uma tarefa não chegou durante mais de duas semanas.|equipa de operações de Olá notificará o cliente de Olá do pacote em falta Olá. Com base na resposta do cliente Olá, a equipa de operações do Olá serão expandir Olá intervalo toowait para Olá pacote tooarrive, ou cancele a tarefa de Olá.<br /><br /> O evento Olá desse cliente Olá não pode ser contactado ou não responder dentro de 30 dias, a equipa de operações do Olá vai iniciar a tarefa de Olá toomove ação de Olá `Shipping` Estado diretamente toohello `Closed` estado.|
|`Completed/Closed`|unidades de Olá nunca foi atingido o endereço do remetente Olá ou foram danificadas no shipment (aplica-se tarefas de exportação tooan apenas).|Se Olá unidades não atingir o endereço do remetente Olá, cliente Olá deve primeira chamada Olá Get Job operação ou verificação de estado da tarefa Olá no Olá portal tooensure que Olá unidades foram fornecidas. Se foram fornecidas unidades Olá, cliente Olá deve contactar o fornecedor tootry de envio Olá e localize Olá unidades.<br /><br /> Se Olá unidades estão danificadas durante shipment, o cliente de Olá poderá pretender toorequest outra tarefa de exportação ou transferência Olá em falta blobs.|
|`Transferring/Packaging`|Tarefa tem um incorreto ou em falta o endereço do remetente.|equipa de operações de Olá irá entrar toohello pessoa contacto para o endereço correto do Olá tarefa tooobtain Olá.<br /><br /> O evento Olá desse cliente Olá não é possível aceder, Olá unidades irão ser destruídas em segurança nos 90 dias.|
|`Creating / Shipping/ Transferring`|Uma unidade que não aparecem na lista de Olá de toobe unidades importada está incluída no Olá envio do pacote.|Olá unidades adicionais não serão processadas e serão devolvidas toohello cliente quando Olá tarefa estiver concluída.|

## <a name="drive-states"></a>Estados de unidade
tabela de Olá e diagrama Olá abaixo descrevem Olá o ciclo de vida de uma unidade individuais passa através de uma tarefa de importação ou exportação. Pode obter o estado de unidade atual Olá ao chamar Olá `Get Job` Olá operação e analisando `State` elemento de Olá `DriveList` propriedade.

![DriveStates](./media/storage-import-export-retrieving-state-info-for-a-job/DriveStates.png "DriveStates")

Olá tabela seguinte descreve cada Estado de uma unidade poderá pass-through.

|Unidade de estado|Descrição|
|-----------------|-----------------|
|`Specified`|Para uma tarefa de importação, quando é criada com Olá operação Put tarefa, a tarefa de Olá Olá o estado inicial para uma unidade é Olá `Specified` estado. Para uma tarefa de exportação, uma vez que não unidade é especificada quando Olá tarefa é criada, o estado da unidade inicial Olá é Olá `Received` estado.|
|`Received`|unidade de Olá passa toohello `Received` de estado quando hello operador do serviço de importação/exportação processou unidades Olá que foram recebidas do Olá da empresa para uma tarefa de importação de envio. Para uma tarefa de exportação, o estado da unidade inicial de Olá é Olá `Received` estado.|
|`NeverReceived`|unidade de Olá moverá toohello `NeverReceived` estado quando hello chegar a esse pacote para uma tarefa, mas o pacote de Olá não contém a unidade de Olá. Pode também mover uma unidade para este estado se duas semanas, uma vez que o serviço de Olá recebeu informações de envio de Olá, mas o pacote de Olá ainda não chegaram Centro de dados de Olá.|
|`Transferring`|Uma unidade irá mover toohello `Transferring` de estado quando hello serviço começa dados tootransfer Olá unidade tooWindows Storage do Azure.|
|`Completed`|Uma unidade irá mover toohello `Completed` quando serviço Olá foi transferido com êxito todos os dados de Olá sem erros de estado.|
|`CompletedMoreInfo`|Uma unidade irá mover toohello `CompletedMoreInfo` quando Olá serviço detetou alguns problemas ao copiar dados a partir de ou toohello unidade de estado. informações de Olá podem incluir erros, avisos e mensagens informativas sobre substituir blobs.|
|`ShippedBack`|unidade de Olá moverá toohello `ShippedBack` estado quando tem sido enviada do endereço devolvido de toohello back do Centro de dados Olá.|

Olá tabela seguinte descreve Olá unidade falha Estados e as ações de Olá executadas para cada Estado.

|Unidade de estado|Evento|Resolução / passo seguinte|
|-----------------|-----------|-----------------------------|
|`NeverReceived`|Uma unidade que está marcada como `NeverReceived` (porque não foi recebida como parte da shipment da tarefa de Olá) chega no shipment outro.|equipa de operações de Olá moverá Olá unidade toohello `Received` estado.|
|`N/A`|Uma unidade que não faz parte de qualquer tarefa chega ao centro de dados de Olá como parte de outra tarefa.|unidade de Olá será marcada como uma unidade adicional e será devolvida toohello cliente quando a tarefa de Olá associada ao pacote original Olá for concluída.|

## <a name="faulted-states"></a>Estados com falhas
Quando uma tarefa ou a unidade falha tooprogress normalmente através do respetivo ciclo de vida esperado, a tarefa de Olá ou unidade será movida para um `Faulted` estado. Nessa altura, a equipa de operações do Olá irá contactar o cliente de Olá por e-mail ou telefone. Assim que for resolvido o problema de Olá, Olá falhou tarefa ou unidade será retirada Olá `Faulted` estado e movido para Olá adequado estado.

## <a name="next-steps"></a>Passos seguintes

* [Utilizar a REST API do serviço de importação/exportação Olá](storage-import-export-using-the-rest-api.md)
