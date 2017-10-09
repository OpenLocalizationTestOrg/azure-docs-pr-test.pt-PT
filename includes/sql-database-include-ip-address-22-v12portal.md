
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com/) em http://portal.azure.com/.
2. Na faixa de Olá esquerdo, clique em **Procurar tudo**. Olá **procurar** é apresentado o painel.
3. Desloque-se e clique em **servidores SQL**. Olá **servidores SQL** é apresentado o painel.
   
    ![Localizar o servidor da SQL Database do Azure no portal de Olá][b21-FindServerInPortal]
4. Para sua comodidade, clique em Olá minimizar o controlo da Olá anteriormente **procurar** painel.
5. Na caixa de texto de filtro de Olá, comece a escrever o nome de hello do servidor. A linha é apresentada.
6. Clique em linha hello do servidor. É apresentado um painel para o servidor.
7. No painel do servidor, clique em **definições**. Olá **definições** é apresentado o painel.
8. Clique em **Firewall**. Olá **as definições da Firewall** é apresentado o painel.
   
    ![Clique em Definições > Firewall][b31-SettingsFirewallNavig]
9. Clique em **Adicionar cliente IP**. Escreva um nome para a nova regra na caixa de texto Olá primeiro.
10. Tipo de Olá baixa e alta os valores de intervalo de Olá pretende de endereços IP tooenable.
    
    * Pode ser útil toohave terminar de valor baixo Olá com **.0** e Olá elevada com **.255**.
    
    ![Adicionar um tooallow de intervalo de endereços IP][b41-AddRange]
11. Clique em **Guardar**.

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
