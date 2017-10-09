---
title: "Atualizações aaaInstall numa matriz Virtual StorSimple | Microsoft Docs"
description: "Descreve como toouse Olá matriz Virtual StorSimple web IU tooapply atualizações através do método de portal e correção de Olá"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7f1b1e7d-04d0-4ca2-9dbb-77077ff19bb9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/07/2016
ms.author: alkohli
ms.openlocfilehash: 10af0f52abb75a5b41562704194157f0d35710bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a>Instalar atualizações na sua matriz de Virtual StorSimple
## <a name="overview"></a>Descrição geral
Este artigo descreve Olá passos tooinstall necessárias atualizações na sua matriz Virtual StorSimple através da IU da web local Olá e via Olá portal clássico do Azure. É necessário tooapply software tookeep atualizações ou correções a matriz de Virtual StorSimple atualizado. 

Tenha em atenção que a instalar uma atualização ou correção reinicia o seu dispositivo. Dado que Olá matriz Virtual StorSimple é um dispositivo de nó único, qualquer e/s em curso é interrompido e período de indisponibilidade ocorre com o seu dispositivo. 

Antes de aplicar uma atualização, recomendamos que tome volumes Olá ou partilhas offline no Olá alojam primeiro e, em seguida, Olá dispositivo. Isto minimiza qualquer possibilidade de danos nos dados.

> [!IMPORTANT]
> Se estiver a executar a atualização 0.1 ou versões de software DG, tem de utilizar o método de correção Olá através de Olá local web IU tooinstall atualização 0.3. Se estiver a executar a atualização 0,2, recomendamos que instale as atualizações de Olá através de Olá portal clássico do Azure.
> 
> 

## <a name="use-hello-local-web-ui"></a>Utilize Olá local IU da web
Existem dois passos, ao utilizar a IU da web local Olá:

* Transferir a atualização de Olá ou da correção de Olá
* Instalar a atualização de Olá ou da correção de Olá

### <a name="download-hello-update-or-hello-hotfix"></a>Transferir a atualização de Olá ou da correção de Olá
Efetue Olá seguintes passos toodownload Olá atualização de software de Olá catálogo Microsoft Update.

#### <a name="toodownload-hello-update-or-hello-hotfix"></a>toodownload Olá Olá de atualização ou correção
1. Inicie o Internet Explorer e navegue demasiado[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Se esta for a primeira vez utilizando Olá catálogo Microsoft Update neste computador, clique em **instalar** quando pedido tooinstall hello do suplemento do catálogo Microsoft Update.
3. Na caixa de pesquisa de Olá de Olá catálogo Microsoft Update, introduza o número de Base de dados de conhecimento (KB) Olá de correção de Olá que pretende toodownload. Introduza **3182061** para atualização 0.3 e, em seguida, clique em **pesquisa**.
   
    Olá listagem de correção é apresentado, por exemplo, **StorSimple Virtual matriz atualização 0.3**.
   
    ![Catálogo de pesquisa](./media/storsimple-ova-install-update-01/download1.png)
4. Clique em **Adicionar**. atualização de Olá está adicionada toohello cesto.
5. Clique em **Ver Cesto**.
6. Clique em **Transferir**. Especifique ou **procurar** tooa localização local onde pretende Olá transfere tooappear. Olá as atualizações são transferidas toohello especificada a localização e colocada numa subpasta com o mesmo nome como atualização Olá de Olá. pasta de Olá também pode ser copiado tooa partilha de rede que seja acessível a partir do dispositivo Olá.
7. Abra Olá copiados pasta, deverá ver um ficheiro de pacote do Microsoft Update autónomo `WindowsTH-KB3011067-x64`. Este ficheiro é utilizado tooinstall Olá atualização ou correção.

### <a name="install-hello-update-or-hello-hotfix"></a>Instalar a atualização de Olá ou da correção de Olá
Instalação de atualização ou correção toohello anterior, certifique-se de que tem Olá atualização ou correção de Olá transferido localmente no seu anfitrião ou acessível através de uma partilha de rede. 

Utilizar atualizações de tooinstall este método num dispositivo com GA ou atualização 0.1 versões de software. Este procedimento assume inferior toocomplete de 2 minutos. Execute o seguinte Olá passos tooinstall Olá atualização ou correção.

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a>tooinstall Olá atualização ou correção de Olá
1. Olá local IU da web, aceda demasiado**manutenção** > **atualização de Software**.
   
    ![atualizar o dispositivo](./media/storsimple-ova-install-update-01/update1m.png)
2. No **caminho do ficheiro de atualização**, introduza o nome de ficheiro Olá para atualização Olá ou Olá correção. Também pode procurar ficheiro de instalação de atualização ou correção toohello se colocado numa partilha de rede. Clique em **Aplicar**.
   
    ![atualizar o dispositivo](./media/storsimple-ova-install-update-01/update2m.png)
3. É apresentado um aviso. Este é um dispositivo de nó único, depois de Olá atualização ser aplicada, Olá dispositivo for reiniciado e existe um período de indisponibilidade. Clique Olá ícone de verificação.
   
   ![atualizar o dispositivo](./media/storsimple-ova-install-update-01/update3m.png)
4. inicia a atualização de Olá. Depois do dispositivo de Olá foi atualizado com êxito, esta reiniciar. Olá IU local não está acessível desta duração.
   
    ![atualizar o dispositivo](./media/storsimple-ova-install-update-01/update5m.png)
5. Após a conclusão do reinício Olá, é direcionado toohello **sessão** página. tooverify que atualizou o software de dispositivos de Olá, no Olá local IU da web do, aceda demasiado**manutenção** > **atualização de Software**. Olá apresentada a versão de software deve estar **10.0.0.0.0.10288.0** para atualização 0.3.
   
   > [!NOTE]
   > Estamos a versões de software Olá de relatório de forma ligeiramente diferente na IU da web local Olá e Olá portal clássico do Azure. Por exemplo, Olá relatórios de IU da local web **10.0.0.0.0.10288** e Olá relatórios de portais clássicos do Azure **10.0.10288.0** para Olá mesma versão. 
   > 
   > 
   
    ![atualizar o dispositivo](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-hello-azure-classic-portal"></a>Utilizar Olá portal clássico do Azure
Se executar a atualização 0,2, recomendamos que instale atualizações através de Olá portal clássico do Azure. procedimento portal Olá requer Olá utilizador tooscan, transferir e, em seguida, instalar atualizações de Olá. Este procedimento assume toocomplete cerca de 7 minutos. Execute o seguinte Olá passos tooinstall Olá atualização ou correção.

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

Olá após a instalação estiver concluída (conforme indicado pelo Estado de tarefa a 100%), aceda demasiado**dispositivos > manutenção > as atualizações de Software**. versão do software Olá apresentado deve ser 10.0.10288.0.

![atualizar o dispositivo](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre [administrar a matriz de Virtual StorSimple](storsimple-ova-web-ui-admin.md).

