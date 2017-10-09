---
title: "aaaAutomated SaaS aplicação aprovisionamento de utilizadores no Azure AD | Microsoft Docs"
description: "Um toohow de introdução, pode utilizar o aprovisionamento de tooautomatically do Azure AD, anular o aprovisionamento e atualizar continuamente as contas de utilizador entre várias aplicações de SaaS de terceiros."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 58c5fa2d-bb33-4fba-8742-4441adf2cb62
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: curtand
ms.openlocfilehash: a1f3ecdd513e2b603f8ad9901e9f551b3b982b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-user-provisioning-and-deprovisioning-toosaas-applications-with-azure-active-directory"></a>Automatizar utilizador aprovisionamento e desaprovisionamento tooSaaS aplicações com o Azure Active Directory
## <a name="what-is-automated-user-provisioning-for-saas-apps"></a>O que é o utilizador o aprovisionamento automatizado para aplicações SaaS?
Azure Active Directory (Azure AD) permite-lhe a criação de Olá tooautomate, manutenção e remoção de identidades de utilizador na nuvem ([SaaS](https://azure.microsoft.com/overview/what-is-saas/)) aplicações como o Dropbox, Salesforce, ServiceNow e muito mais.

**Seguem-se alguns exemplos de que esta funcionalidade permite-lhe toodo:**

* Crie automaticamente novas contas no Olá direita aplicações de SaaS para pessoas novo quando que se associam a sua equipa.
* Desative automaticamente as contas de aplicações SaaS quando as pessoas inevitavelmente deixam equipa Olá.
* Certifique-se de que as identidades de Olá nas suas aplicações de SaaS são mantidas segurança toodate com base nas alterações no diretório de Olá.
* Aprovisionar objetos de não utilizadores, tais como grupos, aplicações de tooSaaS que suportam-los.

**Aprovisionamento de utilizadores automatizada inclui também Olá seguintes funcionalidades:**

* Olá capacidade toomatch existente as identidades entre o Azure AD e aplicações SaaS.
* Toohelp de opções de personalização do Azure AD ajustar as configurações atuais do Olá de Olá aplicações de SaaS que a sua organização está atualmente a utilizar.
* Alertas de e-mail opcional para o aprovisionamento de erros.
* Relatórios e a atividade toohelp de registos com a monitorização e resolução de problemas.

## <a name="why-use-automated-provisioning"></a>Porquê utilizar o aprovisionamento automatizado?
Alguns motivações comuns para utilizar esta funcionalidade incluem:

* os custos de Olá tooavoid, inefficiencies e erro humano associado com processos de aprovisionamento manual.
* toosecure da sua organização, de forma instantânea, removendo as identidades dos utilizadores do chave aplicações SaaS quando se deixam a organização de Olá.
* tooeasily importar em massa um número de utilizadores para uma determinada aplicação SaaS.
* tooenjoy Olá para efeitos práticos de ter a sua solução de aprovisionamento executar retire Olá mesmo políticas de acesso de aplicação que definiu para o Azure AD Single Sign-On.

## <a name="frequently-asked-questions"></a>Perguntas Mais Frequentes
**Frequência é que o Azure AD escrever alterações de diretório toohello aplicações de SaaS?**

Azure AD verifica a existência de alterações a cada cinco minutos tooten. Se Olá SaaS aplicação está a devolver vários erros (como Olá maiúsculas e minúsculas de credenciais de administrador inválido), em seguida, do Azure AD lenta gradualmente respetivo tooonce de tooup frequência por dia até que os erros de Olá sejam corrigidos.

**Quanto será necessário tooprovision os meus utilizadores?**

As alterações incrementais quase instantaneamente acontecer, mas se está a tentar tooprovision maioria do seu diretório, em seguida, depende do número de Olá de utilizadores e grupos que tiver. Diretórios pequenos demorar apenas alguns minutos, diretórios média poderão demorar vários minutos e diretórios muito grandes, podem demorar várias horas.

**Como controlar o progresso de Olá da tarefa de aprovisionamento atual Olá?**

Pode rever Olá relatório de aprovisionamento da conta na secção de relatórios de Olá do seu diretório. Outra opção é o separador de Dashboard Olá toovisit para Olá aplicação SaaS que são aprovisionamento para e procure em Olá secção "Integração Status" quase Olá parte inferior da página Olá.

**Como posso saber se os utilizadores não conseguem tooget aprovisionado corretamente?**

No fim de Olá do Olá assistente configuração aprovisionamento é notificações de tooemail de toosubscribe uma opção para o aprovisionamento de falhas. Também pode verificar toosee de relatório de erros de aprovisionamento de Olá os utilizadores que não foi possível toobe aprovisionado e por que motivo.

**Azure AD escrever alterações do diretório de back-toohello Olá SaaS aplicação?**

Para a maioria das aplicações de SaaS, o aprovisionamento é apenas de saída, que significa que os utilizadores são escritos da aplicação de toohello Olá diretório e as alterações da aplicação Olá não podem ser escritas novamente toohello diretório. Para [Workday](https://msdn.microsoft.com/library/azure/dn762434.aspx), no entanto, o aprovisionamento é de entrada só, que significa que o se os utilizadores são importados para o diretório de Olá do Workday e da mesma forma, as alterações no diretório de Olá não obter gravadas no Workday.

**Como posso submeter a equipa de engenharia do toohello de comentários?**

Contacte-nos através de Olá [fórum de comentários do Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/).

## <a name="how-does-automated-provisioning-work"></a>Como funciona o trabalho de aprovisionamento automatizado?
Azure AD Aprovisiona utilizadores tooSaaS aplicações através da ligação a pontos finais tooprovisioning fornecidos pelo fornecedor de cada aplicação. Permitem a estes pontos finais do Azure AD tooprogrammatically criar, atualizar e remover utilizadores. Segue-se uma breve descrição geral de Olá diferentes passos que do Azure AD demora tooautomate aprovisionamento.

1. Quando ativar o modo de aprovisionamento de uma aplicação para Olá pela primeira vez, Olá seguintes ações é efetuada:
   * Azure AD tentará toomatch quaisquer utilizadores existentes na aplicação de SaaS Olá com as respetivas identidades no diretório de Olá correspondentes. Quando um utilizador é correspondido, são *não* automaticamente ativado para o início de sessão único. Por ordem para uma aplicação de toohello de acesso do utilizador toohave, estes devem ser explicitamente atribuídas toohello aplicação no Azure AD, diretamente ou através de associação de grupo.
   * Se já tiver especificado os utilizadores que devem ser atribuídos toohello aplicação e do Azure AD falhar toofind contas existentes para os utilizadores, do Azure AD irá aprovisionar novas contas para os mesmos na aplicação Olá.
2. Assim que a sincronização inicial Olá foi concluída conforme descrito acima, do Azure AD irá verificar a cada 10 minutos para Olá seguintes alterações:
   * Se os novos utilizadores que foram atribuídos toohello aplicação (diretamente ou através da associação de grupo), em seguida, estes serão aprovisionados uma nova conta na aplicação de SaaS Olá.
   * Se o um utilizador acesso aos foi removido, em seguida, a conta na aplicação de SaaS Olá será marcada como desativado (os utilizadores são nunca totalmente eliminados, que protege, de perda de dados no evento Olá de uma configuração incorreta).
   * Se um utilizador recentemente foi atribuído toohello aplicação e já tinham uma conta no Olá aplicação SaaS, que conta será marcada como ativada e podem ser atualizadas algumas propriedades do utilizador, se estiverem desatualizados toohello em comparação com diretório.
   * Se tem sido alteradas informações de um utilizador (tais como o número de telefone do escritório, etc.) no diretório de Olá, em seguida, essas informações serão também atualizadas no Olá aplicação SaaS.

Para mais informações sobre como os atributos mapeados entre o Azure AD e a aplicação SaaS, consulte o artigo de Olá no [personalizar mapeamentos de atributos](active-directory-saas-customizing-attribute-mappings.md).

## <a name="list-of-apps-that-support-automated-user-provisioning"></a>Lista de aplicações que suportam o aprovisionamento automatizado do utilizador
Todas as aplicações de "Em destaque" Olá na Galeria de aplicações do Azure AD Olá de suportar o aprovisionamento automatizado do utilizador. [lista de Olá de aplicações em destaque pode ser visualizada aqui.](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured)

Por ordem para uma aplicação toosupport automatizada aprovisionamento de utilizadores, este deve primeiro fornecer Olá pontos finais necessários que permitirem a criação do programas externo tooautomate Olá, manutenção e remoção de utilizadores. Por conseguinte, nem todas as aplicações de SaaS são compatíveis com esta funcionalidade. Para aplicações que suportem este, equipa de engenharia do Olá do Azure AD irá, em seguida, ser capaz de toobuild um aprovisionamento toothose de conector de aplicações e este trabalho é definido por Olá às necessidades da atuais e potenciais clientes.

engenharia de Olá do Azure AD toocontact equipa toorequest aprovisionamento suporte para aplicações adicionais, submeta uma mensagem através de Olá [fórum de comentários do Azure Active Directory](https://feedback.azure.com/forums/374982-azure-active-directory-application-requests/category/172035-user-provisioning).

## <a name="related-articles"></a>Artigos relacionados
* [Índice de Artigos da Gestão da Aplicação no Azure Active Directory](active-directory-apps-index.md)
* [Personalizar os mapeamentos de atributos para o aprovisionamento de utilizador](active-directory-saas-customizing-attribute-mappings.md)
* [Escrever expressões para mapeamentos de atributos](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Filtros de âmbito para o aprovisionamento de utilizador](active-directory-saas-scoping-filters.md)
* [Utilizar o SCIM tooenable aprovisionamento automático de utilizadores e grupos do Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Notificações de aprovisionamento de contas](active-directory-saas-account-provisioning-notifications.md)
* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS](active-directory-saas-tutorial-list.md)

