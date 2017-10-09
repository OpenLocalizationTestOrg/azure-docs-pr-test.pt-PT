Criar as credenciais de implementação com Olá [az webapp implementação utilizador definido](/cli/azure/webapp/deployment/user#set) comando.

Um utilizador de implementação é necessário para FTP e o local aplicação de web de tooa a implementação de Git. nome de utilizador Olá e a palavra-passe são o nível de conta. _São diferentes das credenciais da sua subscrição do Azure._

No Olá o seguinte comando, substitua  *\<nome de utilizador >* e  *\<palavra-passe >* com um novo nome de utilizador e palavra-passe. nome de utilizador Olá tem de ser exclusivo. Olá palavra-passe tem de ser, pelo menos, oito carateres, com dois Olá seguintes três elementos: letras, números, símbolos. 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

Se obtiver um ` 'Conflict'. Details: 409` erro, o nome de utilizador de Olá de alteração. Se obtiver o ` 'Bad Request'. Details: 400` erro, utilize uma palavra-passe mais forte.

Este utilizador de implementação só é criado uma vez; pode utilizá-lo em todas as suas implementações do Azure.

> [!NOTE]
> Nome do registo Olá utilizador e palavra-passe. Tem de lhes toodeploy Olá web aplicação mais tarde.
>
>