---
title: "configuração do servidor de iSCSI do aaaMicrosoft matriz Virtual do Azure StorSimple | Microsoft Docs"
description: "Descreve como registar o servidor de iSCSI StorSimple tooperform a configuração inicial e concluir a configuração do dispositivo."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4db116d1-978b-48e8-b572-a719a8425dbc
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: b4ff6391cb2af69d4e83dcdac5e027f8498005b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array--set-up-as-an-iscsi-server-via-azure-portal"></a>Implementar StorSimple Virtual matriz – conjunto de cópias de segurança como um servidor de iSCSI através do portal do Azure

![fluxo de processo de configuração do iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/iscsi4.png)

## <a name="overview"></a>Descrição geral

Este tutorial de implementação aplicam-se toohello matriz Virtual do Microsoft Azure StorSimple. Este tutorial descreve como tooperform a configuração inicial de Olá, registar o servidor de iSCSI do StorSimple, a configuração do dispositivo concluída Olá e, em seguida, criar, montar, inicializar e formatar volumes na sua matriz de Virtual StorSimple configurado como um servidor de iSCSI. 

procedimentos de Olá descritos aqui demorar cerca de 30 minutos too1 hora toocomplete. informações de Olá publicadas neste artigo aplica-se apenas tooStorSimple matrizes Virtual.

## <a name="setup-prerequisites"></a>Pré-requisitos do programa de configuração

Antes de configurar e configurar a matriz de Virtual StorSimple, certifique-se de que:

* Ter aprovisionado uma matriz de virtual e ligados tooit conforme descrito em [implementar StorSimple Virtual matriz - aprovisionar uma matriz virtual no Hyper-V](storsimple-ova-deploy2-provision-hyperv.md) ou [implementar StorSimple Virtual matriz - aprovisionar uma matriz virtual do VMware ](storsimple-virtual-array-deploy2-provision-vmware.md).
* Tem a chave de registo do serviço de Olá de Olá serviço StorSimple Manager de dispositivo que criou toomanage as matrizes de Virtual StorSimple. Para obter mais informações, consulte **passo 2: chave de registo do serviço de Olá Get** no [implementar StorSimple Virtual matriz - preparar o portal de Olá](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).
* Se este for Olá segunda virtual matriz que está a registar com o serviço Gestor de dispositivos do StorSimple existente, deve ter a chave de encriptação de dados de serviço Olá. Esta chave foi gerada quando o primeiro dispositivo de Olá foi registado com êxito com este serviço. Se tiver perdido a esta chave, consulte **chave de encriptação de dados de serviço Olá Get** no [utilize Olá IU da Web tooadminister a matriz de Virtual StorSimple](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key).

## <a name="step-by-step-setup"></a>Programa de configuração passo a passo

Utilizar Olá seguir instruções passo a passo tooset cópias de segurança e configure a matriz de Virtual StorSimple:

* [Passo 1: Concluir web local de Olá configuração da IU e registar o seu dispositivo](#step-1-complete-the-local-web-ui-setup-and-register-your-device)
* [Passo 2: Olá concluída necessária a configuração do dispositivo](#step-2-complete-the-required-device-setup)
* [Passo 3: Adicionar um volume](#step-3-add-a-volume)
* [Passo 4: Montar, inicializar e formatar um volume](#step-4-mount-initialize-and-format-a-volume)

## <a name="step-1-complete-hello-local-web-ui-setup-and-register-your-device"></a>Passo 1: Concluir web local de Olá configuração da IU e registar o seu dispositivo

#### <a name="toocomplete-hello-setup-and-register-hello-device"></a>toocomplete Olá, configuração e registar o dispositivo de Olá

1. Abra uma janela do browser. tipo de IU da web de toohello a tooconnect:
   
    `https://<ip-address of network interface>`
   
    Utilize URL de ligação de Olá que anotou no passo anterior Olá. Verá um erro notificam que há um problema com o certificado de segurança do Web site Olá. Clique em **continuar toothis web página**.
   
    ![Erro de certificado de segurança](./media/storsimple-virtual-array-deploy3-iscsi-setup/image3.png)
2. IU do seu dispositivo virtual como de web de início de sessão toohello **StorSimpleAdmin**. Introduza Olá dispositivo administrador palavra-passe que alterou no passo 3: início Olá virtual dispositivo [implementar StorSimple Virtual matriz - aprovisionar um dispositivo virtual no Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) ou [implementar StorSimple Virtual matriz - Aprovisionar um dispositivo virtual do VMware](storsimple-virtual-array-deploy2-provision-vmware.md).
   
    ![Página de início de sessão](./media/storsimple-virtual-array-deploy3-iscsi-setup/image4.png)
3. Será conduzido toohello **home page** página. Esta página descreve Olá várias definições necessários tooconfigure e registar Olá dispositivo virtual com o serviço de Gestor de dispositivos do StorSimple Olá. Tenha em atenção que Olá **as definições de rede**, **as definições de proxy de Web**, e **tempo definições** são opcionais. Olá, apenas as definições requeridas são **definições do dispositivo** e **definições da Cloud**.
   
    ![página inicial](./media/storsimple-virtual-array-deploy3-iscsi-setup/image5.png)
4. No Olá **as definições de rede** página em **interfaces de rede**, dados 0 serão configurados automaticamente para si. Cada interface de rede é definido por predefinição tooget um endereço IP automaticamente (DHCP). Por conseguinte, um endereço IP, a sub-rede e o gateway serão automaticamente atribuídos (para IPv4 e IPv6).
   
    Quando planear toodeploy o dispositivo como um servidor de iSCSI (armazenamento de blocos tooprovision), recomendamos que desative Olá **obter automaticamente endereço IP** opção e configurar endereços IP estáticos.
   
    ![Página de definições de rede](./media/storsimple-virtual-array-deploy3-iscsi-setup/image6.png)
   
    Se tiver adicionado mais de uma interface de rede durante o aprovisionamento de Olá do dispositivo Olá, pode configurá-las aqui. Tenha em atenção de que pode configurar a sua interface de rede como IPv4 apenas ou como IPv4 e IPv6. Configurações de apenas de IPv6 não são suportadas.
5. Servidores DNS são necessários porque são utilizados quando o dispositivo tenta toocommunicate com os fornecedores de serviços de armazenamento na nuvem ou tooresolve dispositivo por nome se estiver configurado como servidor de ficheiros. No Olá **as definições de rede** página em Olá **servidores DNS**:
   
   1. Um servidor DNS primário e secundário será configurado automaticamente. Se optar por tooconfigure endereços IP estáticos, pode especificar servidores DNS. Para elevada disponibilidade, recomendamos que configure um site primário e um servidor DNS secundário.
   2. Clique em **Aplicar**. Este procedimento irá aplicar e validar as definições de rede Olá.
6. No Olá **definições do dispositivo** página:
   
   1. Atribuir um único **nome** tooyour dispositivo. Este nome pode ter 1-15 carateres e pode conter letra, números e hífenes.
   2. Clique em Olá **servidor iSCSI** ícone ![ícone de iSCSI do servidor](./media/storsimple-virtual-array-deploy3-iscsi-setup/image7.png) para Olá **tipo** de dispositivo que está a criar. Um servidor de iSCSI permitirá tooprovision armazenamento de blocos.
   3. Especifique se pretende que este toobe de dispositivo associados a um domínio. Se o seu dispositivo é um servidor de iSCSI, em seguida, associar domínio Olá é opcional. Se decidir toonot associar o domínio de tooa iSCSI do servidor, clique em **aplicar**, aguarde Olá definições toobe aplicada e, em seguida, avançar toohello próximo passo.
      
       Se pretender que o domínio de tooa toojoin Olá dispositivo. Introduza um **nome de domínio**e, em seguida, clique em **aplicar**.
      
      > [!NOTE]
      > Se associar o domínio tooa do servidor de iSCSI, certifique-se de que a matriz de virtual no seu próprio unidade organizacional (UO) para o Microsoft Azure Active Directory e não existem objetos de política de grupo (GPO) são tooit aplicado.
      > 
      > 
   4. Será apresentada uma caixa de diálogo. Introduza as credenciais de domínio no formato especificado Olá. Clique Olá ícone de verificação ![ícone de verificação](./media/storsimple-virtual-array-deploy3-iscsi-setup/image15.png). as credenciais do domínio Olá serão verificadas. Verá uma mensagem de erro se Olá credenciais estão incorretas.
      
       ![credenciais](./media/storsimple-virtual-array-deploy3-iscsi-setup/image8.png)
   5. Clique em **Aplicar**. Este procedimento irá aplicar e validar as definições de dispositivo Olá.
7. (Opcionalmente)-configure o servidor proxy web. Apesar da configuração de proxy web é opcional, lembre-se de que se utilizar um proxy web, só pode configurá-lo aqui.
   
    ![configurar o web proxy](./media/storsimple-virtual-array-deploy3-iscsi-setup/image9.png)
   
    No Olá **Web proxy** página:
   
   1. Olá de alimentação **URL de proxy Web** neste formato: *http://host-IP endereço* ou *FDQN:Port número*. Tenha em atenção que não são suportados HTTPS URLs.
   2. Especifique **autenticação** como **básico** ou **nenhum**.
   3. Se estiver a utilizar a autenticação, também terá de tooprovide um **Username** e **palavra-passe**.
   4. Clique em **Aplicar**. Isto irá validar e aplicar definições de proxy de web de Olá configurado.
8. (Opcionalmente) configure as definições de hora Olá para o seu dispositivo, como o fuso horário e Olá servidores NTP primário e secundário. Os servidores NTP são necessários porque o seu dispositivo deve sincronizar a hora para se poder autenticar com os fornecedores de serviços em nuvem.
   
    ![Definições de hora](./media/storsimple-virtual-array-deploy3-iscsi-setup/image10.png)
   
    No Olá **tempo definições** página:
   
   1. A partir da Olá na lista pendente, selecione Olá **fuso horário** com base na localização geográfica Olá no qual Olá o dispositivo está a ser implementado. Olá fuso horário predefinido para o dispositivo é PST. O dispositivo utiliza este fuso horário para todas as operações agendadas.
   2. Especifique um **servidor NTP primário** para o seu dispositivo ou aceite o valor predefinido Olá time.windows.com. Certifique-se de que a sua rede permite toopass de tráfego NTP do seu centro de dados de toohello Internet.
   3. Opcionalmente, especifique um **servidor NTP secundário** para o seu dispositivo.
   4. Clique em **Aplicar**. Isto irá validar e aplicar as definições de hora Olá configurado.
9. Configure definições de nuvem Olá para o seu dispositivo. Neste passo, irá concluir a configuração de dispositivo local Olá e, em seguida, registar o dispositivo de Olá com o serviço do Gestor de dispositivos do StorSimple.
   
   1. Introduza Olá **chave de registo do serviço** que obteve **passo 2: chave de registo do serviço de Olá Get** no [implementar StorSimple Virtual matriz - preparar Olá Portal](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).
   2. Se este não for o primeiro dispositivo de Olá que está a registar com este serviço, terá de tooprovide Olá **chave de encriptação de dados do serviço**. Esta chave é necessária com Olá serviço registo tooregister chave dispositivos adicionais com Olá serviço StorSimple Manager do dispositivo. Para obter mais informações, consulte demasiado[chave de encriptação de dados de serviço Olá Get](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) no seu local de IU da web.
   3. Clique em **registar**. Esta ação irá reiniciar o dispositivo de Olá. Poderá ser necessário toowait para 2 a 3 minutos antes do dispositivo de Olá for registado com êxito. Após o reinício do dispositivo Olá, será conduzido toohello início de sessão na página.
      
      ![Registar o dispositivo](./media/storsimple-virtual-array-deploy3-iscsi-setup/image11.png)
10. Devolva toohello portal do Azure.
11. Navegue toohello **dispositivos** painel do seu serviço. Se tiver uma grande quantidade de recursos, clique em **todos os recursos**, clique no nome do serviço (procure-la, se necessário) e, em seguida, clique em **dispositivos**.
12. No Olá **dispositivos** painel, certifique-se de que o dispositivo Olá foi ligado com êxito toohello serviço ao procurar o estado de Olá. Estado do dispositivo Olá deve ser **pronto tooset segurança**.
    
    ![Registar o dispositivo](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png)

## <a name="step-2-configure-hello-device-as-iscsi-server"></a>Passo 2: Configurar o dispositivo de Olá como servidor de iSCSI

Efetue Olá os seguintes passos no Olá toocomplete portal do Azure Olá necessária a configuração do dispositivo.

#### <a name="tooconfigure-hello-device-as-iscsi-server"></a>dispositivo de Olá tooconfigure como servidor de iSCSI

1. Aceda tooyour do serviço StorSimple Manager de dispositivo e, em seguida, aceda demasiado**gestão > dispositivos**. No Olá **dispositivos** painel, o dispositivo de Olá selecione que acabou de criar. Este dispositivo seria apresentados como **pronto tooset segurança**.
   
    ![Configurar o dispositivo como servidor de iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png) 
2. Clique em dispositivo Olá e irá ver uma mensagem de faixa que indica que o dispositivo Olá é toosetup pronto.
   
    ![Configurar o dispositivo como servidor de iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis2m.png)  
3. Clique em **configurar** na barra de comando de dispositivo Olá. Esta ação abre segurança Olá **configurar** painel. No Olá **configurar** painel, Olá a seguir:
   
   * nome do servidor Olá iSCSI é preenchido automaticamente.
   * Certifique-se a encriptação de armazenamento de nuvem Olá estiver definida demasiado**ativado**. Isto garante que os dados de Olá enviados a partir de Olá dispositivo toohello nuvem são encriptados.
   * Especifique uma chave de encriptação de 32 carateres e registe-la numa aplicação Gestão de chaves para consulta futura.
   * Selecione um toobe de conta de armazenamento utilizado com o seu dispositivo. Esta subscrição, pode selecionar uma conta de armazenamento existente ou pode clicar em **adicionar** toochoose uma conta de uma subscrição diferente.
     
     ![Configurar o dispositivo como servidor de iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis4m.png)
4. Clique em **configurar** toocomplete configurar o servidor de iSCSI Olá.
   
    ![Configurar o dispositivo como servidor de iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis5m.png) 
5. Será notificado de que a criação do servidor de iSCSI Olá está em curso. Depois do servidor de iSCSI Olá é criado com êxito, Olá **dispositivos** painel está atualizado e é o estado do dispositivo correspondente Olá **Online**.
   
    ![Configurar o dispositivo como servidor de iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis9m.png)

## <a name="step-3-add-a-volume"></a>Passo 3: Adicionar um volume

1. No Olá **dispositivos** painel, o dispositivo de Olá selecione configurado como um servidor de iSCSI. Clique em **...**  (em alternativa com o botão direito nesta linha) e no menu de contexto de Olá, selecione **adicionar volume**. Também pode clicar em **+ adicionar volume** a partir da barra de comando Olá. Esta ação abre segurança Olá **adicionar volume** painel.
   
    ![Adicionar um volume](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis10m.png)
2. No Olá **adicionar volume** painel, Olá a seguir:
   
   * No Olá **nome do Volume** campo, introduza um nome exclusivo para o volume. nome de Olá tem de ser uma cadeia que contém 3 too127 carateres.
   * No Olá **tipo** pendente lista, especifique se toocreate um **em camadas** ou **afixado localmente** volume. Para cargas de trabalho que necessitem de garantias locais, latências baixas e desempenho superior, selecione **afixado localmente** **volume**. Para todos os outros dados, selecione **em camadas** **volume**.
   * No Olá **capacidade** campo, especifique o tamanho do volume de Olá Olá. Um volume em camadas tem de estar entre 500 GB e 5 TB e um volume localmente afixado tem de estar entre 50 GB e 500 GB.
     
     Um volume localmente afixado é fortemente aprovisionado e assegura que os dados primários de Olá no volume de Olá permanecem no dispositivo Olá e não transbordam toohello nuvem.
     
     Um volume em camadas no Olá é fracamente aprovisionado por outro lado. Quando cria um volume em camadas, aproximadamente, 10% de espaço de Olá é aprovisionado no escalão local Olá e 90% de espaço de Olá é aprovisionado na nuvem de Olá. Por exemplo, se aprovisionar um volume de 1 TB, 100 GB deverá residir no espaço local Olá e 900 GB seria utilizada na nuvem de Olá quando Olá camadas de dados. Isto implica por sua vez é que o se executar todas as espaço local de Olá no dispositivo Olá, não é possível aprovisionar uma partilha em camadas (porque Olá 10% não estará disponível).
     
     ![Adicionar um volume](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis12.png)
   * Clique em **ligados a anfitriões**, selecione um acesso controlo registo (ACR) correspondente toohello iniciador iSCSI que pretende tooconnect toothis volume e, em seguida, clique em **selecione**. <br><br> 
3. tooadd um novo anfitrião ligado, clique em **adicionar novo**, introduza um nome e o iSCSI de anfitrião de Olá do nome qualificado (IQN) e, em seguida, clique em **adicionar**. Se não tiver Olá IQN, aceda demasiado[Olá apêndice a: obter o IQN de um anfitrião do Windows Server](#appendix-a-get-the-iqn-of-a-windows-server-host).
   
      ![Adicionar um volume](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis15m.png)
4. Quando tiver terminado de configurar o volume, clique em **OK**. Será criado um volume com Olá especificado definições e verá uma notificação. Por predefinição, monitorização e de cópia de segurança serão ativadas para o volume de Olá.
   
     ![Adicionar um volume](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis18m.png)
5. tooconfirm Olá volume foi criada com êxito, aceda toohello **Volumes** painel. Deverá ver o volume de Olá listado.
   
   ![Adicionar um volume](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis20m.png)

## <a name="step-4-mount-initialize-and-format-a-volume"></a>Passo 4: Montar, inicializar e formatar um volume

Olá de efetuar os seguintes passos toomount, inicializar e formatar os volumes do StorSimple num anfitrião Windows Server.

#### <a name="toomount-initialize-and-format-a-volume"></a>toomount, inicializar e formatar um volume

1. Abra Olá **iniciador iSCSI** aplicação no servidor adequado Olá.
2. No Olá **propriedades do iniciador iSCSI** janela, no Olá **deteção** separador, clique em **detetar Portal**.
   
    ![detetar portal](./media/storsimple-virtual-array-deploy3-iscsi-setup/image22.png)
3. No Olá **detetar Portal de destino** caixa de diálogo, forneça o endereço IP Olá da sua interface de rede com o iSCSI e, em seguida, clique em **OK**.
   
    ![Endereço IP](./media/storsimple-virtual-array-deploy3-iscsi-setup/image23.png)
4. No Olá **propriedades do iniciador iSCSI** janela, no Olá **destinos** separador, localize Olá **destinos detetados**. (Cada volume será um destino detetado.). Estado do dispositivo Olá deve ser apresentadas como **inativo**.
   
    ![destinos detetados](./media/storsimple-virtual-array-deploy3-iscsi-setup/image24.png)
5. Selecione um dispositivo de destino e, em seguida, clique em **Connect**. Depois do dispositivo de Olá está ligado, o estado de Olá deve ser alterado demasiado**ligado**. (Para obter mais informações sobre como utilizar o Iniciador do iSCSI Olá Microsoft, consulte [iniciador iSCSI instalar e configurar o Microsoft][1].
   
    ![Selecione o dispositivo de destino](./media/storsimple-virtual-array-deploy3-iscsi-setup/image25.png)
6. No anfitrião do Windows, prima a tecla de logótipo do Windows de Olá + X e, em seguida, clique em **executar**.
7. No Olá **executar** caixa de diálogo, escreva **Diskmgmt.msc**. Clique em **OK**e Olá **gestão de discos** será apresentada a caixa de diálogo. painel direito Olá mostrará volumes Olá no seu anfitrião.
8. No Olá **gestão de discos** janela, hello volumes montados serão apresentados como mostrado na seguinte ilustração de Olá. Clique no volume de Olá detetado (clique no nome do disco de Olá) e, em seguida, clique em **Online**.
   
    ![gestão de discos](./media/storsimple-virtual-array-deploy3-iscsi-setup/image26.png)
9. Clique com botão direito e selecione **Inicializar disco**.
   
    ![Inicialize o disco 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image27.png)
10. Na caixa de diálogo Olá, selecione Olá tooinitialize de discos e, em seguida, clique em **OK**.
    
    ![Inicialize o disco 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image28.png)
11. Assistente de novo Volume simples Olá é iniciado. Selecione um tamanho de disco e, em seguida, clique em **seguinte**.
    
    ![Assistente de novo volume 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image29.png)
12. Atribuir um volume de toohello da letra de unidade e, em seguida, clique em **seguinte**.
    
    ![Assistente de novo volume 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image30.png)
13. Introduza o volume de Olá Olá parâmetros tooformat. **No Windows Server, NTFS só é suportada.** Definir too64K de tamanho de unidade de alocação de Olá. Forneça uma etiqueta para o volume. É uma melhor prática recomendada para este nome de volume do toohello idênticas do nome toobe fornecido na sua matriz de Virtual StorSimple. Clique em **Seguinte**.
    
    ![Assistente de novo volume 3](./media/storsimple-virtual-array-deploy3-iscsi-setup/image31.png)
14. Verifique os valores de Olá para o volume e, em seguida, clique em **concluir**.
    
    ![Assistente de novo volume 4](./media/storsimple-virtual-array-deploy3-iscsi-setup/image32.png)
    
    volumes de Olá aparecerão como **Online** no Olá **gestão de discos** página.
    
    ![volumes online](./media/storsimple-virtual-array-deploy3-iscsi-setup/image33.png)

## <a name="next-steps"></a>Passos seguintes

Saiba como toouse Olá IU da web do local demasiado[administrar a matriz de Virtual StorSimple](storsimple-ova-web-ui-admin.md).

## <a name="appendix-a-get-hello-iqn-of-a-windows-server-host"></a>Apêndice a: Olá de Get IQN de um anfitrião Windows Server

Efetuar os seguintes passos tooget Olá iSCSI de Olá nome qualificado (IQN) de um anfitrião do Windows que está a executar o Windows Server 2012.

#### <a name="tooget-hello-iqn-of-a-windows-host"></a>Olá tooget IQN de um anfitrião do Windows

1. Inicie o Iniciador do Olá Microsoft iSCSI no anfitrião do Windows.
2. No Olá **propriedades do iniciador iSCSI** janela, no Olá **configuração** separador, selecione e copie a cadeia de Olá de Olá **nome do iniciador** campo.
   
    ![Propriedades do iniciador iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/image34.png)
3. Guarde esta cadeia.

<!--Reference link-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx



