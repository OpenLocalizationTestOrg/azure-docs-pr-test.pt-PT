---
title: "Do Azure Active Directory B2C: Ferramenta de programa auxiliar de personalização de página IU | Microsoft Docs"
description: "Uma ferramenta de programa auxiliar utilizadas funcionalidade da personalização toodemonstrate Olá página IU no Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: ae935d52-3520-4a94-b66e-b35bb40e7514
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: swkrish
ms.openlocfilehash: 5137ac112019369b4244a925df1acb96fefb758f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-a-helper-tool-used-toodemonstrate-hello-page-user-interface-ui-customization-feature"></a>O Azure Active Directory B2C: Uma ferramenta de programa auxiliar utilizadas funcionalidade de personalização de interface (IU) de utilizador página Olá toodemonstrate
Este artigo é um complemento toohello [principal artigo de personalização de IU](active-directory-b2c-reference-ui-customization.md) no Azure Active Directory (Azure AD) B2C. Olá passos seguintes descrevem como tooexercise Olá funcionalidade da página IU personalização utilizando o conteúdo HTML e CSS de exemplo que fornecemos.

## <a name="get-an-azure-ad-b2c-tenant"></a>Obter um inquilino do Azure AD B2C
Antes de pode personalizar qualquer coisa, é necessário demasiado[obter um inquilino do Azure AD B2C](active-directory-b2c-get-started.md) se ainda não tiver um.

## <a name="create-a-sign-up-or-sign-in-policy"></a>Criar uma política de inscrição ou início de sessão
Olá conteúdo de exemplo que fornecemos pode ser utilizados toocustomze duas páginas de uma [política de inscrição ou início de sessão](active-directory-b2c-reference-policies.md): Olá [unificada página de início de sessão](active-directory-b2c-reference-ui-customization.md) e Olá [automática permitidos atributos página](active-directory-b2c-reference-ui-customization.md). Quando [criar a política de inscrição ou início de sessão](active-directory-b2c-reference-policies.md#create-a-sign-up-or-sign-in-policy), adicione a conta Local (endereço de e-mail), Facebook, Google e Microsoft como **fornecedores de identidade**. Estes são Olá apenas IDPs aceitará nosso conteúdo HTML de exemplo.  Também pode adicionar um subconjunto destas IDPs se desejar.

## <a name="register-an-application"></a>Registar uma aplicação
Terá de demasiado[registar uma aplicação](active-directory-b2c-app-registration.md) no seu B2C inquilino que pode ser utilizado tooexecute a política. Depois de registar a sua aplicação, tem algumas opções que pode utilizar tooactually executar a política de inscrição:

* Criar uma das aplicações de início rápido listadas na secção Olá "Introdução" Olá do Azure AD B2C [inscrever-se e iniciar sessão em consumidores nas suas aplicações](active-directory-b2c-overview.md#get-started).
* Olá utilize criada previamente [do Azure AD B2C Playground](https://aadb2cplayground.azurewebsites.net) aplicação. Se escolher toouse playground de Olá, tem de registar uma aplicação no seu inquilino do B2C utilizando Olá **URI de redirecionamento** `https://aadb2cplayground.azurewebsites.net/`.
* Olá utilize **executar agora** botão na sua política de Olá [portal do Azure](https://portal.azure.com/).

## <a name="customize-your-policy"></a>Personalizar a política
toocustomize Olá aspeto e funcionalidade da sua política, terá de toofirst criar ficheiros HTML e CSS, utilizando as convenções de específico Olá do Azure AD B2C. Em seguida, pode carregar a localização de publicamente disponíveis tooa conteúdo estático para que o Azure AD B2C consegue aceder-lhe. Isto pode ser o próprio servidor web dedicado, Blob Storage do Azure, rede de entrega de conteúdos do Azure ou quaisquer outra estático que aloja o recurso de fornecedor. Step-by-Olá únicos requisitos são se o seu conteúdo está disponível através de HTTPS e pode ser acedido através de CORS. Assim que tiver exposta o conteúdo estático na web Olá, pode editar a localização de toothis toopoint de política e que os clientes de tooyour de conteúdo. Olá [principal artigo de personalização de IU](active-directory-b2c-reference-ui-customization.md) descreve em detalhe como funciona a funcionalidade de personalização de Olá, Azure AD B2C.

Para efeitos de Olá deste tutorial, iremos tiver já criado algum conteúdo de exemplo e está lojado-lo no Blob Storage do Azure. o conteúdo de exemplo de Olá é uma personalização muito básica no tema Olá da nossa empresa fictícias, "No diretório Wingtip Toys". tootry terminar na sua própria política, siga estes passos:

1. Inicie sessão no inquilino tooyour no Olá [portal do Azure](https://portal.azure.com/) e navegue até o painel de funcionalidades de toohello B2C.
2. Clique em **políticas de inscrição ou início de sessão** e, em seguida, clique em sua política (por exemplo, "b2c\_1\_sessão\_cópias de segurança\_sessão\_no").
3. Clique em **personalização de página IU** e, em seguida, **unificado a página de inscrição ou início de sessão**.
4. Olá alternar **página personalizada utilize** comutador demasiado**Sim**. No Olá **página personalizada URI** campo, introduza `https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/unified.html`. Clique em **OK**.
5. Clique em **página de inscrição de conta Local**. Olá alternar **modelo personalizado utilize** comutador demasiado**Sim**. No Olá **página personalizada URI** campo, introduza `https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/selfasserted.html`.
6. Olá repetida mesmo passo para Olá **página de inscrição de redes sociais conta**.
   Clique em **OK** duas vezes tooclose Olá IU personalização painéis.
7. Clique em **Guardar**.

Agora pode experimentar a política personalizada. Pode utilizar o seus próprios playground de aplicação ou Olá do Azure AD B2C se quiser, mas pode também simplesmente clicar Olá **executar agora** comando no painel de política de Olá. Selecione a aplicação na caixa de lista pendente de Olá e escolha o URI de redirecionamento adequado Olá. Clique em Olá **executar agora** botão. Um novo separador do browser será aberto e pode percorrer a experiência de utilizador de Olá de inscrever-se para a sua aplicação com conteúdo novo Olá local!

## <a name="upload-hello-sample-content-tooazure-blob-storage"></a>Carregar tooAzure conteúdo de exemplo Olá Blob Storage
Se quiser toouse Blob Storage do Azure toohost sua página de conteúdo, pode criar a sua própria conta de armazenamento e utilizar os seus ficheiros nosso tooupload de ferramenta de programa auxiliar do B2C.

### <a name="create-a-storage-account"></a>Criar uma conta de armazenamento
1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).
2. Clique em **+ novo** > **dados + armazenamento** > **conta de armazenamento**. Precisa de uma subscrição do Azure de toocreate uma conta do Blob Storage do Azure. Pode inscrever numa avaliação gratuita em Olá [Web site Azure](https://azure.microsoft.com/pricing/free-trial/).
3. Forneça um **nome** para a conta de armazenamento de Olá (por exemplo, "contoso") e escolha Olá as seleções adequadas para **escalão de preço**, **grupo de recursos** e  **Subscrição**. Certifique-se de que tem Olá **Pin tooStartboard** opção selecionada. Clique em **Criar**.
4. Volte toohello Startboard e clique em conta de armazenamento de Olá que acabou de criar.
5. No Olá **resumo** secção, clique em **contentores**e, em seguida, clique em **+ adicionar**.
6. Forneça um **nome** para o contentor de Olá (por exemplo, "b2c") e selecione **Blob** como Olá **aceder tipo**. Clique em **OK**.
7. contentor de Olá que criou irão aparecer na lista de Olá no Olá **Blobs** painel. Anote o URL de Olá do contentor de Olá; Por exemplo, deve ser semelhante demasiado`https://contoso.blob.core.windows.net/b2c`. Fechar Olá **Blobs** painel.
8. No painel de conta de armazenamento Olá, clique em **chaves** e anote os valores de Olá de Olá **nome da conta de armazenamento** e **chave de acesso primária** campos.

> [!NOTE]
> **Chave de acesso primária** é uma credencial de segurança importantes.
> 
> 

### <a name="download-hello-helper-tool-and-sample-files"></a>Transferir ficheiros de ferramenta e exemplos de programa auxiliar de Olá
Pode transferir Olá [Blob Storage do Azure ajuda ferramenta e exemplos ficheiros como um ficheiro. zip](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip) ou cloná-la a partir do GitHub:

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

Este repositório inclui um `sample_templates\wingtip` diretório, que contém o exemplo HTML, CSS e imagens. Para estes modelos tooreference sua própria conta do Blob Storage do Azure, terá de ficheiros de Olá HTML tooedit. Abra `unified.html` e `selfasserted.html` e substituir quaisquer instâncias de `https://localhost` com Olá URL do seu próprio contentor que escreveu para baixo nos passos anteriores Olá. Tem de utilizar o caminho absoluto do Olá dos Olá HTML ficheiros porque neste caso, Olá HTML será servido pelo Azure AD, em domínio Olá `https://login.microsoftonline.com`.

### <a name="upload-hello-sample-files"></a>Carregar ficheiros de exemplo de Olá
No mesmo repositório de Olá, deszipe `B2CAzureStorageClient.zip` e execução Olá `B2CAzureStorageClient.exe` dentro do ficheiro. Este programa simplesmente irá carregar todos os ficheiros de Olá no diretório de Olá especificar conta de armazenamento tooyour e ativar o acesso CORS para esses ficheiros. Se seguiu os passos de Olá acima, Olá HTML e ficheiros CSS irão agora ser apontar tooyour conta de armazenamento. Tenha em atenção que Olá nome da sua conta de armazenamento faz parte de Olá que precede `blob.core.windows.net`; por exemplo, `contoso`. Pode verificar que o conteúdo de Olá terem sido carregado corretamente tentando tooaccess `https://{storage-account-name}.blob.core.windows.net/{container-name}/wingtip/unified.html` num browser. Também utilizar [http://test-cors.org/](http://test-cors.org/) toomake se de que o conteúdo de Olá agora CORS ativada. (Procure "Estado XHR: 200" no resultado de Olá.)

### <a name="customize-your-policy-again"></a>Personalizar a política novamente
Agora que já carregados conta de armazenamento própria de tooyour conteúdo de exemplo de Olá, tem de editar a política de inscrição tooreference-lo. Repita os passos de Olá de Olá ["Personalizar a política"](#customize-your-policy) secção acima, desta vez utilizando o URL da sua própria conta de armazenamento. Olá, por exemplo, a localização do seu `unified.html` ficheiro seria `<url-of-your-container>/wingtip/unified.html`.

Agora, pode utilizar Olá **executar agora** botão ou a sua própria aplicação tooexecute a política novamente. Olá resultado deve procure quase exatamente hello mesmo – é utilizado Olá mesmo HTML e CSS de exemplo em ambos os casos. No entanto, as políticas estão agora a referenciar a sua própria instância do Blob Storage do Azure e são tooedit livre e carregar ficheiros de Olá novamente como.. Para obter mais informações sobre a personalização hello HTML e CSS, consulte toohello [principal artigo de personalização de IU](active-directory-b2c-reference-ui-customization.md).

