### <a name="install-via-composer"></a>Instalar através do compositor
1. [Instalar o Git][install-git]. Tenha em atenção que no Windows, tem também de adicionar variável de ambiente PATH do Olá Git tooyour executável. 
2. Crie um ficheiro denominado **Composer** no Olá raiz do projeto e adicione Olá tooit de código a seguir:
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. Transferir  **[composer.phar] [ composer-phar]**  na raiz do projeto.
4. Abra uma linha de comandos e execute o seguinte comando na raiz do projeto de Olá
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
