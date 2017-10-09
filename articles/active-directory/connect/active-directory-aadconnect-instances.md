---
title: "Do Azure AD Connect: Instâncias do serviço de sincronização | Microsoft Docs"
description: "Esta página documentos considerações especiais para instâncias do Azure AD."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a>O Azure AD Connect: Considerações especiais para instâncias
O Azure AD Connect é utilizado frequentemente com a instância de todo o mundo Olá do Azure AD e o Office 365. Mas também existem outras instâncias e estes têm diferentes requisitos para os URLs e outras considerações especiais.

## <a name="microsoft-cloud-germany"></a>Microsoft Cloud Alemanha
Olá [Datacenters da Microsoft Cloud](http://www.microsoft.de/cloud-deutschland) é uma nuvem sovereign operada por uma trustee de dados em alemão.

| URLs tooopen no servidor de proxy |
| --- |
| \*. microsoftonline.de |
| \*.windows.net |
| + Listas de revogação de certificados |

Quando inicia sessão no inquilino do Azure AD tooyour, tem de utilizar uma conta no domínio de onmicrosoft.de Olá.

Funcionalidades atualmente não estão presentes na Olá Microsoft Cloud Datacenters:

* **O Azure AD Connect Health** não está disponível.
* **As atualizações automáticas** não está disponível.
* **Repetição de escrita de palavras-passe** está disponível para pré-visualização com a versão do Azure AD Connect 1.1.570.0 e depois.
* Não estão disponíveis outros serviços do Azure AD Premium.

## <a name="microsoft-azure-government-cloud"></a>Nuvem do Microsoft Azure Government
Olá [cloud do Microsoft Azure Government](https://azure.microsoft.com/features/gov/) é uma nuvem para dos EUA.

Esta nuvem é suportada por versões anteriores do DirSync. De compilação 1.1.180 do Azure AD Connect, Olá próxima geração da nuvem hello é suportado. Esta geração está a utilizar apenas de E.U.A. baseada em pontos finais e ter uma lista de URLs tooopen diferente no seu servidor proxy.

| URLs tooopen no servidor de proxy |
| --- |
| \*.microsoftonline.com |
| \*. microsoftonline.us |
| \*. gov.us.microsoftonline.com |
| + Listas de revogação de certificados |

O Azure AD Connect não é capaz de tooautomatically detetar que o inquilino do Azure AD está localizado na nuvem de Government Olá. Em vez disso, terá de Olá tootake seguintes ações quando instalar o Azure AD Connect.

1. Inicie a instalação do Olá do Azure AD Connect.
2. Quando for apresentada a página primeiro olá onde é suposto tooaccept Olá EULA, não continuar, mas deixe o Assistente de instalação de Olá em execução.
3. Inicie o regedit e alterar a chave de registo Olá `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello valor `2`.
4. Voltar atrás Assistente de instalação do toohello do Azure AD Connect, aceite o EULA de Olá e continuar. Durante a instalação, certifique-se de que toouse Olá **configuração personalizada** caminho de instalação (e não a instalação Express). Em seguida, continue a instalação de Olá como habitualmente.

Funcionalidades atualmente não estão presentes na nuvem do Microsoft Azure Government de Olá:

* **O Azure AD Connect Health** não está disponível.
* **As atualizações automáticas** não está disponível.
* **Repetição de escrita de palavras-passe** está disponível para pré-visualização com a versão do Azure AD Connect 1.1.570.0 e depois.
* Não estão disponíveis outros serviços do Azure AD Premium.

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre como [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md).
