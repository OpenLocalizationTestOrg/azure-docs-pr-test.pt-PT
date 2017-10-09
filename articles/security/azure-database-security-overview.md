---
title: "Descrição geral de segurança de base de dados aaaAzure | Microsoft Docs"
description: "Este artigo fornece uma descrição geral das funcionalidades de segurança de base de dados do Azure Olá."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: TomSh
ms.openlocfilehash: 13f14b99d15800e85e9906a9d167eb0adf2135de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-overview"></a>Descrição geral de segurança da base de dados do Azure

A segurança é uma preocupação superior quando gerir bases de dados e foi sempre uma prioridade para a SQL Database do Azure. Base de dados SQL do Azure suporta segurança de ligação com as regras de firewall e a encriptação da ligação. Suporta a autenticação com o nome de utilizador e palavra-passe e o Azure Active Directory Authentication, que utiliza identidades geridas pelo Azure Active Directory. Autorização utiliza o controlo de acesso baseado em funções.

Base de dados SQL do Azure suporta a encriptação efetuando em tempo real encriptação e desencriptação de bases de dados, cópias de segurança associadas e os ficheiros de registo de transações Inativos sem necessidade de alterações toohello aplicação.

A Microsoft fornece formas adicionais tooencrypt dados de empresa:

-   Nível de células colunas específicas do encriptação tooencrypt ou até mesmo células de dados com diferentes chaves de encriptação.
-   Se precisar de um módulo de Hardware de segurança ou gestão central da hierarquia de chave de encriptação, considere utilizar o Cofre de chaves do Azure com o SQL Server numa VM do Azure.
-   Sempre encriptado (atualmente em pré-visualização) torna tooapplications transparente de encriptação e permite aos clientes tooencrypt dados confidenciais dentro de aplicações de cliente sem partilhar chaves de encriptação de Olá com base de dados do SQL Server.

Auditoria de base de dados SQL do Azure permite que as empresas toorecord eventos tooan auditoria início de sessão do armazenamento do Azure. Auditoria de base de dados do SQL Server também integra-se com relatórios do Microsoft Power BI toofacilitate desagregar e estatísticas.

 Bases de dados SQL Azure podem ser totalmente protegida toosatisfy mais regulamentação ou requisitos de segurança, incluindo HIPAA, ISO 27001/27002 e PCI DSS nível 1, entre outros. Uma lista atual de certificações de conformidade de segurança está disponível em Olá [site Microsoft Azure Trust Center](http://azure.microsoft.com/support/trust-center/services/).

Este artigo explica Olá Noções básicas do proteger bases de dados do Microsoft Azure SQL Server para Structured, tabela e dados relacionais. Em particular, este artigo irá ajudá-lo a começar a utilizar recursos para proteger dados, controlar o acesso e a monitorização proativa.

Este artigo de descrição geral de segurança do Azure da base de dados centra-se nos Olá seguintes áreas:

-   Proteger os dados
-   Controlo de acesso
-   Monitorização proativa
-   Gestão de segurança centralizada
-   Mercado do Azure

## <a name="protect-data"></a>Proteger os dados

Base de dados SQL protege os seus dados ao fornecer a encriptação dos dados em movimento utilizando [Transport Layer Security](https://support.microsoft.com/kb/3135244), para dadosem rest utilizando [encriptação transparente de dados](http://go.microsoft.com/fwlink/?LinkId=526242)e para os dados em utilização utilizando [ Sempre encriptado](https://msdn.microsoft.com/library/mt163865.aspx).

Nesta secção, iremos falar sobre:

-   Encriptação em movimento
-   Encriptação inativa
-   Encriptação em utilização (cliente)

Para outra formas tooencrypt os dados, considere:

-   [Encriptação de nível de células](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt colunas específicas ou até mesmo células de dados com diferentes chaves de encriptação.
-   Se precisar de um Módulo de Segurança de Hardware ou de fazer a gestão centralizada da hierarquia de chaves de encriptação, considere utilizar o [Azure Key Vault com o SQL Server numa VM do Azure](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx).

### <a name="encryption-in-motion"></a>Encriptação em movimento

Um problema comum para todas as aplicações de cliente/servidor é a necessidade de Olá de privacidade como dados movem-se em redes públicas e privadas. Se mover através de uma rede de dados não for encriptados, não há hipótese de Olá que podem ser capturada e roubada por utilizadores não autorizados. Ao lidar com os serviços de base de dados, terá de toomake certificar-se de que os dados são encriptados entre o cliente de base de dados de Olá e o servidor, bem como entre servidores de base de dados que comunicam entre si e com aplicações de camada média.

Um problema ao administrar uma rede é proteger os dados que estão a ser enviados entre aplicações através de uma rede não fidedigna. Pode utilizar [TLS/SSL](https://docs.microsoft.com/windows-server/security/tls/transport-layer-security-protocol) tooauthenticate servidores e clientes e, em seguida, utilizá-la tooencrypt mensagens entre as partes de Olá autenticado.

No processo de autenticação de Olá, um cliente TLS/SSL envia um servidor TLS/SSL tooa mensagem e Olá responde com as informações de Olá nesse servidor Olá tem tooauthenticate próprio. Olá cliente e o servidor efetuam uma troca adicional de chaves de sessão e Olá extremidades da caixa de diálogo de autenticação. Quando autenticação for concluída, a comunicação protegida por SSL pode começar entre o servidor de Olá e cliente Olá utilizando chaves de encriptação simétrica Olá que são estabelecidas durante o processo de autenticação de Olá.

Todas as ligações tooAzure base de dados do SQL Server exigir encriptação (SSL/TLS) em todas as horas dados enquanto estes se tooand "em trânsito" da base de dados de Olá. SQL Azure utiliza o TLS/SSL tooauthenticate servidores e clientes e, em seguida, utilizá-lo tooencrypt mensagens entre as partes de Olá autenticado. Na cadeia de ligação da sua aplicação, tem de especificar a ligação de Olá tooencrypt de parâmetros e não tootrust Olá certificado de servidor (isto é feito automaticamente se copiar a cadeia de ligação fora Olá Portal clássico do Azure), caso contrário Olá ligação será Não verificar a identidade de hello do servidor de Olá e será suscetíveis demasiado "man-in-the-middle" ataques. Para hello ADO.NET controlador, por exemplo, estes parâmetros de cadeia de ligação são encriptar = True e TrustServerCertificate = False.

### <a name="encryption-at-rest"></a>Encriptação inativa
Pode demorar várias precauções toohelp Olá seguro da base de dados, tais como conceber um sistema seguro, encriptação ativos confidenciais e criação de uma firewall em torno de servidores de base de dados de Olá. No entanto, num cenário em que o suporte de dados físico Olá (por exemplo, discos ou bandas de cópia de segurança) é roubados, uma parte maliciosa pode apenas restaurar ou expor Olá base de dados e procurar dados Olá.

Uma solução tooencrypt Olá dados sensíveis na base de dados de Olá e protege as chaves de Olá que são utilizados tooencrypt Olá dados com um certificado. Isto impede que qualquer pessoa sem chaves Olá utilizando dados Olá, mas este tipo de proteção têm de ser planeado.

toosolve este problema, SQL Server e SQL do Azure suporta [encriptação de dados transparente (TDE)](https://docs.microsoft.com/sql/relational-databases/securityrecryption/transparent-data-encryption-tde). TDE encripta os ficheiros de dados do SQL Server e SQL Database do Azure, conhecidos como dados de encriptação de inativos.

Encriptação de dados transparente de base de dados SQL do Azure ajuda a proteger contra ameaças de Olá de atividade maliciosa através de encriptação em tempo real e a desencriptação da base de dados de Olá, cópias de segurança associadas e os ficheiros de registo de transações Inativos sem necessidade de alterações aplicação de toohello.  

TDE encripta armazenamento Olá de uma base de dados completo com uma chave de encriptação da base de dados de Olá chamado de chave simétrica. Na base de dados do SQL Server, a chave de encriptação de base de dados de Olá está protegido por um certificado de servidor incorporada. certificado de servidor incorporada Olá é exclusivo para cada servidor de base de dados SQL.

Se tiver uma base de dados numa relação GeoDR, está protegido por uma chave diferente em cada servidor. Se duas bases de dados estiverem ligado toohello mesmo servidor, estes partilham Olá mesmo certificado incorporado. Microsoft roda automaticamente estes certificados, pelo menos, todos os 90 dias. Para obter uma descrição geral de TDE, consulte [encriptação de dados transparente (TDE)](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde).

### <a name="encryption-in-use-client"></a>Encriptação em utilização (cliente)

A maioria das falhas de dados envolvem o roubo de Olá de dados críticos, como números de cartão de crédito ou informações pessoais identificáveis. Bases de dados podem ser treasure troves de informações confidenciais. Podem conter dados pessoais dos clientes, informações competitivos confidenciais e propriedade intelectual. Dados perdidos ou roubados, especialmente os dados de cliente, podem resultar em danos marca, desvantagem competitiva e graves fines — mesmo lawsuits.

![Sempre Encriptado](./media/azure-databse-security-overview/azure-database-fig1.png)

[Sempre encriptado](https://msdn.microsoft.com/library/mt163865.aspx) é um funcionalidade concebido tooprotect dados confidenciais, tais como números de cartão de crédito ou números de identificação national (por exemplo, E.U.A. números de segurança social), armazenado nas bases de dados SQL Database do Azure ou SQL Server. Sempre encriptado permite aos clientes tooencrypt dados confidenciais dentro de aplicações de cliente e nunca revelar toohello de chaves de encriptação de Olá motor de base de dados (base de dados SQL ou SQL Server).

Sempre encriptado fornece uma separação entre os utilizadores que possuem dados Olá (e pode vê-la) e os utilizadores que gerem dados Olá (mas deve ter sem acesso). Operadores de base de dados da nuvem, assegurando que os administradores de base de dados no local, ou outros privilégios elevados, mas os utilizadores não autorizados, não é possível aceder a dados Olá encriptado,

Além disso, sempre encriptados torna tooapplications transparente de encriptação. Um ativada sempre encriptado um controlador instalado no computador de cliente Olá, para que possam automaticamente encriptar e desencriptar dados sensíveis na aplicação de cliente Olá. controlador Olá encripta os dados de Olá nas colunas confidenciais antes de passar Olá dados toohello motor de base de dados e automaticamente reescreve consultas para que a aplicação de toohello Olá semântica são preservadas. Da mesma forma, controladores de Olá transparente desencripta os dados, armazenados em colunas de base de dados encriptados contidas nos resultados de consulta.

## <a name="access-control"></a>Controlo de acesso
segurança tooprovide, base de dados SQL controla o acesso com regras de firewall limitar conectividade por endereço IP, a mecanismos de autenticação que requerem tooprove utilizadores as respetivas identidades e mecanismos de autorização limitar ações de toospecific de utilizadores e os dados.

### <a name="database-access"></a>Acesso de base de dados

Proteção de dados começa com controlar tooyour aceder a dados. Olá Centro de dados que aloja os seus dados gere o acesso físico, embora possa configurar uma segurança de toomanage firewall na camada de rede Olá. Também pode controla o acesso ao configurar os inícios de sessão para autenticação e definir permissões para funções de servidor e base de dados.

Nesta secção, iremos falar sobre:

-   Firewall e regras de firewall
-   Autenticação
-   Autorização

#### <a name="firewall-and-firewall-rules"></a>Firewall e regras de firewall

A Base de Dados SQL do Microsoft Azure disponibiliza um serviço de bases de dados relacionais para o Azure e outras aplicações baseadas na Internet. toohelp proteger os seus dados, as firewalls para impedir que todos os acesso tooyour da base de dados servidor até especificar quais os computadores que tem permissão. firewall de Olá concede toodatabases de acesso com base no Olá provenientes de endereços IP de cada pedido. Para obter mais informações, veja [Descrição geral das regras de firewall da Base de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

Olá [SQL Database do Azure](https://azure.microsoft.com/services/sql-database/) serviço só está disponível através da porta TCP 1433. tooaccess uma base de dados do SQL Server do seu computador, certifique-se de que a firewall de computador cliente permite a comunicação de TCP de saída na porta TCP 1433. Se não for necessário para outras aplicações, bloqueie as ligações de entrada na porta TCP 1433.

#### <a name="authentication"></a>Autenticação

Autenticação do SQL Server da base de dados refere-se toohow provar a sua identidade ao ligar toohello base de dados. A Base de Dados SQL suporta dois tipos de autenticação:

-   **Autenticação do SQL Server:** é criada uma conta de início de sessão único quando é criada uma instância do SQL Server lógica, denominado Olá conta de subscritor do SQL Server da base de dados. Esta conta liga-se utilizando [autenticação do SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview) (nome de utilizador e palavra-passe). Esta conta é que um administrador na instância do servidor lógico de Olá e em todas as bases de dados do utilizador ligado toothat instância. permissões de Olá de Olá conta subscritor não podem ser limitadas. Só pode existir uma destas contas.
-   **Autenticação do Active Directory do Azure:** [autenticação do Azure Active Directory](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication) é um mecanismo de ligar tooMicrosoft SQL Database do Azure e o SQL Data Warehouse, utilizando as identidades no Azure Active Directory ( Azure AD). Este permite toocentrally gerir identidades de utilizadores de base de dados.

![Autenticação](./media/azure-databse-security-overview/azure-database-fig2.png)

 Vantagens da autenticação do Azure Active Directory incluem:
  - Fornece uma autenticação de servidor tooSQL alternativo.
  - Também ajuda a parar a proliferação de Olá das identidades de utilizador em servidores de base de dados & permite rotação de palavra-passe num único local.
  - Pode gerir as permissões de base de dados através de grupos do externos (Azure Active Directory).
  - -Pode eliminar armazenar palavras-passe através da autenticação integrada do Windows e outras formas de autenticação suportados pelo Azure Active Directory.

#### <a name="authorization"></a>Autorização
[Autorização](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins) toowhat de refere-se um utilizador pode fazê-lo dentro de uma base de dados do SQL do Azure e este é controlado pela base de dados da sua conta de utilizador [associações de função](https://msdn.microsoft.com/library/ms189121) e [ao nível do objeto permissões](https://msdn.microsoft.com/library/ms191291.aspx). Autorização é o processo de Olá de determinar quais os recursos com capacidade de segurança pode aceder a um principal e as operações são permitidas para esses recursos.

### <a name="application-access"></a>Acesso à aplicação

Nesta secção, iremos falar sobre:

-   Máscara de dados dinâmica
-   Segurança ao Nível da Linha

#### <a name="dynamic-data-masking"></a>Máscara de dados dinâmica
Um representante de serviço no Centro de atendimento telefónico pode identificar os chamadores por vários dígitos do seu número de segurança social ou um número de cartão de crédito, mas esses dados itens não devem estar totalmente expostos toohello representante de serviço.

Pode ser definida uma regra de máscara que, mas Olá de máscaras de todos os últimos quatro dígitos de qualquer número de segurança social ou o número de cartão de crédito no conjunto de resultados de Olá qualquer consulta.

![Máscara de dados dinâmica](./media/azure-databse-security-overview/azure-database-fig3.png)

Outro exemplo, uma máscara de dados adequada pode ser definidos tooprotect dados de informação identificativa (PII), para que um programador pode consultar os ambientes de produção para fins de resolução de problemas sem violar as normas de conformidade.

[SQL Server da base de dados máscara de dados dinâmicos](https://docs.microsoft.com/azure/sql-database/sql-database-dynamic-data-masking-get-started) limita a exposição de dados confidenciais através da máscara os utilizadores de privilégio toonon. A máscara de dados dinâmica é suportada para a versão V12 de Olá da SQL Database do Azure.

[Máscara de dados dinâmicos](https://docs.microsoft.com/sql/relational-databases/security/dynamic-data-masking) ajuda a impedir que os dados de toosensitive de acesso não autorizado, permitindo toodesignate quantidade de dados confidenciais de Olá tooreveal com um impacto mínimo na camada de aplicação Olá. É uma funcionalidade de segurança baseadas em políticas oculta dados confidenciais do Olá no conjunto de resultados de Olá de uma consulta através de campos de base de dados designada, enquanto os dados de Olá na base de dados de Olá não são alterados.


> [!Note]
> Máscara de dados dinâmicos pode ser configurada por base de dados do Azure Olá, admin, administrador do servidor ou funções de responsável pela segurança.

#### <a name="row-level-security"></a>Segurança ao nível da linha
É outro requisito de segurança comuns para bases de dados multi-inquilino [segurança ao nível da linha](https://msdn.microsoft.com/library/dn765131.aspx). Esta funcionalidade permite-lhe toocontrol acesso toorows numa tabela da base de dados com base em caraterísticas Olá do utilizador Olá executar uma consulta (por exemplo, grupo ou execução da associação contexto).

![Segurança de nível de linha](./media/azure-databse-security-overview/azure-database-fig4.png)

lógica de restrição de acesso de Olá é localizado na camada de base de dados de Olá em vez de away de dados de Olá na outra camada de aplicação. sistema de base de dados de Olá aplica restrições de acesso de Olá sempre que esse acesso de dados é tentado a partir de qualquer camada. Isto torna o seu sistema de segurança mais fiável e robusta, reduzindo a área de superfície Olá do seu sistema de segurança.

Segurança ao nível da linha apresenta o controlo de acesso baseado em predicado. Funcionalidades de uma avaliação flexível, centralizada, baseados no predicado que pode ter em consideração metadados ou quaisquer outros critérios Olá administrador determina conforme adequada. o predicado de Olá é utilizado como um critério toodetermine se ou não tem de utilizador Olá adequado aceder a dados de toohello Olá, com base nos atributos de utilizador. Controlo de acesso baseado em etiqueta pode ser implementado utilizando o controlo de acesso baseado em predicado.

## <a name="proactive-monitoring"></a>Monitorização proativa
Base de dados SQL protege os seus dados, fornecendo **auditoria** e **deteção de ameaças** capacidades.

### <a name="auditing"></a>Auditoria
Auditoria de base de dados SQL aumenta a capacidade toogain aprofundadas sobre eventos e as alterações que ocorrem dentro do Olá da base de dados, incluindo atualizações e consultas em relação a dados Olá.

[Auditoria de base de dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-auditing-get-started) controla os eventos de base de dados e escreve-los tooan do registo de auditoria na sua conta do Storage do Azure. A auditoria pode ajudá-lo a manter a conformidade regulatória, a compreender as atividades da base de dados e a obter informações relativas a discrepâncias e anomalias que possam traduzir preocupações comerciais ou suspeitas de violações de segurança. Auditoria permite e facilita as normas de toocompliance aderência mas não garante a compatibilidade.

Auditoria de base de dados SQL permite-lhe:

-   **Manter** um registo de auditoria de eventos selecionados. Pode definir categorias de base de dados ações toobe auditada.
-   **Relatório** na atividade de base de dados. Pode utilizar relatórios pré-configurados e tooget um dashboard a trabalhar rapidamente com atividade e o relatório de eventos.
-   **Analisar** relatórios. Pode encontrar eventos suspeitos, atividade invulgar e tendências.

Existem dois métodos de auditoria:

-   **Auditoria de blob** -os registos são escritos tooAzure Blob Storage. Este é um método de auditoria mais recente, que fornece um desempenho superior, suporta a auditoria de maior granularidade ao nível do objeto e é mais económico.
-   **Auditoria de tabela** -os registos são escritos tooAzure Table Storage.

### <a name="threat-detection"></a>Deteção de ameaças
[A deteção de ameaças de base de dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection) Deteta atividades suspeitas que indicam potenciais ameaças de segurança. A deteção de ameaças permite-lhe toorespond toosuspicious eventos na base de dados de Olá, tais como SQL Injections, à medida que ocorrem. Disponibiliza alertas e permite a utilização de Olá da auditoria de base de dados SQL do Azure tooexplore eventos suspeita Olá.

![Deteção de ameaças](./media/azure-databse-security-overview/azure-database-fig5.jpg)

Por exemplo, a injeção de SQL é uma das Olá Web aplicação segurança problemas comuns no Olá Internet, as aplicações utilizadas tooattack condicionada por dados. Os atacantes tirar partido da aplicação vulnerabilidades tooinject maliciosas instruções SQL para campos de entrada de aplicação, ser, ou modificar dados na base de dados de Olá.

Officers de segurança ou outros administradores designados podem obter uma notificação imediata sobre atividades suspeitas da base de dados à medida que ocorrem. Cada notificação fornece detalhes de atividade suspeita Olá e recomenda como toofurther investigar e mitigar a ameaça de Olá.        

## <a name="centralized-security-management"></a>Gestão de segurança centralizada

[Centro de segurança do Azure](https://azure.microsoft.com/documentation/services/security-center/) ajuda-o a evitar, detetar e responder toothreats. Fornece gestão de políticas e monitorização de segurança integrada nas suas subscrições do Azure, ajuda a detetar ameaças que caso contrário podem passar despercebidas e funciona com um ecossistema abrangente de soluções de segurança.

[Centro de segurança](https://docs.microsoft.com/azure/security-center/security-center-sql-database) ajuda a salvaguardar dados na base de dados do SQL Server, fornecendo visibilidade segurança Olá de todos os servidores e bases de dados. Centro de segurança, pode:

-   Defina políticas para auditoria e de encriptação de base de dados SQL.
-   Monitorizar a segurança de Olá dos recursos de base de dados SQL em todas as subscrições.
-   Rapidamente identificar e resolver problemas de segurança.
-   Integrar alertas a partir do [deteção de ameaças da SQL Database do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).
-   Centro de segurança suporta o acesso baseado em funções.

## <a name="azure-marketplace"></a>Azure Marketplace

Olá, Azure Marketplace é um marketplace de aplicações e serviços online que permite start-ups e independentes de software (ISV) toooffer respetivos clientes de tooAzure soluções à volta de Olá mundo.
combina a Azure Marketplace Olá ecossistemas de parceiros do Microsoft Azure para uma plataforma única e unificada toobetter serve os nossos clientes e parceiros. Clique em [aqui](https://azuremarketplace.microsoft.com/marketplace/apps?search=Database%20Security&page=1) produtos de segurança de base de dados de tooglance disponíveis no Azure Marketplace.

## <a name="next-steps"></a>Passos seguintes

- Saiba mais sobre [proteger a base de dados do SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial).
- Saiba mais sobre [serviço Centro de segurança do Azure e SQL Database do Azure](https://docs.microsoft.com/azure/security-center/security-center-sql-database).
- toolearn mais informações sobre a deteção de ameaças, consulte [deteção de ameaças de base de dados do SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).
- toolearn mais, consulte [desempenho de base de dados do SQL Server melhorar](https://docs.microsoft.com/azure/sql-database/sql-database-performance-tutorial). 
