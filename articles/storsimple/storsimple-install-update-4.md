---
title: aaaInstall Update 4 no dispositivo StorSimple | Microsoft Docs
description: "Explica como tooinstall StorSimple 8000 série Update 4 no seu dispositivo de série 8000 do StorSimple."
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
ms.date: 05/30/2017
ms.author: alkohli
ms.openlocfilehash: 62c0ae94afdbb1027d3075962afa04d49fd1f60a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-4-on-your-storsimple-device"></a>Instalar a atualização 4 no dispositivo StorSimple

## <a name="overview"></a>Descrição geral

Este tutorial explica como Olá, tooinstall Update 4 num dispositivo StorSimple com uma versão anterior do software através do portal clássico do Azure e utilizar o método de correção Olá. método de correção Olá é utilizado quando um gateway é configurado numa interface de rede que não sejam dados 0 de dispositivo do StorSimple Olá e que está a tentar tooupdate de uma versão do software de 1 anterior à atualização.

Atualização 4 inclui o software de dispositivos, USM firmware, LSI controladores e firmware, Storport e Spaceport, SO atualizações de segurança e um anfitrião de outras atualizações do SO.  o software de dispositivos de Olá, USM firmware, Spaceport, Storport e outras atualizações do SO são atualizações não acontece. as atualizações não acontece ou regular de Olá podem ser aplicadas através de Olá portal clássico do Azure ou através do método de correção Olá. atualizações de firmware do disco Olá acontece atualizações e só podem ser aplicadas através do método de correção Olá utilizando a interface do Windows PowerShell Olá do dispositivo Olá. 

> [!IMPORTANT]
> * Um conjunto de pré-verificações de manuais e automáticas são efetuadas toohello antes de instalar toodetermine Olá dispositivo estado de funcionamento em termos de conectividade de rede e estado de hardware. Estas verificações prévias são efetuadas apenas se aplicar atualizações de Olá de Olá portal clássico do Azure.
> * Recomendamos que instale o software de Olá e outras atualizações regulares através de Olá portal clássico do Azure. Só deve passar interface do Windows PowerShell toohello do dispositivo Olá (tooinstall atualizações) se a verificação de pré-atualização gateway Olá falhar no portal de Olá. Consoante a versão de Olá que está a atualizar, Olá atualizações poderão demorar 4 horas (ou superior) tooinstall. as atualizações de modo de manutenção Olá também tem de ser instaladas através da interface do Windows PowerShell Olá do dispositivo Olá. As atualizações de modo de manutenção acontece atualizações, estas resultará na indisponíveis para o seu dispositivo.
> * Se em execução hello opcional Snapshot Manager do StorSimple, certifique-se de que tiver atualizado o seu dispositivo de Olá do Snapshot Manager versão tooUpdate 4 tooupdating anterior.


[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-4-via-hello-azure-classic-portal"></a>Instalar a atualização 4 através de Olá portal clássico do Azure
Efetuar Olá tooupdate passos a seguir o dispositivo demasiado[Update 4](storsimple-update4-release-notes.md).

> [!NOTE]
> Se aplicar a atualização 2 ou posterior (incluindo 2.1 de atualização), a Microsoft será capaz de toopull adicionais as informações de diagnóstico dispositivo Olá. Como resultado, quando a nossa equipa de operações identifica dispositivos que estão a ter problemas, iremos são melhor equipado toocollect informações do dispositivo Olá e diagnosticar problemas. Ao aceitar atualização 2 ou posterior, permite-nos tooprovide este suporte proativa. 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

Certifique-se de que o dispositivo está em execução **StorSimple 8000 série atualização 4 (6.3.9600.17820)**. Olá **atualizado pela última vez data** também deverá ser modificado. 

* Agora verá que as atualizações de modo de manutenção Olá estão disponíveis (esta mensagem continuar toobe apresentado em segurança too24 horas depois de instalar Olá atualizações). As atualizações de modo de manutenção são atualizações acontece resultam num período de indisponibilidade do dispositivo e só podem ser aplicadas através da interface do Windows PowerShell Olá do seu dispositivo.
 
* Transferir atualizações de modo de manutenção de Olá, utilizando os passos de Olá listados no [toodownload correções](#to-download-hotfixes) toosearch para e transferir KB4011837, que instala as atualizações de firmware do disco (hello outras atualizações já devem estar instaladas por agora). Siga os passos de Olá apresentados na [instalar e certifique-se correções do modo de manutenção](#to-install-and-verify-maintenance-mode-hotfixes) atualizações de modo de manutenção de Olá tooinstall. 

## <a name="install-update-4-as-a-hotfix"></a>Instalar a atualização 4 como uma correção
Olá recomendado tooinstall método que Update 4 é através de Olá portal clássico do Azure.

Utilize este procedimento se não efetuar verificação de gateway de Olá durante a tentativa de atualizações de Olá tooinstall através de Olá portal clássico do Azure. verificação de Olá falha à medida que tem um gateway atribuído tooa não-interface rede DATA 0 e o dispositivo está em execução um tooUpdate de anteriores de versão do software 1.

versões de software Olá que podem ser atualizadas utilizando o método de correção Olá são:

* Atualização 0.1, 0,2, 0,3
* Atualizar 1, 1.1, 1.2
* Atualização 2, 2.1, 2.2
* Atualização 3, 3.1 


método de correção Olá envolve Olá seguintes três passos:

1. Transferir Olá correções do Olá catálogo Microsoft Update.
2. Instalar e certifique-se correções do Olá modo normal.
3. Instalar e certifique-se a correção de modo de manutenção de Olá.

#### <a name="download-updates-for-your-device"></a>Transferir atualizações para o seu dispositivo

Tem de transferir e instalar o seguinte Olá correções no Olá prescrita ordenar e Olá pastas sugeridas:

| Ordem | KB | Descrição | Tipo de atualização | Hora de instalação |Instalar na pasta|
| --- | --- | --- | --- | --- | --- |
| 1. |KB4011839 <br> (2 ficheiros) |Atualização de software do dispositivo <br> Atualização do agente de CiS/MDS |Normal <br></br>Não acontece |~ minutos de 25 |FirstOrderUpdate <br> _Instalar a atualização de software do dispositivo antes da atualização do agente Cis/MDS_|
| 2A. |KB4011841 <br> KB4011842 |Controlador de LSI e atualizações de firmware <br> Atualização de firmware USM (versão 3.38) |Normal <br></br>Não acontece |~ 3 h <br> (inclui 2A. + 2B. + 2 C.)|SecondOrderUpdate|
| 2B. |KB3139398, KB3108381 <br> KB3205400, KB3142030 <br> KB3197873, KB3192392  <br> KB3153704, KB3174644 <br> KB3139914  |Pacote de atualizações de segurança do SO |Normal <br></br>Não acontece |- |SecondOrderUpdate|
| 2 C. |KB3210083, KB3103616 <br> KB3146621, KB3121261 <br> KB3123538 |Pacote de atualizações do SO |Normal <br></br>Não acontece |- |SecondOrderUpdate|

Também poderá ser necessário tooinstall atualizações de firmware de disco em todas as atualizações de Olá mostradas na Olá tabelas precedentes. Pode verificar se precisar de Olá atualizações de firmware do disco através da execução Olá `Get-HcsFirmwareVersion` cmdlet. Se estiver a executar estas versões de firmware: `XMGJ`, `XGEG`, `KZ50`, `F6C2`, `VR08`, `N002`, `0106`, em seguida, não precisa de tooinstall estas atualizações.

| Ordem | KB | Descrição | Tipo de atualização | Hora de instalação | Instalar na pasta|
| --- | --- | --- | --- | --- | --- |
| 3. |KB4011837 |Firmware de disco |Manutenção <br></br>Acontece |~ 30 minutos | ThirdOrderUpdate |

<br></br>

> [!IMPORTANT]
> * Toobe de necessidades este procedimento apenas uma vez efetuada tooapply atualização 4. Pode utilizar as atualizações subsequentes do Olá tooapply de portal clássico do Azure.
> * Se atualizar a partir da atualização 3 ou 3.1, a hora de instalação total Olá é too4 fechar horas.
> * Antes de utilizar este Olá tooapply do procedimento de atualização, certifique-se de que tanto os controladores de dispositivo Olá estão online e todos os componentes de hardware de Olá estão em bom Estados.

Efetuar Olá toodownload passos a seguir e instalar correções Olá.

[!INCLUDE [storsimple-install-update4-hotfix](../../includes/storsimple-install-update4-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre Olá [versão de atualização 4](storsimple-update4-release-notes.md).

