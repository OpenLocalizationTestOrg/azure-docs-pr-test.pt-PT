---
title: "Olá aaaDeploy serviço Gestor de dispositivos do StorSimple no Azure | Microsoft Docs"
description: "Explica como toocreate e delete hello do serviço StorSimple Manager de dispositivos no portal do Azure de Olá e descreve como toomanage Olá chave de registo do serviço."
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
ms.date: 07/13/2017
ms.author: alkohli
ms.openlocfilehash: b84a907d6b735c8fee7bdc51f9c0074857297d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-8000-series-devices"></a>Implementar o serviço do Gestor de dispositivos do StorSimple Olá para dispositivos de série 8000 do StorSimple

## <a name="overview"></a>Descrição geral

Olá serviço Gestor de dispositivos do StorSimple é executado no Microsoft Azure e liga toomultiple StorSimple dispositivos. Depois de criar serviço Olá, pode utilizar-toomanage todos os dispositivos de Olá que estão ligado toohello Gestor de dispositivos do StorSimple service partir de uma localização única, central, deste modo, minimizando o fardo administrativo.

Este tutorial descreve os passos de Olá necessários para a criação de Olá, eliminação, a migração do serviço de Olá e gestão de Olá da chave de registo do serviço de Olá. informações de Olá contidas neste artigo são aplicável apenas dispositivos das séries tooStorSimple 8000. Para obter mais informações sobre matrizes Virtual StorSimple, visite demasiado[implementar um serviço StorSimple Manager de dispositivo para a matriz de Virtual StorSimple](storsimple-virtual-array-manage-service.md).

## <a name="create-a-service"></a>Criar um serviço
toocreate um serviço do Gestor de dispositivos do StorSimple, terá de toohave:

* Uma subscrição com um Enterprise Agreement
* Uma conta de armazenamento do Microsoft Azure Active Directory
* Olá, as informações de faturação que são utilizadas para gestão de acesso

Apenas Olá subscrições com um Enterprise Agreement são permitidas. Subscrições do Microsoft Sponsorship que foram permitidas em Olá portal clássico do Azure não são suportadas no Olá portal do Azure. Verá Olá seguir a mensagem ao utilizar uma subscrição não suportada:

![Não é válida de subscrição](./media/storsimple-8000-manage-service/subscription-not-valid.jpg)

Também pode escolher toogenerate uma conta do storage predefinida quando cria Olá service.

Um único serviço pode gerir vários dispositivos. No entanto, um dispositivo não pode abranger vários serviços. Uma grande empresa pode ter vários toowork de instâncias de serviço com diferentes subscrições, as organizações ou até mesmo as localizações de implementação. 

> [!NOTE]
> Terá de instâncias separadas de dispositivos de série do Gestor de dispositivos do StorSimple serviço toomanage 8000 do StorSimple e matrizes Virtual StorSimple.

Efetue Olá os seguintes passos toocreate um serviço.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-8000-create-new-service.md)]


Para cada serviço do Gestor de dispositivos do StorSimple, existe Olá seguintes atributos:

* **Nome** – nome de Olá que foi atribuído o serviço de Gestor de dispositivos do StorSimple tooyour quando foi criado. **Não é possível alterar o nome do serviço Olá depois do serviço de Olá é criado. Isto também se aplica para outras entidades, tais como os dispositivos, volumes, contentores de volume e políticas de cópia de segurança que não não possível mudar o nome no portal do Azure de Olá.**
* **Estado** – Olá estado do serviço de Olá, que pode ser **Active Directory**, **criar**, ou **Online**.
* **Localização** – Olá localização geográfica na qual Olá StorSimple dispositivo será implementado.
* **Subscrição** – hello subscrição que está associada ao seu serviço de faturação.

## <a name="move-a-service-tooazure-portal"></a>Mover um portal de tooAzure de serviço
Série 8000 do StorSimple pode ser agora gerido em Olá portal do Azure. Se tiver um serviço toomanage Olá StorSimple os dispositivos já, recomendamos que mova o toohello serviço portal do Azure. Olá portal clássico do Azure para Olá serviço StorSimple Manager não está disponível após 30 de Setembro de 2017.

Olá opção toomigrate toohello portal do Azure está disponível em fases. Se não vir um portal de tooAzure toomigrate opção, mas pretende toomove e consultou impacto Olá da migração conforme documentado no Olá [considerações para transição](#considerations-for-transition), pode [submeter um pedido](https://aka.ms/ss8000-cx-signup).

### <a name="considerations-for-transition"></a>Considerações para transição

Reveja o impacto de Olá da migração toohello novo portal do Azure antes de mover o serviço de Olá.

#### <a name="before-you-transition"></a>Antes de transição

* O dispositivo está em execução atualização 3.0 ou posterior. Se o dispositivo estiver em execução uma versão mais antiga, instale as atualizações mais recentes do Olá. Para mais informações, visite demasiado[instalar a atualização 4](storsimple-8000-install-update-4.md). Se utilizar uma aplicação de nuvem do StorSimple (8010/8020), crie um novo dispositivo de nuvem com atualização 4.0. 

* Depois de serem transferidas toohello novo portal do Azure, não é possível utilizar Olá toomanage de portal clássico do Azure o dispositivo StorSimple.

* transição de Olá não acontece e não existe nenhum período de indisponibilidade para dispositivo Olá.

* Todos os gestores de dispositivo de StorSimple Olá em Olá especificado subscrição são transferidas.

#### <a name="during-hello-transition"></a>Durante a transição de Olá

* Não é possível gerir o seu dispositivo do portal de Olá.
* Operações como cópias de segurança em camadas e agendadas continuam toooccur.
* Não elimine Olá antigo gestores de dispositivo do StorSimple enquanto transição Olá está em curso.

#### <a name="after-hello-transition"></a>Após a transição de Olá

* Já não pode gerir os seus dispositivos a partir do portal clássico Olá.

* cmdlets do PowerShell de gestão de serviço do Azure (ASM) do Olá existentes não são suportados. Atualize Olá scripts toomanage os seus dispositivos através de Olá do Azure Resource Manager.

* A configuração do serviço e dispositivo são retidos. Todos os volumes e as cópias de segurança também são transferida toohello do portal do Azure.

### <a name="begin-transition"></a>Começar a transição

Efetue Olá tootransition passos a seguir a toohello serviço portal do Azure.

1. Aceda tooyour serviço StorSimple Manager no portal clássico Olá.

2. Verá uma notificação que informa-o de que serviço de Gestor de dispositivos do StorSimple Olá está agora disponível nos Olá portal do Azure. Tenha em atenção que no portal do Azure Olá, serviço Olá tooas referido serviço StorSimple Manager do dispositivo.

    ![Notificação de migração](./media/storsimple-8000-manage-service/service-transition1.jpg)

    1. Certifique-se de que reviu impacto completo do Olá da migração.
    2. Reveja a lista de Olá de gestores de dispositivo do StorSimple que serão movidos do portal clássico Olá.

3. Clique em **migrar**. transição de Olá começa e demora alguns minutos toocomplete.

Depois de concluída a transição de Olá, pode gerir os seus dispositivos através de Olá serviço Gestor de dispositivos do StorSimple no Olá portal do Azure.

No portal do Azure Olá, Olá apenas dispositivos StorSimple com atualização 3.0 e superior, são suportados. dispositivos de Olá que executam versões mais antigas têm suporte limitado. Olá seguir summrizes tabela as operações são suportadas no dispositivo Olá executar versios anterior tooUpdate 3.0, uma vez que migrou do Olá clássico toohello portal do Azure.

| Operação                                                                                                                       | Suportado      |
|---------------------------------------------------------------------------------------------------------------------------------|----------------|
| Registar um dispositivo                                                                                                               | Sim            |
| Configurar definições de dispositivos como geral, rede e segurança                                                                | Sim            |
| Procurar, transferir e instalar atualizações                                                                                             | Sim            |
| Desativar o dispositivo                                                                                                               | Sim            |
| Eliminar o dispositivo                                                                                                                   | Sim            |
| Criar, modificar e eliminar um contentor de volume                                                                                   | Não             |
| Criar, modificar e eliminar um volume                                                                                             | Não             |
| Criar, modificar e eliminar uma política de cópia de segurança                                                                                      | Não             |
| Efetuar uma cópia de segurança manual                                                                                                            | Não             |
| Efetuar uma cópia de segurança agendada                                                                                                         | Não aplicável |
| Restaurar a partir de um backupset                                                                                                        | Não             |
| Clonar o dispositivo de tooa executar a atualização 3.0 e posteriores <br> dispositivo de origem Olá está em execução tooUpdate anterior de versão 3.0.                                | Sim            |
| Clonar o dispositivo de tooa com versões anteriores tooUpdate 3.0                                                                          | Não             |
| Ativação pós-falha como dispositivo de origem <br> (a partir de um dispositivo com a versão anterior tooUpdate 3.0 tooa dispositivo a executar a atualização 3.0 e posterior)                                                               | Sim            |
| Ativação pós-falha como dispositivo de destino <br> (o dispositivo tooa executar tooUpdate anterior da versão do software 3.0)                                                                                   | Não             |
| Limpar um alerta                                                                                                                  | Sim            |
| Ver as políticas de cópia de segurança, o catálogo de cópias de segurança, volumes, contentores de volume, gráficos de monitorização, tarefas e alertas criados no portal clássico | Sim            |
| Ativar e desativar os controladores de dispositivo                                                                                              | Sim            |


## <a name="delete-a-service"></a>Eliminar um serviço

Antes de eliminar um serviço, certifique-se de que não existem dispositivos ligados a estiver a utilizar. Se o serviço de Olá está a ser utilizado, desative dispositivos Olá ligado. Olá desativar operação irá sever ligação Olá entre dispositivos de Olá e o serviço de Olá, mas manter os dados do dispositivo Olá na nuvem de Olá.

> [!IMPORTANT]
> Depois de um serviço é eliminado, não é possível reverter a operação de Olá. Qualquer dispositivo que estava a utilizar o serviço de Olá tem toobe reposição toofactory predefinições antes de poder ser utilizada com outro serviço. Neste cenário, os dados locais Olá no dispositivo Olá, bem como a configuração de Olá, é perdido.

Efetue Olá os seguintes passos toodelete um serviço.

### <a name="toodelete-a-service"></a>toodelete um serviço

1. Pesquisa para o serviço de Olá pretende toodelete. Clique em **recursos** ícone e, em seguida, entrada Olá toosearch termos adequado. Nos resultados de pesquisa de Olá, clique em Olá serviço toodelete.

    ![Toodelete do serviço de pesquisa](./media/storsimple-8000-manage-service/deletessdevman1.png)

2. Isto leva-o painel de serviço do Gestor de dispositivos do StorSimple toohello. Clique em **Eliminar**.

    ![Eliminar o serviço](./media/storsimple-8000-manage-service/deletessdevman2.png)

3. Clique em **Sim** na notificação de confirmação de Olá. Pode demorar alguns minutos para Olá serviço toobe eliminado.

    ![Confirmar eliminação](./media/storsimple-8000-manage-service/deletessdevman3.png)

## <a name="get-hello-service-registration-key"></a>Obter a chave de registo do serviço de Olá

Depois de ter criado com êxito um serviço, terá de tooregister serviço Olá no dispositivo StorSimple. tooregister primeiro dispositivo StorSimple, será necessário Olá chave de registo do serviço. tooregister dispositivos adicionais com um serviço StorSimple, terá de chave de registo Olá e Olá serviço chave de encriptação dados (que é gerado no primeiro dispositivo de Olá durante o registo). Para obter mais informações sobre a chave de encriptação de dados de serviço Olá, consulte [segurança do StorSimple](storsimple-8000-security.md). Pode obter a chave de registo Olá acedendo **chaves** no painel do Gestor de dispositivos do StorSimple.

Efetue Olá chave de registo de serviço de Olá tooget passos a seguir.

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

Manter a chave de registo do serviço de Olá numa localização segura. Terá esta chave, bem como chave de encriptação de dados de serviço Olá, tooregister dispositivos adicionais com este serviço. Depois de obter a chave de registo do serviço de Olá, tem de configurar o dispositivo através do Olá do Windows PowerShell para StorSimple interface.

Para obter detalhes sobre como toouse esta chave, consulte de registo [passo 3: configurar e registar o dispositivo de Olá através do Windows PowerShell para StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

## <a name="regenerate-hello-service-registration-key"></a>Regenerar a chave de registo do serviço de Olá
É necessário tooregenerate uma chave de registo do serviço se for necessário tooperform rotação da chave ou se a lista de Olá dos administradores de serviço foi alterada. Quando voltar a gerar chave Olá, a nova chave de Olá é utilizado apenas para registar dispositivos subsequentes. dispositivos de Olá que já foram registados não são afetados por este processo.

Efetue Olá os seguintes passos tooregenerate uma chave de registo do serviço.

### <a name="tooregenerate-hello-service-registration-key"></a>chave de registo do serviço de Olá tooregenerate
1. No Olá **Gestor de dispositivos do StorSimple** painel, vá demasiado**gestão &gt;**  **chaves**.
    
    ![Painel de chaves](./media/storsimple-8000-manage-service/regenregkey2.png)

2. No Olá **chaves** painel, clique em **regenerar**.

    ![Clique em voltar a gerar](./media/storsimple-8000-manage-service/regenregkey3.png)
3. No Olá **chave de registo do serviço de voltar a gerar** painel, reveja Olá necessária ação ao hello chaves são regeneradas. Todos os dispositivos subsequentes Olá registados com este serviço utilizam nova chave de registo Olá. Clique em **regenerar** tooconfirm. Será notificado depois de concluída a regeneração de Olá.

    ![Confirmar voltar a gerar](./media/storsimple-8000-manage-service/regenregkey4.png)

4. Será apresentada uma nova chave de registo do serviço.

5. Copie esta chave e guarde-a para registar os novos dispositivos com este serviço.



## <a name="change-hello-service-data-encryption-key"></a>Alterar a chave de encriptação de dados de serviço Olá
Chaves de encriptação de dados de serviço são dados de cliente confidencial tooencrypt utilizada, tais como credenciais de conta de armazenamento, que são enviados do dispositivo StorSimple Manager serviço toohello StorSimple. Terá de toochange estas chaves periodicamente se a organização de TI tem uma política de rotação da chave em dispositivos de armazenamento Olá. Olá processo de alteração de chave pode ser ligeiramente diferente consoante esteja há um único ou vários dispositivos geridos pelo Olá serviço StorSimple Manager. Para mais informações, visite demasiado[StorSimple segurança e proteção de dados](storsimple-8000-security.md).

A alteração chave de encriptação de dados do Olá serviço é um processo do passo 3:

1. Utilizar scripts do Windows PowerShell para o Azure Resource Manager, autorize uma chave de encriptação de dados do dispositivo toochange Olá serviço.
2. Com o Windows PowerShell para StorSimple, inicie a alteração de encriptação de dados de serviço do Olá chave.
3. Se tiver mais do que um dispositivo StorSimple, atualize a chave de encriptação do Olá serviço dados em Olá outros dispositivos.

### <a name="step-1-use-windows-powershell-script-tooauthorize-a-device-toochange-hello-service-data-encryption-key"></a>Passo 1: Utilize o Windows PowerShell script tooAuthorize uma chave de encriptação de dados do dispositivo toochange Olá serviço
Normalmente, o administrador de dispositivos de Olá irá solicitar se administrador de serviço Olá autorizar um chaves de encriptação de dados do dispositivo toochange serviço. administrador de serviços de Olá, em seguida, irá autorizar a chave do Olá dispositivo toochange Olá.

Este passo é realizado através de Olá do Azure Resource Manager baseado em script. administrador de serviço de Olá pode selecionar um dispositivo elegível toobe autorizado. dispositivo Olá é, em seguida, o processo de alteração de chave de encriptação de dados de serviço Olá toostart autorizados. 

Para mais informações sobre como utilizar o script de Olá, visite demasiado[autorizar ServiceEncryptionRollover.ps1](https://github.com/anoobbacker/storsimpledevicemgmttools/blob/master/Authorize-ServiceEncryptionRollover.ps1)

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>Os dispositivos que podem ser autorizado chaves de encriptação de dados de serviço toochange?
Um dispositivo tem de cumprir Olá antes de ser alterações chave de encriptação dados de serviço autorizado tooinitiate os seguintes critérios:

* Olá dispositivo tem de estar online toobe elegível para autorização de alteração de chave de encriptação de dados de serviço.
* Podem autorizar Olá mesmo dispositivo novamente após 30 minutos se alterar a chave de Olá não foi iniciado.
* Podem autorizar um dispositivo diferente, desde que a alteração de chave Olá não foi iniciada pelo dispositivo anteriormente autorizado Olá. Depois do novo dispositivo de Olá tem sido autorizado, dispositivo antigo Olá não é possível iniciar a alteração de Olá.
* Não é possível autorizar um dispositivo enquanto Olá rollover da chave de encriptação de dados de serviço Olá está em curso.
* Podem autorizar um dispositivo quando alguns dos dispositivos Olá registados no serviço de Olá tem revertida através de encriptação de Olá enquanto outros utilizadores não têm. 

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>Passo 2: Utilize o Windows PowerShell para StorSimple tooinitiate Olá serviço encriptação chave alteração de dados
Este passo é efetuado no Olá do Windows PowerShell para StorSimple interface Olá autorizado o dispositivo StorSimple.

> [!NOTE]
> Não existem operações podem ser efetuadas no Olá portal do Azure do seu serviço StorSimple Manager até que o rollover da chave Olá esteja concluído.
> 
> 

Se estiver a utilizar interface do Windows PowerShell de toohello tooconnect Olá dispositivo consola de série, execute Olá os seguintes passos.

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a>alterar a chave de encriptação de dados de serviço Olá tooinitiate
1. Selecione a opção 1 toolog com acesso total.
2. Na linha de comandos Olá, escreva:
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Depois de cmdlet Olá foi concluída com êxito, irá receber uma nova chave de encriptação de dados do serviço. Copie e guarde esta chave para utilização no passo 3 deste processo. Esta chave será utilizada tooupdate Olá todos os restantes dispositivos registados com o serviço do StorSimple Manager Olá.
   
   > [!NOTE]
   > Este processo pode ser iniciado no prazo de quatro horas de autorização de um dispositivo StorSimple.
   > 
   > 
   
   Esta nova chave, em seguida, é enviada toohello toobe enviadas por push tooall Olá dispositivos de serviço que são registados com o serviço de Olá. Um alerta, em seguida, serão apresentados no dashboard de serviço Olá. serviço de Olá irá desativar todas as operações de Olá nos dispositivos Olá registado e administrador de dispositivos de Olá, em seguida, terá de chave de encriptação do tooupdate Olá serviço dados em Olá outros dispositivos. No entanto, hello (anfitriões enviar dados toohello na nuvem) e/s serão não interrompidos.
   
   Se tiver um único dispositivo registado tooyour serviço, processo de rollover Olá está agora concluído e pode ignorar o passo seguinte Olá. Se tiver várias dispositivos registados tooyour de serviço, avance toostep 3.

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a>Passo 3: Atualização Olá serviço dados chave de encriptação em outros dispositivos StorSimple
Estes passos devem ser executados na interface do Windows PowerShell Olá do dispositivo StorSimple, se tiver vários dispositivos do serviço StorSimple Manager tooyour registado. chave de Olá que obteve no passo 2 tem de ser utilizado tooupdate todas Olá restantes dispositivo StorSimple registado Olá serviço StorSimple Manager.

Efetue Olá os seguintes passos tooupdate Olá serviço a encriptação de dados no seu dispositivo.

#### <a name="tooupdate-hello-service-data-encryption-key"></a>chave de encriptação de dados de serviço Olá tooupdate
1. Utilize o Windows PowerShell para StorSimple tooconnect toohello consola. Selecione a opção 1 toolog com acesso total.
2. Na linha de comandos Olá, escreva:
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Fornecer Olá serviço dados chave de encriptação que obteve no [passo 2: Utilize o Windows PowerShell para StorSimple tooinitiate Olá serviço dados encriptação alteração de chave](#to-initiate-the-service-data-encryption-key-change).


## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre Olá [processo de implementação do StorSimple](storsimple-8000-deployment-walkthrough-u2.md).
* Saiba mais sobre [gerir a conta de armazenamento StorSimple](storsimple-8000-manage-storage-accounts.md).
* Saiba mais sobre como demasiado[utilize Olá tooadminister de serviço do Gestor de dispositivos do StorSimple o dispositivo StorSimple](storsimple-8000-manager-service-administration.md).
