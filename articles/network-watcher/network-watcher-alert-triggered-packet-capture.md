---
title: "monitorização com alertas e as funções do Azure de rede de toodo de captura de pacotes aaaUse proativa | Microsoft Docs"
description: Este artigo descreve como toocreate um alerta acionado captura de pacotes com observador de rede do Azure
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a>Captura de pacotes de utilização para a rede proativa monitorização com alertas e as funções do Azure

Captura de pacotes do observador de rede cria captura sessões tootrack tráfego que entra e sai de máquinas virtuais. Olá ficheiro de captura pode ter um filtro que está definido tootrack Olá apenas o tráfego que pretende que o toomonitor. Estes dados, em seguida, são armazenados no blob de armazenamento ou localmente no computador convidado de Olá.

Esta capacidade pode ser iniciada remotamente a partir de outros cenários de automatização, tais como as funções do Azure. Oferece de captura de pacotes que Hello capturas de proativa de capacidade toorun com base no definido anomalias de rede. Outras utilizações incluem a recolha de estatísticas de rede, ao obter informações sobre intrusions de rede, as comunicações de cliente-servidor depuração e muito mais.

Recursos que são implementados no Azure executados 24x7. Utilizador e a sua equipa ativamente não é possível monitorizar o estado de Olá de todos os recursos 24/7. Por exemplo, o que acontece se ocorrer um problema às 2 AM?

Ao utilizar o observador de rede, alertas e funções a partir de Olá ecossistema do Azure, pode responder proativamente com problemas de toosolve de dados e as ferramentas de Olá na sua rede.

![Cenário][scenario]

## <a name="prerequisites"></a>Pré-requisitos

* versão mais recente do Olá do [Azure PowerShell](/powershell/azure/install-azurerm-ps).
* Uma instância existente do observador de rede. Se ainda não tiver um, [criar uma instância do observador de rede](network-watcher-create.md).
* Uma máquina virtual existente no Olá mesma região que o observador de rede com Olá [extensão Windows](../virtual-machines/windows/extensions-nwa.md) ou [extensão da máquina virtual Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="scenario"></a>Cenário

Neste exemplo, a VM está a enviar mais segmentos TCP que o habitual e pretender toobe alertado. Segmentos TCP são utilizados como um exemplo aqui, mas pode utilizar qualquer condição de alerta.

Quando for alertado, quer tooreceive dados ao nível do pacote toounderstand por que motivo aumentou a comunicação. Em seguida, pode tomar medidas comunicação de tooregular tooreturn Olá máquina virtual.

Este cenário pressupõe que tem uma instância existente do observador de rede e um grupo de recursos com uma máquina virtual válida.

Olá a seguir lista é uma descrição geral do fluxo de trabalho de Olá que decorre:

1. Um alerta é acionado na VM.
1. alerta de Olá chama a função do Azure através de um webhook.
1. A função do Azure processa alerta Olá e inicia uma sessão de captura de pacotes do observador de rede.
1. captura de pacotes hello é executado no Olá VM e recolhe tráfego.
1. Olá pacote captura ficheiro é carregado tooa a conta de armazenamento para revisão e diagnósticos adicionais.

tooautomate este processo, iremos criar e ligar-se um alerta no nosso tootrigger VM quando o incidente Olá ocorre. Também iremos criar toocall uma função para o observador de rede.

Este cenário Olá seguintes:

* Cria uma função do Azure que inicia uma captura de pacotes.
* Cria uma regra de alerta numa máquina virtual e configura Olá de toocall de regra de alerta de Olá função do Azure.

## <a name="create-an-azure-function"></a>Criar uma função do Azure

primeiro passo de Olá toocreate um alerta de Olá tooprocess função do Azure e criar uma captura de pacotes.

1. No Olá [portal do Azure](https://portal.azure.com), selecione **novo** > **computação** > **aplicação de função**.

    ![Criar uma aplicação de função][1-1]

2. No Olá **aplicação de função** painel, introduza Olá os seguintes valores e, em seguida, selecione **OK** toocreate Olá aplicação:

    |**Definição** | **Valor** | **Detalhes** |
    |---|---|---|
    |**Nome da aplicação** |PacketCaptureExample|nome da aplicação de função Olá Olá.|
    |**Subscrição**|[Sua subscrição] Olá subscrição para a aplicação de função de Olá toocreate.||
    |**Grupo de Recursos**|PacketCaptureRG|Olá recursos grupo toocontain Olá aplicação de função.|
    |**Plano de alojamento**|Plano de consumo| tipo de Olá de planeie as utilizações de aplicação de função. As opções são consumo ou plano do App Service do Azure. |
    |**Localização**|EUA Central| região Olá na aplicação de função que toocreate Olá.|
    |**Conta de armazenamento**|{gerado automaticamente}| conta de armazenamento de Olá que as funções do Azure necessita de armazenamento para fins gerais.|

3. No Olá **PacketCaptureExample função aplicações** painel, selecione **funções** > **função personalizada**  >  **+**.

4. Selecione **HttpTrigger-Powershell**e, em seguida, introduza Olá restantes informações. Por fim, toocreate Olá função, selecione **criar**.

    |**Definição** | **Valor** | **Detalhes** |
    |---|---|---|
    |**Cenário**|Experimental|Tipo de cenário|
    |**Dar um nome à função**|AlertPacketCapturePowerShell|Nome da função de Olá|
    |**Nível de autorização**|Função|Nível de autorização para a função de Olá|

![Exemplo de funções][functions1]

> [!NOTE]
> modelo de PowerShell Olá é experimental e não tem suporte completo.

As personalizações são necessárias para este exemplo e são explicadas em Olá os seguintes passos.

### <a name="add-modules"></a>Adicionar módulos

toouse cmdlets do PowerShell do observador de rede, carregue Olá mais recente do PowerShell módulo toohello aplicação de função.

1. No seu computador local com módulos Olá mais recentes do Azure PowerShell instalada, execute Olá seguinte comando do PowerShell:

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    Este oferece de exemplo Olá caminho local do seu módulos do PowerShell do Azure. Estas pastas são utilizadas num passo posterior. módulos de Olá que são utilizados neste cenário são:

    * AzureRM.Network

    * AzureRM.Profile

    * AzureRM.Resources

    ![Pastas de PowerShell][functions5]

1. Selecione **as definições de aplicação de função** > **aceda tooApp serviço Editor**.

    ![Definições de aplicação de função][functions2]

1. Contexto Olá **AlertPacketCapturePowershell** pasta e, em seguida, crie uma pasta denominada **azuremodules**. 

4. Crie uma subpasta para cada módulo que precisa.

    ![Pasta e as subpastas][functions3]

    * AzureRM.Network

    * AzureRM.Profile

    * AzureRM.Resources

1. Contexto Olá **AzureRM.Network** subpasta e, em seguida, selecione **carregar ficheiros**. 

6. Aceda tooyour Azure módulos. Olá local **AzureRM.Network** pasta, selecione todos os ficheiros de Olá na pasta Olá. Em seguida, selecione **OK**. 

7. Repita estes passos para **AzureRM.Profile** e **AzureRM.Resources**.

    ![Carregar ficheiros][functions6]

1. Depois de terminar, cada pasta deve ter ficheiros de módulo do PowerShell Olá do seu computador local.

    ![Ficheiros de PowerShell][functions7]

### <a name="authentication"></a>Autenticação

os cmdlets do PowerShell do toouse Olá, tem de autenticar. Configurar a autenticação na aplicação de função Olá. autenticação tooconfigure, tem de configurar as variáveis de ambiente e carregar uma aplicação de função de toohello do ficheiro de chave encriptada.

> [!NOTE]
> Este cenário fornece um exemplo de como autenticação de tooimplement com as funções do Azure. Existem outra formas toodo isto.

#### <a name="encrypted-credentials"></a>Credenciais encriptado

Olá seguinte script do PowerShell cria um ficheiro de chave denominado **PassEncryptKey.key**. Também fornece uma versão encriptada da palavra-passe de Olá fornecido. Esta palavra-passe é Olá mesma palavra-passe que está definido para a aplicação do Azure Active Directory Olá que é utilizada para autenticação.

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

No Editor de serviço de aplicações da aplicação de função Olá Olá, crie uma pasta denominada **chaves** em **AlertPacketCapturePowerShell**. Em seguida, carregue Olá **PassEncryptKey.key** ficheiros que criou no exemplo de PowerShell Olá anterior.

![Chave de funções][functions8]

### <a name="retrieve-values-for-environment-variables"></a>Obter os valores de variáveis de ambiente

requisito final Olá é tooset segurança Olá as variáveis de ambiente são valores de Olá tooaccess necessário para autenticação. Olá lista seguinte mostra as variáveis de ambiente de Olá que são criadas:

* AzureClientID

* AzureTenant

* AzureCredPassword


#### <a name="azureclientid"></a>AzureClientID

ID de cliente Olá é Olá ID da aplicação de uma aplicação no Azure Active Directory.

1. Se ainda não tiver uma aplicação toouse, execute uma aplicação Olá toocreate de exemplo a seguir.

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > palavra-passe de Olá que utilizar para criar aplicação Olá deve ser Olá mesma palavra-passe que criou anteriormente ao guardar o ficheiro de chave Olá.

1. No portal do Azure Olá, selecione **subscrições**. Selecione Olá toouse de subscrição e, em seguida, selecione **(IAM) do controlo de acesso**.

    ![Funções IAM][functions9]

1. Escolha Olá toouse de conta e, em seguida, selecione **propriedades**. Copiar Olá ID da aplicação.

    ![ID da aplicação de funções][functions10]

#### <a name="azuretenant"></a>AzureTenant

Obter ID do inquilino Olá executando Olá PowerShell de exemplo a seguir:

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a>AzureCredPassword

Olá o valor da variável de ambiente de AzureCredPassword Olá é valor Olá que obtém a execução Olá PowerShell de exemplo a seguir. Neste exemplo é Olá, mesmo que é apresentado na Olá anterior **encriptação das credenciais** secção. Olá valor que precisa é a saída de Olá da Olá `$Encryptedpassword` variável.  Este é Olá serviço principal palavra-passe que encriptada utilizando o script do PowerShell Olá.

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-hello-environment-variables"></a>Variáveis de ambiente de Olá de arquivo

1. Aceda a aplicação de função toohello. Em seguida, selecione **as definições de aplicação de função** > **configurar definições da aplicação**.

    ![Configurar as definições da aplicação][functions11]

1. Adicionar variáveis de ambiente de Olá e respetivas definições de aplicação de toohello valores e, em seguida, selecione **guardar**.

    ![Definições de aplicação][functions12]

### <a name="add-powershell-toohello-function"></a>Adicionar a função de toohello do PowerShell

Está agora a tempo toomake chama para o observador de rede a partir de dentro Olá função do Azure. Dependendo dos requisitos de Olá, implementação de Olá desta função pode variar. No entanto, o fluxo geral de Olá de código Olá é o seguinte:

1. Parâmetros de entrada do processo.
2. Pacote existente da consulta captura tooverify limites e resolva conflitos de nomes.
3. Crie uma captura de pacotes com os parâmetros adequados.
4. Captura de pacotes de consulta periodicamente até que esteja concluída.
5. Notificar o utilizador Olá que a sessão de captura de pacotes de Olá está concluída.

Olá seguinte exemplo é o código do PowerShell que pode ser utilizado na função de Olá. Existem valores que necessitam de toobe substituído para **subscriptionId**, **resourceGroupName**, e **storageAccountName**.

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a>Obter o URL de função Olá 
1. Depois de criar a função, configure o seu URL de Olá toocall alerta associado à função de Olá. tooget este valor, o URL da função Olá cópia da sua aplicação de função.

    ![Localizar o URL da função Olá][functions13]

2. Copie o URL de função de Olá para a sua aplicação de função.

    ![Copiar o URL da função Olá][2]

Se necessitar de propriedades personalizadas no payload Olá de pedido POST de webhook Olá, consulte demasiado[configurar um webhook num alerta métrico Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

## <a name="configure-an-alert-on-a-vm"></a>Configurar um alerta numa VM

Os alertas podem ser configuradas toonotify indivíduos quando uma métrica específica atravesse um limiar que é atribuído tooit. Neste exemplo, alerta Olá é no Olá segmentos TCP que são enviados, mas pode ser acionada alerta Olá para muitas outras métricas. Neste exemplo, um alerta é configurado toocall uma função do webhook toocall Olá.

### <a name="create-hello-alert-rule"></a>Criar regra de alerta de Olá

Aceda a máquina virtual existente e tooan e, em seguida, adicione uma regra de alerta. Documentação mais detalhada sobre como configurar alertas pode ser encontrada em [criar alertas no Monitor do Azure para serviços do Azure - portal do Azure](../monitoring-and-diagnostics/insights-alerts-portal.md). Introduza Olá os seguintes valores no Olá **regra de alerta** painel e, em seguida, selecione **OK**.

  |**Definição** | **Valor** | **Detalhes** |
  |---|---|---|
  |**Nome**|TCP_Segments_Sent_Exceeded|Nome da regra de alerta de Olá.|
  |**Descrição**|Segmentos TCP enviados limiar excedida|Descrição de Olá de regra de alerta de Olá.||
  |**Métricas**|Segmentos TCP enviados| alerta do Olá toouse métrica tootrigger Olá. |
  |**Condição**|Mais do que| Olá condição toouse ao avaliar a métrica de Olá.|
  |**Limiar**|100| valor de Olá da métrica de Olá que aciona alerta Olá. Este valor deve ser definido tooa um valor válido para o seu ambiente.|
  |**Período**|Ao longo de Olá últimos cinco minutos| Determina o período de Olá no qual toolook para o limiar de Olá de métrica de Olá.|
  |**Webhook**|[webhook o URL da aplicação de função]| URL do webhook Olá da aplicação de função Olá que foi criada nos passos anteriores Olá.|

> [!NOTE]
> métrica de segmentos Olá TCP não está ativada por predefinição. Saiba mais sobre como tooenable métricas adicionais, visitando [ativar a monitorização e diagnóstico](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).

## <a name="review-hello-results"></a>Reveja os resultados de Olá

Depois de critérios de Olá para acionadores alerta Olá, é criada uma captura de pacotes. Aceda tooNetwork observador e, em seguida, selecione **captura de pacotes**. Nesta página, pode selecionar Olá pacote captura ficheiro ligação toodownload Olá captura de pacotes.

![Captura de pacotes de vista][functions14]

Se o ficheiro de captura Olá estiver armazenado localmente, pode obtê-lo pelo início de sessão na máquina virtual de toohello.

Para obter instruções sobre a transferência de ficheiros das contas do storage do Azure, consulte [introdução ao Blob storage do Azure através do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Outra ferramenta, pode utilizar é [Explorador de armazenamento](http://storageexplorer.com/).

Após a captura tenha sido transferida, pode vê-la utilizando qualquer ferramenta que pode ler um **.cap** ficheiro. Seguem-se ligações tootwo destas ferramentas:

- [Analisador de mensagens da Microsoft](https://technet.microsoft.com/library/jj649776.aspx)
- [WireShark](https://www.wireshark.org/)

## <a name="next-steps"></a>Passos seguintes

Saiba como tooview as capturas de pacotes, visitando [análise de captura do pacote com o Wireshark](network-watcher-deep-packet-inspection.md).


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
