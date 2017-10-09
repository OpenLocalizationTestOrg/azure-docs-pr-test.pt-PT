---
title: "uma tarefa para Azure importar/exportar a exportação de aaaCreate | Microsoft Docs"
description: "Saiba como toocreate uma exportação da tarefa para Olá serviço de importação/exportação do Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a>Criar uma tarefa de exportação para Olá serviço importar/exportar do Azure
Criar uma tarefa de exportação para o serviço de importação/exportação do Microsoft Azure Olá utilizando a REST API de Olá envolve Olá os seguintes passos:

-   Selecionar Olá blobs tooexport.

-   Obter uma localização de envio.

-   A criar tarefa de exportação de Olá.

-   Envio sua tooMicrosoft unidades vazio através de um serviço de carrier suportados.

-   A atualizar a tarefa de exportação de Olá com informações de pacote Olá.

-   Receber Olá unidades novamente a partir do Microsoft.

 Consulte [utilizando Olá importação/exportação do Windows Azure serviço tooTransfer dados tooBlob armazenamento](storage-import-export-service.md) para uma descrição geral do serviço de importação/exportação Olá e um tutorial que demonstra como toouse Olá [portal do Azure](https://portal.azure.com/) toocreate e gerir importação e exportação de tarefas.

## <a name="selecting-blobs-tooexport"></a>Selecionar tooexport de blobs
 toocreate uma tarefa de exportação, terá de tooprovide uma lista de blobs que pretende que tooexport da sua conta de armazenamento. Existem algumas formas tooselect blobs toobe exportado:

-   Pode utilizar um tooselect de caminho relativo blob um blob único e todos os respetivos instantâneos.

-   Pode utilizar um tooselect de caminho relativo blob um blob único excluindo respetivos instantâneos.

-   Pode utilizar um caminho relativo de blob e um tooselect de tempo de instantâneos um único instantâneo.

-   Pode utilizar um tooselect de prefixo de blob todos os blobs e instantâneos com Olá fornecido prefixo.

-   Pode exportar todos os blobs e instantâneos na conta do storage Olá.

 Para obter mais informações sobre como especificar blobs tooexport, consulte Olá [colocar tarefa](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação.

## <a name="obtaining-your-shipping-location"></a>Obter a localização de envio
Antes de criar uma tarefa de exportação, terá de tooobtain um nome de localização de envio e o endereço ao chamar Olá [obter localização](https://portal.azure.com) ou [lista localizações](/rest/api/storageimportexport/listlocations) operação. `List Locations`irá devolver uma lista de localizações e os respetivos endereços de correio postal. Pode selecionar uma localização Olá devolvida lista e são enviados o seu endereço de toothat unidades de disco rígido. Também pode utilizar Olá `Get Location` Olá tooobtain de operação de envio endereço para uma localização específica diretamente.

Siga os passos de Olá abaixo localização de envio de Olá tooobtain:

-   Identifica o nome de Olá de localização de Olá da sua conta de armazenamento. Este valor pode ser encontrado na Olá **localização** campo na conta de armazenamento a Olá **Dashboard** no clássico Olá portal ou consultado para utilizando a operação de API de gestão do serviço de Olá [obter Propriedades da conta de armazenamento](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).

-   Obter a localização de Olá que estão disponíveis tooprocess esta conta de armazenamento ao chamar Olá `Get Location` operação.

-   Se hello `AlternateLocations` propriedade de localização de Olá contém localização Olá próprio, em seguida, é toouse pode nesta localização. Caso contrário, chamar Olá `Get Location` operação com uma das localizações alternativas Olá. a localização original Olá pode estar fechada temporariamente para manutenção.

## <a name="creating-hello-export-job"></a>Criar tarefa de exportação de Olá
 tarefa de exportação de Olá toocreate, chamada Olá [colocar tarefa](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação. Terá de Olá tooprovide seguintes informações:

-   Um nome para a tarefa de Olá.

-   nome da conta de armazenamento Olá.

-   Olá envio de nome de localização, obtido no passo anterior Olá.

-   Um tipo de tarefa (exportação).

-   endereço de retorno olá onde devem ser enviadas Olá unidades após conclusão da tarefa de exportação de Olá.

-   Olá toobe de lista de blobs (ou prefixos de blob) exportado.

## <a name="shipping-your-drives"></a>As unidades de envio
 Em seguida, utilizar Olá ferramenta de importação/exportação do Azure toodetermine Olá número de unidades que precisa de toosend, com base em blobs Olá que selecionou toobe exportado e Olá tamanho de unidade. Consulte Olá [referência de ferramenta de importação/exportação do Azure](storage-import-export-tool-how-to-v1.md) para obter mais detalhes.

 Pacote de pacote Olá unidades numa única e envie-los toohello endereço obtido no Olá passo anterior. Tenha em atenção Olá número do seu pacote para o passo seguinte Olá de controlo.

> [!NOTE]
>  Tem de enviar a unidades através de um serviço operadora suportados, o que irá fornecer um número de controlo do seu pacote.

## <a name="updating-hello-export-job-with-your-package-information"></a>Atualizar a tarefa de exportação de Olá com as suas informações de pacote
 Depois de ter o seu número de controlo, chamar Olá [propriedades da tarefa de atualização](/rest/api/storageimportexport/jobs#Jobs_Update) nome da operação tooupdated Olá operadora e o controlo número para a tarefa de Olá. Opcionalmente, pode especificar Olá número de unidades, endereço do remetente Olá e data de envio de Olá bem.

## <a name="receiving-hello-package"></a>Pacotes hello a receber
 Depois de ter sido processada a tarefa de exportação, será devolvida a unidades tooyou com os seus dados encriptados. Pode obter a chave do BitLocker Olá para cada uma das unidades de Olá ao chamar Olá [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operação. Em seguida, pode desbloquear unidade Olá utilizando a chave de Olá. ficheiro de manifesto de unidade de Olá em cada unidade contém a lista de Olá dos ficheiros na unidade de Olá, bem como endereço de blob original Olá para cada ficheiro.

## <a name="next-steps"></a>Passos seguintes

* [Utilizar a REST API do serviço de importação/exportação Olá](storage-import-export-using-the-rest-api.md)
