---
title: "aaaWhat é a automatização do Azure | Microsoft Docs"
description: "Saiba que valor fornece a automatização do Azure e obtenha respostas a perguntas de toocommon para que pode começar a utilizar criação, utilizando runbooks e o Automation DSC do Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "o que é a automatização, automatização do azure, exemplos de automatização do azure"
ms.assetid: 0cf1f3e8-dd30-4f33-b52a-e148e97802a9
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/10/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 1e5a90e272d6b2beb7b5007e2fea2c110dbd79b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-overview"></a>Descrição geral da Automatização do Azure
Automatização do Microsoft Azure fornece uma forma para os utilizadores tooautomate Olá tarefas de manual, execução longa, propensas ao erro e frequentemente repetidas que normalmente são executadas num ambiente de nuvem e empresa. Poupa tempo e aumenta a fiabilidade de Olá das tarefas administrativas normais e agenda-as toobe automaticamente executadas em intervalos regulares. Pode automatizar os processos utilizando runbooks ou automatizar a gestão de configuração utilizando a Configuração de Estado Pretendido. Este artigo fornece uma breve descrição geral de Automatização do Azure e responde a algumas perguntas comuns. Pode consultar tooother artigos nesta biblioteca para informações mais detalhadas sobre os diferentes tópicos de Olá.

## <a name="automating-processes-with-runbooks"></a>Automatizar processos com runbooks
Um runbook é um conjunto de tarefas que efetuam algum processo automatizado na Automatização do Azure. Poderá ser um processo simple, tais como iniciar uma máquina virtual e criar uma entrada de registo ou pode não ter um runbook complexo que combina outro tooperform runbooks mais pequeno um processo complexo através de vários recursos ou mesmo várias nuvens e ambientes no local.  

Por exemplo, pode ter um manual existente processo para truncar uma SQL database se é aproximar-se o tamanho máximo que inclua vários passos, tais como ligação de toohello de servidor, ligar toohello base de dados, obter Olá tamanho atual da base de dados, verifique se o limiar foi excedido e, em seguida, truncá-lo e notificar o utilizador. Em vez de efetuar manualmente cada um destes passos, pode criar um runbook que executará todas estas tarefas como um único processo. Seria iniciar runbook Olá, fornecer informações de Olá necessárias, tais como o nome do servidor SQL Olá, o nome de base de dados e o e-mail do destinatário e, em seguida, Descontraia enquanto Olá processo ser concluído. 

## <a name="what-can-runbooks-automate"></a>O que podem automatizar os runbooks?
Os runbooks na Automatização do Azure são baseados no Windows PowerShell ou no Fluxo de Trabalho do Windows PowerShell, pelo que fazem tudo o que o PowerShell pode fazer. Se uma aplicação ou serviço tiver uma API, um runbook pode trabalhar com a mesma. Se tiver um módulo do PowerShell para a aplicação Olá, pode carregar esse módulo para a automatização do Azure e incluir estes cmdlets no runbook. Os runbooks de automatização do Azure executados na Olá em nuvem do Azure e podem aceder a quaisquer recursos na nuvem ou recursos externos que podem ser acedidos a partir da nuvem Olá. Utilizar [Runbook Worker híbrido](automation-hybrid-runbook-worker.md), os runbooks podem ser nos seus dados locais recursos locais de toomanage center. 

## <a name="getting-runbooks-from-hello-community"></a>Obter runbooks da Comunidade Olá
Olá [Galeria de Runbooks](automation-runbook-gallery.md#runbooks-in-runbook-gallery) contém runbooks da Microsoft e Olá Comunidade que pode utilizar inalterados no seu ambiente ou personalize-os para os seus fins. Também são úteis tooas referências toolearn como toocreate os seus próprios runbooks. Até pode contribuir o seus próprios toohello de runbooks da galeria que pensa que outros utilizadores poderão considerar úteis. 

## <a name="creating-runbooks-with-azure-automation"></a>Criar Runbooks com a Automatização do Azure
Pode [criar os seus próprios runbooks](automation-creating-importing-runbook.md) do zero ou modificar runbooks Olá [Galeria de Runbooks](http://msdn.microsoft.com/library/azure/dn781422.aspx) para os seus requisitos. Pode escolher de entre quatro [tipos de runbooks](automation-runbook-types.md) diferentes com base nos seus requisitos e na sua experiência com o PowerShell. Se preferir toowork diretamente com Olá código do PowerShell, em seguida, pode utilizar um [runbook do PowerShell](automation-runbook-types.md#powershell-runbooks) ou [runbook de fluxo de trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) que edita offline ou com Olá [editordetexto](http://msdn.microsoft.com/library/azure/dn879137.aspx) no Olá portal do Azure. Se preferir tooedit um runbook sem estar exposto toohello subjacente código, em seguida, pode criar um [runbook gráfico](automation-runbook-types.md#graphical-runbooks) utilizando Olá [editor gráfico](automation-graphical-authoring-intro.md) no Olá portal do Azure. 

Prefere ver do tooreading? Tem uma vista de olhos Olá abaixo as vídeo a partir de sessão do Microsoft Ignite de Maio de 2015. Nota: Apesar hello conceitos e funcionalidades descritas neste vídeo estarem corretas, que automatização do Azure tem progredido muito desde que o vídeo foi gravado, agora tem uma IU mais extensa no Olá portal do Azure e suporta as capacidades adicionais.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3451/player]
> 
> 

## <a name="automating-configuration-management-with-desired-state-configuration"></a>Gestão da configuração da automatização com a Configuração de Estado Pretendido
[PowerShell DSC](https://technet.microsoft.com/library/dn249912.aspx) é uma plataforma de gestão que permite-lhe toomanage, implementar e impor uma configuração para anfitriões físicos e máquinas virtuais utilizando uma sintaxe do PowerShell declarativa. Pode definir configurações num Servidor de Solicitação do DSC central que as máquinas de destino podem obter e aplicar automaticamente. O DSC fornece um conjunto de cmdlets do PowerShell que pode utilizar recursos e configurações de toomanage.  

O [Automation DSC do Azure](automation-dsc-overview.md) é uma solução baseada na nuvem para o PowerShell DSC que fornece serviços necessários para ambientes empresariais.  Pode gerir os recursos de DSC na automatização do Azure e aplicar configurações toovirtual ou máquinas físicas provenientes de um servidor de solicitação do DSC na Olá em nuvem do Azure.  Fornece também reporting services que o informam de eventos importantes como, por exemplo, quando nós se desviaram da respetiva configuração atribuída e quando uma nova configuração tiver sido aplicada. 

## <a name="creating-your-own-dsc-configurations-with-azure-automation"></a>Criar as suas configurações do DSC com a Automatização do Azure
[Configurações de DSC](automation-dsc-overview.md) especificar estado Olá pretendido de um nó.  Vários nós podem aplicar Olá mesmo tooassure de configuração que todos mantêm um estado idêntico.  Pode criar uma configuração utilizando qualquer editor de texto na sua máquina local e, em seguida, importá-la para a Automatização do Azure, onde pode compilá-la e aplicar nós à mesma.

## <a name="getting-modules-and-configurations"></a>Obter módulos e configurações
Pode obter [módulos do PowerShell](automation-runbook-gallery.md#modules-in-powershell-gallery) que contêm cmdlets que pode utilizar os seus runbooks e configurações de DSC de Olá [galeria do PowerShell](http://www.powershellgallery.com/). Pode iniciar esta galeria a partir de Olá portal do Azure e importar os módulos diretamente na automatização do Azure, ou pode transferir e importá-los manualmente. Não é possível instalar os módulos de Olá diretamente a partir do portal do Azure de Olá, mas pode transferi-los instalá-los tal como faria com qualquer outro módulo. 

## <a name="example-practical-applications-of-azure-automation"></a>Aplicações práticas de exemplo da Automatização do Azure
Seguem-se alguns exemplos dos tipos de Olá de cenários de automatização com a automatização do Azure. 

* Crie e copie as máquinas virtuais em diferentes subscrições do Azure. 
* Agende cópias de ficheiros a partir de um contentor de Blob Storage do Azure de tooan do computador local. 
* Automatize as funções de segurança, tal como negar pedidos de um cliente quando é detetado um ataque denial-of-service. 
* Certifique-se de que as máquinas alinham continuamente com a política de segurança configurada.
* Gira a implementação contínua do código da aplicação na infraestrutura no local e na nuvem. 
* Crie uma floresta do Active Directory no Azure para o seu ambiente de laboratório. 
* Truncar uma tabela numa SQL Database se a base de dados estiver a atingir o tamanho máximo. 
* Atualize remotamente as definições de ambiente para o Web site do Azure. 

## <a name="how-does-azure-automation-relate-tooother-automation-tools"></a>Como o automatização do Azure relacionados com ferramentas de automatização tooother?
[Service Management Automation (SMA)](http://technet.microsoft.com/library/dn469260.aspx) é tooautomate pretendido tarefas de gestão na nuvem privada Olá. Este é instalado localmente no seu datacenter como um componente do [Microsoft Azure Pack](https://www.microsoft.com/en-us/server-cloud/). SMA e a automatização do Azure utilizam Olá mesmo formato de runbook baseado no Windows PowerShell e o fluxo de trabalho do Windows PowerShell, mas não suporta o SMA [runbooks gráficos](automation-graphical-authoring-intro.md).  

O [System Center 2012 Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) foi concebido para a automatização dos recursos no local. Utiliza um formato de runbook diferente de automatização do Azure e o Service Management Automation e tem um toocreate de interface gráfica os runbooks sem que seja necessário qualquer scripting. Os seus runbooks são compostos por atividades dos Pacotes de Integração que são escritas especificamente para o Orchestrator. 

## <a name="where-can-i-get-more-information"></a>Onde posso obter mais informações?
Uma variedade de recursos estão disponíveis para toolearn mais informações sobre a automatização do Azure e criar os seus próprios runbooks. 

* Neste momento, encontra-se na **Biblioteca da Automatização do Azure**. artigos Olá nesta biblioteca fornecem uma documentação completa sobre configuração de Olá e administração da automatização do Azure e para criar os seus próprios runbooks. 
* Os [cmdlets do Azure PowerShell](http://msdn.microsoft.com/library/jj156055.aspx) fornecem informações para automatizar as operações do Azure com o Windows PowerShell. Os Runbooks utilizam estes cmdlets toowork com recursos do Azure. 
* [Blogue de gestão](https://azure.microsoft.com/blog/tag/azure-automation/) fornece informações mais recentes Olá na automatização do Azure e outras tecnologias de gestão da Microsoft. Deve subscrever toothis blogue toostay segurança toodate com Olá mais recentes da equipa de automatização do Azure Olá. 
* [Fórum de automatização](http://go.microsoft.com/fwlink/p/?LinkId=390561) permite-lhe toopost dúvidas toobe de automatização do Azure resolvidas pela Microsoft e Olá Comunidade de automatização. 
* Os [cmdlets da Automatização do Azure](https://msdn.microsoft.com/library/mt244122.aspx) fornecem informações para automatizar tarefas de administração. Contém as contas de automatização de toomanage cmdlets, recursos, runbooks, DSC.

## <a name="can-i-provide-feedback"></a>Posso enviar comentários?
**Envie-nos comentários!** Se estiver à procura de uma solução de runbook de Automatização do Azure ou um módulo de integração, publique um Pedido de Script no Centro de Scripts. Se tiver comentários ou pedidos funcionalidades para a Automatização do Azure, publique-os na [Voz do Utilizador](http://feedback.windowsazure.com/forums/34192--general-feedback). Obrigado! 

