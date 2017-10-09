## <a name="scenario"></a>Cenário
toobetter mostram como toocreate UDRs, este documento utilizará cenário Olá abaixo.

![DESCRIÇÃO DA IMAGEM](./media/virtual-network-create-udr-scenario-include/figure1.png)

Neste cenário, irá criar um UDR para Olá *sub-rede de fim da frente* e outro UDR para Olá *da sub-rede Back end* , conforme descrito abaixo: 

* **UDR-front-end**. Olá front-end UDR será aplicado toohello *front-end* sub-rede e contêm uma rota:    
  * **RouteToBackend**. Esta rota irá enviar todos os toohello de sub-rede de back-end do tráfego toohello **FW1** máquina virtual.
* **UDR-back-end**. Olá de back-end UDR serão aplicado toohello *back-end* sub-rede e contêm uma rota:    
  * **RouteToFrontend**. Esta rota irá enviar todos os toohello de sub-rede do front-end toohello tráfego **FW1** máquina virtual.

combinação de Olá destas rotas irá garantir que todo o tráfego destinado a partir de uma sub-rede tooanother será encaminhado toohello **FW1** máquina virtual, que está a ser utilizada como uma aplicação virtual. Também precisa de tooturn no reencaminhamento IP para essa VM, tooensure pode receber o tráfego destinado tooother VMs.

