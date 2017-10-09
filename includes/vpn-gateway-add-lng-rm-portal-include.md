1. No portal de Olá, de **todos os recursos**, clique em **+ adicionar**. No Olá **tudo** caixa de pesquisa do painel, escreva **gateway de rede Local**, em seguida, clique em tooreturn uma lista de recursos. Clique em **gateway de rede Local** tooopen Olá painel, em seguida, clique em **criar** tooopen Olá **criar gateway de rede local** painel.
   
    ![criar gateway de rede local](./media/vpn-gateway-add-lng-rm-portal-include/lng.png)

2. No Olá **painel de gateway de rede local criar**, especifique um **nome** para o objeto do gateway de rede local. Se possível, utilize algo intuitiva, tal como **ClassicVNetLocal** ou **TestVNet1Local**. Isto torna mais fácil para tooidentify Olá gateway de rede local no portal de Olá.
3. Especifique um público válido **endereço IP** para o dispositivo VPN de Olá ou toowhich de gateway de rede virtual pretende tooconnect.<br>**Se esta rede local representa uma localização no local:** especifique Olá endereço de IP público do dispositivo VPN de Olá que pretende que sejam tooconnect para. Este não pode ser protegido por NAT e tem toobe acessível pelo Azure.<br>**Se esta rede local representa a outra VNet:** especifique o endereço IP público Olá que foi atribuído ao gateway de rede virtual toohello essa VNet.<br>**Se ainda não tiver o endereço IP Olá:** pode constituem um endereço IP do marcador de posição válido e, em seguida, voltar atrás e modificar esta definição antes de ligar.
4. **Espaço de endereços** refere-se toohello intervalos de endereços de rede de Olá que representa esta rede local. Pode adicionar vários intervalos de espaço de endereços. Certifique-se de que intervalos Olá que especificar aqui não se sobrepõem intervalos toowhich outras redes que ligar.
5. Para **subscrição**, certifique-se de que Olá correto a subscrição está a ser mostrada.
6. Para **grupo de recursos**, selecione os grupo de recursos de Olá que pretende que o toouse. Pode criar um novo grupo de recursos ou selecionar um que já tenha criado.
7. Para **localização**, selecione a localização Olá em que este recurso será criado. Poderá ser útil tooselect Olá mesma localização que a VNet reside num, mas não é necessária toodo, por isso.
8. Clique em **criar** gateway de rede local toocreate Olá.

