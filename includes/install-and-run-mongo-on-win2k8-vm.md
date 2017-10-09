Siga estes passos tooinstall e execute o MongoDB numa máquina virtual com o Windows Server.

> [!IMPORTANT]
> Funcionalidades de segurança do MongoDB, como a autenticação e o enlace de endereço IP, não estão ativadas por predefinição. Funcionalidades de segurança devem ser ativadas antes de implementar o ambiente de produção do MongoDB tooa.  Para obter mais informações, consulte [segurança e autenticação](http://www.mongodb.org/display/DOCS/Security+and+Authentication).
>
>

1. Depois de se ligar máquinas toohello utilizando o ambiente de trabalho remoto, abra o Internet Explorer de Olá **iniciar** menu na máquina virtual de Olá.
2. Selecione Olá **ferramentas** botão no canto superior direito Olá.  No **opções da Internet**, selecione Olá **segurança** separador e, em seguida, selecione Olá **Sites fidedignos** ícone e, finalmente, clique em Olá **Sites** botão. Adicionar *https://\*. mongodb.org* toohello lista de sites fidedignos.
3. Aceda demasiado[transfere - MongoDB](https://www.mongodb.com/download-center#community).
4. Determinar Olá **atual versão estável** de **Comunidade servidor**, selecione hello mais recente **64-bit** versão na coluna de Windows hello. Transferir e, em seguida, execute o instalador do MSI Olá.
5. MongoDB é normalmente instalado na c:\Programas\Microsoft Files\MongoDB. Procure as variáveis de ambiente no ambiente de trabalho Olá e adicione a variável de caminho de toohello binários caminho Olá MongoDB. Por exemplo, poderá determinar os binários de Olá em c:\Programas\Microsoft Files\MongoDB\Server\3.4\bin no seu computador.
6. Criar os diretórios de dados e de registo do MongoDB no disco de dados de Olá (tais como unidade **f:**) que criou no Olá precedente passos. De **iniciar**, selecione **linha de comandos** tooopen uma janela de linha de comandos.  Escreva:

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. toorun Olá base de dados, execute:

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    Todas as mensagens de registo são direcionado toohello *F:\MongoLogs\mongolog.log* de ficheiros mongod.exe servidor é iniciado e preallocates ficheiros do diário. Pode demorar alguns minutos para MongoDB toopreallocate ficheiros do diário Olá e começar a escutar ligações. linha de comandos Olá permanece direcionada para esta tarefa enquanto a instância do MongoDB está em execução.
8. Olá toostart shell administrativa do MongoDB, abrir outra janela de comando de **iniciar** e Olá tipo os seguintes comandos:

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    base de dados de Olá é criado pelo Olá insert.
9. Em alternativa, pode instalar mongod.exe como um serviço:

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    Um serviço é instalado com o nome MongoDB com uma descrição do "BD de Mongo". Olá `--logpath` opção tem de ser toospecify utilizado um ficheiro de registo, desde Olá a executar o serviço não tem uma saída de toodisplay de janela de comando.  Olá `--logappend` opção especifica que um reinício do serviço de Olá provoca o ficheiro de registo saída tooappend toohello existente.  Olá `--dbpath` opção especifica a localização de Olá do diretório de dados de Olá. Para mais relacionados com o serviço opções da linha de comandos, consulte [relacionados com o serviço opções da linha de comandos][MongoWindowsSvcOptions].

    no serviço de Olá toostart, execute este comando:

        C:\> net start MongoDB
10. Agora que MongoDB está instalado e em execução, terá de tooopen uma porta na Firewall do Windows para que as possa remotamente ligar tooMongoDB.  De Olá **iniciar** menu, selecione **ferramentas administrativas** e, em seguida, **Firewall do Windows com segurança avançada**.
11. a) no painel esquerdo Olá, selecione **regras de entrada**.  No Olá **ações** painel Olá direito, selecione **nova regra...** .

    ![Firewall do Windows][Image1]

    b) na Olá **novo Assistente de regras de entrada**, selecione **porta** e, em seguida, clique em **seguinte**.

    ![Firewall do Windows][Image2]

    c) selecione **TCP** e, em seguida, **portas locais específicas**.  Especifique uma porta de "27017" (porta de predefinição Olá MongoDB escuta) e clique em **seguinte**.

    ![Firewall do Windows][Image3]

    d) selecione **permitir ligação Olá** e clique em **seguinte**.

    ![Firewall do Windows][Image4]

    i) clique em **seguinte** novamente.

    ![Firewall do Windows][Image5]

    f) Especifique um nome para a regra de Olá, tal como "MongoPort" e clique em **concluir**.

    ![Firewall do Windows][Image6]

12. Se não configurar um ponto final para o MongoDB quando criou a máquina virtual de Olá, pode fazê-lo agora. Terá de regra de firewall de Olá e Olá endpoint toobe tooconnect capaz de tooMongoDB remotamente.

  No portal do Azure Olá, clique em **máquinas virtuais (clássicas)**, clique no nome de Olá da nova máquina virtual e, em seguida, clique em **pontos finais**.

    ![Pontos Finais][Image7]

13. Clique em **Adicionar**.

14. Adicionar um ponto final com o nome "Mongo" protocolo **TCP**e ambos **pública** e **privada** portas definido demasiado "27017". Abrir esta porta permite toobe MongoDB acedida remotamente.

    ![Pontos Finais][Image9]

> [!NOTE]
> porta Olá 27017 é Olá predefinido porta é utilizada por MongoDB. Pode alterar esta porta predefinida, especificando Olá `--port` parâmetro ao iniciar o servidor de mongod.exe Olá. Certifique-se de que toogive Olá o mesmo número de porta na firewall de Olá e Olá "Mongo" ponto final no Olá precedente instruções.
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png
