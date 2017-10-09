---
title: "aaaTroubleshooting Storage do Azure com o diagnóstico & Message Analyzer | Microsoft Docs"
description: "Um tutorial que demonstra ponto-a-ponto de resolução de problemas com a análise de armazenamento do Azure, o AzCopy e o Microsoft Message Analyzer"
services: storage
documentationcenter: dotnet
author: robinsh
manager: timlt
ms.assetid: 6b23cba5-0d53-439e-870b-de8e406107d8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 74ee126bab30b9a45f4904a065b6fe3006f76101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="end-to-end-troubleshooting-using-azure-storage-metrics-and-logging-azcopy-and-message-analyzer"></a>Resolução de problemas de ponto-a-ponto utilizando as métricas do Storage do Azure e o registo, o AzCopy e o Message Analyzer
[!INCLUDE [storage-selector-portal-e2e-troubleshooting](../../includes/storage-selector-portal-e2e-troubleshooting.md)]

## <a name="overview"></a>Descrição geral
Resolução de problemas e diagnosticar são uma chave skill para criar e suportar aplicações de cliente com o armazenamento do Microsoft Azure. Devido a natureza toohello distribuído de uma aplicação do Azure, diagnosticar e resolução de problemas de erros e problemas de desempenho podem ser mais complexos do que em ambientes tradicionais.

Neste tutorial, vamos demonstrar como cliente tooidentify determinados erros que possam afetar o desempenho e resolver os erros de ponto-a-ponto utilizando as ferramentas fornecidas pelo Microsoft e Storage do Azure, na aplicação de cliente do ordem toooptimize Olá.

Este tutorial fornece uma exploração prática de um cenário de resolução de problemas de ponto a ponto. Para aplicações de armazenamento do Azure tootroubleshooting um Guia conceptual aprofundada, consulte [monitorizar, diagnosticar e resolver problemas de armazenamento do Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="tools-for-troubleshooting-azure-storage-applications"></a>Ferramentas para resolução de problemas de aplicações de armazenamento do Azure
tootroubleshoot as aplicações de cliente utilizando o armazenamento do Microsoft Azure, pode utilizar uma combinação de ferramentas toodetermine quando ocorreu um problema e o que causa Olá problema Olá poderá ser. Estas ferramentas incluem:

* **Análise de armazenamento do Azure**. [Análise de armazenamento do Azure](http://msdn.microsoft.com/library/azure/hh343270.aspx) fornece métricas e registo para o Storage do Azure.

  * **As métricas do Storage** controla as métricas de transação e métricas de capacidade para a sua conta de armazenamento. Utilizar métricas, pode determinar como a aplicação está a funcionar de acordo com tooa diversas medidas diferentes. Consulte [armazenamento esquema da tabela de métricas de análise](http://msdn.microsoft.com/library/azure/hh343264.aspx) para obter mais informações sobre os tipos de Olá das métricas controladas pela análise de armazenamento.
  * **Registo de armazenamento** os registos de cada registo de toohello Storage do Azure serviços tooa lado do servidor do pedido. Olá registo controla dados detalhados para cada pedido, incluindo a operação de Olá efetuar Estado Olá operação Olá, e informações de latência. Consulte [formato de registo de análise do armazenamento](http://msdn.microsoft.com/library/azure/hh343259.aspx) para obter mais informações sobre os dados de pedido e resposta de Olá que são escritos toohello registos através da análise de armazenamento.

> [!NOTE]
> As contas de armazenamento com um tipo de replicação de com redundância de zona de armazenamento (ZRS) não dispõe de métricas de Olá ou capacidade de registo neste momento ativada.
>
>

* **Portal clássico do Azure**. Pode configurar as métricas e registo para a sua conta de armazenamento no Olá [Portal clássico do Azure](https://manage.windowsazure.com). Também pode ver gráficos e gráficos que mostram a forma como a aplicação está a efetuar ao longo do tempo e configurar toonotify alertas que se a aplicação executa de forma diferente que destinados para uma métrica especificada.

    Consulte [monitorizar uma conta de armazenamento no Portal do Azure de Olá](storage-monitor-storage-account.md) para obter informações sobre como configurar a monitorização no Olá Portal clássico do Azure.
* **AzCopy**. Registos do servidor para o Storage do Azure são armazenados como blobs, pelo que pode utilizar o AzCopy toocopy Olá blobs tooa local diretório de registo para análise com o Microsoft Message Analyzer. Consulte [transferir dados com o utilitário de linha de comandos do AzCopy Olá](storage-use-azcopy.md) para obter mais informações sobre o AzCopy.
* **Microsoft Message Analyzer**. Analisador de mensagens é uma ferramenta que consome os ficheiros de registo e apresenta dados de registo num formato visual que torna toofilter fácil, pesquisa e grupo registar dados para conjuntos útil que pode utilizar tooanalyze erros e problemas de desempenho. Consulte [Microsoft mensagem analisador operativo guia](http://technet.microsoft.com/library/jj649776.aspx) para obter mais informações sobre o Message Analyzer.

## <a name="about-hello-sample-scenario"></a>Sobre o cenário de exemplo de Olá
Para este tutorial, vamos examinar um cenário onde as métricas do Storage do Azure indica uma taxa de êxito de percentagem baixa para uma aplicação que chama o armazenamento do Azure. Olá métrica de taxa de êxito de percentagem baixa (apresentada como **PercentSuccess** Olá Portal clássico do Azure e nas tabelas de métricas de Olá) controla as operações que tenha êxito, mas que devolver um código de estado HTTP é superior ao 299. Nos ficheiros de registo de armazenamento do lado do servidor de Olá, estas operações são registadas com um Estado de transação de **ClientOtherErrors**. Para obter mais detalhes sobre a métrica de percentagem de êxito baixa Olá, consulte [métricas mostram PercentSuccess baixa ou entradas de registo de análise tem operações com o estado de transação de ClientOtherErrors](storage-monitoring-diagnosing-troubleshooting.md#metrics-show-low-percent-success).

Operações de armazenamento do Azure podem devolver os códigos de estado HTTP maior 299 como parte da respetiva funcionalidade normal. Mas estes erros em alguns casos indicam que que pode ser capaz de toooptimize a aplicação de cliente para um desempenho melhorado.

Neste cenário, iremos irá considerar um toobe de taxa de êxito de percentagem baixa nada inferior a 100%. Pode escolher um métrico um nível diferente, no entanto, de acordo com as necessidades de tooyour. Recomendamos que durante os testes da aplicação, estabeleça uma tolerância de linha de base para as métricas chave de desempenho. Por exemplo, poderá determinar, com base em testes, que a aplicação deve ter uma taxa de êxito de percentagem consistente de 90% ou 85%. Se os dados de métricas mostram que a aplicação Olá é deviating desse número, em seguida, pode investigar o que poderá estar a causar Olá aumento.

Para o nosso cenário de exemplo, uma vez que estabeleceu que métrica de taxa de êxito de percentagem de Olá é inferior a 100%, iremos irá examinar Olá registos toofind Olá erros correlacionar toohello métricas e utilizá-los toofigure saída que está a causar taxa de êxito de percentagem de inferior Olá. Vamos analisar especificamente erros no intervalo de 400 Olá. Em seguida, iremos irá investigar mais detalhadamente 404 erros (não for encontrado).

### <a name="some-causes-of-400-range-errors"></a>Algumas causas dos erros de intervalo de 400
Exemplos de Olá abaixo apresenta uma amostra de alguns erros de intervalo de 400 para pedidos para o Blob Storage do Azure e das suas causas possíveis. Qualquer um destes erros, bem como erros no intervalo de 300 Olá e o intervalo de 500 Olá, este pode contribuir tooa taxa de êxito de percentagem baixa.

Tenha em atenção que as listas de Olá abaixo longe concluída. Consulte [estado e códigos de erro](http://msdn.microsoft.com/library/azure/dd179382.aspx) para obter mais informações sobre erros gerais de armazenamento do Azure e sobre erros tooeach específicas dos serviços de armazenamento Olá.

**Exemplos de código 404 (não for encontrado) de estado**

Ocorre quando uma operação de leitura em relação a um contentor ou um blob falhará porque os BLOBs Olá ou contentor não foi encontrado.

* Ocorre se um contentor ou um blob foi eliminado por outro cliente antes deste pedido.
* Ocorre se estiver a utilizar uma chamada de API que cria o contentor de Olá ou um blob após verificar se existe. Olá CreateIfNotExists APIs tornar um cabeçalho chamar primeiro toocheck quanto à existência de Olá do contentor de Olá ou um blob; Se não existir, é devolvido um erro 404 e, em seguida, é efetuada uma chamada PUT segundo toowrite Olá contentor ou um blob.

**409 (conflito) Exemplos de código de estado**

* Ocorre se utilizar um toocreate de API de criar um novo contentor ou um blob, sem verificar primeiro existência e já existe um contentor ou um blob com esse nome.
* Ocorre se um contentor está a ser eliminado e tente toocreate um novo contentor com Olá antes de concluída a operação de eliminação de Olá o mesmo nome.
* Ocorre se especificar uma concessão no contentor ou blob e já houver uma concessão presente.

**Código de estado 412 (falhada de pré-condição) Exemplos**

* Ocorre quando a condição de Olá especificada por um cabeçalho condicional não foram cumprida.
* Ocorre quando o ID de concessão de Olá especificado não corresponde ao ID de concessão de Olá no contentor de Olá ou um blob.

## <a name="generate-log-files-for-analysis"></a>Gerar ficheiros de registo de Analysis Services
Neste tutorial, iremos utilizar Message Analyzer toowork com três tipos diferentes de ficheiros de registo, embora poderia escolher toowork com qualquer um dos seguintes:

* Olá **registo server**, que é criado quando ativar o registo de armazenamento do Azure. registo de servidor Olá contém dados sobre cada operação chamado dos serviços de armazenamento do Azure Olá – blob, fila, tabela e ficheiro. registo de servidor Olá indica que a operação foi chamada e o código de estado foi devolvidos, bem como outros detalhes sobre Olá pedido e resposta.
* Olá **registo de cliente .NET**, que é criado quando ativar o registo do lado do cliente de dentro da aplicação .NET. registo de cliente Olá inclui informações detalhadas sobre como Olá cliente prepara o pedido de Olá e recebe e processa Olá resposta.
* Olá **registo de rastreio de rede HTTP**, que recolhe dados de HTTP/HTTPS pedido e resposta de dados, incluindo para operações de armazenamento do Azure. Neste tutorial, iremos irá gerar o rastreio de rede Olá através do analisador de mensagens.

### <a name="configure-server-side-logging-and-metrics"></a>Configurar registo do lado do servidor e métricas
Em primeiro lugar, precisamos tooconfigure o registo de armazenamento do Azure e métricas de, pelo que temos dados a partir de tooanalyze de aplicação de cliente Olá. Pode configurar o registo e as métricas numa variedade de formas - através de Olá [Portal clássico do Azure](https://manage.windowsazure.com), utilizando o PowerShell, ou através de programação. Consulte [ativar as métricas do Storage e visualizar dados de métricas](http://msdn.microsoft.com/library/azure/dn782843.aspx) e [aceder aos dados de registo e ativar o registo de armazenamento](http://msdn.microsoft.com/library/azure/dn782840.aspx) para obter detalhes sobre como configurar o registo e as métricas.

**Olá, através do Portal clássico do Azure**

registo de tooconfigure e métricas para a conta de armazenamento com o portal de Olá, siga instruções de Olá em [monitorizar uma conta de armazenamento no Portal do Azure de Olá](storage-monitor-storage-account.md).

> [!NOTE]
> Não é possível tooset as métricas minuto utilizando Olá Portal clássico do Azure. No entanto, recomendamos que defina-las para efeitos deste tutorial Olá e para investigar problemas de desempenho com a sua aplicação. Pode definir métricas minutos através do PowerShell conforme mostrado abaixo, ou através de programação ou através de Olá Portal clássico do Azure.
>
> Tenha em atenção que Olá Portal clássico do Azure não é possível a apresentação das métricas minutos, apenas as métricas por hora.
>
>

**Através do PowerShell**

tooget iniciado com o PowerShell para o Azure, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

1. Olá utilize [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0) cmdlet tooadd toohello janela do PowerShell da conta de utilizador do Azure:

    ```powershell
     Add-AzureAccount
    ```

2. No Olá **sessão tooMicrosoft Azure** janela, endereço de correio eletrónico do tipo Olá e palavra-passe associada à sua conta. Azure autentica guarda as informações de credencial de Olá e, em seguida, fecha a janela de Olá.
3. Definir Olá conta toohello armazenamento conta do storage predefinida que estiver a utilizar para o tutorial Olá executando estes comandos numa janela do PowerShell Olá:

    ```powershell
    $SubscriptionName = 'Your subscription name'
    $StorageAccountName = 'yourstorageaccount'
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

4. Ative o registo para Olá serviço Blob de armazenamento:

    ```powershell
    Set-AzureStorageServiceLoggingProperty -ServiceType Blob -LoggingOperations Read,Write,Delete -PassThru -RetentionDays 7 -Version 1.0
    ```

5. Ativar as métricas do storage para Olá serviço Blob, tornando tooset se **- MetricsType** demasiado`Minute`:

    ```powershell
    Set-AzureStorageServiceMetricsProperty -ServiceType Blob -MetricsType Minute -MetricsLevel ServiceAndApi -PassThru -RetentionDays 7 -Version 1.0
    ```

### <a name="configure-net-client-side-logging"></a>Configurar o registo do .NET do lado do cliente
tooconfigure do lado do cliente registo para uma aplicação .NET, ative os diagnósticos de .NET no ficheiro de configuração da aplicação Olá (Web. config ou App. config). Consulte [do lado do cliente registo com Olá biblioteca de clientes do Storage .NET](http://msdn.microsoft.com/library/azure/dn782839.aspx) e [do lado do cliente registo com Olá SDK de armazenamento do Microsoft Azure para Java](http://msdn.microsoft.com/library/azure/dn782844.aspx) para obter mais detalhes.

registo do lado do cliente de Olá inclui informações detalhadas sobre como Olá cliente prepara o pedido de Olá e recebe e processa Olá resposta.

Olá biblioteca de clientes de armazenamento armazena dados de registo do lado do cliente na localização de Olá especificada no ficheiro de configuração da aplicação Olá (Web. config ou App. config).

### <a name="collect-a-network-trace"></a>Recolher um rastreio de rede
Pode utilizar o Message Analyzer toocollect um rastreio de rede HTTP/HTTPS enquanto a aplicação de cliente está em execução. Utiliza analisador de mensagens [Fiddler](http://www.telerik.com/fiddler) no Olá back-end. Antes de recolher o rastreio de rede Olá, recomendamos que configure o Fiddler toorecord não encriptada HTTPS tráfego:

1. Instalar [Fiddler](http://www.telerik.com/download/fiddler).
2. Inicie o Fiddler.
3. Selecione **ferramentas | Opções de fiddler**.
4. Na caixa de diálogo Opções Olá, certifique-se de que **capturar liga-se de HTTPS** e **desencriptar o tráfego HTTPS** estão ambos selecionadas, conforme mostrado abaixo.

![Configurar opções de Fiddler](./media/storage-e2e-troubleshooting-classic-portal/fiddler-options-1.png)

Para tutorial Olá, recolher e guardar um rastreio de rede pela primeira vez em Message Analyzer, em seguida, criar um rastreio de Olá do Analysis Services sessão tooanalyze e Olá registos. um rastreio de rede Message Analyzer toocollect:

1. No Message Analyzer, selecione **ficheiro | Rastreio rápido | Não encriptada HTTPS**.
2. rastreio de Olá começará imediatamente. Selecione **parar** toostop Olá rastreio para que podemos configurá-lo apenas o tráfego de armazenamento tootrace.
3. Selecione **editar** sessão de rastreio de Olá tooedit.
4. Selecione Olá **configurar** ligação toohello à direita dos Olá **Microsoft-Pef-WebProxy** fornecedor ETW.
5. No Olá **definições avançadas** caixa de diálogo, clique em Olá **fornecedor** separador.
6. No Olá **Hostname filtro** campo, especifique os pontos finais de armazenamento, separados por espaços. Por exemplo, pode especificar pontos finais da sua forma; alterar `storagesample` toohello nome da conta de armazenamento:

    ```   
    storagesample.blob.core.windows.net storagesample.queue.core.windows.net storagesample.table.core.windows.net
    ```

7. Sair da caixa de diálogo Olá e clique em **reiniciar** toobegin recolher rastreio Olá com filtro de nome de anfitrião Olá no local, para que apenas tráfego de rede de armazenamento do Azure está incluído no rastreio Olá.

> [!NOTE]
> Depois de concluída a recolha de rastreio de rede, recomendamos vivamente que reverter as definições de Olá que pode ter sido alterado no tráfego HTTPS de toodecrypt Fiddler. Na caixa de diálogo de opções de Fiddler Olá, desmarque Olá **capturar liga-se de HTTPS** e **desencriptar o tráfego HTTPS** caixas de verificação.
>
>

Consulte [utilizar funcionalidades de rastreio de rede de Olá](http://technet.microsoft.com/library/jj674819.aspx) na Technet para obter mais detalhes.

## <a name="review-metrics-data-in-hello-azure-classic-portal"></a>Reveja os dados de métricas em Olá Portal clássico do Azure
Assim que a aplicação tem estado em execução durante um período de tempo, pode rever os gráficos de métricas de Olá que aparecem no Olá tooobserve de Portal clássico do Azure como o seu serviço tem sido executar. Em primeiro lugar, vamos adicionar Olá **percentagem de êxito** toohello métrica monitorização página:

1. Navegue toohello Dashboard para a sua conta de armazenamento no Olá [Portal clássico do Azure](https://manage.windowsazure.com), em seguida, selecione **Monitor** Olá tooview monitorização página.
2. Clique em **adicionar métricas** toodisplay Olá **escolha métricas** caixa de diálogo.
3. Desloque para baixo toofind Olá **percentagem de êxito** grupo, expanda-lo, em seguida, selecione **agregado**, conforme mostrado na imagem de Olá abaixo. Esta métrica agrega dados de percentagem de êxito de todas as operações de Blob.

![Escolha as métricas](./media/storage-e2e-troubleshooting-classic-portal/choose-metrics-portal-1.png)

No Portal clássico do Azure Olá, agora verá **percentagem de êxito** no gráfico de monitorização de Olá, juntamente com quaisquer outras métricas que possa ter adicionado (cópia de segurança toosix podem ser apresentadas no gráfico de Olá de uma só vez). Imagem de Olá abaixo, pode ver que essa taxa de êxito de percentagem de Olá é um pouco inferior a 100%, o que é o cenário de Olá que vai investigar junto ao analisar registos de Olá no analisador de mensagens:

![Gráfico de métricas no portal](./media/storage-e2e-troubleshooting-classic-portal/portal-metrics-chart-1.png)

Para obter mais detalhes sobre como adicionar página de monitorização de toohello métricas, consulte [como: adicionar a tabela de métricas de toohello métricas](storage-monitor-storage-account.md#add-metrics-charts-to-the-portal-dashboard).

> [!NOTE]
> Pode demorar algum tempo para a sua tooappear de dados de métricas no Portal clássico do Azure de Olá depois de ativar as métricas do storage. Isto acontece porque as métricas de hora a hora para Olá hora anterior não são apresentadas no Olá Portal clássico do Azure até Olá hora atual tiver decorrido. Além disso, as métricas de minutos não são apresentadas no Olá Portal clássico do Azure. Por isso, consoante o quando ativar métricas, pode demorar dos dados de métricas tootwo horas toosee.
>
>

## <a name="use-azcopy-toocopy-server-logs-tooa-local-directory"></a>Utilizar o AzCopy toocopy servidor registos tooa diretório local
Armazenamento do Azure escreve tooblobs de dados de registo do servidor, enquanto as métricas são escritas tootables. Os blobs de registo estão disponíveis no Olá conhecido `$logs` contentor para a sua conta de armazenamento. Registo blobs são denominados hierárquica por ano, mês, dia e hora, para que possa localizar facilmente intervalo Olá de tempo que pretende tooinvestigate. Por exemplo, no Olá `storagesample` conta, contentor Olá para blobs de registo de Olá para 02/01/2015, de 8-09: 00, é `https://storagesample.blob.core.windows.net/$logs/blob/2015/01/08/0800`. os blobs neste contentor individuais Olá são denominados sequencialmente, começando com `000000.log`.

Pode utilizar toodownload de ferramenta da linha de comandos do AzCopy Olá estes localização de tooa de ficheiros de registo do lado do servidor da sua preferência no seu computador local. Por exemplo, pode utilizar Olá os seguintes ficheiros de registo do comando toodownload Olá para operações de BLOBs que demoraram colocar em 2 de Janeiro de 2015 toohello pasta `C:\Temp\Logs\Server`; substituir `<storageaccountname>` com o nome de Olá da sua conta do storage e `<storageaccountkey>` com o chave de acesso da conta:

```azcopy
AzCopy.exe /Source:http://<storageaccountname>.blob.core.windows.net/$logs /Dest:C:\Temp\Logs\Server /Pattern:"blob/2015/01/02" /SourceKey:<storageaccountkey> /S /V
```

AzCopy está disponível para transferência no Olá [Azure transfere](https://azure.microsoft.com/downloads/) página. Para obter mais informações sobre como utilizar o AzCopy, consulte [transferir dados com o utilitário de linha de comandos do AzCopy Olá](storage-use-azcopy.md).

Para obter informações adicionais sobre a transferir os registos do lado do servidor, consulte [registo do armazenamento de transferência de dados de registo](http://msdn.microsoft.com/library/azure/dn782840.aspx#DownloadingStorageLogginglogdata).

## <a name="use-microsoft-message-analyzer-tooanalyze-log-data"></a>Utilizar dados de registo do Microsoft Message Analyzer tooanalyze
Microsoft Message Analyzer é uma ferramenta para capturar, visualizar e analisar o tráfego, eventos e outras mensagens de sistema ou aplicação em cenários de resolução de problemas e diagnóstico de mensagens de protocolo. Analisador de mensagens também permite-lhe tooload, agregação e analisar dados de registo e guardar ficheiros de rastreio. Para obter mais informações sobre o Message Analyzer, consulte [Microsoft mensagem analisador operativo guia](http://technet.microsoft.com/library/jj649776.aspx).

Analisador de mensagens inclui recursos para o armazenamento do Azure que o ajudam a tooanalyze servidor, cliente e registos de rede. Nesta secção, vamos abordar como toouse tooaddress essas ferramentas Olá problema de sucesso percentagem baixo no Olá os registos de armazenamento.

### <a name="download-and-install-message-analyzer-and-hello-azure-storage-assets"></a>Transfira e instale o Message Analyzer e Olá recursos de armazenamento do Azure
1. Transferir [Message Analyzer](http://www.microsoft.com/download/details.aspx?id=44226) de Olá Microsoft Download Center, e execute o instalador de Olá.
2. Inicie o analisador de mensagens.
3. De Olá **ferramentas** menu, selecione **Gestor do Asset Intelligence**. No Olá **Gestor do Asset Intelligence** caixa de diálogo, selecione **transfere**, em seguida, filtre **Storage do Azure**. Irá ver recursos de armazenamento de Azure Olá, conforme mostrado na imagem de Olá abaixo.
4. Clique em **sincronização todos os itens apresentados** tooinstall Olá recursos de armazenamento do Azure. recursos disponíveis Olá incluem:
   * **Regras de cor de armazenamento do Azure:** as regras de cor de armazenamento do Azure permitem-lhe toodefine filtros especiais que utilizam a cor de texto, e toohighlight mensagens que contêm informações específicas num rastreio de estilos de tipo de letra.
   * **Gráficos de armazenamento do Azure:** gráficos de armazenamento do Azure são gráficos predefinidos que graph dados de registo do servidor. Tenha em atenção que toouse gráficos de armazenamento do Azure neste momento, pode apenas carga Olá registo do servidor para Olá grelha de análise.
   * **Parsers de armazenamento do Azure:** hello do cliente do Storage do Azure parsers parse Olá Storage do Azure, o servidor e o HTTP inicia sessão na ordem toodisplay-los no Olá grelha de análise.
   * **Filtros de armazenamento do Azure:** filtros de armazenamento do Azure são critérios predefinidos que pode utilizar tooquery os dados no Olá grelha de análise.
   * **Esquemas de vista de armazenamento do Azure:** esquemas de vista de armazenamento do Azure são esquemas de coluna predefinida e os agrupamentos no Olá grelha de análise.
5. Reinicie o Message Analyzer depois de instalar ativos Olá.

![Gestor do Asset Intelligence de analisador de mensagens](./media/storage-e2e-troubleshooting-classic-portal/mma-start-page-1.png)

> [!NOTE]
> Instale todos os recursos de armazenamento do Azure Olá mostrados para fins de Olá deste tutorial.
>
>

### <a name="import-your-log-files-into-message-analyzer"></a>Importar os ficheiros de registo para o Message Analyzer
Pode importar todos os seus ficheiros de registo guardado (do lado do servidor, do lado do cliente e rede) para uma única sessão no Microsoft Message Analyzer para análise.

1. No Olá **ficheiro** menu no Microsoft Message Analyzer, clique em **nova sessão**e, em seguida, clique em **sessão em branco**. No Olá **nova sessão** caixa de diálogo, introduza um nome para a sua sessão do Analysis Services. No Olá **detalhes da sessão** painel, clique em Olá **ficheiros** botão.
2. tooload Olá rede rastreio dados gerados por Message Analyzer, clique em **adicionar ficheiros**, procure a localização de toohello onde guardou o ficheiro .matp da sua sessão de rastreio web, ficheiro de .matp selecione Olá, e clique em **abrir**.
3. dados de registo do lado do servidor do tooload Olá, clique em **adicionar ficheiros**, procure a localização de toohello onde transferiu os registos do lado do servidor, selecione os ficheiros de registo de Olá para o intervalo de tempo de Olá pretende tooanalyze e clique em **abrir**. Em seguida, no Olá **detalhes da sessão** painel, conjunto Olá **configuração de registo de texto** pendente para cada ficheiro de registo do lado do servidor demasiado**AzureStorageLog** tooensure pela Microsoft Analisador de mensagens pode analisar o ficheiro de registo Olá corretamente.
4. dados de registo do lado do cliente do tooload Olá, clique em **adicionar ficheiros**, procure a localização de toohello onde guardou os registos do lado do cliente, selecione os ficheiros de registo de Olá pretende tooanalyze e clique em **abra**. Em seguida, no Olá **detalhes da sessão** painel, conjunto Olá **configuração de registo de texto** pendente para cada ficheiro de registo do lado do cliente demasiado**AzureStorageClientDotNetV4** tooensure que Microsoft Message Analyzer pode analisar o ficheiro de registo Olá corretamente.
5. Clique em **iniciar** no Olá **nova sessão** diálogo tooload e análise Olá dados de registo. Apresenta dados de registo Olá no Olá grelha de análise do analisador de mensagens.

imagem de Olá abaixo mostra uma sessão de exemplo configurada com o servidor, cliente e os ficheiros de registo de rastreio de rede.

![Configurar sessão do analisador de mensagens](./media/storage-e2e-troubleshooting-classic-portal/configure-mma-session-1.png)

Tenha em atenção que o Message Analyzer carrega os ficheiros de registo na memória. Se tiver um grande conjunto de dados de registo, é melhor toofiltê-lo na ordem tooget Olá melhor desempenho do analisador de mensagens.

Em primeiro lugar, determine o período de tempo de Olá que está interessado em rever e manter este período de tempo tão reduzida quanto possível. Em muitos casos, é aconselhável tooreview um período de minutos ou horas no máximo. Importar mais pequeno conjunto de Olá de registos que pode satisfazer as suas necessidades.

Se ainda tiver uma grande quantidade de dados de registo, em seguida, poderá ser útil toospecify um toofilter de filtro da sessão os dados de registo antes que o carregamento. No Olá **sessão filtro** caixa, selecione de Olá **biblioteca** botão toochoose um filtro predefinido; por exemplo, escolha **Global tempo filtro I** de Olá filtros de armazenamento do Azure toofilter num intervalo de tempo. Em seguida, pode editar Olá toospecify Olá filtro critérios inicial e final timestamp para o intervalo de Olá pretende toosee. Pode também filtrar por um código de estado específico; Por exemplo, pode escolher tooload apenas entradas de registo em que o código de estado de Olá é 404.

Para obter mais informações sobre como importar dados de registo para o Microsoft Message Analyzer, consulte [obter dados de mensagens](http://technet.microsoft.com/library/dn772437.aspx) no TechNet.

### <a name="use-hello-client-request-id-toocorrelate-log-file-data"></a>Utilizar pedido de cliente de Olá ID dados de ficheiro de registo de toocorrelate
Olá biblioteca de clientes do Storage do Azure gera automaticamente um ID de pedido de cliente exclusivos para cada pedido. Este valor é escrito toohello registo de cliente, o registo de servidor Olá e o rastreio de rede Olá, pelo que pode utilizar este toocorrelate dados em todos os registos de três dentro do analisador de mensagens. Consulte [ID do pedido de cliente](storage-monitoring-diagnosing-troubleshooting.md#client-request-id) para obter informações adicionais sobre o cliente de Olá pedir ID.

secções Olá abaixo descrevem como toouse pré-configurados e vistas de esquema personalizadas toocorrelate e o grupo de dados com base no pedido do cliente Olá ID.

### <a name="select-a-view-layout-toodisplay-in-hello-analysis-grid"></a>Selecione um toodisplay de esquema de vista Olá grelha de análise
Recursos de armazenamento Olá para Message Analyzer incluem esquemas de vista de armazenamento de Azure, que são vistas pré-configuradas que pode utilizar toodisplay os dados com agrupamentos útil e colunas para diferentes cenários. Também pode criar esquemas de vista personalizada e guardá-las para serem reutilizadas.

imagem de Olá abaixo mostra Olá **esquema de vista** menu, disponível selecionando **esquema de vista** do Friso de barra de ferramentas de Olá. esquemas de vista de Olá para armazenamento do Azure estão agrupadas em Olá **Storage do Azure** no menu de Olá nó. Pode procurar `Azure Storage` no Olá toofilter de caixa de pesquisa no armazenamento do Azure ver apenas os esquemas. Também pode selecionar Olá estrela seguinte tooa Vista esquema toomake it um favorito e apresentá-lo, Olá parte superior do menu de Olá.

![Visualizar o menu de esquema](./media/storage-e2e-troubleshooting-classic-portal/view-layout-menu.png)

toobegin com selecione **agrupados por ClientRequestID e módulo**. Grupos de esquema esta vista de registo dados a partir de todos os registos de três primeiro por ID de pedido de cliente, em seguida, ao ficheiro de registo de origem (ou **módulo** no Message Analyzer). Com esta vista, pode desagregar um ID de pedido de cliente específico e ver os dados todos os três ficheiros de registo para esse pedido de cliente ID.

imagem de Olá abaixo mostra estas vista aplicada toohello exemplo registo dados de esquema, com um subconjunto de colunas apresentadas. Pode ver que um ID de pedido de cliente específico, Olá Analysis grelha apresenta dados de registo de cliente Olá, registo de servidor e de rastreio de rede.

![Esquema de vista de armazenamento do Azure](./media/storage-e2e-troubleshooting-classic-portal/view-layout-client-request-id-module.png)

> [!NOTE]
> Ficheiros de registo diferentes têm colunas diferentes, pelo que, quando os dados de vários ficheiros de registo são apresentados na grelha de análise de Olá, algumas colunas não podem conter quaisquer dados para uma linha fornecida. Por exemplo, a imagem de Olá acima, as linhas de registo de cliente não mostram todos os dados para Olá **Timestamp**, **TimeElapsed**, **origem**, e **destino** colunas, porque estas colunas não existe no registo de cliente Olá, mas existe no rastreio de rede Olá. Da mesma forma, Olá **Timestamp** coluna apresenta dados de carimbo do registo de servidor Olá, mas não existem dados são apresentados para Olá **TimeElapsed**, **origem**, e  **Destino** colunas, o que não façam parte do registo de hello do servidor.
>
>

Além disso toousing esquemas de vista de armazenamento do Azure Olá, também pode definir e guarde as seus próprios esquemas de vista. Pode selecionar outros campos para agrupar dados pretendidos e guardar o agrupamento de Olá como parte do seu esquema de personalizado.

### <a name="apply-color-rules-toohello-analysis-grid"></a>Aplicar regras de cor toohello grelha de análise
Recursos de armazenamento Olá também incluir regras de cor, o que oferecem que um visual significa tooidentify diferentes tipos de erros no Olá grelha de análise. Olá as regras de cor predefinida aplicam tooHTTP erros, pelo que aparecem apenas para o rastreio Olá do registo e da rede.

as regras de cor tooapply, selecione **as regras de cor** do Friso de barra de ferramentas de Olá. Verá as regras de cor de armazenamento do Azure Olá no menu de Olá. Tutorial de Olá, selecione **erros de cliente (StatusCode compreendido entre 400 e 499)**, conforme mostrado na imagem de Olá abaixo.

![Esquema de vista de armazenamento do Azure](./media/storage-e2e-troubleshooting-classic-portal/color-rules-menu.png)

Além disso toousing Olá Storage do Azure cor regras, também pode definir e guardar as suas próprias regras de cor.

### <a name="group-and-filter-log-data-toofind-400-range-errors"></a>Grupo e filtro de registo de erros de 400-intervalo de toofind de dados
Em seguida, vamos grupo e filtrar toofind de dados de registo Olá todos os erros no intervalo de Olá 400.

1. Localizar Olá **StatusCode** coluna na Olá grelha de análise, contexto Olá coluna cabeçalho e selecione **grupo**.
2. Em seguida, grupo no Olá **ClientRequestId** coluna. Verá que dados Olá Olá que Analysis grelha agora está organizada por Estado de código e a pedido do cliente ID.
3. Apresentar a janela de ferramenta de filtro de vista de Olá se já não for apresentado. No Friso da barra de ferramentas de Olá, selecione **ferramenta Windows**, em seguida, **vista filtro**.
4. toofilter Olá dados toodisplay apenas 400-intervalo erros do registo, adicionar Olá seguir toohello de critérios de filtro **vista filtro** janela e clique em **aplicar**:

    ```   
    (AzureStorageLog.StatusCode >= 400 && AzureStorageLog.StatusCode <=499) || (HTTP.StatusCode >= 400 && HTTP.StatusCode <= 499)
    ```

imagem de Olá abaixo mostra os resultados de Olá este agrupamento e o filtro. Expansão Olá **ClientRequestID** campo abaixo Olá agrupamento para o código de estado 409, por exemplo, mostra uma operação que resultaram nesse código de estado.

![Esquema de vista de armazenamento do Azure](./media/storage-e2e-troubleshooting-classic-portal/400-range-errors1.png)

Depois de aplicar este filtro, verá que as linhas de registo de cliente Olá são excluídas, como Olá o registo de cliente não inclui um **StatusCode** coluna. toobegin com, iremos irá rever servidor Olá e 404 erros de toolocate registos de rastreio de rede e, em seguida, iremos devolver toohello registo tooexamine Olá cliente operações de cliente que conduziram toothem.

> [!NOTE]
> Pode filtrar por Olá **StatusCode** coluna ainda apresentar dados e de todos os registos de três, incluindo Olá registo de cliente, se adicionar um filtro de toohello expressão que inclui entradas de registo em que o código de estado de Olá é nulo. tooconstruct nesta expressão de filtro, utilize:
>
> <code>&#42;StatusCode >= 400 or !&#42;StatusCode</code>
>
> Este filtro devolve todas as linhas a partir do cliente de Olá registo e apenas as linhas de registo do servidor de Olá e registo HTTP onde o código de estado de Olá é maior do que 400. Se aplicar este esquema de vista toohello agrupada por ID de pedido de cliente e o módulo, pode procurar ou deslocamento através de Olá iniciar sessão entradas toofind aqueles onde todos os registos de três são representados.   
>
>

### <a name="filter-log-data-toofind-404-errors"></a>Registar dados toofind 404 erros de filtro
Recursos de armazenamento Olá incluem filtros predefinidos que pode utilizar erros de Olá toonarrow registo dados toofind ou tendências que procura. Em seguida, iremos irá aplicar dois filtros predefinidos: que filtra o servidor de Olá e registos de rastreio de rede 404 erros e, que filtra os dados de Olá um intervalo de tempo especificado.

1. Apresentar a janela de ferramenta de filtro de vista de Olá se já não for apresentado. No Friso da barra de ferramentas de Olá, selecione **ferramenta Windows**, em seguida, **vista filtro**.
2. Na janela de vista filtro Olá, selecione **biblioteca**e uma procura `Azure Storage` Olá toofind filtros de armazenamento do Azure. O filtro para selecionar Olá **404 (não for encontrado) de mensagens em todos os registos**.
3. Olá apresentar **biblioteca** menu novo e localize e selecione Olá **filtro de tempo Global**.
4. Edite os carimbos de Olá mostrados no intervalo de toohello de filtro de Olá que desejar tooview. Isto irá ajudar toonarrow intervalo Olá tooanalyze de dados.
5. O filtro deve aparecer semelhante exemplo toohello abaixo. Clique em **aplicar** tooapply Olá filtro toohello grelha de análise.

    ```   
    ((AzureStorageLog.StatusCode == 404 || HTTP.StatusCode == 404)) And
    (#Timestamp >= 2014-10-20T16:36:38 and #Timestamp <= 2014-10-20T16:36:39)
    ```

![Esquema de vista de armazenamento do Azure](./media/storage-e2e-troubleshooting-classic-portal/404-filtered-errors1.png)

### <a name="analyze-your-log-data"></a>Analisar os dados de registo
Agora que tem agrupados e filtrar os dados, pode examinar os detalhes de Olá dos pedidos individuais que geraram 404 erros. Esquema de vista atual Olá, os dados de Olá são agrupados por ID de pedido de cliente, em seguida, pela origem de registo. Uma vez que vamos está a filtrar nos pedidos em que o campo de StatusCode Olá contém 404, iremos ver apenas servidor Olá e os dados de rastreio de rede, não Olá cliente dados de registo.

imagem de Olá abaixo mostra um pedido específico em que uma operação de Blob obter geraram um 404 porque blob Olá não existe. Tenha em atenção que algumas colunas foram removidas da visualização padrão Olá dados relevantes do ordem toodisplay Olá.

![Servidor filtrado e registos de rastreio de rede](./media/storage-e2e-troubleshooting-classic-portal/server-filtered-404-error.png)

Em seguida, iremos irá correlacionar este ID de pedido de cliente com toosee de dados de registo de cliente Olá o cliente de Olá ações estava a demorar quando ocorreu um erro de Olá. Pode visualizar uma nova vista de grelha de análise para estas sessão tooview Olá cliente dados de registo, que abre num separador segundo:

1. Em primeiro lugar, copie o valor de Olá da Olá **ClientRequestId** área de transferência do campo toohello. Pode fazer isto, selecionando a linha, localizar Olá **ClientRequestId** campo, clicar no valor de dados de Olá e escolher **cópia 'ClientRequestId'**.
2. No Friso da barra de ferramentas de Olá, selecione **novo Visualizador**, em seguida, selecione **Analysis grelha** tooopen um novo separador. Olá novo separador mostra todos os dados nos seus ficheiros de registo, sem agrupamento, filtragem ou as regras de cor.
3. No Friso da barra de ferramentas de Olá, selecione **esquema de vista**, em seguida, selecione **todas as colunas de cliente .NET** em Olá **Storage do Azure** secção. Este esquema de vista apresenta dados de registo de cliente Olá, bem como Olá registos de rastreio do servidor e da rede. Por predefinição é ordenada na Olá **MessageNumber** coluna.
4. Em seguida, procure o registo de cliente Olá ID de pedido de cliente para Olá. No Friso da barra de ferramentas de Olá, selecione **localizar mensagens**, em seguida, especifique um filtro personalizado no ID de pedido de cliente Olá no Olá **localizar** campo. Utilize esta sintaxe de filtro de Olá, especificando o seu próprio ID do pedido de cliente:

    ```  
    *ClientRequestId == "398bac41-7725-484b-8a69-2a9e48fc669a"
    ```

Analisador de mensagens localiza e seleciona Olá primeiro entrada de registo em que os critérios de pesquisa de Olá corresponde ao ID de pedido de cliente para Olá. No registo de cliente Olá, existem várias entradas para cada ID de pedido de cliente, pelo que poderá ser útil toogroup-las em Olá **ClientRequestId** campo toomake-lo mais fácil toosee-los em conjunto. imagem de Olá abaixo mostra todas as mensagens hello do cliente de Olá registo Olá especificado o ID de pedido do cliente.

![Erros de 404 de apresentação do registo de cliente](./media/storage-e2e-troubleshooting-classic-portal/client-log-analysis-grid1.png)

Utilizar dados Olá apresentados esquemas de vista de Olá desses dois separadores, pode analisar Olá pedido dados toodetermine que poderá ter causado erro Olá. Também pode ver pedidos que precedido este um toosee se um evento anterior resultaram toohello de erro 404. Por exemplo, pode rever as entradas do registo de cliente de Olá precedente este toodetermine de ID do pedido de cliente se blob Olá poderá ter sido eliminado ou se o erro de Olá foi devido a aplicação de cliente toohello chamar uma API CreateIfNotExists num contentor ou BLOBs. No registo de cliente Olá, pode encontrar o endereço de blob Olá no Olá **Descrição** campo; no servidor de Olá e registos de rastreio de rede, estas informações aparecem na Olá **resumo** campo.

Quando souber endereço Olá do blob Olá que geraram erros Olá 404, pode investigar mais. Se procurar entradas de registo de Olá para outras mensagens associadas com operações em Olá mesmo blob, pode verificar se o cliente de Olá eliminado anteriormente entidade Olá.

## <a name="analyze-other-types-of-storage-errors"></a>Analisar os outros tipos de erros de armazenamento
Agora que já está familiarizado com a utilização Message Analyzer tooanalyze os dados de registo, pode analisar outros tipos de erros de utilizar a vista de esquemas, as regras de cor e pesquisar/filtragem. Olá tabelas abaixo apresenta uma lista alguns problemas que poderá encontrar e Olá critérios de filtro, pode utilizar toolocate-los. Para obter mais informações sobre como construir filtros e Olá Message Analyzer filtragem de idioma, consulte o artigo [dados de mensagens de filtragem](http://technet.microsoft.com/library/jj819365.aspx).

| tooInvestigate... | Utilize a expressão de filtro... | Expressão aplica-se tooLog (cliente, de servidor, de rede, todos os) |
| --- | --- | --- |
| Atrasos inesperados na entrega de mensagens numa fila |AzureStorageClientDotNetV4.Description contém "Repetir falha na operação." |Cliente |
| Aumento de HTTP no PercentThrottlingError |PROTOCOLO HTTP. Response.StatusCode = = 500 &#124; &#124; PROTOCOLO HTTP. Response.StatusCode = = 503 |Rede |
| Aumentam PercentTimeoutError |PROTOCOLO HTTP. Response.StatusCode = = 500 |Rede |
| Aumentam PercentTimeoutError (todos) |* StatusCode = = 500 |Todos |
| Aumentam PercentNetworkError |AzureStorageClientDotNetV4.EventLogEntry.Level < 2 |Cliente |
| Mensagens HTTP 403 (proibido) |PROTOCOLO HTTP. Response.StatusCode = = 403 |Rede |
| HTTP 404 (não for encontrado) mensagens |PROTOCOLO HTTP. Response.StatusCode = = 404 |Rede |
| 404 (todos) |* StatusCode = = 404 |Todos |
| Partilhado problema de autorização de assinatura de acesso (SAS) |AzureStorageLog.RequestStatus = = "SASAuthorizationError" |Rede |
| HTTP 409 (conflito) mensagens |PROTOCOLO HTTP. Response.StatusCode = = 409 |Rede |
| 409 (todos) |* StatusCode = = 409 |Todos |
| Entradas de registo PercentSuccess baixa ou análise tem operações com o estado de transação de ClientOtherErrors |AzureStorageLog.RequestStatus = = "ClientOtherError" |Servidor |
| Aviso de Nagle |((AzureStorageLog.EndToEndLatencyMS-AzureStorageLog.ServerLatencyMS) > (AzureStorageLog.ServerLatencyMS * 1.5)) e (AzureStorageLog.RequestPacketSize < 1460) e (AzureStorageLog.EndToEndLatencyMS - AzureStorageLog.ServerLatencyMS > = 200) |Servidor |
| Intervalo de tempo nos registos do servidor e da rede |#Timestamp > = 2014-10-20T16:36:38 e #Timestamp < = 2014-10-20T16:36:39 |Servidor de rede |
| Intervalo de tempo em registos do servidor |AzureStorageLog.Timestamp > = 2014-10-20T16:36:38 e AzureStorageLog.Timestamp < = 2014-10-20T16:36:39 |Servidor |

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre os cenários de ponto a ponto de resolução de problemas no armazenamento do Azure, consulte estes recursos:

* [Monitorizar, diagnosticar e resolver problemas de armazenamento do Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md)
* [Análise de Armazenamento](http://msdn.microsoft.com/library/azure/hh343270.aspx)
* [Monitorizar uma conta de armazenamento no Olá Portal do Azure](storage-monitor-storage-account.md)
* [Transferência de dados com Olá utilitário de linha de comandos AzCopy](storage-use-azcopy.md)
* [Guia de funcionamento de analisador de mensagens da Microsoft](http://technet.microsoft.com/library/jj649776.aspx)
