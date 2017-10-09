---
title: "Relatórios na conta de utilizador automática do Azure Active Directory aprovisionamento tooSaaS aplicações | Microsoft Docs"
description: "Saiba como toocheck Olá Estado automático da conta de utilizador aprovisionamento tarefas e como tootroubleshoot Olá aprovisionamento de utilizadores individuais."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: asmalser-msft
ms.openlocfilehash: 5dcf9e5dbaacf3a2c81183c5d81e331858671b86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-reporting-on-automatic-user-account-provisioning"></a>Tutorial: Relatórios sobre o aprovisionamento da conta de utilizador automáticas


Azure Active Directory inclui uma [conta de utilizador do serviço de fornecimento](active-directory-saas-app-provisioning.md) que ajuda a automatizar Olá aprovisionamento anular aprovisionamento de contas de utilizador em aplicações SaaS e outros sistemas, para fins de Olá do ciclo de vida de identidade de ponto a ponto gestão. AD do Azure suporta conectores para todas as aplicações de Olá e sistemas operativos na Olá "Em destaque" secção de Olá de aprovisionamento de utilizadores de previamente integradas [Galeria de aplicações do Azure AD](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured).

Este artigo descreve como o estado de Olá toocheck de aprovisionamento de tarefas após ter sido definidos até e como tootroubleshoot Olá aprovisionamento de utilizadores individuais e grupos.

## <a name="overview"></a>Descrição geral

Os conectores de aprovisionamento são principalmente configurar e configuradas utilizando Olá [portal de gestão do Azure](https://portal.azure.com), pelos seguinte Olá [fornecido documentação](active-directory-saas-tutorial-list.md) para aplicação olá onde da conta de utilizador aprovisionamento é assim o desejar. Depois de configurada e em execução, o aprovisionamento de tarefas para uma aplicação pode ser comunicado utilizando um dos dois métodos:

* **Portal de gestão do Azure** -este artigo descreve principalmente ao obter informações de relatório do Olá [portal de gestão do Azure](https://portal.azure.com), que fornece tanto um relatório de resumo de aprovisionamento, bem como detalhada de aprovisionamento auditoria de registos para uma determinada aplicação.

* **API de auditoria** -Azure Active Directory também fornece uma API que permite a obtenção programática de Olá detalhadas aprovisionamento registos de auditoria de auditoria. Consulte [auditoria do Azure Active Directory referência da API](active-directory-reporting-api-audit-reference.md) para toousing específico documentação esta API. Embora este artigo não abrange especificamente como toouse Olá API, de detalhe tipos de Olá de eventos que são registados no registo de auditoria Olá de aprovisionamento.

### <a name="definitions"></a>Definições

Este artigo utiliza Olá seguintes termos de licenciamento, definidos abaixo:

* **Sistema de origem** -sincroniza a partir de repositório Olá de utilizadores que Olá o serviço de aprovisionamento do Azure AD. Azure Active Directory é Olá origem para o maioria Olá de pré-integrado aprovisionamento conectores, no entanto, existem algumas exceções (exemplo: a sincronização de entrada do Workday).

* **Sistema de destino** -sincroniza para o repositório de Olá de utilizadores que Olá o serviço de aprovisionamento do Azure AD. Isto é, geralmente, uma aplicação SaaS (exemplos: Salesforce, ServiceNow, Google Apps, Dropbox para empresas), mas, em alguns casos, pode ser um sistema local como o Active Directory (exemplo: a sincronização de entrada do Workday tooActive diretório).


## <a name="getting-provisioning-reports-from-hello-azure-management-portal"></a>Obter relatórios a partir do portal de gestão do Azure de Olá de aprovisionamento

tooget as informações de relatório para uma aplicação específica, o aprovisionamento inicial, iniciando Olá [portal de gestão do Azure](https://portal.azure.com) e navegação toohello Enterprise aplicação para o qual o aprovisionamento estiver configurado. Por exemplo, se estiver a aprovisionar utilizadores tooLinkedIn Elevate, detalhes da aplicação Olá navegação caminho toohello é:

**Azure Active Directory > aplicações da empresa > todas as aplicações > LinkedIn elevar**

Aqui, pode aceder ao relatório de resumo de aprovisionamento de Olá e registos de auditoria de aprovisionamento Olá, ambos descrito abaixo.


### <a name="provisioning-summary-report"></a>Relatório de resumo de aprovisionamento

relatório de resumo de aprovisionamento de Olá está visível no Olá **aprovisionamento** separador fornecido a aplicação. Está localizado na seção de detalhes de sincronização de Olá por baixo **definições**e fornece Olá seguintes informações:

* Olá número total de utilizadores e / grupos que foram sincronizadas e estão atualmente no âmbito de aprovisionamento entre o sistema de origem Olá e sistema de destino Olá.

* Olá última hora Olá sincronização foi executada. As sincronizações ocorram, normalmente, a cada 40 de 20 minutos, depois de uma sincronização completa foi concluída.

* Se pretende ou não uma sincronização completa inicial foi concluída.

* Se pretende ou não Olá processo de aprovisionamento foi colocado em quarentena, não sendo o motivo de Olá para o estado de quarentena de Olá por exemplo, (toocommunicate falha com o sistema de destino devido a credenciais de administrador tooinvalid)

relatório de resumo de aprovisionamento de Olá deve ser Olá primeiro local Administradores aspeto toocheck no estado de funcionamento operacional do Olá da tarefa de aprovisionamento de Olá.

 ![Relatório de resumo](./media/active-directory-saas-provisioning-reporting/summary_report.PNG)

### <a name="provisioning-audit-logs"></a>Aprovisionamento de registos de auditoria
Todas as atividades executadas pelo serviço de fornecimento de Olá são registadas nos registos de auditoria de Olá do Azure AD, que podem ser visualizados no Olá **registos de auditoria** separador em Olá **aprovisionamento da conta** categoria. Os tipos de eventos de atividade registados incluem:

* **Importar eventos** -um evento de "Importar" é registado sempre serviço aprovisionamento Olá do Azure AD obtém informações sobre um grupo ou utilizador individual de um sistema de origem ou o sistema de destino. Durante a sincronização, os utilizadores são obtidos a partir sistema de origem Olá em primeiro lugar, com os resultados de Olá registados como "Importar" eventos. Olá correspondentes IDs de Olá obtida utilizadores, em seguida, são consultados contra toocheck de sistema de destino Olá, caso existam, com os resultados de Olá também registados como "Importar" eventos. Estes eventos de registo todos os atributos de utilizador mapeada e os respetivos valores que foram vistos pelo serviço de aprovisionamento de Olá do Azure AD no momento de Olá do evento de Olá. 

* **Eventos de regra de sincronização** - estes eventos de relatório nos resultados de Olá de regras de mapeamento de atributos de Olá e qualquer configurado filtros de âmbito, depois de serem importados e avaliados a partir dos sistemas de origem e destino Olá dados do utilizador. Por exemplo, se um utilizador num sistema de origem é considerado toobe no âmbito de aprovisionamento e considerado toonot existe no sistema de destino Olá, em seguida, este evento regista que Olá utilizador será aprovisionado no sistema de destino Olá. 

* **Exportar eventos** -um evento de "exportação" é registado sempre serviço aprovisionamento Olá do Azure AD escreve um utilizador conta ou grupo objeto tooa sistema de destino. Estes eventos de registo todos os atributos de utilizador e os respetivos valores que foram escritas Olá serviço de aprovisionamento do Azure AD no momento de Olá do evento de Olá. Se tiver ocorrido um erro ao escrever Olá utilizador conta ou grupo objeto toohello sistema de destino, será apresentado aqui.

* **Processar os eventos de caução** -escrows processo ocorrerem ao hello aprovisionamento do serviço detetar uma falha ao tentar uma operação e começa a operação de Olá tooretry num intervalo de término de tempo. Um evento de "caução" é registado sempre que foi extinguida uma operação de aprovisionamento.

Quando observar os eventos de aprovisionamento de um utilizador individual, Olá normalmente ocorrem eventos pela seguinte ordem:

1. Evento de importação: utilizador obtido a partir do sistema de origem Olá.

2. Evento de importação: o sistema de destino é consultado toocheck quanto à existência de Olá do utilizador Olá obtido.

3. Evento de regra de sincronização: os dados de utilizador de sistemas de origem e de destino são avaliados em comparação com o atributo de Olá configurada regras de mapeamento e toodetermine de filtros de âmbito que ação, se existirem, deve ser efetuada.

4. Exportar eventos: se o evento de regra de sincronização de Olá ditado que deve ser uma ação efetuada (por exemplo, adicionar, atualizar, eliminar), em seguida, Olá os resultados da ação de Olá são registados num evento de exportação.

![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-provisioning-reporting/audit_logs.PNG)


### <a name="looking-up-provisioning-events-for-a-specific-user"></a>Procurar o aprovisionamento de eventos para um utilizador específico

Olá caso de utilização mais comum para registos de auditoria de aprovisionamento de Olá é Olá toocheck estado de uma conta de utilizador individuais de aprovisionamento. toolook os eventos de aprovisionamento último Olá para um utilizador específico:

1. Aceda toohello **registos de auditoria** secção.

2. De Olá **categoria** menu, selecione **aprovisionamento da conta**.

3. No Olá **intervalo de datas** menu, intervalo de datas Olá selecione pretende toosearch,

4. No Olá **pesquisa** barra, introduza o ID de utilizador de Olá do utilizador Olá desejar toosearch para. formato de Olá do valor de ID deve corresponder ao que selecionou como Olá primário ID correspondente na configuração de mapeamento de atributos de Olá (por exemplo, userPrincipalName ou empregado ID número). valor de ID de Olá necessário vai estar visível na coluna de destino (s) de Olá.

5. Prima Enter toosearch. Olá aprovisionamento eventos mais recente será devolvido pela primeira vez.

6. Se os eventos são devolvidos, tenha em atenção de que tipos de atividades de Olá e foi concluída com êxito ou falha. Se não existem resultados são devolvidos, em seguida, significa Olá utilizador não existe, ou ainda não foi detetada pelo Olá processo de aprovisionamento, se uma sincronização completa ainda não foi concluído.

7. Clique em eventos individuais detalhes tooview expandido, incluindo todas as propriedades de utilizador que foram obtidas, avaliadas ou escritas como parte do evento de Olá.


### <a name="tips-for-viewing-hello-provisioning-audit-logs"></a>Sugestões para a visualização de registos de auditoria de aprovisionamento de Olá

Para melhor legibilidade no Olá portal do Azure, selecione Olá **colunas** botão e escolha estas colunas:

* **Data** -mostra Olá data Olá evento ocorreu.
* **Destino (s)** -mostra Olá nome e o utilizador ID da aplicação que estão assuntos Olá do evento de Olá.
* **Atividade** -Olá o tipo de atividade, conforme descrito anteriormente.
* **Estado** - se o evento de Olá concluída com êxito ou não.
* **Motivo do estado** -um resumo do que aconteceu no Olá eventos de aprovisionamento.


## <a name="troubleshooting"></a>Resolução de problemas

Olá registos de auditoria e relatório de resumos de aprovisionamento desempenha um papel chave ajudar os administradores a resolver problemas de aprovisionamento da conta de utilizador vários.

Para obter orientações com base no cenário sobre tootroubleshoot automática aprovisionamento de utilizadores, consulte [problemas de configuração e o aprovisionamento de aplicações de tooan utilizadores](active-directory-application-provisioning-content-map.md).


## <a name="additional-resources"></a>Recursos Adicionais

* [Gerir o aprovisionamento da conta de utilizador para aplicações da empresa](active-directory-enterprise-apps-manage-provisioning.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)
