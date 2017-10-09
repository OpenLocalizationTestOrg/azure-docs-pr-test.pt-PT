### <a name="install-via-composer"></a><span data-ttu-id="64f31-101">Instalar através do compositor</span><span class="sxs-lookup"><span data-stu-id="64f31-101">Install via Composer</span></span>
1. <span data-ttu-id="64f31-102">[Instalar o Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="64f31-102">[Install Git][install-git].</span></span> <span data-ttu-id="64f31-103">Tenha em atenção que no Windows, tem também de adicionar variável de ambiente PATH do Olá Git tooyour executável.</span><span class="sxs-lookup"><span data-stu-id="64f31-103">Note that on Windows, you must also add hello Git executable tooyour PATH environment variable.</span></span> 
2. <span data-ttu-id="64f31-104">Crie um ficheiro denominado **Composer** no Olá raiz do projeto e adicione Olá tooit de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="64f31-104">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. <span data-ttu-id="64f31-105">Transferir  **[composer.phar] [ composer-phar]**  na raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="64f31-105">Download **[composer.phar][composer-phar]** in your project root.</span></span>
4. <span data-ttu-id="64f31-106">Abra uma linha de comandos e execute o seguinte comando na raiz do projeto de Olá</span><span class="sxs-lookup"><span data-stu-id="64f31-106">Open a command prompt and execute hello following command in your project root</span></span>
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
