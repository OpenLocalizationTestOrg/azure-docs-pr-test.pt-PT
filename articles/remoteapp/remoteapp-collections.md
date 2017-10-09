---
title: "tipo de aaaWhat de coleção efetue necessita para o Azure RemoteApp? | Microsoft Docs"
description: "Saiba mais sobre os tipos de Olá de coleções disponíveis com o Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c13ec78d-07e9-4646-8194-cf3efafc1760
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: f00b5fe41af597cf75e26300bf7842c3a8ff94fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-kind-of-collection-do-you-need-for-azure-remoteapp"></a>Que tipo de coleção precisa para o Azure RemoteApp?
> [!IMPORTANT]
> O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017. Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.
> 
> 

O Azure RemoteApp permite-lhe partilhar aplicações e recursos com utilizadores em qualquer dispositivo. Podemos fazê-lo através da criação de coleções toohold Olá aplicações e recursos e, em seguida, partilhar essas coleções com utilizadores. Existem 2 Opções de coleção diferente, com a outra rede e as opções de autenticação - que é mais adequada para si?

Vamos guiá-lo através de considerações de diferentes Olá e opções terá toomake tooget Olá mais fora da sua coleção do Azure RemoteApp. 

## <a name="quick-differences-between-hello-collection-types"></a>Diferenças rápidas entre tipos de coleção de Olá
|  | Nuvem | Híbrido |
| --- | --- | --- |
| Utilize uma VNET existente |Sim |Sim |
| Requer contas ligados AD (DirSync) |Não |Sim |
| Requer a associação a um domínio |Não |Sim |
| Requer tooVNET acessíveis de controlador de domínio |Não |Sim |

## <a name="cloud-collections"></a>Coleções na nuvem
* Toocreate rápida - coleção Olá rapidamente é aprovisionado, que significa que as suas aplicações obter toousers mais rápida.
* Traga as suas aplicações ou partilha ours. Pode utilizar uma imagem personalizada (criada a partir de uma VM do Azure) ou uma das imagens de Olá incluídas na sua subscrição.
* Não precisa de tooconfigure uma ligação entre a coleção e o seu domínio no local.
* Mas, opcionalmente, pode utilizar o seus próprios acesso tooprovide de VNET do Azure para o seu ambiente no local para dados de partilha ou toouse não-autenticação do Windows para recursos como o SQL Server (utilizando a autenticação de base de dados).

OK, como criar um?

* Apenas na nuvem? Criar com Olá **criação rápida** opção no portal de Olá.
* Nuvem + VNET? Criar utilizando Olá **criar com VNET** opção, mas não escolha toojoin um domínio.

## <a name="hybrid-collections"></a>Coleções híbridas
* Forneça a rede de tooon local de acesso total + Azure VNET.
* Inclui o acesso de associação de domínio para as aplicações e dados. Aplicações remotas podem autenticação contra o Active Directory no local -, em seguida, podem aceder a recursos no seu domínio.
* Ativar monitorização avançada gestão e com as soluções do System Center existentes e as políticas de grupo do Windows (através de uma imagem personalizada incorporada no Windows Server 2012 R2)
* Suporte [ExpressRoute](https://azure.microsoft.com/services/expressroute/) tooconnect tooyour seu Azure VNET a VNET local.

Criar utilizando Olá **criar com VNET** opção e escolha toojoin um domínio.

## <a name="authentication-options"></a>Opções de autenticação
O Azure RemoteApp suporta contas Microsoft e contas do Azure Active Directory, mas não todas as coleções suportam todos os métodos. 

| Tipo de conta |  | Nuvem | Nuvem + VNET | Híbrido |
| --- | --- | --- | --- | --- |
| Conta Microsoft | |Sim |Sim |Não |
| Azure Active Directory (Azure AD) | | | | |
| Apenas AD do Azure |Sim |Sim |Não | |
| AD Connect com sincronização de palavra-passe |Sim |Sim |Sim | |
| AD Connect sem sincronização de palavra-passe |Sim |Sim |Não | |
| AD Connect com o AD FS |Sim |Sim |Sim | |
| fornecedores de identidade de suportados pelo Azure de 3rd terceiros (como o Ping) |Sim |Sim |Sim | |
| Multi-Factor Authentication | |Sim |Sim |Sim |

### <a name="cloud-and-cloud--vnet"></a>Nuvem e nuvem + VNET
Com as coleções na nuvem, pode utilizar contas Microsoft, contas do Azure AD ou uma combinação de Olá dois. Utilize as contas de Olá que funcionam melhor para os seus utilizadores.

Não existem não requisitos específicos para a utilização de contas Microsoft. 

Se pretender que as contas do Azure AD de toouse, terá de toomake certificar-se de que o inquilino do Azure AD corresponde ao hello um associados à subscrição. Quando tiver criado a sua subscrição do Azure RemoteApp, inquilino do Azure AD Olá que estava a utilizar foi automaticamente associado à sua subscrição. Qualquer utilizador do Azure AD está a conceder permissão tooneeds toobe esse mesmo inquilino. Se necessário, pode [alterar inquilino do Azure AD de Olá](remoteapp-changetenant.md) associados à subscrição.

### <a name="hybrid-or-cloud--azure-ad--ad"></a>Híbrido (ou nuvem + Azure AD + AD)
Utilizar o Azure AD + no local do Active Directory é um pré-requisito para uma coleção híbrida. É necessário toouse AD Connect toointegrate Olá dois diretórios. Mas ter alguns escolha quando se trata toohow configurar o AD Connect. 

Existem 2 AD Connect cenários - utilizando a sincronização de palavra-passe ou Federação do AD. Veja Olá [AD Connect informações](../active-directory/active-directory-aadconnect.md) toofigure saída que destes funciona melhor para si.

Pode também utilizar o Azure AD + AD com uma coleção na nuvem. Certifique-se de que segue Olá mesmo configurar passos.

Veja [do Azure AD + requisitos do Active Directory para o Azure RemoteApp](remoteapp-ad.md) para Olá passos necessários tooconfigure do Azure AD e do Active Directory.

## <a name="go-create-your-collection"></a>Aceda a criar a sua coleção!
OK, julgo tiver figured-agora, pelo que não existe apenas uma toodo esquerdo de coisa - criar a primeira coleção do Azure RemoteApp.

[Criar uma coleção na nuvem](remoteapp-create-cloud-deployment.md) ou [criar uma coleção híbrida](remoteapp-create-hybrid-deployment.md) -apenas obter criar.

