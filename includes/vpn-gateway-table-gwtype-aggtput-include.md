O Azure oferece Olá seguir SKUs do VPN gateway:

|**SKU**   | **S2S/VNet para VNet<br>Túneis** | **P2S<br>Ligações** | **Referência de<br>Débito de Agregação** |
|---       | ---                             | ---                    | ---                         |
|**VpnGw1**| Um máximo de 30                         | Um máximo de 128               | 650 Mbps                    |
|**VpnGw2**| Um máximo de 30                         | Um máximo de 128               | 1 Gbps                      |
|**VpnGw3**| Um máximo de 30                         | Um máximo de 128               | 1,25 Gbps                   |
|**Básica** | Um máximo de 10                         | Um máximo de 128               | 100 Mbps                    | 
|          |                                 |                        |                             | 

- A Referência de Débito de Agregação baseia-se em medidas de vários túneis agregados através de um único gateway. Não se trata de um débito garantido devido tooInternet condições de tráfego e os comportamentos de aplicação.

- Obter informações sobre preços, podem ser encontrado no Olá [preços](https://azure.microsoft.com/pricing/details/vpn-gateway) página.

- Pode encontrar informações de SLA (contrato de nível de serviço) no Olá [SLA](https://azure.microsoft.com/support/legal/sla/vpn-gateway/) página.
