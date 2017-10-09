## <a name="nic"></a>NIC
Um recurso de cartão (NIC) de interface de rede fornece uma sub-rede existente do tooan de conectividade de rede num recurso VNet. Embora possa criar uma NIC como um objeto de autónomo, tem de tooassociate-tooanother objeto tooactually fornecer conectividade. Uma NIC pode ser utilizado tooconnect uma sub-rede de tooa VM, um endereço IP público ou um balanceador de carga.  

| Propriedade | Descrição | Valores de exemplo |
| --- | --- | --- |
| **máquina virtual** |Olá VM NIC está associado. |/subscriptions/{GUID}/../microsoft.Compute/virtualMachines/vm1 |
| **macAddress** |Endereço MAC para Olá NIC |qualquer valor entre 4 e 30 |
| **networkSecurityGroup** |NSG associado toohello NIC |/subscriptions/{GUID}/../microsoft.Network/networkSecurityGroups/myNSG1 |
| **dnsSettings** |Definições de DNS para Olá NIC |consulte [PIP](#Public-IP-address) |

Uma placa de Interface de rede ou NIC, representa uma interface de rede que pode ser associado tooa máquina de virtual (VM). Uma VM pode ter um ou vários NICs.

![NIC numa única VM](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a>Configurações de IP
Os NICs que têm um objeto subordinado com o nome **ipConfigurations** contendo Olá seguintes propriedades:

| Propriedade | Descrição | Valores de exemplo |
| --- | --- | --- |
| **sub-rede** |Olá sub-rede NIC é onnected para. |/subscriptions/{GUID}/../microsoft.Network/virtualNetworks/myvnet1/Subnets/mysub1 |
| **privateIPAddress** |Endereço IP para Olá NIC na sub-rede Olá |10.0.0.8 |
| **privateIPAllocationMethod** |Método de alocação de IP |Dinâmicas ou estáticas |
| **enableIPForwarding** |Se Olá NIC pode ser utilizado para o encaminhamento |VERDADEIRO ou FALSO |
| **primário** |Se está Olá NIC Olá NIC primário para Olá VM |VERDADEIRO ou FALSO |
| **publicIPAddress** |PIP associado Olá NIC |consulte [as definições de DNS](#DNS-settings) |
| **loadBalancerBackendAddressPools** |Fazer uma cópia Olá de conjuntos de endereços de fim que NIC está associado | |
| **loadBalancerInboundNatRules** |Entrada NIC está associado a dos Olá de regras NAT para Balanceador de carga | |

Exemplo público endereço IP no formato JSON:

    {
        "name": "lb-nic1-be",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkInterfaces",
        "location": "eastus",
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "ipConfigurations": [
                {
                    "name": "NIC-config",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/NIC-config",
                    "etag": "W/\"0027f1a2-3ac8-49de-b5d5-fd46550500b1\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "privateIPAddress": "10.0.0.4",
                        "privateIPAllocationMethod": "Dynamic",
                        "subnet": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet"
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1"
                            }
                        ]
                    }
                }
            ],
            "dnsSettings": { ... },
            "macAddress": "00-0D-3A-10-F1-29",
            "enableIPForwarding": false,
            "primary": true,
            "virtualMachine": {
                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Compute/virtualMachines/web1"
            }
        }
    }

### <a name="additional-resources"></a>Recursos adicionais
* Olá leitura [documentação de referência da REST API](https://msdn.microsoft.com/library/azure/mt163579.aspx) para NICs.

