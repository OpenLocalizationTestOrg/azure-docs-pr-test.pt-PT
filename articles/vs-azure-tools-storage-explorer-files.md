---
title: "aaaUsing Explorador de armazenamento (pré-visualização) com o File storage do Azure | Microsoft Docs"
description: "Saiba como saber como toouse Explorador de armazenamento (pré-visualização) toowork com o ficheiro de partilhas e os ficheiros."
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a>Utilizar o Explorador de Armazenamento (Pré-visualização) com o Armazenamento de ficheiros do Azure

Ficheiros do Azure storage é um serviço que oferece ficheiro partilhas na utilização de nuvem Olá Olá protocolo Server Message Block (SMB) padrão. O SMB 2.1 e o SMB 3.0 são suportados. Com o File storage do Azure, é possível migrar aplicações antigas que se baseiam em tooAzure de partilhas de ficheiros rapidamente e sem reescritas dispendiosas. Pode utilizar os dados de ficheiros armazenamento tooexpose publicamente toohello mundo ou toostore dados da aplicação em privado. Neste artigo, irá aprender como toouse Explorador de armazenamento (pré-visualização) toowork com o ficheiro de partilhas e os ficheiros.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete Olá passos descritos neste artigo, irá precisar seguinte Olá:

- [Transfira e instale o Explorador de Armazenamento (pré-visualização)](http://www.storageexplorer.com/)

- [Ligar a conta de armazenamento do Azure tooa ou serviço](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a>Criar Partilhas de Ficheiros

Todos os ficheiros têm de residir numa partilha de ficheiros, que é simplesmente um agrupamento lógico de ficheiros. Uma conta pode conter um número ilimitado de partilhas de ficheiros e cada partilha pode armazenar um número ilimitado de ficheiros.

Olá, os passos seguintes mostram como toocreate um partilha de ficheiros no Explorador de armazenamento (pré-visualização).

1. Abrir o Explorador de Armazenamento (Pré-visualização).

2. No painel esquerdo Olá, expanda a conta de armazenamento de Olá no qual pretende toocreate Olá partilha de ficheiros

3. Clique com botão direito **partilhas de ficheiros**e, no menu de contexto de Olá - selecione **criar partilha de ficheiros**.

    ![Criar a Partilha de Ficheiros](media/vs-azure-tools-storage-explorer-files/image1.png)

4. Será apresentada uma caixa de texto abaixo Olá **partilhas de ficheiros** pasta. Introduza o nome de Olá para a partilha de ficheiros. Consulte Olá [partilhar regras de nomenclatura](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) secção para obter uma lista de restrições em partilhas de ficheiros de atribuição de nomes e regras.

    ![Atribuição de nome de partilha de Olá](media/vs-azure-tools-storage-explorer-files/image2.png)

5. Prima **Enter** quando toocreate efectuada Olá partilha de ficheiros, ou **Esc** toocancel. Assim que a partilha de ficheiros de Olá foi criada com êxito, será apresentado em Olá **partilhas de ficheiros** pasta para Olá selecionado a conta de armazenamento.

    ![nova partilha de Olá](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a>Ver os conteúdos de uma partilha de ficheiros

As partilhas de ficheiros contêm ficheiros e pastas (que também podem conter ficheiros).

Olá passos seguintes mostram como partilha de conteúdo de Olá tooview de um ficheiro no Explorador de armazenamento (pré-visualização): +

1. Abrir o Explorador de Armazenamento (Pré-visualização).

2. No painel esquerdo Olá, expanda a conta de armazenamento de Olá com partilha de ficheiros de Olá desejar tooview.

3. Expanda a conta de armazenamento a Olá **partilhas de ficheiros**.

4. Partilha de ficheiros do contexto Olá que queira tooview e, no menu de contexto de Olá - selecione **abra**. Também pode fazer duplo clique partilha de ficheiros de Olá desejar tooview.

    ![Abrir a partilha](media/vs-azure-tools-storage-explorer-files/image4.png)

5. painel principal Olá apresentará o conteúdo da partilha de ficheiros Olá.
    
    ![Olá conteúdos da partilha](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a>Eliminar partilhas de ficheiros

É fácil criar e eliminar partilhas de ficheiros, conforme necessário. (toosee como ficheiros individuais toodelete, consulte a secção de toohello, [gerir ficheiros numa partilha de ficheiros](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)

Olá, os passos seguintes ilustram como toodelete um partilha de ficheiros no Explorador de armazenamento (pré-visualização):

1. Abrir o Explorador de Armazenamento (Pré-visualização).

2. No painel esquerdo Olá, expanda a conta de armazenamento de Olá com partilha de ficheiros de Olá desejar tooview.

3. Expanda a conta de armazenamento a Olá **partilhas de ficheiros**.

4. Partilha de ficheiros do contexto Olá que queira toodelete e, no menu de contexto de Olá - selecione **eliminar**. Também pode premir **eliminar** partilha do toodelete Olá ficheiro atualmente selecionado.

    ![Eliminar](media/vs-azure-tools-storage-explorer-files/image6.png)

5. Selecione **Sim** toohello diálogo de confirmação.
    
    ![Caixa de diálogo de confirmação](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a>Copiar partilhas de ficheiros

Explorador de armazenamento (pré-visualização) permite-lhe toocopy uma área de transferência de toohello de partilha de ficheiros e, em seguida, cole que a partilha de ficheiros para outra conta de armazenamento. (toosee como ficheiros individuais toocopy, consulte a secção de toohello, [gerir ficheiros numa partilha de ficheiros](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)

Olá, os passos seguintes mostram como toocopy um ficheiro de partilha de um tooanother de conta de armazenamento.

1. Abrir o Explorador de Armazenamento (Pré-visualização).

2. No painel esquerdo Olá, expanda a conta de armazenamento de Olá com partilha de ficheiros de Olá desejar toocopy.

3. Expanda a conta de armazenamento a Olá **partilhas de ficheiros**.

4. Partilha de ficheiros do contexto Olá que queira toocopy e, no menu de contexto de Olá - selecione **partilha de ficheiros de cópia**.

    ![Copiar Partilha de Ficheiros](media/vs-azure-tools-storage-explorer-files/image8.png)

5. Faça duplo clique de conta de armazenamento de destino"Olá pretendido" para o qual pretende partilha de ficheiros toopaste Olá e - a partir do menu de contexto de Olá - selecione **partilha de ficheiros de colar**.

    ![Criar Partilha de Ficheiros](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a>Obter Olá SAS para uma partilha de ficheiros

A [assinatura de acesso partilhado (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) fornece acesso delegado tooresources na sua conta de armazenamento. Isto significa que pode conceder que um cliente limitada tooobjects de permissões na sua conta de armazenamento para um determinado período de tempo e com um conjunto especificado de permissões, sem ter tooshare as chaves de acesso da conta.

Olá passos seguintes mostram como toocreate partilhar uma SAS para um ficheiro: +

1. Abrir o Explorador de Armazenamento (Pré-visualização).

2. No painel esquerdo Olá, expanda a conta de armazenamento de Olá com partilha de ficheiros de Olá para o qual pretende tooget uma SAS.

3. Expanda a conta de armazenamento a Olá **partilhas de ficheiros**.

4. Partilha de ficheiros pretendido de Olá com o botão direito e, no menu de contexto de Olá - selecione **obter assinatura de acesso partilhado**.

    ![Obter Assinatura de Acesso Partilhado](media/vs-azure-tools-storage-explorer-files/image10.png)

5. No Olá **assinatura de acesso partilhado** caixa de diálogo, especificar a política de Olá, datas de início e de expiração, fuso horário e níveis de que pretende para recursos de Olá de acesso.

    ![Caixa de diálogo SAS](media/vs-azure-tools-storage-explorer-files/image11.png)

6. Quando tiver terminado de especificar opções de SAS Olá, selecione **criar**.

7. Um segundo **assinatura de acesso partilhado** caixa de diálogo, em seguida, irá apresentar que apresenta uma lista de Olá partilha de ficheiros, juntamente com o URL de Olá e QueryStrings pode utilizar tooaccess Olá recursos de armazenamento. Selecione **cópia** seguinte URL de toohello desejar área de transferência do toocopy toohello.
    
    ![Segunda caixa de diálogo SAS](media/vs-azure-tools-storage-explorer-files/image12.png)

8. Quando terminar, selecione **Close (Fechar)**.

## <a name="manage-access-policies-for-a-file-share"></a>Gerir as Políticas de Acesso de uma partilha de ficheiros

Olá passos seguintes mostram como toomanage (adicionar e remover) políticas para uma partilha de ficheiros de acesso: +. Políticas de acesso de Olá é utilizada para criar URLs de SAS através do qual as pessoas podem utilizar tooaccess Olá recurso do ficheiro de armazenamento durante um período de tempo definido.

1. Abrir o Explorador de Armazenamento (Pré-visualização).

2. No painel esquerdo Olá, expanda a conta de armazenamento de Olá com partilha de ficheiros de Olá cujas políticas de acesso pretende toomanage.

3. Expanda a conta de armazenamento a Olá **partilhas de ficheiros**.

4. Selecione a partilha de ficheiros pretendido de Olá e, no menu de contexto de Olá - selecione **gerir políticas de acesso**.

    ![Menu de Contexto Gerir políticas de acesso](media/vs-azure-tools-storage-explorer-files/image13.png)

5. Olá **políticas de acesso** apresentará uma caixa de diálogo lista quaisquer políticas de acesso já criadas para a partilha de ficheiros selecionado Olá.
    
    ![Políticas de Acesso](media/vs-azure-tools-storage-explorer-files/image14.png)

6. Siga estes passos, dependendo da tarefa de gestão de política de acesso de Olá:
    
    - **Adicionar uma política de acesso nova** - selecione **Add (Adicionar)**. Depois de o gerado, Olá **políticas de acesso** diálogo apresentará Olá recém-adicionada política (com as predefinições) de acesso.

    - **Editar uma política de acesso** - faça eventuais alterações que pretenda e selecione **Save (Guardar)**.

    - **Remover uma política de acesso** - selecione **remover** próxima política de acesso de toohello desejar tooremove.

7. Crie um novo URL de SAS através de Olá política de acesso que criou anteriormente:
    
    ![Obter SAS](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Nome e propriedades de SAS](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a>Gerir ficheiros numa partilha de ficheiros

Assim que tiver criado uma partilha de ficheiros, pode carregar uma partilha de ficheiros do ficheiro toothat, transferir um computador local do ficheiro tooyour, abra um ficheiro no seu computador local e muito mais.

Olá passos seguintes mostram como partilharem toomanage Olá ficheiros (e pastas) dentro de um ficheiro.

1.  Abrir o Explorador de Armazenamento (Pré-visualização).

2.  No painel esquerdo Olá, expanda a conta de armazenamento de Olá com partilha de ficheiros de Olá desejar toomanage.

3.  Expanda a conta de armazenamento a Olá **partilhas de ficheiros**.

4.  Faça duplo clique em partilha de ficheiros de Olá desejar tooview.

5.  painel principal Olá apresentará o conteúdo da partilha de ficheiros Olá.

    ![Olá conteúdos da partilha](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  painel principal Olá apresentará o conteúdo da partilha de ficheiros Olá.

7.  Siga estes que passos, dependendo das tarefas de Olá desejar tooperform:

    - **Carregar a partilha de ficheiros de tooa de ficheiros**

        a.  Na barra de ferramentas do painel Olá principal, selecione **carregar**e, em seguida, **carregar ficheiros** no menu de Olá pendente.

        ![Carregar ficheiros](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        b. No Olá **carregar ficheiros** caixa de diálogo, reticências Olá selecione (**...** ) botão no lado direito de Olá de Olá **ficheiros** tooselect Olá ficheiros pretende tooupload de caixa de texto.

        ![Adição ficheiros](media/vs-azure-tools-storage-explorer-files/image19.png)

        c. Selecione **Upload**.

    - **Carregar uma partilha de ficheiros de tooa pasta**
        
        a. Na barra de ferramentas do painel Olá principal, selecione **carregar**e, em seguida, **carregar pasta** no menu de Olá pendente.

        ![Menu Carregar pasta](media/vs-azure-tools-storage-explorer-files/image20.png)

        b. No Olá **carregamento pasta** caixa de diálogo, reticências Olá selecione (**...** ) botão no lado direito de Olá de Olá **pasta** pasta de Olá de tooselect de caixa de texto cujo conteúdo pretende tooupload.

        c. Opcionalmente, especifique uma pasta de destino no qual Olá conteúdo da pasta selecionado será carregado. Se a pasta de destino Olá não existir, será criado.

        d. Selecione **Upload**.

    - **Transferir um computador local do ficheiro tooyour**
        
        a. Selecione o ficheiro de Olá desejar toodownload.
        
        b. Na barra de ferramentas do painel Olá principal, selecione **transferir**.
        
        c. No Olá **Especifique qual toosave Olá transferidos ficheiros** caixa de diálogo, especifique onde pretende que o ficheiro de Olá transferido de localização de Olá e Olá nome desejar toogive-lo.

        d. Selecione **Guardar**.

    - **Abrir um ficheiro no seu computador local**
        
        a.  Selecione o ficheiro de Olá desejar tooopen.
        
        b.  Na barra de ferramentas do painel Olá principal, selecione **abra**.
        
        c.  ficheiro de Olá será transferido e aberta utilizando a aplicação Olá associada ao tipo de ficheiro do ficheiro de Olá subjacente.

    - **Copiar uma área de transferência do ficheiro toohello**

        a. Selecione o ficheiro de Olá desejar toocopy.

        b. Na barra de ferramentas do painel Olá principal, selecione **cópia**.

        c. No painel esquerdo Olá, navegue tooanother partilha de ficheiros e faça duplo clique tooview-lo no painel principal Olá.

        d. Na barra de ferramentas do painel Olá principal, selecione **colar** toocreate uma cópia do ficheiro de Olá.

    - **Eliminar um ficheiro**

        a. Selecione o ficheiro de Olá desejar toodelete.

        b. Na barra de ferramentas do painel Olá principal, selecione **eliminar**.

        c. Selecione **Sim** toohello diálogo de confirmação.

## <a name="next-steps"></a>Passos seguintes

- Olá vista [mais recente notas de versão do Explorador de armazenamento (pré-visualização) e vídeos](http://www.storageexplorer.com/).

- Saiba como demasiado[criar aplicações utilizar blobs do Azure, tabelas, filas e os ficheiros](https://azure.microsoft.com/documentation/services/storage/).
