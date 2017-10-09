---
title: "aaaAzure SDK para notas de versão do .NET 2.8"
description: "Notas de versão do Azure SDK para .NET 2.8"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: de7207ff-ba4f-4008-9141-8742fcaa3254
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 2722dcdd27bf9ab65b48e91dcdb545536f987dd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-28-281-and-282"></a>Azure SDK para .NET 2.8, 2.8.1 e 2.8.2
## <a name="overview"></a>Descrição geral
Este artigo contém notas de versão Olá (que inclui problemas conhecidos e alterações) para Olá Azure SDK para .NET 2.8, 2.8.1 e 2.8.2 versões. 

Para a lista completa das novas funcionalidades e atualizações efetuadas nesta versão, consulte Olá [Azure SDK 2.8 para Visual Studio 2013 e o Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/) anúncio. 

## <a name="azure-sdk-for-net-28"></a>Azure SDK para NET 2.8
### <a name="download-azure-sdk-for-net-28"></a>Transfira o Azure SDK para .NET 2.8
[Azure SDK para .NET 2.8 para Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkId=699285) 

[Azure SDK para .NET 2.8 para o Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkId=699287)

### <a name="net-452-support"></a>Suporta a .NET 4.5.2
#### <a name="known-issues"></a>Problemas conhecidos
2.8 de SDK .NET do Azure permite-lhe toocreate .NET 4.5.2 pacotes do serviço em nuvem. No entanto 4.5.2 do .NET framework não será instalado no predefinido Olá versão de imagens de SO convidado até Janeiro de 2016 SO convidado. Antes dessa, 4.5.2 do .NET framework estarão disponível através de uma versão de lançamento de SO convidado separada – Novembro de 2015-02. Consulte Olá [versões de SO de convidado do Azure e matriz de compatibilidade de SDK](../cloud-services/cloud-services-guestos-update-matrix.md) tootrack página quando a imagem de Olá será lançada.  Assim que a imagem do Olá Novembro de 2015-02 é libertada optar toouse dessa imagem atualizando o seu ficheiro de ficheiro (. cscfg) de configuração do serviço em nuvem. Na configuração do serviço Olá ficheiro definir o atributo de osVersion Olá da cadeia de toohello Olá ServiceConfiguration elemento "WA-convidado-SO-4.26_201511-02". Se escolher tooopt toouse esta imagem, em seguida, já não obterá as atualizações automáticas toohello SO convidado. tooget Olá as atualizações automáticas Olá osVersion tem de ser definido demasiado "*" e a .NET 4.5.2 só estará disponível através de atualizações automáticas de Janeiro de 2016.

### <a name="azure-data-factory"></a>Azure Data Factory
#### <a name="known-issues"></a>Problemas conhecidos
Durante uma **modelo da fábrica de dados** projeto criação que envolvem os dados de exemplo, o script de shell de energia do azure poderão falhar se a versão do azure power shell instalado na máquina de Olá após 0.9.8.

Ordem toosuccessfully criar este tipo de projeto, terá de instalar [versão do azure de power shell 0.9.8](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi).

### <a name="azure-resource-manager-tools"></a>Ferramentas do Gestor de recursos do Azure
#### <a name="breaking-changes"></a>As alterações de última hora
Olá script do PowerShell fornecida pelo projeto do grupo de recursos do Azure de Olá tiver sido atualizado na toowork versão Olá de cmdlets do Azure PowerShell nova versão 1.0.  Este script novo não funcionará com o Visual Studio quando utilizar uma versão do Olá SDK anterior too2.8.  

Scripts de projetos criados em versões anteriores do Olá SDK não serão executada no Visual Studio quando utilizar Olá 2.8 SDK.  Todos os scripts continuará toowork fora do Visual Studio com a versão adequada do Olá do Olá cmdlets Azure PowerShell.  

Olá 2.8 SDK requer a versão 1.0 do Olá cmdlets Azure PowerShell.  Todas as outras versões de Olá SDK requerem a versão 0.9.8 de Olá cmdlets Azure PowerShell.  Para obter mais informações consulte [isto](http://go.microsoft.com/fwlink/?LinkID=623011) blogue.

### <a name="web-tools-extensions"></a>Web das ferramentas de extensões
#### <a name="known-issues"></a>Problemas conhecidos
os seguintes problemas conhecidos de Olá será resolvido em Olá seguir versão.

* Serviço de aplicações relacionadas com o Cloud e Explorador de servidores não funcionam gesto para ambientes de não produção (como o Azure China ou clientes de pilha do Azure). Para publicar os clientes nas seguintes áreas afetados, transferir Olá perfil de Olá portal do Azure irá ativar a capacidade de publicação. Versão futura irá reparar gestos como "Depurador anexar" e "Ver registos de transmissão em fluxo" para o Azure China e os clientes de pilha. 
* Os clientes poderão ver erros durante a criação quando Olá App Insights instância toowhich que estiver a implementar está numa região diferente EUA leste do serviço de aplicações. Nestes cenários, criar um serviço de aplicações no portal de Olá e a transferência Olá perfil de publicação irá ativar cenários de publicação. 

### <a name="azure-hdinsight-tools"></a>Ferramentas do Azure HDInsight
#### <a name="new-updates"></a>Novas atualizações
* Pode executar a consulta do Hive num cluster de Olá através de HiveServer2 com quase nenhuma sobrecarga e ver a tarefa de Olá nos registos em tempo real.
* Utilizar Olá nova vista do Hive tarefas execução pode aprofundar para a tarefa mais aprofundada, encontrar mais detalhes e identificar potenciais problemas.

Para informações, consulte [Azure SDK 2.8 para Visual Studio 2013 e o Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/). 

## <a name="azure-sdk-for-net-281"></a>Azure SDK para .NET 2.8.1
### <a name="known-issues-for-visual-studio-2013-and-visual-studio-2015"></a>Problemas conhecidos do Visual Studio 2013 e o Visual Studio 2015
1. WebJob accionada publica tooslots irá mostrar e o erro e não uma agenda do conjunto, mas será push Olá WebJob tooAzure. Os clientes que estão que necessite de uma tarefa agendada, em seguida, podem utilizar Olá Portal do Azure tooset agendamento Olá para Olá WebJob. 
2. Os clientes de Python podem ter problemas de depurador. Equipa de serviço está a implementar uma correção para este mas se a clientes serem afetados,. permitem que a Microsoft sabe nos fóruns de Olá ou no blogue de anúncio de Olá ou secção de comentários notas de versão. 
3. Os clientes em determinados regiões (por exemplo, Sul da Índia) irão ocorrer erros de aprovisionamento do serviço de aplicações. Isto é consistente com o portal de Olá e os clientes que ocorrer este problema, podem utilizar Olá toorequest portal do Azure acesso toopublish toothese-georregiões. Assim que o pedido de acesso toothese regiões utilizando deverão funcionar Olá aprovisionamento do portal do Azure. 

## <a name="azure-sdk-for-net-282"></a>Azure SDK para .NET 2.8.2
Após a instalação de Olá das ferramentas de Olá 2.8.2, os clientes podem ter Olá seguir o problema.         

* Se estiver a utilizar o Windows 10 e não tiver instalado o Internet Explorer, poderá receber um erro "Internet Explorer não foi possível encontrar".
  problema de Olá tooresolve, instale o Internet Explorer utilizando Olá Adicionar/remover a caixa de diálogo de componentes do Windows.

Se observar este problema, utilize Olá enviar um smile funcionalidade tooreport-lo.

Para obter mais informações, consulte [isto](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-2-for-net/) post.

## <a name="other-updates"></a>Outras atualizações
Para outras atualizações, consulte [post de anúncio do Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).

## <a name="also-see"></a>Consulte também
[Post de anúncio do Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)

[Informações de extinção para Olá Azure SDK para .NET e APIs e suporte](https://msdn.microsoft.com/library/azure/dn479282.aspx)

