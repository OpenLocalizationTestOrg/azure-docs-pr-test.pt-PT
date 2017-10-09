1. No **Explorador de soluções**, clique no projeto Olá e selecione **publicar**. Escolha **Criar Novo** e, em seguida, clique em **Publicar**. 

    ![Publicar cria uma nova aplicação de funções](./media/functions-vstools-publish/functions-vstools-publish-new-function-app.png)

2. Se já não tiver ligado Visual Studio tooyour conta do Azure, clique em **adicionar uma conta...** .  

3. No Olá **criar App Service** caixa de diálogo, utilize Olá **alojamento** definições como Olá especificado na tabela seguinte: 

    ![Tempo de execução local do Azure](./media/functions-vstools-publish/functions-vstools-publish.png)

    | Definição      | Valor sugerido  | Descrição                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Nome da Aplicação** | Nome globalmente exclusivo | Nome que identifica exclusivamente a sua nova aplicação de funções. |
    | **Subscrição** | Escolher a sua subscrição | Olá toouse de subscrição do Azure. |
    | **[Grupo de Recursos](../articles/azure-resource-manager/resource-group-overview.md)** | myResourceGroup |  Nome do recurso de Olá grupo no qual toocreate a aplicação de função. |
    | **[Plano do Serviço de Aplicações](../articles/azure-functions/functions-scale.md)** | Plano de consumo | Certifique-se de que toochoose Olá **consumo** em **tamanho** quando cria um novo plano.  |
    | **[Conta de armazenamento](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)** | Nome globalmente exclusivo | Utilize uma conta de armazenamento existente ou crie uma nova.   |

4. Clique em **criar** toocreate uma aplicação de função no Azure com estas definições. Depois de concluída a Olá aprovisionamento, anote Olá **URL do Site** valor, o que é o endereço de Olá da sua aplicação de função no Azure. 

    ![Tempo de execução local do Azure](./media/functions-vstools-publish/functions-vstools-publish-profile.png)
