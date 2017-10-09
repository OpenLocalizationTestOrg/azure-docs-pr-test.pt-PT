---
title: aaaUse ReportViewer num Web Site | Microsoft Docs
description: "Este tópico descreve como toobuild num site Web do Microsoft Azure com o controlo de Visual Studio ReportViewer Olá que apresenta um relatório armazenado numa máquina de Virtual do Microsoft Azure."
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 78b76318-d9bf-48ef-9d9e-d1b7d8cf3042
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: 8e0729d6657f96c32a9ac7dffdff7745ff92b48d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-reportviewer-in-a-web-site-hosted-in-azure"></a>Utilizar o ReportViewer num Web Site Alojado no Azure
> [!IMPORTANT] 
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.

Pode criar um site do Microsoft Azure Web com Olá controlo ReportViewer do Visual Studio que apresenta um relatório armazenado numa máquina de Virtual do Microsoft Azure. Olá controlo ReportViewer é numa aplicação Web que criar utilizando Olá modelo de aplicação ASP.NET Web.

> [!IMPORTANT]
> modelos de aplicação de Web de MVC do ASP.NET Olá não suportam o controlo de ReportViewer Olá.

tooincorporate ReportViewer no seu site Web do Microsoft Azure, terá de Olá toocomplete seguintes tarefas.

* **Adicionar** assemblagens toohello pacote de implementação
* **Configurar** autenticação e autorização
* **Publicar** Olá tooAzure de aplicação ASP.NET Web

## <a name="prerequisites"></a>Pré-requisitos
Reveja a secção "geral recomendação e melhores práticas" Olá no [SQL Server Business Intelligence em Azure Virtual Machines](../classic/ps-sql-bi.md).

> [!NOTE]
> Controlos de ReportViewer são fornecidos com o Visual Studio, Standard Edition ou superior. Se estiver a utilizar Olá Web Developer Express Edition, tem de instalar Olá [o tempo de execução do MICROSOFT REPORT VIEWER 2012](https://www.microsoft.com/download/details.aspx?id=35747) funcionalidades de tempo de execução do toouse Olá ReportViewer.
> 
> ReportViewer configurado no modo de processamento local não é suportada no Microsoft Azure.

## <a name="adding-assemblies-toohello-deployment-package"></a>Adicionar assemblagens toohello pacote de implementação
Ao alojar ASP.NET aplicações no local, as assemblagens de ReportViewer Olá normalmente instaladas diretamente na Olá global assembly cache (GAC) hello do servidor do IIS durante a instalação do Visual Studio e podem ser acedidas diretamente pelo aplicação Olá. No entanto, quando o anfitrião a aplicação de ASP.NET numa nuvem Olá, o Microsoft Azure não permite qualquer coisa toobe instalada na Olá GAC, pelo que deve certificar-se as assemblagens de ReportViewer Olá estão disponíveis localmente para a sua aplicação. Pode fazê-lo ao adicionar referências toothem no seu projeto e configurá-los toobe copiados localmente.

No modo de processamento remoto, Olá controlo ReportViewer utiliza Olá assemblagens os seguintes:

* **Microsoft.ReportViewer.WebForms.dll**: contém o código de ReportViewer Olá, o que precisa de toouse ReportViewer na sua página. Uma referência para esta assemblagem é adicionada tooyour projeto quando remover um controlo ReportViewer para uma página ASP.NET no seu projeto.
* **Microsoft.ReportViewer.Common.dll**: contém classes utilizadas pelo Olá controlo ReportViewer em tempo de execução. Não é adicionado automaticamente tooyour projeto.

### <a name="tooadd-a-reference-toomicrosoftreportviewercommon"></a>tooadd um tooMicrosoft.ReportViewer.Common de referência
* Clique com o botão direito do seu projeto **referências** nó e selecione **Adicionar referência**, selecione de assemblagem Olá no separador de .NET Olá e clique em **OK**.

### <a name="toomake-hello-assemblies-locally-accessible-by-your-aspnet-application"></a>toomake Olá as assemblagens localmente acessíveis pela sua aplicação ASP.NET
1. No Olá **referências** pasta, clique em assemblagem de Microsoft.ReportViewer.Common Olá, para que as respetivas propriedades são apresentados no painel de propriedades de Olá.
2. No painel de propriedades de Olá, defina **Cópia Local** tooTrue.
3. Repita os passos 1 e 2 para Microsoft.ReportViewer.WebForms.

### <a name="tooget-reportviewer-language-pack"></a>tooget ReportViewer Language Pack
1. Instalar Olá adequado o tempo de execução do Microsoft Report Viewer 2012 pacote redistribuível do [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=317386).
2. Idioma de Olá selecione na lista pendente Olá e página Olá obtém toohello redirecionada correspondente página de centro de transferência.
3. Clique em **transferir** transferências de Olá toostart de ReportViewerLP.exe.
4. Depois de transferir ReportViewerLP.exe, clique em **executar** tooinstall imediatamente, ou clique em **guardar** toosave-tooyour computador. Se clicar em **guardar**, memorizar Olá nome da pasta de olá onde guardar o ficheiro de Olá.
5. Localize a pasta de olá onde guardou o ficheiro de Olá. Clique com o botão direito ReportViewerLP.exe, clique em **executar como administrador**e, em seguida, clique em **Sim**.
6. Depois de executar ReportViewerLP.exe, irá ver Olá c:\windows\assembly tem ficheiros de recursos de Olá **Microsoft.ReportViewer.Webforms.Resources** e **Microsoft.ReportViewer.Common.Resources** .

### <a name="tooconfigure-for-localized-reportviewer-control"></a>tooconfigure para o controlo ReportViewer localizado
1. Transfira e instale o pacote redistribuível do Microsoft Report Viewer 2012 Runtime Olá pelo seguinte Olá acima instruções especificadas.
2. Criar <language> pasta Olá de projeto e copie Olá associados ficheiros de assemblagem de recursos existe. Olá toobe de ficheiros de assemblagem de recursos copiado são: **Microsoft.ReportViewer.Webforms.Resources.dll** e **Microsoft.ReportViewer.Common.Resources.dll**. Selecione os ficheiros de assemblagem de recursos de Olá e, no painel de propriedades de Olá, defina **copiar tooOutput diretório** demasiado "**Copiar sempre**".
3. Definir hello cultura & UICulture para o projeto web de Olá. Para obter mais informações sobre como tooset Olá cultura e cultura da IU para uma página ASP.NET Web, consulte [como: conjunto hello cultura e cultura da IU para globalização de página Web ASP.NET](http://go.microsoft.com/fwlink/?LinkId=237461).

## <a name="configuring-authentication-and-authorization"></a>Configurar a autenticação e autorização
necessita de Olá ReportViewer toouse as credenciais corretas tooauthenticate com o servidor de relatórios de Olá e credenciais de Olá tem de ser autorizadas por Olá relatórios report server tooaccess Olá que quiser. Para informações sobre a autenticação, consulte o documento técnico Olá [relatório do Reporting Services controlo do Visualizador e servidores de relatórios do Microsoft Azure baseada em máquina virtual](https://msdn.microsoft.com/library/azure/dn753698.aspx).

## <a name="publish-hello-aspnet-web-application-tooazure"></a>Publicar Olá tooAzure de aplicação ASP.NET Web
Para obter instruções sobre a publicação de um tooAzure de aplicação ASP.NET Web, consulte [como: publicar um tooAzure de aplicação Web do Visual Studio e migrar](../../../vs-azure-tools-migrate-publish-web-app-to-cloud-service.md) e [introdução às Web Apps e ASP.NET](../../../app-service-web/app-service-web-get-started-dotnet.md).

> [!IMPORTANT]
> Se Olá comando Adicionar projeto de implementação do Azure ou adicionar projeto de serviço de nuvem do Azure não aparecer no menu de atalho Olá no Explorador de soluções, poderá ter o framework de destino de Olá toochange para Olá projeto too.NET Framework 4.
> 
> comandos de Olá dois fornecem essencialmente Olá a mesma funcionalidade. Um ou Olá outros comandos serão apresentada no menu de atalho Olá consoante a versão do SDK do Microsoft Azure de Olá instalou.
> 
> 

## <a name="resources"></a>Recursos
[Relatórios da Microsoft](http://go.microsoft.com/fwlink/?LinkId=205399)

[SQL Server Business Intelligence em Máquinas Virtuais do Azure](../classic/ps-sql-bi.md)

[Utilizar o PowerShell tooCreate um Azure VM com um nativo modo de servidor de relatórios](../classic/ps-sql-report.md)

