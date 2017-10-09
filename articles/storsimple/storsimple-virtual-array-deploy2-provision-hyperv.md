---
title: aaaProvision StorSimple matriz Virtual no Hyper-V | Microsoft Docs
description: "Este tutorial segundo na implementação de matriz Virtual StorSimple envolve o aprovisionamento de uma matriz virtual no Hyper-V."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 4354963c-e09d-41ac-9c8b-f21abeae9913
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f47d642f740827ae1440b819e07067c6a183527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-hyper-v"></a>Implementar StorSimple Virtual matriz - aprovisionar no Hyper-V
![](./media/storsimple-virtual-array-deploy2-provision-hyperv/hyperv4.png)

## <a name="overview"></a>Descrição geral
Este tutorial descreve como tooprovision uma Virtual StorSimple matriz num sistema anfitrião com Hyper-V no Windows Server 2012 R2, Windows Server 2012 ou Windows Server 2008 R2. Este artigo aplica-se a implementação de toohello das matrizes de Virtual StorSimple no portal do Azure e na nuvem do Microsoft Azure Government.

É necessário tooprovision de privilégios de administrador e configurar uma matriz de virtual. programa de configuração de Olá, aprovisionamento e inicial pode demorar cerca de 10 minutos toocomplete.

## <a name="provisioning-prerequisites"></a>Pré-requisitos de aprovisionamento
Aqui, encontrará Olá pré-requisitos tooprovision uma matriz de virtual num sistema anfitrião com Hyper-V no Windows Server 2012 R2, Windows Server 2012 ou Windows Server 2008 R2.

### <a name="for-hello-storsimple-device-manager-service"></a>Para Olá serviço StorSimple Manager de dispositivo
Antes de começar, certifique-se de que:

* Concluiu todos os passos Olá [portal de Olá preparar para a matriz Virtual StorSimple](storsimple-virtual-array-deploy1-portal-prep.md).
* Transferir imagem de matriz virtual Olá do Hyper-V de Olá portal do Azure. Para obter mais informações, consulte **passo 3: imagem de matriz virtual transferência Olá** de [portal de Olá preparar para o guia de matriz Virtual StorSimple](storsimple-virtual-array-deploy1-portal-prep.md).

  > [!IMPORTANT]
  > software Olá em execução no Olá matriz Virtual StorSimple só pode ser utilizado com Olá serviço StorSimple Manager do dispositivo.
  >
  >

### <a name="for-hello-storsimple-virtual-array"></a>Para Olá matriz Virtual StorSimple
Antes de implementar uma matriz de virtual, certifique-se de que:

* Tem o sistema anfitrião tooa de acesso com Hyper-V no Windows Server 2008 R2 ou posterior que podem ser utilizado tooa aprovisionar um dispositivo.
* sistema de anfitrião de Olá é capaz de toodedicate Olá os seguintes recursos tooprovision a matriz de virtual:

  * Um mínimo de 4 núcleos.
  * Pelo menos 8 GB de RAM. Se planear matriz de virtual Olá tooconfigure como servidor de ficheiros, 8 GB suporta inferior a 2 milhões de ficheiros. Terá de ficheiros de 2-4 milhões de toosupport do 16 GB de RAM.
  * Uma interface de rede.
  * Um disco virtual 500 GB de dados.

### <a name="for-hello-network-in-hello-datacenter"></a>Para a rede de Olá Olá Centro de dados
Antes de começar, reveja Olá redes requisitos toodeploy uma matriz de Virtual StorSimple e configure a rede de centro de dados de Olá adequadamente. Para obter mais informações, consulte [matriz Virtual StorSimple requisitos de rede](storsimple-ova-system-requirements.md#networking-requirements).

## <a name="step-by-step-provisioning"></a>Passo a passo de aprovisionamento
tooprovision e ligar matriz virtual tooa, terá de Olá tooperform os seguintes passos:

1. Certifique-se de que o sistema anfitrião de Olá tem suficiente recursos toomeet Olá mínimo matriz virtual os requisitos de.
2. Aprovisione uma matriz virtual no seu hipervisor.
3. Iniciar matriz virtual Olá e obter Olá endereço IP.

Cada um destes passos é explicada no Olá secções a seguir.

## <a name="step-1-ensure-that-hello-host-system-meets-minimum-virtual-array-requirements"></a>Passo 1: Certifique-se de que o sistema anfitrião de Olá cumpre os requisitos de matriz virtual mínima
toocreate uma matriz de virtual, é necessário:

* função de Olá Hyper-V instalada no Windows Server 2012 R2, Windows Server 2012 ou Windows Server 2008 R2 SP1.
* Gestor de Hyper-V do Microsoft num cliente Microsoft Windows ligada toohello anfitrião.

Certifique-se de que Olá subjacente hardware (sistema de anfitrião) no qual está a criar matriz virtual Olá Olá toodedicate capaz de matriz de virtual de tooyour de recursos a seguir:

* Um mínimo de 4 núcleos.
* Pelo menos 8 GB de RAM. Se planear matriz de virtual Olá tooconfigure como servidor de ficheiros, 8 GB suporta inferior a 2 milhões de ficheiros. Terá de ficheiros de 2-4 milhões de toosupport do 16 GB de RAM.
* Uma interface de rede.
* Um disco virtual 500 GB para os dados de sistema.

## <a name="step-2-provision-a-virtual-array-in-hypervisor"></a>Passo 2: Aprovisionar uma matriz virtual no hipervisor
Efetue Olá os seguintes passos tooprovision um dispositivo no seu hipervisor.

#### <a name="tooprovision-a-virtual-array"></a>tooprovision uma matriz de virtual
1. No anfitrião do Windows Server, copie o disco local do Olá matriz virtual imagem tooa. Esta imagem (VHD ou VHDX) que transferiu através de Olá portal do Azure. Tome nota da localização de olá onde copiou imagem Olá como estiver a utilizar esta imagem posteriormente no procedimento de Olá.
2. Abra **Gestor de servidor**. No Olá canto superior direito, clique em **ferramentas** e selecione **Gestor de Hyper-V**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image1.png)  

   Se estiver a executar o Windows Server 2008 R2, abra Olá Gestor de Hyper-V. No Gestor de servidor, clique em **funções > Hyper-V > Gestor de Hyper-V**.
3. No **Gestor de Hyper-V**, no painel de âmbito de Olá, faça duplo clique o menu de contexto do sistema nó tooopen Olá e, em seguida, clique em **novo** > **Máquina Virtual**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image2.png)
4. No Olá **antes de começar** página do Olá Assistente de Nova Máquina Virtual, clique em **seguinte**.
5. No Olá **Especificar nome e localização** , indique uma **nome** para a matriz de virtual. Clique em **Seguinte**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image4.png)
6. No Olá **especificar geração** página, escolha o tipo de imagem de dispositivo Olá e, em seguida, clique em **seguinte**. Esta página não aparece se estiver a utilizar o Windows Server 2008 R2.

   * Escolha **geração 2** se tiver transferido uma imagem. vhdx para o Windows Server 2012 ou posterior.
   * Escolha **geração 1** se tiver transferido uma imagem VHD do Windows Server 2008 R2 ou posterior.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image5.png)
7. No Olá **atribuir memória** página, especifique um **memória de arranque** de, pelo menos, **8192 MB**, não ative a memória dinâmica e, em seguida, clique em **seguinte**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image6.png)  
8. No Olá **configurar redes** página, especifique Olá comutador virtual toohello ligado à Internet e, em seguida, clique em **seguinte**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image7.png)
9. No Olá **ligar disco rígido virtual** página, escolha **utilizar um disco rígido virtual existente**, especifique a localização de Olá da imagem de matriz virtual Olá (. vhdx ou. vhd) e, em seguida, clique em **seguinte**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image8m.png)
10. Olá revisão **resumo** e, em seguida, clique em **concluir** toocreate Olá máquina.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image9.png)
11. requisitos mínimos do Olá toomeet, terá de 4 núcleos. processadores virtuais tooadd 4, selecione o sistema anfitrião Olá **Gestor de Hyper-V** janela. No painel direito Olá na lista de Olá de **máquinas virtuais**, localizar a máquina virtual de Olá que acabou de criar. Selecione e clique no nome da máquina Olá e selecione **definições**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image10.png)
12. No Olá **definições** página, numa Olá painel esquerdo, clique em **processador**. Olá painel direito, defina **número de processadores virtuais** too4 (ou mais). Clique em **Aplicar**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image11.png)
13. requisitos mínimos do Olá toomeet, também terá de tooadd um disco de dados virtual 500 GB. No Olá **definições** página:

    1. No painel esquerdo Olá, selecione **controlador SCSI**.
    2. No painel direito Olá, selecione **rígido,** e clique em **adicionar**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image12.png)
14. No Olá **unidade de disco rígido** página, selecione de Olá **disco rígido Virtual** opção e clique em **novo**. Olá **Assistente de novo disco rígido Virtual** é iniciado.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image13.png)
15. No Olá **antes de começar** página do Olá novo Assistente de disco rígido Virtual, clique em **seguinte**.
16. No Olá **página escolher formato de disco**, aceite a opção predefinida Olá **VHDX** formato. Clique em **Seguinte**. Este ecrã não é apresentado se o Windows Server 2008 R2.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image15.png)
17. No Olá **página escolher tipo de disco**, definir o tipo de disco rígido virtual como **expansão dinâmica** (recomendado). **Um tamanho fixo** disco funcionariam mas poderá ser necessário toowait muito tempo. Recomendamos que utilize Olá **Differencing** opção. Clique em **Seguinte**. No Windows Server 2012 R2 e Windows Server 2012, **expansão dinâmica** é a opção predefinida de Olá enquanto no Windows Server 2008 R2, é a predefinição de Olá **um tamanho fixo**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image16.png)
18. No Olá **Especificar nome e localização** , indique uma **nome** , bem como **localização** (pode procurar tooone) para o disco de dados de Olá. Clique em **Seguinte**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image17.png)
19. No Olá **configurar disco** página, opção Olá selecione **criar um novo disco de rígido virtual em branco** e especifique o tamanho de Olá como **500 GB** (ou mais). Enquanto 500 GB é o requisito mínimo de Olá, pode aprovisionar sempre um disco maior. Tenha em atenção que não é possível expandir ou reduzir disco Olá, uma vez aprovisionado. Para mais informações sobre o tamanho de Olá de disco tooprovision, reveja a secção de dimensionamento de Olá no Olá [documento do melhores práticas](storsimple-ova-best-practices.md). Clique em **Seguinte**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image18.png)
20. No Olá **resumo** , reveja os detalhes de Olá do disco virtual de dados e da página se forem satisfeitos, clique em **concluir** disco de Olá toocreate. Olá assistente for fechado e um disco rígido virtual é adicionado tooyour máquina.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image19.png)
21. Devolver toohello **definições** página. Clique em **OK** tooclose Olá **definições** página e voltar a janela do Gestor de tooHyper-V.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image20.png)

## <a name="step-3-start-hello-virtual-array-and-get-hello-ip"></a>Passo 3: Iniciar matriz virtual Olá e obter Olá IP
Efetuar Olá toostart passos a seguir a matriz de virtual e ligar tooit.

#### <a name="toostart-hello-virtual-array"></a>matriz de virtual toostart Olá
1. Inicie matriz virtual Olá.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image21.png)
2. Depois do dispositivo de Olá está em execução, selecione o dispositivo de Olá, clique com o botão direito e selecione **Connect**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image22.png)
3. Poderá ter toowait 5-10 minutos para Olá dispositivo toobe pronto. É apresentada uma mensagem de estado em curso do Olá consola tooindicate Olá. Depois do dispositivo de Olá estiver pronto, avance demasiado**ação**. Prima `Ctrl + Alt + Delete` toolog na matriz virtual toohello. é utilizador de predefinido Olá *StorSimpleAdmin* e palavra-passe predefinida de Olá *Password1*.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image23.png)
4. Por motivos de segurança, a palavra-passe de administrador de dispositivo Olá expira no primeiro início de sessão Olá. São palavra-passe do pedido toochange Olá.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image24.png)

   Introduza uma palavra-passe com, pelo menos, 8 carateres. Olá palavra-passe deve satisfazer, pelo menos, 3 fora Olá os requisitos de 4: carateres em maiúsculas, minúsculas, numérico e especiais. Reintroduza Olá palavra-passe tooconfirm-lo. Será notificado que essa palavra-passe de Olá foi alterada.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image25.png)
5. Depois de palavra-passe de Olá foi alterado com êxito, pode reiniciar matriz virtual Olá. Aguarde Olá toostart de dispositivo.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image26.png)

    consola do Windows PowerShell Olá do dispositivo Olá é apresentada juntamente com uma barra de progresso.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image27.png)
6. Os passos 6-8 só se aplicam ao arrancar segurança num ambiente não DHCP. Se tiver um ambiente de DHCP, em seguida, ignore estes passos e avance toostep 9. Se arrancado se o dispositivo no ambiente de não DHCP, verá Olá ecrã a seguir.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image28m.png)

    Em seguida, configure a rede de Olá.
7. Olá utilize `Get-HcsIpAddress` comando toolist Olá as interfaces de rede ativadas na sua matriz virtual. Se o dispositivo tem uma única interface de rede ativada, Olá predefinido atribuído nome toothis interface é `Ethernet`.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image29m.png)
8. Olá utilize `Set-HcsIpAddress` rede de Olá tooconfigure de cmdlet. Consulte o seguinte exemplo de Olá:

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image30.png)
9. Depois da configuração inicial Olá está concluída e dispositivo Olá ter arrancado cópias de segurança, verá o texto de faixa Olá dispositivo. Tome nota do endereço IP Olá e o URL de Olá apresentados na Olá faixa texto toomanage Olá no dispositivo. Utilize este IP endereço tooconnect toohello IU da web da sua matriz virtual e a configuração de local de Olá concluída e o registo.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image31m.png)
10. (Opcional) Execute este passo apenas se estiver a implementar o seu dispositivo no Olá Government nuvem. Agora irá ativar o modo de Estados Unidos Federal Information processamento Standard (FIPS) Olá no seu dispositivo. padrão de Olá FIPS 140 define os algoritmos criptográficos aprovados para utilização pelos sistemas de computador government Federal dos EUA para proteção de Olá de dados confidenciais.

    1. tooenable Olá modo FIPS, execute Olá seguinte cmdlet:

        `Enable-HcsFIPSMode`
    2. Reinicie o seu dispositivo depois de ter ativado o modo FIPS Olá, para que validações criptográficos Olá entrem em vigor.

       > [!NOTE]
       > Pode ativar ou desativar o modo FIPS no seu dispositivo. Dispositivo de Olá alternadas entre o modo FIPS e não FIPS não é suportado.
       >
       >

Se o dispositivo não cumpre os requisitos mínimos de configuração de Olá, verá Olá seguir erro no texto de faixa Olá (mostrado abaixo). Modificar configuração de dispositivo Olá, para que hello máquina tem toomeet recursos adequado Olá requisitos mínimos. Pode, em seguida, reiniciar e ligar o dispositivo toohello. Consulte os requisitos mínimos de configuração toohello [passo 1: Certifique-se de que o sistema anfitrião de Olá cumpre os requisitos de matriz virtual mínimo](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).

![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image32.png)

Se enfrentam qualquer outro erro durante a configuração inicial Olá utilizando a IU da web local Olá, consulte toohello seguir fluxos de trabalho:

* Executar testes de diagnóstico demasiado[resolver problemas de configuração de IU da web](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).
* [Gerar o pacote de registo e ver ficheiros de registo](storsimple-ova-web-ui-admin.md#generate-a-log-package).

## <a name="next-steps"></a>Passos seguintes
* [Configurar a matriz de Virtual StorSimple como um servidor de ficheiros](storsimple-virtual-array-deploy3-fs-setup.md)
* [Configurar a matriz de Virtual StorSimple como um servidor de iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md)
