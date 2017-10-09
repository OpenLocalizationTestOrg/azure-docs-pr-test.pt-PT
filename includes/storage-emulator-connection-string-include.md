emulador do storage Olá suporta uma única conta fixa e uma chave de autenticação conhecidos para a autenticação de chave partilhada. Esta conta e chave são Olá credenciais de chave partilhada apenas permitidas para utilização com o emulador do storage Olá. São:

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> chave de autenticação de Olá suportado pelo emulador do storage Olá destina-se apenas para testes Olá funcionalidades do seu código de autenticação de cliente. Servem qualquer objetivo de segurança. Não é possível utilizar a conta de armazenamento de produção e a chave com o emulador do storage Olá. Não deve utilizar a conta de desenvolvimento de Olá com dados de produção.
> 
> emulador do storage Olá suporta a ligação através de HTTP apenas. No entanto, o HTTPS é Olá recomendado protocolo para aceder a recursos na conta do storage do Azure de produção.
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a>Ligar a conta de emulador de toohello utilizando um atalho
Olá mais fácil forma tooconnect toohello emulador de armazenamento da sua aplicação é tooconfigure uma cadeia de ligação no ficheiro de configuração da aplicação que referencia o atalho Olá `UseDevelopmentStorage=true`. Eis um exemplo de um emulador do storage de toohello cadeia ligação num *App. config* ficheiro: 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a>Ligar a conta de emulador de toohello utilizando o nome de conta conhecidos Olá e chave
toocreate uma cadeia de ligação que referências Olá nome da conta do emulador e chave, terá de especificar pontos finais de Olá para cada um dos Olá serviços pretendem toouse do emulador de Olá na cadeia de ligação de Olá. Isto é necessário para que a cadeia de ligação de Olá fará referência Olá emulador pontos finais, que são diferentes dos para uma conta de armazenamento de produção. Por exemplo, valor Olá a cadeia de ligação terá este aspeto:

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

Este valor é atalho toohello idênticos mostrado acima, `UseDevelopmentStorage=true`.

#### <a name="specify-an-http-proxy"></a>Especifique um proxy HTTP
Também pode especificar um toouse de proxy HTTP quando estiver a testar o seu serviço de emulador do storage Olá. Isto pode ser útil para observar os pedidos e respostas HTTP enquanto estiver a depuração operações nos serviços de armazenamento Olá. toospecify um proxy, adicionar Olá `DevelopmentStorageProxyUri` opção toohello cadeia de ligação e defina o URI de proxy toohello de valor. Por exemplo, aqui é uma cadeia de ligação que aponta toohello emulador de armazenamento e configura um proxy HTTP:

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

