## <a name="configure-your-application-tooaccess-azure-storage"></a>Configurar a sua aplicação tooaccess Storage do Azure
Existem duas formas tooauthenticate tooaccess a aplicação dos serviços de armazenamento:

* : Partilhado utilize partilhado chave para fins de teste
* Assinatura de acesso partilhada (SAS): A utilização SAS para aplicações de produção

### <a name="shared-key"></a>Chave Partilhada
Autenticação de chave partilhada significa que a aplicação irá utilizar o seu nome de conta e tooaccess chave de conta dos serviços de armazenamento. Para efeitos Olá rapidamente que mostra como toouse nesta biblioteca, vamos utilizar a autenticação de chave partilhada nesta Introdução.

> [!WARNING] 
> **Utilize apenas autenticação de chave partilhada para fins de teste!** O nome da conta e a chave de conta, que fornece toohello de acesso de leitura/escrita completa associado à conta de armazenamento, será distribuída tooevery pessoa que transfere a sua aplicação. Este é **não** é uma boa praticar como o risco de ter a sua chave fica comprometido por clientes não fidedignos.
> 
> 

Quando utilizar a autenticação de chave partilhada, irá criar um [cadeia de ligação](../articles/storage/common/storage-configure-connection-string.md). cadeia de ligação de Olá é composta por:  

* Olá **DefaultEndpointsProtocol** -pode escolher HTTP ou HTTPS. No entanto, através de HTTPS é altamente recomendável.
* Olá **nome da conta** - hello nome da conta de armazenamento
* Olá **chave da conta** - no Olá [Portal do Azure](https://portal.azure.com), navegue até tooyour conta de armazenamento e clique em Olá **chaves** ícone toofind estas informações.
* (Opcional) **EndpointSuffix** -isto é utilizado para serviços do storage em regiões com os sufixos de outro ponto final, tais como o Azure China ou governação do Azure.

Eis um exemplo de cadeia de ligação utilizando a autenticação de chave partilhada:

`"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here"`

### <a name="shared-access-signatures-sas"></a>Assinaturas de Acesso Partilhado (SAS)
Para uma aplicação móvel, Olá recomendado método para autenticar um pedido por um cliente contra Olá serviço Storage do Azure é utilizar uma assinatura de acesso partilhado (SAS). SAS permite-lhe toogrant um recurso de tooa de acesso de cliente para um determinado período de tempo, com um conjunto especificado de permissões.
Como o proprietário da conta de armazenamento Olá, precisará toogenerate uma SAS para a sua tooconsume de clientes móveis. toogenerate Olá SAS, provavelmente, será útil toowrite um serviço separado que gera Olá SAS toobe distribuída tooyour clientes. Para fins de teste, pode utilizar Olá [Explorador de armazenamento do Microsoft Azure](http://storageexplorer.com) ou Olá [Portal do Azure](https://portal.azure.com) toogenerate uma SAS. Quando cria Olá SAS, pode especificar o intervalo de tempo de Olá ao longo do que Olá SAS é válido e as permissões de Olá Olá SAS concede toohello cliente.

Olá seguinte exemplo mostra como toouse Olá Explorador de armazenamento do Microsoft Azure toogenerate uma SAS.

1. Se ainda não o fez, [instalação Olá Explorador de armazenamento do Microsoft Azure](http://storageexplorer.com)
2. Ligar tooyour subscrição.
3. Clique na sua conta do Storage e clique no separador de Olá "ações" na parte inferior de Olá à esquerda. Clique em "Obter assinatura de acesso partilhado" toogenerate uma "cadeia de ligação" para a SAS.
4. Eis um exemplo de uma cadeia de ligação de SAS que concede ler e escrever as permissões no serviço Olá, o contentor e o nível de objeto para o serviço de blob Olá Olá da conta de armazenamento.
   
   `"SharedAccessSignature=sv=2015-04-05&ss=b&srt=sco&sp=rw&se=2016-07-21T18%3A00%3A00Z&sig=3ABdLOJZosCp0o491T%2BqZGKIhafF1nlM3MzESDDD3Gg%3D;BlobEndpoint=https://youraccount.blob.core.windows.net"`

Como pode, ao utilizar um SAS, não está a expor a chave da conta na sua aplicação. Pode saber mais sobre SAS e melhores práticas para utilizar SAS verificando [assinaturas de acesso partilhado: modelo SAS do compreender Olá](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md).

