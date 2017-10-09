## <a name="scenario"></a>Cenário
toobetter mostram como toocreate NSGs, este documento utilizará cenário Olá abaixo.

![Cenário de VNet](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

Neste cenário, irá criar um NSG para cada sub-rede na Olá **TestVNet** rede virtual, conforme descrito abaixo: 

* **NSG-front-end**. Olá front-end NSG será aplicado toohello *front-end* sub-rede e contêm duas regras:    
  * **regra de RDP**. Esta regra irá permitir RDP tráfego toohello *front-end* sub-rede.
  * **regra de Web**. Esta regra irá permitir HTTP tráfego toohello *front-end* sub-rede.
* **NSG-back-end**. Olá de back-end NSG serão aplicado toohello *back-end* sub-rede e contêm duas regras:    
  * **regra de SQL**. Esta regra permite que o tráfego SQL apenas a partir de Olá *front-end* sub-rede.
  * **regra de Web**. Esta regra negar internet todos os vinculado tráfego de Olá *back-end* sub-rede.

Olá combinação destas regras criar um cenário semelhante a rede de Perímetro, onde sub-rede de back-end de Olá só pode receber o tráfego de entrada para o SQL Server da sub-rede do front-end de Olá e tem toohello sem acesso à Internet, enquanto a sub-rede do front-end Olá pode comunicar com Olá Internet, e receba apenas os pedidos HTTP recebidos.

