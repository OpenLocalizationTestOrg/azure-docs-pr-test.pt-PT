Olá sistema de nomes de domínio (DNS) é utilizado toolocate recursos Olá internet. Por exemplo, quando introduzir um endereço de aplicação web no browser ou clicar numa ligação numa página web, utiliza domínio de Olá tootranslate DNS para um endereço IP. endereço IP Olá é ordenação dos como uma morada, mas não é compatível muito humano. Por exemplo, é muito mais fácil tooremember um nome DNS como **contoso.com** que é tooremember um endereço IP, tais como 192.168.1.88 ou 2001:0:4137:1f67:24a2:3888:9cce:fea3.

Olá sistema DNS baseia-se no *registos*. Regista associar específico *nome*, tais como **contoso.com**, com um endereço IP ou outro nome DNS. Quando uma aplicação, tal como um web browser, o aspeto que tem um nome de DNS, localiza o registo de Olá e utiliza independentemente pontos tooas Olá endereço. Se Olá valor-toois de pontos de um endereço IP, o browser Olá irá utilizar esse valor. Se aponta tooanother nome DNS, a aplicação Olá tem resolução toodo novamente. Em última análise, resolução de nomes de todos os vai terminar dentro de um endereço IP.

Quando criar uma aplicação web no App Service, um nome DNS é atribuído automaticamente toohello web app. Este nome assume a forma de Olá de  **&lt;yourwebappname&gt;. azurewebsites.net**. Há também um endereço IP virtual disponíveis para utilização quando criar DNS regista, pelo que pode criar registos toohello esse ponto **. azurewebsites.net**, ou pode apontar toohello endereço IP.

> [!NOTE]
> endereço IP de Olá da sua aplicação web será alterado se eliminar e recriar a sua aplicação web ou alterar o modo de plano de serviço de aplicações de Olá demasiado**livres** depois de ter sido definido demasiado**básico**, **partilhados**, ou **padrão**.
> 
> 

Também existem vários tipos de registos, cada um com as suas próprias funções e limitações, mas para aplicações web é apenas mais importantes para si sobre dois *A* e *CNAME* registos.

### <a name="address-record-a-record"></a>Registo de endereço (um registo)
Um registo mapeia um domínio, tal como **contoso.com** ou **www.contoso.com**, *ou de um domínio de caráter universal* como  **\*. contoso.com**, tooan endereço IP. No caso de Olá de uma aplicação web no App Service, quer Olá IP virtual do serviço de Olá ou um endereço IP específico que comprou para a sua aplicação web.

benefícios principais do Olá de um registo através de um registo CNAME são:

* Pode mapear um domínio de raiz, tais como **contoso.com** endereço IP tooan; registrars muitos permitem apenas esta registos utilizando
* Pode ter uma entrada que utiliza um caráter universal, tais como  **\*. contoso.com**, que seria processar pedidos de subdomínios vários como **mail.contoso.com**,  **blogs.contoso.com**, ou **www.contso.com**.

> [!NOTE]
> Uma vez que está mapeado um registo tooa o endereço IP estático, não é possível resolver o endereço IP de toohello de alterações da sua aplicação web automaticamente. Um endereço IP para utilização com registos é fornecido quando configurar as definições de nome de domínio personalizado da sua aplicação web; No entanto, este valor pode alterar se eliminar e recriar a sua aplicação web ou alterar Olá tooback de modo de plano do App Service demasiado**livres**.
> 
> 

### <a name="alias-record-cname-record"></a>Registo de alias (registo CNAME)
Um registo CNAME mapeia um *específico* de nomes DNS, tal como **mail.contoso.com** ou **www.contoso.com**, tooanother nome de domínio (canónico). No caso de Olá de Web Apps do App Service, o nome de domínio canónica de Olá é Olá  **&lt;yourwebappname >. azurewebsites.net** nome de domínio da sua aplicação web. Depois de criado, Olá CNAME cria um alias para Olá  **&lt;yourwebappname >. azurewebsites.net** nome de domínio. Olá entrada CNAME irá resolver o endereço IP toohello do seu  **&lt;yourwebappname >. azurewebsites.net** nome de domínio automaticamente, se alterar o endereço IP Olá da aplicação web de Olá, não terá tootake qualquer ação.

> [!NOTE]
> Alguns registrars de domínio apenas lhe permitam toomap subdomínios quando utilizar um registo CNAME, tais como **www.contoso.com**e não raiz nomes, tal como **contoso.com**. Para obter mais informações sobre registos CNAME, consulte a documentação de Olá fornecida pela sua entidade de registo, <a href="http://en.wikipedia.org/wiki/CNAME_record">Olá Wikipedia entrada no registo CNAME</a>, ou Olá <a href="http://tools.ietf.org/html/rfc1035">IETF os nomes de domínio - implementação e a especificação de</a> documento.
> 
> 

### <a name="web-app-dns-specifics"></a>Informações específicas DNS de aplicação Web
A utilização de um registo com as Web Apps requer toofirst criar um dos seguintes registos TXT de Olá:

* **Para o domínio de raiz de Olá** -registo TXT de DNS A  **@**  demasiado  **&lt;yourwebappname&gt;. azurewebsites.net**.
* **Para um subdomínio específico** -nome de DNS de um dos  **&lt;subdomínio >** demasiado**&lt;yourwebappname&gt;. azurewebsites.net**. Por exemplo, **blogues** se se destinar a um registo de Olá **blogs.contoso.com**.
* **Para Olá universal sub-dodmains** -registo TXT de DNS A *** demasiado  **&lt;yourwebappname&gt;. azurewebsites.net**.

Este registo TXT é tooverify utilizado que é seu domínio Olá está a tentar efetuar toouse. Além disso, este é de registo toocreating um um endereço IP virtual toohello da sua aplicação web a apontar.

Pode encontrar o endereço IP Olá e **. azurewebsites.net** Olá nomes para a sua aplicação web, efetuando os seguintes passos:

1. No seu browser, abra Olá [Portal do Azure](https://portal.azure.com).
2. No Olá **Web Apps** painel, clique no nome de Olá da sua aplicação web e, em seguida, selecione **domínios personalizados** de Olá parte inferior da página Olá.
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. No Olá **domínios personalizados** painel, verá Olá endereço IP virtual. Guarde esta informação, como será utilizado ao criar registos DNS
   
    ![](./media/custom-dns-web-site/virtual-ip-address.png)
   
   > [!NOTE]
   > Não é possível utilizar nomes de domínio personalizado com um **livres** aplicação web e tem de atualizar Olá plano do App Service demasiado**partilhados**, **básico**, **padrão**, ou **Premium** camada. Para mais informações sobre Olá do serviço de aplicações plano do escalões de preço, incluindo como toochange Olá escalão de preço da sua aplicação web, consulte [tooscale como aplicações web](../articles/app-service-web/web-sites-scale.md).
   > 
   > 

