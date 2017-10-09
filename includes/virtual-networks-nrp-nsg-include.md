## <a name="network-security-group"></a>Grupo de segurança de rede
Um recurso NSG permite a criação de Olá de limite de segurança para cargas de trabalho, através da implementação de permissão e negação regras. Estas regras podem ser aplicadas tooa VM, um NIC ou uma sub-rede.

| Propriedade | Descrição | Valores de exemplo |
| --- | --- | --- |
| **sub-redes** |Lista de ids de sub-rede Olá NSG é aplicada a. |/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/Providers/Microsoft.Network/virtualNetworks/TestVNet/Subnets/FrontEnd |
| **securityRules** |Lista de regras de segurança que compõem Olá NSG |Consulte [regra de segurança](#Security-rule) abaixo |
| **defaultSecurityRules** |Lista de regras de segurança predefinidas presentes em cada NSG |Consulte [predefinido regras de segurança](#Default-security-rules) abaixo |

* **Regra de segurança** -um NSG pode ter várias regras de segurança definidas. Cada regra pode permitir ou negar os diferentes tipos de tráfego.

### <a name="security-rule"></a>Regra de segurança
Uma regra de segurança é um recurso de subordinados de um NSG que contém as propriedades de Olá abaixo.

| Propriedade | Descrição | Valores de exemplo |
| --- | --- | --- |
| **Descrição** |Descrição da regra de Olá |Permitir o tráfego de entrada para todas as VMs numa sub-rede X |
| **protocolo** |Protocolo toomatch para a regra de Olá |TCP, UDP ou * |
| **sourcePortRange** |Toomatch de intervalo de portas de origem para a regra de Olá |80, 100-200, * |
| **destinationPortRange** |Toomatch de intervalo de portas de destino para a regra de Olá |80, 100-200, * |
| **sourceAddressPrefix** |Toomatch de prefixo de endereço de origem para a regra de Olá |10.10.10.1, 10.10.10.0/24, VirtualNetwork |
| **destinationAddressPrefix** |Toomatch de prefixo de endereço de destino para a regra de Olá |10.10.10.1, 10.10.10.0/24, VirtualNetwork |
| **direção** |Direção do tráfego toomatch para a regra de Olá |De entrada ou de saída |
| **prioridade** |Prioridade da regra de Olá. As regras são verificados por ordem de prioridade, depois de uma regra se aplica, são testadas não mais regras para correspondência. |10, 100, 65000 |
| **acesso** |Tipo de acesso tooapply se Olá regra corresponder |Permitir ou negar |

Exemplo NSG no formato JSON:

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a>Regras de segurança predefinidas

Regras de segurança predefinidas têm Olá mesmas propriedades disponíveis nas regras de segurança. Elas existem tooprovide conectividade básica entre os recursos que tenham toothem NSGs aplicados. Certifique-se de que sabe que [predefinido regras de segurança](../articles/virtual-network/virtual-networks-nsg.md#default-rules) existe.

### <a name="additional-resources"></a>Recursos adicionais
* Obter mais informações [NSGs](../articles/virtual-network/virtual-networks-nsg.md).
* Olá leitura [documentação de referência da REST API](https://msdn.microsoft.com/library/azure/mt163615.aspx) para NSGs.
* Olá leitura [documentação de referência da REST API](https://msdn.microsoft.com/library/azure/mt163580.aspx) para regras de segurança.
