---
title: "considerações de design do aaaAzure do Active Directory híbrida identidade - determinar a estratégia de adoção de ciclo de vida de identidade híbrida | Microsoft Docs"
description: "Ajuda a definir Olá híbrida identidade as tarefas de gestão de acordo com as opções de toohello disponíveis para cada fase do ciclo de vida."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 420b6046-bd9b-4fce-83b0-72625878ae71
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 86ec0a9896f069bc93e49e06006954848f8e4d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="determine-hybrid-identity-lifecycle-adoption-strategy"></a>Determinar a estratégia de adoção de ciclo de vida de identidade híbrida
Nesta tarefa, vai definir a estratégia de gestão de identidade Olá para sua híbrida identidade solução toomeet Olá requisitos empresariais que definiu no [determinar as tarefas de gestão de identidade híbrida](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md).

toodefine Olá híbrida identidade tarefas de gestão em conformidade com o ciclo de vida do ponto-a-ponto identidade toohello apresentado anteriormente neste passo, terá de tooconsider Olá as opções disponíveis para cada fase do ciclo de vida.

## <a name="access-management-and-provisioning"></a>Aprovisionamento e gestão de acesso
Com uma solução de gestão de acesso de conta boa, a organização pode controlar precisamente quem tem acesso toowhat informações em toda a organização de Olá.

Controlo de acesso é uma função crítica de um sistema de aprovisionamento centralizado e o ponto único. Para além de proteger informações confidenciais, controlos de acesso expõem contas existentes que tenham autorizações não aprovadas ou são já não é necessário. as contas obsoleto toocontrol, Olá aprovisionamento informações de conta em conjunto de ligações de sistema com autoritativas informações sobre os utilizadores de Olá que possuem contas Olá. Informações de identidade do utilizador autoritativo, normalmente, são mantidas em bases de dados de Olá e diretórios de recursos humanos.

Contas de empresas de TI sofisticadas incluem centenas de parâmetros que definem as autoridades de Olá e estes detalhes podem ser controlados pelo seu sistema de aprovisionamento. Os novos utilizadores podem ser identificados com dados de Olá que fornecem a partir da origem autoritativa Olá. a capacidade de aprovação de pedidos de acesso Olá inicia processos Olá aprovar (ou rejeitar) recursos de aprovisionamento para os mesmos.

| Fase de gestão do ciclo de vida | No local | Nuvem | Híbrido |
| --- | --- | --- | --- |
| Aprovisionamento e gestão de contas |Ao utilizar a função de servidor de serviços de domínio do Active Directory® (AD DS) Olá, pode criar uma infraestrutura escalável, segura e gerível para a gestão de recursos e utilizadores e fornecer suporte para aplicações com diretório ativado como o Microsoft® Exchange Server. <br><br> [Pode aprovisionar grupos no AD DS através do Gestor de identidade](https://technet.microsoft.com/library/ff686261.aspx) <br>[Pode aprovisionar utilizadores no AD DS](https://technet.microsoft.com/library/ff686263.aspx) <br><br> Os administradores podem utilizar recursos de tooshared de acesso de utilizador toomanage controlo acesso por motivos de segurança. No Active Directory, o controlo de acesso é administrado ao nível do objeto de Olá por definição diferentes níveis de acesso ou permissões, tooobjects, tais como sem acesso, leitura, escrita ou controlo total. Controlo de acesso no Active Directory define como diferentes utilizadores pode utilizar os objetos do Active Directory. Por predefinição, as permissões em objetos no Active Directory estão definidas toohello de definição mais segura. |Ter toocreate uma conta para todos os utilizadores que acedem um serviço em nuvem da Microsoft. Também pode alterar as contas de utilizador ou eliminá-las quando já não forem necessárias. Por predefinição, os utilizadores não têm permissões de administrador, mas pode optar por atribuir-lhes. Para obter mais informações, consulte [gerir os utilizadores no Azure AD](active-directory-create-users.md). <br><br> No Azure Active Directory, uma das principais funcionalidades de Olá é Olá capacidade toomanage acesso tooresources. Estes recursos podem fazer parte do diretório de Olá, como no caso de Olá de objetos de toomanage permissões através de funções no diretório de Olá ou recursos que são directory toohello externo, como aplicações SaaS, serviços do Azure e sites do SharePoint ou no local recursos. <br><br> Em Olá solução de gestão do System center do Azure Active Directory do acesso é o grupo de segurança de Olá. proprietário do recurso Olá (Olá administrador ou do diretório de Olá) pode atribuir um grupo tooprovide um certos acesso toohello direita recursos possuem. Olá os membros do grupo de Olá irão ser fornecidos acesso Olá e proprietário do recurso Olá pode delegar a lista de membros do Olá toomanage direita Olá de uma pessoa – como um Gestor de departamento ou um administrador de suporte técnico de toosomeone de grupo<br> <br> grupos de gestão de Olá tópico do Azure AD fornece mais informações sobre gerir o acesso através de grupos. |Expandir as identidades do Active Directory na nuvem do Olá através de sincronização e a Federação |

## <a name="role-based-access-control"></a>Controlo de acesso baseado em funções
Controlo de acesso baseado em funções (RBAC) utiliza as funções e tooevaluate de políticas de aprovisionamento, testar e impor os processos empresariais e as regras para conceder acesso toousers. Os administradores de chaves criar políticas de aprovisionamento e atribuir utilizadores tooroles e que define os conjuntos de elegibilidade tooresources para estas funções. RBAC expande Olá identidade solução toouse baseada em software processos de gestão e reduzir intervenção manual do utilizador no processo de aprovisionamento de Olá.
RBAC do Azure AD permite quantidade do Olá empresa toorestrict Olá de operações que uma pessoa pode fazê-lo Depois do João tem acesso tooAzure Portal de gestão. Ao utilizar o portal do RBAC toocontrol acesso toohello, se aproxima administradores de TI AC delegar o acesso através da utilização de Olá gestão de acesso a seguir:

* **Atribuição de função com base no grupo**: pode atribuir acesso tooAzure AD grupos que podem ser sincronizados do Active Directory local. Isto permite-lhe tooleverage Olá investimentos existentes que sua organização tem efetuadas nas ferramentas e processos para gerir grupos. Também pode utilizar a funcionalidade de gestão de grupo delegada Olá do Azure AD Premium.
* **Tire partido funções no Azure incorporado**: pode utilizar três funções — tooensure proprietário, Contribuidor, leitor e de, que os utilizadores e grupos têm permissão toodo apenas Olá as tarefas precisam toodo as respetivas tarefas.
* **Acesso granulares tooresources**: pode atribuir toousers de funções e grupos para uma determinada subscrição, o grupo de recursos ou um recurso do Azure individuais como um Web site ou a base de dados. Desta forma, pode certificar-se de que os utilizadores têm acesso a recursos Olá tooall que precisam e nenhum tooresources de acesso que não é necessário toomanage.

## <a name="provisioning-and-other-customization-options"></a>Aprovisionamento e outras opções de personalização
A equipa pode utilizar toodecide planos e requisitos de negócio que solução de identidade toocustomize Olá. Por exemplo, uma grande empresa poderão ser necessários um plano de agregação Escalamento faseado para fluxos de trabalho e personalizadas adaptadores que é baseada numa linha de tempo para o aprovisionamento de forma incremental a aplicações que são utilizadas em grande escala em localizações geográficas. Pode fornecer outro plano de personalização para dois ou mais toobe aplicações aprovisionado numa organização inteira, depois de testar com êxito. Interação de aplicação do utilizador pode ser personalizada e procedimentos para o aprovisionamento de recursos podem ser alterada tooaccommodate automatizada de aprovisionamento.

Pode desaprovisionar tooremove um componente ou serviço. Por exemplo, o desaprovisionamento uma conta significa que a conta de Olá é eliminada de um recurso.

modelo de híbrida Olá de aprovisionamento de recursos de combina pedido e abordagens baseada em funções, que são ambas suportadas pelo Azure AD. Para um subconjunto dos funcionários ou sistemas geridos, uma empresa querer tooautomate acesso com a atribuição baseada em funções. Uma empresa também pode processar todos os outros pedidos de acesso ou exceções através de um modelo baseado em pedidos. Algumas empresas podem começar com atribuição manual e evoluir na direção de um modelo de híbrida, com uma intenção de uma implementação totalmente baseada em funções num momento futuro.

Outras empresas poderão achar impractical para empresas motivos tooachieve completa baseada em funções de aprovisionamento e o destino de uma abordagem de híbrida como um objetivo reclamado. Ainda outras empresas poderão estar satisfeito com apenas baseado em pedidos de aprovisionamento e não pretende tooinvest esforço adicional toodefine e gerir políticas de aprovisionamento baseado em funções, automatizadas.

## <a name="license-management"></a>Gestão de licenças
Gestão de baseado no grupo de licenças no Azure AD permite aos administradores atribuir o grupo de segurança utilizadores tooa e AD do Azure atribui automaticamente licenças tooall Olá os membros Olá grupo. Se um utilizador é, subsequentemente, adicionado ou removido do grupo de Olá, uma licença será automaticamente atribuída ou removida conforme adequada.

Pode utilizar grupos de sincronizar a partir do AD no local ou gerir no Azure AD. O emparelhamento esta cópia de segurança com n Self-Service de grupo de gestão do Azure AD premium pode delegar facilmente licença atribuição toohello adequado decisores. Pode ter a certeza que problemas, como os conflitos de licença e dados de localização em falta são automaticamente ordenados.

## <a name="self-regulating-user-administration"></a>Administração de utilizador Self-regulating
Quando a organização é iniciado tooprovision recursos em todas as organizações internas, implementar a capacidade de administração de utilizador Self-regulating Olá. Pode regressam vantagens Olá e os benefícios de aprovisionamento de utilizadores, entre limites organizacionais. Neste ambiente, uma alteração de estado do utilizador é refletida automaticamente no direitos de acesso através de limites da organização e localizações geográficas. Pode reduzir os custos de aprovisionamento e simplificar processos de aprovação e acesso de Olá. implementação de Olá realiza Olá potencial de implementação de controlo de acesso baseado em funções para a gestão de acesso de ponto a ponto na sua organização. Pode reduzir os custos administrativos através de procedimentos automatizados para que rege o aprovisionamento de utilizadores. Pode melhorar a segurança ao automatizar a imposição de políticas de segurança e simplificar e centralizar a gestão de ciclo de vida de utilizador e aprovisionamento de recursos para populações de grandes dimensões de utilizador.

> [!NOTE]
> Para obter mais informações, consulte Configurar o Azure AD para gestão de acesso de aplicação de self-service
> 
> 

Baseada no licenciamento (baseado em elegibilidade) do Azure AD serviços trabalho por ativar uma subscrição no seu inquilino do Azure AD/serviço de diretório. Depois de Olá subscrição está ativa capacidades de serviço Olá podem ser geridas pelos administradores do serviço de diretório/e utilizadas pelos utilizadores licenciados. Para obter mais informações, consulte como funciona o Azure AD licenciamento trabalho?
Integração com outros fornecedores 3rd

Do Azure Active Directory fornece o início de sessão único e modulação de toothousands de segurança de acesso de aplicação de aplicações SaaS e aplicações de web no local. Para obter uma lista detalhada de Galeria de aplicações do Azure Active Directory para aplicações SaaS suportadas, consulte a lista de compatibilidades de Federação do Azure Active Directory: fornecedores de identidade de terceiros que podem ser utilizado tooimplement de sessão único-

## <a name="define-synchronization-management"></a>Definir a gestão de sincronização
A integração dos diretórios no local com o Azure AD torna os utilizadores mais produtivos, ao fornecer-lhes uma identidade comum para acederem a recursos na nuvem e no local. Esta integração utilizadores e organizações podem beneficiar do seguinte Olá:

* As organizações podem fornecer aos utilizadores com uma identidade híbrida comum no local ou serviços baseados na nuvem tirar partido do Windows Server Active Directory e, em seguida, ligar tooAzure do Active Directory.
* Os administradores podem fornecer o acesso condicional com base nos recursos de aplicação, dispositivo e a identidade do utilizador, localização de rede e a autenticação multifator.
* Os utilizadores podem tirar partido as respetivas identidades comuns através de contas no Azure AD tooOffice 365, o Intune, aplicações SaaS e aplicações de terceiros.
* Os programadores podem criar aplicações que tiram partido do modelo de identidade comum Olá, integrar aplicações no Active Directory no local ou do Azure para aplicações baseadas na nuvem

Olá figura que se segue contém um exemplo de uma vista detalhada do processo de sincronização de identidade.

![](./media/hybrid-id-design-considerations/identitysync.png)

Processo de sincronização de identidade

Reveja Olá opções de sincronização de Olá de toocompare de tabela a seguir:

| Opção de gestão de sincronização | Vantagens | Desvantagens |
| --- | --- | --- |
| Baseadas na sincronização (através de DirSync ou AADConnect) |Utilizadores e grupos sincronizados a partir da nuvem e no local <br>  **Controlo de política**: políticas de conta podem ser definidas através do Active Directory, o que lhe dá a estação de trabalho, políticas de palavra-passe do Olá administrador Olá capacidade toomanage, controlos de limite de bloqueio e restrições e mais, sem ter tooperform adicional tarefas na nuvem de Olá.  <br>  **Controlo de acesso**: pode restringir o acesso toohello nuvem serviço para que os serviços de Olá podem ser acedidos através do ambiente empresarial Olá, através de servidores online ou por ambos. <br>  Reduzido chamadas de suporte: se os utilizadores tiverem menos tooremember de palavras-passe, que são menos provável tooforget-los. <br>  Segurança: Identidades de utilizador e as informações estão protegidos porque todos os servidores de Olá e os serviços utilizados no início de sessão, controladas e controlado no local. <br>  Suporte para autenticação forte: pode utilizar a autenticação forte (também denominada de autenticação de dois fatores) com o serviço de nuvem Olá. No entanto, se utilizar autenticação forte, tem de utilizar o início de sessão único. | |
| Baseada em Federação (através do AD FS) |Ativado por serviço de tokens de segurança (STS). Quando configurar um STS tooprovide único início de sessão acesso com um serviço em nuvem da Microsoft, que vai criar uma confiança federada entre o STS no local e o domínio federado Olá especificadas no seu inquilino do Azure AD. <br> Permite aos utilizadores finais Olá toouse mesmo conjunto de credenciais tooobtain aceder toomultiple a recursos <br>os utilizadores finais não dispõe de toomaintain vários conjuntos de credenciais. Ainda, os utilizadores de Olá têm tooprovide tooeach as respetivas credenciais um Olá participantes recursos., cenários B2B e B2C suportados. |Requer técnico especializados para implementação e manutenção de dedicado no local servidores AD FS. Existem restrições na utilização de Olá de autenticação forte, se planear toouse do AD FS para os STS. Para obter mais informações, consulte [configurar opções avançadas para o AD FS 2.0](http://go.microsoft.com/fwlink/?linkid=235649). |

> [!NOTE]
> Para obter mais informações, consulte [integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md).
> 
> 

## <a name="see-also"></a>Veja Também
[Descrição geral das considerações de design](active-directory-hybrid-identity-design-considerations-overview.md)

