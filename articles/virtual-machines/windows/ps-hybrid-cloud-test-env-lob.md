---
title: "ambiente de teste de aplicação aaaLOB | Microsoft Docs"
description: "Saiba como toocreate um baseada na web, de linha de aplicação empresarial numa versão híbrida cloud ambiente para o IT pro ou o teste de desenvolvimento."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 92d2d8ce-60ed-4512-95e5-a7fe3b0ca00b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: e9f825bbb1cbeb841ee3c974ebf6721dc236c311
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a><span data-ttu-id="b595f-103">Configurar uma aplicação LOB baseada na Web numa cloud híbrida para fins de teste</span><span class="sxs-lookup"><span data-stu-id="b595f-103">Set up a web-based LOB application in a hybrid cloud for testing</span></span>
<span data-ttu-id="b595f-104">Este tópico disponibiliza os passos criação num ambiente de nuvem híbrida simuladas para testar uma baseada na web aplicação de linha de negócio (LOB) alojada no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b595f-104">This topic steps you through creating a simulated hybrid cloud environment for testing a web-based line of business (LOB) application hosted in Microsoft Azure.</span></span> <span data-ttu-id="b595f-105">Segue-se a configuração resultante Olá.</span><span class="sxs-lookup"><span data-stu-id="b595f-105">Here is hello resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="b595f-106">Esta configuração é composta por:</span><span class="sxs-lookup"><span data-stu-id="b595f-106">This configuration consists of:</span></span>

* <span data-ttu-id="b595f-107">Uma rede de simulada no local, alojada no Azure (Olá VNet de laboratório de teste).</span><span class="sxs-lookup"><span data-stu-id="b595f-107">A simulated on-premises network hosted in Azure (hello TestLab VNet).</span></span>
* <span data-ttu-id="b595f-108">Rede virtual de vários locais alojada no Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="b595f-108">A cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="b595f-109">Uma ligação de VPN de VNet a VNet.</span><span class="sxs-lookup"><span data-stu-id="b595f-109">A VNet-to-VNet VPN connection.</span></span>
* <span data-ttu-id="b595f-110">Um servidor LOB baseada na web, o do SQL Server e o controlador de domínio secundário na rede virtual do Olá TestVNET.</span><span class="sxs-lookup"><span data-stu-id="b595f-110">A web-based LOB server, SQL server, and secondary domain controller in hello TestVNET virtual network.</span></span>

<span data-ttu-id="b595f-111">Esta configuração fornece uma base e o ponto de partida comuns partir da qual pode:</span><span class="sxs-lookup"><span data-stu-id="b595f-111">This configuration provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="b595f-112">Desenvolver e testar aplicações de LOB alojadas em serviços de informação Internet (IIS) com um back-end de base de dados do SQL Server 2014 no Azure.</span><span class="sxs-lookup"><span data-stu-id="b595f-112">Develop and test LOB applications hosted on Internet Information Services (IIS) with a SQL Server 2014 database backend in Azure.</span></span>
* <span data-ttu-id="b595f-113">Efetue testes desta híbrida simulada baseado na nuvem IT carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b595f-113">Perform testing of this simulated hybrid cloud-based IT workload.</span></span>

<span data-ttu-id="b595f-114">Existem três fases principais toosetting segurança deste ambiente de teste de nuvem híbrida:</span><span class="sxs-lookup"><span data-stu-id="b595f-114">There are three major phases toosetting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="b595f-115">Configure o ambiente de nuvem híbrida simulada Olá.</span><span class="sxs-lookup"><span data-stu-id="b595f-115">Set up hello simulated hybrid cloud environment.</span></span>
2. <span data-ttu-id="b595f-116">Configure o computador do servidor SQL da Olá (SQL1).</span><span class="sxs-lookup"><span data-stu-id="b595f-116">Configure hello SQL server computer (SQL1).</span></span>
3. <span data-ttu-id="b595f-117">Configure o servidor LOB Olá (LOB1).</span><span class="sxs-lookup"><span data-stu-id="b595f-117">Configure hello LOB server (LOB1).</span></span>

<span data-ttu-id="b595f-118">Esta carga de trabalho requer uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="b595f-118">This workload requires an Azure subscription.</span></span> <span data-ttu-id="b595f-119">Se tiver uma subscrição MSDN ou Visual Studio, consulte [crédito do Azure mensal para subscritores do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="b595f-119">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

<span data-ttu-id="b595f-120">Para obter um exemplo de uma aplicação de LOB alojada no Azure de produção, consulte Olá **aplicações empresariais de linha de** blueprint de arquitetura em [diagramas de arquitetura de Software Microsoft e esquemas](http://msdn.microsoft.com/dn630664).</span><span class="sxs-lookup"><span data-stu-id="b595f-120">For an example of a production LOB application hosted in Azure, see hello **Line of business applications** architecture blueprint at [Microsoft Software Architecture Diagrams and Blueprints](http://msdn.microsoft.com/dn630664).</span></span>

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a><span data-ttu-id="b595f-121">Fase 1: Configurar o ambiente de nuvem híbrida simulada Olá</span><span class="sxs-lookup"><span data-stu-id="b595f-121">Phase 1: Set up hello simulated hybrid cloud environment</span></span>
<span data-ttu-id="b595f-122">Criar Olá [ambiente de teste de cloud híbrida simulada](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b595f-122">Create hello [simulated hybrid cloud test environment](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="b595f-123">Porque este ambiente de teste não requer a presença de hello do servidor de Olá APP1 na sub-rede da rede empresarial de Olá, pode encerrá-la por agora.</span><span class="sxs-lookup"><span data-stu-id="b595f-123">Because this test environment does not require hello presence of hello APP1 server on hello Corpnet subnet, you can shut it down for now.</span></span>

<span data-ttu-id="b595f-124">Esta é a configuração atual.</span><span class="sxs-lookup"><span data-stu-id="b595f-124">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a><span data-ttu-id="b595f-125">Fase 2: Configurar o computador do servidor SQL da Olá (SQL1)</span><span class="sxs-lookup"><span data-stu-id="b595f-125">Phase 2: Configure hello SQL server computer (SQL1)</span></span>
<span data-ttu-id="b595f-126">De Olá portal do Azure, inicie o computador de DC2 de Olá se for necessário.</span><span class="sxs-lookup"><span data-stu-id="b595f-126">From hello Azure portal, start hello DC2 computer if needed.</span></span>

<span data-ttu-id="b595f-127">Em seguida, crie uma máquina virtual para SQL1 com estes comandos numa linha de comandos do Azure PowerShell no computador local.</span><span class="sxs-lookup"><span data-stu-id="b595f-127">Next, create a virtual machine for SQL1 with these commands at an Azure PowerShell command prompt on your local computer.</span></span> <span data-ttu-id="b595f-128">Toorunning anterior estes comandos, preencha Olá valores das variáveis e remover Olá < e > carateres.</span><span class="sxs-lookup"><span data-stu-id="b595f-128">Prior toorunning these commands, fill in hello variable values and remove hello < and > characters.</span></span>

    $rgName="<your resource group name>"
    $locName="<hello Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for hello SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="b595f-129">Utilize Olá tooSQL1 tooconnect portal do Azure utilizando a conta de administrador local Olá de SQL1.</span><span class="sxs-lookup"><span data-stu-id="b595f-129">Use hello Azure portal tooconnect tooSQL1 using hello local administrator account of SQL1.</span></span>

<span data-ttu-id="b595f-130">Em seguida, configure a testar conectividade básica de tooallow de regras do Firewall do Windows e o tráfego do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b595f-130">Next, configure Windows Firewall rules tooallow basic connectivity testing and SQL Server traffic.</span></span> <span data-ttu-id="b595f-131">Um nível de administrador do Windows PowerShell linha de comandos no SQL1, execute estes comandos.</span><span class="sxs-lookup"><span data-stu-id="b595f-131">From an administrator-level Windows PowerShell command prompt on SQL1, run these commands.</span></span>

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="b595f-132">comandos de ping de Olá devem resultar em quatro respostas com êxito do endereço IP 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="b595f-132">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="b595f-133">Em seguida, adicione Olá disco de dados adicionais no SQL1 como um novo volume com letra de unidade de Olá f:.</span><span class="sxs-lookup"><span data-stu-id="b595f-133">Next, add hello extra data disk on SQL1 as a new volume with hello drive letter F:.</span></span>

1. <span data-ttu-id="b595f-134">No painel esquerdo do Olá do Gestor de servidores, clique em **File and Storage Services**e, em seguida, clique em **discos**.</span><span class="sxs-lookup"><span data-stu-id="b595f-134">In hello left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="b595f-135">No painel de conteúdo de Olá, no Olá **discos** , clique em **disco 2** (com Olá **partição** definido demasiado**desconhecido**).</span><span class="sxs-lookup"><span data-stu-id="b595f-135">In hello contents pane, in hello **Disks** group, click **disk 2** (with hello **Partition** set too**Unknown**).</span></span>
3. <span data-ttu-id="b595f-136">Clique em **tarefas**e, em seguida, clique em **Novo Volume**.</span><span class="sxs-lookup"><span data-stu-id="b595f-136">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="b595f-137">Olá antes de começar a página do Assistente de novo Volume de Olá, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="b595f-137">On hello Before you begin page of hello New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="b595f-138">No servidor de Olá selecione Olá e página de disco, clique em **disco 2**e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="b595f-138">On hello Select hello server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="b595f-139">Quando lhe for pedido, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b595f-139">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="b595f-140">Especificar o tamanho de Olá da página de volume Olá Olá, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="b595f-140">On hello Specify hello size of hello volume page, click **Next**.</span></span>
7. <span data-ttu-id="b595f-141">Olá atribuir tooa unidade letra ou pasta página, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="b595f-141">On hello Assign tooa drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="b595f-142">Na página de definições de sistema de ficheiros selecione Olá, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="b595f-142">On hello Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="b595f-143">Na página Olá confirmar seleções, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="b595f-143">On hello Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="b595f-144">Quando terminar, clique em **fechar**.</span><span class="sxs-lookup"><span data-stu-id="b595f-144">When complete, click **Close**.</span></span>

<span data-ttu-id="b595f-145">Execute estes comandos na linha de comandos do Windows PowerShell Olá no SQL1:</span><span class="sxs-lookup"><span data-stu-id="b595f-145">Run these commands at hello Windows PowerShell command prompt on SQL1:</span></span>

    md f:\Data
    md f:\Log
    md f:\Backup

<span data-ttu-id="b595f-146">Em seguida, associe o domínio CORP Windows Server Active Directory de toohello de SQL1 com estes comandos na linha de comandos do Olá do Windows PowerShell no SQL1.</span><span class="sxs-lookup"><span data-stu-id="b595f-146">Next, join SQL1 toohello CORP Windows Server Active Directory domain with these commands at hello Windows PowerShell prompt on SQL1.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="b595f-147">Utilizar a conta de Olá CORP\User1 quando lhe forem pedidas as credenciais da conta de domínio toosupply para Olá **Add-Computer** comando.</span><span class="sxs-lookup"><span data-stu-id="b595f-147">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="b595f-148">Depois de reiniciar, utilize Olá tooconnect portal do Azure tooSQL1 *com a conta de administrador local Olá de SQL1*.</span><span class="sxs-lookup"><span data-stu-id="b595f-148">After restarting, use hello Azure portal tooconnect tooSQL1 *with hello local administrator account of SQL1*.</span></span>

<span data-ttu-id="b595f-149">Em seguida, configure a unidade de f: de Olá do SQL Server 2014 toouse para novas bases de dados e para permissões de conta de utilizador.</span><span class="sxs-lookup"><span data-stu-id="b595f-149">Next, configure SQL Server 2014 toouse hello F: drive for new databases and for user account permissions.</span></span>

1. <span data-ttu-id="b595f-150">A partir do ecrã de início de Olá, escreva **SQL Server Management**e, em seguida, clique em **SQL Server 2014 Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="b595f-150">From hello Start screen, type **SQL Server Management**, and then click **SQL Server 2014 Management Studio**.</span></span>
2. <span data-ttu-id="b595f-151">No **ligar tooServer**, clique em **Connect**.</span><span class="sxs-lookup"><span data-stu-id="b595f-151">In **Connect tooServer**, click **Connect**.</span></span>
3. <span data-ttu-id="b595f-152">No painel de árvore do Olá Object Explorer, clique com botão direito **SQL1**e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="b595f-152">In hello Object Explorer tree pane, right-click **SQL1**, and then click **Properties**.</span></span>
4. <span data-ttu-id="b595f-153">No Olá **propriedades do servidor** janela, clique em **definições de base de dados**.</span><span class="sxs-lookup"><span data-stu-id="b595f-153">In hello **Server Properties** window, click **Database Settings**.</span></span>
5. <span data-ttu-id="b595f-154">Localizar Olá **localizações predefinidas de base de dados** e defina estes valores:</span><span class="sxs-lookup"><span data-stu-id="b595f-154">Locate hello **Database default locations** and set these values:</span></span> 
   * <span data-ttu-id="b595f-155">Para **dados**, o caminho do tipo Olá **f:\Data**.</span><span class="sxs-lookup"><span data-stu-id="b595f-155">For **Data**, type hello path **f:\Data**.</span></span>
   * <span data-ttu-id="b595f-156">Para **registo**, o caminho do tipo Olá **f:\Log**.</span><span class="sxs-lookup"><span data-stu-id="b595f-156">For **Log**, type hello path **f:\Log**.</span></span>
   * <span data-ttu-id="b595f-157">Para **cópia de segurança**, o caminho do tipo Olá **f:\Backup**.</span><span class="sxs-lookup"><span data-stu-id="b595f-157">For **Backup**, type hello path **f:\Backup**.</span></span>
   * <span data-ttu-id="b595f-158">Nota: Só novas bases de dados, utilize estas localizações.</span><span class="sxs-lookup"><span data-stu-id="b595f-158">Note: Only new databases use these locations.</span></span>
6. <span data-ttu-id="b595f-159">Clique em Olá **OK** janela de Olá tooclose.</span><span class="sxs-lookup"><span data-stu-id="b595f-159">Click hello **OK** tooclose hello window.</span></span>
7. <span data-ttu-id="b595f-160">No Olá **Object Explorer** painel de árvore, abra **segurança**.</span><span class="sxs-lookup"><span data-stu-id="b595f-160">In hello **Object Explorer** tree pane, open **Security**.</span></span>
8. <span data-ttu-id="b595f-161">Clique com botão direito **inícios de sessão** e, em seguida, clique em **novo início de sessão**.</span><span class="sxs-lookup"><span data-stu-id="b595f-161">Right-click **Logins** and then click **New Login**.</span></span>
9. <span data-ttu-id="b595f-162">No **nome de início de sessão**, tipo **CORP\User1**.</span><span class="sxs-lookup"><span data-stu-id="b595f-162">In **Login name**, type **CORP\User1**.</span></span>
10. <span data-ttu-id="b595f-163">No Olá **funções de servidor** página, clique em **sysadmin**e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b595f-163">On hello **Server Roles** page, click **sysadmin**, and then click **OK**.</span></span>
11. <span data-ttu-id="b595f-164">Feche o Microsoft SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="b595f-164">Close Microsoft SQL Server Management Studio.</span></span>

<span data-ttu-id="b595f-165">Esta é a configuração atual.</span><span class="sxs-lookup"><span data-stu-id="b595f-165">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a><span data-ttu-id="b595f-166">Passo 3: Configurar o servidor LOB Olá (LOB1)</span><span class="sxs-lookup"><span data-stu-id="b595f-166">Phase 3: Configure hello LOB server (LOB1)</span></span>
<span data-ttu-id="b595f-167">Em primeiro lugar, crie uma máquina virtual para LOB1 com estes comandos na linha de comandos do Azure PowerShell Olá no seu computador local.</span><span class="sxs-lookup"><span data-stu-id="b595f-167">First, create a virtual machine for LOB1 with these commands at hello Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="b595f-168">Em seguida, utilize Olá tooconnect portal do Azure tooLOB1 com credenciais de Olá da conta de administrador local Olá do LOB1.</span><span class="sxs-lookup"><span data-stu-id="b595f-168">Next, use hello Azure portal tooconnect tooLOB1 with hello credentials of hello local administrator account of LOB1.</span></span>

<span data-ttu-id="b595f-169">Em seguida, configure um tráfego de tooallow de regra de Firewall do Windows para testar a conectividade básica.</span><span class="sxs-lookup"><span data-stu-id="b595f-169">Next, configure a Windows Firewall rule tooallow traffic for basic connectivity testing.</span></span> <span data-ttu-id="b595f-170">A partir de uma nível de administrador do Windows PowerShell linha de comandos no LOB1, execute estes comandos.</span><span class="sxs-lookup"><span data-stu-id="b595f-170">From an administrator-level Windows PowerShell command prompt on LOB1, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="b595f-171">comandos de ping de Olá devem resultar em quatro respostas com êxito do endereço IP 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="b595f-171">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="b595f-172">Em seguida, associe domínio de Active Directory CORP toohello LOB1 com estes comandos na linha de comandos do Olá do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b595f-172">Next, join LOB1 toohello CORP Active Directory domain with these commands at hello Windows PowerShell prompt.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="b595f-173">Utilizar a conta de Olá CORP\User1 quando lhe forem pedidas as credenciais da conta de domínio toosupply para Olá **Add-Computer** comando.</span><span class="sxs-lookup"><span data-stu-id="b595f-173">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="b595f-174">Depois de reiniciar, utilize Olá tooconnect portal do Azure tooLOB1 com a conta de Olá CORP\User1 e a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="b595f-174">After restarting, use hello Azure portal tooconnect tooLOB1 with hello CORP\User1 account and password.</span></span>

<span data-ttu-id="b595f-175">Em seguida, configurar LOB1 para o IIS e testar o acesso a partir de CLIENT1.</span><span class="sxs-lookup"><span data-stu-id="b595f-175">Next, configure LOB1 for IIS and test access from CLIENT1.</span></span>

1. <span data-ttu-id="b595f-176">No Gestor de servidores, clique em **para adicionar funções e funcionalidades**.</span><span class="sxs-lookup"><span data-stu-id="b595f-176">From Server Manager, click **Add roles and features**.</span></span>
2. <span data-ttu-id="b595f-177">No Olá **antes de começar** página, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="b595f-177">On hello **Before you begin** page, click **Next**.</span></span>
3. <span data-ttu-id="b595f-178">No Olá **selecionar tipo de instalação** página, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="b595f-178">On hello **Select installation type** page, click **Next**.</span></span>
4. <span data-ttu-id="b595f-179">No Olá **servidor de destino selecione** página, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="b595f-179">On hello **Select destination server** page, click **Next**.</span></span>
5. <span data-ttu-id="b595f-180">No Olá **funções de servidor** página, clique em **servidor Web (IIS)** na lista de Olá de **funções**.</span><span class="sxs-lookup"><span data-stu-id="b595f-180">On hello **Server roles** page, click **Web Server (IIS)** in hello list of **Roles**.</span></span>
6. <span data-ttu-id="b595f-181">Quando lhe for pedido, clique em **adicionar funcionalidades**e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="b595f-181">When prompted, click **Add Features**, and then click **Next**.</span></span>
7. <span data-ttu-id="b595f-182">No Olá **selecionar funcionalidades** página, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="b595f-182">On hello **Select features** page, click **Next**.</span></span>
8. <span data-ttu-id="b595f-183">No Olá **servidor Web (IIS)** página, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="b595f-183">On hello **Web Server (IIS)** page, click **Next**.</span></span>
9. <span data-ttu-id="b595f-184">No Olá **selecionar serviços de função** página, selecione ou desmarque as caixas de verificação de Olá para serviços de Olá precisa para testar a aplicação de LOB e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="b595f-184">On hello **Select role services** page, select or clear hello check boxes for hello services you need for testing your LOB application, and then click **Next**.</span></span>
10. <span data-ttu-id="b595f-185">No Olá **confirmar seleções de instalação** página, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="b595f-185">On hello **Confirm installation selections** page, click **Install**.</span></span>
11. <span data-ttu-id="b595f-186">Aguarde pela conclusão da instalação dos componentes Olá e, em seguida, clique em **fechar**.</span><span class="sxs-lookup"><span data-stu-id="b595f-186">Wait until hello installation of components has completed and then click **Close**.</span></span>
12. <span data-ttu-id="b595f-187">A partir do portal do Azure Olá, ligar o computador de CLIENT1 toohello com as credenciais de conta de CORP\User1 Olá e, em seguida, inicie o Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="b595f-187">From hello Azure portal, connect toohello CLIENT1 computer with hello CORP\User1 account credentials, and then start Internet Explorer.</span></span>
13. <span data-ttu-id="b595f-188">Na barra de endereço Olá, escreva **http://lob1/** e, em seguida, prima ENTER.</span><span class="sxs-lookup"><span data-stu-id="b595f-188">In hello Address bar, type **http://lob1/** and then press ENTER.</span></span> <span data-ttu-id="b595f-189">Deverá ver a página de web IIS 8 do Olá predefinida.</span><span class="sxs-lookup"><span data-stu-id="b595f-189">You should see hello default IIS 8 web page.</span></span>

<span data-ttu-id="b595f-190">Esta é a configuração atual.</span><span class="sxs-lookup"><span data-stu-id="b595f-190">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="b595f-191">Este ambiente está agora pronto para lhe toodeploy a baseada na web aplicação LOB1 e teste a funcionalidade de CLIENT1 na sub-rede da rede empresarial de Olá.</span><span class="sxs-lookup"><span data-stu-id="b595f-191">This environment is now ready for you toodeploy your web-based application on LOB1 and test functionality from CLIENT1 on hello Corpnet subnet.</span></span>

## <a name="next-step"></a><span data-ttu-id="b595f-192">Passo seguinte</span><span class="sxs-lookup"><span data-stu-id="b595f-192">Next step</span></span>
* <span data-ttu-id="b595f-193">Adicionar uma nova máquina virtual utilizando Olá [portal do Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b595f-193">Add a new virtual machine using hello [Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

