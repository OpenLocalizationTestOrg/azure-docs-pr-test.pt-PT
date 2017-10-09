---
title: "Tutorial: Integração do Azure Active Directory com o Salesforce Sandbox | Microsoft Docs"
description: "Saiba como toouse Salesforce Sandbox com o Azure Active Directory tooenable único início de sessão, aprovisionamento automatizado e muito mais!."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: deccd6a07b57c8ba56b7e1c3f3ab311813ca017b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>Tutorial: Integração do Azure Active Directory com o Salesforce Sandbox

o objetivo deste tutorial Olá é integração de Olá tooshow do Azure e a Salesforce Sandbox.  

>[!TIP]
>Para comentários, consulte Olá [página de suporte do Azure](http://go.microsoft.com/fwlink/?LinkId=521878). 
> 

Forneça sandboxes que Olá toocreate de capacidade que várias cópias da sua organização em ambientes diferentes para diversos fins, tal como o desenvolvimento, teste e de preparação, sem comprometer a dados Olá e as aplicações na produção Salesforce organização.  

Para obter mais detalhes, consulte [Sandbox descrição-geral](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)

cenário de Olá descrito neste tutorial pressupõe que já tenha Olá seguintes itens:

* Uma subscrição do Azure válida
* Uma sandbox no site Salesforce.com

Se ainda não tiver uma sandbox válida no site Salesforce.com, terá de toocontact Salesforce.

cenário de Olá descrito neste tutorial consiste em Olá blocos modulares os seguintes:

1. Ativar a integração de aplicações de Olá do Salesforce Sandbox
2. Configurar início de sessão único (SSO)
3. Ativar o seu domínio
4. Configurar o aprovisionamento de utilizadores
5. Atribuir utilizadores

![Cenário](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "cenário")

## <a name="enable-hello-application-integration-for-salesforce-sandbox"></a>Ativar a integração de aplicação Olá para Salesforce Sandbox
o objetivo desta secção Olá é toooutline como integração de aplicações de Olá tooenable do Salesforce sandbox.

**integração de aplicações de Olá tooenable do Salesforce sandbox, execute Olá os seguintes passos:**

1. No Olá portal clássico do Azure, no painel de navegação esquerdo Olá, clique em **do Active Directory**.
   
   ![Do Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "do Active Directory")
2. De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.
3. Clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.
   
   ![Aplicações](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "aplicações")
4. Olá tooopen **Galeria de aplicações**, clique em **adicionar uma aplicação**e, em seguida, clique em **adicionar uma aplicação para a minha organização toouse**.
   
   ![O que fazer pretende toodo? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "Que itens pretende toodo?")
5. No Olá **caixa pesquisa**, tipo **Salesforce Sandbox**.
   
   ![Galeria de aplicações](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Galeria de aplicações")
6. No painel de resultados de Olá, selecione **Salesforce Sandbox**e, em seguida, clique em **concluída** aplicação de Olá tooadd.
   
   ![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")
   
## <a name="configur-single-sign-on-sso"></a>Configur-início de sessão único (SSO)

o objetivo desta secção Olá é toooutline como tooenable utilizadores tooauthenticate tooSalesforce à respetiva conta no Azure AD com Federação com base no protocolo SAML Olá.

**tooconfigure único início de sessão, execute Olá os seguintes passos:**

1. No Olá portal clássico do Azure, no Olá **Salesforce Sandbox** página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá **configurar início de sessão único** caixa de diálogo.
   
   ![Configurar o início de sessão único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "configurar o início de sessão único")
2. No Olá **como seria, como os utilizadores toosign no tooSalesforce Sandbox** página, selecione **Microsoft Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.
   
   ![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")
3. No Olá **URL da aplicação configurar** página, numa Olá **URL de início de sessão** caixa de texto, escreva o URL utilizando Olá seguir o padrão `http://company.my.salesforce.com`e, em seguida, clique em **seguinte**.
   
   ![Configurar o URL da aplicação](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "configurar o URL da aplicação")
4. Se já tiver configurado início de sessão único para outra instância do Salesforce Sandbox no seu diretório, em seguida, também tem de configurar Olá **identificador** toohave Olá mesmo valor que Olá **iniciar sessão no URL**. 
 * Olá **identificador** campo pode ser encontrado verificando Olá **mostrar as definições avançadas** caixa de verificação no Olá **URL da aplicação configurar** página da caixa de diálogo Olá.
5. No Olá **configurar o início de sessão único em Salesforce Sandbox** página, clique em **Transferir certificado**e, em seguida, guarde o ficheiro de certificado Olá no seu computador.
   
   ![Configurar o início de sessão único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "configurar o início de sessão único")
6. Numa janela do browser web diferente, inicie sessão no seu sandbox Salesforce como administrador.
7. No menu de Olá na parte superior do Olá, clique em **configuração**.
   
   ![A configuração](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "programa de configuração")
8. No painel de navegação de Olá Olá esquerda, clique em **controlos de segurança**e, em seguida, clique em **as definições de início de sessão único**.
   
   ![Single Sign-On definições](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "único as definições de início de sessão")
9. Na secção de definições de início de sessão único Olá, execute Olá os seguintes passos:
   
   ![Single Sign-On definições](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "único as definições de início de sessão")  
 1.  Selecione **SAML ativada**. 
 2.  Clique em **Novo**.
10. No Olá SAML único início de sessão da secção definições, execute Olá os seguintes passos:
    
    ![SAML único início de sessão definições](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML único início de sessão definições")  
 1. Na caixa de texto do Olá nome, escreva o nome de Olá da configuração de Olá (por ex.: *SPSSOWAAD\_teste*). 
 2. No Olá portal clássico do Azure, no Olá **configurar o início de sessão único em Salesforce Sandbox** página de diálogo, Olá cópia **URL do emissor** valor e, em seguida, cole-o Olá **emissor**caixa de texto.
 3. No Olá **Id de entidade** caixa de texto, tipo **https://test.salesforce.com** se se tratar de Olá primeira Salesforce Sandbox instância que está a adicionar tooyour diretório. Se já tiver adicionado uma instância do Salesforce Sandbox, em seguida, para Olá **ID de entidade** tipo na Olá **URL de início de sessão**, que deve ter este formato:`http://company.my.salesforce.com`   
 4. Clique em **procurar** Olá tooupload transferido o certificado.  
 5. Como **tipo de identidade de SAML**, selecione **asserção contém Olá Federação ID do objeto de utilizador Olá**. 
 6. Como **SAML identidade localização**, selecione **é de identidade no elemento de NameIdentifier Olá do Olá instrução requerente**.
 7. No Olá portal clássico do Azure, no Olá **configurar o início de sessão único em Salesforce Sandbox** página de diálogo, Olá cópia **URL de início de sessão remoto** valor e, em seguida, cole-o Olá **fornecedor de identidade URL de início de sessão** caixa de texto. 
 8. SFDC não suporta a fim de sessão SAML.  Como solução, cole 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' para Olá **URL de fim de sessão do fornecedor de identidade** caixa de texto.
 9. Como **fornecedor iniciada pedido vínculo de serviço**, selecione **HTTP POST**. 
 10. Clique em **Guardar**.
11. No portal clássico do Azure Olá, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **concluída** tooclose Olá **configurar início de sessão único** caixa de diálogo.
    
    ![Configurar o início de sessão único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "configurar o início de sessão único")

## <a name="enable-your-domain"></a>Ativar o seu domínio
Esta secção assume que já criou um domínio.  Para obter mais detalhes, consulte [definir o nome de domínio](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).

**tooenable o domínio, efetuar Olá os seguintes passos:**

1. No painel de navegação esquerdo Olá, clique em **gestão de domínios**e, em seguida, clique em **meu domínio.**
   
   ![O meu domínio](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "meu domínio")
   
   >[!NOTE]
   >Certifique-se que o seu domínio foi configurado corretamente. 
   > 
2. No Olá **definições de páginas de início de sessão** secção, clique em **editar**, em seguida, como **serviço de autenticação**, selecione nome Olá Olá SAML único início de sessão na definição de Olá anterior secção e, finalmente, clique em **guardar**.
   
   ![O meu domínio](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "meu domínio")

Assim que tiver um domínio configurado, os utilizadores devem utilizar sandbox Salesforce de toohello toologin Olá domínio URL.  

valor de Olá tooget do URL de Olá, clique em perfil SSO Olá que criou na secção anterior Olá.

## <a name="configure-user-provisioning"></a>Configurar o aprovisionamento de utilizadores
o objetivo desta secção Olá é toooutline como tooenable aprovisionamento de utilizadores do utilizador do Active Directory contas tooSalesforce Sandbox.

**tooconfigure aprovisionamento de utilizadores, execute Olá os seguintes passos:**

1. No portal do Salesforce Olá, na barra de navegação superior Olá, selecione o nome tooexpand o menu de utilizador:
   
   ![As minhas definições](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "as minhas definições")
2. No menu do utilizador, selecione **as minhas definições** tooopen sua **as minhas definições** página.
3. No painel esquerdo Olá, clique em **pessoais** tooexpand Olá secção pessoal e, em seguida, clique em **repor o meu Token de segurança**:
   
   ![As minhas definições](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "as minhas definições")
4. No Olá **repor o meu Token de segurança** página, clique em **repor o Token de segurança** toorequest uma mensagem de e-mail que contém o token de segurança em Salesforce.com.
   
   ![Novo Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "novo Token")
5. Verifique a pasta a receber de correio eletrónico para uma mensagem de e-mail em Salesforce.com com "**confirmação de segurança salesforce.com.com**" como requerente.
6. Rever este e-mail e copie Olá segurança token valor.
7. No Olá portal clássico do Azure, no Olá **salesforce Sandbox** página de integração de aplicações, clique em **configurar o aprovisionamento de utilizadores** tooopen Olá **configurar o aprovisionamento de utilizadores**caixa de diálogo.
   
   ![Configurar o aprovisionamento de utilizadores](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "configurar o aprovisionamento de utilizadores")
8. No Olá **introduza aprovisionamento de utilizadores automático o Salesforce Sandbox credenciais tooenable** , indique Olá seguintes definições de configuração:
   
   ![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")   
 1. No Olá **nome de utilizador de Admin do Salesforce Sandbox** caixa de texto, tipo de nome que tem Olá de conta de uma sandbox Salesforce **administrador de sistema** perfil no site Salesforce.com atribuído.
 2. No Olá **palavra-passe de administrador do Salesforce Sandbox** caixa de texto, tipo Olá palavra-passe desta conta.
 3. No Olá **Token de segurança do utilizador** caixa de texto, valor de token de segurança de Olá de colar.
 4. Clique em **validar** tooverify a configuração.
 5. Clique em Olá **seguinte** Olá do botão tooopen **confirmação** página.
9. No Olá **confirmação** página, clique em **concluída** toosave a configuração.
   
## <a name="assigning-users"></a>Atribuir utilizadores

tootest a configuração, terá de toogrant Olá do Azure AD utilizadores tooallow utilizando o tooit de acesso de aplicação atribuindo-los.

**tooassign utilizadores tooSalesforce Sandbox, execute Olá os seguintes passos:**

1. Olá portal clássico do Azure, crie uma conta de teste.
2. No Olá * * Salesforce Sandbox * * página de integração de aplicações, clique em **atribuir utilizadores**.
   
   ![Atribuir utilizadores](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "atribuir utilizadores")
3. Selecione o utilizador de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm a atribuição.
   
   ![Sim](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Sim")

Deve agora Aguarde 10 minutos e certifique-se de que a conta de Olá foi sincronizado tooSalesforce Sandbox.

Se quiser tootest as definições de SSO, abra Olá painel de acesso. Para obter mais detalhes sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](https://msdn.microsoft.com/library/dn308586).

