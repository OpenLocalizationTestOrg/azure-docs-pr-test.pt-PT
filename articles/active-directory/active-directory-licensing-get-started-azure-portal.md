---
title: aaaGet iniciado com o licenciamento no Azure Active Directory | Microsoft Docs
description: "O Azure Active Directory funciona de licenciamento, como tooget iniciado com as melhores práticas"
services: active-directory
keywords: Licenciamento do Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 268dab806b8b959790341d630a0355c6a43871d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="license-yourself-and-your-users-in-azure-active-directory"></a>Licença de si e aos utilizadores no Azure Active Directory

> [!div class="op_single_selector"]
> * [Instruções de portais do Azure](active-directory-licensing-get-started-azure-portal.md)
> * [Obter informações do portal clássica do Azure](active-directory-licensing-what-is.md)
>
>

Azure Active Directory (Azure AD) é uma identidade como uma solução de serviço (IDaaS) e a plataforma da Microsoft. Azure AD é oferecido na edições diferentes do serviço:

* Azure Active Directory livre, que está disponível com o serviço da Microsoft, tais como o Office 365, Dynamics, Microsoft Intune ou do Azure. Azure AD não gera quaisquer taxas de consumo neste modo.

* Azure AD pagamento edições, tal como:
  - Enterprise Mobility + Security 
  - O Azure AD Premium, (P1 e P2)
  - Azure AD Basic
  - Multi-Factor Authentication do Azure

Como muitas do Microsoft online services, mais do Azure AD paga versões são entregues através de elegibilidade por utilizador dado que estão no Office 365, o Microsoft Intune e o Azure AD. Nestes casos, compra do serviço de Olá é representada por uma ou mais subscrições e cada subscrição inclui algumas licenças prepurchased no seu inquilino. É conseguida elegibilidade por utilizador por:

* Atribuir uma licença. 
* Criar uma ligação entre o utilizador Olá e produto Olá.
* Componentes do serviço de Olá ativar para o utilizador Olá.
* Consumir um Olá pago licenças.

[Experimente agora o Azure AD Premium.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

Para uma perspetiva geral das capacidades do serviço do Azure AD, consulte [Novidades do Azure AD?](active-directory-whatis.md). Para obter mais informações, consulte a nossa [página de contratos de nível de serviço](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/).

> [!NOTE]
> As subscrições do Azure de pay as you go permitem a criação de recursos do Azure e mapeá-los tooyour método de pagamento. Não existem nenhum contagens de licença associadas à subscrição Olá. Quando conceder que um toooperate de permissão de utilizador nos recursos do Azure mapeada toohello subscrição, estão associados à subscrição Olá e podem gerir os recursos de subscrição.

## <a name="how-does-azure-active-directory-licensing-work"></a>Como funciona o licenciamento do Azure Active Directory?

Baseada no licenciamento do Azure AD serviços trabalho por ativar uma subscrição no seu inquilino de serviço do Azure AD. Depois de subscrição de Olá está ativa, capacidades do serviço de Olá são geridas por administradores do Azure AD e utilizadas pelos utilizadores licenciados.

### <a name="manage-subscription-information"></a>Gerir informações de subscrição

Quando compra do Enterprise Mobility + de segurança, Azure AD Premium ou do Azure AD Basic, o inquilino é atualizado com a subscrição Olá, incluindo o respetivo período de validade e pago licenças. Informações da sua subscrição, incluindo Olá número de licenças atribuídas ou disponíveis, estão disponíveis através do portal do Azure de Olá: em **do Azure Active Directory**, abra Olá **licenças** mosaico Olá diretório específico. Olá **licenças** painel também é Olá melhor local toomanage suas atribuições de licenças.

Cada subscrição é composta por um ou mais planos de serviço, como o Azure AD, multi-factor Authentication, Intune, Exchange Online ou o SharePoint Online.  Gestão de licenças do Azure AD *não* requer a gestão de nível de plano de serviço. Office 365 difere porque depende este avançadas modo toomanage acesso tooincluded dos serviços de configuração. Azure AD baseia-se nas funcionalidades de tooenable configuração in-service e gerir as permissões individuais.

> [!IMPORTANT]
> O Azure AD Premium, Azure AD Basic e Enterprise Mobility + subscrições de segurança são inquilino e directory limitados tootheir aprovisionado. Subscrições não podem ser divididas entre diretórios ou utilizadores tooentitle utilizado noutros diretórios. Mover uma subscrição entre diretórios for possível, mas necessita de submeter um pedido de suporte ou cancelamento e repurchase para direcionam compras.
>
> Quando do Azure AD ou o Enterprise Mobility + Security é compradas através de uma subscrição de licenciamento em Volume e quando contrato Olá inclui outros serviços Online da Microsoft (por exemplo, o Office 365), ativação ocorre automaticamente. 

### <a name="assign-licenses"></a>Atribuir licenças

Apesar de obter uma subscrição de que todos os terá tooconfigure paga capacidades, terá de distribuir ainda licenças para o Azure AD paga toousers de funcionalidades. Qualquer utilizador que deve ter acesso tooor que é gerido através de um Azure AD paga funcionalidade tem de ser atribuída uma licença. Atribuição de licenças é um mapeamento entre um utilizador e um serviço adquirido, como o Azure AD Premium, Basic ou Enterprise Mobility + Security.


Os utilizadores no seu diretório devem ter uma licença de gestão pode ser conseguido através de: 

* Atribuir licenças toogroups no Olá [portal do Azure](active-directory-licensing-whatis-azure-portal.md).
* Atribuir licenças diretamente toousers título do portal Olá, PowerShell ou APIs. 

Quando estiver a atribuir grupo de tooa de licenças, todos os membros do grupo recebem uma licença. Se os utilizadores são adicionados ou removidos do grupo de Olá, licença adequada Olá é atribuída ou removida. Atribuição de grupo, pode utilizar qualquer tooyou disponíveis da gestão de grupo e que sejam consistentes com a atribuição baseada em grupo tooapplications.

Pode utilizar [atribuição com base no grupo de licenças](active-directory-licensing-whatis-azure-portal.md) tooset segurança regras como seguinte Olá:
* Todos os utilizadores no seu diretório obtém automaticamente uma licença
* Todas as pessoas com cargo adequado Olá obtém uma licença
* Pode delegar gestores tooother de decisão de Olá na organização de Olá (utilizando [grupos self-service](active-directory-accessmanagement-self-service-group-management.md))

Para ver um debate detalhado dos toogroups de atribuição de licença, incluindo avançadas cenários e o Office 365 licenciamento cenários, consulte [atribuir licenças toousers através da associação a grupos no Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md).

## <a name="get-started-with-azure-ad-licensing"></a>Começar com o licenciamento do Azure AD

Introdução ao Azure AD é fácil. Pode criar o diretório como parte da assinatura de cópia de segurança para sempre um [avaliação gratuita do Azure](https://azure.microsoft.com/offers/ms-azr-0044p/).

Olá melhores práticas seguintes podem ajudar a assegurar que o seu inquilino está alinhado com outros serviços Microsoft, que poderá estar a consumir e com os objetivos de serviço Olá:

- Se já estiver a utilizar qualquer um dos Olá serviços organizacionais da Microsoft, já tem um inquilino do Azure AD. É Olá toouse útil que mesmo inquilino para outros serviços, para que a gestão de identidades de núcleos, incluindo aprovisionamento e híbridos-início de sessão único (SSO), pode ser utilizado em serviços Olá. Com início de sessão, os utilizadores beneficiam das capacidades avançadas de Olá nos vários serviços Olá. Assim, se decidir toobuy um serviço do Azure AD pagamento para a sua força de trabalho, recomendamos que utilize Olá mesmo inquilino novamente.

- Recomendamos que utilize um novo inquilino no Olá portal do Azure, se estiver a planear:
  - Utilize o Azure AD para outro conjunto de utilizadores (por exemplo, parceiros e clientes).
  - Avalie a serviços do Azure AD em isolamento do seu serviço de produção.
  - Configure um ambiente sandbox para os serviços.

  novo diretório de Olá é criado com a sua conta como um utilizador externo com permissões de administrador global. Quando inicia sessão no portal do Azure com esta conta de toohello, pode ver este inquilino e aceder a todas as tarefas de administração.

> [!NOTE]
> Azure AD suporta "os utilizadores convidados," que são contas de utilizador um inquilino do Azure AD que foram criadas através de uma conta Microsoft ou uma identidade do Azure AD a partir de outro inquilino. portal de administração de Olá do Office 365 não suporta atualmente estes utilizadores. Convidados os utilizadores com contas Microsoft não estão tooaccess capaz de portal de administração de Olá do Office 365, enquanto os utilizadores convidados de outros inquilinos do Azure AD são ignorados. No caso desta última opção Olá, apenas Olá conta local do utilizador, no Olá do Azure AD ou o inquilino do Office 365 em que foi originalmente criado utilizador Olá, está acessível.

### <a name="select-one-or-more-license-trials"></a>Selecione um ou mais avaliações de licença

Pode ativar um Azure AD Premium ou Enterprise Mobility + subscrição de avaliação de segurança em **do Azure Active Directory** &gt; **início rápido**.

![Selecione uma versão de avaliação de licença](media/active-directory-licensing-get-started-azure-portal/select-a-license-trial.png)

Avaliação licenças estão disponíveis no Olá **licenças** painel.

### <a name="assign-licenses-toousers-and-groups"></a>Atribuir licenças toousers e grupos

Depois de subscrição de Olá está ativa, deve atribuir uma licença tooyourself. Em seguida, atualize Olá tooensure de browser que está a ver todas as funcionalidades de Olá. Olá passo seguinte consiste em tooassign licenças toohello os utilizadores que necessitam de funcionalidades do acesso toopaid do Azure AD. Conforme descrito em [atribuir licenças](#assign-licenses), uma forma fácil de tooassign licenças é grupo de Olá tooidentify que representa Olá pretendido público-alvo e atribua Olá tooit de licença. Desta forma, os utilizadores que são adicionados ou removidos do grupo de Olá ao longo do respetivo ciclo de vida são atribuídos ou removidos da licença de Olá, respetivamente.

> [!NOTE]
> Alguns serviços da Microsoft não estão disponíveis em todas as localizações. Antes de uma licença pode ser atribuída tooa utilizador, administrador Olá tem de especificar Olá **localização de utilização** propriedade para o utilizador Olá. Pode definir esta propriedade em **utilizador** &gt; **perfil** &gt; **definições** no Olá portal do Azure. Quando utilizar a atribuição do grupo de licenças, qualquer utilizador cuja localização de utilização não está especificada herda localização Olá do diretório de Olá.

tooassign uma licença, em **do Azure Active Directory** &gt; **licenças** &gt; **todos os produtos**, selecione um ou mais produtos e, em seguida, selecione **Atribuir** na barra de comandos Olá.

![Selecione um tooassign de licença](media/active-directory-licensing-get-started-azure-portal/select-license-to-assign.png)

Pode utilizar Olá **utilizadores e grupos** toochoose painel planos de vários utilizadores ou grupos toodisable serviço ou produto de Olá. Utilize caixa de pesquisa de Olá no toosearch superior para nomes de utilizador e grupo.

![Selecione um utilizador ou grupo para atribuição de licenças](media/active-directory-licensing-get-started-azure-portal/select-user-for-license-assignment.png)

Quando estiver a atribuir um grupo de tooa de licenças, pode demorar algum tempo antes de todos os utilizadores herdam licença Olá, dependendo do número de Olá de utilizadores no grupo de Olá. Pode verificar o estado de processamento de Olá no Olá **grupo** painel, sob Olá **licenças** mosaico.

![Estado de atribuição de licença](media/active-directory-licensing-get-started-azure-portal/license-assignment-status.png)

Erros de atribuição podem ocorrer durante a atribuição de licença do Azure AD, mas são raros relativamente ao gerir do Azure AD e Enterprise Mobility + produtos de segurança. Potenciais erros de atribuição estão limitados a:
- Conflito de atribuição: quando um utilizador anteriormente foi atribuído uma licença que é incompatível com a licença atual Olá. Neste caso, a atribuição de licenças novo Olá requer remover Olá atual.
- Foi excedido licenças disponíveis: quando o número de Olá de utilizadores nos grupos atribuídos excede licenças disponíveis Olá, o estado de atribuição de um utilizador reflete um tooassign falha devido toomissing licenças.

#### <a name="azure-ad-b2b-collaboration-licensing"></a>Licenciamento e colaboração do Azure AD B2B

Colaboração B2B permite os utilizadores convidados de tooinvite nos serviços do Azure AD inquilino tooprovide acesso tooAzure AD e quaisquer recursos do Azure lhe disponibiliza.  

Não há sem encargos durante inviting B2B utilizadores e atribuir-lhes tooan aplicação no Azure AD. Configurar aplicações too10 por convidado e utilizador 3 relatórios básicos são também livres para os utilizadores de colaboração B2B. Se o utilizador convidado tem as licenças adequadas atribuídas no inquilino do Azure AD do parceiro de Olá, estes irá licenciadas, bem como na sua.

Não é necessário, mas se pretender que as funcionalidades do tooprovide acesso toopaid do Azure AD, os utilizadores de convidado B2B têm de estar licenciados com adequado licenças do Azure AD. Um inquilino convidando com um Azure AD, uma licença paga pode atribuir direitos de utilizador de colaboração B2B os utilizadores convidados de tooan cinco adicionais convidados toohello inquilino. Para cenários e as informações, consulte [colaboração B2B licenciamento orientações](active-directory-b2b-licensing.md).

### <a name="view-assigned-licenses"></a>Licenças de vista atribuída

Uma vista de resumo de licenças atribuídas e disponíveis é apresentada em **do Azure Active Directory** &gt; **licenças** &gt; **todos os produtos**.

![Licença de vista Resumo](media/active-directory-licensing-get-started-azure-portal/view-license-summary.png)

Uma lista detalhada dos atribuído utilizadores e grupos que está disponível quando selecionar um produto específico. Olá **utilizadores licenciados** lista mostra todos os utilizadores atualmente consumir uma licença e indica se o licenciamento Olá foi atribuído diretamente toohello utilizador ou se tiver sido herdado de um grupo.

![Ver detalhes de licença](media/active-directory-licensing-get-started-azure-portal/view-license-detail.png)

Da mesma forma, Olá **licenciado grupos** lista mostra todos os grupos de licenças toowhich foram atribuídas. Selecione um Olá tooopen de utilizador ou grupo **licenças** painel, que mostra todas as licenças atribuídas toothat objeto.

### <a name="remove-a-license"></a>Remover uma licença

tooremove uma licença, visite toohello utilizador ou grupo e abra Olá **licenças** mosaico. Selecione a licença Olá e clique em **remover**.

![Remover uma licença](media/active-directory-licensing-get-started-azure-portal/remove-license.png)

Não não possível remover o herdado por utilizador Olá de um grupo de licenças diretamente. Em vez disso, remova utilizador Olá do grupo de Olá partir do qual estes são herança licenças Olá.

### <a name="extend-trials"></a>Expandir avaliações

As extensões de avaliação para clientes que estão disponíveis como inscrição através do portal do Office 365 de Olá Self-Service. Um administrador de cliente pode aceder toohello portal do Office (acesso depende permissões para o portal do Office Olá) e selecione a versão de avaliação do Olá do Azure AD Premium. Olá clicando em **expandir a avaliação** ligação inicia o processo de extensão de Olá. Um cartão de crédito é obrigatório, mas não está a ser cobrado.

![Expandir uma versão de avaliação Olá portal do Azure](media/active-directory-licensing-get-started-azure-portal/extend-trial-beginning.png)

## <a name="next-steps"></a>Passos seguintes

mais informações sobre como toolearn avançadas cenários para gestão de licenças através de grupos, leia o artigo de Olá [grupo do atribuir licenças tooa](active-directory-licensing-group-assignment-azure-portal.md).

Segue-se informações sobre como tooconfigure e utilizar outro do Azure AD paga funcionalidades:

* [Reposição de palavra-passe self-service](active-directory-manage-passwords.md)
* [Gestão de grupos self-service](active-directory-accessmanagement-self-service-group-management.md)
* [O Azure AD Connect health](active-directory-aadconnect-health.md)
* [Multi-factor Authentication do Azure](../multi-factor-authentication/multi-factor-authentication.md)
* [Direta compra de licenças do Azure AD Premium](http://aka.ms/buyaadp)
