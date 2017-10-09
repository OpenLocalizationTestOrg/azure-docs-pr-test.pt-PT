## <a name="traffic-manager-profile"></a>Perfil do Traffic Manager
Gestor de tráfego e o recurso de ponto final de subordinados permitem tooendpoints de encaminhamento de DNS no Azure e fora do Azure. Essa distribuição de tráfego é regida pelos métodos de encaminhamento de política. Gestor de tráfego permite também toobe de estado de funcionamento do ponto final monitorizada e de tráfego diverted adequadamente com base no estado de funcionamento de Olá de um ponto final. 

| Propriedade | Descrição |
| --- | --- |
| **trafficRoutingMethod** |os valores possíveis são *desempenho*, *Weighted*, e *prioridade* |
| **dnsConfig** |FQDN para o perfil de Olá |
| **Protocolo** |protocolo de monitorização, os valores possíveis são *HTTP* e *HTTPS* |
| **Porta** |monitorização de porta |
| **Caminho** |caminho de monitorização |
| **Pontos finais** |contentor de recursos de ponto final |

### <a name="endpoint"></a>Ponto Final
Um ponto final é um recurso de subordinados de um perfil do Traffic Manager. Representa um serviço ou web endpoint toowhich utilizador o tráfego é distribuído com base na política de Olá configurado no Olá recursos de perfil do Traffic Manager. 

| Propriedade | Descrição |
| --- | --- |
| **Tipo** |Olá, tipo de ponto final de Olá, os valores possíveis são *ponto final do Azure*, *ponto final externo*, e *aninhada ponto final* |
| **targetResourceId** |endereço IP público de um ponto final de serviço ou web. Isto pode ser um ponto final do Azure ou externo. |
| **Peso** |peso de ponto final utilizado na gestão de tráfego. |
| **Prioridade** |prioridade de ponto final de Olá, toodefine utilizado uma ação de ativação pós-falha |

Exemplo de Gestor de tráfego no formato Json: 

        {
            "apiVersion": "[variables('tmApiVersion')]",
            "type": "Microsoft.Network/trafficManagerProfiles",
            "name": "VMEndpointExample",
            "location": "global",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '0')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '1')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '2')]",
            ],
            "properties": {
                "profileStatus": "Enabled",
                "trafficRoutingMethod": "Weighted",
                "dnsConfig": {
                    "relativeName": "[parameters('dnsname')]",
                    "ttl": 30
                },
                "monitorConfig": {
                    "protocol": "http",
                    "port": 80,
                    "path": "/"
                },
                "endpoints": [
                    {
                        "name": "endpoint0",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 0))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint1",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 1))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint2",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 2))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    }
                ]
            }
        }


## <a name="additional-resources"></a>Recursos adicionais
Leitura [documentação da REST API para o Gestor de tráfego](https://msdn.microsoft.com/library/azure/mt163664.aspx) para obter mais informações.

