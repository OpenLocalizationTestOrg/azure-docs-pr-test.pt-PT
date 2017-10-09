## <a name="virtual-network"></a>Rede Virtual
Recursos de redes (VNET) e sub-redes virtuais ajudam a definir um limite de segurança para cargas de trabalho em execução no Azure. Uma VNet é caracterizada por uma coleção de espaços de endereços, definida como blocos CIDR. 

> [!NOTE]
> Os administradores de rede estiver familiarizados com notação CIDR. Se não estiver familiarizado com CIDR, [saber mais acerca do mesmo](http://whatismyipaddress.com/cidr).
> 
> 

![VNet com várias sub-redes](./media/resource-groups-networking/Figure4.png)

As VNets conter Olá seguintes propriedades.

| Propriedade | Descrição | Valores de exemplo |
| --- | --- | --- |
| **addressSpace** |Coleção de prefixos de endereços que compõem Olá VNet em notação CIDR |192.168.0.0/16 |
| **sub-redes** |Coleção de sub-redes que compõem Olá VNet |consulte [sub-redes](#Subnets) abaixo. |
| **ipAddress** |Endereço IP atribuído tooobject. Esta é uma propriedade só de leitura. |104.42.233.77 |

### <a name="subnets"></a>Sub-redes
Uma sub-rede é um recurso de subordinados de uma VNet e ajuda a definir segmentos dos espaços de endereços dentro de um bloco CIDR utilizar prefixos de endereços IP. NICs podem ser adicionados toosubnets e tooVMs ligado, fornecer conectividade de várias cargas de trabalho.

Sub-redes contenham Olá seguintes propriedades. 

| Propriedade | Descrição | Valores de exemplo |
| --- | --- | --- |
| **addressPrefix** |Prefixo de endereço único que compõem a sub-rede de Olá em notação CIDR |192.168.1.0/24 |
| **networkSecurityGroup** |NSG aplicado toohello sub-rede |consulte [NSGs](#Network-Security-Group) |
| **routeTable** |Tabela de rotas aplicadas toohello sub-rede |consulte [UDR](#Route-table) |
| **ipConfigurations** |Coleção de objetos de configruation IP utilizados por NICs toohello ligado sub-rede |consulte [UDR](#Route-table) |

Exemplo VNet no formato JSON:

    {
        "name": "TestVNet",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/virtualNetworks",
        "location": "westus",
        "tags": {
            "displayName": "VNet"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "addressSpace": {
                "addressPrefixes": [
                    "192.168.0.0/16"
                ]
            },
            "subnets": [
                {
                    "name": "FrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "networkSecurityGroup": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "routeTable": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                        },
                        "ipConfigurations": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                            },
                            ...]
                    }
                },
                ...]
        }
    }

### <a name="additional-resources"></a>Recursos adicionais
* Obter mais informações [VNet](../articles/virtual-network/virtual-networks-overview.md).
* Olá leitura [documentação de referência da REST API](https://msdn.microsoft.com/library/azure/mt163650.aspx) para VNets.
* Olá leitura [documentação de referência da REST API](https://msdn.microsoft.com/library/azure/mt163618.aspx) das sub-redes.

