---
title: "implementação de aaaAutomating de uma VM nos Amazon Web Services | Microsoft Docs"
description: "Este artigo demonstra como toouse criação de tooautomate de automatização do Azure de uma VM de serviço do Amazon Web"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 1d85c01a-d795-4523-8194-84fc15b53838
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/14/2017
ms.author: tiandert; bwren
ms.openlocfilehash: dd1f3af47d8700ced85a3ee5a406dde1c1311990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---provision-an-aws-virtual-machine"></a>Cenário de automatização do Azure - aprovisionar uma máquina virtual do AWS
Neste artigo, vamos demonstrar como pode tirar partido da automatização do Azure tooprovision uma máquina virtual na sua subscrição do Amazon Web Service (AWS) e dê essa VM um nome específico – que AWS refere-se tooas "marcação" Olá VM.

## <a name="prerequisites"></a>Pré-requisitos
Para efeitos de Olá deste artigo, terá de toohave uma conta de automatização do Azure e uma subscrição do AWS. Para mais informações sobre como configurar uma conta de automatização do Azure e configurá-lo com as suas credenciais de subscrição do AWS, reveja [configurar a autenticação com os Amazon Web Services](automation-configure-aws-account.md).  Esta conta deve ser criada ou atualizada com as suas credenciais de subscrição do AWS antes de continuar, como podemos fará referência nesta conta no passos Olá abaixo.

## <a name="deploy-amazon-web-services-powershell-module"></a>Implementar o módulo PowerShell do Amazon Web Services
A nossa VM aprovisionamento runbook irá tirar partido da toodo de módulo do PowerShell do AWS Olá respetivo trabalho. Efetue Olá os seguintes passos tooadd Olá módulo tooyour conta de automatização que esteja configurada com as suas credenciais de subscrição do AWS.  

1. Abra o browser e navegue toohello [galeria do PowerShell](http://www.powershellgallery.com/packages/AWSPowerShell/) e clique em Olá **botão de automatização de tooAzure implementar**.<br><br> ![Importação do módulo do AWS PS](./media/automation-scenario-aws-deployment/powershell-gallery-download-awsmodule.png)
2. É direcionado toohello página de início de sessão do Azure e depois de a autenticação, será encaminhado toohello Portal do Azure e apresentadas com Olá seguir painel.<br><br> ![Painel do módulo de importação](./media/automation-scenario-aws-deployment/deploy-aws-powershell-module-parameters.png)
3. Selecione Olá grupo de recursos de Olá **grupo de recursos** pendente lista e no painel de parâmetros de Olá, forneça Olá seguintes informações:
   
   * De Olá **novo ou a conta de automatização existente (cadeia)** selecione na lista pendente **existentes**.  
   * No Olá **nome da conta de automatização (cadeia)** caixa, escreva nome exato Olá de Olá conta de automatização que inclui as credenciais de Olá para a sua subscrição do AWS.  Por exemplo, se tiver criado uma conta dedicada com o nome **AWSAutomation**, em seguida, o que é a escrever na caixa de Olá.
   * Selecione Olá região adequada de Olá **localização da conta de automatização** na lista pendente.
4. Quando tiver terminado de informações de Olá necessário entrar, clique em **criar**.
   
   > [!NOTE]
   > Ao importar um módulo do PowerShell na automatização do Azure, este é também extrair Olá cmdlets e estas atividades não serão apresentado até que o módulo Olá completamente terminou de importar e extrair Olá cmdlets. Este processo pode demorar alguns minutos.  
   > <br>
   > 
   > 
5. No Portal do Azure Olá, abra a sua conta de automatização referenciada no passo 3.
6. Clique em Olá **ativos** mosaico e no Olá **ativos** painel, selecione de Olá **módulos** mosaico.
7. No Olá **módulos** painel verá Olá **AWSPowerShell** módulo na lista de Olá.

## <a name="create-aws-deploy-vm-runbook"></a>Criar AWS implementar runbook VM
Uma vez Olá que módulo do PowerShell AWS tiver sido implementado, pode agora criamos uma tooautomate runbook aprovisionar uma máquina virtual no AWS através de um script do PowerShell. passos de Olá abaixo demonstrar como tooleverage nativo script do PowerShell na automatização do Azure.  

> [!NOTE]
> Para mais opções e informações sobre este script, visite Olá [galeria do PowerShell](https://www.powershellgallery.com/packages/New-AwsVM/DisplayScript).
> 

1. Transferir o script do PowerShell Olá New-AwsVM Olá galeria do PowerShell ao abrir uma sessão do PowerShell e escrever Olá seguinte:<br>
   ```
   Save-Script -Name New-AwsVM -Path <path>
   ```
   <br>
2. Na Olá Portal do Azure, abra a sua conta de automatização e clique em Olá **Runbooks** mosaico.  
3. De Olá **Runbooks** painel, selecione **adicionar um runbook**.
4. No Olá **adicionar um runbook** painel, selecione **criação rápida** (criar um runbook novo).
5. No Olá **Runbook** painel de propriedades, escreva um nome na caixa de nome de Olá para o runbook e Olá **tipo de Runbook** selecione na lista pendente **PowerShell**e, em seguida, clique em  **Criar**.<br><br> ![Painel do módulo de importação](./media/automation-scenario-aws-deployment/runbook-quickcreate-properties.png)
6. Quando é apresentado o painel de editar Runbook do PowerShell de Olá, copie e cole o script do PowerShell Olá runbook Olá criação tela.<br><br> ![Script do PowerShell do Runbook](./media/automation-scenario-aws-deployment/runbook-powershell-script.png)<br>
   
    > [!NOTE]
    > Tenha em atenção o seguinte de Olá ao trabalhar com o exemplo de Olá script do PowerShell:
    > 
    > * runbook Olá contém um número de valores de parâmetro predefinidos. Volte a avaliar todos os valores predefinidos e atualizar sempre que necessário.
    > * Se tiver armazenado as suas credenciais do AWS como um recurso de credencial denominado de forma diferente que **AWScred**, precisa de script de Olá tooupdate numa linha 57 toomatch em conformidade.  
    > * Ao trabalhar com Olá comandos da CLI do AWS no PowerShell, especialmente com este runbook de exemplo, tem de especificar região do Olá AWS. Caso contrário, os cmdlets de Olá irá falhar.  Tópico AWS vista [especificar região do AWS](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-installing-specifying-region.html) no Olá ferramentas AWS para documentos do PowerShell para obter mais detalhes.  
    >

7. tooretrieve uma lista de nomes de imagem da sua subscrição do AWS, inicie o ISE do PowerShell e importar Olá AWS módulo do PowerShell.  Autenticar face AWS, substituindo **Get-AutomationPSCredential** no seu ambiente de ISE com **AWScred = Get-Credential**.  Isto irá solicitar-lhe as suas credenciais e pode fornecer o **ID da chave de acesso** para Olá nome de utilizador e **chave de acesso secreta** palavra-passe de Olá.  Veja o exemplo de Olá abaixo:  

        #Sample tooget hello AWS VM available images
        #Please provide hello path where you have downloaded hello AWS PowerShell module
        Import-Module AWSPowerShell
        $AwsRegion = "us-west-2"
        $AwsCred = Get-Credential
        $AwsAccessKeyId = $AwsCred.UserName
        $AwsSecretKey = $AwsCred.GetNetworkCredential().Password
   
        # Set up hello environment tooaccess AWS
        Set-AwsCredentials -AccessKey $AwsAccessKeyId -SecretKey $AwsSecretKey -StoreAs AWSProfile
        Set-DefaultAWSRegion -Region $AwsRegion
   
        Get-EC2ImageByName -ProfileName AWSProfile

    Olá seguinte resultado é devolvido:<br><br>
   ![Obter imagens AWS](./media/automation-scenario-aws-deployment/powershell-ise-output.png)<br>  
8. Copiar e colar Olá um dos nomes de imagens Olá uma variável de automatização como referenciadas no runbook Olá como **$InstanceType**. Uma vez que, neste exemplo, estamos a utilizar Olá AWS livre camadas subscrição, iremos utilizar **t2.micro** para o nosso exemplo de runbook.  
9. Guardar runbook Olá, em seguida, clique em **publicar** toopublish Olá runbook e, em seguida, **Sim** quando lhe for pedido.

### <a name="testing-hello-aws-vm-runbook"></a>Olá AWS VM runbook de teste
Antes de teste Olá runbook vamos prosseguir, precisamos tooverify algumas coisas. Especificamente:  

* Um recurso de autenticação relativamente aos AWS foi criado chamado **AWScred** ou script Olá foi nome de Olá tooreference atualizado do recurso de credencial.    
* módulo do PowerShell de AWS Olá foi importado na automatização do Azure  
* Foi criado um novo runbook e os valores de parâmetros foram verificados e atualizados sempre que necessário  
* **Criar registos verbosos** e, opcionalmente, **criar registos de progressos** na definição de runbook Olá **registo e rastreio** tiver sido definido demasiado**no**.<br><br> ![Registo do Runbook e o rastreio](./media/automation-scenario-aws-deployment/runbook-settings-logging-and-tracing.png)  

1. Iremos pretende toostart Olá runbook, por isso, clique em **iniciar** e, em seguida, clique em **OK** quando se abre o Painel Iniciar Runbook de Olá.
2. No painel de iniciar Runbook Olá, forneça um **VMname**.  Aceite os valores predefinidos de Olá para Olá outros parâmetros que pré-configurado no script de Olá anteriormente.  Clique em **OK** tarefa de runbook toostart Olá.<br><br> ![Iniciar AwsVM novo runbook](./media/automation-scenario-aws-deployment/runbook-start-job-parameters.png)
3. É aberto um painel de tarefas Olá tarefa de runbook que acabamos de criar. Feche este painel.
4. Iremos pode ver o progresso da saída de tarefa e vista Olá **fluxos** selecionando Olá **todos os registos** mosaico do painel de tarefas de runbook Olá.<br><br> ![Saída de fluxo](./media/automation-scenario-aws-deployment/runbook-job-streams-output.png)
5. Olá tooconfirm VM está a ser aprovisionada, iniciar sessão Olá consola de gestão do AWS, se não tem sessão iniciada.<br><br> ![Consola AWS implementado VM](./media/automation-scenario-aws-deployment/aws-instances-status.png)

## <a name="next-steps"></a>Passos seguintes
* tooget iniciado com runbooks gráficos, consulte [meu primeiro runbook gráfico](automation-first-runbook-graphical.md)
* tooget iniciado com runbooks do fluxo de trabalho do PowerShell, consulte [o meu primeiro runbook do fluxo de trabalho do PowerShell](automation-first-runbook-textual.md)
* tooknow mais informações sobre tipos de runbook, as vantagens e limitações, consulte [tipos de runbook da automatização do Azure](automation-runbook-types.md)
* Para mais informações sobre a funcionalidade de suporte de scripts do PowerShell, consulte o artigo [Suporte de scripts do PowerShell Nativo na Automatização do Azure](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)

