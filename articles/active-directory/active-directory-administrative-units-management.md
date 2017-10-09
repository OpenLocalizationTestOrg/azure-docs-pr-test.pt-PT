---
title: "pré-visualização gestão de unidades de aaaAdministrative no Azure Active Directory"
description: "Utilizar unidades administrativas para mais granular sobre delegação de permissões no Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8464cd6b-1d1a-470d-a4fb-ee29b8eab4c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: elkuzmen
ms.custom: oldportal;it-pro;
ms.openlocfilehash: ee2c7beb6f9f6292bbf3cdeab00801ac066ae0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="administrative-units-management-in-azure-ad---public-preview"></a>Gestão de unidades administrativas no Azure AD - pré-visualização pública
Este artigo descreve unidades administrativas – um novo contentor do Azure Active Directory dos recursos que podem ser utilizadas para delegar permissões administrativas através de subconjuntos de utilizadores e aplicar políticas tooa subconjunto utilizadores. No Azure Active Directory, unidades administrativas permitem aos administradores do administradores central toodelegate permissões tooregional ou tooset política a um nível granular.

Isto é útil em organizações com divisões independentes, por exemplo, um grande university é constituído por muitas autónomas escolas (profissional da empresa, escola engenharia e assim sucessivamente) que são independentes entre si. Essas divisões tem os seus próprios administradores de TI que controlam o acesso, gerem utilizadores e definir políticas especificamente para as respetivas divisão. Administradores centrais pretendem conceder capaz de toobe estas permissões por divisões de administradores através de utilizadores de Olá no respetivos divisões específicos. Mais especificamente, com este exemplo, um administrador central pode, por exemplo, crie uma unidade administrativa para um determinado profissional (escola de negócio) e preenchê-lo com apenas Olá escola utilizadores empresariais. Em seguida, um administrador central pode adicionar escola de negócio Olá IT pessoal tooa âmbito função por outras palavras, conceda Olá equipa de TI de permissões administrativas do profissional de negócio apenas através de unidade de administrativa Olá negócio escola.

> [!IMPORTANT]
> Pode atribuir funções de administrador no âmbito do unidade administrativa apenas se ativar o Azure Active Directory Premium. Para obter mais informações, consulte [introdução ao Azure AD Premium](active-directory-get-started-premium.md).
>


Olá central do ponto de vista de administrador, uma unidade administrativa é um objeto de diretório que pode ser criado e preenchido com os recursos. **Nesta versão de pré-visualização, estes recursos podem ser apenas os utilizadores.** Depois de criadas e preenchidas, unidade administrativa Olá pode ser utilizada como um Olá toorestrict de âmbito concedida permissão apenas através de recursos contidos numa unidade administrativa Olá.

## <a name="managing-administrative-units"></a>Gerir unidades administrativas
Nesta versão de pré-visualização, pode criar e gerir unidades administrativas utilizando cmdlets do módulo Azure Active Directory para Windows PowerShell Olá. mais informações sobre como toolearn toodo que, consulte [trabalhar com unidades administrativas](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)

Para mais informações sobre os requisitos de software e instalar módulo do Olá do Azure AD e para obter informações sobre Olá cmdlets do módulo do Azure AD para gerir unidades administrativas, incluindo sintaxe, descrições de parâmetros e exemplos, consulte [Active Directory do Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0).

## <a name="next-steps"></a>Passos seguintes
[Edições do Azure Active Directory](active-directory-editions.md)
