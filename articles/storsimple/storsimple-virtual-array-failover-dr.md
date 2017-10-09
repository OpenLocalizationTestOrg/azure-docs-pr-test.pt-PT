---
title: "aaaStorSimple matriz Virtual desastre dispositivo e de recuperação de ativação pós-falha | Microsoft Docs"
description: Saiba mais sobre como toofailover a matriz de Virtual StorSimple.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 3c1f9c62-af57-4634-a0d8-435522d969aa
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5f125efd1ffb94489cdfa7cfaafae7d57cc10131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-and-device-failover-for-your-storsimple-virtual-array-via-azure-portal"></a>Ativação pós-falha de dispositivo e de recuperação após desastre para a matriz de Virtual StorSimple através do portal do Azure

## <a name="overview"></a>Descrição geral
Este artigo descreve a recuperação de desastres Olá para o Microsoft Azure StorSimple Virtual matriz, incluindo Olá detalhada os passos toofail através de matriz virtual tooanother. Uma ativação pós-falha permite-lhe toomove os dados a partir de um *origem* dispositivo no Olá datacenter tooa *destino* dispositivo. Olá dispositivo de destino pode ser localizado na Olá mesma ou noutra localização geográfica. ativação pós-falha de dispositivo Olá é para o dispositivo completo Olá. Durante a ativação pós-falha, dados de nuvem de Olá de dispositivo de origem Olá alterações toothat de propriedade do dispositivo-alvo Olá.

Este artigo é aplicável tooStorSimple Virtual as matrizes só. toofail através de um dispositivo da 8000 série, aceda demasiado[dispositivo ativação pós-falha e recuperação após desastre do dispositivo StorSimple](storsimple-device-failover-disaster-recovery.md).

## <a name="what-is-disaster-recovery-and-device-failover"></a>O que é a ativação pós-falha de dispositivo e de recuperação de desastre?

Num cenário de recuperação (DR) após desastre, dispositivo primário Olá deixa de funcionar. Neste cenário, pode mover dados de nuvem Olá associados Olá dispositivo falhada tooanother dispositivo. Pode utilizar o dispositivo primário Olá como Olá *origem* e especifique outro dispositivo como Olá *destino*. Este processo é referenciado tooas Olá *ativação pós-falha*. Durante a ativação pós-falha, Olá todos os volumes ou partilhas de Olá do dispositivo de origem Olá alterar a propriedade e são transferidos toohello dispositivo de destino. Nenhuma filtragem de dados de Olá é permitida.

DR é modelada como um restauro completa de dispositivo utilizando térmico Olá mapa – com base em camadas e de controlo. Está definido um mapa térmico atribuindo um toohello de valor térmico dados com base na leitura e escrita padrões. Este térmico do mapa, em seguida, camadas Olá mais baixa térmico dados segmentos toohello nuvem pela primeira vez, mantendo os segmentos de dados do Olá térmico elevada (mais utilizado) no escalão local Olá. Durante uma DR, StorSimple utiliza toorestore de mapa térmico de Olá e rehydrate dados Olá da nuvem Olá. dispositivo de Olá obtém todas as Olá volumes/partilhas no Olá última cópia de segurança recente (conforme determinado internamente) e efetua um restauro dessa cópia de segurança. matriz virtual Olá orquestra processo de DR completo Olá.

> [!IMPORTANT]
> dispositivo de origem Olá é eliminado no fim de Olá de ativação pós-falha do dispositivo e, por conseguinte, não é suportada uma reativação pós-falha.
> 
> 

Recuperação após desastre é orquestrada através de funcionalidade de ativação pós-falha do dispositivo Olá e é iniciada a partir da Olá **dispositivos** painel. Este painel tabulates todos os Olá StorSimple dispositivos ligados tooyour dispositivo serviço StorSimple Manager. Para cada dispositivo, pode ver o nome amigável Olá, o estado, o capacidade aprovisionada e máxima, o tipo e o modelo.

## <a name="prerequisites-for-device-failover"></a>Pré-requisitos para ativação pós-falha do dispositivo

### <a name="prerequisites"></a>Pré-requisitos

Para um dispositivo de ativação pós-falha, certifique-se de que Olá os seguintes pré-requisitos são cumpridos:

* tem do dispositivo de origem Olá toobe num **desativado** estado.
* Olá dispositivo de destino tem de tooshow cópias de segurança como **pronto tooset segurança** no Olá portal do Azure. Aprovisionar uma matriz de virtual de destino de Olá capacidade igual ou superior. Utilize Olá local web IU tooconfigure e registar com êxito a matriz de Olá virtual de destino.
  
  > [!IMPORTANT]
  > Não tente tooconfigure Olá virtual dispositivo registado através do serviço de Olá. Nenhuma configuração de dispositivo deve ser efetuada através do serviço de Olá.
  > 
  > 
* dispositivo de destino Olá não pode ter Olá mesmo nome como dispositivo de origem Olá.
* Olá dispositivo de origem e de destino tem toobe Olá mesmo tipo. Só pode efetuar a ativação pós-falha de uma matriz virtual configurada como um servidor de ficheiros de tooanother de servidor de ficheiros. Olá mesmo se aplica a um servidor de iSCSI.
* Para um servidor de ficheiros de DR, recomendamos que associa o toohello de dispositivo de destino Olá mesmo domínio como origem Olá. Esta configuração assegura que as permissões de partilha Olá são resolvidas automaticamente. Apenas Olá ativação pós-falha tooa dispositivo de destino no Olá mesmo domínio.
* dispositivos de destino disponíveis Olá para DR são dispositivos que tenham Olá igual ou maior capacidade em comparação com o dispositivo de origem toohello. Olá dispositivos que estão ligado tooyour service mas não cumpre os Olá critérios de espaço suficiente não estão disponíveis como dispositivos de destino.

### <a name="other-considerations"></a>Outras considerações

* Para uma ativação pós-falha planeada 
  
  * Recomendamos que colocar todos os volumes de Olá ou partilhas no dispositivo de origem de Olá offline.
  * Recomendamos que efetuar uma cópia de segurança do dispositivo Olá e, em seguida, continue com a perda de dados de toominimize de ativação pós-falha de Olá. 
* Para uma ativação pós-falha não planeada, o dispositivo Olá utiliza Olá mais recentes dados de Olá de toorestore cópia de segurança.

### <a name="device-failover-prechecks"></a>Prechecks de ativação pós-falha do dispositivo

Antes de Olá que começa a DR, o dispositivo Olá efetua prechecks. Estas verificações garantir que não ocorrerem erros quando começa a DR. Olá prechecks incluem:

* Validar a conta de armazenamento Olá.
* A verificar Olá nuvem conectividade tooAzure.
* A verificar o espaço disponível no dispositivo de destino Olá.
* A verificar se tem um volume de dispositivo de origem de servidor de iSCSI
  
  * nomes válidos ACR.
  * IQN válido (que não exceda 220 carateres).
  * válido CHAP palavras-passe (12-16 carateres).

Se algum dos Olá precedente prechecks falhar, não é possível prosseguir com Olá DR. Resolva os problemas e, em seguida, repita DR.

Olá DR esteja concluída com êxito, a propriedade de Olá de dados de nuvem Olá no dispositivo de origem Olá está toohello transferidos dispositivo de destino. dispositivo de origem Olá, em seguida, já não está disponível no portal de Olá. Acesso tooall Olá volumes/partilhas no dispositivo de origem Olá é bloqueado e dispositivo de destino Olá fica ativo.

> [!IMPORTANT]
> Apesar do dispositivo de Olá já não estiver disponível, máquina virtual Olá que aprovisionou no sistema anfitrião de Olá ainda está a consumir recursos. Assim que for concluída com sucesso Olá DR, pode eliminar esta máquina virtual do sistema anfitrião.
> 
> 

## <a name="fail-over-tooa-virtual-array"></a>Efetuar a ativação pós-falha de matriz virtual tooa

Recomendamos que aprovisionar, configurar e registar noutra matriz de Virtual StorSimple com o serviço do Gestor de dispositivos do StorSimple antes de executar este procedimento.

> [!IMPORTANT]
> 
> * Não é possível efetuar a ativação pós-falha de um 8000 do StorSimple série dispositivo tooa 1200 dispositivo virtual.
> * Pode efetuar a ativação pós-falha de dispositivo do Federal Information Processing Standard (FIPS) ativada dispositivo virtual tooanother FIPS ativada ou tooa não FIPS dispositivos implementadas no portal de administração pública Olá.


Efetue Olá os seguintes passos toorestore Olá dispositivo tooa destino dispositivo virtual StorSimple.

1. Aprovisiona e configura um dispositivo de destino cumpre Olá [pré-requisitos para ativação pós-falha do dispositivo](#prerequisites). Conclua a configuração de dispositivo Olá através da IU da web local Olá e registá-lo tooyour do serviço StorSimple Manager de dispositivo. Se criar um servidor de ficheiros, aceda toostep 1 de [configurado como servidor de ficheiros](storsimple-virtual-array-deploy3-fs-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device). Se criar um servidor de iSCSI, aceda toostep 1 de [configurado como servidor de iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device).

2. Colocar volumes/partilhas offline no anfitrião de Olá. tootake Olá volumes/partilhas offline, consulte as instruções de sistema operativo específicas toohello para o anfitrião de Olá. Se não já offline, terá de tootake todas as Olá volumes/partilhas offline no dispositivo Olá, Olá seguinte.
   
    1. Aceda demasiado**dispositivos** painel e selecione o seu dispositivo.
   
    2. Aceda demasiado**definições > Gerir > partilhas** (ou **definições > Gerir > Volumes**). 
   
    3. Selecione um partilha/volume, clique com o botão direito e selecione **colocar offline**. 
   
    4. Quando lhe for pedido para confirmação, verifique **compreendo impacto Olá de colocar offline nesta partilha.** 
   
    5. Clique em **colocar offline**.

3. No seu serviço do Gestor de dispositivos do StorSimple, aceda demasiado**gestão > dispositivos**. No Olá **dispositivos** painel, selecione e clique em seu dispositivo de origem.

4. No seu **dashboard dispositivo** painel, clique em **desativar**.

5. No Olá **desativar** painel, lhe for pedida a confirmação. A desativação de dispositivo é um *permanente* processo não pode ser anulado. Pode também é reminded tootake os partilhas/volumes offline no anfitrião de Olá. Escreva tooconfirm de nome de dispositivo Olá e clique em **desativar**.
   
    ![](./media/storsimple-virtual-array-failover-dr/failover1.png)
6. a desativação de Olá é iniciado. Receberá uma notificação de desativação de Olá esteja concluída com êxito.
   
    ![](./media/storsimple-virtual-array-failover-dr/failover2.png)
7. Na página de dispositivos de Olá, o estado do dispositivo Olá agora irá alterar demasiado**desativado**.
    ![](./media/storsimple-virtual-array-failover-dr/failover3.png)
8. No Olá **dispositivos** painel, selecione e clique em dispositivo de origem desativada de Olá para ativação pós-falha. 
9. No Olá **dashboard dispositivo** painel, clique em **falhar**. 
10. No Olá **efetuar a ativação pós-falha do dispositivo** painel, Olá a seguir:
    
    1. campo de dispositivo de origem Olá é preenchido automaticamente. Tenha em atenção Olá tamanho total dos dados para o dispositivo de origem Olá. tamanho dos dados Olá deve ser inferior à capacidade disponível do Olá no dispositivo de destino Olá. Reveja os detalhes de Olá associados Olá dispositivo de origem, tais como o nome do dispositivo, capacidade total e nomes de Olá Olá de partilhas de que estão a ativação pós-falha.

    2. A partir da lista pendente de Olá dos dispositivos disponíveis, escolha um **dispositivo-alvo**. Apenas os dispositivos de Olá que tem capacidade suficiente são apresentados na lista pendente de Olá.

    3. Verifique se **compreendo que esta operação irá efetuar a ativação pós-falha do dispositivo-alvo dados toohello**. 

    4. Clique em **falhar**.
    
        ![](./media/storsimple-virtual-array-failover-dr/failover4.png)
11. Inicia uma tarefa de ativação pós-falha e receber uma notificação. Aceda demasiado**dispositivos > tarefas** toomonitor ativação pós-falha de Olá.
    
     ![](./media/storsimple-virtual-array-failover-dr/failover5.png)
12. No Olá **tarefas** painel, verá uma tarefa de ativação pós-falha criada para o dispositivo de origem Olá. Esta tarefa efetua Olá DR prechecks.
    
    ![](./media/storsimple-virtual-array-failover-dr/failover6.png)
    
     Após prechecks Olá DR são bem sucedidas, o trabalho de ativação pós-falha Olá irá gerar as tarefas de restauro para cada partilha/volume que exista no seu dispositivo de origem.
    
    ![](./media/storsimple-virtual-array-failover-dr/failover7.png)
13. Após a ativação pós-falha de Olá toohello concluída, aceda **dispositivos** painel.
    
    1. Selecione e clique em dispositivo StorSimple Olá que foi utilizado como dispositivo de destino Olá para o processo de ativação pós-falha de Olá.
    2. Aceda demasiado**definições > gestão > partilhas** (ou **Volumes** se o servidor de iSCSI). No Olá **partilhas** painel, pode ver todas as partilhas Olá (volumes) do dispositivo antigo Olá.
        ![](./media/storsimple-virtual-array-failover-dr/failover9.png)
14. Terá de demasiado[criar um alias de DNS](https://support.microsoft.com/kb/168322) para que Olá todas as aplicações que estão a tentar tooconnect pode obter toohello redirecionada novo dispositivo.

## <a name="errors-during-dr"></a>Erros durante a DR

**Falha de conectividade de nuvem durante a DR**

Se a conectividade de nuvem Olá é interrompida após DR foi iniciada e antes do restauro de dispositivo Olá estiver concluído, Olá DR irá falhar. Receberá uma notificação de failore. dispositivo de destino Olá para DR está marcado como *não utilizável.* Não é possível utilizar Olá mesmo dispositivo de destino para o DRs futuras.

**Nenhum dispositivo de destino compatível**

Se dispositivos de destino disponíveis Olá não têm espaço suficiente, verá um efeito de toohello de erro que não existem nenhum dispositivo de destino compatível.

**Precheck falhas**

Se um dos Olá prechecks não é satisfeito, em seguida, verá precheck falhas.

## <a name="business-continuity-disaster-recovery-bcdr"></a>Recuperação de desastre de continuidade de negócio (BCDR)

Um cenário de recuperação (BCDR) de desastre de continuidade do negócio ocorre quando Olá todo o datacenter do Azure deixa de funcionar. Isto pode afetar o seu serviço do Gestor de dispositivos do StorSimple e Olá associadas dispositivos StorSimple.

Se existirem dispositivos StorSimple que foram registados antes de um desastre ocorreu, estes dispositivos StorSimple poderão ter toobe eliminado. Após desastre Olá, pode recriá-lo e configurar esses dispositivos.

## <a name="next-steps"></a>Passos seguintes

Saiba mais sobre como demasiado[administrar a matriz de Virtual StorSimple, utilizando a IU da web local Olá](storsimple-ova-web-ui-admin.md).

