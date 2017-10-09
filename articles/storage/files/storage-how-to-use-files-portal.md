---
title: "aaaHow toomanage File storage do Azure de Olá portal do Azure | Microsoft Docs"
description: "Saiba toouse Olá toomanage portal do Azure File storage do Azure."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 6ad2fbbf9ee2f86748b1b175d0f63274144dc5eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a>Como toouse File storage do Azure de Olá Portal do Azure
Olá [portal do Azure](https://portal.azure.com) fornece uma interface de utilizador para gerir o File storage do Azure. Pode efetuar Olá seguintes ações a partir do seu browser web:

* Criar Partilhas de Ficheiros
* Carregar e transferir ficheiros tooand da partilha de ficheiros.
* Monitorizar a utilização real do Olá de cada partilha de ficheiros.
* Ajuste a quota de tamanho da partilha de ficheiros de Olá.
* Copie Olá montagem comandos toouse toomount partilhar o ficheiro de um cliente Windows ou Linux.

## <a name="create-file-share"></a>Criar a partilha de ficheiros
1. Inicie sessão no toohello portal do Azure.
2. No menu de navegação de Olá, clique em **contas do Storage** ou **contas do Storage (clássica)**.
    
    ![Captura de ecrã que mostra como de partilha de ficheiros de toocreate no portal de Olá](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. Escolha a sua conta de armazenamento.

    ![Captura de ecrã que mostra como de partilha de ficheiros de toocreate no portal de Olá](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. Escolha o serviço “Ficheiros”.

    ![Captura de ecrã que mostra como de partilha de ficheiros de toocreate no portal de Olá](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. Clique em "Partilhas de ficheiros" e seguir Olá ligação toocreate partilhar o seu primeiro ficheiro.

    ![Captura de ecrã que mostra como de partilha de ficheiros de toocreate no portal de Olá](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. Preencha nome Olá da partilha de ficheiros e o tamanho de Olá de Olá ficheiro partilha (cópia de segurança too5120 GB) toocreate sua primeira partilha de ficheiros. Quando tiver sido criada a partilha de ficheiros de Olá, possível montá-la a partir de qualquer sistema de ficheiros que suporta SMB 2.1 ou SMB 3.0. Pode clicar em **Quota** no Olá ficheiro partilha toochange Olá tamanho Olá do ficheiro de cópia de segurança too5120 GB. Consulte demasiado[Calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/) custo do armazenamento Olá tooestimate da utilização do File storage do Azure.

    ![Captura de ecrã que mostra como de partilha de ficheiros de toocreate no portal de Olá](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a>Carregar e transferir os ficheiros
1. Escolha uma partilha de ficheiros que já criou.

    ![Captura de ecrã que mostra como ficheiros tooupload e transferências de Olá portal](./media/storage-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. Clique em **carregar** para abrir a interface de utilizador de Olá para carregamento de ficheiros.

    ![Captura de ecrã que mostra como tooupload ficheiros a partir do portal de Olá](./media/storage-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a>Ligar toofile partilha
-  Clique em **Connect** obter Olá linha de comandos para partilha de ficheiros de Olá a montagem do Windows e Linux. Para os utilizadores do Linux, pode também consultar demasiado[como toouse File storage do Azure com o Linux](../storage-how-to-use-files-linux.md) para obter mais instruções de montagem para outras as distribuições do Linux.

    ![Captura de ecrã que mostra como toomount Olá partilha de ficheiros](./media/storage-how-to-use-files-portal/use-files-portal-connect.png)
-  Pode copiar Olá comandos para montar ficheiros partilham no Windows ou Linux e execução-lo da máquina de VM do Azure ou no local.

    ![Captura de ecrã que mostra os comandos de montagem de Olá para o Windows e Linux](./media/storage-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

**Sugestão:**  
toofind chave de acesso da conta de armazenamento de Olá de montagem, clique em **visualizar chaves de acesso para esta conta de armazenamento** na parte inferior de Olá de Olá ligar página.

## <a name="see-also"></a>Consultar também
Consulte as ligações para obter mais informações sobre o Armazenamento de ficheiros do Azure.

* [FAQ](../storage-files-faq.md)
* [Resolução de Problemas no Windows](storage-troubleshoot-windows-file-connection-problems.md)      
* [Resolução de Problemas no Linux](storage-troubleshoot-linux-file-connection-problems.md)    