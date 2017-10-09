---
title: aaaManage dispositivos com o Snapshot Manager do StorSimple | Microsoft Docs
description: "Descreve como toouse Olá Snapshot Manager do StorSimple MMC snap-in tooconnect e gerir dispositivos StorSimple."
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 966ecbe3-a7fa-4752-825f-6694dd949946
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 7a2a2ca830e4ea6eb4b01f2542958df3871c1700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooconnect-and-manage-storsimple-devices"></a>Utilize o Snapshot Manager do StorSimple tooconnect e gerir dispositivos StorSimple
## <a name="overview"></a>Descrição geral
Pode utilizar nós Olá Snapshot Manager do StorSimple **âmbito** tooverify painel importar dados do dispositivo StorSimple e atualizar os dispositivos de armazenamento ligado. Além disso, ao clicar em Olá **dispositivos** nós, pode ver uma lista de dispositivos ligados e as informações de estado correspondente no Olá **resultados** painel.

![Dispositivos ligados](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_connect_devices.png)

**Figura 1: Ligada do StorSimple Snapshot Manager do dispositivo** 

Dependendo do seu **vista** seleções, Olá **resultados** painel mostra Olá seguintes informações sobre cada dispositivo. (Para mais informações sobre como configurar uma vista, visite demasiado[menu Ver](storsimple-use-snapshot-manager.md#view-menu).

| Coluna de resultados | Descrição |
|:--- |:--- |
| Nome |nome de Olá do dispositivo de Olá como configurado na Olá portal clássico do Azure |
| Modelo |número de modelo de Olá do dispositivo Olá |
| Versão |versão de Olá do software de Olá instalado no dispositivo Olá |
| Estado |Se o dispositivo de Olá está disponível |
| Última sincronização |Data e hora quando o dispositivo de Olá última sincronização |
| Número de série |número de série de Olá para dispositivo Olá |

Se, faça duplo clique Olá **dispositivos** nó Olá **âmbito** painel, pode selecionar Olá seguintes ações:

* Adicionar ou substituir um dispositivo
* Ligar um dispositivo e certifique-se de importações
* Atualizar dispositivos ligados

Se clicar em Olá **dispositivos** nome de nó e, em seguida, contexto de um dispositivo no Olá **resultados** painel, pode selecionar Olá seguintes ações:

* Autenticar um dispositivo
* Ver detalhes do dispositivo
* Atualizar um dispositivo
* Eliminar uma configuração de dispositivo
* Alterar uma palavra-passe do dispositivo

> [!NOTE]
> Todas estas ações também estão disponíveis no Olá **ações** painel.


Este tutorial explica como toouse tooconnect Snapshot Manager do StorSimple e gerir dispositivos e executar Olá seguintes tarefas:

* Adicionar ou substituir um dispositivo
* Ligar um dispositivo e certifique-se de importações
* Atualizar dispositivos ligados
* Autenticar um dispositivo
* Ver detalhes do dispositivo
* Atualizar um dispositivo individual
* Eliminar uma configuração de dispositivo
* Alterar uma palavra-passe do dispositivo expirado
* Substituir um dispositivo com falhas

> [!NOTE]
> Para obter informações gerais sobre como utilizar a interface de Snapshot Manager do StorSimple Olá, visite demasiado[interface de utilizador do Snapshot Manager do StorSimple](storsimple-use-snapshot-manager.md).


## <a name="add-or-replace-a-device"></a>Adicionar ou substituir um dispositivo
Utilizar Olá seguir o procedimento tooadd ou substituir um dispositivo StorSimple.

#### <a name="tooadd-or-replace-a-device"></a>tooadd ou substituir um dispositivo
1. Clique em Olá ícone de ambiente de trabalho toostart Snapshot Manager do StorSimple.
2. No Olá **âmbito** painel, contexto Olá **dispositivos** nó e, em seguida, clique em **configurar um dispositivo**. Olá **configurar um dispositivo** é apresentada a caixa de diálogo.
   
    ![Configurar um dispositivo StorSimple](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_config_device.png) 
3. No Olá **dispositivo** caixa pendente, selecione Olá endereço IP dispositivo Olá ou o dispositivo virtual. 
4. No Olá **palavra-passe** caixa de texto, escrever Olá Snapshot Manager do StorSimple palavra-passe que criou para o dispositivo de Olá no Olá portal clássico do Azure. Clique em **OK**. Snapshot Manager do StorSimple procuram dispositivos de Olá que identificou. 
   
   * Se o dispositivo de Olá estiver disponível, o Snapshot Manager do StorSimple adiciona uma ligação.
   * Se o dispositivo Olá estiver indisponível por qualquer motivo, o Snapshot Manager do StorSimple devolve uma mensagem de erro. Clique em **OK** tooclose Olá mensagem de erro e, em seguida, clique em **Cancelar** tooclose Olá **configurar um dispositivo** caixa de diálogo.

## <a name="connect-a-device-and-verify-imports"></a>Ligar um dispositivo e certifique-se de importações
Utilizar Olá seguir o procedimento tooconnect um dispositivo StorSimple e certifique-se de que todos os grupos existentes de volume que associou cópias de segurança são importados.

#### <a name="tooconnect-a-device-and-verify-imports"></a>tooconnect um dispositivo e certifique-se de importações
1. tooconnect tooStorSimple um dispositivo Snapshot Manager, siga as instruções de Olá em Adicionar ou substituir um dispositivo. Quando estabelece ligação tooa dispositivo, o Snapshot Manager do StorSimple responde da seguinte forma:
   
   * Se o dispositivo Olá estiver indisponível por qualquer motivo, o Snapshot Manager do StorSimple devolve uma mensagem de erro. 
   
   * Se o dispositivo de Olá estiver disponível, o Snapshot Manager do StorSimple adiciona uma ligação. Quando selecionar o dispositivo de Olá, é apresentado no Olá **resultados** painel, e o campo de estado de Olá indica que o dispositivo Olá **disponível**. Snapshot Manager do StorSimple importa os grupos de volume configurados para dispositivo Olá, desde que os grupos de volume de Olá ter associados a cópias de segurança. Políticas de cópia de segurança não foram importadas. Grupos de volume que não dispõe de cópias de segurança associadas não foram importados.
2. Clique em Olá ícone de ambiente de trabalho toostart Snapshot Manager do StorSimple.
3. Contexto Olá superior nó Olá **âmbito** painel e, em seguida, clique em **alternar importações apresentar**.
   
    ![Apresentação de importações selecione Ativar/desativar](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Toggle_Imports_Display.png) 
4. Olá **alternar importações apresentar** aparece a caixa de diálogo, que mostra o estado de Olá de Olá importada para grupos de volume e cópias de segurança. Clique em **OK**.

Depois de cópias de segurança e de grupos de volume Olá importadas com êxito, pode utilizar o Snapshot Manager do StorSimple toomanage-las, apenas como iria gerir grupos de volume e cópias de segurança que criar e configurar com Snapshot Manager do StorSimple. 

## <a name="refresh-connected-devices"></a>Atualizar dispositivos ligados
Utilize Olá seguir o procedimento toosynchronize Olá ligado StorSimple dispositivos com o Snapshot Manager do StorSimple.

#### <a name="toorefresh-connected-devices"></a>toorefresh dispositivos ligados
1. Clique em Olá ícone de ambiente de trabalho toostart Snapshot Manager do StorSimple.
2. No Olá **âmbito** painel, faça duplo clique **dispositivos**e, em seguida, clique em **atualizar dispositivos**. Isto sincroniza Olá ligado dispositivos com o Snapshot Manager do StorSimple para que possa visualizar grupos de volume Olá e cópias de segurança, incluindo quaisquer adições recentes. 
   
    ![Atualizar dispositivos do StorSimple Olá](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Refresh_devices.png)

Olá **atualizar dispositivos** ação obtém novos grupos de volume e quaisquer cópias de segurança associadas de dispositivos ligados. Ao contrário Olá **reanalisar volumes** ação disponível para Olá **Volumes** nó, **atualizar dispositivos** não restaurar o registo de cópia de segurança de Olá.

## <a name="authenticate-a-device"></a>Autenticar um dispositivo
Utilize Olá seguir o procedimento tooauthenticate um dispositivo StorSimple com o Snapshot Manager do StorSimple.

#### <a name="tooauthenticate-a-device"></a>tooauthenticate um dispositivo
1. Clique em Olá ícone de ambiente de trabalho toostart Snapshot Manager do StorSimple.
2. No Olá **âmbito** painel, clique em **dispositivos**.
3. No Olá **resultados** painel, clique no nome de Olá do dispositivo de Olá e, em seguida, clique em **autenticar**.
4. Olá **autenticar** é apresentada a caixa de diálogo. Escreva a palavra-passe de dispositivo Olá e, em seguida, clique em **OK**.
   
    ![Caixa de diálogo de autenticação](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Authenticate.png) 

## <a name="view-device-details"></a>Ver detalhes do dispositivo
Utilize Olá os procedimento tooview Olá detalhes de um dispositivo StorSimple e, se necessário, ressincronizar dispositivo Olá com Snapshot Manager do StorSimple.

#### <a name="tooview-and-resynchronize-device-details"></a>tooview e ressincronize detalhes do dispositivo
1. Clique em Olá ícone de ambiente de trabalho toostart Snapshot Manager do StorSimple.
2. No Olá **âmbito** painel, clique em **dispositivos**.
3. No Olá **resultados** painel, clique no nome de Olá do dispositivo de Olá e, em seguida, clique em **detalhes**.

4. Olá **detalhes do dispositivo** é apresentada a caixa de diálogo. Esta caixa apresenta o nome de Olá, modelo, versão, número de série, estado, destino iSCSI nome qualificado (IQN) e última sincronização data e a hora.

* Clique em **ressincronizar** dispositivo de Olá toosynchronize.
* Clique em **OK** ou **Cancelar** caixa de diálogo de Olá tooclose.
  
  ![Detalhes do dispositivo](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Device_details.png) 

## <a name="refresh-an-individual-device"></a>Atualizar um dispositivo individual
Utilize Olá seguir o procedimento tooresynchronize um dispositivo StorSimple individual com Snapshot Manager do StorSimple.

#### <a name="toorefresh-a-device"></a>toorefresh um dispositivo
1. Clique em Olá ícone de ambiente de trabalho toostart Snapshot Manager do StorSimple. 
2. No Olá **âmbito** painel, clique em **dispositivos**. 
3. No Olá **resultados** painel, clique no nome de Olá do dispositivo de Olá e, em seguida, clique em **atualizar dispositivo**. Sincroniza dispositivo Olá com Snapshot Manager do StorSimple.

## <a name="delete-a-device-configuration"></a>Eliminar uma configuração de dispositivo
Utilize Olá seguir o procedimento toodelete uma configuração de dispositivo StorSimple individuais do Snapshot Manager do StorSimple.

#### <a name="toodelete-a-device-configuration"></a>toodelete uma configuração de dispositivo
1. Clique em Olá ícone de ambiente de trabalho toostart Snapshot Manager do StorSimple.
2. No Olá **âmbito** painel, clique em **dispositivos**. 
3. No Olá **resultados** painel, clique no nome de Olá do dispositivo de Olá e, em seguida, clique em **eliminar**. 
4. Olá seguir a mensagem é apresentada. Clique em **Sim** toodelete Olá configuração ou clique em **não** eliminação de Olá toocancel.
   
    ![Eliminar a configuração de dispositivo](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_DeleteDevice.png)

## <a name="change-an-expired-device-password"></a>Alterar uma palavra-passe do dispositivo expirado
Tem de introduzir uma palavra-passe tooauthenticate um dispositivo StorSimple com o Snapshot Manager do StorSimple. Configurar esta palavra-passe quando utilizar tooset de interface do Windows PowerShell Olá segurança dispositivo Olá. No entanto, a palavra-passe de Olá pode expirar. Se isto acontecer, pode utilizar a palavra-passe de Olá do Olá toochange de portal clássico do Azure. Em seguida, porque o dispositivo de Olá configurado no Snapshot Manager do StorSimple antes de palavra-passe de Olá expirado, tem de autenticar novamente dispositivo Olá no Snapshot Manager do StorSimple.

#### <a name="toochange-hello-expired-password"></a>Olá toochange expirada palavra-passe
1. No portal clássico do Azure Olá, inicie o serviço do StorSimple Manager Olá.
2. Clique em **dispositivos** > **configurar** para dispositivo Olá.
3. Desloque para baixo toohello secção Snapshot Manager do StorSimple. Introduza uma palavra-passe é de 14 a 15 carateres. Certifique-se de que essa palavra-passe de Olá contiver uma combinação de carateres em maiúsculas, minúsculas, numérico e especiais.
4. Volte a introduzir Olá palavra-passe tooconfirm-lo.
5. Clique em **guardar** em Olá parte inferior da página Olá.

#### <a name="toore-authenticate-hello-device"></a>toore-autenticar Olá dispositivo
1. Inicie o Snapshot Manager do StorSimple.
2. No Olá **âmbito** painel, clique em **dispositivos**. É apresentada uma lista de dispositivos configurados no Olá **resultados** painel.
3. Selecione o dispositivo de Olá, rato e, em seguida, clique em **autenticar**.
4. No Olá **autenticar** janela, introduza a nova palavra-passe Olá.
5. Selecione o dispositivo de Olá, rato e selecione **atualizar dispositivo**. Sincroniza dispositivo Olá com Snapshot Manager do StorSimple.

## <a name="replace-a-failed-device"></a>Substituir um dispositivo com falhas
Se um dispositivo StorSimple falha e é substituído por um dispositivo de modo de espera (ativação pós-falha), Olá utilize os seguintes passos tooconnect toohello novo dispositivo e ver Olá cópias de segurança associadas.

#### <a name="tooconnect-tooa-new-device-after-failover"></a>tooconnect tooa novo dispositivo após a ativação pós-falha
1. Reconfigure Olá iSCSI ligação toohello novo dispositivo. Para obter instruções, aceda demasiado "passo 7: montar, inicializar e formatar um volume" no [implementar o dispositivo StorSimple no local](storsimple-8000-deployment-walkthrough-u2.md).

> [!NOTE]
> Se o dispositivo StorSimple novo Olá tem hello mesmo endereço IP que Olá antigo, poderá estar tooconnect capaz de configuração da antiga Olá.


1. Pare Olá StorSimple serviço de gestão da Microsoft:
   
   1. Inicie o Gestor de servidor.
   2. No Olá Dashboard do Gestor de servidores, no Olá **ferramentas** menu, selecione **serviços**.
   3. No Olá **serviços** janela, selecione de Olá **serviço de gestão da Microsoft StorSimple**.
   4. No Olá com o botão direito painel, em **serviço de gestão da Microsoft StorSimple**, clique em **parar o serviço de Olá**.
2. Remova dispositivo antigo do Olá configuração informações toohello relacionados:
   
   1. No Explorador de ficheiros, navegue tooC:\ProgramData\Microsoft\StorSimple\BACatalog.
   2. Elimine Olá ficheiros na pasta de BACatalog Olá.
3. Reinicie Olá StorSimple serviço de gestão da Microsoft:
   
   1. No Olá Dashboard do Gestor de servidores, no Olá **ferramentas** menu, selecione **serviços**.
   2. No Olá **serviços** janela, selecione de Olá **serviço de gestão da Microsoft StorSimple**.
   3. No Olá com o botão direito painel, em **serviço de gestão da Microsoft StorSimple**, clique em **Reiniciar serviço Olá**.
4. Inicie o Snapshot Manager do StorSimple.
5. tooconfigure Olá novo dispositivo StorSimple, Olá concluir os passos no passo 2: ligar um dispositivo StorSimple no [implementar Snapshot Manager do StorSimple](storsimple-snapshot-manager-deployment.md).
6. Nó de nível superior de Olá de contexto no Olá **âmbito** painel (Snapshot Manager do StorSimple no exemplo de Olá) e, em seguida, clique em **alternar importações apresentar**. 
7. É apresentada uma mensagem quando Olá importada grupos de volume e cópias de segurança são visíveis no Snapshot Manager do StorSimple. Clique em **OK**.

## <a name="next-steps"></a>Passos seguintes
* Saiba como demasiado[utilizar Snapshot Manager do StorSimple tooadminister solução StorSimple](storsimple-snapshot-manager-admin.md).
* Saiba como demasiado[utilizar tooview Snapshot Manager do StorSimple e gerir volumes](storsimple-snapshot-manager-manage-volumes.md).

