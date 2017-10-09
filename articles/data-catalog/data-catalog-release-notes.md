---
title: "notas de versão do catálogo de dados aaaAzure | Microsoft Docs"
description: "Notas de versão do catálogo de dados do Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 661826f66020ba72a885c6b14522b53c8b469d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-release-notes"></a><span data-ttu-id="4ac9e-103">Notas de versão do catálogo de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="4ac9e-103">Azure Data Catalog release notes</span></span>
## <a name="notes-for-hello-november-20-2015-release-of-azure-data-catalog"></a><span data-ttu-id="4ac9e-104">Notas de versão de 20 de Novembro de 2015 Olá do catálogo de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="4ac9e-104">Notes for hello November 20, 2015 release of Azure Data Catalog</span></span>
### <a name="opening-data-sources-in-power-bi-desktop"></a><span data-ttu-id="4ac9e-105">Abrir as origens de dados no Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="4ac9e-105">Opening Data Sources in Power BI Desktop</span></span>
<span data-ttu-id="4ac9e-106">Ao utilizar a opção de "Abrir no Power BI Desktop" Olá de Olá **catálogo de dados do Azure** portal, os utilizadores poderão encontrar um dos dois problemas no Olá aplicações de ambiente de trabalho do Power BI:</span><span class="sxs-lookup"><span data-stu-id="4ac9e-106">When using hello "Open in Power BI Desktop" option from hello **Azure Data Catalog** portal, users may encounter one of two problems in hello Power BI Desktop application:</span></span>

* <span data-ttu-id="4ac9e-107">É apresentada uma caixa de diálogo com o título de Olá "Não é possível tooOpen documento"</span><span class="sxs-lookup"><span data-stu-id="4ac9e-107">A dialog box with hello title "Unable tooOpen Document" is displayed</span></span>
* <span data-ttu-id="4ac9e-108">Abre Olá aplicação Power BI Desktop, mas o ficheiro Olá aparece toobe vazio</span><span class="sxs-lookup"><span data-stu-id="4ac9e-108">hello Power BI Desktop application opens, but hello file appears toobe empty</span></span>

<span data-ttu-id="4ac9e-109">Para cada situação, problema Olá pode ser resolvido ao descarregar e instalar a versão mais recente do Olá do Power BI Desktop de [PowerBI.com](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="4ac9e-109">For each situation, hello problem can be resolved by downloading and installing hello latest version of Power BI Desktop from [PowerBI.com](https://powerbi.com).</span></span>

## <a name="notes-for-hello-november-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="4ac9e-110">Notas de versão de 13 de Novembro de 2015 Olá do catálogo de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="4ac9e-110">Notes for hello November 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-tooteradata"></a><span data-ttu-id="4ac9e-111">Registar e ligar tooTeradata</span><span class="sxs-lookup"><span data-stu-id="4ac9e-111">Registering and connecting tooTeradata</span></span>
<span data-ttu-id="4ac9e-112">Ao ligar a origens de dados de tooTeradata os utilizadores têm de ter instalada Olá correto Teradata o controlador ODBC que correspondem ao hello número de bits (32 bits ou 64 bits) de software Olá a ser utilizado.</span><span class="sxs-lookup"><span data-stu-id="4ac9e-112">When connecting tooTeradata data sources users must have installed hello correct Teradata ODBC driver that match hello bitness (32-bit or 64-bit) of hello software being used.</span></span>

<span data-ttu-id="4ac9e-113">A partir deste ADC data da versão, hello mais recente [o controlador ODBC do Teradata para windows (versão 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) é compatível com o Office 2013, mas não com o Office 2016.</span><span class="sxs-lookup"><span data-stu-id="4ac9e-113">As of this ADC release date, hello most recent [Teradata ODBC driver for windows ( version 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) is compatible with Office 2013, but not with Office 2016.</span></span>

## <a name="notes-for-hello-july-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="4ac9e-114">Notas de versão de 13 de Julho de 2015 Olá do catálogo de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="4ac9e-114">Notes for hello July 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-toooracle-database"></a><span data-ttu-id="4ac9e-115">Registar e ligar tooOracle da base de dados</span><span class="sxs-lookup"><span data-stu-id="4ac9e-115">Registering and connecting tooOracle Database</span></span>
<span data-ttu-id="4ac9e-116">Quando ligar utilizadores de origens de dados de base de dados de tooOracle deve ter instalada Olá corretos Oracle controladores correspondentes Olá número de bits (32 bits ou 64 bits) de software Olá a ser utilizado.</span><span class="sxs-lookup"><span data-stu-id="4ac9e-116">When connecting tooOracle Database data sources users must have installed hello correct Oracle drivers that match hello bitness (32-bit or 64-bit) of hello software being used.</span></span>

* <span data-ttu-id="4ac9e-117">Quando registar origens de dados Oracle num computador com o Windows de 32 bits, controladores de Oracle de 32 bits Olá serão utilizados</span><span class="sxs-lookup"><span data-stu-id="4ac9e-117">When registering Oracle data sources on a computer running 32-bit Windows, hello 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="4ac9e-118">Quando registar origens de dados Oracle num computador com o Windows de 64 bits, controladores de Oracle de 64 bits Olá serão utilizados</span><span class="sxs-lookup"><span data-stu-id="4ac9e-118">When registering Oracle data sources on a computer running 64-bit Windows, hello 64-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="4ac9e-119">Quando ligar tooOracle origens de dados com o Excel num computador com a versão de 32 bits Olá do Microsoft Office, incluindo no Windows de 64 bits, controladores de Oracle de 32 bits Olá serão utilizados</span><span class="sxs-lookup"><span data-stu-id="4ac9e-119">When connecting tooOracle data sources using Excel on a computer running hello 32-bit version of Microsoft Office, including on 64-bit Windows, hello 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="4ac9e-120">Quando ligar tooOracle origens de dados com o Excel num computador com a versão de 64 bits Olá do Microsoft Office, controladores de Oracle de 64 bits Olá serão utilizados</span><span class="sxs-lookup"><span data-stu-id="4ac9e-120">When connecting tooOracle data sources using Excel on a computer running hello 64-bit version of Microsoft Office, hello 64-bit Oracle drivers will be used</span></span>

### <a name="registering-and-connecting-toosql-server-reporting-services"></a><span data-ttu-id="4ac9e-121">Registar e ligar tooSQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="4ac9e-121">Registering and connecting tooSQL Server Reporting Services</span></span>
<span data-ttu-id="4ac9e-122">Suporte para origens de dados do SQL Server Reporting Services (SSRS) está actualmente limitada tooNative servidores de modo apenas.</span><span class="sxs-lookup"><span data-stu-id="4ac9e-122">Support for SQL Server Reporting Services (SSRS) data sources is currently limited tooNative Mode servers only.</span></span> <span data-ttu-id="4ac9e-123">Suporte para SSRS no modo SharePoint será adicionado a uma versão posterior.</span><span class="sxs-lookup"><span data-stu-id="4ac9e-123">Support for SSRS in SharePoint mode will be added in a later release.</span></span>

### <a name="opening-data-assets-in-excel"></a><span data-ttu-id="4ac9e-124">Recursos de dados de abrir no Excel</span><span class="sxs-lookup"><span data-stu-id="4ac9e-124">Opening data assets in Excel</span></span>
<span data-ttu-id="4ac9e-125">Ao abrir os recursos de dados no Microsoft Excel de Olá **catálogo de dados do Azure** portal, os utilizadores poderão ser-lhe solicitados com um **aviso de segurança do Microsoft Excel** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4ac9e-125">When opening data assets in Microsoft Excel from hello **Azure Data Catalog** portal, users may be prompted with a **Microsoft Excel Security Notice** dialog box.</span></span> <span data-ttu-id="4ac9e-126">Este é padrão, podem selecionar o comportamento esperado e os utilizadores **ativar** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="4ac9e-126">This is standard, expected behavior, and users can select **Enable** toocontinue.</span></span>

<span data-ttu-id="4ac9e-127">Para obter mais informações, consulte [ativar ou desativar alertas de segurança sobre ligações de ficheiros e de Web sites suspeitos](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span><span class="sxs-lookup"><span data-stu-id="4ac9e-127">For more information, see [Enable or disable security alerts about links and files from suspicious websites](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span></span>

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a><span data-ttu-id="4ac9e-128">Registo da origem de dados e configuração de proxy e de política</span><span class="sxs-lookup"><span data-stu-id="4ac9e-128">Proxy and policy configuration and data source registration</span></span>
<span data-ttu-id="4ac9e-129">Os utilizadores podem encontrar uma situação em que podem iniciar sessão no portal do catálogo de dados do Azure de toohello, mas quando tentam toolog no toohello ferramenta origens de dados registo encontrarem uma mensagem de erro que impede que iniciar sessão.</span><span class="sxs-lookup"><span data-stu-id="4ac9e-129">Users may encounter a situation where they can log on toohello Azure Data Catalog portal, but when they attempt toolog on toohello data source registration tool they encounter an error message that prevents them from logging on.</span></span>

<span data-ttu-id="4ac9e-130">Existem duas causas possíveis para este comportamento do problema:</span><span class="sxs-lookup"><span data-stu-id="4ac9e-130">There are two potential causes for this problem behavior:</span></span>

<span data-ttu-id="4ac9e-131">**Causa 1: Configuração de serviços de Federação do Active Directory** utiliza a ferramenta de registo da origem de dados de Olá inícios de sessão de autenticação de formulários toovalidate utilizador contra do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4ac9e-131">**Cause 1: Active Directory Federation Services configuration** hello data source registration tool uses Forms Authentication toovalidate user logons against Active Directory.</span></span> <span data-ttu-id="4ac9e-132">Início de sessão bem-sucedidos, a autenticação de formulários deve ser ativada na política de autenticação Global de Olá por um administrador do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4ac9e-132">For successful logon, Forms Authentication must be enabled in hello Global Authentication Policy by an Active Directory administrator.</span></span>

<span data-ttu-id="4ac9e-133">Em algumas situações, este comportamento de erro pode ocorrer apenas quando o utilizador Olá está na rede da empresa de Olá ou apenas quando o utilizador Olá está a ligar a partir da rede do Olá fora da empresa.</span><span class="sxs-lookup"><span data-stu-id="4ac9e-133">In some situations, this error behavior may occur only when hello user is on hello company network, or only when hello user is connecting from outside hello company network.</span></span> <span data-ttu-id="4ac9e-134">Olá política de autenticação Global permite toobe de métodos de autenticação ativada em separado para intranet e extranet ligações.</span><span class="sxs-lookup"><span data-stu-id="4ac9e-134">hello Global Authentication Policy allows authentication methods toobe enabled separately for intranet and extranet connections.</span></span> <span data-ttu-id="4ac9e-135">Se a autenticação de formulários não está ativada para a rede de Olá do qual Olá utilizador está a ligar, poderão ocorrer erros de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="4ac9e-135">Logon errors may occur if Forms Authentication is not enabled for hello network from which hello user is connecting.</span></span>

<span data-ttu-id="4ac9e-136">Para obter mais informações, consulte [configurar políticas de autenticação](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ac9e-136">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>

<span data-ttu-id="4ac9e-137">**Causa 2: Configuração de proxy de rede** se a rede empresarial Olá utiliza um servidor proxy, ferramenta de registo Olá pode não ser capaz de tooconnect tooAzure do Active Directory através do proxy de Olá.</span><span class="sxs-lookup"><span data-stu-id="4ac9e-137">**Cause 2: Network proxy configuration** If hello corporate network uses a proxy server, hello registration tool may not be able tooconnect tooAzure Active Directory through hello proxy.</span></span> <span data-ttu-id="4ac9e-138">Os utilizadores podem certificar-se essa ferramenta de registo Olá editando o ficheiro de configuração da ferramenta de Olá, adicionar este ficheiro de toohello secção:</span><span class="sxs-lookup"><span data-stu-id="4ac9e-138">Users can ensure that hello registration tool by editing hello tool’s configuration file, adding this section toohello file:</span></span>

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


<span data-ttu-id="4ac9e-139">ficheiro de RegistrationTool.exe.config do toolocate Olá, iniciar a ferramenta de registo Olá e, em seguida, abrir o utilitário de Gestor de tarefas do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="4ac9e-139">toolocate hello RegistrationTool.exe.config file, launch hello registration tool, and then open hello Windows Task Manager utility.</span></span> <span data-ttu-id="4ac9e-140">No separador de detalhes de Olá no Gestor de tarefas, clique com o botão direito no RegistrationTool.exe e escolha a localização de ficheiro aberto a partir do menu de pop-up Olá.</span><span class="sxs-lookup"><span data-stu-id="4ac9e-140">On hello Details tab in Task manager, right-click on RegistrationTool.exe and choose Open file location from hello pop-up menu.</span></span>
