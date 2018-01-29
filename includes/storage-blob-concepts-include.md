## <a name="what-is-blob-storage"></a>O que é o Blob storage?
O Blob Storage do Azure é um serviço para armazenar grandes quantidades de dados de objetos não estruturados, como texto ou dados binários, que podem ser acedidos de qualquer local no mundo através de HTTP ou HTTPS. Pode utilizar o armazenamento de Blobs para expor publicamente os dados ao mundo ou para armazenar dados da aplicação em privado.

Utilizações comuns do armazenamento de Blobs:

* Que serve imagens ou documentos diretamente a um browser.
* Armazenamento de ficheiros para acesso distribuído.
* Transmissão em fluxo de áudio e vídeo.
* Armazenamento de dados para cópia de segurança e restauro, recuperação após desastre e arquivo.
* Armazenamento de dados para análise no local ou serviço alojado no Azure.

## <a name="blob-service-concepts"></a>Conceitos do serviço Blob
O serviço Blob contém os seguintes componentes:

![Diagrama da arquitetura de serviço Blob](./media/storage-blob-concepts-include/blob1.png)

* **Conta de armazenamento:** todos os acessos ao Storage do Azure é efetuado através de uma conta de armazenamento. Esta conta de armazenamento pode ser um **conta do storage para fins gerais** ou um **conta de armazenamento de BLOBs**, que é especializada para armazenar objetos ou os blobs. Consulte [About Azure storage accounts (Acerca das contas de armazenamento do Azure)](../articles/storage/common/storage-create-storage-account.md) para obter mais informações.
* **Contentor:** um contentor fornece um agrupamento de um conjunto de blobs. Todos os blobs tem de estar num contentor. Uma conta pode conter um número ilimitado de contentores. Um contentor pode armazenar um número ilimitado de blobs. Tenha em atenção que o nome do contentor tem de ser em minúsculas.
* **Blob:** um ficheiro de qualquer tipo e tamanho. Storage do Azure oferece três tipos de blobs: blobs de blocos, blobs de acréscimo e blobs de páginas.
  
    Os *blobs de blocos* são ideais para armazenar ficheiros de texto ou binários, como documentos e ficheiros multimédia. Um único blob de blocos pode conter até 50.000 blocos com um máximo de 100 MB cada, para um tamanho total ligeiramente acima de 4.75 TB (100 MB X 50.000). 

    Os *blobs de acréscimo* são semelhantes aos blobs de blocos na medida em que são constituídos por blocos, mas estão otimizados para operações de acréscimo, sendo pois úteis para cenários de registo. Um único blob de acréscimo pode conter até 50.000 blocos com um máximo de 4 MB cada, para um tamanho total ligeiramente acima de 195 GB (4 MB X 50.000).
  
    Os *blobs de páginas* podem ter até 1 TB de tamanho e são mais eficientes para operações de leitura/escrita frequentes. Máquinas virtuais do Azure utilizam blobs de páginas como discos de dados e de sistema operativo.
  
    Para obter detalhes sobre a nomenclatura contentores e blobs, veja [nomenclatura e referência de contentores, blobs e metadados](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).

