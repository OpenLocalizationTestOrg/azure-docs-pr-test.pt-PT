---
title: "aaaRunbook resultados e mensagens na automatização do Azure | Microsoft Docs"
description: "Desribes como mensagens de erro e de saída toocreate e obter a partir de runbooks na automatização do Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 13a414f5-0e2c-4be2-9558-a3e3ec84b6b2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: magoedte;bwren
ms.openlocfilehash: c1505fa889473766bfa47e43aaed2449d60ad851
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-output-and-messages-in-azure-automation"></a>Resultados de Runbook e mensagens na automatização do Azure
A maioria dos runbooks de automatização do Azure terá alguma forma de resultado, como um utilizador de toohello de mensagem de erro ou um objeto complexo destinado toobe consumido por outro fluxo de trabalho. O Windows PowerShell oferece [vários fluxos](http://blogs.technet.com/heyscriptingguy/archive/2014/03/30/understanding-streams-redirection-and-write-host-in-powershell.aspx) toosend um resultado de um script ou o fluxo de trabalho. Automatização do Azure funciona com cada um destes fluxos de forma diferente e devem ser adotadas as melhores práticas toouse cada quando estiver a criar um runbook.

Olá tabela seguinte fornece uma breve descrição de cada um dos fluxos de Olá e o respetivo comportamento no Olá Azure Management Portal quando executar um runbook publicado e quando [testar um runbook](automation-testing-runbook.md). Existem mais detalhes sobre cada fluxo são fornecidos nas secções subsequentes.

| Fluxo | Descrição | Publicado | Teste |
|:--- |:--- |:--- |:--- |
| Saída |Objetos destinados toobe consumido por outros runbooks. |Escrito no histórico da tarefa toohello. |Apresentado no painel de resultados do teste de Olá. |
| Aviso |Mensagem de aviso para o utilizador Olá. |Escrito no histórico da tarefa toohello. |Apresentado no painel de resultados do teste de Olá. |
| Erro |Mensagem de erro para o utilizador Olá. Ao contrário de uma exceção, Olá runbook continua após uma mensagem de erro por predefinição. |Escrito no histórico da tarefa toohello. |Apresentado no painel de resultados do teste de Olá. |
| Verboso |Mensagens de fornecer informações gerais ou depuração. |Escrito no histórico de toojob apenas se o registo verboso está ativado para os Olá runbook. |Apresentado no painel de resultados de teste de Olá apenas se $VerbosePreference for definida tooContinue Olá runbook. |
| Progresso |Registos gerados automaticamente antes e após cada atividade num runbook Olá. Olá runbook não deve tentar toocreate os seus próprios registos de progresso, uma vez que estes se destinam a ser um utilizador interativo. |Escrito no histórico de toojob apenas se o registo de progresso estiver ativado runbook Olá. |Não é apresentado no painel de resultados do teste de Olá. |
| Depurar |Mensagens destinadas para um utilizador interativo. Não devem ser utilizadas em runbooks. |Não é escrito no histórico de toojob. |Não é escrito no tooTest painel de resultados. |

## <a name="output-stream"></a>Fluxo de saída
fluxo de saída Olá destina-se a saída de objetos criados por um script ou um fluxo de trabalho quando é executada corretamente. Na automatização do Azure, este fluxo é utilizado sobretudo para toobe de objetos que se destinam consumida [principal runbooks que chamem o runbook atual Olá](automation-child-runbooks.md). Quando lhe [chamar um runbook inline](automation-child-runbooks.md#invoking-a-child-runbook-using-inline-execution) a partir de um runbook de principal, são devolvidos dados do elemento principal do toohello de fluxo de saída do Olá. Só deve utilizar utilizador back toohello de informações gerais toocommunicate Olá saída fluxo se souber Olá runbook nunca irá ser chamado por outro runbook. Como melhor prática, no entanto, deve normalmente utiliza Olá [fluxo verboso](#Verbose) utilizador de toohello toocommunicate informações gerais.

Pode escrever dados toohello fluxo de saída através de [Write-Output](http://technet.microsoft.com/library/hh849921.aspx) ou ao colocar o objeto de Olá na sua própria linha no runbook Olá.

    #hello following lines both write an object toohello output stream.
    Write-Output –InputObject $object
    $object

### <a name="output-from-a-function"></a>Saída de uma função
Quando escrever o fluxo de saída toohello numa função que está incluída no runbook, o resultado de Olá é passado toohello back-runbook. Se Olá runbook atribuir essa variável tooa de saída, em seguida, não será escrita toohello fluxo de saída. Escrever tooany outros fluxos a partir da função de Olá irá escrever toohello fluxo correspondente Olá runbook.

Considere Olá runbook de exemplo a seguir.

    Workflow Test-Runbook
    {
        Write-Verbose "Verbose outside of function" -Verbose
        Write-Output "Output outside of function"
        $functionOutput = Test-Function
        $functionOutput

    Function Test-Function
     {
        Write-Verbose "Verbose inside of function" -Verbose
        Write-Output "Output inside of function"
      }
    }


fluxo de saída de Olá Olá tarefa de runbook seria:

    Output inside of function
    Output outside of function

Olá fluxo verboso Olá tarefa de runbook seria:

    Verbose outside of function
    Verbose inside of function

Assim que tiver publicado Olá runbook e antes de começá-lo, tem também de ativar o registo nas definições de runbook Olá no Olá de tooget ordem saídas de fluxo verboso verboso.

### <a name="declaring-output-data-type"></a>Tipo de dados de saída declarativo
Um fluxo de trabalho pode especificar o tipo de dados de Olá do respetivo resultado utilizando Olá [atributo OutputType](http://technet.microsoft.com/library/hh847785.aspx). Este atributo não tem efeito durante o tempo de execução, mas fornece um autor de runbook toohello indicação no momento da conceção de saída Olá esperado de Olá runbook. Como conjunto de ferramentas de Olá dos runbooks continua tooevolve, importância Olá de declarar os tipos de dados de saída no momento da conceção será aumentam a importância. Como resultado, é constitui uma melhor prática tooinclude esta declaração em todos os runbooks que criar.

Eis uma lista de exemplo os tipos de saída:

* String
* System. Int32
* System.Collections.Hashtable
* Microsoft.Azure.Commands.Compute.Models.PSVirtualMachine

Olá runbook de exemplo seguinte produz um objeto de cadeia e inclui uma declaração do respetivo tipo de saída. Se o runbook devolve uma matriz de um determinado tipo, em seguida, deve especificar ainda Olá tipo como tooan oposição ao matriz do tipo de Olá.

    Workflow Test-Runbook
    {
       [OutputType([string])]

       $output = "This is some string output."
       Write-Output $output
    }

toodeclare uma saída escreva em runbooks Grapical ou gráfico fluxo de trabalho do PowerShell, pode selecionar Olá **entrada e saída** opção de menu e escreva o nome de Olá de Olá de saída do tipo.  Recomendamos que utilize toomake de nome de classe Olá completa .NET-lo facilmente identificável ao referenciá-lo a partir de um runbook principal.  Isto apresenta todas as propriedades de Olá de barramento de dados de toohello dessa classe no runbook Olá e proporciona muita flexibilidade quando utilizá-los como lógica condicional, registo e de referência como valores para outras atividades no runbook Olá.<br> ![Opção de entrada do Runbook e de saída](media/automation-runbook-output-and-messages/runbook-menu-input-and-output-option.png)

No seguinte exemplo de Olá, temos dois runbooks gráficos toodemonstrate esta funcionalidade.  Se aplicar o modelo de design do runbook modulares Olá, temos um runbook que funciona como Olá *modelo do Runbook de autenticação* gerir a autenticação com a utilização do Azure Olá conta Run As.  Nosso runbook segundo, que normalmente iria efetuar Olá core lógica tooautomate um determinado cenário, neste caso, vai tooexecute Olá *modelo do Runbook de autenticação* e apresentar Olá resultados tooyour **teste** painel de resultados.  Em circunstâncias normais, iremos teria este runbook fazer algo contra uma saída de Olá aproveitamento do recurso a partir do runbook subordinado de Olá.    

Eis a lógica básica de Olá de Olá **AuthenticateTo Azure** runbook.<br> ![Exemplo de modelo do Runbook de autenticar](media/automation-runbook-output-and-messages/runbook-authentication-template.png).  

Inclui o tipo de saída Olá *Microsoft.Azure.Commands.Profile.Models.PSAzureContext*, que irá devolver propriedades de perfil de autenticação de Olá.<br> ![Exemplo de tipo de resultado do Runbook](media/automation-runbook-output-and-messages/runbook-input-and-output-add-blade.png) 

Embora este runbook seja muito diretamente reencaminhar, há um toocall de item de configuração terminar aqui.  última atividade de Olá está a executar o Olá **Write-Output** cmdlet e escritas de paginações hello as variável de _ tooa de dados do perfil $ utilizando uma expressão do PowerShell para Olá **Inputobject** parâmetro, que é necessário para que cmdlet.  

Para o runbook segundo Olá, neste exemplo, com o nome *teste ChildOutputType*, temos simplesmente duas atividades.<br> ![Tipo de Runbook de saída subordinado de exemplo](media/automation-runbook-output-and-messages/runbook-display-authentication-results-example.png) 

primeira actividade a Olá chama Olá **AuthenticateTo Azure** runbook e Olá segunda atividade está em execução Olá **Write-Verbose** cmdlet com Olá **origem de dados** de  **Saída da atividade** e valor Olá **caminho do campo** é **Context.Subscription.SubscriptionName**, que está a especificar um resultado de contexto de Olá Olá  **AuthenticateTo Azure** runbook.<br> ![Origem de dados de parâmetro de cmdlet Write-Verbose](media/automation-runbook-output-and-messages/runbook-write-verbose-parameters-config.png)    

o resultado resultante Olá é nome Olá da subscrição Olá.<br> ![Resultados de Runbook de teste ChildOutputType](media/automation-runbook-output-and-messages/runbook-test-childoutputtype-results.png)

Uma nota sobre o comportamento de Olá de Olá controlo de tipo de saída.  Quando escreve um valor no campo do tipo de saída Olá no Olá entrada e o painel de propriedades de saída, tiver tooclick fora do controlo de Olá depois de escrever, por ordem para a sua toobe de entrada reconhecido pelo controlo de Olá.  

## <a name="message-streams"></a>Fluxos de mensagens
Ao contrário do fluxo de saída Olá, fluxos de mensagens são utilizador de toohello de informações de toocommunicate pretendido. Existem vários fluxos de mensagens para diferentes tipos de informações e cada um é processada de forma pela automatização do Azure.

### <a name="warning-and-error-streams"></a>Fluxos de avisos e erros
fluxos de avisos e erros de Olá são toolog pretendido problemas que ocorrem num runbook. Estes são escritos no histórico da tarefa toohello quando um runbook é executado e estão incluídos no painel de resultados do teste de Olá no Olá Azure Management Portal quando um runbook é testado. Por predefinição, Olá runbook continuará a ser executado após um aviso ou erro. Pode especificar esse runbook Olá deve ser suspenso após um aviso ou erro ao definir um [variável de preferência](#PreferenceVariables) Olá runbook antes de criar mensagem de saudação. Por exemplo, toocause toosuspend um runbook com um erro que teria uma exceção, defina **$ErrorActionPreference** tooStop.

Criar uma mensagem de aviso ou erro utilizando Olá [Write-Warning](https://technet.microsoft.com/library/hh849931.aspx) ou [Write-Error](http://technet.microsoft.com/library/hh849962.aspx) cmdlet. As atividades também podem escrever fluxos toothese.

    #hello following lines create a warning message and then an error message that will suspend hello runbook.

    $ErrorActionPreference = "Stop"
    Write-Warning –Message "This is a warning message."
    Write-Error –Message "This is an error message that will stop hello runbook because of hello preference variable."

### <a name="verbose-stream"></a>Fluxo verboso
fluxo de mensagens verbosas Olá é para obter informações gerais sobre a operação do runbook Olá. Desde Olá [fluxo de depuração](#Debug) não está disponível num runbook, as mensagens verbosas devem ser utilizadas para informações de depuração. Por predefinição, as mensagens verbosas de runbooks publicados não serão armazenadas no histórico da tarefa Olá. as mensagens verbosas toostore, configure os runbooks publicados tooLog registos verbosos no separador de configurar Olá de runbook Olá no Olá Portal de gestão do Azure. Na maioria dos casos, deve manter Olá predefinição não criar registos verbosos para um runbook por motivos de desempenho. Ativar esta tootroubleshoot apenas de opção ou depurar um runbook.

Quando [testar um runbook](automation-testing-runbook.md), as mensagens verbosas não são apresentadas, mesmo que esteja Olá runbook registos verbosos toolog configurado. as mensagens verbosas toodisplay ao [testar um runbook](automation-testing-runbook.md), tem de definir Olá $VerbosePreference tooContinue de variável. Com essa variável definida, as mensagens verbosas serão apresentadas no Olá painel de resultados do teste de Olá portal do Azure.

Criar uma mensagens verbosas utilizando Olá [Write-Verbose](http://technet.microsoft.com/library/hh849951.aspx) cmdlet.

    #hello following line creates a verbose message.

    Write-Verbose –Message "This is a verbose message."

### <a name="debug-stream"></a>Fluxo de depuração
fluxo de depuração de Olá destina-se com um utilizador interativo e não deve ser utilizado em runbooks.

## <a name="progress-records"></a>Registos de progressos
Se configurar um progresso de toolog runbook regista (no separador de configurar Olá de Olá runbook no portal do Azure de Olá), em seguida, um registo será escrito toohello histórico da tarefa antes e após cada atividade é executada. Na maioria dos casos, deve manter a predefinição de Olá de registo não registos de progresso de um runbook no desempenho de toomaximize de ordem. Ativar esta tootroubleshoot apenas de opção ou depurar um runbook. Ao testar um runbook, não são apresentadas mensagens de progresso, mesmo que esteja Olá runbook registos de progressos toolog configurado.

Olá [Write-Progress](http://technet.microsoft.com/library/hh849902.aspx) cmdlet não é válido num runbook, uma vez que este se destina a ser utilizado com um utilizador interativo.

## <a name="preference-variables"></a>Variáveis de preferência
O Windows PowerShell utiliza [variáveis de preferência](http://technet.microsoft.com/library/hh847796.aspx) toodetermine como toorespond toodata enviado toodifferent saída fluxos. Pode definir estas variáveis num toocontrol runbook como este responderá toodata enviados para vários fluxos.

Olá tabela seguinte apresenta uma lista de variáveis de preferência Olá que podem ser utilizadas em runbooks com os respetivos válido e valores predefinidos. Tenha em atenção que esta tabela inclui apenas os valores de Olá que são válidos num runbook. Os valores adicionais são válidos para variáveis de preferência Olá quando utilizado no Windows PowerShell fora da automatização do Azure.

| Variável | Valor predefinido | Valores válidos |
|:--- |:--- |:--- |
| WarningPreference |Continuar |Parar<br>Continuar<br>SilentlyContinue |
| ErrorActionPreference |Continuar |Parar<br>Continuar<br>SilentlyContinue |
| VerbosePreference |SilentlyContinue |Parar<br>Continuar<br>SilentlyContinue |

Olá a tabela seguinte lista o comportamento de Olá para Olá preferência valores das variáveis que são válidas nos runbooks.

| Valor | Comportamento |
|:--- |:--- |
| Continuar |Regista a mensagem de saudação e continua a executar o runbook Olá. |
| SilentlyContinue |Continua a executar Olá runbook sem registar a mensagem de saudação. Isto afeta Olá de ignorar a mensagem de saudação. |
| Parar |Regista a mensagem de saudação e suspende o runbook Olá. |

## <a name="retrieving-runbook-output-and-messages"></a>Obter resultados de runbook e mensagens
### <a name="azure-portal"></a>Portal do Azure
Pode ver os detalhes de Olá de uma tarefa de runbook na Olá portal do Azure a partir do separador de tarefas Olá de um runbook. Olá resumo da tarefa de Olá apresentará os parâmetros de entrada Olá e Olá [fluxo de saída](#Output) na adição toogeneral sobre a tarefa de Olá e quaisquer exceções, caso ocorram. Olá histórico incluirá as mensagens de Olá [fluxo de saída](#Output) e [aviso e erro fluxos](#WarningError) na adição toohello [fluxo verboso](#Verbose) e [progresso Regista](#Progress) se Olá runbook estiver configurado toolog verboso e registos de progressos.

### <a name="windows-powershell"></a>Windows PowerShell
No Windows PowerShell, pode obter resultados e mensagens de um runbook com Olá [Get-AzureAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) cmdlet. Este cmdlet requer Olá ID da tarefa de Olá e tem um parâmetro denominado fluxo onde especificar que fluxo tooreturn. Pode especificar qualquer tooreturn todos os fluxos de trabalho de Olá.

Olá seguinte o exemplo inicia um runbook de exemplo e, em seguida, aguarda para o mesmo toocomplete. Depois de concluída, o fluxo de saída é recolhido da tarefa de Olá.

    $job = Start-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook"

    $doLoop = $true
    While ($doLoop) {
       $job = Get-AzureRmAutomationJob -ResourceGroupName "ResourceGroup01" `
       –AutomationAccountName "MyAutomationAccount" -Id $job.JobId
       $status = $job.Status
       $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped")
    }

    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" -Id $job.JobId –Stream Output

### <a name="graphical-authoring"></a>Criação de gráficos
Para runbooks gráficos, registo extra está disponível no formulário de Olá de rastreio de nível de atividade.  Existem dois níveis de rastreio: básico e detalhados.  Rastreio básico, pode ver Olá iniciar em tentativas de atividade tooany, como o número de tentativas e a hora de início da atividade de Olá relacionadas com a hora de fim de cada atividade num runbook Olá mais informações.  Rastreio de detalhado, receberá básico rastreio adição de entrada e saída para cada atividade.  Tenha em atenção que atualmente registos de rastreio de Olá são escritos utilizando fluxo verboso Olá, pelo que tem de ativar o registo verboso quando ativar o rastreio.  Para runbooks gráficos com rastreio ativado não é necessário toolog registos de progresso, uma vez que funciona de rastreio básico Olá Olá a mesma finalidade e é mais informativo.

![Vista de fluxos de trabalho de criação gráfico](media/automation-runbook-output-and-messages/job-streams-view-blade.png)

Pode ver partir Olá acima captura de ecrã que quando ativar verboso registo e rastreio para runbooks gráficos, estão disponíveis em produção Olá que ver fluxos de trabalho muito mais informações.  Estas informações adicionais podem ser essenciais para a resolução de problemas de produção com um runbook e, por conseguinte, deve apenas ativá-la para essa finalidade e não como uma prática geral.    
registos de rastreio de Olá podem ser especialmente várias.  Com um runbook gráfico rastreio, pode obter dois registos toofour por atividade, dependendo se configurou o rastreio básico ou detalhado.  A menos que precisar desta informação tootrack Olá progresso um runbook para resolução de problemas, pode querer tookeep que rastreio desativado.

**tooenable nível de atividade de rastreio, execute Olá os seguintes passos.**

1. No Portal do Azure Olá, abra a sua conta de automatização.
2. Clique em Olá **Runbooks** mosaico tooopen Olá lista de runbooks.
3. No painel de Runbooks Olá, clique em tooselect um runbook gráfico da sua lista de runbooks.
4. No painel de definições de Olá do runbook Olá selecionado, clique em **registo e rastreio**.
5. Olá registo e rastreio painel, sob criar registos verbosos, clique em **no** tooenable o registo verboso e rastreio udner nível de atividade, alterar o nível de rastreio de Olá demasiado**básico** ou **detalhados**  com base no nível de Olá de rastreio precisa.<br>
   
   ![Registo de criação gráfico e painel de rastreio](media/automation-runbook-output-and-messages/logging-and-tracing-settings-blade.png)

### <a name="microsoft-operations-management-suite-oms-log-analytics"></a>Análise de registos do Microsoft Operations Management Suite (OMS)
Automatização pode enviar runbook tarefa estado e tarefa fluxos tooyour análise de registos do Microsoft Operations Management Suite (OMS) área de trabalho.  Análise de registos pode,

* Obter conhecimentos aprofundados sobre as tarefas de automatização 
* Acionamento um e-mail ou o alerta com base no seu estado de tarefa de runbook (por exemplo, falha ou suspenso) 
* Escrever consultas avançadas nos seus fluxos de trabalho 
* Correlacionar tarefas em contas de automatização 
* Visualizar o histórico do trabalho ao longo do tempo    

Para obter mais informações sobre como tooconfigure integração com toocollect de análise de registos, correlacionar e atuar sobre dados da tarefa, consulte [reencaminhar o estado da tarefa e fluxos de trabalho de automatização tooLog análise (OMS)](automation-manage-send-joblogs-log-analytics.md).

## <a name="next-steps"></a>Passos seguintes
* mais sobre a execução do runbook, como as tarefas de runbook toomonitor e outros detalhes técnicos, consulte toolearn [controlar uma tarefa de runbook](automation-runbook-execution.md)
* toounderstand como runbooks subordinados toodesign e utilização, consulte [runbooks subordinados na automatização do Azure](automation-child-runbooks.md)

