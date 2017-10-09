---
title: "uma nuvem serviço localmente no emulador de computação de Olá aaaProfiling | Microsoft Docs"
services: cloud-services
description: "Investigar problemas de desempenho nos serviços em nuvem com o gerador de perfis do Olá Visual Studio"
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
tags: 
ms.assetid: 25e40bf3-eea0-4b0b-9f4a-91ffe797f6c3
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: fc37c85dad4db4cc0310f73afad56fc0fe5f3963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a><span data-ttu-id="013ef-103">Testar Olá desempenho de um serviço em nuvem localmente num Olá utilizando o emulador de computação do Azure Olá Visual Studio do gerador de perfis</span><span class="sxs-lookup"><span data-stu-id="013ef-103">Testing hello Performance of a Cloud Service Locally in hello Azure Compute Emulator Using hello Visual Studio Profiler</span></span>
<span data-ttu-id="013ef-104">Uma variedade de ferramentas e técnicas estão disponíveis para testar o desempenho de Olá dos serviços em nuvem.</span><span class="sxs-lookup"><span data-stu-id="013ef-104">A variety of tools and techniques are available for testing hello performance of cloud services.</span></span>
<span data-ttu-id="013ef-105">Quando publica um tooAzure do serviço de nuvem, pode ter o Visual Studio recolher dados de criação de perfis e, em seguida, analisá-lo localmente, conforme descrito em [criação de perfis de uma aplicação do Azure][1].</span><span class="sxs-lookup"><span data-stu-id="013ef-105">When you publish a cloud service tooAzure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="013ef-106">Também pode utilizar tootrack diagnóstico contadores de uma variedade de desempenho, conforme descrito em [utilizando os contadores de desempenho no Azure][2].</span><span class="sxs-lookup"><span data-stu-id="013ef-106">You can also use diagnostics tootrack a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="013ef-107">Pode também querer tooprofile a aplicação localmente no emulador de computação Olá antes de o implementar toohello nuvem.</span><span class="sxs-lookup"><span data-stu-id="013ef-107">You might also want tooprofile your application locally in hello compute emulator before deploying it toohello cloud.</span></span>

<span data-ttu-id="013ef-108">Este artigo abrange o método de amostragem de CPU Olá de criação de perfis, que pode ser efetuado localmente no emulador Olá.</span><span class="sxs-lookup"><span data-stu-id="013ef-108">This article covers hello CPU Sampling method of profiling, which can be done locally in hello emulator.</span></span> <span data-ttu-id="013ef-109">A amostragem da CPU é um método de criação de perfis que não é intrusivo muito.</span><span class="sxs-lookup"><span data-stu-id="013ef-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="013ef-110">Num intervalo de amostragem designado, o gerador de perfis de Olá tira um instantâneo da pilha de chamadas de Olá.</span><span class="sxs-lookup"><span data-stu-id="013ef-110">At a designated sampling interval, hello profiler takes a snapshot of hello call stack.</span></span> <span data-ttu-id="013ef-111">Olá dados são recolhidos ao longo de um período de tempo e apresentados num relatório.</span><span class="sxs-lookup"><span data-stu-id="013ef-111">hello data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="013ef-112">Este método de criação de perfis tende tooindicate onde numa aplicação viáveis intensiva maioria do trabalho Olá CPU está a ser efetuada.</span><span class="sxs-lookup"><span data-stu-id="013ef-112">This method of profiling tends tooindicate where in a computationally intensive application most of hello CPU work is being done.</span></span>  <span data-ttu-id="013ef-113">Este oferece Olá oportunidade toofocus no Olá "frequente caminho" em que a aplicação é gastos Olá mais tempo.</span><span class="sxs-lookup"><span data-stu-id="013ef-113">This gives you hello opportunity toofocus on hello "hot path" where your application is spending hello most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="013ef-114">1: configurar o Visual Studio para criação de perfis</span><span class="sxs-lookup"><span data-stu-id="013ef-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="013ef-115">Em primeiro lugar, existem algumas opções de configuração do Visual Studio que poderão ser úteis quando a criação de perfis.</span><span class="sxs-lookup"><span data-stu-id="013ef-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="013ef-116">Olá, toomake sentido de criação de perfis de relatórios, terá de símbolos (ficheiros .pdb) para a sua aplicação e também símbolos para bibliotecas do sistema.</span><span class="sxs-lookup"><span data-stu-id="013ef-116">toomake sense of hello profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="013ef-117">Poderá ser útil se de que o se que fazem referência a servidores de símbolo disponíveis Olá toomake.</span><span class="sxs-lookup"><span data-stu-id="013ef-117">You'll want toomake sure that you reference hello available symbol servers.</span></span> <span data-ttu-id="013ef-118">toodo isto, na Olá **ferramentas** menu no Visual Studio, escolha **opções**, em seguida, escolha **a depuração**, em seguida, **símbolos**.</span><span class="sxs-lookup"><span data-stu-id="013ef-118">toodo this, on hello **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="013ef-119">Certifique-se de que os servidores do Microsoft símbolo está listado em **localizações de ficheiros (.pdb) do símbolo**.</span><span class="sxs-lookup"><span data-stu-id="013ef-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="013ef-120">Também pode referenciar http://referencesource.microsoft.com/symbols, que pode ter ficheiros de símbolo adicionais.</span><span class="sxs-lookup"><span data-stu-id="013ef-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![Opções de símbolo][4]

<span data-ttu-id="013ef-122">Se assim o desejar, pode simplificar a Olá relatórios que gerador de perfis de Olá gera definindo apenas código My.</span><span class="sxs-lookup"><span data-stu-id="013ef-122">If desired, you can simplify hello reports that hello profiler generates by setting Just My Code.</span></span> <span data-ttu-id="013ef-123">Com apenas os meus código ativada, as pilhas de chamada de função são simplificadas, de modo a que as chamadas toolibraries inteiramente interno e Olá .NET Framework estão ocultas dos relatórios de Olá.</span><span class="sxs-lookup"><span data-stu-id="013ef-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal toolibraries and hello .NET Framework are hidden from hello reports.</span></span> <span data-ttu-id="013ef-124">No Olá **ferramentas** menu, escolha **opções**.</span><span class="sxs-lookup"><span data-stu-id="013ef-124">On hello **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="013ef-125">Em seguida, expanda Olá **ferramentas de desempenho** nó e escolha **geral**.</span><span class="sxs-lookup"><span data-stu-id="013ef-125">Then expand hello **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="013ef-126">Selecione a caixa de verificação Olá para **ative apenas os meus código para o gerador de perfis relatórios**.</span><span class="sxs-lookup"><span data-stu-id="013ef-126">Select hello checkbox for **Enable Just My Code for profiler reports**.</span></span>

![Apenas as opções de código My][17]

<span data-ttu-id="013ef-128">Pode utilizar estas instruções com um projeto existente ou com um novo projeto.</span><span class="sxs-lookup"><span data-stu-id="013ef-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="013ef-129">Se criar um novo tootry Olá da projeto técnicas descritas abaixo, escolha um c# **o serviço em nuvem do Azure** projeto e selecione um **função Web** e um **função de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="013ef-129">If you create a new project tootry hello techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Funções de projeto de serviço em nuvem do Azure][5]

<span data-ttu-id="013ef-131">Por exemplo fins, adicionar algum código tooyour projeto demora muito tempo e demonstra a um problema de desempenho óbvios.</span><span class="sxs-lookup"><span data-stu-id="013ef-131">For example purposes, add some code tooyour project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="013ef-132">Por exemplo, adicione Olá projeto de função de trabalho do código tooa os seguintes:</span><span class="sxs-lookup"><span data-stu-id="013ef-132">For example, add hello following code tooa worker role project:</span></span>

    public class Concatenator
    {
        public static string Concatenate(int number)
        {
            int count;
            string s = "";
            for (count = 0; count < number; count++)
            {
                s += "\n" + count.ToString();
            }
            return s;
        }
    }

<span data-ttu-id="013ef-133">Chame este código de Olá método runasync com na classe derivada de RoleEntryPoint da função de trabalho Olá.</span><span class="sxs-lookup"><span data-stu-id="013ef-133">Call this code from hello RunAsync method in hello worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="013ef-134">(Ignorar o aviso de Olá sobre o método de Olá executar de forma síncrona.)</span><span class="sxs-lookup"><span data-stu-id="013ef-134">(Ignore hello warning about hello method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="013ef-135">Compilar e executar localmente o serviço em nuvem sem depuração (Ctrl + F5), com configuração de solução Olá definida demasiado**versão**.</span><span class="sxs-lookup"><span data-stu-id="013ef-135">Build and run your cloud service locally without debugging (Ctrl+F5), with hello solution configuration set too**Release**.</span></span> <span data-ttu-id="013ef-136">Isto garante que todos os ficheiros e pastas são criados para executar a aplicação Olá localmente e garante que todos os emuladores de Olá são iniciados.</span><span class="sxs-lookup"><span data-stu-id="013ef-136">This ensures that all files and folders are created for running hello application locally, and ensures that all hello emulators are started.</span></span> <span data-ttu-id="013ef-137">Inicie Olá IU do emulador de computação de Olá tooverify de barra de tarefas que está a executar a função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="013ef-137">Start hello Compute Emulator UI from hello taskbar tooverify that your worker role is running.</span></span>

## <a name="2-attach-tooa-process"></a><span data-ttu-id="013ef-138">2: ligar tooa processo</span><span class="sxs-lookup"><span data-stu-id="013ef-138">2: Attach tooa process</span></span>
<span data-ttu-id="013ef-139">Em vez de criação de perfis de aplicação Olá por iniciá-lo a partir de Olá IDE de 2010 do Visual Studio, terá de ligar Olá gerador de perfis tooa a executar o processo.</span><span class="sxs-lookup"><span data-stu-id="013ef-139">Instead of profiling hello application by starting it from hello Visual Studio 2010 IDE, you must attach hello profiler tooa running process.</span></span> 

<span data-ttu-id="013ef-140">tooattach Olá gerador de perfis tooa processo, em Olá **analisar** menu, escolha **gerador de perfis** e **anexar/desanexar**.</span><span class="sxs-lookup"><span data-stu-id="013ef-140">tooattach hello profiler tooa process, on hello **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![Anexar a opção de perfil][6]

<span data-ttu-id="013ef-142">Para uma função de trabalho, encontrar o processo de WaWorkerHost.exe Olá.</span><span class="sxs-lookup"><span data-stu-id="013ef-142">For a worker role, find hello WaWorkerHost.exe process.</span></span>

![Processo de WaWorkerHost][7]

<span data-ttu-id="013ef-144">Se a pasta do projeto é numa unidade de rede, o gerador de perfis Olá irá pedir-lhe tooprovide Olá toosave outra localização, criação de perfis de relatórios.</span><span class="sxs-lookup"><span data-stu-id="013ef-144">If your project folder is on a network drive, hello profiler will ask you tooprovide another location toosave hello profiling reports.</span></span>

 <span data-ttu-id="013ef-145">Também pode anexar a função da web tooa ligando tooWaIISHost.exe.</span><span class="sxs-lookup"><span data-stu-id="013ef-145">You can also attach tooa web role by attaching tooWaIISHost.exe.</span></span>
<span data-ttu-id="013ef-146">Se existirem vários processos de função de trabalho na sua aplicação, terá de toouse Olá processID toodistinguish-los.</span><span class="sxs-lookup"><span data-stu-id="013ef-146">If there are multiple worker role processes in your application, you need toouse hello processID toodistinguish them.</span></span> <span data-ttu-id="013ef-147">Pode consultar Olá processID através de programação, ao aceder ao objeto de processo Olá.</span><span class="sxs-lookup"><span data-stu-id="013ef-147">You can query hello processID programmatically by accessing hello Process object.</span></span> <span data-ttu-id="013ef-148">Por exemplo, se adicionar este método de execução do código toohello da classe derivada de RoleEntryPoint de Olá numa função, pode examinar o registo no Olá tooknow de IU do emulador de computação que tooconnect de processo para.</span><span class="sxs-lookup"><span data-stu-id="013ef-148">For example, if you add this code toohello Run method of hello RoleEntryPoint-derived class in a role, you can look at the log in hello Compute Emulator UI tooknow what process tooconnect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="013ef-149">registo de Olá tooview, início Olá IU do emulador de computação.</span><span class="sxs-lookup"><span data-stu-id="013ef-149">tooview hello log, start hello Compute Emulator UI.</span></span>

![Iniciar Olá IU do emulador de computação][8]

<span data-ttu-id="013ef-151">Abra a janela de consola de registo de função de trabalho de Olá na IU do emulador de computação de Olá clicando na barra de título da janela de consola Olá.</span><span class="sxs-lookup"><span data-stu-id="013ef-151">Open hello worker role log console window in hello Compute Emulator UI by clicking on hello console window's title bar.</span></span> <span data-ttu-id="013ef-152">Pode ver o ID do processo Olá no registo de Olá.</span><span class="sxs-lookup"><span data-stu-id="013ef-152">You can see hello process ID in hello log.</span></span>

![ID do processo de vista][9]

<span data-ttu-id="013ef-154">Um que tenha ligado, executar passos Olá num cenário de Olá de tooreproduce de IU (se necessário) da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="013ef-154">One you've attached, perform hello steps in your application's UI (if needed) tooreproduce hello scenario.</span></span>

<span data-ttu-id="013ef-155">Se pretender que a criação de perfis de toostop, escolha Olá **parar a criação de perfis** ligação.</span><span class="sxs-lookup"><span data-stu-id="013ef-155">When you want toostop profiling, choose hello **Stop Profiling** link.</span></span>

![Parar a opção de criação de perfis][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="013ef-157">3: ver relatórios de desempenho</span><span class="sxs-lookup"><span data-stu-id="013ef-157">3: View performance reports</span></span>
<span data-ttu-id="013ef-158">relatório de desempenho de Olá para a sua aplicação é apresentado.</span><span class="sxs-lookup"><span data-stu-id="013ef-158">hello performance report for your application is displayed.</span></span>

<span data-ttu-id="013ef-159">Neste momento, o gerador de perfis de Olá deixa de executar, guarda dados num ficheiro .vsp e apresenta um relatório que mostra uma análise de dados.</span><span class="sxs-lookup"><span data-stu-id="013ef-159">At this point, hello profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![Relatório de gerador de perfis][11]

<span data-ttu-id="013ef-161">Se vir String.wstrcpy no Olá caminho instantâneo, clique em apenas código My toochange Olá vista tooshow utilizador apenas código.</span><span class="sxs-lookup"><span data-stu-id="013ef-161">If you see String.wstrcpy in hello Hot Path, click on Just My Code toochange hello view tooshow user code only.</span></span>  <span data-ttu-id="013ef-162">Se vir String.Concat, tente premindo Olá todo o código Mostrar botão.</span><span class="sxs-lookup"><span data-stu-id="013ef-162">If you see String.Concat, try pressing hello Show All Code button.</span></span>

<span data-ttu-id="013ef-163">Deverá ver o método Concatenate Olá e String.Concat utilizando uma grande parte do tempo de execução de Olá.</span><span class="sxs-lookup"><span data-stu-id="013ef-163">You should see hello Concatenate method and String.Concat taking up a large portion of hello execution time.</span></span>

![Análise de relatório][12]

<span data-ttu-id="013ef-165">Se tiver adicionado o código de concatenação de cadeia Olá neste artigo, deverá ver um aviso no Olá lista de tarefas para esta.</span><span class="sxs-lookup"><span data-stu-id="013ef-165">If you added hello string concatenation code in this article, you should see a warning in hello Task List for this.</span></span> <span data-ttu-id="013ef-166">Também poderá ver um aviso que não há uma quantidade excessiva de recolha de lixo, que é que devem estar toohello número de cadeias que são criados e eliminado.</span><span class="sxs-lookup"><span data-stu-id="013ef-166">You may also see a warning that there is an excessive amount of garbage collection, which is due toohello number of strings that are created and disposed.</span></span>

![Avisos de desempenho][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="013ef-168">4: efetuar alterações e compare o desempenho</span><span class="sxs-lookup"><span data-stu-id="013ef-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="013ef-169">Também pode comparar o desempenho de Olá antes e após uma alteração de código.</span><span class="sxs-lookup"><span data-stu-id="013ef-169">You can also compare hello performance before and after a code change.</span></span>  <span data-ttu-id="013ef-170">Parar Olá a executar o processo e editar Olá código tooreplace Olá cadeia concatenação operação com a utilização de Olá de StringBuilder:</span><span class="sxs-lookup"><span data-stu-id="013ef-170">Stop hello running process, and edit hello code tooreplace hello string concatenation operation with hello use of StringBuilder:</span></span>

    public static string Concatenate(int number)
    {
        int count;
        System.Text.StringBuilder builder = new System.Text.StringBuilder("");
        for (count = 0; count < number; count++)
        {
             builder.Append("\n" + count.ToString());
        }
        return builder.ToString();
    }

<span data-ttu-id="013ef-171">Não executar outra de desempenho e, em seguida, compare o desempenho de Olá.</span><span class="sxs-lookup"><span data-stu-id="013ef-171">Do another performance run, and then compare hello performance.</span></span> <span data-ttu-id="013ef-172">No Explorador de desempenho Olá, se hello executa está disponíveis na Olá mesma sessão, apenas pode selecionar ambos os relatórios, abra o menu de atalho Olá e escolha **comparar o desempenho relatórios**.</span><span class="sxs-lookup"><span data-stu-id="013ef-172">In hello Performance Explorer, if hello runs are in hello same session, you can just select both reports, open hello shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="013ef-173">Se quiser toocompare com uma execução na outra sessão de desempenho, abra Olá **analisar** menu e escolha **comparar o desempenho relatórios**.</span><span class="sxs-lookup"><span data-stu-id="013ef-173">If you want toocompare with a run in another performance session, open hello **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="013ef-174">Especifique ambos os ficheiros na caixa de diálogo Olá, que é apresentada.</span><span class="sxs-lookup"><span data-stu-id="013ef-174">Specify both files in hello dialog box that appears.</span></span>

![Comparar a opção de relatórios de desempenho][15]

<span data-ttu-id="013ef-176">relatórios de Olá realce as diferenças entre duas executa Olá.</span><span class="sxs-lookup"><span data-stu-id="013ef-176">hello reports highlight differences between hello two runs.</span></span>

![Relatório de comparação][16]

<span data-ttu-id="013ef-178">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="013ef-178">Congratulations!</span></span> <span data-ttu-id="013ef-179">Que tiver iniciado com o gerador de perfis de Olá.</span><span class="sxs-lookup"><span data-stu-id="013ef-179">You've gotten started with hello profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="013ef-180">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="013ef-180">Troubleshooting</span></span>
* <span data-ttu-id="013ef-181">Certifique-se de que é uma versão de lançamento de criação de perfis e iniciar sem depuração.</span><span class="sxs-lookup"><span data-stu-id="013ef-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="013ef-182">Se Olá anexar/desanexar opção não estiver ativada no menu do gerador de perfis de Olá, execute Olá Assistente de desempenho.</span><span class="sxs-lookup"><span data-stu-id="013ef-182">If hello Attach/Detach option is not enabled on hello Profiler menu, run hello Performance Wizard.</span></span>
* <span data-ttu-id="013ef-183">Utilize o Olá IU do emulador de computação tooview Olá estado da aplicação.</span><span class="sxs-lookup"><span data-stu-id="013ef-183">Use hello Compute Emulator UI tooview hello status of your application.</span></span> 
* <span data-ttu-id="013ef-184">Se tiver problemas a partir de aplicações emulador Olá ou a anexar Olá gerador de perfis, encerre o emulador de computação Olá e reiniciá-lo.</span><span class="sxs-lookup"><span data-stu-id="013ef-184">If you have problems starting applications in hello emulator, or attaching hello profiler, shut down hello compute emulator and restart it.</span></span> <span data-ttu-id="013ef-185">Se que não resolverem o problema de Olá, tente reiniciar.</span><span class="sxs-lookup"><span data-stu-id="013ef-185">If that doesn't solve hello problem, try rebooting.</span></span> <span data-ttu-id="013ef-186">Este problema pode ocorrer se utilizar Olá emulador de computação toosuspend e remover implementações em execução.</span><span class="sxs-lookup"><span data-stu-id="013ef-186">This problem can occur if you use hello Compute Emulator toosuspend and remove running deployments.</span></span>
* <span data-ttu-id="013ef-187">Se tiver utilizado a qualquer um dos comandos da linha de comandos de criação de perfis de Olá, especialmente Olá definições globais, certifique-se de que VSPerfClrEnv /globaloff EnableNotification for chamada e que VsPerfMon.exe ter sido encerrado.</span><span class="sxs-lookup"><span data-stu-id="013ef-187">If you have used any of hello profiling commands from the command line, especially hello global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="013ef-188">Se quando amostragem, verá a mensagem de saudação "PRF0025: foram recolhidos quaisquer dados," verificação Olá processo ligado atividade toohas da CPU.</span><span class="sxs-lookup"><span data-stu-id="013ef-188">If when sampling, you see hello message "PRF0025: No data was collected," check that hello process you attached toohas CPU activity.</span></span> <span data-ttu-id="013ef-189">As aplicações que não estão a fazer qualquer trabalho computacional podem não produzir quaisquer dados de amostragem.</span><span class="sxs-lookup"><span data-stu-id="013ef-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="013ef-190">Também é possível que o processo de Olá terminado antes de qualquer amostragem foi efetuada.</span><span class="sxs-lookup"><span data-stu-id="013ef-190">It's also possible that hello process exited before any sampling was done.</span></span> <span data-ttu-id="013ef-191">Verifique toosee que método de execução de Olá para uma função que lhe está a criação de perfis não terminar.</span><span class="sxs-lookup"><span data-stu-id="013ef-191">Check toosee that hello Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="013ef-192">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="013ef-192">Next Steps</span></span>
<span data-ttu-id="013ef-193">Instrumentação binários do Azure no emulador Olá não é suportado no gerador de perfis do Olá Visual Studio, mas se pretender que a atribuição de memória tootest, pode escolher essa opção quando a criação de perfis.</span><span class="sxs-lookup"><span data-stu-id="013ef-193">Instrumenting Azure binaries in hello emulator is not supported in hello Visual Studio profiler, but if you want tootest memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="013ef-194">Também pode optar por criação de perfis de simultaneidade, que ajuda a determinar se os threads são perder tempo competir pela bloqueios, ou a camada a criação de perfis de interação, que ajuda a identificar problemas de desempenho quando a interação entre camadas de uma aplicação, mais frequentemente entre a camada de dados de Olá e uma função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="013ef-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between hello data tier and a worker role.</span></span>  <span data-ttu-id="013ef-195">Pode ver as consultas de base de dados de Olá gera a sua aplicação e utilizar Olá a criação de perfis dados tooimprove a utilização da base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="013ef-195">You can view hello database queries that your app generates and use hello profiling data tooimprove your use of hello database.</span></span> <span data-ttu-id="013ef-196">Para obter informações sobre a criação de perfis de interação do escalão, consulte a mensagem de blogue de Olá [explicação passo a passo: utilizar Olá gerador de perfis de interação de camada no Visual Studio Team System 2010][3].</span><span class="sxs-lookup"><span data-stu-id="013ef-196">For information about tier interaction profiling, see hello blog post [Walkthrough: Using hello Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

[1]: http://msdn.microsoft.com/library/azure/hh369930.aspx
[2]: http://msdn.microsoft.com/library/azure/hh411542.aspx
[3]: http://blogs.msdn.com/b/habibh/archive/2009/06/30/walkthrough-using-the-tier-interaction-profiler-in-visual-studio-team-system-2010.aspx
[4]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally09.png
[5]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally10.png
[6]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally02.png
[7]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally05.png
[8]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally010.png
[9]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally07.png
[10]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally06.png
[11]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally03.png
[12]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally011.png
[14]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally04.png 
[15]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally013.png
[16]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally012.png
[17]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally08.png
