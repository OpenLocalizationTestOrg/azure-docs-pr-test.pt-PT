## <a name="what-is-table-storage"></a>O que é o armazenamento de Tabelas
O armazenamento de Tabelas do Azure armazena grandes quantidades de dados estruturados. o serviço de Olá é um arquivo de dados NoSQL que aceita chamadas autenticadas de dentro e fora Olá em nuvem do Azure. As tabelas do Azure são ideais para armazenar dados estruturados não relacionais. Utilizações comuns do Armazenamento de Tabelas:

* Armazenamento de TBs de dados estruturados com capacidade para servirem aplicações de dimensionamento da Web
* Armazenamento de conjuntos de dados que não precisam de associações complexas, chaves externas ou procedimentos armazenados e podem ser desnormalizadas para acesso rápido
* Consulta rápida de dados com um índice em cluster
* Aceder aos dados através do protocolo de OData Olá e consultas LINQ com bibliotecas de .NET de serviço de dados WCF

Pode utilizar o Table storage toostore e consultar conjuntos enormes de dados estruturados não relacionais e suas tabelas serão dimensionadas à medida que aumenta a procura.

## <a name="table-storage-concepts"></a>Conceitos de armazenamento de tabelas
O Table storage contém Olá os seguintes componentes:

![diagrama de componente de armazenamento de tabelas][Table1]

* **Formato do URL:** tabelas de códigos de endereços numa conta com este formato de endereço:   
  http://`<storage account>`.table.core.windows.net/`<table>`  
  
  Pode resolver as tabelas do Azure diretamente com este endereço Olá protocolo OData. Para obter mais informações, veja [OData.org][OData.org].
* **Conta de armazenamento:** todas as acesso tooAzure armazenamento é feito através de uma conta de armazenamento. Veja [Metas de Desempenho e Escalabilidade do Storage do Azure](../articles/storage/common/storage-scalability-targets.md) para obter detalhes acerca da capacidade das contas de armazenamento.
* **Tabela**: uma tabela é uma coleção de entidades. As tabelas não impõem um esquema a entidades, o que significa que uma única tabela pode conter entidades que tenham conjuntos diferentes de propriedades. número de Olá de tabelas que uma conta do storage pode conter só está limitado pelo limite de capacidade da conta de armazenamento de Olá.
* **Entidade**: uma entidade é um conjunto de propriedades de linha de base de dados de tooa semelhantes. Uma entidade pode ter segurança too1MB de tamanho.
* **Propriedades**: uma propriedade é um par nome/valor. Cada entidade pode incluir dados de toostore too252 propriedades. Cada entidade tem também três propriedades do sistema que especificam uma chave de partição, uma chave de linha e um carimbo de data/hora. Entidades com Olá mesma chave de partição pode ser consultada mais rapidamente e inseridas/atualizadas em operações atómicas. A chave de linha de uma entidade é o seu identificador exclusivo dentro de uma partição.

Para obter detalhes sobre a nomenclatura das tabelas e as propriedades, consulte [Olá compreender o modelo de dados do serviço tabela](/rest/api/storageservices/Understanding-the-Table-Service-Data-Model).

[Table1]: ./media/storage-table-concepts-include/table1.png
[OData.org]: http://www.odata.org/
