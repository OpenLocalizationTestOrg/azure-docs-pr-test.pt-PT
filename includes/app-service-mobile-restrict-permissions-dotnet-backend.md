
Por predefinição, APIs de um back-end de Mobile Apps pode ser invocadas anonimamente. Em seguida, terá dos clientes do toorestrict acesso tooonly autenticado.  

* **NODE.js novamente end (através do portal do Azure Olá)** :  

    Nas suas definições de Mobile Apps, clique em **tabelas fácil** e selecione a tabela. Clique em **alterar permissões**, selecione **apenas o acesso autenticado** para todas as permissões e, em seguida, clique em **guardar**.
* **.NET back-end (c#)**:  

    No projeto de servidor Olá, navegue demasiado**controladores** > **TodoItemController.cs**. Adicionar Olá `[Authorize]` atributo toohello **TodoItemController** classe, da seguinte forma. toorestrict acesso apenas toospecific métodos, também pode aplicar esta métodos toothose apenas de atributo em vez de classe de Olá. Voltar a publicar o projeto de servidor Olá.

        [Authorize]
        public class TodoItemController : TableController<TodoItem>

* **Back-end node.js (através de código Node.js)** :  

    autenticação toorequire para acesso de tabela, adicione Olá seguinte script de servidor linha toohello Node.js:

        table.access = 'authenticated';

    Para obter mais detalhes, consulte [como: exigir autenticação para acesso tootables](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-auth). toolearn como projeto de código do toodownload Olá início rápido do seu site, consulte [como: Transferir Olá Node.js back-end código projeto de início rápido utilizando o Git](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart).
