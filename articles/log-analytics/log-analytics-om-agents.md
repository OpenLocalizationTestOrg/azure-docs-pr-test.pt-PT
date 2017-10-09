---
title: aaaConnect do Operations Manager tooLog Analytics | Microsoft Docs
description: "toomaintain expandido do seu investimento existente no System Center Operations Manager e utilizar capacidades de análise de registos, pode integrar o Operations Manager com a sua área de trabalho do OMS."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 245ef71e-15a2-4be8-81a1-60101ee2f6e6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: magoedte
ms.openlocfilehash: b2841c7aa209fec7357dc4c8b1ff4325fdaa37ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-operations-manager-toolog-analytics"></a>Ligar o Operations Manager tooLog análise
toomaintain expandido do seu investimento existente no System Center Operations Manager e utilizar capacidades de análise de registos, pode integrar o Operations Manager com a sua área de trabalho do OMS.  Isto permite-lhe tirar partido das oportunidades de Olá do OMS ao continuar toouse do Operations Manager para:

* Continuar a monitorizar o estado de funcionamento de Olá dos seus serviços de TI com o Operations Manager
* Manter a integração com as suas soluções ITSM suportar gestão de incidente e problema
* Gerir o ciclo de vida de Olá dos agentes implementados tooon local e nuvem pública IaaS as máquinas virtuais que monitorizar com o Operations Manager

Integração com o System Center Operations Manager adiciona a estratégia de operações de serviço do valor tooyour através da utilização de alta velocidade Olá e a eficiência do OMS no recolher, armazenar e analisar dados do Operations Manager.  Correlacione de ajuda do OMS e de trabalho para identificar falhas Olá dos problemas e analisar recurrences para suportar o processo de gestão de problema existente.   Olá flexibilidade Olá pesquisa motor tooexamine desempenho, eventos e alerta de dados, com dashboards avançados e relatórios capacidades tooexpose demonstra a estes dados de formas significativos, força Olá OMS proporciona na complimenting do Operations Manager.

Olá agentes a enviar relatórios grupo de gestão do Operations Manager toohello recolhe dados dos seus servidores com base nas origens de dados de análise de registos de Olá e soluções que tiver ativado na sua subscrição do OMS.  Consoante a solução de Olá que tiver ativado, dados a partir destas soluções são que um enviada diretamente a partir de um servidor de gestão do Operations Manager toohello OMS serviço web, ou devido a Olá volume dos dados recolhidos no sistema Olá de gerido por agente, são enviados diretamente serviço web do Olá agente tooOMS. servidor de gestão de Olá reencaminha os dados OMS Olá diretamente toohello OMS web service; nunca é escrito na base de dados de toohello, OperationsManager ou OperationsManagerDW.  Quando um servidor de gestão perde a conectividade com o serviço web do Olá OMS,-Olá guarda dados em cache localmente até que a comunicação é restabelecida com o OMS.  Se o servidor de gestão de Olá estiver offline devido a manutenção de tooplanned ou falha não planeada, o outro servidor de gestão no grupo de gestão de Olá retoma conectividade com o OMS.  

Olá diagrama seguinte ilustra ligação Olá entre servidores de gestão de Olá e os agentes num grupo de gestão do System Center Operations Manager e o OMS, incluindo direção Olá e portas.   

![OMS-operations-manager-integração-diagrama](./media/log-analytics-om-agents/oms-operations-manager-connection.png)

Se as políticas de segurança de TI não permitir que os computadores no seu toohello tooconnect de rede à Internet, servidores de gestão podem ser configurado tooconnect toohello OMS Gateway tooreceive as informações de configuração e enviar os dados recolhidos consoante na solução de Olá ter ativada.  Para obter mais informações e passos sobre como tooconfigure toocommunicate de grupo de gestão do Operations Manager através do serviço OMS toohello um Gateway do OMS, consulte o artigo [ligar tooOMS de computadores utilizando Olá OMS Gateway](log-analytics-oms-gateway.md).  

## <a name="system-requirements"></a>Requisitos de sistema
Antes de começar, reveja Olá seguir tooverify detalhes cumpre os pré-requisitos.

* OMS só suporta o Operations Manager 2016, UR6 do Operations Manager 2012 SP1 e posterior e UR2 do Operations Manager 2012 R2 e superior.  Foi adicionado suporte de proxy ao Operations Manager 2012 SP1 UR7 e ao Operations Manager 2012 R2 UR3.
* Todos os agentes do Operations Manager têm de cumprir os requisitos de suporte mínimo. Certifique-se de que os agentes estão em atualização mínima Olá, caso contrário, o tráfego de agente do Windows poderão falhar e muitos erros podem preencher o registo de eventos do Operations Manager Olá.
* Uma subscrição do OMS.  Para obter mais informações, consulte [introdução à análise de registos](log-analytics-get-started.md).

### <a name="network"></a>Rede
informações de Olá abaixo lista Olá proxy e de firewall informações de configuração necessárias para o agente do Operations Manager Olá, servidores de gestão e toocommunicate de consola de operações com o OMS.  Tráfego de cada componente é de saída do seu serviço do rede toohello OMS.     

|Recurso | Número de porta| Ignorar a inspeção de HTTP|  
|---------|------|-----------------------|  
|**Agente**|||  
|\*.ods.opinsights.azure.com| 443 |Sim|  
|\*.oms.opinsights.azure.com| 443|Sim|  
|\*.blob.core.windows.net| 443|Sim|  
|\*.azure-automation.net| 443|Sim|  
|**Servidor de gestão**|||  
|\*.service.opinsights.azure.com| 443||  
|\*.blob.core.windows.net| 443| Sim|  
|\*.ods.opinsights.azure.com| 443| Sim|  
|*.azure-automation.net | 443| Sim|  
|**TooOMS de consola do Operations Manager**|||  
|service.systemcenteradvisor.com| 443||  
|\*.service.opinsights.azure.com| 443||  
|\*.live.com| 80 e 443||  
|\*.microsoft.com| 80 e 443||  
|\*.microsoftonline.com| 80 e 443||  
|\*.mms.microsoft.com| 80 e 443||  
|login.windows.net| 80 e 443||  


## <a name="connecting-operations-manager-toooms"></a>A ligação do Operations Manager tooOMS
Efetue Olá seguinte série de passos tooconfigure sua tooone do tooconnect de grupo Gestão do Operations Manager do seu áreas de trabalho do OMS.

1. Na consola do Operations Manager Olá, selecione Olá **administração** área de trabalho.
2. Expanda o nó de Operations Management Suite Olá e clique em **ligação**.
3. Clique em Olá **registar tooOperations Management Suite** ligação.
4. No Olá **Assistente de integração do Operations Management Suite: autenticação** página, introduza o endereço de correio eletrónico Olá ou número de telefone e palavra-passe da conta de administrador de Olá que está associada a sua subscrição do OMS e, em  **Inicie sessão no**.
5. Depois que serem autenticadas com êxito, no Olá **Assistente de integração do Operations Management Suite: selecionar área de trabalho** página, é-lhe pedido que tooselect sua área de trabalho do OMS.  Se tiver mais de uma área de trabalho, selecione Olá área de trabalho que pretende tooregister com o grupo de gestão do Operations Manager Olá de Olá na lista pendente e, em seguida, clique em **seguinte**.
   
   > [!NOTE]
   > O Operations Manager só suporta uma área de trabalho do OMS cada vez. ligação de Olá e computadores de Olá que foram registados tooOMS com área de trabalho anterior Olá são removidos do OMS.
   > 
   > 
6. No Olá **Assistente de integração do Operations Management Suite: resumo** página, confirme as suas definições e se estiverem corretas, clique em **criar**.
7. No Olá **Assistente de integração do Operations Management Suite: concluir** página, clique em **fechar**.

### <a name="add-agent-managed-computers"></a>Adicionar computadores geridos por agente
Após configurar a integração com a sua área de trabalho do OMS, isto só estabelece uma ligação com o OMS, sem os dados são recolhidos de agentes Olá tooyour grupo de gestão de relatórios. Tal não acontecer até depois de configurar os computadores geridos por agente específicos recolhe dados para análise de registos. Pode selecionar objetos de computador Olá individualmente ou pode selecionar um grupo que contenha objetos de computador do Windows. Não é possível selecionar um grupo que contenha as instâncias de outra classe, tais como discos lógicos ou bases de dados SQL.

1. Consola do Operations Manager Olá aberta e selecione Olá **administração** área de trabalho.
2. Expanda o nó de Operations Management Suite Olá e clique em **ligação**.
3. Clique em Olá **adicionar um computador/grupo** ligação em Olá ações cabeçalho no lado direito Olá do painel de Olá.
4. No Olá **computador pesquisa** caixa de diálogo, pode procurar computadores ou grupos monitorizados pelo Operations Manager. Selecione tooOMS tooonboard de computadores ou grupos, clique em **adicionar**e, em seguida, clique em **OK**.

Pode ver os computadores e grupos configurados toocollect dados a partir do nó de computadores geridos por Olá em Operations Management Suite no Olá **administração** Olá da consola de operações da área de trabalho.  Aqui, pode adicionar ou remover computadores e grupos conforme necessário.

### <a name="configure-oms-proxy-settings-in-hello-operations-console"></a>Configurar definições de proxy do OMS na consola de operações de Olá
Efetue Olá os passos seguintes se for um servidor proxy interno entre o grupo de gestão de Olá e o serviço web do OMS.  Estas definições são geridas centralmente do grupo de gestão de Olá e sistemas distribuídos tooagent geridos que estão incluídos nos dados de toocollect Olá âmbito para OMS.  Este é vantajoso para quando determinadas soluções ignorar dados de servidor e envio de gestão de Olá diretamente tooOMS serviço web.

1. Consola do Operations Manager Olá aberta e selecione Olá **administração** área de trabalho.
2. Expanda o Operations Management Suite e, em seguida, clique em **ligações**.
3. Na vista de ligação do OMS Olá, clique em **configurar o servidor de Proxy**.
4. No **assistente Operations Management Suite: servidor Proxy** página, selecione **utilizar um hello do proxy servidor tooaccess Operations Management Suite**, e, em seguida, escreva o URL de Olá com o número da porta Olá, por exemplo, http:// corpproxy:80 e, em seguida, clique em **concluir**.

Se o servidor proxy requer autenticação, execute os passos seguintes Olá tooconfigure credenciais e definições que necessitam de toopropagate toomanaged computadores que comunica tooOMS Olá grupo de gestão.

1. Consola do Operations Manager Olá aberta e selecione Olá **administração** área de trabalho.
2. Em **Configuração RunAs**, selecione **Perfis**.
3. Abra Olá **System Center Advisor executar como Proxy de perfil** perfil.
4. No Olá como assistente do perfil Run, clique em Adicionar toouse uma conta Run As. Pode criar um [conta Run As](https://technet.microsoft.com/library/hh321655.aspx) ou utilizar uma conta existente. Esta conta necessita de toohave toopass de permissões suficientes através do servidor de proxy de Olá.
5. tooset Olá toomanage de conta, escolha **uma classe selecionada, grupo ou objeto**, clique em **selecionar...** e, em seguida, clique em **grupo...** Olá tooopen **grupo pesquisa** caixa.
6. Procure e, em seguida, selecione **grupo do servidor de monitorização do Microsoft System Center Advisor**.  Clique em **OK** depois de selecionar Olá do Olá grupo tooclose **grupo pesquisa** caixa.
7. Clique em **OK** tooclose Olá **adicionar uma conta Run As** caixa.
8. Clique em **guardar** toocomplete Olá assistente e guarde as alterações.

Depois de ligação de Olá é criada e configurar os agentes irão recolher e comunicar dados tooOMS, hello seguinte configuração é aplicada no grupo de gestão de Olá, não necessariamente por ordem:

* Conta Run As de Olá **Microsoft.SystemCenter.Advisor.RunAsAccount.Certificate** é criado.  Está associada ao perfil Run As de Olá **Microsoft System Center Advisor executar como perfil Blob** e está direcionado para duas classes - **servidor recolha** e **grupo de gestão do Operations Manager** .
* São criados dois conectores.  Olá pela primeira vez com o nome **Microsoft.SystemCenter.Advisor.DataConnector** e é automaticamente configurado com uma subscrição que reencaminha todos os alertas gerados a partir de instâncias de todas as classes no tooOMS de grupo de gestão de Olá registo Análise. conector do segundo Olá **Advisor Connector**, que é responsável por comunicar com o serviço web do OMS e partilha de dados.
* Os agentes e grupos que selecionou toocollect dados no grupo de gestão de Olá é adicionada toohello **grupo do servidor de monitorização do Microsoft System Center Advisor**.

## <a name="management-pack-updates"></a>Atualizações de pacotes de gestão
Depois de concluir a configuração, o grupo de gestão do Operations Manager Olá estabelece uma ligação com Olá serviço OMS.  servidor de gestão de Olá sincroniza com o serviço web de Olá e receber informações de configuração atualizada no formulário de Olá dos pacotes de gestão para soluções de Olá tiver ativado, que se integram com o Operations Manager.   O Operations Manager verifica a existência de atualizações destes pacotes de gestão e automaticamente transferir e importa-las quando estiverem disponíveis.  Existem duas regras em particular controlar qual este comportamento:

* **Microsoft.SystemCenter.Advisor.MPUpdate** -Olá base OMS os pacotes de gestão de atualizações. Por predefinição, é executada a cada 12 horas.
* **Microsoft.SystemCenter.Advisor.Core.GetIntelligencePacksRule** -atualizações de pacotes de gestão de solução ativados na sua área de trabalho. Por predefinição, é executada a cada cinco (5) minutos.

Pode substituir estas duas regras tooeither impedir a transferência automática, desativando-los ou modificar a frequência de Olá para frequência hello servidor de gestão sincroniza com o OMS toodetermine se um novo pacote de gestão está disponível e deve ser transferido.  Siga os passos de Olá [como tooOverride uma regra ou Monitor](https://technet.microsoft.com/library/hh212869.aspx) toomodify Olá **frequência** parâmetro com um valor no segundos toochange Olá agenda de sincronização ou modificar Olá **ativado**  regras de Olá toodisable de parâmetro.  Olá de destino substitui tooall objetos da classe do grupo de gestão do Operations Manager.

Se quiser toocontinue seguindo o processo de controlo de alterações existente para controlar as versões do pacote de gestão no grupo de gestão de produção, pode desativar regras Olá e ativá-los durante a horas específicas quando as atualizações são permitidas. Se tiver um desenvolvimento ou grupo de gestão de pergunta e resposta no seu ambiente e tem toohello conectividade à Internet, pode configurar esse grupo de gestão com um toosupport de área de trabalho do OMS neste cenário.  Isto permite-lhe tooreview e avaliar as versões de iterativo Olá Olá OMS de pacotes de gestão antes de libertá-los para o grupo de gestão de produção.

## <a name="switch-an-operations-manager-group-tooa-new-oms-workspace"></a>Mudar um tooa de grupo do Operations Manager nova área de trabalho do OMS
1. Inicie sessão na subscrição do OMS tooyour e criar uma área de trabalho [Microsoft Operations Management Suite](http://oms.microsoft.com/).
2. Consola do Operations Manager Olá abrir com uma conta que seja membro da função de administradores do Operations Manager Olá e selecione Olá **administração** área de trabalho.
3. Expanda o Operations Management Suite e selecione **ligações**.
4. Selecione Olá **reconfigure operação Management Suite** ligação no lado Olá do meio do painel de Olá.
5. Siga Olá **Assistente de integração do Operations Management Suite** e introduza Olá e-mail endereço ou número de telefone e a palavra-passe da conta de administrador de Olá que está associada a sua nova área de trabalho do OMS.
   
   > [!NOTE]
   > Olá **Assistente de integração do Operations Management Suite: selecionar área de trabalho** página apresenta Olá área de trabalho existente que está a ser utilizado.
   > 
   > 

## <a name="validate-operations-manager-integration-with-oms"></a>Validar a integração do Operations Manager com o OMS
Existem algumas formas diferentes pode verificar que o tooOperations OMS Manager integração for concluída com êxito.

### <a name="tooconfirm-integration-from-hello-oms-portal"></a>integração de tooconfirm do portal do OMS Olá
1. No portal do OMS Olá, clique em Olá **definições** mosaico
2. Selecione **ligado origens**.
3. Na tabela de Olá em Olá secção do System Center Operations Manager, deverá ver o nome de Olá Olá do grupo de gestão listado com o número de Olá de agentes e o estado quando os dados foram recebidos pela última vez.
   
   ![definições de OMS-connectedsources](./media/log-analytics-om-agents/oms-settings-connectedsources.png)
4. Olá nota **ID da área de trabalho** valor em Olá à esquerda do lado da página de definições de Olá.  Validá-lo contra o grupo de gestão do Operations Manager, abaixo.  

### <a name="tooconfirm-integration-from-hello-operations-console"></a>integração de tooconfirm Olá na consola de operações
1. Consola do Operations Manager Olá aberta e selecione Olá **administração** área de trabalho.
2. Selecione **pacotes de gestão** e no Olá **procure:** tipo caixa de texto **Advisor** ou **Intelligence**.
3. Dependendo das soluções de Olá que tiver ativado, pode ver um pacote de gestão correspondentes, listado nos resultados de pesquisa de Olá.  Por exemplo, se tiver ativado o Olá solução de gestão de alertas, o pacote de gestão de Olá gestão alertas do Microsoft System Center Advisor está na lista de Olá.
4. De Olá **monitorização** ver, navegue até toohello **operações de gestão Suite\Health estado** vista.  Selecione um servidor de gestão em Olá **estado do servidor de gestão** painel e em Olá **vista detalhada** painel confirmar o valor de Olá para a propriedade **URI do serviço de autenticação** corresponde ao ID da área de trabalho OMS Olá.
   
   ![OMS-opsmgr-mg-authsvcuri-Property-MS](./media/log-analytics-om-agents/oms-opsmgr-mg-authsvcuri-property-ms.png)

## <a name="remove-integration-with-oms"></a>Remova a integração com o OMS
Quando já não necessitar de integração entre o grupo de gestão do Operations Manager e a área de trabalho do OMS, existem vários passos necessários tooproperly remover Olá ligação e a configuração no grupo de gestão de Olá. Olá procedimento tem a atualizar a sua área de trabalho do OMS, eliminando referência Olá do seu grupo de gestão, elimine Olá OMS conectores e, em seguida, elimine os pacotes de gestão que suportam OMS.   

Pacotes de gestão para soluções de Olá tiver ativado, que se integram com o Operations Manager e Olá pacotes necessários toosupport integração de gestão Olá serviço OMS não é possível eliminar facilmente Olá do grupo de gestão.  Isto acontece porque alguns dos pacotes de gestão do OMS Olá terem dependências de outros pacotes de gestão relacionados.  pacotes de gestão de toodelete tendo uma dependência de outros pacotes de gestão, transferir o script de Olá [remover um pacote de gestão com dependências](https://gallery.technet.microsoft.com/scriptcenter/Script-to-remove-a-84f6873e) do Centro de scripts do TechNet.  

1. Abra Olá Shell de comandos do Operations Manager com uma conta que seja um membro da função de administradores do Operations Manager Olá.
   
    > [!WARNING]
    > Certifique-se de que não tem quaisquer pacotes de gestão personalizados com o word Olá Advisor ou IntelligencePack no nome de Olá antes de continuar, caso contrário, os seguintes passos de Olá eliminá-los a Olá do grupo de gestão.
    > 

2. A partir de Olá shell de comandos, escreva`Get-SCOMManagementPack -name "*Advisor*" | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
3. Tipo de próximo`Get-SCOMManagementPack -name “*IntelligencePack*” | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
4. pacotes de quaisquer pacotes de gestão restantes que tenham uma dependência nos outro gestão do System Center Advisor tooremove, utilize o script de Olá *RecursiveRemove.ps1* transferiu a partir do Olá Centro de scripts do TechNet anteriormente.  
 
    > [!NOTE]
    > Não elimine pacotes de gestão do Microsoft System Center Advisor ou o Microsoft System Center Advisor interno Olá.  
    >  

5. Abra a consola de operações do Operations Manager Olá com uma conta que seja um membro da função de administradores do Operations Manager Olá.
6. Em **administração**, selecione Olá **pacotes de gestão** nós e no Olá **procure:** caixa, escreva **Advisor** e certifique-se Olá Estes pacotes de gestão ainda são importados no seu grupo de gestão:
   
   * Microsoft System Center Advisor
   * Microsoft System Center Advisor interno
7. No portal do OMS Olá, clique em Olá **definições** mosaico.
8. Selecione **ligado origens**.
9. Na tabela de Olá em Olá secção do System Center Operations Manager, deverá ver o nome de Olá Olá do grupo de gestão que pretende tooremove da área de trabalho Olá.  Na coluna de Olá **últimos dados**, clique em **remover**.  
   
    > [!NOTE]
    > Olá **remover** ligação não estarão disponível até depois de 14 dias se não existir nenhuma atividade detetada Olá ligados do grupo de gestão.  
    > 

10. Será apresentada uma janela de pedir-lhe tooconfirm que pretende que o tooproceed com a remoção de Olá.  Clique em **Sim** tooproceed. 

toodelete Olá dois conectores - Microsoft.SystemCenter.Advisor.DataConnector e Advisor Connector, guarde o script do PowerShell Olá abaixo tooyour computador e executar utilizando Olá exemplos a seguir:

```
    .\OM2012_DeleteConnector.ps1 “Advisor Connector” <ManagementServerName>
    .\OM2012_DeleteConnectors.ps1 “Microsoft.SytemCenter.Advisor.DataConnector” <ManagementServerName>
```

> [!NOTE]
> computador Olá que tem de executar este script de, se não for um servidor de gestão, deve ter a shell de comandos do Operations Manager Olá instalado, dependendo da versão de Olá do seu grupo de gestão.
> 
> 

```
    `param(
    [String] $connectorName,
    [String] $msName="localhost"
    )
    $mg = new-object Microsoft.EnterpriseManagement.ManagementGroup $msName
    $admin = $mg.GetConnectorFrameworkAdministration()
    ##########################################################################################
    # Configures a connector with hello specified name.
    ##########################################################################################
    function New-Connector([String] $name)
    {
         $connectorForTest = $null;
         foreach($connector in $admin.GetMonitoringConnectors())
    {
    if($connectorName.Name -eq ${name})
    {
         $connectorForTest = Get-SCOMConnector -id $connector.id
    }
    }
    if ($connectorForTest -eq $null)
    {
         $testConnector = New-Object Microsoft.EnterpriseManagement.ConnectorFramework.ConnectorInfo
         $testConnector.Name = $name
         $testConnector.Description = "${name} Description"
         $testConnector.DiscoveryDataIsManaged = $false
         $connectorForTest = $admin.Setup($testConnector)
         $connectorForTest.Initialize();
    }
    return $connectorForTest
    }
    ##########################################################################################
    # Removes a connector with hello specified name.
    ##########################################################################################
    function Remove-Connector([String] $name)
    {
        $testConnector = $null
        foreach($connector in $admin.GetMonitoringConnectors())
       {
        if($connector.Name -eq ${name})
       {
         $testConnector = Get-SCOMConnector -id $connector.id
       }
      }
     if ($testConnector -ne $null)
     {
        if($testConnector.Initialized)
     {
     foreach($alert in $testConnector.GetMonitoringAlerts())
     {
       $alert.ConnectorId = $null;
       $alert.Update("Delete Connector");
     }
     $testConnector.Uninitialize()
     }
     $connectorIdForTest = $admin.Cleanup($testConnector)
     }
    }
    ##########################################################################################
    # Delete a connector's Subscription
    ##########################################################################################
    function Delete-Subscription([String] $name)
    {
      foreach($testconnector in $admin.GetMonitoringConnectors())
      {
      if($testconnector.Name -eq $name)
      {
        $connector = Get-SCOMConnector -id $testconnector.id
      }
    }
    $subs = $admin.GetConnectorSubscriptions()
    foreach($sub in $subs)
    {
      if($sub.MonitoringConnectorId -eq $connector.id)
      {
        $admin.DeleteConnectorSubscription($admin.GetConnectorSubscription($sub.Id))
      }
     }
    }
    #New-Connector $connectorName
    write-host "Delete-Subscription"
    Delete-Subscription $connectorName
    write-host "Remove-Connector"
    Remove-Connector $connectorName
```

Olá futura se planeia restabelecer a ligação sua gestão grupo tooan OMS área de trabalho, terá de importar toore Olá `Microsoft.SystemCenter.Advisor.Resources.\<Language>\.mpb` ficheiro de pacote de gestão do update rollup mais recente de Olá aplicadas tooyour grupo de gestão.  Pode encontrar este ficheiro no Olá `%ProgramFiles%\Microsoft System Center 2012` ou Olá `System Center 2012 R2\Operations Manager\Server\Management Packs for Update Rollups` pasta.

## <a name="next-steps"></a>Passos seguintes
funcionalidade de tooadd e recolha de dados, consulte [soluções de análise de registos de adicionar de Olá soluções galeria](log-analytics-add-solutions.md).


