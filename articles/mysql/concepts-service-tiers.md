---
title: "AAA \"escalões de preço na base de dados do Azure para MySQL | Microsoft Docs\""
description: "Escalões de preço na base de dados do Azure para MySQL"
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 2a05f00aff4f7166f04e035eb2a47e7662888ebc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-options-and-performance-understand-whats-available-in-each-pricing-tier"></a>Base de dados do Azure para MySQL opções e desempenho: compreender o que está disponível em cada escalão de preço
Quando cria uma base de dados do Azure para o servidor de MySQL, decidir após três escolhas principais recursos de Olá tooconfigure atribuídos a esse servidor. Estas opções de impacto no desempenho de Olá e o dimensionamento do servidor de Olá.
- Escalão de preço
- Unidades de Computação
- Armazenamento (GB)

Cada escalão de preço tem um intervalo de desempenho toochoose níveis (unidades de computação), dependendo dos requisitos de cargas de trabalho. Níveis de desempenho superiores fornecem recursos adicionais para o servidor toodeliver concebida maior débito. Pode alterar o nível de desempenho do servidor de Olá dentro de um escalão de preço virtualmente sem período de indisponibilidade de aplicações.

> [!IMPORTANT]
> Enquanto serviço Olá está em pré-visualização pública, não há um contrato de nível de serviço (SLA) garantida.

Dentro de uma Base de Dados do Azure para o servidor MySQL, pode ter uma ou várias bases de dados. Pode optar ativamente por participar toocreate uma base de dados individual por servidor tooutilize todos os recursos de Olá ou criar várias bases de dados tooshare recursos Olá. 

## <a name="choose-a-pricing-tier"></a>Escolha um escalão de preço
Enquanto na pré-visualização, base de dados do Azure para MySQL oferece dois escalões de preços: básico e padrão. Escalão Premium ainda não está disponível, mas estará disponível em breve. 

Olá tabela seguinte fornece exemplos de Olá preços camadas mais adequadas para cargas de trabalho de aplicação diferente.

| Escalão de preço | Cargas de trabalho de destino |
| :----------- | :----------------|
| Básica | Mais adequada para pequenas cargas de trabalho que necessitam de armazenamento e computação escalável sem garantir de IOPS. Os exemplos incluem servidores utilizados para programação ou testes ou dimensionamento pequeno raramente utilizadas aplicações. |
| Standard | Olá toooption de ir para a nuvem aplicações que precisam de IOPS garantir com débito elevado. Os exemplos incluem web ou aplicações analíticas. |
| Premium | Melhor adequados para cargas de trabalho que necessitam de latência baixa para transações e/s. Fornece suporte melhor Olá para muitos utilizadores em simultâneo. Toodatabases aplicável que suportam aplicações fundamentais.<br />o escalão de preço do Olá Premium não está disponível na pré-visualização. |

toodecide sobre um preços da camada, primeiro início ao determinar se a carga de trabalho tem uma garantia IOPS. Se assim for, utilize o escalão de preço padrão.

| **Funcionalidades do escalão de preço** | **Básica** | **Standard** |
| :------------------------ | :-------- | :----------- |
| Unidades de processamento máximo | 100 | 800 | 
| Máximo de armazenamento total | 1 TB | 1 TB | 
| Garantia IOPS de armazenamento | N/D | Sim | 
| IOPS máximo de armazenamento | N/D | 3000 | 
| Período de retenção de cópias de segurança de base de dados | 7 dias | 35 dias | 

Durante o período de tempo de pré-visualização Olá, não é possível alterar o escalão de preço assim que o servidor de Olá é criado. No futuro, Olá, será possível tooupgrade possíveis ou mudar de um servidor a partir de um escalão de tooanother escalão de preço.

## <a name="understand-hello-price"></a>Compreender o preço de Olá
Quando cria uma nova base de dados do Azure para MySQL dentro Olá [Portal do Azure](https://portal.azure.com/#create/Microsoft.MySQLServer), clique em Olá **escalão de preço** painel e Olá custo mensal serão apresentadas com base nas opções de Olá que selecionou. Se não tiver uma subscrição do Azure, utilize Olá tooget Calculadora preço um preço estimado do Azure. Visite Olá [Calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/) Web site, em seguida, clique em **adicionar itens**, expanda Olá **bases de dados** categoria e escolha **base de dados do Azure para MySQL**  opções de Olá toocustomize.

## <a name="choose-a-performance-level-compute-units"></a>Escolha o nível de desempenho (computação unidades)
Depois de ter determinado Olá escalão de preço da base de dados do Azure para o servidor de MySQL, está pronto toodetermine nível de desempenho de Olá selecionando o número de Olá de unidades de computação for necessário. Um ponto de partida é 200 ou 400 unidades de computação para aplicações que necessitam de maior simultaneidade de utilizador para os seus web ou cargas de trabalho analíticas e ajustar incrementalmente conforme necessário. 

Computação unidades são uma medida de débito de processamento de CPU que fique tooa disponíveis toobe única base de dados do Azure para o servidor de MySQL. Uma unidade de computação é uma medida combinada de CPU e memória recursos.  Para obter mais informações, consulte [explicar unidades de computação](concepts-compute-unit-and-storage.md)

### <a name="basic-pricing-tier-performance-levels"></a>Básico preço camada níveis de desempenho:

| **Nível de desempenho** | **50** | **100** |
| :-------------------- | :----- | :------ |
| Unidades de computação máx. | 50 | 100 |
| Tamanho de armazenamento incluídos | 50 GB | 50 GB |
| Tamanho máximo de armazenamento de servidor\* | 1 TB | 1 TB |

### <a name="standard-pricing-tier-performance-levels"></a>Standard preço camada níveis de desempenho:

| **Nível de desempenho** | **100** | **200** | **400** | **800** |
| :-------------------- | :------ | :------ | :------ | :------ |
| Unidades de computação máx. | 100 | 200 | 400 | 800 |
| Tamanho de armazenamento incluídos e IOPS aprovisionado | 125 GB,<br/> 375 IOPS | 125 GB,<br/> 375 IOPS | 125 GB,<br/> 375 IOPS | 125 GB,<br/> 375 IOPS |
| Tamanho máximo de armazenamento de servidor\* | 1 TB | 1 TB | 1 TB | 1 TB |
| Servidor de máx. aprovisionado IOPS | 3,000 IOPS | 3,000 IOPS | 3,000 IOPS | 3,000 IOPS |
| Servidor de máx. aprovisionado IOPS por GB | Corrigido 3 IOPS por GB | Corrigido 3 IOPS por GB | Corrigido 3 IOPS por GB | Corrigido 3 IOPS por GB |

\*Tamanho máximo de armazenamento de servidor refere-se o tamanho de armazenamento aprovisionado máximo toohello para o servidor.

## <a name="storage"></a>Armazenamento 
configuração de armazenamento Olá define a quantidade de Olá de armazenamento capacidade disponível tooan base de dados do Azure para o servidor de MySQL. armazenamento de Olá utilizado pelo serviço de Olá inclui ficheiros de base de dados de Olá, registos de transações e registos do servidor Olá MySQL. Considere o tamanho de armazenamento necessária toohost Olá as bases de dados e Olá requisitos de desempenho (IOPS), ao selecionar configuração de armazenamento Olá.

Alguns capacidade de armazenamento está incluída no mínimo, com cada escalão de preço, que anotou no Olá anterior a tabela como "Tamanho de armazenamento incluídos". Pode ser adicionada a capacidade de armazenamento adicional quando é criado servidor Olá, em incrementos de 125 GB, segurança de armazenamento máxima permitida toohello. capacidade de armazenamento adicional Olá pode ser configurada independentemente da configuração de computação unidades Olá. alterações de preços de Olá com base na quantidade de Olá de armazenamento selecionada.

configuração de IOPS Olá em cada nível de desempenho relacionado com toohello tamanho de armazenamento de Olá escolhido e escalão de preço. O escalão básico não fornece uma garantia IOPS. Dentro do escalão de preço padrão de Olá, Olá IOPS Dimensionar proporcionalmente toomaximum tamanho de armazenamento de um rácio de 3:1 fixo. armazenamento de Olá incluída de garantias de 125 GB para 375 aprovisionado IOPS, cada um com um tamanho de e/s de cópia de segurança too256 KB. Pode escolher armazenamento adicional de segurança too1 TB no máximo, tooguarantee 3,000 aprovisionado IOPS.

Gráfico de métricas de Olá de monitor no Olá Azure portal ou de escrita CLI do Azure comandos toomeasure Olá consumo de armazenamento e de IOPS. Métricas relevantes toomonitor são limite de armazenamento, a percentagem de armazenamento, armazenamento utilizado e percentagem de e/s.

>[!IMPORTANT]
> Enquanto na pré-visualização, selecione quantidade Olá de armazenamento momento Olá quando o servidor de Olá é criado. Ainda, o tamanho de armazenamento Olá num servidor existente a alteração não é suportado. 

## <a name="scaling-a-server-up-or-down"></a>Dimensionamento de um servidor de cópia de segurança ou para baixo
Pode escolher inicialmente Olá nível de desempenho e o escalão de preço, ao criar a base de dados do Azure para MySQL. Mais tarde, pode dimensionar Olá computação unidades ou reduzir vertical dinamicamente, dentro do intervalo de Olá de Olá mesmo escalão de preço. Olá portal do Azure, deslize Olá computação unidades no painel de escalão de preço do servidor de Olá ou script-la seguindo este exemplo: [monitorizar e dimensionar uma base de dados do Azure para o servidor de MySQL utilizando a CLI do Azure](scripts/sample-scale-server.md)

Olá computação unidades de dimensionamento é feito independentemente do tamanho de armazenamento máximo Olá que escolheu.

Em segundo plano do Olá, alterar o nível de desempenho de Olá de uma base de dados cria uma réplica da base de dados original Olá ao nível de desempenho novo Olá e, em seguida, passa ligações toohello réplica. Não se tenha perdido nenhum dado durante este processo. Durante Olá breve neste momento quando iremos comutador através de réplica toohello, base de dados do ligações toohello estão desativadas, para que alguns as transações em trânsito podem ser revertidas. Esta janela varia, mas demora em média em 4 segundos, e em mais de 99% dos casos, demora menos de 30 segundos. Se existirem grandes quantidades de transações em trânsito em ligações de momento Olá estão desativadas, esta janela pode ser maior.

duração de Olá do processo de escala completa Olá depende do tamanho Olá e escalão de preço do servidor de Olá antes e depois de alterar Olá. Por exemplo, um servidor que está a alterar unidades de computação dentro do escalão de preço padrão de Olá, deve ser concluído dentro de alguns minutos. Propriedades da nova Olá para o servidor de Olá não são aplicadas até que as alterações de Olá estiverem concluídas.

## <a name="next-steps"></a>Passos Seguintes
- Para mais informações sobre unidades de computação, consulte [explicar unidades de computação](concepts-compute-unit-and-storage.md)
- Saiba como demasiado[monitorizar e dimensionar uma base de dados do Azure para o servidor de MySQL utilizando a CLI do Azure](scripts/sample-scale-server.md)
