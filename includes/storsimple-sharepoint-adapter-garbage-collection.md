<!--author=SharS last changed: 9/17/15-->

Neste procedimento, irá:

1. [Preparar o executável do toorun Olá responsável pela manutenção](#to-prepare-to-run-the-maintainer) .
2. [Preparar a base de dados de conteúdo Olá e a Reciclagem para eliminação imediata de BLOBs órfãos](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).
3. [Executar Maintainer.exe](#to-run-the-maintainer).
4. [Reverter a base de dados de conteúdo de Olá e definições de reciclagem](#to-revert-the-content-database-and-recycle-bin-settings).

#### <a name="tooprepare-toorun-hello-maintainer"></a>tooprepare toorun Olá responsável pela manutenção
1. No servidor de front-end Web Olá, abra Olá Shell de gestão do SharePoint 2013 como administrador.
2. Navegue toohello pasta *unidade de arranque*: \Programas\Microsoft SQL remoto Blob Storage 10.50\Maintainer\.
3. Mudar o nome **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** demasiado**Web. config**.
4. Utilize `aspnet_regiis -pdf connectionStrings` ficheiro do toodecrypt Olá Web. config.
5. No ficheiro Web. config desencriptada de Olá, em Olá `connectionStrings` nós, adicionar Olá a cadeia de ligação para a instância do SQL server e Olá nome de base de dados de conteúdo. Consulte o seguinte exemplo de Olá.
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. Utilize `aspnet_regiis –pef connectionStrings` toore-encriptar o ficheiro Web. config de Olá. 
7. Mudar o nome tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config Web. config. 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a>tooprepare Olá conteúdo da base de dados e reciclagem tooimmediately eliminar BLOBs órfãos
1. No Olá do SQL Server, no SQL Server Management Studio, execute Olá seguintes consultas de atualização de base de dados conteúdo Olá destino: 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. No Olá front-end servidor web, em **Administração Central**, editar Olá **definições gerais de aplicação Web** para Olá pretendido Olá de desativação do conteúdo da base de dados tootemporarily Reciclagem. Esta ação irá também vazio Olá Reciclagem qualquer relacionados para coleções de sites. toodo, clique em **Administração Central** -> **gestão de aplicações** -> **aplicações Web (gerir web Apps)**  ->  **SharePoint - 80** -> **definições de aplicações gerais**. Conjunto Olá **reciclar o estado de reciclagem** demasiado**OFF**.
   
    ![Definições gerais de aplicação Web](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a>Olá toorun responsável pela manutenção
* No servidor de front-end web Olá, na Olá Shell de gestão do SharePoint 2013, execute Olá responsável pela manutenção da seguinte forma:
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > Apenas Olá `GarbageCollection` operação é suportada para StorSimple neste momento. Note também que os parâmetros de Olá emitidos para Microsoft.Data.SqlRemoteBlobs.Maintainer.exe são sensíveis a maiúsculas e minúsculas. 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a>toorevert Olá conteúdo da base de dados e definições de reciclagem
1. No Olá do SQL Server, no SQL Server Management Studio, execute Olá seguintes consultas de atualização de base de dados conteúdo Olá destino:
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. No servidor de front-end web Olá, no **Administração Central**, editar Olá **definições gerais de aplicação Web** para Olá pretendido Olá toore ativar do conteúdo da base de dados da Reciclagem. toodo, clique em **Administração Central** -> **gestão de aplicações** -> **aplicações Web (gerir web Apps)**  ->  **SharePoint - 80** -> **definições de aplicações gerais**. Definir Olá reciclar o estado de reciclagem demasiado**ON**.

