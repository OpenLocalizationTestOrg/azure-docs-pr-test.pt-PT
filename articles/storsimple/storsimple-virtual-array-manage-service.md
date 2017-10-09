---
title: "aaaDeploy serviço Gestor de dispositivos do StorSimple | Microsoft Docs"
description: "Explica como toocreate e delete hello do serviço StorSimple Manager de dispositivos no portal do Azure de Olá e descreve como toomanage Olá chave de registo do serviço."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a>Implementar o serviço do Gestor de dispositivos do StorSimple Olá matriz Virtual StorSimple
## <a name="overview"></a>Descrição geral

Olá serviço Gestor de dispositivos do StorSimple é executado no Microsoft Azure e liga toomultiple StorSimple dispositivos. Depois de criar serviço Olá, pode utilizá-lo dispositivos Olá toomanage Olá Microsoft Azure portal em execução num browser. Isto permite-lhe toomonitor todos os dispositivos de Olá que estão ligado toohello Gestor de dispositivos do StorSimple service a partir de uma única localização central, deste modo, minimizando o fardo administrativo.

Olá comuns tarefas relacionadas tooa serviço StorSimple Manager de dispositivos são:

* Criar um serviço
* Eliminar um serviço
* Obter a chave de registo do serviço de Olá
* Regenerar a chave de registo do serviço de Olá

Este tutorial descreve como tooperform de Olá tarefas anteriores. informações de Olá contidas neste artigo são aplicável apenas tooStorSimple Virtual as matrizes. Para obter mais informações sobre série 8000 do StorSimple, visite demasiado[implementar um serviço StorSimple Manager](storsimple-manage-service.md).

## <a name="create-a-service"></a>Criar um serviço

toocreate um serviço, terá de toohave:

* Uma subscrição com um Enterprise Agreement
* Uma conta de armazenamento do Microsoft Azure Active Directory
* Olá, as informações de faturação que são utilizadas para gestão de acesso

Também pode escolher toogenerate uma conta de armazenamento ao criar o serviço de Olá.

Um único serviço pode gerir vários dispositivos. No entanto, um dispositivo não pode abranger vários serviços. Uma grande empresa pode ter vários toowork de instâncias de serviço com diferentes subscrições, as organizações ou até mesmo as localizações de implementação.

> [!NOTE]
> Terá de instâncias separadas de dispositivos de série do Gestor de dispositivos do StorSimple serviço toomanage 8000 do StorSimple e matrizes Virtual StorSimple.


Efetue Olá os seguintes passos toocreate um serviço.

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a>Eliminar um serviço

Antes de eliminar um serviço, certifique-se de que não existem dispositivos ligados a estiver a utilizar. Se o serviço de Olá está a ser utilizado, desative dispositivos Olá ligado. Olá desativar operação irá sever ligação Olá entre dispositivos de Olá e o serviço de Olá, mas manter os dados do dispositivo Olá na nuvem de Olá.

> [!IMPORTANT]
> Depois de um serviço é eliminado, não é possível reverter a operação de Olá. Terá de qualquer dispositivo que estava a utilizar o serviço de Olá toobe antes de poder ser utilizada com outro serviço de reposição de fábrica. Neste cenário, os dados locais Olá no dispositivo Olá, bem como a configuração de Olá, serão perdidas.
 

Efetue Olá os seguintes passos toodelete um serviço.

#### <a name="toodelete-a-service"></a>toodelete um serviço

1. Aceda demasiado**todos os recursos**. Pesquisa para o seu serviço do Gestor de dispositivos do StorSimple. Selecione o serviço de Olá pretende toodelete.
   
    ![Selecione toodelete de serviço](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. Aceda tooyour serviço dashboard tooensure existem não existem dispositivos ligados toohello serviço. Se não houver nenhuma dispositivos registados com este serviço, verá também um efeito de toohello de mensagem de faixa. Clique em **Eliminar**.
   
    ![Eliminar o serviço](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. Quando lhe for pedido para confirmação, clique em **Sim** na notificação de confirmação de Olá. 
   
    ![Confirmar eliminação do serviço](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. Pode demorar alguns minutos para Olá serviço toobe eliminado. Depois de Olá serviço é eliminado com êxito, será notificado.
   
    ![Eliminação do serviço concluída com êxito](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

lista de Olá de serviços será atualizada.

 ![Lista atualizada de serviços](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a>Obter a chave de registo do serviço de Olá
Depois de ter criado com êxito um serviço, terá de tooregister serviço Olá no dispositivo StorSimple. tooregister primeiro dispositivo StorSimple, será necessário Olá chave de registo do serviço. tooregister dispositivos adicionais com um serviço StorSimple, terá de chave de registo Olá e Olá serviço chave de encriptação dados (que é gerado no primeiro dispositivo de Olá durante o registo). Para obter mais informações sobre a chave de encriptação de dados de serviço Olá, consulte [segurança do StorSimple](storsimple-security.md). Pode obter a chave de registo Olá acedendo Olá **chaves** painel para o seu serviço.

Efetue Olá chave de registo de serviço de Olá tooget passos a seguir.

#### <a name="tooget-hello-service-registration-key"></a>chave de registo do serviço de Olá tooget
1. No Olá **Gestor de dispositivos do StorSimple** painel, vá demasiado**gestão &gt;**  **chaves**.
   
   ![Painel de chaves](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. No Olá **chaves** aparece do painel, uma chave de registo do serviço. Copie a chave de registo de Olá com ícone de cópia de Olá. 

Manter a chave de registo do serviço de Olá numa localização segura. Terá esta chave, bem como chave de encriptação de dados de serviço Olá, tooregister dispositivos adicionais com este serviço. Depois de obter a chave de registo do serviço de Olá, terá de tooconfigure o dispositivo através do Olá do Windows PowerShell para StorSimple interface.

## <a name="regenerate-hello-service-registration-key"></a>Regenerar a chave de registo do serviço de Olá
Precisa de tooregenerate uma chave de registo do serviço se for necessário tooperform rotação da chave ou se a lista de Olá dos administradores de serviço foi alterada. Quando voltar a gerar chave Olá, a nova chave de Olá é utilizado apenas para registar dispositivos subsequentes. dispositivos de Olá que já foram registados não são afetados por este processo.

Efetue Olá os seguintes passos tooregenerate uma chave de registo do serviço.

#### <a name="tooregenerate-hello-service-registration-key"></a>chave de registo do serviço de Olá tooregenerate
1. No Olá **Gestor de dispositivos do StorSimple** painel, vá demasiado**gestão &gt;**  **chaves**.
   
   ![Painel de chaves](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. No Olá **chaves** painel, clique em **regenerar**.
   
   ![Clique em voltar a gerar](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. No Olá **chave de registo do serviço de voltar a gerar** painel, reveja Olá necessária ação ao hello chaves são regeneradas. Todos os dispositivos subsequentes Olá registados com este serviço irão utilizar a nova chave de registo Olá. Clique em **regenerar** tooconfirm. Será notificado depois de concluída a registo Olá.
   
   ![Confirme a regeneração da chave](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. Será apresentada uma nova chave de registo do serviço.
   
    ![Confirme a regeneração da chave](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   Copie esta chave e guarde-a para registar os novos dispositivos com este serviço.

## <a name="next-steps"></a>Passos seguintes
* Saiba como demasiado[começar](storsimple-virtual-array-deploy1-portal-prep.md) com uma matriz de Virtual StorSimple.
* Saiba como demasiado[administrar o dispositivo StorSimple](storsimple-ova-web-ui-admin.md).

