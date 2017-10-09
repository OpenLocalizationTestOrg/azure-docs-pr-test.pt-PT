---
title: "Do Azure AD Connect: As funcionalidades pré-visualização | Microsoft Docs"
description: "Este tópico descreve em mais funcionalidades de detalhe que estão na pré-visualização no Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a>Obter mais detalhes sobre as funcionalidades em pré-visualização
Este tópico descreve como toouse as funcionalidades atualmente em pré-visualização.

## <a name="group-writeback"></a>Repetição de escrita do grupo
opção de Olá para repetição de escrita do grupo em funcionalidades opcionais permite-lhe toowriteback **grupos do Office 365** tooa floresta com o Exchange instalado. Este é um grupo que é controlado sempre na nuvem de Olá. Se tiver o Exchange no local, em seguida, pode escrever novamente este grupos tooon local para que os utilizadores com uma caixa de correio do Exchange no local podem enviar e receber e-mails destes grupos.

Mais informações sobre grupos do Office 365 e como toouse-los podem ser encontrados [aqui](http://aka.ms/O365g).

Um grupo do Office 365 é representado como um grupo de distribuição no local do AD DS. O servidor do Exchange no local tem de ser no Exchange 2013 atualização cumulativa 8 (lançada em Março de 2015) ou o Exchange 2016 toorecognize este novo tipo de grupo.

**Notas durante a pré-visualização de Olá**

* atributo de livro de endereços de Olá não for preenchido atualmente em pré-visualização Olá. Sem este atributo, o grupo de Olá não estiver visível na Olá GAL. Olá toopopulate de forma mais fácil este atributo é toouse Olá do Exchange PowerShell cmdlet `update-recipient`.
* Só é florestas com o esquema do Exchange de Olá são destinos válidos para grupos. Não se foi detetado nenhum Exchange, em seguida, repetição de escrita do grupo não é possível tooenable.
* Apenas floresta única organização implementações do Exchange são atualmente suportadas. Se tiver mais do que um Exchange organização no local, em seguida, terá de uma solução de GALSync no local para estes grupos tooappear sua noutras florestas.
* funcionalidade de repetição de escrita do grupo de Olá não processa os grupos de segurança ou grupos de distribuição.

> [!NOTE]
> Uma subscrição tooAzure AD Premium é necessário para a repetição de escrita do grupo.
> 
>

## <a name="user-writeback"></a>Repetição de escrita do utilizador
> [!IMPORTANT]
> Olá funcionalidade de pré-visualização de repetição de escrita do utilizador foi removida no Olá Agosto de 2015 update tooAzure AD Connect. Se tiver ativado o-lo, deve desativar esta funcionalidade.
>
>

## <a name="next-steps"></a>Passos seguintes
Continuar a [instalação personalizada do Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

Saiba mais sobre como [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md).
