---
title: "Azure AD Connect: Instalação personalizada | Microsoft Docs"
description: "Este documento fornece detalhes sobre as opções de instalação personalizada do Azure AD Connect. Utilize estas instruções para instalar o Active Directory através do Azure AD Connect."
services: active-directory
keywords: "o que é o Azure AD Connect, instale o Active Directory, componentes precisos para o Azure AD"
documentationcenter: 
author: billmath
manager: mtillman
ms.assetid: 6d42fb79-d9cf-48da-8445-f482c4c536af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/02/2018
ms.author: billmath
ms.openlocfilehash: a12bd2ec296acfb810c8805c92941e5bf70c6ccb
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/03/2018
---
# <a name="custom-installation-of-azure-ad-connect"></a>Instalação personalizada do Azure AD Connect
As **Definições personalizadas** do Azure AD Connect são utilizadas quando pretende mais opções para a instalação. São utilizadas se tiver várias florestas ou se pretender configurar funcionalidades opcionais não abrangidas na instalação rápida. São utilizadas em todos os casos em que a opção [**instalação rápida**](active-directory-aadconnect-get-started-express.md) não satisfaz a sua implementação ou topologia.

Antes de começar a instalar o Azure AD Connect, certifique-se de que [transferiu o Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) e concluiu os pré-requisitos indicados em [Azure AD Connect: Hardware e pré-requisitos](active-directory-aadconnect-prerequisites.md). Certifique-se também de que tem disponíveis as contas necessárias, conforme descrito em [Contas e permissões do Azure AD Connect](active-directory-aadconnect-accounts-permissions.md).

Se as definições personalizadas não coincidirem com a topologia, por exemplo, para atualizar o DirSync, consulte [documentação relacionada](#related-documentation) para obter outros cenários.

## <a name="custom-settings-installation-of-azure-ad-connect"></a>Instalação de definições personalizadas do Azure AD Connect
### <a name="express-settings"></a>Definições Rápidas
Nesta página, clique em **Personalizar** para iniciar uma instalação de definições personalizadas.

### <a name="install-required-components"></a>Instalar os componentes necessários
Quando instalar os serviços de sincronização, pode deixar a secção de configuração opcional desmarcada e o Azure AD Connect configura tudo automaticamente. Configura uma instância do SQL Server 2012 Express LocalDB, cria os grupos adequados e atribui permissões. Se pretender alterar as predefinições, pode utilizar a tabela seguinte para entender as opções de configuração opcionais que estão disponíveis.

![Componentes necessários](./media/active-directory-aadconnect-get-started-custom/requiredcomponents.png)

| Configuração opcional | Descrição |
| --- | --- |
| Utilizar um SQL Server existente |Permite-lhe especificar o nome do SQL Server e o nome da instância. Escolha esta opção se já tiver um servidor de base de dados que pretende utilizar. Introduza o nome da instância, seguido de uma vírgula e do número de porta em **Nome da Instância**, caso o SQL Server não tenha a navegação ativada. |
| Utilizar uma conta de serviço existente |Por predefinição, o Azure AD Connect utiliza uma conta de serviço virtual para ser utilizada pelos serviços de sincronização. Se utilizar um servidor do SQL remoto ou um proxy que exija a autenticação, tem de utilizar uma **conta de serviço gerido** ou utilizar uma conta de serviço no domínio e conhecer a palavra-passe. Nesses casos, introduza a conta a utilizar. Certifique-se de que o utilizador que está a executar a instalação é um SA no SQL Server, para possa ser criado um início sessão para a conta de serviço. Consulte [Contas e permissões do Azure AD Connect](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) |
| Especificar grupos de sincronização personalizados |Por predefinição, o Azure AD Connect cria quatro grupos locais no servidor quando são instalados os serviços de sincronização. Estes grupos são: grupo Administradores, grupo Operadores, grupo Procura e grupo Reposição de Palavra-passe. Pode especificar aqui os seus próprios grupos. Os grupos têm de ser locais no servidor e não podem estar localizados no domínio. |

### <a name="user-sign-in"></a>Início de sessão do utilizador
Depois de instalar os componentes necessários, é-lhe pedido que selecione o método de início de sessão único dos utilizadores. A tabela seguinte fornece uma breve descrição das opções disponíveis. Para obter uma descrição completa dos métodos de início de sessão, consulte [Início de sessão do utilizador](active-directory-aadconnect-user-signin.md).

![Início de Sessão de Utilizador](./media/active-directory-aadconnect-get-started-custom/usersignin2.png)

| Opção Início de Sessão Único | Descrição |
| --- | --- |
| Sincronização hash de palavra-passe |Os utilizadores podem iniciar sessão nos Cloud Services da Microsoft, como o Office 365, utilizando a mesma palavra-passe que utilizam na respetiva rede no local. As palavras-passe dos utilizadores são sincronizadas para o Azure AD como um hash de palavra-passe e a autenticação ocorre na nuvem. Para obter mais informações, veja [Password hash synchronization (Sincronização hash de palavra-passe)](active-directory-aadconnectsync-implement-password-synchronization.md). |
|Autenticação pass-through|Os utilizadores podem iniciar sessão nos Cloud Services da Microsoft, como o Office 365, utilizando a mesma palavra-passe que utilizam na respetiva rede no local.  A palavra-passe dos utilizadores é transmitida para o controlador de domínio do Active Directory no local para ser validada.
| Federação com o AD FS |Os utilizadores podem iniciar sessão nos Cloud Services da Microsoft, como o Office 365, utilizando a mesma palavra-passe que utilizam na respetiva rede no local.  Os utilizadores serão redirecionados para a respetiva instância do AD FS no local para iniciarem sessão e a autenticação ocorre no local. |
| Não configurar |Nenhuma funcionalidade de início de sessão de utilizador é instalada e configurada. Escolha esta opção se já tiver instalado um servidor de federação de terceiros ou outra solução existente. |
|Ativar o Início de sessão Único|Esta opção está disponível com sincronização de palavras-passe e autenticação pass-through e proporciona uma experiência de início de sessão único para utilizadores de ambiente de trabalho na rede da empresa. Veja [Início de sessão único](active-directory-aadconnect-sso.md) para obter mais informações. </br>Nota para clientes do AD FS: esta opção não está disponível porque o AD FS já oferece o mesmo nível de início de sessão único.</br>

### <a name="connect-to-azure-ad"></a>Ligar ao Azure AD
No ecrã Ligar ao Azure AD, introduza uma conta de administrador global e a palavra-passe. Se tiver selecionado **Federação com o AD FS** na página anterior, não inicie sessão com uma conta num domínio que pretenda ativar para federação. Uma das recomendações é utilizar uma conta no domínio predefinido **onmicrosoft.com**, incluído com o diretório do Azure AD.

Esta conta é utilizada apenas para criar uma conta de serviço no Azure AD e deixa de ser utilizada uma vez concluído o assistente.  
![Início de Sessão de Utilizador](./media/active-directory-aadconnect-get-started-custom/connectaad.png)

Se a conta de administrador global tiver a MFA ativada, terá de fornecer novamente a palavra-passe no pop-up início de sessão e completar o desafio MFA. O desafio pode ser fornecer um código de verificação ou uma chamada telefónica.  
![Início de Sessão de Utilizador no MFA](./media/active-directory-aadconnect-get-started-custom/connectaadmfa.png)

A conta de administrador global também pode ter a opção [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md) ativada.

Se receber um erro e tiver problemas com a conectividade, veja [Resolver problemas de conectividade](active-directory-aadconnect-troubleshoot-connectivity.md).

## <a name="pages-under-the-sync-section"></a>Páginas na secção Sincronização

### <a name="connect-your-directories"></a>Ligar os diretórios
Para ligar ao seu serviço do Active Directory Domain Services, o Azure AD Connect precisa do nome da floresta e das credenciais de uma conta com permissões suficientes.

![Ligar o Diretório](./media/active-directory-aadconnect-get-started-custom/connectdir01.png)

Depois de introduzir o nome da floresta e de clicar em **Adicionar Diretório**, é apresentada uma caixa de diálogo de pop-up que mostra as opções seguintes:

| Opção | Descrição |
| --- | --- |
| Criar conta nova | Selecione esta opção se quiser que o assistente do Azure AD Connect crie a conta do AD DS de que precisa para ligar à floresta do AD durante a sincronização de diretórios. Se esta opção estiver selecionada, introduza o nome de utilizador e a palavra-passe de uma conta de administrador empresarial. O assistente do Azure AD Connect vai utilizar a conta de administrador empresarial indicada para criar a conta do AD DS necessária. Pode introduzir a parte do domínio no formato NetBios ou FQDN, ou seja, FABRIKAM\administrator ou fabrikam.com\administrator. |
| Utilizar conta existente | Selecione esta opção se quiser indicar uma conta do AD DS existente para ser utilizada com o Azure AD Connect para ligar à floresta do AD durante a sincronização de diretórios. Pode introduzir a parte do domínio no formato NetBios ou FQDN, ou seja, FABRIKAM\syncuser ou fabrikam.com\syncuser. Esta conta pode ser uma conta de utilizador normal, porque precisa apenas das permissões de leitura predefinidas. No entanto, dependendo do seu cenário, poderá precisar de mais permissões. Para obter mais informações, veja [Azure AD Connect Accounts and permissions](active-directory-aadconnect-accounts-permissions.md#create-the-ad-ds-account) (Contas e permissões do Azure AD Connet). |

![Ligar o Diretório](./media/active-directory-aadconnect-get-started-custom/connectdir02.png)

### <a name="azure-ad-sign-in-configuration"></a>Configuração do início de sessão do Azure AD
Esta página permite-lhe rever os domínios UPN presentes no AD DS no local e que foram verificados no Azure AD. Esta página também lhe permite configurar o atributo a utilizar para userPrincipalName.

![Domínios não verificados](./media/active-directory-aadconnect-get-started-custom/aadsigninconfig.png)  
Reveja todos os domínios marcados como **Não Adicionado** e **Não Verificado**. Certifique-se de que os domínios que utiliza foram verificados no Azure AD. Quando tiver verificado os domínios, clique no símbolo de atualização. Para obter mais informações, consulte [Adicionar e verificar o domínio](../active-directory-domains-add-azure-portal.md)

**UserPrincipalName** -o atributo userPrincipalName é o atributo que os utilizadores utilizam quando iniciam sessão no Azure AD e no Office 365. O domínio utilizado, também conhecido como sufixo UPN, deve ser verificado no Azure AD para que os utilizadores possam ser sincronizados. A Microsoft recomenda que mantenha o atributo predefinido userPrincipalName. Se este atributo não for encaminhável e não puder ser verificado, é possível selecionar outro atributo. Pode, por exemplo, selecionar o correio eletrónico como o atributo que contém o ID de início de sessão. A utilização de um atributo diferente de userPrincipalName é conhecida como **ID Alternativo**. O valor do atributo ID Alternativo tem de seguir a norma RFC822. Um ID Alternativo pode ser utilizado na sincronização de palavras-passe e na federação. O atributo não pode ser definido no Active Directory como com múltiplos valores, mesmo se tiver apenas um valor único.

>[!NOTE]
> Ao ativar a Autenticação Pass-through tem de ter, pelo menos, um domínio verificado para continuar através do assistente.

> [!WARNING]
> A utilização de um ID Alternativo não é compatível com todas as cargas de trabalho do Office 365. Para obter mais informações, veja [Configurar ID de Início de Sessão Alternativo](https://technet.microsoft.com/library/dn659436.aspx).
>
>

### <a name="domain-and-ou-filtering"></a>Filtragem de domínios e de UOs
Por predefinição, todos os domínios e UOs são sincronizados. Se houver domínios ou UOs que não pretende sincronizar com o Azure AD, pode anular a seleção destes domínios e UOs.  
![Filtragem de DomainOU](./media/active-directory-aadconnect-get-started-custom/domainoufiltering.png)  
Esta página no assistente está a configurar filtragem baseada no domínio ou em UO. Se pretender efetuar alterações, consulte [filtragem baseada em domínio](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) e [filtragem baseada em UO](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) antes de efetuar estas alterações. Algumas UOs são essenciais para a funcionalidade e devem estar selecionadas.

Se utilizar a filtragem baseada em UO com uma versão do Azure AD Connect anterior à 1.1.524.0, as novas UOs adicionadas mais tarde são sincronizados por predefinição. Se quiser optar pelo comportamento em que as UOs não são sincronizadas, pode configurar essa opção mais tarde, depois de o assistente terminar a [filtragem baseada em UO](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering). Na versão 1.1.524.0 ou posterior do Azure AD Connect, pode indicar se quer que as UOs novas sejam sincronizadas ou não.

Se planeia utilizar a [filtragem baseada em grupo](#sync-filtering-based-on-groups), certifique-se de que a UO com o grupo é incluída e não é filtrada com filtragem de UO. A filtragem de UO é avaliado antes da filtragem baseada em grupo.

Também é possível que alguns domínios não estejam acessíveis devido a restrições de firewall. Estes domínios estão desmarcados por predefinição e têm um aviso.  
![Domínios inacessíveis](./media/active-directory-aadconnect-get-started-custom/unreachable.png)  
Se vir este aviso, certifique-se de que estes domínios são de facto inacessível e que o aviso é esperado.

### <a name="uniquely-identifying-your-users"></a>Identificar os utilizadores de forma exclusiva

#### <a name="select-how-users-should-be-identified-in-your-on-premises-directories"></a>Selecione a forma como os utilizadores devem ser identificados nos seus diretórios no local
A funcionalidade Correspondência entre florestas permite-lhe definir o modo como são representados no Azure AD os utilizadores das florestas do AD DS. Um utilizador pode ser representado apenas uma vez em todas as florestas ou ter uma combinação de contas ativadas e desativadas. O utilizador também pode ser representado como um contacto em algumas florestas.

![Exclusivo](./media/active-directory-aadconnect-get-started-custom/unique.png)

| Definição | Descrição |
| --- | --- |
| [Os utilizadores são representados apenas uma vez em todas as florestas](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Todos os utilizadores são criados como objetos individuais no Azure AD. Os objetos não estão associados no metaverso. |
| [Atributo de correio](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Esta opção associa utilizadores e contactos se o atributo de correio tiver o mesmo valor em florestas diferentes. Utilize esta opção quando os contactos foram criados utilizando GALSync. Se esta opção for escolhida, os objetos de Utilizador cujo atributo Mail não estiver preenchido não será sincronizados com o Azure AD. |
| [ObjectSID e msExchangeMasterAccountSID/msRTCSIP-OriginatorSid](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Esta opção associa um utilizador ativado numa floresta conta a um utilizador desativado numa floresta de recursos. No Exchange, esta configuração é conhecida como uma caixa de correio ligada. Também pode ser utilizada esta opção se utilizar apenas o Lync e o Exchange não estiver presente na floresta de recursos. |
| sAMAccountName e MailNickName |Esta opção associa atributos em que se espera que o ID de início de sessão do utilizador possa ser encontrado. |
| Um atributo específico |Esta opção permite-lhe selecionar o seu próprio atributo. Se esta opção for escolhida, os objetos de Utilizador cujo atributo (selecionado) não estiver preenchido não serão sincronizados com o Azure AD. **Limitação:** certifique-se de que escolhe um atributo que já pode ser encontrado no metaverso. Se escolher um atributo personalizado (não no metaverso), não é possível concluir o assistente. |

#### <a name="select-how-users-should-be-identified-with-azure-ad---source-anchor"></a>Selecione a forma como os utilizadores devem ser identificados com o Azure AD - Âncora de Origem
O atributo sourceAnchor é imutável durante o ciclo de vida de um objeto de utilizador. É a chave primária da ligação do utilizador no local com o utilizador no Azure AD.

| Definição | Descrição |
| --- | --- |
| Permitir que seja o Azure a gerir a âncora de por mim | Selecione esta opção se pretender que o Azure AD escolha o atributo por si. Se selecionar esta opção, o assistente do Azure AD Connect aplica a lógica de seleção do atributo sourceAnchor descrita na secção do artigo [Azure AD Connect: Design concepts - Using msDS-ConsistencyGuid as sourceAnchor](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor) (Azure AD Connect: Criar conceitos com o msDS-ConsistencyGuid como sourceAnchor). O assistente apresenta o atributo que foi escolhido como o atributo de Âncora de Origem depois de a Instalação personalizada estar concluída. |
| Um atributo específico | Selecione esta opção se pretender especificar um atributo do AD existente como o atributo sourceAnchor. |

Uma vez que o atributo não pode ser alterado, terá de planear um bom atributo para utilizar. Um bom candidato é objectGUID. Este atributo não é alterado, a menos que a conta de utilizador seja movida entre florestas/domínios. Num ambiente de várias florestas em que se movem contas entre florestas, tem de ser utilizado outro atributo, como um atributo com o campo IDdeEmpregado. Evite atributos que se alteram quando uma pessoa se casa ou muda de atribuições. Não é possível utilizar atributos com um @-sign, sendo assim o e-mail e userPrincipalName não podem ser utilizados. O atributo é também sensível a maiúsculas e minúsculas, por isso, ao mover um objeto entre florestas, certifique-se de que preserva as maiúsculas/minúsculas. Os atributos binários são codificados em base64, mas outros tipos de atributo permanecem no seu estado não codificado. Em cenários de federação e em algumas interfaces do Azure AD, este atributo é também conhecido como immutableID. Poderá encontrar mais informações acerca da âncora de origem no artigo [Conceitos de design](active-directory-aadconnect-design-concepts.md#sourceanchor).

### <a name="sync-filtering-based-on-groups"></a>Filtragem de sincronização baseada em grupos
A filtragem na funcionalidade de grupos permite-lhe sincronizar apenas um pequeno subconjunto de objetos para uma implementação piloto. Para utilizar esta funcionalidade, crie um grupo para este efeito no Active Directory no local. Em seguida, adicione os utilizadores e grupos que devem ser sincronizados com o Azure AD como membros diretos. Pode adicionar e remover posteriormente utilizadores deste grupo para manter a lista de objetos que deve estar presente no Azure AD. Todos os objetos que pretende sincronizar têm de ser membros diretos do grupo. Os utilizadores, grupos, contactos e computadores/dispositivos têm de ser todos membros diretos. A associação a grupos aninhados não é resolvida. Ao adicionar um grupo como membro, só é adicionado o grupo em si e não os seus membros.

![Filtragem de sincronização](./media/active-directory-aadconnect-get-started-custom/filter2.png)

> [!WARNING]
> Esta funcionalidade destina-se apenas a suportar uma implementação piloto. Não a utilize numa implementação de produção autêntica.
>
>

Numa implementação de produção autêntica, será difícil manter um único grupo com todos os objetos a sincronizar. Deve utilizar, em vez disso, um dos métodos descritos em [Configurar filtragem](active-directory-aadconnectsync-configure-filtering.md).

### <a name="optional-features"></a>Funcionalidades Opcionais
Este ecrã permite-lhe selecionar as funcionalidades opcionais para os seus cenários específicos.

![Funcionalidades opcionais](./media/active-directory-aadconnect-get-started-custom/optional.png)

> [!WARNING]
> Se tiver atualmente o DirSync ou o Azure AD Sync ativo, não ative nenhuma das funcionalidades de repetição de escrita no Azure AD Connect.
>
>

| Funcionalidades Opcionais | Descrição |
| --- | --- |
| Implementação Híbrida do Exchange |A funcionalidade Implementação Híbrida do Exchange permite a coexistência de caixas de correio do Exchange no local e no Office 365. O Azure AD Connect está a sincronizar um conjunto específico de [atributos](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback) do Azure AD para o diretório no local. |
| Pastas Públicas de Correio do Exchange | A funcionalidade Pastas Públicas de Correio do Exchange permite-lhe sincronizar objetos de Pastas Públicas ativadas para correio do seu Active Directory no local para o Azure AD. |
| Aplicação Azure AD e filtragem de atributos |Ao ativar a aplicação Azure AD e a filtragem de atributos, o conjunto de atributos sincronizados pode ser personalizado. Esta opção adiciona mais duas páginas de configuração ao assistente. Para obter mais informações, consulte [Aplicação Azure AD e filtragem de atributos](#azure-ad-app-and-attribute-filtering). |
| Sincronização de palavras-passe |Se tiver selecionado a federação como solução de início de sessão, poderá ativar esta opção. A sincronização de palavras-passe pode ser utilizada como uma opção de cópia de segurança. Para obter mais informações, consulte [Sincronização de palavras-passe](active-directory-aadconnectsync-implement-password-synchronization.md). </br></br>Se tiver selecionado a Autenticação Pass-through, esta opção também poderá ser ativada para assegurar o suporte para clientes legados e como uma opção de cópia de segurança. Para obter mais informações, consulte [Sincronização de palavras-passe](active-directory-aadconnectsync-implement-password-synchronization.md).|
| Repetição de escrita de palavras-passe |Ao ativar a repetição de escrita de palavras-passe, as alterações de palavras-passe com origem no Azure AD são reescritas no diretório no local. Para mais informações, consulte [Introdução à gestão de palavras-passe](../active-directory-passwords-getting-started.md) |
| Repetição de escrita do grupo |Se utilizar a funcionalidade **Grupos do Office 365**, pode ter estes grupos representados no Active Directory no local. Esta opção só está disponível se tiver o Exchange presente no Active Directory no local. Para obter mais informações, consulte [Repetição de escrita do grupo](active-directory-aadconnect-feature-preview.md#group-writeback). |
| Repetição de escrita do dispositivo |Permite-lhe a repetição de escrita de objetos de dispositivo no Azure AD para o Active Directory no local para cenários de acesso condicional. Para mais informações, consulte [Ativar a repetição de escrita do dispositivo no Azure AD Connect](active-directory-aadconnect-feature-device-writeback.md). |
| Sincronização de atributos de extensões de diretórios |Ao ativar a sincronização de atributos de extensões de diretórios, os atributos especificados são sincronizados com o Azure AD. Para obter mais informações, consulte [Extensões de diretórios](active-directory-aadconnectsync-feature-directory-extensions.md). |

### <a name="azure-ad-app-and-attribute-filtering"></a>Aplicação Azure AD e filtragem de atributos
Se pretender limitar os atributos a sincronizar com o Azure AD, comece por selecionar os serviços que está a utilizar. Se efetuar alterações de configuração nesta página, um novo serviço terá de ser explicitamente selecionado executando novamente o assistente de instalação.

![Aplicações de funcionalidades opcionais](./media/active-directory-aadconnect-get-started-custom/azureadapps2.png)

Com base nos serviços selecionados no passo anterior, esta página mostra todos os atributos que são sincronizados. Esta lista é uma combinação de todos os tipos de objetos que estão a ser sincronizados. Se existirem alguns atributos específicos que não precisa de sincronizar, pode anular a sua seleção.

![Atributos de funcionalidades opcionais](./media/active-directory-aadconnect-get-started-custom/azureadattributes2.png)

> [!WARNING]
> A remoção de atributos pode afetar a funcionalidade. Para obter as melhores práticas e recomendações, consulte [tributos sincronizados](active-directory-aadconnectsync-attributes-synchronized.md#attributes-to-synchronize).
>
>

### <a name="directory-extension-attribute-sync"></a>Sincronização de atributos de Extensões de Diretórios
Pode expandir o esquema no Azure AD com atributos personalizados adicionados através da organização ou outros atributos no Active Directory. Para utilizar esta funcionalidade, selecione **Sincronização de atributos de extensão de diretórios** na página **Funcionalidades Opcionais**. Pode selecionar nesta página mais atributos para sincronizar.

![Extensões de diretórios](./media/active-directory-aadconnect-get-started-custom/extension2.png)

Para obter mais informações, consulte [Extensões de diretórios](active-directory-aadconnectsync-feature-directory-extensions.md).

### <a name="enabling-single-sign-on-sso"></a>Ativar o Início de sessão único (SSO)
A configuração do início de sessão único para utilização com a Sincronização de Palavras-passe ou a Autenticação Pass-through é um processo simples, que só precisa de executar uma vez para cada floresta que está a ser sincronizada com o Azure AD. A configuração envolve dois passos da seguinte forma:

1.  Criar a conta de computador necessária no seu Active Directory no local.
2.  Configurar a zona da intranet das máquinas cliente para suportar o início de sessão único.

#### <a name="create-the-computer-account-in-active-directory"></a>Criar a conta de computador no Active Directory
Para cada floresta que tenha sido adicionada no Azure AD Connect, terá de fornecer credenciais de Administrador de Domínio para que a conta de computador possa ser criada em cada floresta. As credenciais só são utilizadas para criar a conta e não são armazenadas nem utilizadas para qualquer outra operação. Adicione simplesmente as credenciais na página **Ativar o Início de sessão único** do assistente do Azure AD Connect, conforme apresentado abaixo:

![Ativar o Início de sessão único](./media/active-directory-aadconnect-get-started-custom/enablesso.png)

>[!NOTE]
>Pode ignorar uma floresta específica se não quiser utilizar o Início de sessão único nessa floresta.

#### <a name="configure-the-intranet-zone-for-client-machines"></a>Configurar a Zona da Intranet para máquinas cliente
Para se certificar de que o cliente inicia sessão automaticamente na zona da intranet, terá de se certificar de que os dois URLs fazem parte da zona da intranet. Tal garante que o computador associado ao domínio enviará automaticamente um pedido de suporte de Kerberos para o Azure AD quando estiver ligado à rede empresarial.
Num computador que tem as ferramentas de gestão de Política de Grupo.

1.  Abrir as Ferramentas de Gestão da Política de Grupo
2.  Edite a Política de grupo que será aplicada a todos os utilizadores. Por exemplo, a Política de Domínio Predefinida.
3.  Navegue até **Configuração de Utilizador\Modelos Administrativos\Componentes do Windows\Internet Explorer\Painel de Controlo da Internet\Página de Segurança** e selecione **Site para a Lista de Atribuições de Zona** de acordo com a imagem abaixo.
4.  Ative a política e introduza os seguintes dois itens na caixa de diálogo.

        Value: `https://autologon.microsoftazuread-sso.com`  
        Data: 1  
        Value: `https://aadg.windows.net.nsatc.net`  
        Data: 1

5.  Deve ter um aspeto semelhante ao seguinte:  
![Zonas da Intranet](./media/active-directory-aadconnect-get-started-custom/sitezone.png)

6.  Clique em **OK** duas vezes.

## <a name="configuring-federation-with-ad-fs"></a>Configurar a federação com o AD FS
Configurar o AD FS com o Azure AD Connect é simples, bastam apenas alguns cliques. É necessário o seguinte antes da configuração.

* Um servidor Windows Server 2012 R2 ou posterior para o servidor de federação com a gestão remota ativada
* Um servidor Windows Server 2012 R2 ou posterior para o servidor Proxy de Aplicação Web com a gestão remota ativada
* Um certificado SSL para o nome do serviço de federação que pretende utilizar (por exemplo, sts.contoso.com)

>[!NOTE]
>Pode atualizar o certificado SSL do farm do AD FS com o Azure AD Connect, mesmo se não o utilizar para gerir a confiança da federação.

### <a name="ad-fs-configuration-pre-requisites"></a>Pré-requisitos de configuração do AD FS
Para configurar o farm do AD FS com o Azure AD Connect, certifique-se de que o WinRM está ativado nos servidores remotos. Certifique-se de que concluiu as outras tarefas nos [pré-requisitos de federação](active-directory-aadconnect-prerequisites.md#prerequisites-for-federation-installation-and-configuration). Além disso, verifique também os requisitos de portas listados na [Tabela 3 – Servidores do Azure AD Connect e de Federação/WAP](active-directory-aadconnect-ports.md#table-3---azure-ad-connect-and-ad-fs-federation-serverswap).

### <a name="create-a-new-ad-fs-farm-or-use-an-existing-ad-fs-farm"></a>Criar um novo farm do AD FS ou utilizar um existente
Pode utilizar um farm do AD FS existente ou pode optar por criar um novo. Se optar por criar um novo, é necessário fornecer o certificado SSL. Se o certificado SSL estiver protegido por uma palavra-passe, é-lhe pedida a palavra-passe.

![Farm do AD FS](./media/active-directory-aadconnect-get-started-custom/adfs1.png)

Se optar por utilizar um farm do AD FS existente, é direcionado diretamente para a configuração da relação de confiança entre o AD FS e o Azure AD.

>[!NOTE]
>O Azure AD Connect pode servir para gerir apenas um farm do AD FS. Se tiver confiança de federação existente com o Azure AD configurado no farm do AD FS selecionado, a confiança será recriada novamente a partir do zero pelo Azure AD Connect.

### <a name="specify-the-ad-fs-servers"></a>Especificar os servidores do AD FS
Introduza os servidores em que pretende instalar o AD FS. Pode adicionar um ou mais servidores com base nas suas necessidades de planeamento da capacidade. Associe todos os servidores do AD FS (não necessários para servidores WAP) ao Active Directory antes de efetuar esta configuração. A Microsoft recomenda a instalação de um único servidor do AD FS para implementações de teste e piloto. Em seguida, adicione e implemente mais servidores para satisfazer as suas necessidades de dimensionamento, executando novamente o Azure AD Connect após a configuração inicial.

> [!NOTE]
> Certifique-se de que todos os servidores estão associados a um domínio do AD antes de efetuar esta configuração.
>
>

![Servidores do AD FS](./media/active-directory-aadconnect-get-started-custom/adfs2.png)

### <a name="specify-the-web-application-proxy-servers"></a>Especificar os servidores Proxy de Web Apps
Introduza os servidores que pretende ter como servidores proxy de Web Apps. O servidor proxy de Web Apps está implementado na rede de perímetro (com acesso à extranet) e suporta pedidos de autenticação da extranet.
 Pode adicionar um ou mais servidores com base nas suas necessidades de planeamento da capacidade. A Microsoft recomenda a instalação de um único servidor proxy de aplicação Web para implementações de teste e piloto. Em seguida, adicione e implemente mais servidores para satisfazer as suas necessidades de dimensionamento, executando novamente o Azure AD Connect após a configuração inicial. Recomenda-se ter um número equivalente de servidores proxy para satisfazer a autenticação da intranet.

> [!NOTE]
> <li> Se a conta utilizada não for um administrador local nos servidores WAP, ser-lhe-ão pedidas as credenciais de administrador.</li>
> <li> Antes de executar este passo, certifique-se de que existe conectividade HTTP/HTTPS entre o servidor do Azure AD Connect e o servidor Proxy de Web Apps.</li>
> <li> Certifique-se de que existe conectividade HTTP/HTTPS entre o Servidor de Web Apps e o servidor do AD FS, para permitir a passagem de pedidos de autenticação.</li>
>

![Aplicação Web](./media/active-directory-aadconnect-get-started-custom/adfs3.png)

É-lhe pedido que introduza as credenciais para que o servidor de Web Apps possa estabelecer uma ligação segura ao servidor do AD FS. Estas credenciais têm de pertencer a um administrador local no servidor do AD FS.

![Proxy](./media/active-directory-aadconnect-get-started-custom/adfs4.png)

### <a name="specify-the-service-account-for-the-ad-fs-service"></a>Especifique a conta de serviço para o serviço do AD FS
O serviço do AD FS requer uma conta de serviço de domínio para autenticar utilizadores e pesquisar informações sobre utilizadores no Active Directory. Pode suportar dois tipos de contas de serviço:

* **Conta de Serviço Gerida de Grupo** – introduzida nos Serviços de Domínio do Active Directory com o Windows Server 2012. Este tipo de conta fornece serviços, como o AD FS, uma conta única sem necessidade de atualizar regularmente a palavra-passe de conta. Utilize esta opção se já tiver controladores de domínio do Windows Server 2012 no domínio a que pertencem os servidores do AD FS.
* **Conta de Utilizador de Domínio** – este tipo de conta requer uma palavra-passe e a atualização regular da palavra-passe, quando a palavra-passe é alterada ou expira. Utilize esta opção apenas se não tiver controladores de domínio do Windows Server 2012 no domínio a que pertencem os servidores do AD FS.

Se tiver selecionado a Conta de Serviço Gerida de Grupo e esta funcionalidade nunca tiver sido utilizada no Active Directory, ser-lhe-ão pedidas as credenciais de Administrador de Empresa. Estas credenciais são utilizadas para iniciar o armazenamento de chaves e ativar a funcionalidade no Active Directory.

> [!NOTE]
> O Azure AD Connect efetua uma verificação para detetar se o serviço AD FS já está registado como um SPN no domínio.  O AD DS não permitirá o registo de SPNs duplicados em simultâneo.  Se for encontrado um SPN duplicado, não poderá continuar até o SPN ser removido.

![Conta de Serviço do AD FS](./media/active-directory-aadconnect-get-started-custom/adfs5.png)

### <a name="select-the-azure-ad-domain-that-you-wish-to-federate"></a>Selecionar o domínio do Azure AD que pretende federar
Esta configuração é utilizada para configurar a relação de federação entre o AD FS e o Azure AD. Configura o AD FS para emitir tokens de segurança para o Azure AD e configura o Azure AD para confiar nos tokens desta instância específica do AD FS. Esta página permite-lhe apenas configurar um domínio único na instalação inicial. Pode configurar mais domínios posteriormente, executando novamente o Azure AD Connect.

![Domínio do Azure AD](./media/active-directory-aadconnect-get-started-custom/adfs6.png)

### <a name="verify-the-azure-ad-domain-selected-for-federation"></a>Verificar o domínio do Azure AD selecionado para federação
Quando seleciona o domínio a ser federado, o Azure AD Connect fornece-lhe as informações necessárias para verificar um domínio não verificado. Consulte [Adicionar e verificar o domínio](../active-directory-domains-add-azure-portal.md) para saber como utilizar estas informações.

![Domínio do Azure AD](./media/active-directory-aadconnect-get-started-custom/verifyfeddomain.png)

> [!NOTE]
> O AD Connect tenta verificar o domínio durante a fase de configuração. Se continuar a configurar sem adicionar os registos DNS necessários, o assistente não conseguirá concluir a configuração.
>
>

## <a name="configure-and-verify-pages"></a>Páginas de configuração e verificação
A configuração ocorre nesta página.

> [!NOTE]
> Antes de prosseguir com a instalação e se tiver configurado a federação, certifique-se de que configurou a [Resolução de nomes dos servidores de federação](active-directory-aadconnect-prerequisites.md#name-resolution-for-federation-servers).
>
>

![Preparado para configurar](./media/active-directory-aadconnect-get-started-custom/readytoconfigure2.png)

### <a name="staging-mode"></a>Modo de teste
É possível configurar um novo servidor de sincronização em paralelo, com modo de teste. É apenas suportado para ter um servidor de sincronização a exportar para um diretório na nuvem. Mas se pretender mover de outro servidor, por exemplo um a executar o DirSync, pode ativar o Azure AD Connect no modo de teste. Uma vez ativado, o motor de sincronização importa e sincroniza os dados normalmente, mas não exporta nada para o Azure AD ou o AD. A sincronização de palavras-passe de funcionalidades e a repetição de escrita de palavras-passe estão desativadas no modo de teste.

![Modo de teste](./media/active-directory-aadconnect-get-started-custom/stagingmode.png)

No modo de teste, é possível efetuar as alterações necessárias no motor de sincronização e rever o que está prestes a ser exportado. Quando lhe parecer que a configuração está boa, execute novamente o assistente de instalação e desative o modo de teste. Os dados são exportados para o Azure AD deste servidor. Não se esqueça de desativar ao mesmo tempo o outro servidor para que haja apenas um servidor a exportar ativamente.

Para obter mais informações, consulte [Modo de teste](active-directory-aadconnectsync-operations.md#staging-mode).

### <a name="verify-your-federation-configuration"></a>Verificar a configuração de federação
O Azure AD Connect verifica as definições de DNS quando clica no botão Verificar.

**Verificações de conectividade de intranet**

* Resolver FQDN de federação: o Azure AD Connect verifica se o FQDN de federação pode ser resolvido pelo DNS para garantir a conectividade. Se o Azure AD Connect não conseguir resolver o FQDN, a verificação irá falhar. Certifique-se de que um registo DNS está presente no FQDN de serviço de federação para concluir a verificação com êxito.
* Registo A de DNS: o Azure AD Connect verifica se existe um registo A para o seu serviço de federação. Na ausência de um registo A, a verificação irá falhar. Crie um registo A, em vez de um registo CNAME, para o seu FQDN de federação, para que seja concluído com êxito.

**Verificações de conectividade de extranet**

* Resolver FQDN de federação: o Azure AD Connect verifica se o FQDN de federação pode ser resolvido pelo DNS para garantir a conectividade.

![Concluir](./media/active-directory-aadconnect-get-started-custom/completed.png)

![Verificar](./media/active-directory-aadconnect-get-started-custom/adfs7.png)

Adicionalmente, execute os seguintes passos de verificação:

* Confirme que pode iniciar sessão a partir de um browser num computador associado ao domínio na intranet: ligue-se a https://myapps.microsoft.com e verifique o início de sessão com a sua conta com sessão iniciada. A conta de administrador do AD DS incorporada não está sincronizada e não pode ser utilizada para a verificação.
* Confirme que pode iniciar sessão a partir de um dispositivo da extranet. Numa máquina de uso doméstico ou num dispositivo móvel, ligue-se a https://myapps.microsoft.com e forneça as credenciais.
* Valide o início de sessão de cliente avançado. Ligue-se a https://testconnectivity.microsoft.com, escolha o separador **Office 365** e escolha o **Teste de Início de Sessão Único do Office 365**.

## <a name="next-steps"></a>Passos seguintes
Uma vez concluída a instalação, termine e inicie novamente sessão no Windows antes de utilizar o Synchronization Service Manager ou Editor de Regras de Sincronização.

Agora que já tem o Azure AD Connect instalado, pode [verificar a instalação e atribuir licenças](active-directory-aadconnect-whats-next.md).

Saiba mais acerca destas funcionalidades que foram ativadas com a instalação: [Impedir eliminações acidentais](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) e [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Saiba mais acerca destes tópicos comuns: [agendador e como acionar a sincronização](active-directory-aadconnectsync-feature-scheduler.md).

Saiba mais sobre como [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md).
