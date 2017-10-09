# <a name="get-started-using-azure-stream-analytics-real-time-fraud-detection"></a>Começar a utilizar o Azure Stream Analytics: deteção de fraudes em tempo real

Este tutorial fornece uma ilustração de ponto a ponto sobre como toouse Azure Stream Analytics. Saiba como: 

* Traga a transmissão em fluxo de eventos para uma instância de Event Hubs do Azure. Neste tutorial, irá utilizar uma aplicação que fornecemos que simula uma sequência de registos de metadados telemóvel.

* Como o SQL Server Stream Analytics consultas tootransform dados, Agregar informações ou à procura de padrões de escrita. Verá como toouse tooexamine uma consulta Olá fluxo de entrada e procure chamadas que poderão ser fraudulentas.

* Envie Olá resultados tooan sink de saída (armazenamento) que pode analisar informações adicionais. Neste caso, irá enviar o armazenamento de Blobs do Olá chamada suspeita dados tooAzure.

Neste tutorial, utilizamos o exemplo de Olá de deteção de fraudes em tempo real com base nos dados de chamada telefónica. Mas técnica Olá que é ilustrar é também adequada para outros tipos de deteção de fraudes, tais como o roubo de fraudes ou a identidade do cartão de crédito. 

## <a name="scenario-telecommunications-and-sim-fraud-detection-in-real-time"></a>Cenário: Deteção de fraudes de telecomunicações e SIM em tempo real

Uma empresa de telecomunicações tem um grande volume de dados de chamadas recebidas. empresa de Olá pretende toodetect fraudulenta chama em tempo real, para que podem notificar os clientes ou encerrar o serviço para um número específico. Um tipo de fraude SIM envolve várias chamadas de Olá mesma identidade em torno Olá o mesmo tempo, mas em localizações geograficamente diferentes. toodetect este tipo de fraudes, Olá registos de telefone da empresa necessidades tooexamine recebidos e procure padrões específicos, neste caso, para chamadas efetuadas em torno Olá simultâneo em diferentes países. Os registos de telefone que inseridas nesta categoria são escritos toostorage para análise subsequente.

## <a name="prerequisites"></a>Pré-requisitos

Neste tutorial, irá simular dados de chamada telefónica através da utilização de uma aplicação de cliente que gera os metadados de chamada telefónica de exemplo. Alguns dos registos de Olá Olá aplicação produz o aspeto das chamadas fraudulentas. 

Antes de começar, certifique-se de que tem o seguinte Olá:

* Uma conta do Azure.
* aplicação do gerador de eventos de chamada de Olá. Pode obter esta transferindo Olá [TelcoGenerator.zip ficheiro](http://download.microsoft.com/download/8/B/D/8BD50991-8D54-4F59-AB83-3354B69C8A7E/TelcoGenerator.zip) de Olá Microsoft Download Center. Deszipe o pacote para uma pasta no seu computador. Se pretender que o código de origem do toosee Olá e aplicação Olá execução num depurador, pode obter o código de origem da aplicação Olá de [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator). 

    >[!NOTE]
    >Windows poderão bloquear o ficheiro. zip de Olá transferido. Se não é possível descomprimi-lo, clique no ficheiro de Olá e selecione **propriedades**. Se vir Olá mensagem "este ficheiro provém de outro computador e poderá ser bloqueado toohelp proteger neste computador", selecione de Olá **desbloqueio** opção e, em seguida, clique em **aplicar**.

Se pretender que os resultados de Olá tooexamine da tarefa de análise de transmissão em fluxo Olá, terá também uma ferramenta para visualizar conteúdo Olá de um contentor do Blob Storage do Azure. Se utilizar o Visual Studio, pode utilizar [ferramentas do Azure para Visual Studio](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) ou [Visual Studio Cloud Explorer](https://docs.microsoft.com/en-us/azure/vs-azure-tools-resources-managing-with-cloud-explorer). Em alternativa, pode instalar as ferramentas autónomas como [Explorador de armazenamento do Azure](http://storageexplorer.com/) ou [Explorador do Azure](http://www.cerebrata.com/products/azure-explorer/introduction). 

## <a name="create-an-azure-event-hubs-tooingest-events"></a>Criar um evento do Azure eventos de tooingest hubs

tooanalyze um fluxo de dados, *inserção* -lo no Azure. Dados de tooingest uma forma típico são toouse [Event Hubs do Azure](../event-hubs/event-hubs-what-is-event-hubs.md), que lhe permite ingestão de milhões de eventos por segundo e, em seguida, processar e armazenar informações de evento Olá. Para este tutorial, criar um hub de eventos e, em seguida, tiver Olá eventos de chamada gerador aplicação enviar chamada dados toothat hub de eventos. Para obter mais informações sobre os event hubs, consulte Olá [documentação do Service Bus do Azure](https://docs.microsoft.com/en-us/azure/service-bus/).

>[!NOTE]
>Para uma versão mais detalhada deste procedimento, consulte [criar um espaço de nomes de Event Hubs e um hub de eventos utilizando Olá portal do Azure](../event-hubs/event-hubs-create.md). 

### <a name="create-a-namespace-and-event-hub"></a>Criar um hub de espaço de nomes e eventos
Neste procedimento, tem primeiro de criar um espaço de nome de hub de eventos e, em seguida, adicionar um namepsace de toothat do hub de eventos. Espaços de nomes de hub de eventos são utilizados instâncias de barramento de eventos relacionados com o grupo toologically. 

1. Inicie sessão no portal do Azure de Olá e clique em **novo** > **Internet das coisas** > **Hub de eventos**. 

2. No Olá **criar espaço de nomes** painel, introduza um nome de espaço de nomes, como `<yourname>-eh-ns-demo`. Pode utilizar qualquer nome de espaço de nomes de Olá, mas Olá nome tem de ser válido para um URL e tem de ser exclusivo em todo o Azure. 
    
3. Selecionar uma subscrição e crie ou escolha um grupo de recursos e clique em **criar**. 

    ![Criar um espaço de nomes do hub de eventos](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-namespace-new-portal.png)
 
4. Quando o espaço de nomes de Olá tiver concluído a implementação, localize o espaço de nomes de hub de eventos de Olá na sua lista de recursos do Azure. 

5. Clique em novo Olá de espaço de nomes e, no painel de espaço de nomes de Olá, clique em  **+ &nbsp;Hub de eventos**. 

    ![botão Adicionar Hub de eventos de Olá para criar um novo hub de eventos ](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-button-new-portal.png)    
 
6. Nome Olá novo hub de eventos `sa-eh-frauddetection-demo`. Pode utilizar um nome diferente. Se o fizer, tome nota do mesmo, porque tem o nome de Olá mais tarde. Não precisa de tooset quaisquer outras opções para o hub de eventos de Olá neste momento.

    ![Painel para criar um novo hub de eventos](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-new-portal.png)
    
 
7. Clique em **Criar**.
### <a name="grant-access-toohello-event-hub-and-get-a-connection-string"></a>Conceda o hub de eventos do acesso toohello e obter uma cadeia de ligação

Antes de um processo pode enviar o hub de eventos de tooan de dados, o hub de eventos de Olá tem de ter uma política que permite o acesso adequado. política de acesso de Olá produz uma cadeia de ligação que inclui as informações de autorização.

1.  No painel de espaço de nomes de evento Olá, clique em **Event Hubs** e, em seguida, clique no nome de Olá do seu hub de eventos novos.

2.  No painel do hub de eventos de Olá, clique em **políticas de acesso partilhado** e, em seguida, clique em  **+ &nbsp;adicionar**.

    >[!NOTE]
    >Certifique-se de que está a trabalhar com o hub de eventos de Olá, não Olá event hub espaço de nomes.

3.  Adicionar uma política com o nome `sa-policy-manage-demo` e para **afirmação**, selecione **gerir**.

    ![Painel para criar uma nova política de acesso do hub de eventos](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-shared-access-policy-manage-new-portal.png)
 
4.  Clique em **Criar**.

5.  Após ter sido implementada a política de Olá, clique na mesma na lista de Olá de políticas de acesso partilhado.

6.  Caixa de Olá localizar etiquetada **chave primária de cadeia de ligação** e clique em Olá cópia no botão seguinte toohello cadeia de ligação. 
    
    ![Copiar a chave de cadeia de ligação principal Olá da política de acesso de Olá](./media/stream-analytics-real-time-fraud-detection/stream-analytics-shared-access-policy-copy-connection-string-new-portal.png)
 
7.  Cole a cadeia de ligação de Olá num editor de texto. Precisa esta cadeia de ligação para a secção seguinte Olá, depois de efetuar alguns tooit edições pequeno.

    cadeia de ligação de Olá tem o seguinte aspeto:

        Endpoint=sb://YOURNAME-eh-ns-demo.servicebus.windows.net/;SharedAccessKeyName=sa-policy-manage-demo;SharedAccessKey=Gw2NFZwU1Di+rxA2T+6hJYAtFExKRXaC2oSQa0ZsPkI=;EntityPath=sa-eh-frauddetection-demo

    Tenha em atenção que a cadeia de ligação de Olá contém vários pares chave-valor, separadas por ponto e vírgula: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, e `EntityPath`.  

## <a name="configure-and-start-hello-event-generator-application"></a>Configurar e iniciar a aplicação de gerador de evento Olá

Antes de iniciar a aplicação de TelcoGenerator Olá, configurá-lo de modo a que irá enviar hub eventos chamada registos toohello que acabou de criar.

### <a name="configure-hello-telcogeneratorapp"></a>Configurar Olá TelcoGeneratorapp

1.  No editor de olá onde copiou cadeia de ligação de Olá, anote Olá `EntityPath` valor e, em seguida, remova Olá `EntityPath` par (não se esqueça tooremove Olá ponto e vírgula que precede-lo). 

2.  Na pasta de olá onde que deszipada ficheiros de TelcoGenerator.zip Olá, abra o ficheiro de telcodatagen.exe.config Olá num editor. (Há mais de um ficheiro. config, por isso, certifique-se que abrir o direito de Olá um.)

3.  No Olá `<appSettings>` elemento, fazê-lo:

    * Defina o valor de Olá de Olá `EventHubName` o nome do hub de eventos da chave toohello (ou seja, o valor toohello do caminho de entidade Olá).
    * Defina o valor de Olá de Olá `Microsoft.ServiceBus.ConnectionString` toohello cadeia de ligação da chave. 

    Olá `<appSettings>` secção terá um aspeto semelhante Olá seguinte exemplo. (Para efeitos de clareza, iremos encapsulada linhas Olá e removido alguns carateres do token de autorização de Olá.)

    ![Ficheiro de configuração de aplicação TelcoGenerator Mostrar Olá event hub nome e a cadeia ligação](./media/stream-analytics-real-time-fraud-detection/stream-analytics-telcogenerator-config-file-app-settings.png)
 
4.  Guarde o ficheiro de Olá. 

### <a name="start-hello-app"></a>Iniciar a aplicação Olá
1.  Abra uma janela de comandos e altere toohello pasta em que Olá TelcoGenerator aplicação deszipada.
2.  Introduza Olá os seguintes comandos:

        telcodatagen.exe 1000 .2 2

    Olá parâmetros são: 

    * Número de CDRs por hora. 
    * Probabilidade de fraude de cartões SIM: Frequência, como uma percentagem de todas as chamadas, essa aplicação Olá deve simular uma chamada fraudulenta. o valor de Olá.2 significa que cerca de 20% dos registos de chamada de Olá procurará fraudulentas.
    * Duração em horas. número de Olá de horas que Olá aplicação deve ser executada. Também pode parar aplicação Olá qualquer altura ao premir Ctrl + C na linha de comandos Olá.

    Após alguns segundos, a aplicação Olá inicia a apresentar os registos de chamada telefónica no ecrã de Olá como envia-as toohello hub de eventos.

Alguns dos campos de chave Olá que irá utilizar nesta aplicação de deteção de fraudes em tempo real são seguinte Olá:

|**Registo**|**Definição**|
|----------|--------------|
|`CallrecTime`|Olá carimbo de hora de início de chamada de Olá. |
|`SwitchNum`|comutador de telefone Olá utilizado chamada de Olá tooconnect. Neste exemplo, comutadores Olá são cadeias que representam país Olá de origem (E.U.A., China, RU, Datacenters ou Austrália). |
|`CallingNum`|número de telefone de Olá de autor da chamada Olá. |
|`CallingIMSI`|Olá Mobile subscritor identidade IMSI (International). Este é o identificador exclusivo do Olá do autor da chamada Olá. |
|`CalledNum`|número de telefone de Olá de destinatário da chamada de Olá. |
|`CalledIMSI`|Identidade do subscritor móveis internacional (IMSI). Este é o identificador exclusivo do Olá do destinatário da chamada de Olá. |


## <a name="create-a-stream-analytics-job-toomanage-streaming-data"></a>Criar um toomanage de tarefa do Stream Analytics dados de transmissão em fluxo

Agora que tem um fluxo de eventos de chamada, pode configurar uma tarefa de Stream Analytics. tarefa de Olá irá ler os dados do hub de eventos de Olá que configurou. 

### <a name="create-hello-job"></a>Criar tarefa de Olá 

1. No portal do Azure Olá, clique em **novo** > **Internet das coisas** > **tarefa do Stream Analytics**.

2. Tarefa de Olá nome `sa_frauddetection_job_demo`, especifique uma subscrição, o grupo de recursos e a localização.

    É uma boa ideia tooplace Olá tarefa e Olá hub de eventos no Olá mesma região para melhor desempenho e que não paga tootransfer dados entre regiões.

    ![Criar nova tarefa de Stream Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-job-new-portal.png)

3. Clique em **Criar**.

    Olá tarefa é criada e portal Olá apresenta os detalhes da tarefa. Nada se encontra em execução, embora — tiver tarefa de Olá tooconfigure antes que possa ser iniciado.

### <a name="configure-job-input"></a>Configurar a entrada da tarefa

1. No dashboard de Olá ou Olá **todos os recursos** painel, localize e selecione Olá `sa_frauddetection_job_demo` tarefa do Stream Analytics. 
2. No Olá **tarefa topologia** secção Olá painel de tarefas do Stream Analytics, clique em Olá **entrada** caixa.

    ![Caixa de entrada em topologia no painel de tarefas de transmissão em fluxo análise Olá](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-input-box-new-portal.png)
 
3. Clique em  **+ &nbsp;adicionar** e, em seguida, preencha painel Olá com estes valores:

    * **Alias de entrada**: Utilize o nome de Olá `CallStream`. Se utilizar um nome diferente, tome nota do mesmo porque precisará dela mais tarde.
    * **Tipo de origem**: selecione **fluxo de dados**. (**Referência a dados** refere-se os dados de pesquisa de toostatic, que não irão utilizar neste tutorial.)
    * **Origem**: selecione **hub de eventos**.
    * **Opção de importar**: selecione **hub de eventos de utilização da subscrição atual**. 
    * **O espaço de nomes do Service bus**: selecione Olá event hub espaço de nomes que criou anteriormente (`<yourname>-eh-ns-demo`).
    * **Hub de eventos**: hub de eventos de Olá selecione que criou anteriormente (`sa-eh-frauddetection-demo`).
    * **Nome de política do hub de eventos**: selecione a política de acesso de Olá que criou anteriormente (`sa-policy-manage-demo`).

    ![Criar nova entrada para a tarefa de análise de transmissão em fluxo](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-input-new-portal.png)

4. Clique em **Criar**.

## <a name="create-queries-tootransform-real-time-data"></a>Criar consultas tootransform de dados em tempo real

Neste momento, tem uma tarefa de Stream Analytics configurar tooread um fluxo de dados de entrada. Olá passo seguinte consiste em toocreate uma transformação que analisa os dados de Olá em tempo real. Fazê-lo através da criação de uma consulta. Stream Analytics suporta um modelo de consulta simples e declarativo que descreve transformações de processamento em tempo real. consultas de Olá utilizam um idioma de como o SQL Server que tem alguma análise de toostream específico de extensões. 

Uma consulta muito simple simplesmente pode ler todos os dados de entrada de Olá. No entanto, muitas vezes, criar consultas que ter um aspeto de dados específicos ou relações nos dados de Olá. Nesta secção do tutorial Olá, irá criar e testar várias consultas toolearn algumas formas em que pode transformar um fluxo de entrada para análise. 

consultas Olá que criar aqui apenas irão apresentar o ecrã de toohello Olá dados transformados. Numa secção posterior, irá configurar um sink de saída e uma consulta que escreve Olá dados transformados toothat sink.

toolearn mais informações sobre idiomas de Olá, consulte Olá [referência de linguagem de consulta do Azure Stream Analytics](https://msdn.microsoft.com/library/dn834998.aspx).

### <a name="get-sample-data-for-testing-queries"></a>Obter dados de exemplo para consultas de teste

Olá TelcoGenerator aplicação está a enviar registos de chamada toohello hub de eventos e a tarefa de Stream Analytics é configurado tooread do hub de eventos de Olá. Pode utilizar uma consulta tootest Olá tarefa toomake certificar-se de que está a ler corretamente. teste demasiado uma consulta no Olá consola do Azure, terá de dados de exemplo. Nestas instruções, irá extrair dados de exemplo de uma sequência de Olá que estará disponível para o hub de eventos de Olá.

1. Certifique-se de que aplicações de TelcoGenerator Olá está a executar e a produzir registos de chamada.
2. No portal de Olá, devolva toohello painel de tarefas de análise de transmissão em fluxo. (Se tiver fechado painel Olá, procure `sa_frauddetection_job_demo` no Olá **todos os recursos** painel.)
3. Clique em Olá **consulta** caixa. Azure apresenta uma lista de entradas de Olá e saídas que estão configuradas para a tarefa de Olá e permite-lhe criar uma consulta que permite-lhe transformar o fluxo de entrada Olá, é enviado toohello saída.
4. No Olá **consulta** painel, clique em Olá pontos seguinte toohello `CallStream` de entrada e, em seguida, selecione **dados de entrada de exemplo**.

    ![Menu Opções toouse dados de exemplo de Olá entrada da tarefa de análise de transmissão em fluxo, com "Dados de exemplo de entrada" selecionados](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sample-data-from-input.png)

    Esta ação abre um painel que lhe permite especificar quanto tooget de dados de exemplo, definido em termos de quanto tooread Olá entrada fluxo.

5. Definir **minutos** too3 e, em seguida, clique em **OK**. 
    
    ![Opções para a amostragem Olá o fluxo de entrada, com "3 minutos" selecionados.](./media/stream-analytics-real-time-fraud-detection/stream-analytics-input-create-sample-data.png)

    Azure amostras de visão de 3 minutos de dados a partir do fluxo de entrada Olá e notifica-o quando os dados de exemplo de Olá estão prontos. (Esta ação demora algum.) 

dados de exemplo de Olá são temporariamente armazenados e estão disponíveis enquanto tiver janela de consulta Olá abrir. Se fechar a janela de consulta Olá, dados de exemplo de Olá são rejeitados e terá toocreate um novo conjunto de dados de exemplo. 

Como alternativa, pode obter um ficheiro. JSON que tenha dados de exemplo na mesma [a partir do GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/telco.json)e, em seguida, carregue esse toouse de ficheiro. JSON como dados de exemplo de Olá `CallStream` entrada. 

### <a name="test-using-a-pass-through-query"></a>Testar uma consulta pass-through

Se quiser tooarchive cada evento, pode utilizar uma consulta pass-through tooread todos os campos de Olá no payload Olá do evento de Olá.

1. Na janela de consulta Olá, introduza esta consulta:

        SELECT 
            *
        FROM 
            CallStream

    >[!NOTE]
    >Tal como acontece com o SQL Server, palavras-chave não são sensíveis a maiúsculas e minúsculas e espaços em branco não é significativo.

    Esta consulta, `CallStream` é Olá alias que especificou quando criou Olá entrada. Se utilizou um alias diferente, utilize esse nome em vez disso.

2. Clique em **teste**.

    tarefa de Stream Analytics Olá executa Olá consulta em relação a dados de exemplo de Olá e apresenta uma saída Olá em Olá parte inferior da janela de Olá. Isto indica que o hub de eventos de Olá e a tarefa de análise de transmissão em fluxo Olá estão corretamente configuradas. (Conforme indicado, mais tarde irá criar um sink de saída que Olá consulta pode escrever dados.)

    ![Tarefa de Stream Analytics uma saída, que mostra 73 registos gerados](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output.png)

    Olá exato diversas registos que vir dependerá registos quantos tiverem sido capturados num seu exemplo de 3 minutos.
 
### <a name="reduce-hello-number-of-fields-using-a-column-projection"></a>Reduzir o número de Olá de campos utilizando uma projeção de coluna

Em muitos casos, a análise não necessita de todas as colunas de Olá do fluxo de entrada Olá. Pode utilizar um tooproject consulta um conjunto mais pequeno de devolvidos os campos que na consulta pass-through Olá.

1. Consulta de Olá seguir de toohello Olá código editor de alteração:

        SELECT CallRecTime, SwitchNum, CallingIMSI, CallingNum, CalledNum 
        FROM 
            CallStream

2. Clique em **teste** novamente. 

    ![Tarefa de Stream Analytics uma saída de projeção, que mostra 25 registos gerados](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-projection.png)
 
### <a name="count-incoming-calls-by-region-tumbling-window-with-aggregation"></a>Contagem de receber chamadas por região: janela em cascata com agregação

Suponha que pretende que o número de Olá toocount de chamadas recebidas por região. Dados de transmissão em fluxo, se pretender que as funções de agregação tooperform como contar, terá de fluxo de Olá toosegment em unidades temporais (uma vez que o fluxo de dados de Olá em si é efetivamente endless). Fazê-lo utilizando uma análise de transmissão em fluxo [função de janela](stream-analytics-window-functions.md). Em seguida, pode trabalhar com dados de Olá dentro dessa janela como uma unidade.

Para esta transformação, pretende uma sequência de temporais windows que não se sobreponham — cada janela terá um conjunto de dados que pode agrupar e agregado discreto. Este tipo de janela é referenciado tooas um *janela em cascata* . Na janela em cascata de Olá, pode obter uma contagem de chamadas recebidas de Olá agrupados por `SwitchNum`, que representa o país olá onde chamada Olá teve origem. 

1. Consulta de Olá seguir de toohello Olá código editor de alteração:

        SELECT 
            System.Timestamp as WindowEnd, SwitchNum, COUNT(*) as CallCount 
        FROM
            CallStream TIMESTAMP BY CallRecTime 
        GROUP BY TUMBLINGWINDOW(s, 5), SwitchNum

    Esta consulta utiliza Olá `Timestamp By` palavra-chave na Olá `FROM` toospecify cláusula o campo que timestamp no Olá janela do fluxo toouse toodefine Olá em cascata de entrada. Neste caso, o janela Olá divide dados Olá em segmentos por Olá `CallRecTime` campo em cada registo. (Não se for especificado nenhum campo, operação de modos de janela Olá utiliza Olá hora que cada evento chegar ao hub de eventos de Olá. Consulte "Tempo Vs aplicação hora da chegada de" em [referência de linguagem de consulta de análise de sequência](https://msdn.microsoft.com/library/azure/dn834998.aspx). 

    projecção de Olá inclui `System.Timestamp`, que devolve um carimbo para o end Olá de cada janela. 

    toospecify que pretende que o toouse uma janela em cascata, utilizar Olá [TUMBLINGWINDOW](https://msdn.microsoft.com/library/dn835055.aspx) funcionar em Olá `GROUP BY `cláusula. Na função Olá, especifique uma unidade de tempo (em qualquer lugar a partir de um dia de tooa aos microssegundos) e um tamanho de janela (unidades quantos). Neste exemplo, janela em cascata de Olá consiste em intervalos de 5 segundos, pelo que irá obter uma contagem por país para visão de cada 5 segundos de chamadas.

2. Clique em **teste** novamente. Nos resultados de Olá, tenha em atenção que carimbos Olá em **WindowEnd** são em incrementos de 5 segundos.

    ![Tarefa de Stream Analytics uma saída de agregação, que mostra 13 registos gerados](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-aggregation.png)
 
### <a name="detect-sim-fraud-using-a-self-join"></a>Detetar fraude SIM através de uma associação automática

Neste exemplo, pode considerar a utilização fraudulenta toobe chamadas provenientes Olá mesmo utilizador, mas em diferentes localizações dentro de 5 segundos um do outro. Por exemplo, hello mesmo utilizador não é possível legitimamente efetuar uma chamada de Olá E.U.A. e da Austrália em Olá mesmo tempo. 

toocheck nestes casos, pode utilizar uma associação automática de Olá transmissão em fluxo de dados toojoin Olá tooitself de fluxo com base no Olá `CallRecTime` valor. Em seguida, pode ver para chamada regista onde hello `CallingIMSI` valor (Olá originadas número) é Olá mesmo, mas Olá `SwitchNum` valor (país de origem) não é Olá mesmo.

Quando utiliza uma associação com dados de transmissão em fluxo, a associação de Olá tem de fornecer Olá para que correspondam a linhas alguns limites podem ser separados no tempo. (Conforme indicado anteriormente, Olá dados de transmissão em fluxo é efetivamente endless.) limites de tempo de Olá para a relação de Olá são especificados no interior Olá `ON` cláusula de associação de Olá, utilizando Olá `DATEDIFF` função. Neste caso, a associação Olá baseia-se num intervalo de 5 segundos de dados de chamada.

1. Consulta de Olá seguir de toohello Olá código editor de alteração: 

        SELECT  System.Timestamp as Time, 
            CS1.CallingIMSI, 
            CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, 
            CS1.SwitchNum as Switch1, 
            CS2.SwitchNum as Switch2 
        FROM CallStream CS1 TIMESTAMP BY CallRecTime 
            JOIN CallStream CS2 TIMESTAMP BY CallRecTime 
            ON CS1.CallingIMSI = CS2.CallingIMSI 
            AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5 
        WHERE CS1.SwitchNum != CS2.SwitchNum

    Esta consulta é como qualquer associação do SQL Server, exceto Olá `DATEDIFF` função na União Olá. Esta é uma versão de `DATEDIFF` tooStreaming específico análise, e tem de aparecer no Olá `ON...BETWEEN` cláusula. parâmetros de Olá são uma unidade de tempo (segundos neste exemplo) e os aliases de Olá de duas origens de Olá para associar Olá. (Isto é diferente do Olá SQL padrão `DATEDIFF` função.) 

    Olá `WHERE` cláusula inclui condição Olá que sinalizadores chamada fraudulentas Olá: comutadores origem Olá não são Olá mesmo. 

2. Clique em **teste** novamente. 

    ![Tarefa de Stream Analytics uma saída de associação automática, que mostra 6 registos gerados](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-self-join.png)

3. Clique em **Guardar**. Isto poupa a consulta de associação automática Olá como parte da tarefa de análise de transmissão em fluxo Olá. (Se não guardar os dados de exemplo de Olá.)

    ![Guardar a tarefa de Stream Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-query-editor-save-button-new-portal.png)

## <a name="create-an-output-sink-toostore-transformed-data"></a>Criar dados de toostore transformado sink de saída

Definiu um fluxo de eventos, eventos de entrada tooingest do hub de eventos e uma consulta tooperform uma transformação através de fluxo de Olá. último passo de Olá é toodefine um sink de saída para a tarefa de Olá — ou seja, um Olá de toowrite local transformados fluxo para. 

Pode utilizar muitos recursos como saída sinks — uma base de dados do SQL Server, o table storage, armazenamento do Data Lake, Power BI e até mesmo outro hub de eventos. Para este tutorial, irá escrever Olá fluxo tooAzure Blob Storage, o que é uma escolha típica para recolher informações de eventos para análise posterior, uma vez que o se adapta a dados não estruturados.

Se tiver uma conta de armazenamento de blob existente, pode utilizar isso. Para este tutorial, vamos mostrar-lhe como toocreate um novo armazenamento conta apenas para este tutorial.

### <a name="create-an-azure-blob-storage-account"></a>Criar uma conta do Blob Storage do Azure

1. No portal do Azure Olá, devolva toohello painel de tarefas de análise de transmissão em fluxo. (Se tiver fechado painel Olá, procure `sa_frauddetection_job_demo` no Olá **todos os recursos** painel.)
2. No Olá **tarefa topologia** secção, clique em Olá **saída** caixa. 
3. No Olá **saídas** painel, clique em  **+ &nbsp;adicionar** e, em seguida, preencha painel Olá com estes valores:

    * **O alias de saída**: Utilize o nome de Olá `CallStream-FraudulentCalls`. 
    * **Sink**: selecione **armazenamento de BLOBs**.
    * **Importar opções**: selecione **armazenamento de BLOBs de utilização da subscrição atual**.
    * **Conta de armazenamento**. Selecione **criar nova conta de armazenamento.**
    * **Conta de armazenamento** (segunda caixa). Introduza `YOURNAMEsademo`, onde `YOURNAME` é o nome ou de outra cadeia exclusiva. nome de Olá pode utilizar apenas letras minúsculas e números, e tem de ser exclusivo em todo o Azure. 
    * **Contentor**. Introduza `sa-fraudulentcalls-demo`.
    o nome de conta do storage Olá e nome do contentor são tooprovide em conjunto utilizado um URI para armazenamento de BLOBs de Olá, como esta: 

    `http://yournamesademo.blob.core.windows.net/sa-fraudulentcalls-demo/...`
    
    ![Painel "Novo de saída" para a tarefa de Stream Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-output-blob-storage-new-console.png)
    
4. Clique em **Criar**. 

    O Azure cria a conta de armazenamento Olá e gera automaticamente uma chave. 

5. Fechar Olá **saídas** painel. 

## <a name="start-hello-streaming-analytics-job"></a>Iniciar a tarefa de análise de transmissão em fluxo Olá

tarefa de Olá está agora configurada. Já especificou uma entrada (hub de eventos de Olá), uma transformação (Olá toolook de consulta para chamadas fraudulentas) e um resultado (armazenamento de BLOBs). Agora pode iniciar a tarefa de Olá. 

1. Certifique-se a aplicação de TelcoGenerator Olá está em execução.

2. No painel de tarefas Olá, clique em **iniciar**.

    ![Iniciar a tarefa de Stream Analytics Olá](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-output.png)

3. No Olá **iniciar tarefa** painel, tarefa saída hora de início, selecione **agora**. 

4. Clique em **iniciar**. 

    ![Painel "Iniciar a tarefa" para a tarefa de Stream Analytics Olá](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-job-blade.png)

    Azure notifica-o quando a tarefa de Olá foi iniciado e, no painel de tarefas Olá, é apresentado o estado de Olá como **executar**.

    ![Tarefa de Stream Analytics Estado, mostrar "Em execução"](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-running-status.png)
    

## <a name="examine-hello-transformed-data"></a>Examine os dados de Olá transformado

Tem agora uma tarefa de transmissão em fluxo análise completa. tarefa Olá examinar um fluxo de metadados de chamada telefónica, à procura de chamadas telefónicas fraudulentas em tempo real e escrever informações sobre essas toostorage chamadas fraudulentas. 

toocomplete neste tutorial, é aconselhável toolook dados Olá que está a ser capturadas pela tarefa de análise de transmissão em fluxo Olá. dados Olá estão a ser escritos tooAzure blogue armazenamento segmentos (ficheiros). Pode utilizar qualquer ferramenta que lê o Blob Storage do Azure. Conforme indicado na secção pré-requisitos de Olá, pode utilizar extensões do Azure no Visual Studio, ou pode utilizar uma ferramenta como o [Explorador de armazenamento do Azure](http://storageexplorer.com/) ou [Explorador do Azure](http://www.cerebrata.com/products/azure-explorer/introduction). 

Ao examinar o conteúdo de Olá de um ficheiro no armazenamento de BLOBs, verá algo semelhante Olá seguinte:

![Armazenamento de Blobs do Azure com a análise de transmissão em fluxo de saída](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-blob-storage-view.png)
 

## <a name="clean-up-resources"></a>Limpar recursos

Temos de artigos adicionais que continuar com o cenário de deteção de fraudes Olá e que utilizam recursos Olá que criou neste tutorial. Se quiser toocontinue, consulte Sugestões Olá em **passos** mais tarde.

No entanto, se tiver terminado e não precisa de recursos de Olá que criou, pode eliminá-los para que poderá não pagar desnecessários do Azure. Nesse caso, sugerimos que Olá a seguir:

1. Pare a tarefa de análise de transmissão em fluxo de Olá. No Olá **tarefas** painel, clique em **parar** na parte superior do Olá.
2. Pare a aplicação de Telco gerador de Olá. Na janela de comando de olá onde começou aplicação Olá, prima Ctrl + C.
3. Se tiver criado uma nova conta de armazenamento de blob apenas para este tutorial, elimine-o. 
4. Elimine a tarefa de análise de transmissão em fluxo Olá.
5. Elimine o hub de eventos de Olá.
6. Elimine o espaço de nomes de hub de eventos de Olá.

## <a name="get-support"></a>Obter suporte

Para obter mais assistência, experimente a nossa [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passos seguintes

Pode continuar a este tutorial com Olá seguintes artigos:

* [Stream Analytics e o Power BI: um dashboard de análise em tempo real para dados de transmissão em fluxo](stream-analytics-power-bi-dashboard.md). Este artigo mostra como toosend Olá resultado TelCo Olá Stream Analytics tarefa tooPower BI para visualização em tempo real e análise.
* [Como toostore dados do Azure Stream Analytics numa Cache de Redis do Azure com as funções do Azure](stream-analytics-functions-redis.md). Este artigo mostra como toouse das funções do Azure toowrite fraudulenta chama tooan a cache de Redis do Azure através de uma fila do Service Bus.

Para obter mais informações sobre o Stream Analytics em geral, tente nestes artigos:

* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Tarefas de escala do Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência do idioma de consulta do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência de API do REST de gestão do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
