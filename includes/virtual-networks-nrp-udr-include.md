## <a name="route-tables"></a>Tabelas de rotas
Recursos de tabela de rota contém toodefine rotas utilizadas como o tráfego flui dentro da sua infraestrutura do Azure. Pode utilizar definidas pelo utilizador (UDR) de rotas toosend todo o tráfego de uma determinada sub-rede tooa aplicação virtual, tais como um sistema de deteção intrusões ou uma firewall (IDS). Pode associar um toosubnets da tabela de rota. 

As tabelas de rotas contenham Olá seguintes propriedades.

| Propriedade | Descrição | Valores de exemplo |
| --- | --- | --- |
| **rotas** |Coleção de utilizador rotas definidas na tabela de rota Olá |consulte [rotas definidas pelo utilizador](#User-defined-routes) |
| **sub-redes** |Coleção de tabela de rotas de Olá sub-redes é demasiado aplicada|consulte [sub-redes](#Subnets) |

### <a name="user-defined-routes"></a>Rotas definidas pelo utilizador
Pode criar toospecify UDRs onde o tráfego deve ser enviado, com base no respetivo endereço de destino. Pode considerar uma rota como definição de gateway predefinido do Olá com base no endereço de destino Olá de um pacote de rede.

UDRs contenham Olá seguintes propriedades. 

| Propriedade | Descrição | Valores de exemplo |
| --- | --- | --- |
| **addressPrefix** |Prefixo do endereço ou o endereço IP completo para o destino de Olá |192.168.1.0/24, 192.168.1.101 |
| **nextHopType** |Tipo de dispositivo Olá tráfego será enviado|Internet VirtualAppliance, Gateway de VPN |
| **nextHopIpAddress** |Endereço IP do próximo salto de Olá |192.168.1.4 |

Tabela de rota de exemplo no formato JSON:

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a>Recursos adicionais
* Obter mais informações [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).
* Olá leitura [documentação de referência da REST API](https://msdn.microsoft.com/library/azure/mt502549.aspx) para tabelas de rota.
* Olá leitura [documentação de referência da REST API](https://msdn.microsoft.com/library/azure/mt502539.aspx) do utilizador definida rotas (UDRs).

