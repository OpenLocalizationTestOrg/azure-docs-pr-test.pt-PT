---
title: dados de aaaCapture dos Event Hubs no Azure Data Lake Store | Microsoft Docs
description: "Dados de toocapture de utilização do Azure Data Lake Store dos Event Hubs"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a>Dados de toocapture de utilização do Azure Data Lake Store dos Event Hubs

Saiba como toouse dados do Azure Data Lake Store toocapture recebidos pelo Event Hubs do Azure.

## <a name="prerequisites"></a>Pré-requisitos

* **Uma subscrição do Azure**. Consulte [Obter uma avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Uma conta do Azure Data Lake Store**. Para obter instruções sobre como um, ver toocreate [introdução ao Azure Data Lake Store](data-lake-store-get-started-portal.md).

*  **Um espaço de nomes de Event Hubs**. Para obter instruções, consulte [criar um espaço de nomes de Event Hubs](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace). Certifique-se conta de Data Lake Store Olá e espaço de nomes de Hubs de eventos de Olá Olá mesma subscrição do Azure.


## <a name="assign-permissions-tooevent-hubs"></a>Atribua permissões tooEvent Hubs

Nesta secção, vai criar uma pasta dentro da conta de olá onde pretende que os dados de Olá toocapture dos Event Hubs. É também atribuir permissões tooEvent Hubs para que este pode escrever dados para uma conta do Data Lake Store. 

1. Abra a conta de Data Lake Store olá onde pretende toocapture dados dos Event Hubs e, em seguida, clique em **Explorador de dados**.

    ![Explorador de dados do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Explorador de dados do Data Lake Store")

2.  Clique em **nova pasta** e, em seguida, introduza um nome para a pasta onde pretende que toocapture Olá dados.

    ![Crie uma nova pasta no Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "crie uma nova pasta no Data Lake Store")

3. Atribua permissões na raiz de Olá de Olá Data Lake Store. 

    a. Clique em **Explorador de dados**, selecione de raiz de Olá da Olá conta do Data Lake Store e, em seguida, clique em **acesso**.

    ![Atribuir permissões para a raiz do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "atribuir permissões para a raiz do Data Lake Store")

    b. Em **acesso**, clique em **adicionar**, clique em **selecionar utilizador ou grupo**e, em seguida, procure `Microsoft.EventHubs`. 

    ![Atribuir permissões para a raiz do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "atribuir permissões para a raiz do Data Lake Store")
    
    Clique em **Selecionar**.

    c. Em **atribuir permissões**, clique em **selecionar permissões**. Definir **permissões** demasiado**executar**. Definir **adicionar ao** demasiado**esta pasta e todos os elementos subordinados**. Definir **adicionar como** demasiado**uma entrada de permissão de acesso e uma entrada de permissão predefinidas**.

    ![Atribuir permissões para a raiz do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "atribuir permissões para a raiz do Data Lake Store")

    Clique em **OK**.

4. Atribua permissões para a pasta de Olá sob a conta do Data Lake Store onde pretende que os dados de toocapture.

    a. Clique em **Explorador de dados**, selecione a pasta de Olá na Olá conta do Data Lake Store e, em seguida, clique em **acesso**.

    ![Atribuir permissões para a pasta do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "atribuir permissões para a pasta do Data Lake Store")

    b. Em **acesso**, clique em **adicionar**, clique em **selecionar utilizador ou grupo**e, em seguida, procure `Microsoft.EventHubs`. 

    ![Atribuir permissões para a pasta do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "atribuir permissões para a pasta do Data Lake Store")
    
    Clique em **Selecionar**.

    c. Em **atribuir permissões**, clique em **selecionar permissões**. Definir **permissões** demasiado**ler, escrever,** e **executar**. Definir **adicionar ao** demasiado**esta pasta e todos os elementos subordinados**. Finalmente, defina o **adicionar como** demasiado**uma entrada de permissão de acesso e uma entrada de permissão predefinidas**.

    ![Atribuir permissões para a pasta do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "atribuir permissões para a pasta do Data Lake Store")
    
    Clique em **OK**. 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a>Configurar os Event Hubs toocapture dados tooData Lake Store

Nesta secção, vai criar um Hub de eventos dentro de um espaço de nomes de Event Hubs. Também configurar Olá Hub de eventos toocapture dados tooan conta do Azure Data Lake Store. Esta secção assume que já criou um espaço de nomes de Event Hubs.

2. De Olá **descrição geral** painel do espaço de nomes de Event Hubs Olá, clique em **+ Hub de eventos**.

    ![Criar o Hub de eventos](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "criar o Hub de eventos")

3. Fornece seguinte Olá valores tooconfigure Event Hubs toocapture tooData data Lake Store.

    ![Criar o Hub de eventos](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "criar o Hub de eventos")

    a. Forneça um nome para Olá Hub de eventos.
    
    b. Para este tutorial, defina **contagem da partição** e **mensagem retenção** valores predefinidos de toohello.
    
    c. Definir **capturar** demasiado**no**. Conjunto Olá **janela de tempo** (frequência toocapture) e **tamanho da janela** (toocapture de tamanho de dados). 
    
    d. Para **capturar fornecedor**, selecione **Azure Data Lake Store** e hello selecione Olá Data Lake Store que criou anteriormente. Para **caminho do Data Lake**, introduza o nome de Olá da pasta de Olá que criou no Olá conta do Data Lake Store. Só precisa de pasta de toohello tooprovide Olá caminho relativo.

    e. Deixe Olá **formatos de nome de ficheiro de captura de exemplo** valor predefinido de toohello. Esta opção é regida pelas estrutura de pastas de Olá que é criada na pasta de captura Olá.

    f. Clique em **Criar**.

## <a name="test-hello-setup"></a>O programa de configuração do teste Olá

Pode agora testar solução Olá através do envio de dados toohello Hub de eventos do Azure. Siga as instruções de Olá em [enviar eventos tooAzure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md). Depois de começar a enviar dados de Olá, ver dados Olá refletidos no Data Lake Store utilizando a estrutura de pastas de Olá que especificou. Por exemplo, verá uma estrutura de pasta, conforme mostrado no Olá seguinte captura de ecrã, no Data Lake Store.

![Exemplo de dados de EventHub no Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "EventHub de amostra de dados no Data Lake Store")

> [!NOTE]
> Mesmo se não tiver mensagens entra de Event Hubs, os Event Hubs escreve ficheiros vazios com apenas os cabeçalhos de Olá na Olá conta do Data Lake Store. Olá ficheiros são escritos no Olá mesmo intervalo de tempo que forneceu ao criar Olá Event Hubs.
> 
>

## <a name="analyze-data-in-data-lake-store"></a>Analisar dados no Data Lake Store

Assim que estiver dados Olá no Data Lake Store, pode executar tarefas analíticas tooprocess e crunch dados Olá. Consulte [USQL Avro exemplo](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) sobre toodo este utilizando o Azure Data Lake Analytics.
  

## <a name="see-also"></a>Consultar também
* [Secure data in Data Lake Store (Proteger dados no Data Lake Store)](data-lake-store-secure-data.md)
* [Copiar dados de armazenamento de Blobs tooData arquivo Lake do Azure](data-lake-store-copy-data-azure-storage-blob.md)
