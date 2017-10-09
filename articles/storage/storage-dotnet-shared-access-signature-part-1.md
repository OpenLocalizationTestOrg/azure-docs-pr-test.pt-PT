---
title: aaaUsing partilhado assinaturas de acesso (SAS) no Storage do Azure | Microsoft Docs
description: Saiba toouse partilhado acesso assinaturas (SAS) toodelegate acesso tooAzure recursos de armazenamento, incluindo ficheiros, tabelas, filas e blobs.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 46fd99d7-36b3-4283-81e3-f214b29f1152
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/18/2017
ms.author: marsma
ms.openlocfilehash: 53e06c78fbfdaa5fd209add719995ef2a6bc8f61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-shared-access-signatures-sas"></a>Utilizar assinaturas de acesso partilhado (SAS)

Uma assinatura de acesso partilhado (SAS) fornece-lhe um tooobjects de acesso de toogrant limitada de forma na sua conta de armazenamento tooother clientes, sem a chave de conta a exposição. Neste artigo, iremos fornecer uma descrição geral do modelo SAS Olá, rever as melhores práticas SAS e observe alguns exemplos.

Para obter exemplos de códigos adicionais através da SAS para além daquelas aqui apresentadas, consulte [introdução ao armazenamento de Blobs do Azure no .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) e outros exemplos disponíveis no Olá [exemplos de código do Azure](https://azure.microsoft.com/documentation/samples/?service=storage) biblioteca. Pode transferir aplicações de exemplo de Olá e executá-los ou procurar Olá código no GitHub.

## <a name="what-is-a-shared-access-signature"></a>O que é uma assinatura de acesso partilhado?
Uma assinatura de acesso partilhado fornece acesso delegado tooresources na sua conta de armazenamento. Com uma SAS, pode conceder a clientes aceder tooresources na sua conta de armazenamento sem partilha as chaves de conta. Este é Olá ponto chave da utilização de assinaturas de acesso partilhado nas suas aplicações – uma SAS é um tooshare de forma segura os recursos de armazenamento sem comprometer as chaves de conta.

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

Uma SAS dá-lhe um controlo granular sobre o tipo de Olá de acesso que conceda tooclients que tenham Olá SAS, incluindo:

* intervalo de Olá ao longo do que Olá SAS é válido, incluindo a hora de início de Olá e a hora de expiração de Olá.
* Olá, as permissões concedidas pelo Olá SAS. Por exemplo, uma SAS para um blob poderá conceder a leitura e escrita de BLOBs de toothat de permissões, mas não eliminar permissões.
* Opcional endereço IP ou intervalo de endereços IP dos quais o armazenamento do Azure irá aceitar Olá SAS. Por exemplo, poderá especificar um intervalo de endereços IP que pertençam tooyour organização.
* protocolo de Olá durante o qual o Storage do Azure irá aceitar Olá SAS. Pode utilizar este tooclients do parâmetro opcional toorestrict acesso através de HTTPS.

## <a name="when-should-you-use-a-shared-access-signature"></a>Quando deve utilizar uma assinatura de acesso partilhado?
Pode utilizar um SAS quando quiser tooprovide acesso tooresources no seu cliente de tooany de conta de armazenamento não possessing chaves de acesso da sua conta de armazenamento. A conta de armazenamento inclui tanto uma chave de acesso primária e secundária, que conceda a conta de tooyour acesso administrativo e todos os recursos dentro da mesma. A exposição de qualquer uma destas chaves abre-se a possibilidade de toohello de conta de utilização por acidente ou maliciosa. Assinaturas de acesso partilhado fornecem uma alternativa segura que permite aos clientes tooread, escrita e eliminação de dados na sua conta de armazenamento de acordo com as permissões de toohello que explicitamente já atribuídos e sem necessidade de uma chave de conta.

Um cenário comum, onde é útil uma SAS é um serviço em que os utilizadores ler e escrever a sua própria conta de armazenamento de tooyour de dados. Num cenário em que uma conta do storage armazena dados de utilizador, existem dois padrões de conceção comuns:

1. Os clientes carregar e transferir dados através de um serviço de proxy de front-end que efetua a autenticação. Este serviço de proxy de front-end tem a vantagem de Olá ao permitir que a validação de regras de negócio, mas para grandes quantidades de dados ou transações de volume elevado, criação de um serviço que pode ser dimensionados toomatch pedido pode ser difícil ou dispendiosa.

  ![Diagrama do cenário: serviço proxy de front-end][sas-storage-fe-proxy-service]

1. Um serviço simples autentica o cliente de Olá conforme necessário e, em seguida, gera uma SAS. Depois do cliente de Olá recebe Olá SAS, podem aceder a recursos da conta de armazenamento diretamente com permissões de Olá definidas por Olá SAS e para o intervalo de Olá permitido por Olá SAS. Olá SAS atenua a necessidade de Olá de encaminhamento de todos os dados através do serviço de front-end proxy Olá.

  ![Diagrama do cenário: serviço do fornecedor da SAS][sas-storage-provider-service]

Muitos serviços do mundo real podem utilizar uma versão híbrida destas duas abordagens. Por exemplo, alguns dados possam ser processados e validar através do proxy de front-end Olá, enquanto outros dados são guardados e/ou diretamente através da SAS de leitura.

Além disso, terá de toouse um objeto de origem do SAS tooauthenticate Olá numa operação de cópia em determinados cenários:

* Quando copiar um blob de tooanother do blob que reside numa conta do storage diferente, tem de utilizar um SAS tooauthenticate Olá origem blob. Opcionalmente, pode utilizar um SAS tooauthenticate Olá blob de destino, bem como.
* Quando copiar um ficheiro de tooanother de ficheiros que reside numa conta do storage diferente, tem de utilizar um ficheiro de origem do SAS tooauthenticate Olá. Opcionalmente, pode utilizar um SAS tooauthenticate Olá ficheiro de destino, bem como.
* Quando copiar um blob tooa ou um ficheiro tooa blob, tem de utilizar um objeto de origem do SAS tooauthenticate Olá, mesmo se os objetos de origem e destino Olá residem no Olá mesma conta de armazenamento.

## <a name="types-of-shared-access-signatures"></a>Tipos de assinaturas de acesso partilhado
Pode criar dois tipos de assinaturas de acesso partilhado:

* **Serviço SAS.** Os delegados SAS do serviço Olá aceder tooa recurso em apenas um dos serviços de armazenamento Olá: Olá serviço Blob, fila, tabela ou ficheiro. Consulte [construir um serviço SAS](https://msdn.microsoft.com/library/dn140255.aspx) e [exemplos de SAS do serviço](https://msdn.microsoft.com/library/dn140256.aspx) para obter informações aprofundadas sobre a construção de token do Olá serviço SAS.
* **Conta SAS.** Os delegados do Olá conta SAS aceder tooresources em uma ou mais dos serviços de armazenamento Olá. Todas as operações de Olá disponíveis através de um serviço SAS também estão disponíveis através de uma conta SAS. Além disso, com a conta de Olá SAS, pode delegar o acesso toooperations que se aplicam tooa fornecido o serviço, tal como **Get/defina as propriedades de serviço** e **obter estatísticas de serviço**. Também pode delegar o acesso tooread, escrita e operações de eliminação em contentores de BLOBs, tabelas, filas e partilhas de ficheiros que não são permitidas com um serviço SAS. Consulte [construir uma conta SAS](https://msdn.microsoft.com/library/mt584140.aspx) para obter informações aprofundadas sobre a construção de token do Olá conta SAS.

## <a name="how-a-shared-access-signature-works"></a>Como funciona uma assinatura de acesso partilhado
Uma assinatura de acesso partilhado é um URI assinado que aponta tooone ou mais recursos de armazenamento e inclui um token que contém um conjunto especial de parâmetros de consulta. token de Olá indica como os recursos de Olá poderão ser acedidos pelo cliente de Olá. Um dos parâmetros de consulta Olá, Olá assinatura, é construído a partir de parâmetros SAS Olá e assinado com a chave de conta Olá. Esta assinatura é utilizada pelo Olá tooauthenticate do Storage do Azure SAS.

Eis um exemplo de um URI de SAS, o URI do recurso que mostra Olá e o token SAS de Olá:

![Componentes de um URI de SAS][sas-storage-uri]

Olá SAS token é uma cadeia gerar no Olá *cliente* lado (consulte Olá [exemplos SAS](#sas-examples) secção para obter exemplos de código). Um token SAS que gerar com biblioteca de clientes de armazenamento Olá, por exemplo, não é controlado pelo armazenamento do Azure de qualquer forma. Pode criar um número ilimitado de tokens SAS do lado do cliente de Olá.

Quando um cliente fornece um tooAzure URI de SAS de armazenamento como parte de um pedido, o serviço de Olá verifica os parâmetros SAS Olá e tooverify de assinatura que é válido para autenticar o pedido de Olá. Se o serviço de Olá verifica que a assinatura Olá é válida, o pedido de Olá é autenticado. Caso contrário, é recusado um pedido Olá com o código de erro 403 (proibido).

## <a name="shared-access-signature-parameters"></a>Parâmetros de assinatura de acesso partilhado
conta de Olá SAS tokens SAS de serviço incluem alguns parâmetros comuns em também de ter alguns parâmetros que são diferentes.

### <a name="parameters-common-tooaccount-sas-and-service-sas-tokens"></a>Os parâmetros comuns tooaccount SAS e tokens SAS do serviço
* **Versão de API** um parâmetro opcional que especifica o pedido de Olá ao tooexecute do toouse de versão Olá armazenamento serviço.
* **Versão de Service** um parâmetro obrigatório que especifica o pedido de Olá ao tooauthenticate do toouse de versão Olá armazenamento serviço.
* **Hora de início.** Este é Olá hora em que Olá SAS passa a ser válido. hora de início de Olá para uma assinatura de acesso partilhado é opcional. Se uma hora de início for omitida, Olá SAS está em vigor imediatamente. Olá hora de início tem de ser expresso em UTC (Hora Universal Coordenada), com um designador de UTC especial ("Z"), por exemplo `1994-11-05T13:15:30Z`.
* **Hora de expiração.** Este é o tempo de Olá após o qual hello SAS já não é válido. Melhores práticas recomendado especifique uma hora de expiração para um SAS ou que associá-la a uma política de acesso armazenada. Olá hora de expiração tem de ser expresso em UTC (Hora Universal Coordenada), com um designador de UTC especial ("Z"), por exemplo `1994-11-05T13:15:30Z` (consulte mais abaixo).
* **Permissões.** permissões de Olá especificadas no Olá SAS indicam as operações de cliente de Olá pode executa relativamente aos recursos de armazenamento de Olá utilizando Olá SAS. Diferirem permissões disponíveis para uma conta SAS e um serviço SAS.
* **IP.** Um parâmetro opcional que especifica um endereço IP ou um intervalo de endereços IP fora do Azure (consulte a secção de Olá [estado de configuração de sessão de encaminhamento](../expressroute/expressroute-workflows.md#routing-session-configuration-state) para Express Route) dos quais os pedidos de tooaccept.
* **Protocolo.** Um parâmetro opcional que especifica o protocolo de Olá permitido para um pedido. Os valores possíveis são HTTPS e HTTP (`https,http`), que é apenas valor predefinido de Olá ou HTTPS (`https`). Tenha em atenção que HTTP só não é um valor permitido.
* **Assinatura.** assinatura de Olá construída a partir das Olá outros parâmetros especificados como parte de token e, em seguida, são encriptadas. Utilizou o tooauthenticate Olá SAS.

### <a name="parameters-for-a-service-sas-token"></a>Parâmetros para um token SAS de serviço
* **Recursos de armazenamento.** Recursos de armazenamento para o qual pode delegar o acesso com um serviço SAS incluem:
  * Contentores e blobs
  * Partilhas de ficheiros e ficheiros
  * Filas
  * As tabelas e os intervalos de entidades de tabela.

### <a name="parameters-for-an-account-sas-token"></a>Parâmetros para um token SAS de conta
* **Serviço ou serviços.** Uma conta SAS pode delegar acesso tooone ou mais dos serviços de armazenamento Olá. Por exemplo, pode criar uma conta SAS delegados toohello Blob e o ficheiro de serviço de acesso. Ou pode criar uma SAS que delegados tooall quatro dos serviços de acesso (Blob, fila, tabela e ficheiro).
* **Tipos de recursos de armazenamento.** Aplica-se uma conta SAS tooone ou mais classes de recursos de armazenamento, em vez de um recurso específico. Pode criar um conta SAS toodelegate acesso:
  * APIs de nível de serviço, que são chamadas contra o recurso de conta de armazenamento Olá. Os exemplos incluem **Get/defina as propriedades de serviço**, **obter estatísticas de serviço**, e **listar contentores/filas/tabelas/partilhas**.
  * APIs de ao nível do contentor, que são chamadas contra objetos de contentor Olá para cada serviço: blob contentores, filas, tabelas e partilhas de ficheiros. Os exemplos incluem **criar/eliminar contentor**, **criar/eliminar fila**, **criar/eliminar tabela**, **Criar/Eliminar partilha**e  **Listar os Blobs/os ficheiros e diretórios**.
  * APIs de ao nível do objeto, que são chamadas contra ficheiros, as entidades da tabela, fila de mensagens e blobs. Por exemplo, **colocar Blob**, **consulta entidade**, **obter mensagens**, e **criar ficheiro**.

## <a name="examples-of-sas-uris"></a>Exemplos de SAS URIs

### <a name="service-sas-uri-example"></a>Exemplo de URI de SAS do serviço

Eis um exemplo de um serviço URI de SAS que fornece de leitura e escrita de BLOBs de tooa de permissões. tabela de Olá divide cada parte Olá URI toounderstand como contribui-toohello SAS:

```
https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2015-04-05&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D
```

| Nome | Parte da SAS | Descrição |
| --- | --- | --- |
| URI de blob |`https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt` |endereço de Olá do blob Olá. Tenha em atenção que através de HTTPS é vivamente recomendável. |
| Versão de serviços de armazenamento |`sv=2015-04-05` |Para serviços de armazenamento versão 2012-02-12 e posterior, este parâmetro indica Olá versão toouse. |
| Hora de início |`st=2015-04-29T22%3A18%3A26Z` |Especificado na hora UTC. Se quiser Olá SAS toobe válido imediatamente, omita a hora de início Olá. |
| Hora de expiração |`se=2015-04-30T02%3A23%3A26Z` |Especificado na hora UTC. |
| Recurso |`sr=b` |recurso de Olá é um blob. |
| Permissões |`sp=rw` |permissões de Olá concedidas pelos Olá SAS incluem Read (r) e escrever (m). |
| Intervalo de IP |`sip=168.1.5.60-168.1.5.70` |Olá intervalo de endereços IP do que um pedido serão aceites. |
| Protocolo |`spr=https` |São permitidos apenas pedidos através de HTTPS. |
| Assinatura |`sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D` |Utilizar o blob de toohello tooauthenticate acesso. a assinatura de Olá é um HMAC calculada através de uma cadeia para assinar e a chave, utilizando o algoritmo SHA256 de Olá e, em seguida, codificado com codificação Base64. |

### <a name="account-sas-uri-example"></a>Exemplo de URI de SAS de conta

Eis um exemplo de uma conta SAS, que utiliza Olá parâmetros comuns do mesmos no token de Olá. Uma vez que estes parâmetros são descritos acima, estes não são descritas aqui. Apenas os parâmetros de Olá que são específica tooaccount que SAs é descrito na tabela de Olá abaixo.

```
https://myaccount.blob.core.windows.net/?restype=service&comp=properties&sv=2015-04-05&ss=bf&srt=s&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=F%6GRVAZ5Cdj2Pw4tgU7IlSTkWgn7bUkkAg8P6HESXwmf%4B
```

| Nome | Parte da SAS | Descrição |
| --- | --- | --- |
| URI do recurso |`https://myaccount.blob.core.windows.net/?restype=service&comp=properties` |Olá Blob ponto final de serviço, com parâmetros para obter as propriedades do serviço (quando chamado com GET) ou definir as propriedades do serviço (quando chamado com definido). |
| Serviços |`ss=bf` |aplica-se Olá SAS toohello Blob e serviços de ficheiros |
| Tipos de recursos |`srt=s` |Olá SAS aplica-se ao nível do tooservice operações. |
| Permissões |`sp=rw` |permissões de Olá conceder acesso tooread e operações de escrita. |

Uma vez que as permissões estão limitadas a nível de serviço toohello, acessíveis operações com esta SAS são **obter propriedades de serviço Blob** (leitura) e **definir propriedades de serviço Blob** (escrita). No entanto, com um URI de recursos diferente, hello mesmo token SAS também pode ser utilizados toodelegate acesso demasiado**obter estatísticas de serviço Blob** (leitura).

## <a name="controlling-a-sas-with-a-stored-access-policy"></a>Controlar um SAS com uma política de acesso armazenada
Uma assinatura de acesso partilhado pode efetuar uma das duas formas:

* **SAS ad hoc:** quando cria um SAS ad hoc, a hora de início de Olá, a hora de expiração e as permissões para Olá SAS estão especificadas na Olá URI de SAS (ou implícito, no caso de Olá em que a hora de início for omitida). Este tipo de SAS pode ser criado como uma conta SAS ou um serviço SAS.
* **SAS com a política de acesso armazenada:** uma política de acesso armazenada está definido no contentor de recursos – um contentor de blob, tabela, fila, ou partilha – o ficheiro e podem ser utilizados toomanage restrições para um ou mais assinaturas de acesso partilhado. Quando associa um SAS com uma política de acesso armazenada, Olá SAS herda as restrições de Olá – hora de início de Olá, hora de expiração e permissões – definidas para a política de acesso de Olá armazenado.

> [!NOTE]
> Atualmente, uma conta SAS tem de ser um SAS ad hoc. Armazenados acesso políticas não são suportadas ainda para a conta SAS.

Olá diferença entre formulários Olá dois é importante para um cenário de chave: revogação. Como um URI de SAS é um URL, qualquer pessoa que obtém Olá SAS pode utilizá-lo, independentemente de quem o criou originalmente. Se uma SAS é publicada publicamente, pode ser utilizada por qualquer pessoa na Olá mundo. Uma SAS concede acesso tooresources tooanyone possessing-lo até uma das quatro ações acontece:

1. hora de expiração de Olá especificada no Olá que SAs for atingido.
2. hora de expiração de Olá especificada na política de acesso de Olá armazenado referenciada pelo Olá que SAs for atingido (se uma política de acesso armazenada é referenciada e especifica uma hora de expiração). Isto pode ocorrer porque o intervalo de Olá decorrida ou porque tiver modificado política de acesso Olá armazenado com um tempo de expiração em Olá Antigamente, que é uma forma toorevoke Olá SAS.
3. Olá armazenados referenciada pelo Olá que SAs é eliminado, que é Olá outra forma de toorevoke SAS de política de acesso. Tenha em atenção que o se recriar política de acesso de Olá armazenado com exatamente Olá o mesmo nome, SAS existentes todos os tokens será novamente válido de acordo com permissões de toohello associado essa política de acesso armazenada (assumindo que essa hora de expiração de Olá no Olá SAS não passou). Se estiver a destinar toorevoke Olá SAS, ser toouse se um nome diferente se recriá-lo a política de acesso de Olá com um tempo de expiração em Olá futura.
4. regenerar a chave de conta de Olá que foi utilizado toocreate Olá SAS. Voltar a gerar uma chave de conta fará com que todos os componentes da aplicação utilizando essa chave toofail tooauthenticate até que o se estiver a atualizar toouse Olá ou outra chave de conta válido ou chave de conta recentemente regenerada Olá.

> [!IMPORTANT]
> Uma assinatura de acesso partilhado URI está associada a assinatura de Olá de toocreate utilizadas chaves de conta Olá e Olá associado à política de acesso armazenada (se aplicável). Não se for especificada nenhuma política de acesso armazenada, hello apenas forma toorevoke uma assinatura de acesso partilhado é toochange Olá conta chave.

## <a name="authenticating-from-a-client-application-with-a-sas"></a>Autenticação de uma aplicação de cliente com uma SAS
Um cliente que está na posse de um SAS, pode utilizar Olá SAS tooauthenticate um pedido de uma conta de armazenamento para o qual possui chaves de conta Olá. Uma SAS pode ser incluída numa cadeia de ligação ou utilizada a diretamente a partir do método ou construtor adequado Olá.

### <a name="using-a-sas-in-a-connection-string"></a>Com uma SAS numa cadeia de ligação
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

### <a name="using-a-sas-in-a-constructor-or-method"></a>Utilizar um SAS num construtor ou método
Vários construtores de biblioteca de cliente de armazenamento do Azure e sobrecargas do método oferecem um parâmetro SAS, para que pode autenticar um serviço de toohello pedido com uma SAS.

Por exemplo, um URI de SAS Eis toocreate utilizado um blob de bloco de tooa de referência. Olá SAS fornece Olá apenas as credenciais necessárias para o pedido de Olá. referência de blob de bloco de Olá, em seguida, é utilizada para uma operação de escrita:

```csharp
string sasUri = "https://storagesample.blob.core.windows.net/sample-container/" +
    "sampleBlob.txt?sv=2015-07-08&sr=b&sig=39Up9JzHkxhUIhFEjEH9594DJxe7w6cIRCg0V6lCGSo%3D" +
    "&se=2016-10-18T21%3A51%3A37Z&sp=rcw";

CloudBlockBlob blob = new CloudBlockBlob(new Uri(sasUri));

// Create operation: Upload a blob with hello specified name toohello container.
// If hello blob does not exist, it will be created. If it does exist, it will be overwritten.
try
{
    MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    msWrite.Position = 0;
    using (msWrite)
    {
        await blob.UploadFromStreamAsync(msWrite);
    }

    Console.WriteLine("Create operation succeeded for SAS {0}", sasUri);
    Console.WriteLine();
}
catch (StorageException e)
{
    if (e.RequestInformation.HttpStatusCode == 403)
    {
        Console.WriteLine("Create operation failed for SAS {0}", sasUri);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    else
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}

```

## <a name="best-practices-when-using-sas"></a>Melhores práticas através da SAS
Quando utiliza assinaturas de acesso partilhado nas suas aplicações, terá de toobe conhecimento das duas potenciais riscos:

* Se Ocorreu uma fuga uma SAS, pode ser utilizada por qualquer pessoa que obtém, que potencialmente pode comprometer a sua conta do storage.
* Se uma SAS fornecido a aplicação de cliente tooa expira e aplicação Olá é tooretrieve não é possível uma nova SAS do seu serviço, em seguida, a funcionalidade da aplicação Olá poderá ser hindered.

Olá seguintes recomendações para a utilização de assinaturas de acesso partilhado podem ajudar a mitigar estes riscos:

1. **Utilizam sempre HTTPS** toocreate ou distribuir uma SAS. Se uma SAS é transmitida através de HTTP e forem intercetada, um atacante efetuar um ataque man-in-the-middle é capaz de tooread Olá SAS e, em seguida, utilizá-lo tal como Olá pretendido utilizador pode ter potencialmente comprometer a dados confidenciais ou permitindo danos nos dados por Olá utilizador mal intencionado.
2. **Referência armazenadas as políticas de acesso sempre que possível.** Armazenados conceder de políticas de acesso Olá permissões toorevoke de opção sem ter de chaves de conta de armazenamento de Olá tooregenerate. Definir estes muito num Olá expiração Olá futuras (ou infinito) e certifique-se de atualizou regularmente toomove farther para Olá futura.
3. **Utilize um SAS ad hoc near-term tempos de expiração.** Desta forma, mesmo que uma SAS esteja comprometida, é válido apenas para um curto período de tempo. Esta prática é especialmente importante se não é possível referenciar uma política de acesso armazenada. Near-term tempos de expiração também limitam a quantidade de Olá de dados que podem ser gravados tooa blob ao limitar Olá tempo disponível tooupload tooit.
4. **Ter clientes renovar automaticamente Olá SAS, se necessário.** Os clientes devem renovar Olá SAS bem antes da expiração Olá, atempadamente ordem tooallow para novas tentativas se o serviço de Olá fornecer Olá SAS não está disponível. Se a SAS destina-se toobe utilizado para um pequeno número de imediato, curta duração operações que são esperados toobe concluída dentro do período de expiração de Olá, então, isto pode dever-se desnecessários como Olá que SAs não é esperado toobe renovado. No entanto, se tiver o cliente que está a efetuar regularmente pedidos através de SAS, em seguida, possibilidade de Olá de expiração entra play. Olá chave consideração é toobalance Olá necessidade para Olá SAS toobe curta duração (como anteriormente indicado) com Olá necessidade tooensure que hello do cliente está a pedir renovação antecipadamente suficiente (tooavoid interrupção devido a renovação do toohello SAS expirando toosuccessful anterior).
5. **Seja cuidadoso com a hora de início do SAS.** Se definir a hora de início Olá para um SAS demasiado**agora**, em seguida, devido a tooclock desfasamento (diferenças na hora atual de acordo com as máquinas de toodifferent), falhas poderão ser observadas ligados intermitentemente para Olá primeiro alguns minutos. Em geral, defina toobe de hora de início de Olá, pelo menos, 15 minutos na Olá passado. Em alternativa, não defina-o de todo, que tornará válido imediatamente em todos os casos. Olá mesmo tooexpiry tempo bem – aplica-se, geralmente, lembre-se de que pode observar se too15 minutos do relógio dissimetrias em qualquer direção no qualquer pedido. Para clientes que utilizam um REST versão anterior too2012-02-12, a duração máxima do Olá para um SAS que não façam referência a uma política de acesso armazenada é 1 hora e quaisquer políticas de especificar o prazo mais do que o que irá falhar.
6. **Ser específico com Olá recursos toobe acedido.** Uma melhor prática de segurança é tooprovide um utilizador com privilégios mínimos necessários de Olá. Se um utilizador necessita apenas de acesso de leitura tooa única entidade, em seguida, conceda acesso de leitura toothat única entidade e não de leitura/escrita/eliminar acesso tooall entidades. Isto também ajuda a lessen danos Olá se uma SAS é comprometida porque Olá SAS tem menos potência na Olá às mãos de um atacante.
7. **Tenha em atenção que a conta será faturada por qualquer utilização, incluindo feito com uma SAS.** Se fornecer o blob de tooa de acesso de escrita, um utilizador pode escolher tooupload um blob de 200GB. Se concedeu ao-los, bem como o acesso de leitura, que podem escolher toodownload-10 vezes, a incorrer em 2 TB de saída custos para si. Novamente, fornecer permissões limitadas toohelp mitigar ações de potenciais Olá de utilizadores mal intencionados. Utilize esta ameaça de curta duração SAS tooreduce (mas ser mindful do relógio dissimetrias na hora de fim de Olá).
8. **Valide os dados escritos através da SAS.** Quando uma aplicação cliente escreve a conta de armazenamento de dados tooyour, tenha em atenção que só pode haver problemas com os dados. Se a sua aplicação requer que esse dados ser validados ou autorizados antes de ser toouse pronta, deverá efetuar esta validação após Olá dados são escritos e antes de ser utilizado pela sua aplicação. Esta prática também protege contra dados danificados ou maliciosos a ser escritos tooyour conta, por um utilizador a quem adquiriu corretamente Olá SAS, ou por um utilizador explorá uma SAS obtida ilicitamente.
9. **Não utilize sempre SAS.** Por vezes, riscos de Olá associados a uma operação específica em relação a sua conta do storage prevalecem sobre os benefícios de Olá de SAS. Para operações, crie um serviço de camada média que escreve a conta de armazenamento tooyour depois de efetuar o negócio da regra de validação, a autenticação e a auditoria. Além disso, por vezes, é mais simples toomanage acesso de outras formas. Por exemplo, se quiser toomake todos os blobs num contentor legíveis publicamente, pode efetuar Olá contentor público, em vez de fornecer um cliente de tooevery SAS para o acesso.
10. **Utilize a aplicação de toomonitor de análise de armazenamento.** Pode utilizar o registo e tooobserve métricas qualquer aumentam em falhas de autenticação devido a indisponibilidade de tooan na sua SAS fornecedor serviço ou toohello inadvertida remoção de uma política de acesso armazenada. Consulte Olá [blogue da equipa de armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx) para obter informações adicionais.

## <a name="sas-examples"></a>Exemplos SAS
Segue-se alguns exemplos de ambos os tipos de assinaturas de acesso partilhado, a conta SAS e serviço SAS.

toorun c# estes exemplos, terá de Olá tooreference os seguintes pacotes de NuGet no seu projeto:

* [Biblioteca de clientes do Storage do Azure para .NET](http://www.nuget.org/packages/WindowsAzure.Storage), versão 6 ou posterior (toouse conta SAS).
* [Gestor de Configuração do Azure](http://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)

Para obter exemplos adicionais que mostram como toocreate e teste um SAS, consulte o artigo [exemplos de código do Azure para armazenamento](https://azure.microsoft.com/documentation/samples/?service=storage).

### <a name="example-create-and-use-an-account-sas"></a>Exemplo: Criar e utilizar uma conta SAS
Olá exemplo de código seguinte cria uma conta SAS que é válido para Olá Blob e serviços de ficheiros e oferece Olá permissões de cliente de leitura, escrita e permissões de lista tooaccess-um nível de serviço APIs. conta Olá SAS restringe Olá protocolo tooHTTPS, pelo que o pedido de Olá têm de ser efetuado com HTTPS.

```csharp
static string GetAccountSASToken()
{
    // toocreate hello account SAS, you need toouse your shared key credentials. Modify for your account.
    const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

    // Create a new access policy for hello account.
    SharedAccessAccountPolicy policy = new SharedAccessAccountPolicy()
        {
            Permissions = SharedAccessAccountPermissions.Read | SharedAccessAccountPermissions.Write | SharedAccessAccountPermissions.List,
            Services = SharedAccessAccountServices.Blob | SharedAccessAccountServices.File,
            ResourceTypes = SharedAccessAccountResourceTypes.Service,
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Protocols = SharedAccessProtocol.HttpsOnly
        };

    // Return hello SAS token.
    return storageAccount.GetSharedAccessSignature(policy);
}
```

toouse Olá conta SAS tooaccess nível de serviço APIs para o serviço de Blob Olá, construir um objeto de cliente do Blob utilizando Olá SAS e Olá ponto final de armazenamento de BLOBs para a sua conta de armazenamento.

```csharp
static void UseAccountSAS(string sasToken)
{
    // Create new storage credentials using hello SAS token.
    StorageCredentials accountSAS = new StorageCredentials(sasToken);
    // Use these credentials and hello account name toocreate a Blob service client.
    CloudStorageAccount accountWithSAS = new CloudStorageAccount(accountSAS, "account-name", endpointSuffix: null, useHttps: true);
    CloudBlobClient blobClientWithSAS = accountWithSAS.CreateCloudBlobClient();

    // Now set hello service properties for hello Blob client created with hello SAS.
    blobClientWithSAS.SetServiceProperties(new ServiceProperties()
    {
        HourMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        MinuteMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        Logging = new LoggingProperties()
        {
            LoggingOperations = LoggingOperations.All,
            RetentionDays = 14,
            Version = "1.0"
        }
    });

    // hello permissions granted by hello account SAS also permit you tooretrieve service properties.
    ServiceProperties serviceProperties = blobClientWithSAS.GetServiceProperties();
    Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
    Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
    Console.WriteLine(serviceProperties.HourMetrics.Version);
}
```

### <a name="example-create-a-stored-access-policy"></a>Exemplo: Criar uma política de acesso armazenada
Olá código seguinte cria uma política de acesso armazenado num contentor. Pode utilizar restrições de toospecify de políticas de acesso de Olá para um serviço SAS no contentor de Olá ou os respetivos blobs.

```csharp
private static async Task CreateSharedAccessPolicyAsync(CloudBlobContainer container, string policyName)
{
    // Create a new shared access policy and define its constraints.
    // hello access policy provides create, write, read, list, and delete permissions.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
        // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
        SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.List |
            SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create | SharedAccessBlobPermissions.Delete
    };

    // Get hello container's existing permissions.
    BlobContainerPermissions permissions = await container.GetPermissionsAsync();

    // Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    await container.SetPermissionsAsync(permissions);
}
```

### <a name="example-create-a-service-sas-on-a-container"></a>Exemplo: Criar um serviço SAS num contentor
Olá código a seguir cria um SAS num contentor. Se não for fornecido nome de Olá de uma política de acesso armazenada existente, essa política está associada a Olá SAS. Se nenhuma política de acesso armazenada for fornecida, o código de Olá cria um SAS ad-hoc no contentor de Olá.

```csharp
private static string GetContainerSasUri(CloudBlobContainer container, string storedPolicyName = null)
{
    string sasContainerToken;

    // If no stored policy is specified, create a new access policy and define its constraints.
    if (storedPolicyName == null)
    {
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocPolicy = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List
        };

        // Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
        sasContainerToken = container.GetSharedAccessSignature(adHocPolicy, null);

        Console.WriteLine("SAS for blob container (ad hoc): {0}", sasContainerToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello container. In this case, all of hello constraints for the
        // shared access signature are specified on hello stored access policy, which is provided by name.
        // It is also possible toospecify some constraints on an ad-hoc SAS and others on hello stored access policy.
        sasContainerToken = container.GetSharedAccessSignature(null, storedPolicyName);

        Console.WriteLine("SAS for blob container (stored access policy): {0}", sasContainerToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

### <a name="example-create-a-service-sas-on-a-blob"></a>Exemplo: Criar um serviço SAS num blob
Olá código a seguir cria um SAS no blob. Se não for fornecido nome de Olá de uma política de acesso armazenada existente, essa política está associada a Olá SAS. Se nenhuma política de acesso armazenada for fornecida, o código de Olá cria um SAS ad-hoc no blob Olá.

```csharp
private static string GetBlobSasUri(CloudBlobContainer container, string blobName, string policyName = null)
{
    string sasBlobToken;

    // Get a reference tooa blob within hello container.
    // Note that hello blob may not exist yet, but a SAS can still be created for it.
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    if (policyName == null)
    {
        // Create a new access policy and define its constraints.
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocSAS = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create
        };

        // Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
        sasBlobToken = blob.GetSharedAccessSignature(adHocSAS);

        Console.WriteLine("SAS for blob (ad hoc): {0}", sasBlobToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello blob. In this case, all of hello constraints for the
        // shared access signature are specified on hello container's stored access policy.
        sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

        Console.WriteLine("SAS for blob (stored access policy): {0}", sasBlobToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

## <a name="conclusion"></a>Conclusão
Assinaturas de acesso partilhado são úteis para fornecer permissões limitadas tooclients de conta de armazenamento tooyour não deve ter a chave de conta Olá. Como tal, são uma parte vital do modelo de segurança de Olá para qualquer aplicação utilizando o armazenamento do Azure. Se seguir as melhores práticas de Olá listadas aqui, pode utilizar SAS tooprovide uma maior flexibilidade de tooresources de acesso na sua conta de armazenamento, sem comprometer a segurança de Olá da sua aplicação.

## <a name="next-steps"></a>Passos Seguintes
* [Gerir o acesso de leitura anónimo toocontainers e blobs](storage-manage-access-to-resources.md)
* [Delegar Acesso com uma Assinatura de Acesso Partilhado](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [Introduzir tabela e fila SAS](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)

[sas-storage-fe-proxy-service]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-fe-proxy-service.png
[sas-storage-provider-service]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-provider-service.png
[sas-storage-uri]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-uri.png
