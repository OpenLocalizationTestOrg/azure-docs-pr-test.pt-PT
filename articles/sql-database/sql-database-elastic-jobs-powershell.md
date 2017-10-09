---
title: "aaaCreate e gerir as tarefas elásticas com o PowerShell | Microsoft Docs"
description: PowerShell utilizado toomanage conjuntos de SQL Database do Azure
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a>Criar e gerir tarefas elásticas da base de dados do SQL Server através do PowerShell (pré-visualização)

Olá das APIs do PowerShell para **tarefas de bases de dados elásticas** (em pré-visualização), permitem-lhe definir um grupo de bases de dados relativamente ao qual vai executar scripts. Este artigo mostra como toocreate e gerir **tarefas de bases de dados elásticas** utilizando cmdlets do PowerShell. Consulte [descrição geral das tarefas elásticas](sql-database-elastic-jobs-overview.md). 

## <a name="prerequisites"></a>Pré-requisitos
* Uma subscrição do Azure. Para uma versão de avaliação gratuita, consulte [um mês avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Um conjunto de bases de dados criadas com ferramentas de base de dados elástica Olá. Consulte [começar a utilizar as ferramentas de base de dados elástica](sql-database-elastic-scale-get-started.md).
* Azure PowerShell. Para obter informações detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).
* **As tarefas de base de dados elásticas** PowerShell pacote: consulte [tarefas de instalação de base de dados elástica](sql-database-elastic-jobs-service-installation.md)

### <a name="select-your-azure-subscription"></a>Selecione a sua subscrição do Azure
subscrição de Olá tooselect tem o Id de subscrição (**- SubscriptionId**) ou o nome da subscrição (**- SubscriptionName**). Se tiver várias subscrições podem executar Olá **Get-AzureRmSubscription** assim o desejar Olá cmdlet e copie as informações de subscrição do conjunto de resultados de Olá. Assim que tiver informações da sua subscrição, run Olá seguir commandlet tooset esta subscrição predefinida Olá, nomeadamente Olá destino para criar e gerir tarefas:

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

Olá [ISE do PowerShell](https://technet.microsoft.com/library/dd315244.aspx) é recomendado para utilização toodevelop e executar scripts do PowerShell contra as tarefas de bases de dados elásticas Olá.

## <a name="elastic-database-jobs-objects"></a>Objetos de tarefas de base de dados elásticos
Olá seguintes listas de tabela enviados todos os tipos de objeto de Olá de **tarefas de bases de dados elásticas** juntamente com a descrição e APIs relevantes do PowerShell.

<table style="width:100%">
  <tr>
    <th>Tipo de objeto</th>
    <th>Descrição</th>
    <th>APIs de PowerShell relacionados</th>
  </tr>
  <tr>
    <td>Credencial</td>
    <td>Toouse de nome de utilizador e palavra-passe quando ligar toodatabases para aplicação de DACPACs ou execução de scripts. <p>palavra-passe de Olá é encriptado antes de enviar tooand armazenar na base de dados do Olá as tarefas de base de dados elásticas.  palavra-passe de Olá é desencriptado pelo Olá serviço as tarefas de base de dados elásticas através de credencial de Olá criado e carregado a partir de script de instalação de Olá.</td>
    <td><p>Get-AzureSqlJobCredential</p>
    <p>Novo AzureSqlJobCredential</p><p>Conjunto AzureSqlJobCredential</p></td></td>
  </tr>

  <tr>
    <td>Script</td>
    <td>Toobe de script de Transact-SQL utilizada para execução em bases de dados.  script de Olá deve ser idempotent toobe criados uma vez que o serviço de Olá irá repetir a execução do script Olá após falhas.
    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>Get-AzureSqlJobContentDefinition</p>
    <p>Novo AzureSqlJobContent</p>
    <p>Conjunto AzureSqlJobContentDefinition</p>
    </td>
  </tr>

  <tr>
    <td>DACPAC</td>
    <td><a href="https://msdn.microsoft.com/library/ee210546.aspx">Aplicação de camada de dados </a> toobe aplicada em bases de dados do pacote.

    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>Novo AzureSqlJobContent</p>
    <p>Conjunto AzureSqlJobContentDefinition</p>
    </td>
  </tr>
  <tr>
    <td>Destino de base de dados</td>
    <td>Base de dados e o servidor de nome indo tooan SQL Database do Azure.

    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>Novo AzureSqlJobTarget</p>
    </td>
  </tr>
  <tr>
    <td>Destino de mapa de partições horizontais</td>
    <td>Combinação de um destino de base de dados e uma credencial toobe utilizar informações de toodetermine armazenadas dentro de um mapa de partições horizontais bases de dados elásticas.
    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>Novo AzureSqlJobTarget</p>
    <p>Conjunto AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>Destino de recolha personalizada</td>
    <td>Utilize definido grupo de bases de dados toocollectively para execução.</td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>Novo AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>Destino de subordinados de recolha personalizada</td>
    <td>Destino de base de dados que é referenciado a partir de uma coleção personalizada.</td>
    <td>
    <p>AzureSqlJobChildTarget adicionar</p>
    <p>Remover AzureSqlJobChildTarget</p>
    </td>
  </tr>

<tr>
    <td>Tarefa</td>
    <td>
    <p>Definição de parâmetros para uma tarefa que pode ser utilizado tootrigger execução ou toofulfill uma agenda.</p>
    </td>
    <td>
    <p>Get-AzureSqlJob</p>
    <p>Novo AzureSqlJob</p>
    <p>Conjunto AzureSqlJob</p>
    </td>
  </tr>

<tr>
    <td>Execução da tarefa</td>
    <td>
    <p>Política de execução de tooan accordance processados contentor das tarefas toofulfill necessário executar um script ou aplicar um destino de tooa DACPAC utilizando as credenciais para ligações de base de dados com falhas.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Início AzureSqlJobExecution</p>
    <p>Stop-AzureSqlJobExecution</p>
    <p>Espera-AzureSqlJobExecution</p>
  </tr>

<tr>
    <td>Tarefa a execução da tarefa</td>
    <td>
    <p>Única unidade de trabalho toofulfill uma tarefa.</p>
    <p>Se uma tarefa não for capaz de toosuccessfully executar, é registada a mensagem de exceção resultante Olá e uma nova tarefa correspondente será criada e executada na toohello accordance especificado política de execução.</p></p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Início AzureSqlJobExecution</p>
    <p>Stop-AzureSqlJobExecution</p>
    <p>Espera-AzureSqlJobExecution</p>
  </tr>

<tr>
    <td>Política de execução da tarefa</td>
    <td>
    <p>Controlos da tarefa tempos limite de execução, os limites de repetição e os intervalos entre tentativas.</p>
    <p>As tarefas de base de dados elásticas inclui uma política de execução da tarefa ao predefinido que provocar essencialmente infinita tentativas de falhas de tarefas de tarefas com um término exponencial de intervalos entre cada tentativa.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecutionPolicy</p>
    <p>Novo AzureSqlJobExecutionPolicy</p>
    <p>Conjunto AzureSqlJobExecutionPolicy</p>
    </td>
  </tr>

<tr>
    <td>Agenda</td>
    <td>
    <p>Hora baseada especificação para execução tootake local ou num intervalo reoccurring de uma única vez.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobSchedule</p>
    <p>Novo AzureSqlJobSchedule</p>
    <p>Conjunto AzureSqlJobSchedule</p>
    </td>
  </tr>

<tr>
    <td>Aciona a tarefa</td>
    <td>
    <p>Um mapeamento entre uma tarefa e uma execução da tarefa agenda tootrigger toohello agenda de acordo com.</p>
    </td>
    <td>
    <p>Novo AzureSqlJobTrigger</p>
    <p>Remover AzureSqlJobTrigger</p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a>Tipos de grupo de tarefas de bases de dados elásticas suportadas
tarefa de Olá executa os scripts de Transact-SQL (T-SQL) ou a aplicação de DACPACs entre um grupo de bases de dados. Quando um trabalho é submetido toobe executado através de um grupo de bases de dados, a tarefa de Olá "expande" Olá para tarefas subordinadas em que cada uma desempenha Olá pediu para execução em relação a uma base de dados no grupo de Olá. 

Existem dois tipos de grupos que pode criar: 

* [Mapa de partições horizontais](sql-database-elastic-scale-shard-map-management.md) grupo: quando um trabalho for submetido tootarget um mapa de partições horizontais, tarefa Olá consulta toodetermine de mapa de partições horizontais Olá o conjunto atual de shards e, em seguida, cria subordinado tarefas para cada partição horizontal no mapa de partições horizontais Olá.
* Grupo de recolha personalizado: personalizadas um conjunto de bases de dados. Quando uma tarefa está direcionada para uma coleção personalizada, cria subordinado tarefas para cada base de dados atualmente numa coleção personalizada Olá.

## <a name="tooset-hello-elastic-database-jobs-connection"></a>Olá tooset ligação de tarefas da base de dados elástica
Necessita de uma ligação toobe conjunto toohello tarefas *base de dados de controlo* toousing anterior Olá tarefas APIs. Executar este cmdlet aciona uma toopop de janela de credencial segurança pedir o nome de utilizador de Olá e a palavra-passe criado ao instalar as tarefas de bases de dados elásticas. Todos os exemplos fornecidos neste tópico partem do princípio de que já foram realizado neste primeiro passo.

Abra um tarefas de bases de dados elásticas toohello ligação:

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a>Credenciais encriptado dentro de tarefas de bases de dados elásticas Olá
As credenciais da base de dados podem ser inseridas no tarefas Olá *base de dados de controlo* com a respetiva palavra-passe encriptada. É necessário toostore credenciais tooenable tarefas toobe executado num momento posterior, (utilizando as agendas de tarefas).

Encriptação funciona através de um certificado que criou como parte do script de instalação de Olá. script de instalação de Olá cria e carregamentos Olá certificado para Olá o serviço em nuvem do Azure para a desencriptação de Olá armazenados encriptadas palavras-passe. Olá posteriormente para serviço de nuvem do Azure armazena a chave pública do Olá dentro tarefas Olá *base de dados de controlo* que lhe permite Olá de API do PowerShell ou o Portal clássico do Azure de tooencrypt de interface uma palavra-passe fornecida sem necessidade de certificado Olá toobe instalada localmente.

as palavras-passe de credencial de Olá são encriptados e seguros a partir de utilizadores com objetos de tarefas da base de dados de tooElastic de acesso só de leitura. Mas é possível que um utilizador mal intencionado com acesso de leitura e escrita tooElastic tarefas de base de dados objetos tooextract uma palavra-passe. As credenciais são toobe concebida reutilizada em execuções de tarefa. As credenciais são transmitidas tootarget bases de dados quando estabelecer ligações. Não existem atualmente sem restrições nas bases de dados do destino de Olá utilizados para cada credencial, o utilizador mal intencionado pode adicionar um destino de base de dados para uma base de dados sob o controlo do utilizador mal intencionado Olá. utilizador Olá, subsequentemente, foi possível iniciar uma tarefa direcionada para a palavra-passe do base de dados toogain Olá credenciais.

Melhores práticas de segurança para tarefas de bases de dados elásticas incluem:

* Limitar a utilização de indivíduos de tootrusted Olá APIs.
* As credenciais devem ter Olá menos privilégios necessário tooperform Olá tarefa.  Obter mais informações podem ser vistas nisto [autorização e permissões](https://msdn.microsoft.com/library/bb669084.aspx) artigo do MSDN do SQL Server.

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a>toocreate uma credencial encriptada para execução da tarefa em bases de dados
toocreate encriptada de uma nova credencial, hello [ **cmdlet Get-Credential** ](https://technet.microsoft.com/library/hh849815.aspx) pede-lhe um nome de utilizador e palavra-passe que pode ser transmitido toohello [ **AzureSqlJobCredential novo cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a>tooupdate credenciais
Quando alterar as palavras-passe, utilize Olá [ **cmdlet Set-AzureSqlJobCredential** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) e conjunto Olá **CredentialName** parâmetro.

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a>toodefine um destino de mapa de partições horizontais de base de dados elástica
tooexecute uma tarefa em todas as bases de dados de um conjunto de partições horizontais (criado utilizando [biblioteca de clientes de base de dados elástica](sql-database-elastic-database-client-library.md)), utilize um mapa de partições horizontais como destino de base de dados de Olá. Este exemplo requer uma aplicação em partição horizontal criada utilizando a biblioteca de clientes de base de dados elástica Olá. Consulte [introdução com exemplo de ferramentas de base de dados elástica](sql-database-elastic-scale-get-started.md).

base de dados do Olá partições horizontais mapa manager tem de ser definido como um destino de base de dados e, em seguida, o mapa de partições horizontais específico Olá deve ser especificado como um destino.

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a>Criar um Script T-SQL para execução em bases de dados
Ao criar scripts T-SQL para execução, recomenda-se vivamente toobuild-los toobe [idempotent](https://en.wikipedia.org/wiki/Idempotence) e resilientes contra falhas. As tarefas de base de dados elásticas irão repetir a execução de um script sempre que a execução detetar uma falha, independentemente da classificação de Olá de falha de Olá.

Olá utilize [ **cmdlet New-AzureSqlJobContent** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate e guardar um script para execução e defina Olá **- ContentName** e **- CommandText**parâmetros.

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a>Criar um script novo a partir de um ficheiro
Se Olá script T-SQL está definido no âmbito de um ficheiro, utilize este script de Olá tooimport:

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a>script de tooupdate T-SQL para execução em bases de dados
Este atualizações de script de PowerShell Olá texto de comando T-SQL para um script existente.

Olá de conjunto de variáveis tooreflect Olá pretendido script definição toobe conjunto os seguintes:

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="tooupdate-hello-definition-tooan-existing-script"></a>script existente do tooupdate Olá definição tooan
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a>toocreate tooexecute uma tarefa um script através de um mapa de partições horizontais
Este script do PowerShell inicia uma tarefa para execução de um script em cada partição horizontal um mapa de partições horizontais horizontal elástico.

Olá de set seguintes Olá de tooreflect variáveis pretendido script e de destino:

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a>tooexecute uma tarefa
Este script do PowerShell executa uma tarefa existente:

Atualize Olá tooreflect variável Olá pretendido tarefa nome toohave executada os seguintes:

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a>Estado de Olá tooretrieve da execução de uma única tarefa
Olá utilize [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) e conjunto Olá **JobExecutionId** parâmetro tooview Olá Estado execução da tarefa.

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

Utilize Olá mesmo **Get-AzureSqlJobExecution** cmdlet com Olá **includechildren exige** parâmetro tooview Olá Estado execuções de tarefa subordinada, nomeadamente Olá estado específico de cada execução da tarefa em relação a cada a base de dados visada pela tarefa de Olá.

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a>Estado de Olá tooview em várias execuções de tarefa
Olá [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) tem vários parâmetros opcionais que podem ser utilizado toodisplay várias execuções de tarefa, filtradas através de parâmetros de Olá fornecido. seguinte Olá demonstra Algumas das várias formas de Olá toouse Get-AzureSqlJobExecution:

Obter todas as execuções de tarefas ativas de nível superior:

    Get-AzureSqlJobExecution

Obter todas as execuções de tarefa de nível superior, incluindo as execuções de tarefa inativo:

    Get-AzureSqlJobExecution -IncludeInactive

Obter todas as execuções de tarefa de subordinados de um ID de execução da tarefa fornecida, incluindo execuções de tarefa inativo:

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

Obter todas as execuções de tarefa criadas com base numa agenda / combinação, incluindo tarefas Inativas da tarefa:

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

Obter todas as tarefas direcionada para um mapa de partições horizontais especificado, incluindo tarefas Inativas:

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

Obter todas as tarefas direcionada para uma coleção personalizada especificada, incluindo tarefas Inativas:

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

Obter a lista de Olá de execuções de tarefas da tarefa em execução uma tarefa específica:

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

Obter os detalhes de tarefa de execução da tarefa:

Olá seguinte script do PowerShell pode ser utilizados tooview Olá detalhes sobre uma execução de tarefas da tarefa, que é particularmente útil quando a depuração de falhas de execução.

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a>execuções de tarefas de falhas de tooretrieve dentro da tarefa
Olá **JobTaskExecution objeto** inclui uma propriedade para Olá ciclo de vida da tarefa de Olá juntamente com uma propriedade de mensagem. Se uma execução de tarefas da tarefa falhou, Olá ciclo de vida será possível definir a propriedade demasiado*falha* e será possível definir a propriedade de mensagem de Olá toohello resultante mensagem de exceção e a pilha. Se uma tarefa não foi concluída com êxito, é importante tooview Olá detalhes sobre as tarefas que não foram concluída com êxito para uma determinada tarefa.

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a>toowait para um toocomplete de execução da tarefa
Olá seguinte script do PowerShell pode ser utilizado toowait para um toocomplete de tarefas da tarefa:

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a>Criar uma política de execução personalizado
As tarefas de base de dados elásticas suporta a criação de políticas de execução personalizadas que podem ser aplicadas ao iniciar trabalhos.

Atualmente permitem definir políticas de execução:

* Nome: Identificador para a política de execução de Olá.
* Tempo limite de tarefa: Total de tempo antes de uma tarefa será cancelada pelo tarefas de base de dados elásticas.
* Intervalo de repetição inicial: Intervalo toowait antes da repetição primeiro.
* Intervalo máximo de tentativas: Limite de toouse de intervalos de repetição.
* Coeficiente de término de intervalo de repetição: Coeficiente utilizado toocalculate Olá próximo intervalo entre tentativas.  Olá seguinte fórmula utilizada: (intervalo de Repita inicial) * Math.pow ((coeficiente de término de intervalo), (número de tentativas) - 2). 
* Número máximo de tentativas: Olá número máximo de tentativas de repetição tooperform dentro de uma tarefa.

política de execução de predefinida Olá utiliza Olá os seguintes valores:

* Nome: Política de execução de predefinida
* Tempo limite de tarefa: 1 semana
* Intervalo de repetição inicial: 100 milissegundos
* Intervalo máximo de tentativas: 30 minutos
* Repita o coeficiente de intervalo: 2
* Número máximo de tentativas: 2 147 483 647

Crie política de execução de Olá pretendido:

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a>Atualizar uma política de execução personalizado
Atualize tooupdate de política de execução de Olá pretendido:

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a>Cancelar uma tarefa
As tarefas de base de dados elásticas suporta pedidos de cancelamento de tarefas.  Se as tarefas de base de dados elásticas Deteta um pedido de cancelamento de uma tarefa atualmente a ser executado, tentará a tarefa de Olá toostop.

Existem duas formas diferentes, que as tarefas de base de dados elásticas podem executar um cancelamento:

1. Cancelar tarefas a executar atualmente: se for detetado um cancelamento enquanto uma tarefa está atualmente em execução, será tentado a um cancelamento dentro Olá atualmente em execução aspeto de tarefa Olá.  Por exemplo: se houver uma consulta de execução longa atualmente a ser efetuada quando é tentado um cancelamento, existirá uma consulta de Olá toocancel tentativa.
2. As repetições de tarefas a cancelar: se um cancelamento for detetado por thread de controlo de Olá antes de uma tarefa é iniciada para execução, thread de controlo de Olá irá evitar iniciar tarefa Olá e declarar pedido Olá como cancelada.

Se for pedido um cancelamento de tarefas para uma tarefa principal, o pedido de cancelamento Olá será cumprido para a tarefa principal de Olá e para todos os respetivos tarefas subordinadas.

toosubmit um pedido de cancelamento, utilize Olá [ **cmdlet Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) e conjunto Olá **JobExecutionId** parâmetro.

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a>toodelete uma tarefa e histórico da tarefa assíncrona
As tarefas de base de dados elásticas suporta eliminação assíncrona de tarefas. Uma tarefa pode ser marcada para eliminação e sistema Olá irá eliminar a tarefa de Olá e todos os respetivo histórico de tarefas após conclusão da tarefa de Olá todas as execuções de tarefa. sistema de Olá não cancelará automaticamente execuções de tarefas ativas.  

Invocar [ **Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel execuções de tarefas ativas.

eliminação de tarefa tootrigger, utilize Olá [ **cmdlet Remove-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) e conjunto Olá **JobName** parâmetro.

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a>toocreate um destino de base de dados personalizada
Pode definir os destinos de base de dados personalizada para execução direta ou para inclusão dentro de um grupo de base de dados personalizada. Por exemplo, porque **conjuntos elásticos** são ainda não diretamente suportada através das APIs do PowerShell, pode criar um destino de coleção da base de dados personalizada que abrange todas as bases de dados de Olá no agrupamento de Olá e de destino de base de dados personalizada.

Definir Olá seguindo as informações de base de dados do variáveis tooreflect Olá pretendido:

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a>toocreate um destino de coleção da base de dados personalizada
Olá utilize [ **New-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine uma execução de base de dados personalizada do tooenable ao destino coleção entre vários destinos de base de dados definido. Depois de criar um grupo de base de dados, as bases de dados podem ser associados com o destino de coleção personalizada Olá.

Definir Olá a seguinte configuração de destino do variáveis tooreflect Olá pretendido coleção personalizada:

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a>destino de coleção do tooadd bases de dados tooa base de dados personalizada
base de dados tooa personalizado coleção específica de tooadd utilizar Olá [ **adicionar AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a>Reveja as bases de dados de Olá dentro de um destino de coleção da base de dados personalizada
Olá utilize [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve Olá subordinado bases de dados dentro de uma base de dados personalizada recolha de destino. 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a>Criar um script de uma tarefa tooexecute através de um destino de coleção da base de dados personalizada
Olá utilize [ **New-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate uma tarefa de um grupo de bases de dados definidas por um destino de coleção da base de dados personalizada. As tarefas de base de dados elásticas irão expandir tarefa Olá para várias tarefas de subordinados cada base de dados correspondente tooa associados com o destino de coleção de base de dados personalizada Olá e certifique-se de que o script de Olá é executado em relação a cada base de dados. Novamente, é importante que os scripts estão idempotent toobe resiliente tooretries.

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a>Recolha de dados entre bases de dados
Pode utilizar um tooexecute tarefa consulta entre um grupo de bases de dados e enviar tabela do Olá resultados tooa específica. tabela de Olá pode ser consultada após Olá facto toosee Olá resultados da consulta de cada base de dados. Esta opção fornece um método assíncrono tooexecute uma consulta em muitas bases de dados. Tentativas falhadas são processadas automaticamente através de tentativas.

tabela de destino especificado Olá será criada automaticamente se ainda não existir. nova tabela de Olá corresponde ao esquema Olá Olá devolvida um conjunto de resultados. Se um script devolver vários conjuntos de resultados, tarefas de bases de dados elásticas só irão enviar Olá primeira toohello destino tabela.

Olá seguinte script do PowerShell executa um script e recolhe os respetivos resultados numa tabela especificada. Este script parte do princípio de que foi criado um script T-SQL que produz um conjunto de resultados único e que foi criado uma base de dados personalizada recolha de destino.

Este script utiliza Olá [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet. Definir os parâmetros de Olá de script, as credenciais e o destino de execução:

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a>toocreate e iniciar uma tarefa para cenários de recolha de dados
Este script utiliza Olá [ **início AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="tooschedule-a-job-execution-trigger"></a>tooschedule um acionador de execução da tarefa
Olá seguinte script do PowerShell pode ser utilizado toocreate numa agenda periódica. Este script utiliza um intervalo em minuto, mas [ **New-AzureSqlJobSchedule** ](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) também suporta os parâmetros - DayInterval, - HourInterval, - MonthInterval e - WeekInterval. As agendas que executar apenas uma vez que podem ser criadas por transmitir - OneTime.

Crie uma nova agenda:

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a>tootrigger uma tarefa executada num horário
Um acionador da tarefa pode ser definido toohave um tarefa executada according tooa horário. Olá seguinte script do PowerShell pode ser utilizado toocreate um acionador da tarefa.

Utilize [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) e conjunto Olá seguindo tarefa pretendida do variáveis toocorrespond toohello e agenda:

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a>tooremove uma tarefa de toostop associação agendada execução numa agenda
toodiscontinue ocorrer a execução da tarefa através de um acionador da tarefa, acionador da tarefa de Olá pode ser removido. Remover a um toostop de acionamento de tarefa uma tarefa a ser executado de acordo com tooa agenda utilizando Olá [ **cmdlet Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a>Obter tarefa acionadores tooa vinculada horário
Olá seguinte script do PowerShell pode ser utilizado tooobtain e apresentar Olá tarefa acionadores tooa registado específico horário.

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a>acionadores de tarefa tooretrieve vinculado tooa tarefa
Utilize [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain e apresentar agendas que contém uma tarefa registada.

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a>toocreate uma aplicação de camada de dados (DACPAC) para execução em bases de dados
Consulte toocreate um DACPAC [aplicações de camada de dados](https://msdn.microsoft.com/library/ee210546.aspx). toodeploy um DACPAC, utilize Olá [cmdlet New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent). Olá DACPAC tem de ser acessível toohello serviço. É recomendado tooupload um tooAzure DACPAC criado armazenamento e criar um [assinatura de acesso partilhado](../storage/common/storage-dotnet-shared-access-signature-part-1.md) para Olá DACPAC.

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a>tooupdate uma aplicação de camada de dados (DACPAC) para execução em bases de dados
DACPACs existentes registados dentro de tarefas de base de dados elásticas podem ser atualizada toopoint toonew URIs. Olá utilize [ **cmdlet Set-AzureSqlJobContentDefinition** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate Olá DACPAC URI no existente registado DACPAC:

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a>toocreate tooapply uma tarefa uma aplicação de camada de dados (DACPAC) em bases de dados
Depois de ter sido criado um DACPAC dentro de tarefas de base de dados elásticas, uma tarefa pode ser criada tooapply Olá DACPAC entre um grupo de bases de dados. Olá seguinte script do PowerShell pode ser utilizado toocreate uma tarefa DACPAC através de uma coleção personalizada das bases de dados:

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->
