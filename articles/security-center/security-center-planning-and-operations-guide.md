---
title: "Guia de operações e planeamento do Centro de aaaSecurity | Microsoft Docs"
description: "Este documento ajuda-o a tooplan antes de adotar o Centro de segurança do Azure e as considerações relativas à operações diárias."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f984e4a2-ac97-40bf-b281-2f7f473494c4
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: b0a0a6f5fd56fbd46f7736928c99e3bcd0b1e140
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-planning-and-operations-guide"></a>Guia de operações e planeamento do Centro de Segurança do Azure
Este guia destina-se a profissionais de tecnologias de informática (TI) da informação, arquitetos de TI, analistas de segurança de informações e administradores de nuvem cujas organizações estejam a planear toouse do Centro de segurança do Azure.

>[!NOTE] 
>A partir da precoce de Junho de 2017, o Centro de segurança irá utilizar Olá Microsoft Monitoring Agent toocollect e armazenar dados. Consulte [migração de plataforma de centro de segurança do Azure](security-center-platform-migration.md) toolearn mais. informações de Olá neste artigo representam a funcionalidade do Centro de segurança após a transição toohello Microsoft Monitoring Agent.
>

## <a name="planning-guide"></a>Guia de planeamento
Este guia aborda um conjunto de passos e tarefas que pode seguir toooptimize que a utilização do Centro de segurança com base nos requisitos de segurança da sua organização e o modelo de gestão de nuvem. tootake tirem o máximo partido do Centro de segurança, é importante toounderstand forma diferentes pessoas ou equipas na sua organização utilizar Olá serviço toomeet desenvolvimento e operações seguras, monitorização, governação e tem de resposta a incidentes. Olá áreas-chave tooconsider quando planear o Centro de segurança toouse são:

* Funções de Segurança e Controlos de Acesso
* Recomendações e Políticas de Segurança
* Armazenamento e Recolha de Dados
* Monitorização de Segurança em Curso
* Resposta a Incidentes

Na secção seguinte, Olá, ficará a saber como tooplan para cada uma dessas áreas e aplicar as recomendações com base nos seus requisitos.

> [!NOTE]
> Leitura [perguntas mais frequentes sobre (FAQ) do Centro de segurança do Azure](security-center-faq.md) para obter uma lista de perguntas comuns que também podem ser úteis durante Olá conceber e planear fase.
> 

## <a name="security-roles-and-access-controls"></a>Funções de segurança e controlos de acesso
Dependendo do tamanho de Olá e a estrutura da sua organização, várias pessoas e equipas podem utilizar o Centro de segurança tooperform relacionadas com segurança tarefas diferentes. Olá diagrama a seguir, é necessário um exemplo de fictícias e as respetivas funções e responsabilidades de segurança:

![Funções](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig01-new.png)

Centro de segurança permite que estes indivíduos toomeet estas variadas responsabilidades. Por exemplo:

**Jorge (Proprietário da Carga de Trabalho de Nuvem)**

* Gerir uma carga de trabalho de nuvem e os respetivos recursos relacionados
* Responsável pela implementação e manutenção de proteções de acordo com a política de segurança da empresa

**Helena (CISO/CIO)**

* Responsável por todos os aspetos de segurança para a empresa Olá
* Pretende postura de segurança da empresa Olá toounderstand em cargas de trabalho de nuvem
* Tem de toobe informado de ataques principais e os riscos

**Diogo (Segurança de TI)**

* Conjuntos de políticas de segurança tooensure Olá adequado proteções estão implementadas de empresa
* Monitoriza a conformidade com as políticas
* Gera relatórios para liderança ou auditores

**Júlia (Operações de Segurança)**

* Monitoriza e responde toosecurity alertas 24/7
* Escalar tooCloud proprietário da carga de trabalho ou analista de segurança de TI

**Samuel (Analista de Segurança)**

* Investigar ataques
* Trabalhar com a remediação de tooapply proprietário da carga de trabalho de nuvem 

Centro de segurança utiliza [controlo de acesso baseado em funções (RBAC)](../active-directory/role-based-access-control-configure.md), que fornece [funções incorporadas](../active-directory/role-based-access-built-in-roles.md) que podem ser atribuídas toousers, grupos e serviços no Azure. Quando um utilizador abre o Centro de segurança, apenas verá informações relacionadas com tooresources têm acesso. O que significa utilizador Olá tem atribuída a função de Olá de proprietário, Contribuidor ou leitor toohello subscrição ou grupo de recursos que um recurso pertence. Funções de toothese de adição, existem duas funções específicas do Centro de segurança:

- **Leitor de segurança**: utilizador pertence toothis função ser capaz de tooview direitos tooSecurity Center, o que inclui as recomendações, alertas, políticas e estado de funcionamento, mas só estará toomake capaz de alterações.
- **Administrador de segurança**: mesmo que o leitor de segurança, mas também pode atualizar política de segurança de Olá, dispensar recomendações e alertas.

funções de centro de segurança de Olá descritas acima não têm acesso tooother serviço áreas do Azure como armazenamento, Web & Mobile ou Internet das coisas.  

> [!NOTE]
> O utilizador precisa de toobe, pelo menos, uma subscrição, o proprietário do grupo de recursos ou o toosee capaz de contribuinte toobe Centro de segurança no Azure. 
> 
> 

Ao utilizar pessoas fictícias de Olá explicado no diagrama anterior de Olá, Olá, seria necessário o seguinte RBAC:

**Jorge (Proprietário da Carga de Trabalho de Nuvem)**

* Proprietário/Colaborador de Grupo de Recursos

**Diogo (Segurança de TI)**

* Proprietário/Colaborador de Subscrição ou Administrador de Segurança

**Júlia (Operações de Segurança)**

* Leitor de subscrição ou segurança leitor tooview alertas
* Proprietário/colaborador de subscrição ou o administrador de segurança necessário toodismiss alertas

**Samuel (Analista de Segurança)**

* Alertas de tooview de leitor de subscrição
* Proprietário/colaborador de subscrição necessário toodismiss alertas
* Área de trabalho do acesso toohello poderá ser necessária

Algumas outra tooconsider informações importantes:

* Apenas os Proprietários/Contribuintes de subscrição e Administradores de Segurança podem editar uma política de segurança
* Apenas os Proprietários e os Contribuintes do grupo de recursos e de subscrição podem aplicar recomendações de segurança a um recurso

Quando planear o controlo de acesso através do RBAC para o Centro de segurança, ser toounderstand se de que na sua organização vai utilizar o Centro de segurança. Além disso, os tipos de tarefas que vão executar e, em seguida, configura o RBAC em conformidade.

> [!NOTE]
> Recomendamos que atribua Olá função menos permissiva necessária para os utilizadores toocomplete as respetivas tarefas. Por exemplo, os utilizadores que apenas precisam de informações de tooview sobre estado de segurança de Olá dos recursos, mas não tomar medidas, tal como aplicar recomendações ou editar políticas, devem ser atribuídos função de leitor de Olá.
> 
> 

## <a name="security-policies-and-recommendations"></a>Recomendações e políticas de segurança
Uma política de segurança define o conjunto de Olá de controlos, que são recomendados para recursos dentro Olá especificado subscrição. No Centro de segurança, é possível definir políticas de acordo com requisitos de segurança tooyour da empresa e do tipo de Olá de aplicações ou sensibilidade dos dados de Olá.

As políticas que estão ativadas no nível de subscrição de Olá automaticamente propagadas tooall grupos de recursos dentro da subscrição Olá, conforme mostrado no Olá diagrama a seguir:

![Políticas de Segurança](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig2-newUI.png)

> [!NOTE]
> Se precisar de tooreview as políticas que foram alteradas, pode utilizar [registos de auditoria do Azure](https://blogs.msdn.microsoft.com/cloud_solution_architect/2015/03/10/audit-logs-for-azure-events/). As alterações de políticas são sempre registadas nos Registos de Auditoria do Azure.
> 
> 

### <a name="security-recommendations"></a>Recomendações de segurança
Antes de configurar as políticas de segurança, consulte cada uma das Olá [recomendações de segurança](security-center-recommendations.md)e determinar se estas políticas são adequadas às suas várias subscrições e grupos de recursos. Também é importante toounderstand que deverão ser executadas tooaddress [recomendações de segurança](https://docs.microsoft.com/en-us/azure/security-center/security-center-recommendations) e quem na organização será o responsável pela monitorização para novas recomendações e tendo Olá necessários passos.

O Centro de Segurança irá recomendar que forneça os detalhes de contacto de segurança para a sua subscrição do Azure. Esta informação será utilizada pelo Microsoft toocontact se Olá Microsoft Security Response Center (MSRC) Deteta que os dados de cliente foram acedidos por uma entidade ilícita ou não autorizada. Leitura [fornecer detalhes de contacto de segurança no Centro de segurança do Azure](security-center-provide-security-contact-details.md) para obter mais informações sobre como tooenable esta recomendação.

## <a name="data-collection-and-storage"></a>Armazenamento e recolha de dados
Centro de segurança do Azure utiliza Olá Microsoft Monitoring Agent – isto é Olá mesmo agente utilizado por Olá Operations Management Suite e o serviço de análise de registos – toocollect dados de segurança das suas máquinas virtuais. Os dados recolhidos deste agente serão armazenados nas suas áreas de trabalho do Log Analytics.

### <a name="agent"></a>Agente

Após a recolha de dados está ativada na política de segurança de Olá, Olá Microsoft Monitoring Agent (para [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) ou [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents)) está instalado no suportadas todas as VMs do Azure e de quaisquer novos que são criados.  Se Olá que VM já tem Olá Microsoft Monitoring Agent instalada, o Centro de segurança do Azure irá tirar partido da Olá atual agente foi instalado. processo do agente de Olá é concebida toobe não é INVASIVO e ter um impacto muito mínimo no desempenho da VM.

Olá Microsoft Monitoring Agent para o Windows necessita de utilizar a porta TCP 443. Consulte Olá [artigo de resolução de problemas](security-center-troubleshooting-guide.md) para obter detalhes adicionais.

Se, a determinada altura pretender toodisable recolha de dados, pode desativá-la na política de segurança de Olá. No entanto, uma vez que Olá Microsoft Monitoring Agent pode ser utilizado por outra gestão do Azure e monitorização dos serviços, Olá agente será não ser desinstalado automaticamente quando desativar a recolha de dados no Centro de segurança. Pode desinstalar manualmente o agente de Olá se for necessário.

> [!NOTE]
> toofind uma lista de VMs suportadas, leia Olá [perguntas mais frequentes sobre (FAQ) do Centro de segurança do Azure](security-center-faq.md).
> 

### <a name="workspace"></a>Área de trabalho

Dados recolhidos Olá que Microsoft Monitoring Agent (em nome do Centro de segurança do Azure) será armazenado num workspace(s) análise de registos existente associado à sua subscrição do Azure ou um workspace(s) nova, tendo em Olá conta Georreplicação de Olá VM. 

No portal do Azure Olá, pode procurar toosee uma lista de áreas de trabalho das Log Analytics, incluindo quaisquer criado pelo centro de segurança do Azure. Será criado um grupo de recursos relacionados para as novas áreas de trabalho. Ambos seguirão esta convenção de nomenclatura: 

* Área de trabalho: *DefaultWorkspace-[subscription-ID]-[geo]*
* Grupo de Recursos: *DefaultResouceGroup-[geo]*

Para áreas de trabalho criadas pelo Centro de Segurança do Azure, os dados são retidos durante 30 dias. Para sair áreas de trabalho, retenção baseia-se na área de trabalho Olá escalão de preço.

> [!NOTE]
> Microsoft tornam privacidade de Olá compromissos forte tooprotect e segurança destes dados. Microsoft respeita diretrizes de conformidade e segurança toostrict — desde a codificação toooperating um serviço. Para obter mais informações sobre o processamento de dados e privacidade, leia [Segurança de Dados do Centro de Segurança do Azure](security-center-data-security.md).
> 

## <a name="ongoing-security-monitoring"></a>Monitorização de segurança em curso
Após a configuração inicial e a aplicação das recomendações do Centro de segurança, o passo seguinte Olá é considerar os processos operacionais do Centro de segurança.

tooaccess Centro de segurança de Olá portal do Azure, pode clicar em **procurar** e tipo **Centro de segurança** no Olá **filtro** campo. vistas de Olá que Olá utilizador obtém está de acordo com os filtros de toothese aplicada, o exemplo de Olá abaixo mostra um ambiente com muitos toobe de problemas resolvidos:

![dashboard](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig6.png)

> [!NOTE]
> Centro de segurança não irá interferir com os seus procedimentos operacionais normais, ligados passivamente monitorizar as implementações e facultar recomendações com base nas políticas de segurança de Olá ativada.

Quando a, primeiro optar pelas toouse Centro de segurança para o seu ambiente do Azure atual, certifique-se de que revê todas as recomendações, que podem ser efetuadas no Olá **recomendações** mosaico ou por recurso (**computação** **Redes**, **armazenamento & dados**, **aplicação**).

Assim que abordar todas as recomendações, Olá **prevenção** secção deve estar verde em todos os recursos que foram abordados. Monitorização contínua neste momento torna-se mais fácil, uma vez que apenas realizará ações com base nas alterações nos Olá recursos segurança estado de funcionamento e recomendações de mosaicos.

Olá **deteção** secção é mais reativa, estes são alertas relativos a problemas que estão a ocorrer agora, ou que ocorreram Olá anterior e foram detetados pelos controlos do Centro de segurança e 3rd sistemas de terceiros. Mosaico alertas de segurança de Olá mostrará gráficos de barras que representam o número de Olá de alertas de deteção de ameaças que foram encontradas em cada dia e a respetiva distribuição entre Olá diferentes categorias de gravidade (baixa, média, alta). Para obter mais informações sobre alertas de segurança, leia o artigo [toosecurity está a responder e gerir alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md).

> [!NOTE]
> Pode também tirar partido do Microsoft Power BI toovisualize os dados do Centro de segurança. Leia [Obter informações a partir de dados do Centro de Segurança do Azure com Power BI](security-center-powerbi.md).
> 
> 

### <a name="monitoring-for-new-or-changed-resources"></a>Monitorização de recursos novos ou alterados
A maior parte dos ambientes do Azure são dinâmicos, com recursos novos que são regularmente acelerados ou desacelerados, configurações ou alterações, etc. Centro de segurança ajuda a garantir que têm visibilidade para o estado de segurança de Olá destes recursos novos.

Quando adicionar novos recursos (VMs, bds SQL) tooyour ambiente do Azure, o Centro de segurança irá detetar estes recursos e começar toomonitor a segurança dos mesmos automaticamente. Isto também inclui funções da Web e funções de trabalho PaaS. Se a recolha de dados estiver ativada no Olá [política de segurança](security-center-policies.md), adicionais capacidades de monitorização serão ativadas automaticamente para as máquinas virtuais.

![Áreas principais](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig3-newUI.png)

1. Para máquinas virtuais, clique em **Computação**, na secção **Prevenção**. Quaisquer problemas com a ativação de dados ou recomendações relacionadas aparecerão na Olá **descrição geral** separador, e **recomendações de monitorização** secção.
2. Olá vista **recomendações** toosee que, se existirem, riscos de segurança foram identificados para o recurso novo Olá.
3. É muito comum que, quando novas VMs são adicionadas tooyour ambiente, sistema de operativo apenas Olá inicialmente está instalado. proprietário do recurso Olá poderá necessitar de algum tempo toodeploy outras aplicações que serão utilizadas por estas VMs.  Idealmente, deve conhecer intenção final Olá esta carga de trabalho. Vai toobe um servidor de aplicações? Com base no que esta nova carga de trabalho é toobe contínuo, pode ativar Olá adequado **política de segurança**, que é Olá terceiro passo deste fluxo de trabalho.
4. Como são adicionados novos recursos tooyour ambiente do Azure, é possível que apareçam novos alertas no Olá **alertas de segurança** mosaico. Verifique se existem novos alertas neste mosaico e tome medidas de acordo com as recomendações do Centro de tooSecurity sempre.

Também convém tooregularly Olá o estado do monitor de existente recursos tooidentify alterações de configuração que criaram riscos de segurança, que se desviam das linhas de base recomendadas e alertas de segurança. Comece no dashboard do Centro de segurança de Olá. A partir daí tem três áreas principais tooreview, de forma consistente.

![Operações](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig4-newUI.png)

1. Olá **prevenção** painel secção fornece recursos principais do tooyour acesso rápido. Utilize esta opção toomonitor computação, redes, armazenamento e dados e aplicações.
2. Olá **recomendações** painel permite-lhe recomendações do Centro de segurança tooreview. Durante a monitorização em curso pode considerar que não tem recomendações diariamente, que é normal, uma vez que abordou todas as recomendações na configuração de centro de segurança inicial Olá. Por este motivo, poderá não tenha novas informações nesta secção todos os dias e que apenas tenha tooaccess-la conforme necessário.
3. Olá **deteção** secção pode ser alterado de qualquer um dos bastante frequente ou pouco frequente. Reveja sempre os alertas de segurança e tome medidas com base nas recomendações do Centro de Segurança.

## <a name="incident-response"></a>Resposta a incidentes
Centro de segurança Deteta e alerta-o toothreats à medida que ocorrem. As organizações devem monitorizar a existência de novos alertas de segurança e tomar medidas como tooinvestigate necessário mais ou para remediar o ataque de Olá. Para obter mais informações sobre como funciona a deteção de ameaças do Centro de Segurança, leia [Azure Security Center detection capabilities (Capacidades de deteção do Centro de Segurança do Azure)](security-center-detection-capabilities.md).

Embora este artigo não tem tooassist intenção Olá a criar o seus próprios plano de resposta a incidentes, iremos toouse Microsoft Azure Security Response no ciclo de vida de nuvem de Olá como foundation Olá para fases de resposta a incidentes. fases de Olá são apresentadas no Olá diagrama a seguir:

![Atividade suspeita](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-1.png)

> [!NOTE]
> Pode utilizar Olá National Institute of Standards e Technology (NIST) [incidente processamento manual de segurança computador](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf) como uma referência tooassist a criar o seu próprio.
> 

Pode utilizar alertas do Centro de segurança durante Olá seguintes fases:

* **Detetar**: identifique uma atividade suspeita num ou mais recursos. 
* **Avaliar**: efetuar Olá avaliação inicial tooobtain mais informações sobre a atividade suspeita Olá.
* **Diagnosticar**: utilizar Olá remediação passos tooconduct Olá procedimento técnico tooaddress Olá problema.

Cada alerta de segurança faculta informações que podem ser utilizadas toobetter compreender Olá natureza do ataque Olá e sugerir possíveis mitigações. Alguns alertas também fornecem ligações tooeither mais origens de informações ou tooother de informação no Azure. Pode utilizar as informações de Olá fornecidas para investigação adicional e atenuação toobegin e também poderá procurar os dados relacionados com segurança armazenados na sua área de trabalho.

Olá exemplo seguinte mostra uma atividade suspeita de RDP a ocorrer:

![Atividade suspeita](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-ga.png)

Como pode ver, este painel mostra detalhes sobre o tempo de Olá que Olá ataque local, Olá nome de anfitrião de origem, Olá VM visada e também fornece passos de recomendação. Em alguns Olá circunstâncias informações da origem do ataque Olá podem estar vazios. Leia [Informações da Origem em Falta nos Alertas do Centro de Segurança do Azure](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/25/missing-source-information-in-azure-security-center-alerts/) para obter mais informações acerca deste tipo de comportamento.

No Olá [como tooLeverage Olá Centro de segurança do Azure e do Microsoft Operations Management Suite para uma resposta a incidentes](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703) vídeo pode ver alguns demonstrações que podem ajudá-lo toounderstand como o Centro de segurança podem ser utilizado em cada um dessas fases.

> [!NOTE]
> Leitura [Leveraging Centro de segurança do Azure para a resposta a incidentes](security-center-incident-response.md) para obter mais informações sobre como tooassist de capacidades de centro de segurança toouse que durante a sua resposta a incidentes processar. 
> 
> 

## <a name="see-also"></a>Consultar também
Neste documento, aprendeu como tooplan para adoção do Centro de segurança. toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:

* [Gerir e responder a alertas de toosecurity no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md)
* [Monitorização de estado de funcionamento de segurança no Centro de segurança do Azure](security-center-monitoring.md) — Saiba como toomonitor Olá estado de funcionamento dos seus recursos Azure.
* [Monitorizar soluções de parceiros com o Centro de segurança do Azure](security-center-partner-solutions.md) — Saiba como toomonitor Olá estado de funcionamento das suas soluções de parceiros.
* [FAQ do Centro de segurança do Azure](security-center-faq.md) – encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.
* [Blogue de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – Encontre mensagens do blogue acerca da segurança e conformidade do Azure.

