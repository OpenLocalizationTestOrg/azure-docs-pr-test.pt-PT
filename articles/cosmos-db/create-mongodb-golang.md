---
Título: aaa "BD de Cosmos do Azure: criar uma aplicação de consola do MongoDB API com Golang e Olá portal do Azure | Descrição Microsoft Docs": apresenta um exemplo de código Golang pode utilizar tooconnect tooand consultar os serviços do Azure Cosmos DB: cosmos-db autor: Gestor Durgaprasad Budhwani: jhubbard editor: mimig1

MS. Service: MS. topic do cosmos-db: heroína-article MS. Date: author 21/07/2017: mimig
---

# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-golang-and-hello-azure-portal"></a>BD do Azure do Cosmos: Criar uma aplicação de consola do MongoDB API com Golang e Olá portal do Azure

O Azure Cosmos DB é um serviço de bases de dados com vários modelos e distribuído globalmente da Microsoft. Pode criar e consultar documentos, chave/valor e bases de dados de gráfico, sendo todas beneficiam das capacidades de dimensionamento horizontal núcleo Olá da base de dados do Azure Cosmos e distribuição global Olá rapidamente.

Este início rápido demonstra como toouse existente [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) aplicações escritas no [Golang](https://golang.org/) e ligá-lo tooyour Azure Cosmos DB da base de dados, que suporta ligações de cliente do MongoDB.

Por outras palavras, a aplicação de Golang apenas sabe que está a ligar tooa base de dados com APIs do MongoDB. É transparente toohello aplicação Olá dados é armazenada na base de dados do Azure Cosmos.

## <a name="prerequisites"></a>Pré-requisitos

- Uma subscrição do Azure. Se não tiver uma subscrição do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free) antes de começar.
- [Aceda](https://golang.org/dl/) e um conhecimento básico de Olá [aceda](https://golang.org/) idioma.
- Um IDE — [Gogland](https://www.jetbrains.com/go/) da Jetbrains, o [Visual Studio Code](https://code.visualstudio.com/) da Microsoft ou o [Atom](https://atom.io/). Neste tutorial, estamos a utilizar o Goglang.

<a id="create-account"></a>
## <a name="create-a-database-account"></a>Criar uma conta de base de dados

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a>Aplicação de exemplo de Olá do clone

Clone a aplicação de exemplo de Olá e instalar pacotes de Olá necessário.

1. Crie uma pasta denominada CosmosDBSample Olá GOROOT\src pasta, o que é C:\Go\ por predefinição.
2. Execute Olá seguir o comando utilizando uma janela de terminal do git, tais como o repositório do git bash tooclone Olá exemplo na pasta de CosmosDBSample Olá. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-golang-getting-started.git
    ```
3.  Execute Olá pacote do comando tooget Olá mgo a seguir. 

    ```
    go get gopkg.in/mgo.v2
    ```

Olá [mgo](http://labix.org/mgo) controlador (pronuncia-se como *mango*) é um [MongoDB](http://www.mongodb.org/) controlador para Olá [aceda idioma](http://golang.org/) que implementa um avançada e também testado seleção de funcionalidades numa API muito simple padrão aceda idioms a seguir.

<a id="connection-string"></a>

## <a name="update-your-connection-string"></a>Atualizar a cadeia de ligação

Agora, volte atrás toohello tooget portal do Azure que as informações de cadeia de ligação e copie-o para a aplicação Olá.

1. Clique em **início rápido** no Olá menu de navegação esquerdo e, em seguida, clique em **outros** tooview Olá ligação cadeia informações necessárias pela Olá aceda aplicação.

2. No Goglang, abra o ficheiro de main.go de Olá no diretório de GOROOT\CosmosDBSample Olá e atualizar Olá seguintes linhas de código utilizando Olá cadeia as informações de ligação Olá portal do Azure, conforme mostrado na seguinte captura de ecrã de Olá. 

    nome da base de dados de Olá é o prefixo de Olá de Olá **anfitrião** valor no painel de cadeia de ligação de portal do Azure Olá. Para a conta de Olá mostrada na imagem de Olá abaixo, o nome de base de dados de Olá é golang ministrar.

    ```go
    Database: "hello prefix of hello Host value in hello Azure portal",
    Username: "hello Username in hello Azure portal",
    Password: "hello Password in hello Azure portal",
    ```

    ![Painel, outra informações de cadeia de ligação do Olá Mostrar portal do Azure Olá separador de início rápido](./media/create-mongodb-golang/cosmos-db-golang-connection-string.png)

3. Guarde o ficheiro de main.go Olá.

## <a name="review-hello-code"></a>Rever o código de Olá

Certifiquemo-numa revisão rápida do que está a acontecer no ficheiro de main.go Olá. 

### <a name="connecting-hello-go-app-tooazure-cosmos-db"></a>Ligar Olá aceda aplicação tooAzure Cosmos DB

BD do Azure do Cosmos suporta Olá MongoDB SSL ativado. tooconnect tooan MongoDB SSL ativado, terá de toodefine Olá **DialServer** funcionar [mgo. DialInfo](http://gopkg.in/mgo.v2#DialInfo)e a utilização de Olá [tls. *Marcação* ](http://golang.org/pkg/crypto/tls#Dial) ligação de Olá tooperform de função.

Olá seguinte fragmento de código Golang liga ao hello aceda aplicação API do Azure Cosmos DB MongoDB. Olá *DialInfo* classe contém opções para estabelecer uma sessão com um cluster do MongoDB.

```go
// DialInfo holds options for establishing a session with a MongoDB cluster.
dialInfo := &mgo.DialInfo{
    Addrs:    []string{"golang-couch.documents.azure.com:10255"}, // Get HOST + PORT
    Timeout:  60 * time.Second,
    Database: "database", // It can be anything
    Username: "username", // Username
    Password: "Azure database connect password from Azure Portal", // PASSWORD
    DialServer: func(addr *mgo.ServerAddr) (net.Conn, error) {
        return tls.Dial("tcp", addr.String(), &tls.Config{})
    },
}

// Create a session which maintains a pool of socket connections
// tooour Azure Cosmos DB MongoDB database.
session, err := mgo.DialWithInfo(dialInfo)

if err != nil {
    fmt.Printf("Can't connect toomongo, go error %v\n", err)
    os.Exit(1)
}

defer session.Close()

// SetSafe changes hello session safety mode.
// If hello safe parameter is nil, hello session is put in unsafe mode, 
// and writes become fire-and-forget,
// without error checking. hello unsafe mode is faster since operations won't hold on waiting for a confirmation.
// 
session.SetSafe(&mgo.Safe{})
```

Olá **mgo. Dial()** é utilizado o método quando não existe nenhuma ligação de SSL. Para uma ligação SSL, Olá **mgo. DialWithInfo()** método não é necessário.

Uma instância de Olá **{} de DialWIthInfo** objeto é o objeto de sessão de Olá toocreate utilizados. Assim que a sessão de Olá é estabelecida, pode aceder a coleção de Olá utilizando Olá seguinte fragmento de código:

```go
collection := session.DB(“database”).C(“package”)
```

<a id="create-document"></a>

### <a name="create-a-document"></a>Criar um documento

```go
// Model
type Package struct {
    Id bson.ObjectId  `bson:"_id,omitempty"`
    FullName      string
    Description   string
    StarsCount    int
    ForksCount    int
    LastUpdatedBy string
}

// insert Document in collection
err = collection.Insert(&Package{
    FullName:"react",
    Description:"A framework for building native apps with React.",
    ForksCount: 11392,
    StarsCount:48794,
    LastUpdatedBy:"shergin",

})

if err != nil {
    log.Fatal("Problem inserting data: ", err)
    return
}
```

### <a name="query-or-read-a-document"></a>Consultar ou ler um documento

O Azure Cosmos DB suporta consultas extensas de documentos JSON armazenados em cada coleção. Olá código de exemplo seguinte mostra uma consulta que pode ser executado contra documentos Olá na sua coleção.

```go
// Get a Document from hello collection
result := Package{}
err = collection.Find(bson.M{"fullname": "react"}).One(&result)
if err != nil {
    log.Fatal("Error finding record: ", err)
    return
}

fmt.Println("Description:", result.Description)
```


### <a name="update-a-document"></a>Atualizar um documento

```go
// Update a document
updateQuery := bson.M{"_id": result.Id}
change := bson.M{"$set": bson.M{"fullname": "react-native"}}
err = collection.Update(updateQuery, change)
if err != nil {
    log.Fatal("Error updating record: ", err)
    return
}
```

### <a name="delete-a-document"></a>Eliminar um documento

O Azure Cosmos DB suporta a eliminação de documentos JSON.

```go
// Delete a document
query := bson.M{"_id": result.Id}
err = collection.Remove(query)
if err != nil {
   log.Fatal("Error deleting record: ", err)
   return
}
```
    
## <a name="run-hello-app"></a>Executar a aplicação Olá

1. No Goglang, certifique-se de que o GOPATH (disponível em **ficheiro**, **definições**, **aceda**, **GOPATH**) incluem a localização de Olá no qual Olá gopkg foi instalado, que é USERPROFILE\go por predefinição. 
2. Comente linhas Olá que elimina o documento de Olá, linhas 91-96, para que possa ver documentos Olá após a aplicação Olá em execução.
3. No Goglang, clique em **Executar**e, em seguida, clique em **Executar “Criar main.go e executar”**.

    aplicação Olá concluída e apresenta a descrição de Olá documento Olá criado no [criar um documento](#create-document).
    
    ```
    Description: A framework for building native apps with React.
    
    Process finished with exit code 0
    ```

    ![Goglang que mostra a saída de Olá da aplicação Olá](./media/create-mongodb-golang/goglang-cosmos-db.png)
    
## <a name="review-your-document-in-data-explorer"></a>Rever o documento no Data Explorer

Volte toohello toosee portal do Azure o documento no Explorador de dados.

1. Clique em **Explorador de dados (pré-visualização)** no menu de navegação esquerdo Olá, expanda **golang ministrar**, **pacote**e, em seguida, clique em **documentos**. No Olá **documentos** separador, clique em Olá \_documento de Olá toodisplay id no painel direito Olá. 

    ![Documento de Olá recém-criado de que mostra de Explorador de dados](./media/create-mongodb-golang/golang-cosmos-db-data-explorer.png)
    
2. Pode trabalhar com Olá documento inline e clique em **atualização** toosave-lo. Também pode eliminar Olá documento ou criar novos documentos ou consultas.

## <a name="review-slas-in-hello-azure-portal"></a>Reveja os SLAs no Olá portal do Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpar recursos

Se não toocontinue toouse esta aplicação, elimine todos os recursos criados por este guia de introdução no Olá portal do Azure com Olá os seguintes passos:

1. No menu da esquerda de Olá no Olá portal do Azure, clique em **grupos de recursos** e, em seguida, clique em nome de Olá do recurso de Olá que criou. 
2. Na sua página de grupo de recursos, clique em **eliminar**, escreva o nome de Olá de Olá recursos toodelete na caixa de texto Olá e, em seguida, clique em **eliminar**.

## <a name="next-steps"></a>Passos seguintes

Este guia de introdução, aprendeu como toocreate uma conta de base de dados do Azure Cosmos e execute uma aplicação de Golang utilizando hello API para MongoDB. Agora pode importar a conta de base de dados do Cosmos tooyour de dados adicionais. 

> [!div class="nextstepaction"]
> [Importe dados para a base de dados do Azure Cosmos para Olá API do MongoDB](mongodb-migrate.md)
