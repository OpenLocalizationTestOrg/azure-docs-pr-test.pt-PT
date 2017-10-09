---
title: "aaaConfigure mapa de serviço no Operations Management Suite | Microsoft Docs"
description: "Mapa de serviço é uma solução de Operations Management Suite que Deteta automaticamente os componentes da aplicação no Windows e comunicação entre os serviços de Olá sistemas Linux e mapas. Este artigo fornece detalhes para implementar o mapa de serviço no seu ambiente e utilizá-la numa variedade de cenários."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: d3d66b45-9874-4aad-9c00-124734944b2e
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/18/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: 3127f4440f2886370f8ff617c405c6d70a926eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-service-map-in-operations-management-suite"></a>Configurar o mapa de serviço no Operations Management Suite
Mapa de serviço Deteta automaticamente os componentes da aplicação em sistemas Windows e Linux e mapas Olá comunicação entre os serviços. Pode utilizá-la tooview seus servidores como considerá-los – como interligados sistemas que fornecem serviços críticos. Mapa de serviço mostra as ligações entre servidores, processos e portas em qualquer arquitetura TCP ligados sem qualquer configuração necessária, que não seja a instalação de um agente.

Este artigo descreve os detalhes de Olá de configuração de agentes de mapa de serviço e a integração. Para obter informações sobre como utilizar o mapa de serviço, consulte [utilizar a solução de mapa de serviço de Olá no Operations Management Suite](operations-management-suite-service-map.md).

## <a name="dependency-agent-downloads"></a>Transferências de agente de dependência
| Ficheiro | SO | Versão | SHA-256 |
|:--|:--|:--|:--|
| [InstallDependencyAgent Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |


## <a name="connected-sources"></a>Origens ligadas
Mapa de serviço obtém os dados de Olá agente de dependência da Microsoft. Olá agente de dependência depende de Olá agente do OMS para o respetivo tooOperations ligações Management Suite. Isto significa que um servidor têm de ter Olá agente do OMS instalado e configurado o primeiro e, em seguida, Olá que pode ser instalado o agente de dependência. Olá tabela seguinte descreve as origens de Olá ligado que solução de mapa de serviço Olá suporta.

| Origem ligada | Suportado | Descrição |
|:--|:--|:--|
| Agentes do Windows | Sim | Mapa de serviço analisa e recolhe dados de computadores de agente do Windows. <br><br>Na adição toohello [agente do OMS](../log-analytics/log-analytics-windows-agents.md), necessitam de agentes do Windows hello agente de dependência da Microsoft. Consulte Olá [sistemas operativos suportados](#supported-operating-systems) para uma lista completa das versões do sistema operativo. |
| Agentes do Linux | Sim | Mapa de serviço analisa e recolhe dados de computadores de agente do Linux. <br><br>Na adição toohello [agente do OMS](../log-analytics/log-analytics-linux-agents.md), necessitam de agentes Linux Olá agente de dependência da Microsoft. Consulte Olá [sistemas operativos suportados](#supported-operating-systems) para uma lista completa das versões do sistema operativo. |
| Grupo de gestão do System Center Operations Manager | Sim | Mapa de serviço analisa e recolhe dados do Windows e Linux agentes num ligado [grupo de gestão do System Center Operations Manager](../log-analytics/log-analytics-om-agents.md). <br><br>Uma ligação direta de Olá System Center Operations Manager agente computador tooOperations Management Suite é necessário. Dados serão reencaminhados de repositório do Olá gestão grupo toohello Operations Management Suite.|
| Conta de armazenamento do Azure | Não | Mapa de serviço recolhe dados de computadores de agente, pelo que não existem dados a partir do mesmo toocollect do armazenamento do Azure. |

Mapa de serviço suporta apenas plataformas de 64 bits.

No Windows, Olá Microsoft Monitoring Agent (MMA) é utilizado pelo System Center Operations Manager e Operations Management Suite toogather e enviar dados de monitorização. (Este agente é denominado Olá agente do System Center Operations Manager, o agente do OMS, agente de análise do registo, MMA ou agente direta, consoante o contexto de Olá). System Center Operations Manager e Operations Management Suite fornecem versões diferentes fora de Olá caixa Olá MMA. Estas versões de cada relatório tooSystem Center Operations Manager, tooOperations Management Suite ou tooboth.  

No Linux, hello agente do OMS para reúne de Linux e envia dados tooOperations Management Suite de monitorização. Pode utilizar o mapa de serviço em servidores com agentes direta do OMS ou nos servidores que estão anexados tooOperations Management Suite através de grupos de gestão do System Center Operations Manager.  

Neste artigo, vamos deverá mencionar tooall agentes – se Linux ou Windows, se ligado grupo de gestão do System Center Operations Manager tooa ou diretamente tooOperations Management Suite – como Olá "Agente do OMS." Iremos utilizar o nome de implementação específico Olá do agente de Olá apenas se for necessário para o contexto.

agente de mapa de serviço Olá não transmitir quaisquer dados propriamente ditos, e não requer quaisquer alterações toofirewalls ou portas. dados de Olá no mapa de serviço é sempre transmitidos por Olá tooOperations de agente do OMS Management Suite, diretamente ou através de Olá OMS Gateway.

![Agentes de mapa de serviço](media/oms-service-map/agents.png)

Se for um cliente do System Center Operations Manager com um tooOperations ligado do grupo de gestão Management Suite:

- Se os agentes do System Center Operations Manager podem aceder Olá Internet tooconnect tooOperations Management Suite, é necessária nenhuma configuração adicional.  
- Se os agentes do System Center Operations Manager não é possível aceder ao Operations Management Suite através de Olá Internet, terá de tooconfigure Olá OMS Gateway toowork com o System Center Operations Manager.
  
Se estiver a utilizar Olá direta de agente do OMS, tem de tooconfigure Olá agente do OMS próprio tooconnect tooOperations Management Suite ou tooyour OMS Gateway. Olá OMS Gateway pode ser transferido a partir do Olá [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).

### <a name="management-packs"></a>Pacotes de gestão
Quando o mapa de serviço está ativado numa área de trabalho do Operations Management Suite, um pacote de gestão de 300 KB é enviado servidores de Windows hello tooall nessa área de trabalho. Se estiver a utilizar os agentes do System Center Operations Manager num [grupo de gestão ligado](../log-analytics/log-analytics-om-agents.md), for implementada Olá pacote de gestão de mapa de serviço do System Center Operations Manager. Se os agentes de Olá estejam diretamente ligados, o Operations Management Suite fornece o pacote de gestão de Olá.

pacote de gestão de Olá é denominado Microsoft.IntelligencePacks.ApplicationDependencyMonitor. De escrita too%Programfiles%\Microsoft monitorização Agent\Agent\Health serviço State\Management Packs\. Olá origem de dados que utiliza o pacote de gestão de Olá é % programa files%\Microsoft monitorização Agent\Agent\Health serviço State\Resources\<AutoGeneratedID > \ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.

## <a name="installation"></a>Instalação
### <a name="install-hello-dependency-agent-on-microsoft-windows"></a>Instalar o agente de dependência de Olá no Microsoft Windows
Privilégios de administrador são necessária tooinstall ou desinstale o agente de Olá.

Olá dependência agente está instalado em computadores com Windows através do InstallDependencyAgent Windows.exe. Se executar este ficheiro executável sem quaisquer opções, inicia um assistente que pode seguir tooinstall interativamente.  

Utilize Olá os seguintes passos tooinstall Olá agente de dependência em cada computador do Windows:

1.  Instalação Olá agente do OMS, utilizando instruções Olá em [toohello de computadores Windows ligar o serviço de análise de registos do Azure](../log-analytics/log-analytics-windows-agents.md).
2.  Transferir o agente do Windows hello e executá-la utilizando Olá os seguintes comandos: <br>`InstallDependencyAgent-Windows.exe`
3.  Siga o agente de Olá Olá assistente tooinstall.
4.  Se o agente de dependência de Olá falhar toostart, verifique os registos de Olá para informações de erro detalhadas. Nos agentes do Windows, o diretório de registo de Olá é %Programfiles%\Microsoft Agent\logs de dependência. 

#### <a name="windows-command-line"></a>Linha de comandos do Windows
Utilize as opções de Olá seguintes tooinstall da tabela de uma linha de comandos. toosee uma lista dos sinalizadores de instalação de Olá, execute o instalador de Olá utilizando Olá /? Sinalizador da seguinte forma.

    InstallDependencyAgent-Windows.exe /?

| Sinalizador | Descrição |
|:--|:--|
| /? | Obter uma lista de opções da linha de comandos Olá. |
| /S | Efetue uma instalação automática com sem avisos do utilizador. |

Ficheiros de Olá agente de dependência do Windows são colocados no agente de dependência C:\Program Files\Microsoft por predefinição.

### <a name="install-hello-dependency-agent-on-linux"></a>Instalar o agente de dependência de Olá no Linux
Acesso de raiz é necessária tooinstall ou configurar o agente de Olá.

Olá dependência agente está instalado em computadores com Linux através do InstallDependencyAgent-Linux64.bin, um script de shell com um binário de extração. Pode executar ficheiros Olá utilizando ostrar ou adicionar executar permissões toohello próprio ficheiro.
 
Utilize Olá os seguintes passos tooinstall Olá agente de dependência em cada computador Linux:

1.  Instalação Olá agente do OMS, utilizando instruções Olá em [recolher e gerir dados a partir de computadores com Linux](https://technet.microsoft.com/library/mt622052.aspx).
2.  Instale o agente de dependência de Linux Olá como raiz utilizando Olá os seguintes comandos:<br>`sh InstallDependencyAgent-Linux64.bin`
3.  Se o agente de dependência de Olá falhar toostart, verifique os registos de Olá para informações de erro detalhadas. Nos agentes Linux, o diretório de registo de Olá é /var/opt/microsoft/dependency-agent/log.

toosee uma lista dos sinalizadores de instalação de Olá, execute o programa de instalação de Olá com Olá - sinalizador de ajuda da seguinte forma.

    InstallDependencyAgent-Linux64.bin -help

| Sinalizador | Descrição |
|:--|:--|
| -ajudar | Obter uma lista de opções da linha de comandos Olá. |
| -s | Efetue uma instalação automática com sem avisos do utilizador. |
| -Verifique | Verifique as permissões e de sistema de operativo Olá, mas não instale o agente de Olá. |

Ficheiros de Olá agente de dependência são colocados no Olá seguintes diretórios:

| Ficheiros | Localização |
|:--|:--|
| Ficheiros de núcleo | /OPT/Microsoft/Dependency-Agent |
| Ficheiros de registo | /var/OPT/Microsoft/Dependency-Agent/log |
| Ficheiros de configuração | /etc/OPT/Microsoft/Dependency-Agent/Config |
| Ficheiros executáveis do serviço | /OPT/Microsoft/Dependency-Agent/bin/Microsoft-Dependency-Agent<br>/OPT/Microsoft/Dependency-Agent/bin/Microsoft-Dependency-Agent-Manager |
| Ficheiros de armazenamento binário | /var/OPT/Microsoft/Dependency-Agent/Storage |

## <a name="installation-script-examples"></a>Exemplos de script de instalação
tooeasily implementar Olá agente de dependência no número de servidores em simultâneo, ajuda a toouse um script. Pode utilizar Olá toodownload de exemplos de script a seguir e instalar o agente de dependência de Olá no Windows ou Linux.

### <a name="powershell-script-for-windows"></a>Script do PowerShell para Windows
```PowerShell
Invoke-WebRequest "https://aka.ms/dependencyagentwindows" -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S
```

### <a name="shell-script-for-linux"></a>Script de shell para Linux
```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
sh InstallDependencyAgent-Linux64.bin -s
```

## <a name="desired-state-configuration"></a>Configuração do Estado Pretendido
Olá toodeploy agente de dependência através da configuração de estado pretendida, pode utilizar o módulo de xPSDesiredStateConfiguration Olá e pouco de código semelhante Olá seguinte:
```
configuration ServiceMap {

Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = "C:\InstallDependencyAgent-Windows.exe"

Node localhost
{ 
    # Download and install hello Dependency Agent
    xRemoteFile DAPackage 
    {
        Uri = "https://aka.ms/dependencyagentwindows"
        DestinationPath = $DAPackageLocalPath
    }

    xPackage DA
    {
        Ensure="Present"
        Name = "Dependency Agent"
        Path = $DAPackageLocalPath
        Arguments = '/S'
        ProductId = ""
        InstalledCheckRegKey = "HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent"
        InstalledCheckRegValueName = "DisplayName"
        InstalledCheckRegValueData = "Dependency Agent"
        DependsOn = "[xRemoteFile]DAPackage"
    }
  }
}
```

## <a name="uninstallation"></a>Desinstalação
### <a name="uninstall-hello-dependency-agent-on-windows"></a>Desinstalar Olá agente de dependência no Windows
Um administrador pode desinstalar Olá dependência agente para o Windows através do painel de controlo.

Um administrador também pode executar %Programfiles%\Microsoft dependência Agent\Uninstall.exe toouninstall Olá agente de dependência.

### <a name="uninstall-hello-dependency-agent-on-linux"></a>Desinstalar Olá agente de dependência no Linux
desinstalar toocompletely Olá agente de dependência do Linux, tem de remover o próprio agente de Olá e Olá conector, que é instalado automaticamente com o agente de Olá. Pode desinstalar ambos utilizando Olá único comando a seguir:

    rpm -e dependency-agent dependency-agent-connector

## <a name="troubleshooting"></a>Resolução de problemas
Se tiver quaisquer problemas de instalação e execução de mapa de serviço, esta secção pode ajudá-lo. Se ainda não é possível resolver o problema, contacte Support da Microsoft.

### <a name="dependency-agent-installation-problems"></a>Problemas de instalação do agente de dependência
#### <a name="installer-asks-for-a-reboot"></a>Instalador pede-lhe uma reinicialização
Agente de dependência de Olá *geralmente* não requer um reinício após a instalação ou desinstalação. No entanto, em certos casos raros, Windows Server requer um toocontinue de reiniciar o computador com uma instalação. Isto acontece quando uma dependência, normalmente, Olá Microsoft Visual C++ Redistributable, requer uma reinicialização devido a um ficheiro de bloqueado.

#### <a name="message-unable-tooinstall-dependency-agent-visual-studio-runtime-libraries-failed-tooinstall-code--codenumber-appears"></a>Mensagem "não é possível tooinstall agente de dependência: bibliotecas de Runtime do Visual Studio falha tooinstall (código = [code_number])" é apresentada

Olá agente de dependência Microsoft baseia-se em bibliotecas de runtime do Microsoft Visual Studio Olá. Irá receber uma mensagem se houver um problema durante a instalação das bibliotecas de Olá. 

programas de instalação de biblioteca de tempo de execução de Olá criar registos na pasta de %LOCALAPPDATA%\temp Olá. ficheiro de Olá é dd_vcredist_arch_yyyymmddhhmmss.log, onde *arquitetura* é "x86" ou "amd64" e *yyyymmddhhmmss* é Olá data e hora (relógio de 24 horas) em que o registo de Olá foi criado. registo de Olá fornece detalhes sobre o problema de Olá que está a bloquear a instalação.

Poderá ser útil tooinstall Olá [bibliotecas de tempo de execução mais recentes](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) sozinho primeiro.

Olá tabela seguinte apresenta uma lista de números de código e resoluções sugeridas.

| Código | Descrição | Resolução |
|:--|:--|:--|
| 0x17 | Instalador de biblioteca de Olá requer uma atualização do Windows que não foi instalada. | Procure no registo de instalador de biblioteca Olá mais recente.<br><br>Se uma referência demasiado "Windows8.1-KB2999226-x64.msu" é seguido de uma linha "erro 0x80240017: pacote MSU tooexecute falhada," não tem Olá pré-requisitos tooinstall KB2999226. Siga as instruções de Olá na secção pré-requisitos Olá [Universal C tempo de execução no Windows](https://support.microsoft.com/kb/2999226). Poderá ter toorun Windows Update e reiniciar várias vezes na pré-requisitos do ordem tooinstall Olá.<br><br>Execute o instalador do agente de dependência de Microsoft Olá novamente. |

### <a name="post-installation-issues"></a>Problemas de pós-instalação
#### <a name="server-doesnt-appear-in-service-map"></a>Servidor não são apresentados no mapa de serviço
Se a instalação do agente de dependência com êxito, mas não vir o seu servidor na Olá solução de mapa de serviço:
* Olá agente de dependência é instalado com êxito? Pode validar esta verificação toosee se Olá serviço está instalado e em execução.<br><br>
**Windows**: procure serviço Olá com o nome "Microsoft Dependency agente".<br>
**Linux**: procure Olá a executar o processo de "microsoft-dependência-agent."

* Tem a no Olá [livre preços escalão do Operations Management Suite/Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)? plano gratuito Olá permite a cópia de segurança toofive exclusivos servidores de mapa de serviço. Quaisquer servidores subsequentes não serão apresentados no mapa de serviço, mesmo se Olá cinco anterior já não está a enviar dados.

* É o envio de registo do servidor e dados de desempenho tooOperations Management Suite? Aceda tooLog pesquisa e execute Olá seguinte consulta para o seu computador: 

        * Computer="<your computer name here>" | measure count() by Type
        
  Obteve uma variedade de eventos nos resultados de Olá? Dados de Olá é recente? Se Sim, o agente do OMS está a funcionar corretamente e ao comunicar com Olá serviço do Operations Management Suite. Caso contrário, verifique Olá agente do OMS no seu servidor: [resolução de problemas do agente do OMS para Windows](https://support.microsoft.com/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues) ou [agente do OMS para resolução de problemas do Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md).

#### <a name="server-appears-in-service-map-but-has-no-processes"></a>O servidor é apresentado no mapa de serviço, mas não tem nenhum processo
Se vir o seu servidor no mapa de serviço, mas tem nenhum processo ou ligação de dados, que indica que Olá dependência agente está instalado e em execução, mas não carregar controladores de kernel Olá. 

Verifique o ficheiro de C:\Program Files\Microsoft dependência Agent\logs\wrapper.log Olá (Windows) ou /var/opt/microsoft/dependency-agent/log/service.log (Linux). linhas de último Olá do ficheiro de Olá devem indicar a razão pela qual não carregar kernel Olá. Por exemplo, kernel Olá poderá não ser suportado no Linux, se atualizar o kernel.

## <a name="data-collection"></a>Recolha de dados
Pode esperar tootransmit cada agente aproximadamente 25 MB por dia, consoante complexos como as dependências de sistema são. Cada agente envia dados de dependência de mapa de serviço a cada 15 segundos.  

Olá agente de dependência normalmente consome 0.1 percentagem de memória de sistema e 0.1 percentagem de CPU do sistema.

## <a name="supported-azure-regions"></a>Regiões do Azure suportadas
Mapa de serviço está atualmente disponível na Olá seguintes regiões do Azure:
- EUA Leste
- Europa Ocidental
- EUA Centro-Oeste


## <a name="supported-operating-systems"></a>Sistemas operativos suportados
Olá secções seguintes listam os sistemas de operativos Olá suportado para Olá agente de dependência. Mapa de serviço não suporta arquiteturas de 32 bits para qualquer sistema operativo.

### <a name="windows-server"></a>Windows Server
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1

### <a name="windows-desktop"></a>Ambiente de trabalho do Windows
- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux, CentOS Linux e Oracle Linux (com o Kernel do RHEL)
- São suportadas apenas predefinido e versões de kernel do SMP Linux.
- Versões kernel não padrão, tais como PAE e Xen, não são suportados para qualquer distribuição de Linux. Por exemplo, um sistema com a cadeia de versão Olá de "2.6.16.21-0.8-xen" não é suportado.
- Kernels personalizados, incluindo recompilações de kernels padrão, não são suportadas.
- CentOSPlus kernel não é suportada.
- Oracle Unbreakable Enterprise Kernel (UEK) é abrangida numa secção posterior deste artigo.


#### <a name="red-hat-linux-7"></a>Red Hat Linux 7
| Versão do SO | Versão de kernel |
|:--|:--|
| 7.0 | 3.10.0-123 |
| 7.1 | 3.10.0-229 |
| 7.2 | 3.10.0-327 |
| 7.3 | 3.10.0-514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6
| Versão do SO | Versão de kernel |
|:--|:--|
| 6.0 | 2.6.32-71 |
| 6.1 | 2.6.32-131 |
| 6.2 | 2.6.32-220 |
| 6.3 | 2.6.32-279 |
| 6.4 | 2.6.32-358 |
| 6.5 | 2.6.32-431 |
| 6.6 | 2.6.32-504 |
| 6.7 | 2.6.32-573 |
| 6.8 | 2.6.32-642 |

#### <a name="red-hat-linux-5"></a>Red Hat Linux 5
| Versão do SO | Versão de kernel |
|:--|:--|
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398<br>2.6.18-400<br>2.6.18-402<br>2.6.18-404<br>2.6.18-406<br>2.6.18-407<br>2.6.18-408<br>2.6.18-409<br>2.6.18-410<br>2.6.18-411<br>2.6.18-412<br>2.6.18-416<br>2.6.18-417<br>2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Oracle Enterprise Linux com o Kernel Unbreakable Enterprise

#### <a name="oracle-linux-6"></a>Oracle Linux 6
| Versão do SO | Versão de kernel
|:--|:--|
| 6.2 | Oracle 2.6.32-300 (UEK R1) |
| 6.3 | Oracle 2.6.39-200 (UEK R2) |
| 6.4 | Oracle 2.6.39-400 (UEK R2) |
| 6.5 | Oracle 2.6.39-400 (UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400 (UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| Versão do SO | Versão de kernel
|:--|:--|
| 5.8 | Oracle 2.6.32-300 (UEK R1) |
| 5.9 | Oracle 2.6.39-300 (UEK R2) |
| 5.10 | Oracle 2.6.39-400 (UEK R2) |
| 5.11 | Oracle 2.6.39-400 (UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>Servidor Linux Empresarial SUSE

#### <a name="suse-linux-11"></a>SUSE Linux 11
| Versão do SO | Versão de kernel
|:--|:--|
| 11 | 2.6.27 |
| 11 SP1 | 2.6.32 |
| 11 SP2 | 3.0.13 |
| 11 SP3 | 3.0.76 |
| 11 SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10
| Versão do SO | Versão de kernel
|:--|:--|
| 10 SP4 | 2.6.16.60 |

## <a name="diagnostic-and-usage-data"></a>dados de diagnóstico e utilização
A Microsoft recolhe automaticamente dados de utilização e desempenho através da utilização do Olá serviço de mapa de serviço. A Microsoft utiliza este tooprovide de dados e melhorar a qualidade de Olá, segurança e integridade dos Olá serviço de mapa de serviço. Os dados incluem informações sobre a configuração de Olá do seu software, como o sistema operativo e versão. Também inclui endereço IP, o nome DNS e o nome da estação de trabalho na ordem tooprovide exatas e eficientes resolução de problemas capacidades. Não recolhemos nomes, moradas ou outras informações de contacto.

Para obter mais informações sobre a utilização e recolha de dados, consulte Olá [declaração de privacidade do Microsoft Online Services](https://go.microsoft.com/fwlink/?LinkId=512132).



## <a name="next-steps"></a>Passos seguintes
- Saiba como demasiado[utilizar o mapa de serviço](operations-management-suite-service-map.md) depois foi implementado e configurado.
