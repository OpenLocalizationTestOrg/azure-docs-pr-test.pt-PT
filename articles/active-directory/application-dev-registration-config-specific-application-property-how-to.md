---
title: "aaaHow toofill saída campos específicos para uma aplicação desenvolvida personalizado | Microsoft Docs"
description: "Documentação de orientação sobre como toofill saída específicas campos quando registar uma aplicação personalizada desenvolvida com o Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 7e07bc45c58542edb3863db5aad7c845f1a1772e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofill-out-specific-fields-for-a-custom-developed-application"></a>Como toofill saída campos específicos para uma aplicação desenvolvida personalizada

Este artigo dão-lhe uma breve descrição de todos os campos disponíveis Olá no formulário de registo de aplicação Olá no Olá [portal do Azure](https://portal.azure.com).

## <a name="register-a-new-application"></a>Registar uma nova aplicação

-   tooregister uma nova aplicação, navegue toohello [portal do Azure](https://portal.azure.com).

-   No painel de navegação esquerdo Olá, clique em **do Azure Active Directory.**

-   Escolha **registos de aplicação** e clique em **adicionar**.

-   Este Abrir formulário de registo de aplicação Olá de cópia de segurança.

## <a name="fields-in-hello-application-registration-form"></a>Campos no formulário de registo de aplicação Olá


| Campo            | Descrição                                                                              |
|------------------|------------------------------------------------------------------------------------------|
| Nome             | nome da aplicação Olá Olá. Este deve ter um mínimo de quatro caracteres.                |
| Tipo de aplicação | **Web app/Web API**: uma aplicação que representa uma aplicação web, uma API web ou ambos 
| |**Nativo**: uma aplicação que pode ser instalada num computador ou dispositivo do utilizador           |
| URL de início de sessão      | URL de olá onde os utilizadores podem iniciar sessão toouse a aplicação                                  |

Depois de ter preenchidos Olá acima campos, aplicação Olá ser registados no Olá portal do Azure e ser redirecionados toohello página da aplicação. Olá **definições** botão no painel de aplicação Olá abre-se a página de definições de Olá, que tem mais campos para si toocustomize a aplicação. tabela de Olá abaixo descreve todos os campos de Olá na página de definições de Olá. tenha em atenção que apenas conseguiria obter um subconjunto destes campos, dependendo se criou uma aplicação web ou uma aplicação nativa.

| Campo           | Descrição                                                                                                                                                                                                                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID da aplicação  | Ao registar uma aplicação, o Azure AD atribui a aplicação um ID de aplicação. pode ser utilizado o ID da aplicação Olá toouniquely identificar a sua aplicação no tooAzure de pedidos de autenticação AD, bem como recursos tooaccess como Olá Graph API.                                                          |
| URI de ID de aplicação      | Isto deve ser um URI exclusivo, normalmente de forma Olá **https://&lt;inquilino\_nome&gt;/&lt;aplicação\_nome&gt;.** Isto é utilizado durante o fluxo de concessão de autorização de Olá, como identificador exclusivo toospecify Olá recurso o token de Olá deve ser emitido para. Torna também Olá 'aud' afirmações num token de acesso de Olá emitido. |
| Carregar o logótipo novo | Pode utilizar este tooupload um logótipo para a sua aplicação. logótipo de Olá tem de estar no formato *.bmp,. jpg ou PNG e o tamanho do ficheiro Olá deve ser inferior a 100KB. as dimensões de Olá para a imagem de Olá devem ser 215 x 215 pixels, com dimensões de imagem central de 94 x 94 pixels.                                                       |
| URL de página inicial   | Este é Olá início de sessão no URL especificado durante o registo de aplicação.                                                                                                                                                                                                                                              |
| URL de fim de sessão      | Este URL de fim de sessão de início de sessão único Olá. Azure AD envia um URL de toothis de pedido do fim de sessão quando o utilizador Olá limpa a sessão com o Azure AD com qualquer outra aplicação registada.                                                                                                                                       |
| Várias-tenanted  | Este parâmetro especifica se a aplicação Olá pode ser utilizada por vários inquilinos. Normalmente, isto significa que organizações externas podem utilizar a aplicação, registando-o no seu inquilino e os dados da organização tootheir acesso de concessão de permissões.                                                                   |
| URLs de resposta      | URLs de resposta de Olá são pontos finais de olá onde do Azure AD devolver qualquer tokens que solicita a sua aplicação.                                                                                                                                                                                                          |
| URI de redirecionamento   | Para aplicações nativas, este é onde o utilizador Olá ser enviado toofollowing de autorização com êxito. Verificação do AD do Azure que Olá redireciona o URI as fontes de aplicação Olá OAuth 2.0 pedem corresponde a um dos valores de Olá registado no portal de Olá.                                                            |
| Chaves            | Pode criar web de acesso de tooprogrammatically chaves APIs protegidas pelo Azure AD sem qualquer interação do utilizador. De Olá \* \*chaves\* \* página, introduza uma data de expiração de descrição e Olá chave e guardar toogenerate Olá chave. Certifique-se toosave num local seguro, como não será capaz de tooaccess-lo mais tarde.             |

## <a name="next-steps"></a>Passos seguintes
[Gestão de aplicações com o Azure Active Directory](active-directory-enable-sso-scenario.md)
