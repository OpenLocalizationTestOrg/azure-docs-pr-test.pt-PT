---
title: "aaaCustomize o início de sessão página no Azure Active Directory de Olá | Microsoft Docs"
description: "Saiba como tooadd uma página toohello o início de sessão do Azure imagem corporativa da empresa"
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: 7a7ccdeef0764f6cf9e9e224acd4350983031fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-company-branding-tooyour-sign-in-page-in-azure-ad"></a>Guia de introdução: Adicionar página de início de sessão tooyour corporativa no Azure AD
tooavoid confusões, muitas empresas pretendem tooapply uma aspeto e funcionalidade consistentes em todos os sites de Olá e serviços que gerem. Azure Active Directory (Azure AD) fornece esta capacidade, permitindo-lhe o aspecto de Olá toocustomize do início de sessão página Olá com o logótipo da empresa e esquemas de cores personalizados. página de início de sessão Olá é a página Olá que aparece quando inicia sessão no tooOffice 365 ou outras aplicações baseadas na web que estão a utilizar o Azure AD como o fornecedor de identidade. Interagir com esta página tooenter as suas credenciais.

> [!NOTE]
> * Imagem corporativa da empresa está disponível apenas se tiver efetuado a atualização toohello Premium edição ou Basic do Azure AD ou tem uma licença do Office 365. toolearn se uma funcionalidade é suportada pelo tipo de licença, verifique Olá [página de informações de preços do Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).
> 
> * As edições Basic e do Azure Active Directory Premium estão disponíveis para os clientes na China utilizando Olá instância mundial do Azure Active Directory. As edições Basic e do Azure Active Directory Premium não são atualmente suportadas no serviço do Microsoft Azure Olá operado pela 21Vianet na China. Para obter mais informações, contacte-nos em Olá [fórum do Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/).

## <a name="customizing-hello-sign-in-page"></a>Personalizar a página de início de sessão Olá

<!--You can customize hello following elements on hello sign-in page: <attach image>-->

Empresa personalizações de imagem corporativa apresentado na página de início de sessão Olá do Azure AD quando os utilizadores acedem um URL de inquilino específico como [ *https://outlook.com/contoso.com*](https://outlook.com/contoso.com).

Quando os utilizadores visitarem um URL genérico como www.office.com, página de início de sessão Olá não contém corporativa personalizações porque o sistema Olá não souber quem é o utilizador Olá. Imagem corporativa da empresa irá mostrar depois dos utilizadores, introduza o seu ID de utilizador ou selecione um mosaico de utilizador.

> [!NOTE]
> * O nome de domínio tem de aparecer como "Ativo" na Olá **domínios** parte Olá portal do Azure em que tiver configurado uma imagem corporativa. Para obter mais informações, consulte [adicionar um nome de domínio personalizado](add-custom-domain.md).
> * Página de início de sessão de imagem corporativa não passa toohello página de início de sessão para contas Microsoft pessoais. Se os seus funcionários e convidados de negócio inicia sessão com uma conta Microsoft pessoal, a sua página de início de sessão não reflete a Olá imagem corporativa da sua organização.


### <a name="banner-logo"></a>Logótipo de faixa 

Descrição | Restrições | Recomendações
------- | ------- | ----------
logótipo de faixa Olá é apresentado no Olá início de sessão e páginas de painel de acesso de Olá.<br>No início de sessão página Olá, mostra assim que a organização do utilizador Olá é determinada, normalmente, depois de introduzir o nome de utilizador Olá.  | Transparente JPG ou PNG<br>A altura máxima: 36 px<br>A largura máxima: 245 px | Utilize aqui o logótipo da sua organização.<br>Utilize uma imagem transparente. Não parta do princípio que fundo Olá será branco.<br>Não adicione preenchimento à volta o logótipo na imagem de Olá ou o logótipo procurará disproportionately pequeno.

### <a name="username-hint"></a>Sugestão de nome de utilizador   
Descrição | Restrições | Recomendações
------- | ------- | ----------
Isto customizes texto de sugestão Olá no campo de nome de utilizador Olá. | Texto Unicode segurança too64 carateres<br>Apenas texto simples | Recomendamos que não definir esta se espera que os utilizadores convidados fora da sua toosign organização na aplicação tooyour.
            
### <a name="sign-in-page-text"></a>Texto da página de início de sessão   
Descrição | Restrições | Recomendações
------- | ------- | ----------
Isto é apresentado Olá parte inferior do formulário de início de sessão Olá e pode ser utilizados toocommunicate informações adicionais, tais como Olá phone número tooyour suporte técnico ou uma instrução legal. | Texto Unicode segurança too256 carateres<br>Apenas texto simples (sem ligações ou tags de HTML) 

### <a name="sign-in-page-image"></a>Imagem da página de início de sessão  
Descrição | Restrições | Recomendações
------- | ------- | ----------
Esta opção é apresentada no fundo Olá de início de sessão página Olá, toohello ancorada center Olá visualizável do espaço de e será dimensionar e se recortar toofill janela do browser Olá.  <br>Em ecrãs estreitos, como telemóveis, esta imagem não é apresentada.<br>Uma máscara preta com opacidade 0.55 será aplicada sobre esta imagem ao nosso código quando a página Olá é carregada. | JPG ou PNG<br>As dimensões de imagem: px de 1920 x 1080<br>Tamanho de ficheiro: &gt; 300 KB | <br>Utilizar imagens onde não é um foco requerente forte. Olá opaco início de sessão no formulário é apresentado ao longo do Centro de Olá desta imagem e pode abranger qualquer parte da imagem de Olá, consoante o tamanho da janela do browser Olá Olá.<br>Mantenha o tamanho do ficheiro Olá tão pequena como tempos de carregamento rápida de tooensure possíveis. 

### <a name="background-color"></a>Cor de fundo
Descrição | Restrições | Recomendações
------- | ------- | ----------
Esta cor é utilizado em vez de imagem de fundo de Olá em ligações de largura de banda baixa. |   Cor RGB como hexadecimal (exemplo: #FFFFFF | Sugerimos que utilizar Olá primário cor de logótipo de faixa Olá ou a cor da organização.

### <a name="show-option-tooremain-signed-in"></a>Mostrar opção tooremain com sessão iniciada
Descrição | Restrições | Recomendações
------- | ------- | ----------
Azure AD início de sessão fornecem Olá utilizador Olá opção tooremain com sessão iniciada quando fechar e reabrir o seu browser. Utilize este toohide essa opção.<br>Defina esta opção demasiado "não" toohide esta opção dos seus utilizadores. | &nbsp; | Isto não afeta a duração de sessão.<br>Algumas funcionalidades do SharePoint Online e Office 2010 dependem dos utilizadores tooremain toochoose capazes sessão iniciada. Se definir este toobe oculto, os utilizadores poderão ver avisos adicionais e inesperados toosign-in.

> [!NOTE]
> Todos os elementos são opcionais. Por exemplo, se especificar um logótipo de faixa com nenhuma imagem de fundo, página de início de sessão Olá irá mostrar o logótipo e Olá da imagem de fundo para o site de destino Olá (por exemplo, o Office 365).

## <a name="add-company-branding-tooyour-directory"></a>Adicionar publicidade tooyour directory da empresa

1. A iniciar sessão demasiado[Olá portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de Olá.
2. Selecione **mais serviços**, introduza **utilizadores e grupos** no Olá caixa de texto e, em seguida, selecione **Enter**.

   ![Gestão de utilizadores de abertura](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. No Olá **utilizadores e grupos** painel, selecione **da empresa de imagem corporativa**.
4. No Olá **utilizadores e grupos - empresa imagem corporativa** painel, selecione de Olá **editar** comando.

    ![Editar a imagem corporativa personalizado](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. Modifique os elementos de Olá pretende toocustomize. Todos os elementos são opcionais.
6. Clique em **Guardar**.

Pode demorar até uma hora tooan para todas as alterações efetuadas toohello início de sessão página tooappear imagem corporativa.

## <a name="add-language-specific-company-branding-tooyour-directory"></a>Adicionar específicas do idioma imagem corporativa tooyour diretório

1. Inicie sessão no toohello [Centro de administração do Azure AD](https://aad.portal.azure.com) com uma conta que seja um administrador global para o diretório de Olá.
2. Selecione **utilizadores e grupos** no Olá caixa de texto e, em seguida, selecione **Enter**.

   ![Gestão de utilizadores de abertura](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. No Olá **utilizadores e grupos** painel, selecione **da empresa de imagem corporativa**.
4. No Olá **utilizadores e grupos - empresa imagem corporativa** painel, selecione de Olá **Adicionar idioma** comando.

    ![Adicionar elementos de imagem corporativa específicas do idioma](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. Modifique os elementos de Olá pretende toocustomize. Todos os elementos são opcionais.
6. Clique em **Guardar**.

Pode demorar até uma hora tooan para todas as alterações efetuadas toohello início de sessão página tooappear imagem corporativa.

## <a name="next-steps"></a>Passos seguintes
Este guia de introdução, aprendeu como tooadd da empresa a imagem corporativa tooyour do Azure AD directory. 

Pode utilizar Olá seguir ligação tooconfigure sua imagem corporativa no Azure AD de Olá portal do Azure.

> [!div class="nextstepaction"]
> [Configurar o branding da empresa](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LoginTenantBrandingBlade) 