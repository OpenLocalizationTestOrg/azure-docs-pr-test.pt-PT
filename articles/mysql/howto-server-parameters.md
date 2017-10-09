---
title: "aaaHow tooConfigure parâmetros de servidor na base de dados do Azure para MySQL | Microsoft Docs"
description: "Este artigo descreve como parâmetros de servidor disponível tooconfigure na base de dados do Azure para utilizar o MySQL Olá portal do Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/19/2017
ms.openlocfilehash: 8292c8eda605854a06b6a9c82185c857bd353cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-server-parameters-in-azure-database-for-mysql-using-hello-azure-portal"></a>Como parâmetros de servidor tooconfigure na base de dados do Azure para utilizar o MySQL Olá portal do Azure

Base de dados do Azure para MySQL suporta a configuração do alguns parâmetros de servidor. Este artigo descreve como tooconfigure suportado estes parâmetros utilizando Olá portal do Azure e Olá apresenta uma lista de parâmetros, os valores predefinidos de Olá e Olá intervalo de valores válidos. Nem todos os parâmetros de servidor podem ser ajustados. Olá apenas aqueles aqui listados são suportadas.

## <a name="navigate-tooserver-parameters-blade-on-azure-portal"></a>Navegue até o painel de parâmetros de tooServer no portal do Azure

Inicie sessão no portal do Azure de toohello e clique em sua base de dados do Azure para o nome do servidor MySQL. Em Olá **definições** secção, clique em **parâmetros do** tooopen Olá servidor Parâmetros Painel Olá base de dados do Azure para MySQL.

![Painel de parâmetros de servidor do portal do Azure](./media/howto-server-parameters/auzre-portal-server-parameters.png)

## <a name="list-of-configurable-server-parameters"></a>Lista de parâmetros de servidor configurável

Olá a tabela seguinte lista os parâmetros de servidor Olá atualmente suportada. parâmetros de Olá podem ser configurados de acordo com tooyour os requisitos da aplicação.

> [!div class="mx-tableFixed"]
|Nome do Parâmetro|Valor predefinido|intervalo|Descrição|
|---|---|---|---|
|binlog_group_commit_sync_delay|1000|0, 11-1000000|Controlos microssegundos quantos Olá aguarda de consolidação do registo binário antes da sincronização toodisk de ficheiro de registo binário Olá.|
|binlog_group_commit_sync_no_delay_count|0|0-1000000|número máximo de Olá de transações toowait para antes de abortar atraso atual do Olá tal como especificado pelo binlog-grupo-commit-sync-atraso.|
|character_set_server|LATIN1|BIG5, UTF8MB4, etc.|Utilize charset_name como conjunto de carateres de servidor de predefinição Olá.|
|div_precision_increment|4|0-30|Número de dígitos por que escala de Olá tooincrease do resultado de Olá das operações de divisão.|
|group_concat_max_len|1024|4-16777216|Resultado o comprimento máximo permitido em bytes para Olá GROUP_CONCAT().|
|innodb_adaptive_hash_index|ON|DESATIVADO|Indica se os índices de hash adaptável innodb estão ativados ou desativados.|
|innodb_lock_wait_timeout|50|1-3600|comprimento de Olá de tempo em segundos uma transação InnoDB aguarda que um bloqueio de linha antes de desistir.|
|interactive_timeout|1800|10-1800|Número de servidor de Olá segundos aguarda para a atividade de uma ligação antes de o fechar, interativa.|
|log_bin_trust_function_creators|OFF|DESATIVADO|Esta variável é aplicável aplica quando o registo binário está ativado. Controla se a função armazenada criadores podem ser fidedigno não toocreate armazenada as funções que causam toobe insegura eventos escritos no registo binário toohello.|
|log_queries_not_using_indexes|OFF|DESATIVADO|Consultas de registos que são esperados tooretrieve todos os registo de consultas de tooslow de linhas.|
|log_slow_admin_statements|OFF|DESATIVADO|Incluem instruções administrativas lentas nas instruções de Olá escritos no registo de consultas lenta de toohello.|
|log_throttle_queries_not_using_indexes|0|0-4294967295|Os limites Olá diversas estas consultas por minuto que podem ser escritos no registo de consultas lenta de toohello.|
|long_query_time|10|1-1E + 100|Se uma consulta demora mais que este número de segundos, o servidor Olá incrementa a variável de estado de Slow_queries Olá.|
|max_allowed_packet|536870912|1024-1073741824|tamanho máximo de Olá de um pacote ou qualquer cadeia gerado/intermédio ou qualquer parâmetro enviada pelo Olá mysql_stmt_send_long_data() função da API de C.|
|min_examined_row_limit|0|0-18446744073709551615|Os registos de consultas que tenham superior ao número de Olá configurado de linhas no registo de consultas lenta de Olá. |
|server_id|3293747068|1000-4294967295|ID do servidor Olá, utilizada na replicação toogive cada principal e slave uma identidade exclusiva.|
|slave_net_timeout|60|30-3600|número de Olá de toowait segundos para obter mais dados do master Olá antes multisservidor Olá considera ligação Olá quebrada, interrompe Olá ler e tenta tooreconnect.|
|slow_query_log|OFF|DESATIVADO|Ativar ou desativar o registo de consultas lenta de Olá.|
|sql_mode|0 selecionado|ALLOW_INVALID_DATES, IGNORE_SPACE, etc.|Olá servidor SQL o modo atual.|
|time_zone|SISTEMA|Exemplos: -8:00, +05: 30|Olá servidor fuso horário.|
|wait_timeout|120|60-240|número de Hello do servidor de Olá segundos aguarda para a atividade de uma ligação noninteractive antes de o fechá-lo.|

## <a name="next-steps"></a>Passos seguintes
- [Bibliotecas de ligação para base de dados do Azure para MySQL](concepts-connection-libraries.md)
