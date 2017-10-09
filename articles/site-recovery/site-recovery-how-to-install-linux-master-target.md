---
title: "aaaHow tooinstall um servidor de destino principal do Linux para ativação pós-falha do local tooon do Azure | Microsoft Docs"
description: "Antes de trocar uma máquina virtual Linux, precisa de um servidor de destino principal do Linux. Saiba como tooinstall um."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a><span data-ttu-id="80165-104">Instalar um servidor de destino principal do Linux</span><span class="sxs-lookup"><span data-stu-id="80165-104">Install a Linux master target server</span></span>
<span data-ttu-id="80165-105">Após a ativação pós-falha de máquinas virtuais, pode efetuar a site no local do back-Olá máquinas virtuais toohello.</span><span class="sxs-lookup"><span data-stu-id="80165-105">After you fail over your virtual machines, you can fail back hello virtual machines toohello on-premises site.</span></span> <span data-ttu-id="80165-106">toofail novamente, terá de tooreprotect Olá excluir máquina virtual de site do Azure toohello no local.</span><span class="sxs-lookup"><span data-stu-id="80165-106">toofail back, you need tooreprotect hello virtual machine from Azure toohello on-premises site.</span></span> <span data-ttu-id="80165-107">Para que este processo, tem um tráfego de Olá tooreceive de servidor de destino principal de no local.</span><span class="sxs-lookup"><span data-stu-id="80165-107">For this process, you need an on-premises master target server tooreceive hello traffic.</span></span> 

<span data-ttu-id="80165-108">Se a máquina virtual protegida é uma máquina virtual do Windows, em seguida, é necessário um destino principal do Windows.</span><span class="sxs-lookup"><span data-stu-id="80165-108">If your protected virtual machine is a Windows virtual machine, then you need a Windows master target.</span></span> <span data-ttu-id="80165-109">Para uma máquina virtual do Linux, tem um destino principal do Linux.</span><span class="sxs-lookup"><span data-stu-id="80165-109">For a Linux virtual machine, you need a Linux master target.</span></span> <span data-ttu-id="80165-110">Seguinte de Olá leitura passos toolearn como toocreate e instale um Linux destino mestre.</span><span class="sxs-lookup"><span data-stu-id="80165-110">Read hello following steps toolearn how toocreate and install a Linux master target.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80165-111">A partir da versão do servidor de destino mestre Olá 9.10.0, servidor de destino mestre Olá mais recente pode ser apenas instalado num servidor Ubuntu 16.04.</span><span class="sxs-lookup"><span data-stu-id="80165-111">Starting with release of hello 9.10.0 master target server, hello latest master target server can be only installed on an Ubuntu 16.04 server.</span></span> <span data-ttu-id="80165-112">Novas instalações não são permitidas em CentOS6.6 servidores.</span><span class="sxs-lookup"><span data-stu-id="80165-112">New installations aren't allowed on  CentOS6.6 servers.</span></span> <span data-ttu-id="80165-113">No entanto, pode continuar tooupgrade os servidores de destino mestre antigo utilizando Olá 9.10.0 versão.</span><span class="sxs-lookup"><span data-stu-id="80165-113">However, you can continue tooupgrade your old master target servers by using hello 9.10.0 version.</span></span>

## <a name="overview"></a><span data-ttu-id="80165-114">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="80165-114">Overview</span></span>
<span data-ttu-id="80165-115">Este artigo fornece instruções sobre como tooinstall um Linux mestre de destino.</span><span class="sxs-lookup"><span data-stu-id="80165-115">This article provides instructions for how tooinstall a Linux master target.</span></span>

<span data-ttu-id="80165-116">Publique comentários ou perguntas na end Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="80165-116">Post comments or questions at hello end of this article or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80165-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="80165-117">Prerequisites</span></span>

* <span data-ttu-id="80165-118">anfitrião de Olá toochoose que toodeploy Olá destino principal, determinar se a reativação pós-falha da Olá é vai toobe tooan existente no local da máquina virtual ou máquina virtual nova do tooa.</span><span class="sxs-lookup"><span data-stu-id="80165-118">toochoose hello host on which toodeploy hello master target, determine if hello failback is going toobe tooan existing on-premises virtual machine or tooa new virtual machine.</span></span> 
    * <span data-ttu-id="80165-119">Para uma máquina virtual existente, o anfitrião Olá de destino mestre Olá deve ter acesso toohello arquivos de dados da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-119">For an existing virtual machine, hello host of hello master target should have access toohello data stores of hello virtual machine.</span></span>
    * <span data-ttu-id="80165-120">Se a máquina de virtual Olá no local não existe, Olá máquinas de reativação pós-falha é criada no Olá mesmo anfitrião como destino mestre Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-120">If hello on-premises virtual machine does not exist, hello failback virtual machine is created on hello same host as hello master target.</span></span> <span data-ttu-id="80165-121">Pode escolher qualquer anfitrião ESXi destino principal do tooinstall Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-121">You can choose any ESXi host tooinstall hello master target.</span></span>
* <span data-ttu-id="80165-122">o destino principal Olá deve estar numa rede que possa comunicar com o servidor de processos de Olá e o servidor de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-122">hello master target should be on a network that can communicate with hello process server and hello configuration server.</span></span>
* <span data-ttu-id="80165-123">Olá versão de destino mestre Olá tem de ser igual tooor anteriores ao hello as versões do servidor de processos de Olá e servidor de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-123">hello version of hello master target must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="80165-124">Por exemplo, se versão hello do servidor de configuração de Olá 9.4, versão de Olá do destino principal Olá possa ser 9.4 ou 9.3 mas não 9.5.</span><span class="sxs-lookup"><span data-stu-id="80165-124">For example, if hello version of hello configuration server is 9.4, hello version of hello master target can be 9.4 or 9.3 but not 9.5.</span></span>
* <span data-ttu-id="80165-125">só pode ser o destino principal Olá uma máquina virtual VMware e não um servidor físico.</span><span class="sxs-lookup"><span data-stu-id="80165-125">hello master target can only be a VMware virtual machine and not a physical server.</span></span>

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a><span data-ttu-id="80165-126">Criar o destino principal Olá de acordo com toohello diretrizes de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="80165-126">Create hello master target according toohello sizing guidelines</span></span>

<span data-ttu-id="80165-127">Crie o destino principal do Olá em conformidade com as seguintes diretrizes de dimensionamento de Olá:</span><span class="sxs-lookup"><span data-stu-id="80165-127">Create hello master target in accordance with hello following sizing guidelines:</span></span>
- <span data-ttu-id="80165-128">**RAM**: 6 GB ou mais</span><span class="sxs-lookup"><span data-stu-id="80165-128">**RAM**: 6 GB or more</span></span>
- <span data-ttu-id="80165-129">**Tamanho do disco de SO**: 100 GB ou mais (tooinstall CentOS6.6)</span><span class="sxs-lookup"><span data-stu-id="80165-129">**OS disk size**: 100 GB or more (tooinstall CentOS6.6)</span></span>
- <span data-ttu-id="80165-130">**Tamanho de disco adicional para a unidade de retenção**: 1 TB</span><span class="sxs-lookup"><span data-stu-id="80165-130">**Additional disk size for retention drive**: 1 TB</span></span>
- <span data-ttu-id="80165-131">**Núcleos de CPU**: 4 núcleos ou mais</span><span class="sxs-lookup"><span data-stu-id="80165-131">**CPU cores**: 4 cores or more</span></span>

<span data-ttu-id="80165-132">seguinte Olá suportado Ubuntu kernels são suportados.</span><span class="sxs-lookup"><span data-stu-id="80165-132">hello following supported Ubuntu kernels are supported.</span></span>


|<span data-ttu-id="80165-133">Série de kernel</span><span class="sxs-lookup"><span data-stu-id="80165-133">Kernel Series</span></span>  |<span data-ttu-id="80165-134">Suporta segurança demasiado</span><span class="sxs-lookup"><span data-stu-id="80165-134">Support up too</span></span> |
|---------|---------|
|<span data-ttu-id="80165-135">4.4</span><span class="sxs-lookup"><span data-stu-id="80165-135">4.4</span></span>      |<span data-ttu-id="80165-136">4.4.0-81-Generic</span><span class="sxs-lookup"><span data-stu-id="80165-136">4.4.0-81-generic</span></span>         |
|<span data-ttu-id="80165-137">4.8</span><span class="sxs-lookup"><span data-stu-id="80165-137">4.8</span></span>      |<span data-ttu-id="80165-138">4.8.0-56-Generic</span><span class="sxs-lookup"><span data-stu-id="80165-138">4.8.0-56-generic</span></span>         |
|<span data-ttu-id="80165-139">4.10</span><span class="sxs-lookup"><span data-stu-id="80165-139">4.10</span></span>     |<span data-ttu-id="80165-140">4.10.0-24-Generic</span><span class="sxs-lookup"><span data-stu-id="80165-140">4.10.0-24-generic</span></span>        |


## <a name="deploy-hello-master-target-server"></a><span data-ttu-id="80165-141">Implementar o servidor de destino mestre Olá</span><span class="sxs-lookup"><span data-stu-id="80165-141">Deploy hello master target server</span></span>

### <a name="install-ubuntu-16042-minimal"></a><span data-ttu-id="80165-142">Instalar Ubuntu 16.04.2 mínima</span><span class="sxs-lookup"><span data-stu-id="80165-142">Install Ubuntu 16.04.2 Minimal</span></span>

<span data-ttu-id="80165-143">Demorar Olá os seguintes passos Olá tooinstall Olá Ubuntu 16.04.2 64 bits da sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="80165-143">Take hello following hello steps tooinstall hello Ubuntu 16.04.2 64-bit operating system.</span></span>

<span data-ttu-id="80165-144">**Passo 1:** aceda toohello [transferir ligação](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) e escolha espelho mais próximo Olá dos quais transferir um ficheiro Ubuntu 16.04.2 mínimo 64-bit ISO.</span><span class="sxs-lookup"><span data-stu-id="80165-144">**Step 1:** Go toohello [download link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) and choose hello closest mirror from which download an Ubuntu 16.04.2 minimal 64-bit ISO.</span></span>

<span data-ttu-id="80165-145">Manter um ficheiro Ubuntu 16.04.2 mínimo 64-bit ISO na unidade de DVD de Olá e iniciar Olá sistema.</span><span class="sxs-lookup"><span data-stu-id="80165-145">Keep an Ubuntu 16.04.2 minimal 64-bit ISO in hello DVD drive and start hello system.</span></span>

<span data-ttu-id="80165-146">**Passo 2:** selecione **inglês** como linguagem preferencial e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="80165-146">**Step 2:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Selecione uma Linguagem](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

<span data-ttu-id="80165-148">**Passo 3:** selecione **instalar Ubuntu Server**e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="80165-148">**Step 3:** Select **Install Ubuntu Server**, and then select **Enter**.</span></span>

![Selecione instalar Ubuntu Server](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

<span data-ttu-id="80165-150">**Passo 4:** selecione **inglês** como linguagem preferencial e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="80165-150">**Step 4:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Selecione inglês como o idioma preferencial](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

<span data-ttu-id="80165-152">**Passo 5:** Olá, selecione a opção adequada de Olá **fuso horário** lista de opções e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="80165-152">**Step 5:** Select hello appropriate option from hello **Time Zone** options list, and then select **Enter**.</span></span>

![Selecione o fuso horário corretos Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

<span data-ttu-id="80165-154">**Passo 6:** selecione **não** (hello a opção predefinida) e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="80165-154">**Step 6:** Select **No** (hello default option), and then select **Enter**.</span></span>


![Configurar o teclado Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

<span data-ttu-id="80165-156">**Passo 7:** selecione **inglês (EUA)** como Olá país de origem para o teclado Olá e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="80165-156">**Step 7:** Select **English (US)** as hello country of origin for hello keyboard, and then select **Enter**.</span></span>

![Selecione E.U.A. como país Olá de origem](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

<span data-ttu-id="80165-158">**Passo 8:** selecione **inglês (EUA)** como o esquema do teclado Olá e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="80165-158">**Step 8:** Select **English (US)** as hello keyboard layout, and then select **Enter**.</span></span>

![Selecione inglês como o esquema do teclado Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

<span data-ttu-id="80165-160">**Passo 9:** introduza Olá nome de anfitrião para o servidor no Olá **Hostname** caixa e, em seguida, selecione **continuar**.</span><span class="sxs-lookup"><span data-stu-id="80165-160">**Step 9:** Enter hello hostname for your server in hello **Hostname** box, and then select **Continue**.</span></span>

![Introduza o nome de anfitrião Olá para o servidor](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

<span data-ttu-id="80165-162">**Passo 10:** toocreate uma conta de utilizador, introduza o nome de utilizador Olá e, em seguida, selecione **continuar**.</span><span class="sxs-lookup"><span data-stu-id="80165-162">**Step 10:** toocreate a user account, enter hello user name, and then select **Continue**.</span></span>

![Criar uma conta de utilizador](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

<span data-ttu-id="80165-164">**Passo 11:** introduza a palavra-passe de Olá Olá nova conta de utilizador e, em seguida, selecione **continuar**.</span><span class="sxs-lookup"><span data-stu-id="80165-164">**Step 11:** Enter hello password for hello new user account, and then select **Continue**.</span></span>

![Introduza a palavra-passe de Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

<span data-ttu-id="80165-166">**Passo 12:** confirme Olá palavra-passe do utilizador novo Olá e, em seguida, selecione **continuar**.</span><span class="sxs-lookup"><span data-stu-id="80165-166">**Step 12:** Confirm hello password for hello new user, and then select **Continue**.</span></span>

![Confirme as palavras-passe de Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

<span data-ttu-id="80165-168">**Passo 13:** selecione **não** (hello a opção predefinida) e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="80165-168">**Step 13:** Select **No** (hello default option), and then select **Enter**.</span></span>

![Configurar utilizadores e palavras-passe](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

<span data-ttu-id="80165-170">**Passo 14:** se Olá fuso horário que é apresentado está correto, selecione **Sim** (hello a opção predefinida) e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="80165-170">**Step 14:** If hello time zone that's displayed is correct, select **Yes** (hello default option), and then select **Enter**.</span></span>

<span data-ttu-id="80165-171">tooreconfigure seu fuso horário, selecione **não**.</span><span class="sxs-lookup"><span data-stu-id="80165-171">tooreconfigure your time zone, select **No**.</span></span>

![Configure o relógio Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

<span data-ttu-id="80165-173">**Passo 15:** na Olá opções de método de criação de partições, selecione **orientado - a utilizar o disco completo**e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="80165-173">**Step 15:** From hello partitioning method options, select **Guided - use entire disk**, and then select **Enter**.</span></span>

![Selecione a opção de método de criação de partições de Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

<span data-ttu-id="80165-175">**Passo 16:** Olá, selecione um disco apropriado de Olá **selecionar disco toopartition** opções e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="80165-175">**Step 16:** Select hello appropriate disk from hello **Select disk toopartition** options, and then select **Enter**.</span></span>


![Selecione o disco de Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

<span data-ttu-id="80165-177">**Passo 17:** selecione **Sim** toowrite Olá toodisk de alterações e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="80165-177">**Step 17:** Select **Yes** toowrite hello changes toodisk, and then select **Enter**.</span></span>

![Escrever Olá alterações toodisk](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

<span data-ttu-id="80165-179">**Passo 18:** selecione a opção predefinida de Olá, selecione **continuar**e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="80165-179">**Step 18:** Select hello default option, select **Continue**, and then select **Enter**.</span></span>

![Selecione a opção predefinida de Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

<span data-ttu-id="80165-181">**Passo 19:** selecionar Olá a opção adequada para a gestão de atualizações no seu sistema e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="80165-181">**Step 19:** Select hello appropriate option for managing upgrades on your system, and then select **Enter**.</span></span>

![Selecione a forma como toomanage atualiza](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> <span data-ttu-id="80165-183">Porque o servidor de destino principal do Azure Site Recovery Olá requer uma versão muito específica do Olá Ubuntu, terá de tooensure que kernel Olá atualizações estão desativadas para a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-183">Because hello Azure Site Recovery master target server requires a very specific version of hello Ubuntu, you need tooensure that hello kernel upgrades are disabled for hello virtual machine.</span></span> <span data-ttu-id="80165-184">Se estes estiverem ativadas, as atualizações regulares causam toomalfunction de servidor de destino mestre Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-184">If they are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span> <span data-ttu-id="80165-185">Certifique-se de que seleciona Olá **sem as atualizações automáticas** opção.</span><span class="sxs-lookup"><span data-stu-id="80165-185">Make sure you select hello **No automatic updates** option.</span></span>


<span data-ttu-id="80165-186">**Passo 20:** Selecionar opções predefinidas.</span><span class="sxs-lookup"><span data-stu-id="80165-186">**Step 20:** Select default options.</span></span> <span data-ttu-id="80165-187">Se quiser openSSH para estabelecer a ligação SSH, selecione Olá **OpenSSH servidor** opção e, em seguida, selecione **continuar**.</span><span class="sxs-lookup"><span data-stu-id="80165-187">If you want openSSH for SSH connect, select hello **OpenSSH server** option, and then select **Continue**.</span></span>

![Selecione o software](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

<span data-ttu-id="80165-189">**Passo 21:** selecione **Sim**e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="80165-189">**Step 21:** Select **Yes**, and then select **Enter**.</span></span>

![Carregador de arranque do instalação Olá GRUB](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

<span data-ttu-id="80165-191">**Passo 22:** selecione Olá dispositivos adequada para a instalação do carregador de arranque de Olá (preferencialmente, **/dev/sda**) e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="80165-191">**Step 22:** Select hello appropriate device for hello boot loader installation (preferably **/dev/sda**), and then select **Enter**.</span></span>

![Selecione um dispositivo para a instalação do carregador de arranque](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

<span data-ttu-id="80165-193">**Passo 23:** selecione **continuar**e, em seguida, selecione **Enter** instalação de Olá toofinish.</span><span class="sxs-lookup"><span data-stu-id="80165-193">**Step 23:** Select **Continue**, and then select **Enter** toofinish hello installation.</span></span>

![Concluir a instalação de Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

<span data-ttu-id="80165-195">Após concluir a instalação de Olá, inicie sessão toohello VM com as credenciais de utilizador novo Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-195">After hello installation has finished, sign in toohello VM with hello new user credentials.</span></span> <span data-ttu-id="80165-196">(Consulte demasiado**passo 10** para obter mais informações.)</span><span class="sxs-lookup"><span data-stu-id="80165-196">(Refer too**Step 10** for more information.)</span></span>

<span data-ttu-id="80165-197">Siga os passos de Olá que estão descritos na seguinte captura de ecrã tooset Olá raiz de Olá palavra-passe do utilizador.</span><span class="sxs-lookup"><span data-stu-id="80165-197">Take hello steps that are described in hello following screenshot tooset hello ROOT user password.</span></span> <span data-ttu-id="80165-198">Em seguida, inicie sessão como utilizador raiz.</span><span class="sxs-lookup"><span data-stu-id="80165-198">Then sign in as ROOT user.</span></span>

![Palavra-passe de utilizador de raiz de Olá conjunto](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a><span data-ttu-id="80165-200">Preparar a máquina de Olá para configuração como um servidor de destino mestre</span><span class="sxs-lookup"><span data-stu-id="80165-200">Prepare hello machine for configuration as a master target server</span></span>
<span data-ttu-id="80165-201">Em seguida, prepare máquina Olá para configuração como um servidor de destino principal.</span><span class="sxs-lookup"><span data-stu-id="80165-201">Next, prepare hello machine for configuration as a master target server.</span></span>

<span data-ttu-id="80165-202">tooget Olá ID para cada disco de rígido SCSI numa máquina virtual Linux, ativar Olá **disco. EnableUUID = TRUE** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="80165-202">tooget hello ID for each SCSI hard disk in a Linux virtual machine, enable hello **disk.EnableUUID = TRUE** parameter.</span></span>

<span data-ttu-id="80165-203">tooenable deste parâmetro, Olá execute os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="80165-203">tooenable this parameter, take hello following steps:</span></span>

1. <span data-ttu-id="80165-204">Encerre a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="80165-204">Shut down your virtual machine.</span></span>

2. <span data-ttu-id="80165-205">Faça duplo clique entrada Olá para a máquina virtual de Olá no painel esquerdo Olá e, em seguida, selecione **editar definições de**.</span><span class="sxs-lookup"><span data-stu-id="80165-205">Right-click hello entry for hello virtual machine in hello left pane, and then select **Edit Settings**.</span></span>

3. <span data-ttu-id="80165-206">Selecione Olá **opções** separador.</span><span class="sxs-lookup"><span data-stu-id="80165-206">Select hello **Options** tab.</span></span>

4. <span data-ttu-id="80165-207">No painel esquerdo Olá, selecione **avançadas** > **geral**e, em seguida, selecione Olá **parâmetros de configuração** botão na parte inferior direita Olá ecrã Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-207">In hello left pane, select **Advanced** > **General**, and then select hello **Configuration Parameters** button on hello lower-right part of hello screen.</span></span>

    ![Separador Opções](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    <span data-ttu-id="80165-209">Olá **parâmetros de configuração** opção não está disponível quando Olá máquina está em execução.</span><span class="sxs-lookup"><span data-stu-id="80165-209">hello **Configuration Parameters** option is not available when hello machine is running.</span></span> <span data-ttu-id="80165-210">toomake este separador Active Directory, encerrar a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-210">toomake this tab active, shut down hello virtual machine.</span></span>

5. <span data-ttu-id="80165-211">Ver se uma linha com **disco. EnableUUID** já existe.</span><span class="sxs-lookup"><span data-stu-id="80165-211">See whether a row with **disk.EnableUUID** already exists.</span></span>

    - <span data-ttu-id="80165-212">Se o valor de Olá existe e está definido demasiado**falso**, altere o valor de Olá demasiado**verdadeiro**.</span><span class="sxs-lookup"><span data-stu-id="80165-212">If hello value exists and is set too**False**, change hello value too**True**.</span></span> <span data-ttu-id="80165-213">(os valores de Olá não são maiúsculas e minúsculas.)</span><span class="sxs-lookup"><span data-stu-id="80165-213">(hello values are not case-sensitive.)</span></span>

    - <span data-ttu-id="80165-214">Se o valor de Olá existe e está definido demasiado**verdadeiro**, selecione **Cancelar**.</span><span class="sxs-lookup"><span data-stu-id="80165-214">If hello value exists and is set too**True**, select **Cancel**.</span></span>

    - <span data-ttu-id="80165-215">Se o valor de Olá não existe, selecione **linha adicionar**.</span><span class="sxs-lookup"><span data-stu-id="80165-215">If hello value does not exist, select **Add Row**.</span></span>

    - <span data-ttu-id="80165-216">Na coluna de nome de Olá, adicionar **disco. EnableUUID**e, em seguida, defina o valor de Olá demasiado**verdadeiro**.</span><span class="sxs-lookup"><span data-stu-id="80165-216">In hello name column, add **disk.EnableUUID**, and then set hello value too**TRUE**.</span></span>

    ![A verificar se o disco. EnableUUID já existe](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a><span data-ttu-id="80165-218">Desativar as atualizações de kernel</span><span class="sxs-lookup"><span data-stu-id="80165-218">Disable kernel upgrades</span></span>

<span data-ttu-id="80165-219">Servidor de destino principal do Azure Site Recovery requer uma versão muito específica do Olá Ubuntu, certifique-se de que as atualizações de kernel Olá estão desativadas para a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-219">Azure Site Recovery master target server requires a very specific version of hello Ubuntu, ensure that hello kernel upgrades are disabled for hello virtual machine.</span></span>

<span data-ttu-id="80165-220">Se as atualizações de kernel estiverem ativadas, as atualizações regulares causam toomalfunction de servidor de destino mestre Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-220">If kernel upgrades are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span>

#### <a name="download-and-install-additional-packages"></a><span data-ttu-id="80165-221">Transferir e instalar pacotes adicionais</span><span class="sxs-lookup"><span data-stu-id="80165-221">Download and install additional packages</span></span>

> [!NOTE]
> <span data-ttu-id="80165-222">Certifique-se de que tem toodownload de conectividade da Internet e instalar pacotes adicionais.</span><span class="sxs-lookup"><span data-stu-id="80165-222">Make sure that you have Internet connectivity toodownload and install additional packages.</span></span> <span data-ttu-id="80165-223">Se não tiver conectividade à Internet, terá de toomanually localizar estes pacotes RPM e instalá-los.</span><span class="sxs-lookup"><span data-stu-id="80165-223">If you don't have Internet connectivity, you need toomanually find these RPM packages and install them.</span></span>

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a><span data-ttu-id="80165-224">Obter o instalador Olá para configuração</span><span class="sxs-lookup"><span data-stu-id="80165-224">Get hello installer for setup</span></span>

<span data-ttu-id="80165-225">Se o destino principal tiver conectividade à Internet, pode utilizar Olá instalador de Olá toodownload de passos a seguir.</span><span class="sxs-lookup"><span data-stu-id="80165-225">If your master target has Internet connectivity, you can use hello following steps toodownload hello installer.</span></span> <span data-ttu-id="80165-226">Caso contrário, pode copiar o hello installer do servidor de processos de Olá e, em seguida, instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="80165-226">Otherwise, you can copy hello installer from hello process server and then install it.</span></span>

#### <a name="download-hello-master-target-installation-packages"></a><span data-ttu-id="80165-227">Transferir pacotes de instalação de destino mestre Olá</span><span class="sxs-lookup"><span data-stu-id="80165-227">Download hello master target installation packages</span></span>

<span data-ttu-id="80165-228">[Transferir o bits de instalação de destino mestre Olá mais recentes Linux](https://aka.ms/latestlinuxmobsvc).</span><span class="sxs-lookup"><span data-stu-id="80165-228">[Download hello latest Linux master target installation bits](https://aka.ms/latestlinuxmobsvc).</span></span>

<span data-ttu-id="80165-229">toodownload-lo utilizando o Linux, tipo:</span><span class="sxs-lookup"><span data-stu-id="80165-229">toodownload it by using Linux, type:</span></span>

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

<span data-ttu-id="80165-230">Certifique-se de que transfira e deszipe o instalador Olá no seu diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="80165-230">Make sure that you download and unzip hello installer in your home directory.</span></span> <span data-ttu-id="80165-231">Se deszipe demasiado**usr/Local**, instalação Olá falhará.</span><span class="sxs-lookup"><span data-stu-id="80165-231">If you unzip too**/usr/Local**, then hello installation  fails.</span></span>


#### <a name="access-hello-installer-from-hello-process-server"></a><span data-ttu-id="80165-232">Instalador de Olá de acesso do servidor de processos de Olá</span><span class="sxs-lookup"><span data-stu-id="80165-232">Access hello installer from hello process server</span></span>

1. <span data-ttu-id="80165-233">No servidor de processos de Olá, aceda demasiado**C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span><span class="sxs-lookup"><span data-stu-id="80165-233">On hello process server, go too**C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span></span>

2. <span data-ttu-id="80165-234">Copie o ficheiro de instalador necessária de hello do servidor de processos de Olá e guarde-o como **latestlinuxmobsvc.tar.gz** no seu diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="80165-234">Copy hello required installer file from hello process server, and save it as **latestlinuxmobsvc.tar.gz** in your home directory.</span></span>


### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="80165-235">Aplicar alterações de configuração personalizada</span><span class="sxs-lookup"><span data-stu-id="80165-235">Apply custom configuration changes</span></span>

<span data-ttu-id="80165-236">alterações de configuração personalizada tooapply, utilize Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="80165-236">tooapply custom configuration changes, use hello following steps:</span></span>


1. <span data-ttu-id="80165-237">Execute Olá binário de Olá toountar de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="80165-237">Run hello following command toountar hello binary.</span></span>
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Captura de ecrã do Olá comando toorun](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. <span data-ttu-id="80165-239">Execute Olá permissão toogive de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="80165-239">Run hello following command toogive permission.</span></span>
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. <span data-ttu-id="80165-240">Execute Olá seguinte script do comando toorun Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-240">Run hello following command toorun hello script.</span></span>
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> <span data-ttu-id="80165-241">Execute o script de Olá apenas uma vez no servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-241">Run hello script only once on hello server.</span></span> <span data-ttu-id="80165-242">Encerre o servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-242">Shut down hello server.</span></span> <span data-ttu-id="80165-243">Em seguida, reinicie o servidor de Olá depois de adicionar um disco, conforme descrito na secção seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-243">Then restart hello server after you add a disk, as described in hello next section.</span></span>

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a><span data-ttu-id="80165-244">Adicionar uma máquina de virtual de destino principal do retenção disco toohello Linux</span><span class="sxs-lookup"><span data-stu-id="80165-244">Add a retention disk toohello Linux master target virtual machine</span></span>

<span data-ttu-id="80165-245">Utilize os seguintes passos toocreate um disco de retenção de Olá:</span><span class="sxs-lookup"><span data-stu-id="80165-245">Use hello following steps toocreate a retention disk:</span></span>

1. <span data-ttu-id="80165-246">Anexe uma novo disco de 1 TB toohello destino mestre máquina virtual com Linux e, em seguida, iniciar a máquina de Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-246">Attach a new 1-TB disk toohello Linux master target virtual machine, and then start hello machine.</span></span>

2. <span data-ttu-id="80165-247">Olá utilize **multipath -odas** toolearn Olá multipath ID de disco de retenção de Olá de comandos.</span><span class="sxs-lookup"><span data-stu-id="80165-247">Use hello **multipath -ll** command toolearn hello multipath ID of hello retention disk.</span></span>

    ```
    multipath -ll
    ```
    ![ID de multipath Olá do disco de retenção de Olá](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. <span data-ttu-id="80165-249">Formatar o disco de Olá e, em seguida, crie um sistema de ficheiros na unidade Olá de novo.</span><span class="sxs-lookup"><span data-stu-id="80165-249">Format hello drive, and then create a file system on hello new drive.</span></span>

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![A criação de um sistema de ficheiros numa unidade de Olá](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. <span data-ttu-id="80165-251">Depois de criar o sistema de ficheiros de Olá, Monte o disco de retenção de Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-251">After you create hello file system, mount hello retention disk.</span></span>
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Disco de retenção de Olá de montagem](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. <span data-ttu-id="80165-253">Criar Olá **fstab** unidade de retenção de Olá do entrada toomount sempre que o sistema de Olá é iniciado.</span><span class="sxs-lookup"><span data-stu-id="80165-253">Create hello **fstab** entry toomount hello retention drive every time hello system starts.</span></span>
    ```
    vi /etc/fstab
    ```
    <span data-ttu-id="80165-254">Selecione **inserir** toobegin editar Olá ficheiro.</span><span class="sxs-lookup"><span data-stu-id="80165-254">Select **Insert** toobegin editing hello file.</span></span> <span data-ttu-id="80165-255">Criar uma nova linha e, em seguida, inserir Olá seguinte texto.</span><span class="sxs-lookup"><span data-stu-id="80165-255">Create a new line, and then insert hello following text.</span></span> <span data-ttu-id="80165-256">Edite Olá multipath um ID de disco com base no ID de multipath Olá realçado do comando anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-256">Edit hello disk multipath ID based on hello highlighted multipath ID from hello previous command.</span></span>

    <span data-ttu-id="80165-257"> **/Dev/mapeador/ <Retention disks multipath id> /mnt/retenção ext4 RW novos 0 0**</span><span class="sxs-lookup"><span data-stu-id="80165-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span></span>

    <span data-ttu-id="80165-258">Selecione **Esc**e, em seguida, escreva **: wq** (escrever e sair) janela do editor tooclose Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-258">Select **Esc**, and then type **:wq** (write and quit) tooclose hello editor window.</span></span>

### <a name="install-hello-master-target"></a><span data-ttu-id="80165-259">Instalar o destino principal Olá</span><span class="sxs-lookup"><span data-stu-id="80165-259">Install hello master target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80165-260">versão de Hello do servidor de destino mestre Olá tem de ser igual tooor anteriores ao hello as versões do servidor de processos de Olá e servidor de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-260">hello version of hello master target server must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="80165-261">Se esta condição não for cumprida, reproteção for bem sucedida, mas a replicação falha.</span><span class="sxs-lookup"><span data-stu-id="80165-261">If this condition is not met, reprotect succeeds, but replication fails.</span></span>


> [!NOTE]
> <span data-ttu-id="80165-262">Antes de instalar o servidor de destino mestre Olá, verifique que Olá **etc/anfitriões** ficheiro na máquina virtual de Olá contém entradas que mapeiam Olá local hostname toohello endereços IP estão associados a todos os adaptadores de rede.</span><span class="sxs-lookup"><span data-stu-id="80165-262">Before you install hello master target server, check that hello **/etc/hosts** file on hello virtual machine contains entries that map hello local hostname toohello IP addresses that are associated with all network adapters.</span></span>

1. <span data-ttu-id="80165-263">Copie o frase de acesso de Olá de **C:\ProgramData\Microsoft do Azure Site Recovery\private\connection.passphrase** no servidor de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-263">Copy hello passphrase from **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** on hello configuration server.</span></span> <span data-ttu-id="80165-264">Em seguida, guarde-o como **passphrase.txt** Olá mesmo diretório local executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="80165-264">Then save it as **passphrase.txt** in hello same local directory by running hello following command:</span></span>

    ```
    echo <passphrase> >passphrase.txt
    ```
    <span data-ttu-id="80165-265">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="80165-265">Example:</span></span> 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. <span data-ttu-id="80165-266">Tenha em atenção o endereço IP do servidor de configuração Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-266">Note hello configuration server's IP address.</span></span> <span data-ttu-id="80165-267">Terá no passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-267">You need it in hello next step.</span></span>

3. <span data-ttu-id="80165-268">Execute Olá seguir o servidor de destino principal do comando tooinstall Olá e registar o servidor de Olá com o servidor de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-268">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    <span data-ttu-id="80165-269">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="80165-269">Example:</span></span> 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    <span data-ttu-id="80165-270">Aguarde pela conclusão do script Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-270">Wait until hello script finishes.</span></span> <span data-ttu-id="80165-271">Se o destino principal Olá regista com êxito, o destino principal Olá está listado no Olá **infraestrutura de recuperação de Site** página do portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-271">If hello master target registers sucessfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


#### <a name="install-hello-master-target-by-using-interactive-installation"></a><span data-ttu-id="80165-272">Instalar o destino principal Olá utilizando a instalação interativa</span><span class="sxs-lookup"><span data-stu-id="80165-272">Install hello master target by using interactive installation</span></span>

1. <span data-ttu-id="80165-273">Execute Olá destino principal do comando tooinstall Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="80165-273">Run hello following command tooinstall hello master target.</span></span> <span data-ttu-id="80165-274">Para a função de agente Olá, escolha **destino mestre**.</span><span class="sxs-lookup"><span data-stu-id="80165-274">For hello agent role, choose **Master Target**.</span></span>

    ```
    ./install
    ```

2. <span data-ttu-id="80165-275">Escolha a localização predefinida de Olá para instalação e, em seguida, selecione **Enter** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="80165-275">Choose hello default location for installation, and then select **Enter** toocontinue.</span></span>

    ![Escolher uma localização predefinida para a instalação de destino mestre](./media/site-recovery-how-to-install-linux-master-target/image17.png)

<span data-ttu-id="80165-277">Depois de concluir a instalação de Olá, registe o servidor de configuração de Olá utilizando a linha de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-277">After hello installation has finished, register hello configuration server by using hello command line.</span></span>

1. <span data-ttu-id="80165-278">Tenha em atenção o endereço IP de hello do servidor de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-278">Note hello IP address of hello configuration server.</span></span> <span data-ttu-id="80165-279">Terá no passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-279">You need it in hello next step.</span></span>

2. <span data-ttu-id="80165-280">Execute Olá seguir o servidor de destino principal do comando tooinstall Olá e registar o servidor de Olá com o servidor de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-280">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    <span data-ttu-id="80165-281">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="80165-281">Example:</span></span> 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   <span data-ttu-id="80165-282">Aguarde pela conclusão do script Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-282">Wait until hello script finishes.</span></span> <span data-ttu-id="80165-283">Se o destino principal Olá foi registado com êxito, o destino principal Olá está listado no Olá **infraestrutura de recuperação de Site** página do portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-283">If hello master target is registered succesfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


### <a name="upgrade-hello-master-target"></a><span data-ttu-id="80165-284">Atualizar o destino principal Olá</span><span class="sxs-lookup"><span data-stu-id="80165-284">Upgrade hello master target</span></span>

<span data-ttu-id="80165-285">Execute o instalador do Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-285">Run hello installer.</span></span> <span data-ttu-id="80165-286">Deteta automaticamente que o agente Olá está instalado no destino principal Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-286">It automatically detects that hello agent is installed on hello master target.</span></span> <span data-ttu-id="80165-287">tooupgrade, selecione **Y**.  Configuração Olá tenha sido concluída, verifique a versão de Olá de destino mestre Olá instalado utilizando Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="80165-287">tooupgrade, select **Y**.  After hello setup has been completed, check hello version of hello master target installed by using hello following command.</span></span>

    ```
    cat /usr/local/.vx_version
    ```

<span data-ttu-id="80165-288">Pode ver essa Olá **versão** campo indica o número de versão de Olá de destino mestre Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-288">You can see that hello **Version** field gives hello version number of hello master target.</span></span>

### <a name="install-vmware-tools-on-hello-master-target-server"></a><span data-ttu-id="80165-289">Instalar as ferramentas do VMware no servidor de destino mestre Olá</span><span class="sxs-lookup"><span data-stu-id="80165-289">Install VMware tools on hello master target server</span></span>

<span data-ttu-id="80165-290">Terá das ferramentas do VMware tooinstall no destino principal Olá para que possa detetar Olá arquivos de dados.</span><span class="sxs-lookup"><span data-stu-id="80165-290">You need tooinstall VMware tools on hello master target so that it can discover hello data stores.</span></span> <span data-ttu-id="80165-291">Se não estiverem instaladas ferramentas Olá, ecrã de reproteção Olá não está listado nos arquivos de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-291">If hello tools are not installed, hello reprotect screen isn't listed in hello data stores.</span></span> <span data-ttu-id="80165-292">Após a instalação das ferramentas do VMware Olá, terá de toorestart.</span><span class="sxs-lookup"><span data-stu-id="80165-292">After installation of hello VMware tools, you need toorestart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80165-293">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="80165-293">Next steps</span></span>
<span data-ttu-id="80165-294">Após a instalação de Olá e o registo do destino principal Olá tem finsihed, pode ver o destino principal hello apareçam na Olá **destino mestre** secção **infraestrutura de recuperação de Site**, sob Olá Descrição geral do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="80165-294">After hello installation and registration of hello master target has finsihed, you can see hello master target appear on hello **Master Target** section in **Site Recovery Infrastructure**, under hello configuration server overview.</span></span>

<span data-ttu-id="80165-295">Agora pode continuar com [só](site-recovery-how-to-reprotect.md), seguido de reativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="80165-295">You can now proceed with [reprotection](site-recovery-how-to-reprotect.md), followed by failback.</span></span>

## <a name="common-issues"></a><span data-ttu-id="80165-296">Problemas comuns</span><span class="sxs-lookup"><span data-stu-id="80165-296">Common issues</span></span>

* <span data-ttu-id="80165-297">Certifique-se de que não ative vMotion de armazenamento de quaisquer componentes de gestão tais como um destino principal.</span><span class="sxs-lookup"><span data-stu-id="80165-297">Make sure you do not turn on Storage vMotion on any management components such as a master target.</span></span> <span data-ttu-id="80165-298">Se o destino principal Olá move após uma reproteção com êxito, os discos da máquina virtual Olá (VMDKs) não podem ser desligados.</span><span class="sxs-lookup"><span data-stu-id="80165-298">If hello master target moves after a successful reprotect, hello virtual machine disks (VMDKs) cannot be detached.</span></span> <span data-ttu-id="80165-299">Neste caso, a reativação pós-falha falha.</span><span class="sxs-lookup"><span data-stu-id="80165-299">In this case, failback fails.</span></span>

* <span data-ttu-id="80165-300">destino mestre Olá não deve ter todos os instantâneos na máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-300">hello master target should not have any snapshots on hello virtual machine.</span></span> <span data-ttu-id="80165-301">Se existirem instantâneos, irá falhar a reativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="80165-301">If there are snapshots, failback fails.</span></span>

* <span data-ttu-id="80165-302">Atraso toosome NIC personalizado em alguns clientes, interface de rede Olá está desativada durante o arranque e, não é possível inicializar o agente de destino mestre Olá.</span><span class="sxs-lookup"><span data-stu-id="80165-302">Due toosome custom NIC configurations at some customers, hello network interface is disabled during startup, and hello master target agent cannot initialize.</span></span> <span data-ttu-id="80165-303">Certifique-se de que Olá seguintes propriedades estão definidas corretamente.</span><span class="sxs-lookup"><span data-stu-id="80165-303">Make sure that hello following properties are correctly set.</span></span> <span data-ttu-id="80165-304">Verifique estas propriedades no Olá Ethernet /etc/sysconfig/network-scripts/ifcfg do ficheiro de cartão-eth *.</span><span class="sxs-lookup"><span data-stu-id="80165-304">Check these properties in hello Ethernet card file's /etc/sysconfig/network-scripts/ifcfg-eth*.</span></span>
    * <span data-ttu-id="80165-305">BOOTPROTO = dhcp</span><span class="sxs-lookup"><span data-stu-id="80165-305">BOOTPROTO=dhcp</span></span>
    * <span data-ttu-id="80165-306">ONBOOT = yes</span><span class="sxs-lookup"><span data-stu-id="80165-306">ONBOOT=yes</span></span>
