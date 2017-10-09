---
title: "aaaSecurity alertas por tipo no Centro de segurança do Azure | Microsoft Docs"
description: "Este artigo aborda os diferentes tipos de Olá de alertas de segurança disponíveis no Centro de segurança do Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b3e7b4bc-5ee0-4280-ad78-f49998675af1
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: ee69cb9035c35f5bc2ed51f9b9d6f29486b4caf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-security-alerts-in-azure-security-center"></a>Compreender os alertas de segurança no Centro de Segurança do Azure
Este artigo ajuda-o a toounderstand Olá diferentes tipos de alertas de segurança e insights relacionados que estão disponíveis no Centro de segurança do Azure. Para mais informações sobre como ver os alertas de toomanage e incidentes, [toosecurity está a responder e gerir alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md).

> [!NOTE]
> tooset segurança as deteções avançadas, a atualização tooAzure padrão de centro de segurança. Está disponível uma avaliação gratuita de 60 dias. tooupgrade, selecione **escalão de preço** no Olá [política de segurança](security-center-policies.md). toolearn mais, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/security-center/).
>

## <a name="what-type-of-alerts-are-available"></a>Que tipo de alertas estão disponíveis?
Centro de segurança do Azure utiliza uma variedade de [as capacidades de deteção](security-center-detection-capabilities.md) tooalert clientes toopotential ataques filtragem respetivos ambientes. Estes alertas contenham informações importantes sobre Olá que acionada Olá alerta, recursos de Olá direcionados e Olá origem do ataque Olá. informações de Olá incluídas um alerta variam com base no tipo de Olá de análise utilizado toodetect Olá ameaça. Os incidentes também podem conter informações contextuais adicionais que podem ser úteis ao investigar uma ameaça.  Este artigo fornece informações sobre Olá os seguintes tipos de alerta:

* Análise Comportamental de Máquinas Virtuais (VMBA)
* Análise de Rede
* Análise de Recursos
* Informações Contextuais

## <a name="virtual-machine-behavioral-analysis"></a>Análise comportamental de máquinas virtuais
Centro de segurança do Azure podem utilizar recursos de tooidentify comprometido de análise comportamental com base na análise de registos de eventos de máquina virtual. Por exemplo, Eventos de Criação de Processos e Eventos de Início de Sessão. Além disso, não há correlação com outro toocheck sinais para provas de uma campanha ampla.

> [!NOTE]
> Para obter mais informações sobre como funcionam as capacidades de deteção do Centro de Segurança, veja [Capacidades de deteção do Centro de Segurança do Azure](security-center-detection-capabilities.md).
>

### <a name="crash-analysis"></a>Análise de falhas
Análise de memória de informação de falha é um método utilizado toodetect software maligno que é tooevade capaz de soluções de segurança tradicionais. Várias formas de software maligno tente hipótese de Olá tooreduce de que está a ser detetada pelo antivírus ao nunca escrever toodisk ou encriptar componentes de software escritos toodisk. Isto torna toodetect difícil de software maligno Olá através da utilização de abordagens de antimalware tradicionais. No entanto, este tipo de software maligno pode ser detetado através da utilização de análise de memória, porque o software maligno tem de deixar rastreios na memória no toofunction de ordem.

Quando o software falha, as informações de falhas de sistema captura uma parte da memória no momento de Olá de falhas de Olá. falhas de Olá podem ser provocada por software maligno, aplicações gerais ou problemas de sistema. Ao analisar a memória de Olá na captura de falhas de Olá, o Centro de segurança pode detetar técnicas utilizadas tooexploit vulnerabilidades no software, aceder a dados confidenciais e persistir clandestinamente na máquina comprometida. Isto é conseguido com desempenho mínimo impacto toohosts como analysis Olá é realizado Olá terminar do Centro de segurança novamente.

Olá campos a seguir é comuns toohello falhas informação alerta exemplos que são apresentadas neste artigo:

* DUMPFILE: Nome do ficheiro de informação de falha de Olá.
* PROCESSNAME: Nome de Olá processo a falhar.
* PROCESSVERSION: Versão de Olá processo a falhar.

### <a name="shellcode-discovered"></a>Shellcode detetado
Shellcode é payload Olá que é executado após uma vulnerabilidade de software exploits de software maligno. Este alerta indica que a análise da informação de falha de sistema detetou código executável que apresenta um comportamento que é normalmente tido por payloads maliciosos. Apesar de o software não malicioso poder ter este comportamento, não é característico das práticas normais de desenvolvimento de software.

exemplo de alerta de Shellcode Olá fornece Olá seguir campo adicional:

* ENDEREÇO: localização de Olá na memória de Olá shellcode.

Este é um exemplo deste tipo de alerta:

![Alerta de Shellcode](./media/security-center-alerts-type/security-center-alerts-type-fig2.png)

### <a name="module-hijacking-discovered"></a>Módulo de hijacking detetado
O Windows utiliza bibliotecas de ligação dinâmica (DLLs) tooallow software tooutilize comuns Windows funcionalidade do sistema. DLL assumir ocorre quando software maligno alterado Olá DLL carga ordem tooload maliciosos payloads na memória, onde pode ser executado de código arbitrário. Este alerta indica que a análise de captura de falhas de Olá detetado um módulo com o nome da mesma forma que é carregado a partir de dois caminhos diferentes. Um dos caminhos de Olá carregado provém de uma localização comum de sistema binária do Windows.

Os programadores de software legítimos ocasionalmente alterar a ordem de carregamento DLL Olá por motivos não maliciosos, tais como instrumentação, expandir Olá SO Windows ou expandir uma aplicação do Windows. toohelp distinguir entre as alterações malicioso e potencialmente benignas toohello ordem de carregamento da DLL, o Centro de segurança do Azure verifica se um módulo carregado está em conformidade com perfil suspeita tooa. resultado Olá desta verificação é indicado pelo campo com "Assinatura" Olá alerta Olá e será refletido na gravidade Olá de alerta de Olá, descrição do alerta e passos de remediação de alerta. Se o módulo Olá é legítimo ou maliciosos, tooresearch analisar Olá na cópia de disco de Olá assumir o módulo. Por exemplo, pode verificar a assinatura digital do ficheiro de Olá ou executar uma análise de antivírus.

Além disso toohello campos comuns descritos na secção de anterior "Shellcode detetados" Olá, este alerta disponibiliza Olá seguintes campos:

* ASSINATURA: Indica se Olá assumir o módulo está em conformidade tooa perfil de comportamento suspeito.
* HIJACKEDMODULE: nome Olá Olá hijacked módulo de sistema do Windows.
* HIJACKEDMODULEPATH: caminho de Olá de Olá hijacked módulo de sistema do Windows.
* HIJACKINGMODULEPATH: caminho de Olá do módulo de hijacking Olá.

Este é um exemplo deste tipo de alerta:

![Alerta de hijacking do módulo](./media/security-center-alerts-type/security-center-alerts-type-fig3.png)

### <a name="masquerading-windows-module-detected"></a>Módulo do Windows de disfarce detetado
Software maligno pode utilizar nomes comuns dos binários de sistema do Windows (por exemplo, SVCHOST. EXE) ou os módulos (por exemplo, NTDLL. DLL) demasiado*se misturem* e ocultar natureza Olá de software malicioso de Olá aos administradores de sistema. Este alerta indica que a análise de captura de falhas de Olá Deteta que esse ficheiro de informação de falha de Olá contém módulos que utilizem nomes de módulo de sistema do Windows, mas não satisfazer outros critérios que são normais de módulos do Windows. Analisa Olá na cópia de disco do módulo masquerading Olá poderá fornecer mais informações sobre a natureza de legítimos ou maliciosos Olá deste módulo. A análise pode incluir:

* Certifique-se de que o ficheiro Olá em questão vem incluído como parte de um pacote de software legítima.
* Verificar a assinatura digital do ficheiro de Olá.
* Execute uma análise de antivírus no ficheiro de Olá.

Além disso toohello campos comuns descritos anteriormente na secção de "Shellcode detetado" Olá, este alerta disponibiliza Olá seguintes campos adicionais:

* Detalhes: Descreve se os metadados do módulo Olá são válido e se o módulo Olá foi carregado a partir de um caminho de sistema.
* : Olá nome do módulo do Windows masquerading Olá.
* CAMINHO: Olá caminho toohello masquerading módulo do Windows.

Este alerta também extrai e apresenta determinados campos de cabeçalho de PE do módulo Olá, tais como "Soma" e "TIMESTAMP". Estes campos são apresentados apenas se não estiverem presentes no módulo Olá campos Olá. Consulte Olá [Microsoft PE e a especificação de COFF](https://msdn.microsoft.com/windows/hardware/gg463119.aspx) para obter detalhes sobre estes campos.

Este é um exemplo deste tipo de alerta:

![Alerta de Windows de disfarce](./media/security-center-alerts-type/security-center-alerts-type-fig4.png)

### <a name="modified-system-binary-discovered"></a>Binário de sistema modificado detetado
Software maligno pode modificar os binários do sistema de núcleos na ordem toocovertly aceder a dados ou persistir clandestinamente num sistema comprometido. Este alerta indica que o analysis de informação de falha de Olá detetou que os binários de SO de Windows core tem sido modificados na memória ou no disco.

Os programadores de software legítimo modificam ocasionalmente módulos do sistema na memória por razões não maliciosas, por exemplo, para desvios ou para compatibilidade de aplicações. toohelp diferenciar entre módulos maliciosos e potencialmente legítimos, Centro de segurança do Azure verifica se o módulo modificado Olá está em conformidade perfil suspeita tooa. resultado Olá desta verificação é indicado por gravidade Olá de alerta de Olá, descrição do alerta e passos de remediação de alerta.

Além disso toohello campos comuns descritos anteriormente na secção de "Shellcode detetado" Olá, este alerta disponibiliza Olá seguintes campos adicionais:

* MODULENAME: Nome do Olá modificado sistema binário.
* MODULEVERSION: Versão de Olá modificado sistema binário.

Este é um exemplo deste tipo de alerta:

![Alerta de binário do sistema](./media/security-center-alerts-type/security-center-alerts-type-fig5.png)

### <a name="suspicious-process-executed"></a>Processos suspeitos executados
Centro de segurança identificar um processo suspeito que é executado na máquina de virtual de destino Olá e, em seguida, um alerta é acionado. Deteção de Olá não procura o nome específico Olá, mas serve para o parâmetro do ficheiro executável Olá. Por conseguinte, mesmo que o atacante Olá muda o nome de executável Olá, o Centro de segurança pode detetar ainda processo suspeito Olá.

Este é um exemplo deste tipo de alerta:

![Alerta de processos suspeitos](./media/security-center-alerts-type/security-center-alerts-type-fig6-new.png)

### <a name="multiple-domain-accounts-queried"></a>Várias contas de domínio consultadas
Centro de segurança pode detetar várias tentativas tooquery contas de domínio do Active Directory, que é algo normalmente executados pelos atacantes durante reconhecimento de rede. Os atacantes podem tirar partido desta técnica tooquery Olá tooidentify Olá os utilizadores de domínio, identificar contas de administrador de domínio Olá, identificar Olá computadores que são controladores de domínio e também identificam Olá potenciais domínio relação de confiança com outros domínios.

Este é um exemplo deste tipo de alerta:

![Alerta de conta de vários domínios](./media/security-center-alerts-type/security-center-alerts-type-fig7-new.png)

### <a name="local-administrators-group-members-were-enumerated"></a>Foram enumerados membros do grupo de Administradores Locais

Centro de segurança vai tootrigger um alerta quando o evento de segurança Olá 4798, no Windows Server 2016 e o Windows 10, é acionar. Isto acontece quando são enumerados grupos de administradores locais, que é algo normalmente efetuado pelos atacantes durante o reconhecimento de rede. Os atacantes podem tirar partido esta identidade de Olá tooquery técnica de utilizadores com privilégios administrativos.

Este é um exemplo deste tipo de alerta:

![Administrador local](./media/security-center-alerts-type/security-center-alerts-type-fig14-new.png)

### <a name="anomalous-mix-of-upper-and-lower-case-characters"></a>Mistura anómala de carateres minúsculos e maiúsculos

Centro de segurança irá acionar um alerta quando Deteta uma combinação de maiúsculas e minúsculas carateres na linha de comandos Olá utilização Olá. Alguns os atacantes podem utilizar este toohide técnica de maiúsculas e minúsculas ou hash com base em regras de máquina.

Este é um exemplo deste tipo de alerta:

![Mistura anómala](./media/security-center-alerts-type/security-center-alerts-type-fig15-new.png)

### <a name="suspected-kerberos-golden-ticket-attack"></a>Ataque de Pedido Dourado Kerberos suspeito

Um comprometido [krbtgt](https://technet.microsoft.com/library/dn745899.aspx) chave pode ser utilizada por um atacante toocreate Kerberos "Dourada bilhetes," Permitir Olá atacante tooimpersonate qualquer utilizador que pretendam. Centro de segurança vai tootrigger um alerta quando Deteta este tipo de atividade.

> [!NOTE] 
> Para mais informações sobre o Pedido Dourado Kerberos, leia [Windows 10 credential theft mitigation guide (Guia de atenuação de roubo de credenciais do Windows 10)](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx).

Este é um exemplo deste tipo de alerta:

![Pedido dourado](./media/security-center-alerts-type/security-center-alerts-type-fig16-new.png)

### <a name="suspicious-account-created"></a>Conta suspeita criada

O Centro de Segurança irá acionar um alerta quando for criada uma conta semelhante a uma conta de privilégios administrativos incorporada existente. Esta técnica pode ser utilizada por toocreate atacantes um rogue tooavoid que está a ser reparado por humana verificação de conta.
 
Este é um exemplo deste tipo de alerta:

![Conta suspeita](./media/security-center-alerts-type/security-center-alerts-type-fig17-new.png)

### <a name="suspicious-firewall-rule-created"></a>Regra de Firewall suspeita criada

Os atacantes podem tentar toocircumvent segurança de anfitrião através da criação de regras de firewall personalizadas tooallow toocommunicate de malicioso aplicações com o comando e controlo ou ataques de toolaunch através da rede de Olá através de Olá comprometido anfitrião. O Centro de Segurança irá acionar um alerta quando detetar que foi criada uma nova regra de firewall de um ficheiro executável numa localização suspeita.
 
Este é um exemplo deste tipo de alerta:

![Regra de firewall](./media/security-center-alerts-type/security-center-alerts-type-fig18-new.png)

### <a name="suspicious-combination-of-hta-and-powershell"></a>Combinação suspeita de HTA e PowerShell

O Centro de Segurança irá acionar um alerta quando detetar que um Anfitrião de Aplicação HTML (HTA) da Microsoft está a iniciar comandos do PowerShell. Esta é uma técnica utilizada pelo scripts do PowerShell maliciosos toolaunch atacantes.
 
Este é um exemplo deste tipo de alerta:

![HTA e PS](./media/security-center-alerts-type/security-center-alerts-type-fig19-new.png)


## <a name="network-analysis"></a>Análise de rede
A deteção de ameaças de rede do Centro de Segurança funciona através da recolha automática de informações de segurança a partir do tráfego do Azure IPFIX (Internet Protocol Flow Information Export). Analisa esta informação, muitas vezes correlacionando informações de várias origens, tooidentify ameaças.

### <a name="suspicious-outgoing-traffic-detected"></a>Tráfego de saída suspeito detetado
Dispositivos de rede podem ser detetados e profiled no muito Olá mesma forma que outros tipos de sistemas. Normalmente, os atacantes começam por uma análise de portas ou varrimento de portas. No exemplo seguinte Olá, terá de tráfego de Secure Shell (SSH) suspeita de uma VM. Neste cenário, é possível um ataque de força bruta SSH ou de varrimento de portas contra um recurso externo.

![Alerta de tráfego de saída suspeito](./media/security-center-alerts-type/security-center-alerts-type-fig8.png)

Este alerta dá-informações que pode utilizar recursos de Olá tooidentify que foi utilizado tooinitiate este ataque. Este alerta também fornece informações tooidentify Olá comprometido máquina, hora da deteção de Olá, plus protocolo Olá e a porta que foi utilizada. Este painel também fornece uma lista dos passos de remediação que podem ser utilizado toomitigate este problema.

### <a name="network-communication-with-a-malicious-machine"></a>Comunicação de rede com uma máquina maliciosa
Ao tirar partido dos feeds de informações sobre ameaças da Microsoft, o Centro de Segurança do Azure pode detetar máquinas comprometidas que comunicam com endereços IP maliciosos. Em muitos casos, o endereço malicioso Olá é um centro de comando e controlo. Neste caso, o Centro de segurança detetou que a comunicação de Olá foi efetuada através da utilização de software maligno Pony Loader (também conhecido como [Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF)).

![alerta de comunicação de rede](./media/security-center-alerts-type/security-center-alerts-type-fig9.png)

Este alerta dá-informações que lhe permite recursos de Olá tooidentify que foi utilizado tooinitiate este ataque, Olá atacados recursos, Olá IP da vítima, IP do atacante Olá e hora da deteção Olá.

> [!NOTE]
> Os endereços IP em direto foram removidos desta captura de ecrã por motivos de privacidade.
>
>

### <a name="possible-outgoing-denial-of-service-attack-detected"></a>Possível ataque denial-of-service de saída detetado
Anormal tráfego de rede que origina a partir de uma máquina virtual pode fazer com que o Centro de segurança tootrigger um tipo de denial-of-service potencial de ataque.

Este é um exemplo deste tipo de alerta:

![DOS de saída](./media/security-center-alerts-type/security-center-alerts-type-fig10-new.png)

## <a name="resource-analysis"></a>Análise de recursos
Análise de recursos de centro de segurança centra-se na plataforma como dos serviços de serviço (PaaS), tais como a integração de Olá com Olá [deteção de ameaças da SQL Database do Azure](../sql-database/sql-database-threat-detection.md) funcionalidade. Com base nos resultados da análise de Olá destas áreas, o Centro de segurança aciona um alerta de recursos.

### <a name="potential-sql-injection"></a>Potencial injeção de SQL
Injeção de SQL é um ataque onde é inserido código malicioso nas cadeias que são transmitidas posteriormente tooan instância do SQL Server para análise e execução. Uma vez que o SQL Server executa todas as consultas sintaticamente válidas que recebe, qualquer procedimento que crie instruções SQL deve ser revisto em termos de vulnerabilidades de injeção. A deteção de ameaças do SQL Server utiliza o machine learning, análise comportamental e anomalias deteção toodetermine suspeita eventos que podem ser executadas em bases de dados SQL do Azure. Por exemplo:

* Tentativa de acesso à base de dados por um antigo funcionário
* Ataques de injeção de SQL
* Base de dados do access invulgar tooa produção de um utilizador em casa

![Potencial alerta de injeção de SQL](./media/security-center-alerts-type/security-center-alerts-type-fig11.png)

informações de Olá neste alerta podem ser utilizados tooidentify Olá atacado recursos, hora da deteção Olá e estado de Olá de ataque de Olá. Também fornece uma ligação toofurther passos de investigação.

### <a name="vulnerability-toosql-injection"></a>Vulnerabilidade tooSQL Injeção
Este alerta é acionado quando é detetado um erro de aplicação numa base de dados. Este alerta pode indicar a que ataques de injeção de tooSQL uma possível vulnerabilidade.

![Potencial alerta de injeção de SQL](./media/security-center-alerts-type/security-center-alerts-type-fig12-new.png)

### <a name="unusual-access-from-unfamiliar-location"></a>Acesso invulgar a partir de uma localização desconhecida
Este alerta é acionado quando foi detetado um evento de acesso de um endereço IP familiarizado no servidor de Olá, que não foi visualizada no Olá último período.

![Alerta de acesso invulgar](./media/security-center-alerts-type/security-center-alerts-type-fig13-new.png)

## <a name="contextual-information"></a>Informações contextuais
Durante uma investigação, os analistas precisam de contexto adicional tooreach um verdict sobre a natureza Olá ameaça Olá e como toomitigate-lo.  Por exemplo, foi detetada uma anomalias de rede, mas sem compreender que mais está a acontecer na rede de Olá ou com recurso de toohello direcionado regard é que tootake ações toounderstand cada disco rígido seguinte. tooaid com que, um incidente de segurança podem incluir artefactos, eventos relacionados e informações que possam ajudar investigator Olá. Olá disponibilidade das informações adicionais irão variar com base no Olá o tipo de ameaça detetada Olá a configuração do seu ambiente e não estará disponível para todos os incidentes de segurança.

Se estiver disponíveis informações adicionais, será apresentado no Olá incidente de segurança abaixo lista Olá de alertas. Podem estar contidas informações como:

- Eventos de limpeza de registos
- Dispositivo PNP ligado a partir de um dispositivo desconhecido
- Alertas não acionáveis 

![Alerta de acesso invulgar](./media/security-center-alerts-type/security-center-alerts-type-fig20.png) 


## <a name="see-also"></a>Consultar também
Neste artigo, aprendeu sobre os diferentes tipos Olá de alertas de segurança no Centro de segurança. toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:

* [Lidar com incidentes de segurança no Centro de Segurança do Azure](security-center-incident.md)
* [Capacidades de deteção do Centro de Segurança do Azure](security-center-detection-capabilities.md)
* [Guia de operações e planeamento do Centro de Segurança do Azure](security-center-planning-and-operations-guide.md)
* [FAQ do Centro de segurança do Azure](security-center-faq.md): encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.
* [Blogue de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/): encontre mensagens do blogue acerca da segurança e conformidade do Azure.
