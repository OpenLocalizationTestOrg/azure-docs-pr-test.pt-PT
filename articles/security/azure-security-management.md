---
title: "segurança da gestão remota aaaEnhance no Azure | Microsoft Docs"
description: "Este artigo aborda os passos para melhorar a segurança da gestão remota ao administrar ambientes do Microsoft Azure, incluindo serviços cloud, Máquinas Virtuais e aplicações personalizadas."
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 2431feba-3364-4a63-8e66-858926061dd3
ms.service: security
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 9262cfb98bfe51d15fbad8f18997c4573668d9ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="security-management-in-azure"></a>Gestão de segurança no Azure
Os subscritores do Azure poderão gerir os respetivos ambientes de nuvem a partir de vários dispositivos, incluindo estações de trabalho de gestão, PCs de programadores e, até mesmo, dispositivos de utilizador final com privilégios que tenham permissões específicas de tarefas. Em alguns casos, as funções administrativas são efetuadas através das consolas baseadas na web, tais como Olá [portal do Azure](https://azure.microsoft.com/features/azure-portal/). Noutros casos, poderão existir ligações diretas tooAzure de sistemas no local através de redes privadas virtuais (VPNs), os serviços de Terminal, protocolos de aplicação de cliente ou (através de programação) Olá API de gestão de serviço do Azure (SMAPI). Além disso, os pontos finais de cliente podem ser um domínio associado ou isolado e não gerido, como tablets ou smartphones.

Embora várias capacidades de gestão de acesso e fornecem um conjunto avançado de opções, esta variabilidade pode acarretar a implementação de nuvem tooa risco significativo. Pode ser difícil toomanage, controlar e auditar as ações administrativas. Este variabilidade também poderá acarretar ameaças de segurança através do acesso não regulado tooclient os pontos finais que são utilizados para gerir os cloud services. A utilização das estações de trabalho gerais ou pessoais para desenvolver e gerir a infraestrutura abre vetores de ameaças imprevisíveis, como navegação na Web (por exemplo, ataques de tipo “watering hole”) ou e-mail (engenharia social e phishing).

![][1]

Olá potencial ataques aumenta neste tipo de ambiente, porque é difícil tooconstruct as políticas de segurança e mecanismos tooappropriately gerir acesso tooAzure interfaces (por exemplo, SMAPI) a partir de pontos finais bastante diversos.

### <a name="remote-management-threats"></a>Ameaças da gestão remota
Os atacantes tentam frequentemente acesso toogain privilegiado comprometendo as credenciais da conta (por exemplo, através de forçar força a palavra-passe, phishing e recolha de credenciais) ou ludibriando os utilizadores na execução de código prejudicial (por exemplo, a partir de sites prejudiciais por unidade transfere ou anexos de e-mail prejudiciais). Num ambiente de nuvem gerido remotamente, conta de falhas podem levar tooan maior risco devido tooanywhere, acesso em qualquer altura.

Mesmo com controlos apertados em contas de administrador principais, contas de utilizador de nível inferior podem ser utilizados tooexploit fragilidades na estratégia de segurança de um. Falta de formação apropriada em segurança também pode levar toobreaches através de divulgação ou exposição das informações de conta acidental.

Quando uma estação de trabalho do utilizador também é utilizada para tarefas administrativas, pode ficar comprometida em muitos pontos diferentes. Se um utilizador é navegação na web Olá, utilizando as ferramentas de terceiros 3rd e open source ou abrir um ficheiro de documento prejudicial que contém um trojan.

Em geral, ataques direcionados mais resultar em falhas de dados pode ser rastreada toobrowser exploits, plug-ins (por exemplo, Flash, PDF, Java) e spear phishing (e-mail) em computadores. Nestes computadores poderão ter de nível administrativo ou permissões de nível de serviço tooaccess em direto servidores ou dispositivos de rede de operações, quando utilizados para programação ou para a gestão de outros recursos.

### <a name="operational-security-fundamentals"></a>Noções básicas da segurança operacional
Para mais segura e operações de gestão, pode minimizar a superfície de ataque de um cliente ao reduzir o número de Olá de pontos de entrada possíveis. Isto pode ser feito através dos princípios de segurança: “separação de funções” e “segregação dos ambientes”.

Isole as funções sensíveis no outro toodecrease Olá probabilidade que um erro num nível servem como tooa violação noutro. Exemplos:

* As tarefas administrativas não devem ser combinadas com atividades que podem originar tooa comprometimento (por exemplo, software maligno no e-mail de um administrador que, em seguida, infeta diretamente um servidor de infraestrutura).
* Uma estação de trabalho utilizada para operações de elevada sensibilidade não deve ser Olá mesmo sistema utilizado para finalidades de alto risco como navegação Olá Internet.

Reduza a superfície de ataque do sistema de Olá removendo software desnecessário. Exemplo:

* Administrativa padrão de suporte ou estação de trabalho de desenvolvimento não deve requerer a instalação de cliente de e-mail ou outras aplicações de produtividade se o principal objetivo do dispositivo Olá é toomanage serviços de nuvem.

Sistemas de cliente que tenham tooinfrastructure de acesso de administrador componentes devem ser sujeitos riscos de segurança de tooreduce toohello mais estrita possível política. Exemplos:

* As políticas de segurança podem incluir definições de política de grupo negarem o acesso aberto à Internet a partir da Olá dispositivo e utilizar uma configuração de firewall restritiva.
* Utilize VPNs com segurança IPsec seo acesso direto for necessário.
* Configure domínios do Active Directory de gestão e de desenvolvimento separados.
* Isole e filtre o tráfego de rede da estação de trabalho de gestão.
* Utilize software antimalware.
* Implementar o risco de Olá tooreduce autenticação multifator de credenciais roubadas.

Consolidar os recursos de acesso e eliminar os pontos finais não geridos também simplifica as tarefas de gestão.

### <a name="providing-security-for-azure-remote-management"></a>Fornecer segurança para gestão remota do Azure
O Azure oferece segurança administradores de tooaid mecanismos que gerem serviços em nuvem do Azure e máquinas virtuais. Estes mecanismos incluem:

* Autenticação e [controlo de acesso baseado em funções](../active-directory/role-based-access-control-configure.md).
* Monitorização, registo e auditoria.
* Certificados e comunicações encriptadas.
* Um portal de gestão Web.
* Filtragem de pacotes de rede.

Com a configuração de segurança do lado do cliente e implementação de centro de dados de um gateway de gestão, é possíveis toorestrict e monitor administrador acesso toocloud aplicações e dados.

> [!NOTE]
> Algumas recomendações neste artigo poderão resultar numa maior utilização de dados, de rede ou de utilização de recursos de computação e poderão aumentar os custos de licenciamento ou de subscrição.
>
>

## <a name="hardened-workstation-for-management"></a>Estação de trabalho protegida para gestão
objetivo de Olá da proteção de uma estação de trabalho é tooeliminate todos os mas funções mais críticas Olá necessárias para que toooperate, tornando a superfície de ataque potencial Olá tão reduzida quanto possível. A proteção do sistema inclui minimizar Olá diversas aplicações, limitar a execução das aplicações, restringir tooonly de acesso de rede que é necessário, e serviços instalados e sempre manter o sistema de Olá segurança toodate. Além disso, utilizar uma estação de trabalho para gestão protegida segrega as ferramentas e as atividades administrativas de outras tarefas do utilizador final.

Num ambiente empresarial no local, pode limitar a superfície de ataque de Olá da sua infraestrutura física através de redes de gestão dedicadas, salas de servidores com acesso por cartão e estações de trabalho executam em áreas protegidas da rede Olá. Num modelo de TI híbrido ou na nuvem, ser diligente relativamente dos serviços de gestão seguro aos pode ser mais complexo devido à falta de Olá dos recursos de tooIT acesso físico. Implementar soluções de proteção requer uma cuidada configuração do software, processos centrados na segurança e políticas abrangentes.

Utilizando um requisitos de espaço do software minimizado menor privilégio numa estação de trabalho pendentes bloqueado para gestão de nuvem — e para o desenvolvimento de aplicações — pode reduzir o risco de Olá de incidentes de segurança ao uniformizar os ambientes de desenvolvimento e gestão remotas no Olá. Uma configuração de estação de trabalho protegida pode ajudar a evitar o comprometimento de Olá de contas que são utilizados toomanage recursos de nuvem críticos fechando muitas vias comuns utilizadas pelo software maligno e exploits. Especificamente, pode utilizar [Windows AppLocker](http://technet.microsoft.com/library/dd759117.aspx) e toocontrol de tecnologia de Hyper-V e isolar o comportamento do sistema de cliente e mitigar as ameaças, incluindo e-mail ou navegação na Internet.

Na estação de trabalho protegida, o administrador de Olá executa uma conta de utilizador padrão (o que bloqueia a execução de nível administrativo) e aplicações associadas são controladas por uma lista de permissões. elementos básicos de Olá de estação de trabalho protegida são os seguintes:

* Análise ativa e aplicação de patches. Implemente o antimalware software, executar análises de vulnerabilidade regulares e atualizar todas as estações de trabalho através de atualização de segurança mais recente Olá atempadamente.
* Funcionalidade limitada. Desinstale todas as aplicações que não são necessárias e desative os serviços desnecessários (arranque).
* Proteção da rede. Utilize endereços IP Firewall do Windows regras tooallow só é válidos, portas e URLs tooAzure relacionados gestão. Certifique-se de que essa estação de trabalho de toohello ligações remotas de entrada também estão bloqueadas.
* Restrição de execução. Permitir apenas um conjunto de ficheiros executáveis predefinidos que são necessários para toorun de gestão (referidos tooas "predefinição-negar"). Por predefinição, os utilizadores devem ter permissão toorun qualquer programa, a menos que estes esteja explicitamente definido em Olá a lista de permissões.
* Menor privilégio. Utilizadores da estação de trabalho de gestão não devem ter privilégios administrativos no computador local de Olá próprio. Desta forma, não podem alterar a configuração do sistema de Olá ou ficheiros de sistema Olá, intencionalmente ou acidentalmente.

Pode impor tudo isto utilizando [objetos de política de grupo](https://www.microsoft.com/download/details.aspx?id=2612) (GPOs) nos serviços de domínio do Active Directory (AD DS) e aplicá-las através das contas de gestão de tooall de domínio de gestão (local).

### <a name="managing-services-applications-and-data"></a>Gerir serviços, aplicações e dados
Configuração de serviços em nuvem do Azure é efetuada através de Olá portal do Azure ou do SMAPI, através de interface de linha de comandos do Windows PowerShell Olá ou uma aplicação personalizada que tira partido destas interfaces RESTful. Os serviços com estes mecanismos incluem o Azure Active Directory (Azure AD), o Storage do Azure, os Web Sites do Azure, a Azure Virtual Network, entre outros.

Máquina virtual: as aplicações implementadas fornecem as suas próprias ferramentas de cliente e interfaces conforme necessário, como Olá consola de gestão da Microsoft (MMC), uma consola de gestão empresarial (tal como o Microsoft System Center ou o Windows Intune) ou outra gestão aplicações-Microsoft SQL Server Management Studio, por exemplo. Estas ferramentas normalmente residem num ambiente empresarial ou numa rede do cliente e podem depender de protocolos de rede específicos, como o protocolo RDP (Remote Desktop Protocol), que necessitam de ligações diretas com monitorização de estado. Algumas poderão ter interfaces web-ativado que não devem ser acessíveis através de Olá Internet ou publicadas abertamente.

Pode restringir a gestão de serviços de plataforma e tooinfrastructure acesso no Azure utilizando [autenticação multifator](../multi-factor-authentication/multi-factor-authentication.md), [certificados de gestão de x. 509](https://blogs.msdn.microsoft.com/azuresecurity/2015/07/13/certificate-management-in-azure-dos-and-donts/)e as regras de firewall. Olá portal do Azure e o SMAPI requerem Transport Layer Security (TLS). No entanto, serviços e aplicações que implementa no Azure requerem tootake as medidas de proteção adequadas com base na sua aplicação. Estes mecanismos podem ser ativados frequentemente de modo mais fácil através de uma configuração da estação de trabalho protegida normalizada.

### <a name="management-gateway"></a>Gateway de gestão
toocentralize todo administrativa aceder e simplificar a monitorização e o registo, pode implementar um dedicado [Gateway de ambiente de trabalho remoto](https://technet.microsoft.com/library/dd560672) server (Gateway de RD) no seu local de rede, ligado tooyour ambiente do Azure.

Um Gateway de ambiente de trabalho remoto é um serviço proxy baseado na política RDP que impõe requisitos de segurança. Implementar o Gateway de RD juntamente com o Windows Server Network Access Protection (NAP) ajuda a garantir que apenas os clientes que cumprem os critérios de estado de funcionamento de segurança específicos estabelecidos pelo Objetos de Política de Grupo (GPOs) dos Serviços de Domínio do Active Directory (AD DS) podem ligar-se. Além disso:

* Aprovisionar um [certificado de gestão do Azure](http://msdn.microsoft.com/library/azure/gg551722.aspx) no Olá Gateway de RD para que seja anfitrião só Olá permitido tooaccess Olá portal do Azure.
* Associar Olá Gateway de RD toohello mesmo [domínio de gestão](http://technet.microsoft.com/library/bb727085.aspx) como Olá estações de trabalho do administrador. Isto é necessário quando estiver a utilizar um site para site IPsec VPN ou ExpressRoute dentro de um domínio que tenha uma confiança unidirecional de tooAzure AD, ou se forem credenciais de Federação no local instância do AD DS e o Azure AD.
* Configurar um [política de autorização de ligação de cliente](http://technet.microsoft.com/library/cc753324.aspx) toolet Olá Gateway de RD Verifique se o nome do computador cliente Olá é válido (associado ao domínio) e tooaccess permitidos Olá portal do Azure.
* Utilize IPsec para [VPN do Azure](https://azure.microsoft.com/documentation/services/vpn-gateway/) toofurther proteger o tráfego de gestão de roubo de espionagem e token ou considere uma ligação de Internet isolada através de [Azure ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).
* Ative o Multi-Factor Authentication (através do [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)) ou a autenticação por smart card para administradores que iniciem sessão através do Gateway de RD.
* Configurar origem [restrições de endereço IP](http://azure.microsoft.com/blog/2013/08/27/confirming-dynamic-ip-address-restrictions-in-windows-azure-web-sites/) ou [grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md) Azure toominimize Olá diversas pontos finais de gestão permitidos.

## <a name="security-guidelines"></a>Diretrizes de segurança
Em geral, ajudar toosecure administrador as estações de trabalho para utilização com a nuvem de Olá é semelhante toohello práticas utilizadas para qualquer estação de trabalho no local — por exemplo, compilação minimizada e permissões restritivas. Alguns aspetos exclusivos da gestão de nuvem são mais akin tooremote ou de gestão fora de banda empresarial. Estes incluem a utilização de Olá e auditoria de credenciais, acesso remoto avançada de segurança e a deteção de ameaças e resposta.

### <a name="authentication"></a>Autenticação
Pode utilizar endereços IP de origem de tooconstrain de restrições de início de sessão do Azure para aceder a ferramentas administrativas e auditar pedidos de acesso. toohelp Azure identificar os clientes de gestão (estações de trabalho e/ou aplicações), pode configurar o SMAPI (através de ferramentas desenvolvidas por clientes, tais como os cmdlets do Windows PowerShell) e toobe de certificados de gestão do lado do cliente do Olá toorequire portal do Azure instalado, além disso tooSSL certificados. Recomendamos também que o acesso de administrador exija uma autenticação multifator.

Algumas aplicações ou serviços que implementa no Azure podem ter os seus próprios mecanismos de autenticação para acesso de administrador e de utilizador final, enquanto que outros tiram o máximo partido do Azure AD. Dependendo se forem credenciais de Federação através de serviços de Federação do Active Directory (AD FS), utilizando a sincronização de diretórios ou a manutenção de contas de utilizador apenas na Olá nuvem, utilizando o [Microsoft Identity Manager](https://technet.microsoft.com/library/mt218776.aspx) (fazem parte da O Azure AD Premium) ajuda a gerir os ciclos de vida de identidade entre os recursos de Olá.

### <a name="connectivity"></a>Conectividade
Vários mecanismos é tooyour de ligações de cliente seguras toohelp disponíveis redes virtuais do Azure. Dois destes mecanismos, [VPN site a site](https://channel9.msdn.com/series/Azure-Site-to-Site-VPN) (S2S) e [VPN ponto a site](../vpn-gateway/vpn-gateway-point-to-site-create.md) (P2S), ativar a utilização de Olá da indústria padrão IPsec (S2S) ou Olá [(Secure Socket Tunneling Protocol)](https://technet.microsoft.com/magazine/2007.06.cableguy.aspx)(SSTP) (P2S) para encriptação e túnel. Quando o Azure está a ligar a gestão de serviços do Azure destinado ao toopublic como Olá portal do Azure, o Azure requer Hypertext Transfer Protocol Secure (HTTPS).

Uma estação de trabalho protegida autónoma que se ligam tooAzure através de um Gateway de RD deve utilizar Olá baseada em SSTP ponto a site VPN toocreate Olá ligação inicial toohello Azure Virtual Network e, em seguida, estabelecer tooindividual de ligação de RDP virtual máquinas de com o túnel VPN de Olá.

### <a name="management-auditing-vs-policy-enforcement"></a>Auditoria de gestão versus aplicação de políticas
Normalmente, existem duas abordagens para ajudar os processos de gestão toosecure: política de auditoria e imposição. Utilizar as duas abordagens proporciona controlos abrangentes, mas pode não ser possível em todas as situações. Além disso, cada abordagem tem diferentes níveis de risco, custos e esforços associados à gestão de segurança, particularmente como se relaciona com o nível de toohello de confiança colocados nos indivíduos e nas arquiteturas do sistema.

Monitorização, registo e auditoria fornecem uma base para controlar e compreender as atividades administrativas, mas não pode ser sempre tooaudit exequível concluir de todas as ações em detalhe devido toohello quantidade de dados gerados. Eficácia de Olá das políticas de gestão de Olá de auditoria é uma melhor prática, no entanto.

A aplicação de políticas que inclui os controlos de acesso restritos estabelece os mecanismos programáticos que podem reger as ações do administrador e ajuda a garantir que todas as medidas de proteção possíveis estão a ser utilizadas. O registo fornece uma prova da aplicação, no registo de tooa de adição de quem fez o quê, de onde e quando. Registo também permite-lhe tooaudit e uma evidência informações sobre como os administradores seguem as políticas e fornece uma prova de atividades

## <a name="client-configuration"></a>Configuração do cliente
Recomendamos três configurações primárias para uma estação de trabalho protegida. Olá maiores diferenciadores entre essas configurações são o custo, a utilização e acessibilidade, mantendo um perfil de segurança semelhantes em todas as opções. Olá, a tabela seguinte fornece uma breve análise dos Olá tooeach de benefícios e riscos. (Tenha em atenção que "PC empresarial" refere-se tooa ambiente de trabalho PC configuração padrão que seria implementada para todos os utilizadores de domínio, independentemente das funções.)

| Configuração | Benefícios | Contras |
| --- | --- | --- |
| Estação de trabalho autónoma protegida |Estação de trabalho controlada de forma apertada |Custo mais elevado para os computadores dedicados |
| - | Risco reduzido de explorações de aplicações |Esforço de gestão aumentado |
| - | Clara separação das funções | - |
| PC empresarial como máquina virtual |Custos de hardware reduzidos | - |
| - | Segregação da função e das aplicações | - |
| Windows toogo com encriptação de unidade BitLocker |Compatibilidade com a maioria dos PCs |Controlo de recursos |
| - | Eficácia de custos e portabilidade | - |
| - | Ambiente de gestão isolado |- |

É importante que hello estação de trabalho protegida é anfitrião Olá e hello convidado, sem nada entre Olá aloja o hardware de sistema e Olá sistema operativo. Seguir Olá "princípio de origem limpo" (também conhecido como "origem segura") significa que alojam Olá deve ser Olá mais protegido. Caso contrário, hello estação de trabalho protegida (convidado) é requerente tooattacks no sistema de Olá em que está alojado.

Pode segregar mais as funções administrativas através de imagens dedicadas do sistema para cada estação de trabalho protegida que tenha apenas as ferramentas de Olá e as permissões necessitam para gerir selecione Azure aplicações e na cloud, com específico GPOs do DS AD local para Olá tarefas necessárias.

Para ambientes de TI que não tenham nenhuma infraestrutura no local (por exemplo, sem acesso tooa instância local do AD DS para GPOs, porque todos os servidores estão na nuvem de Olá), um serviço, tal como [Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx) pode simplificar a implementação e manutenção configurações de estação de trabalho.

### <a name="stand-alone-hardened-workstation-for-management"></a>Estação de trabalho autónoma protegida para gestão
Com uma estação de trabalho autónoma protegida, os administradores têm um PC ou portátil que podem utilizar para as tarefas administrativas e outro PC ou portátil separado para as tarefas não administrativas. Uma estação de trabalho dedicada toomanaging os serviços do Azure não necessita de outras aplicações instaladas. Além disso, utilizar estações de trabalho que suportam um [Trusted Platform Module](https://technet.microsoft.com/library/cc766159) (TPM) ou tecnologia de criptografia ao nível do hardware semelhante ajuda na autenticação dos dispositivos e na prevenção de determinados ataques. TPM também pode suportar proteção de volume completo da unidade de sistema Olá utilizando [encriptação de unidade BitLocker](https://technet.microsoft.com/library/cc732774.aspx).

Cenário de estação de trabalho autónoma protegida Olá (mostrado abaixo), a instância local do Olá da Firewall do Windows (ou uma firewall para cliente que não sejam da Microsoft) é tooblock configurado ligações, tais como RDP de entrada. administrador de Olá pode iniciar sessão toohello estação de trabalho protegida e iniciar uma sessão do RDP que liga tooAzure depois de estabelecer uma VPN ligar uma rede Virtual do Azure, mas não podem iniciar sessão tooa empresarial PC e utilize RDP tooconnect toohello protegido estação de trabalho em si.

![][2]

### <a name="corporate-pc-as-virtual-machine"></a>PC empresarial como máquina virtual
Em casos onde separada autónoma estação de trabalho protegida tem custos proibitivo ou impraticáveis, Olá estação de trabalho protegida pode alojar um tooperform da máquina virtual que as tarefas de não administrativas.

![][3]

tooavoid várias riscos de segurança que podem surgir da utilização de uma estação de trabalho para gestão de sistemas e outras tarefas de trabalho diárias, pode implementar um toohello de máquina virtual de Hyper-V do Windows protegido estação de trabalho. Esta máquina virtual pode ser utilizada como Olá PC empresarial. ambiente do PC empresarial Olá pode permanecer isolado do Olá anfitrião, o que reduz a superfície de ataque e remove atividades diárias do utilizador Olá (tais como e-mail) deixem de coexistir com as tarefas administrativas sensíveis.

Olá máquinas de virtuais de PC empresarial é executada num espaço protegido e fornece as aplicações de utilizador. o anfitrião de Olá permanece uma "origem limpa" e impõe as políticas de rede restritas no sistema de operativo Olá raiz (por exemplo, bloqueio do acesso RDP da máquina virtual de Olá).

### <a name="windows-toogo"></a>Windows tooGo
Outro toorequiring alternativo uma estação de trabalho autónoma protegida é toouse um [Windows tooGo](https://technet.microsoft.com/library/hh831833.aspx) unidade, uma funcionalidade que suporta uma capacidade de arranque USB do lado do cliente. Windows tooGo permite que os utilizadores tooboot um PC compatível tooan isolado imagem do sistema executando a partir de uma pen USB encriptada. Esta fornece controlos adicionais para pontos finais de administração remota porque a imagem de Olá pode ser completamente gerida por um grupo TI empresarial, com políticas de segurança restritas, uma compilação do SO mínima e suporte do TPM.

Na figura Olá abaixo, Olá imagem dos portáteis é um sistema associado a um domínio que é tooAzure apenas tooconnect pré-configuradas, necessita de autenticação multifator e bloqueia todo o tráfego de gestão não. Se um utilizador arranques hello mesmo PC toohello imagem padrão da empresa e tenta aceder ao Gateway de RD para ferramentas de gestão do Azure, a sessão de Olá está bloqueada. Windows tooGo torna-se o sistema de operativo Olá nível de raiz e não camadas adicionais são necessário (anfitrião de funcionamento do sistema, hipervisor, máquina virtual) que pode ser mais vulneráveis toooutside ataques.

![][4]

É importante toonote que pens USB perdem mais facilmente a um PC de secretária. Utilização do BitLocker tooencrypt Olá volume completo, juntamente com uma palavra-passe segura, torna menos provável que o atacante pode utilizar a imagem de disco Olá para efeitos prejudiciais. Além disso, se se perder Olá pen USB, revogar e [emitir um novo certificado de gestão](https://technet.microsoft.com/library/hh831574.aspx) juntamente com uma palavra-passe rápida reposição pode reduzir a exposição. Registos de auditoria administrativos residem no Azure, não no cliente de Olá, reduzindo ainda mais os potencial perda de dados.

## <a name="best-practices"></a>Melhores práticas
Considere Olá seguintes diretrizes adicionais quando estiver a gerir aplicações e dados no Azure.

### <a name="dos-and-donts"></a>O que deve fazer e o que não deve fazer
Não parta do princípio que porque foi bloqueada de uma estação de trabalho para baixo do que outros requisitos de segurança comuns não é necessário toobe cumprido. risco potencial Olá é superior devido níveis de acesso elevados que geralmente possuem contas de administrador. Exemplos de riscos e as respetivas práticas de segurança alternativas são apresentados na tabela de Olá abaixo.

| O que não deve fazer | O que deve fazer |
| --- | --- |
| Não envie por e-mail as credenciais de acesso de administrador ou outros segredos (por exemplo, certificados SSL ou certificados de gestão) |Mantenha a confidencialidade entregando os nomes de conta e as palavras-passe pessoalmente ou por telefone (mas não os armazenando num voice mail); efetue uma instalação remota dos certificados de cliente/servidor (através de uma sessão encriptada); transfira a partir de uma partilha de rede protegida ou distribua manualmente através do suporte de dados amovível. |
| - | A gestão dos ciclos de vida dos certificados de gestão deve ser feita de forma pró-ativa. |
| Não armazene palavras-passe da conta não encriptadas ou sem hash no armazenamento de aplicações (como folhas de cálculo, sites do SharePoint ou partilhas de ficheiros). |Estabeleça princípios de gestão de segurança e as políticas de proteção do sistema e aplicá-las tooyour ambiente de desenvolvimento. |
| - | Utilize [avançada Mitigation Experience Toolkit 5.5](https://technet.microsoft.com/security/jj653751) afixação de certificado regras de sites do tooensure acesso adequado tooAzure SSL/TLS. |
| Não partilhe as contas ou as palavras-passe entre administradores nem reutilize palavras-passe em várias contas de utilizador ou serviços, especialmente nas redes sociais ou para outras atividades não administrativas. |Criar um toomanage de conta Microsoft dedicada a sua subscrição do Azure — uma conta que não é utilizada para o e-mail pessoal. |
| Não envie por e-mail os ficheiros de configuração. |Os perfis e ficheiros de configuração devem ser instalados a partir de uma origem fidedigna (por exemplo, uma pen USB encriptada) e não a partir de um mecanismo que possa ficar facilmente comprometido, como o e-mail. |
| Não utilize palavras-passe de início de sessão fracas ou simples. |Aplique políticas de palavras-passe seguras, ciclos de expiração (mudança na primeira utilização), tempos limite da consola e bloqueios automáticos das contas. Utilize um sistema de gestão de palavras-passe cliente com Multi-Factor Authentication para acesso ao cofre de palavras-passe. |
| Não exponha as portas de gestão toohello Internet. |Bloqueio para baixo de portas do Azure e acesso de gestão de toorestrict de endereços IP. Para obter mais informações, consulte Olá [segurança de rede de Azure](http://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx) documento técnico. |
| - | Utilize firewalls, VPNs e NAP para todas as ligações de gestão. |

## <a name="azure-operations"></a>Operações do Azure
Na operação do Microsoft Azure, os engenheiros de operações e o pessoal do suporte que acedem aos sistemas de produção do Azure utilizam [PCs de secretária protegidos com VMs](#stand-alone-hardened-workstation-for-management) com aprovisionamento para o acesso à rede empresarial interna e às respetivas aplicações (como e-mail, intranet, etc.). Todos os computadores de estação de trabalho de gestão têm TPMs, unidade de arranque do anfitrião de Olá é encriptada com BitLocker e estão associados a um tooa especial unidade organizacional (UO) no domínio empresarial principal da Microsoft.

A proteção do sistema é aplicada através da Política de Grupo, com a atualização de software centralizada. Para auditoria e análise, os registos de eventos (por exemplo, segurança e AppLocker) são recolhidos a partir de estações de trabalho de gestão e guardados tooa de localização central.

Além disso, dedicadas as caixas de atalhos na rede da Microsoft que necessitam de autenticação de dois fatores são rede de produção do tooAzure tooconnect utilizados.

## <a name="azure-security-checklist"></a>Lista de verificação de segurança do Azure
Minimizar Olá número de tarefas que os administradores podem efetuar numa estação de trabalho protegida ajuda a minimizar a superfície de ataque de Olá no ambiente de gestão e desenvolvimento. Olá de utilização seguintes tecnologias toohelp proteger a sua estação de trabalho protegida:

* Proteção do IE. Olá browser Internet Explorer (ou qualquer browser, para esse fim) é um ponto de entrada chave para código prejudicial devido tooits interações extensas com servidores externos. Reveja as suas políticas de cliente e aplique a execução no modo protegido, desativando os suplementos, desativando as transferências de ficheiros e utilizando a filtragem [Microsoft SmartScreen](https://technet.microsoft.com/library/jj618329.aspx). Certifique-se de que os avisos de segurança são apresentados. Tire partido das zonas de Internet e crie uma lista de sites fidedignos para os quais configurou uma proteção razoável. Bloqueie todos os outros sites e códigos no browser, tal como ActiveX e Java.
* Utilizador padrão. Em execução como utilizador normal proporciona diversos benefícios, fazendo com que Olá é que roubo de credenciais de administrador através de software maligno se torne mais difícil. Além disso, uma conta de utilizador padrão não tem privilégios elevados no sistema de operativo Olá raiz e muitas APIs e opções de configuração são bloqueadas por predefinição.
* AppLocker. Pode utilizar [AppLocker](http://technet.microsoft.com/library/ee619725.aspx) toorestrict Olá programas e os scripts que os utilizadores podem executar. Pode executar o AppLocker no modo de auditoria ou de imposição. Por predefinição, o AppLocker tem uma regra que permite aos utilizadores que tenham um toorun de token de administrador todo o código no cliente Olá. Esta regra existe tooprevent administradores do bloqueiem a próprios, e esta aplica-se apenas tooelevated tokens. Consulte também Integridade do Código como parte da [segurança de núcleo](http://technet.microsoft.com/library/dd348705.aspx) do Windows Server.
* Assinatura de código. A assinatura de código de todas as ferramentas e scripts utilizadas por administradores fornece um mecanismo gerível para a implementação de políticas de bloqueio de aplicações. Os hashes não se ajustam com o código de toohello alterações rápidas e caminhos de ficheiros não fornecem um elevado nível de segurança. Deve combinar regras do AppLocker com um PowerShell [política de execução](http://technet.microsoft.com/library/ee176961.aspx) que só permite o código de assinatura específico e scripts toobe [executado](http://technet.microsoft.com/library/hh849812.aspx).
* Política de Grupo. Criar uma política administrativa global que é aplicado tooany domínio estação de trabalho é utilizada para gestão (e bloqueie o acesso de todos os outros) e contas de toouser autenticadas nessas estações de trabalho.
* Aprovisionamento de segurança melhorada. Salvaguarde a imagem de estação de trabalho protegida de linha de base toohelp proteger contra adulteração. Utilize medidas de segurança, como a encriptação e isolamento toostore imagens, máquinas virtuais e scripts e restringir o acesso (talvez processo utilize uma auditável verificação-na entrada/saída).
* Aplicação de patches. Mantenha uma compilação consistente (ou tenha imagens separadas para o desenvolvimento, operações e outras tarefas administrativas), procure alterações e software maligno regularmente, mantenha a compilação Olá segurança toodate e ative apenas os computadores quando for necessário.
* Encriptação. Certifique-se de que as estações de trabalho de gestão têm um toomore TPM forma segura, permitir [sistema de encriptação de ficheiros](https://technet.microsoft.com/library/cc700811.aspx) (EFS) e o BitLocker. Se estiver a utilizar o Windows tooGo, utilize apenas chaves USB encriptadas juntamente com o BitLocker.
* Governação. Utilize toocontrol de GPOs do DS AD Windows dos administradores Olá todas as interfaces, tais como a partilha de ficheiros. Inclua estações de trabalho de gestão nos processos de auditoria, monitorização e de registo. Controle todos os acessos e utilizações de administrador e programador.

## <a name="summary"></a>Resumo
Utilizar uma configuração de estação de trabalho protegida para administrar os Cloud Services, as Virtual Machines e as aplicações do Azure pode ajudar a evitar vários riscos e ameaças que podem resultar da gestão remota de uma infraestrutura de TI crítica. O Azure e o Windows fornecem mecanismos que pode utilizar toohelp protegerem e controlam o comportamento de comunicações, a autenticação e o cliente.

## <a name="next-steps"></a>Passos seguintes
Olá seguintes recursos estão disponível tooprovide informações mais gerais sobre o Azure e relacionados com serviços da Microsoft, adição toospecific os itens referenciados neste documento:

* [Proteger o acesso privilegiado](https://technet.microsoft.com/library/mt631194.aspx) – Obtenha detalhes técnicos Olá para estruturação e criação de uma estação de trabalho administrativa segura para gestão do Azure
* [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Security/AzureSecurity) - Saiba mais sobre as capacidades da plataforma Azure que protegem Olá a recursos de infraestrutura do Azure e Olá cargas de trabalho que execute no Azure
* [Microsoft Security Response Center](http://www.microsoft.com/security/msrc/default.aspx) – onde podem ser comunicadas as vulnerabilidades de segurança da Microsoft, incluindo problemas com o Azure, ou através de e-mail demasiado[secure@microsoft.com](mailto:secure@microsoft.com)
* [Blogue de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – manter-se toodate no Olá mais recente segurança do Azure

<!--Image references-->
[1]: ./media/azure-security-management/typical-management-network-topology.png
[2]: ./media/azure-security-management/stand-alone-hardened-workstation-topology.png
[3]: ./media/azure-security-management/hardened-workstation-enabled-with-hyper-v.png
[4]: ./media/azure-security-management/hardened-workstation-using-windows-to-go-on-a-usb-flash-drive.png
