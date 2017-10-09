## <a name="sample-scenario"></a>Cenário de exemplo
toobetter mostram como toomanage NSGs, este artigo utiliza o cenário de Olá abaixo.

![Cenário de VNet](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

Neste cenário, irá criar um NSG para cada sub-rede na Olá **TestVNet** rede virtual, conforme descrito abaixo: 

* **NSG-front-end**. Olá front-end NSG será aplicado toohello *front-end* sub-rede e contêm duas regras:    
  * **regra de RDP**. Esta regra irá permitir RDP tráfego toohello *front-end* sub-rede.
  * **regra de Web**. Esta regra irá permitir HTTP tráfego toohello *front-end* sub-rede.
* **NSG-back-end**. Olá de back-end NSG serão aplicado toohello *back-end* sub-rede e contêm duas regras:    
  * **regra de SQL**. Esta regra permite que o tráfego SQL apenas a partir de Olá *front-end* sub-rede.
  * **regra de Web**. Esta regra negar internet todos os vinculado tráfego de Olá *back-end* sub-rede.

combinação de Olá destas regras criar um cenário semelhante a rede de Perímetro, onde Olá back-end só podem receber o tráfego de entrada para o tráfego SQL da sub-rede do front-end de Olá e tem toohello sem acesso à Internet, enquanto a sub-rede do front-end Olá pode comunicar com Olá Internet e receber apenas os pedidos HTTP recebidos.

cenário de Olá toodeploy descrito acima, siga [esta ligação](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), clique em **implementar tooAzure**, substitua os valores de parâmetros de predefinição Olá se necessário e siga as instruções de Olá no portal de Olá. Instruções de exemplo de Olá abaixo, o modelo de Olá foi utilizado toodeploy um recurso, os nomes dos grupos **RG NSG**. 

