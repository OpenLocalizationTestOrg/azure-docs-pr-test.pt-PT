---
title: "aaaHow tooinstall um servidor de destino principal do Linux para ativação pós-falha do local tooon do Azure | Microsoft Docs"
description: "Antes de trocar uma máquina virtual Linux, precisa de um servidor de destino principal do Linux. Saiba como tooinstall um."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a>Instalar um servidor de destino principal do Linux
Após a ativação pós-falha de máquinas virtuais, pode efetuar a site no local do back-Olá máquinas virtuais toohello. toofail novamente, terá de tooreprotect Olá excluir máquina virtual de site do Azure toohello no local. Para que este processo, tem um tráfego de Olá tooreceive de servidor de destino principal de no local. 

Se a máquina virtual protegida é uma máquina virtual do Windows, em seguida, é necessário um destino principal do Windows. Para uma máquina virtual do Linux, tem um destino principal do Linux. Seguinte de Olá leitura passos toolearn como toocreate e instale um Linux destino mestre.

> [!IMPORTANT]
> A partir da versão do servidor de destino mestre Olá 9.10.0, servidor de destino mestre Olá mais recente pode ser apenas instalado num servidor Ubuntu 16.04. Novas instalações não são permitidas em CentOS6.6 servidores. No entanto, pode continuar tooupgrade os servidores de destino mestre antigo utilizando Olá 9.10.0 versão.

## <a name="overview"></a>Descrição geral
Este artigo fornece instruções sobre como tooinstall um Linux mestre de destino.

Publique comentários ou perguntas na end Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Pré-requisitos

* anfitrião de Olá toochoose que toodeploy Olá destino principal, determinar se a reativação pós-falha da Olá é vai toobe tooan existente no local da máquina virtual ou máquina virtual nova do tooa. 
    * Para uma máquina virtual existente, o anfitrião Olá de destino mestre Olá deve ter acesso toohello arquivos de dados da máquina virtual de Olá.
    * Se a máquina de virtual Olá no local não existe, Olá máquinas de reativação pós-falha é criada no Olá mesmo anfitrião como destino mestre Olá. Pode escolher qualquer anfitrião ESXi destino principal do tooinstall Olá.
* o destino principal Olá deve estar numa rede que possa comunicar com o servidor de processos de Olá e o servidor de configuração de Olá.
* Olá versão de destino mestre Olá tem de ser igual tooor anteriores ao hello as versões do servidor de processos de Olá e servidor de configuração de Olá. Por exemplo, se versão hello do servidor de configuração de Olá 9.4, versão de Olá do destino principal Olá possa ser 9.4 ou 9.3 mas não 9.5.
* só pode ser o destino principal Olá uma máquina virtual VMware e não um servidor físico.

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a>Criar o destino principal Olá de acordo com toohello diretrizes de dimensionamento

Crie o destino principal do Olá em conformidade com as seguintes diretrizes de dimensionamento de Olá:
- **RAM**: 6 GB ou mais
- **Tamanho do disco de SO**: 100 GB ou mais (tooinstall CentOS6.6)
- **Tamanho de disco adicional para a unidade de retenção**: 1 TB
- **Núcleos de CPU**: 4 núcleos ou mais

seguinte Olá suportado Ubuntu kernels são suportados.


|Série de kernel  |Suporta segurança demasiado |
|---------|---------|
|4.4      |4.4.0-81-Generic         |
|4.8      |4.8.0-56-Generic         |
|4.10     |4.10.0-24-Generic        |


## <a name="deploy-hello-master-target-server"></a>Implementar o servidor de destino mestre Olá

### <a name="install-ubuntu-16042-minimal"></a>Instalar Ubuntu 16.04.2 mínima

Demorar Olá os seguintes passos Olá tooinstall Olá Ubuntu 16.04.2 64 bits da sistema operativo.

**Passo 1:** aceda toohello [transferir ligação](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) e escolha espelho mais próximo Olá dos quais transferir um ficheiro Ubuntu 16.04.2 mínimo 64-bit ISO.

Manter um ficheiro Ubuntu 16.04.2 mínimo 64-bit ISO na unidade de DVD de Olá e iniciar Olá sistema.

**Passo 2:** selecione **inglês** como linguagem preferencial e, em seguida, selecione **Enter**.

![Selecione uma Linguagem](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

**Passo 3:** selecione **instalar Ubuntu Server**e, em seguida, selecione **Enter**.

![Selecione instalar Ubuntu Server](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

**Passo 4:** selecione **inglês** como linguagem preferencial e, em seguida, selecione **Enter**.

![Selecione inglês como o idioma preferencial](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

**Passo 5:** Olá, selecione a opção adequada de Olá **fuso horário** lista de opções e, em seguida, selecione **Enter**.

![Selecione o fuso horário corretos Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

**Passo 6:** selecione **não** (hello a opção predefinida) e, em seguida, selecione **Enter**.


![Configurar o teclado Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

**Passo 7:** selecione **inglês (EUA)** como Olá país de origem para o teclado Olá e, em seguida, selecione **Enter**.

![Selecione E.U.A. como país Olá de origem](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

**Passo 8:** selecione **inglês (EUA)** como o esquema do teclado Olá e, em seguida, selecione **Enter**.

![Selecione inglês como o esquema do teclado Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

**Passo 9:** introduza Olá nome de anfitrião para o servidor no Olá **Hostname** caixa e, em seguida, selecione **continuar**.

![Introduza o nome de anfitrião Olá para o servidor](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

**Passo 10:** toocreate uma conta de utilizador, introduza o nome de utilizador Olá e, em seguida, selecione **continuar**.

![Criar uma conta de utilizador](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

**Passo 11:** introduza a palavra-passe de Olá Olá nova conta de utilizador e, em seguida, selecione **continuar**.

![Introduza a palavra-passe de Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

**Passo 12:** confirme Olá palavra-passe do utilizador novo Olá e, em seguida, selecione **continuar**.

![Confirme as palavras-passe de Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

**Passo 13:** selecione **não** (hello a opção predefinida) e, em seguida, selecione **Enter**.

![Configurar utilizadores e palavras-passe](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

**Passo 14:** se Olá fuso horário que é apresentado está correto, selecione **Sim** (hello a opção predefinida) e, em seguida, selecione **Enter**.

tooreconfigure seu fuso horário, selecione **não**.

![Configure o relógio Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

**Passo 15:** na Olá opções de método de criação de partições, selecione **orientado - a utilizar o disco completo**e, em seguida, selecione **Enter**.

![Selecione a opção de método de criação de partições de Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

**Passo 16:** Olá, selecione um disco apropriado de Olá **selecionar disco toopartition** opções e, em seguida, selecione **Enter**.


![Selecione o disco de Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

**Passo 17:** selecione **Sim** toowrite Olá toodisk de alterações e, em seguida, selecione **Enter**.

![Escrever Olá alterações toodisk](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

**Passo 18:** selecione a opção predefinida de Olá, selecione **continuar**e, em seguida, selecione **Enter**.

![Selecione a opção predefinida de Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

**Passo 19:** selecionar Olá a opção adequada para a gestão de atualizações no seu sistema e, em seguida, selecione **Enter**.

![Selecione a forma como toomanage atualiza](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> Porque o servidor de destino principal do Azure Site Recovery Olá requer uma versão muito específica do Olá Ubuntu, terá de tooensure que kernel Olá atualizações estão desativadas para a máquina virtual de Olá. Se estes estiverem ativadas, as atualizações regulares causam toomalfunction de servidor de destino mestre Olá. Certifique-se de que seleciona Olá **sem as atualizações automáticas** opção.


**Passo 20:** Selecionar opções predefinidas. Se quiser openSSH para estabelecer a ligação SSH, selecione Olá **OpenSSH servidor** opção e, em seguida, selecione **continuar**.

![Selecione o software](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

**Passo 21:** selecione **Sim**e, em seguida, selecione **Enter**.

![Carregador de arranque do instalação Olá GRUB](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

**Passo 22:** selecione Olá dispositivos adequada para a instalação do carregador de arranque de Olá (preferencialmente, **/dev/sda**) e, em seguida, selecione **Enter**.

![Selecione um dispositivo para a instalação do carregador de arranque](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

**Passo 23:** selecione **continuar**e, em seguida, selecione **Enter** instalação de Olá toofinish.

![Concluir a instalação de Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

Após concluir a instalação de Olá, inicie sessão toohello VM com as credenciais de utilizador novo Olá. (Consulte demasiado**passo 10** para obter mais informações.)

Siga os passos de Olá que estão descritos na seguinte captura de ecrã tooset Olá raiz de Olá palavra-passe do utilizador. Em seguida, inicie sessão como utilizador raiz.

![Palavra-passe de utilizador de raiz de Olá conjunto](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a>Preparar a máquina de Olá para configuração como um servidor de destino mestre
Em seguida, prepare máquina Olá para configuração como um servidor de destino principal.

tooget Olá ID para cada disco de rígido SCSI numa máquina virtual Linux, ativar Olá **disco. EnableUUID = TRUE** parâmetro.

tooenable deste parâmetro, Olá execute os seguintes passos:

1. Encerre a máquina virtual.

2. Faça duplo clique entrada Olá para a máquina virtual de Olá no painel esquerdo Olá e, em seguida, selecione **editar definições de**.

3. Selecione Olá **opções** separador.

4. No painel esquerdo Olá, selecione **avançadas** > **geral**e, em seguida, selecione Olá **parâmetros de configuração** botão na parte inferior direita Olá ecrã Olá.

    ![Separador Opções](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    Olá **parâmetros de configuração** opção não está disponível quando Olá máquina está em execução. toomake este separador Active Directory, encerrar a máquina virtual de Olá.

5. Ver se uma linha com **disco. EnableUUID** já existe.

    - Se o valor de Olá existe e está definido demasiado**falso**, altere o valor de Olá demasiado**verdadeiro**. (os valores de Olá não são maiúsculas e minúsculas.)

    - Se o valor de Olá existe e está definido demasiado**verdadeiro**, selecione **Cancelar**.

    - Se o valor de Olá não existe, selecione **linha adicionar**.

    - Na coluna de nome de Olá, adicionar **disco. EnableUUID**e, em seguida, defina o valor de Olá demasiado**verdadeiro**.

    ![A verificar se o disco. EnableUUID já existe](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a>Desativar as atualizações de kernel

Servidor de destino principal do Azure Site Recovery requer uma versão muito específica do Olá Ubuntu, certifique-se de que as atualizações de kernel Olá estão desativadas para a máquina virtual de Olá.

Se as atualizações de kernel estiverem ativadas, as atualizações regulares causam toomalfunction de servidor de destino mestre Olá.

#### <a name="download-and-install-additional-packages"></a>Transferir e instalar pacotes adicionais

> [!NOTE]
> Certifique-se de que tem toodownload de conectividade da Internet e instalar pacotes adicionais. Se não tiver conectividade à Internet, terá de toomanually localizar estes pacotes RPM e instalá-los.

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a>Obter o instalador Olá para configuração

Se o destino principal tiver conectividade à Internet, pode utilizar Olá instalador de Olá toodownload de passos a seguir. Caso contrário, pode copiar o hello installer do servidor de processos de Olá e, em seguida, instalá-lo.

#### <a name="download-hello-master-target-installation-packages"></a>Transferir pacotes de instalação de destino mestre Olá

[Transferir o bits de instalação de destino mestre Olá mais recentes Linux](https://aka.ms/latestlinuxmobsvc).

toodownload-lo utilizando o Linux, tipo:

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

Certifique-se de que transfira e deszipe o instalador Olá no seu diretório raiz. Se deszipe demasiado**usr/Local**, instalação Olá falhará.


#### <a name="access-hello-installer-from-hello-process-server"></a>Instalador de Olá de acesso do servidor de processos de Olá

1. No servidor de processos de Olá, aceda demasiado**C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.

2. Copie o ficheiro de instalador necessária de hello do servidor de processos de Olá e guarde-o como **latestlinuxmobsvc.tar.gz** no seu diretório raiz.


### <a name="apply-custom-configuration-changes"></a>Aplicar alterações de configuração personalizada

alterações de configuração personalizada tooapply, utilize Olá os seguintes passos:


1. Execute Olá binário de Olá toountar de comando a seguir.
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Captura de ecrã do Olá comando toorun](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. Execute Olá permissão toogive de comando a seguir.
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. Execute Olá seguinte script do comando toorun Olá.
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> Execute o script de Olá apenas uma vez no servidor de Olá. Encerre o servidor de Olá. Em seguida, reinicie o servidor de Olá depois de adicionar um disco, conforme descrito na secção seguinte Olá.

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a>Adicionar uma máquina de virtual de destino principal do retenção disco toohello Linux

Utilize os seguintes passos toocreate um disco de retenção de Olá:

1. Anexe uma novo disco de 1 TB toohello destino mestre máquina virtual com Linux e, em seguida, iniciar a máquina de Olá.

2. Olá utilize **multipath -odas** toolearn Olá multipath ID de disco de retenção de Olá de comandos.

    ```
    multipath -ll
    ```
    ![ID de multipath Olá do disco de retenção de Olá](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. Formatar o disco de Olá e, em seguida, crie um sistema de ficheiros na unidade Olá de novo.

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![A criação de um sistema de ficheiros numa unidade de Olá](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. Depois de criar o sistema de ficheiros de Olá, Monte o disco de retenção de Olá.
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Disco de retenção de Olá de montagem](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. Criar Olá **fstab** unidade de retenção de Olá do entrada toomount sempre que o sistema de Olá é iniciado.
    ```
    vi /etc/fstab
    ```
    Selecione **inserir** toobegin editar Olá ficheiro. Criar uma nova linha e, em seguida, inserir Olá seguinte texto. Edite Olá multipath um ID de disco com base no ID de multipath Olá realçado do comando anterior Olá.

     **/Dev/mapeador/ <Retention disks multipath id> /mnt/retenção ext4 RW novos 0 0**

    Selecione **Esc**e, em seguida, escreva **: wq** (escrever e sair) janela do editor tooclose Olá.

### <a name="install-hello-master-target"></a>Instalar o destino principal Olá

> [!IMPORTANT]
> versão de Hello do servidor de destino mestre Olá tem de ser igual tooor anteriores ao hello as versões do servidor de processos de Olá e servidor de configuração de Olá. Se esta condição não for cumprida, reproteção for bem sucedida, mas a replicação falha.


> [!NOTE]
> Antes de instalar o servidor de destino mestre Olá, verifique que Olá **etc/anfitriões** ficheiro na máquina virtual de Olá contém entradas que mapeiam Olá local hostname toohello endereços IP estão associados a todos os adaptadores de rede.

1. Copie o frase de acesso de Olá de **C:\ProgramData\Microsoft do Azure Site Recovery\private\connection.passphrase** no servidor de configuração de Olá. Em seguida, guarde-o como **passphrase.txt** Olá mesmo diretório local executando Olá os seguintes comandos:

    ```
    echo <passphrase> >passphrase.txt
    ```
    Exemplo: 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. Tenha em atenção o endereço IP do servidor de configuração Olá. Terá no passo seguinte Olá.

3. Execute Olá seguir o servidor de destino principal do comando tooinstall Olá e registar o servidor de Olá com o servidor de configuração de Olá.

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    Exemplo: 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    Aguarde pela conclusão do script Olá. Se o destino principal Olá regista com êxito, o destino principal Olá está listado no Olá **infraestrutura de recuperação de Site** página do portal de Olá.


#### <a name="install-hello-master-target-by-using-interactive-installation"></a>Instalar o destino principal Olá utilizando a instalação interativa

1. Execute Olá destino principal do comando tooinstall Olá a seguir. Para a função de agente Olá, escolha **destino mestre**.

    ```
    ./install
    ```

2. Escolha a localização predefinida de Olá para instalação e, em seguida, selecione **Enter** toocontinue.

    ![Escolher uma localização predefinida para a instalação de destino mestre](./media/site-recovery-how-to-install-linux-master-target/image17.png)

Depois de concluir a instalação de Olá, registe o servidor de configuração de Olá utilizando a linha de comandos Olá.

1. Tenha em atenção o endereço IP de hello do servidor de configuração de Olá. Terá no passo seguinte Olá.

2. Execute Olá seguir o servidor de destino principal do comando tooinstall Olá e registar o servidor de Olá com o servidor de configuração de Olá.

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    Exemplo: 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   Aguarde pela conclusão do script Olá. Se o destino principal Olá foi registado com êxito, o destino principal Olá está listado no Olá **infraestrutura de recuperação de Site** página do portal de Olá.


### <a name="upgrade-hello-master-target"></a>Atualizar o destino principal Olá

Execute o instalador do Olá. Deteta automaticamente que o agente Olá está instalado no destino principal Olá. tooupgrade, selecione **Y**.  Configuração Olá tenha sido concluída, verifique a versão de Olá de destino mestre Olá instalado utilizando Olá os seguintes comandos.

    ```
    cat /usr/local/.vx_version
    ```

Pode ver essa Olá **versão** campo indica o número de versão de Olá de destino mestre Olá.

### <a name="install-vmware-tools-on-hello-master-target-server"></a>Instalar as ferramentas do VMware no servidor de destino mestre Olá

Terá das ferramentas do VMware tooinstall no destino principal Olá para que possa detetar Olá arquivos de dados. Se não estiverem instaladas ferramentas Olá, ecrã de reproteção Olá não está listado nos arquivos de dados de Olá. Após a instalação das ferramentas do VMware Olá, terá de toorestart.

## <a name="next-steps"></a>Passos seguintes
Após a instalação de Olá e o registo do destino principal Olá tem finsihed, pode ver o destino principal hello apareçam na Olá **destino mestre** secção **infraestrutura de recuperação de Site**, sob Olá Descrição geral do servidor de configuração.

Agora pode continuar com [só](site-recovery-how-to-reprotect.md), seguido de reativação pós-falha.

## <a name="common-issues"></a>Problemas comuns

* Certifique-se de que não ative vMotion de armazenamento de quaisquer componentes de gestão tais como um destino principal. Se o destino principal Olá move após uma reproteção com êxito, os discos da máquina virtual Olá (VMDKs) não podem ser desligados. Neste caso, a reativação pós-falha falha.

* destino mestre Olá não deve ter todos os instantâneos na máquina virtual de Olá. Se existirem instantâneos, irá falhar a reativação pós-falha.

* Atraso toosome NIC personalizado em alguns clientes, interface de rede Olá está desativada durante o arranque e, não é possível inicializar o agente de destino mestre Olá. Certifique-se de que Olá seguintes propriedades estão definidas corretamente. Verifique estas propriedades no Olá Ethernet /etc/sysconfig/network-scripts/ifcfg do ficheiro de cartão-eth *.
    * BOOTPROTO = dhcp
    * ONBOOT = yes
