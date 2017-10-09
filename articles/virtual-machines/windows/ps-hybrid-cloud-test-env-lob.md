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
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a>Configurar uma aplicação LOB baseada na Web numa cloud híbrida para fins de teste
Este tópico disponibiliza os passos criação num ambiente de nuvem híbrida simuladas para testar uma baseada na web aplicação de linha de negócio (LOB) alojada no Microsoft Azure. Segue-se a configuração resultante Olá.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

Esta configuração é composta por:

* Uma rede de simulada no local, alojada no Azure (Olá VNet de laboratório de teste).
* Rede virtual de vários locais alojada no Azure (TestVNET).
* Uma ligação de VPN de VNet a VNet.
* Um servidor LOB baseada na web, o do SQL Server e o controlador de domínio secundário na rede virtual do Olá TestVNET.

Esta configuração fornece uma base e o ponto de partida comuns partir da qual pode:

* Desenvolver e testar aplicações de LOB alojadas em serviços de informação Internet (IIS) com um back-end de base de dados do SQL Server 2014 no Azure.
* Efetue testes desta híbrida simulada baseado na nuvem IT carga de trabalho.

Existem três fases principais toosetting segurança deste ambiente de teste de nuvem híbrida:

1. Configure o ambiente de nuvem híbrida simulada Olá.
2. Configure o computador do servidor SQL da Olá (SQL1).
3. Configure o servidor LOB Olá (LOB1).

Esta carga de trabalho requer uma subscrição do Azure. Se tiver uma subscrição MSDN ou Visual Studio, consulte [crédito do Azure mensal para subscritores do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).

Para obter um exemplo de uma aplicação de LOB alojada no Azure de produção, consulte Olá **aplicações empresariais de linha de** blueprint de arquitetura em [diagramas de arquitetura de Software Microsoft e esquemas](http://msdn.microsoft.com/dn630664).

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a>Fase 1: Configurar o ambiente de nuvem híbrida simulada Olá
Criar Olá [ambiente de teste de cloud híbrida simulada](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Porque este ambiente de teste não requer a presença de hello do servidor de Olá APP1 na sub-rede da rede empresarial de Olá, pode encerrá-la por agora.

Esta é a configuração atual.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a>Fase 2: Configurar o computador do servidor SQL da Olá (SQL1)
De Olá portal do Azure, inicie o computador de DC2 de Olá se for necessário.

Em seguida, crie uma máquina virtual para SQL1 com estes comandos numa linha de comandos do Azure PowerShell no computador local. Toorunning anterior estes comandos, preencha Olá valores das variáveis e remover Olá < e > carateres.

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

Utilize Olá tooSQL1 tooconnect portal do Azure utilizando a conta de administrador local Olá de SQL1.

Em seguida, configure a testar conectividade básica de tooallow de regras do Firewall do Windows e o tráfego do SQL Server. Um nível de administrador do Windows PowerShell linha de comandos no SQL1, execute estes comandos.

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

comandos de ping de Olá devem resultar em quatro respostas com êxito do endereço IP 192.168.0.4.

Em seguida, adicione Olá disco de dados adicionais no SQL1 como um novo volume com letra de unidade de Olá f:.

1. No painel esquerdo do Olá do Gestor de servidores, clique em **File and Storage Services**e, em seguida, clique em **discos**.
2. No painel de conteúdo de Olá, no Olá **discos** , clique em **disco 2** (com Olá **partição** definido demasiado**desconhecido**).
3. Clique em **tarefas**e, em seguida, clique em **Novo Volume**.
4. Olá antes de começar a página do Assistente de novo Volume de Olá, clique em **seguinte**.
5. No servidor de Olá selecione Olá e página de disco, clique em **disco 2**e, em seguida, clique em **seguinte**. Quando lhe for pedido, clique em **OK**.
6. Especificar o tamanho de Olá da página de volume Olá Olá, clique em **seguinte**.
7. Olá atribuir tooa unidade letra ou pasta página, clique em **seguinte**.
8. Na página de definições de sistema de ficheiros selecione Olá, clique em **seguinte**.
9. Na página Olá confirmar seleções, clique em **criar**.
10. Quando terminar, clique em **fechar**.

Execute estes comandos na linha de comandos do Windows PowerShell Olá no SQL1:

    md f:\Data
    md f:\Log
    md f:\Backup

Em seguida, associe o domínio CORP Windows Server Active Directory de toohello de SQL1 com estes comandos na linha de comandos do Olá do Windows PowerShell no SQL1.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

Utilizar a conta de Olá CORP\User1 quando lhe forem pedidas as credenciais da conta de domínio toosupply para Olá **Add-Computer** comando.

Depois de reiniciar, utilize Olá tooconnect portal do Azure tooSQL1 *com a conta de administrador local Olá de SQL1*.

Em seguida, configure a unidade de f: de Olá do SQL Server 2014 toouse para novas bases de dados e para permissões de conta de utilizador.

1. A partir do ecrã de início de Olá, escreva **SQL Server Management**e, em seguida, clique em **SQL Server 2014 Management Studio**.
2. No **ligar tooServer**, clique em **Connect**.
3. No painel de árvore do Olá Object Explorer, clique com botão direito **SQL1**e, em seguida, clique em **propriedades**.
4. No Olá **propriedades do servidor** janela, clique em **definições de base de dados**.
5. Localizar Olá **localizações predefinidas de base de dados** e defina estes valores: 
   * Para **dados**, o caminho do tipo Olá **f:\Data**.
   * Para **registo**, o caminho do tipo Olá **f:\Log**.
   * Para **cópia de segurança**, o caminho do tipo Olá **f:\Backup**.
   * Nota: Só novas bases de dados, utilize estas localizações.
6. Clique em Olá **OK** janela de Olá tooclose.
7. No Olá **Object Explorer** painel de árvore, abra **segurança**.
8. Clique com botão direito **inícios de sessão** e, em seguida, clique em **novo início de sessão**.
9. No **nome de início de sessão**, tipo **CORP\User1**.
10. No Olá **funções de servidor** página, clique em **sysadmin**e, em seguida, clique em **OK**.
11. Feche o Microsoft SQL Server Management Studio.

Esta é a configuração atual.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a>Passo 3: Configurar o servidor LOB Olá (LOB1)
Em primeiro lugar, crie uma máquina virtual para LOB1 com estes comandos na linha de comandos do Azure PowerShell Olá no seu computador local.

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

Em seguida, utilize Olá tooconnect portal do Azure tooLOB1 com credenciais de Olá da conta de administrador local Olá do LOB1.

Em seguida, configure um tráfego de tooallow de regra de Firewall do Windows para testar a conectividade básica. A partir de uma nível de administrador do Windows PowerShell linha de comandos no LOB1, execute estes comandos.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

comandos de ping de Olá devem resultar em quatro respostas com êxito do endereço IP 192.168.0.4.

Em seguida, associe domínio de Active Directory CORP toohello LOB1 com estes comandos na linha de comandos do Olá do Windows PowerShell.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

Utilizar a conta de Olá CORP\User1 quando lhe forem pedidas as credenciais da conta de domínio toosupply para Olá **Add-Computer** comando.

Depois de reiniciar, utilize Olá tooconnect portal do Azure tooLOB1 com a conta de Olá CORP\User1 e a palavra-passe.

Em seguida, configurar LOB1 para o IIS e testar o acesso a partir de CLIENT1.

1. No Gestor de servidores, clique em **para adicionar funções e funcionalidades**.
2. No Olá **antes de começar** página, clique em **seguinte**.
3. No Olá **selecionar tipo de instalação** página, clique em **seguinte**.
4. No Olá **servidor de destino selecione** página, clique em **seguinte**.
5. No Olá **funções de servidor** página, clique em **servidor Web (IIS)** na lista de Olá de **funções**.
6. Quando lhe for pedido, clique em **adicionar funcionalidades**e, em seguida, clique em **seguinte**.
7. No Olá **selecionar funcionalidades** página, clique em **seguinte**.
8. No Olá **servidor Web (IIS)** página, clique em **seguinte**.
9. No Olá **selecionar serviços de função** página, selecione ou desmarque as caixas de verificação de Olá para serviços de Olá precisa para testar a aplicação de LOB e, em seguida, clique em **seguinte**.
10. No Olá **confirmar seleções de instalação** página, clique em **instalar**.
11. Aguarde pela conclusão da instalação dos componentes Olá e, em seguida, clique em **fechar**.
12. A partir do portal do Azure Olá, ligar o computador de CLIENT1 toohello com as credenciais de conta de CORP\User1 Olá e, em seguida, inicie o Internet Explorer.
13. Na barra de endereço Olá, escreva **http://lob1/** e, em seguida, prima ENTER. Deverá ver a página de web IIS 8 do Olá predefinida.

Esta é a configuração atual.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

Este ambiente está agora pronto para lhe toodeploy a baseada na web aplicação LOB1 e teste a funcionalidade de CLIENT1 na sub-rede da rede empresarial de Olá.

## <a name="next-step"></a>Passo seguinte
* Adicionar uma nova máquina virtual utilizando Olá [portal do Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

