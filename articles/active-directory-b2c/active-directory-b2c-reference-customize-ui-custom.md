---
title: "Do Azure Active Directory B2C: Referência: Personalizar Olá IU da journey utilizador com as políticas personalizadas | Microsoft Docs"
description: "Um tópico sobre as políticas personalizadas do Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 11f2a7575b95a186399d83266850fe44d650371b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-ui-of-a-user-journey-with-custom-policies"></a>Personalizar Olá IU da journey utilizador com as políticas personalizadas

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

> [!NOTE]
> Este artigo é uma descrição avançada como funciona a personalização da IU e como tooenable com as políticas de B2C personalizada, utilizando Olá Framework de experiência de identidade


Uma experiência de utilizador totalmente integrada é a chave para qualquer solução de empresa-consumidor. Através da experiência de utilizador totalmente integrada, estamos significa uma experiência, no dispositivo ou browser, onde journey de um utilizador através do nosso serviço não pode ser distinguida das serviço de cliente Olá estão a utilizar.

## <a name="understand-hello-cors-way-for-ui-customization"></a>Compreender a forma CORS Olá de personalização de IU

O Azure AD B2C permite toocustomize Olá aspeto-e-funcionalidade de experiência de utilizador (UX) no Olá várias páginas que podem ser servidas e apresentadas pelo Azure AD B2C através de políticas personalizadas do seu potencialmente.

Para essa finalidade, o Azure AD B2C executa o código no browser do cliente e utiliza Olá abordagem moderna e standard [de partilha de recursos de várias origens (CORS)](http://www.w3.org/TR/cors/) conteúdo personalizado tooload a partir de um URL específico que especificar numa política personalizada modelos do toopoint tooyour HTML5/CSS. CORS é um mecanismo que permite recursos restritos, como tipos de letra, no toobe página web pedidos a partir de outro domínio fora do domínio Olá partir do qual o recurso de Olá teve origem.

Em comparação com toohello antigo tradicional forma, onde as páginas de modelo pertencem pela solução de olá onde fornecido limitado de texto e imagens, onde o controlo limitado de esquema e a funcionalidade foi disponibilizado toomore líder de mercado que dificuldades tooachieve uma experiência totalmente integrada, Olá CORS forma suporta HTML5 e CSS e permite-lhe:

- Alojar conteúdo Olá e hello solução injects os controlos com o script do lado do cliente.
- Ter controlo total sobre cada pixel de esquema e a funcionalidade.

Pode fornecer tantos páginas conteúdas como pretender através de composição ficheiros HTML5/CSS, conforme apropriado.

> [!NOTE]
> Por motivos de segurança, a utilização de Olá de JavaScript está atualmente bloqueada para personalização. é necessário toounblock JavaScript, utilização de um nome de domínio personalizado para o seu inquilino do Azure AD B2C.

Cada um dos seus modelos HTML5/CSS, deve fornecer um *âncora* elemento, que corresponde toohello necessário `<div id=”api”>` elemento Olá HTML ou Olá página conteúdo como ilustrar hereafter. O Azure AD B2C requer que todas as páginas de conteúdo têm este div. específico

```
<!DOCTYPE html>
<html>
  <head>
    <title>Your page content’s tile!</title>
  </head>
  <body>
    <div id="api"></div>
  </body>
</html>
```

Conteúdo relacionado com AD B2C do Azure para a página Olá irá ser injetada neste div, ao resto Olá página Olá é mesmo seu toocontrol. no código JavaScript Olá, Azure AD B2C solicita o conteúdo e injects nosso HTML para este elemento div específico. O Azure AD B2C injects Olá seguintes controlos conforme adequado: atributo coleção controlos, controlos (atualmente baseado em telefone) do multi-factor, controlos de início de sessão e controlo de selecionador de conta. O Azure AD B2C garante que todos os controlos de Olá HTML5 acessível e não compatíveis, todos os controlos de Olá podem ser totalmente estilizados da seguinte e, se uma versão de controlo não será regress.

Olá conteúdo intercalado é, eventualmente, apresentado como consumidor de tooyour Olá documento dinâmico.

tooensure de Olá acima funciona conforme esperado, tem de:

- Certifique-se de que o conteúdo é HTML5 acessível e não compatíveis
- Certifique-se de que o servidor de conteúdo está ativado para CORS.
- Servir conteúdo através de HTTPS.
- Utilize URLS absolutos como https://yourdomain/content para todas as ligações e conteúdo do CSS.

> [!TIP]
> tooverify Olá estão a alojar o conteúdo do site tem CORS ativada e pedidos CORS de teste, pode utilizar Olá site http://test-cors.org/. Site de toothis obrigado, pode simplesmente enviar Olá CORS pedido tooa servidor remoto (tootest se for suportada CORS), ou enviar o servidor de teste do Olá CORS pedido tooa (tooexplore determinadas funcionalidades de CORS).

> [!TIP]
> Olá site http://enable-cors.org/ também constitui um mais do que recursos úteis no CORS.

Thanks toothis abordagem baseada em CORS, os utilizadores finais de Olá terá experiências consistentes entre a sua aplicação e páginas de Olá servidas pelo Azure AD B2C.

## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento

Como pré-requisito, tem de toocreate uma conta de armazenamento. Precisa de uma subscrição do Azure de toocreate uma conta do Blob Storage do Azure. Pode inscrever numa avaliação gratuita em Olá [Web site Azure](https://azure.microsoft.com/en-us/pricing/free-trial/).

1. Abra uma sessão de navegação e navegue toohello [portal do Azure](https://portal.azure.com).
2. Inicie sessão com as suas credenciais administrativas.
3. Clique em **novo** > **dados + armazenamento** > **conta de armazenamento**.  A **criar conta de armazenamento** painel abre-se.
4. No **nome**, forneça um nome para a conta de armazenamento Olá, por exemplo, *contoso369b2c*. Este valor será mais tarde referido como demasiado*storageAccountName*.
5. Escolha as seleções adequadas Olá para Olá subscrição Olá, grupo de recursos de Olá e escalão de preço. Certifique-se de que tem Olá **Pin tooStartboard** opção selecionada. Clique em **Criar**.
6. Volte toohello Startboard e clique em conta de armazenamento de Olá que acabou de criar.
7. No Olá **serviços** secção, clique em **Blobs**. A **painel de serviço Blob** abre-se.
8. Clique em **+ contentor**.
9. No **nome**, forneça um nome para o contentor de Olá, por exemplo, *b2c*. Este valor será repetida mais tarde tooas referenciado *containerName*.
9. Selecione **Blob** como Olá **aceder tipo**. Clique em **Criar**.
10. contentor de Olá que criou irão aparecer na lista de Olá no Olá **painel de serviço Blob**.
11. Fechar Olá **Blobs** painel.
12. No Olá **painel de conta de armazenamento**, clique em Olá **chave** ícone. Um **painel chaves de acesso** abre-se.  
13. Anote o valor Olá **chave1**. Este valor será mais tarde referido como *chave1*.

## <a name="downloading-hello-helper-tool"></a>Transferir a ferramenta auxiliar de Olá

1.  Transferir a ferramenta de programa auxiliar de Olá do [GitHub](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip).
2.  Guardar Olá *B2C AzureBlobStorage-cliente master.zip* ficheiro no seu computador local.
3.  Extrair conteúdo de Olá do ficheiro de Olá B2C AzureBlobStorage-cliente master.zip no disco local, por exemplo em Olá **pacote de personalização de IU** pasta. Esta ação irá criar um *B2C-AzureBlobStorage-cliente-master* pasta por baixo.
4.  Abra a pasta e extrair conteúdo de Olá do ficheiro de arquivo de Olá *B2CAzureStorageClient.zip* dentro da mesma.

## <a name="upload-hello-ui-customization-pack-sample-files"></a>Carregar ficheiros de exemplo de pacote de personalização de IU Olá

1.  Através do Explorador do Windows, navegue até toohello pasta *B2C-AzureBlobStorage-cliente-master* localizado Olá *pacote de personalização de IU* pasta que criou na secção anterior Olá.
2.  Executar Olá *B2CAzureStorageClient.exe* ficheiro. Este programa simplesmente irá carregar todos os ficheiros de Olá no diretório de Olá especificar conta de armazenamento tooyour e ativar o acesso CORS para esses ficheiros.
3.  Quando lhe for pedido, especifique: um.  nome de Olá da sua conta de armazenamento, *storageAccountName*, por exemplo *contoso369b2c*.
    b.  chave de acesso primária de Olá do seu armazenamento de Blobs do azure, *chave1*, por exemplo *contoso369b2c*.
    c.  nome de Olá do contentor de armazenamento de BLOBs de armazenamento, *containerName*, por exemplo *b2c*.
    d.  caminho de Olá de Olá *Starter pacote* exemplo ficheiros, por exemplo *... \B2CTemplates\wingtiptoys*.

Se seguiu os passos de Olá acima, Olá HTML5 e CSS ficheiros de Olá *pacote de personalização de IU* para a empresa fictícia Olá **wingtiptoys** irá agora ser apontar tooyour conta de armazenamento.  Pode verificar que foi carregado conteúdo Olá corretamente ao abrir o painel de contentor relacionados Olá no Olá portal do Azure. Em alternativa pode verificar que o conteúdo de Olá terem sido carregado corretamente acedendo à página Olá num browser. Para obter mais informações, consulte [Azure Active Directory B2C: uma ferramenta de programa auxiliar utilizado a funcionalidade de personalização de interface (IU) de utilizador página Olá toodemonstrate](active-directory-b2c-reference-ui-customization-helper-tool.md).

## <a name="ensure-hello-storage-account-has-cors-enabled"></a>Certifique-se conta de armazenamento Olá tem CORS ativada

CORS (transversal à partilha de recursos) tem de ser ativado no seu ponto final para tooload Premium do Azure AD B2C, o conteúdo. Isto acontece porque o conteúdo estiver alojado num domínio diferente que o domínio de Olá Premium do Azure AD B2C será que serve página Olá do.

tooverify armazenamento Olá estão a alojar o seu conteúdo com a CORS ativada, pode continuar com a Olá os seguintes passos:

1. Abra uma sessão de navegação e navegue até a página de toohello *unified.html* utilizando Olá URL completo da respetiva localização na sua conta de armazenamento, `https://<storageAccountName>.blob.core.windows.net/<containerName>/unified.html`. Por exemplo, https://contoso369b2c.blob.core.windows.net/b2c/unified.html.
2. Navegue toohttp://test-cors.org. Este site permite-lhe tooverify que Olá página que está a utilizar tem CORS ativada.  
<!--
![test-cors.org](../../media/active-directory-b2c-customize-ui-of-a-user-journey/test-cors.png)
-->

3. No **URL remoto**, introduza o URL completo Olá para o conteúdo do unified.html e, em **enviar pedido**.
4. Certifique-se de que saída Olá no Olá **resultados** secção contém *Estado XHR: 200*. Isto indica que a CORS está ativada.
<!--
![CORS enabled](../../media/active-directory-b2c-customize-ui-of-a-user-journey/cors-enabled.png)
-->
conta de armazenamento Olá agora deve conter um contentor do blob denominado *b2c* na nossa ilustração que contém Olá seguintes wingtiptoys modelos de Olá *Starter pacote*.

<!--
![Correctly configured storage account](../../articles/active-directory-b2c/media/active-directory-b2c-reference-customize-ui-custom/storage-account-final.png)
-->

Olá tabela seguinte descreve objetivo Olá Olá acima páginas HTML5.

| Modelo de HTML5 | Descrição |
|----------------|-------------|
| *phonefactor.HTML* | Nesta página pode ser utilizada como um modelo para uma página de autenticação multifator. |
| *ResetPassword.HTML* | Nesta página pode ser utilizada como um modelo para um esqueceu a página de palavra-passe. |
| *selfasserted.HTML* | Nesta página pode ser utilizada como um modelo para uma página de inscrição de conta de redes sociais, uma página de inscrição de conta local ou uma página de início de sessão da conta local. |
| *Unified.HTML* | Nesta página pode ser utilizada como um modelo para uma página de inscrição ou início de sessão unificada. |
| *updateprofile.HTML* | Nesta página pode ser utilizada como um modelo para uma página de atualização de perfil. |

## <a name="add-a-link-tooyour-html5css-templates-tooyour-user-journey"></a>Adicionar um journey de utilizador do ligação tooyour HTML5/CSS modelos tooyour

Pode adicionar um journey de utilizador do ligação tooyour HTML5/CSS modelos tooyour editando diretamente uma política personalizada.

Olá personalizado HTML5/CSS modelos toouse da sua viagem de utilizador tem toobe especificado numa lista de definições de conteúdo que podem ser utilizados nos percursos de utilizador. Para essa finalidade, opcional  *<ContentDefinitions>*  elemento XML tem de ser declarado em Olá  *<BuildingBlocks>*  secção Compilation do ficheiro XML de política personalizada.

Olá tabela seguinte descreve Olá conjunto de ids de definição de conteúdo reconhecido pelo motor de experiência de identidade Olá, Azure AD B2C e o tipo de Olá das páginas que está relacionada com toothem.

| Id de definição de conteúdo | Descrição |
|-----------------------|-------------|
| *API.Error* | **Página de erro**. Esta página é apresentada quando é encontrado uma excepção ou um erro. |
| *API.idpselections* | **Página de seleção de fornecedor de identidade**. Esta página contém uma lista de fornecedores Olá utilizador podem escolher durante o início de sessão de identidade. Estes são o fornecedores de identidade empresarial, os fornecedores de identidade de redes sociais como o Facebook e Google + ou contas locais (com base no nome de utilizador ou endereço de e-mail). |
| *API.idpselections.Signup* | **Seleção de fornecedor de identidade para inscrição**. Esta página contém uma lista de fornecedores Olá utilizador podem escolher durante a inscrição de identidade. Estes são o fornecedores de identidade empresarial, os fornecedores de identidade de redes sociais como o Facebook e Google + ou contas locais (com base no nome de utilizador ou endereço de e-mail). |
| *API.localaccountpasswordreset* | **Se esqueceu a página de palavra-passe**. Esta página contém um formulário que o utilizador Olá tem tooinitiate toofill repor a palavra-passe.  |
| *API.localaccountsignin* | **Página de início de sessão da conta local**. Esta página contém um formulário de início de sessão desse utilizador Olá tem toofill no quando iniciar sessão com uma conta local, com base no endereço de e-mail ou um nome de utilizador. formulário de Olá pode conter uma caixa de entrada de texto e a caixa de entrada de palavra-passe. |
| *API.localaccountsignup* | **Página de inscrição de conta local**. Esta página contém um formulário de inscrição que o utilizador Olá tem toofill no quando inscrever-se de uma conta local é baseada num endereço de e-mail ou um nome de utilizador. formulário de Olá pode conter controlos de entrada diferentes, tais como a caixa de entrada de texto, caixa de entrada de palavra-passe, botão de opção, as caixas de lista pendente de selecção única e selecionar vários caixas de verificação. |
| *API.phonefactor* | **Página de autenticação multifator**. Nesta página, os utilizadores podem verificar os respetivos números de telefone (utilizando o Editor de texto ou de voz) durante a inscrição ou início de sessão. |
| *API.selfasserted* | **Página de inscrição de redes sociais conta**. Esta página contém um formulário de inscrição que o utilizador Olá tem toofill no quando inscrever-se utilizar um existente conta de um fornecedor de identidade de redes sociais, como o Facebook ou Google +. Esta página é semelhante toohello acima página de inscrição de redes sociais conta com a exceção de Olá dos campos de entrada de palavra-passe Olá. |
| *API.selfasserted.profileupdate* | **Página de atualização de perfil**. Esta página contém um formulário que o utilizador Olá pode utilizar tooupdate respetivo perfil. Esta página é semelhante toohello acima página de inscrição de redes sociais conta com a exceção de Olá dos campos de entrada de palavra-passe Olá. |
| *API.signuporsignin* | **Página de inscrição ou início de sessão unificada**.  Esta página processa tanto inscrição & início de sessão de utilizadores, que podem utilizar fornecedores de identidade empresarial, fornecedores de identidade de redes sociais, como o Facebook Google + ou para contas locais.

## <a name="next-steps"></a>Passos seguintes
[Referência: Compreender as políticas personalizadas como trabalhar com Olá Framework de experiência de identidade no B2C](active-directory-b2c-reference-custom-policies-understanding-contents.md)
