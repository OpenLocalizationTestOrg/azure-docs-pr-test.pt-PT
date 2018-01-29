---
title: Ligar a Base de Dados do Azure para PostgreSQL com Ruby | Microsoft Docs
description: "Este guia de início rápido fornece um código de exemplo de Ruby que pode utilizar para se ligar e consultar dados da Base de Dados do Azure para PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: ruby
ms.topic: quickstart
ms.date: 11/03/2017
ms.openlocfilehash: 0b8ee73ab86dde2b2c09c9fe2e73209d000b3f26
ms.sourcegitcommit: 38c9176c0c967dd641d3a87d1f9ae53636cf8260
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/06/2017
---
# <a name="azure-database-for-postgresql-use-ruby-to-connect-and-query-data"></a>Base de Dados do Azure para PostgreSQL: utilize o Ruby para ligar e consultar dados
Este início rápido explica como se pode ligar a uma Base de Dados do Azure para PostgreSQL através de uma aplicação [Ruby](https://www.ruby-lang.org). Explica como utilizar as instruções SQL para consultar, inserir, atualizar e eliminar dados da base de dados. Os passos neste artigo pressupõem que está familiarizado com a programação com Ruby e que nunca trabalhou com a Base de Dados do Azure para PostgreSQL.

## <a name="prerequisites"></a>Pré-requisitos
Este guia de início rápido utiliza os recursos criados em qualquer um destes guias como ponto de partida:
- [Criar BD - Portal](quickstart-create-server-database-portal.md)
- [Criar BD - CLI do Azure](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a>Instalar o Ruby
Instale o Ruby no seu próprio computador. 

### <a name="windows"></a>Windows
- Transfira e instale a versão mais recente do [Ruby](http://rubyinstaller.org/downloads/).
- No ecrã de conclusão do instalador MSI, selecione a caixa que diz "Run 'ridk install' to install MSYS2 and development toolchain". Em seguida, clique em **Concluir** para iniciar o instalador seguinte.
- É iniciado o instalador RubyInstaller2 para Windows. Escreva 2 para instalar a atualização do repositório MSYS2. Depois de terminar e regressar à janela de instalação, feche a janela de comando.
- Inicie uma nova linha de comandos (cmd) a partir do menu Iniciar.
- Teste a instalação do Ruby `ruby -v` para ver a versão instalada.
- Teste a instalação do Gem `gem -v` para ver a versão instalada.
- Crie o módulo PostgreSQL para Ruby com Gem ao executar o comando `gem install pg`.

### <a name="macos"></a>MacOS
- Instale o Ruby com Homebrew ao executar o comando `brew install ruby`. Para obter mais opções de instalação, veja a [documentação de instalação](https://www.ruby-lang.org/en/documentation/installation/#homebrew) do Ruby
- Teste a instalação do Ruby `ruby -v` para ver a versão instalada.
- Teste a instalação do Gem `gem -v` para ver a versão instalada.
- Crie o módulo PostgreSQL para Ruby com Gem ao executar o comando `gem install pg`.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Instale o Ruby ao executar o comando `sudo apt-get install ruby-full`. Para obter mais opções de instalação, veja a [documentação de instalação](https://www.ruby-lang.org/en/documentation/installation/) do Ruby.
- Teste a instalação do Ruby `ruby -v` para ver a versão instalada.
- Instale as atualizações mais recentes para Gem ao executar o comando `sudo gem update --system`.
- Teste a instalação do Gem `gem -v` para ver a versão instalada.
- Instale o gcc, make e outras ferramentas de compilação ao executar o comando `sudo apt-get install build-essential`.
- Instale as bibliotecas PostgreSQL ao executar o comando `sudo apt-get install libpq-dev`.
- Crie o módulo Ruby pg com Gem ao executar o comando `sudo gem install pg`.

## <a name="run-ruby-code"></a>Executar código Ruby 
- Guarde o código num ficheiro de texto com a extensão de ficheiro .rb e guarde o ficheiro numa pasta de projeto, como `C:\rubypostgres\read.rb` ou `/home/username/rubypostgres/read.rb`
- Para executar o código, inicie a linha de comandos ou a shell de bash. Altere o diretório para a pasta de projeto `cd rubypostgres` e, em seguida, escreva o comando `ruby read.rb` para executar a aplicação.

## <a name="get-connection-information"></a>Obter informações da ligação
Obtenha as informações de ligação necessárias para se ligar à Base de Dados do Azure para PostgreSQL. Necessita do nome do servidor e das credenciais de início de sessão totalmente qualificados.

1. Inicie sessão no [Portal do Azure](https://portal.azure.com/).
2. No menu esquerdo do portal do Azure, clique em **Todos os recursos** e procure o servidor que acabou de criar, por exemplo, **mypgserver-20170401**.
3. Clique no nome do servidor **mypgserver 20170401**.
4. Selecione a página **Descrição Geral** do servidor. Anote o **Nome do servidor** e **Nome de início de sessão de administrador do servidor**.
 ![Base de Dados do Azure para o PostgreSQL – Início de Sessão de Administrador do Servidor](./media/connect-ruby/1-connection-string.png)
5. Caso se tenha esquecido das informações de início de sessão do seu servidor, navegue até à página **Descrição geral** para visualizar o nome de início de sessão de administrador do Servidor. Se necessário, reponha a palavra-passe.

## <a name="connect-and-create-a-table"></a>Ligar e criar uma tabela
Utilize o código seguinte para ligar e criar uma tabela com a instrução SQL **CREATE TABLE**, seguida das instruções SQL **INSERT INTO** para adicionar linhas à tabela.

O código utiliza um objeto [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) com o construtor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) para se ligar à Base de Dados do Azure para PostgreSQL. Em seguida, chama o método [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) para executar os comandos DROP, CREATE TABLE e INSERT INTO. O código procura erros através da classe [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error). Em seguida, chama o método [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) para fechar a ligação antes de terminar.

Substitua as cadeias `host`, `database`, `user` e `password` pelos seus próprios valores. 
```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection to database'

    # Drop previous table of same name if one exists
    connection.exec('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    connection.exec('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    connection.exec("INSERT INTO inventory VALUES(1, 'banana', 150)")
    connection.exec("INSERT INTO inventory VALUES(2, 'orange', 154)")
    connection.exec("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="read-data"></a>Ler dados
Utilize o código seguinte para se ligar e ler dados com uma instrução SQL **SELECT**. 

O código utiliza um objeto [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) com o construtor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) para se ligar à Base de Dados do Azure para PostgreSQL. Em seguida, chama o método [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) para executar o comando SELECT, mantendo os resultados num conjunto de resultados. A coleção do conjunto de resultados é iterada através do loop `resultSet.each do`, mantendo os valores de linha atuais na variável `row`. O código procura erros através da classe [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error). Em seguida, chama o método [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) para fechar a ligação antes de terminar.

Substitua as cadeias `host`, `database`, `user` e `password` pelos seus próprios valores. 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :database => dbname, :port => '5432', :password => password)
    puts 'Successfully created connection to database.'

    resultSet = connection.exec('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="update-data"></a>Atualizar dados
Utilize o código seguinte para se ligar e atualizar os dados com uma instrução SQL **UPDATE**.

O código utiliza um objeto [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) com o construtor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) para se ligar à Base de Dados do Azure para PostgreSQL. Em seguida, chama o método [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) para executar o comando UPDATE. O código procura erros através da classe [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error). Em seguida, chama o método [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) para fechar a ligação antes de terminar.

Substitua as cadeias `host`, `database`, `user` e `password` pelos seus próprios valores. 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection to database.'

    # Modify some data in table.
    connection.exec('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
    puts 'Updated 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```


## <a name="delete-data"></a>Eliminar dados
Utilize o código seguinte para se ligar e ler os dados com uma instrução SQL **DELETE**. 

O código utiliza um objeto [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) com o construtor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) para se ligar à Base de Dados do Azure para PostgreSQL. Em seguida, chama o método [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) para executar o comando UPDATE. O código procura erros através da classe [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error). Em seguida, chama o método [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) para fechar a ligação antes de terminar.

Substitua as cadeias `host`, `database`, `user` e `password` pelos seus próprios valores. 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection to database.'

    # Modify some data in table.
    connection.exec('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="next-steps"></a>Passos seguintes
> [!div class="nextstepaction"]
> [Migrar a base de dados com Exportar e Importar](./howto-migrate-using-export-and-import.md)
