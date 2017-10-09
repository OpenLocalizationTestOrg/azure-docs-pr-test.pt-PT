---
title: "aaaInstall 2.2 de atualização no dispositivo StorSimple | Microsoft Docs"
description: "Explica como tooinstall 2.2 de atualização de série de 8000 StorSimple no seu dispositivo de série 8000 do StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 047c7a4b-73d0-45ea-8d51-c54d71871392
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/02/2016
ms.author: alkohli
ms.openlocfilehash: cedb83ce42bc6bb81a4e43345da3f25b71036d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-22-on-your-storsimple-device"></a>Instalar a atualização 2.2 no dispositivo StorSimple
## <a name="overview"></a>Descrição geral
Este tutorial explica como Olá, tooinstall 2.2 de atualização num dispositivo StorSimple com uma versão anterior do software através do portal clássico do Azure e utilizar o método de correção Olá. método de correção Olá é utilizado quando um gateway é configurado numa interface de rede que não sejam dados 0 de dispositivo do StorSimple Olá e que está a tentar tooupdate de uma versão do software de 1 anterior à atualização.

Atualização 2.2 inclui o software de dispositivos, WMI e atualizações de iSCSI. Se atualizar da versão 2.1, atualização de software de dispositivo Olá só será necessário toobe aplicada. Se atualizar a partir de uma versão 2 do pré-atualização, também será necessário tooapply LSI controlador, Spaceport, Storport e atualizações de firmware do disco. Olá, software de dispositivos, WMI, iSCSI, LSI controlador, Spaceport e Storport correções atualizações não acontece e podem ser aplicadas através de Olá portal clássico do Azure. atualizações de firmware do disco Olá acontece atualizações e só podem ser aplicadas através da interface do Windows PowerShell Olá do dispositivo Olá. 

> [!IMPORTANT]
> * Um conjunto de pré-verificações de manuais e automáticas são efetuadas toohello antes de instalar toodetermine Olá dispositivo estado de funcionamento em termos de conectividade de rede e estado de hardware. Estas verificações prévias são efetuadas apenas se aplicar atualizações de Olá de Olá portal clássico do Azure.
> * Recomendamos que instale o software de Olá e Olá de atualizações de controladores através do portal clássico do Azure. Só deve passar interface do Windows PowerShell toohello do dispositivo Olá (tooinstall atualizações) se a verificação de pré-atualização gateway Olá falhar no portal de Olá. Consoante a versão de Olá que está a atualizar, Olá atualizações podem demorar horas 1.5 2.5 tooinstall. as atualizações de modo de manutenção Olá tem de ser instaladas através da interface do Windows PowerShell Olá do dispositivo Olá. As atualizações de modo de manutenção acontece atualizações, estas resultará na indisponíveis para o seu dispositivo.
> * Se em execução hello opcional Snapshot Manager do StorSimple, certifique-se de que tiver atualizado o seu dispositivo de Olá do Snapshot Manager versão tooUpdate 2.2 tooupdating anterior.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-22-via-hello-azure-classic-portal"></a>Instalar a atualização 2.2 através de Olá portal clássico do Azure
Efetuar Olá tooupdate passos a seguir o dispositivo demasiado[atualização 2.2](storsimple-update21-release-notes.md).

> [!NOTE]
> Se aplicar a atualização 2 ou posterior (incluindo 2.1 de atualização), a Microsoft será capaz de toopull adicionais as informações de diagnóstico dispositivo Olá. Como resultado, quando a nossa equipa de operações identifica dispositivos que estão a ter problemas, iremos são melhor equipado toocollect informações do dispositivo Olá e diagnosticar problemas. Ao aceitar atualização 2 ou posterior, permite-nos tooprovide este suporte proativa.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Certifique-se de que o dispositivo está em execução **StorSimple 8000 série atualização 2.2 (6.3.9600.17708)**. Olá **atualizado pela última vez data** também deverá ser modificado. 
   
   Se estão a atualizar a partir de um tooUpdate anterior da versão 2, também verá que as atualizações de modo de manutenção Olá estão disponíveis (esta mensagem continuar toobe apresentado em segurança too24 horas depois de instalar Olá atualizações).
   
   As atualizações de modo de manutenção são atualizações acontece resultam num período de indisponibilidade do dispositivo e só podem ser aplicadas através da interface do Windows PowerShell Olá do seu dispositivo. Em alguns casos quando estiver a executar 1.2 de atualização, o firmware do disco já pode ser atualizado, caso em que não precisa de tooinstall qualquer modo de manutenção de atualizações.
   
   Se estão a atualizar a partir da atualização 2, o dispositivo deve ser atualizado. Pode ignorar Olá restantes passos.
2. Transferir atualizações de modo de manutenção de Olá, utilizando os passos de Olá listados no [toodownload correções](#to-download-hotfixes) toosearch para e transferir KB3121899, que instala as atualizações de firmware do disco (hello outras atualizações já devem estar instaladas por agora).
3. Siga os passos de Olá apresentados na [instalar e certifique-se correções do modo de manutenção](#to-install-and-verify-maintenance-mode-hotfixes) atualizações de modo de manutenção de Olá tooinstall. 

## <a name="install-update-22-as-a-hotfix"></a>Instalar a atualização 2.2 como uma correção
Utilize este procedimento se não efetuar verificação de gateway de Olá durante a tentativa de atualizações de Olá tooinstall através de Olá portal clássico do Azure. verificação de Olá falha à medida que tem um gateway atribuído tooa não-interface rede DATA 0 e o dispositivo está em execução um tooUpdate de anteriores de versão do software 1.

versões de software Olá que podem ser atualizadas utilizando o método de correção Olá são:

* Atualização 0.1, 0,2, 0,3
* Atualizar 1, 1.1, 1.2
* Atualização 2, 2.1 

> [!IMPORTANT]
> * Se o dispositivo estiver a executar a versão de lançamento (GA), entre em contacto com [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist com Olá atualizar.
> 
> 

método de correção Olá envolve Olá seguintes três passos:

* Transferir Olá correções do Olá catálogo Microsoft Update.
* Instalar e certifique-se correções do Olá modo normal.
* Instalar e verifique a correção de modo de manutenção de Olá (apenas quando a atualização anterior à atualização de software 2).

#### <a name="download-updates-for-a-device-running-update-21-software"></a>Transferir atualizações para um dispositivo 2.1 de atualização de software em execução
**Se o dispositivo estiver em execução de atualização 2.1**, tem de transferir atualizações de software apenas dispositivos de Olá KB3179904. Instale apenas o ficheiro binário Olá precedido pela 'all-hcsmdssoftwareudpate'. Não instale Olá Cis e a atualização do agente MDS Olá precedido pela `all-cismdsagentupdatebundle`. Falha toodo, por isso, resultará num erro. Esta é uma atualização não acontece, e/s não serão interrompidos e dispositivo Olá não terão qualquer período de inatividade.

#### <a name="download-updates-for-a-device-running-update-2-software"></a>Transferir atualizações para um dispositivo com o software Update 2
**Se o dispositivo estiver a executar a atualização 2**, tem de transferir e instalar Olá correções no Olá prescrita ordem a seguir:

| Ordem | KB | Descrição | Tipo de atualização | Hora de instalação |
| --- | --- | --- | --- | --- |
| 1. |KB3179904 |Atualização de software &#42; |Normal <br></br>Não acontece |~ 45 minutos |
| 2. |KB3146621 |pacote de iSCSI |Normal <br></br>Não acontece |~ 20 minutos |
| 3. |KB3103616 |Pacote WMI |Normal <br></br>Não acontece |~ minutos de 12 |

 &#42;  *Tenha em atenção de que a atualização de software consiste em dois ficheiros binários: precedido de atualização de software do dispositivo com `all-hcsmdssoftwareupdate` Olá Cis e agente Mds precedido pela `all-cismdsagentupdatebundle`. a atualização de software Olá dispositivo tem de estar instalada antes de agente de Olá Cis e Mds. Também tem de reiniciar o controlador de Active Directory Olá através de Olá `Restart-HcsController` cmdlet depois de aplicar Olá Cis e atualização de agente do MDS (e antes de aplicar Olá restantes atualizações).* 

#### <a name="download-updates-for-a-device-running-pre-update-2-software"></a>Transferir atualizações para um dispositivo a executar o anterior à atualização software 2
**Se o seu dispositivo está a executar versões 0,2, 0,3, 1.0 e 1.1**, tem de transferir e instalar Olá LSI controladores e firmware atualizar Ademais toohello software, iSCSI e atualizações WMI. Esta atualização já está instalada se estiver a executar a atualização 1.2 ou 2. 

| Ordem | KB | Descrição | Tipo de atualização | Hora de instalação |
| --- | --- | --- | --- | --- |
| 4. |KB3121900 |Controlador de LSI e firmware |Normal <br></br>Não acontece |~ 20 minutos |

<br></br>
**Se o dispositivo estiver a executar versões 0,2, 0,3, 1.0, 1.1 e 1.2**, tem de transferir e instalar Olá Spaceport e correção de Storport Olá. Estes são instalados se estiverem a executar a atualização 2.

| Ordem | KB | Descrição | Tipo de atualização | Hora de instalação |
| --- | --- | --- | --- | --- |
| 5. |KB3090322 |Correção de spaceport </br> Windows Server 2012 R2 |Normal <br></br>Não acontece |~ 20 minutos |
| 6. |KB3080728 |Correção de Storport </br> Windows Server 2012 R2 |Normal <br></br>Não acontece |~ 20 minutos |

<br></br>
Também poderá ser necessário tooinstall atualizações de firmware de disco. Pode verificar se precisar de Olá atualizações de firmware do disco através da execução Olá `Get-HcsFirmwareVersion` cmdlet. Se estiver a executar estas versões de firmware: `XMGG`, `XGEG`, `KZ50`, `F6C2`, `VR08`, em seguida, não precisa de tooinstall estas atualizações.

| Ordem | KB | Descrição | Tipo de atualização | Hora de instalação |
| --- | --- | --- | --- | --- |
| 7. |KB3121899 |Firmware de disco |Manutenção <br></br>Acontece |~ 30 minutos |

<br></br>

> [!IMPORTANT]
> * Toobe de necessidades este procedimento apenas uma vez efetuada tooapply 2.2 de atualização. Pode utilizar as atualizações subsequentes do Olá tooapply de portal clássico do Azure.
> * Se a atualização a partir do Update 2, a hora de instalação total Olá é too1.5 fechar horas.
> * Antes de utilizar este Olá tooapply do procedimento de atualização, certifique-se de que tanto os controladores de dispositivo Olá estão online e todos os componentes de hardware de Olá estão em bom Estados.
> 
> 

Efetuar Olá toodownload passos a seguir e instalar correções Olá.

[!INCLUDE [storsimple-install-update21-hotfix](../../includes/storsimple-install-update21-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre Olá [versão 2.1 atualização](storsimple-update21-release-notes.md).

