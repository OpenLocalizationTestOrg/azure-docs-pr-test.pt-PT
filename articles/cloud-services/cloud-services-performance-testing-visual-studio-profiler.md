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
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a>Testar Olá desempenho de um serviço em nuvem localmente num Olá utilizando o emulador de computação do Azure Olá Visual Studio do gerador de perfis
Uma variedade de ferramentas e técnicas estão disponíveis para testar o desempenho de Olá dos serviços em nuvem.
Quando publica um tooAzure do serviço de nuvem, pode ter o Visual Studio recolher dados de criação de perfis e, em seguida, analisá-lo localmente, conforme descrito em [criação de perfis de uma aplicação do Azure][1].
Também pode utilizar tootrack diagnóstico contadores de uma variedade de desempenho, conforme descrito em [utilizando os contadores de desempenho no Azure][2].
Pode também querer tooprofile a aplicação localmente no emulador de computação Olá antes de o implementar toohello nuvem.

Este artigo abrange o método de amostragem de CPU Olá de criação de perfis, que pode ser efetuado localmente no emulador Olá. A amostragem da CPU é um método de criação de perfis que não é intrusivo muito. Num intervalo de amostragem designado, o gerador de perfis de Olá tira um instantâneo da pilha de chamadas de Olá. Olá dados são recolhidos ao longo de um período de tempo e apresentados num relatório. Este método de criação de perfis tende tooindicate onde numa aplicação viáveis intensiva maioria do trabalho Olá CPU está a ser efetuada.  Este oferece Olá oportunidade toofocus no Olá "frequente caminho" em que a aplicação é gastos Olá mais tempo.

## <a name="1-configure-visual-studio-for-profiling"></a>1: configurar o Visual Studio para criação de perfis
Em primeiro lugar, existem algumas opções de configuração do Visual Studio que poderão ser úteis quando a criação de perfis. Olá, toomake sentido de criação de perfis de relatórios, terá de símbolos (ficheiros .pdb) para a sua aplicação e também símbolos para bibliotecas do sistema. Poderá ser útil se de que o se que fazem referência a servidores de símbolo disponíveis Olá toomake. toodo isto, na Olá **ferramentas** menu no Visual Studio, escolha **opções**, em seguida, escolha **a depuração**, em seguida, **símbolos**. Certifique-se de que os servidores do Microsoft símbolo está listado em **localizações de ficheiros (.pdb) do símbolo**.  Também pode referenciar http://referencesource.microsoft.com/symbols, que pode ter ficheiros de símbolo adicionais.

![Opções de símbolo][4]

Se assim o desejar, pode simplificar a Olá relatórios que gerador de perfis de Olá gera definindo apenas código My. Com apenas os meus código ativada, as pilhas de chamada de função são simplificadas, de modo a que as chamadas toolibraries inteiramente interno e Olá .NET Framework estão ocultas dos relatórios de Olá. No Olá **ferramentas** menu, escolha **opções**. Em seguida, expanda Olá **ferramentas de desempenho** nó e escolha **geral**. Selecione a caixa de verificação Olá para **ative apenas os meus código para o gerador de perfis relatórios**.

![Apenas as opções de código My][17]

Pode utilizar estas instruções com um projeto existente ou com um novo projeto.  Se criar um novo tootry Olá da projeto técnicas descritas abaixo, escolha um c# **o serviço em nuvem do Azure** projeto e selecione um **função Web** e um **função de trabalho**.

![Funções de projeto de serviço em nuvem do Azure][5]

Por exemplo fins, adicionar algum código tooyour projeto demora muito tempo e demonstra a um problema de desempenho óbvios. Por exemplo, adicione Olá projeto de função de trabalho do código tooa os seguintes:

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

Chame este código de Olá método runasync com na classe derivada de RoleEntryPoint da função de trabalho Olá. (Ignorar o aviso de Olá sobre o método de Olá executar de forma síncrona.)

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

Compilar e executar localmente o serviço em nuvem sem depuração (Ctrl + F5), com configuração de solução Olá definida demasiado**versão**. Isto garante que todos os ficheiros e pastas são criados para executar a aplicação Olá localmente e garante que todos os emuladores de Olá são iniciados. Inicie Olá IU do emulador de computação de Olá tooverify de barra de tarefas que está a executar a função de trabalho.

## <a name="2-attach-tooa-process"></a>2: ligar tooa processo
Em vez de criação de perfis de aplicação Olá por iniciá-lo a partir de Olá IDE de 2010 do Visual Studio, terá de ligar Olá gerador de perfis tooa a executar o processo. 

tooattach Olá gerador de perfis tooa processo, em Olá **analisar** menu, escolha **gerador de perfis** e **anexar/desanexar**.

![Anexar a opção de perfil][6]

Para uma função de trabalho, encontrar o processo de WaWorkerHost.exe Olá.

![Processo de WaWorkerHost][7]

Se a pasta do projeto é numa unidade de rede, o gerador de perfis Olá irá pedir-lhe tooprovide Olá toosave outra localização, criação de perfis de relatórios.

 Também pode anexar a função da web tooa ligando tooWaIISHost.exe.
Se existirem vários processos de função de trabalho na sua aplicação, terá de toouse Olá processID toodistinguish-los. Pode consultar Olá processID através de programação, ao aceder ao objeto de processo Olá. Por exemplo, se adicionar este método de execução do código toohello da classe derivada de RoleEntryPoint de Olá numa função, pode examinar o registo no Olá tooknow de IU do emulador de computação que tooconnect de processo para.

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

registo de Olá tooview, início Olá IU do emulador de computação.

![Iniciar Olá IU do emulador de computação][8]

Abra a janela de consola de registo de função de trabalho de Olá na IU do emulador de computação de Olá clicando na barra de título da janela de consola Olá. Pode ver o ID do processo Olá no registo de Olá.

![ID do processo de vista][9]

Um que tenha ligado, executar passos Olá num cenário de Olá de tooreproduce de IU (se necessário) da sua aplicação.

Se pretender que a criação de perfis de toostop, escolha Olá **parar a criação de perfis** ligação.

![Parar a opção de criação de perfis][10]

## <a name="3-view-performance-reports"></a>3: ver relatórios de desempenho
relatório de desempenho de Olá para a sua aplicação é apresentado.

Neste momento, o gerador de perfis de Olá deixa de executar, guarda dados num ficheiro .vsp e apresenta um relatório que mostra uma análise de dados.

![Relatório de gerador de perfis][11]

Se vir String.wstrcpy no Olá caminho instantâneo, clique em apenas código My toochange Olá vista tooshow utilizador apenas código.  Se vir String.Concat, tente premindo Olá todo o código Mostrar botão.

Deverá ver o método Concatenate Olá e String.Concat utilizando uma grande parte do tempo de execução de Olá.

![Análise de relatório][12]

Se tiver adicionado o código de concatenação de cadeia Olá neste artigo, deverá ver um aviso no Olá lista de tarefas para esta. Também poderá ver um aviso que não há uma quantidade excessiva de recolha de lixo, que é que devem estar toohello número de cadeias que são criados e eliminado.

![Avisos de desempenho][14]

## <a name="4-make-changes-and-compare-performance"></a>4: efetuar alterações e compare o desempenho
Também pode comparar o desempenho de Olá antes e após uma alteração de código.  Parar Olá a executar o processo e editar Olá código tooreplace Olá cadeia concatenação operação com a utilização de Olá de StringBuilder:

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

Não executar outra de desempenho e, em seguida, compare o desempenho de Olá. No Explorador de desempenho Olá, se hello executa está disponíveis na Olá mesma sessão, apenas pode selecionar ambos os relatórios, abra o menu de atalho Olá e escolha **comparar o desempenho relatórios**. Se quiser toocompare com uma execução na outra sessão de desempenho, abra Olá **analisar** menu e escolha **comparar o desempenho relatórios**. Especifique ambos os ficheiros na caixa de diálogo Olá, que é apresentada.

![Comparar a opção de relatórios de desempenho][15]

relatórios de Olá realce as diferenças entre duas executa Olá.

![Relatório de comparação][16]

Parabéns! Que tiver iniciado com o gerador de perfis de Olá.

## <a name="troubleshooting"></a>Resolução de problemas
* Certifique-se de que é uma versão de lançamento de criação de perfis e iniciar sem depuração.
* Se Olá anexar/desanexar opção não estiver ativada no menu do gerador de perfis de Olá, execute Olá Assistente de desempenho.
* Utilize o Olá IU do emulador de computação tooview Olá estado da aplicação. 
* Se tiver problemas a partir de aplicações emulador Olá ou a anexar Olá gerador de perfis, encerre o emulador de computação Olá e reiniciá-lo. Se que não resolverem o problema de Olá, tente reiniciar. Este problema pode ocorrer se utilizar Olá emulador de computação toosuspend e remover implementações em execução.
* Se tiver utilizado a qualquer um dos comandos da linha de comandos de criação de perfis de Olá, especialmente Olá definições globais, certifique-se de que VSPerfClrEnv /globaloff EnableNotification for chamada e que VsPerfMon.exe ter sido encerrado.
* Se quando amostragem, verá a mensagem de saudação "PRF0025: foram recolhidos quaisquer dados," verificação Olá processo ligado atividade toohas da CPU. As aplicações que não estão a fazer qualquer trabalho computacional podem não produzir quaisquer dados de amostragem.  Também é possível que o processo de Olá terminado antes de qualquer amostragem foi efetuada. Verifique toosee que método de execução de Olá para uma função que lhe está a criação de perfis não terminar.

## <a name="next-steps"></a>Passos Seguintes
Instrumentação binários do Azure no emulador Olá não é suportado no gerador de perfis do Olá Visual Studio, mas se pretender que a atribuição de memória tootest, pode escolher essa opção quando a criação de perfis. Também pode optar por criação de perfis de simultaneidade, que ajuda a determinar se os threads são perder tempo competir pela bloqueios, ou a camada a criação de perfis de interação, que ajuda a identificar problemas de desempenho quando a interação entre camadas de uma aplicação, mais frequentemente entre a camada de dados de Olá e uma função de trabalho.  Pode ver as consultas de base de dados de Olá gera a sua aplicação e utilizar Olá a criação de perfis dados tooimprove a utilização da base de dados de Olá. Para obter informações sobre a criação de perfis de interação do escalão, consulte a mensagem de blogue de Olá [explicação passo a passo: utilizar Olá gerador de perfis de interação de camada no Visual Studio Team System 2010][3].

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
