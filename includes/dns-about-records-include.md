### <a name="record-names"></a>Nomes de registo

No DNS do Azure, os registos são especificados com nomes relativos. A *totalmente qualificado* nome de domínio (FQDN) inclui o nome da zona Olá, enquanto que um *relativo* nome não. Por exemplo, nome do registo Olá relativo "www" na zona de Olá "contoso.com" fornece o nome do registo completamente qualificado de Olá "www.contoso.com".

Um *vértice* registo é um registo DNS na raiz de Olá (ou *vértice*) de uma zona DNS. Por exemplo, na zona DNS Olá 'contoso.com', um registo de vértice tem também nome completamente qualificado do Olá 'contoso.com' (Isto denomina-se um *naked* domínio).  Por convenção, Olá nome relativo ' @' é utilizado toorepresent registos de vértice.

### <a name="record-types"></a>Tipos de registo

Cada registo DNS tem um nome e um tipo. Os registos são organizados em vários tipos de acordo com a dados toohello contêm. o tipo mais comuns Olá é um "A" registo, que mapeia um nome tooan endereço IPv4. Outro tipo comum é um registo "MX", que mapeia um servidor de correio tooa do nome.

O DNS do Azure suporta todos os tipos de registo DNS comuns, incluindo A, AAAA, CNAME, MX, NS, PTR, SOA, SRV e TXT. Tenha em atenção que [os registos SPF são representados utilizando registos TXT](../articles/dns/dns-zones-records.md#spf-records).

### <a name="record-sets"></a>Conjuntos de registos

Por vezes, precisa de toocreate mais do que um registo DNS com um determinado nome e tipo. Por exemplo, suponha Olá "www.contoso.com" web site está alojado em dois endereços IP diferentes. site de Olá necessita de dois diferentes registos, um para cada endereço IP. Aqui está um exemplo de um conjunto de registos:

    www.contoso.com.        3600    IN    A    134.170.185.46
    www.contoso.com.        3600    IN    A    134.170.188.221

O DNS do Azure gere todos os registos DNS com *conjuntos de registos*. Um conjunto de registos (também conhecido como um *recursos* conjunto de registos) é Olá coleção de registos DNS numa zona que tenham Olá mesmo nome e de Olá mesmo tipo. A maioria dos conjuntos de registos contêm um único registo. No entanto, os exemplos como Olá um acima, no qual um conjunto de registos contém mais do que um registo, não são incomuns.

Por exemplo, suponha que já criou um registo "www" na zona de Olá "contoso.com", apontando toohello IP endereços '134.170.185.46' (Olá primeiro registo acima).  toocreate Olá segundo registo seria adicionar que registam o registo existente toohello definido, em vez de criar um conjunto de registos adicional.

Olá SOA e tipos de registo CNAME são exceções. as normas DNS de Olá não permitem vários registos com o mesmo nome para estes tipos de Olá, por conseguinte, estes conjuntos de registos só podem conter um único registo.
