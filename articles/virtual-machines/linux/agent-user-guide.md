---
title: "aaaAzure descrição geral do agente de VM Linux | Microsoft Docs"
description: "Saiba como tooinstall e configurar o agente Linux (waagent) toomanage interação da sua máquina virtual com o controlador de recursos de infraestrutura do Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4e08c84d9205f4db7aae6fd1568ec1f15fba395c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-and-using-hello-azure-linux-agent"></a><span data-ttu-id="03b78-103">Compreensão e utilização de Olá agente Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="03b78-103">Understanding and using hello Azure Linux Agent</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a><span data-ttu-id="03b78-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="03b78-104">Introduction</span></span>
<span data-ttu-id="03b78-105">Olá Linux agente do Microsoft Azure (waagent) gere o Linux e FreeBSD aprovisionamento e interação de VM com Olá controlador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="03b78-105">hello Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="03b78-106">Fornece Olá funcionalidade para implementações de Linux e FreeBSD IaaS os seguintes:</span><span class="sxs-lookup"><span data-stu-id="03b78-106">It provides hello following functionality for Linux and FreeBSD IaaS deployments:</span></span>

> [!NOTE]
> <span data-ttu-id="03b78-107">Consulte o agente Linux do Azure de Olá [Leia-me](https://github.com/Azure/WALinuxAgent/blob/master/README.md) para obter detalhes adicionais.</span><span class="sxs-lookup"><span data-stu-id="03b78-107">See hello Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.</span></span>
> 
> 

* <span data-ttu-id="03b78-108">**Imagem de aprovisionamento**</span><span class="sxs-lookup"><span data-stu-id="03b78-108">**Image Provisioning**</span></span>
  
  * <span data-ttu-id="03b78-109">Criação de uma conta de utilizador</span><span class="sxs-lookup"><span data-stu-id="03b78-109">Creation of a user account</span></span>
  * <span data-ttu-id="03b78-110">Configurar tipos de autenticação SSH</span><span class="sxs-lookup"><span data-stu-id="03b78-110">Configuring SSH authentication types</span></span>
  * <span data-ttu-id="03b78-111">Implementação de chaves públicas SSH e pares de chaves</span><span class="sxs-lookup"><span data-stu-id="03b78-111">Deployment of SSH public keys and key pairs</span></span>
  * <span data-ttu-id="03b78-112">Nome da definição Olá anfitrião</span><span class="sxs-lookup"><span data-stu-id="03b78-112">Setting hello host name</span></span>
  * <span data-ttu-id="03b78-113">Publicação Olá nome toohello a plataforma de anfitrião DNS</span><span class="sxs-lookup"><span data-stu-id="03b78-113">Publishing hello host name toohello platform DNS</span></span>
  * <span data-ttu-id="03b78-114">Plataforma do toohello de impressão digital de chave de anfitrião do Reporting Services SSH</span><span class="sxs-lookup"><span data-stu-id="03b78-114">Reporting SSH host key fingerprint toohello platform</span></span>
  * <span data-ttu-id="03b78-115">Gestão de discos de recursos</span><span class="sxs-lookup"><span data-stu-id="03b78-115">Resource Disk Management</span></span>
  * <span data-ttu-id="03b78-116">Formatação e montar o disco de recursos de Olá</span><span class="sxs-lookup"><span data-stu-id="03b78-116">Formatting and mounting hello resource disk</span></span>
  * <span data-ttu-id="03b78-117">Configurar o espaço de comutação</span><span class="sxs-lookup"><span data-stu-id="03b78-117">Configuring swap space</span></span>
* <span data-ttu-id="03b78-118">**Redes**</span><span class="sxs-lookup"><span data-stu-id="03b78-118">**Networking**</span></span>
  
  * <span data-ttu-id="03b78-119">Gere as rotas tooimprove compatibilidade com servidores DHCP de plataforma</span><span class="sxs-lookup"><span data-stu-id="03b78-119">Manages routes tooimprove compatibility with platform DHCP servers</span></span>
  * <span data-ttu-id="03b78-120">Garante estabilidade Olá do nome de interface de rede Olá</span><span class="sxs-lookup"><span data-stu-id="03b78-120">Ensures hello stability of hello network interface name</span></span>
* <span data-ttu-id="03b78-121">**Kernel**</span><span class="sxs-lookup"><span data-stu-id="03b78-121">**Kernel**</span></span>
  
  * <span data-ttu-id="03b78-122">Configura o virtual NUMA (desativar kernel < 2.6.37)</span><span class="sxs-lookup"><span data-stu-id="03b78-122">Configures virtual NUMA (disable for kernel <2.6.37)</span></span>
  * <span data-ttu-id="03b78-123">Consome entropia de Hyper-V para /dev/random</span><span class="sxs-lookup"><span data-stu-id="03b78-123">Consumes Hyper-V entropy for /dev/random</span></span>
  * <span data-ttu-id="03b78-124">Configura os tempos limite de SCSI para o dispositivo de raiz de Olá (que pode ser remoto)</span><span class="sxs-lookup"><span data-stu-id="03b78-124">Configures SCSI timeouts for hello root device (which could be remote)</span></span>
* <span data-ttu-id="03b78-125">**Diagnóstico**</span><span class="sxs-lookup"><span data-stu-id="03b78-125">**Diagnostics**</span></span>
  
  * <span data-ttu-id="03b78-126">Consola toohello de redirecionamento porta série</span><span class="sxs-lookup"><span data-stu-id="03b78-126">Console redirection toohello serial port</span></span>
* <span data-ttu-id="03b78-127">**Implementações do SCVMM**</span><span class="sxs-lookup"><span data-stu-id="03b78-127">**SCVMM Deployments**</span></span>
  
  * <span data-ttu-id="03b78-128">Deteta e bootstraps o agente do VMM Olá para Linux quando executado num ambiente do System Center Virtual Machine Manager 2012 R2</span><span class="sxs-lookup"><span data-stu-id="03b78-128">Detects and bootstraps hello VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment</span></span>
* <span data-ttu-id="03b78-129">**Extensão da VM**</span><span class="sxs-lookup"><span data-stu-id="03b78-129">**VM Extension**</span></span>
  
  * <span data-ttu-id="03b78-130">Inserir componentes criados pela Microsoft e parceiros para a automatização de software e configuração de tooenable de VM com Linux (IaaS)</span><span class="sxs-lookup"><span data-stu-id="03b78-130">Inject component authored by Microsoft and Partners into Linux VM (IaaS) tooenable software and configuration automation</span></span>
  * <span data-ttu-id="03b78-131">Implementação de referência de extensão da VM no [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span><span class="sxs-lookup"><span data-stu-id="03b78-131">VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span></span>

## <a name="communication"></a><span data-ttu-id="03b78-132">Comunicação</span><span class="sxs-lookup"><span data-stu-id="03b78-132">Communication</span></span>
<span data-ttu-id="03b78-133">fluxo de informações de Olá Olá plataforma toohello pelo agente ocorre através de dois canais:</span><span class="sxs-lookup"><span data-stu-id="03b78-133">hello information flow from hello platform toohello agent occurs via two channels:</span></span>

* <span data-ttu-id="03b78-134">Um momento do arranque ligados DVD para implementações IaaS.</span><span class="sxs-lookup"><span data-stu-id="03b78-134">A boot-time attached DVD for IaaS deployments.</span></span> <span data-ttu-id="03b78-135">DVD inclui um ficheiro de configuração compatível com OVF, que inclui todas as informações de aprovisionamento que não sejam Olá real keypairs SSH.</span><span class="sxs-lookup"><span data-stu-id="03b78-135">This DVD includes an OVF-compliant configuration file that includes all provisioning information other than hello actual SSH keypairs.</span></span>
* <span data-ttu-id="03b78-136">Um ponto final TCP expor uma API REST utilizado tooobtain implementação e configuração da topologia.</span><span class="sxs-lookup"><span data-stu-id="03b78-136">A TCP endpoint exposing a REST API used tooobtain deployment and topology configuration.</span></span>

## <a name="requirements"></a><span data-ttu-id="03b78-137">Requisitos</span><span class="sxs-lookup"><span data-stu-id="03b78-137">Requirements</span></span>
<span data-ttu-id="03b78-138">Olá sistemas seguintes foram testados e são conhecidos toowork com Olá agente Linux do Azure:</span><span class="sxs-lookup"><span data-stu-id="03b78-138">hello following systems have been tested and are known toowork with hello Azure Linux Agent:</span></span>

> [!NOTE]
> <span data-ttu-id="03b78-139">Esta lista poderá ser diferente da lista oficial do Olá dos sistemas suportados no Olá plataforma do Microsoft Azure, conforme descrito aqui: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span><span class="sxs-lookup"><span data-stu-id="03b78-139">This list may differ from hello official list of supported systems on hello Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span></span>
> 
> 

* <span data-ttu-id="03b78-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="03b78-140">CoreOS</span></span>
* <span data-ttu-id="03b78-141">CentOS 6.3 +</span><span class="sxs-lookup"><span data-stu-id="03b78-141">CentOS 6.3+</span></span>
* <span data-ttu-id="03b78-142">Red Hat Enterprise Linux 6.7 +</span><span class="sxs-lookup"><span data-stu-id="03b78-142">Red Hat Enterprise Linux 6.7+</span></span>
* <span data-ttu-id="03b78-143">Debian 7.0 +</span><span class="sxs-lookup"><span data-stu-id="03b78-143">Debian 7.0+</span></span>
* <span data-ttu-id="03b78-144">Ubuntu 12.04 +</span><span class="sxs-lookup"><span data-stu-id="03b78-144">Ubuntu 12.04+</span></span>
* <span data-ttu-id="03b78-145">openSUSE 12.3 +</span><span class="sxs-lookup"><span data-stu-id="03b78-145">openSUSE 12.3+</span></span>
* <span data-ttu-id="03b78-146">SLES 11 SP3 +</span><span class="sxs-lookup"><span data-stu-id="03b78-146">SLES 11 SP3+</span></span>
* <span data-ttu-id="03b78-147">Oracle Linux 6.4 +</span><span class="sxs-lookup"><span data-stu-id="03b78-147">Oracle Linux 6.4+</span></span>

<span data-ttu-id="03b78-148">Outros sistemas suportados:</span><span class="sxs-lookup"><span data-stu-id="03b78-148">Other Supported Systems:</span></span>

* <span data-ttu-id="03b78-149">FreeBSD 10 + (agente Linux do Azure v2.0.10 +)</span><span class="sxs-lookup"><span data-stu-id="03b78-149">FreeBSD 10+ (Azure Linux Agent v2.0.10+)</span></span>

<span data-ttu-id="03b78-150">agente do Linux Olá depende alguns pacotes de sistema na ordem toofunction corretamente:</span><span class="sxs-lookup"><span data-stu-id="03b78-150">hello Linux agent depends on some system packages in order toofunction properly:</span></span>

* <span data-ttu-id="03b78-151">Python 2.6 +</span><span class="sxs-lookup"><span data-stu-id="03b78-151">Python 2.6+</span></span>
* <span data-ttu-id="03b78-152">OpenSSL 1.0 +</span><span class="sxs-lookup"><span data-stu-id="03b78-152">OpenSSL 1.0+</span></span>
* <span data-ttu-id="03b78-153">OpenSSH 5.3 +</span><span class="sxs-lookup"><span data-stu-id="03b78-153">OpenSSH 5.3+</span></span>
* <span data-ttu-id="03b78-154">Utilitários de sistema de ficheiros: sfdisk fdisk, mkfs, parted</span><span class="sxs-lookup"><span data-stu-id="03b78-154">Filesystem utilities: sfdisk, fdisk, mkfs, parted</span></span>
* <span data-ttu-id="03b78-155">Ferramentas de palavra-passe: chpasswd, sudo</span><span class="sxs-lookup"><span data-stu-id="03b78-155">Password tools: chpasswd, sudo</span></span>
* <span data-ttu-id="03b78-156">Ferramentas de processamento de texto: PO, grep</span><span class="sxs-lookup"><span data-stu-id="03b78-156">Text processing tools: sed, grep</span></span>
* <span data-ttu-id="03b78-157">Ferramentas de rede: rota ip</span><span class="sxs-lookup"><span data-stu-id="03b78-157">Network tools: ip-route</span></span>
* <span data-ttu-id="03b78-158">Suporta kernel para montar a sistemas de ficheiros instalados UDF.</span><span class="sxs-lookup"><span data-stu-id="03b78-158">Kernel support for mounting UDF filesystems.</span></span>

## <a name="installation"></a><span data-ttu-id="03b78-159">Instalação</span><span class="sxs-lookup"><span data-stu-id="03b78-159">Installation</span></span>
<span data-ttu-id="03b78-160">Instalação a utilizar um RPM ou um pacote de DEB no repositório de pacotes a distribuição é o método de Olá preferido de instalação e atualização Olá agente Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="03b78-160">Installation using an RPM or a DEB package from your distribution's package repository is hello preferred method of installing and upgrading hello Azure Linux Agent.</span></span> <span data-ttu-id="03b78-161">Todos os Olá [aprovadas fornecedores de distribuição](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrar o pacote de agente Linux do Azure Olá as imagens e repositórios.</span><span class="sxs-lookup"><span data-stu-id="03b78-161">All hello [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate hello Azure Linux agent package into their images and repositories.</span></span>

<span data-ttu-id="03b78-162">Consulte a documentação do toohello no Olá [repo do agente Linux do Azure no GitHub](https://github.com/Azure/WALinuxAgent) para opções de instalação avançadas, tais como instalar a partir de localizações de origem ou toocustom ou prefixos.</span><span class="sxs-lookup"><span data-stu-id="03b78-162">Refer toohello documentation in hello [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or toocustom locations or prefixes.</span></span>

## <a name="command-line-options"></a><span data-ttu-id="03b78-163">Opções de linha de comandos</span><span class="sxs-lookup"><span data-stu-id="03b78-163">Command Line Options</span></span>
### <a name="flags"></a><span data-ttu-id="03b78-164">Sinalizadores</span><span class="sxs-lookup"><span data-stu-id="03b78-164">Flags</span></span>
* <span data-ttu-id="03b78-165">verboso: aumentar a verbosidade do comando especificado</span><span class="sxs-lookup"><span data-stu-id="03b78-165">verbose: Increase verbosity of specified command</span></span>
* <span data-ttu-id="03b78-166">forçar: Ignorar confirmação interativa para alguns comandos</span><span class="sxs-lookup"><span data-stu-id="03b78-166">force: Skip interactive confirmation for some commands</span></span>

### <a name="commands"></a><span data-ttu-id="03b78-167">Comandos</span><span class="sxs-lookup"><span data-stu-id="03b78-167">Commands</span></span>
* <span data-ttu-id="03b78-168">ajudar: apresenta uma lista de comandos de Olá suportado e sinalizadores.</span><span class="sxs-lookup"><span data-stu-id="03b78-168">help: Lists hello supported commands and flags.</span></span>
* <span data-ttu-id="03b78-169">deprovision: tentativa de sistema de Olá tooclean e torná-lo adequado para o aprovisionamento de novamente.</span><span class="sxs-lookup"><span data-stu-id="03b78-169">deprovision: Attempt tooclean hello system and make it suitable for re-provisioning.</span></span> <span data-ttu-id="03b78-170">Esta operação eliminados seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="03b78-170">This operation deleted hello following:</span></span>
  
  * <span data-ttu-id="03b78-171">Todas as chaves de anfitrião SSH (se Provisioning.RegenerateSshHostKeyPair 'y' no ficheiro de configuração de Olá)</span><span class="sxs-lookup"><span data-stu-id="03b78-171">All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="03b78-172">Configuração de NameServer no /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="03b78-172">Nameserver configuration in /etc/resolv.conf</span></span>
  * <span data-ttu-id="03b78-173">Palavra-passe de raiz do /etc/shadow (se Provisioning.DeleteRootPassword 'y' no ficheiro de configuração de Olá)</span><span class="sxs-lookup"><span data-stu-id="03b78-173">Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="03b78-174">Concessões de cliente DHCP em cache</span><span class="sxs-lookup"><span data-stu-id="03b78-174">Cached DHCP client leases</span></span>
  * <span data-ttu-id="03b78-175">Reposições toolocalhost.localdomain de nome de anfitrião</span><span class="sxs-lookup"><span data-stu-id="03b78-175">Resets host name toolocalhost.localdomain</span></span>

> [!WARNING]
> <span data-ttu-id="03b78-176">Desaprovisionamento garante que dessa imagem Olá é limpa de todas as informações confidenciais e adequado para a redistribuição.</span><span class="sxs-lookup"><span data-stu-id="03b78-176">Deprovisioning does not guarantee that hello image is cleared of all sensitive information and suitable for redistribution.</span></span>
> 
> 

* <span data-ttu-id="03b78-177">deprovision + utilizador: efetua tudo em - deprovision (acima) e também elimina Olá último aprovisionado conta de utilizador (obtida /var/lib/waagent) e dados associados.</span><span class="sxs-lookup"><span data-stu-id="03b78-177">deprovision+user: Performs everything under -deprovision (above) and also deletes hello last provisioned user account (obtained from /var/lib/waagent) and associated data.</span></span> <span data-ttu-id="03b78-178">Este parâmetro é quando uma imagem que foi anteriormente aprovisionamento no Azure, pelo que podem ser capturada e novamente utilizado de aprovisionamento automatizados.</span><span class="sxs-lookup"><span data-stu-id="03b78-178">This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.</span></span>
* <span data-ttu-id="03b78-179">versão: versão de Olá apresenta de waagent</span><span class="sxs-lookup"><span data-stu-id="03b78-179">version: Displays hello version of waagent</span></span>
* <span data-ttu-id="03b78-180">serialconsole: Configura GRUB toomark ttyS0 (Olá a primeira porta série) como a consola de arranque Olá.</span><span class="sxs-lookup"><span data-stu-id="03b78-180">serialconsole: Configures GRUB toomark ttyS0 (hello first serial port) as hello boot console.</span></span> <span data-ttu-id="03b78-181">Isto garante que os registos do kernel lido enviados toothe de porta série e disponibilizados para depuração.</span><span class="sxs-lookup"><span data-stu-id="03b78-181">This ensures that kernel bootup logs are sent toothe serial port and made available for debugging.</span></span>
* <span data-ttu-id="03b78-182">o daemon: executar waagent como uma interação de toomanage daemon com a plataforma de Olá.</span><span class="sxs-lookup"><span data-stu-id="03b78-182">daemon: Run waagent as a daemon toomanage interaction with hello platform.</span></span> <span data-ttu-id="03b78-183">Este argumento é toowaagent especificado no script de init Olá waagent.</span><span class="sxs-lookup"><span data-stu-id="03b78-183">This argument is specified toowaagent in hello waagent init script.</span></span>
* <span data-ttu-id="03b78-184">iniciar: executar waagent como um processo em segundo plano</span><span class="sxs-lookup"><span data-stu-id="03b78-184">start: Run waagent as a background process</span></span>

## <a name="configuration"></a><span data-ttu-id="03b78-185">Configuração</span><span class="sxs-lookup"><span data-stu-id="03b78-185">Configuration</span></span>
<span data-ttu-id="03b78-186">Um ficheiro de configuração (/ etc/waagent.conf) controlos Olá ações de waagent.</span><span class="sxs-lookup"><span data-stu-id="03b78-186">A configuration file (/etc/waagent.conf) controls hello actions of waagent.</span></span> <span data-ttu-id="03b78-187">Um ficheiro de configuração de exemplo é mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="03b78-187">A sample configuration file is shown below:</span></span>

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

<span data-ttu-id="03b78-188">Olá que várias opções de configuração são descritas detalhadamente abaixo.</span><span class="sxs-lookup"><span data-stu-id="03b78-188">hello various configuration options are described in detail below.</span></span> <span data-ttu-id="03b78-189">Opções de configuração são dos três tipos; Valor booleano, cadeia ou número inteiro.</span><span class="sxs-lookup"><span data-stu-id="03b78-189">Configuration options are of three types; Boolean, String or Integer.</span></span> <span data-ttu-id="03b78-190">Opções de configuração booleano Olá podem ser especificadas como "y" ou "n".</span><span class="sxs-lookup"><span data-stu-id="03b78-190">hello Boolean configuration options can be specified as "y" or "n".</span></span> <span data-ttu-id="03b78-191">Olá especial palavra-chave "None" podem ser utilizadas para alguns cadeia tipo entradas de configuração conforme especificado abaixo.</span><span class="sxs-lookup"><span data-stu-id="03b78-191">hello special keyword "None" may be used for some string type configuration entries as detailed below.</span></span>

<span data-ttu-id="03b78-192">**Provisioning.Enabled:**</span><span class="sxs-lookup"><span data-stu-id="03b78-192">**Provisioning.Enabled:**</span></span>  
<span data-ttu-id="03b78-193">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="03b78-193">Type: Boolean</span></span>  
<span data-ttu-id="03b78-194">Predefinição: y</span><span class="sxs-lookup"><span data-stu-id="03b78-194">Default: y</span></span>

<span data-ttu-id="03b78-195">Isto permite Olá utilizador tooenable ou desativar Olá no agente Olá a funcionalidade de aprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="03b78-195">This allows hello user tooenable or disable hello provisioning functionality in hello agent.</span></span> <span data-ttu-id="03b78-196">Os valores válidos são "y" ou "n".</span><span class="sxs-lookup"><span data-stu-id="03b78-196">Valid values are "y" or "n".</span></span> <span data-ttu-id="03b78-197">Se o aprovisionamento estiver desativado, chaves de anfitrião e o utilizador SSH na imagem de Olá são preservadas e qualquer configuração especificada no Olá API de aprovisionamento do Azure é ignorada.</span><span class="sxs-lookup"><span data-stu-id="03b78-197">If provisioning is disabled, SSH host and user keys in hello image are preserved and any configuration specified in hello Azure provisioning API is ignored.</span></span>

> [!NOTE]
> <span data-ttu-id="03b78-198">Olá `Provisioning.Enabled` demasiado "n" no Ubuntu nuvem imagens que utilizam a nuvem init para o aprovisionamento de predefinições de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="03b78-198">hello `Provisioning.Enabled` parameter defaults too"n" on Ubuntu Cloud Images that use cloud-init for provisioning.</span></span>
> 
> 

<span data-ttu-id="03b78-199">**Provisioning.DeleteRootPassword:**</span><span class="sxs-lookup"><span data-stu-id="03b78-199">**Provisioning.DeleteRootPassword:**</span></span>  
<span data-ttu-id="03b78-200">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="03b78-200">Type: Boolean</span></span>  
<span data-ttu-id="03b78-201">Predefinição: n</span><span class="sxs-lookup"><span data-stu-id="03b78-201">Default: n</span></span>

<span data-ttu-id="03b78-202">Se o conjunto de palavra-passe de raiz de Olá no ficheiro Olá etc/sombra é apagado durante Olá o processo de aprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="03b78-202">If set, hello root password in hello /etc/shadow file is erased during hello provisioning process.</span></span>

<span data-ttu-id="03b78-203">**Provisioning.RegenerateSshHostKeyPair:**</span><span class="sxs-lookup"><span data-stu-id="03b78-203">**Provisioning.RegenerateSshHostKeyPair:**</span></span>  
<span data-ttu-id="03b78-204">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="03b78-204">Type: Boolean</span></span>  
<span data-ttu-id="03b78-205">Predefinição: y</span><span class="sxs-lookup"><span data-stu-id="03b78-205">Default: y</span></span>

<span data-ttu-id="03b78-206">Olá, se o conjunto de todos os SSH anfitrião pares de chaves (ecdsa, dsa e rsa) é eliminado durante o processo de aprovisionamento de /etc/hosts ssh /.</span><span class="sxs-lookup"><span data-stu-id="03b78-206">If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during hello provisioning process from /etc/ssh/.</span></span> <span data-ttu-id="03b78-207">E é gerado um par de chaves de raiz único.</span><span class="sxs-lookup"><span data-stu-id="03b78-207">And a single fresh key pair is generated.</span></span>

<span data-ttu-id="03b78-208">tipo de encriptação de Olá par chave de raiz Olá é configurável pelo Olá Provisioning.SshHostKeyPairType entrada.</span><span class="sxs-lookup"><span data-stu-id="03b78-208">hello encryption type for hello fresh key pair is configurable by hello Provisioning.SshHostKeyPairType entry.</span></span> <span data-ttu-id="03b78-209">Tenha em atenção que algumas distribuições recriará pares de chaves SSH para todos os tipos de encriptação em falta quando daemon de SSH Olá é reiniciado (por exemplo, após um reinício).</span><span class="sxs-lookup"><span data-stu-id="03b78-209">Please note that some distributions will re-create SSH key pairs for any missing encryption types when hello SSH daemon is restarted (for example, upon a reboot).</span></span>

<span data-ttu-id="03b78-210">**Provisioning.SshHostKeyPairType:**</span><span class="sxs-lookup"><span data-stu-id="03b78-210">**Provisioning.SshHostKeyPairType:**</span></span>  
<span data-ttu-id="03b78-211">Tipo: Cadeia</span><span class="sxs-lookup"><span data-stu-id="03b78-211">Type: String</span></span>  
<span data-ttu-id="03b78-212">Predefinição: rsa</span><span class="sxs-lookup"><span data-stu-id="03b78-212">Default: rsa</span></span>

<span data-ttu-id="03b78-213">Isto pode ser definido tipo de algoritmos de encriptação tooan que é suportado pelo daemon de SSH Olá na máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="03b78-213">This can be set tooan encryption algorithm type that is supported by hello SSH daemon on hello virtual machine.</span></span> <span data-ttu-id="03b78-214">valores de Olá normalmente suportado são "rsa", "dsa" e "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="03b78-214">hello typically supported values are "rsa", "dsa" and "ecdsa".</span></span> <span data-ttu-id="03b78-215">Tenha em atenção que "putty.exe" no Windows não suporta "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="03b78-215">Note that "putty.exe" on Windows does not support "ecdsa".</span></span> <span data-ttu-id="03b78-216">Por isso, se tenciona toouse putty.exe no Windows tooconnect tooa implementação Linux, utilize "rsa" ou "dsa".</span><span class="sxs-lookup"><span data-stu-id="03b78-216">So, if you intend toouse putty.exe on Windows tooconnect tooa Linux deployment, please use "rsa" or "dsa".</span></span>

<span data-ttu-id="03b78-217">**Provisioning.MonitorHostName:**</span><span class="sxs-lookup"><span data-stu-id="03b78-217">**Provisioning.MonitorHostName:**</span></span>  
<span data-ttu-id="03b78-218">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="03b78-218">Type: Boolean</span></span>  
<span data-ttu-id="03b78-219">Predefinição: y</span><span class="sxs-lookup"><span data-stu-id="03b78-219">Default: y</span></span>

<span data-ttu-id="03b78-220">Se definido, waagent irá monitorizar Olá máquina de virtual com Linux para que as alterações de nome de anfitrião (tal como devolvido pelo comando de "hostname" Olá) e atualizar automaticamente a configuração da rede Olá Olá imagem tooreflect Olá de alterações do.</span><span class="sxs-lookup"><span data-stu-id="03b78-220">If set, waagent will monitor hello Linux virtual machine for hostname changes (as returned by hello "hostname" command) and automatically update hello networking configuration in hello image tooreflect hello change.</span></span> <span data-ttu-id="03b78-221">No nome do ordem toopush Olá alterar toohello servidores DNS, rede será reiniciada na máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="03b78-221">In order toopush hello name change toohello DNS servers, networking will be restarted in hello virtual machine.</span></span> <span data-ttu-id="03b78-222">Este procedimento resultará na brief perda de conectividade à Internet.</span><span class="sxs-lookup"><span data-stu-id="03b78-222">This will result in brief loss of Internet connectivity.</span></span>

<span data-ttu-id="03b78-223">**Provisioning.DecodeCustomData**</span><span class="sxs-lookup"><span data-stu-id="03b78-223">**Provisioning.DecodeCustomData**</span></span>  
<span data-ttu-id="03b78-224">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="03b78-224">Type: Boolean</span></span>  
<span data-ttu-id="03b78-225">Predefinição: n</span><span class="sxs-lookup"><span data-stu-id="03b78-225">Default: n</span></span>

<span data-ttu-id="03b78-226">Se definido, waagent será descodificar CustomData a partir de Base64.</span><span class="sxs-lookup"><span data-stu-id="03b78-226">If set, waagent will decode CustomData from Base64.</span></span>

<span data-ttu-id="03b78-227">**Provisioning.ExecuteCustomData**</span><span class="sxs-lookup"><span data-stu-id="03b78-227">**Provisioning.ExecuteCustomData**</span></span>  
<span data-ttu-id="03b78-228">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="03b78-228">Type: Boolean</span></span>  
<span data-ttu-id="03b78-229">Predefinição: n</span><span class="sxs-lookup"><span data-stu-id="03b78-229">Default: n</span></span>

<span data-ttu-id="03b78-230">Se definido, waagent executará CustomData após o aprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="03b78-230">If set, waagent will execute CustomData after provisioning.</span></span>

<span data-ttu-id="03b78-231">**Provisioning.PasswordCryptId**</span><span class="sxs-lookup"><span data-stu-id="03b78-231">**Provisioning.PasswordCryptId**</span></span>  
<span data-ttu-id="03b78-232">Tipo: cadeia</span><span class="sxs-lookup"><span data-stu-id="03b78-232">Type:String</span></span>  
<span data-ttu-id="03b78-233">Predefinição: 6</span><span class="sxs-lookup"><span data-stu-id="03b78-233">Default:6</span></span>

<span data-ttu-id="03b78-234">Algoritmo utilizado pela crypt ao gerar o hash de palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="03b78-234">Algorithm used by crypt when generating password hash.</span></span>  
 <span data-ttu-id="03b78-235">1 - MD5</span><span class="sxs-lookup"><span data-stu-id="03b78-235">1 - MD5</span></span>  
 <span data-ttu-id="03b78-236">2a - Blowfish</span><span class="sxs-lookup"><span data-stu-id="03b78-236">2a - Blowfish</span></span>  
 <span data-ttu-id="03b78-237">5 - SHA-256</span><span class="sxs-lookup"><span data-stu-id="03b78-237">5 - SHA-256</span></span>  
 <span data-ttu-id="03b78-238">6 - SHA-512</span><span class="sxs-lookup"><span data-stu-id="03b78-238">6 - SHA-512</span></span>  

<span data-ttu-id="03b78-239">**Provisioning.PasswordCryptSaltLength**</span><span class="sxs-lookup"><span data-stu-id="03b78-239">**Provisioning.PasswordCryptSaltLength**</span></span>  
<span data-ttu-id="03b78-240">Tipo: cadeia</span><span class="sxs-lookup"><span data-stu-id="03b78-240">Type:String</span></span>  
<span data-ttu-id="03b78-241">Predefinição: 10</span><span class="sxs-lookup"><span data-stu-id="03b78-241">Default:10</span></span>

<span data-ttu-id="03b78-242">Comprimento de salt aleatório utilizado ao gerar o hash de palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="03b78-242">Length of random salt used when generating password hash.</span></span>

<span data-ttu-id="03b78-243">**ResourceDisk.Format:**</span><span class="sxs-lookup"><span data-stu-id="03b78-243">**ResourceDisk.Format:**</span></span>  
<span data-ttu-id="03b78-244">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="03b78-244">Type: Boolean</span></span>  
<span data-ttu-id="03b78-245">Predefinição: y</span><span class="sxs-lookup"><span data-stu-id="03b78-245">Default: y</span></span>

<span data-ttu-id="03b78-246">Se definido, disco de recursos de Olá fornecido pela plataforma de Olá será formatado e montado pelas waagent se o tipo de sistema de ficheiros de Olá pedido pelo utilizador Olá "ResourceDisk.Filesystem" é diferente de "ntfs".</span><span class="sxs-lookup"><span data-stu-id="03b78-246">If set, hello resource disk provided by hello platform will be formatted and mounted by waagent if hello filesystem type requested by hello user in "ResourceDisk.Filesystem" is anything other than "ntfs".</span></span> <span data-ttu-id="03b78-247">Uma única partição do tipo Linux (83) será disponibilizada no disco Olá.</span><span class="sxs-lookup"><span data-stu-id="03b78-247">A single partition of type Linux (83) will be made available on hello disk.</span></span> <span data-ttu-id="03b78-248">Tenha em atenção que esta partição não será formatada se podem ser montados com êxito.</span><span class="sxs-lookup"><span data-stu-id="03b78-248">Note that this partition will not be formatted if it can be successfully mounted.</span></span>

<span data-ttu-id="03b78-249">**ResourceDisk.Filesystem:**</span><span class="sxs-lookup"><span data-stu-id="03b78-249">**ResourceDisk.Filesystem:**</span></span>  
<span data-ttu-id="03b78-250">Tipo: Cadeia</span><span class="sxs-lookup"><span data-stu-id="03b78-250">Type: String</span></span>  
<span data-ttu-id="03b78-251">Predefinição: ext4</span><span class="sxs-lookup"><span data-stu-id="03b78-251">Default: ext4</span></span>

<span data-ttu-id="03b78-252">Esta ação Especifica o tipo de sistema de ficheiros de Olá para o disco de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="03b78-252">This specifies hello filesystem type for hello resource disk.</span></span> <span data-ttu-id="03b78-253">Os valores suportados variam consoante a distribuição de Linux.</span><span class="sxs-lookup"><span data-stu-id="03b78-253">Supported values vary by Linux distribution.</span></span> <span data-ttu-id="03b78-254">Se a cadeia de Olá é X, em seguida, mkfs. X deve estar presente na imagem de Linux Olá.</span><span class="sxs-lookup"><span data-stu-id="03b78-254">If hello string is X, then mkfs.X should be present on hello Linux image.</span></span> <span data-ttu-id="03b78-255">SLES 11 imagens, normalmente, devem utilizar 'ext3'.</span><span class="sxs-lookup"><span data-stu-id="03b78-255">SLES 11 images should typically use 'ext3'.</span></span> <span data-ttu-id="03b78-256">Imagens de FreeBSD devem utilizar aqui 'ufs2'.</span><span class="sxs-lookup"><span data-stu-id="03b78-256">FreeBSD images should use 'ufs2' here.</span></span>

<span data-ttu-id="03b78-257">**ResourceDisk.MountPoint:**</span><span class="sxs-lookup"><span data-stu-id="03b78-257">**ResourceDisk.MountPoint:**</span></span>  
<span data-ttu-id="03b78-258">Tipo: Cadeia</span><span class="sxs-lookup"><span data-stu-id="03b78-258">Type: String</span></span>  
<span data-ttu-id="03b78-259">Predefinição: recursos/mnt /</span><span class="sxs-lookup"><span data-stu-id="03b78-259">Default: /mnt/resource</span></span> 

<span data-ttu-id="03b78-260">Esta ação Especifica o caminho de Olá que Olá recurso disco se encontra instalado.</span><span class="sxs-lookup"><span data-stu-id="03b78-260">This specifies hello path at which hello resource disk is mounted.</span></span> <span data-ttu-id="03b78-261">Tenha em atenção de que esse disco de recursos de Olá é um *temporário* disco e poderá ser esvaziada quando Olá VM é desaprovisionada.</span><span class="sxs-lookup"><span data-stu-id="03b78-261">Note that hello resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span>

<span data-ttu-id="03b78-262">**ResourceDisk.MountOptions**</span><span class="sxs-lookup"><span data-stu-id="03b78-262">**ResourceDisk.MountOptions**</span></span>  
<span data-ttu-id="03b78-263">Tipo: Cadeia</span><span class="sxs-lookup"><span data-stu-id="03b78-263">Type: String</span></span>  
<span data-ttu-id="03b78-264">Predefinição: nenhuma</span><span class="sxs-lookup"><span data-stu-id="03b78-264">Default: None</span></span>

<span data-ttu-id="03b78-265">Especifica o disco montagem opções toobe transmitido toohello montagem -o comando.</span><span class="sxs-lookup"><span data-stu-id="03b78-265">Specifies disk mount options toobe passed toohello mount -o command.</span></span> <span data-ttu-id="03b78-266">Esta é uma lista separada por vírgulas de valores, por ex.</span><span class="sxs-lookup"><span data-stu-id="03b78-266">This is a comma separated list of values, ex.</span></span> <span data-ttu-id="03b78-267">'nodev, nosuid'.</span><span class="sxs-lookup"><span data-stu-id="03b78-267">'nodev,nosuid'.</span></span> <span data-ttu-id="03b78-268">Consulte mount(8) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="03b78-268">See mount(8) for details.</span></span>

<span data-ttu-id="03b78-269">**ResourceDisk.EnableSwap:**</span><span class="sxs-lookup"><span data-stu-id="03b78-269">**ResourceDisk.EnableSwap:**</span></span>  
<span data-ttu-id="03b78-270">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="03b78-270">Type: Boolean</span></span>  
<span data-ttu-id="03b78-271">Predefinição: n</span><span class="sxs-lookup"><span data-stu-id="03b78-271">Default: n</span></span>

<span data-ttu-id="03b78-272">Se definir um ficheiro de comutação (/ swapfile) é criado no disco de recursos de Olá e adicionar espaço de comutação do sistema toohello.</span><span class="sxs-lookup"><span data-stu-id="03b78-272">If set, a swap file (/swapfile) is created on hello resource disk and added toohello system swap space.</span></span>

<span data-ttu-id="03b78-273">**ResourceDisk.SwapSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="03b78-273">**ResourceDisk.SwapSizeMB:**</span></span>  
<span data-ttu-id="03b78-274">Tipo: número inteiro</span><span class="sxs-lookup"><span data-stu-id="03b78-274">Type: Integer</span></span>  
<span data-ttu-id="03b78-275">Predefinição: 0</span><span class="sxs-lookup"><span data-stu-id="03b78-275">Default: 0</span></span>

<span data-ttu-id="03b78-276">tamanho de Olá do ficheiro de comutação Olá em megabytes.</span><span class="sxs-lookup"><span data-stu-id="03b78-276">hello size of hello swap file in megabytes.</span></span>

<span data-ttu-id="03b78-277">**Logs.Verbose:**</span><span class="sxs-lookup"><span data-stu-id="03b78-277">**Logs.Verbose:**</span></span>  
<span data-ttu-id="03b78-278">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="03b78-278">Type: Boolean</span></span>  
<span data-ttu-id="03b78-279">Predefinição: n</span><span class="sxs-lookup"><span data-stu-id="03b78-279">Default: n</span></span>

<span data-ttu-id="03b78-280">Se o conjunto de verbosidade do registo é elevado.</span><span class="sxs-lookup"><span data-stu-id="03b78-280">If set, log verbosity is boosted.</span></span> <span data-ttu-id="03b78-281">Waagent regista too/var/log/waagent.log e tira partido Olá logrotate funcionalidade toorotate os registos de sistema.</span><span class="sxs-lookup"><span data-stu-id="03b78-281">Waagent logs too/var/log/waagent.log and leverages hello system logrotate functionality toorotate logs.</span></span>

<span data-ttu-id="03b78-282">**SO. EnableRDMA**</span><span class="sxs-lookup"><span data-stu-id="03b78-282">**OS.EnableRDMA**</span></span>  
<span data-ttu-id="03b78-283">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="03b78-283">Type: Boolean</span></span>  
<span data-ttu-id="03b78-284">Predefinição: n</span><span class="sxs-lookup"><span data-stu-id="03b78-284">Default: n</span></span>

<span data-ttu-id="03b78-285">Se definido, agente Olá irá tentar tooinstall e, em seguida, carregar um controlador de kernel RDMA que corresponde à versão de Olá do firmware de Olá do Olá subjacente hardware.</span><span class="sxs-lookup"><span data-stu-id="03b78-285">If set, hello agent will attempt tooinstall and then load an RDMA kernel driver that matches hello version of hello firmware on hello underlying hardware.</span></span>

<span data-ttu-id="03b78-286">**SO. RootDeviceScsiTimeout:**</span><span class="sxs-lookup"><span data-stu-id="03b78-286">**OS.RootDeviceScsiTimeout:**</span></span>  
<span data-ttu-id="03b78-287">Tipo: número inteiro</span><span class="sxs-lookup"><span data-stu-id="03b78-287">Type: Integer</span></span>  
<span data-ttu-id="03b78-288">Predefinição: 300</span><span class="sxs-lookup"><span data-stu-id="03b78-288">Default: 300</span></span>

<span data-ttu-id="03b78-289">Esta ação configura o tempo limite de SCSI Olá em segundos em unidades de disco e os dados de Olá SO.</span><span class="sxs-lookup"><span data-stu-id="03b78-289">This configures hello SCSI timeout in seconds on hello OS disk and data drives.</span></span> <span data-ttu-id="03b78-290">Se não for definido, sistema hello são utilizadas as predefinições.</span><span class="sxs-lookup"><span data-stu-id="03b78-290">If not set, hello system defaults are used.</span></span>

<span data-ttu-id="03b78-291">**SO. OpensslPath:**</span><span class="sxs-lookup"><span data-stu-id="03b78-291">**OS.OpensslPath:**</span></span>  
<span data-ttu-id="03b78-292">Tipo: Cadeia</span><span class="sxs-lookup"><span data-stu-id="03b78-292">Type: String</span></span>  
<span data-ttu-id="03b78-293">Predefinição: nenhuma</span><span class="sxs-lookup"><span data-stu-id="03b78-293">Default: None</span></span>

<span data-ttu-id="03b78-294">Isto pode ser utilizado toospecify um caminho alternativo para Olá toouse binário do openssl para operações de criptografia.</span><span class="sxs-lookup"><span data-stu-id="03b78-294">This can be used toospecify an alternate path for hello openssl binary toouse for cryptographic operations.</span></span>

<span data-ttu-id="03b78-295">**HttpProxy.Host, HttpProxy.Port**</span><span class="sxs-lookup"><span data-stu-id="03b78-295">**HttpProxy.Host, HttpProxy.Port**</span></span>  
<span data-ttu-id="03b78-296">Tipo: Cadeia</span><span class="sxs-lookup"><span data-stu-id="03b78-296">Type: String</span></span>  
<span data-ttu-id="03b78-297">Predefinição: nenhuma</span><span class="sxs-lookup"><span data-stu-id="03b78-297">Default: None</span></span>

<span data-ttu-id="03b78-298">Se definido, Olá agente irá utilizar este proxy server tooaccess Olá internet.</span><span class="sxs-lookup"><span data-stu-id="03b78-298">If set, hello agent will use this proxy server tooaccess hello internet.</span></span> 

## <a name="ubuntu-cloud-images"></a><span data-ttu-id="03b78-299">Ubuntu nuvem imagens</span><span class="sxs-lookup"><span data-stu-id="03b78-299">Ubuntu Cloud Images</span></span>
<span data-ttu-id="03b78-300">Tenha em atenção que utilizar imagens de nuvem Ubuntu [nuvem init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform Olá de muitas tarefas de configuração que caso contrário, teriam de ser geridas pelo agente Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="03b78-300">Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform many configuration tasks that would otherwise be managed by hello Azure Linux Agent.</span></span>  <span data-ttu-id="03b78-301">Tenha em atenção Olá seguintes diferenças:</span><span class="sxs-lookup"><span data-stu-id="03b78-301">Please note hello following differences:</span></span>

* <span data-ttu-id="03b78-302">**Provisioning.Enabled** predefinições demasiado "n" no Ubuntu nuvem imagens que utilizam tooperform nuvem init aprovisionamento tarefas.</span><span class="sxs-lookup"><span data-stu-id="03b78-302">**Provisioning.Enabled** defaults too"n" on Ubuntu Cloud Images that use cloud-init tooperform provisioning tasks.</span></span>
* <span data-ttu-id="03b78-303">Olá seguir os parâmetros de configuração não tem qualquer efeito nas imagens de nuvem Ubuntu que utilizam nuvem init toomanage Olá recurso disco e a comutação espaço:</span><span class="sxs-lookup"><span data-stu-id="03b78-303">hello following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init toomanage hello resource disk and swap space:</span></span>
  
  * <span data-ttu-id="03b78-304">**ResourceDisk.Format**</span><span class="sxs-lookup"><span data-stu-id="03b78-304">**ResourceDisk.Format**</span></span>
  * <span data-ttu-id="03b78-305">**ResourceDisk.Filesystem**</span><span class="sxs-lookup"><span data-stu-id="03b78-305">**ResourceDisk.Filesystem**</span></span>
  * <span data-ttu-id="03b78-306">**ResourceDisk.MountPoint**</span><span class="sxs-lookup"><span data-stu-id="03b78-306">**ResourceDisk.MountPoint**</span></span>
  * <span data-ttu-id="03b78-307">**ResourceDisk.EnableSwap**</span><span class="sxs-lookup"><span data-stu-id="03b78-307">**ResourceDisk.EnableSwap**</span></span>
  * <span data-ttu-id="03b78-308">**ResourceDisk.SwapSizeMB**</span><span class="sxs-lookup"><span data-stu-id="03b78-308">**ResourceDisk.SwapSizeMB**</span></span>
* <span data-ttu-id="03b78-309">. Consulte Olá seguir o ponto de montagem do disco de recursos do recursos tooconfigure Olá e espaço no Ubuntu nuvem imagens de comutação durante o aprovisionamento:</span><span class="sxs-lookup"><span data-stu-id="03b78-309">Please see hello following resources tooconfigure hello resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:</span></span>
  
  * [<span data-ttu-id="03b78-310">Ubuntu Wiki: Configurar partições de comutação</span><span class="sxs-lookup"><span data-stu-id="03b78-310">Ubuntu Wiki: Configure Swap Partitions</span></span>](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [<span data-ttu-id="03b78-311">Dados personalizados inserirem-se para uma Máquina Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="03b78-311">Injecting Custom Data into an Azure Virtual Machine</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

