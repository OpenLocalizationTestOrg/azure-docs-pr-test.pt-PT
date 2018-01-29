---
title: "Cópia de segurança do Azure - utilize o PowerShell para efetuar cópias de segurança de cargas de trabalho do DPM | Microsoft Docs"
description: "Saiba como implementar e gerir a cópia de segurança do Azure para o Data Protection Manager (DPM) com o PowerShell"
services: backup
documentationcenter: 
author: NKolli1
manager: shreeshd
editor: 
ms.assetid: e9bd223c-2398-4eb1-9bf3-50e08970fea7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: adigan;anuragm;trinadhk;markgal
ms.openlocfilehash: 9322037427c84f0b8a91cc76f5c0fed52167bc3c
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/21/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a>Implementar e gerir cópias de segurança para o Azure em servidores do Data Protection Manager (DPM) com o PowerShell
Este artigo mostra como utilizar o PowerShell para a configuração de cópia de segurança do Azure num servidor DPM e para gerir a cópia de segurança e recuperação.

## <a name="setting-up-the-powershell-environment"></a>Configurar o ambiente de PowerShell
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

Antes de poder utilizar o PowerShell para gerir cópias de segurança do Data Protection Manager para o Azure, tem de ter o direito ambiente no PowerShell. No início de sessão do PowerShell, certifique-se de que execute o seguinte comando para importar os módulos corretos e permitem-lhe referência corretamente os cmdlets do DPM:

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome to the DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a>Configuração e o registo
Para começar:

1. [Transferir o mais recente do PowerShell](https://github.com/Azure/azure-powershell/releases) (versão mínima necessária é: 1.0.0)
2. Ativar os mini-comandos de cópia de segurança do Azure ao mudar para *AzureResourceManager* modo utilizando o **Switch-AzureMode** commandlet:

```
PS C:\> Switch-AzureMode AzureResourceManager
```

As seguintes tarefas de configuração e o registo podem ser automatizadas com o PowerShell:

* Criar um cofre dos Serviços de Recuperação 
* Instalar o agente de cópia de segurança do Azure
* A registar com o serviço de cópia de segurança do Azure
* Definições de rede
* Definições de encriptação

## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos serviços de recuperação
Os seguintes passos encaminharem através da criação de um cofre dos serviços de recuperação. Um cofre dos serviços de recuperação é diferente de um cofre de cópia de segurança.

1. Se estiver a utilizar o Backup do Azure pela primeira vez, tem de utilizar o **Register-AzureRMResourceProvider** cmdlet para registar o fornecedor de serviços de recuperação do Azure com a sua subscrição.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. O Cofre de serviços de recuperação é um recurso ARM, por isso terá de colocá-lo dentro de um grupo de recursos. Pode utilizar um grupo de recursos existente ou crie um novo. Ao criar um novo grupo de recursos, especifique o nome e a localização para o grupo de recursos.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. Utilize o **New-AzureRmRecoveryServicesVault** cmdlet para criar um novo cofre. Lembre-se de que especifique a mesma localização do cofre que foi utilizado para o grupo de recursos.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. Especifique o tipo de redundância de armazenamento a utilizar. Pode utilizar [localmente redundante armazenamento (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) ou [Georreplicação redundante armazenamento (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage). O exemplo seguinte mostra que a opção - BackupStorageRedundancy para testVault está definida como GeoRedundant.

   > [!TIP]
   > Cmdlets de cópia de segurança do Azure muitos requerem o objeto de cofre dos serviços de recuperação como entrada. Por este motivo, é conveniente armazenar o objeto de cofre dos serviços de recuperação de cópia de segurança numa variável.
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-the-vaults-in-a-subscription"></a>Ver os cofres numa subscrição
Utilize **Get-AzureRmRecoveryServicesVault** para ver a lista de todos os cofres na subscrição atual. Pode utilizar este comando para verificar que foi criado um novo cofre, ou cofres de que estão disponíveis na subscrição.

Execute o comando Get-AzureRmRecoveryServicesVault, e são listados todos os cofres na subscrição.

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a>Instalar o agente de cópia de segurança do Azure num servidor DPM
Antes de instalar o agente do Backup do Azure, tem de ter o instalador transferido e presente no servidor do Windows. Pode obter a versão mais recente do instalador do [Microsoft Download Center](http://aka.ms/azurebackup_agent) ou a partir da página do Dashboard do cofre dos serviços de recuperação. Guardar o instalador para uma localização facilmente acessível, como * C:\Downloads\*.

Para instalar o agente, execute o seguinte comando numa consola do PowerShell elevada **no servidor do DPM**:

```
PS C:\> MARSAgentInstaller.exe /q
```

Esta ação instala o agente com todas as opções predefinidas. A instalação demora alguns minutos em segundo plano. Se não especificar o */nu* opção o **Windows Update** é aberta a janela no final da instalação para verificar a existência de quaisquer atualizações.

O agente aparece na lista de programas instalados. Para ver a lista de programas instalados, aceda a **painel de controlo** > **programas** > **programas e funcionalidades**.

![Agente instalado](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a>Opções de instalação
Para ver todas as opções disponíveis através da linha de comandos, utilize o seguinte comando:

```
PS C:\> MARSAgentInstaller.exe /?
```

As opções disponíveis incluem:

| Opção | Detalhes | Predefinição |
| --- | --- | --- |
| /q |Instalação silenciosos |- |
| /p: "localização" |Caminho para a pasta de instalação para o agente de cópia de segurança do Azure. |C:\Program Files\Microsoft Azure Recovery Services Agent |
| /s: "localização" |Caminho para a pasta de cache para o agente de cópia de segurança do Azure. |C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch |
| /m |Optar ativamente por participar no Microsoft Update |- |
| /NU |Não procurar atualizações depois de concluída a instalação |- |
| /d |Desinstala o agente do Microsoft Azure Recovery Services |- |
| / pH |Endereço do anfitrião proxy |- |
| /po |Número de porta de anfitrião do proxy |- |
| /Pu |O nome de utilizador do proxy anfitrião |- |
| /PW |Palavra-passe do proxy |- |

## <a name="registering-dpm-to-a-recovery-services-vault"></a>Ao registar o DPM para uma recuperação cofre dos serviços
Depois de criado o Cofre dos serviços de recuperação, transfira o agente mais recente e as credenciais do cofre e armazene-o numa localização conveniente como C:\Downloads.

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

No servidor do DPM, execute o [início OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet para registar a máquina com o cofre.

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a>Definições de configuração inicial
Depois do servidor do DPM está registado com o Cofre dos serviços de recuperação, começa com as definições predefinidas da subscrição. Estas definições de subscrição incluem redes, encriptação e a área de transição. Para alterar as definições de subscrição tem de obter primeiro um identificador nas definições (predefinição) existentes utilizando o [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

Todas as modificações são efetuadas a este objeto de PowerShell local ```$setting``` e, em seguida, o objeto completo é submetido para o DPM e cópia de segurança do Azure guardá-las utilizando o [conjunto DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet. Tem de utilizar o ```–Commit``` sinalizador para se certificar de que as alterações são mantidas. As definições não serão aplicadas e utilizadas pela cópia de segurança do Azure, a menos que consolidada.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a>Redes
Se a conectividade do computador do DPM para o serviço de cópia de segurança do Azure na internet através de um servidor proxy, as definições do servidor proxy devem ser fornecidas para cópias de segurança com êxito. Isto é feito utilizando o ```-ProxyServer```e ```-ProxyPort```, ```-ProxyUsername``` e o ```ProxyPassword``` parâmetros com o [conjunto DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet. Neste exemplo, não há nenhum servidor de proxy para que iremos explicitamente são limpar quaisquer informações relacionadas com o proxy.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

Também é possível controlar a utilização de largura de banda com opções de ```-WorkHourBandwidth``` e ```-NonWorkHourBandwidth``` para um conjunto especificado de dias da semana. Neste exemplo, vamos não define qualquer limitação.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-the-staging-area"></a>Configurar a área de transição
O agente de cópia de segurança do Azure em execução no servidor do DPM precisa de armazenamento temporário para dados restaurados a partir da nuvem (área de transição local). Configurar a área de transição, utilizando o [conjunto DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet e o ```-StagingAreaPath``` parâmetro.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

No exemplo acima, a área de transição será definida para *C:\StagingArea* no objeto do PowerShell ```$setting```. Certifique-se de que a pasta especificada já existe; caso contrário, a consolidação final das definições de subscrição irá falhar.

### <a name="encryption-settings"></a>Definições de encriptação
Os dados de cópia de segurança enviados para a cópia de segurança do Azure são encriptados para proteger a confidencialidade dos dados. A frase de acesso de encriptação é a "palavra-passe" para desencriptar os dados no momento do restauro. É importante manter esta informação seguro e segura quando está definido.

No exemplo abaixo, o primeiro comando converte a cadeia ```passphrase123456789``` para uma cadeia segura e atribui a cadeia segura para a variável com o nome ```$Passphrase```. o segundo comando define a cadeia segura em ```$Passphrase``` como a palavra-passe para encriptar as cópias de segurança.

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> Manter as informações da frase de acesso seguro e segura quando está definido. Não será possível restaurar dados a partir do Azure sem esta frase de acesso.
>
>

Nesta fase, deve efetuar as alterações necessárias para o ```$setting``` objeto. Lembre-se a consolidar as alterações.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a>Proteger os dados para cópia de segurança do Azure
Nesta secção, irá adicionar um servidor de produção para o DPM e, em seguida, proteger os dados para armazenamento do DPM local e, em seguida, a cópia de segurança do Azure. Nos exemplos, vamos demonstrar como fazer uma cópia de segurança de ficheiros e pastas. A lógica facilmente pode ser expandida a cópia de segurança de qualquer origem de dados suportados pelo DPM. Todas as suas cópias de segurança do DPM são regidas por um grupo de proteção (PG) com quatro partes:

1. **Os membros do grupo** é uma lista de todos os objetos passíveis de proteção (também conhecido como *origens de dados* no DPM) que pretende proteger no mesmo grupo de proteção. Por exemplo, poderá proteger produção VMs num grupo de proteção e bases de dados do SQL Server noutro grupo de proteção podem ter requisitos de cópia de segurança diferentes. Antes de fazer qualquer origem de dados num servidor de produção, que tem de certificar-se de que o agente do DPM está instalado no servidor e for gerido pelo DPM. Siga os passos para [instalar o agente do DPM](https://technet.microsoft.com/library/bb870935.aspx) e ligar ao servidor do DPM adequado.
2. **Método de proteção de dados** Especifica as cópia de segurança localizações dos destinos de-banda, disco e na nuvem. No nosso exemplo, irá proteger dados no disco local e na nuvem.
3. A **agenda de cópia de segurança** que especifica quando as cópias de segurança têm de ser executadas e com que frequência os dados devem ser sincronizados entre o servidor do DPM e o servidor de produção.
4. A **agenda de retenção** que especifica o período de tempo para manter os pontos de recuperação no Azure.

### <a name="creating-a-protection-group"></a>Criar um grupo de proteção
Comece por criar um novo grupo de proteção utilizando o [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

O cmdlet acima irá criar um grupo de proteção com o nome *ProtectGroup01*. Também é possível modificar um grupo de proteção existente mais tarde para adicionar a cópia de segurança na nuvem do Azure. No entanto, para efetuar quaisquer alterações ao grupo de proteção - novo ou existente - é necessário obter um identificador num *modificável* objeto utilizando o [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a>A adição de membros do grupo ao grupo de proteção
Cada agente do DPM a conhecer a lista de origens de dados no servidor que está instalada. Para adicionar uma origem de dados para o grupo de proteção, o agente do DPM tem de enviar primeiro uma lista das origens de dados para o servidor do DPM. Um ou mais origens de dados, em seguida, são selecionadas e adicionadas ao grupo de proteção. Os passos de PowerShell necessários para atingir esse objetivo são:

1. Obter uma lista de todos os servidores geridos pelo DPM através do agente do DPM.
2. Escolha um servidor específico.
3. Obter uma lista de todas as origens de dados no servidor.
4. Escolha um ou mais origens de dados e adicioná-los ao grupo de proteção

A lista de servidores em que o agente do DPM está instalado e está a ser gerido pelo servidor DPM é adquirida com o [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet. Neste exemplo, iremos filtrar e configure apenas PS com nome *productionserver01* para cópia de segurança.

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”}
```

Agora obter a lista de origens de dados no ```$server``` utilizando o [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet. Neste exemplo, está a filtrar o volume de * D:\* que queremos configurar para cópia de segurança. Esta origem de dados é então adicionada ao grupo de proteção utilizando o [adicionar DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet. Não se esqueça de utilizar o *modificável* objeto do grupo de proteção ```$MPG``` para tornar as adições.

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

Repita este passo como tantas vezes quantas as necessárias, até ter adicionado todas as origens de dados que escolheu para o grupo de proteção. Também pode começar a utilizar apenas uma origem de dados e concluir o fluxo de trabalho para criar o grupo de proteção e mais tarde, adicione mais origens de dados para o grupo de proteção.

### <a name="selecting-the-data-protection-method"></a>Selecionar o método de proteção de dados
Assim que as origens de dados foram adicionadas ao grupo de proteção, o passo seguinte é especificar o método de proteção utilizando o [conjunto DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet. Neste exemplo, o grupo de proteção está configurado para cópia de segurança de nuvem e de disco local. Também tem de especificar a origem de dados que pretende proteger na nuvem utilizando o [adicionar DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet com - sinalizador Online.

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a>Definir o período de retenção
Definir a retenção para pontos de cópia de segurança utilizando o [conjunto DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet. Enquanto pode parecer ímpar definir a retenção antes da agenda de cópia de segurança tiver sido definida, utilizando o ```Set-DPMPolicyObjective``` cmdlet define automaticamente uma agenda de cópia de segurança predefinida, em seguida, pode ser modificada. É sempre possível conjunto agendar a cópia de segurança pela primeira vez e a política de retenção depois.

No exemplo abaixo, o cmdlet define os parâmetros de retenção para cópias de segurança de disco. Isto irá manter cópias de segurança para 10 dias e os dados de sincronização a cada 6 horas entre o servidor de produção e o servidor do DPM. O ```SynchronizationFrequencyMinutes``` não define a frequência um ponto de cópia de segurança é criado, mas como muitas vezes, os dados são copiados para o servidor do DPM.  Esta definição impede que as cópias de segurança fique demasiado grande.

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

Para cópias de segurança do Azure vai (DPM refere-se aos mesmos como cópias de segurança Online) os intervalos de retenção podem ser configurados para [utilizando um esquema de avô-pai-filho (GFS) de retenção de longo prazo](backup-azure-backup-cloud-as-tape.md). Ou seja, pode definir uma política de retenção combinado que envolvem diária, semanal, mensal e anual políticas de retenção. Neste exemplo, vamos criar uma matriz que representa o esquema de retenção complexas que queremos e, em seguida, configure o intervalo de retenção utilizando o [conjunto DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a>Defina a agenda de cópia de segurança
O DPM define uma agenda de cópia de segurança predefinida automaticamente se especificar a utilização do objetivo de proteção a ```Set-DPMPolicyObjective``` cmdlet. Para alterar as agendas predefinidas, utilize o [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet seguido de [DPMPolicySchedule conjunto](https://technet.microsoft.com/library/hh881723) cmdlet.

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

No exemplo acima, ```$onlineSch``` é uma matriz com quatro elementos que contém a agenda de proteção online existente para o grupo de proteção no esquema GFS:

1. ```$onlineSch[0]```contém a agenda diária
2. ```$onlineSch[1]```contém a semanal
3. ```$onlineSch[2]```contém a agenda mensal
4. ```$onlineSch[3]```contém a agenda anual

Por isso se necessitar de modificar a agenda semanal, terá de fazer referência ao ```$onlineSch[1]```.

### <a name="initial-backup"></a>Cópia de segurança inicial
Quando cópia de segurança de uma origem de dados pela primeira vez, o DPM tem cria réplica inicial de que cria uma cópia completa da origem de dados estar protegida num volume de réplica do DPM. Esta atividade pode ser está agendada para uma hora específica ou pode ser acionada manualmente, utilizando o [conjunto DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet com o parâmetro ```-NOW```.

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a>Alteração do tamanho da réplica do DPM e o volume de pontos de recuperação
Também pode alterar o tamanho do volume de réplica do DPM e a utilização de volume de cópia sombra de volumes [conjunto DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet como no exemplo seguinte: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Origem de dados $DS - ProtectionGroup $MPG-manual - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)

### <a name="committing-the-changes-to-the-protection-group"></a>Consolidar as alterações ao grupo de proteção
Por fim, as alterações têm de ser confirmadas antes do DPM pode efetuar a cópia de segurança pela nova configuração do grupo de proteção. Isto pode ser conseguido utilizando o [conjunto DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a>Ver os pontos de cópia de segurança
Pode utilizar o [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet para obter uma lista de todos os pontos de recuperação para uma origem de dados. Neste exemplo, iremos:

* obter todos os PGs no servidor do DPM e armazenado numa matriz```$PG```
* obter as origens de dados correspondente para o```$PG[0]```
* obter todos os pontos de recuperação para uma origem de dados.

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a>Restaurar os dados protegidos no Azure
Restauro de dados é uma combinação de um ```RecoverableItem``` objeto e um ```RecoveryOption``` objeto. Na secção anterior, mas obteve uma lista dos pontos de cópia de segurança para uma origem de dados.

No exemplo abaixo, iremos demonstrar como restaurar uma máquina virtual de Hyper-V a partir de cópia de segurança do Azure através da combinação de pontos de cópia de segurança com o destino de recuperação. Este exemplo inclui:

* Criar uma opção de recuperação utilizando o [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.
* Obter a matriz de pontos de cópia de segurança utilizando o ```Get-DPMRecoveryPoint``` cmdlet.
* Escolher um ponto de cópia de segurança para restaurar a partir de.

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

Os comandos podem facilmente ser expandidos para qualquer tipo de origem de dados.

## <a name="next-steps"></a>Passos Seguintes
* Para obter mais informações sobre o DPM para cópia de segurança do Azure, consulte [introdução à cópia de segurança do DPM](backup-azure-dpm-introduction.md)
