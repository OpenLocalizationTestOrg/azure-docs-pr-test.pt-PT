---
title: aaaConnect Windows computadores tooAzure Log Analytics | Microsoft Docs
description: "Este artigo mostra computadores com Windows hello passos tooconnect Olá no seu toohello de infraestrutura no local serviço análise de registos ao utilizar uma versão personalizada da Olá Microsoft Monitoring Agent (MMA)."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a>Ligar o serviço de análise de registos do Windows computadores toohello no Azure

Este artigo mostra Olá passos tooconnect computadores com Windows no seu áreas de trabalho de tooOMS de infraestrutura no local utilizando uma versão personalizada da Olá Microsoft Monitoring Agent (MMA). Tem de tooinstall e ligar agentes para todos os computadores de Olá que pretende que tooonboard serem no serviço de análise de registos do toosend dados toohello e tooview e act nesses dados. Cada agente pode reportar toomultiple áreas de trabalho.

Pode instalar agentes utilizando a configuração, a linha de comandos, ou com pretendido Estado Configuration (DSC) na automatização do Azure.  

>[!NOTE]
Para máquinas virtuais em execução no Azure, pode simplificar a instalação utilizando Olá [extensão da máquina virtual](log-analytics-azure-vm-extension.md).

Em computadores com a conectividade à Internet, o agente de Olá utiliza Olá ligação toohello Internet toosend dados tooOMS. Para computadores que não têm acesso à Internet, pode utilizar um proxy ou Olá [OMS Gateway](log-analytics-oms-gateway.md).

Ligar o seu tooOMS de computadores do Windows é simples utilizar três passos simples:

1. Transferir o ficheiro de configuração do agente de Olá a partir do portal do OMS Olá
2. Instalar o agente de Olá utilizando o método de Olá que escolher
3. Configure o agente de Olá ou adicione áreas de trabalho adicionais, se necessário

Olá seguinte diagrama mostra Olá relação entre os computadores com o Windows e o OMS depois de ter instalado e configurado os agentes.

![OMS-direta-agente-diagrama](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

Se as políticas de segurança de TI não permitir que os computadores no seu toohello tooconnect de rede à Internet, pode configurar o seu toohello de tooconnect computadores OMS Gateway. Para obter mais informações e passos sobre como tooconfigure sua toocommunicate servidores através do serviço OMS toohello um Gateway do OMS, consulte o artigo [ligar tooOMS de computadores utilizando Olá OMS Gateway](log-analytics-oms-gateway.md).

## <a name="system-requirements-and-required-configuration"></a>Requisitos de sistema e a configuração necessária
Antes de instalar ou implementar agentes, reveja Olá tooensure detalhes que cumpre os requisitos de Olá a seguir.

- Só pode instalar Olá OMS MMA em computadores com o Windows Server 2008 SP 1 ou posterior ou Windows 7 SP1 ou posterior.
- Necessita de uma subscrição do Azure.  Para obter mais informações, consulte [introdução à análise de registos](log-analytics-get-started.md).
- Cada computador com o Windows tem de ser capaz de tooconnect toohello Internet através de HTTPS ou toohello OMS Gateway. Esta ligação pode ser direta, através de um proxy ou através de Olá OMS Gateway.
- Pode instalar Olá OMS MMA em computadores autónomos, servidores e máquinas virtuais. Se pretender tooconnect tooOMS de máquinas de virtuais alojado no Azure, veja [tooLog de máquinas virtuais do Azure ligar análise](log-analytics-azure-vm-extension.md).
- agente de Olá tem toouse a porta TCP 443 para vários recursos.

### <a name="network"></a>Rede

Para Windows agentes tooconnect tooand registar com o serviço OMS Olá, têm de ter acesso toonetwork recursos, incluindo URLs de domínio e de números de porta de Olá.

- Para servidores proxy, tem de tooensure Olá recursos estão configurados nas definições do agente de servidor de proxy adequado.
- Para firewalls que restringem o acesso toohello Internet, ou os engenheiros de rede necessário tooconfigure tooOMS de acesso de toopermit sua firewall. Não é necessária nenhuma ação nas definições do agente.

Olá, a tabela seguinte mostra os recursos necessários para a comunicação.

>[!NOTE]
>Alguns dos Olá os seguintes recursos mencionar das informações operacionais, que era um nome anterior para análise de registos.

| Recursos do Agente | Portas | Inspeção de HTTPS direto |
|---|---|---|
| *.ods.opinsights.azure.com | 443 | Sim |
| *.oms.opinsights.azure.com | 443 | Sim |
| *.blob.core.windows.net | 443 | Sim |
| *.azure-automation.net | 443 | Sim |



## <a name="download-hello-agent-setup-file-from-oms"></a>Transferir o ficheiro de configuração do agente de Olá do OMS
1. No portal do OMS Olá, no Olá **descrição geral** página, clique em Olá **definições** mosaico.  Clique em Olá **origens ligadas** separador na parte superior do Olá.  
    ![Separador de origens ligada](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)
2. Clique em **servidores Windows** e, em seguida, clique em **transferir o agente do Windows** tooyour aplicável computador processador tipo toodownload Olá ficheiro da configuração.
3. No Olá à direita dos **ID da área de trabalho**, clique Olá ícone de cópia e colagem Olá ID no bloco de notas.
4. No Olá à direita dos **chave primária**, clique Olá ícone de cópia e colagem chave Olá no bloco de notas.     

## <a name="install-hello-agent-using-setup"></a>Instalar o agente de Olá utilizando o programa de configuração
1. Execute o agente de Olá de tooinstall de configuração num computador que pretende que o toomanage.
2. Na página de boas-vindas Olá, clique em **seguinte**.
3. Na página de termos de licenciamento de Olá, leia Olá de licenciamento e, em seguida, clique em **concordo**.
4. Na página de pasta de destino Olá, altere ou mantenha a pasta de instalação predefinida de Olá e, em seguida, clique em **seguinte**.
5. Na página de opções de configuração do agente de Olá, pode escolher tooconnect Olá agente tooAzure análise de registos (OMS), Operations Manager, ou pode deixar as escolhas de Olá em branco se pretende que o agente de Olá tooconfigure mais tarde. Clique em **Seguinte**.   
    - Se tiver escolhido tooconnect tooAzure análise de registos (OMS), cole Olá **ID da área de trabalho** e **chave da área de trabalho (chave primária)** copiado no bloco de notas no procedimento anterior Olá e, em seguida, clique em  **Seguinte**.  
        ![Cole o ID da área de trabalho e a chave primária](./media/log-analytics-windows-agents/connect-workspace.png)
    - Se tiver escolhido tooconnect tooOperations Manager, escreva Olá **Management Group Name**, **servidor de gestão** nome, e **porta do servidor de gestão**e, em seguida, clique em **Seguinte**. Na página de conta de ação do agente de Olá, escolha a conta do sistema Local Olá ou uma conta de domínio local e, em seguida, clique em **seguinte**.  
        ![configuração do grupo de gestão](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![conta de ação do agente](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)

6. Na página de tooInstall pronto Olá, reveja as suas opções e, em seguida, clique em **instalar**.
7. No Olá concluir com êxito a configuração da página, clique em **concluir**.
8. Quando terminar, Olá **Microsoft Monitoring Agent** aparece no **painel de controlo**. Pode rever a configuração não existe e certifique-se de que o agente Olá tooOperational ligado Insights (OMS). Quando Olá tooOMS ligados, o agente apresenta uma mensagem a indicar: **Olá Microsoft Monitoring Agent foi ligado com êxito o serviço do Microsoft Operations Management Suite toohello.**

## <a name="configure-proxy-settings"></a>Configurar definições de proxy

Pode utilizar Olá seguir o procedimento tooconfigure as definições de proxy Olá Microsoft Monitoring Agent utilizando o painel de controlo. É necessário toouse este procedimento para cada servidor. Se tiver vários servidores que precisa de tooconfigure, poderá considerar mais fácil toouse tooautomate um script este processo. Se Sim, consulte o procedimento seguinte Olá [tooconfigure as definições de proxy para o Microsoft Monitoring Agent utilizando um script de Olá](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a>definições de proxy tooconfigure Olá Microsoft Monitoring Agent utilizando o painel de controlo
1. Abra o **Painel de Controlo**.
2. Abra o **Agente de Monitorização da Microsoft**.
3. Clique em Olá **as definições de Proxy** separador.  
    ![separador de definições de proxy](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)
4. Selecione **utilizar um servidor proxy** e escreva o URL de Olá e número de porta, se um exemplo de toohello necessários, semelhante mostrado. Se o servidor proxy requer autenticação, escreva Olá nome de utilizador e palavra-passe tooaccess Olá servidor proxy.


### <a name="verify-agent-connectivity-toooms"></a>Certifique-se tooOMS de conectividade de agente

Pode facilmente verificar se os agentes estão a comunicar com o OMS Olá seguir o procedimento a utilizar:

1.  No computador de Olá com o agente do Windows hello, abra o painel de controlo.
2.  Abra o Microsoft Monitoring Agent.
3.  Clique Olá separador de análise de registos do Azure (OMS).
4.  Na coluna de estado de Olá, deverá ver que o agente Olá ligado com êxito toohello o serviço do Operations Management Suite.

![agente ligado](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a>definições de proxy tooconfigure Olá Microsoft Monitoring Agent utilizando um script
Copie Olá seguinte exemplo, atualizá-lo com o ambiente de tooyour específicos de informação, guarde-o com uma extensão de nome de ficheiro PS1 e, em seguida, execute o script de Olá em cada computador que estabelece diretamente ligação de serviço do toohello OMS.

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a>Instalar o agente de Olá utilizando a linha de comandos Olá
- Modificar e, em seguida, utilize Olá seguinte agente Olá tooinstall de exemplo utilizando Olá linha de comandos. exemplo de Olá executa uma instalação totalmente automática.

    >[!NOTE]
    Se quiser tooupgrade um agente, terá de toouse Olá Log Analytics API de scripting. Consulte Olá seguinte secção tooupgrade um agente.

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

agente de Olá utiliza IExpress como respetivo Self-extractor utilizando Olá `/c` comando. Pode ver os parâmetros da linha de comandos do Olá em [comutadores da linha de comandos para IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) e, em seguida, atualização Olá exemplo toosuit às suas necessidades.

|Opções de MMA específico                   |Notas         |
|---------------------------------------|--------------|
|ADD_OPINSIGHTS_WORKSPACE               | 1 = área de trabalho do configurar Olá agente tooreport tooa                |
|OPINSIGHTS_WORKSPACE_ID                | Id da área de trabalho (guid) para Olá tooadd de área de trabalho                    |
|OPINSIGHTS_WORKSPACE_KEY               | Autenticar tooinitially utilizada chave de área de trabalho com área de trabalho Olá |
|OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE  | Especifique o ambiente de nuvem olá onde está localizada a área de trabalho Olá <br> 0 = em nuvem comerciais do azure (predefinição) <br> 1 = azure Government |
|OPINSIGHTS_PROXY_URL               | URI para Olá proxy toouse |
|OPINSIGHTS_PROXY_USERNAME               | Nome de utilizador tooaccess um proxy autenticado |
|OPINSIGHTS_PROXY_PASSWORD               | Palavra-passe tooaccess um proxy autenticado |

>[!NOTE]
limite de comprimento de linha de comandos atingir de Olá do tooavoid de IExpress, instale o agente de Olá com nenhuma área de trabalho configurada e, em seguida, utilizar uma configuração de tooset de script para a área de trabalho de Olá.

>[!NOTE]
Se obtiver um `Command line option syntax error.` quando utilizar Olá `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parâmetro, pode utilizar Olá solução os seguintes:
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a>Adicionar uma área de trabalho através de um script
Adicione uma área de trabalho utilizando a API de scripting de agente do Olá análise de registos com o seguinte exemplo de Olá:

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

tooadd uma área de trabalho do Azure para US Government, Olá utilizar script de exemplo a seguir:
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
Se tiver utilizado a linha de comandos Olá ou script anteriormente tooinstall ou configurar o agente de Olá, `EnableAzureOperationalInsights` foi substituído por `AddCloudWorkspace`.

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a>Instalar o agente de Olá utilizando DSC na automatização do Azure

Pode utilizar Olá seguinte script exemplo tooinstall Olá agente utilizando DSC na automatização do Azure. exemplo de Olá instala Olá agente de 64 bits, identificado por Olá `URI` valor. Também pode utilizar a versão de 32 bits Olá, substituindo o valor do URI Olá. Olá URIs para ambas as versões são:

- O agente de 64 bits do Windows - https://go.microsoft.com/fwlink/?LinkId=828603
- O agente de 32 bits do Windows - https://go.microsoft.com/fwlink/?LinkId=828604


>[!NOTE]
Este procedimento e o script de exemplo não irá atualizar um agente existente.

1. Importar Olá xPSDesiredStateConfiguration módulo DSC de [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) na automatização do Azure.  
2.  Criar recursos de variável de automatização do Azure para *OPSINSIGHTS_WS_ID* e *OPSINSIGHTS_WS_KEY*. Definir *OPSINSIGHTS_WS_ID* tooyour ID da área de trabalho de análise de registos do OMS e defina *OPSINSIGHTS_WS_KEY* toohello chave primária da sua área de trabalho.
3.  Utilizar Olá script a seguir e guarde-o como MMAgent.ps1
4.  Modificar e, em seguida, utilize Olá seguinte agente Olá tooinstall de exemplo utilizando DSC na automatização do Azure. Importe MMAgent.ps1 para automatização do Azure utilizando a interface de automatização do Azure Olá ou o cmdlet.
5.  Atribua uma configuração de toohello de nó. Em 15 minutos, o nó de Olá verifica a respetiva configuração e Olá MMA é feito o Push de nó toohello.

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-hello-latest-productid-value"></a>Obter o valor de ProductId Olá mais recente

Olá `ProductId value` Olá MMAgent.ps1 script é a versão do agente tooeach exclusivo. Quando uma versão atualizada de cada agente for publicada, alterações Olá ProductId valor. Por isso, quando Olá ProductId for alterada no futuro Olá, pode encontrar a versão do agente Olá através de um script simple. Depois de ter Olá mais recente versão do agente instalado no servidor de teste, pode utilizar Olá seguinte script tooget Olá instalado ProductId valor. Utilizar o valor de ProductId mais recente Olá, pode atualizar o valor Olá Olá MMAgent.ps1 script.

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a>Configure manualmente um agente ou adicione áreas de trabalho adicionais
Se instalou agentes, mas não foi possível configurá-las ou se quiser áreas de trabalho do Olá agente tooreport toomultiple, pode utilizar Olá seguir informações tooenable um agente ou reconfigurá-lo. Depois de configurar o agente de Olá, vai registar com o serviço de agente Olá e irá obter as informações de configuração necessário e pacotes de gestão que contêm informações de soluções.

1. Depois de instalar o Microsoft Monitoring Agent de Olá, abra **painel de controlo**.
2. Abra **Microsoft Monitoring Agent** e, em seguida, clique em Olá **análise de registos do Azure (OMS)** separador.   
3. Clique em **adicionar** tooopen Olá **adicionar uma área de trabalho de análise do registo** caixa.
4. Olá colar **ID da área de trabalho** e **chave da área de trabalho (chave primária)** copiado no bloco de notas num procedimento anterior para a área de trabalho de Olá que pretende tooadd e, em seguida, clique em **OK**.  
    ![configurar as informações operacionais](./media/log-analytics-windows-agents/add-workspace.png)

Depois dos dados são recolhidos a partir de computadores monitorizados por agente Olá, número de Olá dos computadores monitorizados pelo OMS irão aparecer no portal do OMS Olá no Olá **origens ligadas** separador **definições** como  **Servidores ligados**.


## <a name="toodisable-an-agent"></a>toodisable um agente
1. Depois de instalar o agente de Olá, abra **painel de controlo**.
2. Abra o Microsoft Monitoring Agent e, em seguida, clique em Olá **análise de registos do Azure (OMS)** separador.
3. Selecione uma área de trabalho e, em seguida, clique em **remover**. Repita este passo para todas as outras áreas de trabalho.


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a>Opcionalmente, configure o grupo de gestão do agentes tooreport tooan do Operations Manager

Se utilizar o Operations Manager na sua infraestrutura de TI, também pode utilizar o agente MMA Olá como um agente do Operations Manager.

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a>grupo de gestão ao Operations Manager do tooan de tooreport tooconfigure MMA agentes
1.  Olá onde está instalado o agente de Olá, abra no computador **painel de controlo**.  
2.  Abra **Microsoft Monitoring Agent** e, em seguida, clique em Olá **do Operations Manager** separador.  
    ![Separador do Microsoft Monitoring Agent do Operations Manager](./media/log-analytics-windows-agents/om-mg01.png)
3.  Se os servidores do Operations Manager tem integração com o Active Directory, clique em **atualizar automaticamente atribuições de grupo de gestão do AD DS**.
4.  Clique em **adicionar** tooopen Olá **adicionar um grupo de gestão** caixa de diálogo.  
    ![O Microsoft Monitoring Agent adicionar um grupo de gestão](./media/log-analytics-windows-agents/oms-mma-om02.png)
5.  No **nome do grupo de gestão** caixa, o nome do tipo Olá do seu grupo de gestão.
6.  No Olá **servidor de gestão principal** caixa, nome de computador do tipo Olá Olá principal do servidor de gestão.
7.  No Olá **porta do servidor de gestão** caixa, número de porta TCP de Olá de tipo.
8.  Em **conta de ação do agente**, escolha a conta do sistema Local Olá ou uma conta de domínio local.
9.  Clique em **OK** tooclose Olá **adicionar um grupo de gestão** caixa de diálogo e, em seguida, clique em **OK** tooclose Olá **propriedades de agente de monitorização da Microsoft**caixa de diálogo.


## <a name="next-steps"></a>Passos seguintes

- [Adicionar soluções de análise de registos de Olá soluções galeria](log-analytics-add-solutions.md) tooadd funcionalidade e a recolha de dados.
