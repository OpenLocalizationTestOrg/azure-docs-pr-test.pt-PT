# Descrição geral
## [Redes virtuais](virtual-networks-overview.md)
## [Encaminhamento](virtual-networks-udr-overview.md)
## [Peering de rede virtual](virtual-network-peering-overview.md)
## [Pontos finais do serviço de rede virtual](virtual-network-service-endpoints-overview.md)
## [Rede virtual para serviços do Azure](virtual-network-for-azure-services.md)
## [Segurança](security-overview.md)
## [Funcionamento em rede do contentor](container-networking.md)
## [Continuidade do negócio](virtual-network-disaster-recovery-guidance.md)
## [Endereçamento IP](virtual-network-ip-addresses-overview-arm.md)
## [Proteção contra DDOS](ddos-protection-overview.md)
## [FAQ](virtual-networks-faq.md)
## Clássica
### [Endereçamento IP](virtual-network-ip-addresses-overview-classic.md)
### [Listas de controlo de acesso](virtual-networks-acl.md)

# Introdução
## [Crie a sua primeira rede virtual](virtual-network-get-started-vnet-subnet.md)

# Procedimento
## Planear e conceber
### [Redes virtuais](virtual-network-vnet-plan-design-arm.md)
### [Grupos de segurança de rede](virtual-networks-nsg.md)

## Implementação
### [Redes virtuais](virtual-networks-create-vnet-arm-pportal.md)
#### [Azure PowerShell](virtual-networks-create-vnet-arm-ps.md)
#### [CLI do Azure](virtual-networks-create-vnet-arm-cli.md)
#### [Modelo](virtual-networks-create-vnet-arm-template-click.md)

### Grupos de segurança de rede
#### [Portal do Azure](virtual-networks-create-nsg-arm-pportal.md)
#### [Azure PowerShell](virtual-networks-create-nsg-arm-ps.md)
#### [CLI do Azure](virtual-networks-create-nsg-arm-cli.md)
#### [Modelo](virtual-networks-create-nsg-arm-template.md)
#### [Grupos de segurança de aplicações](create-network-security-group-preview.md)
#### Clássica
##### [Azure PowerShell](virtual-networks-create-nsg-classic-ps.md)
##### [CLI do Azure 1.0](virtual-networks-create-nsg-classic-cli.md)

### Rotas definidas pelo utilizador
#### [Portal do Azure](create-user-defined-route-portal.md)
#### [Azure PowerShell](virtual-network-create-udr-arm-ps.md)
#### [CLI do Azure](virtual-network-create-udr-arm-cli.md)
#### [Modelo](virtual-network-create-udr-arm-template.md)
#### Clássica
##### [Azure PowerShell](virtual-network-create-udr-classic-ps.md)
##### [CLI do Azure](virtual-network-create-udr-classic-cli.md)

### Peering de rede virtual
#### [Mesmo modelo de implementação - mesma subscrição](virtual-network-create-peering.md)
#### [Mesmo modelo de implementação - subscrições diferentes](create-peering-different-subscriptions.md)
#### [Diferentes modelos de implementação - mesma subscrição](create-peering-different-deployment-models.md)
#### [Diferentes modelos de implementação - subscrições diferentes](create-peering-different-deployment-models-subscriptions.md)

### [Pontos finais do serviço de rede virtual](virtual-network-service-endpoints-configure.md)

### Endereço IP público - zona de disponibilidade
#### [Portal do Azure](create-public-ip-availability-zone-portal.md)
#### [CLI do Azure](create-public-ip-availability-zone-cli.md)
#### [PowerShell](create-public-ip-availability-zone-powershell.md)

### Máquinas virtuais
#### [Débito de rede de máquina virtual](virtual-machine-network-throughput.md)
#### Criar uma VM com um endereço IP público estático
##### [Portal do Azure](virtual-network-deploy-static-pip-arm-portal.md)
##### [Azure PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
##### [CLI do Azure](virtual-network-deploy-static-pip-arm-cli.md)
##### [Modelo](virtual-network-deploy-static-pip-arm-template.md)
##### Clássica
###### [Azure PowerShell](virtual-networks-reserved-public-ip.md)

#### Criar VM - endereço IP privado estático
##### [Portal do Azure](virtual-networks-static-private-ip-arm-pportal.md)
##### [Azure PowerShell](virtual-networks-static-private-ip-arm-ps.md)
##### [CLI do Azure](virtual-networks-static-private-ip-arm-cli.md)
##### Clássica
###### [Portal do Azure](virtual-networks-static-private-ip-classic-pportal.md)
###### [Azure PowerShell](virtual-networks-static-private-ip-classic-ps.md)
###### [CLI do Azure](virtual-networks-static-private-ip-classic-cli.md)

#### Criar VM - várias interfaces de rede
##### [Azure PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
##### [CLI do Azure](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
##### [Modelo](virtual-network-deploy-multinic-arm-template.md)

##### Clássica
###### [Azure PowerShell](virtual-network-deploy-multinic-classic-ps.md)
###### [CLI do Azure](virtual-network-deploy-multinic-classic-cli.md)

#### Criar VM - vários endereços IP
##### [Portal do Azure](virtual-network-multiple-ip-addresses-portal.md)
##### [Azure PowerShell](virtual-network-multiple-ip-addresses-powershell.md)
##### [CLI do Azure](virtual-network-multiple-ip-addresses-cli.md)
##### [Modelo](virtual-network-multiple-ip-addresses-template.md)

#### Criar VM - redes aceleradas
##### [Azure PowerShell](create-vm-accelerated-networking-powershell.md)
##### [CLI do Azure](create-vm-accelerated-networking-cli.md)

### Cenários de conectividade
#### [Rede virtual (VNet) para VNet](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [VNet (Resource Manager) para uma VNet (Clássica)](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [VNet para rede no local (VPN)](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [VNet para rede no local (ExpressRoute)](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [Arquitetura de rede híbrida de elevada disponibilidade](../guidance/guidance-hybrid-network-expressroute-vpn-failover.md?toc=%2fazure%2fvirtual-network%2ftoc.json)

### Cenários de segurança
#### [Proteger redes com aplicações virtuais](virtual-network-scenario-udr-gw-nva.md)
#### [DMZ entre o Azure e a Internet](../guidance/guidance-iaas-ra-secure-vnet-dmz.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [Serviço em nuvem e segurança de rede](../best-practices-network-security.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
##### [Criar um DMZ com NSGs](virtual-networks-dmz-nsg.md)
##### [Criar um DMZ com NSGs (Clássico)](virtual-networks-dmz-nsg-asm.md)
##### [Criar um DMZ com firewall e NSGs (Clássico)](virtual-networks-dmz-nsg-fw-asm.md)
##### [DMZ com firewall, UDR e NSGs (Clássico)](virtual-networks-dmz-nsg-fw-udr-asm.md)

##### [Aplicação de exemplo](virtual-networks-sample-app.md)

### Clássica
#### [Rede virtual](create-virtual-network-classic.md)
##### [Portal do Azure](virtual-networks-create-vnet-classic-pportal.md)
##### [Azure PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md)
##### [CLI do Azure](virtual-networks-create-vnet-classic-cli.md)
#### [Especificar as definições de DNS num ficheiro de configuração de rede virtual](virtual-networks-specifying-a-dns-settings-in-a-virtual-network-configuration-file.md)
#### [Especificar as definições de DNS num ficheiro de configuração do serviço](virtual-networks-specifying-dns-settings-in-a-service-configuration-file.md)

## Configurar
### Máquinas virtuais
#### [Adicionar ou remover interfaces de rede](virtual-network-network-interface-vm.md)
#### [Resolução de nomes para VMs e serviços cloud](virtual-networks-name-resolution-for-vms-and-role-instances.md)
#### [Utilizar o DNS dinâmico para registar nomes de anfitrião no seu próprio servidor DNS](virtual-networks-name-resolution-ddns.md)
#### [Otimizar o débito de rede](virtual-network-optimize-network-bandwidth.md)
#### [Ver e modificar nomes de anfitriões](virtual-networks-viewing-and-modifying-hostnames.md)
#### Clássica
##### Endereços IP estáticos
###### [PowerShell](virtual-networks-reserved-private-ip.md)
###### [CLI](virtual-networks-static-private-ip-classic-cli.md)
##### [Endereço IP público ao nível da instância](virtual-networks-instance-level-public-ip.md)

### Clássica
#### Lista de controlo de acesso
##### [Portal do Azure](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
##### [Azure PowerShell](virtual-networks-acl-powershell.md)

## Gerir
### [Redes virtuais](virtual-network-manage-network.md)
#### [Sub-redes](virtual-network-manage-subnet.md)
#### [Peerings](virtual-network-manage-peering.md)
#### Clássica
##### [Ficheiro de configuração de rede](virtual-networks-using-network-configuration-file.md)
##### [Migrar de um grupo de afinidades para uma região](virtual-networks-migrate-to-regional-vnet.md)
### Grupos de segurança de rede
#### [Portal do Azure](virtual-network-manage-nsg-arm-portal.md)
#### [Azure PowerShell](virtual-network-manage-nsg-arm-ps.md)
#### [CLI do Azure](virtual-network-manage-nsg-arm-cli.md)

#### [Registos](virtual-network-nsg-manage-log.md)
### Interfaces de rede (NICs)
#### [Criar, alterar ou eliminar NICs](virtual-network-network-interface.md)
#### [Adicionar, alterar ou remover endereços IP](virtual-network-network-interface-addresses.md)
### Máquinas virtuais
#### [Mover uma VM para outra sub-rede](virtual-networks-move-vm-role-to-subnet.md)
### [Endereços IP públicos](virtual-network-public-ip-address.md)
### Proteção contra DDOS
#### [Portal do Azure](ddos-protection-manage-portal.md)
#### [Azure PowerShell](ddos-protection-manage-ps.md)

## Resolução de problemas
### Grupos de segurança de rede
#### [Portal do Azure](virtual-network-nsg-troubleshoot-portal.md)
#### [Azure PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
### Rotas
#### [Portal do Azure](virtual-network-routes-troubleshoot-portal.md)
#### [Azure PowerShell](virtual-network-routes-troubleshoot-powershell.md)
### [Teste de débito](virtual-network-bandwidth-testing.md)
### [Não é possível eliminar redes virtuais](virtual-network-troubleshoot-cannot-delete-vnet.md)
### [Problemas de conectividade VM a VM](virtual-network-troubleshoot-connectivity-problem-between-vms.md)

# Referência
## [Exemplos de código](https://azure.microsoft.com/en-us/resources/samples/?service=virtual-network)
## [Azure PowerShell (Resource Manager)](/powershell/module/azurerm.network)
## [Azure PowerShell (clássico)](/powershell/module/azure/)
## [CLI do Azure](/cli/azure/network)
## [Java](/java/api/)
## [REST (Resource Manager)](https://msdn.microsoft.com/library/mt163658.aspx)
## [REST (Clássico)](https://msdn.microsoft.com/library/jj157182.aspx)


# Relacionado
## [Máquinas Virtuais](/azure/virtual-machines/)
## [Gateway de Aplicação](/azure/application-gateway/)
## [DNS do Azure](/azure/dns/)
## [Gestor de Tráfego](/azure/traffic-manager/)
## [Balanceador de Carga](/azure/load-balancer/)
## [Gateway de VPN](/azure/vpn-gateway/)
## [ExpressRoute](/azure/expressroute/)

# Recursos
## [Mapa do Azure](https://azure.microsoft.com/roadmap/?category=networking)
## [Blogue das redes](http://azure.microsoft.com/blog/topics/networking)
## [Fórum de redes](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesVirtualNetwork)
## [Preços](https://azure.microsoft.com/pricing/details/virtual-network)
## [Calculadora de preços](https://azure.microsoft.com/pricing/calculator/)
## [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-virtual-network)
## [Fornecedor de recursos de rede](resource-groups-networking.md)
