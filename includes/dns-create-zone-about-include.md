Uma zona DNS é utilizado toohost Olá registos DNS para um determinado domínio. toostart alojamento do seu domínio no DNS do Azure, terá de toocreate uma zona DNS para que o nome do domínio. Cada registo DNS para o seu domínio é então criado no interior desta zona DNS.

Por exemplo, Olá domínio "contoso.com" pode conter vários registos DNS, tais como "mail.contoso.com" (para um servidor de correio) e "www.contoso.com" (para um web site).

Ao criar uma zona DNS no Azure DNS:

* nome de Olá da zona de Olá têm de ser exclusivo dentro do grupo de recursos de Olá e zona Olá não pode já existir. Caso contrário, a operação de Olá falha.
* Olá mesmo nome de zona pode ser reutilizado num grupo de recursos diferente ou outra subscrição do Azure.
* Em que várias zonas partilham Olá mesmo nome, cada instância é atribuída os endereços de servidor de nome diferente. Apenas um conjunto de endereços pode ser configurado com a entidade de registo de nome de domínio de Olá.

> [!NOTE]
> Não dispõe de tooown um toocreate de nome de domínio uma zona DNS com esse nome de domínio no DNS do Azure. No entanto, terá de servidores de nomes ao DNS do Azure do Olá de tooconfigure tooown Olá domínio como Olá servidores de nomes correto para o nome de domínio de Olá com a entidade de registo de nome de domínio de Olá.
> 
> Para obter mais informações, consulte [delegar tooAzure um domínio DNS](../articles/dns/dns-domain-delegation.md).
