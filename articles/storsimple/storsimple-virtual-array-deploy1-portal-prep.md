---
title: "aaaPortal preparação para a matriz Virtual StorSimple | Microsoft Docs"
description: "Primeiro toodeploy tutorial matriz virtual StorSimple envolve a preparação Olá portal do Azure"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 68a4cfd3-94c9-46cb-805c-46217290ce02
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5332b235e7296a9274f2e7dafcdf72f4b9cdadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---prepare-hello-azure-portal"></a>Implementar StorSimple Virtual matriz - preparar Olá portal do Azure

![](./media/storsimple-virtual-array-deploy1-portal-prep/getstarted4.png)
## <a name="overview"></a>Descrição geral

Este é o artigo primeiro Olá na série de Olá dos tutoriais de implementação necessária toocompletely implementar a matriz de virtual como um servidor de ficheiros ou um servidor de iSCSI através do modelo do Resource Manager Olá. Este artigo descreve Olá preparação necessária toocreate e configurar o seu tooprovisioning de anteriores de serviço do Gestor de dispositivos do StorSimple uma matriz de virtual. Este artigo também contém ligações saída tooa implementação configuração e de lista de verificação de pré-requisitos de configuração.

Terá de administrador privilégios toocomplete Olá instalação e configuração processo. Recomendamos que reveja a lista de verificação de configuração de implementação de Olá antes de começar. preparação de portal Olá demora menos de 10 minutos.

informações de Olá publicadas neste artigo aplica-se a implementação toohello de matrizes de Virtual StorSimple no Olá portal do Azure e na nuvem do Microsoft Azure Government.

### <a name="get-started"></a>Introdução
fluxo de trabalho de implementação de Olá consiste em preparação portal Olá, uma matriz virtual no seu ambiente virtualizado de aprovisionamento e concluir a configuração de Olá. tooget à implementação de matriz Virtual StorSimple Olá como um servidor de ficheiros ou um servidor de iSCSI, é necessário toohello toorefer recursos apresentados a seguir.

#### <a name="deployment-articles"></a>Artigos de implementação

toodeploy a matriz de Virtual StorSimple, consulte toohello seguintes artigos Olá prescrita sequência.

| **#** | **Neste passo** | **Fazê-lo...** | **E utilizar estes documentos.** |
| --- | --- | --- | --- |
| 1. |**Configurar Olá portal do Azure** |Criar e configurar o seu tooprovisioning de anteriores de serviço do Gestor de dispositivos do StorSimple uma matriz de Virtual StorSimple. |[Preparar o portal de Olá](storsimple-virtual-array-deploy1-portal-prep.md) |
| 2. |**Aprovisionar Olá matriz Virtual** |Para o Hyper-V, Aprovisione e ligar tooa matriz Virtual StorSimple num sistema anfitrião com Hyper-V no Windows Server 2012 R2, Windows Server 2012 ou Windows Server 2008 R2. <br></br> <br></br> Para VMware, Aprovisione e ligar tooa matriz Virtual StorSimple num sistema anfitrião com o VMware ESXi 5.5 e acima.<br></br> |[Aprovisionar uma matriz virtual no Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) <br></br> <br></br> [Aprovisionar uma matriz virtual do VMware](storsimple-virtual-array-deploy2-provision-vmware.md) |
| 3. |**Configurar Olá matriz Virtual** |Para o servidor de ficheiros, execute a configuração inicial, registar o servidor de ficheiros do StorSimple e concluir a configuração de dispositivo Olá. Em seguida, pode aprovisionar partilhas SMB. <br></br> <br></br> Para o servidor de iSCSI, execute a configuração inicial, registar o servidor de iSCSI StorSimple e concluir a configuração de dispositivo Olá. Em seguida, pode aprovisionar volumes de iSCSI. |[Configurar a matriz virtual como servidor de ficheiros](storsimple-virtual-array-deploy3-fs-setup.md)<br></br> <br></br>[Configurar matriz virtual como servidor de iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md) |

Agora pode começar tooset segurança Olá portal do Azure.

## <a name="configuration-checklist"></a>Lista de verificação de configuração

lista de verificação de configuração de Olá descreve as informações de Olá que terá de toocollect antes de configurar o software de Olá na sua matriz de Virtual StorSimple. A preparar a estas informações à frente das ajuda-o tempo otimizar Olá processo de implementação de dispositivo do StorSimple Olá no seu ambiente. Dependendo se a matriz de Virtual StorSimple é implementada como um servidor de ficheiros ou um servidor de iSCSI, precisa de um dos Olá seguintes listas de verificação.

* Transferir Olá [StorSimple Virtual matriz ficheiro servidor de configuração de lista de verificação](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).
* Transferir Olá [iSCSI da matriz Virtual StorSimple lista de verificação de configuração de servidor](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).

## <a name="prerequisites"></a>Pré-requisitos

Aqui poderá encontrar Olá pré-requisitos de configuração do serviço StorSimple Manager de dispositivo, a matriz Virtual StorSimple e rede de centro de dados de Olá.

### <a name="for-hello-storsimple-device-manager-service"></a>Para Olá serviço StorSimple Manager de dispositivo

Antes de começar, certifique-se de que:

* Tem a conta Microsoft com credenciais de acesso.
* Tem a conta do Storage do Microsoft Azure com credenciais de acesso.
* A subscrição do Microsoft Azure deve estar ativada para o serviço do Gestor de dispositivos do StorSimple.

### <a name="for-hello-storsimple-virtual-array"></a>Para Olá matriz Virtual StorSimple

Antes de implementar uma matriz de virtual, certifique-se de que:

* Tem acesso tooa anfitrião sistema que executa o Hyper-V no Windows Server 2008 R2 ou posterior ou VMware (ESXi 5.5 ou posterior) que pode ser utilizado tooa aprovisionar um dispositivo.
* sistema de anfitrião de Olá é capaz de toodedicate Olá os seguintes recursos tooprovision a matriz de virtual:
  
  * Um mínimo de 4 núcleos.
  * Pelo menos 8 GB de RAM. Se planear matriz de virtual Olá tooconfigure como servidor de ficheiros, 8 GB suporta ficheiros de milhões de 2. Terá de ficheiros de 2-4 milhões de toosupport do 16 GB de RAM.
  * Uma interface de rede.
  * Um disco virtual 500 GB para os dados de sistema.

### <a name="for-hello-datacenter-network"></a>Para a rede de centro de dados de Olá

Antes de começar, certifique-se de que:

* rede de Olá no seu centro de dados está configurada de acordo com requisitos de rede Olá para o dispositivo StorSimple. Para obter mais informações, consulte Olá [requisitos de sistema de matriz Virtual StorSimple](storsimple-ova-system-requirements.md).
* A matriz de Virtual StorSimple tem uma banda de Internet de Mbps 5 dedicado (ou mais) disponível em todas as vezes. Esta largura de banda não deve ser partilhada com outras aplicações.

## <a name="step-by-step-preparation"></a>Preparação passo a passo

Utilize Olá seguir instruções passo a passo tooprepare seu portal para Olá serviço StorSimple Manager do dispositivo.

## <a name="step-1-create-a-new-service"></a>Passo 1: Criar um novo serviço

Uma única instância do serviço do Gestor de dispositivos do StorSimple de Olá pode gerir várias matrizes de Virtual StorSimple. Efetue Olá os seguintes passos toocreate uma instância do serviço de Gestor de dispositivos do StorSimple Olá. Se tiver um serviço toomanage existente do Gestor de dispositivos do StorSimple as matrizes de virtuais, ignore este passo e vá demasiado[passo 2: chave de registo do serviço de Olá Get](#step-2-get-the-service-registration-key).

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

> [!IMPORTANT]
> Se não tiver ativado a criação automática de Olá de uma conta de armazenamento com o serviço, terá de toocreate pelo menos uma conta de armazenamento depois de ter criado com êxito um serviço.
> 
> * Se não tiver criado uma conta do storage automaticamente, aceda demasiado[configurar uma nova conta de armazenamento para o serviço de Olá](#optional-step-configure-a-new-storage-account-for-the-service) para obter instruções detalhadas.
> * Se tiver ativado a criação de uma conta de armazenamento automática Olá, vá demasiado[passo 2: chave de registo do serviço de Olá Get](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Passo 2: Obter a chave de registo do serviço de Olá

Depois de Olá serviço StorSimple Manager de dispositivo está a funcionar, terá de chave de registo do serviço de Olá tooget. Esta chave é utilizada tooregister e ligar o dispositivo StorSimple com o serviço de Olá.

Efetuar Olá os seguintes passos no Olá [portal do Azure](https://portal.azure.com/).

[!INCLUDE [storsimple-virtual-array-get-service-registration-key](../../includes/storsimple-virtual-array-get-service-registration-key.md)]

> [!NOTE]
> Olá chave de registo do serviço é utilizado tooregister Olá todos os dispositivos de Gestor de dispositivos do StorSimple que necessitam de tooregister com o serviço do Gestor de dispositivos do StorSimple.
> 
> 

## <a name="step-3-download-hello-virtual-array-image"></a>Passo 3: Transferir a imagem de matriz virtual Olá

Depois de ter a chave de registo do serviço de Olá, terá de toodownload Olá matriz virtual adequado imagem tooprovision uma matriz de virtual no sistema anfitrião. as imagens de matriz virtual Olá são específicas do sistema operativo e podem ser transferidas a partir da página de início rápido Olá no Olá portal do Azure.

> [!IMPORTANT]
> software Olá em execução no Olá matriz Virtual StorSimple só pode ser utilizado com Olá serviço StorSimple Manager do dispositivo.
> 
> 

Efetuar Olá os seguintes passos no Olá [portal do Azure](https://portal.azure.com/).

#### <a name="tooget-hello-virtual-array-image"></a>imagem de matriz virtual tooget Olá

1. Inicie sessão em Olá [portal do Azure](https://portal.azure.com/). 
2. No portal do Azure Olá, clique em **Procurar > gestores de dispositivos do StorSimple**.
3. Selecione um serviço StorSimple Manager de dispositivo existente. No Olá **Gestor de dispositivos do StorSimple** painel, clique em **início rápido**. 
4. Clique em Olá ligação correspondente toohello imagem que pretende que o toodownload de Olá Microsoft Download Center. ficheiros de imagem de Olá são aproximadamente 4.8 GB.
   
   * VHDX para Hyper-V no Windows Server 2012 e versões posteriores
   * VHD para o Hyper-V no Windows Server 2008 R2 e versões posteriores
   * VMDK para o VMWare ESXi 5.5 e posterior
5. Transfira e deszipe Olá ficheiro tooa unidade local, fazer uma nota de onde está localizado o ficheiro deszipada Olá.

## <a name="optional-step-configure-a-new-storage-account-for-hello-service"></a>Passo opcional: configurar uma nova conta de armazenamento para o serviço de Olá

Este passo é opcional e deve ser efetuado apenas se não tiver ativado a criação automática de Olá de uma conta de armazenamento com o serviço.

Se precisar de toocreate uma conta de armazenamento do Azure numa região diferente, consulte [como toocreate uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) para obter instruções passo a passo.

Efetuar Olá os seguintes passos no Olá [portal do Azure](https://ms.portal.azure.com/) no Olá Gestor de dispositivos do StorSimple serviço página tooadd uma conta de armazenamento existente do Microsoft Azure.

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

## <a name="next-step"></a>Passo seguinte

Olá passo seguinte consiste em tooprovision uma máquina virtual para a matriz de Virtual StorSimple. Consoante o sistema operativo anfitrião, consulte Olá obter instruções detalhadas:

* [Aprovisionar uma matriz de Virtual StorSimple no Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md)
* [Aprovisionar uma matriz de Virtual StorSimple no VMware](storsimple-virtual-array-deploy2-provision-vmware.md)

