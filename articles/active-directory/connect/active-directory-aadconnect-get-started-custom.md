---
title: "Azure AD Connect: Instalação personalizada | Microsoft Docs"
description: "Este documento fornece detalhes sobre as opções de instalação personalizada Olá do Azure AD Connect. Utilize estas instruções tooinstall do Active Directory através do Azure AD Connect."
services: active-directory
keywords: "o que é o Azure AD Connect, instale o Active Directory, componentes precisos para o Azure AD"
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 6d42fb79-d9cf-48da-8445-f482c4c536af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: c49724fab78c5a1688662043f69506fff6f82104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="custom-installation-of-azure-ad-connect"></a>Instalação personalizada do Azure AD Connect
O Azure AD Connect **definições personalizadas do** é utilizada quando pretende mais opções para a instalação de Olá. É utilizada se tiver várias florestas ou se quiser tooconfigure funcionalidades opcionais não abrangidas na instalação rápida Olá. É utilizado em todos os casos em que hello [ **instalação rápida** ](active-directory-aadconnect-get-started-express.md) opção não satisfaz a sua implementação ou topologia.

Antes de começar a instalar o Azure AD Connect, certifique-se demasiado[transferir o Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) e pré-requisitos Olá concluir os passos em [do Azure AD Connect: Hardware e pré-requisitos](active-directory-aadconnect-prerequisites.md). Certifique-se também de que tem disponíveis as contas necessárias, conforme descrito em [Contas e permissões do Azure AD Connect](active-directory-aadconnect-accounts-permissions.md).

Se as definições personalizadas não coincidirem com a topologia, por exemplo tooupgrade DirSync, consulte [documentação relacionada](#related-documentation) para obter outros cenários.

## <a name="custom-settings-installation-of-azure-ad-connect"></a>Instalação de definições personalizadas do Azure AD Connect
### <a name="express-settings"></a>Definições Rápidas
Nesta página, clique em **personalizar** toostart uma instalação de definições personalizadas.

### <a name="install-required-components"></a>Instalar os componentes necessários
Ao instalar serviços de sincronização de Olá, pode deixar a secção de configuração opcional Olá desmarcada e o Azure AD Connect configura tudo automaticamente. Configura uma instância do SQL Server 2012 Express LocalDB, criar grupos adequados Olá e atribuir permissões. Se desejar toochange Olá predefinições, pode utilizar Olá tabela toounderstand Olá opções de configuração opcionais que estão disponíveis os seguintes.

![Componentes necessários](./media/active-directory-aadconnect-get-started-custom/requiredcomponents.png)

| Configuração opcional | Descrição |
| --- | --- |
| Utilizar um SQL Server existente |Permite-lhe nome do toospecify Olá do SQL Server e o nome de instância de Olá. Escolha esta opção se já tiver um servidor de base de dados que pretende toouse. Introduza o nome da instância Olá seguido por um vírgula e número de porta no **nome da instância** se o SQL Server não tenha a navegação ativada. |
| Utilizar uma conta de serviço existente |Por predefinição do Azure AD Connect utiliza uma conta de serviço virtuais para toouse de serviços de sincronização de Olá. Se utilizar um SQL server remoto ou utilizar um proxy que requeira autenticação, terá de toouse um **conta de serviço gerida** ou utilize uma conta de serviço no domínio Olá e conhecer a palavra-passe de Olá. Nesses casos, introduza Olá toouse de conta. Certifique-se de utilizador de Olá executar Olá instalação é um SA no SQL Server para que um início de sessão para a conta de serviço Olá pode ser criado. Consulte [Contas e permissões do Azure AD Connect](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) |
| Especificar grupos de sincronização personalizados |Por predefinição o Azure AD Connect cria quatro servidor de local toohello grupos quando são instalados os serviços de sincronização de Olá. Estes grupos são: grupo Administradores, grupo operadores, grupo procura e Olá grupo reposição de palavra-passe. Pode especificar aqui os seus próprios grupos. grupos de Olá devem ser locais no servidor de Olá e não podem estar localizados no domínio de Olá. |

### <a name="user-sign-in"></a>Início de sessão do utilizador
Depois de instalar os componentes de Olá necessário, é-lhe perguntado tooselect os seus utilizadores único método de início de sessão. Olá, a tabela seguinte fornece uma breve descrição das opções disponíveis Olá. Para obter uma descrição completa dos métodos de início de sessão Olá, consulte [sessão do utilizador](active-directory-aadconnect-user-signin.md).

![Início de Sessão de Utilizador](./media/active-directory-aadconnect-get-started-custom/usersignin2.png)

| Opção Início de Sessão Único | Descrição |
| --- | --- |
| Sincronização de Palavra-passe |Os utilizadores são capaz toosign nos serviços de nuvem tooMicrosoft, como o Office 365, utilizando Olá a mesma palavra-passe que utilizam na respetiva rede no local. as palavras-passe de utilizadores de Olá são sincronizado tooAzure AD como um hash de palavra-passe e a autenticação ocorre na nuvem de Olá. Consulte [Sincronização de palavras-passe](active-directory-aadconnectsync-implement-password-synchronization.md) para obter mais informações. |
|Autenticação pass-through (Pré-visualização)|Os utilizadores são capaz toosign nos serviços de nuvem tooMicrosoft, como o Office 365, utilizando Olá a mesma palavra-passe que utilizam na respetiva rede no local.  palavra-passe de utilizadores de Olá é transmitido através do toohello no local do Active Directory controlador toobe validada.
| Federação com o AD FS |Os utilizadores são capaz toosign nos serviços de nuvem tooMicrosoft, como o Office 365, utilizando Olá a mesma palavra-passe que utilizam na respetiva rede no local.  os utilizadores de Olá são redirecionados tootheir no local do AD FS instância toosign no e a autenticação ocorre no local. |
| Não configurar |Nenhuma destas funcionalidades é instalada e configurada. Escolha esta opção se já tiver instalado um servidor de federação de terceiros ou outra solução existente. |
|Ativar o Início de sessão Único|Esta opção está disponível com sincronização de palavra-passe e a autenticação pass-through e fornece um início de sessão único na experiência para os utilizadores de ambiente de trabalho na rede empresarial Olá.  Veja [Início de sessão único](active-directory-aadconnect-sso.md) para obter mais informações. </br>Tenha em atenção para clientes de AD FS esta opção não está disponível porque do AD FS já ofertas Olá mesmo nível de início de sessão único.</br>(se PTA não é libertado em Olá simultâneo)
|Opção Início de Sessão|Esta opção está disponível para clientes de sincronização de palavra-passe e fornece um início de sessão único na experiência para os utilizadores de ambiente de trabalho na rede empresarial Olá.  </br>Veja [Início de sessão único](active-directory-aadconnect-sso.md) para obter mais informações. </br>Tenha em atenção para clientes de AD FS esta opção não está disponível porque do AD FS já ofertas Olá mesmo nível de início de sessão único.


### <a name="connect-tooazure-ad"></a>Ligar tooAzure AD
No ecrã de tooAzure AD Connect de Olá, introduza uma conta de administrador global e a palavra-passe. Se tiver selecionado **federação com o AD FS** na página anterior Olá, não inicie sessão com uma conta num domínio planear tooenable para Federação. Uma recomendação é toouse uma conta no predefinido Olá **onmicrosoft.com** domínio, o que vem com o seu diretório do Azure AD.

Esta conta é apenas utilizado toocreate uma conta de serviço no Azure AD e não é utilizada após a conclusão do Assistente de Olá.  
![Início de Sessão de Utilizador](./media/active-directory-aadconnect-get-started-custom/connectaad.png)

Se a sua conta de administrador global tiver a MFA ativada, terá tooprovide Olá palavra-passe novamente Olá início de sessão no pop-up e concluída Olá desafio MFA. desafio Olá pode ser fornecer um código de verificação ou uma chamada telefónica.  
![Início de Sessão de Utilizador no MFA](./media/active-directory-aadconnect-get-started-custom/connectaadmfa.png)

Também pode ter a conta de administrador global Olá [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md) ativada.

Se receber um erro e tiver problemas com a conectividade, veja [Resolver problemas de conectividade](active-directory-aadconnect-troubleshoot-connectivity.md).

## <a name="pages-under-hello-section-sync"></a>Páginas na secção de Olá sincronização

### <a name="connect-your-directories"></a>Ligar os diretórios
tooconnect tooyour os serviços de domínio do Active Directory, Azure AD Connect tem o nome de floresta de Olá e credenciais de uma conta com permissões suficientes.

![Ligar o Diretório](./media/active-directory-aadconnect-get-started-custom/connectdir01.png)

Depois de introduzir o nome da floresta Olá e clicando em **Adicionar diretório**, uma caixa de diálogo de pop-up aparece e pede-lhe com Olá seguintes opções:

| Opção | Descrição |
| --- | --- |
| Utilizar conta existente | Selecione esta opção se pretender que a conta de tooprovide um existente do AD DS toobe utilizado o Azure AD Connect para ligar a floresta toohello AD durante a sincronização de diretórios. Pode introduzir parte do domínio Olá no formato NetBios ou FQDN, ou seja, FABRIKAM\syncuser ou com\syncuser.. Esta conta pode ser uma conta de utilizador normal, porque apenas tem permissões para ler Olá predefinido. No entanto, dependendo do seu cenário, poderá precisar de mais permissões. Para obter mais informações, veja [Azure AD Connect Accounts and permissions](active-directory-aadconnect-accounts-permissions.md#create-the-ad-ds-account) (Contas e permissões do Azure AD Connet). |
| Criar conta nova | Selecione esta opção se pretender que a conta Olá do AD DS do Azure AD Connect assistente toocreate necessária pelo Azure AD Connect para ligar a floresta toohello AD durante a sincronização de diretórios. Quando esta opção está selecionada, introduza Olá nome de utilizador e palavra-passe para uma conta de administrador de empresa. Olá a conta de administrador de empresa fornecida será utilizada pelo Azure AD Connect Olá do assistente toocreate necessária a conta do AD DS. Pode introduzir parte do domínio Olá no formato NetBios ou FQDN, ou seja, fabrikam\administrador ou com\administrador.. |

![Ligar o Diretório](./media/active-directory-aadconnect-get-started-custom/connectdir02.png)


### <a name="azure-ad-sign-in-configuration"></a>Configuração do início de sessão do Azure AD
Esta página permite-lhe domínios UPN de Olá tooreview presentes no local do AD DS e que foram verificados no Azure AD. Esta página também permite-lhe tooconfigure Olá atributo toouse para Olá userPrincipalName.

![Domínios não verificados](./media/active-directory-aadconnect-get-started-custom/aadsigninconfig.png)  
Reveja todos os domínios marcados como **Não Adicionado** e **Não Verificado**. Certifique-se de que os domínios que utiliza foram verificados no Azure AD. Clique em Símbolo de atualização de Olá quando tiver verificado os domínios. Para obter mais informações, consulte [adicionar e verificar o domínio de Olá](../active-directory-add-domain.md)

**UserPrincipalName** -Olá atributo userPrincipalName é utilizadores de atributo Olá utilizam quando iniciam sessão no tooAzure AD e do Office 365. domínios de Olá utilizado, também conhecido como Olá sufixo UPN, deve ser verificado no Azure AD para que utilizadores Olá estão sincronizados. A Microsoft recomenda tookeep Olá predefinido atributo userPrincipalName. Se este atributo não for encaminhável e não pode ser verificado, em seguida, é possível tooselect outro atributo. Pode, por exemplo, selecionar o correio eletrónico como atributo de Olá que contém o ID de Olá início de sessão. A utilização de um atributo diferente de userPrincipalName é conhecida como **ID Alternativo**. Olá valor do atributo ID alternativo tem de seguir Olá RFC822 padrão. Um ID Alternativo pode ser utilizado na sincronização de palavras-passe e na federação.

>[!NOTE]
> Ao ativar a autenticação pass-through tem de ter, pelo menos, um domínio verificado na ordem toocontinue através do Assistente de Olá.

> [!WARNING]
> A utilização de um ID Alternativo não é compatível com todas as cargas de trabalho do Office 365. Para obter mais informações, consulte demasiado[configurar ID de início de sessão alternativo](https://technet.microsoft.com/library/dn659436.aspx).
>
>

### <a name="domain-and-ou-filtering"></a>Filtragem de domínios e de UOs
Por predefinição, todos os domínios e UOs são sincronizados. Se houver domínios ou UOs que não pretende toosynchronize tooAzure AD, pode desmarcar destes domínios e UOs.  
![Filtragem de DomainOU](./media/active-directory-aadconnect-get-started-custom/domainoufiltering.png)  
Esta página no Assistente de Olá está a configurar filtragem baseada na UO e baseados em domínio. Se planear toomake alterações, consulte [filtragem baseada em domínio](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) e [filtragem baseada na UO](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) antes de efetuar estas alterações. Alguns UOs são essenciais para a funcionalidade de Olá e não devem ser não seleccionados.

Se utilizar a filtragem baseada em UO com uma versão do Azure AD Connect anterior à 1.1.524.0, as novas UOs adicionadas mais tarde são sincronizados por predefinição. Se pretender que o comportamento de Olá nesse novo UOs não devem ser sincronizadas, em seguida, pode configurá-lo após a conclusão do Assistente de Olá com [filtragem baseada na UO](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering). Para o Azure AD Connect versão 1.1.524.0 ou depois, pode indicar se pretende que o novo toobe de UOs sincronizada ou não.

Se planear toouse [filtragem baseada no grupo](#sync-filtering-based-on-groups), em seguida, certifique-se Olá UO com grupo Olá é incluída e não filtrada com a filtragem de UO. A filtragem de UO é avaliado antes da filtragem baseada em grupo.

Também é possível que alguns domínios não estejam acessíveis devido a restrições de toofirewall. Estes domínios estão desmarcados por predefinição e têm um aviso.  
![Domínios inacessíveis](./media/active-directory-aadconnect-get-started-custom/unreachable.png)  
Se vir este aviso, certifique-se de que estes domínios são de facto inacessíveis e Olá aviso é esperado.

### <a name="uniquely-identifying-your-users"></a>Identificar os utilizadores de forma exclusiva

#### <a name="select-how-users-should-be-identified-in-your-on-premises-directories"></a>Selecione a forma como os utilizadores devem ser identificados nos seus diretórios no local
Olá funcionalidade correspondência entre florestas permite-lhe toodefine como os utilizadores a partir de florestas do AD DS são representados no Azure AD. Um utilizador pode ser representado apenas uma vez em todas as florestas ou ter uma combinação de contas ativadas e desativadas. utilizador Olá também pode ser representado como um contacto em algumas florestas.

![Exclusivo](./media/active-directory-aadconnect-get-started-custom/unique.png)

| Definição | Descrição |
| --- | --- |
| [Os utilizadores são representados apenas uma vez em todas as florestas](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Todos os utilizadores são criados como objetos individuais no Azure AD. objetos de Olá não estão associados no metaverso Olá. |
| [Atributo de correio](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Esta opção associa utilizadores e contactos se o atributo de correio Olá tem Olá mesmo valor em florestas diferentes. Utilize esta opção quando os contactos foram criados utilizando GALSync. Se for escolhida esta opção, os objetos de utilizador não são preenchidos cujo atributo de correio não será sincronizado tooAzure AD. |
| [ObjectSID e msExchangeMasterAccountSID/msRTCSIP-OriginatorSid](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Esta opção associa um utilizador ativado numa floresta conta a um utilizador desativado numa floresta de recursos. No Exchange, esta configuração é conhecida como uma caixa de correio ligada. Também pode ser utilizada esta opção se utilizar apenas o Lync e Exchange não está presente na floresta de recursos de Olá. |
| sAMAccountName e MailNickName |Esta opção associa atributos onde é esperado Olá início de sessão no ID de utilizador Olá pode ser encontrado. |
| Um atributo específico |Esta opção permite-lhe tooselect os seus próprios atributos. Se for escolhida esta opção, os objetos de utilizador não são preenchidos cujo atributo (selecionado) não serão sincronizado tooAzure AD. **Limitação:** Certifique-se de que toopick um atributo que já pode ser encontrado no metaverso Olá. Se escolher um atributo personalizado (não no metaverso Olá), não é possível concluir o Assistente de Olá. |

#### <a name="select-how-users-should-be-identified-with-azure-ad---source-anchor"></a>Selecione a forma como os utilizadores devem ser identificados com o Azure AD - Âncora de Origem
Olá atributo sourceAnchor é um atributo que é imutável durante a duração de Olá de um objeto de utilizador. Esta é a chave primária Olá associar utilizadores no local de Olá com utilizador Olá no Azure AD.

| Definição | Descrição |
| --- | --- |
| Permitir que o Azure gerir âncora de origem Olá para mim | Selecione esta opção se pretender o atributo do Azure AD toopick Olá por si. Se selecionar esta opção, o Assistente do Azure AD Connect aplica-se descritos na secção do artigo dos lógica de seleção de atributo para sourceAnchor Olá [do Azure AD Connect: conceitos - utilizando msDS-ConsistencyGuid como sourceAnchor de Design](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). Assistente de Olá informa-o atributo foi selecionado como atributo de âncora de origem Olá após a conclusão da instalação personalizada. |
| Um atributo específico | Selecione esta opção se quiser toospecify um atributo de AD existente como atributo de sourceAnchor Olá. |

Uma vez que não é possível alterar o atributo de Olá, terá de planear um bom atributo toouse. Um bom candidato é objectGUID. Este atributo não é alterado, a menos que a conta de utilizador Olá é movida entre florestas/domínios. Num ambiente de várias floresta onde se movem contas entre florestas, deve ser utilizado outro atributo, tal como um atributo com o campo IDdeEmpregado de Olá. Evite atributos que se alteram quando uma pessoa se casa ou muda de atribuições. Não é possível utilizar atributos com um @-sign, sendo assim o e-mail e userPrincipalName não podem ser utilizados. atributo de Olá também é maiúsculas e minúsculas, por isso, quando mover um objeto entre florestas, certifique-se de que toopreserve Olá maiúsculas/minúsculas. Os atributos binários são codificados em base64, mas outros tipos de atributo permanecem no seu estado não codificado. Em cenários de federação e em algumas interfaces do Azure AD, este atributo é também conhecido como immutableID. Podem encontrar mais informações sobre a âncora de origem Olá no Olá [conceitos de design](active-directory-aadconnect-design-concepts.md#sourceanchor).

### <a name="sync-filtering-based-on-groups"></a>Filtragem de sincronização baseada em grupos
Olá filtragem funcionalidade grupos permite-lhe toosync apenas um pequeno subconjunto de objetos para um piloto. toouse esta funcionalidade, crie um grupo para este efeito no Active Directory no local. Em seguida, adicione utilizadores e grupos que devem ser sincronizado tooAzure AD como membros diretos. Mais tarde, pode adicionar e remover a lista de utilizadores toothis grupo toomaintain Olá de objetos que deve estar presente no Azure AD. Todos os objetos que pretende toosynchronize tem de ser membros diretos do grupo de Olá. Os utilizadores, grupos, contactos e computadores/dispositivos têm de ser todos membros diretos. A associação a grupos aninhados não é resolvida. Quando adiciona um grupo como um membro, apenas Olá grupo é adicionado e não os seus membros.

![Filtragem de sincronização](./media/active-directory-aadconnect-get-started-custom/filter2.png)

> [!WARNING]
> Esta funcionalidade é apenas pretendido toosupport uma implementação piloto. Não a utilize numa implementação de produção autêntica.
>
>

Numa implementação de produção autêntica, pretender toobe rígido toomaintain um único grupo com todos os objetos toosynchronize. Em vez disso, deve utilizar um dos métodos de Olá no [configurar filtragem](active-directory-aadconnectsync-configure-filtering.md).

### <a name="optional-features"></a>Funcionalidades Opcionais
Este ecrã permite-lhe tooselect Olá as funcionalidades opcionais para os seus cenários específicos.

![Funcionalidades opcionais](./media/active-directory-aadconnect-get-started-custom/optional.png)

> [!WARNING]
> Se tiver atualmente o DirSync ou o Azure AD Sync Active Directory, não ative nenhuma das funcionalidades de repetição de escrita de Olá no Azure AD Connect.
>
>

| Funcionalidades Opcionais | Descrição |
| --- | --- |
| Implementação Híbrida do Exchange |Olá funcionalidade implementação híbrida do Exchange permite Olá coexistência de caixas de correio do Exchange no local e no Office 365. O Azure AD Connect está a sincronizar um conjunto específico de [atributos](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback) do Azure AD para o diretório no local. |
| Pastas Públicas de Correio do Exchange | funcionalidade de pastas públicas do Exchange correio Olá permite-lhe toosynchronize objetos de pasta pública com capacidade de correio da sua tooAzure do Active Directory no local AD. |
| Aplicação Azure AD e filtragem de atributos |Ao ativar a aplicação Azure AD e filtragem de atributos, hello conjunto de atributos sincronizados pode ser adaptado. Esta opção adiciona dois mais páginas toohello o Assistente de configuração. Para obter mais informações, consulte [Aplicação Azure AD e filtragem de atributos](#azure-ad-app-and-attribute-filtering). |
| Sincronização de palavras-passe |Se tiver selecionado a Federação como solução de início de sessão Olá, em seguida, pode ativar esta opção. A sincronização de palavras-passe pode ser utilizada como uma opção de cópia de segurança. Para obter mais informações, consulte [Sincronização de palavras-passe](active-directory-aadconnectsync-implement-password-synchronization.md). </br></br>Se tiver selecionado autenticação pass-through esta opção está ativada por predefinição tooensure suporte para clientes legados e como uma opção de cópia de segurança. Para obter mais informações, consulte [Sincronização de palavras-passe](active-directory-aadconnectsync-implement-password-synchronization.md).|
| Repetição de escrita de palavras-passe |Ao ativar a repetição de escrita de palavras-passe, as alterações de palavra-passe que têm origem no Azure AD não são gravados diretório no local de tooyour. Para mais informações, consulte [Introdução à gestão de palavras-passe](../active-directory-passwords-getting-started.md) |
| Repetição de escrita do grupo |Se utilizar Olá **grupos do Office 365** funcionalidade, pode ter estes grupos representados no Active Directory no local. Esta opção só está disponível se tiver o Exchange presente no Active Directory no local. Para obter mais informações, consulte [Repetição de escrita do grupo](active-directory-aadconnect-feature-preview.md#group-writeback). |
| Repetição de escrita do dispositivo |Permite-lhe toowriteback os objetos de dispositivo no Azure AD tooyour no local do Active Directory para cenários de acesso condicional. Para mais informações, consulte [Ativar a repetição de escrita do dispositivo no Azure AD Connect](active-directory-aadconnect-feature-device-writeback.md). |
| Sincronização de atributos de extensões de diretórios |Ao ativar a sincronização de atributos de extensões de diretórios, os atributos especificados são sincronizado tooAzure AD. Para obter mais informações, consulte [Extensões de diretórios](active-directory-aadconnectsync-feature-directory-extensions.md). |

### <a name="azure-ad-app-and-attribute-filtering"></a>Aplicação Azure AD e filtragem de atributos
Se quiser toolimit que tooAzure toosynchronize de atributos AD, em seguida, comece por selecionar os serviços que está a utilizar. Se efetuar alterações de configuração nesta página, um novo serviço tem toobe explicitamente selecionado executando o Assistente de instalação de Olá.

![Aplicações de funcionalidades opcionais](./media/active-directory-aadconnect-get-started-custom/azureadapps2.png)

Com base nos serviços de Olá selecionados no passo anterior Olá, esta página mostra todos os atributos que são sincronizados. Esta lista é uma combinação de todos os tipos de objetos que estão a ser sincronizados. Se existirem alguns atributos específicos terá toonot sincronizar, pode desmarcar esses atributos.

![Atributos de funcionalidades opcionais](./media/active-directory-aadconnect-get-started-custom/azureadattributes2.png)

> [!WARNING]
> A remoção de atributos pode afetar a funcionalidade. Para obter as melhores práticas e recomendações, consulte [tributos sincronizados](active-directory-aadconnectsync-attributes-synchronized.md#attributes-to-synchronize).
>
>

### <a name="directory-extension-attribute-sync"></a>Sincronização de atributos de Extensões de Diretórios
Pode expandir o esquema de Olá no Azure AD com atributos personalizados adicionados através da organização ou outros atributos no Active Directory. toouse esta funcionalidade, selecione **sincronização de atributos de extensão de diretório** no Olá **funcionalidades opcionais** página. Pode selecionar mais atributos toosync nesta página.

![Extensões de diretórios](./media/active-directory-aadconnect-get-started-custom/extension2.png)

Para obter mais informações, consulte [Extensões de diretórios](active-directory-aadconnectsync-feature-directory-extensions.md).

### <a name="enabling-single-sign-on-sso"></a>Ativar o Início de sessão único (SSO)
Configurar o início de sessão para utilização com a autenticação de sincronização de palavra-passe ou pass-through é um processo simple que apenas terá de toocomplete uma vez para cada floresta que está a ser sincronizado tooAzure AD. A configuração envolve dois passos da seguinte forma:

1.  Crie conta de computador necessários Olá no Active Directory no local.
2.  Configure a zona de intranet Olá das máquinas de cliente Olá toosupport único início de sessão.

#### <a name="create-hello-computer-account-in-active-directory"></a>Criar conta de computador Olá no Active Directory
Para cada floresta que tenha sido adicionada no Azure AD Connect, terá as credenciais de administrador de domínio de toosupply para que a conta de computador Olá pode ser criada em cada floresta. credenciais de Olá são apenas utilizadas toocreate Olá conta e não são armazenadas ou utilizadas em nenhuma outra operação. Basta adicionar credenciais Olá Olá **ativar o único início de sessão** página do Olá do Azure AD Connect assistente conforme mostrado:

![Ativar o Início de sessão único](./media/active-directory-aadconnect-get-started-custom/enablesso.png)

>[!NOTE]
>Pode ignorar uma determinado floresta se não desejar toouse início de sessão único dessa floresta.

#### <a name="configure-hello-intranet-zone-for-client-machines"></a>Configurar a zona de Intranet Olá para computadores cliente do
tooensure que Olá cliente inícios de sessão automaticamente na intranet Olá zona precisa de tooensure se os dois URLs fazem parte da zona de intranet Olá. Isto garante que esse computador associado a domínio Olá envia automaticamente um tooAzure de permissão de Kerberos AD quando é ligado toohello rede empresarial.
Num computador que tem as ferramentas de gestão de política de grupo Olá.

1.  Abrir ferramentas de gestão de política de grupo de Olá
2.  Edite política de grupo Olá que serão aplicados tooall utilizadores. Por exemplo, Olá política de domínio predefinida.
3.  Navegue demasiado**utilizador computador\Modelos administrativos\Componentes Components\Internet Explorer\Internet controlo Panel\Security página** e selecione **tooZone lista de atribuição de Site** por imagem Olá abaixo.
4.  Ativar política de Olá e introduza Olá seguintes dois itens na caixa de diálogo Olá.

        Value: `https://autologon.microsoftazuread-sso.com`  
        Data: 1  
        Value: `https://aadg.windows.net.nsatc.net`  
        Data: 1

5.  Deve ser semelhante toohello seguinte:  
![Zonas da Intranet](./media/active-directory-aadconnect-get-started-custom/sitezone.png)

6.  Clique em **OK** duas vezes.

## <a name="configuring-federation-with-ad-fs"></a>Configurar a federação com o AD FS
Configurar o AD FS com o Azure AD Connect é simples, bastam apenas alguns cliques. seguinte Olá é necessário para que a configuração de Olá.

* Um servidor do Windows Server 2012 R2 para o servidor de Federação Olá com a gestão remota ativada
* Um servidor do Windows Server 2012 R2 para o servidor de Proxy de aplicações Web Olá com a gestão remota ativada
* Um certificado SSL para a Federação Olá service nome toouse (por exemplo, sts.contoso.com)

### <a name="ad-fs-configuration-pre-requisites"></a>Pré-requisitos de configuração do AD FS
tooconfigure do AD FS com o Azure AD Connect do farm, certifique-se de que WinRM está ativado em servidores remotos Olá. Além disso, passam pelo requisitos de portas de Olá listados no [tabela 3 – Azure AD Connect e os servidores de Federação/WAP](active-directory-aadconnect-ports.md#table-3---azure-ad-connect-and-ad-fs-federation-serverswap).

### <a name="create-a-new-ad-fs-farm-or-use-an-existing-ad-fs-farm"></a>Criar um novo farm do AD FS ou utilizar um existente
Pode utilizar um farm do AD FS existente ou pode escolher toocreate um novo farm do AD FS. Se optar por toocreate um novo, é certificado SSL de Olá tooprovide necessária. Se o certificado SSL Olá estiver protegido por uma palavra-passe, é-lhe pedida a palavra-passe de Olá.

![Farm do AD FS](./media/active-directory-aadconnect-get-started-custom/adfs1.png)

Se optar por toouse um farm do AD FS existente, é direcionado diretamente toohello configurar relação de confiança Olá entre ecrã do AD FS e o Azure AD.

### <a name="specify-hello-ad-fs-servers"></a>Especifique os servidores de Olá do AD FS
Introduza Olá servidores que pretende tooinstall do AD FS nos. Pode adicionar um ou mais servidores com base nas suas necessidades de planeamento da capacidade. Associe todos os servidores tooActive diretório antes de efetuar esta configuração. A Microsoft recomenda a instalação de um único servidor do AD FS para implementações de teste e piloto. Em seguida, adicione e implemente mais servidores toomeet suas necessidades de dimensionamento, executando o Azure AD Connect novamente após a configuração inicial.

> [!NOTE]
> Certifique-se de que todos os servidores AD de tooan associado ao domínio antes de efetuar esta configuração.
>
>

![Servidores do AD FS](./media/active-directory-aadconnect-get-started-custom/adfs2.png)

### <a name="specify-hello-web-application-proxy-servers"></a>Especifique os servidores de Proxy de aplicações Web Olá
Introduza Olá servidores que pretende que os servidores de proxy de aplicação Web. o servidor de proxy de aplicações Olá web é implementado no DMZ (com acesso à extranet) e suporta pedidos de autenticação de Olá extranet. Pode adicionar um ou mais servidores com base nas suas necessidades de planeamento da capacidade. A Microsoft recomenda a instalação de um único servidor proxy de aplicação Web para implementações de teste e piloto. Em seguida, adicione e implemente mais servidores toomeet suas necessidades de dimensionamento, executando o Azure AD Connect novamente após a configuração inicial. Recomenda-se ter um número equivalente de autenticação de toosatisfy de servidores de proxy de intranet Olá.

> [!NOTE]
> <li> Se a conta de Olá que utilizar não é um administrador local nos servidores de Olá do AD FS, em seguida, lhe forem pedidas as credenciais de administrador.</li>
> <li> Certifique-se de que existe conectividade HTTP/HTTPS entre servidores do Azure AD Connect de Olá e Olá Proxy de aplicações Web antes de executar este passo.</li>
> <li> Certifique-se de que existe conectividade HTTP/HTTPS entre hello do servidor de aplicações Web e Olá AD FS server tooallow autenticação pedidos tooflow através de.</li>
>

![Aplicação Web](./media/active-directory-aadconnect-get-started-custom/adfs3.png)

São credenciais tooenter pedido para que hello servidor de aplicações web pode estabelecer um servidor do ligação segura toohello AD FS. Estas credenciais têm toobe um administrador local no servidor do AD FS de Olá.

![Proxy](./media/active-directory-aadconnect-get-started-custom/adfs4.png)

### <a name="specify-hello-service-account-for-hello-ad-fs-service"></a>Especifique a conta de serviço Olá para Olá serviço AD FS
serviço de Olá AD FS requer um domínio informações do utilizador de pesquisa no Active Directory e os utilizadores tooauthenticate da conta de serviço. Pode suportar dois tipos de contas de serviço:

* **Conta de Serviço Gerida de Grupo** – introduzida nos Serviços de Domínio do Active Directory com o Windows Server 2012. Este tipo de conta fornece serviços, como o AD FS, uma conta única sem necessitar de palavra-passe de conta de Olá tooupdate regularmente. Utilize esta opção se já tiver controladores de domínio do Windows Server 2012 no domínio Olá que pertencem os servidores do AD FS.
* **Conta de utilizador de domínio** -este tipo de conta requer tooprovide uma palavra-passe e regularmente a palavra-passe Olá de atualização quando a palavra-passe de Olá alterada ou expira. Utilize esta opção apenas quando não tiver controladores de domínio do Windows Server 2012 no domínio Olá que pertencem os servidores do AD FS.

Se tiver selecionado a Conta de Serviço Gerida de Grupo e esta funcionalidade nunca tiver sido utilizada no Active Directory, ser-lhe-ão pedidas as credenciais de Administrador de Empresa. Estas credenciais são armazenamento de chaves de Olá tooinitiate utilizado e ativar a funcionalidade de Olá no Active Directory.

> [!NOTE]
> O Azure AD Connect efetua uma toodetect de verificação se o serviço do Olá AD FS já está registado como um SPN no domínio Olá.  AD DS não permitirá toobe duplicado SPN registado em simultâneo.  Se for encontrado um SPN duplicado, não será capaz de tooproceed mais enquanto Olá SPN não for removido.

![Conta de Serviço do AD FS](./media/active-directory-aadconnect-get-started-custom/adfs5.png)

### <a name="select-hello-azure-ad-domain-that-you-wish-toofederate"></a>Selecione o domínio de Olá do Azure AD que pretende toofederate
Esta configuração é utilizada toosetup Olá Federação relação entre o AD FS e o Azure AD. Configura o tooAzure de tokens de segurança do AD FS tooissue AD e configura tokens de Olá tootrust do Azure AD desta instância específica do AD FS. Esta página permite-lhe apenas tooconfigure um único domínio na instalação inicial Olá. Pode configurar mais domínios posteriormente, executando novamente o Azure AD Connect.

![Domínio do Azure AD](./media/active-directory-aadconnect-get-started-custom/adfs6.png)

### <a name="verify-hello-azure-ad-domain-selected-for-federation"></a>Verifique o domínio de Olá do Azure AD selecionado para Federação
Quando seleciona Olá toobe de domínio federado, o Azure AD Connect fornece-lhe as informações necessárias tooverify um domínio não verificado. Consulte [adicionar e verificar o domínio de Olá](../active-directory-add-domain.md) como toouse estas informações.

![Domínio do Azure AD](./media/active-directory-aadconnect-get-started-custom/verifyfeddomain.png)

> [!NOTE]
> Domínio do AD Connect tenta tooverify Olá durante Olá configurar fase. Se continuar tooconfigure sem adicionar registos DNS necessários do Olá, o Assistente de Olá configuração não é capaz de toocomplete Olá.
>
>

## <a name="configure-and-verify-pages"></a>Páginas de configuração e verificação
a configuração de Olá ocorre nesta página.

> [!NOTE]
> Antes de prosseguir com a instalação e se tiver configurado a federação, certifique-se de que configurou a [Resolução de nomes dos servidores de federação](active-directory-aadconnect-prerequisites.md#name-resolution-for-federation-servers).
>
>

![Tooconfigure pronto](./media/active-directory-aadconnect-get-started-custom/readytoconfigure2.png)

### <a name="staging-mode"></a>Modo de teste
É possível toosetup um novo servidor de sincronização em paralelo com modo de teste. É apenas suportado toohave um servidor de sincronização exportar tooone diretório na nuvem de Olá. Mas, se quiser toomove a partir de outro servidor, por exemplo um a executar o DirSync, em seguida, pode ativar o Azure AD Connect no modo de teste. Quando ativada, a sincronização de Olá motor importar e sincronizar os dados como normal, mas não exporta nada tooAzure AD ou o AD. Olá funcionalidades palavra-passe sincronização e a palavra-passe de repetição de escrita estão desativados enquanto estiver no modo de teste.

![Modo de teste](./media/active-directory-aadconnect-get-started-custom/stagingmode.png)

Enquanto estiver no modo de teste, é o motor de sincronização do toomake possíveis as alterações necessárias toohello e rever o que é sobre toobe exportado. Quando a configuração de Olá procura boa, execute novamente o Assistente de instalação de Olá e desativar o modo de teste. Os dados estão agora exportado tooAzure AD deste servidor. Certifique-se de que toodisable Olá outro servidor ao hello mesmo tempo, por isso, apenas um servidor a exportar ativamente.

Para obter mais informações, consulte [Modo de teste](active-directory-aadconnectsync-operations.md#staging-mode).

### <a name="verify-your-federation-configuration"></a>Verificar a configuração de federação
O Azure AD Connect verifica as definições de DNS Olá ao clicar no botão de verifique Olá.

**Verificações de conectividade de intranet**

* Resolver o FQDN de Federação: o Azure AD Connect verifica se a Federação Olá FQDN pode ser resolvida através da conectividade de tooensure DNS. Se o Azure AD Connect não é possível resolver o FQDN de Olá, verificação de Olá irá falhar. Certifique-se de que existe um registo DNS para FQDN de serviço de Federação Olá na verificação do ordem toosuccessfully Olá concluída.
* Registo A de DNS: o Azure AD Connect verifica se existe um registo A para o seu serviço de federação. Na ausência de Olá de um registo, a verificação de Olá irá falhar. Criar um um registo e não registo CNAME para o FQDN de Federação na ordem toosuccessfully concluir a verificação de Olá.

**Verificações de conectividade de extranet**

* Resolver o FQDN de Federação: o Azure AD Connect verifica se a Federação Olá FQDN pode ser resolvida através da conectividade de tooensure DNS.

![Concluir](./media/active-directory-aadconnect-get-started-custom/completed.png)

![Verificar](./media/active-directory-aadconnect-get-started-custom/adfs7.png)

Além disso, execute Olá seguindo os passos de verificação:

* Confirme que pode iniciar sessão num browser de computador associado a um domínio na intranet Olá: ligar toohttps://myapps.microsoft.com e certifique-se Olá início de sessão com a sua conta com sessão iniciada. conta de administrador Olá incorporada AD DS não está sincronizada e não pode ser utilizada para verificação.
* Confirme que pode iniciar sessão a partir de um dispositivo de Olá extranet. Num computador doméstico ou um dispositivo móvel, ligue toohttps://myapps.microsoft.com e forneça as credenciais.
* Valide o início de sessão de cliente avançado. Ligar toohttps://testconnectivity.microsoft.com, escolha Olá **do Office 365** Olá separador e escolha **Office 365 Sign-On teste único**.

## <a name="next-steps"></a>Passos seguintes
Após a conclusão da instalação Olá, termine e inicie sessão novamente tooWindows antes de utilizar o Synchronization Service Manager ou Editor de regras de sincronização.

Agora que tem o Azure AD Connect instalado, pode [verificar Olá instalação e atribuir licenças](active-directory-aadconnect-whats-next.md).

Saiba mais acerca destas funcionalidades que foram ativadas com a instalação de Olá: [impedir eliminações acidentais](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) e [do Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Saiba mais acerca destes tópicos comuns: [Agendador e como sincronizar tootrigger](active-directory-aadconnectsync-feature-scheduler.md).

Saiba mais sobre como [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md).
