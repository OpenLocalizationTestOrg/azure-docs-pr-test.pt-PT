1. Olá à esquerda do lado da página de portal Olá, clique em  **+**  e escreva "Gateway de rede Virtual" na pesquisa. Em **Resultados**, localize e clique em **Gateway de rede Virtual**.
2. Na Olá parte inferior do painel de "Gateway de rede Virtual" Olá, clique em **criar**. Esta ação abre Olá **criar gateway de rede virtual** painel.

    ![Campos do painel Criar gateway de rede virtual](./media/vpn-gateway-add-gw-s2s-rm-portal-include/vnet_gw.png "Novo gateway")

3. No Olá **criar gateway de rede virtual** painel, especificar valores de Olá para o gateway de rede virtual.

  - **Nome**: dê um nome ao gateway. Isto é não Olá, mesmo que atribuir nome a uma sub-rede de gateway. -'S nome Olá do objeto do gateway Olá que estiver a criar.
  - **Tipo de gateway**: selecione **VPN**. Gateways de VPN utilizam o tipo de gateway de rede virtual Olá **VPN**. 
  - **Tipo de VPN**: selecionar tipo de VPN de Olá especificado para a sua configuração. A maioria das configurações requerem um tipo de VPN baseado em rotas.
  - **SKU**: SKU de gateway Olá selecione na lista pendente de Olá. SKUs de Olá listados na lista pendente de Olá dependem Olá tipo de VPN que selecionar. Para obter mais informações sobre os SKUs de gateway, veja [SKUs de Gateway](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).
  - **Localização**: poderá ter tooscroll toosee localização. Ajustar Olá **localização** campo toopoint toohello localização onde está localizada a sua rede virtual. Se a localização de Olá não está a apontar região toohello onde reside a sua rede virtual, rede virtual Olá não aparecerá no passo seguinte Olá 'Escolher uma rede virtual' pendente.
  - **Rede virtual**: escolha Olá toowhich de rede virtual pretende tooadd este gateway. Clique em **rede Virtual** 'Escolher uma rede virtual' Painel do Olá tooopen. Selecione Olá VNet. Se não vir a VNet, certifique-se de que o campo de localização de Olá está a apontar toohello região na qual está localizada a sua rede virtual.
  - **Endereço IP público**: painel de 'Criar endereço IP público' Olá cria um objeto de endereço IP público. endereço IP público Olá dinamicamente é atribuído ao gateway de VPN Olá criado. O Gateway de VPN, atualmente, apenas suporta a alocação de endereços IP públicos *dinâmicos*. No entanto, isto não significa que o endereço IP Olá alterado depois de lhe ser atribuído tooyour gateway de VPN. tempo apenas Olá alterações do endereço de IP público de Olá quando é Olá gateway é eliminado e recriado. Não é alterado ao redimensionar, repor ou ao realizar qualquer outra manutenção/atualização interna do gateway de VPN.

    - Em primeiro lugar, clique em **endereço IP público** tooopen Olá painel 'Escolher endereço IP público', em seguida, clique em **+ criar novos** 'Criar endereço IP público' Painel do Olá tooopen.
    - Em seguida, introduza um **nome** do endereço IP público, em seguida, clique em **OK** em Olá parte inferior da toosave painel as suas alterações.

      ![Criar IP público](./media/vpn-gateway-add-gw-s2s-rm-portal-include/pip.png "Criar PIP")

4. Verifique as definições de Olá. Pode selecionar **Pin toodashboard** em Olá parte inferior do painel de Olá se pretender que o seu tooappear de gateway no dashboard de Olá. 
5. Clique em **criar** toobegin criar gateway VPN Olá. Olá definições serão validadas e verá Olá "Gateway de rede Virtual da implementação" mosaico no dashboard de Olá. Criar um gateway pode demorar até too45 minutos. Poderá ser necessário toorefresh o estado de Olá concluída toosee página do portal.

Depois de criado o gateway de Olá, ver o endereço IP Olá que tenha sido atribuído tooit observando a rede virtual do Olá no portal de Olá. gateway de Olá aparece como um dispositivo ligado. Pode clicar em Olá ligado dispositivo (gateway da rede virtual) tooview obter mais informações.
