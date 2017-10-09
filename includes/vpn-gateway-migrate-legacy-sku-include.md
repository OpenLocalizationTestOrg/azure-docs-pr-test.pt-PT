> [!NOTE]
> * gateway de VPN Olá endereço IP público será alterado quando migrar a partir de um tooa SKU antigo SKU de novo.
> * Não é possível migrar clássico toohello de gateways VPN SKUs de novo. Clássico VPN gateways pode apenas utilizar Olá legados SKUs (antigos).
> 

Não é possível redimensionar a VPN do Azure gateways entre Olá SKUs antigos e Olá novas famílias SKU. Se tiver de gateways de VPN no modelo de implementação do Resource Manager Olá que utilizam a versão mais antiga do Olá do Olá SKUs, pode migrar toohello SKUs de novo. toomigrate, elimine o gateway VPN existente Olá na sua rede virtual, em seguida, crie um novo.

Fluxo de trabalho de migração:

1. Remova qualquer gateway de rede virtual toohello ligações.
2. Elimine gateway de VPN Olá antigo.
3. Crie o novo gateway de VPN Olá.
4. Atualize os dispositivos VPN no local com Olá novo VPN gateway endereço IP (para as ligações Site a Site).
5. Atualize o valor do endereço IP de gateway do Olá para quaisquer gateways de rede local de VNet a VNet que irão ligar toothis gateway.
6. Transferir novos pacotes de configuração de VPN de cliente para clientes de P2S ligar a rede virtual toohello através deste gateway VPN.
7. Recrie o gateway de rede virtual do Olá ligações toohello.
