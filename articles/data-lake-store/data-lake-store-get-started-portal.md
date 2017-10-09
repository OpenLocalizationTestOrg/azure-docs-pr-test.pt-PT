---
title: iniciado aaaUse tooget portal do Azure Data Lake Store | Microsoft Docs
description: "Utilizar Olá toocreate do portal do Azure, uma conta de Data Lake Store e executar operações básicas no Olá Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: fea324d0-ad1a-4150-81f0-8682ddb4591c
ms.service: data-lake-store
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/06/2017
ms.author: nitinme
ms.openlocfilehash: 6bb3413f00bfa4393f08aed18bc1d5f8a2f28fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-hello-azure-portal"></a>Introdução ao Azure Data Lake Store utilizando Olá portal do Azure
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [SDK do .NET](data-lake-store-get-started-net-sdk.md)
> * [SDK Java](data-lake-store-get-started-java-sdk.md)
> * [API REST](data-lake-store-get-started-rest-api.md)
> * [CLI 2.0 do Azure](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [python](data-lake-store-get-started-python.md)
>
> 

Saiba como toouse Olá toocreate do portal do Azure, uma conta do Azure Data Lake Store e executar operações básicas, tais como criar pastas, carregar e transferem ficheiros de dados, eliminar a conta, etc. Para obter mais informações, veja [Descrição geral do Azure Data Lake Store](data-lake-store-overview.md).

Olá seguir dois vídeos conter Olá mesma informação, tal como descrito neste artigo:

* [Criar uma conta do Data Lake Store](https://mix.office.com/watch/1k1cycy4l4gen)
* [Gerir dados no Data Lake Store utilizando Olá Explorador de dados](https://mix.office.com/watch/icletrxrh6pc)

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, tem de ter Olá seguintes itens:

* **Uma subscrição do Azure**. Consulte [Obter uma avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-an-azure-data-lake-store-account"></a>Criar uma conta do Azure Data Lake Store

1. Inicie sessão no novo toohello [portal do Azure](https://portal.azure.com).
2. Clique em **NOVO**, **Dados + Armazenamento** e, em seguida, em **Azure Data Lake Store**. Ler informações de Olá na Olá **Azure Data Lake Store** painel e, em seguida, clique em **criar** no canto Olá inferior esquerdo do painel de Olá.
3. No Olá **novo Data Lake Store** painel, forneça valores de Olá, conforme mostrado na seguinte captura de ecrã de Olá:
   
    ![Criar uma nova conta do Azure Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Create.New.Account.png "Criar uma nova conta do Azure Data Lake")
   
   * **Nome**. Introduza um nome exclusivo para Olá conta do Data Lake Store.
   * **Subscrição**. Selecione a subscrição de Olá sob a qual pretende toocreate uma nova conta de Data Lake Store.
   * **Grupo de Recursos**. Selecione um grupo de recursos existente ou selecione Olá **criar nova** toocreate opção um. Um grupo de recursos é um contentor que retém recursos relacionados para uma aplicação. Para obter mais informações, veja [Grupos de Recursos no Azure](../azure-resource-manager/resource-group-overview.md#resource-groups).
   * **Localização**: selecione uma localização onde pretende que a conta de Data Lake Store toocreate Olá.
   * **Definições de Encriptação**. Existem três opções:
     
     * **Não ativar a encriptação**.
     * **Utilizar chaves geridas pelo Azure Data Lake**.  Se pretender que o Azure Data Lake Store toomanage as chaves de encriptação.
     * **Escolha as chaves a partir do Azure Key Vault**. Pode selecionar um Azure Key Vault existente ou criar um novo. chaves de Olá toouse de um cofre de chaves, tem de atribuir permissões para Olá conta do Azure Data Lake Store tooaccess Olá Cofre de chaves do Azure. Para obter instruções de Olá, consulte [atribuir permissões tooAzure Cofre de chaves](#assign-permissions-to-azure-key-vault).
       
        ![Encriptação do Data Lake Store](./media/data-lake-store-get-started-portal/adls-encryption-2.png "Encriptação do Data Lake Store")
       
        Clique em **OK** no Olá **definições de encriptação** painel.

        Para obter mais informações, veja [Encriptação de dados no Azure Data Lake Store](./data-lake-store-encryption.md).

4. Clique em **Criar**. Se tiver escolhido o dashboard de toohello toopin Olá conta, é direcionado novamente toohello dashboard e pode ver o progresso de Olá de aprovisionamento da conta do Data Lake Store. Uma vez Olá conta do Data Lake Store é aprovisionado, o painel de conta Olá aparece.

Também pode criar uma conta do Data Lake Store com modelos do Azure Resource Manager. Estes modelos são acessíveis a partir dos [Modelos de Início Rápido do Azure](https://azure.microsoft.com/resources/templates/?term=data+lake+store):

- Sem encriptação de dados: [Implementar a conta do Azure Data Lake Store sem encriptação de dados](https://azure.microsoft.com/en-us/resources/templates/101-data-lake-store-no-encryption/).
- Com encriptação de dados através do Data Lake Store: [Implementar a conta do Data Lake Store com encriptação (Data Lake)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-adls/).
- Com encriptação de dados através do Azure Key Vault: [Implementar a conta do Data Lake Store com encriptação (Key Vault)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-key-vault/).

### <a name="assign-permissions-to-azure-key-vault"></a>Atribuir permissões tooAzure Cofre de chaves
Se utilizou as chaves de encriptação de tooconfigure um cofre de chaves do Azure no Olá conta do Data Lake Store, tem de configurar o acesso entre contas de Data Lake Store Olá e Olá Cofre de chaves do Azure. Efetue Olá, por isso, os seguintes passos toodo.

1. Se utilizou as chaves de Olá Cofre de chaves do Azure, o painel Olá Olá conta do Data Lake Store apresenta um aviso na parte superior do Olá. Clique em Olá do Olá aviso tooopen **configurar permissões de Cofre de chave** painel.
   
    ![Encriptação do Data Lake Store](./media/data-lake-store-get-started-portal/adls-encryption-3.png "Encriptação do Data Lake Store")
2. Painel de Olá mostra acesso de tooconfigure duas opções.
   
   * Na primeira opção Olá, clique em **conceder permissão** tooconfigure acesso. opção de primeiro Olá está ativada apenas quando o utilizador de Olá que criou a conta de Data Lake Store Olá também é um administrador Olá Cofre de chaves do Azure.
   * Olá outra opção é apresentado no painel de Olá o toorun Olá PowerShell cmdlet. Tem de proprietário Olá toobe Olá Cofre de chaves do Azure ou tem permissões de toogrant de capacidade de Olá Olá Cofre de chaves do Azure. Depois de executar o cmdlet de Olá, volte toohello painel e clique em **ativar** tooconfigure acesso.

## <a name="createfolder"></a>Criar pastas na conta do Azure Data Lake Store
Pode criar pastas na sua toomanage de conta do Data Lake Store e armazenar dados.

1. Abra a conta de Data Lake Store Olá que criou. No painel esquerdo Olá, clique em **procurar**, clique em **Data Lake Store**e, em seguida, no painel do Data Lake Store Olá, clique em nome da conta Olá sob a qual pretende toocreate pastas. Se o tiver afixado Olá conta toohello startboard, clique no mosaico dessa conta.
2. No painel da conta do Data Lake Store, clique em **Explorador de Dados**.
   
    ![Criar pastas numa conta do Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Create.Folder.png "Criar pastas numa conta do Data Lake Store")
3. No painel de conta do Data Lake Store, clique em **nova pasta**, introduza um nome para a nova pasta de Olá e, em seguida, clique em **OK**.
   
    ![Criar pastas numa conta do Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Folder.Name.png "Criar pastas numa conta do Data Lake Store")
   
    pasta de Olá recém-criado está listada no Olá **Explorador de dados** painel. Pode criar pastas aninhadas até qualquer nível.
   
    ![Criar pastas numa conta do Data Lake](./media/data-lake-store-get-started-portal/ADL.New.Directory.png "Criar pastas numa conta do Data Lake")

## <a name="uploaddata"></a>Carregar a conta de Data Lake Store tooAzure de dados
Pode carregar o tooan dados conta do Azure Data Lake Store diretamente no Olá nível ou tooa pasta raiz que criou na conta de Olá. No Olá seguinte captura de ecrã, siga tooupload de passos Olá uma subpasta do ficheiro tooa do Olá **Explorador de dados** painel. Nesta captura de ecrã, ficheiro Olá é subpasta tooa carregado mostrada na navegação estrutural Olá (marcado numa caixa vermelha).

Se estiver à procura de alguns tooupload de dados de exemplo, pode obter Olá **Ambulance Data** pasta a partir de Olá [repositório de Git do Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).

![Carregar dados](./media/data-lake-store-get-started-portal/ADL.New.Upload.File.png "Carregar dados")

## <a name="properties"></a>Propriedades e ações disponíveis nos Olá armazenados dados
Clique em Olá de tooopen de ficheiro recém-adicionada Olá **propriedades** painel. Propriedades de Olá associadas ao ficheiro Olá e ações de Olá que pode efetuar no ficheiro de Olá estão disponíveis neste painel. Também pode copiar Olá caminho completo toofile na sua conta do Azure Data Lake Store, realçada na caixa de Olá vermelho no Olá captura de ecrã a seguir:

![Propriedades nos dados de Olá](./media/data-lake-store-get-started-portal/ADL.File.Properties.png "propriedades nos dados de Olá")

* Clique em **pré-visualização** toosee uma pré-visualização do ficheiro de Olá, diretamente a partir do browser Olá. Pode especificar o formato de Olá de pré-visualização Olá bem. Clique em **pré-visualização**, clique em **formato** no Olá **pré-visualização do ficheiro** painel e em Olá **formato de pré-visualização do ficheiro** painel especificar Olá opções tal número de linhas toodisplay, codificação toouse, toouse delimitador, etc.
  
  ![Formato de pré-visualização do ficheiro](./media/data-lake-store-get-started-portal/ADL.File.Preview.png "Formato de pré-visualização do ficheiro")
* Clique em **transferir** computador tooyour do toodownload Olá ficheiro.
* Clique em **mudança de nome de ficheiro** ficheiros de Olá toorename.
* Clique em **eliminar ficheiro** ficheiros de Olá toodelete.

## <a name="secure-your-data"></a>Proteger os dados
Pode proteger dados de Olá armazenados na sua conta do Azure Data Lake Store utilizando o Azure Active Directory e o controlo de acesso (ACLs). Para obter instruções sobre como toodo que, consulte [proteger dados no Azure Data Lake Store](data-lake-store-secure-data.md).

## <a name="delete-azure-data-lake-store-account"></a>Eliminar conta do Azure Data Lake Store
toodelete uma conta do Azure Data Lake Store, a partir do painel Data Lake Store, clique **eliminar**. tooconfirm ação de Olá, terá de ser o nome de Olá tooenter pedido da conta de Olá que desejar toodelete. Introduza Olá nome da conta de Olá e, em seguida, clique em **eliminar**.

![Eliminar conta do Data Lake](./media/data-lake-store-get-started-portal/ADL.Delete.Account.png "Eliminar conta do Data Lake")

## <a name="next-steps"></a>Passos seguintes
* [Secure data in Data Lake Store (Proteger dados no Data Lake Store)](data-lake-store-secure-data.md)
* [Utilizar o Azure Data Lake Analytics com o Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Use Azure HDInsight with Data Lake Store (Utilizar o Azure HDInsight com o Data Lake Store)](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Access diagnostic logs for Data Lake Store (Registos de diagnóstico de acesso do Data Lake Store)](data-lake-store-diagnostic-logs.md)

