Neste passo, testar a escuta do grupo de disponibilidade de Olá utilizando uma aplicação cliente que está em execução no Olá mesma rede.

Conectividade de clientes tem Olá os seguintes requisitos:

* Serviço de escuta de toohello de ligações de cliente tem de ser de máquinas que residem num serviço cloud diferente que Olá um que anfitriões Olá réplicas de disponibilidade Always On.
* Se Olá Always On réplicas estarem em sub-redes diferentes, os clientes têm de especificar *MultisubnetFailover = True* na cadeia de ligação de Olá. Isto resulta de condição na ligação paralela tenta tooreplicas no Olá várias sub-redes. Este cenário inclui a uma implementação de por várias regiões Always On disponibilidade grupo.

Um exemplo é o serviço de escuta do tooconnect toohello a partir de um Olá VMs no Olá mesma rede virtual do Azure (mas não um que aloja uma réplica). Uma forma fácil toocomplete este teste é de escuta de grupo de disponibilidade SQL Server Management Studio toohello tootry tooconnect. Outro método simple é toorun [SQLCMD.exe](https://technet.microsoft.com/library/ms162773.aspx), da seguinte forma:

    sqlcmd -S "<ListenerName>,<EndpointPort>" -d "<DatabaseName>" -Q "select @@servername, db_name()" -l 15

> [!NOTE]
> Se for Olá EndpointPort valor *1433*, não são necessária toospecify-lo na chamada de Olá. Olá chamada anterior também assume que a máquina cliente Olá toohello associado ao mesmo domínio e que chamador Olá foram concedidas permissões na base de dados de Olá, utilizando a autenticação do Windows.
> 
> 

Quando testar o serviço de escuta de Olá, ser toofail se através de toomake de grupo de disponibilidade de Olá certificar-se de que os clientes podem ligar o serviço de escuta do toohello entre as ativações pós-falha.

