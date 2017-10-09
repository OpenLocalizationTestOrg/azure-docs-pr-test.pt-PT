---
title: "aaaStorSimple administração de serviço do Gestor de dispositivos | Microsoft Docs"
description: "Saiba como toomanage o dispositivo StorSimple utilizando Olá serviço Gestor de dispositivos do StorSimple no Olá portal do Azure."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: alkohli
ms.openlocfilehash: d73dc32bd39b2c832d5c4a5edda32a2e7f55a503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooadminister-your-storsimple-device"></a>Utilizar tooadminister de serviço do Gestor de dispositivos do StorSimple Olá o dispositivo StorSimple

## <a name="overview"></a>Descrição geral

Este artigo descreve a interface de serviço do Gestor de dispositivos do StorSimple Olá, incluindo como tooconnect tooit, Olá várias opções disponíveis e liga saída toohello específico fluxos de trabalho que podem ser efetuados através deste IU. Esta orientação é aplicável tooboth; o dispositivo físico StorSimple Olá e dispositivo de Olá de nuvem.

Depois de ler este artigo, irá aprender a:

* Ligar o serviço do Gestor de dispositivos de tooStorSimple
* Administrar o dispositivo StorSimple através de Olá serviço StorSimple Manager de dispositivo

## <a name="connect-toostorsimple-device-manager-service"></a>Ligar o serviço do Gestor de dispositivos de tooStorSimple

Olá serviço Gestor de dispositivos do StorSimple é executado no Microsoft Azure e liga toomultiple StorSimple dispositivos. Utilizar um portal central do Microsoft Azure em execução no toomanage browser estes dispositivos. tooconnect toohello serviço Gestor de dispositivos do StorSimple, Olá a seguir.

#### <a name="tooconnect-toohello-service"></a>serviço de toohello tooconnect
1. Navegue demasiado[https://portal.azure.com/](https://portal.azure.com/).
2. Utilizar as credenciais da conta Microsoft, inicie sessão no portal do Microsoft Azure toohello (localizado em Olá parte superior direita do painel de Olá).
3. Desloque para baixo Olá deixado navegação painel tooaccess Olá dispositivo do serviço StorSimple Manager.


## <a name="administer-storsimple-device-using-storsimple-device-manager-service"></a>Administrar o dispositivo StorSimple com o serviço do Gestor de dispositivos do StorSimple

Olá tabela seguinte mostra um resumo de todas as tarefas de gestão comuns do Olá e fluxos de trabalho complexos que podem ser efetuados dentro de Olá serviço Gestor de dispositivos do StorSimple da IU. Estas tarefas são organizadas com base nos painéis de IU Olá em que são iniciadas.

Para obter mais informações sobre cada fluxo de trabalho, clique em procedimento apropriado da Olá na tabela de Olá.

#### <a name="storsimple-device-manager-workflows"></a>Fluxos de trabalho do Gestor de dispositivos do StorSimple

| Se quiser toodo isto... | Utilize este procedimento. |
| --- | --- |
| Criar um serviço</br>Eliminar um serviço</br>Obter a chave de registo do serviço</br>Regenerar a chave de registo do serviço |[Implementar um serviço do Gestor de dispositivos do StorSimple](storsimple-8000-manage-service.md) |
| Ver registos de atividade de Olá |[Utilizar o serviço de Gestor de dispositivos do StorSimple Olá resumo](storsimple-8000-service-dashboard.md) |
| Alterar a chave de encriptação de dados de serviço Olá</br>Ver registos de operação de Olá |[Utilize o dashboard de serviço do Gestor de dispositivos do StorSimple Olá](storsimple-8000-service-dashboard.md) |
| Desativar um dispositivo</br>Eliminar um dispositivo |[Desativar ou eliminar um dispositivo](storsimple-8000-deactivate-and-delete-device.md) |
| Saiba mais sobre a ativação pós-falha de dispositivo e de recuperação de desastre</br>Dispositivo físico de tooa de ativação pós-falha</br>Dispositivo virtual de tooa de ativação pós-falha</br>Recuperação de desastre de continuidade de negócio (BCDR) |[Ativação pós-falha e recuperação após desastre para o dispositivo StorSimple](storsimple-8000-device-failover-disaster-recovery.md) |
| Lista as cópias de segurança para um volume</br>Selecione um conjunto de cópia de segurança</br>Eliminar um conjunto de cópia de segurança |[Gerir cópias de segurança](storsimple-8000-manage-backup-catalog.md) |
| Clonar um volume |[Clonar um volume](storsimple-8000-clone-volume-u2.md) |
| Restaurar um conjunto de cópia de segurança |[Restaurar um conjunto de cópia de segurança](storsimple-8000-restore-from-backup-set-u2.md) |
| Sobre as contas de armazenamento</br>Adicionar uma conta de armazenamento</br>Editar uma conta de armazenamento</br>Eliminar uma conta do Storage</br>Rotação da chave de contas do storage |[Gerir contas de armazenamento](storsimple-8000-manage-storage-accounts.md) |
| Sobre os modelos de largura de banda</br>Adicionar um modelo de largura de banda</br>Editar um modelo de largura de banda</br>Eliminar um modelo de largura de banda</br>Utilizar um modelo de largura de banda predefinido</br>Criar um modelo de largura de banda all-day que inicia no tempo especificado |[Gerir modelos de largura de banda](storsimple-8000-manage-bandwidth-templates.md) |
| Sobre os registos de controlo de acesso</br>Criar um registo de controlo de acesso</br>Editar um registo de controlo de acesso</br>Elimine um registo de controlo de acesso |[Gerir registos de controlo de acesso](storsimple-8000-manage-acrs.md) |
| Ver detalhes da tarefa</br>Cancelar uma tarefa |[Gerir tarefas](storsimple-8000-manage-jobs-u2.md) |
| Receber notificações de alerta</br>Gerir alertas</br>Rever os alertas |[Ver e gerir alertas do StorSimple](storsimple-8000-manage-alerts.md) |
| Criar gráficos de monitorização |[Monitorizar o dispositivo StorSimple](storsimple-monitor-device.md) |
| Adicionar um contentor de volume</br>Modificar um contentor de volume</br>Eliminar um contentor de volume |[Gerir contentores de volumes](storsimple-8000-manage-volume-containers.md) |
| Adicionar um volume</br>Modificar um volume</br>Colocar offline um volume</br>Eliminar um volume</br>Monitorizar um volume |[Gerir volumes](storsimple-8000-manage-volumes-u2.md) |
| Modificar as definições do dispositivo</br>Modificar as definições de hora</br>Modificar as definições de DNS.md</br>Configurar as interfaces de rede |[Modificar configuração de dispositivo para o dispositivo StorSimple](storsimple-8000-modify-device-config.md) |
| Ver definições de proxy web |[Configurar o proxy web para o seu dispositivo](storsimple-8000-configure-web-proxy.md) |
| Modifique a palavra-passe de administrador do dispositivo</br>Modifique a palavra-passe do Snapshot Manager do StorSimple |[Alterar as palavras-passe do StorSimple](storsimple-8000-change-passwords.md) |
| Configurar a gestão remota |[Ligar remotamente o dispositivo StorSimple tooyour](storsimple-8000-remote-connect.md) |
| Configurar definições de alerta |[Ver e gerir alertas do StorSimple](storsimple-8000-manage-alerts.md) |
| Configurar o CHAP para o dispositivo StorSimple |[Configurar o CHAP para o dispositivo StorSimple](storsimple-configure-chap.md) |
| Adicionar uma política de cópias de segurança</br>Adicionar ou modificar uma agenda</br>Eliminar uma política de cópia de segurança</br>Efetuar uma cópia de segurança manual</br>Criar uma política de cópia de segurança personalizada com vários volumes e agendas |[Gerir políticas de cópia de segurança](storsimple-8000-manage-backup-policies-u2.md) |
| Parar os controladores de dispositivo</br>Reinicie os controladores de dispositivo</br>Encerrar os controladores de dispositivo</br>Repor as predefinições de toofactory de dispositivo</br>(Acima destinam-se apenas a dispositivos no local) |[Gerir o controlador de dispositivo do StorSimple](storsimple-8000-manage-device-controller.md) |
| Saiba mais sobre os componentes de hardware do StorSimple</br>Monitorizar o estado do hardware</br>(Acima destinam-se apenas a dispositivos no local) |[Componentes de hardware do monitor](storsimple-8000-monitor-hardware-status.md) |
| Criar um pacote de suporte |[Criar e gerir um pacote de suporte](storsimple-8000-contact-microsoft-support.md#start-a-support-session-in-windows-powershell-for-storsimple) |
| Instalar atualizações de software |[Atualizar o seu dispositivo](storsimple-update-device.md) |

## <a name="next-steps"></a>Passos seguintes

Se surgirem problemas com a operação diária de Olá do dispositivo StorSimple ou com qualquer um dos respetivos componentes de hardware, consulte:

* [Resolver problemas com a ferramenta de diagnóstico de Olá](storsimple-8000-diagnostics.md)
* [Utilizar monitorização LEDs indicador do StorSimple](storsimple-monitoring-indicators.md)

Se não conseguir resolver problemas de Olá e precisar de toocreate um pedido de serviço, consulte demasiado[contactar o suporte da Microsoft](storsimple-8000-contact-microsoft-support.md).

