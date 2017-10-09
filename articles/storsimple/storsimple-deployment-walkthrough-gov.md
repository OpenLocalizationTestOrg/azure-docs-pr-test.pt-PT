---
title: "o dispositivo StorSimple aaaDeploy no Portal de administração pública | Microsoft Docs"
description: "Descreve os passos de Olá e melhores práticas para a implementação de Olá StorSimple Update 1 de dispositivo e o serviço no portal do Azure Government de Olá."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 3fe3648d-e0b6-4928-a2cb-8d3ccc50d62a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/17/2016
ms.author: v-sharos
ms.openlocfilehash: 045c838a28efc92d0f67ae3bab2a7393d1badc12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-in-hello-government-portal"></a>Implementar o dispositivo StorSimple no local Olá Government Portal
[!INCLUDE [storsimple-version-selector-deploy-gov](../../includes/storsimple-version-selector-deploy-gov.md)]

## <a name="overview"></a>Descrição geral
Bem-vindo tooMicrosoft Azure StorSimple a implementação do dispositivo. Estes tutoriais de implementação aplicam-se toohello série de 8000 do StorSimple execução 1 de atualização de software no Olá Portal do Azure Government. Esta série de tutoriais descreve como tooconfigure o dispositivo StorSimple e inclui uma lista de verificação de configuração, a pré-requisitos de configuração e a configuração detalhada passos.

informações de Olá nestes tutoriais pressupõem que ter revisto as precauções de segurança Olá e descompactado, montou em bastidor e instalou os cabos do dispositivo StorSimple. Se ainda precisar de tooperform das tarefas, comece por ler Olá [precauções de segurança](storsimple-safety.md). Dependendo do modelo do dispositivo, pode descompactar, montar em bastidor e instalar os cabos seguindo as instruções de Olá em:

* [Descompactar, montar em bastidor e instalar os cabos do 8100](storsimple-8100-hardware-installation.md)
* [Descompactar, montar em bastidor e instalar os cabos do 8600](storsimple-8600-hardware-installation.md)

Terá de administrador privilégios toocomplete Olá instalação e configuração processo. Recomendamos que reveja a lista de verificação de configuração de Olá antes de começar. processo de implementação e configuração de Olá pode demorar algum tempo toocomplete.

> [!NOTE]
> as informações de implementação do Olá StorSimple publicadas no Web site do Microsoft Azure de Olá aplica-se tooStorSimple 8000 série apenas dispositivos. Para obter informações completas sobre dispositivos das séries Olá 7000, aceda a: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). Para informações sobre a implementação de 7000 séries, consulte Olá [StorSimple sistema Guia Rápido](http://onlinehelp.storsimple.com/111_Appliance/).
> 
> 

## <a name="deployment-steps"></a>Passos da implementação
Efetue estes passos necessários tooconfigure o dispositivo StorSimple e ligá-lo tooyour do serviço StorSimple Manager. Além disso toohello necessários passos, existem passos e procedimentos que poderá ser necessário durante a implementação de Olá opcionais. instruções de implementação passo a passo Olá indicam quando deve efetuar cada um dos seguintes passos opcionais.

| Passo | Descrição |
| --- | --- |
| **PRÉ-REQUISITOS** |Estes têm toobe foi concluída em preparação para implementação futura Olá. |
| Lista de verificação das configurações de implementação. |Utilize esta lista de verificação toogather e registo informações anterior tooand durante a implementação de Olá. |
| Pré-requisitos da implementação. |Estes validam Olá ambiente está preparado para implementação. |
|  | |
| **IMPLEMENTAÇÃO PASSO-A-PASSO** |Estes passos é necessário toodeploy o dispositivo StorSimple em produção. |
| Passo 1: Criar um novo serviço. |Configure a gestão e o armazenamento na nuvem do dispositivo StorSimple. Se já existir um serviço para outros dispositivos StorSimple, ignore este passo. |
| Passo 2: Obter a chave de registo do serviço de Olá. |Utilize esta chave tooregister & ligar o dispositivo StorSimple com o serviço de gestão de Olá. |
| Passo 3: Configurar e registar o dispositivo de Olá através do Windows PowerShell para StorSimple. |Ligar Olá dispositivo tooyour rede e registá-lo com a configuração de Olá toocomplete do Azure utilizando o serviço de gestão de Olá. |
| Passo 4: Concluir a configuração mínima do dispositivo</br>Opcional: Atualizar o dispositivo StorSimple. |Utilize a configuração de dispositivo do Olá gestão serviço toocomplete Olá e ativá-la tooprovide armazenamento. |
| Passo 5: Criar um contentor de volume. |Crie um contentor tooprovision volumes. Um contentor de volume possui uma conta de armazenamento, largura de banda e definições de encriptação em todos os volumes de Olá nele contidos. |
| Passo 6: Criar um volume. |Aprovisionar volumes de armazenamento no dispositivo do StorSimple Olá para os servidores. |
| Passo 7: Montar, inicializar e formatar um volume.</br>Opcional: Configurar o MPIO. |Ligar o servidores toohello o armazenamento iSCSI fornecido pelo dispositivo Olá. Opcionalmente, configure tooensure MPIO que os servidores podem tolerar a ligação, rede e falha da interface. |
| Passo 8: Efetuar uma cópia de segurança. |Configurar a política de cópia de segurança tooprotect os dados |
|  | |
| **OUTROS PROCEDIMENTOS** |Poderá ser necessário procedimentos de toothese toorefer como implementar a sua solução. |
| Configure uma nova conta de armazenamento para o serviço de Olá. | |
| Utilize a consola de série do dispositivo PuTTY tooconnect toohello. | |
| Procurar e aplicar atualizações. | |
| Obter Olá IQN de um anfitrião Windows Server. | |
| Criar uma cópia de segurança manual. | |
| Configure o MPIO. | |

## <a name="deployment-configuration-checklist"></a>Lista de verificação das configurações de implementação
Olá seguinte lista de verificação de configuração de implementação descreve as informações de Olá que terá de toocollect antes e quando configurar o software de Olá no dispositivo StorSimple. A preparar algumas destas informações antecedência ajudará a simplificar o processo de Olá de implementação de dispositivo do StorSimple Olá no seu ambiente. Utilize este nota de tooalso de lista de verificação pendente detalhes de configuração de Olá à medida que implementa o seu dispositivo.

| Fase | Parâmetro | Detalhes | Valores |
| --- | --- | --- | --- |
| **Instalação dos cabos do dispositivo** |Acesso de série |Configuração inicial do dispositivo |Sim/Não |
|  | | | |
| **Configurar e registar o dispositivo** |Definições da rede de dados 0 |Endereço IP de Dados 0:</br>Máscara de subrede:</br>Gateway:</br>Servidor DNS primário:</br>Servidor NTP primário:</br>IP/FQDN do servidor proxy Web (opcional):</br>Porta de proxy Web: | |
| &nbsp; |Palavra-passe do administrador do dispositivo |A palavra-passe tem de ter entre 8 e 15 carateres e deve incluir minúsculas, maiúsculas, números e carateres especiais. | |
| &nbsp; |Palavra-passe do Snapshot Manager StorSimple |A palavra-passe tem de ter entre 14 e 15 carateres e deve incluir minúsculas, maiúsculas, números e carateres especiais. | |
| &nbsp; |Chave de Registo do Serviço |Esta chave é gerada a partir de Olá portal do Azure. | |
| &nbsp; |Chave de Encriptação dos Dados do Serviço |Esta chave é criada quando o dispositivo de Olá está registado no serviço de gestão de Olá através de Olá do Windows PowerShell para StorSimple. Copie esta chave e guarde-a numa localização segura. | |
|  | | | |
| **Concluir a configuração mínima do dispositivo** |Nome amigável do dispositivo |Este é um nome descritivo para o dispositivo de Olá. | |
| &nbsp; |Fuso horário |O dispositivo utiliza este fuso horário para todas as operações agendadas. | |
| &nbsp; |Servidor DNS secundário |Esta é uma configuração obrigatória. | |
| &nbsp; |Interface de rede: IPs fixos do controlador de dados 0 |Estes IPs devem ser encaminhável toohello Internet.</br>Endereço IP fixo do controlador 0:</br>Endereço IP fixo do controlador 1: | |
|  | | | |
| **Definições adicionais da interface de rede** |Interface de rede: dados 1</br>Se estiver ativada a iSCSI, não configure Olá Gateway. |Objetivo: nuvem/iSCSI/Não utilizado</br>Endereço IP:</br>Máscara de subrede:</br>Gateway: | |
| &nbsp; |Interface de rede: dados 2</br>Se estiver ativada a iSCSI, não configure Olá Gateway. |Objetivo: nuvem/iSCSI/Não utilizado</br>Endereço IP:</br>Máscara de subrede:</br>Gateway: | |
| &nbsp; |Interface de rede: dados 3</br>Se estiver ativada a iSCSI, não configure Olá Gateway. |Objetivo: nuvem/iSCSI/Não utilizado</br>Endereço IP:</br>Máscara de subrede:</br>Gateway: | |
| &nbsp; |Interface de rede: dados 4</br>Se estiver ativada a iSCSI, não configure Olá Gateway. |Objetivo: nuvem/iSCSI/Não utilizado</br>Endereço IP:</br>Máscara de subrede:</br>Gateway: | |
| &nbsp; |Interface de rede: dados 5</br>Se estiver ativada a iSCSI, não configure Olá Gateway. |Objetivo: nuvem/iSCSI/Não utilizado</br>Endereço IP:</br>Máscara de subrede:</br>Gateway: | |
|  | | | |
| **Criar um contentor de volumes** |Nome do contentor de volume: |Nome do contentor de Olá | |
| &nbsp; |Conta do Storage do Azure: |Armazenamento conta acesso & nome da chave tooassociate com este contentor de volume | |
| &nbsp; |Chave de encriptação do armazenamento na nuvem: |Chave de encriptação do armazenamento em cada contentor | |
|  | | | |
| **Criar um volume** |Detalhes de cada volume |Nome do volume: | |
| &nbsp; |&nbsp; |Tamanho: | |
| &nbsp; |&nbsp; |Tipo de utilização: | |
| &nbsp; |&nbsp; |Nome ACR: | |
| &nbsp; |&nbsp; |Política de cópia de segurança predefinida: | |
|  | | | |
| **Montar, inicializar e formatar um volume** |Detalhes para cada servidor de anfitrião ligar toohello armazenamento |Nome do Windows Server: | |
| &nbsp; |&nbsp; |IQN do Windows Server: | |
| &nbsp; |&nbsp; |Nome do volume do Windows Server: | |
| &nbsp; |&nbsp; |Letra da unidade/ponto de montagem NTFS: | |

## <a name="deployment-prerequisites"></a>Pré-requisitos da implementação
Olá secções a seguir explica Olá pré-requisitos de configuração do serviço StorSimple Manager e o dispositivo StorSimple.

### <a name="for-hello-storsimple-manager-service"></a>Para Olá serviço StorSimple Manager
Antes de começar, certifique-se de que:

* Tem a conta Microsoft com credenciais de acesso.
* Tem a conta do Storage do Microsoft Azure com credenciais de acesso.
* A subscrição do Microsoft Azure está ativada para Olá serviço StorSimple Manager. A subscrição deve ser comprada através de Olá [Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).
* Tem o software de emulação do acesso tooterminal como o PuTTY.

### <a name="for-hello-device-in-hello-datacenter"></a>Para o dispositivo de Olá Olá Centro de dados
Antes de configurar o dispositivo de Olá, certifique-se de que:

* O dispositivo é completamente descompactado, montado em bastidor e é feita a instalação dos cabos de alimentação, rede e acesso de série, conforme descrito em:
  
  * [Descompactar, montar em bastidor e instalar os cabos do dispositivo 8100](storsimple-8100-hardware-installation.md)
  * [Descompactar, montar em bastidor e instalar os cabos do dispositivo 8600](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a>Para a rede de Olá Olá Centro de dados
Antes de começar, certifique-se de que:

* Olá portas na firewall do datacenter são tooallow aberta para o tráfego iSCSI e na nuvem, tal como descrito no [requisitos de rede para o dispositivo StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).

## <a name="step-by-step-deployment"></a>Implementação passo-a-passo
Utilize Olá seguir instruções passo a passo toodeploy o dispositivo StorSimple no datacenter de Olá.

## <a name="step-1-create-a-new-service"></a>Passo 1: Criar um novo serviço
Um serviço StorSimple Manager pode gerir diversos dispositivos StorSimple. Efetue Olá os seguintes passos toocreate uma nova instância do serviço do StorSimple Manager Olá.

[!INCLUDE [storsimple-create-new-service-gov](../../includes/storsimple-create-new-service-gov.md)]

> [!IMPORTANT]
> Se não tiver ativado a criação automática de Olá de uma conta de armazenamento com o serviço, terá de toocreate pelo menos uma conta de armazenamento depois de ter criado com êxito um serviço. Esta conta do Storage será utilizada quando criar um contentor de volume.
> 
> * Se não tiver criado uma conta do storage automaticamente, aceda demasiado[configurar uma nova conta de armazenamento para o serviço de Olá](#configure-a-new-storage-account-for-the-service) para obter instruções detalhadas.
> * Se tiver ativado a criação de uma conta de armazenamento automática Olá, vá demasiado[passo 2: chave de registo do serviço de Olá Get](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Passo 2: Obter a chave de registo do serviço de Olá
Depois de Olá serviço StorSimple Manager se encontra em execução, terá de chave de registo do serviço de Olá tooget. Esta chave é utilizada tooregister e ligar o seu serviço de toohello do dispositivo StorSimple.

Efetue Olá os seguintes passos no Olá Government Portal.

[!INCLUDE [storsimple-get-service-registration-key-gov](../../includes/storsimple-get-service-registration-key-gov.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>Passo 3: Configurar e registar o dispositivo de Olá através do Windows PowerShell para StorSimple
Utilize o Windows PowerShell para StorSimple toocomplete Olá a configuração inicial do dispositivo StorSimple conforme explicado no Olá procedimento a seguir. Terá de toocomplete de software de emulação do terminal toouse este passo. Para obter mais informações, consulte [utilizar o PuTTY tooconnect toohello consola de série dispositivo](#use-putty-to-connect-to-the-device-serial-console).

[!INCLUDE [storsimple-configure-and-register-device-gov](../../includes/storsimple-configure-and-register-device-gov.md)]

## <a name="step-4-complete-minimum-device-setup"></a>Passo 4: Concluir a configuração mínima do dispositivo
Para Olá configuração mínima do dispositivo StorSimple, é necessário:

* Configure o servidor DNS secundário de Olá.
* Ativar o iSCSI em, pelo menos, uma interface de rede.
* Atribua endereços IP fixos controladores de Olá tooboth.

Efetue Olá seguindo os passos do programa de configuração do Olá Government Portal toocomplete Olá mínima do dispositivo.

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a>Passo 5: Criar um contentor de volume
Um contentor de volume possui uma conta de armazenamento, largura de banda e definições de encriptação em todos os volumes de Olá nele contidos. Precisa de toocreate um contentor de volume antes de poder começar a aprovisionar volumes no dispositivo StorSimple.

Efetue Olá os seguintes passos no Portal de administração pública de Olá toocreate um contentor de volume.

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>Passo 6: Criar um volume
Depois de criar um contentor de volume, pode aprovisionar um volume de armazenamento no dispositivo do StorSimple Olá para os servidores. Execute os seguintes passos no Olá Government Portal toocreate um volume de Olá.

> [!IMPORTANT]
> Azure StorSimple pode criar apenas volumes com aprovisionamento dinâmico.  Não é possível criar totalmente aprovisionamento totais ou parciais volumes num sistema Azure StorSimple.
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>Passo 7: Montar, inicializar e formatar um volume
Execute estes passos no anfitrião do Windows Server.

> [!IMPORTANT]
> * Para Olá elevada disponibilidade da solução StorSimple, recomendamos que configure o MPIO no seu iSCSI de tooconfiguring anterior de servidores (opcional) de anfitrião. Configuração do MPIO nos servidores de anfitrião irá garantir que os servidores de Olá podem tolerar uma ligação, a rede ou a falha de interface.
> * Para MPIO e do iSCSI instalação e configuração instruções num anfitrião Windows Server, aceda demasiado[configurar o MPIO para o dispositivo StorSimple](storsimple-configure-mpio-windows-server.md). Também estes irão incluir Olá passos toomount, inicializar e formatar volumes do StorSimple.
> * Para MPIO e do iSCSI instalação e configuração instruções num anfitrião Linux, visite demasiado[configurar o MPIO para o anfitrião Linux do StorSimple](storsimple-configure-mpio-on-linux.md)
> 
> 

Se decidir não tooconfigure MPIO, execute Olá toomount passos a seguir, inicializar e formatar os volumes do StorSimple num anfitrião Windows Server.

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>Passo 8: Efetuar uma cópia de segurança
As cópias de segurança fornecem proteção para um ponto anterior no tempo dos volumes e melhoram a capacidade de recuperação enquanto minimizam os tempos de restauro. Pode efetuar dois tipos de cópia de segurança no dispositivo StorSimple: instantâneos locais e instantâneos de nuvem. Cada um destes tipos de cópia de segurança pode ser **Agendado** ou **Manual**.

Efetue Olá os seguintes passos no Olá Government Portal toocreate uma cópia de segurança agendada.

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

Pode efetuar uma cópia de segurança manual em qualquer altura. Para obter os procedimentos, vá demasiado[criar uma cópia de segurança manual](#create-a-manual-backup).

## <a name="configure-a-new-storage-account-for-hello-service"></a>Configurar uma nova conta de armazenamento para o serviço de Olá
Este passo é opcional que terá de tooperform apenas se não tiver ativado a criação automática de Olá de uma conta de armazenamento com o serviço. Uma conta de armazenamento do Microsoft Azure é necessário toocreate um contentor de volume do StorSimple.

Se precisar de toocreate uma conta de armazenamento do Azure numa região diferente, consulte [sobre contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md) para obter instruções passo a passo.

Efetuar Olá os seguintes passos no Olá Government Portal, no Olá **serviço StorSimple Manager** página.

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>Utilize a consola de série do dispositivo PuTTY tooconnect toohello
tooconnect tooWindows do PowerShell para StorSimple, terá de toouse software de emulação do terminal como o PuTTY. Pode utilizar o PuTTY quando aceder ao dispositivo de Olá diretamente através da consola de série de Olá ou ao abrir uma sessão telnet a partir de um computador remoto.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Procurar e aplicar atualizações
A atualização do dispositivo pode demorar várias horas. Efetuar Olá tooscan passos para os seguintes e aplicar atualizações no seu dispositivo.

<!--If you have a gateway configured on a network interface other than Data 0, you will need toodisable Data 2 and Data 3 network interfaces before installing hello update. Go too**Devices > Configure** and disable Data 2 and Data 3 interfaces. You should re-enable these interfaces after hello device is updated.-->

#### <a name="tooupdate-your-device"></a>tooupdate o dispositivo
1. No dispositivo Olá **início rápido** página, clique em **dispositivos**. Selecione o dispositivo físico Olá, clique em **manutenção** e, em seguida, clique em **procurar atualizações**.  
2. É criada uma tarefa tooscan para as atualizações disponíveis. Se as atualizações estiverem disponíveis, Olá **procurar atualizações** alterações demasiado**instalar atualizações**. Clique em **Instalar Atualizações**.
3. Será criada uma tarefa de atualização. Monitorizar o estado de Olá da atualização, navegando demasiado**tarefas**.
   
   > [!NOTE]
   > Quando inicia a tarefa de atualização de Olá, é imediatamente apresentado Estado Olá como 50 por cento. Olá estado é alterado too100 percentagem apenas depois de tarefa de atualização de Olá está concluída. Não há nenhum Estado em tempo real para o processo de atualização de Olá.
   > 
   > 
4. Depois do dispositivo de Olá foi atualizado com êxito, ative as interfaces de rede de dados 2 e dados 3 se estas tiverem sido desativadas.

## <a name="get-hello-iqn-of-a-windows-server-host"></a>Obter Olá IQN de um anfitrião Windows Server
Efetuar os seguintes passos tooget Olá iSCSI de Olá nome qualificado (IQN) de um anfitrião do Windows que está a executar o Windows Server® 2012.

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>Criar uma cópia de segurança manual
Efetue Olá os seguintes passos no Olá Government Portal toocreate uma pedido cópia de segurança manual de um único volume no dispositivo StorSimple.

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup-gov.md)]

## <a name="configure-mpio"></a>Configurar o MPIO
Multipath I/O (MPIO) é uma funcionalidade opcional e, por predefinição, não está instalada no Windows Server. Deve ser instalada como uma funcionalidade através do Server Manager. Para obter instruções de instalação do MPIO, vá demasiado[configurar o MPIO para o dispositivo StorSimple](storsimple-configure-mpio-windows-server.md).

Para obter instruções de instalação do MPIO para um dispositivo StorSimple ligado tooa anfitrião Linux, vá demasiado[configurar o MPIO para o anfitrião Linux](storsimple-configure-mpio-on-linux.md).

> [!NOTE]
> O MPIO não é suportado num dispositivo virtual StorSimple.
> 
> 

## <a name="next-steps"></a>Passos seguintes
* Configurar um [dispositivo virtual](storsimple-virtual-device-u2.md).
* Olá utilize [serviço StorSimple Manager](https://msdn.microsoft.com/library/azure/dn772396.aspx) toomanage o dispositivo StorSimple.

