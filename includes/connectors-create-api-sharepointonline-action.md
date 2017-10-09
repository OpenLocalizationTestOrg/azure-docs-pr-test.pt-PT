Agora que tem de adicionar um acionador, o respetivo toodo tempo algo interessante com dados de Olá que são gerados pelo acionador Olá. Siga estes Olá de tooadd passos **SharePoint Online - criar o ficheiro** ação. Esta ação irá criar um ficheiro no SharePoint Online cada hora Olá novo item acionador é desencadeado. 

tooconfigure Olá esta ação, terá de Olá tooprovide informações a seguir. Como fornecer esta informação, irá reparar que é gerados pelo acionador Olá como entrada para algumas das propriedades de Olá para o novo ficheiro de Olá de dados de toouse fácil:

| Criar a propriedade de ficheiro | Descrição |
| --- | --- |
| URL do site |Este é o URL de Olá do site do SharePoint Online olá onde pretende que o novo ficheiro de toocreate Olá. Selecione o site de Olá Olá apresentados na lista. |
| Caminho da pasta |Isto é Olá pasta (no URL do Site selecionado no passo anterior Olá Olá) onde o novo ficheiro de Olá irão ser colocado. Procure e selecione a pasta de Olá. |
| Nome de ficheiro |Este é o nome de Olá do ficheiro de Olá a ser criado. |
| Conteúdo do ficheiro |conteúdo de Olá que será escrito toohello ficheiro. |

1. Selecione **+ novo passo** ação de Olá tooadd.  
   ![Imagem de ação online do SharePoint 1](./media/connectors-create-api-sharepointonline/action-1.png)  
2. Selecione Olá **adicionar uma ação** ligação. Esta caixa de pesquisa de Olá abre onde pode procurar qualquer ação gostaria de tootake. Neste exemplo, as ações do SharePoint são de interesse.    
   ![Imagem de ação online do SharePoint 2](./media/connectors-create-api-sharepointonline/action-2.png)    
3. Introduza *sharepoint* toosearch para ações de tooSharePoint relacionados.
4. Selecione **SharePoint Online - criar o ficheiro** como Olá tootake de ação.   **Tenha em atenção**: lhe será pedido tooauthorize sua tooaccess de aplicação lógica, o SharePoint conta se não tiver criado anteriormente um tooSharePoint ligação Online.    
   ![Imagem de ação online do SharePoint 3](./media/connectors-create-api-sharepointonline/action-3.png)    
5. Olá **criar ficheiro** controlar é aberto.   
   ![Imagem de ação online do SharePoint 4](./media/connectors-create-api-sharepointonline/action-4.png)     
6. Selecione **URL do Site** e procurar toofind Olá site onde pretende que o ficheiro de Olá toocreate.     
   ![Imagem de ação online do SharePoint 5](./media/connectors-create-api-sharepointonline/action-5.png)  
7. Selecione **caminho da pasta** e procurar toofind Olá pasta onde o novo ficheiro de Olá irão ser colocado.  
   ![Imagem de ação online do SharePoint 6](./media/connectors-create-api-sharepointonline/action-6.png)  
8. Selecione Olá **nome de ficheiro** controlar e introduza o nome de Olá do ficheiro de Olá pretende toocreate. Aqui, pode introduzir o nome de ficheiro Olá diretamente ou pode utilizar qualquer uma das propriedades de Olá do acionador de Olá que criou anteriormente. Fazê-lo ao selecionar propriedades da lista de Olá de **saídas da quando é criado um novo item**. Esta lista é apresentar apenas depois de selecionar Olá **nome de ficheiro** controlo. Neste walkthough, posso selecionado ID (ID de Olá do novo item da lista Olá) como nome de Olá do ficheiro de Olá que está a ser criado pela Olá **SharePoint Online - criar o ficheiro** ação.    
   ![Imagem de ação online do SharePoint 7](./media/connectors-create-api-sharepointonline/action-7.png)  
9. Selecione Olá **conteúdo do ficheiro** controlar e introduza o conteúdo de Olá que será escrito toohello ficheiro que será criado. Para o conteúdo do ficheiro Olá, tenha em atenção que pode utilizar qualquer uma das propriedades de Olá do acionador de Olá que criou anteriormente. Basta selecione propriedades Olá Olá apresentados na lista. Em alternativa, pode introduzir Olá **conteúdo do ficheiro** texto diretamente para o controlo de Olá. Neste exemplo, posso selecionado algumas propriedades e adicionar os espaços e um hífen entre cada propriedade.        
   ![Imagem de ação online do SharePoint 8](./media/connectors-create-api-sharepointonline/action-8.png)  
10. Guardar o fluxo de trabalho do Olá alterações tooyour  
11. Parabéns, tem agora uma aplicação de lógica completamente funcional que é acionada quando um novo item é adicionado a lista de tooa SharePoint Online. aplicação Olá, em seguida, irá criar um ficheiro, com algumas das propriedades de Olá do novo item da lista Olá.  Agora pode testá-lo através da criação de um novo item na lista do SharePoint Olá. 

