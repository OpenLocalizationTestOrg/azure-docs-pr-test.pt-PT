## <a name="scenario"></a>Cenário
toobetter ilustrar como toocreate uma VNet e sub-redes, este documento irá utilizar o cenário de Olá abaixo.

![Cenário de VNet](./media/virtual-networks-create-vnet-scenario-include/vnet-scenario.png)

Neste cenário, vai criar uma VNet com o nome **TestVNet** com um bloco CIDR reservado de **192.168.0.0./16**. A VNet irá conter Olá seguintes sub-redes: 

* **Front-end**, utilizando **192.168.1.0/24** como bloco CIDR.
* **Back-end**, utilizando **192.168.2.0/24** como bloco CIDR.

