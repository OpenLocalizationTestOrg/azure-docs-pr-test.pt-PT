---
title: "aaaClone um volume num série 8000 do StorSimple | Microsoft Docs"
description: "Descreve os tipos de clone diferentes Olá e a utilização e explica como pode utilizar um conjunto de cópia de segurança de tooclone um volume individuais num dispositivo série 8000 do StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: 4f7e1f62f17c7b2bd72820a00a5ab87b7e192332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-tooclone-a-volume"></a>Utilizar o serviço de Gestor de dispositivos do StorSimple Olá no tooclone do portal do Azure, um volume

## <a name="overview"></a>Descrição geral

Este tutorial descreve como pode utilizar um tooclone de conjunto de cópia de segurança num volume individual através de Olá **catálogo de cópia de segurança** painel. Também explica diferença Olá entre *transitório* e *permanente* clones. orientações de Olá neste tutorial aplica-se tooall Olá 8000 do StorSimple série dispositivo a executar a atualização 3 ou posterior.

Olá serviço StorSimple Manager de dispositivo **catálogo de cópia de segurança** painel apresenta todos os conjuntos de cópias de segurança Olá que são criados quando são efetuadas cópias de segurança manuais ou automáticas. Em seguida, pode selecionar um volume na tooclone conjunto de cópia de segurança.

 ![Lista de conjunto de cópia de segurança](./media/storsimple-8000-clone-volume-u2/bucatalog.png)

## <a name="considerations-for-cloning-a-volume"></a>Considerações para a clonagem de um volume

Considere Olá informações a seguir ao clonar um volume.

- Um clone comporta-se Olá mesma forma que um volume normal. Todas as operações que é possível num volume estão disponível para clone Olá.

- Monitorização e predefinido cópia de segurança automaticamente estão desativadas num volume clonado. Terá tooconfigure um volume clonado para quaisquer cópias de segurança.

- Um volume localmente afixado é clonado como um volume em camadas. Se precisar de hello toobe clonado volume afixado localmente, pode converter o volume de tooa localmente afixado de clone Olá operação de clonagem Olá esteja concluída com êxito. Para obter informações sobre a conversão de um tooa volume em camadas localmente afixado volume, aceda demasiado[alterar tipo de volume Olá](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).

- Se tentar tooconvert que um volume clonado da toolocally em camadas afixado imediatamente após a clonagem (quando ainda é um clone transitório), a conversão de Olá falha com Olá seguir a mensagem de erro:

    `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.`

    Este erro é recebido apenas se estão a clonagem em tooa noutro dispositivo. Pode converter com êxito Olá volume toolocally afixado se converter clone permanente do Olá clone transitório tooa primeiro. Tirar um instantâneo nuvem Olá clone transitório tooconvert-clone permanente tooa.

## <a name="create-a-clone-of-a-volume"></a>Crie um clone de um volume

Pode criar um clone no Olá mesmo dispositivo, outro dispositivo ou mesmo uma aplicação de nuvem através da utilização de uma local ou na nuvem instantâneo.

procedimento Olá abaixo descreve como toocreate um clone de Olá cópia de segurança catálogo.  Um clone de tooinitiate método alternativo é toogo demasiado**Volumes**, selecione um volume, em seguida, clique no menu de contexto de Olá tooinvoke e selecione **Clone**.

Efetue Olá seguintes passos toocreate um clone do volume de catálogo Olá de cópia de segurança.

#### <a name="tooclone-a-volume"></a>tooclone um volume

1. Aceda tooyour do serviço StorSimple Manager de dispositivo e, em seguida, clique em **catálogo de cópia de segurança**.

2. Selecione uma cópia de segurança definida da seguinte forma:
   
   1. Selecione Olá de dispositivo adequados.
   2. Na Olá na lista pendente, escolha política de cópia de segurança ou volume de Olá para cópia de segurança de Olá pretende tooselect.
   3. Especifique o intervalo de tempo de Olá.
   4. Clique em **aplicar** tooexecute esta consulta.

    Olá cópias de segurança associadas a política de cópia de segurança ou volume Olá selecionado devem aparecer na lista de Olá de conjuntos de cópia de segurança.
   
    ![Lista de conjunto de cópia de segurança](./media/storsimple-8000-clone-volume-u2/bucatalog.png)
     
3. Expanda os volumes do Olá conjunto de cópia de segurança tooview Olá associado. Estes volumes devem ser colocados offline no anfitrião de Olá e dispositivo antes de pode restaurá-las. Aceder aos volumes Olá Olá **Volumes** painel do dispositivo e, em seguida, Olá siga os passos em [colocar offline um volume](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake-las offline.
   
   > [!IMPORTANT]
   > Certifique-se de que seguiu volumes Olá offline no anfitrião de Olá em primeiro lugar, antes de colocar offline os volumes de Olá no dispositivo Olá. Se não efetuar volumes de Olá offline no anfitrião de Olá, pode, potencialmente, levar toodata danos.
   
4. Navegue back toohello **catálogo de cópia de segurança** e selecione um volume num conjunto de cópia de segurança. Clique com botão direito e, em seguida, no menu de contexto de Olá, selecione **Clone**.

   ![Lista de conjunto de cópia de segurança](./media/storsimple-8000-clone-volume-u2/clonevol3b.png) 

3. No Olá **Clone** painel, Olá os seguintes passos:
   
    1. Identifica um dispositivo de destino. Esta é a localização de olá onde será criada clone Olá. Pode escolher Olá mesmo dispositivo ou especifique outro dispositivo.

      > [!NOTE]
      > Certifique-se de que a capacidade de Olá necessária para o clone Olá é inferior à capacidade de Olá disponível no dispositivo de destino Olá.
       
    2. Especifique um nome exclusivo de volume para o clone. nome de Olá tem de conter entre 3 e 127 carateres.
      
        > [!NOTE]
        > Olá **Clone Volume como** campo será **em camadas** , mesmo que a clonagem de um volume afixado localmente. Não é possível alterar esta definição; No entanto, se necessário hello toobe clonado volume localmente afixado bem, pode converter volume do Olá clone tooa afixado localmente depois de criar o clone de Olá com êxito. Para obter informações sobre a conversão de um tooa volume em camadas localmente afixado volume, aceda demasiado[alterar tipo de volume Olá](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).
          
    3. Em **ligados a anfitriões**, especifique um registo de controlo de acesso (ACR) para clone Olá. Pode adicionar um novo ACR ou escolher entre uma lista existente de Olá. Olá ACR irá determinar os anfitriões que podem aceder a este clone.
      
        ![Lista de conjunto de cópia de segurança](./media/storsimple-8000-clone-volume-u2/clonevol3a.png) 

    4. Clique em **Clone** operação de Olá toocomplete.

4. Uma tarefa de clone é iniciada e será notificado quando clone Olá é criado com êxito. Clique em notificação da tarefa de Olá ou vá demasiado**tarefas** tarefa de clone do painel toomonitor Olá.

    ![Lista de conjunto de cópia de segurança](./media/storsimple-8000-clone-volume-u2/clonevol5.png)

7. Após a conclusão da tarefa de clone Olá, aceda tooyour dispositivo e, em seguida, clique em **Volumes**. Na lista de Olá de volumes, deverá ver clone Olá que acabou de ser criada no Olá mesmo contentor de volume que contém o volume de origem Olá.

    ![Lista de conjunto de cópia de segurança](./media/storsimple-8000-clone-volume-u2/clonevol6.png)

Um clone criado desta forma é um clone transitório. Para obter mais informações sobre os tipos de clone, consulte [transitório vs clones permanentes](#transient-vs-permanent-clones).


## <a name="transient-vs-permanent-clones"></a>Transitório vs clones permanentes
Clones transitórios são criados apenas quando clonar tooanother dispositivo. Pode clonar um volume específico de um conjunto de cópia de segurança tooa diferentes de dispositivos geridos pelo Olá Gestor de dispositivos do StorSimple. clone transitório Olá tem referências toohello dados no volume original Olá e utiliza essa tooread de dados e a escrita localmente no dispositivo de destino Olá.

Depois de tomar um instantâneo de nuvem de um clone transitório, clone resultante Olá é um *permanente* clone. Durante este processo, uma cópia dos dados de Olá é criada no cloud Olá Olá toocopy tempo que estes dados são determinados pelo tamanho de Olá dos dados de Olá e Olá latências do Azure (isto é uma cópia do Azure para o Azure). Este processo pode demorar dias tooweeks. clone transitório Olá torna-se de um clone permanente e não tem quaisquer referências toohello original volume dados que foi clonado a partir do.

## <a name="scenarios-for-transient-and-permanent-clones"></a>Cenários para clones transitórios e permanentes
Olá secções a seguir descreve situações de exemplo em que podem ser utilizados os clones transitórios e permanentes.

### <a name="item-level-recovery-with-a-transient-clone"></a>Recuperação ao nível do item com um clone transitório
É necessário toorecover um ficheiro de apresentação do Microsoft PowerPoint antigo de ano de um. O administrador de TI identifica cópia de segurança específicas do Olá de tempo e, em seguida, filtros Olá volume. administrador de Olá, em seguida, clones volume Olá, localiza o ficheiro de Olá que está a procurar e fornece-tooyou. Neste cenário, é utilizado um clone transitório.

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>Teste no ambiente de produção Olá com um clone permanente
É necessário tooverify um erro de teste no ambiente de produção Olá. Crie um clone de volume Olá no ambiente de produção Olá e, em seguida, tirar um instantâneo nuvem toocreate este clone um volume clonado independente. Neste cenário, é utilizado um clone permanente.

## <a name="next-steps"></a>Passos seguintes
* Saiba como demasiado[restaurar um volume StorSimple a partir de um conjunto de cópia de segurança](storsimple-8000-restore-from-backup-set-u2.md).
* Saiba como demasiado[utilize Olá tooadminister de serviço do Gestor de dispositivos do StorSimple o dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

