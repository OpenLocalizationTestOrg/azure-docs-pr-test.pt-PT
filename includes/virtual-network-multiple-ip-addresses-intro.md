> [!div class="op_single_selector"]
> * [Portal](../articles/virtual-network/virtual-network-multiple-ip-addresses-portal.md)
> * [PowerShell](../articles/virtual-network/virtual-network-multiple-ip-addresses-powershell.md)
> * [CLI 2.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli.md)
> * [CLI 1.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli-nodejs.md)
> * [Modelo](../articles/virtual-network/virtual-network-multiple-ip-addresses-template.md)
>

Uma Máquina Virtual do Azure (VM) tem um ou mais interfaces de rede (NIC) ligado tooit. Qualquer NIC pode ter um ou mais estático ou dinâmico IP público e privado endereços tooit atribuído. Atribuição de IP de vários endereços tooa VM permite Olá seguintes capacidades:

* Alojar vários Web Sites ou serviços com diferentes endereços IP e certificados SSL num único servidor.
* Servir de dispositivo virtual de rede, como uma firewall ou um balanceador de carga.
* Olá tooadd capacidade qualquer IP privado Olá endereços para qualquer uma das Olá NICs tooan conjunto de back-end de Balanceador de carga do Azure. Olá passado apenas Olá primário do endereço IP Olá que NIC primário pode ser adicionados tooa conjunto de back-end. mais informações sobre como toolearn como tooload equilibrar várias configurações de IP, leia Olá [várias configurações de IP de balanceamento de carga](../articles/load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo.

Cada tooa NIC anexado VM tem um ou mais configurações de IP associadas tooit. A cada configuração é atribuído um endereço IP privado estático ou dinâmico. Cada configuração também poderá ter um tooit de recursos associados de endereço IP público. Um recurso de endereço IP público tem ambos um dinâmica ou estática pública IP endereço atribuído tooit. endereços toolearn mais informações sobre o IP no Azure, leia Olá [endereços IP no Azure](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md) artigo. 

Não há um limite toohow muitos IP privado endereços podem ser atribuídos a NIC de tooa. Há também um limite toohow vários endereços IP públicos que podem ser utilizados numa subscrição do Azure. Consulte Olá [Azure limita](../articles/azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) artigo para obter detalhes.
