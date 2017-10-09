---
title: "aaaTroubleshooting problemas comuns da automatização do Azure | Microsoft Docs"
description: "Este artigo fornece informações toohelp resolver problemas e corrija erros comuns de automatização do Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
tags: top-support-issue
keywords: "Erro de automatização, resolução de problemas, problema"
ms.assetid: 5f3cfe61-70b0-4e9c-b892-d02daaeee07d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: sngun; v-reagie
ms.openlocfilehash: eb7d1cc5726f2b7a86c860e8f0c8340fa4221b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-common-issues-in-azure-automation"></a>Resolução de problemas comuns na automatização do Azure 
Este artigo fornece ajuda de resolução de problemas de erros comuns que pode ocorrer na automatização do Azure e sugere possíveis soluções tooresolve-los.

## <a name="authentication-errors-when-working-with-azure-automation-runbooks"></a>Erros de autenticação quando trabalhar com runbooks de automatização do Azure
### <a name="scenario-sign-in-tooazure-account-failed"></a>Cenário: Falha da conta de início de sessão tooAzure
**Erro:** recebe o erro de Olá "Unknown_user_type: utilizador tipo desconhecido" quando trabalhar com os cmdlets Add-AzureAccount ou Login-AzureRmAccount de Olá.

**Motivo erro Olá:** este erro ocorre se o nome de recurso de credencial de Olá não é válido ou se hello nome de utilizador e palavra-passe que utilizou o recurso de credencial de automatização toosetup Olá não são válidos.

**Sugestões de resolução de problemas:** na ordem toodetermine Novidades errado, demorar Olá os seguintes passos:  

1. Certifique-se de que não tem quaisquer carateres especiais, incluindo Olá  **@**  caráter no Olá automatização recurso nome da credencial que está a utilizar tooconnect tooAzure.  
2. Certifique-se de que pode utilizar Olá nome de utilizador e palavra-passe que são armazenadas na credencial de automatização do Azure Olá no seu editor local do ISE do PowerShell. Pode fazê-lo executando Olá os seguintes cmdlets no Olá ISE do PowerShell:  

        $Cred = Get-Credential  
        #Using Azure Service Management   
        Add-AzureAccount –Credential $Cred  
        #Using Azure Resource Manager  
        Login-AzureRmAccount –Credential $Cred
3. Se a autenticação falhar localmente, isto significa que ainda não configurou as credenciais do Azure Active Directory corretamente. Consulte demasiado[autenticar tooAzure utilizando o Azure Active Directory](https://azure.microsoft.com/blog/azure-automation-authenticating-to-azure-using-azure-active-directory/) as conta do Active Directory do Azure tooget de post do blogue Olá corretamente configurado.  

### <a name="scenario-unable-toofind-hello-azure-subscription"></a>Cenário: Olá toofind não é possível subscrição do Azure
**Erro:** recebe o erro de Olá "Olá subscrição com o nome ``<subscription name>`` não é possível encontrar" ao trabalhar com Olá Select-AzureSubscription ou Select-AzureRmSubscription cmdlets.

**Motivo erro Olá:** este erro ocorre se o nome da subscrição Olá não é válido ou se o utilizador do Azure Active Directory de Olá que está a tentar detalhes da subscrição tooget Olá não está configurado como um administrador de subscrição de Olá.

**Sugestões de resolução de problemas:** ordem toodetermine se corretamente ter autenticado tooAzure e ter acesso toohello subscrição que está a tentar tooselect, tomar Olá os seguintes passos:  

1. Certifique-se de que executa Olá **Add-AzureAccount** antes de executar Olá **Select-AzureSubscription** cmdlet.  
2. Se continuar a ver esta mensagem de erro, modificar o seu código adicionando Olá **Get-AzureSubscription** cmdlet seguir Olá **Add-AzureAccount** cmdlet e, em seguida, executar código Olá.  Agora, verifique se o resultado Olá Get-AzureSubscription contém os detalhes da sua subscrição.  

   * Se não vir quaisquer detalhes da subscrição na saída de Olá, isto significa que subscrição Olá não está inicializada.  
   * Se vir detalhes da subscrição Olá na saída de Olá, confirme que está a utilizar ID ou nome de subscrição correta Olá com Olá **Select-AzureSubscription** cmdlet.   

### <a name="scenario-authentication-tooazure-failed-because-multi-factor-authentication-is-enabled"></a>Cenário: Autenticação tooAzure falhou porque a autenticação multifator é ativada
**Erro:** recebe o erro de Olá "Add-AzureAccount: AADSTS50079: inscrição de autenticação forte (prova cópia de segurança) é necessária" durante a autenticação tooAzure com o nome de utilizador do Azure e a palavra-passe.

**Motivo erro Olá:** se tiver a autenticação multifator na sua conta do Azure, não é possível utilizar um tooAzure de tooauthenticate de utilizador do Azure Active Directory.  Em vez disso, terá de toouse um certificado ou um tooAzure principal tooauthenticate de serviço.

**Sugestões de resolução de problemas:** toouse um certificado com Olá cmdlets de gestão de serviço do Azure, consulte demasiado[criação e adição de um certificado toomanage Azure serviços.](http://blogs.technet.com/b/orchestrator/archive/2014/04/11/managing-azure-services-with-the-microsoft-azure-automation-preview-service.aspx) toouse um principal de serviço com os cmdlets do Azure Resource Manager, consulte demasiado[criar serviço principal através do portal do Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md) e [autenticar um principal de serviço com o Azure Resource Manager.](../azure-resource-manager/resource-group-authenticate-service-principal.md)

## <a name="common-errors-when-working-with-runbooks"></a>Erros comuns ao trabalhar com runbooks
### <a name="scenario-hello-runbook-job-start-was-attempted-three-times-but-it-failed-toostart-each-time"></a>Cenário: início de tarefa de runbook Olá foi tentado três vezes, mas não conseguiu toostart sempre
**Erro:** runbook falha com o erro de Olá "" tarefa Olá foi tentou três vezes mas não foi possível."

**Motivo erro Olá:** este erro pode ser causado por Olá seguintes motivos:  

1. Limite de memória.  Podemos ter documentados limites na quantidade de memória alocada tooa Sandbox [limites de serviço de automatização](../azure-subscription-service-limits.md#automation-limits) para uma tarefa o poderá falhar se estiver a utilizar mais de 400 MB de memória. 

2. Módulo incompatível.  Isto pode ocorrer se as dependências de módulo não estão corretas e se não forem, o runbook, normalmente, irá devolver um "comando não foi encontrado" ou "Não é possível vincular o parâmetro" mensagem. 

**Sugestões de resolução de problemas:** qualquer uma das seguintes soluções de Olá irá corrigir o problema de Olá:  

* Métodos sugeridos toowork dentro do limite de memória de Olá estão carga de trabalho do toosplit Olá entre vários runbooks, não processar como a quantidade de dados na memória, não toowrite desnecessários saída a partir dos seus runbooks ou considere quantos pontos de verificação escrever para o PowerShell runbooks do fluxo de trabalho.  

* Terá de tooupdate os módulos do Azure, seguindo os passos de Olá [como tooupdate módulos do Azure PowerShell na automatização do Azure](automation-update-azure-modules.md).  


### <a name="scenario-runbook-fails-because-of-deserialized-object"></a>Cenário: O Runbook falhar devido ao objeto de serialização anulado
**Erro:** runbook falha com o erro de Olá "não é possível vincular o parâmetro ``<ParameterName>``. Não é possível converter Olá ``<ParameterType>`` valor do tipo Deserialized ``<ParameterType>`` tootype ``<ParameterType>``".

**Motivo erro Olá:** se o runbook for um fluxo de trabalho do PowerShell, armazena objetos complexos num formato de serialização anulado na ordem toopersist o estado de runbook se o fluxo de trabalho Olá é suspenso.  

**Sugestões de resolução de problemas:**  
Qualquer uma das Olá seguintes três soluções irá corrigir este problema:

1. Se estiver a encaminhando os objetos complexos de um cmdlet tooanother, molde estes cmdlets num InlineScript.  
2. Passe nome Olá ou valor que precisa de objeto complexo de Olá em vez de transmitir o objeto Olá de todo.  
3. Utilize um runbook do PowerShell em vez de um runbook de fluxo de trabalho do PowerShell.  

### <a name="scenario-runbook-job-failed-because-hello-allocated-quota-exceeded"></a>Cenário: A tarefa de Runbook falhou porque Olá atribuído a quota foi excedida
**Erro:** a tarefa de runbook falha com o erro de Olá "Olá quota Olá mensal total tarefa tempo de execução foi atingido para esta subscrição".

**Motivo erro Olá:** este erro ocorre quando hello execução da tarefa excede a quota de livre 500 minuto Olá para a sua conta. Esta quota aplica-se tooall tipos de tarefas de execução da tarefa como uma tarefa de teste, inicie uma tarefa a partir do portal de Olá, executar uma tarefa utilizando webhooks e agendar uma tarefa tooexecute utilizando qualquer um dos Olá portal do Azure ou no seu centro de dados. toolearn mais informações sobre preços para automatização, consulte [automatização preços](https://azure.microsoft.com/pricing/details/automation/).

**Sugestões de resolução de problemas:** se quiser toouse mais do que 500 minutos de processamento por mês, terá de toochange a sua subscrição do toohello o escalão básico Olá escalão gratuito. Pode atualizar o escalão básico toohello por Olá efetuando os seguintes passos:  

1. Inicie sessão no tooyour a subscrição do Azure  
2. Selecione a conta de automatização de Olá que desejar tooupgrade  
3. Clique em **definições** > **utilização e escalão de preço** > **escalão de preço**  
4. No Olá **escolher o escalão de preço** painel, selecione **básico**    

### <a name="scenario-cmdlet-not-recognized-when-executing-a-runbook"></a>Cenário: Cmdlet não reconhecido ao executar um runbook
**Erro:** falha a tarefa de runbook com o erro de Olá "``<cmdlet name>``: termo Olá ``<cmdlet name>`` não é reconhecida como Olá nome de um cmdlet, a função, o ficheiro de script ou programa operável."

**Motivo erro Olá:** este erro é causado quando o motor de PowerShell Olá não é possível encontrar o cmdlet Olá estiver a utilizar no runbook.  Isto pode dever-se ao facto do módulo Olá contendo Olá cmdlet está em falta da conta de Olá, existe um conflito de nomes com um nome de runbook, ou também existe Olá cmdlet no módulo de outro e automatização não é possível resolver o nome de Olá.

**Sugestões de resolução de problemas:** qualquer uma das seguintes soluções de Olá irá corrigir o problema de Olá:  

* Verifique o nome do cmdlet Olá ter introduzido corretamente.  
* Certifique-se Olá cmdlet existe na sua conta de automatização e de que existem não está em conflito. tooverify se Olá cmdlet estiver presente, abra um runbook no modo de edição e procure Olá cmdlet que pretende toofind na biblioteca de Olá ou executa **Get-Command ``<CommandName>``** .  Depois de validar este cmdlet Olá conta toohello disponíveis, e que não existem nenhum nome entra em conflito com outros cmdlets ou runbooks, adicioná-lo toohello tela e certifique-se de que está a utilizar um parâmetro válido definido no runbook.  
* Se tiver um conflito de nomes e Olá cmdlet está disponível em dois módulos diferentes, pode resolver isto utilizando Olá nome completamente qualificado para Olá cmdlet. Por exemplo, pode utilizar **ModuleName\CmdletName**.  
* Se se encontram em execução Olá runbook no local num grupo de trabalho híbrida, em seguida, certifique-se de que Olá cmdlet do módulo é instalado na máquina de Olá que aloja a função de trabalho híbrida Olá.

### <a name="scenario-a-long-running-runbook-consistently-fails-with-hello-exception-hello-job-cannot-continue-running-because-it-was-repeatedly-evicted-from-hello-same-checkpoint"></a>Cenário: Um runbook de execução longa consistentemente falha com a exceção de Olá: "tarefa Olá não é possível continuar a ser executada porque este foi expulso repetidamente de Olá mesmo ponto de verificação".
**Motivo erro Olá:** isto é comportamento de design devido toohello "Fração justa" monitorização de processos dentro da automatização do Azure, que suspenda automaticamente um runbook se a ser executada superior a 3 horas. No entanto, Olá a mensagem de erro devolvida não fornece "que seguinte" opções. Um runbook pode ser suspensa para uma série de razões. Suspende a acontecer principalmente devida tooerrors. Por exemplo, uma exceção não identificada no runbook, uma falha de rede ou uma falha no Olá executar Olá runbook do Runbook Worker, serão todos causar Olá runbook toobe suspenso e iniciar a partir do último ponto de verificação quando retomado.

**Sugestões de resolução de problemas:** Olá documentados solução tooavoid este problema é toouse pontos de verificação num fluxo de trabalho.  toolearn mais Consulte demasiado[Learning fluxos de trabalho do PowerShell](automation-powershell-workflow.md#checkpoints).  Pode encontrar uma explicação mais detalhada de "Quota justa" e o ponto de verificação neste artigo do blogue [utilizando pontos de verificação em Runbooks](https://azure.microsoft.com/en-us/blog/azure-automation-reliable-fault-tolerant-runbook-execution-using-checkpoints/).

## <a name="common-errors-when-importing-modules"></a>Erros comuns ao importar os módulos
### <a name="scenario-module-fails-tooimport-or-cmdlets-cant-be-executed-after-importing"></a>Cenário: Falha do módulo tooimport ou não é possível executar cmdlets depois de importar
**Erro:** um módulo falha tooimport ou importa com êxito, mas não os cmdlets são extraídos.

**Motivo erro Olá:** algumas comuns entre as razões que um módulo pode não importar com êxito tooAzure automatização são:  

* estrutura de Olá não corresponde à estrutura de Olá que a automatização necessita toobe no.  
* módulo Olá está dependente de outro módulo que não foi implementado tooyour conta de automatização.  
* módulo Olá faltam as respetivas dependências na pasta Olá.  
* Olá **New-AzureRmAutomationModule** cmdlet está a ser módulo Olá de tooupload utilizado e não ter fornecidos o caminho de armazenamento total Olá ou não foram carregados módulo Olá utilizando um URL acessível publicamente.  

**Sugestões de resolução de problemas:**  
Qualquer uma das seguintes soluções de Olá irá corrigir o problema de Olá:  

* Certifique-se de que módulo Olá segue Olá seguinte formato:  
  ModuleName.Zip  **->**  ModuleName ou um número de versão  **->**  (ModuleName.psm1, ModuleName.psd1)
* Abrir o ficheiro. psd1 Olá e se o módulo Olá tem quaisquer dependências.  Se existir, carregue toohello estes módulos conta de automatização.  
* Certifique-se de que estão presentes na pasta do módulo Olá qualquer .dlls referenciado.  

## <a name="common-errors-when-working-with-desired-state-configuration-dsc"></a>Erros comuns ao trabalhar com configuração de estado pretendido (DSC)
### <a name="scenario-node-is-in-failed-status-with-a-not-found-error"></a>Cenário: Nó está num Estado de falha com um erro "Não encontrada"
**Erro:** o nó de Olá tem um relatório com **falha** estado e de que contém o erro de Olá "Olá tentativa tooget Olá ação do servidor https://``<url>``//accounts/``<account-id>``/Nodes(AgentId=``<agent-id>``) / GetDscAction falhou porque uma configuração válida ``<guid>`` não é possível localizar. "

**Motivo erro Olá:** este erro ocorre normalmente quando hello nó está atribuído o nome da configuração tooa (por exemplo, ABC) em vez de um nome de configuração do nó (por exemplo, ABC. Servidor Web).  

**Sugestões de resolução de problemas:**  

* Certifique-se de que está a atribuir nó Olá com "nome do nó de configuração" e não Olá "nome de configuração".  
* Pode atribuir um nó de tooa de configuração de nó com o Azure portal ou com um cmdlet do PowerShell.

  * Na ordem tooassign um nó de tooa de configuração de nó através do portal do Azure, abra Olá **nós de DSC** painel, em seguida, selecione um nó e clique em **atribuir a configuração do nó** botão.  
  * Na ordem tooassign um nó de tooa de configuração de nó utilizando o cmdlet do PowerShell, utilize **conjunto AzureRmAutomationDscNode** cmdlet

### <a name="scenario--no-node-configurations-mof-files-were-produced-when-a-configuration-is-compiled"></a>Cenário: Não existem configurações de nó (ficheiros MOF) foram produzidas quando uma configuração é compilada
**Erro:** suspende a tarefa de compilação de DSC com o erro de Olá: "compilação foi concluída com êxito, mas não .mofs de configuração de nó foram geradas".

**Motivo erro Olá:** quando Olá expressão seguir Olá **nó** palavra-chave na configuração de Olá DSC avalia demasiado$ nulo e não configurações de nó serão produzidas.    

**Sugestões de resolução de problemas:**  
Qualquer uma das seguintes soluções de Olá irá corrigir o problema de Olá:  

* Certifique-se de que toohello seguinte da expressão de Olá **nó** palavra-chave na definição de configuração de Olá não está a avaliar demasiado nulo$.  
* Se está a transmitir ConfigurationData ao compilar a configuração de Olá, certifique-se de que está a transmitir valores de esperados Olá requer que a configuração Olá do [ConfigurationData](automation-dsc-compile.md#configurationdata).

### <a name="scenario--hello-dsc-node-report-becomes-stuck-in-progress-state"></a>Cenário: Olá relatório de nó DSC fica bloqueada no seu estado "em curso"
**Erro:** DSC agente produz "Não existe uma instância encontrada com fornecida valores de propriedade."

**Motivo erro Olá:** atualizou a sua versão do WMF e ter danificado WMI.  

**Sugestões de resolução de problemas:** Siga instruções Olá Olá [DSC problemas e limitações conhecidos](https://msdn.microsoft.com/powershell/wmf/5.0/limitation_dsc) problema de Olá toofix.

### <a name="scenario--unable-toouse-a-credential-in-a-dsc-configuration"></a>Cenário: Não é possível toouse uma credencial numa configuração de DSC
**Erro:** foi suspenso a tarefa de compilação de DSC com o erro de Olá: "erro System.InvalidOperationException propriedade credencial do tipo de processamento ``<some resource name>``: conversão e armazenar uma palavra-passe encriptada como texto simples só é permitida se PSDscAllowPlainTextPassword está definido tootrue".

**Motivo erro Olá:** utilizou uma credencial numa configuração mas não fornecer adequada **ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue para cada nó configuração.  

**Sugestões de resolução de problemas:**  

* Certifique-se toopass no Olá adequada **ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue para cada configuração de nó mencionada na configuração de Olá. Para obter mais informações, consulte demasiado[ativos no Automation DSC do Azure](automation-dsc-compile.md#assets).

## <a name="next-steps"></a>Passos seguintes
Se seguiu Olá acima de passos de resolução de problemas e não é possível encontrar a resposta de Olá, pode rever as opções de suporte adicionais Olá abaixo.

* Obter a ajuda de especialistas do Azure. Submeter o seu problema toohello [fóruns do MSDN Azure ou Stack Overflow.](https://azure.microsoft.com/support/forums/).
* Ficheiro de um incidente de suporte do Azure. Aceda toohello [site Azure suporta](https://azure.microsoft.com/support/options/) e clique em **obter suporte** em **técnica e faturação suporte**.
* Publique um pedido de Script no [Centro de scripts](https://azure.microsoft.com/documentation/scripts/) se estiver à procura de uma solução de runbook da automatização do Azure ou um módulo de integração.
* Publique comentários ou pedidos funcionalidades para a automatização do Azure no [voz do utilizador](https://feedback.azure.com/forums/34192--general-feedback).
