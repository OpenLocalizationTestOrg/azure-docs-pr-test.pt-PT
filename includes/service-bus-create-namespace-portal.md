filas toobegin utilizando o Service Bus no Azure, primeiro tem de criar um espaço de nomes com um nome que seja exclusivo em todo o Azure. Um espaço de nomes fornece um contentor de âmbito para abordar os recursos do Service Bus na sua aplicação.

toocreate um espaço de nomes:

1. Inicie sessão no toohello [portal do Azure][Azure portal].
2. No painel de navegação esquerdo Olá do portal de Olá, clique em **novo**, em seguida, clique em **integração empresarial com**e, em seguida, clique em **Service Bus**.
3. No Olá **criar espaço de nomes** caixa de diálogo, introduza um nome de espaço de nomes. sistema de Olá verifica imediatamente toosee se o nome de Olá está disponível.
4. Depois de efetuar o nome de espaço de nomes de Olá se estiver disponível, escolha Olá (básica, Standard ou Premium) de escalão de preço.
5. No Olá **subscrição** campo, escolha uma subscrição do Azure no espaço de nomes de Olá que toocreate.
6. No Olá **grupo de recursos** campo, escolha um grupo de recursos existente na qual Olá espaço de nomes em direto ou, crie um novo.      
7. No **localização**, escolha o país Olá ou região onde será alojado o espaço de nomes.
   
    ![Create namespace][create-namespace]
8. Clique em **Criar**. Agora, o sistema Olá cria o seu espaço de nomes e ativa-o. Poderá ter toowait alguns minutos enquanto Olá sistema Aprovisiona recursos para a sua conta.

### <a name="obtain-hello-management-credentials"></a>Obter credenciais de gestão de Olá

1. Na lista de Olá dos espaços de nomes, clique em Olá recém-criado espaço de nomes.
2. No painel de espaço de nomes de Olá, clique em **políticas de acesso partilhado**.
3. No Olá **políticas de acesso partilhado** painel, clique em **RootManageSharedAccessKey**.
   
    ![connection-info][connection-info]
4. No Olá **política: RootManageSharedAccessKey** painel, clique no botão de cópia de Olá junto demasiado**chave de cadeia – primária da ligação**, toocopy Olá ligação cadeia tooyour área de transferência para utilização posterior. Cole este valor no Bloco de Notas ou noutra localização temporária.
   
    ![connection-string][connection-string]

5. Passo anterior repetida Olá, copiar e colar o valor Olá **chave primária** tooa localização temporária para utilização posterior.

<!--Image references-->

[create-namespace]: ./media/service-bus-create-namespace-portal/create-namespace.png
[connection-info]: ./media/service-bus-create-namespace-portal/connection-info.png
[connection-string]: ./media/service-bus-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
