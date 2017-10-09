---
title: "Descrição geral do Gestor de dados do Azure StorSimple aaaMicrosoft | Microsoft Docs"
description: "Fornece uma descrição geral de Olá serviço StorSimple Manager de dados (pré-visualização privada)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 5d29f7d26be9f2b36857526bdea770d991cece6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a>Descrição geral do Gestor de dados do StorSimple (pré-visualização privada)

## <a name="overview"></a>Descrição geral

Microsoft Azure StorSimple é uma solução de armazenamento de nuvem híbrida endereços Olá complexidades de dados não estruturados normalmente associadas a partilhas de ficheiros. StorSimple utiliza armazenamento na nuvem como uma extensão de Olá solução no local e automaticamente as camadas de dados através de armazenamento do Olá no local e na nuvem. Integrado proteção de dados no local e na nuvem instantâneos, elimina a necessidade de Olá de uma infraestrutura de armazenamento sprawling. Arquivo e recuperação após desastre é também totalmente integrada com a nuvem Olá a agir como uma localização fora das instalações.

serviço de transformação de dados Olá que iremos introduzir neste documento, permite-lhe tooseamlessly acesso Olá StorSimple dados na nuvem de Olá. Este serviço fornece dados de tooextract APIs do StorSimple e apresente-tooother Azure serviços nos formatos que podem ser prontamente consumidos. formatos de Olá suportados nesta pré-visualização são blobs do Azure e os recursos de Media Services do Azure. Esta transformação permite-lhe tooeasily durante a transmissão dos serviços, tais como dados de toooperate Media Services do Azure, Azure HDInsight, do Azure Machine Learning e da Azure Search no dispositivo de no local de série 8000 do StorSimple.

Um diagrama de blocos de alto nível que ilustra isto é mostrado abaixo.

![Diagrama de alto nível](./media//storsimple-data-manager-overview/high-level-diagram.png)

Este documento explica como pode inscrever para uma versão de pré-visualização privada deste serviço. Também explica como pode utilizar aplicações de toowrite este serviço que utilizam dados StorSimple e outros serviços do Azure na nuvem de Olá.

## <a name="sign-up-for-data-manager-preview"></a>Inscrever-se para a pré-visualização do Gestor de dados
Antes de se inscrever no serviço do Gestor de dados de Olá, reveja Olá os seguintes pré-requisitos.

### <a name="prerequisites"></a>Pré-requisitos

Neste exercício parte do princípio de que tem
* Uma subscrição do Azure Active Directory.
* acesso tooa registado o dispositivo de série 8000 do StorSimple
* Olá todas as chaves associadas ao dispositivo de série de Olá 8000 do StorSimple.

### <a name="sign-up"></a>Inscrever-se

Olá StorSimple Manager de dados está em pré-visualização privada. Execute Olá toosign passos para uma versão de pré-visualização privada deste serviço os seguintes:

1.  Inicie sessão no Olá portal do Azure com a extensão do Gestor de dados do StorSimple Olá em: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager). Utilize o toolog de credenciais do Azure no.

2.  Clique em Olá  **+**  ícone toocreate um serviço. Clique em **armazenamento** e, em seguida, clique em **ver todos os** no painel de Olá que se abre.

    ![Ícone de Gestor de dados do StorSimple pesquisa](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. Pode ver o ícone de Gestor de dados do StorSimple Olá.

    ![Selecione o ícone do Gestor de dados do StorSimple](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. Clique em Gestor de dados do StorSimple ícone e, em seguida, clique em **criar**. Escolha a subscrição de Olá que pretende tooenable para pré-visualização privada Olá e, em seguida, clique em **inscrever-me!**

    ![Inscrever-me](./media/storsimple-data-manager-overview/sign-me-up.png)

5. Esta ação envia um pedido tooonboard. Iremos carregar, logo que possível. Depois de ativar a sua subscrição, pode criar um serviço StorSimple Manager de dados.

6. tooeasily aceder ao serviço StorSimple Manager de dados Olá, clique em Olá ícone de estrela toopin-tooyour Favoritos.

    ![Gestores de dados do StorSimple de acesso](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a>Passos seguintes

[Utilize a IU do Gestor de dados de StorSimple tootransform os dados](storsimple-data-manager-ui.md).
