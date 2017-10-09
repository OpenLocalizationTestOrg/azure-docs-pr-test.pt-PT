---
title: "aaaAzure proteção de identidade do Active Directory | Microsoft Docs"
description: "Saiba como do Azure AD Identity Protection permite-lhe capacidade de Olá toolimit de tooexploit um atacante uma identidade comprometida ou dispositivo e toosecure uma identidade ou um dispositivo que anteriormente estava toobe conhecido ou potencialmente comprometido."
services: active-directory
keywords: "proteção de identidade do Azure Active Directory, o cloud app discovery, gestão de aplicações, segurança, risco, nível de risco, vulnerabilidade, política de segurança"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a>Azure Active Directory Identity Protection

Azure Active Directory Identity Protection é uma funcionalidade de edição de Olá, Azure AD Premium P2 que lhe permite:

- Detetar potenciais vulnerabilidades que afetam as identidades da organização

- Configurar respostas automáticas toodetected suspeita ações que são identidades da organização tooyour relacionados  

- Investigar incidentes suspeitas e tome as medidas adequadas tooresolve-las   


## <a name="getting-started"></a>Introdução

Microsoft protege identidades baseado na nuvem para a mais do que um decade. Com o Azure Active Directory Identity Protection, no seu ambiente, pode utilizar Olá sistemas de proteção mesmo Microsoft utiliza toosecure identidades.

Coloque vasta maioria de Olá de tomar de falhas de segurança quando os atacantes ganham ambiente de tooan acesso roubo de identidade do utilizador. Ao longo de anos Olá, os atacantes tem tornar-se cada vez mais eficientes tirar partido das violações de terceiros e utilização de ataques de phishing sofisticadas. Assim que um atacante obtiver acesso a contas de utilizador com privilégios baixa tooeven, é relativamente fácil para os mesmos toogain aceder tooimportant a recursos empresariais através de movimento lateral.

Como consequência, tem de:

- Proteger todas as identidades independentemente do respetivo nível de privilégios

- Proativamente impedir identidades comprometidas que está a ser abused

Detetar identidades comprometidas não é nenhuma tarefa fácil. Azure Active Directory utiliza adaptável algoritmos de aprendizagem automática e anomalias de toodetect heurística e incidentes suspeitas que indiquem potencialmente comprometido identidades. Utilizando estes dados, Identity Protection gera relatórios e alertas que permitem Olá tooevaluate detetados problemas e demorar mitigação adequada ou ações de remediação.

Azure Active Directory Identity Protection é maior do que uma monitorização e a ferramenta de relatórios. tooprotect as identidades da organização, pode configurar as políticas baseadas em risco que respondam automaticamente toodetected problemas quando for atingido a um nível de risco especificado. Estas políticas, além disso tooother condicional aceder controlos fornecidos pelo Azure Active Directory e o EMS, pode bloquear automaticamente ou iniciar ações de remediação adaptável incluindo reposições de palavra-passe e de imposição de autenticação multifator.


#### <a name="identity-protection-capabilities"></a>Capacidades de proteção de identidade

**Detetar vulnerabilidades e contas de risco:**  

* Fornecer recomendações personalizado tooimprove geral postura de segurança por realce vulnerabilidades
* A calcular níveis de risco de início de sessão
* A calcular níveis de risco do utilizador


**Investigar os eventos de risco:**

* Enviar notificações para eventos de risco
* Investigar os eventos de risco utilizando informações relevantes e contextuais
* Fornecer as investigações de tootrack de fluxos de trabalho básicos
* Fornecer acesso fácil tooremediation ações, como a reposição de palavra-passe

**Políticas de acesso condicional baseado em risco:**

* Política toomitigate arriscados inícios de sessão por bloquear inícios de sessão ou exigindo desafios de autenticação multifator.
* Política tooblock ou contas de utilizador de risco segura
* Política toorequire utilizadores tooregister para autenticação multifator



## <a name="identity-protection-roles"></a>Funções de proteção de identidade

tooload saldo Olá atividades de gestão em torno da sua implementação Identity Protection, pode atribuir várias funções. Azure AD Identity Protection suporta 3 funções do diretório:

| Função                         | Pode fazê-lo                          | Não é possível efetuar
| :--                          | ---                                |  ---   |
| Administrador global         | Acesso total tooIdentity proteção, carregar Identity Protection| |
| Administrador de segurança       | Acesso total tooIdentity proteção | Carregar Identity Protection, repor palavras-passe para um utilizador |
| Leitor de segurança              | Acesso só de pronto tooIdentity proteção | Carregar Identity Protection, remidiate utilizadores, configurar políticas, repor palavras-passe |




Para obter mais detalhes, consulte [atribuir funções de administrador no Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)



## <a name="detection"></a>Deteção

### <a name="vulnerabilities"></a>Vulnerabilidades

Azure Active Directory Identity Protection analyses a configuração e Deteta que pode ter um impacto nas identidades dos utilizadores. Para obter mais detalhes, consulte [vulnerabilidades detetadas pelo Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).

### <a name="risk-events"></a>Eventos de risco

Azure Active Directory utiliza adaptável do machine learning algoritmos e heurística toodetect suspeitas ações que são as identidades dos utilizadores tooyour relacionados. sistema de Olá cria um registo para cada ação suspeito detetado. Estes registos são também conhecidos como eventos de risco.  
Para obter mais detalhes, veja [Eventos de risco do Azure Active Directory](active-directory-identity-protection-risk-events.md).


## <a name="investigation"></a>Investigação
Da sua viagem através da proteção de identidade normalmente começa com o dashboard de Identity Protection Olá.

![Remediação](./media/active-directory-identityprotection/1000.png "remediação")

dashboard de Olá dá-lhe acesso ao:

* Os relatórios tal como **utilizadores sinalizados para risco**, **eventos de risco** e **vulnerabilidades**
* Definições, tais como a configuração de Olá do seu **políticas de segurança**, **notificações** e **registo de autenticação multifator**

É, geralmente, o ponto de partida para investigação, que é o processo de Olá de rever Olá atividades, registos e outras informações relevantes tooa relacionado toodecide de eventos de risco, se são necessários passos de remediação ou atenuação, e como identidade Olá foi comprometido e compreender como Olá comprometido identidade foi utilizada.

Pode associar o seu toohello de atividades de investigação [notificações](active-directory-identityprotection-notifications.md) do Azure Active Directory proteção enviar por e-mail.

Olá secções seguintes fornecem mais detalhes e passos de Olá que estão relacionados tooan investigação.  


## <a name="risky-sign-ins"></a>Risco inícios de sessão

Azure Active Directory Deteta [tipos de eventos de risco](active-directory-reporting-risk-events.md#risk-event-types) no offline e em tempo real. Cada evento de risco que foi detetado para um início de sessão de um utilizador contribui conceito lógico tooa chamado arriscado início de sessão. Um risco início de sessão é um indicador para uma tentativa de início de sessão não pode ter sido efetuada pelo proprietário de legítimos Olá de uma conta de utilizador.


### <a name="sign-in-risk-level"></a>Nível de risco de início de sessão

Um nível de risco de início de sessão é uma indicação (alta, média ou baixa) de probabilidade de Olá que uma tentativa de início de sessão não foi efetuada pelo proprietário de legítimos Olá de uma conta de utilizador.

### <a name="mitigating-sign-in-risk-events"></a>Mitigar o risco de início de sessão de eventos

Uma mitigação é uma capacidade de Olá toolimit de ação de um atacante tooexploit uma identidade comprometida ou dispositivo sem estado de restauro Olá identidade ou dispositivo tooa seguro. Uma mitigação não resolver eventos de risco de início de sessão anteriores associados à identidade Olá ou dispositivo.

inícios de sessão de risco toomitigate automaticamente, pode configurar policicies de segurança de início de sessão de risco. Utilizar estas políticas, consideram o nível de risco Olá de utilizador de Olá ou Olá início de sessão tooblock arriscados inícios de sessão ou exigir a autenticação multifator tooperform Olá. Estas ações podem impedir que um atacante explorá danos de toocause uma identidade roubado e poderão dar-lhe identidade de Olá de toosecure algum tempo.

### <a name="sign-in-risk-security-policy"></a>Política de segurança de início de sessão risco
Uma política de início de sessão risco é uma política de acesso condicional que avalia Olá risco tooa específico início de sessão e aplica-se mitigações com base nas condições predefinidas e as regras.

![Política de início de sessão risco](./media/active-directory-identityprotection/1014.png "início de sessão da política de risco")

Azure AD Identity Protection ajuda a gerir mitigação de Olá do risco de inícios de sessão, permitindo:

* Conjunto Olá utilizadores e grupos Olá política aplica-se a:

    ![Política de início de sessão risco](./media/active-directory-identityprotection/1015.png "início de sessão da política de risco")
* Definir Olá início de sessão risco nível limiar (baixa, média ou alta) que aciona a política de Olá:

    ![Política de início de sessão risco](./media/active-directory-identityprotection/1016.png "início de sessão da política de risco")
* Conjunto Olá controlos toobe imposta quando a política de Olá aciona:  

    ![Política de início de sessão risco](./media/active-directory-identityprotection/1017.png "início de sessão da política de risco")
* Estado do comutador Olá da sua política:

    ![Registo do MFA](./media/active-directory-identityprotection/403.png "registo do MFA")
* Rever e avaliar o impacto de Olá uma alteração antes de ativar esta:

    ![Política de início de sessão risco](./media/active-directory-identityprotection/1018.png "início de sessão da política de risco")

#### <a name="what-you-need-tooknow"></a>O que precisa de tooknow
Pode configurar uma risco de início de sessão segurança política toorequire a autenticação multifator:

![Política de início de sessão risco](./media/active-directory-identityprotection/1017.png "início de sessão da política de risco")

No entanto, por motivos de segurança, esta definição só funciona para os utilizadores que já foram registados para autenticação multifator. Se a autenticação multifator do Olá condição toorequire for satisfeita para um utilizador que ainda não está registado para autenticação multifator, utilizador de Olá está bloqueado.

Como melhor prática, se pretender que a autenticação multifator toorequire para inícios de sessão risco, deve:

1. Ativar Olá [política de registo de autenticação multifator](#multi-factor-authentication-registration-policy) para Olá utilizadores afetados.
2. Exigir Olá afetados toologin de utilizadores no tooperform sessão não arriscados um registo do MFA

Concluir estes passos garante que a autenticação multifator é necessária para um risco início de sessão.

#### <a name="best-practices"></a>Melhores práticas
Escolher um **elevada** limiar reduz o número de Olá de vezes que uma política é acionada e minimiza Olá impacto toousers.  

No entanto, exclui **baixa** e **média** inícios de sessão sinalizados para risco da política de Olá, que não pode bloquear um atacante de explorá uma identidade comprometida.

Quando a definição Olá política,

* Excluir os utilizadores que não o fizer / não podem ter a autenticação multifator
* Excluir utilizadores nas regiões onde o ativar política de Olá não é prático (por exemplo toohelpdesk sem acesso)
* Excluir os utilizadores que são toogenerate provavelmente uma grande quantidade de Falso-positivos (programadores, os analistas de segurança)
* Utilize um **elevada** limiar durante a agregação de política iniciais, ou se tem minimizar desafios vistos pelos utilizadores finais.
* Utilize um **baixa** limiar se a sua organização precisar de maior segurança. Selecionar um **baixa** limiar apresenta utilizador adicionais início de sessão desafios, mas uma maior segurança.

Olá recomendado predefinido para a maioria das organizações é tooconfigure uma regra para um **média** limiar toostrike um equilíbrio entre capacidade de utilização e segurança.

política de início de sessão risco Olá é:

* Tráfego de browser tooall aplicados e inícios de sessão que utilizam autenticação moderna.
* Não aplicado tooapplications utilizar protocolos de segurança mais antigos, desativando o ponto final de WS-Trust de Olá no IDP Olá federado, tais como o ADFS.

Olá **eventos de risco** página na consola de Identity Protection Olá apresenta uma lista de todos os eventos:

* Esta política foi aplicada ao
* Pode Olá actividade de revisão e determinar se a ação de Olá foi adequada ou não

Para obter uma descrição geral de Olá relacionadas com a experiência de utilizador, consulte:

* [Recuperação de risco início de sessão](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [Risco início de sessão bloqueado](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [Início de sessão experiências com o Azure AD Identity Protection](active-directory-identityprotection-flows.md)  

**caixa de diálogo de configuração relacionados de Olá de tooopen**:

- No Olá **do Azure AD Identity Protection** painel, no Olá **configurar** secção, clique em **início de sessão da política de risco**.

    ![Política do utilizador ridk](./media/active-directory-identityprotection/1014.png "ridk de política de utilizador")



## <a name="users-flagged-for-risk"></a>Utilizadores sinalizados para risco

Todas as ativas [eventos de risco](active-directory-identity-protection-risk-events.md) que foram detetados pelo Azure Active Directory para um utilizador contribuir conceito lógico tooa chamado risco do utilizador. Um utilizador sinalizado para risco é um indicador de uma conta de utilizador que possam ter sido comprometido.

![Utilizadores sinalizados para risco](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a>Nível de risco do utilizador

Um nível de risco do utilizador é uma indicação (alta, média ou baixa) de probabilidade de Olá que a identidade do utilizador Olá tiver sido comprometida. Esta é calculada com base em eventos de risco de utilizador Olá que estão associados a identidade do utilizador.

Olá estado de um evento de risco é **Active Directory** ou **fechado**. Apenas os eventos que são de risco **Active Directory** contribuir cálculo de nível de risco do toohello utilizador.

nível de risco do utilizador Olá é calculado com Olá seguintes entradas:

* Eventos de risco Active Directory afetar utilizador Olá
* Nível de risco destes eventos
* Indica se foram efetuadas as ações de remediação

![Riscos de utilizador](./media/active-directory-identityprotection/1031.png "riscos de utilizador")

Pode utilizar Olá utilizador risco níveis toocreate políticas de acesso condicional que impeça os utilizadores de risco de início de sessão ou forçá-los toosecurely alterar a palavra-passe.

### <a name="closing-risk-events-manually"></a>Fechar os eventos de risco manualmente

Na maioria dos casos, irá tome as ações de remediação, tais como os eventos de risco fechar tooautomatically de reposição de uma palavra-passe segura. No entanto, isto poderá não ser sempre possível.  
Isto é, por exemplo, caso Olá, quando:

* Foi eliminado um utilizador com eventos de risco Active Directory
* Uma investigação revela de que tem foi efetuar um evento de risco comunicado pelo utilizador legítimo Olá

Uma vez que os eventos de risco que são **Active Directory** contribuir cálculo de risco toohello utilizador, poderá ter toomanually reduzir um nível de risco fechando os eventos de risco manualmente.  
Decorrer Olá de investigação, pode escolher tootake qualquer uma destas ações toochange Olá Estado um evento de risco:

![Ações](./media/active-directory-identityprotection/34.png "ações")

* **Resolver** - se depois de investigar um evento de risco, demorou uma ação de remediação adequado fora Identity Protection e achar que eventos de risco Olá devem ser considerados fechados, o evento de Olá marca como resolvido. Eventos resolvidos definirá tooClosed de estado do evento de risco Olá e eventos de risco Olá já não irão contribuir toouser risco.
* **Marcar como falso-positivos** -em alguns casos, pode investigar um evento de risco e detetar que incorretamente foi sinalizado como um risco. Pode ajudar a reduzir o número de Olá de tais ocorrências assinalando eventos de risco Olá como falso-positivos. Isto irá ajudar Olá aprendizagem automática classificação de Olá tooimprove algoritmos de eventos semelhantes em Olá futura. Estado de Olá de eventos de Falso-positivos é demasiado**fechado** e já não contribuem toouser risco.
* **Ignorar** - se de que não tenha sido qualquer ação de remediação, mas pretende Olá toobe de eventos de risco foi removido da lista de Active Directory Olá, pode marcar um evento de risco ignorar e o estado do evento Olá será fechado. Eventos ignorados não contribuir toouser risco. Esta opção só deve ser utilizada em circunstâncias invulgares.
* **Reativar** -o risco de eventos que foram fechados manualmente (escolhendo **resolver**, **falsos positivos**, ou **ignorar**) pode ser reativado, definição Olá Estado do evento fazer uma cópia de demasiado**Active Directory**. Eventos de risco reativado contribuem cálculo de nível de risco do toohello utilizador. Eventos de risco fechados através de remediação (tal como repor uma palavra-passe segura) não podem ser reativados.

**caixa de diálogo de configuração relacionados de Olá de tooopen**:

1. No Olá **do Azure AD Identity Protection** painel, em **investigar**, clique em **eventos de risco**.

    ![Reposição de palavra-passe manual](./media/active-directory-identityprotection/1002.png "reposição de palavra-passe Manual")
2. No Olá **eventos de risco** lista, clique em risco.

    ![Reposição de palavra-passe manual](./media/active-directory-identityprotection/1003.png "reposição de palavra-passe Manual")
3. No painel de risco Olá, faça duplo clique um utilizador.

    ![Reposição de palavra-passe manual](./media/active-directory-identityprotection/1004.png "reposição de palavra-passe Manual")

### <a name="closing-all-risk-events-for-a-user-manually"></a>Fechar todos os eventos de risco de um utilizador manualmente
Em vez de manualmente fechar os eventos de risco de um utilizador individualmente, do Azure Active Directory Identity Protection também fornece um método tooclose todos os eventos para um utilizador com um clique.

![Ações](./media/active-directory-identityprotection/2222.png "ações")

Ao clicar em **dispensar todos os eventos**, todos os eventos estão fechados e utilizador Olá afetado já não está em risco.

### <a name="remediating-user-risk-events"></a>Eventos de risco de utilizador de remediação

Uma remediação é toosecure uma ação uma identidade ou um dispositivo que anteriormente era suspeito ou conhecido toobe comprometido. Uma ação de remediação restaura Olá identidade Estado ou de dispositivo tooa seguro e resolve os eventos de risco anteriores associados à identidade Olá ou dispositivo.

eventos de risco de utilizador tooremediate, pode:

* Efetue manualmente um eventos de risco utilizador de tooremediate de reposição de palavra-passe segura
* Configurar um toomitigate de política de segurança do utilizador risco ou remediar automaticamente os eventos de risco de utilizador
* Dispositivo de recriar a imagem de Olá infetado  

#### <a name="manual-secure-password-reset"></a>Reposição de palavra-passe segura manual
Uma reposição de palavra-passe segura é uma remediação eficaz para muitos eventos de risco e, quando efetuada, automaticamente fecha estes eventos de risco e recalcula o nível de risco Olá utilizador. Pode utilizar Olá Identity Protection dashboard tooinitiate uma palavra-passe de reposição de um utilizador de risco.

caixa de diálogo relacionados Olá fornece dois métodos diferentes tooreset uma palavra-passe:

**Repor palavra-passe** - selecione **requerem Olá utilizador tooreset a palavra-passe** tooallow Olá tooself-recuperação de utilizador, se tiver registado utilizador Olá para autenticação multifator. Durante a próximo início de sessão do utilizador Olá, utilizador de Olá será necessário toosolve uma autenticação multifator com êxito de desafio e a palavra-passe do toochange forçada, em seguida, Olá. Esta opção não está disponível se a conta de utilizador Olá já não está registada autenticação multifator.

**Palavra-passe temporária** - selecione **gerar uma palavra-passe temporária** tooimmediately invalidar palavra-passe Olá existente e criar uma nova palavra-passe temporária utilizador Olá. Envie Olá nova palavra-passe temporária tooan endereço de e-mail alternativo para o utilizador Olá ou o Gestor do utilizador toohello. Porque a palavra-passe de Olá é temporário, utilizador de Olá será palavra-passe Olá de toochange pedido após o início de sessão.

![Política](./media/active-directory-identityprotection/1005.png "política")

**caixa de diálogo de configuração relacionados de Olá de tooopen**:

1. No Olá **do Azure AD Identity Protection** painel, clique em **utilizadores sinalizados para risco**.

    ![Reposição de palavra-passe manual](./media/active-directory-identityprotection/1006.png "reposição de palavra-passe Manual")
2. Na lista de Olá de utilizadores, selecione um utilizador com eventos de risco pelo menos um.

    ![Reposição de palavra-passe manual](./media/active-directory-identityprotection/1007.png "reposição de palavra-passe Manual")
3. No painel de utilizador de Olá, clique em **Repor palavra-passe**.

    ![Reposição de palavra-passe manual](./media/active-directory-identityprotection/1008.png "reposição de palavra-passe Manual")

### <a name="user-risk-security-policy"></a>Política de segurança de risco do utilizador
Uma política de segurança do utilizador risco é uma política de acesso condicional que avalia utilizador específico de tooa ao nível do risco de Olá e aplica as ações de remediação e atenuação com base nas condições predefinidas e as regras.

![Política do utilizador ridk](./media/active-directory-identityprotection/1009.png "ridk de política de utilizador")

Azure AD Identity Protection ajuda a gerir mitigação de Olá e remediação de utilizadores sinalizados para risco ao permitir-lhe:

* Conjunto Olá utilizadores e grupos Olá política aplica-se a:

    ![Política do utilizador ridk](./media/active-directory-identityprotection/1010.png "ridk de política de utilizador")
* Definir Olá utilizador risco nível limiar (baixa, média ou alta) que aciona a política de Olá:

    ![Política do utilizador ridk](./media/active-directory-identityprotection/1011.png "ridk de política de utilizador")
* Conjunto Olá controlos toobe imposta quando a política de Olá aciona:

    ![Política do utilizador ridk](./media/active-directory-identityprotection/1012.png "ridk de política de utilizador")
* Estado do comutador Olá da sua política:

    ![Política do utilizador ridk](./media/active-directory-identityprotection/403.png "registo do MFA")
* Rever e avaliar o impacto de Olá uma alteração antes de ativar esta:

    ![Política do utilizador ridk](./media/active-directory-identityprotection/1013.png "ridk de política de utilizador")

Escolher um **elevada** limiar reduz o número de Olá de vezes que uma política é acionada e minimiza Olá impacto toousers.
No entanto, exclui **baixa** e **média** utilizadores sinalizados para risco de política de Olá, que poderá não segura identidades ou dispositivos que foram anteriormente suspeito ou conhecidos toobe comprometido.

Quando a definição Olá política,

* Excluir os utilizadores que são toogenerate provavelmente uma grande quantidade de Falso-positivos (programadores, os analistas de segurança)
* Excluir utilizadores nas regiões onde o ativar política de Olá não é prático (por exemplo toohelpdesk sem acesso)
* Utilize um **elevada** limiar durante a agregação de política iniciais, ou se tem minimizar desafios vistos pelos utilizadores finais.
* Utilize um **baixa** limiar se a sua organização precisar de maior segurança. Selecionar um **baixa** limiar apresenta utilizador adicionais início de sessão desafios, mas uma maior segurança.

Olá recomendado predefinido para a maioria das organizações é tooconfigure uma regra para um **média** limiar toostrike um equilíbrio entre capacidade de utilização e segurança.

Para obter uma descrição geral de Olá relacionadas com a experiência de utilizador, consulte:

* [Comprometido fluxo da recuperação de conta](active-directory-identityprotection-flows.md#compromised-account-recovery).  
* [Comprometido fluxo conta bloqueada](active-directory-identityprotection-flows.md#compromised-account-blocked).  

**caixa de diálogo de configuração relacionados de Olá de tooopen**:

- No Olá **do Azure AD Identity Protection** painel, no Olá **configurar** secção, clique em **política do utilizador risco**.

    ![Política do utilizador ridk](./media/active-directory-identityprotection/1009.png "ridk de política de utilizador")

### <a name="mitigating-user-risk-events"></a>Mitigar os eventos de risco do utilizador
Os administradores podem definir um utilizador risco política tooblock os utilizadores de segurança após o início de sessão, dependendo do nível de risco Olá.

Bloquear um início de sessão:

* Impede a geração de Olá novo utilizador de eventos de risco para o utilizador Olá afetado
* Permite que os administradores toomanually remediar eventos de risco Olá que afetam a identidade do utilizador Olá e restaurá-lo Estado segura tooa



## <a name="multi-factor-authentication-registration-policy"></a>Política de registo de autenticação multifator
A autenticação multifator do Azure é um método de verificar que é que requer a utilização de Olá de mais do que apenas um nome de utilizador e palavra-passe. Fornece uma segunda camada de segurança toouser inícios de sessão e transações.  
Recomendamos que necessitam do Azure multi-factor authentication para inícios de sessão de utilizador porque esta:

* Fornece autenticação forte com uma gama de opções de verificação fácil
* Desempenha uma função de chave na preparação da sua organização tooprotect e recuperar os compromissos de conta

![Política do utilizador ridk](./media/active-directory-identityprotection/1019.png "ridk de política de utilizador")

Para obter mais detalhes, consulte [que é o Azure multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)

Azure AD Identity Protection ajuda a gerir Olá roll-out do registo de autenticação multifator ao configurar uma política que permite-lhe:

* Conjunto Olá utilizadores e grupos Olá política aplica-se a:

    ![Política da MFA](./media/active-directory-identityprotection/1020.png "política da MFA")
* Conjunto Olá controlos toobe imposta quando a política de Olá aciona::  

    ![Política da MFA](./media/active-directory-identityprotection/1021.png "política da MFA")
* Estado do comutador Olá da sua política:

    ![Política da MFA](./media/active-directory-identityprotection/403.png "política da MFA")
* Ver o estado do registo atual Olá:

    ![Política da MFA](./media/active-directory-identityprotection/1022.png "política da MFA")

Para obter uma descrição geral de Olá relacionadas com a experiência de utilizador, consulte:

* [Fluxo de registo de autenticação multifator](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).  
* [Início de sessão experiências com o Azure AD Identity Protection](active-directory-identityprotection-flows.md).  

**caixa de diálogo de configuração relacionados de Olá de tooopen**:

- No Olá **do Azure AD Identity Protection** painel, no Olá **configurar** secção, clique em **registo de multi-factor authentication**.

    ![Política da MFA](./media/active-directory-identityprotection/1019.png "política da MFA")

## <a name="next-steps"></a>Passos seguintes
* [Canal 9: Do Azure AD e mostrar de identidade: identidade pré-visualização de proteção](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [Ativar a proteção de identidade do Azure Active Directory](active-directory-identityprotection-enable.md)

* [Vulnerabilidades detetadas pelo Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md)

* [Eventos de risco do Azure Active Directory](active-directory-identity-protection-risk-events.md)

* [Notificações de proteção de identidade do Active Directory do Azure](active-directory-identityprotection-notifications.md)

* [Azure Active Directory Identity Protection manual de comunicação social](active-directory-identityprotection-playbook.md)

* [Glossário do Azure Active Directory Identity Protection](active-directory-identityprotection-glossary.md)

* [Início de sessão experiências com o Azure AD Identity Protection](active-directory-identityprotection-flows.md)

* [Proteção do Azure Active Directory identidade - como toounblock utilizadores](active-directory-identityprotection-unblock-howto.md)

* [Introdução ao Azure Active Directory Identity Protection e o Microsoft Graph](active-directory-identityprotection-graph-getting-started.md)
