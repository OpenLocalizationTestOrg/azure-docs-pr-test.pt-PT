---
title: "desempenho de Olá aaaTesting de um serviço em nuvem | Microsoft Docs"
description: "Testar o desempenho de Olá de um serviço em nuvem utilizando o gerador de perfis do Olá Visual Studio"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7a5501aa-f92c-457c-af9b-92ea50914e24
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 98bd775e6ffcf948e737c5ec26399c81f4770fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service"></a>Teste Olá desempenho de um serviço em nuvem
## <a name="overview"></a>Descrição geral
Pode testar o desempenho de Olá de um serviço em nuvem na Olá seguintes formas:

* Utilize diagnósticos do Azure toocollect informações sobre pedidos e as ligações e estatísticas de site tooreview que mostram a forma como o serviço de Olá efetua uma perspetiva do cliente. tooget começar a utilizar, consulte [configurar diagnósticos para máquinas virtuais e serviços Cloud do Azure](http://go.microsoft.com/fwlink/p/?LinkId=623009).
* Utilize Olá Visual Studio do gerador de perfis tooget uma análise aprofundada de aspetos computacional Olá como o serviço de Olá é executado. Como este tópico descreve, pode utilizar o desempenho de toomeasure do gerador de perfis de Olá como um serviço é executado no Azure. Para obter informações sobre como desempenho toomeasure de gerador de perfis de Olá do toouse como um serviço é executada localmente no emulador de computação, consulte [Olá testar desempenho de um Azure na nuvem serviço localmente no Olá utilizando o emulador de computação Olá Visual Studio do gerador de perfis ](http://go.microsoft.com/fwlink/p/?LinkId=262845).

## <a name="choosing-a-performance-testing-method"></a>Escolher um método de teste de desempenho
### <a name="use-azure-diagnostics-toocollect"></a>Utilize toocollect de diagnóstico do Azure:
* Estatísticas em páginas web ou de serviços, como pedidos e ligações.
* Estatísticas de funções, tais como a frequência uma função é reiniciada.
* Em geral sobre a utilização de memória, como percentagem de Olá de tempo que Olá demora de recoletor de lixo ou Olá memória definido de uma função em execução.

### <a name="use-hello-visual-studio-profiler-to"></a>Utilize o gerador de perfis do Olá Visual Studio para:
* Determine as funções que demorada Olá mais.
* Medir quanto tempo demora de cada parte de um programa viáveis intensiva.
* Comparação detalhada do desempenho de relatórios para duas versões de um serviço.
* Analise a atribuição de memória em mais detalhe que nível de Olá de alocações de memória individuais.
* Analise problemas de concorrência no código multithread.

Quando utiliza o gerador de perfis de Olá, é possível recolher dados quando um serviço em nuvem é executada localmente ou no Azure.

### <a name="collect-profiling-data-locally-to"></a>Recolha a criação de perfis dados localmente para:
* Testar o desempenho de Olá de uma parte de um serviço em nuvem, tais como a execução de Olá da função de trabalho específico, que não necessita de uma carga simulada realista.
* Testar o desempenho de Olá de um serviço em nuvem no isolamento, em condições controladas.
* Teste Olá desempenho de um serviço em nuvem antes de implementá-la tooAzure.
* Teste o desempenho de Olá de um serviço de nuvem privada, sem implementações existentes de Olá disturbing.
* Testar o desempenho de Olá do serviço de Olá sem incorrer em custos de em execução no Azure.

### <a name="collect-profiling-data-in-azure-to"></a>Recolha dados de criação de perfis no Azure para:
* Testar o desempenho de Olá de um serviço em nuvem com uma carga real ou simulado.
* Utilize o método de instrumentação de Olá de recolha de dados de criação de perfis, tal como este tópico descreve mais tarde.
* Testar o desempenho de Olá do serviço de Olá no Olá mesmo ambiente, como quando o serviço de Olá é executada na produção.

Normalmente, a simular um serviços de cloud de tootest de carga em normal ou realçar condições.

## <a name="profiling-a-cloud-service-in-azure"></a>Criação de perfis de um serviço em nuvem no Azure
Quando publicar o seu serviço em nuvem do Visual Studio, pode perfil serviço Olá e especificar Olá criação de perfis de definições que forneça que Olá informações que pretende. Uma sessão de criação de perfis é iniciada para cada instância de uma função. Para obter mais informações sobre como toopublish o serviço a partir do Visual Studio, consulte o artigo [publicação tooan serviço de nuvem do Azure a partir do Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx).

toounderstand mais informações sobre a criação de perfis de desempenho no Visual Studio, consulte [manual de principiantes tooPerformance criação de perfis](https://msdn.microsoft.com/library/azure/ms182372.aspx) e [analisar o desempenho de aplicações através de ferramentas de criação de perfis](https://msdn.microsoft.com/library/azure/z9z62c29.aspx).

> [!NOTE]
> Pode ativar o IntelliTrace ou criação de perfis quando publicar o seu serviço em nuvem. Não é possível ativar a ambos.
> 
> 

### <a name="profiler-collection-methods"></a>Métodos de coleção do gerador de perfis
Pode utilizar métodos de coleção diferente para a criação de perfis, com base na sua problemas de desempenho:

* **A amostragem da CPU** -este método recolhe estatísticas de aplicações que são úteis para análise inicial dos problemas de utilização da CPU. A amostragem da CPU é Olá método sugerido para iniciar a maioria das investigações de desempenho. Há um impacto baixo na aplicação Olá que lhe está a criação de perfis quando recolher os dados da amostragem de CPU.
* **Instrumentação** -este método recolhe dados de temporização detalhadas que é útil para análise focada e para analisar problemas de desempenho de entrada/saída. método de instrumentação Olá regista cada entrada, saída e chamada de função das funções de Olá num módulo durante uma criação de perfis de execução. Este método é útil para reunir informações de temporização detalhadas sobre uma secção do seu código e para compreender o impacto de Olá de operações de entrada e de saída no desempenho da aplicação. Este método está desativado para um computador a executar um sistema operativo de 32 bits. Esta opção está disponível apenas quando executa o serviço em nuvem Olá no Azure, não localmente no emulador de computação Olá.
* **Atribuição de memória de .NET** -este método recolhe dados de alocação de memória de .NET Framework utilizando o método de criação de perfis de amostragem de Olá. Olá os dados recolhidos incluem o número de Olá e tamanho dos objetos alocados.
* **Simultaneidade** -este método recolhe dados de contenção de recursos e o processo e o thread de dados de execução que são útil analisar vários threads e processos várias aplicações. método de concorrência Olá recolhe dados para cada evento que a execução de blocos de código, tal como quando um thread aguarda bloqueado acesso tooan aplicação recursos toobe libertado. Este método é útil para analisar aplicações com vários threads.
* Também pode ativar **criação de perfis de interação do escalão**, que fornece informações adicionais sobre os tempos de execução de Olá ADO.NET síncrona chama nas funções de aplicações de várias camadas de mensagens em fila que comunicam com um ou mais bases de dados. Pode recolher dados de interação do escalão com qualquer um dos métodos de criação de perfis de Olá. Para obter mais informações sobre a criação de perfis de interação do escalão, consulte [camada interações vista](https://msdn.microsoft.com/library/azure/dd557764.aspx).

## <a name="configuring-profiling-settings"></a>Configurar definições de criação de perfis
Olá a seguinte ilustração mostra como tooconfigure as definições de criação de perfis da caixa de diálogo Publicar aplicação Azure Olá.

![Configurar definições de criação de perfis](./media/vs-azure-tools-performance-profiling-cloud-services/IC526984.png)

> [!NOTE]
> Olá tooenable **ativar a criação de perfis** caixa de verificação, tem de ter o gerador de perfis de Olá instalado no computador local Olá que está a utilizar toopublish seu serviço em nuvem. Por predefinição, o gerador de perfis de Olá é instalado quando instalar o Visual Studio.
> 
> 

### <a name="tooconfigure-profiling-settings"></a>tooconfigure as definições de criação de perfis
1. No Explorador de soluções, abra o menu de atalho Olá para o projeto do Azure e, em seguida, escolha **publicar**. Para obter passos detalhados sobre como toopublish um serviço em nuvem, consulte [publicação de uma nuvem utilizando o serviço Olá ferramentas do Azure](http://go.microsoft.com/fwlink/p?LinkId=623012).
2. No Olá **publicar aplicação Azure** caixa de diálogo, escolha Olá **definições avançadas** separador.
3. tooenable a criação de perfis, selecione Olá **ativar a criação de perfis** caixa de verificação.
4. tooconfigure as definições de criação de perfis, escolha Olá **definições** hyperlink. é apresentada a caixa de diálogo de definições de criação de perfis de Olá.
5. De Olá **que método de criação de perfis teria como toouse** botões de opção, escolha o tipo de Olá de criação de perfis que precisa.
6. interação de camada de Olá toocollect criação de perfis de dados, selecione de Olá **ativar camada interação de criação de perfis** caixa de verificação.
7. definições de Olá toosave, escolha Olá **OK** botão.
   
    Quando publicar esta aplicação, estas definições são Olá toocreate utilizadas sessões para cada função de criação de perfis.

## <a name="viewing-profiling-reports"></a>Visualizar relatórios de criação de perfis
É criada uma sessão de criação de perfis para cada instância de uma função no seu serviço em nuvem. tooview a criação de perfis de relatórios de cada sessão a partir do Visual Studio, pode ver a janela do Explorador de servidores de Olá e, em seguida, escolha uma instância de uma função de Olá tooselect de nó de computação do Azure. Em seguida, pode ver Olá relatório de criação de perfis, conforme mostrado na seguinte ilustração de Olá.

![Vista de criação de perfis de relatório a partir do Azure](./media/vs-azure-tools-performance-profiling-cloud-services/IC748914.png)

### <a name="tooview-profiling-reports"></a>tooview relatórios de criação de perfis
1. tooview Olá servidor janela do Explorador no Visual Studio, escolha do barra menu Olá vista, Explorador de servidores.
2. Escolha o nó de computação do Azure Olá e, em seguida, escolha nó de implementação do Azure Olá para o serviço em nuvem Olá que selecionou tooprofile quando publicou a partir do Visual Studio.
3. a criação de perfis de tooview relatórios para uma instância, escolha a função Olá no serviço de Olá, o menu de atalho Olá aberta de uma instância específica e, em seguida, escolha **Ver relatório de criação de perfis**.
   
    relatório de Olá, um ficheiro de .vsp, agora é transferido a partir do Azure e é apresentado o estado de Olá da transferência Olá no Olá registo de atividade do Azure. Quando concluída a transferência de Olá, Olá criação de perfis de relatório é apresentado num separador num editor de Olá para Visual Studio com o nome <Role name>  *<Instance Number>*  <identifier>.vsp. Dados de resumo para o relatório de Olá aparece.
4. toodisplay vistas diferentes do relatório de Olá, na lista de vista atual Olá, escolha o tipo de Olá de vista que pretende. Para obter mais informações, consulte [vistas de relatório de ferramentas de criação de perfis](https://msdn.microsoft.com/library/azure/bb385755.aspx).

## <a name="next-steps"></a>Passos seguintes
[Depuração serviços Cloud](https://msdn.microsoft.com/library/azure/ee405479.aspx)

[Publicação tooan serviço de nuvem do Azure a partir do Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx)

