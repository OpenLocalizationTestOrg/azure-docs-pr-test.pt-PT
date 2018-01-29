---
title: "Ligar à Base de Dados do Azure para MySQL a partir de Node.js | Microsoft Docs"
description: "Este guia de início rápido disponibiliza vários exemplos de código Node.js que pode utilizar para se ligar e consultar dados da Base de Dados do Azure para MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql
ms.custom: mvc
ms.devlang: nodejs
ms.topic: quickstart
ms.date: 09/22/2017
ms.openlocfilehash: 2f18016614b229273aa4d661991149be949ce238
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/11/2017
---
# <a name="azure-database-for-mysql-use-nodejs-to-connect-and-query-data"></a>Base de Dados do Azure para MySQL: utilizar Node.js para se ligar e consultar dados
Este guia de início rápido explica como se pode ligar a uma Base de Dados do Azure para MySQL através do [Node.js](https://nodejs.org/) a partir de plataformas Windows, Ubuntu Linux e Mac. Explica como utilizar as instruções SQL para consultar, inserir, atualizar e eliminar dados da base de dados. Este tópico pressupõe que está familiarizado com a programação com Node.js e que nunca trabalhou com a Base de Dados do Azure para MySQL.

## <a name="prerequisites"></a>Pré-requisitos
Este guia de início rápido utiliza os recursos criados em qualquer um desTes guias como ponto de partida:
- [Criar uma Base de Dados do Azure para o servidor MySQL com o portal do Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Criar uma Base de Dados do Azure para o servidor MySQL com a CLI do Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

Também tem de:
- Instalar o runtime de [Node.js](https://nodejs.org).
- Instalar o pacote [mysql2](https://www.npmjs.com/package/mysql2) para ligar ao MySQL a partir da aplicação Node.js. 

## <a name="install-nodejs-and-the-mysql-connector"></a>Instalar Node.js e o conector de MySQL
Dependendo da sua plataforma, siga as instruções na secção adequada para instalar o Node.js. Utilize npm para instalar o pacote mysql2 e as respetivas dependências na pasta do seu projeto.

### <a name="windows"></a>**Windows**
1. Visite a [página de transferências do Node. js](https://nodejs.org/en/download/) e, em seguida, selecione a opção de instalador Windows que pretende.
2. Crie uma pasta de projeto local , como `nodejsmysql`. 
3. Inicie a linha de comandos e, em seguida, altere o diretório para a pasta do projeto, como `cd c:\nodejsmysql\`
4. Execute a ferramenta NPM para instalar a biblioteca de mysql2 na pasta do projeto.

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. Procure `mysql2@1.3.5` no texto da saída `npm list` para verificar a instalação.

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**
1. Execute os seguintes comandos para instalar **Node.js** e **npm**, o gestor de pacotes para Node.js.

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. Execute os seguintes comandos para criar a pasta do projeto `mysqlnodejs` e instalar o pacote de mysql2 na mesma.

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. Procure `mysql2@1.3.5` no texto da saída da lista de npm para verificar a instalação.

### <a name="mac-os"></a>**Mac OS**
1. Introduza os seguintes comandos para instalar **brew**, um gestor de pacotes de fácil utilização para Mac OS X e **Node.js**.

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. Execute os seguintes comandos para criar a pasta do projeto `mysqlnodejs` e instalar o pacote de mysql2 na mesma.

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. Procure `mysql2@1.3.6` no texto da saída `npm list` para verificar a instalação. O número da versão pode variar à medida que forem sendo lançados patches novos.

## <a name="get-connection-information"></a>Obter informações da ligação
Obtenha as informações de ligação necessárias para se ligar à Base de Dados do Azure para MySQL. Necessita do nome do servidor e das credenciais de início de sessão totalmente qualificados.

1. Inicie sessão no [Portal do Azure](https://portal.azure.com/).
2. No painel do lado esquerdo, clique em **Todos os recursos** e procure o servidor que criou (por exemplo, **myserver4demo**).
3. Clique no nome do servidor, **myserver4demo**.
4. Selecione a página de **Propriedades** e, em seguida, tome nota do **Nome do servidor** e **Nome de início de sessão de administração do servidor**.
 ![Base de Dados do Azure para o MySQL – Início de sessão de administrador do servidor](./media/connect-nodejs/1_server-properties-name-login.png)
5. Caso se tenha esquecido das informações de início de sessão do seu servidor, navegue até à página **Descrição geral** para visualizar o nome de início de sessão de administrador do servidor e, se necessário, repor a palavra-passe.

## <a name="running-the-javascript-code-in-nodejs"></a>Executar o código JavaScript no Node.js
1. Cole o código JavaScript em ficheiros de texto e, em seguida, guarde-o numa pasta de projeto com a extensão de ficheiro .js, tal como (C:\nodejsmysql\createtable.js ou /home/username/nodejsmysql/createtable.js).
2. Inicie a linha de comandos ou shell do bash e, em seguida, altere o diretório para a pasta do projeto, `cd nodejsmysql`.
3. Para executar a aplicação, escreva o comando do nó seguido do nome do ficheiro, como, por exemplo, `node createtable.js`.
4. No Windows, se a aplicação node não estiver no caminho de variável do seu ambiente, poderá ter de utilizar o caminho completo para iniciá-la, como, por exemplo, `"C:\Program Files\nodejs\node.exe" createtable.js`.

## <a name="connect-create-table-and-insert-data"></a>Ligar, criar tabela e inserir dados
Utilize o seguinte código para se ligar e carregar os dados com as instruções SQL **CREATE TABLE** e **INSERT INTO**.

O método [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) é utilizado para fazer a interface com o servidor MySQL. A função [connect()](https://github.com/mysqljs/mysql#establishing-connections) é utilizada para estabelecer a ligação ao servidor. A função [query()](https://github.com/mysqljs/mysql#performing-queries) é utilizada para executar a consulta SQL na base de dados MySQL. 

Substitua os parâmetros `host`, `user`, `password`, e `database` pelos valores que especificou quando criar o servidor e a base de dados.

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
    if (err) { 
        console.log("!!! Cannot connect !!! Error:");
        throw err;
    }
    else
    {
       console.log("Connection established.");
           queryDatabase();
    }   
});

function queryDatabase(){
       conn.query('DROP TABLE IF EXISTS inventory;', function (err, results, fields) { 
            if (err) throw err; 
            console.log('Dropped inventory table if existed.');
        })
       conn.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);', 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Created inventory table.');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['banana', 150], 
            function (err, results, fields) {
                if (err) throw err;
            else console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['orange', 154], 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['apple', 100], 
        function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.end(function (err) { 
        if (err) throw err;
        else  console.log('Done.') 
        });
};
```

## <a name="read-data"></a>Ler dados
Utilize o código seguinte para se ligar e ler dados com uma instrução SQL **SELECT**. 

O método [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) é utilizado para fazer a interface com o servidor MySQL. O método [connect()](https://github.com/mysqljs/mysql#establishing-connections) é utilizado para estabelecer a ligação ao servidor. O método [query()](https://github.com/mysqljs/mysql#performing-queries) é utilizado para executar a consulta SQL na base de dados MySQL. A matriz de resultados é utilizada para armazenar os resultados da consulta.

Substitua os parâmetros `host`, `user`, `password`, e `database` pelos valores que especificou quando criar o servidor e a base de dados.

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            readData();
        }   
    });

function readData(){
        conn.query('SELECT * FROM inventory', 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Selected ' + results.length + ' row(s).');
                for (i = 0; i < results.length; i++) {
                    console.log('Row: ' + JSON.stringify(results[i]));
                }
                console.log('Done.');
            })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Closing connection.') 
        });
};
```

## <a name="update-data"></a>Atualizar dados
Utilize o código seguinte para se ligar e ler os dados com uma instrução SQL **UPDATE**. 

O método [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) é utilizado para fazer a interface com o servidor MySQL. O método [connect()](https://github.com/mysqljs/mysql#establishing-connections) é utilizado para estabelecer a ligação ao servidor. O método [query()](https://github.com/mysqljs/mysql#performing-queries) é utilizado para executar a consulta SQL na base de dados MySQL. 

Substitua os parâmetros `host`, `user`, `password`, e `database` pelos valores que especificou quando criar o servidor e a base de dados.

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            updateData();
        }   
    });

function updateData(){
       conn.query('UPDATE inventory SET quantity = ? WHERE name = ?', [200, 'banana'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Updated ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="delete-data"></a>Eliminar dados
Utilize o código seguinte para se ligar e ler os dados com a instrução SQL **DELETE**. 

O método [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) é utilizado para fazer a interface com o servidor MySQL. O método [connect()](https://github.com/mysqljs/mysql#establishing-connections) é utilizado para estabelecer a ligação ao servidor. O método [query()](https://github.com/mysqljs/mysql#performing-queries) é utilizado para executar a consulta SQL na base de dados MySQL. 

Substitua os parâmetros `host`, `user`, `password`, e `database` pelos valores que especificou quando criar o servidor e a base de dados.

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            deleteData();
        }   
    });

function deleteData(){
       conn.query('DELETE FROM inventory WHERE name = ?', ['orange'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Deleted ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="next-steps"></a>Passos seguintes
> [!div class="nextstepaction"]
> [Migrar a base de dados com Exportar e Importar](./concepts-migrate-import-export.md)
