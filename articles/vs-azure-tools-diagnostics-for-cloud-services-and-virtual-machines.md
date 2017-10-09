---
title: "aaaConfiguring diagnósticos para máquinas virtuais e serviços Cloud do Azure | Microsoft Docs"
description: "Descreve como informações de diagnóstico de tooconfigure de depuração do Azure cloude serviços e máquinas virtuais (VMs) no Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: e70cd7b4-6298-43aa-adea-6fd618414c26
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 74cdf49413d6d89a84195070dd9d817da2463373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-diagnostics-for-azure-cloud-services-and-virtual-machines"></a>Configuração de diagnósticos de máquinas virtuais e serviços em nuvem do Azure
Quando precisar de tootroubleshoot um serviço em nuvem do Azure ou a máquina virtual do Azure, pode configurar mais facilmente diagnóstico do Azure utilizando o Visual Studio. Diagnóstico do Azure captura de dados de sistema e dados de registo em máquinas de virtuais Olá e instâncias de máquina virtual com o seu serviço em nuvem e transferências de dados para uma conta de armazenamento à sua escolha. Consulte [ativar o registo de diagnóstico para web apps no App Service do Azure](app-service-web/web-sites-enable-diagnostic-log.md) para obter mais informações sobre o diagnóstico de registo no Azure.

Este tópico mostra como tooenable e configurar o diagnóstico do Azure no Visual Studio, ambos antes e após a implementação, bem como em máquinas virtuais do Azure. Mostra também como tipos de Olá tooselect de toocollect de informações de diagnóstico e como as informações de Olá tooview depois são recolhidas.

Pode configurar o diagnóstico do Azure no Olá seguintes formas:

* Pode alterar as definições de configuração de diagnóstico através de Olá **configuração de diagnósticos** caixa de diálogo no Visual Studio. definições de Olá são guardadas num ficheiro denominado diagnostics.wadcfgx (diagnostics.wadcfg no Azure SDK 2.4 ou anterior). Em alternativa, pode modificar diretamente o ficheiro de configuração de Olá. Se atualizar manualmente os ficheiros de Olá, as alterações de configuração de Olá irão demorar Olá efeito próxima vez que implementar tooAzure de serviço de nuvem Olá ou o serviço de execução Olá no emulador Olá.
* Utilize **Cloud Explorer** ou **Explorador de servidores** no Visual Studio toochange Olá as definições de diagnóstico para um serviço em nuvem em execução ou a máquina virtual.

## <a name="azure-26-diagnostics-changes"></a>Alterações de diagnóstico do Azure 2.6
Para projetos de 2.6 de SDK do Azure no Visual Studio, Olá seguintes alterações foram efetuada. (Estas alterações também se aplicam toolater versões do SDK do Azure.)

* emulador local Olá suporta agora o diagnóstico. Isto significa que pode recolher dados de diagnóstico e certifique-se de que a aplicação está a criar Olá rastreios direita enquanto estiver a desenvolver e testar no Visual Studio. cadeia de ligação de Olá `UseDevelopmentStorage=true` permite a recolha de dados de diagnóstico enquanto estiver a executar o projeto de serviço em nuvem no Visual Studio, utilizando o emulador de armazenamento do Azure Olá. Todos os dados de diagnóstico são recolhidos na conta do storage Olá (armazenamento de desenvolvimento).
* cadeia de ligação de conta de armazenamento de diagnóstico do Olá (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) é novamente armazenada no ficheiro de configuração (. cscfg) do serviço de Olá. No Azure SDK 2.5 conta de armazenamento do diagnostics Olá foi especificada no ficheiro de diagnostics.wadcfgx Olá.

Existem algumas diferenças importantes entre como cadeia de ligação de Olá trabalhado no Azure SDK 2.4 e anterior e como funciona no Azure SDK 2.6 e posterior.

* No Azure SDK 2.4 e versões anteriores, cadeia de ligação de Olá era utilizada como um tempo de execução por Olá diagnóstico Plug-in tooget Olá armazenamento informações da conta para transferir os registos de diagnóstico.
* No Azure SDK 2.6 ou posterior, a cadeia de ligação de diagnóstico de Olá é utilizada pela extensão de diagnóstico do Visual Studio tooconfigure Olá com as informações de conta de armazenamento adequado Olá durante a publicação. cadeia de ligação de Olá permite-lhe definir as contas de armazenamento diferentes para configurações de serviço diferente que o Visual Studio irá utilizar quando publicar. No entanto, porque o plug-in de diagnóstico de Olá já não está disponível (após o Azure SDK 2.5), o ficheiro. cscfg Olá por si só não é possível ativar Olá extensão de diagnóstico. Tem a extensão de Olá tooenable em separado através de ferramentas, como o Visual Studio ou o PowerShell.
* processo de Olá toosimplify de configuração da extensão de diagnóstico de Olá com o PowerShell, saída de pacotes hello a partir do Visual Studio também contém Olá pública XML de configuração para a extensão de diagnóstico de Olá para cada função. Visual Studio utiliza Olá diagnóstico ligação cadeia toopopulate Olá armazenamento conta informações presentes na configuração pública de Olá. ficheiros de configuração pública de Olá são criados na pasta de extensões de Olá e seguem o padrão de Olá PaaSDiagnostics. &lt;RoleName >. PubConfig.xml. Todas as implementações do PowerShell com base podem utilizar este padrão toomap tooa cada configuração função.
* cadeia de ligação de Olá no ficheiro. cscfg Olá também é utilizada por Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) tooaccess Olá dados de diagnóstico, pelo que pode aparecer no Olá **monitorização** é necessária a cadeia de ligação de Olá separador. tooconfigure Olá serviço tooshow verboso dados no portal de Olá de monitorização.

## <a name="migrating-projects-tooazure-sdk-26-and-later"></a>Migrar projetos tooAzure SDK 2.6 e posterior
Quando migrar do Azure SDK 2.5 tooAzure SDK 2.6 ou posterior, se tiver uma conta de armazenamento do diagnostics especificada no ficheiro de .wadcfgx Olá, em seguida,-permanecerão não existe. tootake partido flexibilidade Olá da utilização de armazenamento diferente das contas para configurações de armazenamento diferente, terá de toomanually adicionar Olá ligação cadeia tooyour projeto. Se estiver a migrar um projeto do Azure SDK 2.4 ou anterior tooAzure SDK 2.6, em seguida, Olá diagnóstico cadeias de ligação são preservadas. No entanto,. tenha em atenção Olá as alterações no como cadeias de ligação são tratadas num Azure SDK 2.6 conforme especificado na secção anterior Olá.

### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a>Como o Visual Studio determina a conta de armazenamento do diagnostics Olá
* Se uma cadeia de ligação de diagnóstico é especificada no ficheiro. cscfg Olá, Visual Studio utiliza-a extensão de diagnóstico de Olá tooconfigure durante a publicação e ao gerar ficheiros de xml de configuração pública de Olá durante empacotamento.
* Não se for especificada nenhuma cadeia de ligação de diagnósticos no ficheiro. cscfg Olá, em seguida, Visual Studio retrocede conta do storage toousing Olá especificada no Olá .wadcfgx tooconfigure Olá diagnóstico extensão de ficheiro ao publicar e gerar Olá público ficheiros do xml de configuração quando empacotamento.
* cadeia de ligação de diagnóstico Olá no ficheiro. cscfg Olá tem precedência sobre a conta de armazenamento Olá no ficheiro de .wadcfgx Olá. Se for uma cadeia de ligação de diagnóstico especificado no ficheiro. cscfg Olá, em seguida, Visual Studio utiliza esse e ignora a conta de armazenamento Olá no .wadcfgx.

### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a>O que does Olá "Atualizar as cadeias de ligação de armazenamento de desenvolvimento..." fazer a caixa de verificação?
Olá caixa de verificação **atualizar as cadeias de ligação de armazenamento de desenvolvimento de diagnóstico e de colocação em cache com credenciais de conta de armazenamento do Microsoft Azure ao publicar tooMicrosoft Azure** dá-lhe uma forma conveniente tooupdate qualquer cadeias de ligação de conta de armazenamento de desenvolvimento com a conta de armazenamento do Azure Olá especificada durante a publicação.

Por exemplo, suponha que selecionar esta caixa de verificação e especifica a cadeia de ligação de diagnóstico de Olá `UseDevelopmentStorage=true`. Quando publica Olá projeto tooAzure, Visual Studio será automaticamente atualizado cadeia de ligação de diagnóstico de Olá com a conta de armazenamento de Olá que especificou no Assistente de publicação Olá. No entanto, se uma conta de armazenamento real foi especificada como cadeia de ligação de diagnóstico de Olá, em seguida, essa conta é utilizada em vez disso.

## <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Diferenças de funcionalidade de diagnóstico entre o Azure SDK 2.4 e anterior e do Azure SDK 2,5 e posterior
Se estiver a atualizar o projeto do Azure SDK 2.4 tooAzure SDK 2,5 ou posterior, deve tenha no Olá atenção os seguintes diferenças de funcionalidade de diagnóstico.

* **APIs de configuração foram preteridas** – configuração programática do diagnostics está disponível no Azure SDK 2.4 ou versões anteriores, mas foi preterida no Azure SDK 2.5 e posterior. Se a configuração de diagnósticos atualmente está definida no código, terá de tooreconfigure essas definições a partir do zero no projeto de migrados Olá por ordem para trabalhar de tookeep de diagnóstico. ficheiro de configuração de diagnósticos de Olá para o Azure SDK 2.4 é diagnostics.wadcfg e diagnostics.wadcfgx para o Azure SDK 2.5 e posterior.
* **Diagnósticos para aplicações de serviço em nuvem só podem ser configurados ao nível de função Olá, não ao nível de instância de Olá.**
* **Sempre que implementar a sua aplicação, a configuração de diagnósticos de Olá é atualizada** – Isto pode causar problemas de paridade, se alterar a configuração de diagnósticos no Explorador de servidores e, em seguida, volte a implementar a sua aplicação.
* **No Azure SDK 2.5 e posterior, informações de estado de falha são configuradas no ficheiro de configuração de diagnósticos de Olá, não no código** – se tiver configuradas no código de capturas de falhas, terá de configuração de Olá toomanually transferência do ficheiro de configuração do código toohello, porque as informações de falhas de Olá não são transferidas durante a migração de Olá tooAzure SDK 2.6.

## <a name="enable-diagnostics-in-cloud-service-projects-before-deploying-them"></a>Ativar o diagnóstico na projetos do serviço em nuvem antes de implementá-las
No Visual Studio, pode escolher os dados de diagnóstico toocollect para funções que são executados no Azure, quando executa o serviço de Olá no emulador Olá antes de o implementar. Todas as definições de toodiagnostics de alterações no Visual Studio são guardadas no ficheiro de configuração de diagnostics.wadcfgx Olá. Estas definições de configuração especificam conta de armazenamento de olá onde os dados de diagnóstico são guardados quando implementar o serviço de nuvem.

[!INCLUDE [cloud-services-wad-warning](../includes/cloud-services-wad-warning.md)]

### <a name="tooenable-diagnostics-in-visual-studio-before-deployment"></a>diagnóstico de tooenable no Visual Studio antes da implementação
1. No menu de atalho Olá para a função de Olá que lhe interessa, escolha **propriedades**e, em seguida, escolha Olá **configuração** separador da função de Olá **propriedades** janela.
2. No Olá **diagnóstico** secção, certifique-se de que Olá **ativar diagnósticos** caixa de verificação está selecionada.
   
    ![Aceder a opção de ativar o diagnóstico Olá](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796660.png)
3. Escolha Olá reticências (…) botão toospecify Olá conta do storage onde pretende toobe de dados de diagnóstico de Olá armazenado. conta de armazenamento de Olá que escolher serão localização Olá armazenar dados de diagnóstico.
   
    ![Especifique toouse de conta de armazenamento Olá](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796661.png)
4. No Olá **criar cadeia de ligação de armazenamento** diálogo caixa, especifique se pretende tooconnect utilizando Olá emulador do Storage do Azure, uma subscrição do Azure, ou introduzir manualmente as credenciais.
   
    ![Caixa de diálogo de conta de armazenamento](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796662.png)
   
   * Se escolher a opção de emulador do Storage do Microsoft Azure Olá, cadeia de ligação de Olá está definida tooUseDevelopmentStorage = true.
   * Se optar por Olá a opção de subscrição, pode escolher Olá pretende toouse e Olá nome da conta de subscrição do Azure. Pode escolher que gerir contas de Olá botão toomanage suas subscrições do Azure.
   * Se escolher Olá introduzida manualmente as credenciais opção, está nome de Olá tooenter pedido e a chave do Olá pretende toouse de conta do Azure.
5. Escolha Olá **configurar** Olá do botão tooview **configuração de diagnósticos** caixa de diálogo. Cada separador (exceto para **geral** e **registo diretórios**) representa uma origem de dados de diagnóstico que pode recolher. separador da predefinição de Olá, **geral**, oferece Olá seguintes opções de recolha de dados de diagnóstico: **apenas erros**, **todas as informações**, e **plano personalizada** . Olá opção predefinida, **apenas erros**, demora Olá mínimo de armazenamento porque não transferir avisos ou mensagens de rastreio. Olá Olá a maioria das informações de todas as transferências de opção de informações e é, por conseguinte, Olá opção mais dispendiosa em termos de armazenamento.
   
    ![Ativar o diagnóstico do Azure e a configuração](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
6. Para este exemplo, selecione Olá **plano personalizada** opção, pelo que pode personalizar os dados de Olá recolhidos.
7. Olá **Quota de disco em MB** caixa especifica quanto espaço pretende tooallocate no seu armazenamento em conta os dados de diagnóstico. Pode alterar o valor predefinido de Olá se pretender.
8. Em cada separador de dados de diagnóstico que pretende toocollect, selecione o **ativar transferência do <log type>**  caixa de verificação. Por exemplo, se pretender que os registos de aplicações toocollect, selecione Olá **ativar a transferência dos registos de aplicação** caixa de verificação Olá **registos da aplicação** separador. Além disso, especifique como outras informações de que cada tipo de dados de diagnóstico. Consulte a secção de Olá **configurar origens de dados de diagnóstico** mais adiante neste tópico para obter informações de configuração em cada separador.
9. Depois de ativar a coleção de todos os dados de diagnóstico de Olá pretende, escolha Olá **OK** botão.
10. Execute o projeto de serviço em nuvem do Azure no Visual Studio como habitualmente. Como utilizar a aplicação, as informações de registo de Olá ativou são guardadas toohello conta de armazenamento do Azure que especificou.

## <a name="enable-diagnostics-in-azure-virtual-machines"></a>Ativar o diagnóstico em máquinas virtuais do Azure
No Visual Studio, pode escolher os dados de diagnóstico toocollect máquinas virtuais do Azure.

### <a name="tooenable-diagnostics-in-azure-virtual-machines"></a>diagnóstico de tooenable em máquinas virtuais do Azure
1. No **Explorador de servidores**, escolha Olá nó do Azure e, em seguida, ligar tooyour subscrição do Azure, se ainda não está ligado.
2. Expanda Olá **máquinas virtuais** nós. Pode criar uma nova máquina virtual ou selecione uma que já não existe.
3. No menu de atalho Olá para a máquina virtual Olá que lhe interessa, escolha **configurar**. Isto mostra a caixa de diálogo de configuração de máquina virtual de Olá.
   
    ![Configurar uma máquina virtual do Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796663.png)
4. Se ainda não estiver instalado, adicione a extensão de diagnóstico de agente de monitorização Microsoft Olá. Esta extensão permite-lhe recolher dados de diagnóstico para Olá máquina virtual do Azure. Na lista de extensões instaladas Olá, escolha o menu de selecionar uma extensão disponíveis pendentes Olá e, em seguida, escolha diagnósticos de agente de monitorização Microsoft.
   
    ![Instalar uma extensão de máquina virtual do Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766024.png)
   
   > [!NOTE]
   > Outras extensões de diagnóstico estão disponíveis para as máquinas virtuais. Para obter mais informações, consulte as extensões de VM do Azure e funcionalidades.
   > 
   > 
5. Escolha Olá **adicionar** botão extensão de Olá tooadd e ver o **configuração de diagnósticos** caixa de diálogo.
6. Escolha Olá **configurar** botão toospecify uma conta de armazenamento e, em seguida, escolha Olá **OK** botão.
   
    Cada separador (exceto para **geral** e **registo diretórios**) representa uma origem de dados de diagnóstico que pode recolher.
   
    ![Ativar o diagnóstico do Azure e a configuração](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
   
    separador da predefinição de Olá, **geral**, oferece Olá seguintes opções de recolha de dados de diagnóstico: **apenas erros**, **todas as informações**, e **plano personalizada** . Olá opção predefinida, **apenas erros**, demora Olá mínimo de armazenamento porque não transferir avisos ou mensagens de rastreio. Olá **todas as informações** opção transferências Olá a maioria das informações e é, por conseguinte, a opção mais dispendiosa do Olá em termos de armazenamento.
7. Para este exemplo, selecione Olá **plano personalizada** opção, pelo que pode personalizar os dados de Olá recolhidos.
8. Olá **Quota de disco em MB** caixa especifica quanto espaço pretende tooallocate no seu armazenamento em conta os dados de diagnóstico. Pode alterar o valor predefinido de Olá se pretender.
9. Em cada separador de dados de diagnóstico que pretende toocollect, selecione o **ativar transferência do <log type>**  caixa de verificação.
   
    Por exemplo, se pretender que os registos de aplicações toocollect, selecione Olá **ativar a transferência dos registos de aplicação** caixa de verificação Olá **registos da aplicação** separador. Além disso, especifique como outras informações de que cada tipo de dados de diagnóstico. Consulte a secção de Olá **configurar origens de dados de diagnóstico** mais adiante neste tópico para obter informações de configuração em cada separador.
10. Depois de ativar a coleção de todos os dados de diagnóstico de Olá pretende, escolha Olá **OK** botão.
11. Guarde o projeto de Olá atualizado.
    
     Verá uma mensagem na Olá **registo de atividade do Microsoft Azure** janela Olá máquina virtual foi atualizada.

## <a name="configure-diagnostics-data-sources"></a>Configurar origens de dados de diagnóstico
Depois de ativar a recolha de dados de diagnóstico, pode escolher exatamente que origens de dados que pretende toocollect e as informações recolhidas. Olá segue-se uma lista dos separadores no Olá **configuração de diagnósticos** caixa de diálogo e significa que cada opção de configuração.

### <a name="application-logs"></a>Registos de aplicações
**Os registos de aplicações** contêm informações de diagnóstico produzidas por uma aplicação web. Se pretender que os registos de aplicações toocapture, selecione Olá **ativar a transferência dos registos de aplicação** caixa de verificação. Pode aumentar ou reduzir Olá número de minutos quando são transferidos os registos da aplicação Olá conta de armazenamento tooyour alterando Olá **período transferência (mín)** valor. Também pode alterar a quantidade de Olá de informações capturadas no registo de Olá definindo o valor de nível de registo de Olá. Por exemplo, pode escolher **verboso** tooget obter mais informações ou escolha **crítico** erros críticos apenas toocapture. Se tiver um fornecedor de diagnóstico específico que emite os registos de aplicações, pode capturá-los adicionando toohello GUID do fornecedor de Olá **GUID de fornecedor** caixa.

  ![Registos de aplicações](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758145.png)

  Consulte [ativar o registo de diagnóstico para web apps no App Service do Azure](app-service-web/web-sites-enable-diagnostic-log.md) para obter mais informações sobre os registos de aplicações.

### <a name="windows-event-logs"></a>Registos de eventos do Windows
Se pretender que os registos de eventos do Windows toocapture, selecione Olá **ativar a transferência de registos de eventos do Windows** caixa de verificação. Pode aumentar ou reduzir Olá número de minutos quando são transferidos os registos de eventos de Olá conta de armazenamento tooyour alterando Olá **período transferência (mín)** valor. Selecione as caixas de verificação de Olá para tipos de Olá de eventos que pretende que o tootrack.

  ![Registos de Eventos](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796664.png)

Se estiver a utilizar o Azure SDK 2.6 ou posterior e quiser toospecify uma origem de dados personalizada, introduza-o no Olá  **<Data source name>**  texto caixa e, em seguida, escolha Olá **adicionar** tooit seguinte do botão. origem de dados de Olá é adicionada toohello diagnostics.cfcfg ficheiro.

Se estiver a utilizar o Azure SDK 2.5 e quiser toospecify uma origem de dados personalizados, pode adicioná-lo toohello `WindowsEventLog` secção Olá diagnostics.wadcfgx de ficheiros, tal como no seguinte exemplo de Olá.

```
<WindowsEventLog scheduledTransferPeriod="PT1M">
   <DataSource name="Application!*" />
   <DataSource name="CustomDataSource!*" />
</WindowsEventLog>
```
### <a name="performance-counters"></a>Contadores de desempenho
Informações do contador de desempenho podem ajudar a localizar congestionamentos de sistema e otimizar o desempenho do sistema e aplicação. Consulte [criar e utilizar os contadores de desempenho de uma aplicação do Azure](https://msdn.microsoft.com/library/azure/hh411542.aspx) para obter mais informações. Se pretender que os contadores de desempenho toocapture, selecione Olá **ativar a transferência dos contadores de desempenho** caixa de verificação. Pode aumentar ou reduzir Olá número de minutos quando são transferidos os registos de eventos de Olá conta de armazenamento tooyour alterando Olá **período transferência (mín)** valor. Selecione as caixas de verificação Olá para hello contadores de desempenho que pretende que o tootrack.

  ![Contadores de Desempenho](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758147.png)

tootrack um contador de desempenho que não está listado, introduza-o utilizando Olá sintaxe sugerida e, em seguida, escolha Olá **adicionar** botão. sistema de operativo Olá na máquina virtual de Olá determina que contadores de desempenho pode controlar. Para obter mais informações sobre sintaxe, consulte [especificando um caminho de contador](https://msdn.microsoft.com/library/windows/desktop/aa373193.aspx).

### <a name="infrastructure-logs"></a>Registos de infraestrutura
Se pretender que os registos de infraestrutura de toocapture, que contêm informações sobre Olá infraestrutura de diagnóstico do Azure, o módulo de RemoteAccess Olá e o módulo de RemoteForwarder Olá, selecione Olá **ativar a transferência dos registos de infraestrutura**caixa de verificação. Pode aumentar ou reduzir Olá número de minutos quando são transferidos Olá registos conta de armazenamento tooyour alterando o valor de período de transferência (mín) Olá.

  ![Registos de infraestrutura de diagnóstico](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758148.png)

  Consulte [recolher dados de registo por utilizando o Azure Diagnostics](https://msdn.microsoft.com/library/azure/gg433048.aspx) para obter mais informações.

### <a name="log-directories"></a>Diretórios de registo
Se pretender que os diretórios de registo toocapture, que contêm dados recolhidos a partir de diretórios de registo para pedidos de serviços de informação Internet (IIS), os pedidos falhados ou pastas que escolher, selecione Olá **ativar transferência do registo diretórios**caixa de verificação. Pode aumentar ou reduzir Olá número de minutos quando são transferidos Olá registos conta de armazenamento tooyour alterando Olá **período transferência (mín)** valor.

Pode selecionar caixas Olá de registos de Olá pretende toocollect, tal como **registos de IIS** e **falhou pedido** registos. São fornecidos os nomes de contentor de armazenamento predefinido, mas pode alterar os nomes de Olá se pretender.

Além disso, pode capturar os registos de qualquer pasta. Especifique apenas o caminho de Olá no Olá **registo do diretório absoluto** secção e, em seguida, escolha Olá **Adicionar diretório** botão. Olá registos irão ser capturados toohello especificado contentores.

  ![Diretórios de registo](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796665.png)

### <a name="etw-logs"></a>Registos ETW
Se utilizar [rastreio de eventos para o Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803\(v=vs.85\).aspx) (ETW) e pretende toocapture ETW registos, selecione de Olá **ativar a transferência dos registos de ETW** caixa de verificação. Pode aumentar ou reduzir Olá número de minutos quando são transferidos Olá registos conta de armazenamento tooyour alterando Olá **período transferência (mín)** valor.

eventos de Olá são capturados a partir de origens de eventos e manifestos de eventos que especificar. toospecify uma origem de evento, introduza um nome na Olá **origens de eventos** secção e, em seguida, escolha Olá **Adicionar origem de evento** botão. Da mesma forma, pode especificar um manifesto de eventos no Olá **manifestos de eventos** secção e, em seguida, escolha Olá **adicionar evento manifesto** botão.

  ![Registos ETW](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766025.png)

  arquitetura ETW hello é suportada no ASP.NET através de classes no Olá [System.Diagnostics.aspx] (espaço de nomes https://msdn.microsoft.com/library/system.diagnostics (v=vs.110). Olá Microsoft.WindowsAzure.Diagnostics espaço de nomes que herda e expande padrão [System.Diagnostics.aspx] (classes https://msdn.microsoft.com/library/system.diagnostics (v=vs.110), permite Olá utilização ([System.Diagnostics.aspx] https://msdn.microsoft.com/library/System.Diagnostics (v=vs.110) como uma arquitetura de registo Olá ambiente do Azure. Para obter mais informações, consulte [assumir o controlo de registo e rastreio no Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) e [ativar diagnósticos no Cloud Services do Azure e máquinas virtuais](cloud-services/cloud-services-dotnet-diagnostics.md).

### <a name="crash-dumps"></a>Informações de falhas
Se pretender obter informações de toocapture sobre quando falhas de uma instância de função, selecione Olá **ativar transferência de informações de falhas** caixa de verificação. (Porque o ASP.NET processa a maioria das exceções, isto é geralmente úteis apenas para as funções de trabalho.) Pode aumentar ou diminuir a percentagem de Olá de armazenamento espaço dedicados capturas de falhas de toohello alterando Olá **Quota de diretório (%)** valor. Pode alterar o contentor de armazenamento olá onde capturas de falhas de Olá são armazenadas e pode selecionar se pretende que toocapture um **completa** ou **Mini** informação.

os processos de Olá atualmente a ser controlados estão listados. Selecione as caixas de verificação de Olá para processos de Olá que pretende que o toocapture. tooadd outro processo toohello lista introduzir o nome do processo de Olá e, em seguida, escolha Olá **processo adicionar** botão.

  ![Informações de falhas](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766026.png)

  Consulte [assumir o controlo de registo e rastreio no Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) e [4 do Microsoft Azure Diagnostics parte: componentes de registo personalizado e o Azure Diagnostics 1.3 alterações](http://justazure.com/microsoft-azure-diagnostics-part-4-custom-logging-components-azure-diagnostics-1-3-changes/) para obter mais informações.

## <a name="view-hello-diagnostics-data"></a>Ver dados de diagnóstico de Olá
Depois de já recolhidos dados de diagnóstico de Olá para um serviço em nuvem ou de uma máquina virtual, pode vê-la.

### <a name="tooview-cloud-service-diagnostics-data"></a>dados de diagnóstico de serviço de nuvem tooview
1. Implementar o serviço em nuvem como habitual e, em seguida, executá-la.
2. Pode ver os dados de diagnóstico de Olá num relatório que gera o Visual Studio ou tabelas na sua conta de armazenamento. dados de Olá tooview num relatório, abra **Cloud Explorer** ou **Explorador de servidores**, abra o menu de atalho Olá do nó de Olá para a função de Olá que lhe interessa e, em seguida, escolha **ver dados de diagnóstico** .
   
    ![Ver dados de diagnóstico](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748912.png)
   
    Um relatório que mostre os dados disponíveis Olá aparece.
   
    ![Relatório de diagnóstico do Microsoft Azure no Visual Studio](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796666.png)
   
    Se os dados mais recentes Olá não aparecem, poderá ter toowait para Olá transferência período tooelapse.
   
    Escolha Olá **atualizar** associar dados de Olá tooimmediately atualização, ou escolha um intervalo no Olá **atualização automática** pendente caixa toohave Olá dados da lista atualizados automaticamente. dados de erro do tooexport Olá, escolha Olá **exportar tooCSV** botão toocreate um ficheiro de valores separados por vírgulas pode abrir numa folha de cálculo.
   
    No **Cloud Explorer** ou **Explorador de servidores**, abra a conta de armazenamento de Olá que está associada à implementação de Olá.
3. Abra tabelas de diagnóstico de Olá no Visualizador de tabela Olá e, em seguida, reveja os dados de Olá que recolheu. Para registos de IIS e registos personalizados, pode abrir um contentor do blob. Analisando Olá a tabela seguinte, pode localizar o contentor de tabela ou blob Olá que contém dados Olá que lhe interessa. Além do ficheiro de registo de dados de toohello para que, entradas da tabela de Olá contenham EventTickCount, DeploymentId, função e toohelp RoleInstance identificar que máquina virtual e a função gerado dados Olá e quando. 
   
   | Dados de diagnóstico | Descrição | Localização |
   | --- | --- | --- |
   | Registos de aplicações |Registos que gera o código ao chamar os métodos de Olá Trace classe. |WADLogsTable |
   | Registos de Eventos |Estes dados são de registos de eventos do Windows hello em máquinas de virtuais Olá. Windows armazena informações nestes registos, mas as aplicações e serviços também utilizá-los tooreport erros ou informações de registo. |WADWindowsEventLogsTable |
   | Contadores de Desempenho |É possível recolher dados em qualquer contador de desempenho que está disponível na máquina virtual de Olá. sistema de operativo Olá fornece os contadores de desempenho, que incluem estatísticas muitos tal como o tempo de processador e utilização de memória. |WADPerformanceCountersTable |
   | Registos de infraestrutura |Estes registos são gerados da infraestrutura de diagnóstico de Olá próprio. |WADDiagnosticInfrastructureLogsTable |
   | Registos de IIS |Estes registos registam pedidos web. Se o seu serviço em nuvem obtém uma quantidade significativa de tráfego, estes registos podem ser bastante demorados, pelo que deve recolher e armazenar estes dados apenas quando precisar dele. |Pode encontrar os registos de pedido falhou no contentor de blob Olá em wad iis failedreqlogs sob um caminho para essa instância, a função e a implementação. Pode encontrar registos completos em wad-iis-logfiles. As entradas para cada ficheiro que são efetuadas na tabela de WADDirectories Olá. |
   | Informações de falhas |Estas informações fornecem imagens binárias do processo do seu serviço em nuvem (normalmente uma função de trabalho). |contentor de BLOBs de capturas de crush WAD |
   | Ficheiros de registo personalizado |Registos de dados que lhe predefinidos. |Pode especificar na localização de Olá código personalizado de ficheiros de registo na sua conta de armazenamento. Por exemplo, pode especificar um contentor do blob personalizado. |
4. Se são truncados dados de qualquer tipo, pode experimentar aumentar Olá da memória intermédia para esse tipo de dados ou encurtar o intervalo de Olá entre as transferências de dados a partir da conta de armazenamento tooyour do Olá máquina virtual.
5. (opcional) Remover dados do armazenamento de Olá conta ocasionalmente tooreduce os custos de armazenamento geral.
6. Quando efetuar uma implementação completa, ficheiros de diagnostics.cscfg Olá (.wadcfgx para o Azure SDK 2.5) é atualizado no Azure e o serviço em nuvem escolherá qualquer configuração de diagnósticos de tooyour de alterações. Se, em vez disso, atualizar uma implementação existente, o ficheiro. cscfg Olá não está atualizado no Azure. Ainda pode alterar as definições de diagnóstico, seguindo os passos de Olá na secção seguinte, Olá. Para obter mais informações sobre como efetuar uma implementação completa e atualizar uma implementação existente, consulte [publicar Assistente da aplicação Azure](vs-azure-tools-publish-azure-application-wizard.md).

### <a name="tooview-virtual-machine-diagnostics-data"></a>dados de diagnóstico da máquina virtual de tooview
1. No menu de atalho Olá para a máquina virtual de Olá, escolha **ver dados de diagnóstico**.
   
    ![Ver dados de diagnóstico na máquina virtual do Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766027.png)
   
    Esta ação abre Olá **resumo de diagnóstico** janela.
   
    ![Resumo de diagnóstico de máquina virtual do Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796667.png)  
   
    Se os dados mais recentes Olá não aparecem, poderá ter toowait para Olá transferência período tooelapse.
   
    Escolha Olá **atualizar** associar dados de Olá tooimmediately atualização, ou escolha um intervalo no Olá **atualização automática** pendente caixa toohave Olá dados da lista atualizados automaticamente. dados de erro do tooexport Olá, escolha Olá **exportar tooCSV** botão toocreate um ficheiro de valores separados por vírgulas pode abrir numa folha de cálculo.

## <a name="configure-cloud-service-diagnostics-after-deployment"></a>Configurar o diagnóstico de serviço de nuvem após a implementação
Se estiver a investigar um problema com um serviço em nuvem que já em execução, pode querer toocollect dados que não especificou antes de função Olá originalmente implementadas. Neste caso, pode iniciar toocollect esses dados utilizando as definições de Olá no Explorador de servidores. Pode configurar diagnósticos para uma única instância ou todas as instâncias de Olá numa função, dependendo se abrir a caixa de diálogo de configuração de diagnósticos de Olá no menu de atalho Olá para a instância de Olá ou função Olá. Se configurar o nó de função Olá, quaisquer alterações aplicam tooall instâncias. Se configurar o nó de instância de Olá, quaisquer alterações aplicam-se apenas a instância toothat.

### <a name="tooconfigure-diagnostics-for-a-running-cloud-service"></a>diagnóstico de tooconfigure num serviço em nuvem em execução
1. No Explorador de servidores, expanda Olá **serviços em nuvem** nó e, em seguida, expanda a função de Olá nós toolocate ou a instância que pretende que o tooinvestigate ou ambos.
   
    ![Configuração de diagnósticos](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748913.png)
2. No menu de atalho Olá para um nó de instância ou um nó de função, escolha **as definições de diagnóstico de atualização**e, em seguida, escolha Olá definições de diagnóstico que pretende que o toocollect.
   
    Para obter informações sobre as definições de configuração de Olá, consulte **configurar origens de dados de diagnóstico** neste tópico. Para obter informações sobre como tooview Olá dados de diagnóstico, consulte **ver dados de diagnóstico de Olá** neste tópico.
   
    Se mudar de recolha de dados no **Explorador de servidores**, estas alterações permanecem em vigor até totalmente de Reimplementar o seu serviço em nuvem. Se utilizar definições de publicação predefinida Olá, alterações de Olá não são substituídas, uma vez que a predefinição de Olá publicar definição é implementação existente do tooupdate Olá, em vez de Efetue uma reimplementação completa. limpar as definições de Olá se toomake no momento da implementação, aceda toohello **definições avançadas** separador no Assistente de publicação Olá e desmarque Olá **atualização da implementação** caixa de verificação. Quando implementar novamente com essa caixa de verificação desmarcada, as definições de Olá reverter toothose no ficheiro de Olá .wadcfgx (ou .wadcfg) conforme definido através do editor de propriedades de Olá para a função de Olá. Se atualizar a implementação, o Azure mantém as definições antigas do Olá.

## <a name="troubleshoot-azure-cloud-service-issues"></a>Resolver problemas de serviço em nuvem do Azure
Se surgirem problemas com os projetos do serviço em nuvem, tal como uma função que obtém bloqueada no estado "ocupado", repetidamente recicla ou emitir um erro de servidor interno, existem ferramentas e técnicas que pode utilizar toodiagnose e corrigir estes problemas. Para obter exemplos específicos de problemas e soluções comuns, bem como uma descrição geral dos conceitos de Olá e ferramentas utilizadas toodiagnose e resolva esses erros, consulte [dados de diagnóstico de computação do Azure PaaS](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

## <a name="q--a"></a>P&R
**O que é o tamanho da memória intermédia de Olá e, como grandes deverá ser?**

Em cada instância de máquina virtual, quotas limitam a quantidade de dados diagnóstico pode ser armazenado no sistema de ficheiros local Olá. Além disso, especificar um tamanho de memória intermédia para cada tipo de dados de diagnóstico que está disponíveis. Este tamanho de memória intermédia funciona como uma quota individuais para esse tipo de dados. Verificando Olá parte inferior da caixa de diálogo Olá, pode determinar Olá quota geral e a quantidade de Olá de memória que permanece. Se especificar memórias intermédias maiores ou mais tipos de dados, terá de abordar Olá quota geral. Pode alterar Olá geral quota ao modificar o ficheiro de configuração de diagnostics.wadcfg/.wadcfgx Olá. Olá, diagnóstico de Olá os dados são armazenados no mesmo sistema de ficheiros como dados da sua aplicação, para que o se a sua aplicação utiliza uma grande quantidade de espaço em disco, não deve aumentar Olá geral quota de diagnóstico.

**O que é o período de transferência Olá e quanto deve ser?**

período de transferência de Olá é Olá período de tempo que decorrer entre dados de captura. Após cada período de transferência, é mover os dados de sistema de ficheiros local Olá no tootables máquina virtual na sua conta de armazenamento. Se Olá dados que são recolhidos excede a quota de Olá antes de fim de Olá de um período de transferência, são rejeitados dados mais antigos. Pode querer período de transferência de Olá toodecrease se estiver a perda de dados porque os dados excedem o tamanho de memória intermédia de Olá ou Olá quota geral.

**O fuso horário são Olá carimbos de data / hora na?**

carimbos de data / hora Olá é Olá fuso horário local do Centro de dados de Olá que aloja o serviço em nuvem. Olá seguintes três colunas timestamp nas tabelas de registo hello são utilizadas.

* **PreciseTimeStamp** é Olá ETW timestamp do evento de Olá. Ou seja, o evento de Olá de tempo de Olá é registado a partir do cliente de Olá.
* **TIMESTAMP** PreciseTimeStamp é arredondado para baixo limites de frequência de carregamento de toohello. Por isso, se a frequência de carregamento é 5 minutos e eventos de Olá 00:17:12 de tempo, TIMESTAMP será 00:15:00.
* **Timestamp** é timestamp Olá no qual Olá entidade foi criada no Olá tabela do Azure.

**Como gerir os custos aquando da recolha de informações de diagnóstico?**

Olá predefinições (**nível de registo** definido demasiado**erro** e **transferência período** definido demasiado**1 minuto**) são toominimize concebida custo. Os custos de computação irão aumentar se recolher mais dados de diagnóstico ou diminua o período de transferência Olá. Não recolha mais dados do que o que precisa e não se esqueça de recolha de dados de toodisable quando já não precisar dele. Pode sempre ativá-lo novamente, mesmo em runtime, conforme mostrado na secção anterior Olá.

**Como recolher registos de pedido falhou a partir do IIS?**

Por predefinição, o IIS não recolher registos de pedido falhou. Pode configurar toocollect IIS Olá-las, se editar o ficheiro Web. config para a função da web.

**Não consigo estou a obter informações de rastreio do RoleEntryPoint métodos como OnStart. O que é incorreto?**

métodos para Olá RoleEntryPoint são denominados no contexto de Olá da WAIISHost.exe, não IIS. Por conseguinte, Olá informações de configuração em Web. config que normalmente permite rastreio não se aplica. tooresolve este problema, adicione um projeto de função do web. config ficheiro tooyour e nome Olá ficheiro toomatch Olá saída assemblagem que contém o código de RoleEntryPoint Olá. No projeto de função da web do predefinido Olá, nome de Olá do ficheiro. config de Olá seria WAIISHost.exe.config. Em seguida, adicione Olá seguintes linhas toothis ficheiro:

```
<system.diagnostics>
  <trace>
      <listeners>
          <add name “AzureDiagnostics” type=”Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener”>
              <filter type=”” />
          </add>
      </listeners>
  </trace>
</system.diagnostics>
```

Agora, no Olá **propriedades** janela, conjunto Olá **copiar tooOutput diretório** propriedade demasiado**Copiar sempre**.

## <a name="next-steps"></a>Passos seguintes
toolearn mais informações sobre o diagnóstico de registo no Azure, consulte [ativar diagnósticos no Cloud Services do Azure e máquinas virtuais](cloud-services/cloud-services-dotnet-diagnostics.md) e [ativar o registo de diagnóstico para web apps no App Service do Azure](app-service-web/web-sites-enable-diagnostic-log.md).

