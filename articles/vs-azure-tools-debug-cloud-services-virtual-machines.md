---
title: "aaaDebugging do Azure na nuvem, serviço ou máquina virtual no Visual Studio | Microsoft Docs"
description: "A depuração de um serviço em nuvem ou Máquina Virtual no Visual Studio"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 945e06e0-2100-41af-b218-72347367ddab
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 32a326430021ba2ea9317a6a71fa005d4b87c273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-an-azure-cloud-service-or-virtual-machine-in-visual-studio"></a>A depuração de um serviço em nuvem do Azure ou a máquina virtual no Visual Studio
Visual Studio fornece-lhe diferentes opções para a depuração de máquinas virtuais e serviços em nuvem do Azure.

## <a name="debug-your-cloud-service-on-your-local-computer"></a>Depurar o seu serviço em nuvem no seu computador local
Pode poupar tempo e dinheiro utilizando toodebug de emulador de computação do Azure Olá seu serviço em nuvem num computador local. Por depuração localmente um serviço antes de implementá-lo, pode melhorar a fiabilidade e desempenho sem pagar tempo de computação. No entanto, poderão ocorrer alguns erros apenas quando executa um serviço em nuvem no Azure em si. Pode depurar estes erros se ativar a depuração remota quando publicar o serviço e, em seguida, anexar a instância de função Olá depurador tooa.

emulador Olá simula o serviço de computação do Azure Olá e é executado no seu ambiente local para que possa testar e depurar o seu serviço em nuvem antes de implementá-lo. os identificadores de emulador de Olá Olá ciclo de vida das suas instâncias de função e fornece acesso toosimulated recursos, tais como o armazenamento local. Quando a depuração ou executar o serviço a partir do Visual Studio, inicia o emulador de Olá automaticamente como uma aplicação de segundo plano e, em seguida, implementa o emulador de toohello do serviço. Pode utilizar Olá emulador tooview seu serviço quando for executada no ambiente local Olá. Pode executar a versão completa do Olá ou versão rápida de Olá do emulador de Olá. (A partir do Azure 2.3, Olá rápida versão do emulador de Olá é predefinido Olá.) Consulte [tooRun utilizando o emulador Express e depuração um serviço em nuvem localmente](https://msdn.microsoft.com/library/dn339018.aspx).

### <a name="toodebug-your-cloud-service-on-your-local-computer"></a>toodebug sua nuvem de serviço no seu computador local
1. Na barra de menus Olá, escolha **depurar**, **iniciar depuração** toorun projeto de serviço em nuvem do Azure. Como alternativa, pode premir F5. Verá uma mensagem que Olá emulador de computação está a iniciar. Quando inicia o emulador de Olá, o ícone de tabuleiro de sistema Olá confirma-lo.

    ![Emulador do Azure no tabuleiro de sistema Olá](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC783828.png)
2. Apresentar o interface de utilizador de Olá para o emulador de computação Olá ao abrir o menu de atalho Olá para Olá Azure ícone na área de notificação de Olá e, em seguida, selecione **mostrar IU do emulador de computação**.

    painel esquerdo do Olá da Olá IU mostra Olá serviços atualmente implementado toohello computação emulador e Olá instâncias de função que cada serviço está em execução. Pode escolher Olá serviço ou funções toodisplay ciclo de vida, registo e informações de diagnóstico no painel direito Olá. Se o put foco Olá na margem superior do Olá de uma janela incluída, que expande painel à direita do toofill Olá.
3. Passo através da aplicação Olá selecionando comandos no Olá **depurar** menu e a definição de pontos de interrupção no seu código. Como passo através da aplicação Olá no depurador Olá, painéis de Olá são atualizados com o estado atual do Olá da aplicação Olá. Quando deixa de depuração, a implementação da aplicação Olá é eliminada. Se a aplicação inclui uma função da web e definiu Olá arranque ação propriedade toostart Olá browser da web, o Visual Studio inicia a aplicação web no browser Olá. Se alterar o número de Olá de instâncias de uma função da configuração do serviço de Olá, tem de parar o serviço de nuvem e, em seguida, reinicie a depuração para que pode depurar estas novas instâncias da função de Olá.

    **Nota:** quando parar de executar ou depuração do seu serviço, Olá emulador de computação local e o emulador de armazenamento não estão parados. Tem de pará-los explicitamente partir da área de notificação de Olá.

## <a name="debug-a-cloud-service-in-azure"></a>Depurar um serviço em nuvem no Azure
toodebug um serviço em nuvem a partir de um computador remoto, tem de ativar essa funcionalidade explicitamente quando implementar o serviço de nuvem, para que o necessário serviços (msvsmon.exe, por exemplo) estão instalados em máquinas virtuais Olá que executam as instâncias da função. Se não ativar a depuração remota quando publicado serviço Olá, tem de serviço de Olá toorepublish com a depuração remota ativada.

Se ativar a depuração remota para um serviço em nuvem, não apresentem um degradação do desempenho ou implicar custos adicionais. Não deve utilizar a depuração remota no serviço de produção, porque os clientes que utilizam o serviço de Olá poderão ser afetados negativamente.

> [!NOTE]
> Quando publica um serviço em nuvem do Visual Studio, pode ativar **IntelliTrace** para quaisquer funções em que esse Olá destino .NET Framework 4 de serviço ou Olá .NET Framework 4.5. Ao utilizar **IntelliTrace**, pode examinar os eventos que ocorreram numa instância de função no Olá anterior e reproduzir o contexto de Olá do tempo. Consulte [depuração um serviço de nuvem publicada com IntelliTrace e o Visual Studio](http://go.microsoft.com/fwlink/?LinkID=623016) e [utilizando IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx).
>
>

### <a name="tooenable-remote-debugging-for-a-cloud-service"></a>tooenable remoto de depuração para um serviço em nuvem
1. Abra o menu de atalho Olá para Olá projeto do Azure e, em seguida, selecione **publicar**.
2. Selecione Olá **transição** ambiente e Olá **depurar** configuração.

    Isto é apenas uma orientação. Pode escolher toorun seus ambientes de teste num ambiente de produção. No entanto, pode afetar negativamente os utilizadores se ativar a depuração remota no ambiente de produção Olá. Pode escolher a configuração da versão Olá, mas a configuração de depuração Olá torna mais fácil a depuração.

    ![Escolha a configuração de depuração Olá](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746717.gif)
3. Siga os passos habitual Olá, mas Olá selecione **ativar remoto depurador para todas as funções** caixa de verificação Olá **definições avançadas** separador.

    ![Configuração de depuração](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746718.gif)

### <a name="tooattach-hello-debugger-tooa-cloud-service-in-azure"></a>tooattach Olá depurador tooa serviço em nuvem do Azure
1. No Explorador de servidores, expanda o nó de Olá do serviço em nuvem.
2. Menu de atalho Olá aberto para a função de Olá ou toowhich de instância de função que pretende tooattach e, em seguida, selecione **anexar depurador**.

    Se depurar uma função, o depurador do Visual Studio Olá anexa tooeach instância de função. depurador Olá irá interromper a no ponto de interrupção para Olá primeira instância de função que executa dessa linha de código e cumpre as condições desse ponto de interrupção. Se a depuração uma instância, o depurador Olá anexa tooonly que a instância e as quebras de um ponto de interrupção apenas quando a essa instância específica executa dessa linha de código e cumpre Olá condições do ponto de interrupção.

    ![Anexar o depurador](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746719.gif)
3. Depois de depurador de Olá anexa tooan instância, depurar como habitualmente. depurador Olá anexa automaticamente toohello o processo de anfitrião adequado para a sua função. Dependendo do que Olá função for, Olá depurador anexa toow3wp.exe, WaWorkerHost.exe ou WaIISHost.exe. está ligado tooverify Olá processo toowhich Olá depurador, expanda o nó de instância de Olá no Explorador de servidores. Consulte [arquitetura de função do Azure](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx) para obter mais informações sobre processos de Azure.

    ![Selecione a caixa de diálogo de tipo de código](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
4. os processos de Olá tooidentify está ligado toowhich Olá depurador, abra a caixa de diálogo de processos do Olá por, no menu de Olá barra, escolher depuração, Windows, os processos. (Teclado: Ctrl + Alt + Z) toodetach um processo específico, abra o menu de atalho e, em seguida, selecione **desanexar processo**. Ou, localizar o nó de instância de Olá no Explorador de servidores, encontrar o processo de Olá, abra o menu de atalho e, em seguida, selecione **desanexar processo**.

    ![Os processos de depuração](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC690787.gif)

> [!WARNING]
> Evitar deixa de tempo em pontos de interrupção quando remoto depuração. Azure trata de um processo que é interrompido durante um período superior a alguns minutos enquanto não responde e interrompe a instância de toothat tráfego a enviar. Se parar há demasiado tempo, msvsmon.exe Desanexa do processo de Olá.
>
>

depurador de Olá toodetach de todos os processos na sua instância ou a função, o menu de atalho Olá aberto para a função Olá ou instância que está a depuração e, em seguida, selecione **desanexar depurador**.

## <a name="limitations-of-remote-debugging-in-azure"></a>Limitações de depuração remota no Azure
Do Azure SDK 2.3, depuração remota tem Olá limitações a seguir.

* Com a depuração remota ativada, não é possível publicar um serviço em nuvem em que qualquer função tem mais de 25 instâncias.
* depurador Olá utiliza too30424 30400 portas, 31400 too31424 e 32400 too32424. Se tentar toouse qualquer um destas portas, não será capaz de toopublish o serviço e uma das seguintes mensagens de erro de Olá aparecerá no registo de atividade Olá para o Azure:

  * Erro ao validar ficheiro. cscfg Olá contra o ficheiro. csdef Olá.
    Olá reservado intervalo de portas 'intervalo' para o ponto final que Microsoft.windowsazure.plugins.remotedebugger.Connector da função "função" sobrepõe-se um intervalo ou a porta já definida.
  * Falha na alocação. Tente novamente mais tarde, tente reduzir Olá tamanho da VM ou o número de instâncias de função ou experimente implementar noutra região de tooa.

## <a name="debugging-azure-virtual-machines"></a>A depuração de máquinas virtuais do Azure
Pode depurar programas que são executadas em máquinas virtuais do Azure utilizando o Explorador de servidores no Visual Studio. Quando ativar a depuração remota numa máquina virtual do Azure, Azure instala a extensão de depuração remota Olá na máquina virtual de Olá. Em seguida, pode anexar tooprocesses na máquina virtual de Olá e depurar como faria normalmente.

> [!NOTE]
> Máquinas virtuais criadas através da pilha de Gestor de recursos do Azure Olá pode ser debugged remotamente através da utilização de Cloud Explorer no Visual Studio 2015. Para obter mais informações, consulte [gerir recursos do Azure com Cloud Explorer](http://go.microsoft.com/fwlink/?LinkId=623031).
>
>

### <a name="toodebug-an-azure-virtual-machine"></a>toodebug uma máquina virtual do Azure
1. No Explorador de servidores, expanda o nó de máquinas virtuais de Olá e nó de Olá selecione da máquina virtual de Olá que pretende que o toodebug.
2. Abra o menu de contexto de Olá e selecione **ativar a depuração**. Quando lhe for perguntado se tem a certeza se quiser tooenable depuração na máquina virtual de Olá, selecione **Sim**.

    Azure instala a extensão de depuração remota Olá sobre a depuração de tooenable do Olá máquina virtual.

    ![Máquina virtual ativar comando de depuração](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Registo de atividade do Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)
3. Após a extensão de depuração remota Olá instalar, abra o menu de contexto da máquina virtual Olá e selecione **anexar depurador...**

    Azure obtém uma lista dos processos de Olá na máquina virtual de Olá e mostra-los na caixa de diálogo Olá anexar tooProcess.

    ![Anexar o comando do depurador](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)
4. No Olá **anexar tooProcess** caixa de diálogo, selecione **selecione** resultados de Olá toolimit listam apenas os tipos Olá tooshow de código que pretende toodebug. Pode depurar código de 32 ou 64-bits gerido, o código nativo ou ambos.

    ![Selecione a caixa de diálogo de tipo de código](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
5. Selecione os processos de Olá que pretende toodebug na máquina virtual de Olá e, em seguida, selecione **anexar**. Por exemplo, poderá escolher o processo de w3wp.exe Olá se pretendesse toodebug uma aplicação web na máquina virtual de Olá. Consulte [depurar uma ou mais processos no Visual Studio](https://msdn.microsoft.com/library/jj919165.aspx) e [arquitetura de função do Azure](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx) para obter mais informações.

## <a name="create-a-web-project-and-a-virtual-machine-for-debugging"></a>Criar um projeto web e uma máquina virtual para depuração
Antes de publicar o projeto do Azure, poderá achar útil tootest-la num ambiente que suporta a depuração e testar cenários e onde pode instalar teste e monitorização programas contido. Toodo unidirecional trata tooremotely depurar a aplicação numa máquina virtual.

Projetos do Visual Studio ASP.NET oferecem uma opção toocreate uma máquina virtual à mão, que pode utilizar para testar a aplicação. máquina virtual de Olá inclui pontos finais necessários normalmente como o PowerShell, o ambiente de trabalho remoto e o WebDeploy.

### <a name="toocreate-a-web-project-and-a-virtual-machine-for-debugging"></a>toocreate um projeto web e uma máquina virtual para depuração
1. No Visual Studio, crie uma nova aplicação Web de ASP.NET.
2. Na caixa de diálogo da novo projeto ASP.NET Olá, na secção do Azure, de Olá escolha **Máquina Virtual** na caixa de listagem pendente Olá. Deixe Olá **criar recursos remotos** caixa de verificação selecionada. Selecione **OK** tooproceed.

    Olá **criar máquina virtual no Azure** é apresentada a caixa de diálogo.

    ![Criar caixa de diálogo de projeto de web ASP.NET](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746723.png)

    **Nota:** irá ser-lhe pedido toosign no tooyour conta do Azure se ainda não tem sessão iniciada.

1. Selecione Olá várias definições para a máquina virtual de Olá e, em seguida, selecione **OK**. Consulte [máquinas virtuais](http://go.microsoft.com/fwlink/?LinkId=623033) para obter mais informações.

    nome de Olá que introduziu para nome DNS será o nome de Olá da máquina virtual de Olá.

    ![Criar máquina virtual na caixa de diálogo do Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746724.png)

    O Azure cria a máquina virtual de Olá e, em seguida, Aprovisiona e configura pontos finais de Olá, tais como o ambiente de trabalho remoto e o Web Deploy
2. Depois de máquina virtual de Olá completamente estar configurada, selecione o nó da máquina virtual Olá no Explorador de servidores.
3. Abra o menu de contexto de Olá e selecione **ativar a depuração**. Quando lhe for perguntado se tem a certeza se quiser tooenable depuração na máquina virtual de Olá, selecione **Sim**.

    Azure instala Olá depuração extensão toohello máquina virtual tooenable depuração remota.

    ![Máquina virtual ativar comando de depuração](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Registo de atividade do Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)
4. Publicar o seu projeto conforme descrito na [como: implementar um projeto através de um clique publicação na Web no Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx). Porque pretende toodebug numa máquina virtual de Olá, no Olá **definições** página do Olá **publicar Web** assistente, selecione **depurar** como configuração Olá. Isto certifica-se de que os símbolos de código estão disponíveis durante a depuração.

    ![Definições de publicação](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718349.png)
5. No Olá **opções de publicação do ficheiro**, selecione **remover ficheiros adicionais no destino** se projeto Olá já foi implementado cedo.
6. Depois do projeto de Olá publica, no menu de contexto da máquina virtual Olá no Explorador de servidores, selecione **anexar depurador...**

    Azure obtém uma lista dos processos de Olá na máquina virtual de Olá e mostra-los na caixa de diálogo Olá anexar tooProcess.

    ![Anexar o comando do depurador](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)
7. No Olá **anexar tooProcess** caixa de diálogo, selecione **selecione** resultados de Olá toolimit listam apenas os tipos Olá tooshow de código que pretende toodebug. Pode depurar código de 32 ou 64-bits gerido, o código nativo ou ambos.

    ![Selecione a caixa de diálogo de tipo de código](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
8. Selecione os processos de Olá que pretende toodebug na máquina virtual de Olá e, em seguida, selecione **anexar**. Por exemplo, poderá escolher o processo de w3wp.exe Olá se pretendesse toodebug uma aplicação web na máquina virtual de Olá. Consulte [depurar uma ou mais processos no Visual Studio](https://msdn.microsoft.com/library/jj919165.aspx) para obter mais informações.

## <a name="next-steps"></a>Passos seguintes
* Utilize **Intellitrace** toocollect um registo de eventos de um servidor de versão e chamadas. Consulte [depuração um serviço de nuvem publicada com IntelliTrace e o Visual Studio](http://go.microsoft.com/fwlink/?LinkID=623016).
* Utilize **diagnósticos do Azure** toolog obter informações detalhadas a execução de código dentro de funções, se as funções de Olá estão em execução no ambiente de desenvolvimento de Olá ou no Azure. Consulte [recolher dados de registo utilizando o Azure Diagnostics](http://go.microsoft.com/fwlink/p/?LinkId=400450).
