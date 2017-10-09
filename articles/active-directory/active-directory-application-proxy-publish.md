---
title: "aaaPublish aplicações com o Proxy de aplicações do Azure AD | Microsoft Docs"
description: "Publica na nuvem de toohello de aplicações no local com o Proxy de aplicações do Azure AD no portal clássico Olá."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7926998314c65521ae48aebcceb33cb0c67e0b87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>Publicar aplicações com o Proxy da Aplicação do Azure AD

> [!div class="op_single_selector"]
> * [Portal do Azure](application-proxy-publish-azure-portal.md)
> * [Portal Clássico do Azure](active-directory-application-proxy-publish.md)

Proxy de aplicações do Azure AD ajuda-o suporte a funcionários remotos através da publicação toobe de aplicações no local através do Olá internet. Nesta altura, já deverá ter [ativado o Proxy da aplicação no portal clássico do Azure de Olá](active-directory-application-proxy-enable.md). Este artigo explica-lhe Olá passos toopublish aplicações que estão em execução na sua rede local e fornecem acesso remoto seguro fora da rede. Depois de concluir este artigo, estará pronto tooconfigure aplicação de Olá com informação personalizada ou requisitos de segurança.

> [!NOTE]
> Proxy de aplicações é uma funcionalidade que só está disponível se tiver efetuado a atualização toohello Premium edição ou Basic do Azure Active Directory. Para obter mais informações, consulte [Edições do Azure Active Directory](active-directory-editions.md). Se quiser toouse Proxy de aplicações, pode [publicar aplicações no portal do Azure de Olá](application-proxy-publish-azure-portal.md).

## <a name="publish-an-app-using-hello-wizard"></a>Publicar uma aplicação utilizando o Assistente de Olá
1. Inicie sessão como administrador no Olá [portal clássico do Azure](https://manage.windowsazure.com/).
2. Aceda tooActive diretório e selecione o diretório de olá onde ativou o Proxy de aplicações.
   
    ![Active Directory – ícone](./media/active-directory-application-proxy-publish/ad_icon.png)
3. Clique em Olá **aplicações** separador e, em seguida, clique em Olá **adicionar** botão na Olá parte inferior do ecrã de Olá
   
    ![Adicionar aplicação](./media/active-directory-application-proxy-publish/aad_appproxy_selectdirectory.png)
4. Selecione **Publicar uma aplicação acessível fora da rede**.
   
    ![Publicar uma aplicação acessível fora da rede](./media/active-directory-application-proxy-publish/aad_appproxy_addapp.png)
5. Fornece Olá seguintes informações sobre a sua aplicação:
   
   * **Nome**: nome amigável de utilizador do Olá para a sua aplicação. Tem de ser exclusivo no diretório.
   * **URL interno**: endereço Olá Olá conector do Proxy da aplicação utiliza tooaccess Olá aplicação dentro da sua rede privada. Pode fornecer um caminho específico no Olá toopublish de servidor de back-end, enquanto o resto hello do servidor de Olá é publicado. Desta forma, poderá publicar sites diferentes no Olá mesmo servidor e atribuir a cada um seus próprio nome e regras de acesso.
     
     > [!TIP]
     > Se publicar um caminho, certifique-se de que inclui todas as imagens necessárias Olá, scripts e folhas de estilo para a sua aplicação. Por exemplo, se a aplicação estiver em https://yourapp/app e utiliza as imagens localizadas em https://yourapp/media, deve publicar https://yourapp/ como caminho Olá.
     > 
     > 
   * **Método de pré-autenticação**: como Proxy da aplicação verifica os utilizadores antes de conceder acesso tooyour aplicação. Escolha uma das opções de Olá Olá menu de lista pendente.
     
     * Azure Active Directory: O Proxy da aplicação redireciona os utilizadores toosign sessão no Azure AD, que autentica as respetivas permissões para o diretório de Olá e a aplicação.
     * Passth-Rough: Os utilizadores não têm aplicações de Olá tooauthenticate tooaccess.
     
     ![Propriedades da aplicação](./media/active-directory-application-proxy-publish/aad_appproxy_appproperties.png)  
6. Assistente de Olá toofinish, clique em marca de verificação Olá em Olá parte inferior do ecrã de Olá. aplicação de Olá está agora definida no Azure AD.

## <a name="assign-users-and-groups-toohello-application"></a>Atribuir utilizadores e grupos toohello aplicação
Ordenar para os seus utilizadores tooaccess a aplicação publicada, terá de tooassign-los individualmente ou em grupos. (Lembre-se tooassign si aceder, demasiado.) Cada utilizador que atribuir precisa de uma licença para o Azure Básico ou superior. Pode atribuir licenças individualmente ou toogroups. Para obter mais informações, consulte [atribuir utilizadores tooan aplicação](active-directory-applications-guiding-developers-assigning-users.md). 

Para aplicações que requerem pré-autenticação, atribuir um utilizador concede a aplicação de Olá toouse de permissão. Para aplicações que não necessitam de pré-autenticação, atribuir um utilizador significa que o utilizador Olá pode aceder à aplicação de Olá através do painel de acesso de Olá.

1. Após o Assistente Adicionar aplicação Olá adira agora, pode ver Olá página para a sua aplicação de início rápido. toomanage quem tem acesso toohello aplicação, selecione **utilizadores e grupos**.
   
    ![Início rápido do Proxy da Aplicação para atribuir utilizadores – captura de ecrã](./media/active-directory-application-proxy-publish/aad_appproxy_usersgroups.png)
2. Procure grupos específicos no diretório ou veja todos os utilizadores. resultados de pesquisa do toodisplay Olá, clique em marca de verificação Olá.
   
      ![Procurar grupos ou utilizadores - captura de ecrã](./media/active-directory-application-proxy-publish/aad_appproxy_search.png)
3. Selecione cada utilizador ou grupo que pretende tooassign toothis aplicação e clique em **atribuir**. É-lhe pedido tooconfirm esta ação.

> [!NOTE]
> Para aplicações de Autenticação Integrada do Windows, apenas pode atribuir utilizadores e grupos que são sincronizados a partir do Active Directory no local. As aplicações publicadas com o Proxy da Aplicação do Azure Active Directory não podem ser atribuídas a utilizadores que iniciam sessão com uma conta Microsoft ou a convidados. Certifique-se de que os utilizadores iniciam sessão com as credenciais que fazem parte do Olá mesmo domínio que aplicação Olá que está a publicar.
> 
> 

## <a name="test-your-published-application"></a>Testar a aplicação publicada
Assim que tiver publicado a aplicação, pode testá-la navegando toohello URL que publicou. Verifique se consegue aceder à aplicação, se compõe corretamente e se tudo funciona conforme esperado. Se tiver dificuldade ou receber uma mensagem de erro, tente Olá [guia de resolução de problemas](active-directory-application-proxy-troubleshoot.md).

## <a name="configure-your-application"></a>Configurar a aplicação
Pode modificar as aplicações publicadas ou configurar opções avançadas na página de configuração de Olá. Nesta página, pode personalizar a sua aplicação ao alterar o nome de Olá ou ao carregar um logótipo. Também pode gerir as regras de acesso como Olá método de pré-autenticação ou a autenticação multifator.

![Configuração avançada](./media/active-directory-application-proxy-publish/aad_appproxy_configure.png)

Depois de publicar aplicações com o Proxy de aplicações de diretório Active Directory do Azure, estas aparecem na lista de aplicações de Olá no Azure AD e pode gerir.

Se desativar os serviços do Proxy da aplicação depois de ter publicado aplicações, aplicações de Olá deixam de estar acessíveis fora da rede privada. Os utilizadores ainda podem aceder Olá aplicações no local como habitualmente.

tooview uma aplicação e faça Certifique-se que é acessível, faça duplo clique Olá nome da aplicação Olá. Se estiver desativado Olá serviço Proxy de aplicações e aplicação Olá não está disponível, aparece uma mensagem de aviso, Olá parte superior do ecrã de Olá.

toodelete uma aplicação, selecione uma aplicação na lista de Olá e, em seguida, clique em **eliminar**.

## <a name="next-steps"></a>Passos seguintes
* [Publicar aplicações com o seu próprio nome de domínio](active-directory-application-proxy-custom-domains.md)
* [Ativar o início de sessão único](active-directory-application-proxy-sso-using-kcd.md)
* [Ativar o acesso condicional](active-directory-application-proxy-conditional-access.md)
* [Trabalhar com aplicações com suporte para afirmações](active-directory-application-proxy-claims-aware-apps.md)

Para obter notícias mais recentes Olá e atualizações, consulte Olá [blogue do Proxy da aplicação](http://blogs.technet.com/b/applicationproxyblog/)

