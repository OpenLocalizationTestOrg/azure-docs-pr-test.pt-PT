---
title: "aaaMonitoring uma VM com Linux com uma extensão VM | Microsoft Docs"
description: "Saiba como toouse Olá desempenho de Olá toomonitor de extensão de diagnóstico de Linux e os dados de diagnóstico de uma VM com Linux no Azure."
services: virtual-machines-linux
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f54a11c5-5a0e-40ff-af6c-e60bd464058b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: Ning
ms.openlocfilehash: cf7bfebca8c0367941f7a975417f60fe2e2dab25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-linux-diagnostic-extension-toomonitor-hello-performance-and-diagnostic-data-of-a-linux-vm"></a>Utilize o desempenho do Olá extensão de diagnóstico do Linux toomonitor Olá e dados de diagnóstico de uma VM com Linux

Este documento descreve a versão 2.3 de Olá extensão de diagnóstico do Linux.

> [!IMPORTANT]
> Esta versão foi preterido e poderá ser anulada qualquer altura após 30 de Junho de 2018. Foi substituído por versão 3.0. Para obter mais informações, consulte Olá [documentação para a versão 3.0 das Olá extensão de diagnóstico do Linux](../diagnostic-extension.md).

## <a name="introduction"></a>Introdução

(**Nota**: Olá extensão de diagnóstico do Linux é obtido aberta no [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) onde informações mais recentes do Olá numa extensão de Olá são publicadas pela primeira vez. É aconselhável toocheck Olá [página do GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) primeiro.)

Olá extensão de diagnóstico do Linux ajuda um Olá de monitor de utilizador VMs do Linux que estão em execução no Microsoft Azure. Tem Olá seguintes capacidades:

* Recolhe e carrega as informações de desempenho do sistema de Olá da tabela de armazenamento Olá VM com Linux toohello utilizador, incluindo informações de diagnóstico e de syslog.
* Permite que os utilizadores toocustomize Olá dados as métricas que serão recolhidas e carregadas.
* Permite que os utilizadores tooupload especificado ficheiros tooa armazenamento designado tabela de registo de.

Na versão atual do Olá 2.3, os dados de Olá incluem:

* Todos os registos de Linux Rsyslog, incluindo o sistema, segurança e os registos de aplicações.
* Todos os dados de sistema que estão especificados na [site de soluções de plataforma cruzada do System Center Olá](https://scx.codeplex.com/wikipage?title=xplatproviders).
* Ficheiros de registo especificado de um utilizador.

Esta extensão funciona com Olá clássico e modelos de implementação do Resource Manager.

### <a name="current-version-of-hello-extension-and-deprecation-of-old-versions"></a>Versão atual do descontinuação de versões antigas e a extensão de Olá

Olá a versão mais recente da extensão de Olá **2.3**, e **quaisquer versões antigas (2.0, 2.1 e 2.2) serão preteridos e não publicados pela extremidade deste ano (2017)**. Se instalou Olá extensão de diagnóstico do Linux com a atualização de versões de secundárias automática desativada, é vivamente recomendado que desinstalar a extensão de Olá e reinstalá-la com a atualização de versões de secundárias automática ativada. Em clássicas (ASM) VMs, pode conseguir isto, especificando '2.*' como versão de Olá, se estiver a instalar extensão Olá através da CLI XPLAT do Azure ou do Powershell. Em VMs do ARM, pode conseguir isto, incluindo ' "autoUpgradeMinorVersion": true' no modelo de implementação de VM Olá. Além disso, qualquer nova instalação da extensão de Olá deve ter Olá automaticamente as versões secundárias atualizar opção ativada.

## <a name="enable-hello-extension"></a>Ativar a extensão de Olá

Pode ativar esta extensão utilizando Olá [portal do Azure](https://portal.azure.com/#), Azure PowerShell ou scripts da CLI do Azure.

tooview sistema Olá e configurar dados de desempenho diretamente do Olá portal do Azure, siga [estes passos no blogue do Azure de Olá](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).

Este artigo incida no como tooenable e configurar a extensão de Olá através da utilização de comandos da CLI do Azure. Isto permite-lhe tooread e ver dados Olá diretamente a partir da tabela de armazenamento Olá.

Tenha em atenção que os métodos de configuração de Olá que são descritos aqui não irão funcionar em Olá portal do Azure. tooview e configurar dados de sistema e o desempenho de Olá diretamente a partir do portal do Azure de Olá, a extensão de Olá tem de ser ativada através do portal Olá.

## <a name="prerequisites"></a>Pré-requisitos

* **Agente Linux do Azure versão 2.0.6 ou posterior**.

  Tenha em atenção que a maioria das imagens de galeria do Azure VM Linux incluem a versão 2.0.6 ou posterior. Pode executar **WAAgent-versão** tooconfirm qual é a versão está instalada no Olá VM. Se executar uma versão anterior ao 2.0.6 Olá VM, pode seguir [estas instruções no GitHub](https://github.com/Azure/WALinuxAgent "instruções") tooupdate-lo.
* **CLI do Azure**. Siga [este orientações para instalar a CLI](../../../cli-install-nodejs.md) tooset segurança ambiente da CLI do Azure de Olá no seu computador. Após instalar a CLI do Azure, pode utilizar Olá **azure** comando da sua interface de linha de comandos (Bash, Terminal ou linha de comandos) tooaccess Olá CLI do Azure comandos. Por exemplo:

  * Executar **conjunto de extensão de vm do azure – ajuda** para obter informações de ajuda detalhada.
  * Executar **início de sessão do azure** toosign no tooAzure.
  * Executar **vm do azure lista** toolist Olá todas as máquinas virtuais que possuem no Azure.
* Um dados Olá toostore conta de armazenamento. É necessário um nome de conta de armazenamento que foi criado anteriormente e um chave tooupload Olá dados tooyour o armazenamento acesso.

## <a name="use-hello-azure-cli-command-tooenable-hello-linux-diagnostic-extension"></a>Utilizar Olá do Olá CLI do Azure comando tooenable extensão de diagnóstico do Linux

### <a name="scenario-1-enable-hello-extension-with-hello-default-data-set"></a>Cenário 1. Ativar a extensão de Olá com o conjunto de dados do Olá predefinido

Na versão 2.3 ou posterior, os dados de predefinição de Olá que serão recolhidos incluem:

* Todas as informações de Rsyslog (incluindo o sistema, segurança e os registos de aplicações).  
* Um conjunto de núcleos de dados de base do sistema. Tenha em atenção que Olá conjunto completo de dados é descrita no Olá [site soluções de plataforma cruzada do System Center](https://scx.codeplex.com/wikipage?title=xplatproviders).
  Se quiser tooenable dados adicionais, prossiga com passos de Olá em cenários de 2 e 3.

Passo 1. Crie um ficheiro denominado PrivateConfig.json com Olá seguinte conteúdo:

    {
        "storageAccountName" : "hello storage account tooreceive data",
        "storageAccountKey" : "hello key of hello account"
    }

Passo 2. Executar  **extensão da vm do azure definir vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* – o caminho de configuração privada PrivateConfig.json**.

### <a name="scenario-2-customize-hello-performance-monitor-metrics"></a>Cenário 2. Personalizar as métricas de monitor de desempenho de Olá

Esta secção descreve como toocustomize Olá, desempenho e a tabela de dados de diagnóstico.

Passo 1. Crie um ficheiro denominado PrivateConfig.json com conteúdo de Olá que foi descrito no cenário 1. Também crie um ficheiro denominado PublicConfig.json. Especifique os dados de determinado Olá pretende toocollect.

Para todos suportados fornecedores e variáveis, referência Olá [site soluções de plataforma cruzada do System Center](https://scx.codeplex.com/wikipage?title=xplatproviders). Pode ter várias consultas e armazená-las em várias tabelas, acrescentando o script de toohello consultas mais.

Por predefinição, Olá Rsyslog dados sempre é recolhido.

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


Passo 2. Executar  **extensão da vm do azure definir vm_name LinuxDiagnostic Microsoft.OSTCExtensions ' 2.*' – o caminho de configuração privada PrivateConfig.json – o caminho de configuração público PublicConfig.json**.

### <a name="scenario-3-upload-your-own-log-files"></a>Cenário 3. Carregar os seus próprios ficheiros de registo

Esta secção descreve como o tooyour conta de armazenamento de ficheiros de registo específico do toocollect e carregar. É necessário toospecify tanto Olá caminho tooyour registo ficheiro Olá nome da tabela de olá onde pretende toostore o início de sessão. Pode criar vários ficheiros de registo adicionando o script do toohello várias entradas de ficheiros/tabela.

Passo 1. Crie um ficheiro denominado PrivateConfig.json com conteúdo de Olá que foi descrito no cenário 1. Em seguida, crie outro ficheiro com o nome PublicConfig.json com Olá seguinte conteúdo:

```json
{
    "fileCfg" :
    [
        {
            "file" : "/var/log/mysql.err",
            "table" : "mysqlerr"
            }
    ]
}
```

Passo 2. Execute `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.

Tenha em atenção que com esta definição no Olá extensão versões anteriores too2.3, todos os registos de escritas demasiado`/var/log/mysql.err` podem estar duplicados demasiado`/var/log/syslog` (ou `/var/log/messages` consoante Olá Linux distro) bem. Se quiser tooavoid este duplicado registo, pode excluir o registo de `local6` registos de instalação na configuração rsyslog. Depende Olá Linux distro, mas num sistema Ubuntu 14.04, Olá ficheiro toomodify é `/etc/rsyslog.d/50-default.conf` e pode substituir a linha de Olá `*.*;auth,authpriv.none -/var/log/syslog` demasiado`*.*;auth,authpriv,local6.none -/var/log/syslog`. Este problema seja resolvido numa versão correções mais recente de Olá do 2.3 (2.3.9007), pelo que o se tiver uma extensão de Olá versão 2.3, não deve ocorrer este problema. Se continuar, mesmo depois de reiniciar a VM, contacte-nos e ajude-na resolver problemas com a razão pela qual a versão de correções mais recente Olá não é instalado automaticamente.

### <a name="scenario-4-stop-hello-extension-from-collecting-any-logs"></a>Cenário 4. Parar a extensão de Olá de recolher os registos

Esta secção descreve como extensão de Olá toostop de recolha de registos. Tenha em atenção que o processo de agente de monitorização de Olá será ainda em execução mesmo com esta reconfiguração. Se quiser Olá toostop completamente o processo de agente de monitorização, pode fazê-lo por desativar a extensão de Olá. Olá comando toodisable Olá extensão é `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.

Passo 1. Crie um ficheiro denominado PrivateConfig.json com conteúdo de Olá que foi descrito no cenário 1. Crie outro ficheiro com o nome PublicConfig.json com Olá seguinte conteúdo:

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


Passo 2. Executar  **extensão da vm do azure definir vm_name LinuxDiagnostic Microsoft.OSTCExtensions ' 2.*' – o caminho de configuração privada PrivateConfig.json – o caminho de configuração público PublicConfig.json**.

## <a name="review-your-data"></a>Reveja os dados

desempenho de Olá e dados de diagnóstico são armazenados numa tabela de armazenamento do Azure. Reveja [como toouse Azure Table Storage do Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) toolearn como dados de Olá tooaccess no armazenamento de Olá tabela utilizando scripts da CLI do Azure.

Além disso, pode utilizar os seguintes IU ferramentas tooaccess Olá dados:

1. Explorador de servidores do Visual Studio. Aceda a conta de armazenamento tooyour. Após a execução Olá VM durante cerca de cinco minutos, verá as tabelas de predefinição Olá quatro: "LinuxCpu", "LinuxDisk", "LinuxMemory" e "Linuxsyslog". Faça duplo clique Olá nomes tooview Olá os dados da tabela.
1. [Explorador de armazenamento do Azure](https://azurestorageexplorer.codeplex.com/ "Explorador de armazenamento do Azure").

![Imagem](./media/diagnostic-extension/no1.png)

Se ativou fileCfg ou perfCfg (conforme descrito em cenários de 2 e 3), pode utilizar dados de não predefinidas tooview Explorador de servidores do Visual Studio e o Explorador de armazenamento do Azure.

## <a name="known-issues"></a>Problemas conhecidos

* Olá Rsyslog informações e ficheiro de registo especificado de cliente só pode ser acedido através do scripting.
