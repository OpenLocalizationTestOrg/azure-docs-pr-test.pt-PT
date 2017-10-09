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
# <a name="manage-a-scale-out-process-server"></a><span data-ttu-id="e4309-103">Gerir um servidor de processos de escalamento horizontal</span><span class="sxs-lookup"><span data-stu-id="e4309-103">Manage a Scale-out Process Server</span></span>

<span data-ttu-id="e4309-104">Servidor de processos de escalamento horizontal atua como um coordenador de transferência de dados entre os serviços de recuperação de Site de Olá e da sua infraestrutura no local.</span><span class="sxs-lookup"><span data-stu-id="e4309-104">Scale-out Process Server acts as a coordinator for data transfer between hello Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="e4309-105">Este artigo descreve como pode configurar, configurar e gerir um servidor de processos de escalamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="e4309-105">This article describes how you can set up, configure, and manage a Scale-out Process Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4309-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e4309-106">Prerequisites</span></span>
<span data-ttu-id="e4309-107">Olá seguem Olá recomendado hardware, software e rede tooset de configuração necessária configurar um servidor de processos de escalamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="e4309-107">hello following are hello recommended hardware, software, and network configuration required tooset up a Scale-out Process Server.</span></span>

> [!NOTE]
> <span data-ttu-id="e4309-108">[Planeamento da capacidade](site-recovery-capacity-planner.md) é tooensure um passo importante que implemente hello do servidor de processos de escalamento horizontal com uma configuração de conjuntos de que os requisitos de carga.</span><span class="sxs-lookup"><span data-stu-id="e4309-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step tooensure that you deploy hello Scale-out Process Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="e4309-109">Leia mais sobre [dimensionamento características para um servidor de processos de escalamento horizontal](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="e4309-109">Read more about [Scaling characteristics for a Scale-out Process Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a><span data-ttu-id="e4309-110">Transferir software de servidor de processos de escalamento horizontal Olá</span><span class="sxs-lookup"><span data-stu-id="e4309-110">Downloading hello Scale-out Process Server software</span></span>
1. <span data-ttu-id="e4309-111">Inicie sessão no toohello Azure tooyour de portal e procurar cofre dos serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="e4309-111">Log on toohello Azure portal and browse tooyour Recovery Services Vault.</span></span>
2. <span data-ttu-id="e4309-112">Procurar demasiado**infraestrutura de recuperação de Site** > **servidores de configuração** (em para o VMware e máquinas físicas).</span><span class="sxs-lookup"><span data-stu-id="e4309-112">Browse too**Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>
3. <span data-ttu-id="e4309-113">Selecione o seu toodrill do servidor de configuração para baixo na página de detalhes do servidor de configuração Olá.</span><span class="sxs-lookup"><span data-stu-id="e4309-113">Select your configuration server toodrill down into hello configuration server's details page.</span></span>
4. <span data-ttu-id="e4309-114">Clique em Olá **+ o servidor de processos** botão.</span><span class="sxs-lookup"><span data-stu-id="e4309-114">Click hello **+ Process Server** button.</span></span>
5. <span data-ttu-id="e4309-115">No Olá **servidor de processos adicionar** página, selecione **no local do servidor de processos de implementar, escalamento horizontal** opção de Olá **escolha onde pretende toodeploy o servidor de processos** pendente.</span><span class="sxs-lookup"><span data-stu-id="e4309-115">In hello **Add Process server** page, select **Deploy a Scale-out Process Server on-premises** option from hello **Choose where you want toodeploy your process server** drop-down.</span></span>

  ![Adicionar página de servidores](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. <span data-ttu-id="e4309-117">Clique em Olá **Olá de transferência de configuração de unificada do Microsoft Azure Site Recovery** versão mais recente do ligação toodownload Olá da instalação do servidor de processos de Olá Escalamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="e4309-117">Click hello **Download hello Microsoft Azure Site Recovery Unified Setup** link toodownload hello latest version of hello Scale-out Process Server installation.</span></span>

  > [!WARNING]
  <span data-ttu-id="e4309-118">Olá versão do seu servidor de processos de escalamento horizontal deve ser igual tooor inferior à versão de servidor de configuração de Olá em execução no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="e4309-118">hello version of your Scale-out Process Server should be equal tooor lesser than hello Configuration Server version running in your environment.</span></span> <span data-ttu-id="e4309-119">Compatibilidade da versão tooensure uma forma simples é toouse Olá mesmo bits de instalador que recentemente utilizou tooinstall/atualizar o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="e4309-119">A simple way tooensure version compatibility is toouse hello same installer bits that you recently used tooinstall/update your Configuration Server.</span></span>

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a><span data-ttu-id="e4309-120">Instalar e registar um servidor de processos de escalamento horizontal de GUI</span><span class="sxs-lookup"><span data-stu-id="e4309-120">Installing and registering a Scale-out Process Server from GUI</span></span>
<span data-ttu-id="e4309-121">Se tiver tooscale fora da sua implementação, para além de 200 máquinas de origem, ou um diário total churn taxa de mais do que 2 TB, é necessário o volume de tráfego do processo suplementar servidores toohandle Olá.</span><span class="sxs-lookup"><span data-stu-id="e4309-121">If you have tooscale out your deployment beyond 200 source machines, or a total daily churn rate of more than 2 TB, you need additional process servers toohandle hello traffic volume.</span></span>

<span data-ttu-id="e4309-122">Verifique Olá [tamanho recomendações para servidores de processos](#size-recommendations-for-the-process-server)e, em seguida, siga tooset estas instruções se o servidor de processos de Olá.</span><span class="sxs-lookup"><span data-stu-id="e4309-122">Check hello [size recommendations for process servers](#size-recommendations-for-the-process-server), and then follow these instructions tooset up hello process server.</span></span> <span data-ttu-id="e4309-123">Depois de configurar o servidor de Olá, migrar toouse de máquinas de origem-lo.</span><span class="sxs-lookup"><span data-stu-id="e4309-123">After setting up hello server, you migrate source machines toouse it.</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a><span data-ttu-id="e4309-124">Instalar e registar um servidor de processos de escalamento horizontal através da linha de comandos</span><span class="sxs-lookup"><span data-stu-id="e4309-124">Installing and registering a Scale-out Process Server using command-line</span></span>

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a><span data-ttu-id="e4309-125">Utilização de exemplo</span><span class="sxs-lookup"><span data-stu-id="e4309-125">Sample usage</span></span>
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a><span data-ttu-id="e4309-126">Escalamento horizontal servidor de processos da linha de comandos os argumentos do instalador.</span><span class="sxs-lookup"><span data-stu-id="e4309-126">Scale-out Process Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="e4309-127">Criar um ficheiro de configuração de definições de proxy</span><span class="sxs-lookup"><span data-stu-id="e4309-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="e4309-128">Parâmetro de ProxySettingsFilePath assume um ficheiro como entrada.</span><span class="sxs-lookup"><span data-stu-id="e4309-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="e4309-129">Crie o ficheiro utilizando Olá seguinte formato e transmita-o como parâmetro de entrada ProxySettingsFilePath.</span><span class="sxs-lookup"><span data-stu-id="e4309-129">Create file using hello following format and pass it as input ProxySettingsFilePath parameter.</span></span>
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a><span data-ttu-id="e4309-130">Modificar definições de proxy do servidor de processos de escalamento horizontal</span><span class="sxs-lookup"><span data-stu-id="e4309-130">Modifying proxy settings for Scale-out Process Server</span></span>
1. <span data-ttu-id="e4309-131">Inicie sessão no seu servidor de processos de escalamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="e4309-131">Login  into your Scale-out Process Server.</span></span>
2. <span data-ttu-id="e4309-132">Abra uma janela de comando do PowerShell de administrador.</span><span class="sxs-lookup"><span data-stu-id="e4309-132">Open an Admin PowerShell command window.</span></span>
3. <span data-ttu-id="e4309-133">Olá execute os seguintes comandos</span><span class="sxs-lookup"><span data-stu-id="e4309-133">Run hello following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. <span data-ttu-id="e4309-134">Em seguida procurar no diretório de toohello **%PROGRAMDATA%\ASR\Agent** e Olá execute os seguintes comandos</span><span class="sxs-lookup"><span data-stu-id="e4309-134">Next browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello following command</span></span>
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a><span data-ttu-id="e4309-135">Volte a registar um servidor de processos de escalamento horizontal</span><span class="sxs-lookup"><span data-stu-id="e4309-135">Re-registering a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* <span data-ttu-id="e4309-136">Em seguida, abra uma linha de comandos de administrador.</span><span class="sxs-lookup"><span data-stu-id="e4309-136">Next open an Admin command prompt.</span></span>
* <span data-ttu-id="e4309-137">Procurar no diretório toohello **%PROGRAMDATA%\ASR\Agent** e execute o comando de Olá</span><span class="sxs-lookup"><span data-stu-id="e4309-137">Browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello command</span></span>

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a><span data-ttu-id="e4309-138">Atualizar um servidor de processos de escalamento horizontal</span><span class="sxs-lookup"><span data-stu-id="e4309-138">Upgrading a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a><span data-ttu-id="e4309-139">Desativar um servidor de processos de escalamento horizontal</span><span class="sxs-lookup"><span data-stu-id="e4309-139">Decommissioning a Scale-out Process Server</span></span>
1. <span data-ttu-id="e4309-140">Certifique-se de que:</span><span class="sxs-lookup"><span data-stu-id="e4309-140">Ensure that:</span></span>
  - <span data-ttu-id="e4309-141">Mostra o estado de ligação do servidor de configuração como **ligado** no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e4309-141">Configuration Server's connection state shows as **Connected** in hello Azure portal</span></span>
  - <span data-ttu-id="e4309-142">Servidor de processos é capaz de ainda toocommunicate com o servidor de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="e4309-142">Process Server's is still able toocommunicate with hello Configuration server.</span></span>
2. <span data-ttu-id="e4309-143">Inicie sessão no servidor de processos toohello como um administrador</span><span class="sxs-lookup"><span data-stu-id="e4309-143">Log in toohello process server as an administrator</span></span>
3. <span data-ttu-id="e4309-144">Abra o painel de controlo > programa > desinstalar programas</span><span class="sxs-lookup"><span data-stu-id="e4309-144">Open up Control Panel > Program > Uninstall Programs</span></span>
4. <span data-ttu-id="e4309-145">Desinstale programas Olá na sequência de Olá indicada a seguir:</span><span class="sxs-lookup"><span data-stu-id="e4309-145">Uninstall hello programs in hello sequence given following:</span></span>
  * <span data-ttu-id="e4309-146">Servidor de processo do servidor de configuração do Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="e4309-146">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="e4309-147">Dependências de servidor de configuração de recuperação de sites de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e4309-147">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="e4309-148">Agente dos Serviços de Recuperação do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e4309-148">Microsoft Azure Recovery Services Agent</span></span>

<span data-ttu-id="e4309-149">Pode demorar até too15 minutos para tooreflect de eliminação do servidor de processos de Olá no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e4309-149">It can take up-too15 minutes for hello Process Server deletion tooreflect in hello Azure portal.</span></span>

  > [!NOTE]
  <span data-ttu-id="e4309-150">Se o servidor de processos de Olá está toocommunicate não é possível com hello do servidor de configuração (estado de ligação no portal estiver desligado), em seguida, terá de toofollow Olá os seguintes passos toopurge-lo de hello do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="e4309-150">If hello Process server is unable toocommunicate with hello Configuration Server (Connection State in portal is Disconnected), then you need toofollow hello following steps toopurge it from hello Configuration Server.</span></span>

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a><span data-ttu-id="e4309-151">Anulação do registo do servidor de processos de escalamento horizontal desligado de um servidor de configuração</span><span class="sxs-lookup"><span data-stu-id="e4309-151">Unregistering a disconnected Scale-out Process server from a Configuration Server</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a><span data-ttu-id="e4309-152">Requisitos de dimensionamento para um servidor de processos de escalamento horizontal</span><span class="sxs-lookup"><span data-stu-id="e4309-152">Sizing requirements for a Scale-out Process Server</span></span>

| <span data-ttu-id="e4309-153">**Servidor de processos adicionais**</span><span class="sxs-lookup"><span data-stu-id="e4309-153">**Additional process server**</span></span> | <span data-ttu-id="e4309-154">**Tamanho da cache do disco**</span><span class="sxs-lookup"><span data-stu-id="e4309-154">**Cache disk size**</span></span> | <span data-ttu-id="e4309-155">**Taxa de alteração de dados**</span><span class="sxs-lookup"><span data-stu-id="e4309-155">**Data change rate**</span></span> | <span data-ttu-id="e4309-156">**Máquinas protegidas**</span><span class="sxs-lookup"><span data-stu-id="e4309-156">**Protected machines**</span></span> |
| --- | --- | --- | --- |
|<span data-ttu-id="e4309-157">4 vCPUs (2 sockets * 2 núcleos @ GHz 2,5), 8 GB de memória</span><span class="sxs-lookup"><span data-stu-id="e4309-157">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8-GB memory</span></span> |<span data-ttu-id="e4309-158">300 GB</span><span class="sxs-lookup"><span data-stu-id="e4309-158">300 GB</span></span> |<span data-ttu-id="e4309-159">250 GB ou inferior</span><span class="sxs-lookup"><span data-stu-id="e4309-159">250 GB or less</span></span> |<span data-ttu-id="e4309-160">Replicar máquinas 85 ou menos.</span><span class="sxs-lookup"><span data-stu-id="e4309-160">Replicate 85 or less machines.</span></span> |
|<span data-ttu-id="e4309-161">8 vCPUs (2 sockets * 4 núcleos @ GHz 2,5), 12 GB de memória</span><span class="sxs-lookup"><span data-stu-id="e4309-161">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12-GB memory</span></span> |<span data-ttu-id="e4309-162">600 GB</span><span class="sxs-lookup"><span data-stu-id="e4309-162">600 GB</span></span> |<span data-ttu-id="e4309-163">250 GB too1 TB</span><span class="sxs-lookup"><span data-stu-id="e4309-163">250 GB too1 TB</span></span> |<span data-ttu-id="e4309-164">Replicar entre 85 150 máquinas.</span><span class="sxs-lookup"><span data-stu-id="e4309-164">Replicate between 85-150 machines.</span></span> |
|<span data-ttu-id="e4309-165">12 vCPUs (2 sockets * 6 núcleos @ GHz 2,5) 24 GB de memória</span><span class="sxs-lookup"><span data-stu-id="e4309-165">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24-GB memory</span></span> |<span data-ttu-id="e4309-166">1 TB</span><span class="sxs-lookup"><span data-stu-id="e4309-166">1 TB</span></span> |<span data-ttu-id="e4309-167">1 TB too2 TB</span><span class="sxs-lookup"><span data-stu-id="e4309-167">1 TB too2 TB</span></span> |<span data-ttu-id="e4309-168">Replicar entre 150 225 máquinas.</span><span class="sxs-lookup"><span data-stu-id="e4309-168">Replicate between 150-225 machines.</span></span> |
