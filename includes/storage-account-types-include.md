Existem dois tipos de contas do armazenamento:

### <a name="general-purpose-storage-accounts"></a>Contas de Armazenamento para fins gerais
Um fornecem de conta do storage para fins gerais que aceder a serviços de armazenamento de tooAzure como tabelas, filas, ficheiros, Blobs e Azure discos da máquina virtual numa conta única. Este tipo de conta de armazenamento tem dois escalões de desempenho:

* Um escalão de desempenho de armazenamento standard que lhe permite toostore tabelas, filas, ficheiros, Blobs e Azure discos da máquina virtual.
* Um escalão de desempenho de armazenamento Premium que atualmente apenas suporta discos de máquinas virtuais do Azure. Veja [Armazenamento Premium: Armazenamento de Elevado Desempenho para Cargas de Trabalho de Máquinas Virtuais do Azure](../articles/storage/common/storage-premium-storage.md) para obter uma descrição geral aprofundada do armazenamento Premium.

### <a name="blob-storage-accounts"></a>Contas do Blob Storage
Uma conta de armazenamento de Blobs é uma conta de armazenamento especializada para armazenar os seus dados não estruturados como blobs (objetos) no Storage do Azure. Contas do blob storage são semelhantes tooyour para fins gerais contas do storage existentes e partilham todas as Olá excelentes características de durabilidade, disponibilidade, escalabilidade e desempenho funcionalidades que utiliza atualmente, incluindo 100% de consistência de API para blobs de blocos e blobs de acréscimo. Para aplicações que requerem apenas armazenamento de blobs de blocos ou de blobs de acréscimo, recomendamos a utilização das contas de armazenamento de Blobs.

> [!NOTE]
> As contas de armazenamento de Blobs suportam apenas blobs de blocos e blobs de acréscimo e não suportam blobs de páginas.
> 
> 

Contas do blob storage expõem Olá **camada de acesso** atributo que pode ser especificado durante a criação da conta e modificado mais tarde, conforme necessário. Existem dois tipos de camadas de acesso que podem ser especificados com base no seu padrão de acesso a dados:

* A **frequente** camada de acesso que indica que Olá objetos na conta do storage Olá serão acedidos com mais frequência. Isto permite-lhe toostore dados a um custo mais baixo acesso.
* A **frios** camada de acesso que indica que Olá objetos na conta do storage Olá serão acedidos com menos frequência. Isto permite-lhe toostore dados a um custo de armazenamento de dados mais baixo.

Se houver alteração Olá padrão de utilização dos seus dados, pode também alternar entre estas camadas de acesso em qualquer altura. Camada de acesso de Olá alteração poderá resultar em encargos adicionais. Veja [Preços e faturação das contas de armazenamento de Blobs ](../articles/storage/blobs/storage-blob-storage-tiers.md#pricing-and-billing) para obter mais detalhes.

Para obter mais detalhes sobre as contas de armazenamento de Blobs, veja [ Blob Storage do Azure: camadas de acesso Frequente e Esporádico](../articles/storage/blobs/storage-blob-storage-tiers.md).

Antes de poder criar uma conta do storage, tem de ter uma subscrição do Azure, o que é um plano que dá-lhe aceder tooa vários serviços do Azure. Pode começar com o Azure com uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/). Assim que decidir toopurchase um plano de subscrição, pode escolher entre uma variedade de [opções de compra](https://azure.microsoft.com/pricing/purchase-options/). Se for um [Subscritor MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), obterá créditos mensais gratuitos que pode utilizar com os serviços do Azure, incluindo o Storage do Azure. Veja [Preços de Armazenamento do Azure ](https://azure.microsoft.com/pricing/details/storage/) para obter informações sobre os preços de volumes.

toolearn como toocreate uma conta de armazenamento, consulte [criar uma conta de armazenamento](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account) para obter mais detalhes. Pode criar cópias de segurança too200 exclusivamente com o nome de contas do storage com uma única subscrição. Veja [Metas de Desempenho e Escalabilidade do Armazenamento do Azure](../articles/storage/common/storage-scalability-targets.md) para obter detalhes sobre os limites das contas de armazenamento.

