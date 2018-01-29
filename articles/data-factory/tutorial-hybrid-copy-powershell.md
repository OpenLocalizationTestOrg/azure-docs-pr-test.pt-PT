---
title: Copiar dados do SQL Server para o Armazenamento de Blobs com o Azure Data Factory | Microsoft Docs
description: "Saiba como copiar dados de um arquivo de dados no local para a cloud do Azure mediante a utilização de um integration runtime autoalojado no Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/22/2018
ms.author: jingwang
ms.openlocfilehash: 221af59c211cc6ce0471718908db1544ca2d75ed
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/23/2018
---
# <a name="tutorial-copy-data-from-an-on-premises-sql-server-database-to-azure-blob-storage"></a>Tutorial: copiar dados de uma base de dados SQL Server no local para o Armazenamento de Blobs do Azure
Neste tutorial, vai utilizar o Azure PowerShell para criar um pipeline de fábrica de dados que copia dados de uma base de dados do SQL Server no local para o armazenamento de Blobs do Azure. Vai criar e utilizar um runtime de integração autoalojado, que move dados entre arquivos de dados no local e na cloud. 

> [!NOTE]
> Este artigo aplica-se à versão 2 do Azure Data Factory, que está atualmente em pré-visualização. Se estiver a utilizar a versão 1 do serviço Data Factory, que está disponível em geral (GA), veja a [documentação da versão 1 do Data Factory](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Este artigo não disponibiliza uma introdução detalhada do serviço Data Factory. Para obter mais informações, veja [Introdução ao Azure Data Factory](introduction.md). 

Neste tutorial, vai executar os seguintes passos:

> [!div class="checklist"]
> * Criar uma fábrica de dados.
> * Crie um integration runtime autoalojado.
> * Criar serviços ligados do SQL Server e do Armazenamento do Azure. 
> * Criar conjuntos de dados do SQL Server e dos Blobs do Azure.
> * Criar um pipeline com uma atividade de cópia para mover os dados.
> * Iniciar uma execução de pipeline.
> * Monitorizar a execução do pipeline.

## <a name="prerequisites"></a>Pré-requisitos
### <a name="azure-subscription"></a>Subscrição do Azure
Antes de começar, se não tiver uma subscrição do Azure, [crie uma conta gratuita](https://azure.microsoft.com/free/).

### <a name="azure-roles"></a>Funções do Azure
Para criar instâncias de fábricas de dados, a conta de utilizador que utiliza para iniciar sessão no Azure tem de ter atribuída a função *contribuidor* ou *proprietário* ou ser *administradora* da subscrição do Azure. 

Para ver as permissões que a sua subscrição tem, aceda ao portal do Azure, selecione o seu nome de utilizador, no canto superior direito, e selecione **Permissões**. Se tiver acesso a várias subscrições, selecione a subscrição apropriada. Para obter instruções de exemplo sobre como adicionar um utilizador a uma função, veja o artigo [Add roles](../billing/billing-add-change-azure-subscription-administrator.md) (Adicionar funções).

### <a name="sql-server-2014-2016-and-2017"></a>SQL Server 2014, 2016 e 2017
Neste tutorial, vai utilizar uma base de dados do SQL Server no local como um arquivo de dados de *origem*. O pipeline da fábrica de dados que vai criar neste tutorial copia dados desta base de dados do SQL Server no local (origem) para o Armazenamento de blobs do Azure (sink). Vai criar uma tabela com o nome **emp** na sua base de dados do SQL Server e insira duas entradas de exemplo na mesma. 

1. Inicie o SQL Server Management Studio. Se ainda não estiver instalado no seu computador, aceda a [Transferir o SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms). 

2. Utilize as suas credenciais para se ligar à sua instância do SQL Server. 

3. Crie uma base de dados de exemplo. Na vista de árvore, clique com o botão direito do rato em **Bases de Dados** e selecione **Nova Base de Dados**. 
 
4. Na janela **Nova Base de Dados**, introduza um nome para a base de dados e selecione **OK**. 

5. Para criar a tabela **emp** e inserir alguns dados de exemplo na mesma, execute o script de consulta seguinte na base de dados:

   ```
       INSERT INTO emp VALUES ('John', 'Doe')
       INSERT INTO emp VALUES ('Jane', 'Doe')
       GO
   ```

6. Na vista de árvore, clique com o botão direito do rato na base de dados que criou e selecione **Nova Consulta**.

### <a name="azure-storage-account"></a>Conta de armazenamento do Azure
Neste tutorial, vai utilizar uma Conta de Armazenamento do Azure de fins gerais (mais concretamente, o Armazenamento de Blobs do Azure) como arquivo de dados de destino/sink. Se não tiver uma conta de armazenamento do Azure para fins gerais, veja [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account). O pipeline da fábrica de dados que vai criar neste tutorial copia dados da base de dados do SQL Server no local (origem) para este armazenamento de Blobs do Azure (sink). 

#### <a name="get-storage-account-name-and-account-key"></a>Obter o nome e a chave da conta de armazenamento
Utilize o nome e a chave da sua conta de armazenamento do Azure neste tutorial. Obtenha o nome e a chave da sua conta de armazenamento da seguinte forma: 

1. Inicie sessão no [portal do Azure](https://portal.azure.com) com o seu nome de utilizador e sua palavra-passe do Azure. 

2. No painel do lado esquerdo, selecione **Mais Serviços**, utilize a palavra-chave **Armazenamento** para filtrar e selecione **Contas de Armazenamento**.

    ![Procurar contas de armazenamento](media/tutorial-hybrid-copy-powershell/search-storage-account.png)

3. Na lista das contas de armazenamento, filtre para encontrar a sua conta de armazenamento (se necessário) e selecione-a. 

4. Na janela **Conta de armazenamento**, selecione **Chaves de acesso**.

    ![Obter o nome e a chave da conta de armazenamento](media/tutorial-hybrid-copy-powershell/storage-account-name-key.png)

5. Nas caixas **Nome da conta de armazenamento** e **key1**, copie os valores e cole-os no Bloco de notas ou noutro editor, para utilizar mais adiante no tutorial. 

#### <a name="create-the-adftutorial-container"></a>Criar o contentor adftutorial 
Nesta secção, vai criar um contentor de blobs com o nome **adftutorial** no seu armazenamento de Blobs do Azure. 

1. Na janela **Conta de armazenamento**, mude para a **Descrição Geral** e selecione **Blobs**. 

    ![Selecionar a opção Blobs](media/tutorial-hybrid-copy-powershell/select-blobs.png)

2. Na janela **Serviço de Blob**, selecione **Contentor**. 

    ![Adicionar o botão de contentor](media/tutorial-hybrid-copy-powershell/add-container-button.png)

3. Na janela **Novo Contentor**, na caixa **Nome**, introduza **adftutorial** e selecione **OK**. 

    ![Introduzir o nome do contentor](media/tutorial-hybrid-copy-powershell/new-container-dialog.png)

4. Na lista de contentores, clique em **adftutorial**.  

    ![Selecionar o contentor](media/tutorial-hybrid-copy-powershell/seelct-adftutorial-container.png)

5. Mantenha a janela do **contentor** de **adftutorial** aberta. Vai utilizá-la para verificar o resultado no final deste tutorial. O Data Fabric cria automaticamente a pasta de saída neste contentor, pelo que não precisa de a criar.

    ![Janela do contentor](media/tutorial-hybrid-copy-powershell/container-page.png)

### <a name="windows-powershell"></a>Windows PowerShell

#### <a name="install-azure-powershell"></a>Instalar o Azure PowerShell
Instale a versão mais recente do Azure PowerShell, se ainda não a tiver no seu computador. 

1. Aceda a [Transferências de SDKs do Azure](https://azure.microsoft.com/downloads/). 

2. Em **Ferramentas da linha de comandos**, na secção **PowerShell**, selecione **Instalação do Windows**. 

3. Para instalar o Azure PowerShell, execute o ficheiro MSI. 

Para obter informações detalhadas, veja [Como instalar e configurar o Azure PowerShell](/powershell/azure/install-azurerm-ps). 

#### <a name="log-in-to-powershell"></a>Iniciar sessão no PowerShell

1. Inicie o PowerShell no seu computador e mantenha-o aberto até concluir este tutorial de início rápido. Se o fechar e reabrir, terá de executar os comandos novamente.

    ![Iniciar o PowerShell](media/tutorial-hybrid-copy-powershell/search-powershell.png)

2. Execute o comando seguinte e introduza o nome de utilizador e a palavra-passe do Azure que utiliza para iniciar sessão no portal do Azure:
       
    ```powershell
    Login-AzureRmAccount
    ```        

3. Se tiver várias subscrições do Azure, execute o comando seguinte selecionar aquela com que pretende trabalhar. Substitua **SubscriptionId** pelo ID da sua subscrição do Azure:

    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<SubscriptionId>"       
    ```

## <a name="create-a-data-factory"></a>Criar uma fábrica de dados

1. Defina uma variável para o nome do grupo de recursos que vai utilizar mais tarde nos comandos do PowerShell. Copie o texto do comando seguinte para o PowerShell, especifique um nome para o [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) (entre aspas duplas, como, por exemplo, `"adfrg"`) e execute o comando. 
   
     ```powershell
    $resourceGroupName = "ADFTutorialResourceGroup"
    ```

2. Para criar o grupo de recursos do Azure, execute o comando abaixo: 

    ```powershell
    New-AzureRmResourceGroup $resourceGroupName $location
    ``` 

    Se o grupo de recursos já existir, pode não substituí-lo. Atribua outro valor à variável `$resourceGroupName` e execute novamente o comando.

3. Defina uma variável para o nome da fábrica de dados que possa utilizar em comandos do PowerShell mais tarde. O nome tem de começar com uma letra ou um número e só pode conter letras, números e o caráter de travessão (-).

    > [!IMPORTANT]
    >  Atualize o nome da fábrica de dados com um que seja globalmente exclusivo. Por exemplo, ADFTutorialFactorySP1127. 

    ```powershell
    $dataFactoryName = "ADFTutorialFactory"
    ```

4. Defina uma variável para a localização da fábrica de dados: 

    ```powershell
    $location = "East US"
    ```  

5. Para criar a fábrica de dados, execute o cmdlet `Set-AzureRmDataFactoryV2`: 
    
    ```powershell       
    Set-AzureRmDataFactoryV2 -ResourceGroupName $resourceGroupName -Location $location -Name $dataFactoryName 
    ```

> [!NOTE]
> 
> * O nome da fábrica de dados tem de ser globalmente exclusivo. Se receber o erro seguinte, altere o nome e tente novamente.
>    ```
>    The specified data factory name 'ADFv2TutorialDataFactory' is already in use. Data factory names must be globally unique.
>    ```
> * Para criar instâncias de fábricas de dados, a conta de utilizador que utiliza para iniciar sessão no Azure tem de ter atribuída a função *contribuidor* ou *proprietário* ou ser *administradora* da subscrição do Azure.
> * Atualmente, se utilizar a versão 2 do Data Factory, só pode criar fábricas de dados nas regiões E.U.A. Leste, E.U.A. Leste 2 e Europa Ocidental. Os arquivos de dados (Armazenamento do Azure, Base de Dados SQL do Azure, etc.) e as computações (Azure HDInsight, etc.) que a fábrica de dados utiliza podem estar noutras regiões.
> 
> 

## <a name="create-a-self-hosted-integration-runtime"></a>Criar um integration runtime autoalojado

Nesta secção, vai criar um integration runtime autoalojado e vai associá-lo a um computador no local com a base de dados do SQL Server. O integration runtime autoalojado é o componente que copia os dados da base de dados SQL Server no seu computador para o armazenamento de Blobs do Azure. 

1. Crie uma variável para o nome do runtime de integração. Utilize um nome exclusivo e aponte-o. Vai utilizá-lo mais tarde no tutorial. 

    ```powershell
   $integrationRuntimeName = "ADFTutorialIR"
    ```

2. Crie um integration runtime autoalojado. 

    Segue-se o resultado do exemplo:

    ```json
    Id                : /subscriptions/<subscription ID>/resourceGroups/ADFTutorialResourceGroup/providers/Microsoft.DataFactory/factories/onpremdf0914/integrationruntimes/myonpremirsp0914
    Type              : SelfHosted
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Name              : myonpremirsp0914
    Description       :
    ```

3. Para obter o estado do integration runtime criado, execute o comando seguinte:

    ```powershell
   Get-AzureRmDataFactoryV2IntegrationRuntime -name $integrationRuntimeName -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -Status
    ```

    Segue-se o resultado do exemplo:
    
    ```json
    Nodes                     : {}
    CreateTime                : 9/14/2017 10:01:21 AM
    InternalChannelEncryption :
    Version                   :
    Capabilities              : {}
    ScheduledUpdateDate       :
    UpdateDelayOffset         :
    LocalTimeZoneOffset       :
    AutoUpdate                :
    ServiceUrls               : {eu.frontend.clouddatahub.net, *.servicebus.windows.net}
    ResourceGroupName         : <ResourceGroup name>
    DataFactoryName           : <DataFactory name>
    Name                      : <Integration Runtime name>
    State                     : NeedRegistration
    ```

4. Para obter as *chaves de autenticação* para registar o integration runtime autoalojado no serviço Data Factory na cloud, execute o comando seguinte. Copie uma das chaves (excluindo as aspas) para registar o integration runtime autoalojado que vai instalar no computador no passo seguinte: 

    ```powershell
    Get-AzureRmDataFactoryV2IntegrationRuntimeKey -Name $integrationRuntimeName -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName | ConvertTo-Json
    ```
    
    Segue-se o resultado do exemplo:
    
    ```json
    {
        "AuthKey1":  "IR@0000000000-0000-0000-0000-000000000000@xy0@xy@xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx=",
        "AuthKey2":  "IR@0000000000-0000-0000-0000-000000000000@xy0@xy@yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy="
    }
    ```

## <a name="install-the-integration-runtime"></a>Instalar o integration runtime
1. Transfira o [Integration Runtime do Azure Data Factory](https://www.microsoft.com/download/details.aspx?id=39717) num computador Windows local e execute a instalação. 

2. No assistente **Bem-vindo à Configuração do Microsoft Integration Runtime** , selecione**Seguinte**.  

3. Na janea **Contrato de Licença do Utilizador Final**, aceite os termos e o contrato de licença e selecione **Seguinte**. 

4. Na janela **Pasta de Destino**, selecione **Seguinte**. 

5. Na janela **Pronto para instalar o Microsoft Integration Runtime**, selecione **Instalar**. 

6. Se vir uma mensagem de erro que diz que o computador está a ser configurado para entrar no modo de suspensão ou hibernação quando não estiver a ser utilizado, selecione **OK**. 

7. Se a janela **Opções de Energia** for apresentada, feche-a e mude para a janela de configuração. 

8. No assistente **Configuração do Microsoft Integration Runtime Concluída**, selecione **Concluir**.

9. Na janela **Registar o Integration Runtime (Autoalojado)**, cole a chave que guardou na secção anterior e selecione **Registar**. 

    ![Registar o integration runtime](media/tutorial-hybrid-copy-powershell/register-integration-runtime.png)

    Quando o integration runtime autoalojado for registado com êxito, é apresentada a mensagem seguinte: 

    ![Registado com êxito](media/tutorial-hybrid-copy-powershell/registered-successfully.png)

10. Na janela **Novo Nó do Integration Runtime (Autoalojado)**, selecione **Seguinte**. 

    ![Janela Novo Nó do Integration Runtime](media/tutorial-hybrid-copy-powershell/new-integration-runtime-node-page.png)

11. Na janela **Canal de Comunicação da Intranet**, selecione **Ignorar**.  
    Pode selecionar a certificação TLS/SSL para proteger a comunicação intra-nós num ambiente de runtime de integração de vários nós.

    ![Janela de canal comunicação da Intranet](media/tutorial-hybrid-copy-powershell/intranet-communication-channel-page.png)

12. Na janela **Registar Integration Runtime (Autoalojado)**, selecione **Configuration Manager**. 

13. Quando o nó for ligado ao serviço cloud, é apresentada a página seguinte:

    ![O nó está ligado](media/tutorial-hybrid-copy-powershell/node-is-connected.png)

14. Teste a conectividade à base de dados do SQL Server, fazendo o seguinte:

    ![Separador Diagnóstico](media/tutorial-hybrid-copy-powershell/config-manager-diagnostics-tab.png)   

    a. Na janela do **Configuration Manager**, mude para o separador **Diagnósticos**.

    b. Na caixa **Tipo de origem de dados**, selecione **SqlServer**.

    c. Introduza o nome do servidor.

    d. Introduza o nome da base de dados. 

    e. Selecione o modo de autenticação. 

    f. Introduza o nome de utilizador. 

    g. Introduza a palavra-passe que está associado ao nome de utilizador.

    h. Para confirmar que o integration runtime se consegue ligar ao SQL Server selecione **Testar**.  
    Se a ligação for bem-sucedida, é apresentada uma marca de verificação verde. Caso contrário, receberá uma mensagem de erro associada à falha. Corrija os problemas e confirme que o integration runtime se consegue ligar à sua instância do SQL Server.

    Aponte todos os valores anteriores para utilizar mais adiante neste tutorial.
    
## <a name="create-linked-services"></a>Criar serviços ligados
Para ligar os seus arquivos de dados e serviços de computação à fábrica de dados, crie serviços ligados na mesma. Neste tutorial, vai associar a sua conta de armazenamento do Azure e a instância do SQL Server no local ao arquivo de dados. Os serviços ligados têm as informações de ligação que o serviço do Data Factory utiliza no runtime para se ligar aos mesmos. 

### <a name="create-an-azure-storage-linked-service-destinationsink"></a>Criar um serviço ligado do Armazenamento do Azure (destino/sink)
Neste passo, vai ligar a sua conta de armazenamento do Azure à fábrica de dados.

1. Crie um ficheiro JSON com o nome *AzureStorageLinkedService.json* na pasta *C:\ADFv2Tutorial* com o código seguinte. Se a pasta *ADFv2Tutorial* ainda não existir, crie-a.  

    > [!IMPORTANT]
    > Antes de guardar o ficheiro, substitua \<accountName> e \<accountKey> pelo nome e a chave da sua conta de armazenamento do Azure. Estas informações foram apontadas na secção [Pré-requisitos](#get-storage-account-name-and-account-key).

   ```json
    {
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>;EndpointSuffix=core.windows.net"
                }
            }
        },
        "name": "AzureStorageLinkedService"
    }
   ```

2. No PowerShell, mude para a pasta *C:\ADFv2Tutorial*.

3. Para criar o serviço ligado AzureStorageLinkedService, execute o cmdlet `Set-AzureRmDataFactoryV2LinkedService`: 

   ```powershell
   Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $ResourceGroupName -Name "AzureStorageLinkedService" -File ".\AzureStorageLinkedService.json"
   ```

   Eis uma saída de exemplo:

    ```json
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureStorageLinkedService
    ```

    Se receber o erro "Ficheiro não encontrado", execute o comando `dir` para confirmar que existe. Se o nome de ficheiro tiver a extensão *.txt* (por exemplo, AzureStorageLinkedService.json.txt), remove-a e execute novamente o comando do PowerShell. 

### <a name="create-and-encrypt-a-sql-server-linked-service-source"></a>Criar e encriptar um serviço ligado do SQL Server (origem)
Neste passo, vai ligar a instância do SQL Server no local à fábrica de dados.

1. Crie um ficheiro JSON com o nom *SqlServerLinkedService.json* na pasta *C:\ADFv2Tutorial*, mediante o código seguinte:

    > [!IMPORTANT]
    > Selecione a secção que tem como base a autenticação que utiliza para se ligar ao SQL Server.

    **Ligar com a Autenticação SQL (sa):**

    ```json
    {
        "properties": {
            "type": "SqlServer",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=<servername>;Database=<databasename>;User ID=<username>;Password=<password>;Timeout=60"
                }
            },
            "connectVia": {
                "type": "integrationRuntimeReference",
                "referenceName": "<integration runtime name>"
            }
        },
        "name": "SqlServerLinkedService"
    }
   ```    

    **Utilizar a autenticação do Windows:**

    ```json
    {
        "properties": {
            "type": "SqlServer",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=<server>;Database=<database>;Integrated Security=True"
                },
                "userName": "<user> or <domain>\\<user>",
                "password": {
                    "type": "SecureString",
                    "value": "<password>"
                }
            },
            "connectVia": {
                "type": "integrationRuntimeReference",
                "referenceName": "<integration runtime name>"
            }
        },
        "name": "SqlServerLinkedService"
    }    
    ```

    > [!IMPORTANT]
    > - Selecione a secção que tem como base a autenticação que utiliza para se ligar à sua instância do SQL Server.
    > - Substitua **\<integration runtime name>** pelo nome do integration runtime.
    > - Antes de guardar o ficheiro, substitua **\<servername>**, **\<databasename>**, **\<username>** e **\<password>** pelos valores da sua instância do SQL Server.
    > - Se precisar de utilizar um caráter de barra invertida (\\) no nome da sua conta de utilizador ou no nome do seu servidor, utilize o caráter de escape (\\) como prefixo. Por exemplo, utilize *omeudominion\\\\omeuutilizador*. 

2. Para encriptar os dados confidenciais (nome de utilizador, palavra-passe, etc.), execute o cmdlet `New-AzureRmDataFactoryV2LinkedServiceEncryptedCredential`.  
    Esta encriptação garante que as credenciais são encriptadas com a interface DPAPI (Data Protection Application Programming Interface). As credenciais encriptadas são armazenadas loclamente no nó do runtime de integração autoalojado (computador local). O payload de saída pode ser redirecionado para outro ficheiro JSON (neste caso, *encryptedLinkedService.json*) que contém credenciais encriptadas.
    
   ```powershell
   New-AzureRmDataFactoryV2LinkedServiceEncryptedCredential -DataFactoryName $dataFactoryName -ResourceGroupName $ResourceGroupName -IntegrationRuntimeName $integrationRuntimeName -File ".\SQLServerLinkedService.json" > encryptedSQLServerLinkedService.json
   ```

3. Execute o comando seguinte, que cria EncryptedSqlServerLinkedService:

   ```powershell
   Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $ResourceGroupName -Name "EncryptedSqlServerLinkedService" -File ".\encryptedSqlServerLinkedService.json"
   ```


## <a name="create-datasets"></a>Criar conjuntos de dados
Neste passo, vai criar conjuntos de dados de entrada e saída. Estes representam os dados de entrada e de saída da operação de cópia, que copia dados da base de dados do SQL Server no local para o armazenamento de Blobs do Azure.

### <a name="create-a-dataset-for-the-source-sql-server-database"></a>Criar um conjunto de dados para a base de dados SQL de origem
Neste passo, vai definir um conjunto de dados que representa os dados na instância da base de dados do SQL Server. O conjunto de dados é do tipo SqlServerTable. Faz referência ao serviço ligado SQL Server que criou no passo anterior. O serviço ligado tem as informações de ligação que o serviço do Data Factory utiliza para se ligar à sua instância do SQL Server no runtime. Este conjunto de dados especifica a tabela SQL na base de dados que contém os dados. Neste tutorial, a tabela **emp** contém a origem de dados. 

1. Crie um ficheiro JSON com o nome *SqlServerDataset.json* na pasta *C:\ADFv2Tutorial*, com o código seguinte:  

    ```json
    {
       "properties": {
            "type": "SqlServerTable",
            "typeProperties": {
                "tableName": "dbo.emp"
            },
            "structure": [
                 {
                    "name": "ID",
                    "type": "String"
                },
                {
                    "name": "FirstName",
                    "type": "String"
                },
                {
                    "name": "LastName",
                    "type": "String"
                }
            ],
            "linkedServiceName": {
                "referenceName": "EncryptedSqlServerLinkedService",
                "type": "LinkedServiceReference"
            }
        },
        "name": "SqlServerDataset"
    }
    ```

2. Para criar o conjunto de dados SqlServerDataset, execute o cmdlet `Set-AzureRmDataFactoryV2Dataset`.

    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SqlServerDataset" -File ".\SqlServerDataset.json"
    ```

    Segue-se o resultado do exemplo:

    ```json
    DatasetName       : SqlServerDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Structure         : {"name": "ID" "type": "String", "name": "FirstName" "type": "String", "name": "LastName" "type": "String"}
    Properties        : Microsoft.Azure.Management.DataFactory.Models.SqlServerTableDataset
    ```

### <a name="create-a-dataset-for-azure-blob-storage-sink"></a>Criar um conjunto de dados para o armazenamento de Blobs do Azure (sink)
Neste passo, vai definir um conjunto de dados que representa os dados que vão ser copiados para o armazenamento de Blobs do Azure. O conjunto de dados é do tipo AzureBlob. Faz referência ao serviço ligado Armazenamento do Azure que criou anteriormente neste tutorial. 

O serviço ligado tem as informações de ligação que a fábrica de dados utiliza no runtime para se ligar à sua conta de armazenamento do Azure. Este conjunto de dados especifica a pasta no armazenamento do Azure para o qual os dados são copiados a partir da base de dados SQL Server. Neste tutorial, a pasta é *adftutorial/fromonprem*, em que `adftutorial` é o contentor de blobs e `fromonprem` é a pasta. 

1. Crie um ficheiro JSON com o nome *AzureBlobDataset.json* na pasta *C:\ADFv2Tutorial*, com o código seguinte:

    ```json
    {
        "properties": {
            "type": "AzureBlob",
            "typeProperties": {
                "folderPath": "adftutorial/fromonprem",
                "format": {
                    "type": "TextFormat"
                }
            },
            "linkedServiceName": {
                "referenceName": "AzureStorageLinkedService",
                "type": "LinkedServiceReference"
            }
        },
        "name": "AzureBlobDataset"
    }
    ```

2. Para criar o conjunto de dados AzureBlobDataset, execute o cmdlet `Set-AzureRmDataFactoryV2Dataset`.

    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureBlobDataset" -File ".\AzureBlobDataset.json"
    ```

    Segue-se o resultado do exemplo:

    ```json
    DatasetName       : AzureBlobDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureBlobDataset
    ```

## <a name="create-a-pipeline"></a>Criar um pipeline
Neste tutorial, vai criar um pipeline com uma atividade de cópia. A atividade de cópia utiliza SqlServerDataset como o conjunto de dados de entrada e AzureBlobDataset como o conjunto de dados de saída. O tipo de origem está definido como *SqlSource* e o tipo de sink como *BlobSink*.

1. Crie um ficheiro JSON com o nome *SqlServerToBlobPipeline.json* na pasta *C:\ADFv2Tutorial*, com o código seguinte:

    ```json
    {
       "name": "SQLServerToBlobPipeline",
        "properties": {
            "activities": [       
                {
                    "type": "Copy",
                    "typeProperties": {
                        "source": {
                            "type": "SqlSource"
                        },
                        "sink": {
                            "type":"BlobSink"
                        }
                    },
                    "name": "CopySqlServerToAzureBlobActivity",
                    "inputs": [
                        {
                            "referenceName": "SqlServerDataset",
                            "type": "DatasetReference"
                        }
                    ],
                    "outputs": [
                        {
                            "referenceName": "AzureBlobDataset",
                            "type": "DatasetReference"
                        }
                    ]
                }
            ]
        }
    }
    ```

2. Para criar o pipeline SQLServerToBlobPipeline, execute o cmdlet `Set-AzureRmDataFactoryV2Pipeline`.

    ```powershell
    Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SQLServerToBlobPipeline" -File ".\SQLServerToBlobPipeline.json"
    ```

    Segue-se o resultado do exemplo:

    ```json
    PipelineName      : SQLServerToBlobPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Activities        : {CopySqlServerToAzureBlobActivity}
    Parameters        :  
    ```

## <a name="create-a-pipeline-run"></a>Criar uma execução de pipeline
Inicie uma execução de pipeline para o pipeline SQLServerToBlobPipeline e capture o ID de execução do pipeline para monitorização futura.

```powershell
$runId = Invoke-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineName 'SQLServerToBlobPipeline'
```

## <a name="monitor-the-pipeline-run"></a>Monitorizar a execução do pipeline.

1. Para verificar continuamente o estado de execução do pipeline SQLServerToBlobPipeline, execute o script seguinte no PowerShell e imprima o resultado final:

    ```powershell
    while ($True) {
        $result = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $runId -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)

        if (($result | Where-Object { $_.Status -eq "InProgress" } | Measure-Object).count -ne 0) {
            Write-Host "Pipeline run status: In Progress" -foregroundcolor "Yellow"
            Start-Sleep -Seconds 30
        }
        else {
            Write-Host "Pipeline 'SQLServerToBlobPipeline' run finished. Result:" -foregroundcolor "Yellow"
            $result
            break
        }
    }
    ```

    Eis o resultado da execução de exemplo:

    ```jdon
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    ActivityName      : copy
    PipelineRunId     : 4ec8980c-62f6-466f-92fa-e69b10f33640
    PipelineName      : SQLServerToBlobPipeline
    Input             :  
    Output            :  
    LinkedServiceName :
    ActivityRunStart  : 9/13/2017 1:35:22 PM
    ActivityRunEnd    : 9/13/2017 1:35:42 PM
    DurationInMs      : 20824
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    ```

2. Pode executar o comando seguinte para obter o ID de execução do pipeline SQLServerToBlobPipeline e verificar o resultado da execução de atividade detalhado: 

    ```powershell
    Write-Host "Pipeline 'SQLServerToBlobPipeline' run result:" -foregroundcolor "Yellow"
    ($result | Where-Object {$_.ActivityName -eq "CopySqlServerToAzureBlobActivity"}).Output.ToString()
    ```

    Eis o resultado da execução de exemplo:

    ```json
    {
      "dataRead": 36,
      "dataWritten": 24,
      "rowsCopied": 2,
      "copyDuration": 3,
      "throughput": 0.01171875,
      "errors": [],
      "effectiveIntegrationRuntime": "MyIntegrationRuntime",
      "billedDuration": 3
    }
    ```

## <a name="verify-the-output"></a>Verificar a saída
O pipeline cria automaticamente a pasta de saída com o nome *fromonprem* no contentor de blobs `adftutorial`. Confirme que consegue ver o ficheiro *dbo.emp.txt* na pasta de saída. 

1. No portal do Azure, na janela do contentor **adftutorial**, selecione **Atualizar** para ver a pasta de saída.

    ![Pasta de saída criada](media/tutorial-hybrid-copy-powershell/fromonprem-folder.png)
2. Selecione `fromonprem` na lista de pastas. 
3. Confirme que vê um ficheiro com o nome `dbo.emp.txt`.

    ![Ficheiro de saída](media/tutorial-hybrid-copy-powershell/fromonprem-file.png)


## <a name="next-steps"></a>Passos seguintes
O pipeline neste exemplo copia dados de uma localização para outra localização no amazenamento de Bobs do Azure. Aprendeu a:

> [!div class="checklist"]
> * Criar uma fábrica de dados.
> * Crie um integration runtime autoalojado.
> * Criar serviços ligados do SQL Server e do Armazenamento do Azure. 
> * Criar conjuntos de dados do SQL Server e dos Blobs do Azure.
> * Criar um pipeline com uma atividade de cópia para mover os dados.
> * Iniciar uma execução de pipeline.
> * Monitorizar a execução do pipeline.

Para obter uma lista dos arquivos de dados que o Data Factory suporta, veja [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) (Arquivos de Dados suportados).

Para aprender a copiar dados em massa de uma origem para um destino, avance para o tutorial seguinte:

> [!div class="nextstepaction"]
>[Copiar dados em massa](tutorial-bulk-copy.md)
