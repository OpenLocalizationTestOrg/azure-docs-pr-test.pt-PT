---
title: "Olá aaaDeploy serviço StorSimple Manager | Microsoft Docs"
description: "Explica como toocreate e delete Olá serviço StorSimple Manager na Olá portal clássico do Azure e descreve como toomanage Olá chave de registo do serviço."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: bc1d5650-275c-42ed-bc77-cdb596f85943
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f49b647d91b03bb89ebd0e5cce196e50e3c00296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-manager-service-in-hello-azure-classic-portal"></a>Implementar o serviço StorSimple Manager Olá Olá portal clássico do Azure

## <a name="overview"></a>Descrição geral
Olá serviço StorSimple Manager é executado no Microsoft Azure e liga toomultiple StorSimple dispositivos. Depois de criar serviço Olá, pode utilizá-lo dispositivos Olá toomanage Olá Microsoft Azure clássico portal em execução num browser. Isto permite-lhe toomonitor todos os dispositivos de Olá que estão ligado toohello StorSimple Manager service a partir de uma única localização central, deste modo, minimizando o fardo administrativo.

página de destino do StorSimple Manager Olá apresenta uma lista de todos os serviços de StorSimple Manager Olá pode utilizar toomanage os dispositivos de armazenamento StorSimple. Para cada serviço StorSimple Manager, Olá seguintes informações é apresentada na página de StorSimple Manager Olá:

* **Nome** – nome de Olá que foi atribuído o serviço do StorSimple Manager tooyour quando foi criado. **Não é possível alterar o nome do serviço Olá depois do serviço de Olá é criado. Isto também se aplica para outras entidades, tais como os dispositivos, volumes, contentores de volume e políticas de cópia de segurança que não não possível mudar o nome no portal clássico do Azure de Olá.**
* **Estado** – Olá estado do serviço de Olá, que pode ser **Active Directory**, **criar**, ou **Online**.
* **Localização** – Olá localização geográfica na qual Olá StorSimple dispositivo será implementado.
* **Subscrição** – hello subscrição que está associada ao seu serviço de faturação.

tarefas comuns de Olá que podem ser efetuadas através de página do StorSimple Manager Olá são:

* Criar um serviço
* Eliminar um serviço
* Obter a chave de registo do serviço de Olá
* Regenerar a chave de registo do serviço de Olá

Este tutorial descreve como tooperform, cada uma destas tarefas.

## <a name="create-a-service"></a>Criar um serviço
Olá utilize **criação rápida** opção toocreate um serviço StorSimple Manager se pretender toodeploy o dispositivo StorSimple. toocreate um serviço, terá de toohave:

* Uma subscrição com um Enterprise Agreement
* Uma conta de armazenamento do Microsoft Azure Active Directory
* Olá, as informações de faturação que são utilizadas para gestão de acesso

Também pode escolher toogenerate uma conta do storage predefinida quando cria Olá service.

Um único serviço pode gerir vários dispositivos. No entanto, um dispositivo não pode abranger vários serviços. Uma grande empresa pode ter vários toowork de instâncias de serviço com diferentes subscrições, as organizações ou até mesmo as localizações de implementação. Tenha em atenção que precisar de separar as instâncias de dispositivos de série do StorSimple Manager serviço toomanage 8000 do StorSimple e matrizes Virtual StorSimple.

> [!IMPORTANT] 
> Se tiver um serviço não utilizado criado (nenhum dispositivo de operações que foram efetuadas neste recurso) anterior tooAugust 2016, não podem ser gerido através do portal do Azure ou o portal clássico do Azure. Recomendamos que crie um novo serviço no Olá portal do Azure.

Efetue Olá os seguintes passos toocreate um serviço.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

## <a name="delete-a-service"></a>Eliminar um serviço
Antes de eliminar um serviço, certifique-se de que não existem dispositivos ligados a estiver a utilizar. Se o serviço de Olá está a ser utilizado, desative dispositivos Olá ligado. Olá desativar operação irá sever ligação Olá entre dispositivos de Olá e o serviço de Olá, mas manter os dados do dispositivo Olá na nuvem de Olá.

> [!IMPORTANT] 
> Depois de um serviço é eliminado, não é possível reverter a operação de Olá. Terá de qualquer dispositivo que estava a utilizar o serviço de Olá toobe antes de poder ser utilizada com outro serviço de reposição de fábrica. Neste cenário, os dados locais Olá no dispositivo Olá, bem como a configuração de Olá, serão perdidas.

Efetue Olá os seguintes passos toodelete um serviço.

### <a name="toodelete-a-service"></a>toodelete um serviço
1. No Olá **serviço StorSimple Manager** página serviço Olá Selecione se pretende toodelete.
2. Clique em **eliminar** em Olá parte inferior da página Olá.
3. Clique em **Sim** na notificação de confirmação de Olá. Pode demorar alguns minutos para Olá serviço toobe eliminado.

## <a name="get-hello-service-registration-key"></a>Obter a chave de registo do serviço de Olá
Depois de ter criado com êxito um serviço, terá de tooregister serviço Olá no dispositivo StorSimple. tooregister primeiro dispositivo StorSimple, será necessário Olá chave de registo do serviço. tooregister dispositivos adicionais com um serviço StorSimple, terá de chave de registo Olá e Olá serviço chave de encriptação dados (que é gerado no primeiro dispositivo de Olá durante o registo). Para obter mais informações sobre a chave de encriptação de dados de serviço Olá, consulte [segurança do StorSimple](storsimple-security.md). Pode obter a chave de registo Olá acedendo **chave de registo** no Olá **serviços** página.

Efetue Olá chave de registo de serviço de Olá tooget passos a seguir.

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

Manter a chave de registo do serviço de Olá numa localização segura. Terá esta chave, bem como chave de encriptação de dados de serviço Olá, tooregister dispositivos adicionais com este serviço. Depois de obter a chave de registo do serviço de Olá, terá de tooconfigure o dispositivo através do Olá do Windows PowerShell para StorSimple interface.

Para obter detalhes sobre como toouse esta chave, consulte de registo [passo 3: configurar e registar o dispositivo de Olá através do Windows PowerShell para StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

## <a name="regenerate-hello-service-registration-key"></a>Regenerar a chave de registo do serviço de Olá
Precisa de tooregenerate uma chave de registo do serviço se for necessário tooperform rotação da chave ou se a lista de Olá dos administradores de serviço foi alterada. Quando voltar a gerar chave Olá, a nova chave de Olá é utilizado apenas para registar dispositivos subsequentes. dispositivos de Olá que já foram registados não são afetados por este processo.

Efetue Olá os seguintes passos tooregenerate uma chave de registo do serviço.

### <a name="tooregenerate-hello-service-registration-key"></a>chave de registo do serviço de Olá tooregenerate
1. No Olá **serviço StorSimple Manager** página, clique em **chave de registo**.
2. No Olá **chave de registo do serviço** caixa de diálogo, clique em **regenerar**.
3. Verá uma mensagem de confirmação. Clique em **OK** toocontinue com a regeneração de uma vez Olá.
4. Será apresentada uma nova chave de registo do serviço.
5. Copie esta chave e guarde-a para registar os novos dispositivos com este serviço.
6. Clique Olá ícone de verificação ![Ícone de verificação](./media/storsimple-manage-service/HCS_CheckIcon.png) tooclose esta caixa de diálogo.

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre Olá [processo de implementação do StorSimple](storsimple-deployment-walkthrough-u2.md).
* Saiba mais sobre [gerir a conta de armazenamento StorSimple](storsimple-manage-storage-accounts.md).
* Saiba mais sobre como demasiado[utilize Olá tooadminister de serviço StorSimple Manager, o dispositivo StorSimple](storsimple-manager-service-administration.md).
