| Recurso | Limite Predefinido |
| --- | --- |
| Número de contas do storage por subscrição |200<sup>1</sup> |
| Capacidade de conta de armazenamento máximo |500 TB<sup>2</sup> |
| Número máx. de contentores de BLOBs, blobs, partilhas de ficheiros, tabelas, filas, entidades ou mensagens por conta de armazenamento |Sem limite |
| Tamanho máx. de um contentor de blob único, tabelas ou filas |Igual à capacidade das contas de armazenamento máximo |
| Máximas número de blocos de um blob de blocos ou BLOBs de acréscimo |50,000 |
| Tamanho máx. de um bloco num blob de bloco |100 MB |
| Tamanho máx. de um blob de bloco |50 000 x 100 MB (aprox 4.75 TB) |
| Tamanho máx. de um bloco num blob de acréscimo |4 MB |
| Tamanho máx. de um blob de acréscimo |50 000 4 MB (aprox 195 GB) |
| Tamanho máx. de um blob de página |8 TB |
| Tamanho máx. de uma entidade de tabela |1 MB |
| Número máx. de propriedades de uma entidade de tabela |252 |
| Tamanho máx. de uma mensagem numa fila |64 KB |
| Tamanho máx. de uma partilha de ficheiros |5 TB |
| Tamanho máximo dos ficheiros numa partilha de ficheiros |1 TB |
| Número máx. de ficheiros numa partilha de ficheiros |Apenas o limite é capacidade total de 5 TB Olá Olá da partilha de ficheiros |
| IOPS máximo por partilha |1000 |
| Número máx. de ficheiros numa partilha de ficheiros |Apenas o limite é capacidade total de 5 TB Olá Olá da partilha de ficheiros |
| Número máx. de políticas de acesso armazenada por contentor, partilha de ficheiros, tabelas ou filas |5 |
| Taxa de pedidos de mensagens em fila máximo por conta de armazenamento |BLOBs: pedidos de 20.000 por segundo<sup>2</sup> para blobs de qualquer tamanho válido (limitado apenas por limites de entrada/saída da conta de Olá) <br />Ficheiros: 1000 IOPS (8 KB de tamanho) por partilha de ficheiros <br />Filas: 20.000 mensagens por segundo (partindo do princípio de tamanho da mensagem ' 1 KB ')<br />Tabelas: transações de 20.000 por segundo (partindo do princípio de 1 KB entidade tamanho de) |
| Débito de destino para o blob único |Cópia de segurança too60 MB por segundo ou cópia de segurança too500 pedidos por segundo |
| Débito de destino para a fila única (mensagens de 1 KB) |Cópia de segurança too2000 mensagens por segundo |
| Débito de destino para a partição da tabela individual (entidades de 1 KB) |Cópia de segurança entidades too2000 por segundo |
| Débito de destino para a partilha de ficheiro único |Cópia de segurança too60 MB por segundo |
| Entrada máximo<sup>3</sup> por conta de armazenamento (regiões EUA) |10 Gbps se GRS/ZRS<sup>4</sup> ativada, 20 Gbps para LRS<sup>2</sup> |
| Saída máximo<sup>3</sup> por conta de armazenamento (regiões EUA) |20 Gbps se RA-GRS/GRS/ZRS<sup>4</sup> ativada, 30 Gbps para LRS<sup>2</sup> |
| Entrada máximo<sup>3</sup> por conta de armazenamento (regiões de não-US) |5 Gbps se GRS/ZRS<sup>4</sup> ativada, 10 Gbps para LRS<sup>2</sup> |
| Saída máximo<sup>3</sup> por conta de armazenamento (regiões de não-US) |10 Gbps se RA-GRS/GRS/ZRS<sup>4</sup> ativada, 15 Gbps para LRS<sup>2</sup> |

<sup>1</sup>Isto inclui as contas do storage Standard e Premium. Se necessitar de mais de 200 contas de armazenamento, efetue um pedido através do [Suporte do Azure](https://azure.microsoft.com/support/faq/). equipa de armazenamento do Azure Olá irá consultar o seu cenário de negócio e pode aprovar segurança too250 contas de armazenamento. 

<sup>2</sup> tooget contas de armazenamento standard toogrow passado Olá anunciados limites na taxa de capacidade, a entrada/saída e a pedido,. efetue um pedido de [suporte do Azure](https://azure.microsoft.com/support/faq/). equipa de armazenamento do Azure Olá irá rever pedido Olá e pode aprovar os limites superiores numa base de maiúsculas e minúsculas, maiúsculas e minúsculas.

<sup>3</sup>*entrada* refere-se os dados de tooall (pedidos) que está a ser enviados tooa conta de armazenamento. *Saída* refere-se os dados de tooall (respostas) que está a ser recebidos de uma conta de armazenamento.  

<sup>4</sup>as opções de replicação do Storage do azure incluem:
* **RA-GRS**: armazenamento georredundante com acesso de leitura. Se estiver ativada RA-GRS, destinos de saída para a localização secundária Olá são idêntico toothose para a localização principal Olá.
* **GRS**: armazenamento georredundante. 
* **O ZRS**: armazenamento com redundância de zona. Disponível apenas para blobs de blocos. 
* **LRS**: armazenamento localmente redundante. 


