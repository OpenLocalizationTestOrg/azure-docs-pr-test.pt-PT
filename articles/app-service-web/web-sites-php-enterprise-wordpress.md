---
title: classe de aaaEnterprise WordPress no Azure | Microsoft Docs
description: Saiba como toohost WordPress uma classe de enterprise site no App Service do Azure
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 22d68588-2511-4600-8527-c518fede8978
ms.service: app-service-web
ms.devlang: php
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 4347eddb31d622d1189dc5db4d81b0f3745d6e69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-class-wordpress-on-azure"></a>Classe de Enterprise WordPress no Azure
App Service do Azure fornece um ambiente escalável, seguro e fácil de utilizar para fundamentais, em grande escala [WordPress] [ wordpress] sites. Microsoft próprio executa sites de classe empresarial como Olá [Office] [ officeblog] e [Bing] [ bingblog] blogues. Este artigo mostra-lhe como toouse Olá funcionalidade Web Apps do App Service do Microsoft Azure tooestablish e manter uma classe de enterprise, o site do WordPress baseado na nuvem que pode processar um grande volume de visitantes.

## <a name="architecture-and-planning"></a>Planeamento e arquitetura
Uma instalação de WordPress básica tem apenas dois requisitos:

* **Base de dados MySQL**: Este requisito está disponível através do [ClearDB no Olá Azure Marketplace][cdbnstore]. Como alternativa, pode gerir a seus próprios instalação MySQL em Azure Virtual Machines utilizando [Windows] [ mysqlwindows] ou [Linux][mysqllinux].

  > [!NOTE]
  > ClearDB fornece várias configurações MySQL. Cada configuração tem características de desempenho diferentes. Consulte Olá [arquivo Azure] [ cdbnstore] para obter informações sobre as ofertas que são fornecidos através de Olá Azure Store ou diretamente visto no Olá [ClearDB site](http://www.cleardb.com/pricing.view).
  >
  >
* **PHP 5.2.4 ou superior**: App Service do Azure fornece atualmente [versões do PHP 5.4, 5.5 e 5.6][phpwebsite].

  > [!NOTE]
  > Recomendamos que Olá sempre execução mais recente versão do PHP para que tenham correções de segurança mais recentes Olá.
  >
  >

### <a name="basic-deployment"></a>Implementação básica
Se utilizar apenas Olá requisitos básicos, pode criar uma solução básica de dentro de uma região do Azure.

![Uma aplicação web do Azure e a base de dados MySQL alojado numa única região do Azure][basic-diagram]

Apesar de Isto iria permitem criar várias instâncias de aplicações Web de Olá site tooscale horizontalmente a aplicação, tudo está alojado num Olá centros de dados numa região geográfica específica. Visitantes a partir de fora desta região de poderão ver os tempos de resposta lento quando utilizarem o site de Olá. Se Olá centros de dados nesta região ficarem inativos, por isso, não a aplicação.

### <a name="multi-region-deployment"></a>Implementação de multirregião
Ao utilizar o Azure [Gestor de tráfego][trafficmanager], pode dimensionar o seu site WordPress em várias regiões geográficas e fornecer hello mesmo URL para todos os visitantes. Todos os visitantes vêm num através do Gestor de tráfego e não estão Olá, região tooa encaminhado com base na configuração de balanceamento de carga.

![Uma aplicação web do Azure, alojada em várias regiões, com disponibilidade elevada CDBR router tooroute tooMySQL em regiões][multi-region-diagram]

Cada região, site do WordPress Olá seria ainda ser ampliada em múltiplas instâncias de aplicações Web, mas este dimensionamento é tooa específico de região. Regiões de tráfego elevado e regiões de baixo tráfego podem ser ampliadas diferente.

tooreplicate e encaminhar tráfego toomultiple MySQL bases de dados, pode utilizar [ClearDB routers de elevada disponibilidade (CDBRs)] [ cleardbscale] (mostrado esquerda) ou [MySQL Cluster operadora nível Edition (CGE)] [cge].

### <a name="multi-region-deployment-with-media-storage-and-caching"></a>Implementação de multirregião com armazenamento de suporte de dados e a colocação em cache
Se o site de Olá aceita carregamentos ou ficheiros de suporte de dados de anfitriões, utilize o Blob storage do Azure. Se precisar de colocação em cache, considere [a cache de Redis][rediscache], [Memcache nuvem](http://azure.microsoft.com/gallery/store/garantiadata/memcached/), [MemCachier](http://azure.microsoft.com/gallery/store/memcachier/memcachier/), ou um dos Olá outras ofertas de colocação em cache no Olá [Arquivo azure](http://azure.microsoft.com/gallery/store/).

![Uma aplicação web do Azure, alojada em várias regiões, com o router CDBR elevada disponibilidade para MySQL, com a Cache geridos, de armazenamento de BLOBs e de rede de entrega de conteúdos][performance-diagram]

O blob storage é geo-distribuição em regiões por predefinição, pelo que não tem tooworry sobre replicar os ficheiros em todos os sites. Também pode ativar Olá Azure [rede de entrega de conteúdos] [ cdn] para o Blob storage, que distribui ficheiros tooend nós próximo tooyour visitantes.

### <a name="planning"></a>Planeamento
#### <a name="additional-requirements"></a>Requisitos adicionais
| toodo isto... | Utilize... |
| --- | --- |
| **Carregar ou armazenar ficheiros grandes** |[Plug-in do WordPress para utilizando o Blob storage][storageplugin] |
| **Enviar correio eletrónico** |[SendGrid] [ storesendgrid] e Olá [Plug-in do WordPress, para utilizar SendGrid][sendgridplugin] |
| **Nomes de domínio personalizados** |[Configurar um nome de domínio personalizado no App Service do Azure][customdomain] |
| **HTTPS** |[Ativar HTTPS para uma aplicação web no App Service do Azure][httpscustomdomain] |
| **Validação de pré-produção** |[Configurar ambientes para web apps no App Service do Azure de teste][staging] <p>Quando move uma aplicação web de transição tooproduction, também mover configuração de WordPress Olá. Certifique-se de que todas as definições são atualizadas toohello requisitos para a sua aplicação de produção antes de mover tooproduction de aplicação Olá pré-configurados.</p> |
| **Monitorização e resolução de problemas** |[Ativar o registo de diagnóstico para web apps no App Service do Azure] [ log] e [Monitor Web Apps no App Service do Azure][monitor] |
| **Implementar o site** |[Implementar uma aplicação web no App Service do Azure][deploy] |

#### <a name="availability-and-disaster-recovery"></a>Disponibilidade e recuperação após desastre
| toodo isto... | Utilize... |
| --- | --- |
| **Sites de balanceamento de carga** ou **georreplicação-distribuir sites** |[Encaminhar o tráfego com o Gestor de tráfego do Azure][trafficmanager] |
| **Criar cópias de segurança e restauro** |[Cópia de segurança numa aplicação web no App Service do Azure] [ backup] e [restaurar uma aplicação web no App Service do Azure][restore] |

#### <a name="performance"></a>Desempenho
Desempenho na nuvem de Olá é conseguido principalmente através da colocação em cache e escalável. No entanto, Olá memória, largura de banda e outros atributos de alojamento de aplicações Web devem ser considerados.

| toodo isto... | Utilize... |
| --- | --- |
| **Compreender as capacidades de instância de serviço de aplicações** |[Detalhes dos preços, incluindo as capacidades de camadas de serviço de aplicações][websitepricing] |
| **Recursos de cache** |[A cache de redis][rediscache], [Memcache nuvem](/gallery/store/garantiadata/memcached/), [MemCachier](/gallery/store/memcachier/memcachier/), ou um dos Olá outras ofertas de colocação em cache no Olá [loja do Azure](/gallery/store/) |
| **Dimensionar a sua aplicação** |[Dimensionar a uma aplicação web no App Service do Azure] [ websitescale] e [ClearDB elevada disponibilidade encaminhamento][cleardbscale]. Se escolher toohost e gerir a seus próprios instalação MySQL, deve considerar [MySQL Cluster CGE] [ cge] de escalamento horizontal. |

#### <a name="migration"></a>Migração
Existem dois métodos toomigrate um existente tooAzure de site do WordPress do serviço de aplicações:

* **[Exportar WordPress][export]**: Este método exporta conteúdo Olá do seu blogue. Em seguida, pode importar Olá tooa conteúdo novo site do WordPress no App Service do Azure utilizando Olá [Plug-in do WordPress importador][import].

  > [!NOTE]
  > Durante este processo permite-lhe migrar o seu conteúdo, não consegue migrar qualquer plug-ins, temas ou outras personalizações. Tem de instalar novamente manualmente estes componentes.
  >
  >
* **Migração manual**: [cópia de segurança do site] [ wordpressbackup] e [base de dados][wordpressdbbackup]e, em seguida, manualmente restaurá-lo tooa web aplicação no Azure Serviço de aplicações e a base de dados MySQL associada. Este método é útil toomigrate altamente personalizado sites porque evita tedium Olá de instalar manualmente o plug-ins, temas e outras personalizações.

## <a name="step-by-step-instructions"></a>Instruções passo a passo
### <a name="create-a-wordpress-site"></a>Criar um site do WordPress
1. Olá utilize [Azure Marketplace] [ cdbnstore] toocreate uma base de dados MySQL do tamanho de Olá que identificou nas Olá [planeamento e arquitetura](#planning) secção região Olá ou regiões em que irá alojar o seu site.
2. Siga os passos Olá [criar uma aplicação web WordPress no App Service do Azure] [ createwordpress] toocreate uma aplicação web WordPress. Quando cria Olá web app, selecione **utilizar uma base de dados MySQL existente**e, em seguida, selecione a base de dados de Olá que criou no passo 1.

Se estiver a migrar um site existente do WordPress, consulte o artigo [migrar uma existente tooAzure de site do WordPress](#Migrate-an-existing-WordPress-site-to-Azure) depois de criar uma nova aplicação web.

### <a name="migrate-an-existing-wordpress-site-tooazure"></a>Migrar uma existente tooAzure de site do WordPress
Tal como mencionado na Olá [planeamento e arquitetura](#planning) secção, existem duas formas toomigrate um site WordPress:

* **Utilizar a exportação e importação** para sites que não tem muito personalização ou onde pretende o conteúdo de Olá toomove.
* **Cópia de segurança de utilização e de restauro** para sites que tenham uma grande quantidade de personalização onde pretende toomove tudo.

Utilize um dos Olá toomigrate secções a seguir o seu site.

#### <a name="hello-export-and-import-method"></a>Olá exportar e importar o método
1. Utilize [WordPress exportar] [ export] tooexport existentes do site.
2. Criar uma aplicação web, utilizando os passos de Olá no Olá [criar um site WordPress](#Create-a-new-WordPress-site) secção.
3. Inicie sessão no site do WordPress tooyour no Olá [portal do Azure][mgmtportal]e, em seguida, clique em **plug-ins** > **adicionar novo**. Procurar e instalar Olá **WordPress importador** Plug-in.
4. Depois de instalar Olá Plug-in do importador do WordPress, clique em **ferramentas** > **importação**e, em seguida, clique em **WordPress** toouse Olá Plug-in do WordPress importador.
5. No Olá **importação WordPress** página, clique em **Escolher ficheiro**. Localizar o ficheiro WXR Olá que foi exportado a partir do seu site WordPress existente e, em seguida, clique em **ficheiros de carregamento e importar**.
6. Clique em **submeter**. É-lhe pedido que a importação de Olá foi concluída com êxito.
7. Depois de concluir todos estes passos, reinicie o seu site a partir da respetiva **serviços aplicacionais** painel no Olá [portal do Azure][mgmtportal].

Depois de importar site Olá, poderá ser necessário Olá tooperform seguintes definições de tooenable de passos que não estão no ficheiro de importação de Olá.

| Se estava a utilizar isto... | Ao fazê-lo... |
| --- | --- |
| **Permalinks** |No dashboard do WordPress Olá do novo site de Olá, clique em **definições** > **Permalinks**e, em seguida, atualize a estrutura de Permalinks Olá. |
| **ligações de imagem/suporte de dados** |tooupdate ligações toohello nova localização, utilize Olá [Plug-in do Velvet Blues atualizar URLs][velvet], uma pesquisa e substitua ferramenta ou atualizar manualmente as ligações de Olá na base de dados. |
| **Temas** |Aceda demasiado**aspeto** > **tema**e, em seguida, atualizar tema de site Olá conforme necessário. |
| **Menus** |Se o tema suporta menus, home page do ligações tooyour ter subdiretório antigo Olá incorporado nos mesmos. Aceda demasiado**aspeto** > **Menus**e, em seguida, atualizá-las. |

#### <a name="hello-backup-and-restore-method"></a>Olá cópia de segurança e restaurar o método
1. Cópia de segurança do WordPress existentes do site através da utilização de informações Olá [cópias de segurança do WordPress][wordpressbackup].
2. Cópia de segurança da base de dados existente, utilizando informações Olá [cópia de segurança da base de dados][wordpressdbbackup].
3. Criar uma base de dados e restaurar Olá cópia de segurança.

   1. Adquira uma nova base de dados de Olá [Azure Marketplace][cdbnstore], ou configurar uma base de dados MySQL num [Windows] [ mysqlwindows] ou [Linux ] [ mysqllinux] máquina virtual.
   2. Utilizar um cliente MySQL como [MySQL Workbench] [ workbench] tooconnect toohello novos da base de dados e importar a base de dados do WordPress.
   3. Olá da base de dados toochange Olá domínio entradas tooyour novo App Service do Azure domínio de atualização, por exemplo, mywordpress.azurewebsites.net. Olá utilize [procurar e substituir de Script de bases de dados do WordPress] [ searchandreplace] toosafely Altere todas as instâncias.
4. Criar uma aplicação web no portal do Azure de Olá e publicar a cópia de segurança do Olá WordPress.

   1. toocreate uma aplicação web que tem uma base de dados, no Olá [portal do Azure][mgmtportal], clique em **novo** > **Web + móvel**  >  **Do azure Marketplace** > **aplicações Web** > **aplicação Web + SQL** (ou **aplicação Web + MySQL**) > **Criar**. Configure todas as toocreate de definições de Olá necessária uma aplicação web em branco.
   2. Na sua cópia de segurança do WordPress, localize Olá **wp-config.php** do ficheiro e abri-lo no editor. Substitua Olá entradas com informações de Olá para a sua nova base de dados MySQL os seguintes:

      * **DB_NAME**: nome de utilizador de Olá da base de dados de Olá.
      * **DB_USER**: Olá utilizador nome utilizado tooaccess Olá da base de dados.
      * **DB_PASSWORD**: palavra-passe de utilizador de Olá.

        Depois de alterar estas entradas, guarde e feche Olá **wp-config.php** ficheiro.
   3. Olá utilize [implementar uma aplicação web no App Service do Azure] [ deploy] informações tooenable Olá o método de implementação que pretende toouse e, em seguida, implementar a aplicação de web de cópia de segurança tooyour WordPress no App Service do Azure.
5. Depois de ter sido implementado o site do WordPress Olá, devem ser novo site de tooaccess capaz de Olá (como um aplicação web do app Service) utilizando Olá *. azurewebsite.net URL para o site de Olá.

### <a name="configure-your-site"></a>Configurar o seu site
Depois do site do WordPress Olá foi criada ou migrada, utilize Olá seguir o desempenho de tooimprove informações ou activar funcionalidades adicionais.

| toodo isto... | Utilize... |
| --- | --- |
| **Definir o modo de plano de serviço de aplicações, tamanho e ativar dimensionamento** |[Dimensionar a uma aplicação web no App Service do Azure][websitescale]. |
| **Ativar as ligações de base de dados persistente** |Por predefinição, o WordPress não utiliza ligações de base de dados persistente, o que poderão fazer com que a sua base de dados de toohello ligação toobecome limitada após várias ligações. ligações persistentes do tooenable, instalar Olá [Plug-in de adaptador de ligações persistentes](https://wordpress.org/plugins/persistent-database-connection-updater/installation/). |
| **Melhorar o desempenho** |<ul><li><p><a href="https://azure.microsoft.com/en-us/blog/disabling-arrs-instance-affinity-in-windows-azure-web-sites/">Desativar o cookie ARR Olá</a>, que pode melhorar o desempenho quando WordPress é executada em várias instâncias de aplicações Web.</p></li><li><p>Ative colocação em cache. Pode utilizar <a href="http://msdn.microsoft.com/library/azure/dn690470.aspx">a cache de Redis</a> (pré-visualização) com Olá <a href="https://wordpress.org/plugins/redis-object-cache/">Redis Plug-in WordPress de cache de objeto</a>, ou pode utilizar um dos Olá outras ofertas de colocação em cache de Olá <a href="/gallery/store/">arquivo Azure</a>.</p></li><li><p>[Certifique-WordPress mais rápido com Wincache](https://wordpress.org/plugins/w3-total-cache/). Wincache é ativado por predefinição para aplicações web. Ao utilizar o WinCache e Cache dinâmica em conjunto, desativar a cache de ficheiros do WinCache, mas deixe utilizador Olá e ativada a cache da sessão. tooturn desativar a cache de ficheiros, num ficheiro. ini de ao nível do sistema, defina Olá seguinte valor:<br/><code>wincache.fcenabled = 0</code></p></li><li><p>[Dimensionar a uma aplicação web no App Service do Azure] [ websitescale] e utilizar <a href="http://www.cleardb.com/developers/cdbr/introduction">ClearDB elevada disponibilidade encaminhamento</a> ou <a href="http://www.mysql.com/products/cluster/">MySQL Cluster CGE</a>.</p></li></ul> |
| **Utilize blobs de armazenamento** |<ol><li><p>[Criar uma conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md).</p></li><li><p>Saiba como demasiado[Olá utilize rede de distribuição de conteúdos](../cdn/cdn-create-new-endpoint.md) toogeo-distribuir dados armazenados em blobs.</p></li><li><p>Instalar e configurar Olá <a href="https://wordpress.org/plugins/windows-azure-storage/">Storage do Azure para o plug-in do WordPress</a>.</p><p>Para a configuração detalhada e informações de configuração para o plug-in de Olá, consulte Olá <a href="http://plugins.svn.wordpress.org/windows-azure-storage/trunk/UserGuide.docx">Guia do utilizador</a>.</p> </li></ol> |
| **Ativar o e-mail** |Ativar <a href="https://azure.microsoft.com/en-us/marketplace/partners/sendgrid/sendgrid-azure/">SendGrid</a> utilizando Olá Azure Store. Instalar Olá <a href="http://wordpress.org/plugins/sendgrid-email-delivery-simplified">Plug-in do SendGrid</a> para WordPress. |
| **Configurar um nome de domínio personalizado** |[Configurar um nome de domínio personalizado no App Service do Azure][customdomain]. |
| **Ativar HTTPS para um nome de domínio personalizado** |[Ativar HTTPS para uma aplicação web no App Service do Azure][httpscustomdomain]. |
| **Carregar saldo ou georreplicação-distribuir o seu site** |[Encaminhar o tráfego com o Azure Traffic Manager][trafficmanager]. Se estiver a utilizar um domínio personalizado, consulte o artigo [configurar um nome de domínio personalizado no App Service do Azure] [ customdomain] para obter informações sobre como toouse Gestor de tráfego com nomes de domínio personalizado. |
| **Ativar as cópias de segurança automatizadas** |[Cópia de segurança numa aplicação web no App Service do Azure][backup]. |
| **Ativar o registo de diagnóstico** |[Ativar o registo de diagnóstico para web apps no App Service do Azure][log]. |

## <a name="next-steps"></a>Passos seguintes
* [Otimização do WordPress](http://codex.wordpress.org/WordPress_Optimization)
* [Converter toomultisite WordPress no App Service do Azure](web-sites-php-convert-wordpress-multisite.md)
* [Assistente do Azure de atualização de ClearDB](http://www.cleardb.com/store/azure/upgrade)
* [Alojamento WordPress numa subpasta da sua aplicação web no App Service do Azure](http://blogs.msdn.com/b/webapps/archive/2013/02/13/hosting-wordpress-in-a-subfolder-of-your-windows-azure-web-site.aspx)
* [Passo a passo: Criar um site do WordPress através do Azure](http://blogs.technet.com/b/blainbar/archive/2013/08/07/article-create-a-wordpress-site-using-windows-azure-read-on.aspx)
* [Alojar o seu blogue do WordPress existente no Azure](http://blogs.msdn.com/b/msgulfcommunity/archive/2013/08/26/migrating-a-self-hosted-wordpress-blog-to-windows-azure.aspx)
* [Ativar permalinks pretty no WordPress](http://www.iis.net/learn/extensions/url-rewrite-module/enabling-pretty-permalinks-in-wordpress)
* [Como toomigrate e execute o blogue do WordPress no App Service do Azure](http://www.kefalidis.me/2012/06/how-to-migrate-and-run-your-wordpress-blog-on-windows-azure-websites/)
* [Como toorun WordPress no Azure App Service para libertar](http://architects.dzone.com/articles/how-run-wordpress-azure)
* [WordPress no Azure em dois minutos ou menos](http://www.sitepoint.com/wordpress-windows-azure-2-minutes-less/)
* [Mover um tooAzure blogue do WordPress - parte 1: criar um blogue do WordPress no Azure](http://www.davebost.com/2013/07/10/moving-a-wordpress-blog-to-windows-azure-part-1)
* [Mover um tooAzure blogue do WordPress - parte 2: Transferir o conteúdo](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-transferring-your-content)
* [Mover um tooAzure blogue do WordPress - parte 3: configurar o domínio personalizado](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-3-setting-up-your-custom-domain)
* [Mover um tooAzure blogue do WordPress - parte 4: Pretty permalinks e as regras de URL Rewrite](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-4-pretty-permalinks-and-url-rewrite-rules)
* [Mover um tooAzure blogue do WordPress - parte 5: mover de uma raiz de toohello subpasta](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-5-moving-from-a-subfolder-to-the-root)
* [Como tooset segurança um WordPress web de aplicação na sua conta do Azure](http://www.itexperience.net/2014/01/20/how-to-set-up-a-wordpress-website-in-your-windows-azure-account/)
* [Propping segurança WordPress no Azure](http://www.johnpapa.net/wordpress-on-azure/)
* [Sugestões para WordPress no Azure](http://www.johnpapa.net/azurecleardbmysql/)

> [!NOTE]
> Se quiser tooget iniciado com o App Service do Azure antes de se inscrever numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service. Sem cartões de crédito são necessários e, sem compromissos.
>
>

## <a name="whats-changed"></a>O que mudou
Para uma alteração de toohello do guia de Web sites tooApp serviço, consulte [App Service do Azure e o respetivo impacto nos serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714).

<!-- URL List -->

[performance-diagram]: ./media/web-sites-php-enterprise-wordpress/performance-diagram.png
[basic-diagram]: ./media/web-sites-php-enterprise-wordpress/basic-diagram.png
[multi-region-diagram]: ./media/web-sites-php-enterprise-wordpress/multi-region-diagram.png
[wordpress]: http://www.microsoft.com/web/wordpress
[officeblog]: http://blogs.office.com/
[bingblog]: http://blogs.bing.com/
[cdbnstore]: http://www.cleardb.com/store/azure
[storageplugin]: https://wordpress.org/plugins/windows-azure-storage/
[sendgridplugin]: http://wordpress.org/plugins/sendgrid-email-delivery-simplified/
[phpwebsite]: web-sites-php-configure.md
[customdomain]: app-service-web-tutorial-custom-domain.md
[trafficmanager]: ../traffic-manager/traffic-manager-overview.md
[backup]: web-sites-backup.md
[restore]: web-sites-restore.md
[rediscache]: https://azure.microsoft.com/documentation/services/redis-cache/
[managedcache]: http://msdn.microsoft.com/library/azure/dn386122.aspx
[websitescale]: web-sites-scale.md
[managedcachescale]: http://msdn.microsoft.com/library/azure/dn386113.aspx
[cleardbscale]: http://www.cleardb.com/developers/cdbr/introduction
[staging]: web-sites-staged-publishing.md
[monitor]: web-sites-monitor.md
[log]: web-sites-enable-diagnostic-log.md
[httpscustomdomain]: app-service-web-tutorial-custom-ssl.md
[mysqlwindows]:../virtual-machines/windows/classic/mysql-2008r2.md
[mysqllinux]:../virtual-machines/linux/classic/mysql-on-opensuse.md
[cge]: http://www.mysql.com/products/cluster/
[websitepricing]: /pricing/details/app-service/
[export]: http://en.support.wordpress.com/export/
[import]: http://wordpress.org/plugins/wordpress-importer/
[wordpressbackup]: http://wordpress.org/plugins/wordpress-importer/
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[createwordpress]: web-sites-php-web-site-gallery.md
[velvet]: https://wordpress.org/plugins/velvet-blues-update-urls/
[mgmtportal]: https://portal.azure.com/
[wordpressbackup]: http://codex.wordpress.org/WordPress_Backups
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[workbench]: http://www.mysql.com/products/workbench/
[searchandreplace]: http://interconnectit.com/124/search-and-replace-for-wordpress-databases/
[deploy]: web-sites-deploy.md
[posh]: /powershell/azureps-cmdlets-docs
[Azure CLI]:../cli-install-nodejs.md
[storesendgrid]: https://azure.microsoft.com/marketplace/partners/sendgrid/sendgrid-azure/
[cdn]: ../cdn/cdn-overview.md
