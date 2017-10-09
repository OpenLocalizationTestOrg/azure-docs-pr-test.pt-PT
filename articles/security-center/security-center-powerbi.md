---
title: "aaaGet conhecimentos aprofundados sobre dados do Centro de segurança do Azure com Power BI | Microsoft Docs"
description: "Olá pacote de conteúdos do Power BI do Centro de segurança do Azure torna mais fácil toofind alertas de segurança, recomendações, recursos atacados e tendências, com base num conjunto de dados que foi criado para o seu relatório."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 0ded6bc7-52e8-43b4-8940-0bee137526e3
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: af68aef626034fe03d793c36b515a3f26619e5f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-insights-from-azure-security-center-data-with-power-bi"></a>Obter informações a partir de dados do Centro de Segurança do Azure com Power BI
Olá [Dashboard do Power BI](http://aka.ms/azure-security-center-power-bi) para o Centro de segurança do Azure permite-lhe toovisualize, analisar e filtrar recomendações e alertas de segurança a partir de qualquer lugar, incluindo o seu dispositivo móvel. Utilize as tendências do Olá Power BI dashboard tooreveal e padrões de ataques – veja alertas de segurança por recurso ou endereço IP de origem e riscos de segurança não abordados por recurso ou idade.

Também pode misturar recomendações e alertas de segurança do Centro de Segurança com outros dados de formas interessantes, por exemplo, utilizando dados dos [Registos de Auditoria do Azure](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) e da [Auditoria da Base de Dados SQL do Azure](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/). Dashboards do Power BI e também pode exportar esta tooExcel de dados para facilmente relatórios acerca do Estado de segurança de Olá dos seus recursos de nuvem.

## <a name="using-azure-security-center-dashboard-tooaccess-power-bi"></a>Utilizar o Centro de segurança do Azure dashboard tooaccess Power BI
Também pode utilizar relatórios do Power BI tooaccess Olá Centro de segurança do Azure dashboard. Siga Olá passos tooperform esta tarefa:

1. No Olá **Centro de segurança do Azure** dashboard, clique em **Power BI** botão.

    ![Ligar através do Power BI do Centro de segurança tooAzure](./media/security-center-powerbi/security-center-powerbi-fig1-1-newUI-2017.png)
2. Olá **Power BI** painel abre no lado direito de Olá, conforme mostrado no seguinte ecrã de Olá:

    ![Ligar através do Power BI do Centro de segurança tooAzure](./media/security-center-powerbi/security-center-powerbi-fig1-new11-2017.png)
3. Se estiver a criar dashboard do Power BI Olá para Olá pela primeira vez, pode escolher uma das seguintes Olá opções na Olá **explorar no Power BI** painel:

   * **Dashboard de conhecimentos de segurança**: Escolha esta opção se quiser toocreate um dashboard que inclua o estado de segurança, threads e deteções. Esta opção é mais comum para a função DevOps que é responsável por analisar o respetivo estado de proteção e os alertas detetados nas subscrições.
   * **Dashboard de gestão de políticas**: Escolha esta opção se pretender que a política de gestão e de imposição de tooexplore.  Esta opção é mais comum para os departamentos de TI centrais mais focados no setor governativo. Podem utilizar este visibilidade de toogain de dashboard e conhecimentos aprofundados no cumprimento das políticas de segurança na respetiva organização.
   * Se já tiver um dashboard do Power BI, clique em **aceda tooyour dashboard do Power BI atual**.
4. Para efeitos deste exemplo, clique na opção **Dashboard de conhecimentos de segurança aprofundados**. Se este for Olá pela primeira vez, está a criar um dashboard do Power BI para o Centro de segurança que é-lhe pedido que o pacote de conteúdos do tooinstall Olá. Clique em **obter** botão no Olá **pacotes de conteúdo do Power BI** janela conforme mostrado no seguinte ecrã de Olá:

    ![Dashboard de Conhecimentos de Segurança Aprofundados do Centro de Segurança do Azure](./media/security-center-powerbi/security-center-powerbi-fig1-new3.png)
5. Olá **ligar conhecimentos aprofundados segurança do Centro de segurança do tooAzure** aparecer a janela. Certifique-se de que Olá **autenticação** método é **oAuth2** conforme mostrado abaixo e clique em **sessão** botão.

    ![Autenticação](./media/security-center-powerbi/security-center-powerbi-fig1-new4.png)
6. Poderá ser-lhe pedido tooauthenticate novamente com as suas credenciais do Azure. O seu dashboard será criado assim que se autenticar. Assim que for criado o dashboard de Olá, ver um relatório com uma estrutura semelhante Olá, conforme mostrado no seguinte ecrã de Olá:

    ![Dashboard do Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new5.png)

> [!NOTE]
> Uma atualização do relatório de Olá é o local de tootake agendado numa base diária. No caso de ocorrer uma falha nesta atualização, leia [potenciais problemas de atualização com o Power BI do Centro de segurança do Azure de Olá](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/), para obter mais informações sobre como tootroubleshoot.
>
>

Aqui pode ver o número de Olá de alertas de segurança e as recomendações, bem como Olá número de VMs, bases de dados SQL do Azure e os recursos de rede monitorizados pelo centro de segurança do Azure.

Um centro de segurança de tooAzure ligação redireciona toohello portal do Azure. Olá gráficos fazem como que toovisualize fácil informações sobre as recomendações de segurança e os alertas, incluindo:

* Estado de Segurança do Recurso
* Recomendações Pendentes
* Recomendações da VM
* Alertas ao longo do tempo
* Recursos atacados
* IPs atacados

Atrás de cada gráfico existem informações adicionais. Selecione um mosaico toosee obter mais informações. Por exemplo, Olá **estado de segurança de recursos** mosaico mostra-lhe detalhes adicionais acerca das recomendações pendentes pelos recursos conforme mostrado no seguinte ecrã de Olá:

![Recomendações](./media/security-center-powerbi/security-center-powerbi-fig1-new6.png)

Se clicar em qualquer linha deste gráfico, Olá outros vai toogray enviados e foco apenas em Olá um que selecionou. tooreturn toohello dashboard, clique em **Centro de segurança do Azure** em Olá **Dashboards** opção no painel esquerdo Olá desta página.

> [!NOTE]
> Se quiser toocustomize os seus relatórios adicionando campos adicionais ou alterar os efeitos visuais existentes, pode editar o relatório de Olá. Leia [Interagir com um relatório na Vista de Edição no Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) para obter mais informações.
>
>

Olá **alertas ao longo do tempo, recursos atacados** e **IPs atacantes** mosaicos terão o resultado semelhante Olá quando clica em cada um deles. Isto acontece porque o relatório de Olá agrega as informações relativas essas três variáveis e denomina- **recursos sob ataque** conforme mostrado no seguinte ecrã de Olá:

![Recursos sob ataque](./media/security-center-powerbi/security-center-powerbi-fig1-new7.png)

Neste momento também pode guardar uma cópia deste relatório, imprimi-la ou publicá-la na web Olá utilizando Olá opções disponíveis no Olá **ficheiro** menu.

![Menu Ficheiro](./media/security-center-powerbi/security-center-powerbi-fig8.png)

## <a name="exploring-your-azure-security-center-data-with-power-bi-services"></a>Explorar os dados do Centro de Segurança do Azure com os serviços Power BI
Ligar toohello [serviços do pacote de conteúdos do Power BI](https://msit.powerbi.com/groups/me/getdata/services) no Power BI e executar Olá os seguintes passos:

1. No Olá **pacote de conteúdos do Power BI** janela verá duas opções conforme é mostrado abaixo.

    ![Pacote de conteúdo para o Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new.png)

   > [!NOTE]
   > Se já executada Olá primeira parte deste artigo, verá apenas uma opção, o que é a gestão de política do Centro de segurança do Azure.
   >
   >
2. Para o objetivo de Olá deste exemplo, clique em **obter** no Olá **gestão de política do Centro de segurança do Azure** mosaico.
3. No Olá **ligar tooAzure gestão de política do Centro de segurança** janela, tooselect se disponibilizar **oAuth2** em **método de autenticação** menu pendente, conforme mostrado abaixo e clique em **Sessão** botão.

    ![Janela de Gestão de Políticas](./media/security-center-powerbi/security-center-powerbi-fig1-new8.png)
4. Será redirecionado tooan página de autenticação onde deve escrever as credenciais de Olá que está a utilizar o Centro de segurança de tooAzure tooconnect. Após a conclusão do processo de autenticação de Olá, Power BI inicia a importação dos dados toobuild os seus relatórios. Durante este tempo, pode ver Olá seguir a mensagem no canto direito de Olá do seu browser:

    ![Ligar através do Power BI do Centro de segurança tooAzure](./media/security-center-powerbi/security-center-powerbi-fig4.png)

   > [!NOTE]
   > Quando o dashboard de Olá está a ser criada para Olá pela primeira vez, poderá demorar mais do que o habitual, principalmente para cenários em que tiver várias subscrições.
   >
   >
5. Depois de terminar o processo de Olá, o dashboard do Power BI do Centro de segurança do Azure será carregado com Olá **gestão de políticas** reportar toohello semelhante mostrado abaixo:

    ![Dashboard de Gestão de Políticas](./media/security-center-powerbi/security-center-powerbi-fig1-new9.png)

## <a name="see-also"></a>Consultar também
Neste documento, aprendeu como toouse Power BI no Centro de segurança do Azure. toolearn mais acerca do Centro de segurança do Azure, consulte o artigo seguinte Olá:

* [Guia de operações e planeamento do Centro de segurança do Azure](security-center-planning-and-operations-guide.md) — Saiba como tooplan adoção do Centro de segurança do Azure.
* [Definir políticas de segurança no Centro de segurança do Azure](security-center-policies.md) — Saiba como tooconfigure definições de segurança no Centro de segurança do Azure
* [Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md) — Saiba como alertas de toosecurity toomanage e respondeu
* [FAQ do Centro de segurança do Azure](security-center-faq.md) – encontre as perguntas mais frequentes sobre a utilização do serviço de Olá
* [Blogue de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – Encontre mensagens do blogue acerca da segurança e conformidade do Azure
