<!--author=SharS last changed: 9/17/15-->

### <a name="upgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-storsomple-adapter-for-sharepoint"></a>Atualizar tooSharePoint 2010 do SharePoint 2013 e, em seguida, instalar Olá StorSomple adaptador para o SharePoint
> [!IMPORTANT]
> Quaisquer ficheiros que foram anteriormente movidos tooexternal armazenamento através de RBS não estarão disponível até que Olá atualização estiver concluída e Olá funcionalidade RBS seja ativada de novo. utilizador toolimit afeta, executar qualquer atualização ou reinstalação durante uma janela de manutenção planeada.
> 
> 

#### <a name="tooupgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-adapter"></a>tooSharePoint tooupgrade 2010 do SharePoint 2013 e, em seguida, instalar Olá adaptador
1. No farm do SharePoint 2010 de Olá nota Olá BLOB armazenar o caminho para Olá externalized BLOBs Olá conteúdo bases de dados e para o qual RBS está ativada. 
2. Instalar e configurar o farm do SharePoint 2013 novo Olá. 
3. Mova bases de dados, aplicações e coleções de sites do farm do SharePoint 2013 Olá SharePoint 2010 farm toohello novo. Para obter instruções, aceda demasiado[descrição geral do processo de atualização de Olá tooSharePoint 2013](https://technet.microsoft.com/library/cc262483.aspx).
4. Instale Olá StorSimple adaptador para o SharePoint no farm Olá de novo. Aceda demasiado[Olá instalar adaptador StorSimple para SharePoint](#install-the-storsimple-adapter-for-sharepoint) para obter os procedimentos.
5. Utilização de informações de Olá que anotou no passo 1, ative RBS para Olá mesmo conjunto de bases de dados de conteúdos e fornecer Olá BLOB mesmo armazenar caminho que utilizou na instalação Olá SharePoint 2010. Aceda demasiado[configurar RBS](#configure-rbs) para obter os procedimentos. Depois de concluir este passo, os ficheiros anteriormente externalized devem ser acessíveis a partir do novo farm de Olá. 

### <a name="upgrade-hello-storsimple-adapter-for-sharepoint"></a>Atualizar Olá StorSimple adaptador para o SharePoint
> [!IMPORTANT]
> Deve agendar esta atualização toooccur durante uma janela de manutenção planeada para Olá seguintes motivos:
> 
> * Anteriormente conteúdo externalized não estarão disponível até que o adaptador de Olá será reinstalado.
> * Todos os conteúdos carregados toohello site após a desinstalação da versão anterior do Olá do Olá StorSimple adaptador para o SharePoint, mas antes de instalar a nova versão Olá, serão armazenados na base de dados de conteúdo Olá. Terá de toomove que o dispositivo StorSimple toohello conteúdo depois de instalar novo adaptador de Olá. Pode utilizar Olá Microsoft` RBS Migrate()` cmdlet do PowerShell incluído com o conteúdo do SharePoint toomigrate Olá. Para obter mais informações, consulte [migrar conteúdo ou a sair RBS](https://technet.microsoft.com/library/ff628255.aspx). 
> 
> 

#### <a name="tooupgrade-hello-storsimple-adapter-for-sharepoint"></a>Olá tooupgrade StorSimple adaptador para o SharePoint
1. Desinstale a versão anterior do Olá do StorSimple adaptador para o SharePoint.
   
   > [!NOTE]
   > Isto desativará RBS automaticamente em bases de dados de conteúdo Olá. No entanto, os BLOBs existentes permanecem no dispositivo do StorSimple Olá. Uma vez RBS está desativada e Olá BLOBs não foram migrados toohello back conteúdo bases de dados, todos os pedidos para os BLOBs irão falhar. 
   > 
   > 
2. Instalação hello novo adaptador StorSimple para SharePoint. nova placa de Olá automaticamente reconhecerá Olá conteúdo bases de dados que foram anteriormente ativados ou desativados para RBS e irão utilizar definições anteriores Olá.

