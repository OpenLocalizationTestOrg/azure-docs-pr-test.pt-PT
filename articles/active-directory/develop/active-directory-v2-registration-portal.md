---
title: "Tópicos de ajuda do Portal de registo de aaaApp | Microsoft Docs"
description: "Uma descrição de diversas funcionalidades do portal de registo de aplicação do Olá Microsoft."
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: f0507c28-9464-4d3e-bd53-de9053fd5278
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: 3eb17b629577446a336152799497e7d980fb825d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="app-registration-reference"></a>Referência de registo de aplicação
Este documento fornece contexto e descrições de diversas funcionalidades encontradas no Olá Portal de registo de aplicações do Microsoft [https://apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).

## <a name="my-applications"></a>As Minhas Aplicações
Esta lista contém todas as aplicações registadas para utilização com o ponto final de v 2.0 do Olá do Azure AD.  Estas aplicações têm Olá capacidade toosign os utilizadores com ambas as contas pessoais da conta Microsoft e contas de trabalho/escola do Azure Active Directory.  toolearn mais informações sobre o ponto final de v 2.0 Olá do Azure AD, consulte a nossa [descrição geral de v 2.0](active-directory-appmodel-v2-overview.md).  Estas aplicações também podem ser utilizado toointegrate com Olá Microsoft conta ponto final de autenticação, `https://login.live.com`.

## <a name="live-sdk-applications"></a>Aplicações do SDK em direto
Esta lista contém todas as aplicações registadas para utilização apenas com a conta Microsoft.  Não estão ativadas para utilização com o Azure Active Directory contratutal.  Este é o qual irá obter todas as aplicações que tinham sido registadas com o portal do programador MSA Olá em `https://account.live.com/developers/applications`.  Todas as funções que efetuou anteriormente em `https://account.live.com/developers/applications` agora pode ser efetuada neste portal novo, `https://apps.dev.microsoft.com`.  Se tiver alguma questão mais sobre as aplicações de conta Microsoft, contacte-nos.

## <a name="application-secrets"></a>Segredos de aplicação
Os segredos de aplicação são credenciais que permitem que a aplicação tooperform fiável [autenticação de cliente](http://tools.ietf.org/html/rfc6749#section-2.3) com o Azure AD.  OAuth & OpenID Connect, segredos uma aplicação é normalmente referidos tooas um `client_secret`.  No protocolo de v 2.0 Olá, qualquer aplicação que recebe um token de segurança numa localização endereçável web (através de um `https` esquema) tem de utilizar um tooidentify segredo de aplicação em si tooAzure AD após resgate esse de token de segurança.  Além disso, qualquer cliente nativo que irão ser proibidos recieves tokens num dispositivo da utilização de uma autenticação de cliente de tooperform segredo de aplicação, toodiscourage Olá armazenamento de segredos em ambientes inseguras.

Cada aplicação pode conter dois segredos de aplicação válida dado momento.  Mantendo dois segredos, tiver Olá ablilty tooperform periódica rollover da chave em todo o ambiente da sua aplicação.  Depois de ter migrado a totalidade de Olá da sua aplicação tooa novo segredo, pode eliminar o segredo antigo Olá e aprovisionar uma nova.

Neste momento, apenas dois tipos de segredos de aplicação são permitidos no portal de registo de aplicação Olá.  Escolher **gerar a nova palavra-passe** irá gerar e armazenar um segredo partilhado no arquivo de dados correspondentes Olá, que pode utilizar na sua aplicação.  Escolher **gerar novo par de chaves** irá criar um novo par de chaves públicas/privadas que pode ser transferido e utilizado para autenticação de cliente tooAzure AD.

## <a name="profile"></a>Perfil
secção de perfil de Olá do portal de registo de aplicação Olá pode ser utilizado o início de sessão do toocustomize Olá na página para a sua aplicação.  Neste momento, pode alterar Olá de início de sessão logótipo de aplicação da página, os termos do URL do serviço e a declaração de privacidade.  Olá logótipo tem de ser uma imagem de pixel de 48 x 48 ou 50 x 50 transparente num ficheiro GIF, PNG ou JPEG 15 KB ou mais pequeno.  Tente alterar Olá visualização resultante da página de início de sessão e valores de Olá!

## <a name="live-sdk-support"></a>Suporte do SDK em direto
Quando ativa "Live SDK suporte", qualquer aplicação segredos que criar serão aprovisionados Olá do Azure AD e os dados da Microsoft Account armazena.  Isto permitirá toointegrate a aplicação diretamente com Olá serviço Account Microsoft (login.live.com).  Se desejar toobuild uma aplicação utilizando o Microsoft Account diretamente (como ponto final v 2.0 do toousing oposição ao hello do Azure AD), deve certificar-se de que o suporte de SDK em direto está ativado.

Desativar o suporte de Live SDK irá garantir que segredo da aplicação Olá só é escrito no arquivo de dados de Olá do Azure AD.  arquivo de dados do Azure AD de Olá incorpora regulamentos de nível empresarial que lhe permite toomeet determinadas normas, como a conformidade de FISMA.  Se ativar o suporte de SDK em direto, a aplicação não pode obter a conformidade com algumas dessas normas.

Se pretender apenas alguma vez o ponto final v 2.0 do toouse Olá do Azure AD, pode desativar em segurança o suporte de Live SDK.

