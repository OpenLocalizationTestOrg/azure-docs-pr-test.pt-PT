---
title: "migração de plataforma aaaSecurity Center FAQ | Microsoft Docs"
description: "Estas perguntas mais frequentes respondem a dúvidas sobre Olá migração de plataforma Centre de segurança do Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4d1364cd-7847-425a-bb3a-722cb0779f78
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: terrylan
ms.openlocfilehash: fcb14ae83167ef79a60371e4fcb625cf99bee6c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="security-center-platform-migration-faq"></a>Migração de plataforma do Centro de segurança FAQ
No precoce de Junho de 2017, o Centro de segurança do Azure começou a utilizar Olá Microsoft Monitoring Agent toocollect e arquivo de dados. toolearn mais, consulte [migração de plataforma de centro de segurança do Azure](security-center-platform-migration.md). Estas perguntas mais frequentes respondem a dúvidas sobre a migração de plataforma Olá.

## <a name="data-collection-agents-and-workspaces"></a>Recolha de dados, os agentes e áreas de trabalho

### <a name="how-is-data-collected"></a>Como os dados são recolhidos?
Centro de segurança utiliza dados de segurança do Olá Microsoft Monitoring Agent toocollect das suas VMs. dados de segurança de Olá incluem informações sobre configurações de segurança, que são utilizados tooidentify vulnerabilidades, e eventos de segurança, que são utilizados toodetect ameaças. Dados recolhidos pelo agente Olá são armazenados num toohello de área de trabalho ligada de análise de registos VM existente ou uma nova área de trabalho criados pelo centro de segurança. Quando o Centro de segurança cria uma nova área de trabalho, geolocalização Olá de Olá VM é contemplada.

> [!NOTE]
> Olá Microsoft Monitoring Agent é Olá mesmo agente utilizado pelo Olá Operations Management Suite (OMS), o serviço de análise de registos e o System Center Operations Manager (SCOM).
>
>

Quando a recolha de dados é ativada para Olá pela primeira vez ou quando as subscrições são migradas, o Centro de segurança verifica toosee se Olá Microsoft Monitoring Agent já está instalada como uma extensão do Azure em cada uma das suas VMs. Se Olá Microsoft Monitoring Agent não está instalado, o Centro de segurança irá:

- instalar o agente do Microsoft Monitoring Olá Olá VM
   - uma área de trabalho criada pelo centro de segurança já existe na Olá geolocalização mesma como Olá VM, Olá agente estiver ligada toothis área de trabalho
   - Se não existir uma área de trabalho, o Centro de segurança cria um novo grupo de recursos predefinidos a área de trabalho que geolocalização e estabelecer a ligação de área de trabalho do Olá agente toothat. Convenção de nomenclatura de Olá para o grupo de recursos e área de trabalho de Olá são:

       Área de trabalho: DefaultWorkspace-[ID de subscrição]-[georreplicação]

       Grupo de recursos: DefaultResouceGroup-[georreplicação]
- instalar uma solução de centro de segurança na área de trabalho Olá

localização de Olá da área de trabalho Olá é com base na localização de Olá de Olá VM. toolearn mais, consulte [segurança dos dados](security-center-data-security.md).

> [!NOTE]
> Migração tooplatform anterior, o Centro de segurança recolhidos dados de segurança das suas VMs utilizando Olá o agente de monitorização do Azure e dados que foram armazenados na sua conta de armazenamento. Após a migração de plataforma Olá, o Centro de segurança utiliza Olá Microsoft Monitoring Agent e toocollect da área de trabalho e arquivo Olá mesmos dados. conta de armazenamento Olá pode ser removida após a migração de Olá.
>
>

### <a name="am-i-billed-for-log-analytics-or-oms-on-hello-workspaces-created-by-security-center"></a>Estou cobrado para análise de registos ou OMS em áreas de trabalho Olá criadas pelo centro de segurança?
Não. Áreas de trabalho criadas pelo centro de segurança, embora a configurada para OMS por faturação de nó, não pagar OMS. Faturação do Centro de segurança baseia-se sempre no seu centro de segurança de política e Olá soluções de segurança instaladas na área de trabalho:

- **Escalão gratuito** – Centro de segurança instala a solução de 'SecurityCenterFree' Olá na área de trabalho do Olá predefinido. Não são cobradas para o escalão gratuito Olá.
- **Escalão Standard** – Olá 'SecurityCenterFree' instala o Centro de segurança e soluções de 'Security' no Olá área de trabalho predefinida.

Para obter mais informações sobre preços, consulte [preços do Centro de segurança](https://azure.microsoft.com/pricing/details/security-center/). Olá, endereços de página de preços altera o armazenamento de dados de toosecurity e proporcional faturação a partir de Junho de 2017.

> [!NOTE]
> escalão de preço OMS Olá de áreas de trabalho criados pelo centro de segurança não afeta a faturação do Centro de segurança.
>
>

### <a name="can-i-delete-hello-default-workspaces-created-by-security-center"></a>Pode eliminar as áreas de trabalho de predefinição do Olá criadas pelo centro de segurança?
**Não é recomendada a eliminar a área de trabalho do Olá predefinida.** Centro de segurança utiliza Olá os dados de segurança da toostore de áreas de trabalho de predefinida das suas VMs.  Se eliminar uma área de trabalho, o Centro de segurança não é possível toocollect estes dados e algumas recomendações de segurança e alertas estão indisponíveis

toorecover, remover Olá Microsoft Monitoring Agent na área de trabalho do Olá VMs toohello ligado eliminado. Centro de segurança reinstala agente Olá e cria novas áreas de trabalho predefinido.

### <a name="what-if-hello-microsoft-monitoring-agent-was-already-installed-as-an-extension-on-hello-vm"></a>E se Olá Microsoft Monitoring Agent já foi instalado como uma extensão no Olá VM?
Centro de segurança não substitui a áreas de trabalho do existente ligações toouser. Dados de segurança do Centro de segurança arquivos de Olá VM na área de trabalho Olá já estabeleceu ligação.

### <a name="what-if-i-had-a-microsoft-monitoring-agent-installed-on-hello-machine-but-not-as-an-extension"></a>E se posso tinha um Microsoft Monitoring Agent instalada na máquina de Olá, mas não como uma extensão?
Se Olá Microsoft Monitoring Agent é instalada diretamente no Olá VM (não como uma extensão do Azure), o Centro de segurança não instalará Olá Microsoft Monitoring Agent e monitorização de segurança serão limitada.

### <a name="what-is-hello-impact-of-removing-these-extensions"></a>O que é o impacto de Olá da remoção estas extensões?
Se remover Olá a extensão de monitorização Microsoft, o Centro de segurança não é capaz de toocollect dados segurança Olá VM e algumas recomendações de segurança e alertas não estão disponíveis. Dentro de 24 horas, o Centro de segurança determina que Olá VM está em falta na extensão de Olá e volta a instalar Olá extensão.

### <a name="how-do-i-stop-hello-automatic-agent-installation-and-workspace-creation"></a>Como parar instalação automática do agente de Olá e a criação de área de trabalho?
Pode desativar a recolha de dados para as suas subscrições na política de segurança de Olá, mas isto não é recomendado. Desativar alertas e limites de recolha de dados as recomendações do Centro de segurança. Recolha de dados é necessária para subscrições no escalão de preço padrão Olá. recolha de dados de toodisable:

1. Se a sua subscrição está configurada para o escalão Standard Olá, abra a política de segurança de Olá para essa subscrição e selecione Olá **livres** camada.

   ![Escalão de preço][1]

2. Em seguida, desativar a recolha de dados selecionando **desativar** no Olá **política de segurança – recolha de dados** painel.

   ![Recolha de dados][2]

### <a name="how-do-i-remove-oms-extensions-installed-by-security-center"></a>Como posso remover extensões OMS instaladas pelo centro de segurança?
Pode remover manualmente Olá Microsoft Monitoring Agent. Não é recomendado como limita as recomendações do Centro de segurança e alertas.

> [!NOTE]
> Se a recolha de dados estiver ativada, o Centro de segurança irá reinstalar agente Olá depois removê-la.  Terá de recolha de dados de toodisable antes de remover manualmente o agente de Olá. Consulte [como parar a criação de instalação e a área de trabalho de automática do agente de Olá?](#how-do-i-stop-the-automatic-agent-installation-and-workspace-creation?) para obter instruções sobre como desativar a recolha de dados.
>
>

toomanually remover agente Olá:

1.  No portal de Olá, abra **Log Analytics**.
2.  No painel de análise de registos de Olá, selecione uma área de trabalho:
3.  Selecione cada VM que não pretende toomonitor e selecione **desligar**.

   ![Remover agente Olá][3]

> [!NOTE]
> Se uma VM com Linux já tem um agente do OMS de extensão de nome, remover a extensão de Olá remove o agente de Olá, bem como e o cliente de Olá tem tooreinstall-lo.
>
>

## <a name="existing-oms-customers"></a>Clientes existentes do OMS

### <a name="does-security-center-override-any-existing-connections-between-vms-and-workspaces"></a>O Centro de segurança substituir todas as ligações existentes entre as VMs e áreas de trabalho?
Se uma VM já tem Olá Microsoft Monitoring Agent instalada como uma extensão do Azure, o Centro de segurança não substitui ligação de área de trabalho existente Olá. Em vez disso, o Centro de segurança utiliza a área de trabalho existente Olá.

Uma solução de centro de segurança está instalado na área de trabalho Olá se não estiver já presente, não sendo solução Olá aplicado toohello apenas VMs relevantes. Quando adiciona uma solução, é automaticamente implementada pelo tooall Windows e Linux agentes tooyour ligado Log Analytics área de trabalho predefinida. [Filtragem de solução](../operations-management-suite/operations-management-suite-solution-targeting.md), que é uma funcionalidade do OMS, permite-lhe tooapply um âmbito tooyour soluções.

Se Olá Microsoft Monitoring Agent é instalada diretamente no Olá VM (não como uma extensão do Azure), o Centro de segurança não instalará Olá Microsoft Monitoring Agent e monitorização de segurança é limitado.

### <a name="what-should-i-do-if-i-suspect-that-hello-data-platform-migration-broke-hello-connection-between-one-of-my-vms-and-my-workspace"></a>O que posso fazer se posso suspeita que a migração de plataforma de dados de Olá quebrou ligação Olá entre uma das minhas VMs e a minha área de trabalho?
Isto não deve ocorrer. Se esta situação ocorrer, em seguida, [para criar um pedido de suporte do Azure](../azure-supportability/how-to-create-azure-support-request.md) e incluir Olá os detalhes:

- ID de recurso do Azure Olá de Olá afetado VM
- ID de recurso do Azure Olá da área de trabalho Olá configurada numa extensão de Olá antes de ligação de Olá foi interrompida
- agente de Olá e a versão que foi anteriormente instalado

### <a name="does-security-center-install-solutions-on-my-existing-oms-workspaces-what-are-hello-billing-implications"></a>Centro de segurança instalar soluções no meu áreas de trabalho do OMS existentes? Quais são as implicações de faturação Olá?
Quando o Centro de segurança identificar uma VM já está ligado tooa área de trabalho que criou, o Centro de segurança permite soluções no tooyour escalão de preço de acordo com esta área de trabalho. Olá soluções é aplicado toohello apenas as VMs do Azure relevantes, através de [solução filtragem](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting), por isso, permanece faturação Olá Olá mesmo.

- **Escalão gratuito** – Centro de segurança instala a solução de 'SecurityCenterFree' Olá na área de trabalho Olá. Não são cobradas para o escalão gratuito Olá.
- **Escalão Standard** – Olá 'SecurityCenterFree' instala o Centro de segurança e soluções de 'Security' no Olá área de trabalho.

   ![Soluções na área de trabalho predefinido][4]

> [!NOTE]
> Olá solução 'Security' na análise de registos é Olá segurança & soluções de auditoria no OMS.
>
>

### <a name="i-already-have-workspaces-in-my-environment-can-i-use-them-toocollect-security-data"></a>Já tenho áreas de trabalho no meu ambiente, posso utilizar-os dados de segurança toocollect?
Se uma VM já tem Olá Microsoft Monitoring Agent instalada como uma extensão do Azure, o Centro de segurança utiliza Olá área de trabalho existente ligado. Uma solução de centro de segurança está instalado na área de trabalho Olá se não estiver já presente, não sendo solução Olá aplicado toohello apenas relevantes VMs através de [solução filtragem](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting).

Quando o Centro de segurança instala Olá Microsoft Monitoring Agent em VMs, utiliza Olá predefinido workspace(s) criado pelo centro de segurança. Assim que os clientes que serão capaz tooconfigure que workspace(s) é utilizados.

### <a name="i-already-have-security-solution-on-my-workspaces-what-are-hello-billing-implications"></a>Já tenho solução de segurança no meu áreas de trabalho. Quais são as implicações de faturação Olá?
Olá solução de segurança e de auditoria é tooenable utilizadas funcionalidades do escalão padrão de centro de segurança para VMs do Azure. Se a solução de segurança & auditoria Olá já está instalada na área de trabalho, o Centro de segurança utiliza solução existente Olá. Não há nenhuma alteração no faturação.

## <a name="next-steps"></a>Passos seguintes
toolearn mais informações sobre a migração de plataforma do Centro de segurança de Olá, consulte

- [Migração de plataforma do Centro de segurança do Azure](security-center-platform-migration.md)
- [Guia de resolução de problemas do Centro de segurança do Azure](security-center-troubleshooting-guide.md)

<!--Image references-->
[1]: ./media/security-center-platform-migration-faq/pricing-tier.png
[2]: ./media/security-center-platform-migration-faq/data-collection.png
[3]: ./media/security-center-platform-migration-faq/remove-the-agent.png
[4]: ./media/security-center-platform-migration-faq/solutions.png
