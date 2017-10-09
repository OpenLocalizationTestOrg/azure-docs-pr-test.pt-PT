## <a name="prerequisites"></a>Pré-requisitos
Antes, pode escrever o código de gestão de CDN, é necessário toodo algumas tooenable preparação toointeract nosso código com Olá do Azure Resource Manager.  toodo, tem de:

* Criar um Olá de toocontain do grupo de recursos perfil da CDN criamos neste tutorial
* Configurar a autenticação de tooprovide do Azure Active Directory para a nossa aplicação
* Aplicar as permissões de grupo de recursos de toohello, de modo a que apenas pessoal autorizado utilizadores a partir do nosso inquilino do Azure AD pode interagir com o nosso perfil da CDN

### <a name="creating-hello-resource-group"></a>Criar grupo de recursos de Olá
1. Iniciar sessão Olá [Portal do Azure](https://portal.azure.com).
2. Clique em Olá **novo** botão no canto superior esquerdo Olá e, em seguida, **gestão**, e **grupo de recursos**.

    ![Criar um novo grupo de recursos](./media/cdn-app-dev-prep/cdn-new-rg-1-include.png)
3. Chamar o grupo de recursos *CdnConsoleTutorial*.  Selecione a sua subscrição e escolha uma localização perto de si.  Se assim o desejar, pode clicar em Olá **Pin toodashboard** caixa de verificação toopin Olá grupo toohello dashboard de recursos no portal de Olá.  Isto tornarão mais fácil toofind mais tarde.  Depois de efetuadas as suas seleções, clique em **criar**.

    ![Grupo de recursos de Olá nomenclatura](./media/cdn-app-dev-prep/cdn-new-rg-2-include.png)
4. Depois de criar o grupo de recursos de Olá, se não tiver afixá-lo tooyour dashboard, pode encontrá-lo ao clicar em **procurar**, em seguida, **grupos de recursos**.  Clique em tooopen de grupo de recursos de Olá-lo.  Tome nota do seu **ID de subscrição**.  Iremos irá precisar dele mais tarde.

    ![Grupo de recursos de Olá nomenclatura](./media/cdn-app-dev-prep/cdn-subscription-id-include.png)

### <a name="creating-hello-azure-ad-application-and-applying-permissions"></a>Criar aplicação Olá do Azure AD e aplicar permissões
Existem duas abordagens tooapp autenticação no Azure Active Directory: utilizadores individuais ou de um principal de serviço. Um principal de serviço é a conta de serviço tooa semelhante no Windows.  Em vez de conceder um toointeract de permissões de utilizador específico com perfis da CDN Olá, iremos em vez disso, conceder permissões de Olá toohello principal de serviço.  Principais de serviço são geralmente utilizados para os processos automatizados, não interativo.  Apesar deste tutorial é escrever uma aplicação de consola interativa, iremos irá focar-se na abordagem de principal de serviço de Olá.

Criar um principal de serviço é composta por vários passos, incluindo a criação de uma aplicação do Azure Active Directory.  toodo isto, vamos demasiado[siga este tutorial](../articles/resource-group-create-service-principal-portal.md).

> [!IMPORTANT]
> Ser toofollow se todos os passos de Olá Olá [tutorial ligado](../articles/resource-group-create-service-principal-portal.md).  É *extremamente importante* que conclua-lo tal como descrito.  Certifique-se de que toonote sua **ID de inquilino**, **nome de domínio do inquilino** (normalmente uma *. onmicrosoft.com* domínio, exceto se tiver especificado um domínio personalizado), **ID de cliente** , e **chave de autenticação de cliente**, uma vez que vamos precisar deles mais tarde.  Ser muito cuidado tooguard sua **ID de cliente** e **chave de autenticação de cliente**, uma vez que estas credenciais podem ser utilizados por qualquer pessoa tooexecute operações como principal de serviço Olá.
>
> Quando obtiver passo toohello com o nome de aplicação de multi-inquilino de configurar, selecione **não**.
>
> Quando obtiver toohello passo [atribuir aplicação toorole](../articles/azure-resource-manager/resource-group-create-service-principal-portal.md#assign-application-to-role), grupo de recursos de Olá de utilização que criou anteriormente, *CdnConsoleTutorial*, mas em vez de Olá **leitor** função, atribuir Olá **contribuinte de perfil de CDN** função.  Depois de atribuir Olá de aplicação Olá **contribuinte de perfil de CDN** função no seu grupo de recursos, tutorial de retorno toothis. 
>
>

Assim que tiver criado a sua Olá de serviço principal e atribuídos **contribuinte de perfil de CDN** função, Olá **utilizadores** painel para o grupo de recursos deve ter um aspeto semelhante toothis.

![Painel de utilizadores](./media/cdn-app-dev-prep/cdn-service-principal-include.png)

### <a name="interactive-user-authentication"></a>Autenticação de utilizador interativa
Se, em vez de um principal de serviço, em vez disso, deverá dispor autenticação interativa de utilizador individuais, o processo de Olá é muito semelhante toothat para um principal de serviço.  Na verdade, terá de toofollow Olá mesmo procedimento, mas fazer algumas alterações secundárias.

> [!IMPORTANT]
> Apenas siga estes passos, se escolher a autenticação de utilizador individuais toouse em vez de um principal de serviço.
>
>

1. Ao criar a sua aplicação, em vez de **aplicação Web**, escolha **aplicação nativa**.

    ![Aplicação nativa](./media/cdn-app-dev-prep/cdn-native-application-include.png)
2. Na página seguinte do Olá, será solicitado para um **URI de redirecionamento**.  Olá URI não serão validados, mas não se esqueça de que introduziu.  Precisará dela mais tarde.
3. Não há nenhum toocreate é necessário um **chave de autenticação de cliente**.
4. Em vez de atribuir um toohello principal de serviço **contribuinte de perfil de CDN** função, vamos tooassign utilizadores ou grupos individuais.  Neste exemplo, pode ver que posso tiver atribuída *CDN demonstração de utilizador* toohello **contribuinte de perfil de CDN** função.  

    ![Acesso de utilizador individuais](./media/cdn-app-dev-prep/cdn-aad-user-include.png)
