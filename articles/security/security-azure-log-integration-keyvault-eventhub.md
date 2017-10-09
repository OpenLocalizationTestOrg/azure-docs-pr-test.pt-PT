---
title: registos de aaaIntegrate a partir do Cofre de chaves do Azure com os Hubs de eventos | Microsoft Docs
description: "Tutorial que fornece os passos necessários de Olá toomake Cofre de chaves de registo disponível tooa SIEM utilizando a integração de registo do Azure"
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a>Tutorial de integração de registo do Azure: eventos de Cofre de chaves do Azure de processo ao utilizar os Hubs de eventos

Pode utilizar a integração de registo do Azure tooretrieve registado eventos e torná-los tooyour disponíveis informações e event management (SIEM) sistema de segurança. Este tutorial mostra um exemplo de como a integração de registo do Azure podem ser utilizados tooprocess registos adquiridos junto de Event Hubs do Azure.
 
Utilize este tutorial tooget acquainted com a forma como a integração de registo do Azure e do Event Hubs trabalho em conjunto pela seguinte Olá passos de exemplo e compreender a forma como cada passo suporta solução Olá. Em seguida, pode tirar o que aprendeu aqui toocreate o seus próprios toosupport passos requisitos exclusivos da sua empresa.

>[!WARNING]
passos de Olá e comandos neste tutorial não são toobe pretendido copiados e colados. Se estiver a apenas exemplos. Não utilize comandos do PowerShell Olá "tal como está" no seu ambiente em direto. Devem ser personalizadas com base no seu ambiente exclusivo.


Este tutorial orienta-o através de processo de Olá de colocar o hub de eventos do Cofre de chaves do Azure atividade tooan com sessão iniciada e disponibilizar como sistema do JSON ficheiros tooyour SIEM. Em seguida, pode configurar os SIEM sistema tooprocess Olá JSON os ficheiros.

>[!NOTE]
>A maior parte dos passos deste tutorial Olá envolve configurar cofres de chaves, contas de armazenamento e dos event hubs. os passos de integração de registo do Azure específicos Olá estão no final deste tutorial Olá. Não execute estes passos num ambiente de produção. Estes destinam-se apenas num ambiente de laboratório. Tem de personalizar os passos de Olá antes de os utilizar na produção.

Foram fornecidas informações ao longo de ajuda de forma Olá que compreender motivos Olá atrás de cada passo. Artigos de tooother ligações dão-lhe mais detalhes em determinados tópicos.

Para obter mais informações sobre os serviços de Olá menciona suportadas neste tutorial, consulte: 

- [Cofre de Chaves do Azure](../key-vault/key-vault-whatis.md)
- [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)
- [Integração de registos do Azure](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a>Configuração inicial

Antes de concluir os passos de Olá neste artigo, é necessário o seguinte Olá:

1. Uma subscrição do Azure e a conta que subscrição com direitos de administrador. Se não tiver uma subscrição, pode criar um [conta gratuita](https://azure.microsoft.com/free/).
 
2. Um sistema com toohello de acesso à internet que cumpra Olá os requisitos para instalar a integração de registo do Azure. sistema Olá alojado no local ou pode ser num serviço em nuvem.

3. [Integração de registo do Azure](https://www.microsoft.com/download/details.aspx?id=53324) instalado. tooinstall-lo:

   a. Utilize o sistema toohello tooconnect de ambiente de trabalho remoto mencionado no passo 2.   
   b. Copie o sistema de toohello instalador do Olá a integração de registo do Azure. Pode [transferir ficheiros de instalação de Olá](https://www.microsoft.com/download/details.aspx?id=53324).   
   c. Inicie o instalador Olá e aceitar os termos de licenciamento de Software do Olá Microsoft.   
   d. Se irá fornecer informações de telemetria, deixe a caixa de verificação de Olá selecionada. Se seria não enviar tooMicrosoft de informações de utilização, desmarque a caixa de verificação de Olá.
   
   Para obter mais informações sobre a integração de registo do Azure e como tooinstall-lo, consulte [a integração de registo do Azure com o registo de diagnóstico do Azure e o reencaminhamento de eventos do Windows](security-azure-log-integration-get-started.md).

4. versão de PowerShell mais recente Olá.
 
   Se tiver instalado o Windows Server 2016, em seguida, tiver, pelo menos, PowerShell 5.0. Se estiver a utilizar qualquer outra versão do Windows Server, poderá ter uma versão anterior do PowerShell instalada. Pode verificar a versão de Olá introduzindo ```get-host``` numa janela do PowerShell. Se não tiver PowerShell 5.0 instalado, pode [transferi-lo](https://www.microsoft.com/download/details.aspx?id=50395).

   Depois de ter, pelo menos, PowerShell 5.0, pode continuar a versão mais recente do tooinstall Olá:
   
   a. Na janela do PowerShell, introduza Olá ```Install-Module Azure``` comando. Conclua os passos de instalação de Olá.    
   b. Introduza Olá ```Install-Module AzureRM``` comando. Conclua os passos de instalação de Olá.

   Para obter mais informações, consulte [instalar o Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).


## <a name="create-supporting-infrastructure-elements"></a>Criar suporte de infraestrutura de elementos

1. Abra uma janela elevada do PowerShell e aceda demasiado**C:\Program Files\Microsoft Azure registo integração**.
2. Importe Olá AzLog cmdlets ao executar o script de Olá LoadAzLogModule.ps1. Introduza Olá `.\LoadAzLogModule.ps1` comando. (Olá de aviso ". \ \" nesse comando.) Deverá ver algo semelhante ao seguinte:</br>

   ![Lista de módulos carregados](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. Introduza Olá `Login-AzureRmAccount` comando. Na janela de início de sessão de Olá, introduza as informações de credencial de Olá para a subscrição de Olá que irá utilizar para este tutorial.

   >[!NOTE]
   >Se este for Olá pela primeira vez que está a registar no tooAzure desta máquina, verá uma mensagem sobre dados de utilização do Microsoft toocollect do PowerShell. Recomendamos que ative a recolha de dados porque será utilizado tooimprove Azure PowerShell.

4. Após a autenticação com êxito, tem sessão iniciada e ver informações Olá Olá seguinte captura de ecrã. Tome nota do nome de ID e a subscrição da subscrição Olá, porque irá precisar deles mais tarde passos toocomplete.

   ![Janela do PowerShell](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. Crie variáveis toostore valores que serão utilizados mais tarde. Introduza cada um dos Olá seguintes linhas de PowerShell. Poderá ser necessário tooadjust Olá valores toomatch no seu ambiente.
    - ```$subscriptionName = ‘Visual Studio Ultimate with MSDN’```(O nome da sua subscrição poderão ser diferente. Pode vê-lo como parte da saída de Olá do comando anterior Olá.)
    - ```$location = 'West US'```(Esta variável será onde devem ser criados os recursos de localização do Olá toopass utilizados. Pode alterar esta variável toobe qualquer localização da sua escolha.)
    - ```$random = Get-Random```
    - ``` $name = 'azlogtest' + $random```(nome de Olá pode ser qualquer coisa, mas deve incluir apenas letras minúsculas e números).
    - ``` $storageName = $name```(Esta variável será utilizada para o nome de conta de armazenamento Olá).
    - ```$rgname = $name ```(Esta variável será utilizada para o nome do grupo de recursos de Olá).
    - ``` $eventHubNameSpaceName = $name```(Este é o nome de Olá do espaço de nomes de hub de eventos de Olá.)
6. Especifique a subscrição de Olá com os quais irão trabalhar com:
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. Criar um grupo de recursos:
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   Se introduzir `$rg` neste momento, deverá ver a captura de ecrã saída semelhante toothis:

   ![Saída após a criação de um grupo de recursos](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. Crie uma conta de armazenamento que será utilizado tookeep controlar de informações de estado:
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. Crie o espaço de nomes de hub de eventos de Olá. Isto é necessário toocreate um hub de eventos.
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. Obter ID de regra de Olá que será utilizado com o fornecedor de insights Olá:
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. Obter todas as localizações do Azure possíveis e adicionar Olá nomes tooa variável que pode ser utilizado num passo posterior:
    
    a. ```$locationObjects = Get-AzureRMLocation```    
    b. ```$locations = @('global') + $locationobjects.location```
    
    Se introduzir `$locations` neste momento, ver os nomes de localização de Olá sem informações adicionais de Olá devolvidas pelo Get-AzureRmLocation.
12. Crie um perfil de registo do Gestor de recursos do Azure: 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    Para mais informações sobre Olá perfil de registos do Azure, consulte [descrição geral do Olá registo de atividade do Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).

> [!NOTE]
> Poderá receber uma mensagem de erro quando tenta toocreate um perfil de registo. Em seguida, pode rever documentação Olá para Get-AzureRmLogProfile e Remove-AzureRmLogProfile. Se executar Get-AzureRmLogProfile, pode ver informações sobre o perfil de registo Olá. Pode eliminar o perfil de registo existente Olá introduzindo Olá ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` comando.
>
>![Erro de perfil do Gestor de recursos](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a>Criar um cofre de chaves

1. Crie Cofre de chaves de Olá:

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. Configure o registo para o Cofre de chaves Olá:

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a>Gerar a atividade de registo

Pedidos necessitam toobe enviado tooKey atividade de registo do cofre toogenerate. Ações, como a geração de chaves, armazenar segredos, ou ao ler os segredos do Cofre de chaves, irá criar entradas de registo.

1. Apresentar as chaves de armazenamento atual Olá:
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. Gerar um novo **key2**:
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. Voltar a apresentar chaves Olá e ver que **key2** contém um valor diferente:
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. Defina e ler um segredo toogenerate entradas de registo adicionais:
    
   a. ```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b. ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Devolveu secreta](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a>Configurar a integração de registos do Azure

Agora que configurou o hub de eventos de tooan de registo do Cofre de chaves Olá elementos necessários toohave todos os, terá de tooconfigure a integração de registo do Azure:

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

Execute o comando de AzLog Olá para cada hub de eventos:

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

Depois de um minuto ou da execução Olá últimos dois comandos, deve ver ficheiros JSON que está a ser gerados. Pode confirmar que pela monitorização de diretório de Olá **C:\users\AzLog\EventHubJson**.

## <a name="next-steps"></a>Passos seguintes

- [Integração de registos do Azure FAQ](security-azure-log-integration-faq.md)
- [Introdução à integração do registo do Azure](security-azure-log-integration-get-started.md)
- [Integrar o seu sistemas SIEM registos de recursos do Azure](security-azure-log-integration-overview.md)
