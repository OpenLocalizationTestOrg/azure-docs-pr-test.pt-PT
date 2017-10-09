1. Navegue tooand painel de Olá aberta para o gateway de rede virtual. Existem várias formas toonavigate. No nosso exemplo, vamos navegar toohello gateway 'VNet1GW' acedendo demasiado**TestVNet1 -> Descrição geral -> ligado dispositivos -> VNet1GW**.
2. No painel Olá VNet1GW, clique em **ligações**. Olá parte superior do painel de ligações de Olá, clique em **+ adicionar** tooopen Olá **adicionar ligação** painel.

    ![Criar uma ligação Site a Site](./media/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include/connection1.png)

3. No Olá **adicionar ligação** painel, preencha Olá valores toocreate a ligação.

  - **Nome:** Atribua um nome à sua ligação. Usamos **VNet1toSite2** no nosso exemplo.
  - **Tipo de ligação:** Selecione **Site a site(IPSec)**.
  - **Gateway de rede virtual:** valor Olá é fixo porque está a estabelecer a ligação deste gateway.
  - **Gateway de rede local:** clique **escolher um gateway de rede local** e selecione Olá gateway de rede local que pretende que o toouse. No nosso exemplo, usamos **Site2**.
  - **A chave partilhada:** valor Olá aqui tem de corresponder ao valor de Olá que está a utilizar para o dispositivo VPN local no local. Exemplo de Olá, utilizámos 'abc123', mas pode (e deve) utilizar algo mais complexo. Olá importante é que o valor Olá que especificar aqui tem de ser Olá que mesmo valor que especificou quando configurar o seu dispositivo VPN.
  - Olá restantes valores para **subscrição**, **grupo de recursos**, e **localização** sejam corrigidos.

4. Clique em **OK** toocreate a ligação. Verá *criar ligação* piscar no ecrã de Olá.
5. Pode ver a ligação de Olá no Olá **ligações** painel Olá virtuais do gateway de rede. Olá estado irá passar do *desconhecido* demasiado*ligação*e, em seguida, demasiado*com êxito*.
