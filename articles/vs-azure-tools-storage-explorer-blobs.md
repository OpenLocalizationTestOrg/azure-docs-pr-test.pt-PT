---
title: "aaaManage recursos de armazenamento de Blobs do Azure com o Explorador de armazenamento (pré-visualização) | Microsoft Docs"
description: "Gerir os contentores de Blobs do Azure e Blobs com o Explorador de armazenamento (pré-visualização)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a>Gerir recursos de armazenamento de Blobs do Azure com o Explorador de armazenamento (pré-visualização)
## <a name="overview"></a>Descrição geral
[Armazenamento de Blobs do Azure](storage/blobs/storage-dotnet-how-to-use-blobs.md) é um serviço para armazenar grandes quantidades de dados não estruturados, tais como texto ou dados binários, que podem ser acedidos de qualquer local no mundo Olá através de HTTP ou HTTPS.
Pode utilizar os dados do Blob storage tooexpose publicamente toohello mundo ou toostore dados da aplicação em privado. Neste artigo, irá aprender como toouse Explorador de armazenamento (pré-visualização) toowork com blobs e contentores de Blobs.

## <a name="prerequisites"></a>Pré-requisitos
toocomplete Olá passos descritos neste artigo, irá precisar seguinte Olá:

* [Transfira e instale o Explorador de Armazenamento (pré-visualização)](http://www.storageexplorer.com)
* [Ligar a conta de armazenamento do Azure tooa ou serviço](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a>Criar um contentor de blob
Todos os blobs tem de residir num contentor de blob, que é simplesmente um agrupamento lógico de blobs. Uma conta pode conter um número ilimitado de contentores, e cada contentor pode armazenar um número ilimitado de blobs.

Olá passos seguintes mostram como toocreate um contentor do blob no Explorador de armazenamento (pré-visualização).

1. Abrir o Explorador de Armazenamento (Pré-visualização).
2. No painel esquerdo Olá, expanda a conta de armazenamento de Olá no qual pretende o contentor de BLOBs de Olá toocreate.
3. Clique com botão direito **contentores de BLOBs**e, no menu de contexto de Olá - selecione **criar contentor de Blob**.

   ![Criar o menu de contexto de contentores de BLOBs][0]
4. Será apresentada uma caixa de texto abaixo Olá **contentores de BLOBs** pasta. Introduza o nome de Olá para o contentor do blob. Consulte Olá [regras de nomenclatura de contentor](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) secção para obter uma lista de restrições em contentores de BLOBs de atribuição de nomes e regras.

   ![Criar caixa de texto de contentores de BLOBs][1]
5. Prima **Enter** concluída ao contentor do blob toocreate hello, ou **Esc** toocancel. Depois de contentor do blob Olá foi criado com êxito, será apresentado em Olá **contentores de BLOBs** pasta para Olá selecionado a conta de armazenamento.

   ![Criada o contentor de BLOBs][2]

## <a name="view-a-blob-containers-contents"></a>Ver os conteúdos de um contentor de BLOBs
Os contentores de blob contém os blobs e de pastas (que também podem conter os blobs).

Olá passos seguintes mostram como conteúdo Olá tooview um contentor do blob no Explorador de armazenamento (pré-visualização):

1. Abrir o Explorador de Armazenamento (Pré-visualização).
2. No painel esquerdo Olá, expanda a conta de armazenamento de Olá que contém o contentor de blob Olá desejar tooview.
3. Expanda a conta de armazenamento a Olá **contentores de BLOBs**.
4. Contentor de blob do contexto Olá que queira tooview e, no menu de contexto de Olá - selecione **abra Editor de contentor do Blob**.
   Também pode fazer duplo clique contentor do blob Olá desejar tooview.

   ![Menu de contexto de editor de contentor de blob aberta][19]
5. painel principal Olá apresentará o conteúdo do contentor de blob Olá.

   ![Editor de contentor do blob][3]

## <a name="delete-a-blob-container"></a>Eliminar um contentor do blob
Contentores de blob podem ser facilmente criados e eliminadas, conforme necessário. (toosee como blobs toodelete individuais, consulte a secção de toohello, [gerir os blobs num contentor de blob](#managing-blobs-in-a-blob-container).)

Olá passos seguintes mostram como toodelete um contentor do blob no Explorador de armazenamento (pré-visualização):

1. Abrir o Explorador de Armazenamento (Pré-visualização).
2. No painel esquerdo Olá, expanda a conta de armazenamento de Olá que contém o contentor de blob Olá desejar tooview.
3. Expanda a conta de armazenamento a Olá **contentores de BLOBs**.
4. Contentor de blob do contexto Olá que queira toodelete e, no menu de contexto de Olá - selecione **eliminar**.
   Também pode premir **eliminar** contentor de blob atualmente selecionado toodelete Olá.

   ![Eliminar o menu de contexto de contentor do blob][4]
5. Selecione **Sim** toohello diálogo de confirmação.

   ![Eliminar o blob confirmação do contentor][5]

## <a name="copy-a-blob-container"></a>Copie um contentor do blob
Explorador de armazenamento (pré-visualização) permite-lhe toocopy uma área de transferência do toohello de contentor do blob e, em seguida, colar que o contentor de blob para outra conta de armazenamento. (toosee como blobs toocopy individuais, consulte a secção de toohello, [gerir os blobs num contentor de blob](#managing-blobs-in-a-blob-container).)

Olá, os passos seguintes mostram como toocopy um contentor de Blobs do armazenamento de uma conta tooanother.

1. Abrir o Explorador de Armazenamento (Pré-visualização).
2. No painel esquerdo Olá, expanda a conta de armazenamento de Olá que contém o contentor de blob Olá desejar toocopy.
3. Expanda a conta de armazenamento a Olá **contentores de BLOBs**.
4. Contentor de blob do contexto Olá que queira toocopy e, no menu de contexto de Olá - selecione **contentor de BLOBs de cópia**.

   ![Copie o menu de contexto de contentor do blob][6]
5. Faça duplo clique de conta de armazenamento de destino"Olá pretendido" para o qual pretende contentor do blob toopaste Olá e - a partir do menu de contexto de Olá - selecione **contentor de BLOBs de colar**.

   ![Menu de contexto de contentor de blob de colar][7]

## <a name="get-hello-sas-for-a-blob-container"></a>Obter Olá SAS para um contentor de blob
A [assinatura de acesso partilhado (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) fornece acesso delegado tooresources na sua conta de armazenamento.
Isto significa que pode conceder que um cliente limitada tooobjects de permissões na sua conta de armazenamento para um determinado período de tempo e com um conjunto especificado de permissões, sem ter de partilhar as chaves de acesso da conta.

Olá passos seguintes mostram como toocreate uma SAS para um contentor do blob:

1. Abrir o Explorador de Armazenamento (Pré-visualização).
2. No painel esquerdo Olá, expanda a conta de armazenamento de Olá que contém o contentor de blob Olá para o qual pretende tooget uma SAS.
3. Expanda a conta de armazenamento a Olá **contentores de BLOBs**.
4. Clique no contentor de blob pretendido Olá e, no menu de contexto de Olá - selecione **obter assinatura de acesso partilhado**.

   ![Obter o menu de contexto SAS][8]
5. No Olá **assinatura de acesso partilhado** caixa de diálogo, especificar a política de Olá, datas de início e de expiração, fuso horário e níveis de que pretende para recursos de Olá de acesso.

   ![Obter as opções de SAS][9]
6. Quando tiver terminado de especificar opções de SAS Olá, selecione **criar**.
7. Um segundo **assinatura de acesso partilhado** caixa de diálogo, em seguida, irá apresentar que apresenta uma lista de Olá contentor de blob, juntamente com o URL de Olá e QueryStrings pode utilizar tooaccess Olá recursos de armazenamento.
   Selecione **cópia** seguinte URL de toohello desejar área de transferência do toocopy toohello.

   ![Copie o URL SAS][10]
8. Quando terminar, selecione **Close (Fechar)**.

## <a name="manage-access-policies-for-a-blob-container"></a>Gerir políticas de acesso para um contentor do blob
Olá passos seguintes mostram como toomanage (adicionar e remover) políticas para um contentor de BLOBs de acesso:

1. Abrir o Explorador de Armazenamento (Pré-visualização).
2. No painel esquerdo Olá, expanda a conta de armazenamento de Olá que contém o contentor de BLOBs de Olá cujas políticas de acesso pretende toomanage.
3. Expanda a conta de armazenamento a Olá **contentores de BLOBs**.
4. Selecione o contentor de blob pretendido Olá e, no menu de contexto de Olá - selecione **gerir políticas de acesso**.

   ![Menu de Contexto Gerir políticas de acesso][11]
5. Olá **políticas de acesso** apresentará uma caixa de diálogo lista quaisquer políticas de acesso já criadas para o contentor de blob selecionado Olá.

   ![Opções de política de acesso][12]        
6. Siga estes passos, dependendo da tarefa de gestão de política de acesso de Olá:

   * **Adicionar uma política de acesso nova** - selecione **Add (Adicionar)**. Depois de o gerado, Olá **políticas de acesso** diálogo apresentará Olá recém-adicionada política (com as predefinições) de acesso.
   * **Editar uma política de acesso** - efetue as edições pretendidas e selecione **guardar**.
   * **Remover uma política de acesso** - selecione **remover** próxima política de acesso de toohello desejar tooremove.

## <a name="set-hello-public-access-level-for-a-blob-container"></a>Definir Olá nível de acesso público para um contentor do blob
Por predefinição, cada contentor de blob está definido demasiado "Sem acesso de público".

Olá passos seguintes mostram como toospecify um público de acesso ao nível para um contentor do blob.

1. Abrir o Explorador de Armazenamento (Pré-visualização).
2. No painel esquerdo Olá, expanda a conta de armazenamento de Olá que contém o contentor de BLOBs de Olá cujas políticas de acesso pretende toomanage.
3. Expanda a conta de armazenamento a Olá **contentores de BLOBs**.
4. Selecione o contentor de blob pretendido Olá e, no menu de contexto de Olá - selecione **definir o nível de acesso público**.

   ![Defina o menu de contexto de nível de acesso público][13]
5. No Olá **definido ao nível do contentor acesso público** caixa de diálogo, especifique o nível de acesso de Olá assim o desejar.

   ![Definir opções de nível de acesso público][14]
6. Selecione **Aplicar**.

## <a name="managing-blobs-in-a-blob-container"></a>Gerir os blobs num contentor de blob
Depois de criar um contentor de blob, pode carregar um contentor de blob do blob toothat, transferir um computador local do blob tooyour, abra um blob no seu computador local e muito mais.

Olá, os passos seguintes mostram como toomanage Olá blobs (e pastas) dentro de um contentor do blob.

1. Abrir o Explorador de Armazenamento (Pré-visualização).
2. No painel esquerdo Olá, expanda a conta de armazenamento de Olá que contém o contentor de blob Olá desejar toomanage.
3. Expanda a conta de armazenamento a Olá **contentores de BLOBs**.
4. Faça duplo clique de contentor do blob Olá desejar tooview.
5. painel principal Olá apresentará o conteúdo do contentor de blob Olá.

   ![Contentor de BLOBs de vista][3]
6. painel principal Olá apresentará o conteúdo do contentor de blob Olá.
7. Siga estes que passos, dependendo das tarefas de Olá desejar tooperform:

   * **Carregar o contentor de BLOBs de tooa de ficheiros**

     1. Na barra de ferramentas do painel Olá principal, selecione **carregar**e, em seguida, **carregar ficheiros** no menu de Olá pendente.

        ![Carregar o menu de ficheiros][15]
     2. No Olá **carregar ficheiros** caixa de diálogo, reticências Olá selecione (**...** ) botão no lado direito de Olá de Olá **ficheiros** tooselect Olá ficheiros pretende tooupload de caixa de texto.

        ![Opções de ficheiros de carregamento][16]
     3. Especifique o tipo Olá de **Blob tipo**. artigo de Olá [introdução ao Blob storage do Azure através do .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explica Olá as diferenças entre Olá vários tipos de Blobs.
     4. Opcionalmente, especifique uma pasta de destino no qual os ficheiros selecionados Olá serão carregados. Se a pasta de destino Olá não existir, será criado.
     5. Selecione **Upload**.
   * **Carregar um contentor do blob tooa pasta**

     1. Na barra de ferramentas do painel Olá principal, selecione **carregar**e, em seguida, **carregar pasta** no menu de Olá pendente.

        ![Menu Carregar pasta][17]
     2. No Olá **carregamento pasta** caixa de diálogo, reticências Olá selecione (**...** ) botão no lado direito de Olá de Olá **pasta** pasta de Olá de tooselect de caixa de texto cujo conteúdo pretende tooupload.

        ![Carregue as opções de pastas][18]
     3. Especifique o tipo Olá de **Blob tipo**. artigo de Olá [introdução ao Blob storage do Azure através do .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explica Olá as diferenças entre Olá vários tipos de Blobs.
     4. Opcionalmente, especifique uma pasta de destino no qual Olá conteúdo da pasta selecionado será carregado. Se a pasta de destino Olá não existir, será criado.
     5. Selecione **Upload**.
   * **Transferir o computador local blob tooyour**

     1. Selecione o blob Olá desejar toodownload.
     2. Na barra de ferramentas do painel Olá principal, selecione **transferir**.
     3. No Olá **Especifique qual toosave Olá transferidos blob** caixa de diálogo, especifique onde pretende que o blob Olá transferido de localização de Olá e Olá nome desejar toogive-lo.  
     4. Selecione **Guardar**.
   * **Abra um blob no seu computador local**

     1. Selecione o blob Olá desejar tooopen.
     2. Na barra de ferramentas do painel Olá principal, selecione **abra**.
     3. blob Olá será transferida e aberta utilizando a aplicação Olá associada ao tipo de ficheiro do blob Olá subjacente.
   * **Copiar uma área de transferência do blob toohello**

     1. Selecione o blob Olá desejar toocopy.
     2. Na barra de ferramentas do painel Olá principal, selecione **cópia**.
     3. No painel esquerdo Olá, navegue tooanother contentor de blob e faça duplo clique tooview-lo no painel principal Olá.
     4. Na barra de ferramentas do painel Olá principal, selecione **colar** toocreate uma cópia do blob Olá.
   * **Eliminar um blob**

     1. Selecione o blob Olá desejar toodelete.
     2. Na barra de ferramentas do painel Olá principal, selecione **eliminar**.
     3. Selecione **Sim** toohello diálogo de confirmação.

## <a name="next-steps"></a>Passos seguintes
* Olá vista [mais recente notas de versão do Explorador de armazenamento (pré-visualização) e vídeos](http://www.storageexplorer.com).
* Saiba como demasiado[criar aplicações utilizar blobs do Azure, tabelas, filas e os ficheiros](https://azure.microsoft.com/documentation/services/storage/).

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
