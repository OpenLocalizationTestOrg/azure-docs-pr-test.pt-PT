
1. privilégios tooescalate, tipo:
   
        sudo -s
   
    Introduza a sua palavra-passe.
2. tooinstall edição de servidor de Comunidade do MySQL, escreva:
   
        zypper install mysql-community-server
   
    Aguarde enquanto o MySQL transfere e instala.
3. tooset MySQL toostart quando inicia o sistema de Olá, escreva:
   
        insserv mysql
4. Inicie manualmente o daemon de MySQL Olá (mysqld) com este comando:
   
        rcmysql start
   
    Estado de Olá toocheck de Olá MySQL daemon, escreva:
   
        rcmysql status
   
    Olá toostop MySQL daemon, escreva:
   
        rcmysql stop
   
   > [!IMPORTANT]
   > Após a instalação, a palavra-passe de raiz do Olá MySQL está vazio por predefinição. Recomendamos que execute **mysql\_segura\_instalação**, um script que ajuda a proteger MySQL. script de Olá solicita a sua palavra-passe de raiz de toochange Olá MySQL, remova contas de utilizador anónimo, desativar inícios de sessão remoto raiz, remover bases de dados de teste e recarregar a tabela de privilégios Olá. Recomendamos que responder Sim tooall destas opções e altere a palavra-passe de raiz de Olá.
   > 
   > 
5. Escreva este script de Olá toorun MySQL script de instalação:
   
        mysql_secure_installation
6. Inicie sessão no tooMySQL:
   
        mysql -u root -p
   
    Introduza Olá MySQL palavra-passe raiz (o que mudou no passo anterior Olá) e irá ser apresentado numa linha de onde pode emitir toointeract de declarações do SQL Server com a base de dados de Olá.
7. toocreate um novo utilizador MySQL, executar Olá seguinte Olá **mysql >** linha:
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    Tenha em atenção, ponto e vírgula do Olá (;) no fim de Olá do Olá linhas são cruciais para comandos Olá a terminar.
8. toocreate Olá uma base de dados e conceder `mysqluser` permissões de utilizador no mesmo, Olá problema os seguintes comandos:
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    Tenha em atenção que os nomes de utilizador de base de dados e as palavras-passe só são utilizadas pelos scripts ligar toohello base de dados.  Os nomes das contas de utilizador de base de dados não representa necessariamente contas de utilizador real no sistema de Olá.
9. toolog na partir de outro computador, tipo:
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    onde `ip-address` é Olá o endereço IP do computador Olá partir do qual irá ligar tooMySQL.
10. Olá tooexit utilitário de administração de base de dados MySQL, escreva:
    
        quit

## <a name="add-an-endpoint"></a>Adicionar um ponto final
1. Depois de instalado o MySQL, terá de remotamente tooconfigure tooaccess um ponto final MySQL. Inicie sessão no toohello [portal clássico do Azure][AzurePortal]. Clique em **máquinas virtuais**, clique no nome de Olá da nova máquina virtual e, em seguida, clique em **pontos finais**.
2. Clique em **adicionar** em Olá parte inferior da página Olá.
3. Adicionar um ponto final com o nome "MySQL" com o protocolo **TCP**, e **pública** e **privada** portas definido demasiado "3306".
4. tooremotely ligar a máquina virtual de toohello do seu computador, o tipo:
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    Por exemplo, se utilizar Olá virual máquina que foi criada neste tutorial, escreva este comando:
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
