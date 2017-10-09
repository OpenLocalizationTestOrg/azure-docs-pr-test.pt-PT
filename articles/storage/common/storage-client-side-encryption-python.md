---
title: "Encriptação do lado do aaaClient com o Python para o armazenamento do Microsoft Azure | Microsoft Docs"
description: "Olá biblioteca de clientes do Storage do Azure para Python suporta a encriptação do lado do cliente para segurança máxima para as suas aplicações de armazenamento do Azure."
services: storage
documentationcenter: python
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: f9bf7981-9948-4f83-8931-b15679a09b8a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/11/2017
ms.author: lakasa
ms.openlocfilehash: 3a52b64f93daf85a55308f8a4bee9c98b2315d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-with-python-for-microsoft-azure-storage"></a>Encriptação do lado do cliente com o Python de armazenamento do Microsoft Azure
[!INCLUDE [storage-selector-client-side-encryption-include](../../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>Descrição geral
Olá [biblioteca de clientes do Storage do Azure para Python](https://pypi.python.org/pypi/azure-storage) suporta a encriptação de dados dentro de aplicações de cliente antes de carregar tooAzure armazenamento e a desencriptação de dados ao transferir toohello cliente.

> [!NOTE]
> biblioteca de Python de armazenamento do Azure Olá está em pré-visualização.
> 
> 

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>Encriptação e desencriptação através de técnica de envelope Olá
os processos de Olá de encriptação e desencriptação siga técnica de envelope Olá.

### <a name="encryption-via-hello-envelope-technique"></a>Encriptação através de técnica de envelope Olá
Encriptação através de técnica de envelope Olá funciona em Olá seguinte forma:

1. biblioteca de clientes do storage do Azure Olá gera uma chave de encriptação de conteúdo (CEK), que é uma chave simétrica one time utilização.
2. Dados de utilizador são encriptados utilizando este CEK.
3. Olá CEK, em seguida, da aplicação (encriptadas) utilizando a chave de encriptação de chaves Olá (de chaves KEK). Olá KEK é identificada por um identificador de chave e pode ser um par de chaves assimétricas ou uma chave simétrica, que é gerida localmente.
   biblioteca de clientes de armazenamento Olá próprio tem nunca tooKEK de acesso. biblioteca de Olá invoca chave Olá algoritmo que é fornecido pela Olá KEK de encapsulamento de aplicações. Os utilizadores possam escolher toouse fornecedores personalizados para a chave encapsulamento de aplicações/abertura se assim o desejar.
4. Olá dados encriptados em seguida, são carregado toohello serviço de armazenamento do Azure. Olá chave encapsulada juntamente com alguns metadados de encriptação adicionais é armazenada como metadados (num blob) ou interpolated com dados Olá encriptado (fila de mensagens e as entidades da tabela).

### <a name="decryption-via-hello-envelope-technique"></a>Desencriptação através de técnica de envelope Olá
Desencriptação através de técnica de envelope Olá funciona em Olá seguinte forma:

1. biblioteca de clientes Olá parte do princípio de que o utilizador Olá está a gerir chaves de encriptação de chaves Olá (de chaves KEK) localmente. utilizador Olá não precisa de tooknow Olá chave específica que foi utilizado para encriptação. Em vez disso, uma resolução de chave, o qual resolve tookeys de identificadores de chave diferentes, pode configurar e utilizar.
2. biblioteca de clientes Olá transfere os dados de Olá encriptada, juntamente com quaisquer material de encriptação que é armazenado no serviço de Olá.
3. a chave de encriptação de conteúdo encapsulada Olá (CEK) é, em seguida, utilizar (desencriptados) e não encapsulada Olá a chave de encriptação de chaves (KEK). Aqui, biblioteca de clientes Olá não tem acesso tooKEK. Basta invoca algoritmo de abertura do fornecedor Olá personalizado.
4. Olá conteúdo de chave de encriptação (CEK) é, em seguida, utilizar dados de utilizador do toodecrypt Olá encriptado.

## <a name="encryption-mechanism"></a>Mecanismo de encriptação
biblioteca de clientes do storage Olá utiliza [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) nos dados de utilizador de tooencrypt de ordem. Especificamente, [encadeamento de bloco de cifras (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) modo com AES. Cada serviço funciona de forma ligeiramente diferente, pelo que, vamos abordar cada um deles aqui.

### <a name="blobs"></a>Blobs
biblioteca de clientes de Olá atualmente suporta encriptação de todo blobs apenas. Especificamente, a encriptação é suportada quando os utilizadores utilizam Olá **criar*** métodos. Para as transferências, ambos completos e transferências de intervalo são suportadas e parallelization de carregamento e transferência está disponível.

Durante a encriptação, a biblioteca de clientes do Olá irá gerar um Vetor de inicialização aleatório (IV) de 16 bytes, juntamente com uma chave de encriptação de conteúdo aleatório (CEK) de 32 bytes e efetuar a encriptação de envelope dos dados de blob Olá utilizando estas informações. Olá encapsulada CEK e alguns metadados de encriptação adicionais, em seguida, são armazenadas como metadados, juntamente com o blob encriptado do Olá no serviço de Olá do blob.

> [!WARNING]
> Se estiver a editar ou carregar os suas próprias metadados de blob Olá, terá de tooensure que estes metadados são preservados. Se carregar novos metadados sem estes metadados, Olá CEK encapsulada, IV e outros metadados serão perdidos e conteúdo do blob Olá nunca será recuperável novamente.
> 
> 

Transferência de um blob encriptado envolve a obter Olá conteúdo de blob todo Olá utilizando Olá **obter*** métodos conveniência. Olá CEK encapsulada está e não encapsulada e utilizado em conjunto com Olá IV (armazenadas como metadados do blob neste caso) tooreturn Olá desencriptada dados toohello utilizadores.

Transferir um intervalo de arbitrário (**obter*** transmitido métodos com parâmetros de intervalo) Olá blob encriptado envolve ajustar o intervalo de Olá fornecido por utilizadores na ordem tooget uma pequena quantidade de dados adicionais que podem ser utilizados toosuccessfully desencriptar Olá solicitou intervalo.

Os blobs de blocos e blobs de páginas só podem ser encriptados/desencriptar a utilização deste esquema. Não são atualmente suportadas para encriptação de blobs de acréscimo.

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
3. Olá encapsulada CEK e alguns metadados de encriptação adicionais, em seguida, são armazenadas como duas propriedades reservadas adicionais. Olá reservado primeiro a propriedade (\_ClientEncryptionMetadata1) é uma propriedade de cadeia que contém informações de Olá sobre IV, versão e chave encapsulada. Olá propriedade segundo reservada (\_ClientEncryptionMetadata2) é uma propriedade binária que contém informações de Olá sobre as propriedades de Olá que são encriptados. Olá informações nesta segunda propriedade (\_ClientEncryptionMetadata2) é o próprio encriptados.
4. Devido a toothese reservado propriedades adicionais necessárias para a encriptação, os utilizadores agora podem ter apenas 250 propriedades personalizadas em vez de 252. tamanho total do Olá da entidade de Olá tem de ser inferior a 1MB.
   
   Tenha em atenção que as propriedades de cadeia só podem ser encriptadas. Se outros tipos de propriedades são toobe encriptado, tem de ser convertida toostrings. cadeias de Olá encriptado são armazenadas no serviço de Olá como propriedades binárias e estes são convertidos toostrings back (cadeias não processadas, não EntityProperties com tipo EdmType.STRING) depois de desencriptação.
   
   Para as tabelas, além disso toohello política de encriptação, os utilizadores tem de especificar Olá propriedades toobe encriptado. Isto pode ser feito armazenando o estas propriedades em objetos de TableEntity com Olá tipo conjunto tooEdmType.STRING e encriptar encryption_resolver_function de Olá de definição ou tootrue definido no objeto de tableservice Olá. Um resolvedor de encriptação é uma função que utiliza uma chave de partição, chave de linha e nome de propriedade e devolve um valor boleano que indica se essa propriedade deve ser encriptada. Durante a encriptação, a biblioteca de clientes do Olá irá utilizar este toodecide informações se uma propriedade deve ser encriptada durante a escrita toohello durante a transmissão. Também fornece delegado Olá para a possibilidade de Olá da lógica em torno da forma como as propriedades são encriptadas. (Por exemplo, se X, então encriptar propriedade um; caso contrário, encriptar propriedades A e B.) Tenha em atenção que é necessário não tooprovide estas informações ao ler ou consultar entidades.

### <a name="batch-operations"></a>Operações de lote
Uma política de encriptação aplica-se tooall linhas do lote de Olá. biblioteca de clientes Olá internamente irá gerar um novo IV aleatória e CEK aleatório por linha num batch Olá. Os utilizadores também podem optar tooencrypt propriedades diferentes para cada operação no lote de Olá, definindo este comportamento na resolução de encriptação de Olá.
Se um lote é criado como um Gestor de contexto através do método de batch() Olá tableservice, política de encriptação do Olá tableservice será automaticamente aplicados toohello batch. Se um lote for criado explicitamente ao chamar o construtor de Olá, política de encriptação de Olá têm de ser transmitida como um parâmetro e à esquerda, não modificada para duração Olá do batch Olá.
Tenha em atenção que as entidades são encriptadas conforme estes forem inseridos em batch Olá através da política de encriptação do batch Olá (entidades não são encriptadas na hora de Olá de consolidar o lote de Olá através da política de encriptação do Olá tableservice).

### <a name="queries"></a>Consultas
operações de consulta tooperform, tem de especificar uma resolução de chave que é capaz de tooresolve Olá todas as chaves no conjunto de resultados de Olá. Se uma entidade contida no resultado da consulta Olá não puder ser resolvido tooa fornecedor, a biblioteca de clientes Olá irá gerar um erro. Para qualquer consulta que efetua projeções de lado do servidor, a biblioteca de clientes do Olá irá adicionar propriedades de metadados de encriptação do especial Olá (\_ClientEncryptionMetadata1 e \_ClientEncryptionMetadata2) por predefinição toohello selecionada colunas .

> [!IMPORTANT]
> Tenha em atenção estes pontos importantes quando utilizar a encriptação do lado do cliente:
> 
> * Quando tooan ao ler a partir de ou escrever encriptados blob, utilizar comandos de carregamento de blob todo e comandos de transferência de blob de intervalo/inteiro. Evitar a escrita de BLOBs encriptados tooan com operações de protocolo, tais como colocar bloco, colocar a lista de bloqueios, escrever páginas ou desmarque páginas; caso contrário poderá danificar blob encriptado Olá e torná-lo ilegível.
> * Para as tabelas, existe uma restrição semelhante. Ser toonot cuidado atualização encriptada propriedades sem atualizar os metadados de encriptação de Olá.
> * Se definir os metadados no blob encriptado Olá, poderá substituir metadados relacionados com a encriptação de Olá necessários para a desencriptação, uma vez que a definição de metadados não é semiaditivas. Isto também se aplica aos instantâneos; Evite especificar metadados durante a criação de um instantâneo de um blob encriptado. Se os metadados tem de ser definido, ser se toocall Olá **get_blob_metadata** tooget primeiro método Olá atual metadados de encriptação e evitar escritas em simultâneo, enquanto estiver a ser definido metadados.
> * Ativar Olá **require_encryption** sinalizador no objeto de serviço Olá para utilizadores que deverão funcionar apenas com os dados encriptados. Consulte abaixo para obter mais informações.
> 
> 

biblioteca de clientes do storage Olá espera Olá fornecido KEK e resolução de chave Olá tooimplement seguir interface. [O Cofre de chaves do Azure](https://azure.microsoft.com/services/key-vault/) suporte para a gestão de Python KEK está pendente e irá ser integrada nesta biblioteca quando tiver terminado.

## <a name="client-api--interface"></a>Cliente API / da Interface
Depois de ter sido criado um objeto de serviço de armazenamento (ou seja, blockblobservice), o utilizador Olá poderá atribuir valores de campos de toohello que constituem uma política de encriptação: key_encryption_key, key_resolver_function e require_encryption. Os utilizadores podem fornecer apenas KEK, apenas uma resolução, ou ambos. key_encryption_key é Olá básico tipo de chave que é identificado com um identificador de chave e que fornece lógica Olá de encapsulamento de aplicações/abertura. key_resolver_function é tooresolve utilizado uma chave durante o processo de desencriptação de Olá. Devolve um KEK válido fornecido um identificador de chave. Isto proporciona aos utilizadores Olá capacidade toochoose entre várias chaves que são geridos em várias localizações.

Olá KEK tem de implementar seguinte Olá métodos toosuccessfully encriptar dados:

* wrap_key(cek): Olá encapsula num wrapper especificado utilizando um algoritmo da preferência do utilizador Olá CEK (bytes). Olá devolve chave moldada.
* get_key_wrap_algorithm(): algoritmo de Olá devolve utilizado toowrap chaves.
* get_kid(): devolve Olá cadeia id de chave para este KEK.
  Olá KEK tem de implementar Olá os seguintes dados de desencriptação de toosuccessfully métodos:
* unwrap_key (cek, algoritmo): devolve Olá e não encapsulada formato Olá especificado CEK utilizando Olá especificada de cadeia algoritmo.
* get_kid(): devolve um id de chave de cadeia para este KEK.

resolução de chave Olá tem de implementar, pelo menos, um método que, recebe um id de chave, devolve Olá correspondente KEK implementar Olá interface acima. Apenas este método é toobe atribuído toohello key_resolver_function propriedade no objecto de serviço Olá.

* Para a encriptação, chave Olá é sempre utilizado e ausência de Olá de uma chave resultará num erro.
* Para desencriptação:
  
  * resolução de chave Olá é invocada se chave de Olá tooget não especificado. Se a resolução de Olá for especificada, mas não tem um mapeamento para o identificador da chave Olá, será emitido um erro.
  * Se o resolvedor não for especificado, mas foi especificada uma chave, a chave de Olá é utilizada se o respetivo identificador corresponde ao identificador da chave Olá necessário. Se não corresponde ao identificador de Olá, é emitido um erro.
    
    Olá amostras de encriptação no azure.storage.samples <fix URL>demonstrar um cenário de ponto a ponto mais detalhado para tabelas, filas e blobs.
      As implementações de exemplo de Olá KEK e resolução de chave são fornecidas nos ficheiros de exemplo de Olá como KeyWrapper e KeyResolver respetivamente.

### <a name="requireencryption-mode"></a>Modo de RequireEncryption
Os utilizadores, opcionalmente, podem ativar um modo de funcionamento em que todos os carregamentos e transferências tem de estar encriptadas. Neste modo, as tentativas tooupload dados sem um encriptação política ou a transferência de dados que não é encriptado no serviço de Olá irão falhar num cliente Olá. Olá **require_encryption** sinalizador em controlos de objeto do serviço de Olá este comportamento.

### <a name="blob-service-encryption"></a>Encriptação do serviço blob
Definir campos de política de encriptação de Olá Olá blockblobservice objeto. Tudo o resto será processado pela biblioteca de cliente Olá internamente.

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_block_blob_service.key_encryption_key = kek
my_block_blob_service.key_resolver_funcion = key_resolver.resolve_key

# Upload hello encrypted contents toohello blob.
my_block_blob_service.create_blob_from_stream(container_name, blob_name, stream)

# Download and decrypt hello encrypted contents from hello blob.
blob = my_block_blob_service.get_blob_to_bytes(container_name, blob_name)
```

### <a name="queue-service-encryption"></a>Encriptação do serviço fila
Definir campos de política de encriptação de Olá Olá queueservice objeto. Tudo o resto será processado pela biblioteca de cliente Olá internamente.

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_queue_service.key_encryption_key = kek
my_queue_service.key_resolver_funcion = key_resolver.resolve_key

# Add message
my_queue_service.put_message(queue_name, content)

# Retrieve message
retrieved_message_list = my_queue_service.get_messages(queue_name)
```

### <a name="table-service-encryption"></a>Encriptação do serviço tabela
Além disso toocreating uma política de encriptação e defini-la nas opções de pedido, deve especificar um **encryption_resolver_function** no Olá **tableservice**, ou Olá conjunto encriptar o atributo Olá EntityProperty.

### <a name="using-hello-resolver"></a>Utilizar o Resolvedor de Olá

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Define hello encryption resolver_function.
def my_encryption_resolver(pk, rk, property_name):
        if property_name == 'foo':
                return True
        return False

# Set hello KEK and key resolver on hello service object.
my_table_service.key_encryption_key = kek
my_table_service.key_resolver_funcion = key_resolver.resolve_key
my_table_service.encryption_resolver_function = my_encryption_resolver

# Insert Entity
my_table_service.insert_entity(table_name, entity)

# Retrieve Entity
# Note: No need toospecify an encryption resolver for retrieve, but it is harmless tooleave hello property set.
my_table_service.get_entity(table_name, entity['PartitionKey'], entity['RowKey'])
```

### <a name="using-attributes"></a>Utilizar atributos
Tal como mencionado acima, uma propriedade pode estar marcada para encriptação, armazenando-um objeto de EntityProperty e definição Olá encriptar campo.

```python
encrypted_property_1 = EntityProperty(EdmType.STRING, value, encrypt=True)
```

## <a name="encryption-and-performance"></a>Encriptação e de desempenho
Tenha em atenção que encriptar os resultados de dados de armazenamento em overhead de desempenho adicionais. Olá conteúdo IV e a chave tem de ser gerado, tem de estar encriptado próprio conteúdo de Olá e metadados adicionais têm de ser formatado e carregados. Esta sobrecarga irá variar dependendo da quantidade de Olá de dados que está a ser encriptados. Recomendamos que os clientes sempre testar as aplicações de desempenho durante o desenvolvimento.

## <a name="next-steps"></a>Passos seguintes
* Transferir Olá [biblioteca de clientes do Storage do Azure para Java PyPi pacote](https://pypi.python.org/pypi/azure-storage)
* Transferir Olá [biblioteca de clientes do Storage do Azure para Python o código de origem a partir do GitHub](https://github.com/Azure/azure-storage-python)
