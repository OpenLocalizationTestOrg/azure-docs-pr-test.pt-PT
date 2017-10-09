<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> Quando efetuar alterações toohello adaptador StorSimple para a configuração do SharePoint RBS, tem de ser sessão iniciada com uma conta de utilizador que pertence toohello grupo Admins do domínio. Além disso, tem de aceder a página de configuração de Olá num browser em execução no Olá mesmo anfitrião como Administração Central.
> 
> 

#### <a name="tooconfigure-rbs"></a>tooconfigure RBS
1. Abra a página de Administração Central do SharePoint Olá e procurar demasiado**definições do sistema**. 
2. No Olá **Azure StorSimple** secção, clique em **configurar adaptador do StorSimple**.
   
    ![Configurar Olá adaptador do StorSimple](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. No Olá **configurar adaptador do StorSimple** página:
   
   1. Certifique-se de que Olá **ativar caminho edição** caixa de verificação está selecionada.
   2. Na caixa de texto Olá, escreva o caminho de convenção de Nomenclatura Universal (UNC) Olá do arquivo de BLOB Olá.
      
      > [!NOTE]
      > volume de arquivo BLOB Olá tem de estar alojado num volume iSCSI configurado no dispositivo StorSimple de Olá.

   3. Clique em Olá **ativar** no botão abaixo cada Olá conteúdo bases de dados que pretende que tooconfigure para armazenamento remoto.
      
      > [!NOTE]
      > arquivo de BLOB Olá tem de ser partilhados e pode ser acedida por todos os servidores (WFE) front-end web e conta de utilizador de Olá que está configurada para o farm de servidores do SharePoint Olá tem de ter a partilha de toohello de acesso.
      
      ![Ativar Olá RBS fornecedor](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      Quando ativar ou desativar RBS, também verá Olá seguir a mensagem.
      
      ![Configurar StorSimple adaptador Ativar desativar](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. Clique em Olá **atualização** configuração de Olá tooapply do botão. Ao clicar em Olá **atualização** botão, Olá estado da configuração RBS será atualizada em todos os servidores WFE, e todo o farm Olá serão RBS-ativado. Olá seguir a mensagem é apresentada.
      
      ![Mensagem de configuração do adaptador](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > Se estiver a configurar RBS para um farm do SharePoint com um número muito elevado de bases de dados (superior a 200), página de web de Administração Central do SharePoint Olá poderá tempo limite. Se isso ocorrer, atualize a página Olá. Isto não afeta o processo de configuração de Olá.

4. Verifique a configuração de Olá:
   
   1. Inicie sessão no Web site de Administração Central do SharePoint toohello e procurar toohello **configurar adaptador do StorSimple** página.
   2. Verifique toomake de detalhes de configuração de Olá certificar-se de que correspondem à definições Olá que introduziu. 
5. Certifique-se de que RBS funciona corretamente:
   
   1. Carregar um tooSharePoint do documento. 
   2. Procure o caminho UNC toohello que configurou. Certifique-se de que a estrutura de diretórios do Olá RBS foi criada e que contém o objeto de Olá carregado.
6. (Opcional) Pode utilizar Olá Microsoft RBS `Migrate()` cmdlet do PowerShell incluído com o SharePoint toomigrate existente BLOB toohello conteúdo dispositivo StorSimple. Para obter mais informações, consulte [migrar conteúdo ou a sair RBS no SharePoint 2013] [ 6] ou [migrar conteúdo ou a sair RBS (SharePoint Foundation 2010)] [7].
7. (Opcional) Nas instalações de teste, pode verificar que Olá BLOBs foram movidos fora da base de dados conteúdo Olá, da seguinte forma: 
   
   1. Inicie o SQL Server Management Studio.
   2. Execute consulta ListBlobsInDB_2010.sql ou ListBlobsInDB_2013.sql Olá, da seguinte forma.
      
      ```
      **ListBlobsInDB_2013.sql**
      
        USE WSS_Content
        GO
      
        SELECT DocStreams.DocId,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               DocStreams.RbsId,
               TimeLastModified
      
        FROM DocStreams
      
             INNER JOIN AllDocs ON DocStreams.DocId = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      
      **ListBlobsInDB_2010.sql**
      
        USE WSS_Content
        GO
      
        SELECT AllDocStreams.Id,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               RbsId,
               TimeLastModified
        FROM AllDocStreams
      
             INNER JOIN AllDocs ON AllDocStreams.Id = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      ```
      
      Se RBS foi configurada corretamente, deverá aparecer um valor nulo na coluna de SizeOfContentInDB Olá para qualquer objeto que foi carregada e externalized com êxito com RBS.
8. (Opcional) Depois de configurar RBS e mover todos os BLOBS conteúdo toohello dispositivo StorSimple, pode mover o dispositivo de toohello Olá conteúdo da base de dados. Se escolher toomove Olá conteúdo da base de dados, recomendamos que configurar o armazenamento de base de dados de conteúdo de Olá no dispositivo Olá como um volume primário. Em seguida, utilize estabelecida que do SQL Server melhores práticas de dispositivo do StorSimple toohello toomigrate Olá conteúdo da base de dados. 
   
   > [!NOTE]
   > Dispositivo de toohello de base de dados de conteúdo Olá mover só é suportado para a série 8000 do StorSimple de Olá (que não é suportado para a série de Olá 5000 ou 7000).
   
   Se armazenar os BLOBs e base de dados de conteúdo Olá em volumes separados no dispositivo do StorSimple Olá, recomendamos que configurar no Olá mesmo contentor de volume. Isto garante que estes irão ser copiados em segurança em conjunto.
   
   > [!WARNING]
   > Se não tiver ativado RBS, não recomendamos mover o dispositivo StorSimple de toohello à base de dados de conteúdo Olá. Esta é uma configuração untested.
   
9. Aceda toohello próximo passo: [configurar recolha de lixo](#configure-garbage-collection).

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
