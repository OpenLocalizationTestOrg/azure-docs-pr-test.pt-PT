---
title: aaaUnderstand arquitetura do Azure Active Directory | Microsoft Docs
description: "Explica o que é um inquilino do Azure AD e como toomanage do Azure através do Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
writer: v-lorisc
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/02/2017
ms.author: markvi
ms.openlocfilehash: 799943c012dcc309907ed3c36372038a0aad222a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-active-directory-architecture"></a>Compreender a arquitetura do Azure Active Directory
Azure Active Directory (Azure AD) permite que as toosecurely gerir acesso tooAzure serviços e recursos para os seus utilizadores. Incluído com o Azure AD está um conjunto completo de capacidades de gestão de identidades. Para obter informações sobre as funcionalidades do Azure AD, veja [What is Azure Active Directory?](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-whatis) (O que é o Azure Active Directory?)

Com o Azure AD, pode criar e gerir utilizadores e grupos e ativar tooallow de permissões e negar o acesso a recursos de tooenterprise. Para obter informações sobre a gestão de identidade, consulte [Olá Noções básicas sobre a gestão de identidades do Azure](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity).

## <a name="azure-ad-architecture"></a>Arquitetura do Azure AD
Arquitetura distribuída geograficamente do Azure AD combina monitorização exaustiva redirecionamento automatizada, a ativação pós-falha e funcionalidades de recuperação permitem-nos toodeliver nível empresarial disponibilidade e desempenho tooour que os clientes.

os seguintes elementos da arquitetura de Olá é abordada neste artigo:
 *  Design da arquitetura do serviço
 *  Escalabilidade 
 *  Disponibilidade contínua
 *  Datacenters

### <a name="service-architecture-design"></a>Design da arquitetura do serviço
Olá um sistema dimensionável, elevada disponibilidade, avançada em termos de dados é efetuada através de independentes blocos modulares ou unidades de escala de camada de dados do Azure AD de Olá mais comuns toobuild de forma, as unidades de escala são denominadas *partições*. 

camada de dados de Olá tem vários serviços de front-end que fornecem a capacidade de leitura e escrita. Diagrama de Olá abaixo mostra como Olá os componentes de uma partição de diretório única são distribuídos ao longo de centros de dados de distrubuted geograficamente. 

  ![Partições de Diretório Único](./media/active-directory-architecture/active-directory-architecture.png)

componentes de Olá da arquitetura do Azure AD incluem uma réplica primária e as réplicas secundárias.

**Réplica primária**

Olá *réplica primária* recebe todos *escreve* para a partição de Olá pertence. Qualquer escrever operação é imediatamente replicada tooa réplica secundária num centro de dados diferentes, antes de o devolver êxito toohello autor da chamada, que garante a durabilidade com redundância geográfica das escritas.

**Réplicas secundárias**

Todas as *leituras* do diretório são servidas a partir de *réplicas secundárias*, que estão em datacenters localizados fisicamente em diferentes geografias. Existem muitas réplicas secundárias, uma vez que os dados são replicados de forma assíncrona. Leituras de diretório, tais como pedidos de autenticação, são servidas de centros de dados que são clientes tooour fechar. réplicas secundárias Olá são responsáveis por leitura escalabilidade.

### <a name="scalability"></a>Escalabilidade

Escalabilidade é a capacidade de Olá de toomeet de tooexpand um serviço aumento dos requisitos de desempenho. Escreva a escalabilidade é conseguida através da criação de partições de dados de Olá. Escalabilidade de leitura é conseguida através da replicação de dados de uma partição toomultiple as réplicas secundárias distribuídas por toda Olá mundo.

Pedidos de aplicações de diretório são geralmente encaminhadas toohello Centro de dados que estão fisicamente mais próximo. Escreve são réplica primária de toohello redirecionado de forma transparente tooprovide consistência de leitura e escrita. Réplicas secundárias significativamente expandem a escala de Olá de partições porque Olá diretórios são, normalmente, lê a maioria do tempo de Olá.

Aplicações de diretório ligarem toohello mais próximo de centros de dados. Isto melhora o desempenho e, consequentemente, possibilita o aumento horizontal. Uma vez que uma partição de diretório pode ter várias réplicas secundárias, podem ser colocadas as réplicas secundárias mais próximo dos clientes de diretório toohello. Apenas diretório interno componentes do serviço que estão diretamente a réplica primária do destino de escrita intensivas Olá Active Directory.

### <a name="continuous-availability"></a>Disponibilidade contínua

Disponibilidade (ou disponibilidade) define a capacidade de Olá de tooperform um sistema interrompido. Olá chave tooAzure do AD de elevada disponibilidade é que o nossos serviços podem deslocar rapidamente tráfego entre múltiplos centros de dados distribuída geograficamente. Cada datacenter é independente, o que possibilita os modos de falha de descorrelação.

Estrutura de partição do Azure AD é simplificada toohello em comparação com enterprise design do AD, que é fundamental para o dimensionamento sistema Olá. Adotámos um design de mestre único que inclui um processo de ativação pós-falha de réplicas primárias determinístico e cuidadosamente orquestrado.

**Tolerância a falhas**

Um sistema é mais disponível se se tratar de tolerância a falhas toohardware, rede e software. Para cada partição no diretório de Olá, existe uma réplica principal elevada: réplica primária Olá. Apenas o escritas toohello partição são efetuadas nesta réplica. Esta réplica é continuamente e rigorosamente monitorizados e de escrita pode ser imediatamente desviado tooanother réplica (que fica Olá nova principal) se for detetada uma falha. Durante a ativação pós-falha, poderá haver uma perda de disponibilidade de escrita de cerca de 1 a 2 minutos, geralmente. A disponibilidade de leitura não é afetada durante este período.

As operações de leitura (que outnumber escritas por muitas as ordens de grandeza) apenas aceda toosecondary réplicas. Uma vez que as réplicas secundárias idempotent, perda de quaisquer uma réplica de uma determinada partição é facilmente compensada fornecendo indicações Olá leituras tooanother réplica, normalmente em Olá ao mesmo centro de dados.

**Durabilidade de dados**

Uma operação de escrita é tooat consolidada de forma durável, pelo menos, dois dados centros anterior tooit que está a ser confirmada. Isto ocorre pela primeira vez ao consolidar a escrita de Olá em Olá primário e, em seguida, imediatamente a replicar Olá escrita tooat, pelo menos, um outro centro de dados. Isto garante que uma potencial perda catastrófica de Olá dados center alojamento Olá primário não resultar na perda de dados.

Azure AD mantém um zero [objetivo de tempo de recuperação (RTO)](https://en.wikipedia.org/wiki/Recovery_time_objective) para emissão de tokens e de diretório lê e por ordem de Olá minutos (~ 5 minutos) RTO para o diretório escreve. Também mantemos um [Objetivo de Ponto de Recuperação (RPO)](https://en.wikipedia.org/wiki/Recovery_point_objective) de zero e não perdemos dados em ativações pós-falha.

### <a name="data-centers"></a>Datacenters

As réplicas do Azure AD são armazenadas nos centros de dados localizados ao longo de Olá mundo. Para obter mais informações, veja [Datacenters do Azure](https://azure.microsoft.com/en-us/overview/datacenters).

Azure AD funciona em todos os centros de dados com Olá seguintes características:

 * Autenticação, o gráfico e outros serviços do AD estiverem protegidos por Olá serviço de Gateway. Olá Gateway gere o balanceamento de carga destes serviços. Se forem detetados servidores em mau estado de funcionamento, através de sondas de estado de funcionamento transacionais, é feita a ativação pós-falha do mesmo automaticamente. Com base nestes sondas de estado de funcionamento, Olá Gateway dinamicamente encaminha o tráfego toohealthy os centros de dados.
 * Para *lê*, diretório Olá tem réplicas secundárias e serviços de front-end correspondentes uma configuração de ativo-ativo funcionar em vários centros de dados. Em caso de falha de um centro de dados completo, o tráfego será automaticamente encaminhadas tooa Centro de dados diferente.
 *  Para *escreve*, Olá diretório irá ativação pós-falha (principal) réplica primária em todos os centros de dados através de planeada (a nova principal é sincronizado tooold primário) ou os procedimentos de ativação pós-falha de emergência. Durabilidade de dados é conseguida através da replicação de centros de dados de tooat, pelo menos, dois qualquer confirmação.

**Consistência de dados**

modelo de diretório Olá é uma das consistência eventual. Um problema comum com sistemas distribuídos de forma assíncrona replicação é que os dados de Olá devolvidos por uma réplica "específica" não podem ser segurança toodate. 

O Azure AD fornece uma consistência de leitura e escrita para aplicações direcionada para uma réplica secundária por encaminhamento a réplica primária do escritas toohello e, em sincronia extrair Olá escreve novamente toohello de réplica secundária.

Aplicação escreve utilizando Olá Graph API do Azure AD são abstracted de manter a réplica de diretório de tooa de afinidade de consistência de leitura e escrita. Olá serviço Azure AD Graph mantém uma sessão lógica, que tem afinidade tooa réplica secundária utilizada para leituras; afinidade é capturada num "réplica token" que Olá gráfico caches de serviço através de uma cache distribuída. Este token é seguidamente utilizada para operações subsequentes no Olá mesma sessão lógico. 

 >[!NOTE]
 >Escritas imediatamente são replicadas foram emitidas leituras toohello réplica secundária toowhich Olá lógica da sessão.
 >

**Proteção de cópia de segurança**

diretório de Olá implementa elimina de forma recuperável, em vez de disco rígida elimina, para os utilizadores e os inquilinos para fácil recuperação em caso de eliminações acidentais, por um cliente. Se o administrador de inquilinos forma acidental elimina os utilizadores, pode facilmente anular e restaurar os utilizadores de Olá eliminado. 

O Azure AD implementa cópias de segurança diárias de todos os dados, pelo que consegue restaurar com autoridade dados, em caso de eliminações lógicas ou danos nos dados. A nossa camada de dados utiliza códigos de correção de erros, de modo a poder procurar erros e corrigir automaticamente determinados tipos de erros de disco.

**Métricas e monitores**

A execução de um serviço de elevada disponibilidade requer capacidades de métricas e monitorização de topo. O Azure AD analisa e comunica, de forma contínua, as métricas-chave de estado de funcionamento e os critérios de sucesso relativos a cada um dos seus serviços. Desenvolvemos e aperfeiçoamos continuamente as métricas, a monitorização e os alertas para cada cenário, em cada serviço do Azure AD e em todos os serviços.

Se qualquer serviço Azure AD não está a funcionar conforme esperado, iremos imediatamente demorar a funcionalidade de toorestore ação mais rapidamente possível. Olá controla mais importantes de métrica do Azure AD é rapidez é pode detetar e mitigar um cliente ou em direto problema do site. Iremos investir descontos elevados na monitorização e alertas toominimize tempo toodetect (destino TTD: < 5 minutos) e preparação operacional toominimize tempo toomitigate (destino TTM: < 30 minutos).

**Operações seguras**

Empregamos controlos operacionais, como a autenticação multifator (MFA), em qualquer operação, bem como auditoria de todas as operações. Além disso, utilizamos um elevação de just-in-time sistema toogrant necessário acesso temporário para qualquer operacional tarefas-a pedido numa base contínua. Para obter mais informações, consulte [Olá nuvem fidedigno](https://azure.microsoft.com/en-us/support/trust-center).

## <a name="next-steps"></a>Passos seguintes
[Guia para programadores do Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-developers-guide)

