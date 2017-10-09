---
title: credenciais da conta do storage aaaManage matriz Virtual StorSimple | Microsoft Docs
description: "Explica como pode utilizar Olá tooadd da página de configuração do Gestor de dispositivos do StorSimple, editar, eliminar ou chaves de segurança de Olá rotate para credenciais de conta de armazenamento associadas Olá matriz Virtual StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 234bf8bb-d5fe-40be-9d25-721d7482bc3b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: 22a0341eae0b89020065be4dbfaae77999f8be0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-storage-account-credentials-for-storsimple-virtual-array"></a>Utilize o Gestor de dispositivos StorSimple toomanage credenciais da conta de armazenamento para a matriz Virtual StorSimple

## <a name="overview"></a>Descrição geral
Olá **configuração** secção do painel de serviço Gestor de dispositivos do StorSimple Olá da sua matriz de Virtual StorSimple apresenta parâmetros de serviço global Olá que podem ser criados no Olá serviço StorSimple Manager. Estes parâmetros podem ser aplicados tooall Olá dispositivos ligados toohello serviço e incluem:

* Credenciais da conta de armazenamento
* Registos de controlo de acesso
  
  ![Dashboard de serviço do Gestor de dispositivos](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccts-dashboard.png)  

Este tutorial explica como pode adicionar, editar ou eliminar as credenciais da conta de armazenamento para a matriz de Virtual StorSimple. informações de Olá neste tutorial aplica-se apenas toohello matriz Virtual StorSimple. Para obter informações sobre como contas de armazenamento toomanage série 8000, consulte [utilize Olá toomanage de serviço StorSimple Manager, a conta do storage](storsimple-manage-storage-accounts.md).

Conta de armazenamento credenciais contenham credenciais Olá Olá dispositivo utiliza tooaccess sua conta do storage com o fornecedor de serviço em nuvem. Para contas de armazenamento do Microsoft Azure, estas são as credenciais, tais como o nome da conta Olá e a chave de acesso primária de Olá.

No Olá **as credenciais da conta de armazenamento** painel, a conta de armazenamento de todas as credenciais que são criadas para Olá faturação da subscrição são apresentadas em formato tabular contendo Olá seguintes informações:

* **Nome** – Olá exclusivo atribuído toohello conta quando foi criado.
* **SSL ativado** – se hello SSL esteja ativado e a comunicação do dispositivo para a nuvem é efetuada através de canal seguro Olá.
  
  ![Secção de configuração](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccountcredentials-blade.png)

tarefas mais comuns Olá relacionadas com as credenciais da conta de toostorage podem ser efetuadas num Olá **as credenciais da conta de armazenamento** painel são:

* Adicionar uma credencial da conta de armazenamento
* Editar uma credencial de conta de armazenamento
* Eliminar uma credencial de conta de armazenamento

## <a name="types-of-storage-account-credentials"></a>Tipos de credenciais de conta de armazenamento
Existem três tipos de credenciais de conta de armazenamento que podem ser utilizados com o dispositivo StorSimple.

* **As credenciais da conta de armazenamento gerado automaticamente** – como o nome de Olá sugere, este tipo de credencial de conta de armazenamento é gerado automaticamente quando o serviço de Olá é criado pela primeira vez. toolearn mais informações sobre como esta credencial de conta de armazenamento é criado, consulte [criar um novo serviço](storsimple-virtual-array-manage-service.md#create-a-service).
* **as credenciais da conta de armazenamento na subscrição do serviço de Olá** – estas são a conta de armazenamento do Azure Olá Olá de credenciais que estão associadas a mesma subscrição do serviço de Olá. toolearn mais informações sobre como são criados estas credenciais de conta de armazenamento, consulte [sobre contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md).
* **as credenciais da conta de armazenamento fora da subscrição do serviço Olá** – estes são credenciais de conta de armazenamento do Azure Olá que não estão associadas ao seu serviço e Olá provável que existiam antes do serviço foi criado.

## <a name="add-a-storage-account-credential"></a>Adicionar uma credencial da conta de armazenamento
Pode adicionar uma configuração de serviço do armazenamento conta credencial tooyour Gestor de dispositivos do StorSimple, fornecendo um exclusivo credenciais de acesso e o nome amigáveis que estão ligados toohello conta de armazenamento. Tem também a opção Olá de ativação Olá secure sockets layer (SSL) modo toocreate um canal seguro para a comunicação de rede entre a nuvem de dispositivo e Olá.

Pode criar várias contas para um fornecedor de serviços de nuvem especificada. Enquanto está a ser guardada credencial de conta de armazenamento Olá, o serviço de Olá tenta toocommunicate com o fornecedor de serviço em nuvem. as credenciais de Olá e material de acesso de Olá que forneceu são autenticados neste momento. Uma credencial de conta de armazenamento é criada apenas se a autenticação de Olá for bem sucedida. Se falhar a autenticação de Olá, em seguida, é apresentada uma mensagem de erro apropriada.

Utilize Olá credenciais da conta do storage do Azure tooadd procedimentos a seguir:

* Olá, tooadd uma credencial de conta de armazenamento que tenha a mesma subscrição do Azure como o serviço do Gestor de dispositivos de Olá
* tooadd uma credencial de conta de armazenamento do Azure que está fora da subscrição de serviço do Gestor de dispositivos de Olá

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a>Olá, tooadd uma credencial de conta de armazenamento que tenha a mesma subscrição do Azure como o serviço do Gestor de dispositivos de Olá

1. Navegue tooyour serviço Gestor de dispositivos, selecione e faça duplo clique. Esta ação abre Olá **descrição geral** painel.
2. Selecione **as credenciais da conta de armazenamento** dentro Olá **configuração** secção.
3. Clique em **Adicionar**.
4. No Olá **adicionar uma conta de armazenamento** painel, Olá a seguir:
   
    1. Para **subscrição**, selecione **atual**.
    2. Forneça o nome de Olá da sua conta de armazenamento do Azure.
    3. Selecione **ativar** toocreate um canal seguro para a comunicação de rede entre a nuvem de dispositivo e Olá do StorSimple. Selecione **desativar** apenas se estiver a utilizar uma nuvem privada.
    4. Clique em **Adicionar**. Será notificado depois de conta de armazenamento Olá é criada com êxito.<br></br>
   
        ![Adicionar uma credencial de conta de armazenamento existente](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

#### <a name="tooadd-an-azure-storage-account-credential-that-is-outside-of-hello-device-manager-service-subscription"></a>tooadd uma credencial de conta de armazenamento do Azure que está fora da subscrição de serviço do Gestor de dispositivos de Olá

1. Navegue tooyour serviço Gestor de dispositivos, selecione e faça duplo clique. Esta ação abre Olá **descrição geral** painel.
2. Selecione **as credenciais da conta de armazenamento** dentro Olá **configuração** secção. Isto apresenta uma lista quaisquer credenciais de conta de armazenamento existente associadas Olá serviço StorSimple Manager do dispositivo.
3. Clique em **Adicionar**.
4. No Olá **adicionar uma conta de armazenamento** painel, Olá a seguir:
   
    1. Para **subscrição**, selecione **outros**.
   
    2. Forneça o nome de Olá das suas credenciais de conta de armazenamento do Azure.
   
    3. No Olá **chave de acesso de conta do Storage** caixa de texto, forneça Olá chave de acesso primária para a credencial da conta de armazenamento do Azure. tooget nesta chave, aceda a toohello serviço de armazenamento do Azure, selecione as suas credenciais de conta de armazenamento e, em **gerir chaves de conta**. Agora pode copiar a chave de acesso primária de Olá.
   
    4. tooenable SSL, clique em Olá **ativar** botão toocreate um canal seguro para a comunicação de rede entre o Gestor de dispositivos do StorSimple Olá e do serviço em nuvem. Clique em Olá **desativar** botão apenas se estiver a utilizar uma nuvem privada.
   
    5. Clique em **Adicionar**. Será notificado depois de credencial de conta de armazenamento Olá é criado com êxito.

5. Olá recém-criado credencial da conta de armazenamento é apresentado no painel de service Manager do StorSimple configurar dispositivo Olá em **as credenciais da conta de armazenamento**.
   
    ![Adicionar uma credencial de conta de armazenamento fora Olá subscrição de serviço do Gestor de dispositivos](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-outside-storageacct.png)

## <a name="edit-a-storage-account-credential"></a>Editar uma credencial de conta de armazenamento
Pode editar uma credencial de conta de armazenamento utilizada pelo seu dispositivo. Se editar uma credencial de conta de armazenamento que está atualmente em utilização, Olá campos disponíveis toomodify são a chave de acesso Olá e modo SSL Olá para credenciais de conta de armazenamento Olá. Pode fornecer a chave de acesso de armazenamento Olá novo ou modificar Olá **modo SSL ativar** seleção e guardar as definições de Olá atualizado.

#### <a name="tooedit-a-storage-account-credential"></a>tooedit uma credencial de conta de armazenamento
1. Navegue tooyour serviço Gestor de dispositivos, selecione e faça duplo clique. Esta ação abre Olá **descrição geral** painel.
2. Selecione **as credenciais da conta de armazenamento** dentro Olá **configuração** secção. Isto apresenta uma lista quaisquer credenciais de conta de armazenamento existente associadas Olá serviço StorSimple Manager do dispositivo.
3. Na lista de tabela Olá das credenciais de conta de armazenamento, selecione e faça duplo clique conta Olá que pretende que o toomodify.
4. Na credencial de conta de armazenamento Olá **propriedades** painel, Olá a seguir:
   
   1. Se necessário, pode modificar Olá **ativar SSL** seleção de modo.
   2. Pode escolher tooregenerate as chaves de acesso de credencial de conta de armazenamento. Para obter mais informações, consulte [voltar a gerar chaves de conta de armazenamento Olá](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys). Forneça a chave de credencial de conta Olá novo armazenamento. Para uma conta de armazenamento do Azure, esta é a chave de acesso primária de Olá.
   3. Clique em **guardar** , Olá parte superior do Olá **propriedades** as definições do painel toosave Olá. definições de Olá foram atualizadas em Olá **as credenciais da conta de armazenamento** painel.
      
      ![Editar uma credencial de conta de armazenamento](./media/storsimple-virtual-array-manage-storage-accounts/ova-edit-storageacct.png)

## <a name="delete-a-storage-account-credential"></a>Eliminar uma credencial de conta de armazenamento
> [!IMPORTANT]
> Pode eliminar uma credencial de conta de armazenamento apenas se não está em utilização. Se uma credencial de conta de armazenamento está a ser utilizado, será notificado.
> 
> 

#### <a name="toodelete-a-storage-account-credential"></a>toodelete uma credencial de conta de armazenamento
1. Navegue tooyour serviço Gestor de dispositivos, selecione e faça duplo clique. Esta ação abre Olá **descrição geral** painel.
2. Selecione **as credenciais da conta de armazenamento** dentro Olá **configuração** secção. Isto apresenta uma lista quaisquer credenciais de conta de armazenamento existente associadas Olá serviço StorSimple Manager do dispositivo.
3. Na lista de tabela Olá das credenciais de conta de armazenamento, selecione e faça duplo clique conta Olá que pretende que o toodelete.
4. Na credencial de conta de armazenamento Olá **propriedades** painel, Olá a seguir:
   
   1. Clique em **eliminar** credenciais de Olá toodelete.
   2. Quando lhe for pedido para confirmação, clique em **Sim** toocontinue com eliminação de Olá. a listagem tabular Olá está atualizado tooreflect Olá alterações.
      
      ![Eliminar uma credencial de conta de armazenamento](./media/storsimple-virtual-array-manage-storage-accounts/ova-del-storageacct.png)

## <a name="synchronizing-storage-account-credential-keys"></a>Sincronizar as chaves de credencial de conta de armazenamento
Por motivos de segurança, rotação da chave é frequentemente um requisito nos centros de dados. Um administrador do Microsoft Azure pode voltar a gerar ou alterar a chave primária ou secundária de Olá ao aceder diretamente a credencial de conta de armazenamento Olá (através do serviço de armazenamento do Microsoft Azure Olá). Olá serviço StorSimple Manager de dispositivo não ver automaticamente esta alteração.

tooinform Olá dispositivo do serviço StorSimple Manager alteração Olá, terá de tooaccess Olá dispositivo do serviço StorSimple Manager, aceder ao armazenamento de Olá credenciais de conta e, em seguida, sincronizar a chave de primária ou secundária de Olá (dependendo do que um foi alterada). serviço Olá, em seguida, obtém a chave mais recente Olá, encripta chaves Olá e envia Olá encriptados toohello chave dispositivo.

#### <a name="toosynchronize-keys-for-storage-account-credentials-in-hello-same-subscription-as-hello-service-azure-only"></a>Olá, chaves de toosynchronize para as credenciais da conta de armazenamento na mesma subscrição do serviço de Olá (apenas para o Azure)
1. No painel de destino de serviço Olá, selecione o seu serviço, faça duplo clique em serviço Olá, nome Serv. e, em seguida, no Olá **configuração** secção, clique em **as credenciais da conta de armazenamento**.
2. No Olá **as credenciais da conta de armazenamento** painel, na lista de Olá das credenciais de conta de armazenamento, selecione credencial de conta de armazenamento Olá cujas chaves que pretende que o toosynchronize.
3. No Olá **propriedades** painel Olá selecionada credencial da conta de armazenamento, Olá a seguir:
   
    1. Clique em **mais**e, em seguida, clique em **chave de acesso de sincronização**.
   
    2. Quando lhe for pedido para confirmação, clique em **chave sincronização** sincronização de Olá toocomplete.
    
4. Olá serviço Gestor de dispositivos do StorSimple, terá de chave de Olá tooupdate que anteriormente foi alterada no Olá serviço de armazenamento do Microsoft Azure. No Olá **sincronizar a chave de conta do storage** painel, se a chave de acesso primária de Olá foi alterada (regenerada), clique em principal e, em seguida, clique em **sincronização chave**. Se a chave secundária Olá foi alterado, clique em **secundário**e, em seguida, clique em **sincronização chave**.
   
    ![Chave de acesso de sincronização](./media/storsimple-virtual-array-manage-storage-accounts/ova-sync-acess-key.png)

## <a name="next-steps"></a>Passos seguintes
* Saiba como demasiado[administrar a matriz de Virtual StorSimple](storsimple-ova-web-ui-admin.md).

