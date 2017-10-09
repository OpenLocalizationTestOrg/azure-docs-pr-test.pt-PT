---
title: "utilizadores do Azure Active Directory aaaLicense Olá portal clássico do Azure | Microsoft Docs"
description: "Descrição de licenciamento do Microsoft Azure Active Directory, como funciona, como tooget iniciado e melhores práticas, incluindo o Office 365, Microsoft Intune e Azure Active Directory Premium e as edições Basic"
services: active-directory
keywords: Licenciamento do Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d769e8c6-7581-43f5-a3b4-de4b1dca2344
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;H1Hack27Feb2017
ms.openlocfilehash: 4d5f244cbee2ae37a30976f70b5d4f21c3516d90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-microsoft-azure-active-directory-licensing-in-hello-azure-classic-portal"></a>O que é Microsoft Azure Active Directory de licenciamento no Olá portal clássico do Azure?

> [!div class="op_single_selector"]
> * [Obter instruções de portais do Azure](active-directory-licensing-get-started-azure-portal.md)
> * [Informações do portal clássica do Azure](active-directory-licensing-what-is.md)
>
>

Azure Active Directory (Azure AD) é a identidade da Microsoft como uma solução de serviço (IDaaS) e a plataforma. Azure AD é oferecido num número de versões de técnicas e funcionais entre o Azure AD livre, o que está disponível com o serviço da Microsoft, tais como o Office 365, Dynamics, Microsoft Intune e do Azure (Azure AD não gerar os eventuais encargos consumo neste modo), tooAzure AD paga versões, como o Enterprise Mobility Suite (EMS), o Azure AD Premium e Basic, bem como o Azure multi-factor Authentication (MFA). Como muitas do Microsoft online services, mais do Azure AD paga versões são entregues através de elegibilidade por utilizador dado que estão no Office 365, o Microsoft Intune e o Azure AD. Nestes casos, compra do serviço de Olá é representada com uma ou mais subscrições e cada subscrição inclui um número de pré-compra de licenças no seu inquilino. Elegibilidade por utilizador é conseguida através da atribuição de licenças, criar uma ligação entre o utilizador Olá e produto Olá, permitindo componentes do serviço Olá para utilizador Olá, e consumir um Olá pago licenças.

> [!IMPORTANT]
> A Microsoft recomenda que gere o Azure AD através de Olá [Centro de administração do Azure AD](https://aad.portal.azure.com) no Olá portal do Azure em vez de utilizar Olá portal clássico do Azure referenciado neste artigo. Para como tooassign funções de administrador no Azure AD de Olá, admin center, consulte [licença si e aos utilizadores no Azure AD](active-directory-licensing-get-started-azure-portal.md).

[Experimente agora premium do Azure AD.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

> [!NOTE]
> Portal de administração do Azure AD é uma parte de Olá portal clássico do Azure. Ao utilizar o Azure AD não requer qualquer compras do Azure, aceder a este portal requer uma subscrição do Azure Active Directory ou uma [subscrição de avaliação do Azure](https://azure.microsoft.com/pricing/free-trial/).
>
>

Para uma perspetiva geral das capacidades do serviço do Azure AD, consulte [Novidades do Azure AD](active-directory-whatis.md).
[Saiba mais sobre os níveis de serviço do Azure AD](https://azure.microsoft.com/support/legal/sla/)

> [!NOTE]
> Subscrições do Azure pay o as you go são diferentes: enquanto também representados no seu diretório, estas subscrições permitir a criação de recursos do Azure e mapeá-los tooyour método de pagamento. Neste caso, não existem nenhum contagens de licença associadas à subscrição Olá. Associação dos utilizadores com subscrição Olá, recursos de subscrição de toomanaging de acesso dos utilizadores Olá, é conseguida ao conceder-lhes permissões toooperate recursos do Azure mapeados toohello subscrição.
>
>

## <a name="how-does-azure-ad-licensing-work"></a>Como funciona o licenciamento do Azure AD?
Baseada no licenciamento (baseado em elegibilidade) do Azure AD serviços trabalho por ativar uma subscrição no seu inquilino do Azure AD/serviço de diretório. Depois de Olá subscrição está ativa capacidades de serviço Olá podem ser geridas pelos administradores do serviço de diretório/e utilizadas pelos utilizadores licenciados.

Ao utilizador o compra ou ativar o Enterprise Mobility Suite, Azure AD Premium ou do Azure AD Basic, o diretório é atualizado com a subscrição Olá, incluindo o respetivo período de validade e pago licenças. Informações da sua subscrição, incluindo o estado, o próximo ciclo de vida evento e o número de Olá de licenças atribuídas ou disponíveis está disponível através do Olá portal clássico do Azure, no separador de licenças de Olá de diretório específico Olá. Isto também é toobest local toomanage suas atribuições de licenças.

Cada subscrição é composta por um ou mais planos de serviço, cada Olá mapeamento incluído o nível funcional do tipo de serviço Olá; Por exemplo, do Azure AD, MFA do Azure, Microsoft Intune, Exchange Online ou o SharePoint Online. Gestão de licenças do Azure AD não requer a gestão de nível de plano de serviço. Isto é diferente do Office 365, que se baseia neste avançadas modo toomanage acesso tooincluded dos serviços de configuração. Azure AD depende da configuração de serviço, tooenable funcionalidades e gerir as permissões individuais.

Em geral, as informações de subscrição do Azure AD são geridas através de Olá portal clássico do Azure, no separador de licenças de Olá de diretório específico Olá. Subscrições do Azure do AD, com exceção de Olá do Azure AD Premium, não aparecer no portal do Office Olá.

> [!IMPORTANT]
> Azure AD Premium e Basic, bem como as subscrições do Enterprise Mobility Suite, são inquilino e directory limitados tootheir aprovisionado. Subscrições não podem ser divididas entre diretórios ou utilizadores tooentitle utilizado noutros diretórios. Mover uma subscrição entre diretórios é possível, mas necessita de submeter um pedido de suporte ou cancelamento e adquirir novamente no caso de Olá de compras diretas.
>
> Quando a compra do Azure AD ou através de licenciamento em Volume a ativação da subscrição do Enterprise Mobility Suite acontecerá automaticamente quando o contrato de Olá inclui outros serviços Online da Microsoft, por exemplo, o Office 365.
>
>

Paga leque de Olá span do diretório de Olá de funcionalidades do Azure AD. Os exemplos incluem:

* Atribuição baseada em grupo tooapplications, que está ativada em Olá específico de aplicação que estiver a gerir.
* Avançadas e capacidades de gestão de grupo personalizada estão disponíveis com a configuração do diretório Olá ou num grupo específico de Olá.
* Relatórios de segurança de Premium estão no separador de relatórios de Olá
* Deteção de aplicação de nuvem aparece no Olá portal do Azure com identidade.

### <a name="assigning-licenses"></a>Atribuir licenças
Ao obter uma subscrição é tooconfigure paga capacidades de todos os que necessita, utilizar o seu Azure AD paga funcionalidades requer a distribuição indivíduos de direito de toohello de licenças. Em geral, deve ser atribuído a qualquer utilizador que deve ter acesso tooor que é gerido através de um Azure AD paga funcionalidade uma licença. Uma atribuição de licença é um mapeamento entre um utilizador e um serviço adquirido, como o Azure AD Premium, Basic ou Enterprise Mobility Suite.

Gerir os utilizadores no seu diretório devem ter uma licença é simple. Pode ser conseguido através da atribuição tooa grupo toocreate as regras de atribuição através do portal de administração do Azure AD Olá ou através da atribuição de licenças diretamente toohello indivíduos direito através de um portal, PowerShell ou APIs. Ao atribuir grupo de tooa de licenças, todos os membros do grupo serão atribuídos uma licença. Se os utilizadores são adicionados ou removidos do grupo de Olá estará licença adequada Olá atribuídos ou removidos. Pode utilizar qualquer tooyou disponíveis da gestão de grupo de atribuição de grupo e é consistente com a atribuição baseada em grupo tooapplications. Através desta abordagem, pode configurar regras de forma a que são atribuídos automaticamente todos os utilizadores no seu diretório, certifique-se de que todas as pessoas com cargo adequado Olá tem uma licença ou mesmo delegar gestores tooother de decisão de Olá na organização de Olá.

Com a atribuição baseada em grupo de licenças, qualquer utilizador em falta uma localização de utilização irão herdar de localização do diretório Olá durante a atribuição. Esta localização pode ser alterada pelo administrador de Olá em qualquer altura. Em casos onde Olá automatizada falhou devido a atribuição tooerror, informações de utilizador Olá em que o tipo de licença irá refletir esse Estado.

## <a name="getting-started-with-azure-ad-licensing"></a>Introdução ao licenciamento do Azure AD
Introdução ao Azure AD é fácil; Pode sempre criar o diretório como parte da inscrição tooa versão de avaliação gratuita do Azure. [Saiba mais sobre como inscrever-se como uma organização](sign-up-organization.md). seguinte Olá pode ajudá-lo, certifique-se de que o seu diretório melhor está alinhado com outros serviços Microsoft, poderá estar a consumir ou estiver a planear tooconsume e os objetivos na obtenção do serviço de Olá.

Seguem-se algumas melhores práticas:

* Se já estiver a utilizar qualquer um dos serviços de organizacionais da Microsoft, já tem um diretório do Azure AD. Neste caso, deve continuar toouse Olá mesmo diretório para outros serviços, para que a gestão de identidades de núcleos, incluindo aprovisionamento e híbridos SSO, pode ser utilizada em serviços Olá. Os seus utilizadores terão uma experiência de início de sessão único e irão beneficiar das capacidades mais rica nos vários serviços Olá. Como resultado, se decidir toobuy um do Azure AD paga serviço para a sua força de trabalho, recomendamos que utilize Olá mesmo diretório toodo isto.
* Se estiver a planear toouse do Azure AD para outro conjunto de utilizadores (parceiros, clientes e assim sucessivamente) ou se pretende que os serviços de tooevaluate do Azure AD e gostaria de toodo que em isolamento do seu serviço de produção, ou se estiver à procura toosetup um ambiente sandbox para os serviços, recomendamos que crie um novo diretório através do portal clássico do Azure do Azure Olá primeiro. [Saiba mais sobre como criar um novo diretório do Azure AD no portal clássico do Azure de Olá](active-directory-licensing-directory-independence.md). novo diretório de Olá será criado com a sua conta como um utilizador externo com permissões de administrador global. Quando inicia sessão no toohello clássico do Azure portal com esta conta, irá ser capaz de toosee neste diretório e aceder a todas as tarefas de administração de diretórios. Recomendamos que crie uma conta local com os privilégios apropriados toomanage outros serviços da Microsoft (as que não está acessível através de Olá portal clássico do Azure). [Saiba mais sobre como criar contas de utilizador no Azure AD](active-directory-create-users.md).

> [!NOTE]
> Azure AD suporta "utilizadores externos" que são contas de utilizador numa instância do Azure AD que foram criadas com uma conta Microsoft (MSA) ou uma identidade do Azure AD de outro diretório. Enquanto que se encontram ocupadas alargar esta capacidade em todos os serviços de organizacionais da Microsoft, de momento estas contas não são suportadas em algumas das experiências dos serviços de Olá; Por exemplo, o portal de administração de Olá do Office 365 não suporta atualmente estes utilizadores. Como resultado, utilizadores externos com contas Microsoft não serão possível tooaccess capaz de portal de administração de Olá do Office 365, enquanto utilizadores externos de outros diretórios do Azure AD serão ignorados. No caso desta última opção Olá, do utilizador Olá apenas conta local, Olá do Azure AD ou o Office 365 diretório onde Olá foi originalmente criado, seria acessível através de experiências destas.
>
>

Conforme indicado, o Azure AD dispõe diferentes versões pagas. Estas versões tem algumas pequenas diferenças na respetiva disponibilidade compra:

| Produto | EA/VL | Aberto | CSP | Direitos de utilização de MPN | Compra direta | Avaliação |
| --- | --- | --- | --- | --- | --- | --- |
| Enterprise Mobility Suite |X |X |X |X | |X |
| Azure AD Premium |X |X |X | |X |X |
| Azure AD Basic |X |X |X |X |<br /> |<br /> |

### <a name="select-one-or-more-license-trials"></a>Selecione um ou mais avaliações de licença
 Em todos os casos, pode ativar uma subscrição de avaliação do Azure AD Premium ou Enterprise Mobility Suite, selecionando a avaliação específico Olá que quiser no separador de licenças de Olá no seu diretório. A versão de avaliação contém uma subscrição de 30 dias com 100 licenças.

![Planos de licença de avaliação do Azure Active Directory](./media/active-directory-licensing-what-is/trial_plans.png)

![Planos de licença de avaliação do Enterprise Mobility Suite](./media/active-directory-licensing-what-is/EMS_trial_plan.png)

![Planos de licença de avaliação de Active Directory](./media/active-directory-licensing-what-is/active_license_trials.png)

### <a name="assign-licenses"></a>Atribuir licenças
Depois de subscrição de Olá está ativa, deve atribuir uma licença tooyourself e atualizar Olá tooensure de browser que está a ver todas as suas funcionalidades. Olá próximo passo é tooassign licenças toohello utilizadores que terão tooaccess ou ser incluídos paga funcionalidades do Azure AD. Conforme foi mencionado na "Atribuir licenças," Olá melhor forma toodo isto é tooidentify Olá grupo que representa o público-alvo de Olá pretendida e atribua-lhe toohello licença; desta forma, os utilizadores que são adicionados ou removidos do grupo de Olá ao longo do respetivo ciclo de vida serão atribuídos tooor removido da licença de Olá.

Olá, tooassign um grupo de tooa licenças ou utilizadores individuais, selecionados o plano de licenciamento que teria como tooassign e clique em **atribuir** na barra de comandos Olá.

![Planos de licença de avaliação de Active Directory](./media/active-directory-licensing-what-is/assign_licenses.png)

Depois de Olá atribuição caixa de diálogo de plano selecionado Olá, pode selecionar utilizadores e adicioná-los toohello **atribuir** coluna no Olá à direita. Pode percorrer a lista de utilizadores Olá ou procure indivíduos específicos utilizando Olá à procura de transparência na Olá principais direita da grelha de utilizador Olá. grupos de tooassign, selecione "Grupos de" Olá **mostrar** menu e, em seguida, clique no botão de verificação de Olá no Olá toorefresh direita Olá atribuições que são apresentados.

![Atribuir licenças toogroups](./media/active-directory-licensing-what-is/assign_licenses_to_groups.png)

Agora pode pesquisar ou página através de grupos e adicioná-los toohello **atribuir** coluna na Olá mesma forma. Pode utilizar estes tooassign uma combinação de utilizadores e grupos numa única operação. toocomplete Olá o processo de atribuição, clique no botão de verificação de Olá no Olá canto inferior direito da página Olá.

![Mensagem de progresso de atribuição de licença](./media/active-directory-licensing-what-is/license_assignment_progress_message.png)

Quando é atribuído um grupo, os seus membros herdam licenças Olá dentro de 30 minutos, mas normalmente 1-2 minutos.

Erros de atribuição podem ocorrer durante a atribuição de licença do Azure AD, mas são relativamente raros. Potenciais erros de atribuição estão limitados a:

* Conflito de atribuição - quando um utilizador anteriormente foi atribuído uma licença que é incompatível com a licença atual Olá. Neste caso, a atribuição de licenças novo Olá necessitará de remover Olá anterior.
* Licenças disponíveis excedeu - quando o número de Olá de utilizadores de grupos atribuídos exceder licenças disponíveis, o estado de atribuição dos utilizadores Olá irá refletir um tooassign falha devido toomissing licenças.

### <a name="view-assigned-licenses"></a>Licenças de vista atribuída
Uma vista de resumo de licenças atribuídas, incluindo eventos de ciclo de vida de subscrição disponível, atribuído e seguinte são apresentados no Olá **licenças** separador.

![Vista Olá número de licenças atribuídas](./media/active-directory-licensing-what-is/view_assigned_licenses.png)

Uma lista detalhada dos utilizadores atribuídos e grupos, incluindo o estado de atribuição e o caminho (direto ou herdado de um ou mais grupos) está disponível quando navegar para um plano de licenciamento.

![Apresentar detalhes de licenças atribuídas para um plano de licença](./media/active-directory-licensing-what-is/assigned_licenses_detail.png)

A remoção de licenças é tão fácil como lhes atribuir. Se lhe utilizador Olá esteja diretamente atribuída ou para um grupo atribuído, pode remover licença Olá ao selecionar o tipo de licença de Olá, selecionar **remover**, adicionar utilizador Olá ou uma lista de remover toohello de grupo e confirmar a ação de Olá. Em alternativa, pode abrir um tipo de licença, grupo ou utilizador específico Olá selecione e toque em **remover** na barra de comandos Olá. tooend herança de um utilizador de uma licença de um grupo, basta remover utilizador Olá grupo Olá.

### <a name="extending-trials"></a>Expandir avaliações
As extensões de avaliação para clientes que estão disponíveis como personalizada através do portal Olá do Office 365. Um administrador de cliente pode navegar toohello [portal do Office](https://portal.office.com/#Billing) (acesso depende permissões para o portal do Office Olá) e selecione a versão de avaliação do Azure AD Premium. Clique em Olá **expandir a avaliação** e siga as instruções de Olá da ligação. Terá de tooenter um cartão de crédito, mas não será cobrado.

![Expandir uma versão de avaliação de licença no portal do Office Olá](./media/active-directory-licensing-what-is/extend_license_trial.png)

Os clientes podem também pedir uma extensão da avaliação submeter um pedido de suporte. Um administrador de cliente pode navegar toohello do Office 365 portal [página suporte](http://aka.ms/extendAADtrial) (acesso depende permissões para a página de suporte do Office Olá). Nesta página, selecione "Subscrições e avaliações" em funcionalidades e "Perguntas de avaliação" em sintoma. Por fim, introduza informações em circunstâncias Olá

![Expandir uma versão de avaliação de licença através de um pedido de suporte](./media/active-directory-licensing-what-is/alternate_office_aad_trial_extension.png)

## <a name="next-steps"></a>Passos seguintes
Agora pode ser preparado tooconfigure e utilizar algumas funcionalidades do Azure AD Premium.

* [Reposição de palavra-passe self-service](active-directory-manage-passwords.md)
* [Gestão de grupos self-service](active-directory-accessmanagement-self-service-group-management.md)
* [Estado de funcionamento de AD Connect do Azure](active-directory-aadconnect-health.md)
* [Tooapplications de atribuição de grupo](active-directory-manage-groups.md)
* [Multi-factor Authentication do Azure](../multi-factor-authentication/multi-factor-authentication.md)
* [Direta compra de licenças do Azure AD Premium](http://aka.ms/buyaadp)
