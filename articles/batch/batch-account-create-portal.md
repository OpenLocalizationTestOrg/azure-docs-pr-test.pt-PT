---
title: "aaaCreate uma conta do Batch no portal do Azure de Olá | Microsoft Docs"
description: "Saiba como toocreate um Azure Batch conta no Olá toorun portal do Azure, cargas de trabalho paralelas em grande escala na nuvem de Olá"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2176f88ba0a1a3298023de8f520d46ef28a664b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-portal"></a>Criar uma conta do Batch com Olá portal do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](batch-account-create-portal.md)
> * [Gestão de Batch .NET](batch-management-dotnet.md)
>
>

Saiba como toocreate um Azure Batch conta no Olá [portal do Azure][azure_portal]e escolha as propriedades da conta de Olá que se adeque ao seu cenário de computação. Saiba onde toofind propriedades da conta de importante que as chaves de acesso e os URLs de conta.

Para fundo sobre cenários e de contas do Batch, consulte Olá [descrição geral da funcionalidade](batch-api-basics.md).



## <a name="create-a-batch-account"></a>Criar uma conta do Batch

Utilize um dos Olá dois Olá portal toocreate uma conta do Batch *modos de alocação de conjunto*: **serviço Batch** modo ou Olá mais recente **subscrição de utilizador** modo, o que requer mais configuração. Para obter informações sobre estes dois modos, consulte Olá [descrição geral da funcionalidade](batch-api-basics.md#account). Para funcionalidades do modo de subscrição de utilizador Olá, consulte também Olá [blogue](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).

## <a name="batch-service-mode"></a>Modo de serviço do Batch



1. Inicie sessão no toohello [portal do Azure][azure_portal].
2. Clique em **Novo** > **Computação** > **Serviço Batch**.

    ![Batch no Olá Marketplace][marketplace_portal]
3. Olá **nova conta do Batch** é apresentado o painel. Consulte as descrições de Olá abaixo de cada elemento do painel.

    ![Criar uma conta do Batch][account_portal]

    a. **Nome da conta**: nome da conta de Batch de Olá que escolher tem de ser exclusivo num Olá região do Azure onde será criada a conta de Olá (consulte **localização** abaixo). o nome de conta Olá pode conter apenas carateres em minúsculas ou números e tem de ser 3 e 24 carateres de comprimento.

    b. **Subscrição**: Olá subscrição na qual Olá toocreate conta do Batch. Se tiver apenas uma subscrição, está selecionada por predefinição.

    c. **Modo de alocação do conjunto**: selecione **serviço do Batch**.

    c. **Grupo de recursos**: selecione um grupo de recursos existente para a sua nova conta do Batch ou, opcionalmente, para criar um novo.

    d. **Localização**: Olá região do Azure na qual Olá toocreate conta do Batch. Apenas as regiões Olá suportadas pela sua subscrição e o grupo de recursos são apresentadas como opções.

    e. **Conta de armazenamento** (opcional): uma conta de Armazenamento do Azure para fins gerais que associa à conta do Batch. Esta opção é recomendada para a maioria das contas do Batch. Veja [Linked Azure Storage account (Conta do Armazenamento do Azure Ligada)](#linked-azure-storage-account) mais tarde neste artigo para obter mais informações.

4. Clique em **criar** conta de Olá toocreate.

   portal de Olá indica a implementação está em curso. Após a conclusão, aparece a notificação **Implementações concluídas com êxito** em **Notificações**.

## <a name="user-subscription-mode"></a>Modo de subscrição do utilizador

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a>Permitir que o Azure Batch tooaccess subscrição Olá (operação única)
Ao criar a sua conta do Batch primeiro no modo de subscrição de utilizador, efetue Olá tooregister passos a seguir a sua subscrição com o Batch. (Se fez anteriormente isto, ignorar a secção seguinte toohello.)

1. Inicie sessão no toohello [portal do Azure][azure_portal].

2. Clique em **mais serviços** > **subscrições**e clique em subscrição Olá pretende toouse para Olá conta do Batch.

3. No Olá **subscrição** painel, clique em **(IAM) do controlo de acesso** > **adicionar**.

    ![Controlo de acesso da subscrição][subscription_access]

4. No Olá **adicionar permissões** painel, selecione de Olá **contribuinte** função, procure Olá API do Batch. Pesquisa para cada um destas cadeias até encontrar Olá API:
    1. **MicrosoftAzureBatch**.
    2. **Batch do Microsoft Azure**. Os inquilinos mais recentes podem utilizar este nome.
    3. **ddbf3205-c6bd-46ae-8127-60eb93363864** Olá ID para Olá API do Batch. 

5. Depois de encontrar Olá API do Batch, selecione-o e clique em **guardar**.

    ![Adicionar permissões do Batch][add_permission]

### <a name="create-a-key-vault"></a>Criar um cofre de chaves
No modo de subscrição de utilizador, é necessário um cofre de chaves do Azure que pertence toothe mesmo grupo de recursos como toobe de conta de Batch de Olá criado. Certifique-se de grupo de recursos de Olá numa região onde está o Batch [disponíveis](https://azure.microsoft.com/regions/services/) e que suporta a sua subscrição.

1. No Olá [portal do Azure][azure_portal], clique em **novo** > **segurança + identidade** > **Cofre de chaves** .

2. No Olá **criar Cofre de chaves** painel, introduza um nome para o Cofre de chaves Olá e criar um grupo de recursos na região de Olá que pretende para a sua conta do Batch. Deixe Olá restantes definições em valores predefinidos, em seguida, clique em **criar**.

### <a name="create-a-batch-account"></a>Criar uma conta do Batch

1. No Olá [portal do Azure][azure_portal], clique em **novo** > **computação** > **deserviçodeBatch**.

    ![Batch no Olá Marketplace][marketplace_portal]
3. Olá **nova conta do Batch** é apresentado o painel. Consulte as descrições de Olá abaixo de cada elemento do painel.

    ![Criar uma conta do Batch][account_portal_byos]

    a. **Nome da conta**: nome da conta de Batch de Olá que escolher tem de ser exclusivo num Olá região do Azure onde será criada a conta de Olá (consulte **localização** abaixo). o nome de conta Olá pode conter apenas carateres em minúsculas ou números e tem de ser 3 e 24 carateres de comprimento.

    b. **Subscrição**: Se tiver mais do que uma subscrição, selecione a subscrição de Olá que registado Olá serviço Batch.

    c. **Modo de alocação do conjunto**: selecione **Subscrição do utilizador**.

    d. **Cofre da chave**: o Cofre de chaves Olá selecione que criou para a sua conta do Batch na secção anterior Olá. Opcionalmente, crie um novo cofre de chaves. Depois de selecionar o Cofre de Olá, selecione Olá caixa de verificação toogrant do Azure Batch acesso toohello Cofre de chave.

    c. **Grupo de recursos**: grupo de recursos de Olá selecione onde criou o Cofre de chaves Olá.

    d. **Localização**: Olá região do Azure onde criou o Cofre de chaves Olá Olá conta de Batch.

    e. **Conta de armazenamento** (opcional): uma conta de Armazenamento do Azure para fins gerais que associa à conta do Batch. Esta opção é recomendada para a maioria das contas do Batch. Veja [Conta do Armazenamento do Azure Ligada](#linked-azure-storage-account), abaixo, para obter mais informações.

4. Clique em **criar** conta de Olá toocreate.

   portal de Olá indica a implementação está em curso. Após a conclusão, aparece a notificação **Implementações concluídas com êxito** em **Notificações**.



## <a name="view-batch-account-properties"></a>Ver propriedades da conta do Batch
Quando tiver sido criada a conta de Olá, pode abrir Olá **painel de conta do Batch** tooaccess respetivas propriedades e definições. Pode aceder a todas as definições de conta e as propriedades utilizando o menu à esquerda do Olá do painel de conta de Batch de Olá.

![Painel Conta do Batch no portal do Azure][account_blade]

* **O URL da conta do batch**: quando desenvolver uma aplicação com Olá [APIs do Batch](batch-apis-tools.md#azure-accounts-for-batch-development), terá uma tooaccess de URL da conta os recursos do Batch. Um URL de conta do Batch tem Olá seguinte formato:

    `https://<account_name>.<region>.batch.azure.com`

![URL da conta do Batch no portal][account_url]

* **Chaves de acesso** (modo de serviço do Batch): tooauthenticate acesso tooyour conta do Batch da sua aplicação, terá de uma chave de acesso da conta. (Esta definição não está disponível no modo de subscrição de utilizador, onde utiliza a autenticação do Azure Active Directory.)

    tooview ou voltar a gerar chaves de acesso da sua conta do Batch, introduza `keys` no menu à esquerda Olá **pesquisa** caixa no painel de conta de Batch de Olá, em seguida, selecione **chaves**.

    ![Chaves da conta do Batch no portal do Azure][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a>Conta do Armazenamento do Azure Ligada

Opcionalmente, pode ligar um tooyour de conta de armazenamento do Azure conta do Batch para fins gerais. Olá [pacotes de aplicações](batch-application-packages.md) funcionalidade do Batch utiliza o Blob storage do Azure, como sucede Olá [.NET do Batch ficheiro convenções](batch-task-output.md) biblioteca. Estas funcionalidades opcionais ajudá-lo a implementar Olá com as suas tarefas Batch, dados e aplicações persistentes Olá produzem.

Recomendamos que crie uma nova conta de Armazenamento para utilização exclusiva por parte da sua conta do Batch.

![Criar uma conta de armazenamento para fins gerais][storage_account]

> [!NOTE]
> O Azure Batch atualmente suporta apenas Olá para fins gerais armazenamento tipo de conta. Este tipo de conta é descrito no passo 5, [Criar uma conta de armazenamento] (../storage/common/storage-create-storage-account.md#create-a-storage-account), em [Sobre as contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md).
>
>

> [!WARNING]
> Tenha cuidado quando regenerar chaves de acesso de Olá de uma conta de armazenamento ligada. Voltar a gerar apenas uma chave de conta do Storage e clique em **sincronizar chaves** no Olá ligado painel de conta de armazenamento. Aguardar cinco minutos tooallow Olá chaves toopropagate toohello nós de computação em seus conjuntos e, em seguida, voltar a gerar e sincronizar Olá outra chave se for necessário. Se voltar a gerar ambas as chaves em Olá mesmo tempo, os nós de computação não será capaz de toosynchronize nenhuma das chaves e estas perdem o acesso toohello armazenamento conta.
>
>

![Regenerar chaves de conta de armazenamento][4]

## <a name="batch-service-quotas-and-limits"></a>Quotas e limites do serviço Batch
Tenha ser que como com a sua subscrição do Azure e outro Azure serviços, a determinados [quotas e limites](batch-quota-limit.md) aplicar tooBatch contas. As quotas atuais numa conta de Batch de aparecer no portal de Olá na conta de Olá **propriedades**.

![Quotas das contas do Batch no portal do Azure][quotas]



Além disso, muitas destas quotas podem ser aumentadas simplesmente com um pedido de suporte de produto livre submetido na Olá portal do Azure. Consulte [Quotas e limites para Olá serviço Azure Batch](batch-quota-limit.md) para obter detalhes sobre a quota aumenta a pedir.

## <a name="other-batch-account-management-options"></a>Outras opções de gestão de contas do Batch
Além disso toousing Olá portal do Azure, também pode criar e gerir contas do Batch com seguinte Olá:

* [Cmdlets do PowerShell do Batch](batch-powershell-cmdlets-get-started.md)
* [CLI do Azure](batch-cli-get-started.md)
* [Gestão de Batch .NET](batch-management-dotnet.md)

## <a name="next-steps"></a>Passos seguintes
* Consulte Olá [descrição geral da funcionalidade do Batch](batch-api-basics.md) toolearn mais sobre as funcionalidades e conceitos do serviço Batch. Olá artigo aborda Olá recursos do Batch principais como conjuntos, nós de computação, trabalhos e tarefas e fornece uma descrição geral de Olá funcionalidades do serviço que permitem a execução de cargas de trabalho de computação em grande escala.
* Saiba Olá Noções básicas sobre desenvolver uma aplicação preparada para Batch utilizando Olá [biblioteca de cliente .NET do Batch](batch-dotnet-get-started.md) ou [Python](batch-python-tutorial.md). Estes artigos introdutórias ajudá-lo através de uma aplicação de trabalho que utiliza Olá Batch serviço tooexecute uma carga de trabalho em vários nós de computação e inclui a utilização do armazenamento do Azure para teste de ficheiros da carga de trabalho e obtenção.

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: ./media/batch-account-create-portal/batch_acct_04.png "Regenerar chaves de conta de armazenamento"
[marketplace_portal]: ./media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: ./media/batch-account-create-portal/account_keys.PNG
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[quotas]: ./media/batch-account-create-portal/quotas.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[account_portal_byos]: ./media/batch-account-create-portal/batch_acct_portal_byos.png
