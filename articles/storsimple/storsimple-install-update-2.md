---
title: "aaaInstall atualização 2 no dispositivo StorSimple | Microsoft Docs"
description: "Explica como tooinstall atualização 2 do StorSimple 8000 série no seu dispositivo de série 8000 do StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8c8981df-75d9-4d19-b137-d6c6ba39dcfb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 33a0bea4358c944644563192f686af332d2ad7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-2-on-your-storsimple-device"></a>Instalar a atualização 2 no dispositivo StorSimple
## <a name="overview"></a>Descrição geral
Este tutorial explica como tooinstall atualizar 2 num dispositivo StorSimple com uma versão anterior do software através de Olá portal clássico do Azure. tutorial de Olá também inclui passos de Olá necessários para atualizar de Olá quando um gateway é configurado numa interface de rede que não sejam dados 0 de dispositivo do StorSimple Olá e que está a tentar tooupdate de uma versão do software de 1 anterior à atualização.

A atualização 2 inclui dispositivo as atualizações de software, atualizações de controladores de LSI e atualizações de firmware do disco. o software de dispositivos de Olá e atualizações de LSI atualizações não acontece e podem ser aplicadas através de Olá portal clássico do Azure. atualizações de firmware do disco Olá acontece atualizações e só podem ser aplicadas através da interface do Windows PowerShell Olá do dispositivo Olá.

> [!IMPORTANT]
> * Poderá não ver Update 2 imediatamente porque fazemos de uma implementação faseada de Olá atualizações. Análise de atualizações de alguns dias novamente como esta atualização irá tornar-se disponível em breve.
> * Um conjunto de pré-verificações de manuais e automáticas são efetuadas toohello antes de instalar toodetermine Olá dispositivo estado de funcionamento em termos de conectividade de rede e estado de hardware. Estas verificações prévias são efetuadas apenas se aplicar atualizações de Olá de Olá portal clássico do Azure.
> * Recomendamos que instale o software de Olá e Olá de atualizações de controladores através do portal clássico do Azure. Só deve passar interface do Windows PowerShell toohello do dispositivo Olá (tooinstall atualizações) se a verificação de pré-atualização gateway Olá falhar no portal de Olá. atualizações de Olá poderão demorar tooinstall 7 de 4 horas (incluindo Olá atualizações do Windows). as atualizações de modo de manutenção Olá tem de ser instaladas através da interface do Windows PowerShell Olá do dispositivo Olá. As atualizações de modo de manutenção acontece atualizações, estas resultará na indisponíveis para o seu dispositivo.
> * Se em execução hello opcional Snapshot Manager do StorSimple, certifique-se de que tiver atualizado o seu dispositivo de Olá do Snapshot Manager versão tooUpdate 2 tooupdating anterior.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-2-via-hello-azure-classic-portal"></a>Instalar a atualização 2 através de Olá portal clássico do Azure
Efetuar Olá tooupdate passos a seguir o dispositivo demasiado[Update 2](storsimple-update2-release-notes.md).

> [!NOTE]
> A atualização 2 permite Microsoft toopull diagnóstico informações adicionais do dispositivo Olá. Como resultado, quando a nossa equipa de operações identifica dispositivos que estão a ter problemas, iremos são melhor equipado toocollect informações do dispositivo Olá e diagnosticar problemas. Ao aceitar atualização 2, permite-nos tooprovide este suporte proativa.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Certifique-se de que o dispositivo está em execução **StorSimple 8000 série Update 2 (6.3.9600.17673)**. Olá **atualizado pela última vez data** também deverá ser modificado. Também verá que as atualizações de modo de manutenção estão disponíveis (esta mensagem continuar toobe apresentado em segurança too24 horas depois de instalar Olá atualizações).
   
   As atualizações de modo de manutenção são atualizações acontece resultam num período de indisponibilidade do dispositivo e só podem ser aplicadas através da interface do Windows PowerShell Olá do seu dispositivo. Em alguns casos quando estiver a executar 1.2 de atualização, o firmware do disco já pode ser atualizado, caso em que não precisa de tooinstall qualquer modo de manutenção de atualizações.
2. Transferir atualizações de modo de manutenção de Olá, utilizando os passos de Olá listados no [toodownload correções](#to-download-hotfixes) toosearch para e transferir KB3121899, que instala as atualizações de firmware do disco (hello outras atualizações já devem estar instaladas por agora).
3. Siga os passos de Olá apresentados na [instalar e certifique-se correções do modo de manutenção](#to-install-and-verify-maintenance-mode-hotfixes) atualizações de modo de manutenção de Olá tooinstall.

## <a name="install-update-2-as-a-hotfix"></a>Instalar a atualização 2 como uma correção
Utilize este procedimento se não efetuar verificação de gateway de Olá durante a tentativa de atualizações de Olá tooinstall através de Olá portal clássico do Azure. verificação de Olá falha à medida que tem um gateway atribuído tooa não-interface rede DATA 0 e o dispositivo está em execução um tooUpdate de anteriores de versão do software 1.

versões de software Olá que podem ser atualizadas utilizando o método de correção Olá são atualização 0.1, atualização 0,2 e atualização 0.3, atualização 1, atualização 1.1 e 1.2 de atualização. método de correção Olá envolve Olá seguintes três passos:

* Transferir Olá correções do Olá catálogo Microsoft Update.
* Instalar e certifique-se correções do Olá modo normal.
* Instalar e certifique-se a correção de modo de manutenção de Olá.

tooinstall Update 2 como uma correção, tem de transferir e instalar Olá seguintes correções:

| Ordem | KB | Descrição | Tipo de atualização |
| --- | --- | --- | --- |
| 1 |KB3121901 |Atualização de software |Normal |
| 2 |KB3121900 |Controlador de LSI |Normal |
| 3 |KB3080728 |Correção de Storport </br> Windows Server 2012 R2 |Normal |
| 4 |KB3090322 |Correção de spaceport </br> Windows Server 2012 R2 |Normal |
| 5 |KB3121899 |Firmware de disco |Manutenção |

> [!IMPORTANT]
> * Se o dispositivo estiver a executar a versão de lançamento (GA), entre em contacto com [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist com Olá atualizar.
> * Toobe de necessidades este procedimento apenas uma vez efetuada tooapply Update 2. Pode utilizar as atualizações subsequentes do Olá tooapply de portal clássico do Azure.
> * Cada instalação de correção pode demorar cerca de 20 minutos toocomplete. Hora de instalação total é too2 fechar horas.
> * Antes de utilizar este Olá tooapply do procedimento de atualização, certifique-se de que ambos os controladores de dispositivo estão online e todos os componentes de hardware de Olá estão em bom Estados.
> 
> 

Efetue Olá tooapply passos a seguir esta atualização como uma correção.

[!INCLUDE [storsimple-install-update2-hotfix](../../includes/storsimple-install-update2-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre Olá [versão de atualização 2](storsimple-update2-release-notes.md).

