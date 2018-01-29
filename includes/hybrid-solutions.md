# <a name="azure-service-bus"></a>Service Bus do Azure
Se uma aplicação ou serviço é executado na nuvem ou de modo local, muitas vezes, tem de interagir com outros serviços ou aplicações. Para fornecer uma forma amplamente útil de efetuar este procedimento, o Azure oferece Service Bus. Este artigo dá uma vista de olhos a esta tecnologia, descreve o que é e por que razão poderá pretender utilizá-la.

## <a name="service-bus-fundamentals"></a>Noções básicas do Service Bus
Situações diferentes exigem estilos diferentes de comunicação. Por vezes, permitir às aplicações enviar e receber mensagens através de uma fila simples é a melhor solução. Noutras situações, uma fila comum não é suficiente e é melhor uma fila com um mecanismo de publicação e subscrição. E, em alguns casos, tudo o que realmente necessário é uma ligação entre aplicações &#151; não são precisas filas. O Service Bus fornece as três opções, permitindo que as aplicações podem interagir de várias maneiras diferentes.

O Service Bus é um serviço de nuvem multi-inquilino, o que significa que vários utilizadores partilham o serviço. Cada utilizador, como um programador de aplicações, cria um *espaço de nomes*, em seguida, define os mecanismos de comunicação que precisa dentro desse espaço de nomes. [Figura 1](#Fig1) mostra que aspeto.

<a name="Fig1"></a>![Diagrama do Service Bus do Azure][svc-bus]

**Figura 1: O Service Bus fornece um serviço multi-inquilino para ligar aplicações através da nuvem.**

Dentro de um espaço de nomes, pode utilizar uma ou mais instâncias dos quatro diferentes mecanismos de comunicação, os quais ligam aplicações de forma diferente. As opções são:

* *Filas*, que permitem comunicação unidirecional. Cada fila funciona como um intermediário (por vezes denominado *mediador*) que armazena as mensagens enviadas até serem recebidas. Cada mensagem é recebida por um único destinatário.
* *Tópicos*, que proporcionam uma comunicação unidirecional através de *subscrições* – um só tópico pode ter várias subscrições. Tal como as filas, o tópico funciona como um mediador, mas cada subscrição pode utilizar opcionalmente um filtro para receber apenas as mensagens que correspondem a critérios específicos.
* *Reencaminhamentos*, que proporcionam comunicação bidirecional. Ao contrário das filas e tópicos, um reencaminhamento não armazena as mensagens em trânsito - não é um mediador. Simplesmente, transmite-as à aplicação de destino.
* *Event Hubs*, que proporcionam entrada em grande escala de telemetria e de eventos para a nuvem, com baixa latência e alta fiabilidade.

Ao criar uma fila, tópico, reencaminhamento ou Event Hub, atribui-lhe um nome. Quando combinado com o espaço de nomes, cria-se um identificador exclusivo para o objeto. As aplicações podem fornecer este nome ao Service Bus e, em seguida, utilizar essa fila, tópico, reencaminhamento ou Event Hub para comunicar entre si. 

Para utilizar qualquer um destes objetos, as aplicações do Windows podem utilizar o Windows Communication Foundation (WCF). Para as filas, tópicos e Event Hubs, as aplicações de Windows também podem utilizar as APIs de mensagens definidas pelo Service Bus. Para facilitar a utilização destes objetos a partir de aplicações que não sejam de Windows, a Microsoft disponibiliza SDKs para Java, Node.js e outras linguagens. Também pode aceder às filas, tópicos e Event Hubs utilizando as APIs REST através do HTTP. 

É importante compreender que, apesar do Service Bus propriamente dito ser executado na nuvem (ou seja, nos datacenters de Azure da Microsoft), as aplicações que o utilizam podem ser executadas em qualquer lugar. Pode utilizar o Service Bus para ligar aplicações que se executam, por exemplo, no Azure, ou aplicações que se executam dentro do seu próprio datacenter. Também pode utilizá-lo para ligar uma aplicação em execução no Azure ou noutra plataforma na nuvem com uma aplicação no local ou com telemóveis e tablets. Também é possível ligar aparelhos domésticos, sensores e outros dispositivos a uma aplicação central ou entre si. O Service Bus é um mecanismo de comunicação genérico na nuvem que é acessível em praticamente qualquer lugar. O modo como o utiliza depende do que tem de realizar a aplicação.

## <a name="queues"></a>Filas
Suponha que decide ligar duas aplicações com uma fila do Service Bus. [Figura 2](#Fig2) ilustra esta situação.

<a name="Fig2"></a>![Diagrama de filas do Service Bus][queues]

**Figura 2: As filas do Service Bus proporcionam filas unidirecionais assíncronas.**

O processo é simples: um remetente envia uma mensagem para uma fila do Service Bus e um recetor apanha essa mensagem mais tarde. Uma fila pode ter apenas um único recetor como [figura 2](#Fig2) mostra ou várias aplicações podem ler a partir da mesma fila. Na última situação, cada mensagem é lida por apenas um recetor - para um serviço com multi-difusão deve antes utilizar um tópico.

Cada mensagem tem duas partes: um conjunto de propriedades, cada uma delas um par chave/valor, e um corpo de mensagem binário. O modo como são utilizados depende do que a aplicação está a tentar fazer. Por exemplo, uma aplicação que envia uma mensagem sobre uma venda recente pode incluir as propriedades *Vendedor="Ava"* e *Valor= 10000*. O corpo da mensagem poderá conter uma imagem digitalizada do contrato de venda assinado ou, se não existir, pode permanecer vazio.

O recetor pode ler uma mensagem da fila do Service Bus de duas formas diferentes. A primeira opção, denominada *ReceiveAndDelete*, remove a mensagem da fila e elimina-a imediatamente. Isto é simples, mas se há uma falha da parte do recetor antes de concluir o processamento da mensagem, esta será perdida. Dado que é removida da fila, nenhum outro recetor pode aceder à mesma. 

A segunda opção, *PeekLock*, foi criada para solucionar este problema. Como ReceiveAndDelete, uma leitura PeekLock remove a mensagem da fila. No entanto, não elimina a mensagem. Neste caso, bloqueia a mensagem, pelo que fica invisível para os outros recetores, em seguida, aguarda que um dos três eventos ocorra:

* Se o recetor processar a mensagem com êxito, aquele invoca *Concluir* e a fila elimina a mensagem. 
* Se o recetor decidir que não é possível processar a mensagem com êxito, aquele invoca *Abandonar*. A fila, em seguida, remove o bloqueio da mensagem e torna-o disponível para outros recetores.
* Se o recetor não invocar nenhuma destas opções num período de tempo configurável (60 segundos, por predefinição), a fila assume que o recetor falhou. Neste caso, comporta-se como se o recetor invocasse abandono, pelo que a mensagem disponível para outros recetores.

Tenha em atenção o que pode acontecer aqui: a mesma mensagem poderá ser entregue duas vezes, talvez a dois recetores diferentes. As aplicações que utilizam filas do Service Bus devem estar preparadas para tal. Para facilitar a deteção duplicada, que cada mensagem tem uma propriedade MessageID exclusiva, que, por predefinição, permanece o mesmo, independentemente de como número de vezes que se leia mensagem numa fila. 

As filas são úteis em determinadas situações. Permitem às aplicações comunicar entre si, mesmo quando ambas não estão a ser executadas ao mesmo tempo, algo que é especialmente útil com lotes e aplicações. Uma fila com vários recetores também proporciona um balanceamento de carga automático, uma vez que as mensagens enviadas são distribuídas por estes recetores.

## <a name="topics"></a>Tópicos
Ainda que sejam úteis, as filas não sempre são a solução certa. Por vezes, os tópicos do Service Bus são melhores. [Figura 3](#Fig3) ilustra a ideia.

<a name="Fig3"></a>![Diagrama de tópicos de Service Bus e subscrições][topics-subs]

**Figura 3: Com base no filtro especificado por uma aplicação de subscrição, pode receber algumas ou todas as mensagens enviadas para um tópico do Service Bus.**

Um tópico é semelhante em muitos aspetos a uma fila. Os remetentes submetem mensagens a um tópico da mesma forma que submetem mensagens a uma fila e essas mensagens têm o mesmo aspeto que nas filas. A grande diferença é que os tópicos permitem a cada aplicação de receção criar a sua própria subscrição, definindo um *filtro*. Consequentemente, o subscritor verá apenas as mensagens que correspondem a esse filtro. Por exemplo, [figura 3](#Fig3) mostra um remetente e um tópico com três subscritores, cada um com o seu próprio filtro:

* O subscritor 1 recebe apenas as mensagens que contêm a propriedade *Vendedor="Ava"*.
* O subscritor 2 recebe mensagens que contêm a propriedade *Vendedor="Ruby"* e/ou contem a propriedade *Valor* cujo valor é superior a 100.000. Talvez Ruby seja a gestora de vendas e, por isso que pretende ver a suas próprias vendas e todas as vendas grandes, independentemente de quem as faz.
* O subscritor 3 definiu o seu filtro como *True*, o que significa que recebe todas as mensagens. Por exemplo, esta aplicação pode ser responsável por manter um registo de auditoria e, por conseguinte, precisa de ver todas as mensagens.

Tal como acontece com as filas, os subscritores de um tópico podem ler mensagens através de ReceiveAndDelete ou PeekLock. No entanto, ao contrário das filas, uma única mensagem enviada para um tópico pode recebida por vários subscritores. Esta abordagem, geralmente designada por *publicar e subscrever*, é útil quando várias aplicações podem ser interessadas nas mesmas mensagens. Se definir o filtro adequado, cada subscritor pode recuperar apenas a parte do fluxo de mensagens que quer ver.

## <a name="relays"></a>Reencaminhamentos
Tanto as filas como os tópicos proporcionam comunicação assíncrona unidirecional através de um mediador. O tráfego flui numa única direção e não existe uma ligação direta entre os remetentes e os recetores. Mas e se não o quiser? Suponha que as suas aplicações precisam de enviar e receber mensagens ou talvez pretenda uma ligação direta entre elas e não precisa de um mediador para armazenar as mensagens. Para solucionar como esta, Service Bus proporciona reencaminhamentos, como [figura 4](#Fig4) mostra.

<a name="Fig4"></a>![Diagrama de reencaminhamento do Service Bus][relay]

**Figura 4: O reencaminhamento do Service Bus proporciona comunicação síncrona bidirecional entre as aplicações.**

A questão óbvia sobre os reencaminhamentos que se coloca é esta: por que tenho de utilizar um? Mesmo que não precise de filas, por que motivo fazer com que as aplicações comuniquem através de um serviço em nuvem em vez de apenas interagir diretamente? A resposta é que comunicar diretamente pode ser mais difícil de que se pensa.

Suponha que pretende ligar duas aplicações no local, ambas em execução dentro dos datacenters empresariais. Cada uma dessas aplicações encontra-se protegida por uma firewall e cada datacenter utiliza provavelmente tradução de endereços de rede (NAT). A firewall bloqueia os dados recebidos em quase todas as portas e NAT significa que a máquina em que se executa cada aplicação não tem um endereço IP fixo ao qual pode aceder diretamente a partir de fora do datacenter. Se não houver ajuda extra, é complicado ligar estas aplicações através da Internet pública.

Um reencaminhamento de Service Bus proporciona esta ajuda. Para comunicar de forma bidirecional através de um reencaminhamento, cada aplicação estabelece uma ligação TCP de saída com o Service Bus e mantém-na aberta. Toda a comunicação entre as duas aplicações percorre essas ligações. Uma vez que cada ligação se estabeleceu de dentro do datacenter, a firewall permitirá o tráfego de entrada para cada aplicação sem abrir novas portas. Esta abordagem também contorna o problema de NAT porque cada aplicação dispõe de um ponto final consistente na nuvem durante toda a duração da comunicação. Ao trocar dados através do reencaminhamento, as aplicações podem evitar os problemas que dificultariam a comunicação. 

Para utilizar os reencaminhamentos do Service Bus, as aplicações baseiam-se no Windows Communication Foundation (WCF). O Service Bus proporciona enlaces WCF que facilitam a interação das aplicações de Windows através dos reencaminhamentos. As aplicações que já utilizam WCF podem normalmente especificar apenas um destes enlaces e depois comunicar entre si através de um reencaminhamento. Todavia, ao contrário das filas e tópicos, a utilização de reencaminhamentos a partir de aplicações que não sejam de Windows, ainda que possível, necessita de algum esforço de programação; não são fornecidas bibliotecas padrão.

Ao contrário do que acontece com as filas e tópicos, as aplicações não criam reencaminhamentos de forma explícita. Quando uma aplicação que pretende receber mensagens estabelece uma ligação TCP com o Service Bus, é criado automaticamente um reencaminhamento. Este é eliminado quando se abandona a ligação. Para permitir que uma aplicação encontre o reencaminhamento criado por um serviço de escuta específico, o Service Bus fornece um registo que permite às aplicações localizar um reencaminhamento específico por nome.

Os reencaminhamentos são a solução certa quando precisa de comunicação direta entre aplicações. Por exemplo, imagine um sistema de reserva de uma companhia aérea que se executa num datacenter no local e que tem de ser acedido em quiosques de check-in, dispositivos móveis e outros computadores. As aplicações que se executam em todos estes sistemas poderiam depender dos reencaminhamentos do Service Bus na nuvem para comunicar, independentemente do local em que estão em execução.

## <a name="event-hubs"></a>Event Hubs
Os Event Hubs são um serviço de ingestão de dados altamente dimensionável, que pode processar milhões de eventos por segundo para que a sua aplicação possa processar e analisar as quantidades enormes de dados produzidos pelos dispositivos e aplicações ligados. Por exemplo, pode utilizar um Event Hub para recolher dados de desempenho do motor em direto de uma frota de automóveis. Depois de recolhidos nos Event Hubs, pode transformar e armazenar dados em qualquer fornecedor de análise em tempo real ou cluster de armazenamento. Para obter mais informações sobre os Event Hubs, consulte o [descrição geral dos Event Hubs][Event Hubs overview].

## <a name="summary"></a>Resumo
A ligação de aplicações sempre fez parte da criação de soluções completas e a variedade de cenários que precisam que as aplicações e os serviços comuniquem entre si aumentará logo que mais aplicações e dispositivos se liguem à Internet. Ao fornecer tecnologias baseadas na nuvem para consegui-lo através de filas, tópicos, reencaminhamentos e Event Hubs, o Service Bus tem como objetivo tornar essa função essencial mais fácil de implementar e mais amplamente disponível.

[svc-bus]: ./media/hybrid-solutions/SvcBus_01_architecture.png
[queues]: ./media/hybrid-solutions/SvcBus_02_queues.png
[topics-subs]: ./media/hybrid-solutions/SvcBus_03_topicsandsubscriptions.png
[relay]: ./media/hybrid-solutions/SvcBus_04_relay.png
[Event Hubs overview]: https://msdn.microsoft.com/library/azure/dn836025.aspx
