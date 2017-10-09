## <a name="what-are-service-bus-topics-and-subscriptions"></a>O que são os tópicos e as subscrições do Service Bus?
Os tópicos e as subscrições do Service Bus suportam um modelo de comunicação de mensagens de *publicação/subscrição*. Ao utilizar tópicos e subscrições, os componentes de uma aplicação distribuída não comunicam diretamente entre si; trocam antes mensagens através de um tópico, que funciona como um intermediário.

![TopicConcepts](./media/howto-service-bus-topics/sb-topics-01.png)

Ao contrário das filas do Service Bus, em que cada mensagem é processada por um único consumidor, os tópicos e as subscrições proporcionam uma forma de comunicação de “um-para-muitos”, utilizando um padrão de publicação/subscrição. É possível registar o tópico de tooa várias subscrições. Quando uma mensagem é enviada tooa tópico,-lo, em seguida, ficam disponíveis tooeach subscrição toohandle/processe independentemente.

Um tópico de tooa subscrição é semelhante uma fila virtual que recebe cópias das mensagens hello que foram enviadas toohello tópico. Opcionalmente, pode registar regras de filtro para um tópico numa base por subscrição, que lhe permite toofilter ou restringir o tópico de tooa mensagens são recebidas por que subscrições desse tópico.

Tópicos do Service Bus e subscrições permitem-lhe tooscale e processam um número muito grande de mensagens entre muito utilizadores e aplicações.

## <a name="create-a-namespace"></a>Criar um espaço de nomes
toobegin utilizar tópicos do Service Bus e subscrições no Azure, primeiro tem de criar um *espaço de nomes de serviço*. Um espaço de nomes fornece um contentor de âmbito para abordar os recursos do Service Bus na sua aplicação.

toocreate um espaço de nomes:

1. Inicie sessão no toohello [portal do Azure][Azure portal].
2. No painel de navegação esquerdo Olá do portal de Olá, clique em **novo**, em seguida, clique em **integração empresarial com**e, em seguida, clique em **Service Bus**.
3. No Olá **criar espaço de nomes** caixa de diálogo, introduza um nome de espaço de nomes. sistema de Olá verifica imediatamente toosee se o nome de Olá está disponível.
4. Depois de efetuar o nome de espaço de nomes de Olá se estiver disponível, escolha Olá (básica, Standard ou Premium) de escalão de preço.
5. No Olá **subscrição** campo, escolha uma subscrição do Azure no espaço de nomes de Olá que toocreate.
6. No Olá **grupo de recursos** campo, escolha um grupo de recursos existente na qual Olá espaço de nomes em direto ou, crie um novo.      
7. No **localização**, escolha o país Olá ou região onde será alojado o espaço de nomes.
   
    ![Create namespace][create-namespace]
8. Clique em Olá **criar** botão. Agora, o sistema Olá cria o seu espaço de nomes e ativa-o. Poderá ter toowait alguns minutos enquanto Olá sistema Aprovisiona recursos para a sua conta.

### <a name="obtain-hello-credentials"></a>Obter credenciais Olá
1. Na lista de Olá dos espaços de nomes, clique em Olá recém-criado espaço de nomes.
2. No Olá **espaço de nomes do Service Bus** painel, clique em **políticas de acesso partilhado**.
3. No Olá **políticas de acesso partilhado** painel, clique em **RootManageSharedAccessKey**.
   
    ![connection-info][connection-info]
4. No Olá **política: RootManageSharedAccessKey** painel, clique no botão de cópia de Olá junto demasiado**chave de cadeia – primária da ligação**, toocopy Olá ligação cadeia tooyour área de transferência para utilização posterior.
   
    ![connection-string][connection-string]

[Azure portal]: https://portal.azure.com
[create-namespace]: ./media/howto-service-bus-topics/create-namespace.png
[connection-info]: ./media/howto-service-bus-topics/connection-info.png
[connection-string]: ./media/howto-service-bus-topics/connection-string.png


