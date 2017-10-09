### <a name="prerequisites"></a>Pré-requisitos
* Uma conta do Azure; Pode criar um [conta gratuita](https://azure.microsoft.com/free)
* Um [conta do Blob Storage do Azure](../articles/storage/common/storage-create-storage-account.md) , incluindo o nome de conta do storage Olá e a sua chave de acesso. Estas informações são listadas por Olá as propriedades da conta do storage Olá no Olá portal do Azure. Leia mais sobre [Storage do Azure](../articles/storage/common/storage-introduction.md).

Antes de utilizar a sua conta do Blob Storage do Azure numa aplicação lógica, ligar a conta de armazenamento de Blobs do Azure tooyour. Pode fazê-facilmente na sua aplicação lógica em Olá portal do Azure.  

Ligar a conta de armazenamento de Blobs do Azure de tooyour utilizando Olá os seguintes passos:  

1. Crie uma aplicação lógica. No designer de aplicações lógicas Olá, adicione um acionador e, em seguida, adicionar uma ação. Selecione **Mostrar Microsoft APIs geridas** Olá na lista pendente e, em seguida, introduza "blob" na caixa de pesquisa de Olá. Selecione uma das ações de Olá:  
   
    ![Passo de criação de ligação de armazenamento de Blobs do Azure](./media/connectors-create-api-azureblobstorage/azureblobstorage-1.png)  
2. Se ainda não criou anteriormente todas as ligações tooAzure armazenamento, serão apresentadas para detalhes de ligação de Olá:   
   
    ![Passo de criação de ligação de armazenamento de Blobs do Azure](./media/connectors-create-api-azureblobstorage/connection-details.png)  
3. Introduza os detalhes da conta de armazenamento Olá. Propriedades com um asterisco são necessárias.
   
   | Propriedade | Detalhes |
   | --- | --- |
   | Nome da ligação * |Introduza um nome para a sua ligação. |
   | Nome da conta de armazenamento do Azure * |Introduza o nome de conta de armazenamento de Olá. o nome de conta do storage Olá é apresentado nas propriedades de armazenamento Olá na Olá portal do Azure. |
   | Chave de acesso de conta do Storage do Azure * |Introduza a chave de conta do storage Olá. chaves de acesso de Olá são apresentadas nas propriedades de armazenamento Olá na Olá portal do Azure. |
   
    Estas credenciais são utilizada tooauthorize sua tooconnect de aplicação lógica e aceder aos seus dados. 
4. Selecione **Criar**.
5. Tenha em atenção Olá ligação foi criada. Agora, pode continuar com a Olá outro passos seguintes na sua aplicação lógica: 
   
    ![Passo de criação de ligação de armazenamento de Blobs do Azure](./media/connectors-create-api-azureblobstorage/azureblobstorage-3.png)  

