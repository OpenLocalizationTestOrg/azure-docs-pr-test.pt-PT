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
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a>Como toovalidate VPN tooa virtual uma rede de débito

Uma ligação de gateway VPN permite-lhe tooestablish segura, uma conectividade entre instalações entre a rede Virtual no Azure e no local infraestrutura de TI.

Este artigo mostra como toovalidate o débito de rede de Olá no local recursos tooan máquina virtual do Azure. Também fornece orientações de resolução de problemas.

>[!NOTE]
>Este artigo destina toohelp diagnosticar e corrigir problemas comuns. Se tiver o problema de Olá toosolve não é possível utilizando Olá seguintes informações, [contacte o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
>
>

## <a name="overview"></a>Descrição geral

Olá ligação de gateway VPN envolve Olá os seguintes componentes:

- Dispositivo VPN no local (ver uma lista de [validado dispositivos VPN)](vpn-gateway-about-vpn-devices.md#devicetable).
- Internet pública
- Gateway VPN do Azure
- Máquina virtual do Azure

Olá seguinte diagrama mostra a conectividade de lógica de Olá de um tooan de rede no local rede virtual do Azure através de VPN.

![Rede de lógica tooMSFT de conectividade de rede de cliente através da VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a>Calcular Olá máximo esperado entrada/saída

1.  Determine os requisitos de débito de linha de base da sua aplicação.
2.  Determine os limites de débito do gateway de VPN do Azure. Para obter ajuda, consulte a secção Olá "débito agregado por tipo de SKU e a VPN" [planeamento e design para o Gateway de VPN](vpn-gateway-plan-design.md).
3.  Determinar Olá [orientações de débito de VM do Azure](../virtual-machines/virtual-machines-windows-sizes.md) para o tamanho da VM.
4.  Determine a largura de banda do fornecedor de serviços Internet (ISP).
5.  Calcular o débito esperado - menos largura de banda de Internet (ISP VM, Gateway,) * 0.8.

Se o débito calculado não cumpre os requisitos de débito de linha de base da sua aplicação, terá de largura de banda do tooincrease Olá de recursos de Olá que identificou como estrangulamento Olá. tooresize um Gateway de VPN do Azure, consulte [alterar um SKU de gateway](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku). tooresize uma máquina virtual, consulte [redimensionar uma VM](../virtual-machines/virtual-machines-windows-resize-vm.md). Se não ocorrerem esperada largura de banda de Internet, também poderá toocontact seu ISP.

## <a name="validate-network-throughput-by-using-performance-tools"></a>Validar o débito de rede utilizando ferramentas de desempenho

Esta validação deve ser efetuada durante o horário de pico, como saturação de débito de túnel VPN durante o teste não atribua resultados precisos.

ferramenta de Olá que utilizamos para este teste é iPerf, que funciona no Windows e Linux e tem os modos de cliente e servidor. É limitado too3 Gbps para VMs do Windows.

Esta ferramenta não efetua qualquer toodisk de operações de leitura/escrita. Produz apenas tráfego TCP gerado automaticamente a partir de um toohello final outros. Gerou com base na experimentação que mede Olá largura de banda disponível entre os nós cliente e servidor de estatísticas. Ao testar entre dois nós, um atua como servidor de Olá e Olá como um cliente. Depois deste teste está concluído, recomendamos que inverte Olá funções tootest ambos carregar e transferir o débito em ambos os nós.

### <a name="download-iperf"></a>Transferir iPerf
Transferir [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip). Para obter mais informações, consulte [iPerf documentação](https://iperf.fr/iperf-doc.php).

 >[!NOTE]
 >os produtos de terceiros de Olá que este artigo aborda são fabricados por empresas que são independentes da Microsoft. Microsoft não faz nenhuma garantia, implícita ou, caso contrário, sobre desempenho Olá ou fiabilidade destes produtos.
 >
 >

### <a name="run-iperf-iperf3exe"></a>Executar iPerf (iperf3.exe)
1. Ative uma regra NSG/ACL a permitir o tráfego de Olá (para o endereço IP público teste numa VM do Azure).

2. Em ambos os nós, ative uma exceção de firewall para a porta 5001.

    **Windows:** seguinte Olá de execução de comandos como administrador:

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    regra de Olá tooremove quando o teste estiver concluída, execute este comando:

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    **Linux do Azure:** permissiva firewalls de ter imagens de Linux do Azure. Se existir uma aplicação à escuta numa porta, o tráfego de Olá é permitido através de. Imagens personalizadas que são protegidas podem ter portas abertas explicitamente. Firewalls de camada de SO Linux comuns incluem `iptables`, `ufw`, ou `firewalld`.

3. No nó de servidor Olá, altere o diretório de toohello onde iperf3.exe é extraído. Em seguida, executar iPerf no modo de servidor e defina-o toolisten na porta 5001 como Olá os seguintes comandos:

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. No nó de cliente Olá, altere o diretório de toohello em que iperf ferramenta é extraída e, em seguida, executar Olá os seguintes comandos:

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    cliente de Olá é inducing tráfego no servidor de toohello 5001 de porta para 30 segundos. Olá sinalizador '-P ' que indica que estamos a utilizar um nó do servidor toohello ligações simultâneas 32.

    Olá ecrã seguinte mostra saída Olá neste exemplo:

    ![Saída](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. (Opcional) toopreserve Olá testar os resultados, executados este comando:

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. Depois de concluir os passos anteriores Olá, execute Olá mesmos passos com funções de Olá inversa, para que hello nó de servidor irá agora ser cliente Olá e vice-versa.

## <a name="address-slow-file-copy-issues"></a>Resolver problemas de cópia de ficheiros lenta
Pode deparar-se ficheiro lento coping quando utilizar o Explorador do Windows ou a arrastar e largar através de uma sessão do RDP. Este problema é normalmente devido tooone ou ambos Olá seguintes fatores:

- Aplicações de cópia de ficheiros, como o Explorador do Windows e RDP, não utilizam vários threads ao copiar ficheiros. Para um melhor desempenho, utilize uma aplicação de cópia de ficheiros com vários threads, como [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy ficheiros através da utilização de 32 ou 16 threads. número de threads de Olá toochange para cópia de ficheiros no Richcopy, clique em **ação** > **copiar opções** > **cópia do ficheiro**.<br><br>
![Problemas de cópia de ficheiros lenta](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)<br>
- Velocidade de leitura/escrita do disco VM insuficiente. Para obter mais informações, consulte [resolução de problemas de armazenamento do Azure](../storage/common/storage-e2e-troubleshooting.md).

## <a name="on-premises-device-external-facing-interface"></a>Interface com acesso externo dispositivo no local
Se Olá no local o dispositivo VPN endereço IP de acesso à Internet está incluído no Olá [rede local](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definição no Azure, pode deparar-se incapacidade toobring Olá desliga a VPN, esporádicas ou problemas de desempenho.

## <a name="checking-latency"></a>A verificação de latência
Utilize tracert tootrace tooMicrosoft Azure Edge dispositivo toodetermine se existem quaisquer atrasos exceder os 100 ms entre saltos.

A partir da rede no local de Olá, execute *tracert* toohello VIP de Olá Gateway do Azure ou de VM. Assim que só vê * devolvido, sabe que foi atingido Olá limite do Azure. Quando vir nomes DNS que incluem "MSN" devolvido, sabe que atingiu o principal de Microsoft hello.<br><br>
![A verificação de latência](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações ou ajuda, consulte Olá seguintes ligações:

- [Otimizar o débito de rede para máquinas virtuais do Azure](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [Suporte da Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
