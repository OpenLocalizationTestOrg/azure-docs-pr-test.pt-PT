---
title: 'O Azure AD Connect: Topologias suportadas | Microsoft Docs'
description: "Este tópico descreve as topologias suportadas e não suportadas para o Azure AD Connect"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 1034c000-59f2-4fc8-8137-2416fa5e4bfe
ms.service: active-directory
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: identity
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 41632a54e8e85492fbf1a751ef4e618c8870abe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="topologies-for-azure-ad-connect"></a>Topologias do Azure AD Connect
Este artigo descreve as várias topologias do Azure Active Directory (Azure AD) que utilizam a sincronização do Azure AD Connect como solução de integração chave Olá e no local. Este artigo inclui as configurações suportadas e não suportadas.

Segue-se a legenda de Olá para imagens artigo Olá:

| Descrição | Símbolo |
| --- | --- |
| Floresta do Active Directory no local |![Floresta do Active Directory no local](./media/active-directory-aadconnect-topologies/LegendAD1.png) |
| No local do Active Directory com a importação filtrado |![Active Directory com a importação filtrada](./media/active-directory-aadconnect-topologies/LegendAD2.png) |
| Servidor de sincronização do Azure AD Connect |![Servidor de sincronização do Azure AD Connect](./media/active-directory-aadconnect-topologies/LegendSync1.png) |
| Servidor sincronização do Azure AD Connect, "modo de teste" |![Servidor sincronização do Azure AD Connect, "modo de teste"](./media/active-directory-aadconnect-topologies/LegendSync2.png) |
| GALSync com do Forefront Identity Manager (FIM) 2010 ou do Microsoft Identity Manager (MIM) 2016 |![GALSync com o FIM 2010 ou o MIM 2016](./media/active-directory-aadconnect-topologies/LegendSync3.png) |
| Servidor de sincronização do Azure AD Connect, detalhada |![Servidor de sincronização do Azure AD Connect, detalhada](./media/active-directory-aadconnect-topologies/LegendSync4.png) |
| Azure AD |![Azure Active Directory](./media/active-directory-aadconnect-topologies/LegendAAD.png) |
| Cenário não suportado |![Cenário não suportado](./media/active-directory-aadconnect-topologies/LegendUnsupported.png) |

## <a name="single-forest-single-azure-ad-tenant"></a>Floresta única, único inquilino do Azure AD
![Topologia para uma floresta única e um único inquilino](./media/active-directory-aadconnect-topologies/SingleForestSingleDirectory.png)

topologia mais comuns Olá é um único local floresta, com um ou vários domínios e um único do Azure AD de inquilino. Para a autenticação do Azure AD, é utilizada a sincronização de palavra-passe. instalação rápida do Olá do Azure AD Connect suporta apenas esta topologia.

### <a name="single-forest-multiple-sync-servers-tooone-azure-ad-tenant"></a>Floresta única, vários inquilinos de tooone do Azure AD de servidores de sincronização
![Topologia não suportada, filtrada para uma única floresta](./media/active-directory-aadconnect-topologies/SingleForestFilteredUnsupported.png)

Ter múltiplos servidores de sincronização do Azure AD Connect inquilino toohello ligado mesmo Azure AD não é suportado, exceto para um [transição servidor](#staging-server). Tem não suportado, mesmo que estes servidores são toosynchronize configurado com um conjunto de objetos mutuamente exclusivo. Poderá ter considerado esta topologia se não é possível contactar todos os domínios na floresta de Olá de um único servidor ou se quiser toodistribute carga por vários servidores.

## <a name="multiple-forests-single-azure-ad-tenant"></a>Várias florestas, único inquilino do Azure AD
![Topologia de várias florestas e de um único inquilino](./media/active-directory-aadconnect-topologies/MultiForestSingleDirectory.png)

Muitas organizações têm ambientes com várias florestas de Active Directory no local. Existem várias razões para ter mais do que uma floresta de Active Directory no local. Exemplos típicos são estruturas com o resultado de florestas e Olá de recurso de conta de uma fusão ou aquisição.

Se tiver várias florestas, todas as florestas tem de estar acessível por um único servidor de sincronização do Azure AD Connect. Não tem o domínio de tooa toojoin Olá servidor. Se necessário tooreach todas as florestas, pode colocar o servidor de Olá numa rede de perímetro (também conhecida como DMZ, zona desmilitarizada e sub-rede filtrada).

Assistente de instalação do Olá do Azure AD Connect oferece várias opções tooconsolidate utilizadores são representados em várias florestas. objetivo de Olá é representado apenas uma vez que um utilizador no Azure AD. Existem algumas topologias comuns que pode configurar no caminho de instalação personalizada Olá no Assistente de instalação de Olá. No Olá **identificar os utilizadores de forma exclusiva** página, a opção de correspondente Olá selecione que representa a topologia. consolidação de Olá está configurada apenas para os utilizadores. Grupos de duplicados não são consolidados com a configuração predefinida de Olá.

Topologias comuns são abordadas nas secções Olá sobre [separar topologias](#multiple-forests-separate-topologies), [completa mesh](#multiple-forests-full-mesh-with-optional-galsync), e [Olá topologia de recurso de conta](#multiple-forests-account-resource-forest).

pressupõe que a configuração predefinida de Olá na sincronização do Azure AD Connect:

* Cada utilizador tem apenas uma conta ativada, não sendo floresta olá onde está localizada a esta conta de utilizador de Olá tooauthenticate utilizados. Este pressuposto destina-se a sincronização de palavra-passe e a Federação. UserPrincipalName e sourceAnchor/immutableID provenientes nesta floresta.
* Cada utilizador tem apenas uma caixa de correio.
* floresta de Olá que aloja as caixas de correio Olá para um utilizador tem Olá melhor da qualidade dos dados de atributos visíveis na Olá Exchange lista de endereços Global (GAL). Se não existir nenhuma caixa de correio para o utilizador Olá, qualquer floresta pode ser utilizado toocontribute estes valores de atributo.
* Se tiver uma caixa de correio ligada, há também uma conta numa floresta diferente utilizada para início de sessão.

Se o seu ambiente não corresponde nesses pressupostos, hello ações seguintes ocorrem:

* Se tiver mais do que uma conta Active Directory ou mais do que uma caixa de correio, o motor de sincronização de Olá escolhe um e ignora Olá outro.
* Uma caixa de correio ligada com nenhuma conta de Active Directory não é exportado tooAzure AD. conta de utilizador Olá não é representada como um membro em qualquer grupo. Uma caixa de correio ligada no DirSync sempre é representada como uma caixa de correio normal. Esta alteração é intencionalmente cenários de floresta múltiplos um comportamento diferente toobetter suporte.

Pode encontrar mais detalhes em [configuração predefinida do compreender Olá](active-directory-aadconnectsync-understanding-default-configuration.md).

### <a name="multiple-forests-multiple-sync-servers-tooone-azure-ad-tenant"></a>Várias florestas, vários inquilinos de tooone do Azure AD de servidores de sincronização
![Topologia não suportada para várias florestas e de múltiplos servidores de sincronização](./media/active-directory-aadconnect-topologies/MultiForestMultiSyncUnsupported.png)

Não é suportada a ter mais do que um tooa de servidor ligado do sincronização do Azure AD Connect único inquilino do Azure AD. Olá exceção é Olá utilização de um [transição servidor](#staging-server).

### <a name="multiple-forests-separate-topologies"></a>Várias florestas, topologias separadas
![Opção para representar os utilizadores apenas uma vez em todos os diretórios](./media/active-directory-aadconnect-topologies/MultiForestUsersOnce.png)

![Depiction de várias florestas e topologias separadas](./media/active-directory-aadconnect-topologies/MultiForestSeperateTopologies.png)

Neste ambiente, todas as florestas no local são tratadas como entidades separadas. Nenhum utilizador está presente em qualquer outra floresta. Cada floresta tem a sua própria organização do Exchange e não há nenhum GALSync entre florestas Olá. Esta topologia poderão situação Olá após uma fusão/aquisição ou numa organização onde cada unidade de negócio funciona independentemente. Estas florestas estão num Olá mesma organização no Azure AD e são apresentados com uma GAL unificada. No Olá anterior a imagem, cada objeto em cada floresta é representado uma vez no metaverso Olá e agregado no inquilino do destino do Azure AD Olá.

### <a name="multiple-forests-match-users"></a>Várias florestas: corresponder a utilizadores
Tooall comuns estes cenários é essa distribuição e grupos de segurança podem conter uma mistura de utilizadores, contactos e as principais de segurança externa (FSPs). FSPs são utilizados em membros de toorepresent de serviços de domínio do Active Directory (AD DS) de outras florestas num grupo de segurança. Todos os FSPs são objecto real toohello resolvido no Azure AD.

### <a name="multiple-forests-full-mesh-with-optional-galsync"></a>Várias florestas: completa mesh com GALSync opcional
![Opção para utilizar o atributo de correio Olá para efetuar a correspondência quando existem identidades de utilizadores em vários diretórios](./media/active-directory-aadconnect-topologies/MultiForestUsersMail.png)

![Topologia de malha completa para várias florestas](./media/active-directory-aadconnect-topologies/MultiForestFullMesh.png)

Uma topologia de malha completa permite aos utilizadores e toobe recursos localizados em qualquer floresta. Normalmente, existem confianças bidirecionais entre florestas Olá.

Se estiver presente na floresta de mais do que um Exchange, poderão existir (opcionalmente) uma solução de GALSync no local. Todos os utilizadores, em seguida, é representado como um contacto em todas as outras florestas. GALSync normalmente é implementado através do FIM 2010 ou o MIM 2016. O Azure AD Connect não pode ser utilizado para GALSync no local.

Neste cenário, os objetos de identidade são associados através do atributo de correio Olá. Um utilizador que tem uma caixa de correio numa floresta é associado contactos de Olá no Olá noutras florestas.

### <a name="multiple-forests-account-resource-forest"></a>Várias florestas: floresta de recursos de conta
![Opção para a utilização de atributos de Sidobjeto e msExchMasterAccountSID Olá para efetuar a correspondência quando existem identidades em vários diretórios](./media/active-directory-aadconnect-topologies/MultiForestUsersObjectSID.png)

![Topologia de floresta de recursos de conta para várias florestas](./media/active-directory-aadconnect-topologies/MultiForestAccountResource.png)

Uma topologia de floresta de recursos de conta, tem um ou mais *conta* florestas com contas de utilizador do Active Directory. Também tem um ou mais *recursos* florestas com contas desativadas.

Neste cenário, um (ou mais) recursos confianças de floresta todas as florestas de contas. floresta de recursos de Olá normalmente tem um esquema do Active Directory expandido com o Exchange e o Lync. Serviços de todos os Exchange e o Lync, juntamente com outros serviços partilhados, encontram-se nesta floresta. Os utilizadores têm uma conta de utilizador desativado nesta floresta, e está ligada a caixa de correio Olá toohello floresta de contas.

## <a name="office-365-and-topology-considerations"></a>Office 365 e considerações sobre a topologia
Algumas cargas de trabalho do Office 365 têm determinadas restrições em topologias suportadas:

| Carga de trabalho | Restrições |
--------- | ---------
| Exchange Online | Se existir mais do que uma organização de Exchange no local (ou seja, Exchange foi implementado toomore que uma floresta), tem de utilizar o Exchange 2013 SP1 ou posterior. Para obter mais informações, consulte [implementações híbridas com várias florestas do Active Directory](https://technet.microsoft.com/library/jj873754.aspx). |
| Skype para empresas | Quando estiver a utilizar várias florestas no local, a topologia de floresta de recursos de conta Olá só é suportada. Para obter mais informações, consulte [requisitos ambientais para o Skype para empresas servidor 2015](https://technet.microsoft.com/library/dn933910.aspx). |


## <a name="staging-server"></a>Servidor de teste
![Servidor de teste numa topologia](./media/active-directory-aadconnect-topologies/MultiForestStaging.png)

Azure AD Connect suporta a instalação de um segundo servidor no *modo de teste*. Um servidor no modo lê dados de todos os diretórios ligados, mas não escrever nada tooconnected diretórios. Utiliza o ciclo de sincronização normal de Olá e, por conseguinte, tem uma cópia atualizada Olá de dados de identidade.

Um desastre em que o servidor primário Olá falha, pode falhar toohello servidor de teste. Fazê-lo no Assistente do Azure AD Connect de Olá. Este segundo servidor pode estar localizado num centro de dados diferentes porque nenhuma infraestrutura está partilhada com o servidor primário Olá. Tem de copiar manualmente qualquer alteração de configuração efetuada no Olá servidor primário toohello segundo servidor.

Pode utilizar uma transição tootest de servidor um novo personalizado configuração e Olá efeito que tem nos seus dados. Pode pré-visualizar as alterações de Olá e ajustar a configuração de Olá. Quando estiver satisfeito com uma nova configuração de Olá, pode efetuar Olá servidor ativo do servidor Olá de teste e definir o modo de toostaging do Olá antigo servidor ativo.

Também pode utilizar este servidor de sincronização do Active Directory do método tooreplace Olá. Prepare Olá novo servidor e configurá-lo toostaging modo. Certifique-se de que está em bom estado, desativar (tornando-o Active Directory), de modo de teste e encerrar Olá de servidor atualmente ativo.

É possível toohave mais do que um servidor de teste quando quiser toohave várias cópias de segurança em datacenters diferentes.

## <a name="multiple-azure-ad-tenants"></a>Vários inquilinos do Azure AD
Recomenda-se ter um único inquilino no Azure AD para uma organização.
Antes de planear toouse vários inquilinos do Azure AD, consulte o artigo de Olá [gestão unidades administrativas no Azure AD](../active-directory-administrative-units-management.md). Abrange os cenários comuns em que pode utilizar um único inquilino.

![Topologia de várias florestas e de vários inquilinos](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectory.png)

Há uma relação de 1:1 entre um servidor de sincronização do Azure AD Connect e um inquilino do Azure AD. Para cada inquilino do Azure AD, precisa de uma instalação de servidor de sincronização do Azure AD Connect. instâncias de inquilino do Azure AD Olá são isoladas por predefinição. Ou seja, os utilizadores no inquilino de um não é possível ver os utilizadores Olá outro inquilino. Se pretender que esta separação, esta é uma configuração suportada. Caso contrário, deve utilizar Olá único modelo de inquilino do Azure AD.

### <a name="each-object-only-once-in-an-azure-ad-tenant"></a>Cada objeto apenas uma vez num inquilino do Azure AD
![Topologia filtrada para uma única floresta](./media/active-directory-aadconnect-topologies/SingleForestFiltered.png)

Nesta topologia, um servidor de sincronização do Azure AD Connect é inquilino tooeach ligado do Azure AD. servidores de sincronização do Azure AD Connect Olá tem de ser configurados para efeitos de filtragem para que cada tem um conjunto de objetos toooperate mutuamente exclusivo no. Pode, por exemplo, definir o âmbito cada domínio específico do servidor tooa ou unidade organizacional.

Um domínio DNS pode ser registado em apenas um único inquilino do Azure AD. Olá UPNs de utilizadores de Olá na instância do Olá no local do Active Directory também tem de utilizar espaços de nomes separados. Por exemplo, no Olá anterior a imagem, três sufixos UPN separados estão registados na instância do Olá no local do Active Directory: contoso.com, fabrikam.com e wingtiptoys.com. utilizadores de Olá em cada domínio de Active Directory no local, utilizar um espaço de nomes diferentes.

Não há nenhum GALSync entre instâncias de inquilino do Azure AD Olá. Olá no livro de endereços no Exchange Online e Skype para mostra negócio só Olá, os utilizadores no mesmo inquilino.

Esta topologia tem seguinte Olá restrições no caso contrário, suportada cenários:

* Apenas um dos inquilinos Olá do Azure AD pode ativar uma híbrida do Exchange com a instância do Olá no local do Active Directory.
* Dispositivos Windows 10 pode ser associada com apenas um inquilino do Azure AD.
* Olá único início de sessão (SSO) opção para autenticação de pass-through e de sincronização de palavra-passe pode ser utilizada com apenas um inquilino do Azure AD.

requisito de Olá para um conjunto de objetos mutuamente também se aplica toowriteback. Algumas funcionalidades de repetição de escrita não são suportadas com esta topologia porque estes partem do princípio de uma única configuração no local. Estas funcionalidades incluem:

* Repetição de escrita grupo com a configuração predefinida.
* Repetição de escrita do dispositivo.

### <a name="each-object-multiple-times-in-an-azure-ad-tenant"></a>Cada objeto várias vezes num inquilino do Azure AD
![Topologia não suportada para uma única floresta e de vários inquilinos](./media/active-directory-aadconnect-topologies/SingleForestMultiDirectoryUnsupported.png) ![Topologia não suportada para uma floresta única e vários conectores](./media/active-directory-aadconnect-topologies/SingleForestMultiConnectorsUnsupported.png)

Estas tarefas não são suportadas:

* Sincronização Olá mesmo inquilinos do utilizador toomultiple do Azure AD.
* Fazer uma configuração alterar para que os utilizadores um inquilino do Azure AD são apresentados como contactos no outro inquilino do Azure AD.
* Modificar os inquilinos do Azure AD Connect sincronização tooconnect toomultiple do Azure AD.

### <a name="galsync-by-using-writeback"></a>GALSync através da utilização de repetição de escrita
![Topologia não suportada para várias florestas e de vários diretórios, com GALSync concentrar-se no Azure AD](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync1Unsupported.png) ![Topologia não suportada para várias florestas e de vários diretórios, com GALSync concentrar-se no local do Active Directory](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync2Unsupported.png)

Inquilinos do Azure AD são isolados por predefinição. Estas tarefas não são suportadas:

* Alterar a configuração de Olá de dados de tooread de sincronização do Azure AD Connect de outro inquilino do Azure AD.
* Exportação de utilizadores como instância de Active Directory no local do contactos tooanother através da utilização de sincronização do Azure AD Connect.

### <a name="galsync-with-on-premises-sync-server"></a>GALSync com o servidor de sincronização no local
![GALSync numa topologia de várias florestas e de vários diretórios](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync.png)

Pode utilizar o FIM 2010 ou o MIM 2016 utilizadores no local toosync (através de GALSync) entre duas organizações do Exchange. utilizadores de Olá de uma organização aparecem como externos utilizadores por contactos nas Olá outra organização. Estes diferentes no local do Active Directory instâncias, em seguida, podem ser sincronizadas com os seus próprios inquilinos do Azure AD.

## <a name="next-steps"></a>Passos seguintes
toolearn como tooinstall do Azure AD Connect nestes cenários, consulte [instalação personalizada do Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

Saiba mais sobre Olá [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuração.

Saiba mais sobre [integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md).
