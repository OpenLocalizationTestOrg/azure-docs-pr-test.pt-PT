Olá sistema de nomes de domínio (DNS) é utilizado toolocate coisas Olá internet. Por exemplo, quando introduzir um endereço no seu browser ou clicar numa ligação numa página web, utiliza domínio de Olá tootranslate DNS para um endereço IP. endereço IP Olá é ordenação dos como uma morada, mas não é compatível muito humano. Por exemplo, é muito mais fácil tooremember um nome DNS como **contoso.com** que é tooremember um endereço IP, tais como 192.168.1.88 ou 2001:0:4137:1f67:24a2:3888:9cce:fea3.

Olá sistema DNS baseia-se no *registos*. Regista associar específico *nome*, tais como **contoso.com**, com um endereço IP ou outro nome DNS. Quando uma aplicação, tal como um web browser, o aspeto que tem um nome de DNS, localiza o registo de Olá e utiliza independentemente pontos tooas Olá endereço. Se Olá valor-toois de pontos de um endereço IP, o browser Olá irá utilizar esse valor. Se aponta tooanother nome DNS, a aplicação Olá tem resolução toodo novamente. Em última análise, resolução de nomes de todos os vai terminar dentro de um endereço IP.

Quando cria um Web site do Azure, um nome DNS é automaticamente toohello site atribuído. Este nome assume a forma de Olá de  **&lt;yoursitename&gt;. azurewebsites.net**. Quando adicionar o seu Web site como um ponto de final do Gestor de tráfego do Azure, o seu Web site, em seguida, é acessível através de Olá  **&lt;yourtrafficmanagerprofile&gt;. trafficmanager.net** domínio.

> [!NOTE]
> Quando o seu Web site está configurado como um ponto final do Gestor de tráfego, que irá utilizar Olá **. trafficmanager.net** endereço quando criar registos DNS.
> 
> Só pode utilizar registos CNAME com o Gestor de tráfego
> 
> 

Também existem vários tipos de registos, cada um com as suas próprias funções e limitações, mas para Web sites configurados tooas pontos finais do Gestor de tráfego, iremos apenas mais importantes para si sobre um; *CNAME* registos.

### <a name="cname-or-alias-record"></a>Registo CNAME ou Alias
Um registo CNAME mapeia um *específico* de nomes DNS, tal como **mail.contoso.com** ou **www.contoso.com**, tooanother nome de domínio (canónico). No caso de Olá de Web sites do Azure utilizando o Gestor de tráfego, o nome de domínio canónica de Olá é Olá  **&lt;myapp >. trafficmanager.net** nome de domínio do perfil do Traffic Manager. Depois de criado, Olá CNAME cria um alias para Olá  **&lt;myapp >. trafficmanager.net** nome de domínio. Olá entrada CNAME irá resolver o endereço IP toohello do seu  **&lt;myapp >. trafficmanager.net** nome de domínio automaticamente, se alterar o endereço IP de Olá do Web site de Olá, não terá tootake qualquer ação.

Assim que o tráfego chega ao Gestor de tráfego, em seguida, encaminha Olá tráfego tooyour Web site, Olá método balanceamento de carga que está configurado para a utilizar. Este é o Web site de tooyour toovisitors completamente transparente. Verão apenas o nome de domínio personalizado de Olá no browser.

> [!NOTE]
> Alguns registrars de domínio apenas lhe permitam toomap subdomínios quando utilizar um registo CNAME, tais como **www.contoso.com**e não raiz nomes, tal como **contoso.com**. Para obter mais informações sobre registos CNAME, consulte a documentação de Olá fornecida pela sua entidade de registo, <a href="http://en.wikipedia.org/wiki/CNAME_record">Olá Wikipedia entrada no registo CNAME</a>, ou Olá <a href="http://tools.ietf.org/html/rfc1035">IETF os nomes de domínio - implementação e a especificação de</a> documento.
> 
> 

