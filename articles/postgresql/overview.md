---
title: "aaaOverview da base de dados do Azure para o serviço de base de dados relacional PostgreSQL | Microsoft Docs"
description: "Fornece uma descrição geral da base de dados do Azure para o serviço de base de dados relacional PostgreSQL."
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.custom: mvc
ms.service: postgresql
ms.topic: overview
ms.date: 08/01/2017
ms.openlocfilehash: fd6821b56e5295b8b341d87b14d113f7a4b247c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-postgresql"></a>O que é a base de dados do Azure para PostgreSQL?

Base de dados do Azure para PostgreSQL é um serviço de base de dados relacional no Olá nuvem da Microsoft incorporada para programadores com base na versão de Comunidade Olá dos open source [PostgreSQL](https://www.postgresql.org/) motor de base de dados. Este serviço está em pré-visualização pública. Fornece a base de dados do Azure para PostgreSQL:
- Desempenho previsível, com vários níveis de serviço
- Dinâmica escalabilidade sem período de indisponibilidade de aplicações
- Elevada disponibilidade incorporada
- Proteção de dados

Todas estas funcionalidades requerem quase sem administração, e todos os são fornecidos sem custos adicionais. Estas funcionalidades permitem-lhe toofocus no desenvolvimento rápido de aplicações e acelerar o seu toomarket de tempo, em vez de alocar tempo precioso e de infraestrutura e de recursos toomanaging máquinas virtuais. Além disso, pode continuar toodevelop a aplicação com Olá abrir ferramentas de origem e de plataforma da sua preferência e fornecer com velocidade de Olá e eficiência a sua empresa exige sem ter toolearn competências de novo. 

Este artigo é uma tooAzure de introdução da base de dados PostgreSQL conceitos de núcleos e tooperformance relacionados funcionalidades, escalabilidade e capacidade de gestão. Consulte que estes rápida começa tooget que tiver iniciado:

- [Criar uma base de dados do Azure para PostgreSQL através do portal do Azure](quickstart-create-server-database-portal.md)
- [Criar uma base de dados do Azure para PostgreSQL utilizando Olá CLI do Azure](quickstart-create-server-database-azure-cli.md)

Para um conjunto de amostras de CLI do Azure e PowerShell, veja:

- [Exemplos da CLI do Azure para a base de dados do Azure para PostgreSQL](./sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a>Ajuste o desempenho e dimensione a capacidade sem períodos de indisponibilidade

Base de dados do Azure para o serviço de PostgreSQL atualmente oferece dois escalões de serviço: básico e padrão. Cada escalão de serviço oferece [diferentes níveis de desempenho, garantias IOPS e capacidades](concepts-service-tiers.md) cargas de trabalho do toosupport tooheavyweight simples da base de dados. Pode criar a primeira aplicação num servidor pequeno para alguns euros por mês e, em seguida, [alterar o nível de desempenho de Olá](scripts/sample-scale-server-up-or-down.md) no âmbito do serviço de camada manualmente ou programaticamente em qualquer necessidades de Olá toomeet de tempo da sua solução. Pode fazê-lo sem período de indisponibilidade tooyour aplicação ou um tooyour clientes. Ativa a escalabilidade dinâmica tootransparently a base de dados responder toorapidly alterar os requisitos de recursos e permite tooonly paga Olá recursos que necessita ao que precisar.

## <a name="monitoring-and-alerting"></a>Monitorização e alertas
Como a decidir quando toodial acima e abaixo? Utilizar a monitorização de desempenho incorporado Olá e funcionalidades, juntamente com as classificações de desempenho de Olá com base em unidades de computação de alertas. Utilizar estas ferramentas, pode avaliar rapidamente o impacto de Olá de dimensionamento de computação unidades cópias de segurança ou para baixo com base nas suas necessidades de desempenho atual ou prevista. Para obter mais informações, consulte [base de dados do Azure para PostgreSQL opções e desempenho: compreender o que está disponível em cada camada de serviço](./concepts-service-tiers.md).

## <a name="keep-your-app-and-business-running"></a>Mantenha a sua aplicação e o seu negócio operacionais
Líderes 99,99% disponibilidade (não disponível na pré-visualização) nível contrato de serviço (SLA), utiliza a tecnologia de uma rede global de datacenters gerida pela Microsoft, da indústria do Azure ajuda a manter a sua aplicação em execução 24/7. Com cada base de dados do Azure para o servidor de PostgreSQL, pode tirar partido de segurança incorporadas, tolerância a falhas e proteção de dados teria toobuy ou estrutura, criar e gerir. Com base de dados do Azure para PostgreSQL, cada escalão de serviço oferece um conjunto completo de funcionalidades de continuidade do negócio e as opções que pode utilizar tooget cópias de segurança e em execução e mantenha-se dessa forma. Pode utilizar [restauro de ponto no tempo](howto-restore-server-portal.md) tooreturn tooan uma base de dados de estado anteriormente, até 35 dias. Além disso, se o datacenter de Olá que aloja as bases de dados sofrer uma falha, pode restaurar bases de dados de georredundante cópias das cópias de segurança recentes.

## <a name="secure-your-data"></a>Proteger os dados
Serviços de base de dados do Azure tem um tradição de segurança de dados que a base de dados do Azure para PostgreSQL mantém com funcionalidades que limitam o acesso, proteger dados em rest e em movimento e ajudam a monitorizar a atividade. Visite Olá [Centro de fidedignidade do Azure](https://www.microsoft.com/TrustCenter/Security/default.aspx) para obter informações sobre a segurança da plataforma do Azure.

Olá base de dados do Azure para o serviço de PostgreSQL utiliza a encriptação de armazenamento para dados em rest. Incluindo cópias de segurança de dados são encriptados em disco (com exceção de Olá dos ficheiros temporários criados pelo motor de Olá durante a execução de consultas). serviço Olá utiliza cifras AES 256 bits que está incluída na encriptação de armazenamento do Azure e as chaves de Olá são gerido de sistema. Encriptação de armazenamento está sempre ativada e não pode ser desativada.

Por predefinição, Olá base de dados do Azure para o serviço PostgreSQL é configurado toorequire [segurança de ligação SSL](./concepts-ssl-connection-security.md) para dados em movimento através de rede de Olá. Imposição de ligações de SSL entre o servidor de base de dados e as aplicações de cliente ajuda a proteger contra ataques "man no meio de Olá" ao encriptar o fluxo de dados de Olá entre o servidor de Olá e a sua aplicação.  Opcionalmente, pode desativar exigir o SSL para estabelecer a ligação de serviço de base de dados de tooyour se a aplicação de cliente não suporta a conectividade SSL.

## <a name="next-steps"></a>Passos seguintes
- Consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/postgresql/) para comparações de preços e calculadoras.
- Introdução por [criar a sua primeira base de dados do Azure para PostgreSQL](./quickstart-create-server-database-portal.md).
- Criar a sua primeira aplicação no Python, PHP, Ruby, C\#, Java, Node.js: [bibliotecas de ligação](./concepts-connection-libraries.md)
