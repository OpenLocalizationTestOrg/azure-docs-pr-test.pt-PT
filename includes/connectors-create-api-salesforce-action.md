Agora que tem de adicionar uma condição, o respetivo toodo tempo algo interessante com dados de Olá que são gerados pelo acionador Olá. Siga estes Olá de tooadd passos **Salesforce - objeto Get** ação. Esta ação irá obter dados de Olá sempre que é criada uma antecedência de novo. Também irá adicionar uma segunda ação que irá utilizar Olá dados do Salesforce - Get toosend de ação um objeto de Olá uma mensagem de e-mail utilizando o conector de Olá do Office 365.  

tooconfigure Olá esta ação, terá de Olá tooprovide informações a seguir. Vai notar que é gerados pelo acionador Olá como entrada para algumas das propriedades de Olá para o novo ficheiro de Olá de dados de toouse fácil:

| Criar a propriedade de ficheiro | Descrição |
| --- | --- |
| Tipo de objeto |Este é o tipo de Olá do objeto do Salesforce que está interessado. Os exemplos são oportunidades potenciais, a conta, etc. |
| ID de objeto |Representa um identificador de objeto de Olá. |

1. Selecione **adicionar uma ação** ligação. Esta caixa de pesquisa de Olá abre onde pode procurar qualquer ação gostaria de tootake. Neste exemplo, Salesforce ações são úteis.      
   ![Imagem da ação Salesforce 1](./media/connectors-create-api-salesforce/action-1.png)  
2. Introduza *salesforce* toosearch para ações de toosalesforce relacionados.
3. Selecione **Salesforce - objeto Get** como Olá tootake de ação.   **Tenha em atenção**: lhe será pedido tooauthorize sua tooaccess de aplicação de lógica de conta do Salesforce se não o fez, anteriormente.    
   ![Imagem da ação Salesforce 2](./media/connectors-create-api-salesforce/action-2.png)    
4. Olá **Get objeto** controlar é aberto.  
5. Selecione *levar* como tipo de objeto Olá.
6. Selecione Olá **ID de objeto** controlo.
7. Selecione **...**  lista de Olá tooexpand de tokens que podem ser utilizadas como entrada para ações.       
   ![Imagem da ação Salesforce 3](./media/connectors-create-api-salesforce/action-3.png)    
8. Selecione **levar ID** controlar é aberto.   
   ![Imagem da ação Salesforce 4](./media/connectors-create-api-salesforce/action-4.png)     
9. Tenha em atenção de que esse token de ID levar Olá está agora em Olá controlo de ID de objeto, que indica que Olá Get ação de objeto irá procurar uma antecedência com um ID que é o ID de oportunidades potenciais toohello igual de oportunidades potenciais que acionou esta aplicação lógica.  
   ![Imagem da ação Salesforce 5](./media/connectors-create-api-salesforce/action-5.png)  
10. Guarde o seu trabalho. Já está, adicionou a aplicação de lógica de tooyour objeto ação Olá Get. O controlo de objeto Get deve ter o seguinte aspeto:    
    ![Imagem da ação Salesforce 6](./media/connectors-create-api-salesforce/action-6.png)  

Agora que adicionou um tooget ação uma antecedência, poderá ser útil toodo algo interessante com antecedência Olá recentemente criado. Numa empresa, poderá ser útil toosend toonotify um e-mail uma lista de distribuição que foi criada uma antecedência de novo. Vamos utilizar Olá do Office 365 conector toosend um e-mail com algumas das informações relevantes do Olá do objeto de novas oportunidades potenciais Olá no Salesforce.  

1. Selecione **adicionar uma ação** , em seguida, introduza *e-mail* no controlo de procura Olá. Este procedimento filtra Olá ações toothose toosending relacionado e receber correio eletrónico.  
2. Selecione Olá **Office 365 Outlook - envie um e-mail** item da lista. Se já não criou um *ligação* tooyour conta do Office 365, poderá ser pedido tooenter toocreate de credenciais do Office 365 it agora. Depois de terminar, Olá **enviar um e-mail** controlar é aberto.        
   ![Imagem da ação Salesforce 7](./media/connectors-create-api-salesforce/action-7.png)  
3. Introduza o endereço de correio eletrónico Olá que gostaria de Olá do toosend e-mail tooin **para** controlo.
4. No Olá **requerente** controlar, introduza *levar nova criada* -, em seguida, selecione Olá *empresa* token. Isto irá apresentar Olá *empresa* campo de Olá novas oportunidades potenciais criado no Salesforce.  
5. No Olá **corpo** controlo, pode selecionar qualquer um dos tokens de Olá do novo objeto de oportunidades potenciais Olá e também pode introduzir qualquer texto que gostaria de toodisplay no corpo de Olá de Olá correio eletrónico. Eis um exemplo:  
   ![Imagem da ação Salesforce 8](./media/connectors-create-api-salesforce/action-8.png)   
6. Guarde o fluxo de trabalho.  

E já está. A aplicação lógica está agora concluída.  

Agora, pode testar a sua aplicação lógica: Salesforce, criar uma novo antecedência que satisfaça a condição de Olá que criou.  Se seguiu totalmente esta passagem, acabou de criar uma antecedência com um endereço de correio eletrónico que contém *amazon.com* no mesmo. Após alguns segundos a sua aplicação lógica deve ser acionada e resultados Olá podem ter um aspeto semelhante toothis:  
![Imagem da ação Salesforce 9](./media/connectors-create-api-salesforce/action-9.png)  

