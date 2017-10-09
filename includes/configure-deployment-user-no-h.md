<span data-ttu-id="ab12a-101">Criar as credenciais de implementação com Olá [az webapp implementação utilizador definido](/cli/azure/webapp/deployment/user#set) comando.</span><span class="sxs-lookup"><span data-stu-id="ab12a-101">Create deployment credentials with hello [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command.</span></span>

<span data-ttu-id="ab12a-102">Um utilizador de implementação é necessário para FTP e o local aplicação de web de tooa a implementação de Git.</span><span class="sxs-lookup"><span data-stu-id="ab12a-102">A deployment user is required for FTP and local Git deployment tooa web app.</span></span> <span data-ttu-id="ab12a-103">nome de utilizador Olá e a palavra-passe são o nível de conta.</span><span class="sxs-lookup"><span data-stu-id="ab12a-103">hello user name and password are account level.</span></span> <span data-ttu-id="ab12a-104">_São diferentes das credenciais da sua subscrição do Azure._</span><span class="sxs-lookup"><span data-stu-id="ab12a-104">_They are different from your Azure subscription credentials._</span></span>

<span data-ttu-id="ab12a-105">No Olá o seguinte comando, substitua  *\<nome de utilizador >* e  *\<palavra-passe >* com um novo nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="ab12a-105">In hello following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="ab12a-106">nome de utilizador Olá tem de ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="ab12a-106">hello user name must be unique.</span></span> <span data-ttu-id="ab12a-107">Olá palavra-passe tem de ser, pelo menos, oito carateres, com dois Olá seguintes três elementos: letras, números, símbolos.</span><span class="sxs-lookup"><span data-stu-id="ab12a-107">hello password must be at least eight characters long, with two of hello following three elements: letters, numbers, symbols.</span></span> 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="ab12a-108">Se obtiver um ` 'Conflict'. Details: 409` erro, o nome de utilizador de Olá de alteração.</span><span class="sxs-lookup"><span data-stu-id="ab12a-108">If you get a ` 'Conflict'. Details: 409` error, change hello username.</span></span> <span data-ttu-id="ab12a-109">Se obtiver o ` 'Bad Request'. Details: 400` erro, utilize uma palavra-passe mais forte.</span><span class="sxs-lookup"><span data-stu-id="ab12a-109">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

<span data-ttu-id="ab12a-110">Este utilizador de implementação só é criado uma vez; pode utilizá-lo em todas as suas implementações do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab12a-110">You create this deployment user only once; you can use it for all your Azure deployments.</span></span>

> [!NOTE]
> <span data-ttu-id="ab12a-111">Nome do registo Olá utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="ab12a-111">Record hello user name and password.</span></span> <span data-ttu-id="ab12a-112">Tem de lhes toodeploy Olá web aplicação mais tarde.</span><span class="sxs-lookup"><span data-stu-id="ab12a-112">You need them toodeploy hello web app later.</span></span>
>
>