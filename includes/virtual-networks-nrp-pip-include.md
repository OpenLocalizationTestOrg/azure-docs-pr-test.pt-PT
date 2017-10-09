## <a name="public-ip-address"></a>Endereço IP público
Fornece um recurso de endereço IP público ou uma com acesso à endereço IP de Internet reservado ou dinâmico. Apesar de poder criar um endereço IP público como um objeto de autónomo, tem de tooassociate-tooanother objeto tooactually utilizar endereço Olá. Pode associar um balanceador de carga do tooa de endereço IP público, gateway de aplicação ou uma NIC tooprovide Internet aceder toothose a recursos.  

| Propriedade | Descrição | Valores de exemplo |
| --- | --- | --- |
| **publicIPAllocationMethod** |Define se é o endereço IP Olá *estático* ou *dinâmica*. |estática, dinâmica |
| **idleTimeoutInMinutes** |Define Olá inativo tempo limite, com um valor predefinido de 4 minutos. Se não for recebida nenhuma mais pacotes para uma determinada sessão dentro desta vez, Olá de sessão é terminada. |qualquer valor entre 4 e 30 |
| **ipAddress** |Endereço IP atribuído tooobject. Esta é uma propriedade só de leitura. |104.42.233.77 |

### <a name="dns-settings"></a>Definições de DNS
Endereços IP públicos têm um objeto subordinado com o nome **dnsSettings** contendo Olá seguintes propriedades:

| Propriedade | Descrição | Valores de exemplo |
| --- | --- | --- |
| **domainNameLabel** |Com o nome do anfitrião utilizado para a resolução do nome. |www, ftp, vm1 |
| **FQDN** |Nome completamente qualificado para o IP público Olá. |www.westus.cloudapp.Azure.com |
| **reverseFqdn** |Nome de domínio completamente qualificado que resolve toohello endereço IP e está registado no DNS como um registo PTR. |www.contoso.com. |

Exemplo público endereço IP no formato JSON:

    {
       "name": "PIP01",
       "location": "North US",
       "tags": { "key": "value" },
       "properties": {
          "publicIPAllocationMethod": "Static",
          "idleTimeoutInMinutes": 4,
          "ipAddress": "104.42.233.77",
          "dnsSettings": {
             "domainNameLabel": "mylabel",
             "fqdn": "mylabel.westus.cloudapp.azure.com",
             "reverseFqdn": "contoso.com."
          }
       }
    } 

### <a name="additional-resources"></a>Recursos adicionais
* Obter mais informações [endereços IP públicos](../articles/virtual-network/virtual-networks-reserved-public-ip.md).
* Saiba mais sobre [instância nível endereços IP públicos](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).
* Olá leitura [documentação de referência da REST API](https://msdn.microsoft.com/library/azure/mt163638.aspx) para o IP público endereços.

