---
title: "máscara de dados dinâmicos do aaaAzure base de dados SQL | Documentos da Microsoft"
description: "Máscara de dados dinâmicos da base de dados SQL limita a exposição de dados confidenciais através da máscara os utilizadores de privilégio toonon"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: 4b36d78e-7749-4f26-9774-eed1120a9182
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/09/2017
ms.author: ronitr; ronmat
ms.openlocfilehash: 68b55128dc096f7e3dd0e5ed1427b39da5d64736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-dynamic-data-masking"></a>Máscara de dados dinâmicos da base de dados SQL

Máscara de dados dinâmicos da base de dados SQL limita a exposição de dados confidenciais através da máscara os utilizadores de privilégio toonon. 

Máscara de dados dinâmicos ajuda a impedir que os dados de toosensitive de acesso não autorizado ao ativar os clientes toodesignate quantidade de dados confidenciais de Olá tooreveal com um impacto mínimo na camada de aplicação Olá. É uma funcionalidade de segurança baseadas em políticas oculta dados confidenciais do Olá no conjunto de resultados de Olá de uma consulta através de campos de base de dados designada, enquanto os dados de Olá na base de dados de Olá não são alterados.

Por exemplo, um representante de serviço no Centro de atendimento telefónico pode identificar os chamadores por vários dígitos do seu número de cartão de crédito, mas esses dados itens não devem estar totalmente expostos toohello representante de serviço. Pode ser definida uma regra de máscara que, mas Olá de máscaras de todos os últimos quatro dígitos de qualquer número de cartão de crédito no conjunto de resultados de Olá qualquer consulta. Outro exemplo, uma máscara de dados adequada pode ser definidos tooprotect dados de informação identificativa (PII), para que um programador pode consultar os ambientes de produção para fins de resolução de problemas sem violar as normas de conformidade.

## <a name="sql-database-dynamic-data-masking-basics"></a>Noções básicas de máscara de dados dinâmica base de dados SQL
Configurar um política no Olá de máscara de dados dinâmicos portal do Azure ao selecionar a operação no painel de configuração de base de dados SQL ou painel de definições de máscara de dados dinâmico Olá.

### <a name="dynamic-data-masking-permissions"></a>Permissões de máscara de dados dinâmicos
Máscara de dados dinâmicos pode ser configurada por base de dados do Azure Olá, admin, administrador do servidor ou funções de responsável pela segurança.

### <a name="dynamic-data-masking-policy"></a>Política de máscara de dados dinâmicos
* **Utilizadores SQL excluídos da máscara** - um conjunto de utilizadores do SQL Server ou as identidades do AAD que obtêm dados sem máscara no Olá SQL resultados de consulta. Os utilizadores com privilégios de administrador são sempre excluídos da máscara e ver Olá dados original sem qualquer máscara.
* **Regras de máscara** -um conjunto de regras que definem Olá designado toobe campos mascarado e Olá máscara de função que é utilizada. Olá designado campos pode ser definido utilizando um nome de esquema de base de dados, o nome da tabela e o nome da coluna.
* **As funções de máscara** -um conjunto de métodos que controlam a exposição de Olá dos dados para diferentes cenários.

| Função de máscara | Lógica de máscara |
| --- | --- |
| **Predefinição** |**Completa máscara de dados de toohello de acordo com a tipos de Olá designado campos**<br/><br/>• Utilize XXXX ou Xs menos se o tamanho do campo Olá Olá for inferior a 4 carateres para tipos de dados de cadeia (nchar, ntext, nvarchar).<br/>• Utilizar um valor de zero para tipos de dados numérico (bigint, bits, decimal, int, dinheiro, numérico, smallint, em smallmoney, tinyint, vírgula flutuante, real).<br/>• Utilizar 01-01-1900 para tipos de dados de data/hora (data, datetime2, datetime, datetimeoffset, smalldatetime, hora).<br/>• Para SQL variant, Olá valor predefinido do tipo atual Olá é utilizado.<br/>• Para um documento XML Olá <masked/> é utilizado.<br/>• Utilizar um valor vazio para tipos de dados especiais (timestamp de tabela, hierarchyid, GUID, binary, imagem, os tipos geográficos varbinary). |
| **Cartão de crédito** |**Máscara de método, o que expõe Olá últimos quatro dígitos do Olá designado campos** e adiciona uma cadeia constante como um prefixo no formulário de Olá de um cartão de crédito.<br/><br/>XXXX-XXXX-XXXX-1234 |
| **Correio eletrónico** |**Máscara de método, o que expõe a primeira letra de Olá e substitui o domínio de Olá com XXX.com** utilizando um prefixo de constante de cadeia no formato Olá um endereço de e-mail.<br/><br/>aXX@XXXX.com |
| **Número aleatório** |**Máscara de método, o que gera um número aleatório** toohello de acordo com selecionados limites e os tipos de dados real. Se Olá designado limites é igual, Olá função de máscara é um número constante.<br/><br/>![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/1_DDM_Random_number.png) |
| **Texto personalizado** |**Método, que expõe Olá primeiro e último carateres de máscara** e adiciona uma cadeia de preenchimento personalizado no meio de Olá. Se for mais curta do que o prefixo de Olá exposto e o sufixo de cadeia original Olá, apenas os Olá preenchimento cadeia é utilizado. <br/>sufixo de prefixo [preenchimento]<br/><br/>![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/2_DDM_Custom_text.png) |

<a name="Anchor1"></a>

### <a name="recommended-fields-toomask"></a>Campos recomendados toomask
Olá motor de recomendações de ddm de autor, sinalizadores determinados campos da sua base de dados como campos potencialmente confidenciais, que podem ser ideais para máscara. Olá máscara de dados dinâmicos painel no portal de Olá, verá Olá recomendado colunas para a base de dados. Tudo o que precisa toodo é clique **adicionar máscara** para uma ou mais colunas e, em seguida, **guardar** tooapply uma máscara para estes campos.

## <a name="set-up-dynamic-data-masking-for-your-database-using-powershell-cmdlets"></a>Configurar para a base de dados utilizando cmdlets do Powershell de máscara de dados dinâmicos
Consulte [Cmdlets de base de dados SQL do Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx).

## <a name="set-up-dynamic-data-masking-for-your-database-using-rest-api"></a>Configurar a máscara de dados dinâmicos para a base de dados utilizando a REST API
Consulte [operações para bases de dados SQL do Azure](https://msdn.microsoft.com/library/dn505719.aspx).

