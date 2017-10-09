---
title: "aaaClone volume de série 8000 do StorSimple | Microsoft Docs"
description: "Descreve Olá clone diferentes tipos e quando toouse-los e explica como pode utilizar um tooclone de conjunto de cópia de segurança num volume individual."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 070ac53e-7388-4c48-b8a5-8ed7f9108b2c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: f457625d2e3aa173f7ccf26984e1902a64e33b5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooclone-a-volume-update-2"></a>Utilizar Olá StorSimple Manager serviço tooclone um volume (atualização 2)
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a>Descrição geral
Olá serviço StorSimple Manager **catálogo de cópias de segurança** página apresenta todos os conjuntos de cópias de segurança Olá que são criados quando são efetuadas cópias de segurança manuais ou automáticas. Pode utilizar este toolist página todas as cópias de segurança Olá para uma política de cópia de segurança ou um volume, selecione ou eliminar as cópias de segurança, ou utilizar uma cópia de segurança toorestore ou clonar um volume.

![Página do catálogo de cópias de segurança](./media/storsimple-clone-volume-u2/backupCatalog.png)  

Este tutorial descreve como pode utilizar um tooclone de conjunto de cópia de segurança num volume individual. Também explica diferença Olá entre *transitório* e *permanente* clones.

> [!NOTE]
> Um volume localmente afixado será clonado como um volume em camadas. Se precisar de hello toobe clonado volume afixado localmente, pode converter o volume de tooa localmente afixado de clone Olá operação de clonagem Olá esteja concluída com êxito. Para obter informações sobre a conversão de um tooa volume em camadas localmente afixado volume, aceda demasiado[alterar tipo de volume Olá](storsimple-manage-volumes-u2.md#change-the-volume-type).
> 
> Se tentar tooconvert que um volume clonado da toolocally em camadas afixado imediatamente após a clonagem (quando ainda é um clone transitório), a conversão de Olá irá falhar com Olá seguir a mensagem de erro:
> 
> `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.` 
> 
> Este erro é recebido apenas se estão a clonagem em tooa noutro dispositivo. Pode converter com êxito Olá volume toolocally afixado se converter clone permanente do Olá clone transitório tooa primeiro. tooconvert Olá clone transitório tooa permanente clonar, tire um instantâneo de nuvem do mesmo.
> 
> 

## <a name="create-a-clone-of-a-volume"></a>Crie um clone de um volume
Pode criar um clone no Olá mesmo dispositivo, outro dispositivo ou mesmo uma máquina virtual através da utilização de uma local ou na nuvem instantâneo.

#### <a name="tooclone-a-volume"></a>tooclone um volume
1. Na página do serviço de Olá StorSimple Manager, clique em Olá **catálogo de cópia de segurança** separador e selecione um conjunto de cópia de segurança.
2. Expanda os volumes do Olá conjunto de cópia de segurança tooview Olá associado. Clique e selecione um volume do conjunto de cópias de segurança de Olá.
   
     ![Clonar um volume](./media/storsimple-clone-volume-u2/CloneVol.png) 
3. Clique em **Clone** toobegin clonagem de volume Olá selecionado.
4. No Assistente de clonagem de Volume Olá, sob **Especificar nome e localização**:
   
   1. Identifica um dispositivo de destino. Esta é a localização de olá onde será criada clone Olá. Pode escolher Olá mesmo dispositivo ou especifique outro dispositivo. Se escolher um volume associado a outros fornecedores de serviços em nuvem (não do Azure), Olá pendente listar para o dispositivo de destino Olá mostrará apenas a dispositivos físicos. Não é possível clonar um volume associado a outros fornecedores de serviços em nuvem num dispositivo virtual.
      
      > [!NOTE]
      > Certifique-se de que a capacidade de Olá necessária para o clone Olá é inferior à capacidade de Olá disponível no dispositivo de destino Olá.
      > 
      > 
   2. Especifique um nome exclusivo de volume para o clone. nome de Olá tem de conter entre 3 e 127 carateres. 
      
      > [!NOTE]
      > Olá **Clone Volume como** campo será **em camadas** , mesmo que a clonagem de um volume afixado localmente. Não é possível alterar esta definição; No entanto, se necessário hello toobe clonado volume localmente afixado bem, pode converter volume do Olá clone tooa afixado localmente depois de criar o clone de Olá com êxito. Para obter informações sobre a conversão de um tooa volume em camadas localmente afixado volume, aceda demasiado[alterar tipo de volume Olá](storsimple-manage-volumes-u2.md#change-the-volume-type).
      > 
      > 
      
        ![Assistente de clonagem 1](./media/storsimple-clone-volume-u2/clone1.png) 
   3. Clique Olá ícone de seta ![ícone de seta](./media/storsimple-clone-volume-u2/HCS_ArrowIcon.png) tooproceed toohello a página seguinte.
5. Em **especificar anfitriões que podem utilizar este volume**:
   
   1. Especifique um registo de controlo de acesso (ACR) para clone Olá. Pode adicionar um novo ACR ou escolher entre uma lista existente de Olá.
      
        ![Assistente de clonagem 2](./media/storsimple-clone-volume-u2/clone2.png) 
   2. Clique Olá ícone de verificação ![ícone de verificação](./media/storsimple-clone-volume-u2/HCS_CheckIcon.png)operação de Olá toocomplete.
6. Uma tarefa de clone será iniciada e será notificado quando clone Olá é criado com êxito. Clique em **ver tarefa** toomonitor a tarefa de clone de Olá no Olá **tarefas** página. Verá Olá seguir mensagem quando a tarefa de clone Olá for concluída:
   
    ![Mensagem de clone](./media/storsimple-clone-volume-u2/CloneMsg.png) 
7. Depois de Olá a conclusão da tarefa de clone:
   
   1. Aceda toohello **dispositivos** página e selecione Olá **contentores de Volume** separador. 
   2. Selecione o contentor de volume Olá que está associado ao volume de origem Olá que clonou. Na lista de Olá de volumes, deverá ver clone Olá que acabou de criar.

> [!NOTE]
> Monitorização e predefinido cópia de segurança automaticamente estão desativadas num volume clonado.
> 
> 

Um clone criado desta forma é um clone transitório. Para obter mais informações sobre os tipos de clone, consulte [transitório vs clones permanentes](#transient-vs-permanent-clones).

Este clone agora é um volume normal e todas as operações que é possível num volume estarão disponíveis para o clone Olá. Terá de tooconfigure este volume para quaisquer cópias de segurança.

## <a name="transient-vs-permanent-clones"></a>Transitório vs clones permanentes
Clones transitórios são criados apenas quando são clonagem tooa noutro dispositivo. Pode clonar um volume específico de um conjunto de cópia de segurança tooa diferentes de dispositivos geridos pelo Olá StorSimple Manager. clone transitório Olá será tem referências toohello dados no volume original Olá e utilizar essa tooread de dados e escrever localmente no dispositivo de destino Olá. 

Depois de tirar um instantâneo de nuvem de um clone transitório, clone resultante Olá será um *permanente* clone. Durante este processo, uma cópia dos dados de Olá é criada no cloud Olá Olá toocopy tempo que estes dados são determinados pelo tamanho de Olá dos dados de Olá e Olá latências do Azure (isto é uma cópia do Azure para o Azure). Este processo pode demorar dias tooweeks. clone transitório Olá torna-se um clone permanente desta forma e não tem quaisquer referências toohello original volume dados que foi clonado a partir do. 

## <a name="scenarios-for-transient-and-permanent-clones"></a>Cenários para clones transitórios e permanentes
Olá secções a seguir descreve situações de exemplo em que podem ser utilizados os clones transitórios e permanentes.

### <a name="item-level-recovery-with-a-transient-clone"></a>Recuperação ao nível do item com um clone transitório
É necessário toorecover um ficheiro de apresentação do Microsoft PowerPoint antigo de ano de um. O administrador de TI identifica Olá específico cópia de segurança desse período de tempo e, em seguida, filtros Olá volume. administrador de Olá, em seguida, clones volume Olá, localiza o ficheiro de Olá que está a procurar e fornece-tooyou. Neste cenário, é utilizado um clone transitório. 

![Vídeo disponível](./media/storsimple-clone-volume-u2/Video_icon.png) **Vídeo disponível**

toowatch um vídeo que demonstra como pode utilizar o clone Olá e restaurar as funcionalidades nos ficheiros de toorecover eliminado do StorSimple, clique em [aqui](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>Teste no ambiente de produção Olá com um clone permanente
É necessário tooverify um erro de teste no ambiente de produção Olá. Crie um clone de volume Olá no ambiente de produção Olá e, em seguida, tirar um instantâneo nuvem toocreate este clone um volume clonado independente. Neste cenário, é utilizado um clone permanente.  

## <a name="next-steps"></a>Passos seguintes
* Saiba como demasiado[restaurar um volume StorSimple a partir de um conjunto de cópia de segurança](storsimple-restore-from-backup-set-u2.md).
* Saiba como demasiado[utilize Olá tooadminister de serviço StorSimple Manager, o dispositivo StorSimple](storsimple-manager-service-administration.md).

