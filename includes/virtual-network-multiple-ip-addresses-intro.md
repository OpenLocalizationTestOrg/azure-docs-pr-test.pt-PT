> [!div class="op_single_selector"]
> * [Portal do Azure](../articles/virtual-network/virtual-network-multiple-ip-addresses-portal.md)
> * [PowerShell](../articles/virtual-network/virtual-network-multiple-ip-addresses-powershell.md)
> * [CLI do Azure](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli.md)
> * [Modelo](../articles/virtual-network/virtual-network-multiple-ip-addresses-template.md)
>

Uma Máquina Virtual do Azure (VM) tem uma ou mais interfaces de rede (NIC) ligadas à mesma. Qualquer NIC pode ter um ou mais endereços IP públicos e privados estáticos ou dinâmicos atribuídos à mesma. Atribuir vários endereços IP a uma VM permite as seguintes funcionalidades:

* Alojar vários Web Sites ou serviços com diferentes endereços IP e certificados SSL num único servidor.
* Servir de dispositivo virtual de rede, como uma firewall ou um balanceador de carga.
* A capacidade de adicionar qualquer um dos endereços IP privados de qualquer uma das NICs a um conjunto de back-end do Balanceador de Carga do Azure. Anteriormente, apenas era possível adicionar o endereço IP principal da NIC principal a um conjunto de back-end. Para saber mais sobre como fazer o balanceamento de carga de várias configurações de IP, leia o artigo [Balanceamento de carga de várias configurações de IP](../articles/load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

Cada NIC anexada a uma VM tem uma ou mais configurações de IP associadas à mesma. A cada configuração é atribuído um endereço IP privado estático ou dinâmico. Cada configuração também pode ter um recurso de endereço IP público associado a si. Um recurso de endereço IP público tem um endereço IP público dinâmico ou estático atribuído. Para saber mais sobre endereços IP no Azure, leia o artigo [Endereços IP no Azure](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md). 

Não há um limite para quantas endereços IP privados pode ser atribuído a um NIC. Também é um limite para quantas endereços IP públicos que pode ser utilizada numa subscrição do Azure. Veja o artigo [Limites do Azure](../articles/azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) para obter detalhes.
