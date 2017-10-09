---
title: "aaaCreate identidade da aplicação do Azure no portal | Microsoft Docs"
description: "Descreve como toocreate uma nova aplicação do Azure Active Directory e que podem ser utilizados com controlo de acesso baseado em funções de Olá no Azure Resource Manager toomanage principal de serviço tooresources de acesso."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a>Utilizar o portal toocreate uma aplicação do Azure Active Directory e o principal de serviço que pode aceder a recursos

Quando tiver uma aplicação que necessita de tooaccess ou modificar recursos, tem de configurar uma aplicação do Azure Active Directory (AD) e atribuir tooit de permissões de Olá necessário. Esta abordagem é preferível toorunning Olá aplicação com as suas próprias credenciais porque:

* Pode atribuir permissões de identidade de aplicação toohello diferentes a suas própria permissões. Normalmente, estas permissões são tooexactly restrito tem de aplicação que Olá toodo.
* Não dispõe de credenciais da aplicação Olá toochange se alterar as suas responsabilidades. 
* Pode utilizar uma autenticação de certificados de tooautomate ao executar um script automático.

Este tópico mostra como tooperform os passos através do portal de Olá. Concentra-se uma aplicação do inquilino único em que a aplicação Olá é toorun pretendido dentro da organização apenas um. Normalmente utiliza aplicações de inquilino único para aplicações de linha de negócio que são executadas dentro da sua organização.
 
## <a name="required-permissions"></a>Permissões necessárias
toocomplete neste tópico, tem de ter uma aplicação de tooregister de permissões suficientes com o seu inquilino do Azure AD e atribuir a função de tooa Olá aplicações na sua subscrição do Azure. Vamos certificar-se de que ter Olá permissões corretas tooperform esses passos.

### <a name="check-azure-active-directory-permissions"></a>Verifique as permissões do Azure Active Directory
1. Inicie sessão no tooyour conta do Azure através de Olá [portal do Azure](https://portal.azure.com).
2. Selecione **do Azure Active Directory**.

     ![Selecione do azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. No Azure Active Directory, selecione **as definições de utilizador**.

     ![Selecione as definições de utilizador](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. Verifique Olá **registos de aplicação** definição. Se definido demasiado**Sim**, os utilizadores que não podem registar aplicações AD. Esta definição significa que qualquer utilizador no inquilino do Azure AD Olá pode registar uma aplicação. Para poder continuar demasiado[permissões de subscrição do Azure verifique](#check-azure-subscription-permissions).

     ![registos de aplicação de vista](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. Se os registos de aplicação Olá definição estiver definido demasiado**não**, apenas os utilizadores administradores podem registar aplicações. É necessário toocheck se a sua conta é um administrador inquilino do Azure AD Olá. Selecione **descrição geral** e **localizar um utilizador** de tarefas rápidas.

     ![Localizar utilizador](./media/resource-group-create-service-principal-portal/find-user.png)
6. Pesquisa para a sua conta e selecioná-lo quando a encontrá-lo.

     ![utilizador de pesquisa](./media/resource-group-create-service-principal-portal/show-user.png)
7. Para a sua conta, selecione **função de diretório**. 

     ![função de diretório](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. Ver a sua função de diretório atribuído no Azure AD. Se a conta está atribuída a função de utilizador toohello, mas hello registo definição de aplicação (Olá precedente passos) é limitado tooadmin utilizadores, peça ao seu administrador tooeither atribuir tooan função de administrador ou tooenable utilizadores tooregister aplicações.

     ![função de vista](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a>Verifique as permissões de subscrição do Azure
Na sua subscrição do Azure, a conta tem de ter `Microsoft.Authorization/*/Write` tooassign uma função do AD aplicação tooa de acesso. Esta ação é concedida através de Olá [proprietário](../active-directory/role-based-access-built-in-roles.md#owner) função ou [administrador de acesso de utilizador](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) função. Se a sua conta está atribuída toohello **contribuinte** função, não tem permissão suficiente. Receberá um erro durante a tentativa de função de principal tooa de serviço de Olá tooassign. 

toocheck as permissões de subscrição:

1. Se não já pretender na sua conta do Azure AD de Olá precedente passos, selecione **do Azure Active Directory** a partir do painel esquerdo Olá.

2. Localize a conta do Azure AD. Selecione **descrição geral** e **localizar um utilizador** de tarefas rápidas.

     ![Localizar utilizador](./media/resource-group-create-service-principal-portal/find-user.png)
2. Pesquisa para a sua conta e selecioná-lo quando a encontrá-lo.

     ![utilizador de pesquisa](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. Selecione **recursos do Azure**.

     ![Selecione recursos](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. Ver as funções atribuídas e determinar se tem permissões adequadas tooassign uma função do AD aplicação tooa. Se não, peça ao seu tooadd de administrador de subscrição tooUser acesso função de administrador. Olá seguinte imagem, utilizador de Olá é atribuído toohello função de proprietário para duas subscrições, que significa que o utilizador tem permissões adequadas. 

     ![Mostrar permissões](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a>Criar uma aplicação do Azure Active Directory
1. Inicie sessão no tooyour conta do Azure através de Olá [portal do Azure](https://portal.azure.com).
2. Selecione **do Azure Active Directory**.

     ![Selecione do azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. Selecione **registos de aplicação**.   

     ![Selecione os registos de aplicação](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. Selecione **Adicionar**.

     ![Adicionar aplicação](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. Forneça um nome e o URL para a aplicação Olá. Selecione **aplicação Web / API** ou **nativo** para o tipo de Olá da aplicação que pretende toocreate. Depois de definir valores de Olá, selecione **criar**.

     ![aplicação de nome](./media/resource-group-create-service-principal-portal/create-app.png)

Foi criada com a aplicação.

## <a name="get-application-id-and-authentication-key"></a>Obter a chave de autenticação e ID de aplicação
Quando programaticamente iniciar sessão, precisa de Olá ID para a sua aplicação e uma chave de autenticação. tooget os valores, Olá utilize os seguintes passos:

1. De **registos de aplicação** no Azure Active Directory, selecione a aplicação.

     ![Selecionar aplicação](./media/resource-group-create-service-principal-portal/select-app.png)
2. Olá cópia **ID da aplicação** e armazená-las no código da aplicação. Olá aplicações no Olá [aplicações de exemplo](#sample-applications) secção Consulte toothis valor como id de cliente Olá.

     ![id de cliente](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. toogenerate uma chave de autenticação, selecione **chaves**.

     ![Selecione as chaves](./media/resource-group-create-service-principal-portal/select-keys.png)
4. Forneça uma descrição da chave de Olá e uma duração para a chave de Olá. Quando terminar, selecione **guardar**.

     ![Guardar chave](./media/resource-group-create-service-principal-portal/save-key.png)

     Depois de guardar a chave de Olá, é apresentado o valor de Olá da chave de Olá. Copie este valor, porque não é capaz de tooretrieve chave de Olá mais tarde. Forneça o valor de chave de Olá com toolog de ID de aplicação Olá na como aplicação Olá. Armazenar o valor de chave olá onde a aplicação pode obtê-lo.

     ![guardar a chave](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a>Obter ID de inquilino
Quando programaticamente iniciar sessão, terá de ID do inquilino toopass Olá com o seu pedido de autenticação. 

1. ID do inquilino Olá tooget, selecione **propriedades** para o seu inquilino do Azure AD. 

     ![selecionar propriedades do Azure AD](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. Olá cópia **ID de diretório**. Este valor é o ID do inquilino.

     ![id do inquilino](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a>Atribuir toorole de aplicação
tooaccess recursos na sua subscrição, tem de atribuir função de tooa Olá aplicações. Decida qual a função representa permissões corretas de Olá para aplicação Olá. toolearn sobre as funções disponíveis Olá, consulte [RBAC: funções incorporadas](../active-directory/role-based-access-built-in-roles.md).

Pode definir o âmbito de Olá ao nível de Olá de subscrição de Olá, grupo de recursos ou recursos. As permissões são herdadas toolower níveis de âmbito. Por exemplo, a adição de que uma função de leitor de toohello de aplicação para um grupo de recursos, significa pode ler o grupo de recursos de Olá e quaisquer recursos que nele contidos.

1. Navegue toohello nível do âmbito de que aplicação Olá tooassign desejar. Por exemplo, tooassign Selecione uma função no âmbito de subscrição de Olá, **subscrições**. Em vez disso, pode selecionar um grupo de recursos ou um recurso.

     ![Selecione a subscrição](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. Selecione Olá determinada subscrição (grupo de recursos ou recursos) tooassign Olá aplicação.

     ![Selecione a subscrição de atribuição](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. Selecione **(IAM) do controlo de acesso**.

     ![Selecione o acesso](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. Selecione **Adicionar**.

     ![Selecionar adicionar](./media/resource-group-create-service-principal-portal/select-add.png)
6. Selecione a função de Olá desejar tooassign toohello aplicação. Olá imagem seguinte mostra Olá **leitor** função.

     ![Selecione a função](./media/resource-group-create-service-principal-portal/select-role.png)

8. Procure a aplicação e selecione-o.

     ![Procure a aplicação](./media/resource-group-create-service-principal-portal/search-app.png)
9. Selecione **OK** toofinish atribuir função Olá. Verá a aplicação na lista de Olá de utilizadores atribuídos tooa função para esse âmbito.

## <a name="log-in-as-hello-application"></a>Inicie sessão como uma aplicação Olá

A aplicação está agora definida no Azure Active Directory. Tem um ID e a chave toouse para iniciar sessão como aplicação Olá. aplicação Olá é atribuída a função de tooa que concede-lhe determinadas ações que pode realizar. Para informações sobre como iniciar sessão como uma aplicação Olá através de plataformas diferentes, consulte:

* [PowerShell](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [CLI do Azure](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [REST](/rest/api/#create-the-request)
* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a>Passos seguintes
* tooset se uma aplicação multi-inquilino, consulte [tooauthorization do Guia do programador com Olá API do Azure Resource Manager](resource-manager-api-authentication.md).
* toolearn sobre como especificar políticas de segurança, consulte [controlo de acesso baseado em funções do Azure](../active-directory/role-based-access-control-configure.md).  
* Para obter uma lista de ações disponíveis que pode ser concedeu ou negou toousers, consulte [operações de fornecedor de recursos do Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).
