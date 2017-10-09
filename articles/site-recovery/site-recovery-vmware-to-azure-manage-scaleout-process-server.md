---
title: " Gerir um servidor de processos de escalamento horizontal no Azure Site Recovery | Microsoft Docs"
description: Este artigo descreve como tooset configurar e gerir um servidor de processos de escalamento horizontal no Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 3d72f9c2c7014a4ff2fa2af168aa55ad1452eae5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-scale-out-process-server"></a>Gerir um servidor de processos de escalamento horizontal

Servidor de processos de escalamento horizontal atua como um coordenador de transferência de dados entre os serviços de recuperação de Site de Olá e da sua infraestrutura no local. Este artigo descreve como pode configurar, configurar e gerir um servidor de processos de escalamento horizontal.

## <a name="prerequisites"></a>Pré-requisitos
Olá seguem Olá recomendado hardware, software e rede tooset de configuração necessária configurar um servidor de processos de escalamento horizontal.

> [!NOTE]
> [Planeamento da capacidade](site-recovery-capacity-planner.md) é tooensure um passo importante que implemente hello do servidor de processos de escalamento horizontal com uma configuração de conjuntos de que os requisitos de carga. Leia mais sobre [dimensionamento características para um servidor de processos de escalamento horizontal](#sizing-requirements-for-a-configuration-server).

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a>Transferir software de servidor de processos de escalamento horizontal Olá
1. Inicie sessão no toohello Azure tooyour de portal e procurar cofre dos serviços de recuperação.
2. Procurar demasiado**infraestrutura de recuperação de Site** > **servidores de configuração** (em para o VMware e máquinas físicas).
3. Selecione o seu toodrill do servidor de configuração para baixo na página de detalhes do servidor de configuração Olá.
4. Clique em Olá **+ o servidor de processos** botão.
5. No Olá **servidor de processos adicionar** página, selecione **no local do servidor de processos de implementar, escalamento horizontal** opção de Olá **escolha onde pretende toodeploy o servidor de processos** pendente.

  ![Adicionar página de servidores](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. Clique em Olá **Olá de transferência de configuração de unificada do Microsoft Azure Site Recovery** versão mais recente do ligação toodownload Olá da instalação do servidor de processos de Olá Escalamento horizontal.

  > [!WARNING]
  Olá versão do seu servidor de processos de escalamento horizontal deve ser igual tooor inferior à versão de servidor de configuração de Olá em execução no seu ambiente. Compatibilidade da versão tooensure uma forma simples é toouse Olá mesmo bits de instalador que recentemente utilizou tooinstall/atualizar o servidor de configuração.

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a>Instalar e registar um servidor de processos de escalamento horizontal de GUI
Se tiver tooscale fora da sua implementação, para além de 200 máquinas de origem, ou um diário total churn taxa de mais do que 2 TB, é necessário o volume de tráfego do processo suplementar servidores toohandle Olá.

Verifique Olá [tamanho recomendações para servidores de processos](#size-recommendations-for-the-process-server)e, em seguida, siga tooset estas instruções se o servidor de processos de Olá. Depois de configurar o servidor de Olá, migrar toouse de máquinas de origem-lo.

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a>Instalar e registar um servidor de processos de escalamento horizontal através da linha de comandos

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a>Utilização de exemplo
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a>Escalamento horizontal servidor de processos da linha de comandos os argumentos do instalador.
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a>Criar um ficheiro de configuração de definições de proxy
Parâmetro de ProxySettingsFilePath assume um ficheiro como entrada. Crie o ficheiro utilizando Olá seguinte formato e transmita-o como parâmetro de entrada ProxySettingsFilePath.
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a>Modificar definições de proxy do servidor de processos de escalamento horizontal
1. Inicie sessão no seu servidor de processos de escalamento horizontal.
2. Abra uma janela de comando do PowerShell de administrador.
3. Olá execute os seguintes comandos
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. Em seguida procurar no diretório de toohello **%PROGRAMDATA%\ASR\Agent** e Olá execute os seguintes comandos
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a>Volte a registar um servidor de processos de escalamento horizontal
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* Em seguida, abra uma linha de comandos de administrador.
* Procurar no diretório toohello **%PROGRAMDATA%\ASR\Agent** e execute o comando de Olá

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a>Atualizar um servidor de processos de escalamento horizontal
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a>Desativar um servidor de processos de escalamento horizontal
1. Certifique-se de que:
  - Mostra o estado de ligação do servidor de configuração como **ligado** no Olá portal do Azure
  - Servidor de processos é capaz de ainda toocommunicate com o servidor de configuração de Olá.
2. Inicie sessão no servidor de processos toohello como um administrador
3. Abra o painel de controlo > programa > desinstalar programas
4. Desinstale programas Olá na sequência de Olá indicada a seguir:
  * Servidor de processo do servidor de configuração do Microsoft Azure Site Recovery
  * Dependências de servidor de configuração de recuperação de sites de Microsoft Azure
  * Agente dos Serviços de Recuperação do Microsoft Azure

Pode demorar até too15 minutos para tooreflect de eliminação do servidor de processos de Olá no Olá portal do Azure.

  > [!NOTE]
  Se o servidor de processos de Olá está toocommunicate não é possível com hello do servidor de configuração (estado de ligação no portal estiver desligado), em seguida, terá de toofollow Olá os seguintes passos toopurge-lo de hello do servidor de configuração.

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a>Anulação do registo do servidor de processos de escalamento horizontal desligado de um servidor de configuração

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a>Requisitos de dimensionamento para um servidor de processos de escalamento horizontal

| **Servidor de processos adicionais** | **Tamanho da cache do disco** | **Taxa de alteração de dados** | **Máquinas protegidas** |
| --- | --- | --- | --- |
|4 vCPUs (2 sockets * 2 núcleos @ GHz 2,5), 8 GB de memória |300 GB |250 GB ou inferior |Replicar máquinas 85 ou menos. |
|8 vCPUs (2 sockets * 4 núcleos @ GHz 2,5), 12 GB de memória |600 GB |250 GB too1 TB |Replicar entre 85 150 máquinas. |
|12 vCPUs (2 sockets * 6 núcleos @ GHz 2,5) 24 GB de memória |1 TB |1 TB too2 TB |Replicar entre 150 225 máquinas. |
