---
title: "Validar VPN débito tooa Microsoft Azure Virtual Network | Microsoft Docs"
description: "Olá objetivo deste documento é toohelp um utilizador validar o débito de rede Olá do respetivo tooan de recursos no local máquina virtual do Azure."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: jasmc
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2017
ms.author: radwiv;chadmat;genli
ms.openlocfilehash: 9cf0b67145645a3c2a9556b0cc910066cc62a9ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a><span data-ttu-id="c7772-103">Como toovalidate VPN tooa virtual uma rede de débito</span><span class="sxs-lookup"><span data-stu-id="c7772-103">How toovalidate VPN throughput tooa virtual network</span></span>

<span data-ttu-id="c7772-104">Uma ligação de gateway VPN permite-lhe tooestablish segura, uma conectividade entre instalações entre a rede Virtual no Azure e no local infraestrutura de TI.</span><span class="sxs-lookup"><span data-stu-id="c7772-104">A VPN gateway connection enables you tooestablish secure, cross-premises connectivity between your Virtual Network within Azure and your on-premises IT infrastructure.</span></span>

<span data-ttu-id="c7772-105">Este artigo mostra como toovalidate o débito de rede de Olá no local recursos tooan máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7772-105">This article shows how toovalidate network throughput from hello on-premises resources tooan Azure virtual machine.</span></span> <span data-ttu-id="c7772-106">Também fornece orientações de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="c7772-106">It also provides troubleshooting guidance.</span></span>

>[!NOTE]
><span data-ttu-id="c7772-107">Este artigo destina toohelp diagnosticar e corrigir problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="c7772-107">This article is intended toohelp diagnose and fix common issues.</span></span> <span data-ttu-id="c7772-108">Se tiver o problema de Olá toosolve não é possível utilizando Olá seguintes informações, [contacte o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="c7772-108">If you're unable toosolve hello issue by using hello following information, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="c7772-109">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="c7772-109">Overview</span></span>

<span data-ttu-id="c7772-110">Olá ligação de gateway VPN envolve Olá os seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="c7772-110">hello VPN gateway connection involves hello following components:</span></span>

- <span data-ttu-id="c7772-111">Dispositivo VPN no local (ver uma lista de [validado dispositivos VPN)](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="c7772-111">On-premises VPN device (view a list of [validated VPN devices)](vpn-gateway-about-vpn-devices.md#devicetable).</span></span>
- <span data-ttu-id="c7772-112">Internet pública</span><span class="sxs-lookup"><span data-stu-id="c7772-112">Public Internet</span></span>
- <span data-ttu-id="c7772-113">Gateway VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="c7772-113">Azure VPN gateway</span></span>
- <span data-ttu-id="c7772-114">Máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="c7772-114">Azure virtual machine</span></span>

<span data-ttu-id="c7772-115">Olá seguinte diagrama mostra a conectividade de lógica de Olá de um tooan de rede no local rede virtual do Azure através de VPN.</span><span class="sxs-lookup"><span data-stu-id="c7772-115">hello following diagram shows hello logical connectivity of an on-premises network tooan Azure virtual network through VPN.</span></span>

![Rede de lógica tooMSFT de conectividade de rede de cliente através da VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a><span data-ttu-id="c7772-117">Calcular Olá máximo esperado entrada/saída</span><span class="sxs-lookup"><span data-stu-id="c7772-117">Calculate hello maximum expected ingress/egress</span></span>

1.  <span data-ttu-id="c7772-118">Determine os requisitos de débito de linha de base da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="c7772-118">Determine your application's baseline throughput requirements.</span></span>
2.  <span data-ttu-id="c7772-119">Determine os limites de débito do gateway de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7772-119">Determine your Azure VPN gateway throughput limits.</span></span> <span data-ttu-id="c7772-120">Para obter ajuda, consulte a secção Olá "débito agregado por tipo de SKU e a VPN" [planeamento e design para o Gateway de VPN](vpn-gateway-plan-design.md).</span><span class="sxs-lookup"><span data-stu-id="c7772-120">For help, see hello "Aggregate throughput by SKU and VPN type" section of [Planning and design for VPN Gateway](vpn-gateway-plan-design.md).</span></span>
3.  <span data-ttu-id="c7772-121">Determinar Olá [orientações de débito de VM do Azure](../virtual-machines/virtual-machines-windows-sizes.md) para o tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="c7772-121">Determine hello [Azure VM throughput guidance](../virtual-machines/virtual-machines-windows-sizes.md) for your VM size.</span></span>
4.  <span data-ttu-id="c7772-122">Determine a largura de banda do fornecedor de serviços Internet (ISP).</span><span class="sxs-lookup"><span data-stu-id="c7772-122">Determine your Internet Service Provider (ISP) bandwidth.</span></span>
5.  <span data-ttu-id="c7772-123">Calcular o débito esperado - menos largura de banda de Internet (ISP VM, Gateway,) * 0.8.</span><span class="sxs-lookup"><span data-stu-id="c7772-123">Calculate your expected throughput - Least bandwidth of (VM, Gateway, ISP) * 0.8.</span></span>

<span data-ttu-id="c7772-124">Se o débito calculado não cumpre os requisitos de débito de linha de base da sua aplicação, terá de largura de banda do tooincrease Olá de recursos de Olá que identificou como estrangulamento Olá.</span><span class="sxs-lookup"><span data-stu-id="c7772-124">If your calculated throughput does not meet your application's baseline throughput requirements, you need tooincrease hello bandwidth of hello resource that you identified as hello bottleneck.</span></span> <span data-ttu-id="c7772-125">tooresize um Gateway de VPN do Azure, consulte [alterar um SKU de gateway](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="c7772-125">tooresize an Azure VPN Gateway, see [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="c7772-126">tooresize uma máquina virtual, consulte [redimensionar uma VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span><span class="sxs-lookup"><span data-stu-id="c7772-126">tooresize a virtual machine, see [Resize a VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span></span> <span data-ttu-id="c7772-127">Se não ocorrerem esperada largura de banda de Internet, também poderá toocontact seu ISP.</span><span class="sxs-lookup"><span data-stu-id="c7772-127">If you are not experiencing expected Internet bandwidth, you may also want toocontact your ISP.</span></span>

## <a name="validate-network-throughput-by-using-performance-tools"></a><span data-ttu-id="c7772-128">Validar o débito de rede utilizando ferramentas de desempenho</span><span class="sxs-lookup"><span data-stu-id="c7772-128">Validate network throughput by using performance tools</span></span>

<span data-ttu-id="c7772-129">Esta validação deve ser efetuada durante o horário de pico, como saturação de débito de túnel VPN durante o teste não atribua resultados precisos.</span><span class="sxs-lookup"><span data-stu-id="c7772-129">This validation should be performed during non-peak hours, as VPN tunnel throughput saturation during testing does not give accurate results.</span></span>

<span data-ttu-id="c7772-130">ferramenta de Olá que utilizamos para este teste é iPerf, que funciona no Windows e Linux e tem os modos de cliente e servidor.</span><span class="sxs-lookup"><span data-stu-id="c7772-130">hello tool we use for this test is iPerf, which works on both Windows and Linux and has both client and server modes.</span></span> <span data-ttu-id="c7772-131">É limitado too3 Gbps para VMs do Windows.</span><span class="sxs-lookup"><span data-stu-id="c7772-131">It is limited too3 Gbps for Windows VMs.</span></span>

<span data-ttu-id="c7772-132">Esta ferramenta não efetua qualquer toodisk de operações de leitura/escrita.</span><span class="sxs-lookup"><span data-stu-id="c7772-132">This tool does not perform any read/write operations toodisk.</span></span> <span data-ttu-id="c7772-133">Produz apenas tráfego TCP gerado automaticamente a partir de um toohello final outros.</span><span class="sxs-lookup"><span data-stu-id="c7772-133">It solely produces self-generated TCP traffic from one end toohello other.</span></span> <span data-ttu-id="c7772-134">Gerou com base na experimentação que mede Olá largura de banda disponível entre os nós cliente e servidor de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c7772-134">It generated statistics based on experimentation that measures hello bandwidth available between client and server nodes.</span></span> <span data-ttu-id="c7772-135">Ao testar entre dois nós, um atua como servidor de Olá e Olá como um cliente.</span><span class="sxs-lookup"><span data-stu-id="c7772-135">When testing between two nodes, one acts as hello server and hello other as a client.</span></span> <span data-ttu-id="c7772-136">Depois deste teste está concluído, recomendamos que inverte Olá funções tootest ambos carregar e transferir o débito em ambos os nós.</span><span class="sxs-lookup"><span data-stu-id="c7772-136">Once this test is completed, we recommend that you reverse hello roles tootest both upload and download throughput on both nodes.</span></span>

### <a name="download-iperf"></a><span data-ttu-id="c7772-137">Transferir iPerf</span><span class="sxs-lookup"><span data-stu-id="c7772-137">Download iPerf</span></span>
<span data-ttu-id="c7772-138">Transferir [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span><span class="sxs-lookup"><span data-stu-id="c7772-138">Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span></span> <span data-ttu-id="c7772-139">Para obter mais informações, consulte [iPerf documentação](https://iperf.fr/iperf-doc.php).</span><span class="sxs-lookup"><span data-stu-id="c7772-139">For details, see [iPerf documentation](https://iperf.fr/iperf-doc.php).</span></span>

 >[!NOTE]
 ><span data-ttu-id="c7772-140">os produtos de terceiros de Olá que este artigo aborda são fabricados por empresas que são independentes da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c7772-140">hello third-party products that this article discusses are manufactured by companies that are independent of Microsoft.</span></span> <span data-ttu-id="c7772-141">Microsoft não faz nenhuma garantia, implícita ou, caso contrário, sobre desempenho Olá ou fiabilidade destes produtos.</span><span class="sxs-lookup"><span data-stu-id="c7772-141">Microsoft makes no warranty, implied or otherwise, about hello performance or reliability of these products.</span></span>
 >
 >

### <a name="run-iperf-iperf3exe"></a><span data-ttu-id="c7772-142">Executar iPerf (iperf3.exe)</span><span class="sxs-lookup"><span data-stu-id="c7772-142">Run iPerf (iperf3.exe)</span></span>
1. <span data-ttu-id="c7772-143">Ative uma regra NSG/ACL a permitir o tráfego de Olá (para o endereço IP público teste numa VM do Azure).</span><span class="sxs-lookup"><span data-stu-id="c7772-143">Enable an NSG/ACL rule allowing hello traffic (for public IP address testing on Azure VM).</span></span>

2. <span data-ttu-id="c7772-144">Em ambos os nós, ative uma exceção de firewall para a porta 5001.</span><span class="sxs-lookup"><span data-stu-id="c7772-144">On both nodes, enable a firewall exception for port 5001.</span></span>

    <span data-ttu-id="c7772-145">**Windows:** seguinte Olá de execução de comandos como administrador:</span><span class="sxs-lookup"><span data-stu-id="c7772-145">**Windows:** Run hello following command as an administrator:</span></span>

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    <span data-ttu-id="c7772-146">regra de Olá tooremove quando o teste estiver concluída, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="c7772-146">tooremove hello rule when testing is complete, run this command:</span></span>

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    <span data-ttu-id="c7772-147">**Linux do Azure:** permissiva firewalls de ter imagens de Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7772-147">**Azure Linux:**  Azure Linux images have permissive firewalls.</span></span> <span data-ttu-id="c7772-148">Se existir uma aplicação à escuta numa porta, o tráfego de Olá é permitido através de.</span><span class="sxs-lookup"><span data-stu-id="c7772-148">If there is an application listening on a port, hello traffic is allowed through.</span></span> <span data-ttu-id="c7772-149">Imagens personalizadas que são protegidas podem ter portas abertas explicitamente.</span><span class="sxs-lookup"><span data-stu-id="c7772-149">Custom images that are secured may need ports opened explicitly.</span></span> <span data-ttu-id="c7772-150">Firewalls de camada de SO Linux comuns incluem `iptables`, `ufw`, ou `firewalld`.</span><span class="sxs-lookup"><span data-stu-id="c7772-150">Common Linux OS-layer firewalls include `iptables`, `ufw`, or `firewalld`.</span></span>

3. <span data-ttu-id="c7772-151">No nó de servidor Olá, altere o diretório de toohello onde iperf3.exe é extraído.</span><span class="sxs-lookup"><span data-stu-id="c7772-151">On hello server node, change toohello directory where iperf3.exe is extracted.</span></span> <span data-ttu-id="c7772-152">Em seguida, executar iPerf no modo de servidor e defina-o toolisten na porta 5001 como Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c7772-152">Then run iPerf in server mode and set it toolisten on port 5001 as hello following commands:</span></span>

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. <span data-ttu-id="c7772-153">No nó de cliente Olá, altere o diretório de toohello em que iperf ferramenta é extraída e, em seguida, executar Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c7772-153">On hello client node, change toohello directory where iperf tool is extracted and then run hello following command:</span></span>

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    <span data-ttu-id="c7772-154">cliente de Olá é inducing tráfego no servidor de toohello 5001 de porta para 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="c7772-154">hello client is inducing traffic on port 5001 toohello server for 30 seconds.</span></span> <span data-ttu-id="c7772-155">Olá sinalizador '-P ' que indica que estamos a utilizar um nó do servidor toohello ligações simultâneas 32.</span><span class="sxs-lookup"><span data-stu-id="c7772-155">hello flag '-P ' that indicates we are using 32 simultaneous connections toohello server node.</span></span>

    <span data-ttu-id="c7772-156">Olá ecrã seguinte mostra saída Olá neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="c7772-156">hello following screen shows hello output from this example:</span></span>

    ![Saída](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. <span data-ttu-id="c7772-158">(Opcional) toopreserve Olá testar os resultados, executados este comando:</span><span class="sxs-lookup"><span data-stu-id="c7772-158">(OPTIONAL) toopreserve hello testing results, run this command:</span></span>

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. <span data-ttu-id="c7772-159">Depois de concluir os passos anteriores Olá, execute Olá mesmos passos com funções de Olá inversa, para que hello nó de servidor irá agora ser cliente Olá e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="c7772-159">After completing hello previous steps, execute hello same steps with hello roles reversed, so that hello server node will now be hello client and vice-versa.</span></span>

## <a name="address-slow-file-copy-issues"></a><span data-ttu-id="c7772-160">Resolver problemas de cópia de ficheiros lenta</span><span class="sxs-lookup"><span data-stu-id="c7772-160">Address slow file copy issues</span></span>
<span data-ttu-id="c7772-161">Pode deparar-se ficheiro lento coping quando utilizar o Explorador do Windows ou a arrastar e largar através de uma sessão do RDP.</span><span class="sxs-lookup"><span data-stu-id="c7772-161">You may experience slow file coping when using Windows Explorer or dragging and dropping through an RDP session.</span></span> <span data-ttu-id="c7772-162">Este problema é normalmente devido tooone ou ambos Olá seguintes fatores:</span><span class="sxs-lookup"><span data-stu-id="c7772-162">This problem is normally due tooone or both of hello following factors:</span></span>

- <span data-ttu-id="c7772-163">Aplicações de cópia de ficheiros, como o Explorador do Windows e RDP, não utilizam vários threads ao copiar ficheiros.</span><span class="sxs-lookup"><span data-stu-id="c7772-163">File copy applications, such as Windows Explorer and RDP, do not use multiple threads when copying files.</span></span> <span data-ttu-id="c7772-164">Para um melhor desempenho, utilize uma aplicação de cópia de ficheiros com vários threads, como [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy ficheiros através da utilização de 32 ou 16 threads.</span><span class="sxs-lookup"><span data-stu-id="c7772-164">For better performance, use a multi-threaded file copy application such as [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy files by using 16 or 32 threads.</span></span> <span data-ttu-id="c7772-165">número de threads de Olá toochange para cópia de ficheiros no Richcopy, clique em **ação** > **copiar opções** > **cópia do ficheiro**.</span><span class="sxs-lookup"><span data-stu-id="c7772-165">toochange hello thread number for file copy in Richcopy, click **Action** > **Copy options** > **File copy**.</span></span><br><br><span data-ttu-id="c7772-166">
![Problemas de cópia de ficheiros lenta](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span><span class="sxs-lookup"><span data-stu-id="c7772-166">
![Slow file copy issues](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span></span><br>
- <span data-ttu-id="c7772-167">Velocidade de leitura/escrita do disco VM insuficiente.</span><span class="sxs-lookup"><span data-stu-id="c7772-167">Insufficient VM disk read/write speed.</span></span> <span data-ttu-id="c7772-168">Para obter mais informações, consulte [resolução de problemas de armazenamento do Azure](../storage/common/storage-e2e-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="c7772-168">For more information, see [Azure Storage Troubleshooting](../storage/common/storage-e2e-troubleshooting.md).</span></span>

## <a name="on-premises-device-external-facing-interface"></a><span data-ttu-id="c7772-169">Interface com acesso externo dispositivo no local</span><span class="sxs-lookup"><span data-stu-id="c7772-169">On-premises device external facing interface</span></span>
<span data-ttu-id="c7772-170">Se Olá no local o dispositivo VPN endereço IP de acesso à Internet está incluído no Olá [rede local](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definição no Azure, pode deparar-se incapacidade toobring Olá desliga a VPN, esporádicas ou problemas de desempenho.</span><span class="sxs-lookup"><span data-stu-id="c7772-170">If hello on-premises VPN device Internet-facing IP address is included in hello [local network](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definition in Azure, you may experience inability toobring up hello VPN, sporadic disconnects, or performance issues.</span></span>

## <a name="checking-latency"></a><span data-ttu-id="c7772-171">A verificação de latência</span><span class="sxs-lookup"><span data-stu-id="c7772-171">Checking latency</span></span>
<span data-ttu-id="c7772-172">Utilize tracert tootrace tooMicrosoft Azure Edge dispositivo toodetermine se existem quaisquer atrasos exceder os 100 ms entre saltos.</span><span class="sxs-lookup"><span data-stu-id="c7772-172">Use tracert tootrace tooMicrosoft Azure Edge device toodetermine if there are any delays exceeding 100 ms between hops.</span></span>

<span data-ttu-id="c7772-173">A partir da rede no local de Olá, execute *tracert* toohello VIP de Olá Gateway do Azure ou de VM.</span><span class="sxs-lookup"><span data-stu-id="c7772-173">From hello on-premises network, run *tracert* toohello VIP of hello Azure Gateway or VM.</span></span> <span data-ttu-id="c7772-174">Assim que só vê * devolvido, sabe que foi atingido Olá limite do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7772-174">Once you see only * returned, you know you have reached hello Azure edge.</span></span> <span data-ttu-id="c7772-175">Quando vir nomes DNS que incluem "MSN" devolvido, sabe que atingiu o principal de Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="c7772-175">When you see DNS names that include "MSN" returned, you know you have reached hello Microsoft backbone.</span></span><br><br><span data-ttu-id="c7772-176">
![A verificação de latência](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span><span class="sxs-lookup"><span data-stu-id="c7772-176">
![Checking Latency](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7772-177">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c7772-177">Next steps</span></span>
<span data-ttu-id="c7772-178">Para obter mais informações ou ajuda, consulte Olá seguintes ligações:</span><span class="sxs-lookup"><span data-stu-id="c7772-178">For more information or help, check out hello following links:</span></span>

- [<span data-ttu-id="c7772-179">Otimizar o débito de rede para máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="c7772-179">Optimize network throughput for Azure virtual machines</span></span>](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [<span data-ttu-id="c7772-180">Suporte da Microsoft</span><span class="sxs-lookup"><span data-stu-id="c7772-180">Microsoft Support</span></span>](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
