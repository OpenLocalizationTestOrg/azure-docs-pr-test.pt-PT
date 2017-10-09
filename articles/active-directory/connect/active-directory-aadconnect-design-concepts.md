---
title: 'O Azure AD Connect: Conceitos de Design | Microsoft Docs'
description: "Este tópico descreve algumas áreas de estrutura de implementação"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4114a6c0-f96a-493c-be74-1153666ce6c9
ms.service: active-directory
ms.custom: azure-ad-connect
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1e5d5c6a716ca653fb14fc059e8155124b433732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-design-concepts"></a>O Azure AD Connect: Conceitos de Design
Olá objetivo deste tópico é toodescribe áreas que devem considerar durante a estrutura de implementação de Olá do Azure AD Connect. Este tópico é uma descrição profunda sobre algumas áreas e estes conceitos uma breve descrição, bem como outros tópicos.

## <a name="sourceanchor"></a>sourceAnchor
atributo de sourceAnchor Olá está definido como *um atributo imutável durante a duração de Olá de um objeto*. Identifica exclusivamente um objeto como sendo Olá mesmo objeto no local e no Azure AD. atributo de Olá também é denominado **immutableId** e nomes de Olá dois são utilizados permutáveis.

Olá palavra imutável, que é "não é possível alterar", é importante toothis tópico. Uma vez que o valor deste atributo não pode ser alterado depois de ter sido definido, é importante toopick uma estrutura que suporta o seu cenário.

atributo de Olá é utilizado para Olá os seguintes cenários:

* Quando um novo servidor do motor de sincronização é criado ou reconstruído após um cenário de recuperação após desastre, este atributo liga objetos existentes no Azure AD com objetos no local.
* Se mover de um modelo de identidade sincronizados tooa identidade apenas na nuvem, em seguida, este atributo permite objetos demasiado "correspondência de disco rígido" objetos existentes no Azure AD com objetos no local.
* Se utilizar a Federação, em seguida, este atributo, juntamente com Olá **userPrincipalName** é utilizada na Olá afirmação toouniquely identificar um utilizador.

Este tópico aborda apenas sourceAnchor no que respeita toousers. Olá mesmas regras aplicam-se os tipos de objeto tooall, mas destina-se apenas os utilizadores que deste problema, normalmente, é importante.

### <a name="selecting-a-good-sourceanchor-attribute"></a>Selecionar um atributo sourceAnchor boa
o valor do atributo Olá tem de seguir Olá seguintes regras:

* Ter menos de 60 carateres de comprimento
  * Carateres que não estão a ser a-z, A-Z ou 0-9 são codificados e contabilizado como 3 carateres
* Não contém um caráter especial: &#92;! # $ % & * + / = ? ^ &#96; { } | ~ < > ( ) ' ; : , [ ] " @ _
* Deve ser globalmente exclusivo
* Tem de ser uma cadeia, número inteiro ou binário
* Não devem ser baseadas no nome do utilizador, estas alterações
* Não deve ser sensíveis a maiúsculas e evitar valores que podem variar devido por maiúsculas e minúsculas
* Deve ser atribuído quando Olá objeto é criado

Se Olá selecionado sourceAnchor não é do tipo cadeia, tooensure de valor de atributo do Azure AD Connect Base64Encode Olá sem carateres especiais aparecer. Se utilizar outro servidor de federação que o AD FS, certifique-se o servidor pode também atributo de Olá Base64Encode.

atributo de sourceAnchor Olá diferencia maiúsculas de minúsculas. Um valor de "JohnDoe" não é Olá igual a "johndoe". Mas não deve ter dois objectos diferentes com apenas uma diferença nas maiúsculas e minúsculas.

Se tiver uma única floresta no local, em seguida, atributos de Olá deve utilizar seja **objectGUID**. Isto também se o atributo de Olá utilizado quando utilizar as definições rápidas no Azure AD Connect e também Olá atributo utilizado pelo DirSync.

Se tiver várias florestas e não mova os utilizadores entre florestas e domínios, em seguida, **objectGUID** é um bom atributo toouse mesmo neste caso.

Se mover utilizadores entre florestas e domínios, em seguida, tem de encontrar um atributo que não alteram ou pode ser movido com utilizadores Olá durante Olá mudança. Uma abordagem recomendada é toointroduce um atributo sintético. Um atributo que foi contêm algo que aparente ser um GUID seria adequado. Durante a criação do objeto, um novo GUID é criado e carimbo de data / no utilizador Olá. Uma regra de sincronização personalizados pode ser criada no toocreate de servidor de motor de sincronização de Olá este valor com base no Olá **objectGUID** e atualização Olá atributo selecionado no ADDS. Quando mover objeto Olá, certifique-se de que tooalso cópia Olá conteúdo este valor.

Outra solução é toopick um atributo existente a que se sabe não se altera. Atributos comuns incluem **campo IDdeEmpregado**. Se considerar um atributo que contém a letras, certificar-se de que não há que nenhum caso de Olá hipótese (maiúsculas vs. minúsculas) pode ser alteradas para o valor do atributo Olá. Atributos incorretos, que não devem ser utilizados incluem esses atributos com o nome de Olá do utilizador Olá. Um marriage ou divorce, nome de Olá é toochange esperado, o que não é permitido para este atributo. Isto também é um motivo por que motivo atributos como **userPrincipalName**, **correio**, e **targetAddress** não são possível mesmo tooselect na instalação do Olá do Azure AD Connect Assistente. Esses atributos também contêm Olá "@" caráter, que não é permitido no Olá sourceAnchor.

### <a name="changing-hello-sourceanchor-attribute"></a>Alterar o atributo de sourceAnchor Olá
Não é possível alterar o valor do atributo sourceAnchor Olá depois do objeto de Olá foi criado no Azure AD e Olá identidade está sincronizada.

Por este motivo, Olá seguintes restrições aplicam-se tooAzure AD Connect:

* atributo de sourceAnchor Olá só pode ser definido durante a instalação inicial. Se voltar a executar o Assistente de instalação de Olá, esta opção é só de leitura. Se precisar de toochange esta definição, tem de desinstalar e reinstalar.
* Se instalar outro servidor do Azure AD Connect, em seguida, que tem selecione Olá mesmo atributo sourceAnchor utilizado anteriormente. Se anteriormente tiver sido utilizando o DirSync e mover tooAzure AD Connect, em seguida, tem de utilizar **objectGUID** , uma vez que é que o atributo de Olá utilizado pelo DirSync.
* Se o valor de Olá para sourceAnchor é alterado depois do objeto de Olá foi exportado tooAzure AD, em seguida, o Azure AD Connect, emite um erro de sincronização e não permite mais alterações nesse objecto antes de correção do problema Olá e Olá sourceAnchor é alterado no Olá diretório de origem.

## <a name="using-msds-consistencyguid-as-sourceanchor"></a>Utilizar msDS-ConsistencyGuid como sourceAnchor
Por predefinição, o Azure AD Connect (versão 1.1.486.0 e anterior) utiliza objectGUID como atributo de sourceAnchor Olá. ObjectGUID é gerado pelo sistema. Não é possível especificar o respetivo valor durante a criação de locais objetos do AD. Conforme explicado na secção [sourceAnchor](#sourceanchor), existem cenários onde necessita de valor de sourceAnchor toospecify Olá. Se a cenários de Olá tooyou aplicável, tem de utilizar um atributo de AD (por exemplo, msDS-ConsistencyGuid) configurável como atributo de sourceAnchor Olá.

O Azure AD Connect (versão 1.1.524.0 e após) agora facilita a utilização de Olá de msDS-ConsistencyGuid como atributo sourceAnchor. Quando utilizar esta funcionalidade, o Azure AD Connect configura automaticamente regras de sincronização de Olá para:

1. Utilize msDS-ConsistencyGuid como atributo de sourceAnchor Olá para objetos de utilizador. ObjectGUID é utilizada para outros tipos de objeto.

2. Para qualquer fornecido no local utilizador AD objeto cujo atributo msDS-ConsistencyGuid não se encontra preenchido, o Azure AD Connect escreve o respetivo atributo msDS-ConsistencyGuid do objectGUID valor back toohello no Active Directory no local. Depois de preencher o atributo msDS-ConsistencyGuid de Olá, Azure AD Connect, em seguida, exporta Olá objeto tooAzure AD.

>[!NOTE]
> Uma vez no local objecto do AD é importado para o Azure AD Connect (que é, importado para Olá espaço de conector do AD e é projetado em Olá Metaverso), não é possível alterar o valor de sourceAnchor já. valor de sourceAnchor Olá toospecify para uma dada no local AD objeto, configure o atributo msDS-ConsistencyGuid antes de serem importados para o Azure AD Connect.

### <a name="permission-required"></a>Permissão necessária
Para esta funcionalidade toowork, Olá AD DS conta utilizada toosynchronize com o Active Directory no local têm de ser concedida escrita permissão toohello msDS-ConsistencyGuid atributo no Active Directory no local.

### <a name="how-tooenable-hello-consistencyguid-feature---new-installation"></a>Como tooenable Olá ConsistencyGuid funcionalidade - nova instalação
Pode ativar a utilização de Olá de ConsistencyGuid como sourceAnchor durante a instalação de novo. Esta secção abrange instalação rápida e personalizados nos detalhes.

  >[!NOTE]
  > Apenas as versões mais recentes do Azure AD Connect (1.1.524.0 e após) suporta Olá utilização de ConsistencyGuid como sourceAnchor durante a instalação de novo.

### <a name="how-tooenable-hello-consistencyguid-feature"></a>Como tooenable Olá ConsistencyGuid funcionalidade
Atualmente, a funcionalidade de Olá só pode ser ativada durante a nova instalação do Azure AD Connect apenas.

#### <a name="express-installation"></a>Instalação rápida
Ao instalar o Azure AD Connect com o modo de rápida, do Assistente do Azure AD Connect Olá determina automaticamente Olá AD mais adequado atributo toouse como atributo de sourceAnchor Olá utilizando Olá lógica os seguintes:

* Em primeiro lugar, consultas de assistente Olá do Azure AD Connect utilizado o atributo de Olá AD de tooretrieve de inquilino do Azure AD como Olá atributo sourceAnchor na instalação do Olá anterior do Azure AD Connect (se aplicável). Se esta informação está disponível, o Azure AD Connect utiliza um atributo Olá mesmo AD.

  >[!NOTE]
  > Apenas as versões mais recentes do Azure AD Connect (1.1.524.0 e após) arquivos sobre no seu inquilino do Azure AD atributo sourceAnchor de Olá utilizado durante a instalação. As versões mais antigas do Azure AD Connect não.

* Se informações sobre o atributo de sourceAnchor Olá utilizado não estiver disponíveis, o Assistente de Olá verifica o estado de Olá do atributo msDS-ConsistencyGuid de Olá no Active Directory no local. Se o atributo de Olá não está configurado qualquer objeto no diretório de Olá, o Assistente de Olá utiliza Olá msDS-ConsistencyGuid como atributo de sourceAnchor Olá. Se o atributo Olá está configurado numa ou mais objetos no diretório de Olá, o Assistente de Olá conclui atributo Olá está a ser utilizado por outras aplicações e não é adequado como atributo sourceAnchor...

* Caso em que o Assistente de Olá retrocede toousing objectGUID como atributo de sourceAnchor Olá.

* Depois de decidir o atributo de sourceAnchor Olá, o Assistente de Olá armazena informações de Olá no seu inquilino do Azure AD. Olá informações serão utilizadas pela instalação futura do Azure AD Connect.

Uma vez concluída a instalação rápida, o assistente Olá informa-o atributo tem sido selecionado como atributo de âncora de origem Olá.

![Assistente informa o atributo de AD selecionado para sourceAnchor](./media/active-directory-aadconnect-design-concepts/consistencyGuid-01.png)

#### <a name="custom-installation"></a>Instalação personalizada
Ao instalar o Azure AD Connect com o modo personalizado, o Assistente do Azure AD Connect de Olá fornece duas opções ao configurar o atributo sourceAnchor:

![Instalação personalizada - sourceAnchor configuração](./media/active-directory-aadconnect-design-concepts/consistencyGuid-02.png)

| Definição | Descrição |
| --- | --- |
| Permitir que o Azure gerir âncora de origem Olá para mim | Selecione esta opção se pretender o atributo do Azure AD toopick Olá por si. Se selecionar esta opção, o Azure AD Connect, aplica-se do assistente Olá mesmo [lógica de seleção de atributo sourceAnchor utilizada durante a instalação rápida](#express-installation). Instalação de tooExpress semelhante, assistente Olá informa-o atributo de que tem sido selecionado como Olá atributo âncora de origem após a conclusão da instalação personalizada. |
| Um atributo específico | Selecione esta opção se quiser toospecify um atributo de AD existente como atributo de sourceAnchor Olá. |

### <a name="how-tooenable-hello-consistencyguid-feature---existing-deployment"></a>Como tooenable Olá ConsistencyGuid funcionalidade - implementação existente
Se tiver uma implementação existente do Azure AD Connect que está a utilizar objectGUID como atributo de âncora de origem Olá, pode mudar-toousing ConsistencyGuid em vez disso.

>[!NOTE]
> Apenas as versões mais recentes do Azure AD Connect (1.1.552.0 e após) suporta a mudança de ObjectGuid tooConsistencyGuid como atributo de âncora de origem Olá.

tooswitch de objectGUID tooConsistencyGuid como atributo de âncora de origem Olá:

1. Iniciar o Assistente do Olá do Azure AD Connect e clique em **configurar** ecrã do toogo toohello tarefas.

2. Selecione Olá **configurar âncora de origem** opção de tarefas e clique em **seguinte**.

   ![Ativar ConsistencyGuid para implementação existente - passo 2](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment01.png)

3. Introduza as credenciais de administrador do Azure AD e clique em **seguinte**.

4. Assistente do Azure AD Connect analisa o estado de Olá do atributo msDS-ConsistencyGuid de Olá no Active Directory no local. Se o atributo de Olá não está configurado em qualquer objeto no diretório, Azure AD Connect conclui que nenhuma outra aplicação está atualmente a utilizar o atributo de Olá sendo toouse seguro de Olá-lo como atributo âncora de origem de Olá. Clique em **seguinte** toocontinue.

   ![Ativar ConsistencyGuid para implementação existente - passo 4](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment02.png)

5. No Olá **tooConfigure pronto** ecrã, clique em **configurar** alteração da configuração toomake Olá.

   ![Ativar ConsistencyGuid para implementação existente - passo 5](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment03.png)

6. Uma vez concluída a configuração de Olá, o Assistente de Olá indica que msDS-ConsistencyGuid agora está a ser utilizado como atributo de âncora de origem Olá.

   ![Ativar ConsistencyGuid para implementação existente - passo 6](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment04.png)

Durante a análise de Olá (passo 4), se o atributo Olá está configurado numa ou mais objetos no diretório de Olá, conclui o Assistente de Olá atributo Olá está a ser utilizado por outra aplicação e devolve um erro, conforme ilustrado no diagrama de Olá abaixo. Se tiver a certeza de que esse atributo Olá não é utilizado por aplicações existentes, terá de toocontact suporte para obter informações sobre como toosuppress Olá erro.

![Ativar ConsistencyGuid para implementação existente - erro](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeploymenterror.png)

### <a name="impact-on-ad-fs-or-third-party-federation-configuration"></a>Impacto no AD FS ou a configuração de Federação de terceiros
Se estiver a utilizar o Azure AD Connect toomanage no local implementação do AD FS, Olá do Azure AD Connect atualiza automaticamente atributo Olá mesmo AD toouse de regras de afirmação de Olá como sourceAnchor. Isto garante que afirmações de ImmutableID Olá geradas pelo AD FS são consistente com Olá sourceAnchor valores exportado tooAzure AD.

Se estiver a gerir o AD FS fora do Azure AD Connect ou estiver a utilizar servidores de Federação de terceiros para autenticação, tem de atualizar manualmente as regras de afirmação Olá para ImmutableID afirmação toobe consistentes com os valores de sourceAnchor Olá exportado tooAzure AD como descrito na secção do artigo [regras de afirmação de modificar o AD FS](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-management#modclaims). Assistente de Olá devolve Olá seguir aviso após a conclusão da instalação:

![Configuração de Federação de terceiros](./media/active-directory-aadconnect-design-concepts/consistencyGuid-03.png)

### <a name="adding-new-directories-tooexisting-deployment"></a>Adicionar nova implementação de tooexisting de diretórios
Suponha que tiver implementado o Azure AD Connect com Olá ConsistencyGuid funcionalidade ativada e agora gostaria tooadd outra implementação de toohello de diretório. Quando tenta tooadd diretório de Olá, o Assistente do Azure AD Connect verifica Estado Olá do atributo mSDS-ConsistencyGuid de Olá no diretório de Olá. Se o atributo de Olá está configurado numa ou mais objetos no diretório de Olá, o assistente Olá conclui atributo Olá está a ser utilizado por outras aplicações e devolve um erro, conforme ilustrado no diagrama de Olá abaixo. Se tiver a certeza de que esse atributo Olá não é utilizado por aplicações existentes, terá de toocontact suporte para obter informações sobre como toosuppress Olá erro.

![Adicionar nova implementação de tooexisting de diretórios](./media/active-directory-aadconnect-design-concepts/consistencyGuid-04.png)

## <a name="azure-ad-sign-in"></a>Azure AD início de sessão
Ao integrar o seu diretório no local com o Azure AD, é importante toounderstand como as definições de sincronização de Olá podem afetar o utilizador de forma Olá efetua a autenticação. AD do Azure utiliza o utilizador de Olá de tooauthenticate userPrincipalName (UPN). No entanto, quando sincroniza os seus utilizadores, tem de escolher Olá atributo toobe utilizado para o valor do userPrincipalName cuidadosamente.

### <a name="choosing-hello-attribute-for-userprincipalname"></a>Escolher o atributo de Olá para userPrincipalName
Quando selecionar o atributo de Olá para fornecer valor Olá toobe UPN utilizado no Azure deve certificar-se

* está em conformidade com os valores de atributo de Olá toohello UPN sintaxe (RFC 822), deve ter o formato de Oláusername@domain
* sufixo Olá no Olá tooone de correspondências de valores de Olá verificados domínios personalizados no Azure AD

Nas definições rápidas, Olá pressupõe-se que escolha para o atributo de Olá é userPrincipalName. Se o atributo de userPrincipalName Olá não contém um valor de Olá pretende que o seu toosign de utilizadores no tooAzure, em seguida, tem de escolher **instalação personalizada**.

### <a name="custom-domain-state-and-upn"></a>Estado de domínio personalizado e UPN
É importante tooensure que há um domínio verificado do sufixo UPN de Olá.

O João é um utilizador em contoso.com. Pretende que o João toouse Olá no local UPN john@contoso.com toosign no tooAzure depois foram sincronizadas, por isso, os utilizadores tooyour do Azure AD directory contoso.onmicrosoft.com. toodo, precisa de tooadd e verificar contoso.com como um domínio personalizado no Azure AD antes de começar a sincronizar utilizadores de Olá. Se o sufixo UPN Olá João, por exemplo, contoso.com, não corresponde um domínio verificado no Azure AD, do Azure AD substitui o sufixo UPN de Olá com contoso.onmicrosoft.com.

### <a name="non-routable-on-premises-domains-and-upn-for-azure-ad"></a>Domínios não encaminhável no local e o UPN para o Azure AD
Algumas organizações têm domínios não encaminháveis internos, como contoso. local, ou domínios de etiqueta única simples, como contoso. Não é possível tooverify um domínio não encaminháveis internos no Azure AD. O Azure AD Connect pode sincronizar tooonly um domínio verificado no Azure AD. Quando cria um diretório do Azure AD, cria um domínio encaminhável que torna-se o domínio predefinido do Azure AD, por exemplo, contoso.onmicrosoft.com. Por conseguinte, torna-se tooverify necessário qualquer outro domínio encaminhável neste cenário no caso de não pretender que o domínio onmicrosoft.com do toosync toohello predefinido.

Leitura [adicionar o seu tooAzure de nome de domínio personalizado do Active Directory](../active-directory-add-domain.md) para obter mais informações sobre adicionar e verificar domínios.

O Azure AD Connect Deteta se estiver a executar num ambiente de domínio não encaminháveis internos e iria adequadamente avisá-lo de aceder diretamente com as definições rápidas. Se estiver a utilizar num domínio não encaminháveis internos, em seguida, é provável que Olá UPN dos utilizadores Olá ter demasiado sufixos não encaminháveis internos. Por exemplo, se estiver a executar em contoso. local, o Azure AD Connect sugere toouse definições personalizadas, em vez de utilizar definições expressas. Utilizar as definições personalizadas, são toospecify capaz de atributo de Olá que deve ser utilizado como toosign UPN no tooAzure depois dos utilizadores de Olá são sincronizada tooAzure AD.

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre como [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md).
