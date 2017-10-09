1. No portal de Olá, de **todos os recursos**, clique em **+ adicionar**. 
2. No Olá **tudo** caixa de pesquisa do painel, escreva **gateway de rede Local**, em seguida, clique em toosearch. Isto irá devolver uma lista. Clique em **gateway de rede Local** tooopen Olá painel, em seguida, clique em **criar** tooopen Olá **criar gateway de rede local** painel.

  ![criar gateway de rede local](./media/vpn-gateway-add-lng-s2s-rm-portal-include/createlng.png)

3. No Olá **painel de gateway de rede local criar**, especificar valores de Olá para gateway de rede local.

  - **Nome:** Especifique um nome para seu objeto de gateway de rede local.
  - **Endereço IP:** este é o endereço IP público Olá do dispositivo VPN de Olá que pretende que o Azure tooconnect para. Especifique um endereço IP público válido. endereço IP Olá não pode ser protegido por NAT e tem toobe acessível pelo Azure. Se não tiver o endereço IP Olá neste momento, pode utilizar valores de Olá mostrados na captura de ecrã de Olá, mas vai precisar toogo novamente e substitua o seu endereço IP do marcador de posição pelo endereço IP público Olá do seu dispositivo VPN. Caso contrário, Azure não será capaz de tooconnect.
  - **Espaço de endereços** refere-se toohello intervalos de endereços de rede de Olá que representa esta rede local. Pode adicionar vários intervalos de espaço de endereços. Certifique-se de que intervalos Olá que especificar aqui não se sobrepõem intervalos outras redes que pretende que sejam tooconnect para. Azure encaminhará o intervalo de endereços de Olá que especifique o endereço IP do dispositivo VPN do toohello no local. *Utilizar os seus próprios valores aqui, não Olá valores mostrados na captura de ecrã Olá*.
  - **Subscrição:** Certifique-se de que Olá correto a subscrição está a ser mostrada.
  - **Grupo de recursos:** grupo de recursos de Olá Selecione se pretende toouse. Pode criar um novo grupo de recursos ou selecionar um que já tenha criado.
  - **Localização:** selecionar localização Olá que este objeto será criado. Poderá ser útil tooselect Olá mesma localização que a VNet reside num, mas não é necessária toodo, por isso.

4. Quando tiver terminado de especificar valores de Olá, clique em **criar** na parte inferior de Olá Olá painel toocreate Olá local do gateway de rede.
