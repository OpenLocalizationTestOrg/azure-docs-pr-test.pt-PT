---
title: aaaDeploy Snapshot Manager do StorSimple | Microsoft Docs
description: "Saiba como toodownload e instalar Olá Snapshot Manager do StorSimple, um snap-in MMC para gerir as funcionalidades de proteção e cópia de segurança de dados do StorSimple."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: f0128f57-519e-49ec-9187-23575809cdbe
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: dd90cca2bbb3410bb8cd459fb1a3ff3fb5f2997b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-snapshot-manager-mmc-snap-in"></a>Implementar Olá snap-in MMC de Snapshot Manager do StorSimple

## <a name="overview"></a>Descrição geral
Olá Snapshot Manager do StorSimple é um snap-in Consola de gestão da Microsoft (MMC) que simplifica a gestão de cópia de segurança num ambiente do Microsoft Azure StorSimple e proteção de dados. Com o Snapshot Manager do StorSimple, pode gerir o Microsoft Azure StorSimple no local e armazenamento na nuvem como se fosse um sistema de armazenamento totalmente integrada, criando assim simplificar processos de cópia de segurança e restauro e reduzindo os custos. 

Este tutorial descreve os requisitos de configuração, bem como dos procedimentos para instalar, remover e atualizar o Snapshot Manager do StorSimple.

> [!NOTE]
> * Não é possível utilizar o Snapshot Manager do StorSimple toomanage Microsoft Azure StorSimple Virtual matrizes (também conhecido como StorSimple no local dispositivos virtuais).
> * Se planear tooinstall atualização 2 do StorSimple no dispositivo StorSimple, se toodownload Olá versão mais recente do Snapshot Manager do StorSimple e instalá-lo **antes de instalar a atualização 2 do StorSimple**. versão mais recente do Olá do Snapshot Manager do StorSimple é retrocompatível e funciona com todas as versões de lançamento do Microsoft Azure StorSimple. Se estiver a utilizar versão anterior do Olá do Snapshot Manager do StorSimple, terá de tooupdate it (não precisa de versão anterior do toouninstall Olá antes de instalar a nova versão de Olá).


## <a name="storsimple-snapshot-manager-installation"></a>Instalação do Snapshot Manager do StorSimple
Snapshot Manager do StorSimple podem ser instalado em computadores que estejam a executar o sistema de operativo do Windows Server 2008 R2 SP1, Windows Server 2012 ou Windows Server 2012 R2 Olá. Em servidores com o Windows 2008 R2, também tem de instalar o Windows Server 2008 SP1 e o Windows Management Framework 3.0.

Antes de instalar ou atualizar Olá Snapshot Manager do StorSimple snap-in para Olá consola de gestão da Microsoft (MMC), certifique-se de que o dispositivo Microsoft Azure StorSimple Olá e servidor de anfitrião estão configuradas corretamente.

## <a name="configure-prerequisites"></a>Configurar os pré-requisitos
Olá passos seguintes fornecem uma descrição geral de alto nível das tarefas de configuração que tem de concluir antes de instalar Olá Snapshot Manager do StorSimple. Para a configuração completa do Microsoft Azure StorSimple e informações de configuração, incluindo os requisitos de sistema e instruções passo a passo, consulte [implementar o dispositivo StorSimple no local](storsimple-8000-deployment-walkthrough-u2.md).

> [!IMPORTANT]
> Antes de começar, reveja Olá [lista de verificação de configuração de implementação](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist) e e [os pré-requisitos de implementação](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites) no [implementar o dispositivo StorSimple no local](storsimple-8000-deployment-walkthrough-u2.md).
> <br>
> 
> 

### <a name="before-you-install-storsimple-snapshot-manager"></a>Antes de instalar o Snapshot Manager do StorSimple
1. Descompactar, montar e ligar o dispositivo de Microsoft Azure StorSimple Olá conforme descrito em [instalar o seu dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md) ou [instalar o seu dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md).
2. Certifique-se de que o computador anfitrião está a executar um dos seguintes sistemas operativos de Olá:
   
   * Windows Server 2008 R2 (em servidores com o Windows 2008 R2, deve instalar também o Windows Server 2008 SP1 e o Windows Management Framework 3.0)
   * Windows Server 2012
   * Windows Server 2012 R2
     
     Para um dispositivo virtual StorSimple, o anfitrião de Olá tem de ser uma máquina de Virtual do Microsoft Azure.
3. Certifique-se de que cumpre todos os requisitos de configuração do Microsoft Azure StorSimple Olá. Para obter mais informações, visite demasiado[os pré-requisitos de implementação](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites).
4. Ligar Olá dispositivo toohello anfitrião e execute a configuração inicial do Olá. Para obter mais informações, visite demasiado[passos de implementação](storsimple-8000-deployment-walkthrough-u2.md#deployment-steps).
5. Crie volumes no dispositivo Olá, atribuir-lhes toohello anfitriões e certifique-se de que alojam Olá pode montar e utilizá-los. Snapshot Manager do StorSimple suporta Olá tipos de volumes seguintes:
   
   * Volumes básicos
   * Volumes simples
   * Volumes dinâmicos
   * Volumes dinâmicos espelhados (RAID 1)
   * Volumes partilhados de cluster
     
     Para informações sobre a criação de volumes no dispositivo do StorSimple Olá ou o dispositivo virtual StorSimple, aceda demasiado[passo 6: criar um volume](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume), na [implementar o dispositivo StorSimple no local](storsimple-8000-deployment-walkthrough-u2.md).

## <a name="install-a-new-storsimple-snapshot-manager"></a>Instalar um novo Snapshot Manager do StorSimple
Antes de instalar o Snapshot Manager do StorSimple, certifique-se de que os volumes de Olá que criou no dispositivo do StorSimple Olá ou o dispositivo virtual StorSimple são montados, inicializados e formatados conforme descrito em [configurar pré-requisitos](#configure-prerequisites).

> [!IMPORTANT]
> * Para um dispositivo virtual StorSimple, o anfitrião de Olá tem de ser uma máquina de Virtual do Microsoft Azure. 
> * Olá anfitrião deve executar o Windows 2008 R2, Windows Server 2012 ou Windows Server 2012 R2. Se o servidor estiver a executar o Windows Server 2008 R2, tem de instalar também Windows Server 2008 SP1 e o Windows Management Framework 3.0.
> * Tem de configurar uma ligação de iSCSI do dispositivo StorSimple do Olá anfitrião toohello antes de poder ligar Olá dispositivo tooStorSimple Snapshot Manager.

Siga estes passos toocomplete uma instalação de raiz do Snapshot Manager do StorSimple. Se estiver a instalar uma atualização, visite demasiado[atualizar ou reinstalar o Snapshot Manager do StorSimple](#upgrade-or-reinstall-storsimple-snapshot-manager).

* Passo 1: Instalar o instantâneo do StorSimple Manager 
* Passo 2: Ligar o dispositivo de tooa Snapshot Manager do StorSimple 
* Passo 3: Verificar o dispositivo de toohello Olá ligação 

### <a name="step-1-install-storsimple-snapshot-manager"></a>Passo 1: Instalar o instantâneo do StorSimple Manager
Utilize Olá os seguintes passos tooinstall Snapshot Manager do StorSimple.

#### <a name="tooinstall-storsimple-snapshot-manager"></a>tooinstall Snapshot Manager do StorSimple
1. Transferir o software Snapshot Manager do StorSimple de Olá (aceda demasiado[Snapshot Manager do StorSimple](https://www.microsoft.com/download/details.aspx?id=44220) no Olá Microsoft Download Center) e guarde-o localmente no anfitrião de Olá.
2. No Explorador de ficheiros, faça duplo clique pasta comprimida Olá e, em seguida, clique em **extrair todos os**.
3. No Olá **pastas extrair comprimidos (Zipped)** janela, no Olá **selecione um destino e extrair ficheiros** caixa, escreva ou procure o caminho de toohello onde pretende que toobe toofile extraído.
   
    > [!IMPORTANT]
    > Tem de instalar o Snapshot Manager do StorSimple no Olá unidade c:.
    
4. Selecione Olá **Mostrar extrair ficheiros concluído** caixa de verificação e, em seguida, clique em **extrair**.
   
    ![Extrair a caixa de diálogo de ficheiros](./media/storsimple-snapshot-manager-deployment/HCS_SSM_extract_files.png) 
5. Quando estiver concluída a extração Olá, a pasta de destino Olá abre. Faça duplo clique ícone de configuração de aplicação Olá que aparece na pasta de destino Olá.
6. Quando Olá **com êxito a configuração** mensagem for apresentada, clique em **fechar**. Deverá ver o ícone de Snapshot Manager do StorSimple Olá no ambiente de trabalho.
   
    ![ícone de ambiente de trabalho](./media/storsimple-snapshot-manager-deployment/HCS_SSM_desktop_icon.png) 

### <a name="step-2-connect-storsimple-snapshot-manager-tooa-device"></a>Passo 2: Ligar o dispositivo de tooa Snapshot Manager do StorSimple
Utilize Olá os seguintes passos tooconnect dispositivo StorSimple tooa Snapshot Manager do StorSimple.

#### <a name="tooconnect-storsimple-snapshot-manager-tooa-device"></a>tooconnect dispositivo tooa Snapshot Manager do StorSimple
1. Clique em Olá Snapshot Manager do StorSimple no ícone no seu ambiente de trabalho. é apresentada a janela do Olá Snapshot Manager do StorSimple. janela de Olá contém um **âmbito** painel, um **resultados** painel e um **ações** painel. 
   
    ![Interface de utilizador do Snapshot Manager do StorSimple](./media/storsimple-snapshot-manager-deployment/HCS_SSM_gui_panes.png)
   
   * Olá **âmbito** painel (painel esquerdo Olá) contém uma lista de nós organizados de uma estrutura de árvore. Pode expandir alguns nós tooselect uma vista ou o nó de toothat relacionados dados específicos. Clique em tooexpand de ícone de seta de Olá ou fechar um nó. Faça duplo clique num item Olá **âmbito** painel toosee uma lista de ações disponíveis para que o item.
   * Olá **resultados** painel (Olá center) contém informações de estado detalhadas sobre o nó de Olá, vista ou dados que selecionou na Olá **âmbito** painel.
   * Olá **ações** painel lista as operações de Olá que pode efetuar no nó de Olá, vista ou dados que selecionou na Olá **âmbito** painel.
     
     Para obter uma descrição completa de interface de utilizador do Snapshot Manager do StorSimple Olá, consulte [interface de utilizador do Snapshot Manager do StorSimple](storsimple-use-snapshot-manager.md).
2. No Olá **âmbito** painel, contexto Olá **dispositivos** nó e, em seguida, clique em **configurar um dispositivo**. Olá **configurar um dispositivo** é apresentada a caixa de diálogo.
   
    ![Configurar um dispositivo](./media/storsimple-snapshot-manager-deployment/HCS_SSM_config_device.png) 
3. No Olá **dispositivo** lista caixa, endereço IP de Olá selecione do dispositivo de Microsoft Azure StorSimple Olá ou o dispositivo virtual. No Olá **palavra-passe** caixa de texto, escrever Olá Snapshot Manager do StorSimple palavra-passe que criou para o dispositivo de Olá no Olá portal do Azure. Clique em **OK**.
4. Snapshot Manager do StorSimple procuram dispositivos de Olá que identificou. Se o dispositivo de Olá estiver disponível, o Snapshot Manager do StorSimple adiciona uma ligação. Pode [Verifique se o dispositivo de toohello Olá ligação](#to-verify-the-connection) tooconfirm Olá ligação foi adicionado com êxito.
   
    Se o dispositivo Olá estiver indisponível por qualquer motivo, o Snapshot Manager do StorSimple devolve uma mensagem de erro. Clique em **OK** tooclose Olá mensagem de erro e, em seguida, clique em **Cancelar** tooclose Olá **configurar um dispositivo** caixa de diálogo.
5. Quando estabelece ligação tooa dispositivo, o Snapshot Manager do StorSimple importa cada grupo de volume configurado para que o dispositivo, desde que hello volume tem associadas ao grupo de cópias de segurança. Grupos de volume que não dispõe de cópias de segurança associadas não foram importados. Além disso, as políticas de cópia de segurança que foram criadas para um grupo de volume não são importadas. toosee Olá grupos importados, faça duplo clique Olá mais alto **Volume grupos** nó Olá **âmbito** painel e clique em **alternar grupos importados**.

### <a name="step-3-verify-hello-connection-toohello-device"></a>Passo 3: Verificar o dispositivo de toohello Olá ligação
Utilize Olá tooverify passos que Snapshot Manager do StorSimple é o dispositivo StorSimple ligado toohello a seguir.

#### <a name="tooverify-hello-connection"></a>ligação de Olá tooverify
1. No Olá **âmbito** painel, clique em Olá **dispositivos** nós.
   
    ![Estado do dispositivo Snapshot Manager do StorSimple](./media/storsimple-snapshot-manager-deployment/HCS_SSM_Device_status.png) 
2. Verifique Olá **resultados** painel: 
   
   * Se é apresentado um indicador de verde no ícone de dispositivo Olá e **disponível** aparece no Olá **estado** coluna, em seguida, dispositivos de Olá está ligada. 
   * Se é apresentado um indicador de vermelho no ícone de dispositivo Olá e indisponível aparece no Olá **estado** coluna, em seguida, dispositivos de Olá não está ligada. 
   * Se **atualizar** aparece no Olá **estado** coluna, em seguida, Snapshot Manager do StorSimple está a obter grupos de volume e cópias de segurança associadas para um dispositivo ligado.

## <a name="upgrade-or-reinstall-storsimple-snapshot-manager"></a>Atualizar ou reinstalar o Snapshot Manager do StorSimple
Deve desinstalar completamente Snapshot Manager do StorSimple antes de atualizar ou reinstalar o software de Olá. 

Antes de reinstalar o Snapshot Manager do StorSimple, cópia de segurança Olá Snapshot Manager do StorSimple base de dados existente no computador do anfitrião de Olá. Isto guarda informações de configuração e as políticas de cópia de segurança no Olá, para que facilmente pode restaurar estes dados a partir de cópia de segurança.

Se estiver a atualizar ou reinstalar o Snapshot Manager do StorSimple, siga estes passos:

* Passo 1: Desinstalar Snapshot Manager do StorSimple 
* Passo 2: Criar cópias de segurança base de dados do Olá Snapshot Manager do StorSimple 
* Passo 3: Reinstale o Snapshot Manager do StorSimple e restaurar a base de dados de Olá 

### <a name="step-1-uninstall-storsimple-snapshot-manager"></a>Passo 1: Desinstalar Snapshot Manager do StorSimple
Utilize Olá os seguintes passos toouninstall Snapshot Manager do StorSimple.

#### <a name="toouninstall-storsimple-snapshot-manager"></a>toouninstall Snapshot Manager do StorSimple
1. No computador do anfitrião de Olá, abra Olá **painel de controlo**, clique em **programas**e, em seguida, clique em **programas e funcionalidades**.
2. No painel esquerdo Olá, clique em **desinstalar ou alterar um programa**.
3. Clique com botão direito **Snapshot Manager do StorSimple**e, em seguida, clique em **desinstalação**.
4. Esta ação inicia Olá programa de configuração do Snapshot Manager do StorSimple. Clique em **modificar o programa de configuração**e, em seguida, clique em **desinstalação**.
   
   > [!NOTE]
   > Se existem quaisquer processos MMC em execução em segundo plano de Olá, tais como Snapshot Manager do StorSimple ou gestão de discos, desinstalar Olá irá falhar e receberá uma mensagem tooclose todas as instâncias do MMC antes de tentarem programa de Olá toouninstall. Selecione **automaticamente feche as aplicações e tente toorestart-las após a configuração concluir**e, em seguida, clique em **OK**.
   > 
   > 
5. Quando desinstala Olá processo estiver concluído, um **com êxito a configuração** é apresentada a mensagem. Clique em **Fechar**.

### <a name="step-2-back-up-hello-storsimple-snapshot-manager-database"></a>Passo 2: Criar cópias de segurança base de dados do Olá Snapshot Manager do StorSimple
Utilizar Olá toocreate passos a seguir e guarde uma cópia da base de dados do Olá Snapshot Manager do StorSimple.

#### <a name="tooback-up-hello-database"></a>tooback cópias de segurança da base de dados de Olá
1. Pare Olá StorSimple serviço de gestão da Microsoft:
   
   1. Inicie o Gestor de servidor.
   2. No Olá Dashboard do Gestor de servidores, no Olá **ferramentas** menu, selecione **serviços**.
   3. No Olá **serviços** página, selecione **serviço de gestão da Microsoft StorSimple**.
   4. No Olá com o botão direito painel, em **serviço de gestão da Microsoft StorSimple**, clique em **parar o serviço de Olá**.
      
        ![Parar o serviço de Gestor de dispositivos do StorSimple Olá](./media/storsimple-snapshot-manager-deployment/HCS_SSM_stop_service.png)
2. Procure tooC:\ProgramData\Microsoft\StorSimple\BACatalog. 
   
   > [!NOTE]
   > ProgramData é uma pasta oculta.
  
3. Localize ficheiro XML do catálogo de Olá, copiar o ficheiro de Olá e arquivo Olá cópia numa localização segura ou na nuvem de Olá.
   
    ![Ficheiro de catálogo de cópias de segurança do StorSimple](./media/storsimple-snapshot-manager-deployment/HCS_SSM_bacatalog.png)
4. Reinicie Olá StorSimple serviço de gestão da Microsoft: 
   
   1. No Olá Dashboard do Gestor de servidores, no Olá **ferramentas** menu, selecione **serviços**.
   2. No Olá **serviços** página, selecione de Olá **Microsoft StorSimple gestão Servic**i.
   3. No Olá com o botão direito painel, em **serviço de gestão da Microsoft StorSimple**, clique em **Reiniciar serviço Olá**. 

### <a name="step-3-reinstall-storsimple-snapshot-manager-and-restore-hello-database"></a>Passo 3: Reinstale o Snapshot Manager do StorSimple e restaurar a base de dados de Olá
tooreinstall Snapshot Manager do StorSimple, siga os passos Olá [instalar um novo Snapshot Manager do StorSimple](#install-a-new-storsimple-snapshot-manager). Em seguida, utilize Olá seguinte base de dados do procedimento toorestore Olá Snapshot Manager do StorSimple.

#### <a name="toorestore-hello-database"></a>base de dados do toorestore Olá
1. Pare Olá StorSimple serviço de gestão da Microsoft:
   
   1. Inicie o Gestor de servidor.
   2. No Olá Dashboard do Gestor de servidores, no Olá **ferramentas** menu, selecione **serviços**.
   3. No Olá **serviços** página, selecione **serviço de gestão da Microsoft StorSimple**.
   4. No Olá com o botão direito painel, em **serviço de gestão da Microsoft StorSimple**, clique em **parar o serviço de Olá**.
2. Procure tooC:\ProgramData\Microsoft\StorSimple\BACatalog.
   
   > [!NOTE]
   > ProgramData é uma pasta oculta.
   > 
   > 
3. Eliminar o ficheiro XML do catálogo de Olá e substitua-o com a versão de Olá que guardou anteriormente.
4. Reinicie Olá StorSimple serviço de gestão da Microsoft: 
   
   1. No Olá Dashboard do Gestor de servidores, no Olá **ferramentas** menu, selecione **serviços**.
   2. No Olá **serviços** página, selecione **serviço de gestão da Microsoft StorSimple**.
   3. No Olá com o botão direito painel, em **serviço de gestão da Microsoft StorSimple**, clique em **Reiniciar serviço Olá**.

## <a name="next-steps"></a>Passos seguintes
* toolearn mais sobre o Snapshot Manager do StorSimple, aceda demasiado[Novidades Snapshot Manager do StorSimple?](storsimple-what-is-snapshot-manager.md).
* toolearn mais informações sobre a interface de utilizador do Olá Snapshot Manager do StorSimple, aceda demasiado[interface de utilizador do Snapshot Manager do StorSimple](storsimple-use-snapshot-manager.md).
* toolearn mais sobre a utilização do Snapshot Manager do StorSimple, aceda demasiado[Snapshot Manager do StorSimple utilize tooadminister solução StorSimple](storsimple-snapshot-manager-admin.md).

