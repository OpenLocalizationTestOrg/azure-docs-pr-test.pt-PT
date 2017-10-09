---
title: "O Azure AD Connect: Se já tiver do Azure AD | Microsoft Docs"
description: "Este tópico descreve a forma como toouse ligam quando tiver um inquilino do Azure AD existente."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f7b166e9e85c1f03330e8e0074d4afa4036738c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-when-you-have-an-existent-tenant"></a>O Azure AD Connect: Se tiver um inquilino existente
A maioria dos tópicos de Olá para como toouse do Azure AD Connect parte do princípio de começa com um novo Azure inquilino do AD e de que não existe nenhum utilizador ou outros objetos não existe. Mas se tiver iniciado com um inquilino do Azure AD, preenchido este com utilizadores e outros objetos e agora pretende toouse ligar, em seguida, este tópico é que o utilizador.

## <a name="hello-basics"></a>Noções básicas de Olá
Um objeto no Azure AD ou é controlado na nuvem de Olá (Azure AD) ou no local. Para um único objeto, não é possível gerir alguns atributos no local e alguns outros atributos no Azure AD. Cada objeto tem um sinalizador que indica onde o objecto de Olá é gerido.

Pode gerir alguns utilizadores no local e outros na nuvem de Olá. Um cenário comum para esta configuração é uma organização com uma combinação dos técnicos de gestão de contas e técnicos de vendas. Olá trabalhadores de gestão de contas de ter um local conta AD, mas trabalhadores de vendas Olá não compatíveis, que têm uma conta no Azure AD. Iria gerir alguns utilizadores no local e algumas no Azure AD.

Se tiver iniciado toomanage utilizadores no Azure AD que também estejam no AD no local e posteriormente quiser toouse ligar, em seguida, existem algumas questões adicionais que terá tooconsider.

## <a name="sync-with-existing-users-in-azure-ad"></a>Sincronizar com os utilizadores existentes no Azure AD
Quando instalar o Azure AD Connect e iniciá-la, hello serviço de sincronização do Azure AD (no Azure AD) faz uma verificação de cada objeto novo e tente toofind um toomatch objeto existente. Existem três atributos utilizados para executar este processo: **userPrincipalName**, **proxyAddresses**, e **sourceAnchor**/**immutableID**. Uma correspondência na **userPrincipalName** e **proxyAddresses** é conhecido como um **correspondência de forma recuperável**. Uma correspondência na **sourceAnchor** é conhecido como **correspondência de disco rígida**. Para Olá **proxyAddresses** atributo apenas um valor de Olá com **SMTP:**, que é o endereço de e-mail principal Olá, é utilizado para avaliação Olá.

correspondência de Olá é avaliada apenas novos objetos feitos Connect. Se alterar um objeto exiting para esta correspondência qualquer um destes atributos, em seguida, verá um erro em vez disso.

Se o Azure AD localiza um objeto onde os valores de atributo Olá são Olá mesmo para um objeto proveniente do Connect e que já se encontra no Azure AD, em seguida, hello objeto no Azure AD é tomado over by Connect. Olá anteriormente objeto gerido de nuvem está assinalado como gerido no local. Todos os atributos no Azure AD com um valor no local no AD são substituídos com o valor do Olá no local. Exceção de Olá é quando um atributo tem um **nulo** valor no local. Neste caso, valor de Olá no Azure AD permanece, mas ainda só pode alterá-la no local toosomething pessoa.

> [!WARNING]
> Uma vez que todos os atributos no Azure AD que vão toobe substituída pelo valor do Olá no local, certifique-se de que tem os dados no local. Por exemplo, se apenas a ter geridas endereço de correio eletrónico no Office 365 e não são mantidas atualizadas no local do AD DS, e perder quaisquer valores no Azure AD/Office 365 não está presente no AD DS.

> [!IMPORTANT]
> Se utilizar a sincronização de palavra-passe, o que é sempre utilizada pelas definições rápidas, em seguida, Olá palavra-passe no Azure AD é substituído pela Olá palavra-passe no local no AD. Se os utilizadores são utilizados toomanage diferentes palavras-passe, em seguida, terá de tooinform-o de que devem utilizar Olá palavra-passe de no local quando instalou o ligar.

secção anterior Olá e aviso devem ser consideradas no seu planeamento. Se tiver efetuado alterações muitos no Azure AD não serão refletido no local do AD DS, em seguida, precisa de tooplan para como toopopulate do AD DS com Olá atualizado valores antes de poder sincronizar os objetos com o Azure AD Connect.

Se corresponder os objetos com uma correspondência de forma recuperável, em seguida, Olá **sourceAnchor** é adicionada toohello objeto no Azure AD para uma correspondência de disco rígida possam ser utilizada mais tarde.

### <a name="hard-match-vs-soft-match"></a>Disco rígido-match vs correspondência de forma recuperável
Para uma nova instalação do Connect, não há qualquer diferença prática entre uma configuração soft - e uma disco rígido correspondência. diferença de Olá é uma situação de recuperação após desastre. Se tiver perdido o seu servidor com o Azure AD Connect, pode reinstalar uma nova instância sem perder quaisquer dados. Um objeto com um sourceAnchor é enviado tooConnect durante a instalação inicial. Olá correspondência pode, em seguida, ser avaliada pelo cliente de Olá (Azure AD Connect), que é muito mais rápida do que ao fazê-lo Olá mesmo no Azure AD. Uma correspondência de disco rígida é avaliada por ligar e pelo Azure AD. Uma correspondência de forma recuperável é avaliada apenas pelo Azure AD.

### <a name="other-objects-than-users"></a>Outros objetos que os utilizadores
Os utilizadores têm normalmente a userPrincipalName e proxyAddresses, efetuar correspondência Olá fácil. Mas outros objetos, tais como grupos de segurança, não têm os. Neste caso, só pode corresponder numa correspondência de disco rígida utilizando Olá sourceAnchor. Olá sourceAnchor é sempre Olá Base64 convertido **objectGUID** no local, pelo que tem de atualizar o valor de Olá no Azure AD quando necessita de dois objetos toomatch. Olá sourceAnchor/immutableID só pode ser atualizado com o PowerShell e não através de portais de Olá.

## <a name="create-a-new-on-premises-active-directory-from-data-in-azure-ad"></a>Criar um novo diretório Active Directory no local a partir dos dados no Azure AD
Alguns clientes começam com uma solução apenas na nuvem com o Azure AD e não têm um local AD. Mais tarde pretende tooconsume no local recursos e pretender toobuild no local AD com base nos dados do Azure AD. O Azure AD Connect não pode ajudá-lo para este cenário. Não cria os utilizadores no local e não tem qualquer capacidade tooset Olá palavra-passe no local toohello mesmo do Azure AD.

Se o motivo apenas Olá motivo pelo qual planeia tooadd no local AD está toosupport LOBs (aplicações de linha de negócio), em seguida, talvez a considerar toouse [serviços de domínio do Azure AD](../../active-directory-domain-services/index.md) em vez disso.

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre como [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md).
