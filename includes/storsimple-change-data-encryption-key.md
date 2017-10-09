<!--author=SharS last changed: 12/01/15-->

### <a name="step-1-authorize-a-device-toochange-hello-service-data-encryption-key-in-hello-azure-classic-portal"></a>Passo 1: Autorizar uma chave de encriptação do dispositivo toochange Olá serviço dados no Olá portal clássico do Azure
Normalmente, o administrador de dispositivos de Olá irá solicitar se administrador de serviço Olá autorizar um chaves de encriptação de dados do dispositivo toochange serviço. administrador de serviços de Olá, em seguida, irá autorizar a chave do Olá dispositivo toochange Olá.

Este passo é efetuado na Olá portal clássico do Azure. administrador de serviço de Olá pode selecionar um dispositivo de uma lista apresentada de dispositivos de Olá que são elegível toobe autorizado. dispositivo Olá é, em seguida, o processo de alteração de chave de encriptação de dados de serviço Olá toostart autorizados.

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>Os dispositivos que podem ser autorizado chaves de encriptação de dados de serviço toochange?
Um dispositivo tem de cumprir Olá antes de ser alterações chave de encriptação dados de serviço autorizado tooinitiate os seguintes critérios:

* Olá dispositivo tem de estar online toobe elegível para autorização de alteração de chave de encriptação de dados de serviço.
* Podem autorizar Olá mesmo dispositivo novamente após 30 minutos se alterar a chave de Olá não foi iniciado.
* Podem autorizar um dispositivo diferente, desde que a alteração de chave Olá não foi iniciada pelo dispositivo anteriormente autorizado Olá. Depois do novo dispositivo de Olá tem sido autorizado, dispositivo antigo Olá não é possível iniciar a alteração de Olá.
* Não é possível autorizar um dispositivo enquanto Olá rollover da chave de encriptação de dados de serviço Olá está em curso.
* Podem autorizar um dispositivo quando alguns dos dispositivos Olá registados no serviço de Olá tem revertida através de encriptação de Olá enquanto outros utilizadores não têm. Nestes casos, os dispositivos elegíveis Olá são Olá aqueles que concluiu a alteração de encriptação de dados de serviço do Olá chave.

> [!NOTE]
> No portal clássico do Azure Olá, StorSimple dispositivos virtuais não são apresentados na lista de Olá de dispositivos que podem estar autorizado a alteração de chave toostart Olá.
> 
> 

Efetuar Olá tooselect passos a seguir e autorizar uma dispositivo tooinitiate Olá serviço dados encriptação alteração de chave.

#### <a name="tooauthorize-a-device-toochange-hello-key"></a>tooauthorize uma chave do dispositivo toochange Olá
1. Na página do dashboard de serviço de Olá, clique em **chave de encriptação de dados de serviço de alteração**.
   
    ![Chave de encriptação do serviço de alteração](./media/storsimple-change-data-encryption-key/HCS_ChangeServiceDataEncryptionKey-include.png)
2. No Olá **chave de encriptação de dados de serviço de alteração** diálogo caixa, selecionar e autorizar uma dispositivo tooinitiate Olá serviço dados encriptação alteração de chave. Olá na lista pendente tem todos os dispositivos elegíveis Olá que podem ser autorizados.
3. Clique Olá ícone de verificação ![ícone de verificação](./media/storsimple-change-data-encryption-key/HCS_CheckIcon-include.png).

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>Passo 2: Utilize o Windows PowerShell para StorSimple tooinitiate Olá serviço encriptação chave alteração de dados
Este passo é efetuado no Olá do Windows PowerShell para StorSimple interface Olá autorizado o dispositivo StorSimple.

> [!NOTE]
> Não existem operações podem ser efetuadas no Olá portal clássico do Azure do seu serviço StorSimple Manager até que o rollover da chave Olá esteja concluído.
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
Estes passos devem ser executados na interface do Windows PowerShell Olá do dispositivo StorSimple, se tiver vários dispositivos do serviço StorSimple Manager tooyour registado. chave de Olá que obteve no passo 2: Utilize o Windows PowerShell para StorSimple tooinitiate Olá serviço encriptação chave alteração de dados tem de ser utilizado tooupdate todas Olá restantes dispositivo StorSimple registado Olá serviço StorSimple Manager.

Efetue Olá os seguintes passos tooupdate Olá serviço a encriptação de dados no seu dispositivo.

#### <a name="tooupdate-hello-service-data-encryption-key"></a>chave de encriptação de dados de serviço Olá tooupdate
1. Utilize o Windows PowerShell para StorSimple tooconnect toohello consola. Selecione a opção 1 toolog com acesso total.
2. Na linha de comandos Olá, escreva:
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Fornecer Olá serviço dados chave de encriptação que obteve no [passo 2: Utilize o Windows PowerShell para StorSimple tooinitiate Olá serviço dados encriptação alteração de chave](#to-initiate-the-service-data-encryption-key-change).

