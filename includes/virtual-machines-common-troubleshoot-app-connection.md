Existem várias razões quando não é possível iniciar ou ligar a aplicação de tooan em execução numa máquina virtual do Azure (VM). Por motivos incluem aplicação Olá não está em execução ou a escutar nas portas Olá esperado, Olá a porta de escuta bloqueado ou regras correctamente transmitir aplicação toohello de tráfego de rede. Este artigo descreve uma abordagem methodical toofind e problema Olá correto.

Se estiver a ter problemas em ligar tooyour VM utilizando o RDP ou SSH, consulte um dos seguintes Olá artigos primeiro:

* [Resolver problemas de ligações de ambiente de trabalho remoto tooa baseados em Windows Máquina Virtual do Azure](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)
* [Resolver problemas de Secure Shell (SSH) ligações tooa baseado em Linux máquina virtual do Azure](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).

> [!NOTE]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../articles/resource-manager-deployment-model.md). Este artigo abrange os dois modelos, mas a Microsoft recomenda que as implementações mais novas utilizem o modelo do Resource Manager Olá.

Se precisar de mais ajuda, a qualquer altura neste artigo, pode contactar Olá especialistas do Azure no [Olá MSDN Azure e Olá Stack Overflow fóruns](https://azure.microsoft.com/support/forums/). Em alternativa, pode também ficheiro um incidente de suporte do Azure. Aceda toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e selecione **obter suporta**.

## <a name="quick-start-troubleshooting-steps"></a>Passos de resolução de problemas de início rápido
Se tiver problemas de ligação tooan aplicação, tente seguir os passos de resolução de problemas gerais de Olá. Depois de cada passo, tente estabelecer ligação novamente tooyour aplicação:

* Reiniciar a máquina virtual de Olá
* Recrie o ponto final de Olá / regras de firewall / regras de segurança de grupo (NSG) de rede
  * [Modelo do Resource Manager - gerir grupos de segurança de rede](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
  * [Modelo de clássico - pontos finais de gerir os serviços Cloud](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
* Ligar a partir de uma localização diferente, tal como uma rede virtual do Azure diferente
* Volte a implementar máquina virtual de Olá
  * [Reimplementar a VM do Windows](../articles/virtual-machines/windows/redeploy-to-new-node.md)
  * [Reimplementar a VM com Linux](../articles/virtual-machines/linux/redeploy-to-new-node.md)
* Recriar a máquina virtual de Olá

Para obter mais informações, consulte [resolução de problemas de Conetividade de ponto final (RDP/SSH/HTTP, falhas de etc.)](https://social.msdn.microsoft.com/Forums/azure/en-US/538a8f18-7c1f-4d6e-b81c-70c00e25c93d/troubleshooting-endpoint-connectivity-rdpsshhttp-etc-failures?forum=WAVirtualMachinesforWindows).

## <a name="detailed-troubleshooting-overview"></a>Descrição geral de resolução de problemas detalhada
Existem quatro áreas principais acesso de Olá tootroubleshoot de uma aplicação que está a ser executado numa máquina virtual do Azure.

![resolver problemas de não é possível iniciar a aplicação](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access1.png)

1. aplicação Olá em execução no Olá máquina virtual do Azure.
   * Aplicação Olá propriamente dito está a funcionar corretamente?
2. Olá máquina virtual do Azure.
   * Olá própria VM está a ser executado corretamente e responder toorequests?
3. Pontos finais de rede do Azure.
   * Pontos finais de serviço para máquinas virtuais no modelo de implementação clássica Olá da nuvem.
   * Grupos de segurança de rede e regras NAT de entrada para máquinas virtuais no modelo de implementação do Resource Manager.
   * Pode tráfego o fluxo de utilizadores toohello VM/aplicação em portas Olá esperada?
4. O dispositivo de limite de Internet.
   * São as regras de firewall no local impedir que o tráfego que flui corretamente?

Para computadores de cliente que estão a aceder a aplicação Olá através de uma ligação de VPN ou ExpressRoute do site para site, as áreas principais Olá que podem causar problemas são aplicação Olá e Olá máquina virtual do Azure.

origem de Olá toodetermine de problema de Olá e a correção, siga estes passos.

## <a name="step-1-access-application-from-target-vm"></a>Passo 1: Aceder à aplicação a partir do destino VM
Tente tooaccess Olá aplicação com o programa de cliente adequado Olá VM Olá no qual está a ser executado. Utilize o nome de anfitrião local Olá, o endereço IP local Olá ou o endereço de loopback Olá (127.0.0.1).

![iniciar a aplicação diretamente a partir de Olá VM](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access2.png)

Por exemplo, se a aplicação de Olá é um servidor web, abra um browser no Olá VM e tente tooaccess uma página web alojadas no Olá VM.

Se pode aceder à aplicação Olá, aceda demasiado[passo 2](#step2).

Se não é possível aceder à aplicação Olá, certifique-se Olá seguintes definições:

* aplicação Olá está em execução na máquina de virtual de destino Olá.
* aplicação Olá está a escutar nas portas TCP e UDP de Olá esperado.

No Windows e máquinas virtuais baseadas em Linux, utilize Olá **netstat - um** comando tooshow Olá as portas de escuta Active Directory. Examine a saída de Olá para portas Olá esperado no qual deve deve ainda ouvir a sua aplicação. Reiniciar a aplicação Olá ou configurar portas de Olá esperado toouse conforme necessário e tente novamente a aplicação de Olá tooaccess localmente.

## <a id="step2"></a>Passo 2: Aceder à aplicação a partir de outra VM na Olá mesma rede virtual
Tente tooaccess aplicação Olá VM diferente, mas no Olá mesma rede virtual, com o nome do anfitrião da VM Olá ou o Azure atribuído public, private ou fornecedor de endereço IP. Para máquinas virtuais criadas com o modelo de implementação clássica Olá, não utilize o endereço IP público de Olá do serviço de nuvem Olá.

![iniciar a aplicação de uma VM diferente](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access3.png)

Por exemplo, se a aplicação de Olá é um servidor web, tooaccess tente uma web página num browser numa VM diferente no Olá mesma rede virtual.

Se pode aceder à aplicação Olá, aceda demasiado[passo 3](#step3).

Se não é possível aceder à aplicação Olá, certifique-se Olá seguintes definições:

* firewall de anfitrião Olá no destino Olá VM está a permitir tráfego de saída de resposta e pedido de entrada Olá.
* Deteção de intrusões ou software em execução numa VM de destino Olá de monitorização de rede está a permitir o tráfego de Olá.
* Pontos finais de serviços em nuvem ou grupos de segurança de rede estão a permitir o tráfego de Olá:
  * [Modelo de clássico - pontos finais de gerir os serviços Cloud](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
  * [Modelo do Resource Manager - gerir grupos de segurança de rede](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
* Um componente separado em execução na sua VM no caminho de Olá entre teste Olá VM e a VM, como um balanceador de carga ou uma firewall, está a permitir o tráfego de Olá.

Numa máquina virtual baseado no Windows, utilize a Firewall do Windows com segurança avançada toodetermine se as regras de firewall de Olá excluir o tráfego de entrada e saída da sua aplicação.

## <a id="step3"></a>Passo 3: Aceder à aplicação a partir da rede virtual de Olá externa
Tente tooaccess aplicação Olá de um computador fora da rede virtual Olá como VM Olá no qual a aplicação Olá está em execução. Utilize uma rede diferente que o computador cliente original.

![iniciar a aplicação de um computador fora da rede virtual Olá](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access4.png)

Por exemplo, se a aplicação de Olá é um servidor web, tente tooaccess Olá web página num browser em execução num computador que não se encontra na rede virtual Olá.

Se não é possível aceder à aplicação Olá, certifique-se Olá seguintes definições:

* Para VMs criada utilizando o modelo de implementação clássica Olá:
  
  * Certifique-se de que configuração de ponto final de Olá para Olá que VM está a permitir o tráfego recebido Olá, especialmente protocolo Olá (TCP ou UDP) e números de porta pública e privada Olá.
  * Certifique-se de que as listas de controlo de acesso (ACLs) no ponto final de Olá não estão a impedir tráfego de entrada de Olá Internet.
  * Para obter mais informações, consulte [como tooSet pontos finais de cópia de segurança tooa Máquina Virtual](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* Para VMs criadas utilizando o modelo de implementação do Resource Manager Olá:
  
  * Certifique-se de que Olá entrada configuração da regra NAT para Olá que VM está a permitir o tráfego recebido Olá, especialmente protocolo Olá (TCP ou UDP) e números de porta pública e privada Olá.
  * Certifique-se de que os grupos de segurança de rede estão a permitir tráfego de saída de resposta e pedido de entrada Olá.
  * Para obter mais informações, consulte o artigo [O que é um Grupo de Segurança de Rede (NSG)?](../articles/virtual-network/virtual-networks-nsg.md)

Se a máquina virtual de Olá ou o ponto final é um membro de um conjunto com balanceamento de carga:

* Certifique-se de que o protocolo de sonda de Olá (TCP ou UDP) e o número da porta estão corretos.
* Se a pesquisa de Olá protocolo e porta é diferente de Olá conjunto com balanceamento de carga protocolo e porta:
  * Certifique-se de que a aplicação Olá é escutar no protocolo de sonda de Olá (TCP ou UDP) e o número de porta (utilizar **netstat – a** no Olá destino VM).
  * Certifique-se de que Olá anfitrião a firewall no destino Olá que VM está a permitir o pedido de entrada de sonda de Olá e tráfego de resposta de sonda de saída.

Se pode aceder à aplicação Olá, certifique-se de que o seu dispositivo de limite de Internet está a permitir:

* tráfego de pedido de aplicação de saída de Olá da sua toohello do computador cliente máquina virtual do Azure.
* Olá tráfego de resposta de aplicação de entrada de Olá máquina virtual do Azure.

## <a name="step-4-if-you-cannot-access-hello-application-use-ip-verify-toocheck-hello-settings"></a>Passo 4, se não é possível aceder à aplicação Olá, utilizar IP verifique toocheck Olá definições. 

Para obter mais informações, consulte [descrição geral da monitorização de rede do Azure](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview). 

## <a name="additional-resources"></a>Recursos adicionais
[Resolver problemas de ligações de ambiente de trabalho remoto tooa baseados em Windows Máquina Virtual do Azure](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)

[Resolver problemas de Secure Shell (SSH) ligações tooa baseado em Linux máquina virtual do Azure](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)

