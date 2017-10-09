---
title: aaaManaging simultaneidade no armazenamento do Microsoft Azure
description: "Como toomanage simultaneidade Olá serviços Blob, fila, tabela e ficheiro"
services: storage
documentationcenter: 
author: jasontang501
manager: tadb
editor: tysonn
ms.assetid: cc6429c4-23ee-46e3-b22d-50dd68bd4680
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: jasontang501
ms.openlocfilehash: 277fbbb880906da6be67b2267ed5c8e457455bd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-concurrency-in-microsoft-azure-storage"></a>Gerir a Simultaneidade no Armazenamento do Microsoft Azure
## <a name="overview"></a>Descrição geral
Aplicações modernas de Internet com base normalmente têm vários utilizadores ver e atualizar os dados em simultâneo. Isto requer que os programadores de aplicações toothink cuidadosamente sobre como tooprovide previsível uma experiência que os utilizadores finais tootheir, particularmente para cenários em que vários utilizadores podem atualizar Olá mesmo dados. Existem três estratégias de simultaneidade de dados principais programadores, normalmente, iremos considerar:  

1. Simultaneidade otimista – uma aplicação, efetuar uma atualização como parte da respetiva atualização verificará se os dados de Olá foi alterada desde aplicação Olá pela última vez ler os dados. Por exemplo, se dois utilizadores visualizar uma página wiki efetuar uma atualização toohello página mesmo, a plataforma de wiki Olá tem de se certificar que Olá segundo a atualização não substituir a primeira atualização Olá – e que ambos os utilizadores compreender se os seus atualização foi concluída com êxito ou não. Esta estratégia é frequentemente utilizada em aplicações web.
2. Simultaneidade pessimistic – uma aplicação que está à procura tooperform uma atualização irá demorar um bloqueio de um objeto a impedir que outros utilizadores ao actualizar dados de Olá até que o bloqueio de Olá é libertado. Por exemplo, um cenário de replicação de dados principal/subordinado onde o mestre de Olá apenas irá efetuar atualizações mestre Olá normalmente armazena um bloqueio exclusivo para um período prolongado de tempo no Olá dados tooensure não ninguém pode atualizá-lo.
3. Último escritor wins – uma abordagem que permite que qualquer tooproceed de operações de atualização sem verificar se qualquer outra aplicação tem Olá dados atualizados, uma vez que a aplicação Olá ler primeiro dados Olá. Esta estratégia (ou à falta de uma estratégia de formal) é normalmente utilizada em que os dados estão particionados de forma a que não há nenhum probabilidade que vários utilizadores terão acesso às Olá mesmos dados. Pode também ser útil em que estão a ser processados fluxos de dados de curta duração.  

Este artigo fornece uma descrição geral de como plataforma de armazenamento do Azure Olá simplifica a programação ao fornecer suporte de primeira classe para todas as três estratégias estes concorrência.  

## <a name="azure-storage--simplifies-cloud-development"></a>Armazenamento do Azure – simplifica a programação de nuvem
Olá serviço de armazenamento do Azure suporta todas as estratégias de três, embora seja distinctive no respetivo suporte completo de tooprovide de capacidade de simultaneidade otimista e pessimistic porque foi concebida tooembrace um modelo a consistência forte garante que, ao Olá consolidações de serviço de armazenamento dados de inserir ou atualizar a operação de todos os dados de toothat acessos mais Verão Olá atualização mais recente. Plataformas de armazenamento que utilizam um modelo de consistência eventual têm um atraso entre quando uma operação de escrita é efetuada por um utilizador e quando Olá atualizado dados podem ser vistos por outros utilizadores, por conseguinte, complicating desenvolvimento de aplicações de cliente no inconsistências de tooprevent de ordem de afetar os utilizadores finais.  

Além disso tooselecting um programadores de estratégia de concorrência adequado devem também estar ciente de como uma plataforma de armazenamento isola as alterações – particularmente toohello de alterações mesmo objeto em transações. Olá serviço de armazenamento do Azure utiliza tooallow de isolamento do instantâneo ler operações toohappen simultaneamente com operações de escrita dentro de uma única partição. Ao contrário de outros níveis de isolamento, o isolamento do instantâneo garante que todas as leituras consulte um instantâneo consistente dos dados de Olá, mesmo quando as atualizações estão a ocorrer – essencialmente ao devolver valores de consolidada último Olá enquanto uma transação de atualização está a ser processada.  

## <a name="managing-concurrency-in-blob-storage"></a>Gerir a simultaneidade no Blob storage
Pode optar ativamente por participar toouse a simultaneidade otimista ou pessimistic modelos toomanage acesso tooblobs e contentores no Olá serviço blob. Se não especificar explicitamente uma estratégia de última escreve wins é a predefinição de Olá.  

### <a name="optimistic-concurrency-for-blobs-and-containers"></a>Simultaneidade otimista para os blobs e contentores
Olá serviço de armazenamento atribui um objeto de tooevery identificador armazenado. Este identificador é atualizado sempre que é executada uma operação de atualização de um objeto. Identificador de Olá é devolvido toohello cliente como parte de uma resposta de HTTP GET utilizando o cabeçalho do Olá ETag (tag de entidade) que esteja definido no protocolo Olá HTTP. Um utilizador efetuar uma atualização desse objecto pode enviar por Olá ETag original juntamente com um cabeçalho condicional tooensure que uma atualização situação ocorrerá apenas se tiver sido cumprida uma condição de determinados – neste caso, a condição de Olá é um cabeçalho de "If-Match" que necessita de Olá armazenamento Serviço tooensure Olá valor Olá ETag especificado no pedido de actualização Olá é Olá idênticos aos armazenados no Olá serviço de armazenamento.  

Descrição de Olá deste processo é o seguinte:  

1. Obter um blob do serviço de armazenamento de Olá, resposta Olá inclui um valor de cabeçalho ETag de HTTP que identifica a versão atual do Olá do objeto de Olá no serviço de armazenamento Olá.
2. Quando atualizar o blob Olá, incluir valor ETag de Olá recebido no passo 1 Olá **If-Match** condicional cabeçalho de pedido de Olá enviar toohello serviço.
3. serviço de Olá compara o valor de ETag de Olá no pedido de Olá com o valor ETag atual Olá do blob Olá.
4. Se o valor ETag atual Olá do blob Olá é uma versão diferente de Olá ETag no Olá **If-Match** cabeçalho condicional num pedido de Olá, serviço Olá devolve um cliente de toohello 412 erro. Isto indica que outro processo atualizou blob Olá, uma vez que o cliente de Olá obtido de cliente de toohello.
5. Se Olá atual ETag é o valor de blob Olá Olá mesma versão que Olá ETag no Olá **If-Match** cabeçalho condicional num pedido de Olá, serviço Olá efetua Olá pedida a operação e atualizações Olá valor ETag atual do blob Olá tooshow que criou uma nova versão.  

Olá seguinte fragmento de c# (utilizando Olá biblioteca de clientes de armazenamento 4.2.0) mostra um exemplo simples como tooconstruct um **If-Match AccessCondition** com base no Olá valor ETag, que é acedida a partir das propriedades de Olá de um blob que foi anteriormente obtido ou inserida. Em seguida, utiliza Olá **AccessCondition** objeto quando-atualizar blob Olá: Olá **AccessCondition** objeto adiciona Olá **If-Match** pedido toohello de cabeçalho. Se outro processo tiver atualizado o blob Olá, o serviço de blob Olá devolve uma mensagem de estado 412 HTTP (falha de pré-condição). Pode transferir o exemplo completo Olá aqui: [gerir concorrência com o Storage do Azure](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).  

```csharp
// Retrieve hello ETag from hello newly created blob
// Etag is already populated as UploadText should cause a PUT Blob call
// toostorage blob service which returns hello etag in response.
string orignalETag = blockBlob.Properties.ETag;

// This code simulates an update by a third party.
string helloText = "Blob updated by a third party.";

// No etag, provided so orignal blob is overwritten (thus generating a new etag)
blockBlob.UploadText(helloText);
Console.WriteLine("Blob updated. Updated ETag = {0}",
blockBlob.Properties.ETag);

// Now try tooupdate hello blob using hello orignal ETag provided when hello blob was created
try
{
    Console.WriteLine("Trying tooupdate blob using orignal etag toogenerate if-match access condition");
    blockBlob.UploadText(helloText,accessCondition:
    AccessCondition.GenerateIfMatchCondition(orignalETag));
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
    {
        Console.WriteLine("Precondition failure as expected. Blob's orignal etag no longer matches");
        // TODO: client can decide on how it wants toohandle hello 3rd party updated content.
    }
    else
        throw;
}  
```

Olá serviço de armazenamento também inclui suporte para os cabeçalhos condicionais adicionais, tais como **If-modificado-Since**, **If-Unmodified-Since** e **If-None-Match** , bem como combinações de ambos. Para obter mais informações consulte [especificando condicional cabeçalhos para operações de serviço Blob](http://msdn.microsoft.com/library/azure/dd179371.aspx) no MSDN.  

Olá tabela seguinte resume as operações de contentor Olá que aceitam, tais como cabeçalhos condicionais **If-Match** no pedido de Olá e que devolva um valor ETag na resposta Olá.  

| Operação | Devolve o valor ETag de contentor | Aceita condicionais cabeçalhos |
|:--- |:--- |:--- |
| Criar contentor |Sim |Não |
| Obter as propriedades do contentor |Sim |Não |
| Obter metadados do contentor |Sim |Não |
| Definir os metadados do contentor |Sim |Sim |
| Obter o contentor ACL |Sim |Não |
| Definir o contentor ACL |Sim |Sim (*) |
| Eliminar o contentor |Não |Sim |
| Contentor de concessão |Sim |Sim |
| Lista de Blobs |Não |Não |

(*) as permissões Olá definidas pelo SetContainerACL são colocadas em cache e atualizações toothese permissões que demore 30 segundos toopropagate durante o período de atualizações não são garantida toobe consistente.  

Olá tabela seguinte resume as operações de BLOBs de Olá aceitam, tais como cabeçalhos condicionais **If-Match** no pedido de Olá e que devolva um valor ETag na resposta Olá.

| Operação | Devolve o valor ETag | Aceita condicionais cabeçalhos |
|:--- |:--- |:--- |
| Colocar Blob |Sim |Sim |
| Obter o Blob |Sim |Sim |
| Obter propriedades de Blob |Sim |Sim |
| Defina as propriedades de Blob |Sim |Sim |
| Obter metadados do Blob |Sim |Sim |
| Definir os metadados do Blob |Sim |Sim |
| Blob de concessão (*) |Sim |Sim |
| Blob de instantâneo |Sim |Sim |
| Copiar Blob |Sim |Sim (para o blob de origem e de destino) |
| Abortar copiar Blob |Não |Não |
| Eliminar o Blob |Não |Sim |
| Colocar bloco |Não |Não |
| Colocar a lista de bloqueios |Sim |Sim |
| Obter a lista de bloqueios |Sim |Não |
| Colocar a página |Sim |Sim |
| Obter intervalos de página |Sim |Sim |

(*) Blob de concessão não altera Olá ETag no blob.  

### <a name="pessimistic-concurrency-for-blobs"></a>Simultaneidade pessimistic blobs
um blob para utilização exclusiva toolock, pode adquirir um [concessão](http://msdn.microsoft.com/library/azure/ee691972.aspx) no mesmo. Quando adquirir uma concessão, especifique durante quanto precisa Olá concessão: Isto pode ser de entre 15 segundos too60 ou infinito que bloqueio exclusivo do tooan de quantidades. Pode renovar um tooextend concessão finito e pode de versão qualquer concessão quando tiver terminado com o mesmo. serviço de blob Olá versões automaticamente concessões finito quando expirarem.  

Concessões ativar toobe do estratégias de sincronização diferentes suportado, incluindo escrita exclusiva / partilhado a escrita de leitura, exclusiva / exclusiva de ler e partilhado de escrita / leitura exclusivos. Onde existe uma concessão do serviço de armazenamento Olá impõe exclusiva de escritas (put, defina e eliminar operações) no entanto, garantir exclusivity para operações de leitura requer Olá programador tooensure que todas as aplicações de cliente utilizam um ID de concessão e que o cliente apenas um de cada vez tem um ID de concessão válido. Operações de leitura que inclua um resultado de ID de concessão no leituras partilhadas.  

Olá c# fragmento seguinte mostra um exemplo de adquirir uma concessão exclusiva para 30 segundos num blob, atualização de Olá conteúdo de blob Olá e, em seguida, libertar concessão Olá. Se já existir uma concessão válida no blob Olá quando tenta tooacquire uma concessão novo, o serviço de blob de Olá devolve um resultado de estado de "Conflito HTTP (409)". o fragmento de Olá abaixo utiliza um **AccessCondition** objeto informações de concessão de Olá tooencapsulate quando faz um pedido tooupdate Olá de blob no serviço de armazenamento Olá.  Pode transferir o exemplo completo Olá aqui: [gerir concorrência com o Storage do Azure](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).

```csharp
// Acquire lease for 15 seconds
string lease = blockBlob.AcquireLease(TimeSpan.FromSeconds(15), null);
Console.WriteLine("Blob lease acquired. Lease = {0}", lease);

// Update blob using lease. This operation will succeed
const string helloText = "Blob updated";
var accessCondition = AccessCondition.GenerateLeaseCondition(lease);
blockBlob.UploadText(helloText, accessCondition: accessCondition);
Console.WriteLine("Blob updated using an exclusive lease");

//Simulate third party update tooblob without lease
try
{
    // Below operation will fail as no valid lease provided
    Console.WriteLine("Trying tooupdate blob without valid lease");
    blockBlob.UploadText("Update without lease, will fail");
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
        Console.WriteLine("Precondition failure as expected. Blob's lease does not match");
    else
        throw;
}  
```

Se tentar uma operação de escrita no blob em leasing sem transmissão do ID de concessão de Olá, o pedido de Olá falha com um erro de 412. Tenha em atenção que se hello expira concessão antes de chamar Olá **UploadText** método mas ainda transmita o ID de concessão de Olá, pedido Olá também falha com um **412** erro. Para obter mais informações sobre a gestão de tempos de expiração de concessão e ids de concessão, consulte Olá [concessão Blob](http://msdn.microsoft.com/library/azure/ee691972.aspx) documentação REST.  

Olá seguintes operações de blob podem utilizar concessões toomanage pessimistic concorrência:  

* Colocar Blob
* Obter o Blob
* Obter propriedades de Blob
* Defina as propriedades de Blob
* Obter metadados do Blob
* Definir os metadados do Blob
* Eliminar o Blob
* Colocar bloco
* Colocar a lista de bloqueios
* Obter a lista de bloqueios
* Colocar a página
* Obter intervalos de página
* Blob de instantâneo - ID de concessão opcional se existir uma concessão
* Copiar Blob - concessão ID necessárias se uma concessão existe no blob de destino Olá
* Necessário de ID de concessão de BLOBs de cópia de abortar - se uma concessão infinita existe no blob de destino Olá
* Blob de concessão  

### <a name="pessimistic-concurrency-for-containers"></a>Simultaneidade pessimistic para contentores
Concessões nos contentores ativar Olá mesmo toobe de estratégias de sincronização suportado como blobs (exclusiva de escrita / partilhado a escrita de leitura, exclusiva / exclusiva de ler e partilhado de escrita / leitura exclusivo) no entanto, ao contrário de blobs de serviço de armazenamento Olá apenas impõe exclusivity operações de eliminação. toodelete um contentor com uma concessão ativa, um cliente tem de incluir Olá ID de concessão ativa com pedidos de eliminação de Olá. Todas as outras operações de contentor ter êxito se for um contentor em leasing sem incluir o ID de concessão de Olá caso em que são partilhados operações. Se for necessária a exclusivity de atualização (put ou definido) ou operações de leitura, em seguida, os programadores devem certificar-se que todos os clientes utilizam um ID de concessão e que apenas um cliente a uma hora tem um ID de concessão válido.  

Olá seguintes operações de contentor podem utilizar concessões toomanage pessimistic concorrência:  

* Eliminar o contentor
* Obter as propriedades do contentor
* Obter metadados do contentor
* Definir os metadados do contentor
* Obter o contentor ACL
* Definir o contentor ACL
* Contentor de concessão  

Para obter mais informações, consulte:  

* [Especificar condicionais cabeçalhos para operações de serviço Blob](http://msdn.microsoft.com/library/azure/dd179371.aspx)
* [Contentor de concessão](http://msdn.microsoft.com/library/azure/jj159103.aspx)
* [Blob de concessão](http://msdn.microsoft.com/library/azure/ee691972.aspx)

## <a name="managing-concurrency-in-hello-table-service"></a>A gestão de concorrência Olá serviço tabela
serviço de tabela Olá utiliza otimista simultaneidade verifica como comportamento predefinido de Olá quando estiver a trabalhar com as entidades, ao contrário do serviço de blob olá onde deve escolher explicitamente tooperform simultaneidade otimista verificações. Olá outra diferença entre os serviços de tabela e BLOBs Olá é que só pode gerir comportamento de concorrência Olá de entidades enquanto com o serviço de blob Olá pode gerir simultaneidade de Olá de contentores e blobs.  

simultaneidade otimista toouse e toocheck se outro processo modificou uma entidade, uma vez que obtidos a partir do serviço de armazenamento de tabela Olá, pode utilizar o valor de ETag Olá que recebe quando o serviço de tabela Olá devolve uma entidade. Descrição de Olá deste processo é o seguinte:  

1. Obter uma entidade a partir do serviço de armazenamento de tabela Olá, resposta Olá inclui um valor ETag que identifica o identificador atual Olá associado a essa entidade no serviço de armazenamento Olá.
2. Quando atualizar entidade Olá, incluir valor ETag de Olá recebido no passo 1 Olá obrigatório **If-Match** cabeçalho de pedido de Olá enviar toohello serviço.
3. serviço de Olá compara o valor de ETag de Olá no pedido de Olá com o valor ETag atual Olá da entidade de Olá.
4. Se o valor ETag atual Olá da entidade de Olá é diferente de Olá ETag no Olá obrigatório **If-Match** cabeçalho no pedido de Olá, serviço Olá devolve um cliente de toohello 412 erro. Isto indica que outro processo atualizou a entidade de Olá, uma vez que o cliente de Olá obtido de cliente de toohello.
5. Se o valor ETag atual Olá da entidade de Olá é Olá igual ao hello ETag no Olá obrigatório **If-Match** cabeçalho no pedido de Olá ou Olá **If-Match** cabeçalho contém Olá caráter de caráter universal (*), serviço Olá efetua Olá pedida a operação e atualizações Olá valor ETag atual do Olá entidade tooshow que tenha sido atualizado.  

Tenha em atenção que, ao contrário do serviço de blob Olá, serviço de tabela Olá requer Olá cliente tooinclude um **If-Match** cabeçalho em pedidos de atualização. No entanto, é possível tooforce um incondicional atualizar (último escritor wins estratégia) e ignorar a simultaneidade verifica se o cliente de Olá define Olá **If-Match** cabeçalho toohello caráter universal (*) pedido Olá.  

Olá c# fragmento a seguir mostra uma entidade de cliente que foi está criada anteriormente ou a obtenção de ter o respetivo endereço de e-mail atualizado. Olá inicial inserir ou obter valor ETag da operação arquivos Olá no objeto de cliente Olá e uma vez que utiliza o exemplo Olá hello mesma instância de objeto, quando executa a Olá operação de substituição, envia automaticamente Olá ETag valor back toohello tabela serviço Ativar Olá serviço toocheck de violações de concorrência. Se outro processo tiver atualizado entidade Olá no table storage, o serviço de Olá devolve uma mensagem de estado de 412 HTTP (falha de pré-condição).  Pode transferir o exemplo completo Olá aqui: [gerir concorrência com o Storage do Azure](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).

```csharp
try
{
    customer.Email = "updatedEmail@contoso.org";
    TableOperation replaceCustomer = TableOperation.Replace(customer);
    customerTable.Execute(replaceCustomer);
    Console.WriteLine("Replace operation succeeded.");
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == 412)
        Console.WriteLine("Optimistic concurrency violation – entity has changed since it was retrieved.");
    else
        throw;
}  
```

tooexplicitly desativar a verificação de concorrência Olá, deverá definir Olá **ETag** propriedade Olá **empregado** objeto demasiado "*" antes de executar a operação de substituição de Olá.  

```csharp
customer.ETag = "*";  
```

Olá tabela seguinte resume como operações da entidade Olá tabela utilizam ETag valores:

| Operação | Devolve o valor ETag | Necessita de cabeçalho de pedido de If-Match |
|:--- |:--- |:--- |
| Entidades de consulta |Sim |Não |
| Inserir a entidade |Sim |Não |
| Entidade de atualização |Sim |Sim |
| Intercalar entidade |Sim |Sim |
| Eliminar a entidade |Não |Sim |
| Inserir ou substituir entidade |Sim |Não |
| Inserir ou Merge entidade |Sim |Não |

Tenha em atenção que Olá **inserir ou substituir entidade** e **inserção ou entidade intercalar** efetue operações *não* efetuar as verificações de concorrência porque não enviar uma toohello de valor ETag serviço tabela.  

Em geral, os programadores com tabelas deverá confiar na simultaneidade otimista quando desenvolver aplicações dimensionáveis. Se necessitar de bloqueio pessimistic, os programadores de uma abordagem podem tomar quando aceder a tabelas é tooassign um blob designado para cada tabela e tente tootake uma concessão no blob Olá antes da tabela de Olá a utilizar. Esta abordagem requer Olá aplicação tooensure acesso a dados todos os caminhos de obter a concessão de Olá anterior toooperating na tabela de Olá. Também deve note que o período de concessão mínima de Olá é 15 segundos que requer cuidado considerações sobre escalabilidade.  

Para obter mais informações, consulte:  

* [Operações de entidades](http://msdn.microsoft.com/library/azure/dd179375.aspx)  

## <a name="managing-concurrency-in-hello-queue-service"></a>A gestão de concorrência Olá serviço fila
Um cenário que no qual simultaneidade for uma preocupação no serviço de colocação de Olá é onde vários clientes são obtenção de uma fila de mensagens. Quando uma mensagem é obtida da fila de Olá, resposta Olá inclui a mensagem de saudação e um valor de receção pop, que é a mensagem de saudação toodelete necessária. mensagem de saudação não é automaticamente eliminada da fila de Olá mas, depois de obtido, não é visível tooother clientes para o intervalo de tempo de Olá especificado pelo parâmetro de visibilitytimeout Olá. cliente de Olá que obtém a mensagem de saudação é mensagem de saudação toodelete esperado depois de ser processada e antes de Olá tempo especificado pelo Olá TimeNextVisible o elemento de resposta Olá, que é calculada com base no valor Olá Olá visibilitytimeout parâmetro. valor Olá visibilitytimeout é adicionada tempo toohello no qual Olá mensagem é obter o valor Olá toodetermine TimeNextVisible.  

serviço de fila de Olá não tem suporte para simultaneidade otimista ou pessimistic e para este clientes razão, as mensagens obtidas a partir de uma fila de processamento devem certificar-se as mensagens são processadas de forma idempotent. Uma estratégia de wins último escritor é utilizada para operações de atualização como SetQueueServiceProperties, SetQueueMetaData, SetQueueACL e UpdateMessage.  

Para obter mais informações, consulte:  

* [API de REST do serviço fila](http://msdn.microsoft.com/library/azure/dd179363.aspx)
* [Receber mensagens](http://msdn.microsoft.com/library/azure/dd179474.aspx)  

## <a name="managing-concurrency-in-hello-file-service"></a>A gestão de concorrência Olá serviço de ficheiros
serviço de ficheiros de Olá pode ser acedido através de dois protocolo diferentes pontos finais – SMB e REST. Olá serviço REST não tem suporte para o bloqueio otimista ou bloqueio pessimistic e todas as atualizações serão siga uma estratégia de wins último escritor. Clientes SMB que montagem partilhas de ficheiros podem tirar partido do ficheiro bloqueio mecanismos toomanage acesso tooshared ficheiros do sistema – incluindo Olá capacidade tooperform pessimistic bloqueio. Quando um cliente do SMB abre um ficheiro, especifica o acesso a ficheiros Olá e partilha modo. Definir uma opção de acesso a ficheiros de "Escrever" ou "Leitura/escrita" juntamente com um modo de partilha de ficheiros de "None" resultará no ficheiro de Olá a ser bloqueado por um cliente do SMB, até que o ficheiro de Olá está fechado. Se a operação REST for tentada num ficheiro em que um cliente do SMB tem os ficheiros de Olá bloqueado Olá serviço REST irá devolver o código de estado 409 (conflito) com o código de erro SharingViolation.  

Quando um cliente do SMB abre um ficheiro para eliminar, marca ficheiro Olá como pendente eliminação até que todos os outros clientes SMB são fechadas alças abertas nesse ficheiro. Enquanto um ficheiro é marcado como pendente delete, qualquer operação REST nesse ficheiro irá devolver o código de estado 409 (conflito) com o código de erro SMBDeletePending. Não é devolvido o código de estado 404 (não for encontrado), uma vez que é possível hello do Olá SMB cliente tooremove pendentes ficheiros de Olá eliminação sinalizador tooclosing anterior. Por outras palavras, código de estado 404 (não for encontrado) só é esperado quando Olá ficheiro foi removido. Tenha em atenção que enquanto um ficheiro está a ser um SMB estado de eliminação pendente, não será incluído no Olá que listam os ficheiros de resultados. Tenha em atenção que as operações de eliminação de ficheiros de REST e REST eliminar o diretório de Olá são consolidadas atomically e resulta numa pendentes eliminará também estado.  

Para obter mais informações, consulte:  

* [Gerir ficheiros bloqueia](http://msdn.microsoft.com/library/azure/dn194265.aspx)  

## <a name="summary-and-next-steps"></a>Resumo e os passos seguintes
Olá armazenamento do Microsoft Azure, o serviço foi concebido necessidades de Olá toomeet de aplicações online mais complexas de Olá sem forçar a programadores toocompromise ou rethink estrutura chave pressupostos, tais como a consistência de dados e de concorrência que tenham entram tootake Para conceder.  

Para Olá conclua a aplicação de exemplo referenciada neste blogue:  

* [Gestão de concorrência com o Storage do Azure - exemplo de aplicação](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114)  

Para obter mais informações, consulte Storage do Azure:  

* [Página inicial de armazenamento do Microsoft Azure](https://azure.microsoft.com/services/storage/)
* [Introdução tooAzure armazenamento](storage-introduction.md)
* Armazenamento de introdução para [Blob](storage-dotnet-how-to-use-blobs.md), [tabela](storage-dotnet-how-to-use-tables.md), [filas](storage-dotnet-how-to-use-queues.md), e [ficheiros](storage-dotnet-how-to-use-files.md)
* Arquitetura de armazenamento – [Storage do Azure: um serviço de armazenamento de nuvem de elevada disponibilidade com consistência forte](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

