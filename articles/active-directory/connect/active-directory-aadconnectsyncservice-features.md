---
title: "funcionalidades e configuração de serviço de sincronização do aaaAzure AD Connect | Microsoft Docs"
description: "Descreve as funcionalidades do lado do serviço para o serviço de sincronização do Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 7ad05c45bb6b5fd5deaa3466e2936b19d3d9eabb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-features"></a>Funcionalidades do serviço de sincronização do Azure AD Connect
funcionalidade de sincronização de Olá do Azure AD Connect tem dois componentes:

* componente do Olá no local com o nome **sincronização do Azure AD Connect**, também chamado **motor de sincronização**.
* serviço de Olá que reside no Azure AD também conhecido como **serviço de sincronização do Azure AD Connect**

Este tópico explica como Olá seguintes funcionalidades de Olá **serviço de sincronização do Azure AD Connect** trabalho e como pode configurá-los através do Windows PowerShell.

Estas definições são configuradas por Olá [módulo Azure Active Directory para Windows PowerShell](http://aka.ms/aadposh). Transfira e instale-o em separado a partir do Azure AD Connect. cmdlets de Olá documentados neste tópico foram introduzidos no Olá [versão de Março de 2016 (compilação 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1). Se não tiver cmdlets Olá documentados neste tópico ou não produzem Olá mesmo resulta, em seguida, certifique-se, executar a versão mais recente Olá.

configuração de Olá toosee no diretório do Azure AD, execute `Get-MsolDirSyncFeatures`.  
![Get-MsolDirSyncFeatures resultado](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)

Muitas destas definições só podem ser alteradas pelo Azure AD Connect.

Olá seguintes definições podem ser configuradas pelo `Set-MsolDirSyncFeature`:

| DirSyncFeature | Comentário |
| --- | --- |
| [EnableSoftMatchOnUpn](#userprincipalname-soft-match) |Permite objetos toojoin no userPrincipalName endereço tooprimary SMTP de adição. |
| [SynchronizeUpnForManagedUsers](#synchronize-userprincipalname-updates) |Permite que o atributo userPrincipalName de Olá tooupdate Olá sincronização motor para gerido/licenciado utilizadores (não federada). |

Depois de ter ativado uma funcionalidade, não é possível desativar novamente.

> [!NOTE]
> De 24 de Agosto de 2016 Olá funcionalidade *duplicado resiliência de atributo* está ativada por predefinição para o novo Azure diretórios AD. Esta funcionalidade será também revertida e ativada em diretórios criados antes desta data. Receberá uma notificação por e-mail ao seu diretório é sobre tooget esta funcionalidade ativada.
> 
> 

Olá seguintes definições são configuradas pelo Azure AD Connect e não pode ser modificadas por `Set-MsolDirSyncFeature`:

| DirSyncFeature | Comentário |
| --- | --- |
| DeviceWriteback |[O Azure AD Connect: Ativar a repetição de escrita do dispositivo](active-directory-aadconnect-feature-device-writeback.md) |
| DirectoryExtensions |[Sincronização do Azure AD Connect: extensões de diretórios](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency](#duplicate-attribute-resiliency) |Permite que um toobe atributo colocados em quarentena quando é um duplicado de outro objeto em vez de objeto Olá de toda a falhar durante a exportação. |
| PasswordSync |[Implementar a sincronização de palavras-passe com a sincronização do Azure AD Connect](active-directory-aadconnectsync-implement-password-synchronization.md) |
| UnifiedGroupWriteback |[Pré-visualização: Repetição de escrita de grupo](active-directory-aadconnect-feature-preview.md#group-writeback) |
| UserWriteback |Não é atualmente suportado. |

## <a name="duplicate-attribute-resiliency"></a>Resiliência de atributo duplicado
Em vez de falhar tooprovision objetos com UPNs duplicados / proxyAddresses, atributo duplicado Olá é "colocados em quarentena" e um valor temporário está atribuído. Quando o conflito de Olá for resolvido, Olá temporário UPN é alterado automaticamente o valor adequado toohello. Para obter mais detalhes, consulte [resiliência de atributo de sincronização e duplicado identidade](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).

## <a name="userprincipalname-soft-match"></a>Correspondência de forma recuperável UserPrincipalName
Quando esta funcionalidade está ativada, configuração soft-match está ativada para UPN na adição toohello [endereço SMTP principal](https://support.microsoft.com/kb/2641663), que está sempre ativada. Correspondência de forma recuperável é utilizadores de nuvem existente toomatch utilizado no Azure AD com utilizadores no local.

Se precisar de toomatch no local Contas de anúncios com criados na nuvem de Olá de contas existentes e não estiver a utilizar Exchange Online, em seguida, esta funcionalidade é útil. Neste cenário, geralmente não tiver um atributo de SMTP do motivo tooset Olá na nuvem de Olá.

Esta funcionalidade está em por predefinição para recentemente criada diretórios do Azure AD. Pode ver se esta funcionalidade está ativada para si, executando a aplicação:  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

Se esta funcionalidade não está ativada para o diretório do Azure AD, pode ativá-la ao executar:  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a>Sincronizar atualizações de userPrincipalName
Historicamente, atributo UserPrincipalName toohello de atualizações utilizando o serviço de sincronização de Olá no local foi bloqueado, exceto se ambas estas condições forem verdadeiras:

* utilizador Olá é gerido (não federada).
* Não foi atribuída uma licença de utilizador de Olá.

Para obter mais detalhes, consulte [utilizador nomes no Office 365, Azure ou Intune não correspondem Olá UPN no local ou o ID de início de sessão alternativo](https://support.microsoft.com/kb/2523192).

Ativar esta funcionalidade permite Olá sincronização motor tooupdate Olá userPrincipalName quando é alterado no local e utilizar a sincronização de palavra-passe. Se utilizar a Federação, esta funcionalidade não é suportada.

Esta funcionalidade está em por predefinição para recentemente criada diretórios do Azure AD. Pode ver se esta funcionalidade está ativada para si, executando a aplicação:  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

Se esta funcionalidade não está ativada para o diretório do Azure AD, pode ativá-la ao executar:  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

Depois de ativar esta funcionalidade, os valores de userPrincipalName existentes permanecerá como-é. Na próxima alteração de Olá userPrincipalName atributo no local, a sincronização de diferenças normal Olá nos utilizadores atualizará Olá UPN.  

## <a name="see-also"></a>Consultar também
* [Sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md)
* [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md).

