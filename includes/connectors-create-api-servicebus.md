### <a name="prerequisites"></a>Pré-requisitos
Tem de ter um [Service Bus](https://azure.microsoft.com/services/service-bus/) conta.  

Antes de poder utilizar a sua conta do Service Bus do Azure numa aplicação lógica, tem de autorizar Olá lógica tooconnect tooyour service bus conta da aplicação. Felizmente, pode fazê-facilmente na sua aplicação lógica em Olá portal do Azure.  

Seguem-se Olá passos tooauthorize sua tooyour de tooconnect de aplicação lógica conta do Service Bus:  

1. Selecione de uma ligação tooService Bus, no designer de aplicação de lógica de Olá, toocreate **Mostrar Microsoft APIs geridas** no Olá na lista pendente. Em seguida, introduza **service bus** na caixa de pesquisa de Olá. Selecione o acionador de Olá ou ação que pretende toouse.  
    ![Imagem de ligação do Service Bus 1](./media/connectors-create-api-servicebus/servicebus-1.png)  
2. Se ainda não criou quaisquer tooService de ligações de barramento anteriormente, será pedido tooprovide as suas credenciais do Service Bus. Estas credenciais são utilizada tooauthorize sua tooand de tooconnect de aplicação lógica aceder a dados da sua conta de Service Bus. conector do Service Bus Olá necessita de cadeia de ligação de Olá para Olá espaço de nomes de barramento de serviço. Também requer **gerir** permissões. Tooknow uma boa forma, se a cadeia de ligação for para Olá espaço de nomes ou uma entidade específica é se contém Olá `EntityPath` parâmetro. Se existir, não é cadeia de ligação correta Olá para uma aplicação lógica.  
    ![Cadeia de ligação do Service Bus](./media/connectors-create-api-servicebus/connectionstring.png)
3. Após ter recebido a cadeia de ligação de Olá para Olá espaço de nomes, pode utilizá-lo para Olá ligação da API em Logic Apps.  
    ![Imagem de ligação do Service Bus 2](./media/connectors-create-api-servicebus/servicebus-2.png)  
4. Repare ligação Olá foi criada e está agora tooproceed livre com Olá outro passos na sua aplicação lógica.  
    ![Imagem de ligação do Service Bus 3](./media/connectors-create-api-servicebus/servicebus-3.png)   

