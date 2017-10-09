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
# <a name="azure-data-catalog-release-notes"></a>Notas de versão do catálogo de dados do Azure
## <a name="notes-for-hello-november-20-2015-release-of-azure-data-catalog"></a>Notas de versão de 20 de Novembro de 2015 Olá do catálogo de dados do Azure
### <a name="opening-data-sources-in-power-bi-desktop"></a>Abrir as origens de dados no Power BI Desktop
Ao utilizar a opção de "Abrir no Power BI Desktop" Olá de Olá **catálogo de dados do Azure** portal, os utilizadores poderão encontrar um dos dois problemas no Olá aplicações de ambiente de trabalho do Power BI:

* É apresentada uma caixa de diálogo com o título de Olá "Não é possível tooOpen documento"
* Abre Olá aplicação Power BI Desktop, mas o ficheiro Olá aparece toobe vazio

Para cada situação, problema Olá pode ser resolvido ao descarregar e instalar a versão mais recente do Olá do Power BI Desktop de [PowerBI.com](https://powerbi.com).

## <a name="notes-for-hello-november-13-2015-release-of-azure-data-catalog"></a>Notas de versão de 13 de Novembro de 2015 Olá do catálogo de dados do Azure
### <a name="registering-and-connecting-tooteradata"></a>Registar e ligar tooTeradata
Ao ligar a origens de dados de tooTeradata os utilizadores têm de ter instalada Olá correto Teradata o controlador ODBC que correspondem ao hello número de bits (32 bits ou 64 bits) de software Olá a ser utilizado.

A partir deste ADC data da versão, hello mais recente [o controlador ODBC do Teradata para windows (versão 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) é compatível com o Office 2013, mas não com o Office 2016.

## <a name="notes-for-hello-july-13-2015-release-of-azure-data-catalog"></a>Notas de versão de 13 de Julho de 2015 Olá do catálogo de dados do Azure
### <a name="registering-and-connecting-toooracle-database"></a>Registar e ligar tooOracle da base de dados
Quando ligar utilizadores de origens de dados de base de dados de tooOracle deve ter instalada Olá corretos Oracle controladores correspondentes Olá número de bits (32 bits ou 64 bits) de software Olá a ser utilizado.

* Quando registar origens de dados Oracle num computador com o Windows de 32 bits, controladores de Oracle de 32 bits Olá serão utilizados
* Quando registar origens de dados Oracle num computador com o Windows de 64 bits, controladores de Oracle de 64 bits Olá serão utilizados
* Quando ligar tooOracle origens de dados com o Excel num computador com a versão de 32 bits Olá do Microsoft Office, incluindo no Windows de 64 bits, controladores de Oracle de 32 bits Olá serão utilizados
* Quando ligar tooOracle origens de dados com o Excel num computador com a versão de 64 bits Olá do Microsoft Office, controladores de Oracle de 64 bits Olá serão utilizados

### <a name="registering-and-connecting-toosql-server-reporting-services"></a>Registar e ligar tooSQL Server Reporting Services
Suporte para origens de dados do SQL Server Reporting Services (SSRS) está actualmente limitada tooNative servidores de modo apenas. Suporte para SSRS no modo SharePoint será adicionado a uma versão posterior.

### <a name="opening-data-assets-in-excel"></a>Recursos de dados de abrir no Excel
Ao abrir os recursos de dados no Microsoft Excel de Olá **catálogo de dados do Azure** portal, os utilizadores poderão ser-lhe solicitados com um **aviso de segurança do Microsoft Excel** caixa de diálogo. Este é padrão, podem selecionar o comportamento esperado e os utilizadores **ativar** toocontinue.

Para obter mais informações, consulte [ativar ou desativar alertas de segurança sobre ligações de ficheiros e de Web sites suspeitos](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a>Registo da origem de dados e configuração de proxy e de política
Os utilizadores podem encontrar uma situação em que podem iniciar sessão no portal do catálogo de dados do Azure de toohello, mas quando tentam toolog no toohello ferramenta origens de dados registo encontrarem uma mensagem de erro que impede que iniciar sessão.

Existem duas causas possíveis para este comportamento do problema:

**Causa 1: Configuração de serviços de Federação do Active Directory** utiliza a ferramenta de registo da origem de dados de Olá inícios de sessão de autenticação de formulários toovalidate utilizador contra do Active Directory. Início de sessão bem-sucedidos, a autenticação de formulários deve ser ativada na política de autenticação Global de Olá por um administrador do Active Directory.

Em algumas situações, este comportamento de erro pode ocorrer apenas quando o utilizador Olá está na rede da empresa de Olá ou apenas quando o utilizador Olá está a ligar a partir da rede do Olá fora da empresa. Olá política de autenticação Global permite toobe de métodos de autenticação ativada em separado para intranet e extranet ligações. Se a autenticação de formulários não está ativada para a rede de Olá do qual Olá utilizador está a ligar, poderão ocorrer erros de início de sessão.

Para obter mais informações, consulte [configurar políticas de autenticação](https://technet.microsoft.com/library/dn486781.aspx).

**Causa 2: Configuração de proxy de rede** se a rede empresarial Olá utiliza um servidor proxy, ferramenta de registo Olá pode não ser capaz de tooconnect tooAzure do Active Directory através do proxy de Olá. Os utilizadores podem certificar-se essa ferramenta de registo Olá editando o ficheiro de configuração da ferramenta de Olá, adicionar este ficheiro de toohello secção:

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


ficheiro de RegistrationTool.exe.config do toolocate Olá, iniciar a ferramenta de registo Olá e, em seguida, abrir o utilitário de Gestor de tarefas do Windows hello. No separador de detalhes de Olá no Gestor de tarefas, clique com o botão direito no RegistrationTool.exe e escolha a localização de ficheiro aberto a partir do menu de pop-up Olá.
