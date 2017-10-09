## <a name="scenario"></a>Cenário
Uma VM com um único NIC é a rede virtual tooa criados e ligados. Olá VM requer três diferentes *privada* IP endereços e dois *pública* endereços IP. endereços IP Olá são atribuídos toohello seguintes configurações de IP:

* **IPConfig-1:** atribui um *estático* endereço IP privado e um *estático* endereço IP público.
* **IPConfig-2:** atribui um *estático* endereço IP privado e um *estático* endereço IP público.
* **IPConfig-3:** atribui um *estático* endereço IP privado e nenhum endereço IP público.
  
    ![Vários endereços IP](./media/virtual-network-multiple-ip-addresses-scenario/multiple-ipconfigs.png)

configurações de IP Olá estão associado toohello NIC quando Olá NIC é criado e Olá NIC anexado toohello VM quando Olá VM é criada. tipos de Olá de endereços IP utilizados para o cenário de Olá são para fins de ilustração. Pode atribuir qualquer tipos de endereço e a atribuição de IP precisa.

> [!NOTE]
> Apesar de os passos Olá neste artigo atribui todas as tooa de configurações de IP único NIC, também pode atribuir várias tooany de configurações de IP NIC na VM de vários NICs. toolearn como toocreate uma VM com vários NICs, lidos Olá [criar uma VM com vários NICs](../articles/virtual-network/virtual-network-deploy-multinic-arm-ps.md) artigo.
