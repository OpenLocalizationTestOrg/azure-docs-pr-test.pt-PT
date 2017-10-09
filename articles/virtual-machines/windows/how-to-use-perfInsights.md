---
title: aaaHow toouse PerfInsights no Microsoft Azure | Microsoft Docs
description: Aprende como problemas de desempenho do toouse PerfInsights tootroubleshoot VM do Windows.
services: virtual-machines-windows'
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: genli
ms.openlocfilehash: f23ff7708c0c63bd02674b1bdc07753e8a89d9be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-perfinsights"></a>Como toouse PerfInsights 

[PerfInsights](http://aka.ms/perfinsightsdownload) é um script automatizado que recolhe informações de diagnóstico úteis, executa cargas de esforço de e/s e fornece um toohelp de relatório de análise resolver problemas de desempenho da VM do Windows no Microsoft Azure. 

Recomendamos que execute este script antes de abrir um pedido de suporte com a Microsoft para problemas de desempenho da VM.

## <a name="supported-troubleshooting-scenarios"></a>Suportado cenários de resolução de problemas

PerfInsights pode recolher e analisar vários tipos de informações que são agrupados em cenários exclusivos.

### <a name="collect-disk-configuration"></a>Recolher configuração de disco 

Este cenário recolhe a configuração do disco Olá e outras informações importantes, incluindo Olá seguintes itens:

-   Registos de eventos

-   Estado da rede para todas as ligações de entrada e saídas

-   Definições de configuração de rede e de firewall

-   Lista de todas as aplicações que estão atualmente em execução no sistema de Olá tarefas

-   Ficheiro de informações criado pela msinfo32 Olá máquina de virtual (VM)

-   Definições de configuração de base de dados Microsoft SQL Server (se Olá VM é identificado como um servidor que está a executar o SQL Server)

-   Contadores de fiabilidade de armazenamento

-   Correções importantes do Windows

-   Controladores de filtro instalado

Esta é uma coleção de informações que não devem afetar sistema Olá passiva. 

>[!Note]
>Este cenário é automaticamente incluído em cada um dos seguintes cenários de Olá.

### <a name="benchmarkstorage-performance-test"></a>Teste de desempenho do benchmark/armazenamento

Este cenário é executado Olá [diskspd](https://github.com/Microsoft/diskspd) passa por referenciar teste (IOPS e MBPS) para todas as unidades que estejam anexados toohello VM. 

> [!Note]
> Este cenário pode afetar o sistema de Olá e não deve ser executado num sistema de produção em direto. Se necessário, execute este cenário num tooavoid de janela de manutenção dedicada quaisquer problemas. Maior carga de trabalho que é causada por um teste de rastreio ou benchmark negativamente pode afetar o desempenho de Olá da sua VM.
>

### <a name="general-vm-slow-analysis"></a>Análise de geral VM lenta 

Este cenário é executado um [contador de desempenho](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) rastreio utilizando contadores Olá especificadas no ficheiro de Generalcounters.txt Olá. Se hello VM for identificada como um servidor que está a executar o SQL Server, é executado um rastreio de contador de desempenho utilizando contadores Olá que se encontram no ficheiro de Sqlcounters.txt Olá. Também inclui dados de diagnóstico de desempenho.

### <a name="vm-slow-analysis-and-benchmark"></a>Análise de VM lenta e benchmark

Este cenário é executado um [contador de desempenho](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) rastreio que é seguido um [diskspd](https://github.com/Microsoft/diskspd) teste benchmark. 

> [!Note]
> Este cenário pode afetar o sistema de Olá e não deve ser executado num sistema de produção em direto. Se necessário, execute este cenário num tooavoid de janela de manutenção dedicada quaisquer problemas. Maior carga de trabalho que é causada por um teste de rastreio ou benchmark negativamente pode afetar o desempenho de Olá da sua VM.
>

### <a name="azure-files-analysis"></a>Análise de ficheiros do Azure 

Este cenário é executada uma captura de contador de desempenho especial, juntamente com um rastreio de rede. A captura inclui todos os contadores de "Partilhas de cliente SMB" Olá. Olá, são alguns chaves SMB cliente partilha contadores de desempenho que fazem parte da captura Olá:

| **Tipo**     | **Contador de partilhas de cliente do SMB** |
|--------------|-------------------------------|
| IOPS         | Pedidos de dados/seg             |
|              | Pedidos de leitura/seg             |
|              | Escrever pedidos/seg            |
| Latência      | Média de pedidos de dados/seg         |
|              | Média de seg/leitura                 |
|              | Média de seg/escrita                |
| Tamanho de e/s      | Média Pedido de bytes/dados       |
|              | Média Bytes/leitura               |
|              | Média Bytes/escrita              |
| Débito   | Bytes de dados/seg                |
|              | Bytes lidos/seg                |
|              | Escrever Bytes/seg               |
| Comprimento da fila | Média Comprimento da fila de leitura        |
|              | Média Comprimento da fila de escrita       |
|              | Média Comprimento da fila de dados        |

### <a name="custom-configuration"></a>Configuração personalizada 

Quando executa uma configuração personalizada, estiver a executar todos os rastreios (diagnóstico de desempenho, contador de desempenho, xperf, rede, storport) em paralelo, dependendo de quantos rastreios diferentes estão selecionados. O rastreio esteja concluída, a ferramenta de Olá é executada benchmark de diskspd Olá, se estiver selecionada. 

> [!Note]
> Este cenário pode afetar o sistema de Olá e não deve ser executado num sistema de produção em direto. Se necessário, execute este cenário num tooavoid de janela de manutenção dedicada quaisquer problemas. Maior carga de trabalho que é causada por um teste de rastreio ou benchmark negativamente pode afetar o desempenho de Olá da sua VM.
>

## <a name="what-kind-of-information-is-collected-by-hello-script"></a>Que tipo de informações recolhido pelo script de Olá?

Configuração de conjuntos de informações sobre a VM do Windows, discos ou o armazenamento, os contadores de desempenho, os registos e vários rastreios são recolhidos dependendo do cenário de desempenho de Olá utilizado:

|Dados recolhidos                              |  |  | Cenários de desempenho |  |  | |
|----------------------------------|----------------------------|------------------------------------|--------------------------|--------------------------------|----------------------|----------------------|
|                              | Recolher configuração do disco | Teste de desempenho do benchmark/armazenamento | Análise de geral VM lenta | Análise de VM lenta e benchmark | Análise de ficheiros do Azure | Configuração personalizada |
| Informações de registos de eventos      | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Informações do sistema               | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Mapa de volume                       | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Mapa de disco                         | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Tarefas em execução                    | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Contadores de fiabilidade de armazenamento     | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Informações de armazenamento              | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Saída de fsutil                    | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Informações do controlador de filtro               | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Netstat saída                   | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Configuração da rede            | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Configuração da firewall           | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Configuração do SQL Server         | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Os rastreios de diagnóstico de desempenho * |                            |                                    | Sim                      |                                |                      | Sim                  |
| O contador de desempenho rastreio * *     |                            |                                    |                          |                                |                      | Sim                  |
| O contador SMB rastreio * *             |                            |                                    |                          |                                | Sim                  |                      |
| Contador do SQL Server rastreio * *      |                            |                                    |                          |                                |                      | Sim                  |
| Rastreio XPerf                      |                            |                                    |                          |                                |                      | Sim                  |
| Rastreio StorPort                   |                            |                                    |                          |                                |                      | Sim                  |
| Rastreio de rede                    |                            |                                    |                          |                                | Sim                  | Sim                  |
| Rastreio de Diskspd Benchmark ***      |                            | Sim                                |                          | Sim                            |                      |                      |
|       |                            |                         |                                                   |                      |                      |

### <a name="performance-diagnostics-trace-"></a>Rastreio de diagnóstico de desempenho (*)

Executa um motor baseado na regra em dados de toocollect Olá em segundo plano e diagnosticar problemas de desempenho em curso. Olá seguintes regras é atualmente suportada:

- Regra de HighCpuUsage: Deteta períodos de utilização elevados da CPU e mostra os consumidores de utilização de CPU superiores Olá durante os períodos.
- Regra de HighDiskUsage: Deteta períodos de utilização elevada de disco em discos físicos e mostra os consumidores de utilização de disco superior Olá durante os períodos.
- Regra de HighResolutionDiskMetric: mostra IOPS, débito e métricas de latência de e/s por 50 milissegundos para cada disco físico. Ajuda a tooquickly identificar períodos de limitação de disco.
- Regra de HighMemoryUsage: Deteta períodos de utilização elevada da memória e mostra os consumidores de utilização de memória superior Olá durante os períodos.

> [!NOTE] 
> Atualmente, são suportadas versões do Windows que inclua Olá .NET Framework 3.5 ou versões posteriores.

### <a name="performance-counter-trace-"></a>Rastreio de contador de desempenho (*)

Recolhe os seguintes contadores de desempenho de Olá:

- \Process \Processor, \Memory, \Thread, \PhysicalDisk, \LogicalDisk
- \Cache\Dirty páginas, \Cache\Lazy escrita esvaziamentos/seg, \Server\Pool na memória não paginável, falhas, falhas de \Server\Pool bloco paginado
- Selecionar contadores em \Network Interface, \IPv4\Datagrams \IPv6\Datagrams, \TCPv4\Segments, \TCPv6\Segments, \Network adaptador, \WFPv4\Packets, \WFPv6\Packets, \UDPv4\Datagrams, \UDPv6\Datagrams, \TCPv4\Connection, \TCPv6\Connection, \ QoS Policy\Packets, \Per processador rede Interface Card atividade, \Microsoft Winsock BSP de rede

#### <a name="for-sql-server-instances"></a>Para instâncias do SQL Server
- Gestor de servidor: memória intermédia \SQL, estatísticas de agrupamento \SQLServer:Resource, \SQLServer:SQL Statistics\
- \SQLServer:Locks, \SQLServer:General, estatísticas
- Métodos de \SQLServer:Access

#### <a name="for-azure-files"></a>Para ficheiros do Azure
Partilhas de cliente \SMB

### <a name="diskspd-benchmark-trace-"></a>Rastreio de Diskspd Benchmark (*)
Testes de carga de trabalho de e/s Diskspd [disco do SO (escrita) e unidades de agrupamento (leitura/escrita)]

## <a name="run-hello-perfinsights-on-your-vm"></a>Executar Olá PerfInsights na VM

### <a name="what-do-i-have-tooknow-before-i-run-hello-script"></a>O que é necessário tooknow antes de executar o script de Olá? 

**Requisitos de script**

1.  Este script tem de ser executado no Olá VM que possui um problema de desempenho Olá. 

2.  Olá sos seguintes são suportados: Windows Server 2008 R2, 2012, 2012 R2, 2016; Windows 8.1 e Windows 10.

**Possíveis problemas ao executar o script de Olá em produção VMs:**

1.  script de Olá poderá afetar negativamente desempenho Olá de Olá VM quando é utilizado em conjunto com o cenário de "Benchmark" ou "Personalizada" Olá que é configurado utilizando XPerf ou DiskSpd. Tenha cuidado quando executar o script de Olá num ambiente de produção.

2.  Quando utiliza o script de Olá, juntamente com o cenário de "Benchmark" ou "Personalizada" Olá que é configurado utilizando DiskSpd, certifique-se de que nenhuma outra atividade em segundo plano interfere com carga de trabalho de e/s de Olá em discos de Olá testado.

3.  Por predefinição, o script de Olá utiliza dados de toocollect de unidade de armazenamento temporário de Olá. Se rastreio permanece ativada durante mais tempo, a quantidade de Olá de dados que são recolhidos pode ser relevante. Isto pode reduzir a disponibilidade de Olá de espaço em disco temporário Olá, afetar, por conseguinte, qualquer aplicação que se baseie nesta unidade.

### <a name="how-do-i-run-perfinsights"></a>Como posso executar PerfInsights? 

toorun Olá script, siga estes passos:

1. Transferir [PerfInsights.zip](http://aka.ms/perfinsightsdownload).

2. Ficheiro de PerfInsights.zip Olá de desbloqueio. toodo, o ficheiro de PerfInsights.zip Olá de contexto, selecione **propriedades**. No Olá **geral** separador, selecione **desbloqueio** e, em seguida, selecione **OK**. Esta ação irá garantir que o script de Olá é executado sem avisos adicionais de segurança.  

    ![Desbloquear o ficheiro zip Olá](media/how-to-use-perfInsights/unlock-file.png)

3.  Expanda Olá comprimido PerfInsights.zip ficheiro para a unidade temporária (por predefinição, normalmente, a unidade de Olá D). Olá ficheiro comprimido deve conter os seguintes Olá ficheiros e pastas:

    ![ficheiros na pasta de zip Olá](media/how-to-use-perfInsights/file-folder.png)

4.  Abra o Windows PowerShell como administrador e, em seguida, execute o script de PerfInsights.ps1 Olá.

    ```
    cd <hello path of PerfInsights folder >
    Powershell.exe -ExecutionPolicy UnRestricted -NoProfile -File .\\PerfInsights.ps1
    ```

    Poderá ter tooenter "y" tooif que é mais frequentes tooconfirm que pretende que a política de execução de Olá toochange.

    Na caixa de diálogo de exclusão de responsabilidade Olá, é-lhe dada Olá opção tooshare informações de diagnóstico com Support da Microsoft. Também terá de consentir toocontinue de contrato de licença toohello. Faça as suas seleções e, em seguida, clique em **executar Script**.

    ![Caixa de exclusão de responsabilidade](media/how-to-use-perfInsights/disclaimer.png)

5.  Submeta o número de cenários de Olá, se estiver disponível, ao executar o script de Olá (trata-se para a nossa estatísticas). Em seguida, clique em **OK**.
    
    ![Introduza o ID de suporte](media/how-to-use-perfInsights/enter-support-number.png)

6.  Selecione a unidade de armazenamento temporário. Olá Script pode deteção automática letra de unidade de Olá da unidade de Olá. Se ocorrerem problemas nesta fase, poderá ser pedido que a unidade de Olá tooselect (unidade predefinida do Olá é D). Registos gerados são armazenados aqui no registo de Olá\_pasta de coleção. Depois de introduzir ou aceitar a letra de unidade de Olá, clique em **OK**.

    ![Introduza a unidade](media/how-to-use-perfInsights/enter-drive.png)

7.  Selecione um cenário de resolução de problemas Olá lista fornecida.

       ![Selecione os cenários de suporte](media/how-to-use-perfInsights/select-scenarios.png)

8.  Também pode executar PerfInsights sem a IU.

    seguinte Olá comando executa Olá "Geral VM lenta Analysis Services" cenário sem uma linha de comandos de IU de resolução de problemas ou a captura de dados para 30 segundos. Pede-lhe tooconsent toohello mesmo exclusão de responsabilidade e EULA mencionados no passo 4.

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30"

    Se pretender PerfInsights toorun no modo silencioso, utilize o **- AcceptDisclaimerAndShareDiagnostics** parâmetro. Por exemplo, utilize Olá os seguintes comandos:

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30 -AcceptDisclaimerAndShareDiagnostics"

### <a name="how-do-i-troubleshoot-issues-while-running-hello-script"></a>Como posso resolver problemas ao executar o script Olá?

Se o script de Olá termina anormalmente, é possível limpar estado inconsistente ao executar script de Olá em conjunto com Olá - comutador de limpeza, da seguinte forma:

    powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -Cleanup"

Se ocorrerem problemas durante a deteção automática de Olá de unidade temporária Olá, poderá ser pedido que a unidade de Olá tooselect (unidade predefinida do Olá é D).

![unidade introduza](media/how-to-use-perfInsights/enter-drive.png)

script de Olá desinstala ferramentas Olá e remove pastas temporárias.

### <a name="troubleshooting-other-script-issues"></a>Resolução de problemas de outros problemas de script 

Se ocorrerem problemas ao executar o script de Olá, prima Ctrl + C a execução do script toointerrupt Olá. objetos temporários tooremove, consulte a secção de "Limpar após a terminação anormal" Olá.

Se continuar a falha de script tooexperience, mesmo após várias tentativas, recomendamos que execute o script de Olá no "modo de depuração" utilizando Olá "-Debug" opção de parâmetro no arranque.

Após a falha de Olá ocorre cópia Olá saída completa da consola do PowerShell Olá e envie-o agente do toohello Support da Microsoft que está a prestar assistência, o toohelp resolver o problema de Olá.

### <a name="how-do-i-run-hello-script-in-custom-configuration-mode"></a>Como executar o script de Olá no modo de configuração personalizado?

Ao selecionar Olá **personalizada** configuração, pode ativar várias rastreios em paralelo (utilize Shift toomulti-selecione):

![Selecione cenários](media/how-to-use-perfInsights/select-scenario.png)

Quando seleciona o diagnóstico de desempenho de Olá, rastreio de contador de desempenho, XPerf rastreio, rastreio da rede ou Storport rastreio cenários, siga as instruções de Olá nas caixas de diálogo Olá e tente problema de desempenho lento do tooreproduce Olá depois de iniciar os rastreios de Olá.

Olá seguintes da caixa de diálogo permite-lhe iniciar um rastreio:

![rastreio de início](media/how-to-use-perfInsights/start-trace-message.png)

toostop rastreios de Olá, terá de comando de Olá tooconfirm numa segunda caixa de diálogo.

![Stop-rastreio](media/how-to-use-perfInsights/stop-trace-message.png)
![stop-rastreio](media/how-to-use-perfInsights/ok-trace-message.png)

Quando Olá rastreios ou operações são concluídas, é gerado um novo ficheiro na d:\\registo\_coleção (ou unidade temporária Olá) com o nome **CollectedData\_aaaa-MM-dd\_hh\_mm \_ss.zip.** Pode enviar este agente de suporte do ficheiro toohello para análise.

## <a name="review-hello-diagnostics-report-created-by-perfinsights"></a>Reveja relatório de diagnóstico de Olá criado pelo PerfInsights

Dentro do Olá **CollectedData\_aaaa-MM-dd\_hh\_mm\_ss.zip ficheiro,** que é gerado pelo PerfInsights, pode encontrar um relatório HTML que explica em detalhe findings Olá de PerfInsights. tooreview Olá relatório, expanda Olá **CollectedData\_aaaa-MM-dd\_hh\_mm\_ss.zip** de ficheiros e, em seguida, abra Olá **PerfInsights Report.html**ficheiro.

Selecione Olá **Findings** separador.

![localizar separador](media/how-to-use-perfInsights/findingtab.png)

**Notas**

-   Mensagens vermelho são conhecidas problemas de configuração que podem causar problemas de desempenho.

-   As mensagens no amarelo são avisos que representam não ideal configurações que não necessariamente a causar problemas de desempenho.

-   As mensagens azul são apenas as instruções informativos.

Olá revisão ligações HTTP para todas as mensagens de erro tooget vermelho mais informações detalhadas sobre findings Olá e como pode afetar o desempenho de Olá ou melhores práticas para configurações de desempenho optimizado.

### <a name="disk-configuration-tab"></a>Separador de configuração do disco

Olá **descrição geral** secção apresenta vistas diferentes da configuração de armazenamento de Olá, incluindo informações de Diskpart e espaços de armazenamento

Olá **DiskMap** e **VolumeMap** secções descrevem numa perspetiva dupla lógica como volumes e discos físicos estão relacionado tooeach outro.

No Olá PhysicalDisk perspetiva (DiskMap), a tabela de Olá mostra todos os volumes lógicos que estão em execução no disco Olá. No seguinte exemplo de Olá, PhysicalDrive2 executa 2 Volumes lógica criados em várias partições (J e H):

![separador de dados](media/how-to-use-perfInsights/disktab.png)

No Olá perspetiva de Volume (*VolumeMap*), tabelas Olá mostram todos os discos físicos Olá em cada volume lógico. Tenha em atenção que para discos RAID/dinâmico, poderá executar a um volume lógico após vários discos físicos. No seguinte exemplo de Olá *c:\\montar* é uma pontodemontagem configurada como *SpannedDisk* no PhysicalDisks \#2 e \#3:

![separador de volume](media/how-to-use-perfInsights/volumetab.png)

### <a name="sql-server-tab"></a>Separador do SQL Server

Se o destino de Olá VM aloja quaisquer instâncias do SQL Server, verá um separador adicional no relatório de Olá denominado **do SQL Server**:

![separador de SQL](media/how-to-use-perfInsights/sqltab.png)

Esta secção contém uma descrição "geral" e separadores sub adicionais para cada uma das instâncias do SQL Server Olá alojadas no Olá VM.

Olá secção "Descrição geral" contém uma tabela útil que resume a todos os Olá discos físicos (discos de dados e do sistema) que estão em execução e que contenham uma mistura de ficheiros de dados e ficheiros de registo de transações.

No seguinte exemplo, de Olá *PhysicalDrive0* (em execução unidade Olá C) é apresentado porque ambos Olá *modeldev* e *modellog* ficheiros estão localizados na unidade de Olá C, e são de diferentes tipos (por exemplo, o ficheiro de dados e registo de transações, respetivamente):

![LogInfo](media/how-to-use-perfInsights/loginfo.png)

separadores de específico da instância do SQL Server Olá contenham uma secção geral que apresenta informações básicas sobre a instância selecionada Olá e as secções adicionais para as informações avançadas, incluindo opções de utilizador, as configurações e definições.

## <a name="references-toohello-external-tools-used"></a>Referencia ferramentas externas toohello utilizadas

### <a name="diskspd"></a>Diskspd

O DISKSPD é um armazenamento de carga e o desempenho do gerador de ferramenta de teste das equipas de engenharia do Windows Server e do Windows infraestrutura de servidor de nuvem Olá. Para obter mais informações, consulte [Diskspd](https://github.com/Microsoft/diskspd).

### <a name="xperf"></a>XPerf

XPerf é rastreios de toocapture uma ferramenta da linha de comandos de Olá Kit de ferramentas de desempenho do Windows.

Para obter mais informações, consulte [Toolkit de desempenho do Windows – Xperf](https://blogs.msdn.microsoft.com/ntdebugging/2008/04/03/windows-performance-toolkit-xperf/).

## <a name="next-steps"></a>Passos Seguintes

### <a name="upload-diagnostics-logs-and-reports-toomicrosoft-support-for-further-review"></a>Carregar os registos de diagnóstico e relatórios tooMicrosoft suporte para uma revisão mais aprofundada

Quando trabalha com Olá pessoal Support da Microsoft, pode ser resultado de Olá tootransmit solicitado que é gerado pelo PerfInsights tooassist Olá processo de resolução de problemas.

agente de suporte de Olá irá criar uma área de trabalho DTM para si e receberá uma mensagem de e-mail que inclua um toohello de ligação [DTM portal (https://filetransfer.support.microsoft.com/EFTClient/Account/Login.htm) e um ID de utilizador exclusivo e uma palavra-passe.

Esta mensagem será enviada **CTS automatizada diagnóstico serviços** (ctsadiag@microsoft.com).

![Exemplo de mensagem de saudação](media/how-to-use-perfInsights/supportemail.png)

Para segurança adicional, será necessário toochange a palavra-passe no primeiro utilizar.

Depois de iniciar sessão no tooDTM, encontrará um Olá de tooupload de caixa de diálogo **CollectedData\_aaaa-MM-dd\_hh\_mm\_ss.zip** ficheiro que foi recolhido por PerfInsights.
