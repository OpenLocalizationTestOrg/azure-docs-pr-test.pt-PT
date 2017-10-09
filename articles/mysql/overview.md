---
title: "aaaOverview da base de dados do Azure para o serviço de base de dados relacional MySQL | Microsoft Docs"
description: "Descrição geral do Olá base de dados do Azure para o serviço de base de dados relacional MySQL."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 08/02/2017
ms.custom: mvc
ms.openlocfilehash: f02493e2c3c38ccab408a718f98861600481812d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-mysql-service-introduction"></a>O que é a base de dados do Azure para MySQL? Introdução de serviço
Base de dados do Azure para MySQL é um serviço de base de dados relacional no Olá com base na nuvem da Microsoft [MySQL Comunidade edição](https://www.mysql.com/products/community/) motor de base de dados.  Fornece a base de dados do Azure para MySQL:

- Desempenho previsível, com vários níveis de serviço
- Dinâmica escalabilidade sem período de indisponibilidade de aplicações
- Elevada disponibilidade incorporada
- Proteção de dados

Estas capacidades requerem quase sem administração, e todos os são fornecidos sem custos adicionais. Estas permitem-lhe toofocus no desenvolvimento rápido de aplicações e acelerar o seu toomarket de tempo, em vez de atribuir tempo precioso e de infraestrutura e de recursos toomanaging máquinas virtuais. Além disso, pode continuar toodevelop a aplicação com Olá abrir ferramentas de origem e de plataforma da sua preferência e fornecer com velocidade de Olá e eficiência a sua empresa exige sem ter toolearn competências de novo.

![Base de dados do Azure para o diagrama conceptual MySQL](media/overview/1-azure-db-for-mysql-conceptual-diagram.png)

Este artigo é uma tooAzure de introdução da base de dados para conceitos principais de MySQL e tooperformance relacionados funcionalidades, escalabilidade e capacidade de gestão, com detalhes de tooexplore ligações. Consulte que estes rápida começa tooget que tiver iniciado:
- [Criar uma Base de Dados do Azure para o servidor MySQL com o portal do Azure](quickstart-create-mysql-server-database-using-azure-portal.md)
- [Criar uma Base de Dados do Azure para o servidor MySQL com a CLI do Azure](quickstart-create-mysql-server-database-using-azure-cli.md)

Para um conjunto de exemplos de CLI do Azure, consulte:
- [Exemplos da CLI do Azure para a base de dados do Azure para MySQL](sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a>Ajuste o desempenho e dimensione a capacidade sem períodos de indisponibilidade
Base de dados do Azure para o serviço de MySQL oferece dois escalões de serviço: básico e padrão. Cada camada oferece desempenho diferentes e cargas de trabalho do capacidades toosupport tooheavyweight simples da base de dados. Pode criar a primeira aplicação numa base de dados pequena para utilizados no compromisso alguns um mês, em seguida, altere o tooscale de camada de serviço com necessidades da sua solução sem período de indisponibilidade. Escalabilidade dinâmica permite que a sua toorapidly respondeu do tootransparently de base de dados alterar os requisitos de recursos. Só paga pelos recursos Olá que precisa de, quando que precisar.

## <a name="monitoring-and-alerting"></a>Monitorização e alertas
Como saber Olá paragem certo quando aumentar e reduzir verticalmente? Utilizar a monitorização de desempenho incorporado Olá e funcionalidades, juntamente com as classificações de desempenho de Olá com base na unidade de computação de alerta. Utilizar estas funcionalidades, pode avaliar rapidamente impacto Olá de aumentar ou reduzir verticalmente com base na sua atual ou necessidades de desempenho do projeto. Consulte [conceitos: escalões de serviço](concepts-service-tiers.md) para obter mais detalhes.

## <a name="keep-your-app-and-business-running"></a>Mantenha a sua aplicação e o seu negócio operacionais
Líderes 99,99% disponibilidade nível contrato de serviço (SLA), utiliza a tecnologia de uma rede global de datacenters gerida pela Microsoft, da indústria do Azure ajuda a manter a sua aplicação em execução 24/7. Com cada base de dados do Azure para o servidor de MySQL, pode tirar partido de segurança incorporadas, tolerância a falhas e proteção de dados teria toobuy ou estrutura, criar e gerir. Com base de dados do Azure para MySQL, pode utilizar o restauro de ponto no tempo toorecover tooan um servidor de estado anteriormente, até 35 dias.

## <a name="secure-your-data"></a>Proteger os dados
Serviços de base de dados do Azure tem um tradição de segurança de dados que a base de dados do Azure para MySQL mantém com funcionalidades que limitam o acesso, proteger dados em rest e em movimento e ajudam a monitorizar a atividade. Visite Olá [Centro de fidedignidade do Azure](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx) para obter informações sobre a segurança da plataforma do Azure.

Olá base de dados do Azure para o serviço de MySQL utiliza a encriptação de armazenamento para dados em rest. Dados incluindo cópias de segurança, são encriptados em disco (com exceção de Olá dos ficheiros temporários criados pelo motor de Olá durante a execução de consultas). serviço Olá utiliza cifras AES 256 bits que está incluída na encriptação de armazenamento do Azure e as chaves de Olá são gerido de sistema. Encriptação de armazenamento está sempre ativada e não pode ser desativada.

Por predefinição, Olá base de dados do Azure para o serviço de MySQL é configurado toorequire [segurança de ligação SSL](./concepts-ssl-connection-security.md) para dados em movimento através de rede de Olá. Imposição de ligações de SSL entre o servidor de base de dados e as aplicações de cliente ajuda a proteger contra ataques "man no meio de Olá" ao encriptar o fluxo de dados de Olá entre o servidor de Olá e a sua aplicação.  Opcionalmente, pode desativar exigir o SSL para estabelecer a ligação de serviço de base de dados de tooyour se a aplicação de cliente não suporta a conectividade SSL.

## <a name="next-steps"></a>Passos Seguintes
Agora que já tiver um tooAzure de introdução da base de dados de leitura para o MySQL e respondidas pergunta Olá "Qual é a base de dados do Azure para MySQL?", está pronto para:
- Consulte Olá página para comparações de preços e calculadoras de preços. [Preços](https://azure.microsoft.com/pricing/details/mysql/)
- Comece por criar o primeiro servidor. [Criar uma Base de Dados do Azure para o servidor MySQL com o portal do Azure](quickstart-create-mysql-server-database-using-azure-portal.md)
- Criar a sua primeira aplicação no Python, PHP, Ruby, C\#, Java, Node.js: [bibliotecas de conectividade utilizados tooconnect tooAzure da base de dados para MySQL](concepts-connection-libraries.md)
