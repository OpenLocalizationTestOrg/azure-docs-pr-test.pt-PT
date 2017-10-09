---
title: "aaaSupported tipos de recursos através de estado de funcionamento de recursos do Azure | Microsoft Docs"
description: "Tipos de recurso suportados através do Estado de funcionamento de recursos do Azure"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 03/19/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: a37d5c33f6ef6fdfbce0daf392bc7fa57853c7d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="resource-types-and-health-checks-in-azure-resource-health"></a>Tipos de recursos e o estado de funcionamento verifica-se no estado de funcionamento de recursos do Azure
Segue-se uma lista completa de todas as verificações de Olá executado através de estado de funcionamento de recursos por tipos de recursos.

## <a name="microsoftcacheredisredis"></a>Microsoft.CacheRedis/Redis
|Verificações executadas|
|---|
|<ul><li>São todos os nós de Cache de Olá cópias de segurança e em execução?</li><li>Olá Cache acessível num centro de dados de Olá?</li><li>Tem a Cache atingiu o número máximo de Olá de ligações de Olá?</li><li> Cache de Olá esgotou a memória disponível? </li><li>Olá Cache estão a ocorrer um elevado número de falhas de paginação?</li><li>É Olá Cache com muita carga?</li></ul>|

## <a name="microsoftcdnprofile"></a>Microsoft.CDN/profile
|Verificações executadas|
|---|
|<ul> <li>Qualquer um dos pontos finais de Olá foi parado, removidas ou mal configurada?</li><li>Portal suplementar Olá está acessível para operações de configuração da CDN?</li><li>Existem problemas de entrega em curso com Olá pontos finais da CDN?</li><li>Os utilizadores podem alterar a configuração Olá dos respetivos recursos CDN?</li><li>As alterações de configuração são propagar a taxa de Olá esperada?</li><li>Os utilizadores podem gerir a configuração de CDN de Olá utilizando Olá portal do Azure, PowerShell ou Olá API?</li> </ul>|

## <a name="microsoftclassiccomputevirtualmachines"></a>Microsoft.classiccompute/virtualmachines
|Verificações executadas|
|---|
|<ul><li>É o servidor de anfitrião Olá cópias de segurança e em execução?</li><li>Olá anfitrião SO arrancar concluiu?</li><li>É o contentor da máquina virtual Olá aprovisionado e utiliza a tecnologia cópias de segurança?</li><li>Existe conectividade de rede entre o anfitrião de Olá e conta de armazenamento Olá?</li><li>Arranque de Olá de SO de convidado de Olá concluiu?</li><li>Existe a manutenção planeada em curso?</li></ul>|

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.cognitiveservices/Accounts
|Verificações executadas|
|---|
|<ul><li>Conta de Olá acessível num centro de dados de Olá?</li><li>É Olá cognitivos fornecedor de recursos de serviços disponíveis?</li><li>É Olá cognitivos serviço disponível na região adequado Olá?</li><li>Pode ler possível efetuar as operações da conta do storage Olá que contém os metadados do recurso de Olá?</li><li>Tem foi atingida a quota de chamada de Olá API?</li><li>Foi atingido o limite de leitura do chamada Olá API?</li></ul>|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.Compute/virtualmachines
|Verificações executadas|
|---|
|<ul><li>É o servidor de Olá alojar esta máquina virtual a cópia de segurança e em execução?</li><li>Olá anfitrião SO arrancar concluiu?</li><li>É o contentor da máquina virtual Olá aprovisionado e utiliza a tecnologia cópias de segurança?</li><li>Existe conectividade de rede entre o anfitrião de Olá e conta de armazenamento Olá?</li><li>Arranque de Olá de SO de convidado de Olá concluiu?</li><li>Existe a manutenção planeada em curso?</li></ul>|

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.datalakeanalytics/Accounts
|Verificações executadas|
|---|
|<ul><li>Podem utilizadores submeter tarefas tooData Lake Analytics no Olá região?</li><li>Fazer a região do tarefas básico Olá executado e concluído com êxito no?</li><li>Podem utilizadores listar itens de catálogo na região de Olá?</li>|


## <a name="microsoftdatalakestoreaccounts"></a>Microsoft.datalakestore/Accounts
|Verificações executadas|
|---|
|<ul><li>Podem utilizadores carregar tooData de data Lake Store na região de Olá?</li><li>Os utilizadores transferem dados do Data Lake Store numa região de Olá</li></ul>|

## <a name="microsoftdocumentdbdatabaseaccounts"></a>Microsoft.documentdb/databaseAccounts
|Verificações executadas|
|---|
|<ul><li>Ter ocorrido quaisquer pedidos de base de dados ou de coleção não servidos devido a indisponibilidade de serviço do DocumentDB tooa?</li><li>Ter ocorrido quaisquer pedidos de documento não servidos devido a indisponibilidade de serviço do DocumentDB tooa?</li></ul>|

## <a name="microsoftnetworkconnections"></a>Microsoft.Network/Connections
|Verificações executadas|
|---|
|<ul><li>Túnel VPN de Olá ligado</li><li>Existem conflitos de configuração na ligação de Olá?</li><li>Estão chaves pré-partilhadas Olá configuradas corretamente?</li><li>Olá VPN no local o dispositivo for acessível?</li><li>Existem correspondência na política de segurança do IPSec/IKE Olá?</li><li>É a ligação de S2S VPN Olá corretamente aprovisionado ou em estado de falha?</li><li>Corretamente aprovisionado ou em estado de falha, é ligação Olá VNET a VNET?</li></ul>|

## <a name="microsoftnetworkvirtualnetworkgateways"></a>Microsoft.network/virtualNetworkGateways
|Verificações executadas|
|---|
|<ul><li>É o gateway de VPN Olá acessível a partir do Olá internet?</li><li>É Olá o Gateway de VPN no modo de reserva dinâmica?</li><li>Olá serviço VPN está em execução no gateway de Olá?</li></ul>|

## <a name="microsoftnotificationhubsnamespace"></a>Microsoft.NotificationHubs/namespace
|Verificações executadas|
|---|
|<ul><li> Tempo de execução operações, como o registo, a instalação ou a enviar podem ser executadas num espaço de nomes de Olá?</li></ul>|

## <a name="microsoftpowerbiworkspacecollections"></a>Microsoft.PowerBI/workspaceCollections
|Verificações executadas|
|---|
|<ul><li>É anfitrião Olá SO cópias de segurança e em execução?</li><li>Olá workspaceCollection é acessível a partir de fora do datacenter Olá?</li><li>É Olá o fornecedor de recursos do PowerBI disponível?</li><li>É Olá serviço PowerBI disponível na região adequado Olá?</li></ul>|

## <a name="microsoftsearchsearchservices"></a>Microsoft.search/searchServices
|Verificações executadas|
|---|
|<ul><li>Operações de diagnóstico podem ser efetuadas num cluster de Olá?</li></ul>|

## <a name="microsoftsqlserverdatabase"></a>Microsoft.SQL/Server/database
|Verificações executadas|
|---|
|<ul><li> Não existe ter sido a base de dados de inícios de sessão toohello?</li></ul>|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs
|Verificações executadas|
|---|
|<ul><li>São todos os anfitriões de olá onde tarefa Olá está a executar cópias de segurança e em execução?</li><li>Foi Olá tarefa não é possível toostart?</li><li>Existem atualizações de tempo de execução em curso?</li><li>Tarefa de Olá num estado esperado (por exemplo em execução ou parada pelo cliente)?</li><li>Olá tarefa encontrou saída de exceções de memória?</li><li>Existem atualizações em curso computação agendada?</li><li>É Olá Gestor de execução (plano de controlo) está disponível?</li></ul>|

## <a name="microsoftwebserverfarms"></a>Microsoft.web/serverFarms
|Verificações executadas|
|---|
|<ul><li>É o servidor de anfitrião Olá cópias de segurança e em execução?</li><li>Serviços de informação Internet está em execução?</li><li>Balanceador de carga Olá está em execução?</li><li>Pode Olá plano do Web Service ser aceder a partir num centro de dados de Olá?</li><li>Está disponível Olá armazenamento conta alojamento Olá sites conteúdo para Olá serverFarm??</li></ul>|

## <a name="microsoftwebsites"></a>Microsoft.Web/sites
|Verificações executadas|
|---|
|<ul><li>É o servidor de anfitrião Olá cópias de segurança e em execução?</li><li>Servidor de informação Internet está em execução?</li><li>Balanceador de carga Olá está em execução?</li><li>Olá aplicação Web acessível num centro de dados de Olá?</li><li>Conta de armazenamento Olá aloja o conteúdo do site Olá disponível?</li></ul>|

Consulte estes toolearn de recursos mais sobre o estado de funcionamento de recursos:
-  [Estado de funcionamento de recursos de tooAzure de introdução](Resource-health-overview.md)
-  [Perguntas mais frequentes sobre o estado de funcionamento de recursos do Azure](Resource-health-faq.md)

