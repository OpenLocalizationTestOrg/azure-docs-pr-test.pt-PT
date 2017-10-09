---
title: aaaManage os volumes do StorSimple (U2) | Microsoft Docs
description: "Explica como tooadd, modificar, monitorizar e eliminar os volumes do StorSimple e como tootake-las offline se necessário."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 57896932-0aa5-4805-970c-d13403ae7551
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 10/28/2016
ms.author: alkohli
ms.openlocfilehash: 8b64f1d92023646cdf881882854d9bc5d7334a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-volumes-update-2"></a>Utilizar Olá StorSimple Manager serviço toomanage volumes (atualização 2)
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a>Descrição geral
Este tutorial explica como toouse Olá toocreate de serviço StorSimple Manager e gerir volumes no dispositivo do StorSimple Olá e o dispositivo virtual StorSimple com o Update 2 instalado.

Olá serviço StorSimple Manager é uma extensão no Olá portal clássico do Azure permite-lhe gerir solução StorSimple a partir de uma interface web único. Em volumes de toomanaging de adição, pode utilizar toocreate de serviço do StorSimple Manager Olá e gerir serviços StorSimple, ver e gerir dispositivos, ver alertas e ver e gerir políticas de cópia de segurança e de catálogo Olá de cópia de segurança.

## <a name="volume-types"></a>Tipos de volume
Volumes do StorSimple podem ser:

* **Afixado localmente volumes**: dados destes volumes permanecem no dispositivo StorSimple local do Olá permanente.
* **Volumes em camadas**: dados destes volumes podem transbordam toohello nuvem.

Um volume de arquivo é um tipo de volume em camadas. Olá eliminação de duplicados segmento tamanho maior utilizado para volumes de arquivo permite segmentos maior de Olá dispositivo tootransfer de toohello de dados na nuvem. 

Se necessário, pode alterar o tipo de volume Olá local tootiered ou a toolocal em camadas. Para mais informações, visite demasiado[alterar tipo de volume Olá](#change-the-volume-type).

### <a name="locally-pinned-volumes"></a>Volumes localmente afixados
Volumes localmente afixados são totalmente aprovisionados volumes que não camada toohello de dados na nuvem, assegurando local garante para dados primários, independentemente da conectividade de nuvem. Em volumes localmente afixados não é eliminação de duplicados e dados comprimidos; No entanto, os instantâneos de volumes localmente afixados tenham os duplicados eliminados. 

Volumes localmente afixados são totalmente aprovisionados; Por conseguinte, tem de ter espaço suficiente no seu dispositivo quando criá-los. Pode aprovisionar volumes localmente afixados tooa tamanho máximo de 8 TB no dispositivo Olá StorSimple 8100 e 20 TB no dispositivo 8600 de Olá. StorSimple reserva espaço local restante Olá dispositivos de Olá de instantâneos, metadados e o processamento de dados. Pode aumentar o tamanho de Olá de um volume localmente afixado toohello espaço máximo disponível, mas não é possível a diminuir o tamanho de Olá de um volume depois de criado.

Quando cria um volume localmente afixado, o espaço disponível do Olá para a criação de volumes em camadas é reduzido. Olá inversa também se aplica: Se tiver de volumes em camadas existentes, espaço Olá disponível para criar localmente afixado volumes serão inferior ao hello os limites máximos indicados acima. Para obter mais informações sobre volumes locais, consulte toohello [perguntas mais frequentes em volumes localmente afixados](storsimple-local-volume-faq.md).   

### <a name="tiered-volumes"></a>Volumes em camadas
Volumes em camadas são volumes de aprovisionamento dinâmico no qual Olá frequentemente dados acedidos permanecem local no dispositivo Olá e menos utilizados frequentemente dados é automaticamente em camadas toohello nuvem. Aprovisionamento dinâmico é uma tecnologia de virtualização em que o armazenamento disponível aparece recursos físicos tooexceed. Em vez de reservar antecipadamente armazenamento suficiente, StorSimple utiliza tooallocate de aprovisionamento dinâmico suficiente toomeet atual os requisitos de espaço. natureza elástico Olá armazenamento na nuvem facilita esta abordagem porque StorSimple pode aumentar ou diminuir cloud storage toomeet evolutivos.

Se estiver a utilizar Olá volume em camadas para dados de arquivo, selecionar Olá **utilizar este volume para menos dados de arquivo acedidos com frequência** tamanho dos segmentos de eliminação de duplicados Olá para o volume de alterações de caixa de verificação too512 KB. Se não selecionar esta opção, o volume em camadas correspondente de Olá irá utilizar um tamanho de segmentos de 64 KB. Um tamanho de segmentos de eliminação de duplicados maior permite a transferência do Olá dispositivo tooexpedite Olá da nuvem de toohello do arquivo de dados de grandes dimensões.

> [!NOTE]
> Arquivo volumes criados com versão anterior à atualização 2 do StorSimple serão importados como em camadas com Olá caixa de verificação arquivo selecionada.
> 
> 

### <a name="provisioned-capacity"></a>Capacidade de aprovisionamento
Consulte toohello para a capacidade máxima de aprovisionado para cada tipo de dispositivo e o volume a tabela seguinte. (Tenha em atenção de que os volumes localmente afixados não estão disponíveis num dispositivo virtual.)

|  | Tamanho máximo de volume em camadas | Tamanho do volume de afixado localmente máximo |
| --- | --- | --- |
| **Dispositivos físicos** | | |
| 8100 |64 TB |8 TB |
| 8600 |64 TB |20 TB |
| **Dispositivos virtuais** | | |
| 8010 |30 TB |N/D |
| 8020 |64 TB |N/D |

## <a name="hello-volumes-page"></a>página de Volumes de Olá
Olá **Volumes** página permite-lhe toomanage Olá armazenamento volumes que estão aprovisionados no dispositivo do Microsoft Azure StorSimple Olá para os iniciadores (servidores). Apresenta a lista de Olá de volumes no dispositivo StorSimple.

 ![Página de volumes](./media/storsimple-manage-volumes-u2/VolumePage.png)

Um volume é constituída por uma série de atributos:

* **Nome do volume** – um nome descritivo que têm de ser exclusivos e ajuda a identificar o volume de Olá. Este nome também é utilizado em relatórios de monitorização ao filtrar num volume específico.
* **Estado** – pode ser online ou offline. Se um volume estiver offline, não é visível tooinitiators (servidores) que são permitidos acesso toouse Olá volume.
* **Capacidade** – Especifica a quantidade total de Olá de dados que podem ser armazenados pelo iniciador Olá (servidor). Volumes localmente afixado são totalmente aprovisionados e residem no dispositivo do StorSimple Olá. Volumes em camadas são com aprovisionamento dinâmico e dados de Olá tem eliminação de duplicados. Com volumes de aprovisionamento dinâmico, o dispositivo não previamente alocar a capacidade de armazenamento físico internamente ou em nuvem Olá tooconfigured capacidade do volume de acordo com. capacidade do volume Olá está atribuída e consumida a pedido.
* **Tipo** – indica se o volume de Olá é **em camadas** (Olá predefinição) ou **afixado localmente**.
* **Cópia de segurança** – indica se uma política de cópia de segurança predefinida existe para o volume de Olá.
* **Acesso** – Especifica Olá os iniciadores (servidores) que são permitidos acesso toothis volume. Os iniciadores que não sejam membros de registo de controlo de acesso (ACR) que esteja associado a um volume Olá não irão ver o volume de Olá.
* **Monitorização** – Especifica se pretende ou não está a ser monitorizado um volume. Um volume terão monitorização ativada por predefinição, quando é criado. Monitorização irá, no entanto, ser desativado para um clone de volume. tooenable monitorização para um volume, siga as instruções Olá [monitorizar um volume](#monitor-a-volume). 

Utilize as instruções de Olá Olá este tutorial tooperform seguintes tarefas:

* Adicionar um volume 
* Modificar um volume 
* Alterar o tipo de volume Olá
* Eliminar um volume 
* Colocar offline um volume 
* Monitorizar um volume 

## <a name="add-a-volume"></a>Adicionar um volume
[Criado um volume](storsimple-deployment-walkthrough-u2.md#step-6-create-a-volume) durante a implementação da solução StorSimple. A adição de um volume é um procedimento semelhante.

#### <a name="tooadd-a-volume"></a>tooadd um volume
1. No Olá **dispositivos** página, selecione o dispositivo de Olá, faça duplo clique e, em seguida, clique em Olá **contentores de Volume** separador.
2. Selecione um contentor de volume na lista de Olá e faça duplo clique tooaccess Olá volumes associados ao contentor de Olá.
3. Clique em **adicionar** em Olá parte inferior da página Olá. inicia a Olá Assistente adicionar um volume.
   
     ![Adicionar Assistente de volume definições básicas](./media/storsimple-manage-volumes-u2/TieredVolEx.png)
4. No Olá Assistente para adicionar um volume, em **definições básicas**, Olá a seguir:
   
   1. Forneça um **Nome** para o volume.
   2. Selecione um **tipo de utilização** de Olá na lista pendente. Para cargas de trabalho que requerem toobe dados disponível localmente no dispositivo de Olá permanente, selecione **afixado localmente**. Para todos os outros tipos de dados, selecione **em camadas**. (**Em camadas** Olá predefinido.)
   3. Se tiver selecionado **em camadas** no passo 2, pode selecionar Olá **utilizar este volume para menos dados de arquivo acedidos com frequência** tooconfigure de caixa de verificação de um volume de arquivo.
   4. Introduza Olá **capacidade aprovisionada** para o volume em GB ou TB. Consulte [aprovisionado capacidade](#provisioned-capacity) para tamanhos máximos para cada tipo de dispositivo e de volume. Observe Olá **capacidade disponível** toodetermine quantidade de armazenamento está, efetivamente, disponível no seu dispositivo.
5. Clique Olá ícone de seta![Ícone de seta](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png). Se estiver a configurar um volume localmente afixado, verá Olá seguir a mensagem.
   
    ![Alterar a mensagem do tipo de Volume](./media/storsimple-manage-volumes-u2/LocalVolEx.png)
6. Clique em ícone de seta de Olá ![ícone de seta](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png)novamente toogo toohello **definições adicionais** página.
   
    ![Adicionar definições adicionais do Assistente de Volume](./media/storsimple-manage-volumes-u2/AddVolume2.png)<br>
7. Em **definições adicionais**, adicione um novo registo de controlo de acesso (ACR):
   
   1. Selecione um registo de controlo de acesso (ACR) Olá na lista pendente. Em alternativa, pode adicionar um novo ACR. ACRs determinar os anfitriões que podem aceder os volumes ao hello correspondente anfitrião IQN com que listados no registo de Olá. Se não especificar um ACR, verá Olá seguir a mensagem.
      
        ![Especifique o ACR](./media/storsimple-manage-volumes-u2/SpecifyACR.png)
   2. Recomendamos que selecione Olá **ativar uma cópia de segurança predefinido para este volume** caixa de verificação.
   3. Clique Olá ícone de verificação ![Ícone de verificação](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png) volume de Olá toocreate com Olá especificar as definições.

O novo volume está agora pronto toouse.

> [!NOTE]
> Se criar um volume afixado localmente e, em seguida, criar outra localmente afixado volume imediatamente posteriormente, as tarefas de criação do volume Olá são executados sequencialmente. tarefa de criação de volume Olá primeiro deve ser concluído antes de começar a tarefa de criação de volume Olá seguinte.
> 
> 

## <a name="modify-a-volume"></a>Modificar um volume
Modificar um volume quando precisar de tooexpand-lo ou alteração Olá anfitriões que acedem ao volume Olá.

> [!IMPORTANT]
> * Se modificar o tamanho do volume Olá no dispositivo Olá, o tamanho do volume Olá tem toobe alterado no anfitrião de Olá, bem como. 
> * passos do lado do anfitrião de Olá descritos aqui são para o Windows Server 2012 (2012R2). Procedimentos para Linux ou outros sistemas operativos de anfitrião será diferentes. Consulte as instruções de sistema operativo do anfitrião tooyour quando modificar o volume de Olá num anfitrião com outro sistema operativo. 
> 
> 

#### <a name="toomodify-a-volume"></a>toomodify um volume
1. No Olá **dispositivos** página, selecione o dispositivo de Olá, faça duplo clique e, em seguida, clique em Olá **contentores de Volume** separador.
2. Selecione um contentor de volume na lista de Olá e faça duplo clique volumes de Olá tooview associados ao contentor de Olá.
3. Selecione um volume e, em Olá parte inferior da página Olá, clique em **modificar**. inicia o Assistente de volume Olá modificar.
4. No Olá modificar Assistente de volume, em **definições básicas**, pode fazê-lo seguinte Olá:
   
   * Editar Olá **nome**.
   * Converter Olá **tipo de utilização** tootiered afixado localmente ou a toolocally em camadas afixado (consulte [alterar tipo de volume Olá](#change-the-volume-type) para obter mais informações).
   * Aumentar Olá **capacidade aprovisionada**. Olá **capacidade aprovisionada** só pode ser aumentada. Não é possível encolher o volume depois de criado.
5. Em **definições adicionais**, pode modificar Olá ACR, desde que o volume de Olá está offline. Se o volume de Olá estiver online, terá de tootake-lo primeiro offline. Consulte os passos toohello [colocar offline um volume](#take-a-volume-offline) toomodifying anterior Olá ACR.
   
   > [!NOTE]
   > Não é possível alterar Olá **ativar uma cópia de segurança predefinida** opção para volume Olá.
   > 
   > 
6. Guarde as alterações ao clicar em ícone de verificação Olá ![ícone de verificação](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png). Olá portal clássico do Azure irá apresentar uma mensagem de volume de atualização. Apresentará uma mensagem de êxito quando o volume de Olá foi atualizada com êxito.
7. Se está a expandir um volume, conclua Olá os seguintes passos no seu computador de anfitrião do Windows:
   
   1. Aceda demasiado**gestão de computadores** ->**gestão de discos**.
   2. Clique com botão direito **gestão de discos** e selecione **reanalisar discos**.
   3. Na lista de Olá de discos, selecione o volume de Olá que tenha atualizado, rato e, em seguida, selecione **Expandir Volume**. Assistente de expandir o Volume de Olá é iniciado. Clique em **Seguinte**.
   4. Conclua o Assistente de Olá, aceitando os valores predefinidos de Olá. Depois de concluído o Assistente de Olá, volume de Olá deve mostrar Olá maior tamanho.
      
      > [!NOTE]
      > Se expandir um volume afixado localmente e, em seguida, expanda outro localmente afixado volume imediatamente posteriormente, as tarefas de expansão de volume Olá são executados sequencialmente. tarefa de expansão de volume Olá primeiro deve ser concluído antes de começar a tarefa de expansão de volume Olá seguinte.
      > 
      > 

![Vídeo disponível](./media/storsimple-manage-volumes-u2/Video_icon.png) **Vídeo disponível**

toowatch um vídeo que demonstra como tooexpand um volume, clique em [aqui](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/).

## <a name="change-hello-volume-type"></a>Alterar o tipo de volume Olá
Pode alterar o tipo de volume Olá toolocally em camadas afixado ou a tootiered afixado localmente. No entanto, esta conversão não deve ser uma ocorrência frequente. Algumas razões para a conversão de um volume em camadas toolocally afixado são:

* Garantias locais sobre desempenho e disponibilidade de dados
* Eliminação de latências de nuvem e de problemas de conectividade de nuvem.

Normalmente, estes são pequenos volumes existentes que pretende que tooaccess com frequência. Um volume localmente afixado é totalmente aprovisionado quando é criado. Se estiver a converter um volume localmente afixado de tooa do volume em camadas, StorSimple verifica que tem espaço suficiente no seu dispositivo antes de iniciar a conversão Olá. Se tiver espaço suficiente, receberá um erro e operação Olá será cancelada. 

> [!NOTE]
> Antes de iniciar uma conversão de toolocally em camadas afixado, certifique-se de que considerar Olá requisitos de espaço em de outras cargas de trabalho. 
> 
> 

Pode querer toochange tooa um volume localmente afixado camadas volume se precisar de espaço adicional tooprovision outros volumes. Quando converter tootiered de volume localmente afixado de Olá, aumenta a capacidade disponível do Olá no dispositivo Olá ao tamanho Olá da capacidade de Olá lançada. Se os problemas de conectividade impedirem a conversão de Olá de um volume de Olá tipo local toohello camadas tipo, hello local volume plantas propriedades de um volume em camadas até concluir a conversão de Olá. Isto acontece porque alguns dados poderão ter spilled toohello nuvem. Estes dados spilled continuará toooccupy espaço local no dispositivo de Olá que não pode ser libertado até que a operação de Olá é reiniciada e concluída.

> [!NOTE]
> Converter um volume pode demorar algum tempo e não é possível cancelar uma conversão depois desta ser iniciada. volume de Olá permanece online durante a conversão de Olá e pode fazer cópias de segurança, mas não é possível expandir ou restaurar o volume de Olá enquanto decorre a conversão Olá.  
> 
> 

Conversão de um volume em camadas tooa afixado localmente pode afetar negativamente o desempenho do dispositivo. Além disso, Olá seguintes fatores pode aumentar o tempo de Olá demora a conversão de Olá toocomplete:

* Não há largura de banda suficiente.
* Não há nenhuma cópia de segurança atual.

toominimize Olá os efeitos que possam ter estes fatores:

* Reveja a políticas de limitação de largura de banda e certifique-se de que uma largura de banda Mbps dedicado 40 está disponível.
* Agendar a conversão de Olá durante as horas de ponta.
* Antes de iniciar a conversão de Olá, tire um instantâneo de nuvem.

Se estiver a converter vários volumes (suportar cargas de trabalho diferentes), em seguida, deve dê prioridade à conversão do volume de Olá, para que os volumes de prioridade superiores são convertidos primeiro. Por exemplo, deve converter volumes que alojam máquinas virtuais (VMs) ou volumes com cargas de trabalho do SQL Server antes de converter volumes com cargas de trabalho de partilha de ficheiros.

#### <a name="toochange-hello-volume-type"></a>tipo de volume de Olá toochange
1. No Olá **dispositivos** página, selecione o dispositivo de Olá, faça duplo clique e, em seguida, clique em Olá **contentores de Volume** separador.
2. Selecione um contentor de volume na lista de Olá e faça duplo clique volumes de Olá tooview associados ao contentor de Olá.
3. Selecione um volume e, em Olá parte inferior da página Olá, clique em **modificar**. inicia o Assistente de volume Olá modificar.
4. No Olá **definições básicas** página, altere o tipo de utilização de Olá selecionando o novo tipo de Olá de Olá **tipo de utilização** na lista pendente.
   
   * Se estiver a alterar o tipo de Olá demasiado**afixado localmente**, StorSimple irá verificar toosee se existir capacidade suficiente.
   * Se estiver a alterar o tipo de Olá demasiado**em camadas** e este volume será utilizado para dados de arquivo, selecione de Olá **utilizar este volume para menos dados de arquivo acedidos com frequência** caixa de verificação.
     
       ![Caixa de verificação do arquivo](./media/storsimple-manage-volumes-u2/ModifyTieredVolEx.png)
5. Clique em ícone de seta de Olá ![ícone de seta](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png) toogo toohello **definições adicionais** página. Se estiver a configurar um volume localmente afixado, hello mensagem seguinte é apresentada.
   
    ![Alterar a mensagem do tipo de Volume](./media/storsimple-manage-volumes-u2/ModifyLocalVolEx.png)
6. Clique Olá ícone de seta ![ícone de seta](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png) toocontinue novamente.
7. Clique Olá ícone de verificação ![Ícone de verificação](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png) processo de conversão de Olá toostart. Olá portal do Azure irá apresentar uma mensagem de volume de atualização. Apresentará uma mensagem de êxito quando o volume de Olá foi atualizada com êxito.

## <a name="take-a-volume-offline"></a>Colocar offline um volume
Poderá ser necessário tootake offline um volume quando estiver a planear toomodify-lo ou eliminá-lo. Quando um volume estiver offline, não está disponível para acesso de leitura e escrita. Terá de tootake Olá volume offline no anfitrião de Olá, bem como no dispositivo Olá. 

#### <a name="tootake-a-volume-offline"></a>tootake offline um volume
1. Certifique-se de que o volume de Olá em questão não está em utilização antes de colocar-offline.
2. Colocar o volume de Olá offline no anfitrião Olá primeiro. Isto elimina a qualquer potencial risco de danos nos dados no volume de Olá. Para obter passos específicos, consulte toohello instruções para o seu sistema operativo do anfitrião.
3. Depois de anfitrião de Olá estiver offline, demorar volume Olá no dispositivo de Olá offline efetuando Olá os seguintes passos:
   
   1. No Olá **dispositivos** página, selecione o dispositivo de Olá, faça duplo clique e, em seguida, clique em Olá **contentores de Volume** Olá separador **contentores de Volume** separador listas em formato tabular todos os contentores de volume do Olá que estão associados ao dispositivo Olá.
   2. Selecione um contentor de volume e clique na mesma lista de Olá toodisplay de todos os volumes de Olá dentro do contentor de Olá.
   3. Selecione um volume e clique em **colocar offline**.
   4. Quando lhe for pedida a confirmação, clique em **Sim**. volume de Olá deve agora estar offline.
      
      Depois de um volume estiver offline, Olá **colocar Online** opção fica disponível.

> [!NOTE]
> Olá **Colocar Offline** comando envia um volume de Olá do pedido toohello dispositivo tootake offline. Se anfitriões ainda estiver a utilizar o volume de Olá, isto resulta em ligações quebradas, mas colocar offline o volume de Olá não irá falhar. 
> 
> 

## <a name="delete-a-volume"></a>Eliminar um volume
> [!IMPORTANT]
> Pode eliminar um volume apenas se estiver offline.
> 
> 

Concluir Olá os seguintes passos toodelete um volume.

#### <a name="toodelete-a-volume"></a>toodelete um volume
1. No Olá **dispositivos** página, selecione o dispositivo de Olá, faça duplo clique e, em seguida, clique em Olá **contentores de Volume** separador.
2. Selecione o contentor de volume Olá que tem o volume de Olá pretende toodelete. Clique em Olá de tooaccess de contentor de volume Olá **Volumes** página.
3. Todos os volumes de Olá associados a este contentor são apresentados em formato tabular. Verificar o estado de Olá do volume de Olá pretende toodelete. Se o volume de Olá pretende toodelete não estiver offline, levá-los passos Olá primeiro, seguintes offline [colocar offline um volume](#take-a-volume-offline).
4. Depois de volume Olá estiver offline, clique em **eliminar** em Olá parte inferior da página Olá.
5. Quando lhe for pedida a confirmação, clique em **Sim**. volume de Olá agora serão eliminadas e Olá **Volumes** página mostrará a lista de Olá atualizado de volumes dentro do contentor de Olá.
   
   > [!NOTE]
   > Se eliminar um volume localmente afixado, espaço Olá disponível para novos volumes não pode ser atualizado imediatamente. Olá serviço StorSimple Manager atualiza periodicamente espaço local Olá disponível. Sugerimos que aguarde alguns minutos antes de tentar de novo volume do toocreate Olá.<br> Além disso, se eliminar um volume afixado localmente e, em seguida, elimine o outro localmente afixado volume imediatamente posteriormente, as tarefas de eliminação do volume Olá são executados sequencialmente. tarefa de eliminação de volume Olá primeiro deve ser concluído antes de começar a tarefa de eliminação de volume Olá seguinte.
   > 
   > 

## <a name="monitor-a-volume"></a>Monitorizar um volume
Monitorização de volume permite-lhe toocollect I/O-relacionadas com as estatísticas de um volume. A monitorização está ativada por predefinição para Olá primeiro 32 volumes que criar. Monitorização de volumes adicionais está desativada por predefinição. Monitorização de volumes clonados também é desativado por predefinição.

Execute Olá os seguintes passos tooenable ou desativar a monitorização para um volume.

#### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable ou desativar a monitorização volume
1. No Olá **dispositivos** página, selecione o dispositivo de Olá, faça duplo clique e, em seguida, clique em Olá **contentores de Volume** separador.
2. Selecione o contentor de volume Olá em que Olá reside volume e, em seguida, clique em Olá de tooaccess de contentor de volume Olá **Volumes** página.
3. Todos os volumes de Olá associados a este contentor estão listados na tabela de apresentação Olá. Clique e selecione o volume de Olá ou um clone de volume.
4. Na Olá parte inferior da página Olá, clique em **modificar**.
5. No Assistente para modificar o Volume de Olá, sob **definições básicas**, selecione **ativar** ou **desativar** de Olá **monitorização** na lista pendente.

## <a name="next-steps"></a>Passos seguintes
* Saiba como demasiado[clonar um volume StorSimple](storsimple-clone-volume.md).
* Saiba como demasiado[utilize Olá tooadminister de serviço StorSimple Manager, o dispositivo StorSimple](storsimple-manager-service-administration.md).

