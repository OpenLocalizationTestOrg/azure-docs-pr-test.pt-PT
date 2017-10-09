---
title: "Encriptação do lado do aaaClient com o Java para armazenamento do Microsoft Azure | Microsoft Docs"
description: "Olá biblioteca de clientes do Storage do Azure para Java suporta encriptação do lado do cliente e a integração com o Cofre de chaves do Azure para segurança máxima para as suas aplicações de armazenamento do Azure."
services: storage
documentationcenter: java
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: 3df49907-554c-404a-9b0c-b3e3269ad04f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 05/11/2017
ms.author: lakasa
ms.openlocfilehash: cb40c737b9065005f0f31f654e7e43fd27b923f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-and-azure-key-vault-with-java-for-microsoft-azure-storage"></a>Encriptação do lado do cliente e o Azure Cofre de chaves com o Java para armazenamento do Microsoft Azure
[!INCLUDE [storage-selector-client-side-encryption-include](../../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>Descrição geral
Olá [biblioteca de clientes do Storage do Azure para Java](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage) suporta a encriptação de dados dentro de aplicações de cliente antes de carregar tooAzure armazenamento e a desencriptação de dados ao transferir toohello cliente. biblioteca de Olá também suporta a integração com [Cofre de chaves do Azure](https://azure.microsoft.com/services/key-vault/) para gestão de chaves de conta de armazenamento.

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>Encriptação e desencriptação através de técnica de envelope Olá
os processos de Olá de encriptação e desencriptação siga técnica de envelope Olá.  

### <a name="encryption-via-hello-envelope-technique"></a>Encriptação através de técnica de envelope Olá
Encriptação através de técnica de envelope Olá funciona em Olá seguinte forma:  

1. biblioteca de clientes do storage do Azure Olá gera uma chave de encriptação de conteúdo (CEK), que é uma chave simétrica one time utilização.  
2. Dados de utilizador são encriptados utilizando este CEK.   
3. Olá CEK, em seguida, da aplicação (encriptadas) utilizando a chave de encriptação de chaves Olá (de chaves KEK). Olá KEK é identificada por um identificador de chave e pode ser um par de chaves assimétricas ou uma chave simétrica e pode ser gerido localmente ou armazenado em cofres de chaves do Azure.  
   biblioteca de clientes de armazenamento Olá próprio tem nunca tooKEK de acesso. biblioteca de Olá invoca o algoritmo de chave de moldagem de Olá fornecida pelo Cofre de chaves. Os utilizadores possam escolher toouse fornecedores personalizados para a chave encapsulamento de aplicações/abertura se assim o desejar.  
4. Olá dados encriptados em seguida, são carregado toohello serviço de armazenamento do Azure. Olá chave encapsulada juntamente com alguns metadados de encriptação adicionais é armazenada como metadados (num blob) ou interpolated com dados Olá encriptado (fila de mensagens e as entidades da tabela).

### <a name="decryption-via-hello-envelope-technique"></a>Desencriptação através de técnica de envelope Olá
Desencriptação através de técnica de envelope Olá funciona em Olá seguinte forma:  

1. biblioteca de clientes Olá parte do princípio de que o utilizador Olá está a gerir chaves de encriptação de chaves Olá (de chaves KEK) localmente ou cofres de chaves do Azure. utilizador Olá não precisa de tooknow Olá chave específica que foi utilizado para encriptação. Em vez disso, uma resolução de chave que é resolvido tookeys de identificadores de chave diferentes pode ser configurada e utilizada.  
2. biblioteca de clientes Olá transfere os dados de Olá encriptada, juntamente com quaisquer material de encriptação que é armazenado no serviço de Olá.  
3. a chave de encriptação de conteúdo encapsulada Olá (CEK) é, em seguida, utilizar (desencriptados) e não encapsulada Olá a chave de encriptação de chaves (KEK). Aqui, biblioteca de clientes Olá não tem acesso tooKEK. Basta invoca Olá personalizado ou o algoritmo de abertura do fornecedor do Cofre de chaves.  
4. Olá conteúdo de chave de encriptação (CEK) é, em seguida, utilizar dados de utilizador do toodecrypt Olá encriptado.

## <a name="encryption-mechanism"></a>Mecanismo de encriptação
biblioteca de clientes do storage Olá utiliza [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) nos dados de utilizador de tooencrypt de ordem. Especificamente, [encadeamento de bloco de cifras (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) modo com AES. Cada serviço funciona de forma ligeiramente diferente, pelo que, vamos abordar cada um deles aqui.

### <a name="blobs"></a>Blobs
biblioteca de clientes de Olá atualmente suporta encriptação de todo blobs apenas. Especificamente, a encriptação é suportada quando os utilizadores utilizam Olá **carregar*** métodos ou Olá **openOutputStream** método. Para as transferências, ambos completos e transferências de intervalo são suportadas.  

Durante a encriptação, a biblioteca de clientes do Olá irá gerar um Vetor de inicialização aleatório (IV) de 16 bytes, juntamente com uma chave de encriptação de conteúdo aleatório (CEK) de 32 bytes e efetuar a encriptação de envelope dos dados de blob Olá utilizando estas informações. Olá encapsulada CEK e alguns metadados de encriptação adicionais, em seguida, são armazenadas como metadados, juntamente com o blob encriptado do Olá no serviço de Olá do blob.

> [!WARNING]
> Se estiver a editar ou carregar os suas próprias metadados de blob Olá, terá de tooensure que estes metadados são preservados. Se carregar novos metadados sem estes metadados, Olá CEK encapsulada, IV e outros metadados serão perdidos e conteúdo do blob Olá nunca será recuperável novamente.
> 
> 

Transferência de um blob encriptado envolve a obter Olá conteúdo de blob todo Olá utilizando Olá  **transferir*/openInputStream** métodos conveniência. Olá CEK encapsulada está e não encapsulada e utilizado em conjunto com Olá IV (armazenadas como metadados do blob neste caso) tooreturn Olá desencriptada dados toohello utilizadores.

Transferência de um intervalo de arbitrário (**downloadRange*** métodos) Olá blob encriptado envolve ajustar o intervalo de Olá fornecida por utilizadores na ordem tooget uma pequena quantidade de dados adicionais que podem ser utilizado toosuccessfully desencriptar Olá intervalo pedido.  

Todos os tipos de BLOBs (blobs de blocos, blobs de páginas e blobs de acréscimo) podem ser encriptados/desencriptados utilizando este esquema.

### <a name="queues"></a>Filas
Uma vez que a fila de mensagens pode ser de qualquer formato, a biblioteca de clientes Olá define um formato personalizado que inclua Olá Vetor de inicialização (IV) e a chave de encriptação de conteúdo encriptado Olá (CEK) no texto da mensagem Olá.  

Durante a encriptação, a biblioteca de clientes Olá gera um IV aleatória de 16 bytes juntamente com um CEK aleatória de bytes de 32 e efetua a encriptação do envelope de texto da mensagem de fila de Olá utilizando estas informações. Olá encapsulada CEK e alguns metadados de encriptação adicionais, em seguida, são adicionados a mensagem de fila encriptados toohello. Esta mensagem modificada (mostrada abaixo) é armazenada no serviço de Olá.

```
<MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>
```

Durante a desencriptação, chave encapsulada Olá é extraído da mensagem da fila de saudação e não encapsulada. Olá IV também é extraído da mensagem da fila de saudação e utilizado juntamente com dados de mensagens de fila de Olá toodecrypt chave Olá e não encapsulada. Tenha em atenção de que esses metadados de encriptação Olá são pequeno (em 500 bytes), pelo que enquanto-contam para limite de 64KB Olá para uma mensagem de fila, impacto Olá deve ser fácil de gerir.

### <a name="tables"></a>Tabelas
Olá cliente biblioteca suporta encriptação de propriedades de entidade para inserção e substitua operações.

> [!NOTE]
> Intercalação não é atualmente suportada. Uma vez que um subconjunto de propriedades poderá ter sido encriptado anteriormente com uma chave diferente, basta intercalação novas propriedades de Olá e atualizar os metadados de Olá resultará na perda de dados. A intercalação um requer efetuar serviço adicional chama entidade pré-existente de Olá tooread do serviço de Olá ou utilizar uma nova chave por propriedade, que não são adequadas por motivos de desempenho.
> 
> 

Encriptação de dados de tabela funciona da seguinte forma:  

1. Os utilizadores especificarem Olá propriedades toobe encriptado.  
2. biblioteca de cliente Olá gera um Vetor de inicialização aleatório (IV) de 16 bytes juntamente com uma chave de encriptação de conteúdo aleatório (CEK) de bytes de 32 para cada entidade e efetua a encriptação de envelope no Olá propriedades individuais toobe encriptado ao efetuar a derivação de uma nova IV por propriedade. propriedade de Olá encriptado é armazenada como dados binários.  
3. Olá encapsulada CEK e alguns metadados de encriptação adicionais, em seguida, são armazenadas como duas propriedades reservadas adicionais. propriedade reservado primeiro Olá (_ClientEncryptionMetadata1) é uma propriedade de cadeia que contém informações de Olá sobre IV, versão e chave encapsulada. propriedade reservado segundo Olá (_ClientEncryptionMetadata2) é uma propriedade binária que contém informações de Olá sobre as propriedades de Olá que são encriptados. informações de Olá nesta segunda propriedade (_ClientEncryptionMetadata2) são próprio encriptados.  
4. Devido a toothese reservado propriedades adicionais necessárias para a encriptação, os utilizadores agora podem ter apenas 250 propriedades personalizadas em vez de 252. tamanho total do Olá da entidade de Olá tem de ser inferior a 1MB.  
   
   Tenha em atenção que as propriedades de cadeia só podem ser encriptadas. Se outros tipos de propriedades são toobe encriptado, tem de ser convertida toostrings. cadeias de Olá encriptado são armazenadas no serviço de Olá como propriedades binárias e estes são convertidos toostrings anterior depois de desencriptação.
   
   Para as tabelas, além disso toohello política de encriptação, os utilizadores tem de especificar Olá propriedades toobe encriptado. Pode fazê-lo especificando a um atributo [encriptar] (para entidades POCO que derivem de TableEntity) ou um resolvedor de encriptação nas opções de pedido. Um resolvedor de encriptação é um delegado que utiliza uma chave de partição, chave de linha e nome de propriedade e devolve um valor boleano que indica se essa propriedade deve ser encriptada. Durante a encriptação, a biblioteca de clientes do Olá irá utilizar este toodecide informações se uma propriedade deve ser encriptada durante a escrita toohello durante a transmissão. Também fornece delegado Olá para a possibilidade de Olá da lógica em torno da forma como as propriedades são encriptadas. (Por exemplo, se X, então encriptar propriedade um; caso contrário, encriptar propriedades A e B.) Tenha em atenção que é necessário não tooprovide estas informações ao ler ou consultar entidades.

### <a name="batch-operations"></a>Operações de lote
Em operações de lote, hello KEK mesmo irá ser utilizada em todas as linhas Olá essa operação em lote porque a biblioteca de clientes Olá só permite um objeto de opções (e, por conseguinte, uma política/KEK) por operação em lote. No entanto, biblioteca de clientes Olá internamente gerará uma nova IV aleatória e CEK aleatório por linha no lote de Olá. Os utilizadores também podem optar tooencrypt propriedades diferentes para cada operação no lote de Olá, definindo este comportamento na resolução de encriptação de Olá.

### <a name="queries"></a>Consultas
operações de consulta tooperform, tem de especificar uma resolução de chave que é capaz de tooresolve Olá todas as chaves no conjunto de resultados de Olá. Se uma entidade contida no resultado da consulta Olá não puder ser resolvido tooa fornecedor, a biblioteca de clientes Olá irá gerar um erro. Para qualquer consulta que efetua projeções de lado do servidor, a biblioteca de clientes do Olá irá adicionar propriedades de metadados de encriptação do especial Olá (_ClientEncryptionMetadata1 e _ClientEncryptionMetadata2) por colunas de toohello selecionado predefinido.

## <a name="azure-key-vault"></a>Azure Key Vault
O Cofre de Chaves do Azure ajuda a salvaguardar as chaves criptográficas e os segredos utilizados pelas aplicações em cloud e pelos serviços. Ao utilizar o Cofre de chaves do Azure, os utilizadores podem encriptar chaves e segredos (tal como chaves de autenticação, chaves de conta de armazenamento, chaves de encriptação de dados. Ficheiros PFX e palavras-passe) utilizando as teclas que estão protegidas por módulos de segurança de hardware (HSMs). Para obter mais informações, consulte [que é o Cofre de chaves do Azure?](../../key-vault/key-vault-whatis.md).

biblioteca de clientes do storage Olá utiliza biblioteca de principal do Cofre de chaves Olá na ordem tooprovide uma estrutura comum através do Azure para a gestão de chaves. Os utilizadores obtêm também benefício adicional de Olá de utilizar a biblioteca de extensões do Cofre de chaves Olá. biblioteca de extensões de Olá fornece uma funcionalidade útil em torno simple e totalmente integrada Symmetric/RSA local e os fornecedores de chave de nuvem, bem como com agregação e a colocação em cache.

### <a name="interface-and-dependencies"></a>Interface e dependências
Existem três pacotes do Cofre de chaves:  

* Azure-keyvault-core contém Olá IKey e IKeyResolver. É um pacote pequeno sem dependências. biblioteca de clientes do storage Olá para Java define-o como uma dependência.
* Azure keyvault contém cliente de REST do Cofre de chave de Olá.  
* extensões de keyvault Azure contém um código de extensão que inclui as implementações de algoritmos criptográficos e um RSAKey e um SymmetricKey. É também depende Olá espaços de nomes de núcleo e de KeyVault e fornece funcionalidade toodefine um resolvedor de agregação (quando os utilizadores querem toouse vários fornecedores de chaves) e uma resolução de chave de colocação em cache. Embora a biblioteca de clientes do storage Olá não diretamente dependem deste pacote, se os utilizadores desejar toouse Cofre de chaves do Azure toostore as respetivas chaves ou Olá do toouse Olá Cofre de chaves extensões tooconsume local e na nuvem fornecedores de criptografia, terá este pacote.  
  
  O Cofre de chaves foi concebido para chaves mestras de alto valor e limitação limites por Cofre de chaves são concebidos com isto em mente. Quando efetuar a encriptação do lado do cliente com o Cofre de chaves, o modelo preferencial Olá é toouse simétrica mestre as chaves armazenadas como segredos no Cofre de chaves e colocadas em cache localmente. Os utilizadores devem efetuar seguinte Olá:  

1. Criar um segredo offline e carregá-la tooKey cofre.  
2. Utilize o identificador de base do segredo Olá como um parâmetro tooresolve Olá versão atual do segredo Olá para a encriptação e em cache localmente estas informações. Utilizar CachingKeyResolver para colocar em cache; os utilizadores é tooimplement não esperado as seus próprios de colocação em cache lógica.  
3. Utilize o Resolvedor de colocação em cache Olá como uma entrada ao criar a política de encriptação de Olá.
   Podem encontrar mais informações sobre a utilização do Cofre de chaves nos exemplos de código Olá encriptação. <fix URL>  

## <a name="best-practices"></a>Melhores práticas
Suporte de encriptação está disponível apenas na biblioteca de clientes de armazenamento de Olá para Java.

> [!IMPORTANT]
> Tenha em atenção estes pontos importantes quando utilizar a encriptação do lado do cliente:
> 
> * Quando tooan ao ler a partir de ou escrever encriptados blob, utilizar comandos de carregamento de blob todo e comandos de transferência de blob de intervalo/inteiro. Evitar a escrita de BLOBs encriptados tooan utilizando o protocolo operações como colocar bloco, colocar a lista de bloqueios, escrever páginas, desmarque páginas ou acrescentar bloco; caso contrário poderá danificar blob encriptado Olá e torná-lo ilegível.
> * Para as tabelas, existe uma restrição semelhante. Ser toonot cuidado atualização encriptada propriedades sem atualizar os metadados de encriptação de Olá.  
> * Se definir os metadados no blob encriptado Olá, poderá substituir metadados relacionados com a encriptação de Olá necessários para a desencriptação, uma vez que a definição de metadados não é semiaditivas. Isto também se aplica aos instantâneos; Evite especificar metadados durante a criação de um instantâneo de um blob encriptado. Se os metadados tem de ser definido, ser se toocall Olá **downloadAttributes** tooget primeiro método Olá atual metadados de encriptação e evitar escritas em simultâneo, enquanto estiver a ser definido metadados.  
> * Ativar Olá **requireEncryption** sinalizador nas opções de pedido predefinido Olá para utilizadores que deverão funcionar apenas com os dados encriptados. Consulte abaixo para obter mais informações.  
> 
> 

## <a name="client-api--interface"></a>Cliente API / da Interface
Ao criar um objeto de EncryptionPolicy, os utilizadores podem fornecer apenas uma chave (implementar IKey), apenas uma resolução (implementar IKeyResolver) ou ambos. IKey é Olá básico tipo de chave que é identificado com um identificador de chave e que fornece lógica Olá de encapsulamento de aplicações/abertura. IKeyResolver é tooresolve utilizado uma chave durante o processo de desencriptação de Olá. Define um método de ResolveKey que devolva uma IKey fornecido um identificador de chave. Isto proporciona aos utilizadores Olá capacidade toochoose entre várias chaves que são geridos em várias localizações.

* Para a encriptação, chave Olá é sempre utilizado e ausência de Olá de uma chave resultará num erro.  
* Para desencriptação:  
  
  * resolução de chave Olá é invocada se chave de Olá tooget não especificado. Se a resolução de Olá for especificada, mas não tem um mapeamento para o identificador da chave Olá, será emitido um erro.  
  * Se o resolvedor não for especificado, mas foi especificada uma chave, a chave de Olá é utilizada se o respetivo identificador corresponde ao identificador da chave Olá necessário. Se não corresponde ao identificador de Olá, é emitido um erro.  
    
    Olá [amostras de encriptação](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples) <fix URL>demonstrar um cenário de ponto a ponto mais detalhado para blobs, filas e tabelas, along com a integração do Cofre de chaves.

### <a name="requireencryption-mode"></a>Modo de RequireEncryption
Os utilizadores, opcionalmente, podem ativar um modo de funcionamento em que todos os carregamentos e transferências tem de estar encriptadas. Neste modo, as tentativas tooupload dados sem um encriptação política ou a transferência de dados que não é encriptado no serviço de Olá irão falhar num cliente Olá. Olá **requireEncryption** sinalizador do objeto de opções de pedido de Olá controla este comportamento. Se a aplicação será encriptar todos os objetos armazenados no Storage do Azure, em seguida, pode definir Olá **requireEncryption** propriedade nas opções de pedido Olá predefinido para o objeto de cliente do serviço Olá.   

Por exemplo, utilizar **CloudBlobClient.getDefaultRequestOptions().setRequireEncryption(true)** toorequire encriptação para todas as operações de blob realizado através desse objeto de cliente.

### <a name="blob-service-encryption"></a>Encriptação do serviço blob
Criar um **BlobEncryptionPolicy** objeto e defina-o nas opções de pedido de Olá (por API ou a um nível de cliente utilizando **DefaultRequestOptions**). Tudo o resto será processado pela biblioteca de cliente Olá internamente.

```java
// Create hello IKey used for encryption.
RsaKey key = new RsaKey("private:key1" /* key identifier */);

// Create hello encryption policy toobe used for upload and download.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(key, null);

// Set hello encryption policy on hello request options.
BlobRequestOptions options = new BlobRequestOptions();
options.setEncryptionPolicy(policy);

// Upload hello encrypted contents toohello blob.
blob.upload(stream, size, null, options, null);

// Download and decrypt hello encrypted contents from hello blob.
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
blob.download(outputStream, null, options, null);
```

### <a name="queue-service-encryption"></a>Encriptação do serviço fila
Criar um **QueueEncryptionPolicy** objeto e defina-o nas opções de pedido de Olá (por API ou a um nível de cliente utilizando **DefaultRequestOptions**). Tudo o resto será processado pela biblioteca de cliente Olá internamente.

```java
// Create hello IKey used for encryption.
RsaKey key = new RsaKey("private:key1" /* key identifier */);

// Create hello encryption policy toobe used for upload and download.
QueueEncryptionPolicy policy = new QueueEncryptionPolicy(key, null);

// Add message
QueueRequestOptions options = new QueueRequestOptions();
options.setEncryptionPolicy(policy);

queue.addMessage(message, 0, 0, options, null);

// Retrieve message
CloudQueueMessage retrMessage = queue.retrieveMessage(30, options, null);
```

### <a name="table-service-encryption"></a>Encriptação do serviço tabela
Além disso toocreating uma política de encriptação e defini-la nas opções de pedido, deve especificar um **EncryptionResolver** no **TableRequestOptions**, ou defina o atributo de Olá [encriptar] no Olá entidade getter e setter.

### <a name="using-hello-resolver"></a>Utilizar o Resolvedor de Olá

```java
// Create hello IKey used for encryption.
RsaKey key = new RsaKey("private:key1" /* key identifier */);

// Create hello encryption policy toobe used for upload and download.
TableEncryptionPolicy policy = new TableEncryptionPolicy(key, null);

TableRequestOptions options = new TableRequestOptions()
options.setEncryptionPolicy(policy);
options.setEncryptionResolver(new EncryptionResolver() {
    public boolean encryptionResolver(String pk, String rk, String key) {
        if (key == "foo")
        {
            return true;
        }
        return false;
    }
});

// Insert Entity
currentTable.execute(TableOperation.insert(ent), options, null);

// Retrieve Entity
// No need toospecify an encryption resolver for retrieve
TableRequestOptions retrieveOptions = new TableRequestOptions()
retrieveOptions.setEncryptionPolicy(policy);

TableOperation operation = TableOperation.retrieve(ent.PartitionKey, ent.RowKey, DynamicTableEntity.class);
TableResult result = currentTable.execute(operation, retrieveOptions, null);
```

### <a name="using-attributes"></a>Utilizar atributos
Tal como mencionado acima, se a entidade de Olá implementa TableEntity, em seguida, Olá getter de propriedades e setter pode ser decorado com atributos de Olá [encriptar] em vez de especificar Olá **EncryptionResolver**.

```java
private string encryptedProperty1;

@Encrypt
public String getEncryptedProperty1 () {
    return this.encryptedProperty1;
}

@Encrypt
public void setEncryptedProperty1(final String encryptedProperty1) {
    this.encryptedProperty1 = encryptedProperty1;
}
```

## <a name="encryption-and-performance"></a>Encriptação e de desempenho
Tenha em atenção que encriptar os resultados de dados de armazenamento em overhead de desempenho adicionais. Olá conteúdo IV e a chave tem de ser gerado, tem de estar encriptado próprio conteúdo de Olá e adicional meta-data tem de ser formatado e carregado. Esta sobrecarga irá variar dependendo da quantidade de Olá de dados que está a ser encriptados. Recomendamos que os clientes sempre testar as aplicações de desempenho durante o desenvolvimento.

## <a name="next-steps"></a>Passos seguintes
* Transferir Olá [biblioteca de clientes do Storage do Azure para o pacote Maven de Java](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage)  
* Transferir Olá [biblioteca de clientes do Storage do Azure para Java o código de origem a partir do GitHub](https://github.com/Azure/azure-storage-java)   
* Transferir Olá biblioteca do Azure chave de cofre Maven para pacotes de Java Maven:
  * [Core](http://mvnrepository.com/artifact/com.microsoft.azure/azure-keyvault-core) pacote
  * [Cliente](http://mvnrepository.com/artifact/com.microsoft.azure/azure-keyvault) pacote
* Visite Olá [documentação de Cofre de chaves do Azure](../../key-vault/key-vault-whatis.md)
