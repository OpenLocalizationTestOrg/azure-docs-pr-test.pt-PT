Se possui um URL de assinatura (SAS) de acesso partilhado que concede que acesso tooresources numa conta do storage, pode utilizar Olá SAS numa cadeia de ligação. Porque Olá SAS contém pedido de Olá Olá informações tooauthenticate necessário, uma cadeia de ligação com uma SAS fornece Olá credenciais necessárias tooaccess Olá recurso, de ponto final de serviço Olá e de protocolo de Olá.

toocreate uma cadeia de ligação que inclui uma assinatura de acesso partilhado, especifique a cadeia de Olá no Olá seguinte formato:

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

Cada ponto final de serviço é opcional, embora a cadeia de ligação de Olá tem de conter, pelo menos, um.

> [!NOTE]
> É recomendado utilizar HTTPS com uma SAS como melhor prática.
>
> Se especificar uma SAS numa cadeia de ligação num ficheiro de configuração, poderá ser necessário tooencode carateres especiais no URL Olá.
>
>

### <a name="service-sas-example"></a>Exemplo de SAS do serviço
Eis um exemplo de uma cadeia de ligação que inclui um serviço SAS para o Blob storage:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

E Eis um exemplo de Olá mesma cadeia de ligação com codificação de carateres especiais:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a>Exemplo SAS de conta
Eis um exemplo de uma cadeia de ligação que inclui uma conta SAS para o armazenamento de Blob e o ficheiro. Tenha em atenção que os pontos finais para ambos os serviços são especificados:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

E Eis um exemplo de Olá mesma cadeia de ligação com codificação URL:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

