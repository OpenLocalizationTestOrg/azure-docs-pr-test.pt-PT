---
title: "aaaHow tooconfigure um serviço em nuvem (portal) | Microsoft Docs"
description: "Saiba como tooconfigure cloud services no Azure. Obter a configuração do serviço de nuvem do tooupdate Olá e configurar as instâncias de toorole de acesso remoto. Estes exemplos utilizam Olá portal do Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: 969a08558473e8c79153192942bfda587eb5ada5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a><span data-ttu-id="4db49-105">Como tooConfigure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="4db49-105">How tooConfigure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4db49-106">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4db49-106">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="4db49-107">Portal Clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="4db49-107">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
>
>

<span data-ttu-id="4db49-108">Pode configurar as definições de Olá normalmente utilizada para um serviço em nuvem no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4db49-108">You can configure hello most commonly used settings for a cloud service in hello Azure portal.</span></span> <span data-ttu-id="4db49-109">Ou, se pretender tooupdate diretamente, os ficheiros de configuração transfira um tooupdate de ficheiro de configuração de serviço e, em seguida, carregue Olá atualizado de ficheiros e atualização Olá serviço em nuvem com alterações de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="4db49-109">Or, if you like tooupdate your configuration files directly, download a service configuration file tooupdate, and then upload hello updated file and update hello cloud service with hello configuration changes.</span></span> <span data-ttu-id="4db49-110">Qualquer forma, as atualizações de configuração de Olá são instalados sem solicitação tooall instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="4db49-110">Either way, hello configuration updates are pushed out tooall role instances.</span></span>

<span data-ttu-id="4db49-111">Também pode gerir instâncias Olá das suas funções de serviço na nuvem ou ambiente de trabalho remoto em-los.</span><span class="sxs-lookup"><span data-stu-id="4db49-111">You can also manage hello instances of your cloud service roles, or remote desktop into them.</span></span>

<span data-ttu-id="4db49-112">Azure pode apenas Certifique-se de disponibilidade do serviço de percentagem de 99,95 durante Olá atualizações de configuração se tiver, pelo menos, duas instâncias de função para cada função.</span><span class="sxs-lookup"><span data-stu-id="4db49-112">Azure can only ensure 99.95 percent service availability during hello configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="4db49-113">Que permite que uma máquina virtual tooprocess os pedidos de cliente enquanto Olá outro está a ser atualizado.</span><span class="sxs-lookup"><span data-stu-id="4db49-113">That enables one virtual machine tooprocess client requests while hello other is being updated.</span></span> <span data-ttu-id="4db49-114">Para obter mais informações, consulte [contratos de nível de serviço](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="4db49-114">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="4db49-115">Alterar um serviço em nuvem</span><span class="sxs-lookup"><span data-stu-id="4db49-115">Change a cloud service</span></span>
<span data-ttu-id="4db49-116">Após a abertura Olá [portal do Azure](https://portal.azure.com/), navegue até tooyour o serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="4db49-116">After opening hello [Azure portal](https://portal.azure.com/), navigate tooyour cloud service.</span></span> <span data-ttu-id="4db49-117">Aqui, gerir vários aspetos do mesmo.</span><span class="sxs-lookup"><span data-stu-id="4db49-117">From here, you manage many aspects of it.</span></span>

![Página de definições](./media/cloud-services-how-to-configure-portal/cloud-service.png)

<span data-ttu-id="4db49-119">Olá **definições** ou **todas as definições** irão abrir ligações Olá **definições** painel onde pode alterar Olá **propriedades**, alterar Olá **Configuração**, gerir Olá **certificados**, configuração **regras de alerta**e gerir Olá **utilizadores** quem tem acesso o serviço em nuvem toothis.</span><span class="sxs-lookup"><span data-stu-id="4db49-119">hello **Settings** or **All settings** links will open up hello **Settings** blade where you can change hello **Properties**, change hello **Configuration**, manage hello **Certificates**, setup **Alert rules**, and manage hello **Users** who have access toothis cloud service.</span></span>

![Painel de definições de serviço em nuvem do Azure](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a><span data-ttu-id="4db49-121">Gerir a versão de SO convidado</span><span class="sxs-lookup"><span data-stu-id="4db49-121">Manage Guest OS version</span></span>

<span data-ttu-id="4db49-122">Por predefinição, o Azure atualiza periodicamente a convidado toohello mais recente suportada imagem do SO no Olá família de SO especificadas na sua configuração de serviço (. cscfg), como o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="4db49-122">By default, Azure periodically updates your guest OS toohello latest supported image within hello OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span></span>

<span data-ttu-id="4db49-123">Se precisar de tootarget uma versão de SO específica, pode defini-lo no Olá **configuração** painel.</span><span class="sxs-lookup"><span data-stu-id="4db49-123">If you need tootarget a specific OS version, you can set it in hello **Configuration** blade.</span></span>

![Definir a versão de SO](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> <span data-ttu-id="4db49-125">Escolher que uma versão de SO específica desativa SO automático de atualizações e faz a responsabilidade de aplicação de patches.</span><span class="sxs-lookup"><span data-stu-id="4db49-125">Choosing a specific OS version disables automatic OS updates and makes patching your responsibility.</span></span> <span data-ttu-id="4db49-126">Tem de garantir que as instâncias da função estão a receber atualizações ou pode expor as vulnerabilidades de toosecurity de aplicação.</span><span class="sxs-lookup"><span data-stu-id="4db49-126">You must ensure that your role instances are receiving updates or you may expose your application toosecurity vulnerabilities.</span></span>

## <a name="monitoring"></a><span data-ttu-id="4db49-127">Monitorização</span><span class="sxs-lookup"><span data-stu-id="4db49-127">Monitoring</span></span>
<span data-ttu-id="4db49-128">Pode adicionar o serviço de nuvem tooyour de alertas.</span><span class="sxs-lookup"><span data-stu-id="4db49-128">You can add alerts tooyour cloud service.</span></span> <span data-ttu-id="4db49-129">Clique em **definições** > **regras de alerta** > **Adicionar alerta**.</span><span class="sxs-lookup"><span data-stu-id="4db49-129">Click **Settings** > **Alert Rules** > **Add alert**.</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

<span data-ttu-id="4db49-130">Aqui, pode configurar um alerta.</span><span class="sxs-lookup"><span data-stu-id="4db49-130">From here, you can setup an alert.</span></span> <span data-ttu-id="4db49-131">Com Olá **métrica** pendente caixa, pode configurar um alerta para Olá tipos de dados seguintes.</span><span class="sxs-lookup"><span data-stu-id="4db49-131">With hello **Metric** drop down box, you can setup an alert for hello following types of data.</span></span>

* <span data-ttu-id="4db49-132">Lidos de disco</span><span class="sxs-lookup"><span data-stu-id="4db49-132">Disk read</span></span>
* <span data-ttu-id="4db49-133">Escrita de disco</span><span class="sxs-lookup"><span data-stu-id="4db49-133">Disk write</span></span>
* <span data-ttu-id="4db49-134">Rede no</span><span class="sxs-lookup"><span data-stu-id="4db49-134">Network in</span></span>
* <span data-ttu-id="4db49-135">Limite de rede</span><span class="sxs-lookup"><span data-stu-id="4db49-135">Network out</span></span>
* <span data-ttu-id="4db49-136">Percentagem de CPU</span><span class="sxs-lookup"><span data-stu-id="4db49-136">CPU percentage</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a><span data-ttu-id="4db49-137">Configurar a monitorização a partir de um mosaico métrico</span><span class="sxs-lookup"><span data-stu-id="4db49-137">Configure monitoring from a metric tile</span></span>
<span data-ttu-id="4db49-138">Em vez de utilizar **definições** > **regras de alerta**, pode clicar dos mosaicos de métrica de Olá no Olá **monitorização** secção Olá **na nuvem serviço** painel.</span><span class="sxs-lookup"><span data-stu-id="4db49-138">Instead of using **Settings** > **Alert Rules**, you can click on one of hello metric tiles in hello **Monitoring** section of hello **Cloud service** blade.</span></span>

![Monitorização do serviço de nuvem](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

<span data-ttu-id="4db49-140">Aqui pode personalizar o gráfico de Olá utilizado com o mosaico Olá ou adicionar uma regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="4db49-140">From here you can customize hello chart used with hello tile, or add an alert rule.</span></span>

## <a name="reboot-reimage-or-remote-desktop"></a><span data-ttu-id="4db49-141">Reiniciar o computador, a recriação de imagem ou o ambiente de trabalho remoto</span><span class="sxs-lookup"><span data-stu-id="4db49-141">Reboot, reimage, or remote desktop</span></span>
<span data-ttu-id="4db49-142">Neste momento, não é possível configurar o ambiente de trabalho remoto utilizando Olá **portal do Azure**.</span><span class="sxs-lookup"><span data-stu-id="4db49-142">At this time you cannot configure remote desktop using hello **Azure portal**.</span></span> <span data-ttu-id="4db49-143">No entanto, pode configurá-lo através de Olá [portal clássico do Azure](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), ou através de [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="4db49-143">However, you can set it up through hello [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span></span>

<span data-ttu-id="4db49-144">Em primeiro lugar, clique na instância do serviço de nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="4db49-144">First, click on hello cloud service instance.</span></span>

![Instância de serviço de nuvem](./media/cloud-services-how-to-configure-portal/cs-instance.png)

<span data-ttu-id="4db49-146">De Olá painel que abre-se de pode iniciar uma ligação de ambiente de trabalho remota, reiniciar remotamente Olá instâncias, ou remotamente recriação de imagem (começar com uma nova imagem) Olá.</span><span class="sxs-lookup"><span data-stu-id="4db49-146">From hello blade that opens you can initiate a remote desktop connection, remotely reboot hello instance, or remotely reimage (start with a fresh image) hello instance.</span></span>

![Botões de instância de serviço de nuvem](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a><span data-ttu-id="4db49-148">Reconfigure o. cscfg</span><span class="sxs-lookup"><span data-stu-id="4db49-148">Reconfigure your .cscfg</span></span>
<span data-ttu-id="4db49-149">Poderá ser necessário tooreconfigure o serviço de nuvem através de Olá [a configuração do serviço (. cscfg)](cloud-services-model-and-package.md#cscfg) ficheiro.</span><span class="sxs-lookup"><span data-stu-id="4db49-149">You may need tooreconfigure your cloud service through hello [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span></span> <span data-ttu-id="4db49-150">Primeiro tem de toodownload o. cscfg do ficheiro, modificá-lo, em seguida, carregá-la.</span><span class="sxs-lookup"><span data-stu-id="4db49-150">First you need toodownload your .cscfg file, modify it, then upload it.</span></span>

1. <span data-ttu-id="4db49-151">Clique em Olá **definições** ícone ou Olá **todas as definições** ligação tooopen segurança Olá **definições** painel.</span><span class="sxs-lookup"><span data-stu-id="4db49-151">Click on hello **Settings** icon or hello **All settings** link tooopen up hello **Settings** blade.</span></span>

    ![Página de definições](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. <span data-ttu-id="4db49-153">Clique em Olá **configuração** item.</span><span class="sxs-lookup"><span data-stu-id="4db49-153">Click on hello **Configuration** item.</span></span>

    ![Painel de configuração](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. <span data-ttu-id="4db49-155">Clique em Olá **transferir** botão.</span><span class="sxs-lookup"><span data-stu-id="4db49-155">Click on hello **Download** button.</span></span>

    ![Transferência](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. <span data-ttu-id="4db49-157">Depois de atualizar o ficheiro de configuração do serviço de Olá, carregar e aplicar atualizações de configuração de Olá:</span><span class="sxs-lookup"><span data-stu-id="4db49-157">After you update hello service configuration file, upload and apply hello configuration updates:</span></span>

    ![Carregar](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. <span data-ttu-id="4db49-159">Selecione o ficheiro. cscfg Olá e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4db49-159">Select hello .cscfg file and click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4db49-160">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4db49-160">Next steps</span></span>
* <span data-ttu-id="4db49-161">Saiba como demasiado[implementar um serviço em nuvem](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4db49-161">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="4db49-162">Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4db49-162">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="4db49-163">[Gerir o serviço de nuvem](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4db49-163">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="4db49-164">Configurar [certificados ssl](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4db49-164">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
