---
title: "alterações de aaaTrack com Log Analytics do Azure | Microsoft Docs"
description: "Olá solução de controlo de alterações no Log Analytics ajuda a identificar o software e as alterações de serviço do Windows que ocorrem no seu ambiente."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f8040d5d-3c89-4f0c-8520-751c00251cb7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2bb1938caad25101e167927200ac3ef495120fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="track-software-changes-in-your-environment-with-hello-change-tracking-solution"></a>Controlar as alterações de software no seu ambiente com Olá solução de controlo de alterações

![Símbolo de controlo de alterações](./media/log-analytics-change-tracking/change-tracking-symbol.png)

Este artigo ajuda-o a utilizar Olá solução de controlo de alterações na análise de registos tooeasily identificar as alterações no seu ambiente. solução de Olá controla tooWindows de alterações e software do Linux, os ficheiros do Windows e chaves de registo, serviços do Windows e Linux daemons. Identificar as alterações de configuração pode ajudar a identificar problemas operacionais.

Instalar o tipo de Olá Olá solução tooupdate do agente que tenha instalado. Alterações tooinstalled software, serviços do Windows e Linux daemons nos servidores de Olá monitorizada de leitura. Em seguida, Olá são enviados dados toohello serviço de análise de registos na nuvem de Olá para processamento. Lógica é aplicado toohello recebida dados e o serviço em nuvem Olá regista dados de Olá. Ao utilizar as informações de Olá no dashboard de controlo de alterações de Olá, facilmente pode ver as alterações de Olá efetuadas na sua infraestrutura de servidor.

## <a name="installing-and-configuring-hello-solution"></a>Instalar e configurar a solução de Olá
Utilize Olá tooinstall informações a seguir e configurar a solução de Olá.

* Tem de ter um [Windows](log-analytics-windows-agents.md), [do Operations Manager](log-analytics-om-agents.md), ou [Linux](log-analytics-linux-agents.md) agente em cada computador onde pretende toomonitor alterações.
* Adicionar Olá alterações solução tooyour OMS área de trabalho de Olá [do Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ChangeTrackingOMS?tab=Overview). Em alternativa, pode adicionar solução Olá utilizando informações Olá [soluções de análise de registos de adicionar de Olá soluções galeria](log-analytics-add-solutions.md). Não é necessária nenhuma configuração adicional.

### <a name="configure-linux-files-tootrack"></a>Configurar tootrack de ficheiros do Linux
Utilize Olá os seguintes passos tooconfigure ficheiros tootrack em computadores com Linux.

1. No portal do OMS Olá, clique em **definições** (symbol de engrenagem Olá).
2. No Olá **definições** página, clique em **dados**e, em seguida, clique em **controlo de ficheiro do Linux**.
3. Sob controlo de alterações do ficheiro de Linux, escreva o caminho completo de Olá, incluindo o nome de ficheiro Olá do ficheiro de Olá que pretende tootrack e, em seguida, clique em Olá **adicionar** símbolo. Por exemplo: "/etc/*.conf"
4. Clique em **Guardar**.  

> [!NOTE]
> Controlo de ficheiro de Linux tem capacidades adicionais, incluindo o controlo de diretório, recrusion através de diretórios e o caráter universal de controlo.

### <a name="configure-windows-files-tootrack"></a>Configurar tootrack de ficheiros do Windows
Utilize Olá os seguintes passos tooconfigure ficheiros tootrack em computadores Windows.

1. No portal do OMS Olá, clique em **definições** (symbol de engrenagem Olá).
2. No Olá **definições** página, clique em **dados**e, em seguida, clique em **controlo de ficheiro do Windows**.
3. Sob controlo de alterações do ficheiro de Windows, escreva o caminho completo de Olá, incluindo o nome de ficheiro Olá do ficheiro de Olá que pretende tootrack e, em seguida, clique em Olá **adicionar** símbolo. Por exemplo: C:\Program Files (x86) \Internet Explorer\iexplore.exe ou C:\Windows\System32\drivers\etc\hosts.
4. Clique em **Guardar**.  
   ![Registo de alterações do ficheiro de Windows](./media/log-analytics-change-tracking/windows-file-change-tracking.png)

### <a name="configure-windows-registry-keys-tootrack"></a>Configurar tootrack de chaves de registo do Windows
Utilize Olá os seguintes passos tooconfigure registo chaves tootrack em computadores Windows.

1. No portal do OMS Olá, clique em **definições** (symbol de engrenagem Olá).
2. No Olá **definições** página, clique em **dados**e, em seguida, clique em **controlo de registo do Windows**.
3. Sob controlo de alterações do registo de Windows, escreva chave completa de Olá que pretende tootrack e, em seguida, clique em Olá **adicionar** símbolo.
4. Clique em **Guardar**.  
   ![Registo de alterações do registo de Windows](./media/log-analytics-change-tracking/windows-registry-change-tracking.png)

### <a name="explanation-of-linux-file-collection-properties"></a>Explicação de propriedades de coleção de ficheiros do Linux
1. **Tipo**
   * **Ficheiro** (relatório de metadados do ficheiro - tamanho, data de modificação, hash, etc.)
   * **Diretório** (relatório metadados do diretório - tamanho, a data de modificação, etc.)
2. **Ligações** (symlink Linux processamento referencia tooother ficheiros ou diretórios)
   * **Ignorar** (ignorar symlinks durante recurions toonot incluem Olá ficheiros/diretórios referenciados)
   * **Siga** (siga Olá symlinks durante recursão tooalso incluem Olá ficheiros/diretórios referenciados)
   * **Gerir** (siga Olá symlinks e alterar o tratamento de Olá de conteúdo devolvido)

   > [!NOTE]   
   > Olá opção de ligações de "Gerir" não é recomendada. Obtenção de conteúdo do ficheiro não é suportada.

3. **Recurse** (Recurse através de níveis de pasta e controlar todos os ficheiros de reunião, instrução de caminho Olá)
4. **Sudo** (ativar o acesso aos ficheiros ou diretórios que necessitam de privilégios sudo)

### <a name="limitations"></a>Limitações
Olá solução de controlo de alterações não suporta atualmente Olá seguintes itens:

* Pastas (diretórios) para controlo de ficheiro do Windows
* Recursão para o ficheiro de controlo do Windows
* Os carateres universais para o controlo de ficheiro do Windows
* Variáveis de caminho
* Sistemas de ficheiros de rede
* Conteúdo do ficheiro

Outras limitações:

* Olá **tamanho de ficheiro máximo** e valores de coluna são utilizados na implementação atual Olá.
* Se recolher ficheiros mais de 2500 no ciclo de recolha de 30 minutos de Olá, o desempenho da solução pode ser degradado.
* Quando o tráfego de rede é elevado, registos de alteração poderão demorar até tooa máximo de toodisplay seis horas.
* Se modificar a configuração de Olá enquanto um computador é encerrado, o computador Olá poderá publicarmos alterações de ficheiro que pertenciam toohello de configuração anterior.

## <a name="change-tracking-data-collection-details"></a>Alterar os detalhes de recolha de dados de controlo
Registo de alterações recolhe inventário de software e os metadados de serviço do Windows utilizando os agentes de Olá que tiver ativado.

Olá tabela seguinte mostra os métodos de recolha de dados e outros detalhes sobre como os dados são recolhidos para controlo de alterações.

| Plataforma | Direcionar o agente | Agente do Operations Manager | Agente Linux | Storage do Azure | O Operations Manager necessárias? | Dados de agente do Operations Manager enviados através do grupo de gestão | Frequência de recolha |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Windows e Linux | &#8226; | &#8226; | &#8226; |  |  | &#8226; | 5 minutos too50 minutos, consoante o tipo de alteração de Olá. Consulte Olá seguinte tabela para obter mais informações. |


Olá tabela seguinte mostra a frequência de recolha de dados de Olá para tipos de Olá das alterações.

| **Altere o tipo** | **frequência** | **Does****agente****enviar as diferenças quando encontradas?**  |
| --- | --- | --- |
| Registo do Windows | minutos de 50 | Não |
| Ficheiro do Windows | 30 minutos | Sim. Se não houver nenhuma alteração no 24 horas, é enviado um instantâneo. |
| Ficheiro do Linux | 15 minutos | Sim. Se não houver nenhuma alteração no 24 horas, é enviado um instantâneo. |
| Serviços Windows | 30 minutos | Sim, a cada 30 minutos quando se encontram as alterações. A cada 24 horas um instantâneo é enviado, independentemente da alteração. Por isso, o instantâneo de Olá é enviado, mesmo que não foram efetuadas alterações. |
| Aplicações daemons do Linux | 5 minutos | Sim. Se não houver nenhuma alteração no 24 horas, é enviado um instantâneo. |
| Software do Windows | 30 minutos | Sim, a cada 30 minutos quando se encontram as alterações. A cada 24 horas um instantâneo é enviado, independentemente da alteração. Por isso, o instantâneo de Olá é enviado, mesmo que não foram efetuadas alterações. |
| Software do Linux | 5 minutos | Sim. Se não houver nenhuma alteração no 24 horas, é enviado um instantâneo. |

### <a name="registry-key-change-tracking"></a>Alteração de chave de registo de controlo

Análise de registos efetua o registo do Windows, monitorização e controlo com Olá solução de controlo de alterações. objetivo de Olá de monitorização de alterações tooregistry chaves é pontos de extensibilidade toopinpoint onde podem ativar o código de terceiros e de software maligno. seguinte Olá lista mostra Olá predefinido as chaves de registo que são controlados pela solução de Olá e por que motivo cada é controlada.

- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Startup
    - Scripts de monitores que são executados no arranque.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Shutdown
    - Scripts de monitores que são executados no encerramento.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Run
    - Monitoriza as chaves que são carregadas antes Olá utilizador iniciar sessão no tootheir conta do Windows. chave de Olá é utilizada para programas de 32 bits em execução nos computadores de 64 bits.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Active Setup\Installed componentes
    - Monitores alterações tooapplication definições.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\ShellEx\ContextMenuHandlers
    - Monitores comuns autostart entradas que ligue diretamente no Explorador do Windows e, normalmente, execução no processo com Explorer.exe.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\Shellex\CopyHookHandlers
    - Monitores comuns autostart entradas que ligue diretamente no Explorador do Windows e, normalmente, execução no processo com Explorer.exe.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\Background\ShellEx\ContextMenuHandlers
    - Monitores comuns autostart entradas que ligue diretamente no Explorador do Windows e, normalmente, execução no processo com Explorer.exe.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - Monitores para o ícone de sobreposição de registo do processador.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - Monitores para o ícone de sobreposição de registo de processador para programas de 32 bits em execução nos computadores de 64 bits.
- HKEY\_LOCAL\_objetos de programa auxiliar de MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\Browser
    - Monitores para o novo browser auxiliar objeto plug-ins para o Internet Explorer. Utilizado tooaccess Olá documento Object Model (DOM) de navegação de página e toocontrol atual no Olá.
- HKEY\_LOCAL\_objetos de programa auxiliar de MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\Browser
    - Monitores para o novo browser auxiliar objeto plug-ins para o Internet Explorer. Utilizado tooaccess Olá documento Object Model (DOM) de Olá atual página e toocontrol navegação para programas de 32 bits em execução nos computadores de 64 bits.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Internet Explorer\Extensions
    - Monitores para novas extensões de Internet Explorer, tais como menus de ferramenta personalizada e botões da barra de ferramentas personalizadas.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Internet Explorer\Extensions
    - Monitores para novas extensões de Internet Explorer, tais como menus de ferramenta personalizada e botões da barra de ferramentas personalizadas para os programas de 32 bits em execução nos computadores de 64 bits.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    - Monitoriza os controladores de 32 bits de Olá associados wavemapper, wave1 e wave2, msacm.imaadpcm, .msadpcm, .msgsm610 e vidc. Secção toohello [controladores] semelhante no Olá sistema. Ficheiro INI.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    - Controladores de 32 bits de Olá monitores associados wavemapper, wave1 e wave2, msacm.imaadpcm, .msadpcm, .msgsm610 e vidc para programas de 32 bits em execução nos computadores de 64 bits. Secção toohello [controladores] semelhante no Olá sistema. Ficheiro INI.
- HKEY\_LOCAL\_MACHINE\System\CurrentControlSet\Control\Session Manager\KnownDlls
    - Monitores Olá lista do sistema conhecido ou frequentemente utilizada DLLs; Este sistema impede que pessoas explorá permissões do diretório de aplicação fracos, arrastando em versões de Trojan horse de DLLs do sistema.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify
    - Lista de Olá de monitores de notificações de eventos de tooreceive capaz de pacotes do Winlogon, o modelo de suporte de início de sessão interativo Olá para sistema de operativo do Windows hello.


## <a name="use-change-tracking"></a>Utilizar o registo de alterações
Depois de solução Olá estiver instalada, pode ver resumo de Olá de alterações para os servidores monitorizados utilizando Olá **alterações** mosaico Olá **descrição geral** página no OMS.

![imagem de controlo de alterações mosaico](./media/log-analytics-change-tracking/change-tracking-tile.png)

Pode ver a infraestrutura de tooyour de alterações e, em seguida, desagregue para detalhes de Olá seguintes categorias:

* Alterações por tipo de configuração para o software e serviços do Windows
* Alterações de software tooapplications e atualizações para servidores individuais
* Número total de alterações de software para cada aplicação
* Pacotes de Linux
* Alterações de serviço do Windows para servidores individuais
* Alterações do Linux daemon

![imagem do dashboard do controlo de alterações](./media/log-analytics-change-tracking/change-tracking-dash01.png)

![imagem do dashboard do controlo de alterações](./media/log-analytics-change-tracking/change-tracking-dash02.png)

### <a name="tooview-changes-for-any-change-type"></a>alterações de tooview para qualquer alterar tipo
1. No Olá **descrição geral** página, clique em Olá **alterações** mosaico.
2. No Olá **Alterar controlo** dashboard, reveja as informações de resumo de Olá dos painéis de tipo de alteração de Olá e, em seguida, clique numa tooview informações detalhadas sobre-lo no Olá **pesquisa registo** página.
3. Em qualquer uma das páginas de pesquisa de registo Olá, pode ver os resultados por tempo, os resultados detalhados e o histórico de pesquisa de registo. Também pode filtrar por resultados de Olá facetas toonarrow.

## <a name="next-steps"></a>Passos seguintes
* Utilize [pesquisas de registo na análise de registos](log-analytics-log-searches.md) tooview detalhadas alterações de dados.
