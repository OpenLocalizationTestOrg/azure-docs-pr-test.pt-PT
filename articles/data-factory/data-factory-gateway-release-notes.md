---
title: notas de aaaRelease do Data Management Gateway | Microsoft Docs
description: "Notas de versão do Data Management Gateway tory"
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 3165d7537410a0531e0bb7f7fe584767f9155574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-data-management-gateway"></a>Notas de lançamento do Gateway de Gestão de Dados
Um dos desafios de Olá para integração de dados modernas é toomove dados tooand de toocloud no local. Fábrica de dados torna esta integração com o Data Management Gateway, que é um agente que pode instalar o movimento de dados no local tooenable híbrida.

Consulte Olá seguintes artigos para obter informações detalhadas sobre o Data Management Gateway e como toouse-lo:

*  [Data Management Gateway](data-factory-data-management-gateway.md)
*  [Mover dados entre no local e na nuvem utilizando o Azure Data Factory](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a>VERSÃO ATUAL (2.10.6347.7)

### <a name="enhancements-"></a>Melhoramentos-
- Pode adicionar barramento de serviço de toowhitelist de entradas DNS, em vez de adicionar à lista branca todos os endereços IP do Azure da sua firewall (se necessário). Pode encontrar a respetiva entrada DNS no portal do Azure (Data Factory -> 'Criar e implementar' -> 'Gateways' -> "serviceUrls" (no JSON)
- Conector do HDFS suporta agora autoassinado certificado público, permitindo-lhe ignorar a validação de SSL.
- Fixo: Problema com o gateway offline durante a atualização (devido tooclock desfasamento)



## <a name="earlier-versions"></a>Versões anteriores

## <a name="2963132"></a>2.9.6313.2
### <a name="enhancements-"></a>Melhoramentos-
-   Pode adicionar entradas DNS toowhitelist Service Bus, em vez de adicionar à lista branca todos os endereços IP do Azure da sua firewall (se necessário). Obter mais detalhes aqui.
-   Agora pode copiar dados de/para um blob de bloco única cópia de segurança too4.75 TB, que é o tamanho de Olá máx. suportado de BLOBs de blocos. (limite anterior era 195 GB).
-   Fixa: Fora de problema de memória ao unzipping vários ficheiros pequenos durante a atividade de cópia.
-   Fixo: Índice fora do problema do intervalo ao copiar de Document DB tooan no local do SQL Server com a funcionalidade de idempotency.
-   Fixo: Script de limpeza do SQL Server não funciona com o servidor de SQL no local do Assistente para copiar.
-   Fixo: Nome de coluna com o espaço no final de Olá não funciona na atividade de cópia.

## <a name="28662833"></a>2.8.66283.3
### <a name="enhancements-"></a>Melhoramentos-
- Fixo: Problema com a falta de credenciais no reinício do computador de gateway.
- Fixo: Problema com o registo durante gateway restaurar o utilizando um ficheiro de cópia de segurança.


## <a name="2762401"></a>2.7.6240.1
### <a name="enhancements-"></a>Melhoramentos-
- Fixa: Leitura incorreta de um valor nulo Decimal do Oracle como origem.

## <a name="2661922"></a>2.6.6192.2
### <a name="whats-new"></a>Novidades
- Os clientes podem fornecer comentários no gateway registar experiência.
- Suportar um novo formato de compressão: ZIP (Deflate)

### <a name="enhancements-"></a>Melhoramentos-
- Melhoramento de desempenho para Sink do Oracle, origem HDFS.
- Correção de erros para automático de gateway atualizar, capacidade de processamento paralelo de gateway.


## <a name="2561641"></a>2.5.6164.1
### <a name="enhancements"></a>Melhoramentos
- Melhor e mais robusta Gateway registo experiência-agora pode controlar o estado do progresso durante o processo de registo do Olá Gateway, que faz com que o registo de Olá experiência mais dinâmico.
- Melhoria no Gateway restaurar processo - que pode continuar a recuperar gateway, mesmo se não tiver ficheiros de cópia de segurança de gateway de Olá com esta atualização. Isto seria requerem credenciais de serviço ligado de tooreset no Portal.
- Correção de erro.

## <a name="2461511"></a>2.4.6151.1

### <a name="whats-new"></a>Novidades

- Agora pode armazenar credenciais da origem de dados localmente. Olá credenciais estão encriptadas. credenciais de origens de dados de Olá podem ser recuperadas e restaurados com autoridade utilizando o ficheiro de cópia de segurança de Olá que pode ser exportado da Olá existente Gateway, todos os no local.

### <a name="enhancements-"></a>Melhoramentos-

- Experiência de registo de Gateway melhor e mais robusta.
- Suporta a deteção automática da configuração de QuoteChar para formato de texto no Assistente para copiar e melhorar Olá global Formatar precisão de deteção.

## <a name="2361002"></a>2.3.6100.2

- Suporte firstRowAsHeader e a deteção automática SkipLineCount no Assistente de cópia de ficheiros de texto no sistema de ficheiros no local e HDFS.
- Melhorar a estabilidade Olá de ligação de rede entre o gateway e o Service Bus
- Algumas correções de erros


## <a name="2260721"></a>2.2.6072.1

*  Suporta a definição de proxy HTTP para utilizar o gateway Olá Olá Gestor de configuração do Gateway. Se configurado, o Blob do Azure, tabelas do Azure, Azure Data Lake e Document DB são acedidos através do proxy HTTP.
*  Processamento de TextFormat ao copiar dados a partir de cabeçalho de suporta / tooAzure Blob, o Azure Data Lake Store, sistema de ficheiros no local e no local HDFS.
*  Suporta a copiar dados de BLOBs de acréscimo e BLOBs de páginas, juntamente com Olá já suportadas BLOBs de blocos.
*  Apresenta um novo estado do gateway **Online (limitado)**, que indica que essa funcionalidade principal de Olá do gateway de Olá funciona, exceto o suporte de operação interativa Olá para o Assistente para copiar.
*  Melhora robustez Olá do registo de gateway utilizando a chave de registo.

## <a name="216040"></a>2.1.6040.

*  Controlador DB2 está incluído no pacote de instalação do gateway Olá agora. Não é necessário tooinstall-lo em separado.
*  Controlador DB2 suporta agora o z/SO e DB2 para posso (como / 400) juntamente com plataformas Olá já suportadas (Linux, Unix e Windows).
*  Suporta a utilização de base de dados do Azure Cosmos como uma origem ou de destino para os arquivos de dados no local
*  Suporta a copiar o armazenamento de BLOBs de/toocold/frequente de dados, juntamente com Olá já suportadas conta do storage para fins gerais.
*  Permite-lhe tooconnect tooon local do SQL Server através do gateway com privilégios de início de sessão remoto.  

## <a name="2060131"></a>2.0.6013.1

*  Pode selecionar Olá cultura do idioma toobe utilizado por um gateway durante a instalação manual.

*  Quando o gateway não funciona conforme esperado, pode escolher os registos do gateway toosend dos últimos sete dias tooMicrosoft toofacilitate resolução de problemas do problema Olá. Se o gateway não está ligado toohello o serviço em nuvem, pode escolher toosave e arquivar registos do gateway.  

*  Melhoramentos de interface de utilizador para o Gestor de configuração do gateway:

    *  Tornar o estado do gateway mais visíveis no separador de início de Olá.

    *  Controlos reorganizados e simplificados.

    *  Pode copiar dados de um armazenamento utilizando Olá [ferramenta de pré-visualização de cópia sem código](data-factory-copy-data-wizard-tutorial.md). Consulte [testado cópia](data-factory-copy-activity-performance.md#staged-copy) para obter detalhes sobre esta funcionalidade em geral.
*  Pode utilizar dados de tooingress do Data Management Gateway diretamente a partir de uma base de dados do SQL Server no local para o Azure Machine Learning.

*  Melhorias de desempenho

    * Melhore o desempenho sobre a visualização de esquema/pré-visualização contra do SQL Server na ferramenta de pré-visualização de cópia sem código.

## <a name="11259531"></a>1.12.5953.1

*  Correções de erros

## <a name="11159181"></a>1.11.5918.1

*  Tamanho máximo do registo de eventos do gateway Olá aumentou de 1 MB too40 MB.

*  Uma caixa de diálogo de aviso é apresentada no caso seja necessário um reinício durante a atualização automática do gateway. Pode escolher toorestart direito, em seguida, ou posterior.

*  No caso de falha de atualização automática, o instalador do gateway repete a atualização automática três vezes no máximo.

*  Melhorias de desempenho

    * Melhore o desempenho para carregar tabelas grandes a partir do servidor no local, num cenário de cópia sem código.

*  Correções de erros

## <a name="11058921"></a>1.10.5892.1

*  Melhorias de desempenho

*  Correções de erros

## <a name="1958652"></a>1.9.5865.2

*  Capacidade de atualização de automática zero touch
*  Ícone de tabuleiro novo com indicadores de estado do gateway
*  Capacidade demasiado "atualizar agora" do cliente de Olá
*  Hora de agendamento de atualização de tooset de capacidade
*  Script do PowerShell para ativando ou desativando a atualização automática /
*  Suporte para o formato JSON  
*  Melhorias de desempenho
*  Correções de erros

## <a name="1858221"></a>1.8.5822.1

*  Melhorar a experiência de resolução de problemas
*  Melhorias de desempenho
*  Correções de erros

### <a name="1757951"></a>1.7.5795.1

*  Melhorias de desempenho
*  Correções de erros

### <a name="1757641"></a>1.7.5764.1

*  Melhorias de desempenho
*  Correções de erros

### <a name="1657351"></a>1.6.5735.1

*  Suporte no local HDFS origem/Sink
*  Melhorias de desempenho
*  Correções de erros

### <a name="1656961"></a>1.6.5696.1

*  Melhorias de desempenho
*  Correções de erros

### <a name="1656761"></a>1.6.5676.1

*  Ferramentas de diagnóstico de suporte no Configuration Manager
*  Colunas de tabela de suporte para origens de dados em tabela do Azure Data Factory
*  Suporte de armazém de dados SQL do Azure Data Factory
*  Suporte Reclusive BlobSource e FileSource do Azure Data Factory
*  Suporta CopyBehavior – MergeFiles, PreserveHierarchy e FlattenHierarchy BlobSink e FileSink com cópia binária do Azure Data Factory
*  Suporta a atividade de cópia de relatório de progresso do Azure Data Factory
*  Validação da conectividade de origem de dados de suporte do Azure Data Factory
*  Correções de erros

### <a name="1656721"></a>1.6.5672.1

*  Nome da tabela de suporte para a origem de dados ODBC do Azure Data Factory
*  Melhorias de desempenho
*  Correções de erros

### <a name="1656581"></a>1.6.5658.1

*  Sink do ficheiro de suporte do Azure Data Factory
*  Suporte preservar hierarquia na cópia de binária para o Azure Data Factory
*  Suporta Idempotency de atividade de cópia do Azure Data Factory
*  Correções de erros

### <a name="1656401"></a>1.6.5640.1

*  Suporte 3 mais origens de dados para o Azure Data Factory (ODBC OData, HDFS)
*  Suporte caráter da plica no parser de csv para o Azure Data Factory
*  Suporte de compressão (BZip2)
*  Correções de erros

### <a name="1556121"></a>1.5.5612.1

*  Suporta cinco bases de dados relacionais (MySQL, PostgreSQL, DB2, Teradata e Sybase) do Azure Data Factory
*  Suporte de compressão (Gzip e Deflate)
*  Melhorias de desempenho
*  Correções de erros

### <a name="1455491"></a>1.4.5549.1

*  Adicionar suporte de origem de dados Oracle para o Azure Data Factory
*  Melhorias de desempenho
*  Correções de erros

### <a name="1454921"></a>1.4.5492.1

*  Binário unificado que suporte serviços do Microsoft Azure Data Factory e Office 365 Power BI
*  Otimizar o processo de IU de configuração e registo Olá
*  O Azure Data Factory – suportam a entrada do Azure e de saída para a origem de dados do SQL Server

### <a name="1253031"></a>1.2.5303.1

*  Corrija toosupport de problema de tempo limite mais ligações de origens de dados morosa.

### <a name="1155268"></a>1.1.5526.8

*  Requer o .NET Framework 4.5.1 como pré-requisito durante a configuração.

### <a name="1051442"></a>1.0.5144.2

*  Não existem alterações que afetam os cenários do Azure Data Factory.
