---
title: "segurança aaaDatabase - base de dados do Azure Cosmos | Microsoft Docs"
description: "Saiba como base de dados do Azure Cosmos fornece segurança de dados e proteção de base de dados para os seus dados."
keywords: "nosql da base de dados segurança, segurança de informações, segurança de dados, a encriptação de base de dados, proteção de base de dados, as políticas de segurança, segurança de teste"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: a02a6a82-3baf-405c-9355-7a00aaa1a816
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: mimig
ms.openlocfilehash: 85ffa62f611bfad00bf3fc5dbe536f91f97f1113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-security"></a>Segurança de base de dados do Cosmos BD do Azure

Este artigo descreve os procedimentos de segurança da base de dados e as principais funcionalidades oferecidas pelo Azure Cosmos DB toohelp evitar, detetar e responder toodatabase falhas.
 
## <a name="whats-new-in-azure-cosmos-db-security"></a>Novidades na segurança de base de dados do Azure Cosmos?

Encriptação de Inativos está agora disponível para documentos e cópias de segurança armazenadas na base de dados do Azure Cosmos em todas as regiões do Azure. Encriptação de Inativos é aplicada automaticamente para clientes novos e existentes, estas regiões. Não há nenhum tooconfigure necessidade nada; e receber Olá a mesma latência excelente, débito, disponibilidade e a funcionalidade conforme antes com vantagem Olá de saber os seus dados estão seguros e segura com a encriptação de inativos.

## <a name="how-do-i-secure-my-database"></a>Como proteger a minha base de dados? 

Segurança de dados é uma responsabilidade partilhada entre si, o cliente de Olá e o fornecedor de bases de dados. Dependendo do fornecedor de bases de dados de Olá que escolher, pode variar a quantidade de Olá de responsabilidade executados. Se escolher uma solução no local, terá de tooprovide tudo de segurança de toophysical de proteção de ponto final do seu hardware - ou seja, não existem tarefas fácil. Se optar por um fornecedor de base de dados de nuvem PaaS, tais como a base de dados do Azure Cosmos, a área de preocupação diminui consideravelmente. Olá seguintes imagem, borrowed a partir da Microsoft [partilhado responsabilidades de informática em nuvem](https://aka.ms/sharedresponsibility) documento técnico, mostra como a sua responsabilidade diminui com um fornecedor de PaaS como base de dados do Azure Cosmos.

![Responsabilidades de fornecedor de cliente e a base de dados](./media/database-security/nosql-database-security-responsibilities.png)

Olá anterior componentes de segurança de nuvem de alto nível do diagrama mostra, mas que itens precisa tooworry sobre especificamente para a sua solução de base de dados? E como pode comparar soluções tooeach outros? 

Recomendamos Olá seguinte lista de verificação de requisitos em que sistemas de base de dados toocompare:

- Segurança de rede e as definições da firewall
- Autenticação de utilizador e controlos de utilizador detalhada
- Capacidade tooreplicate dados globalmente falhas regionais
- As ativações pós-falha tooperform de capacidade dos dados de um centro tooanother
- Replicação de dados local no Centro de dados
- Cópias de segurança automáticas dos dados
- Restauro de dados eliminadas de cópias de segurança
- Proteger e a isolar os dados confidenciais
- Monitorização de ataques
- Responder tooattacks
- Restrições de governação do capacidade toogeo fence dados tooadhere toodata
- Proteção física dos servidores nos centros de dados protegidos

E embora possa parecer óbvios, recentes [falhas da base de dados em grande escala](http://thehackernews.com/2017/01/mongodb-database-security.html) lembrar-na importância simples mas críticos Olá de Olá os seguintes requisitos:
- Corrigido servidores que são mantidos segurança toodate
- HTTPS através da encriptação SSL/predefinido
- Contas administrativas com palavras-passe fortes

## <a name="how-does-azure-cosmos-db-secure-my-database"></a>Como a base de dados do Azure Cosmos secure minha base de dados?

Vamos observar novamente Olá precedente lista - quantos esses requisitos de segurança de base de dados do Azure Cosmos fornece? Cada um único.

Vamos aprofundar para cada um em detalhe.

|Requisito de segurança|Abordagem de segurança da BD Cosmos do Azure|
|---|---|---|
|Segurança da rede|Utilizar uma firewall IP é Olá primeira camada de proteção toosecure a base de dados. BD do Cosmos do Azure suporta a política orientadas por controlos de acesso baseado em IP para o suporte de firewall de entrada. controlos de acesso baseado em IP Olá são semelhantes toohello as regras de firewall utilizadas pelos sistemas de base de dados tradicionais, mas estes são expandidos para que uma conta de base de dados de base de dados do Azure Cosmos só é acessível a partir de um conjunto de máquinas ou serviços em nuvem aprovado. <br><br>BD do Azure do Cosmos permite tooenable combinações de intervalos de IPs e, de um intervalo IP (168.61.48.0/8) e de um endereço IP específico (168.61.48.0). <br><br>Todos os pedidos provenientes de máquinas fora desta lista de permitidos são bloqueados por base de dados do Azure Cosmos. Máquinas de aprovação de pedidos de serviços em nuvem, em seguida, tem de ser concluida toobe de processo de autenticação de Olá fornecido recursos de toohello de controlo de acesso.<br><br>Saiba mais em [suporte de firewall de base de dados do Azure Cosmos](firewall-support.md).|
|Autorização|BD do Cosmos do Azure utiliza o código de autenticação de mensagens com base em hash (HMAC) para autorização. <br><br>Cada pedido é protegido por hash utilizando a chave de conta secreta Olá e Olá subsequentes base-64 codificado hash é enviado com cada tooAzure de chamada de base de dados do Cosmos. o pedido toovalidate Olá, utiliza de serviço de base de dados do Azure Cosmos Olá Olá chave secreta correta e propriedades toogenerate um hash, em seguida, este compara o valor de Olá com Olá um pedido de Olá. Se dois valores de Olá corresponderem, a operação de Olá está autorizada com êxito e processamento do pedido de Olá, caso contrário, não existe uma falha de autorização e Olá o pedido foi rejeitado.<br><br>Pode utilizar tanto um [chave mestra](secure-access-to-data.md#master-keys), ou um [token de recurso](secure-access-to-data.md#resource-tokens) que permite recursos de tooa acesso detalhado, tais como um documento.<br><br>Saiba mais em [proteger o acesso tooAzure Cosmos DB recursos](secure-access-to-data.md).|
|Utilizadores e permissões|Utilizar Olá [chave mestra](#master-key) para a conta de Olá, pode criar recursos de utilizador e de recursos de permissão por base de dados. A [token de recurso](#resource-token) está associado uma permissão numa base de dados e determina se o utilizador Olá tem acesso (leitura / escrita, só de leitura ou sem acesso) recursos de aplicação tooan na base de dados de Olá. Recursos de aplicação incluem coleções, documentos, os anexos, procedimentos armazenados, acionadores e UDFs. token de recurso Olá é utilizado durante a autenticação tooprovide ou negar o acesso toohello recursos.<br><br>Saiba mais em [proteger o acesso tooAzure Cosmos DB recursos](secure-access-to-data.md).|
|Integração do Active Directory (RBAC)| Também pode fornecer conta de base de dados de toohello de acesso com controlo de acesso (IAM) no Olá portal do Azure, conforme mostrado na captura de ecrã de Olá que se segue nesta tabela. IAM fornece controlo de acesso baseado em funções e integrado no Active Directory. Pode utilizar funções incorporadas ou funções personalizadas para indivíduos e grupos, conforme mostrado no Olá seguinte imagem.|
|Replicação global|BD do Azure do Cosmos oferece chave na mão distribuição global, que lhe permite tooreplicate tooany os dados de um botão de um dos centros de dados de todo o mundo do Azure com Olá clique. Replicação global permite-lhe dimensioná-las globalmente e fornecer acesso de latência baixa tooyour dados em torno Olá mundo.<br><br>No contexto de Olá de segurança, replicação global forma, assegura a proteção de dados contra falhas regionais.<br><br>Saiba mais em [distribuir dados globalmente](distribute-data-globally.md).|
|Ativações pós-falha regional|Se ter replicado dados no Centro de dados mais do que uma, base de dados do Azure Cosmos automaticamente faz o sobre as operações de deve um centro de dados regionais fique offline. Pode criar uma lista prioritária de regiões de ativação pós-falha utilizando regiões Olá na qual os dados são replicados. <br><br>Saiba mais em [as ativações pós-falha Regional do BD Azure Cosmos](regional-failover.md).|
|Replicação local|Mesmo dentro de um único centro de dados, base de dados do Azure Cosmos replica automaticamente dados de elevada disponibilidade dá ao hello escolha de [níveis de consistência](consistency-levels.md). Esta ação garante uma [99,99% de disponibilidade mensal SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db) e inclui uma garantia financeira - algo não pode fornecer nenhum outro serviço de base de dados.|
|Cópias de segurança online automatizadas|Bases de dados de base de dados do Cosmos do Azure são uma cópia de segurança regularmente e armazenados num arquivo georedundant. <br><br>Saiba mais em [automática cópia de segurança online e de restauro com base de dados do Azure Cosmos](online-backup-and-restore.md).|
|Restaurar eliminado os dados|Olá automatizadas cópias de segurança online podem estar utilizado toorecover dados que poderá ter acidentalmente eliminado segurança demasiado ~ 30 dias após evento de Olá. <br><br>Saiba mais em [automática cópia de segurança online e de restauro com base de dados do Azure Cosmos](online-backup-and-restore.md)|
|Proteger e a isolar os dados confidenciais|Todos os dados em regiões Olá listados no [Novidades?](#whats-new) agora são encriptados em pausa.<br><br>PII e outros dados confidenciais podem ser coleções toospecific isolado e leitura e escrita ou acesso só de leitura pode ser limitadas toospecific utilizadores.|
|Monitor de ataques|Ao utilizar um registo de auditoria e registos de atividade, pode monitorizar a sua conta para a atividade normal e anormal. Pode ver as operações que foram efetuadas nos seus recursos, o que iniciou a operação de Olá, quando a operação de Olá ocorreu, estado Olá da operação de Olá e muito mais como mostrado na captura de ecrã de Olá após esta tabela.|
|Responder tooattacks|Depois de contactar o suporte do Azure tooreport um ataque potencial, um processo de resposta a incidentes passo 5 é arrancou. Olá objetivo do processo de passo 5 Olá é toorestore serviço normal segurança e as operações mais rapidamente possível após é detetado um problema e é iniciada uma investigação.<br><br>Saiba mais em [Microsoft Azure Security Response no Olá nuvem](https://aka.ms/securityresponsepaper).|
|Barreiras geográficas|BD do Azure do Cosmos garante a governação de dados e conformidade para regiões sovereign (por exemplo, na Alemanha, China, nos US).|
|Instalações protegidas|Dados na base de dados do Azure Cosmos são armazenados em SSDs nos centros de dados protegidos do Azure.<br><br>Saiba mais em [os datacenters globais da Microsoft](https://www.microsoft.com/en-us/cloud-platform/global-datacenters)|
|Encriptação HTTPS/SSL/TLS|Todas as interações de base de dados do Azure Cosmos do serviço de cliente são SSL/TLS 1.2 imposta. Além disso, todos os intra datacenter e em vários centros de dados a replicação está SSL/TLS 1.2 imposta.|
|Encriptação inativa|Todos os dados armazenados na base de dados do Azure Cosmos são encriptados em pausa. Saiba mais em [encriptação de base de dados do Azure Cosmos Inativos](.\database-encryption-at-rest.md)|
|Corrigido servidores|Como uma base de dados gerido, base de dados do Azure Cosmos elimina Olá necessidade toomanage patch servidores e, que efetuou para si, automaticamente.|
|Contas administrativas com palavras-passe fortes|De disco rígido toobelieve iremos mesmo têm toomention este requisito mas, ao contrário de algumas das nossas concorrentes, é impossível toohave uma conta de administrador com nenhuma palavra-passe do BD Azure Cosmos.<br><br> Segurança através de SSL e HMAC autenticação baseada em segredo está integrada por predefinição.|
|Certificações de proteção de dados e segurança|Tem de BD do Azure do Cosmos [ISO 27001](https://www.microsoft.com/en-us/TrustCenter/Compliance/ISO-IEC-27001), [alfabetos modelo cláusulas (EUMC)](https://www.microsoft.com/en-us/TrustCenter/Compliance/EU-Model-Clauses), e [HIPAA](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA) certificações. Certificações adicionais estão em curso.|

Olá seguinte captura de ecrã mostra integração do Active Directory (RBAC) utilizando o controlo de acesso (IAM) no portal do Azure de Olá: ![o controlo de acesso (IAM) no Olá portal do Azure – demonstrar a segurança da base de dados](./media/database-security/nosql-database-security-identity-access-management-iam-rbac.png)

Olá seguinte captura de ecrã mostra como pode utilizar um registo de auditoria e atividade regista toomonitor sua conta: ![atividade nos registos do Azure Cosmos DB](./media/database-security/nosql-database-security-application-logging.png)

## <a name="next-steps"></a>Passos seguintes

Para obter mais detalhes sobre o mestre de chaves e os tokens de recursos, consulte [tooAzure de acesso de proteger dados da base de dados do Cosmos](secure-access-to-data.md).

Para obter mais detalhes sobre certificações da Microsoft, consulte [Centro de fidedignidade do Azure](https://azure.microsoft.com/support/trust-center/).
