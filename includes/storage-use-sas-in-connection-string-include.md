<span data-ttu-id="2067e-101">Se possui um URL de assinatura (SAS) de acesso partilhado que concede que acesso tooresources numa conta do storage, pode utilizar Olá SAS numa cadeia de ligação.</span><span class="sxs-lookup"><span data-stu-id="2067e-101">If you possess a shared access signature (SAS) URL that grants you access tooresources in a storage account, you can use hello SAS in a connection string.</span></span> <span data-ttu-id="2067e-102">Porque Olá SAS contém pedido de Olá Olá informações tooauthenticate necessário, uma cadeia de ligação com uma SAS fornece Olá credenciais necessárias tooaccess Olá recurso, de ponto final de serviço Olá e de protocolo de Olá.</span><span class="sxs-lookup"><span data-stu-id="2067e-102">Because hello SAS contains hello information required tooauthenticate hello request, a connection string with a SAS provides hello protocol, hello service endpoint, and hello necessary credentials tooaccess hello resource.</span></span>

<span data-ttu-id="2067e-103">toocreate uma cadeia de ligação que inclui uma assinatura de acesso partilhado, especifique a cadeia de Olá no Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="2067e-103">toocreate a connection string that includes a shared access signature, specify hello string in hello following format:</span></span>

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

<span data-ttu-id="2067e-104">Cada ponto final de serviço é opcional, embora a cadeia de ligação de Olá tem de conter, pelo menos, um.</span><span class="sxs-lookup"><span data-stu-id="2067e-104">Each service endpoint is optional, although hello connection string must contain at least one.</span></span>

> [!NOTE]
> <span data-ttu-id="2067e-105">É recomendado utilizar HTTPS com uma SAS como melhor prática.</span><span class="sxs-lookup"><span data-stu-id="2067e-105">Using HTTPS with a SAS is recommended as a best practice.</span></span>
>
> <span data-ttu-id="2067e-106">Se especificar uma SAS numa cadeia de ligação num ficheiro de configuração, poderá ser necessário tooencode carateres especiais no URL Olá.</span><span class="sxs-lookup"><span data-stu-id="2067e-106">If you are specifying a SAS in a connection string in a configuration file, you may need tooencode special characters in hello URL.</span></span>
>
>

### <a name="service-sas-example"></a><span data-ttu-id="2067e-107">Exemplo de SAS do serviço</span><span class="sxs-lookup"><span data-stu-id="2067e-107">Service SAS example</span></span>
<span data-ttu-id="2067e-108">Eis um exemplo de uma cadeia de ligação que inclui um serviço SAS para o Blob storage:</span><span class="sxs-lookup"><span data-stu-id="2067e-108">Here's an example of a connection string that includes a service SAS for Blob storage:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

<span data-ttu-id="2067e-109">E Eis um exemplo de Olá mesma cadeia de ligação com codificação de carateres especiais:</span><span class="sxs-lookup"><span data-stu-id="2067e-109">And here's an example of hello same connection string with encoding of special characters:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a><span data-ttu-id="2067e-110">Exemplo SAS de conta</span><span class="sxs-lookup"><span data-stu-id="2067e-110">Account SAS example</span></span>
<span data-ttu-id="2067e-111">Eis um exemplo de uma cadeia de ligação que inclui uma conta SAS para o armazenamento de Blob e o ficheiro.</span><span class="sxs-lookup"><span data-stu-id="2067e-111">Here's an example of a connection string that includes an account SAS for Blob and File storage.</span></span> <span data-ttu-id="2067e-112">Tenha em atenção que os pontos finais para ambos os serviços são especificados:</span><span class="sxs-lookup"><span data-stu-id="2067e-112">Note that endpoints for both services are specified:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

<span data-ttu-id="2067e-113">E Eis um exemplo de Olá mesma cadeia de ligação com codificação URL:</span><span class="sxs-lookup"><span data-stu-id="2067e-113">And here's an example of hello same connection string with URL encoding:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

