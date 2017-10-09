---
title: "aaaCreate uma tarefa de importação para o Azure importar/exportar | Microsoft Docs"
description: "Saiba como toocreate uma importação de Olá serviço de importação/exportação do Microsoft Azure."
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a>Criar uma tarefa de importação para Olá serviço importar/exportar do Azure

Criar uma tarefa de importação para o serviço de importação/exportação do Microsoft Azure Olá utilizando a REST API de Olá envolve Olá os seguintes passos:

-   A preparar unidades com Olá ferramenta de importação/exportação do Azure.

-   Obter Olá localização toowhich tooship Olá unidade.

-   A criar tarefa de importação de Olá.

-   Envio Olá unidades tooMicrosoft através de um serviço de carrier suportados.

-   Atualizar a tarefa de importação de Olá com Olá detalhes de envio.

 Consulte [utilizando Olá importação/exportação do Microsoft Azure service tooTransfer dados tooBlob armazenamento](storage-import-export-service.md) para uma descrição geral do serviço de importação/exportação Olá e um tutorial que demonstra como toouse Olá [portal do Azure](https://portal.azure.com/) toocreate e gerir importação e exportação de tarefas.

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a>Preparar as unidades com Olá ferramenta de importação/exportação do Azure

Olá passos tooprepare unidades para uma tarefa de importação são Olá, mesmo se criar Olá portal de Olá jobvia ou através de Olá REST API.

Segue-se uma breve descrição geral da preparação da unidade. Consulte toohello [Azure importação ExportTool referência](storage-import-export-tool-how-to-v1.md) para obter instruções completas. Pode transferir a ferramenta de importação/exportação do Azure de Olá [aqui](http://go.microsoft.com/fwlink/?LinkID=301900).

Envolve a preparação da sua unidade:

-   Identificar Olá dados toobe importado.

-   Identificar os blobs de destino de Olá no armazenamento do Microsoft Azure.

-   Utilizar Olá ferramenta de importação/exportação do Azure toocopy tooone os dados ou mais unidades de disco rígido.

 Olá ferramenta de importação/exportação do Azure também irá gerar um ficheiro de manifesto para cada uma das unidades de Olá conforme está preparado. Contém um ficheiro de manifesto:

-   Enumeração de todos os ficheiros de Olá concebida para carregar e mapeamentos de Olá de tooblobs estes ficheiros.

-   Somas de verificação de segmentos de Olá de cada ficheiro.

-   Informações sobre tooassociate de metadados e as propriedades de Olá com cada blob.

-   Uma lista de Olá ação tootake se um blob que está a ser carregado tem Olá mesmo nome como um blob existente no contentor de Olá. Opções possíveis: a) Substituir BLOBs Olá com o ficheiro de Olá, b) manter blob existente Olá e ignorar a carregar ficheiro Olá, c) Acrescentar um nome de toohello sufixo, para que este não entra em conflito com outros ficheiros.

## <a name="obtaining-your-shipping-location"></a>Obter a localização de envio

Antes de criar uma tarefa de importação, terá de tooobtain um nome de localização de envio e o endereço ao chamar Olá [lista localizações](/rest/api/storageimportexport/listlocations) operação. `List Locations`irá devolver uma lista de localizações e os respetivos endereços de correio postal. Pode selecionar uma localização Olá devolvida lista e são enviados o seu endereço de toothat unidades de disco rígido. Também pode utilizar Olá `Get Location` Olá tooobtain de operação de envio endereço para uma localização específica diretamente.

 Siga os passos de Olá abaixo localização de envio de Olá tooobtain:

-   Identifica o nome de Olá de localização de Olá da sua conta de armazenamento. Este valor pode ser encontrado na Olá **localização** campo na conta de armazenamento a Olá **Dashboard** no Olá Azure portal ou consultado para utilizando a operação de API de gestão do serviço de Olá [obter armazenamento Propriedades da conta](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).

-   Obter a localização de Olá que está disponível tooprocess esta conta de armazenamento ao chamar Olá `Get Location` operação.

-   Se hello `AlternateLocations` propriedade de localização de Olá contém localização Olá próprio, em seguida, é toouse pode nesta localização. Caso contrário, chamar Olá `Get Location` operação com uma das localizações alternativas Olá. a localização original Olá pode estar fechada temporariamente para manutenção.

## <a name="creating-hello-import-job"></a>Criar tarefa de importação de Olá
tarefa de importação de Olá toocreate, chamada Olá [colocar tarefa](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação. Terá de Olá tooprovide seguintes informações:

-   Um nome para a tarefa de Olá.

-   nome da conta de armazenamento Olá.

-   Olá envio de nome de localização, obtido a partir do passo anterior Olá.

-   Um tipo de tarefa (importar).

-   endereço de retorno olá onde devem ser enviadas Olá unidades após conclusão da tarefa de importação de Olá.

-   lista de Olá de unidades de tarefa Olá. Para cada unidade, tem de incluir Olá informações que foi obtidas durante o passo de preparação de unidade de Olá os seguintes:

    -   Id de unidade de Olá

    -   chave do BitLocker Olá

    -   caminho relativo do ficheiro de manifesto de Olá no disco rígido Olá

    -   Olá Base16 codificado hash do ficheiro de manifesto MD5

## <a name="shipping-your-drives"></a>As unidades de envio
Tem a enviar o seu endereço de toohello de unidades que obteve no passo anterior Olá, e tem de fornecer Olá serviço de importação/exportação com Olá número de pacotes de Olá de controlo.

> [!NOTE]
>  Tem de enviar a unidades através de um serviço operadora suportados, o que irá fornecer um número de controlo do seu pacote.

## <a name="updating-hello-import-job-with-your-shipping-information"></a>Atualizar a tarefa de importação de Olá com as suas informações de envio
Depois de ter o seu número de controlo, chamar Olá [propriedades da tarefa de atualização](/api/storageimportexport/jobs#Jobs_Update) Olá tooupdate de operação de envio nome da operadora, o número de controlo de Olá para a tarefa de Olá e o número de conta de carrier Olá para envio de retorno. Opcionalmente, pode especificar o número de Olá de unidades e Olá, bem como a data de envio.

## <a name="next-steps"></a>Passos seguintes

* [Utilizar a REST API do serviço de importação/exportação Olá](storage-import-export-using-the-rest-api.md)
