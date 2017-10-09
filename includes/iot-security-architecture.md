# <a name="internet-of-things-security-architecture"></a>Arquitetura de segurança da Internet das coisas
Ao conceber um sistema, é importante toounderstand Olá ameaças toothat sistema e adicionar defesas adequadas em conformidade, como sistema de Olá é concebido e criado de. É particularmente importante toodesign Olá produto Olá início com segurança em mente, porque a compreender como um atacante poderá ser capaz de toocompromise um sistema de ajuda Certifique-se mitigações adequadas estão no local a partir do início de Olá. 

## <a name="security-starts-with-a-threat-model"></a>Segurança começa com um modelo de ameaça
Microsoft utilizou longa modelos de ameaça para os produtos e efetuou ameaça da empresa Olá modelação processo disponível publicamente. Olá experiência da empresa demonstra que Olá modelling tem vantagens inesperadas para além de Olá imediata de compreender de que são Olá relativo à maioria dos. Por exemplo, também cria um compromissos para um debate aberto com outras pessoas fora da equipa de desenvolvimento de Olá, que pode levar toonew ideias e melhoramentos no produto Olá.

objetivo do Olá de modelação de ameaça é toounderstand como um atacante poderá ser capaz de toocompromise um sistema e, em seguida, certifique-se mitigações adequadas são cumpridos. Modelação de ameaça força mitigações de tooconsider de equipa de design Olá como sistema Olá foi concebido em vez depois de um sistema é implementado. Este facto é extremamente importante, porque retrofitting segurança defesas tooa conjunto de dispositivos no campo Olá é infeasible, propensas ao erro e sair clientes em risco.

As equipas de desenvolvimento muitos efetuar uma tarefa excelente capturar Olá funcional os requisitos do sistema de Olá que beneficiam de clientes. No entanto, a identificar as formas não óbvios que alguém poderá utilizar indevidamente sistema Olá é mais difícil. Modelação de ameaça pode ajudar a compreender que um atacante pode fazer as equipas de desenvolvimento e por que motivo. Modelação de ameaça é um processo estruturado, que cria um debate sobre a segurança de Olá decisões de conceção no sistema de Olá, bem como a estrutura de toohello as alterações efetuadas ao longo de forma a Olá ter impacto na segurança. Enquanto um modelo de ameaça é simplesmente um documento, esta documentação também representa uma forma ideal tooensure continuidade de dados de conhecimento, retenção de lições aprendidas e ajudar a equipa do novo carregar rapidamente. Por fim, um resultado de modelação de ameaça é tooenable tooconsider outros aspetos de segurança, tais como os compromissos de segurança pretende tooprovide tooyour clientes. Estes compromissos em conjunto com modelação de ameaça irão informar e unidade testar da sua solução Internet das coisas (IoT).

### <a name="when-toothreat-model"></a>Quando o modelo de toothreat
[Modelação de ameaça](http://www.microsoft.com/security/sdl/adopt/threatmodeling.aspx) ofertas Olá maior valor se incorporada na fase de conceção de Olá. Quando está a conceber, terá de Olá mais flexibilidade toomake alterações tooeliminate ameaças. Eliminar ameaças por predefinição é o resultado desejado Olá. É muito fácil adicionar mitigações, teste-los e assegurar que permanecem atuais e além disso, essa eliminação não é sempre possível. Torna mais difícil tooeliminate ameaças como um produto torna-se mais madura e, por sua vez, fundamentalmente, necessitará mais tarefas e muito mais difícil fala que ameaça numa fase inicial no modelação de desenvolvimento de Olá.

### <a name="what-toothreat-model"></a>O modelo de toothreat
Deve thread solução Olá de modelo como um todo bem como o foco na Olá seguintes áreas:

* funcionalidades de segurança e privacidade Olá
* funcionalidades de Olá cujas falhas são relevante de segurança
* funcionalidades de Olá que touch um limite de fidedignidade 

### <a name="who-threat-models"></a>Quem ameaça modelos
Modelação de ameaça é um processo como qualquer outro.  Este é um documento de modelo de ameaça do boa ideia tootreat Olá como qualquer outro componente da solução de Olá e validá-lo. As equipas de desenvolvimento muitos efetuar uma tarefa excelente capturar Olá funcional os requisitos do sistema de Olá que beneficiam de clientes. No entanto, a identificar as formas não óbvios que alguém poderá utilizar indevidamente sistema Olá é mais difícil. Modelação de ameaça pode ajudar a compreender que um atacante pode fazer as equipas de desenvolvimento e por que motivo.

### <a name="how-toothreat-model"></a>Como toothreat modelo
processo de modelação de ameaça de Olá é constituída por quatro passos; passos de Olá são:

* Aplicação Olá modelo
* Enumerar ameaças
* Mitigar ameaças
* Validar mitigações Olá

#### <a name="hello-process-steps"></a>passos do processo Olá
Três regras prática tookeep em consideração quando criar um modelo de ameaça:

1. Crie um diagrama de arquitetura de referência. 
2. Inicie leque primeiro. Obter uma descrição geral e compreender o sistema de Olá como um todo, antes de diving de avançada.  Isto ajuda a certifique-se de que coloca a descrição profunda no Olá à direita.
3. Unidade processo Olá, não permita que o processo de Olá unidade. Se encontrar um problema na fase de modelação de Olá e pretender tooexplore-lo, vá para o mesmo!  Não pode ter toofollow estes passos slavishly.  

#### <a name="threats"></a>Ameaças
Olá quatro principais elementos de um modelo de ameaça são:

* Os processos (serviços web, os serviços de Win32, * nix daemons, etc. Tenha em atenção que podem ser abstracted algumas entidades complexas (por exemplo, os gateways de campo e sensores) como um processo quando um técnico desagregação nas seguintes áreas não é possível.
* Armazena os dados (em qualquer lugar os dados são armazenados, tal como um ficheiro de configuração ou a base de dados)
* Fluxo de dados (onde dados movem-se entre a outros elementos na aplicação Olá)
* As entidades externas (tudo o que interage com o sistema de Olá, mas não estiver sob controlo Olá da aplicação Olá, os exemplos incluem os utilizadores e satélite feeds)

Todos os elementos de diagrama da arquitetura de Olá são ameaças de toovarious requerente; Utilizaremos mnemónica de ser exigido STRIDE Olá. Leitura [Threat Modeling novamente, STRIDE](https://blogs.msdn.microsoft.com/larryosterman/2007/09/04/threat-modeling-again-stride/) tooknow mais sobre elementos STRIDE Olá.

Diferentes elementos de diagrama de aplicação Olá são ameaças do requerente toocertain STRIDE:

* Os processos são tooSTRIDE do requerente
* Fluxos de dados são tooTID do requerente
* Arquivos de dados são tooTID do requerente e, por vezes, R, se os arquivos de dados de Olá são ficheiros de registo.
* As entidades externas são tooSRD do requerente

## <a name="security-in-iot"></a>Segurança de IoT
Dispositivos com objetivos especiais ligados tem um número significativo de potenciais áreas de interação superfície e padrões de interação, todos os de que tem de ser considerados tooprovide uma arquitetura para proteger o acesso digital toothose dispositivos. o termo de Olá "acesso digital" é utilizado toodistinguish aqui de quaisquer operações que são executadas através da interação do dispositivo direta onde a segurança de acesso é fornecida através de controlo de acesso físico. Por exemplo, colocar o dispositivo Olá para uma sala de um bloqueio na porta Olá. Enquanto o acesso físico não pode ser negado utilizando o software e hardware, medidas podem ser tomadas tooprevent acesso físico da esquerda toosystem interferências. 

Como podemos explorar padrões de interação Olá, veremos "controlo de dispositivo" e "dados de dispositivo" com Olá mesmo nível de atenção. "Controlo de dispositivo" pode ser classificado como todas as informações que são fornecidas tooa dispositivo por quaisquer terceiros com o objetivo de Olá de alterar ou que influencia as respetivo comportamento para o respetivo estado ou Olá do seu ambiente. "Dados de dispositivo" podem ser classificados como quaisquer informações que um dispositivo emite tooany outro interveniente sobre o estado e Olá observado o estado do respetivo ambiente.

Na ordem toooptimize melhores práticas de segurança, recomenda-se que uma arquitetura IoT típica ser divididos em vários componentes/zonas como parte do exercício de modelação de ameaça de Olá. Estes zonas descritas totalmente em toda esta secção e incluem:

* Dispositivo,
* Gateway de campo
* Gateways, de nuvem e
* Serviços.

Zonas estão abrangentes toosegment de forma uma solução; cada zona tem muitas vezes, os seus próprios requisitos de dados e a autenticação e autorização. Zonas também podem ser utilizado tooisolation prejudicar e restringir o impacto de Olá das zonas de fidedignidade baixa em zonas de confiança superiores.

Cada zona é separada por um limite de fidedignidade, que é apresentado como Olá separada por pontos vermelha linha no diagrama de Olá abaixo. Representa uma transição de dados/informações a partir de uma origem tooanother. Durante esta transição, informações e dados Olá pode ser requerente tooSpoofing, violação, rejeição, divulgação de informações, Denial of Service e elevação de privilégio (STRIDE).

![Zonas de segurança de IoT](media/iot-security-architecture/iot-security-architecture-fig1.png) 

Olá componentes representados dentro de cada limite também estão sujeitos tooSTRIDE, ativar uma 360 completa vista da solução de Olá de modelação de ameaça. secções Olá abaixo elaboradasm em cada um dos componentes de Olá e preocupações de segurança específicos e soluções que devem ser colocadas no local.

as secções de Olá que se segue abordar componentes padrão a geralmente encontrados destas zonas.

### <a name="hello-device-zone"></a>Olá zona de dispositivo
Olá ambiente dispositivo espaço Olá imediata físico em torno do dispositivo olá onde o acesso físico e/ou digital ponto-a-ponto de "rede local" aceder toohello dispositivo for viável. Um "da rede local", é assumida toobe uma rede que é distinto e insulated de – mas potencialmente com bridge Internet pública demasiado – Olá e inclui qualquer tecnologia de botões de opção sem fios short-range que permite a comunicação de ponto-a-ponto dos dispositivos. Faz *não* incluem quaisquer tecnologia de Virtualização de rede criar ilusão de Olá de uma rede local e também não incluir redes de operador público que necessitam de qualquer toocommunicate dois dispositivos em espaço de rede pública se estivessem relação de comunicação tooenter um ponto-a-ponto.

### <a name="hello-field-gateway-zone"></a>Olá zona de Gateway de campo
Gateway de campo é uma aplicação/dispositivo ou algum software de computador do servidor para fins gerais que age como ativador de comunicação e, potencialmente, como um sistema de controlo do dispositivo e o hub de processamento de dados do dispositivo. zona de gateway de campo Olá inclui Olá campo próprio gateway e todos os dispositivos que estão anexados tooit. Como Olá nome indica, gateways de campo agir de processamento de dados dedicado fora das instalações, são normalmente localização vinculado, é potencialmente intrusões toophysical de assunto e será limitada redundância operacional. Todos os toosay que um gateway de campo é normalmente uma coisa um pode touch e sabotage sabendo que a sua função é. 

Um gateway de campo é diferente de um router de tráfego mere em que tenha tido uma função ativa na gestão de acesso e fluxo de informações, que significa que é uma aplicação resolvido ligação de rede e de entidade ou sessão de terminal. Um dispositivo NAT ou uma firewall, por outro lado, não se qualificam como gateways de campo, uma vez que não são ligação explícita ou terminals de sessão, mas em vez de um ligações rota (ou bloco) ou sessões efetuadas através de-los. gateway de campo Olá tem duas áreas superfície distintas. Um enfrenta dispositivos Olá que estão anexado tooit e representa Olá dentro de zona Olá e Olá outro enfrenta todas as entidades externas e Olá contorno da zona de Olá.   

### <a name="hello-cloud-gateway-zone"></a>zona de gateway de nuvem Olá
Gateway de nuvem é um sistema que permite a comunicação remota do e gateways toodevices ou o campo de vários sites diferentes em espaço de rede pública, normalmente, para um baseado na nuvem controlo e dados de Analysis Services sistema, Federação destes sistemas. Em alguns casos, um gateway de nuvem imediatamente poderá facilitar acesso toospecial finalidade dispositivos terminals como tablets ou telemóveis. No contexto de Olá abordado aqui, "nuvem" destina-se toorefer tooa dedicado sistema de processamento de dados que não se encontra vinculada toohello Olá anexado dispositivos ou gateways de campo do mesmo site. Também uma zona de nuvem, medidas operacionais impedem o acesso físico de destino em não é necessariamente expostas tooa infraestrutura de "nuvem pública".  

Um gateway de nuvem, potencialmente, pode ser mapeado para um rede sobreposição tooinsulate Olá nuvem gateway de Virtualização de e para todos os respetivos dispositivos ligados ou gateways de campo de qualquer outro tráfego de rede. Olá nuvem próprio gateway é nem um sistema de controlo de dispositivos nem um processamento ou um local de armazenamento para dados de dispositivo as instalações de interface com o gateway de nuvem Olá. zona de gateway de nuvem Olá inclui Olá gateway de nuvem própria juntamente com todos os gateways de campo e dispositivos direta ou indiretamente ligadas tooit. limite de Olá da zona de Olá é uma área de superfície distinta em que todas as entidades externas comunicam através de.

### <a name="hello-services-zone"></a>zona de serviços de Olá
"Serviço" está definido para este contexto como qualquer componente de software ou o módulo é interfacing com dispositivos através de um gateway de campo ou na nuvem para recolha de dados e análise, bem como para o comando e controlo.  Os serviços são mediators. Se agirem em sua identidade para gateways e outros subsistemas, armazenam e analisam dados, forma autónoma problema comandos toodevices com base nas informações de dados ou de agendas e expor informações e controlo capacidades tooauthorized os utilizadores finais.

### <a name="information-devices-vs-special-purpose-devices"></a>Dispositivos de informações vs dispositivos com objetivos especiais
PCs, telemóveis e tablets são principalmente os dispositivos de informações interativo. Telemóveis e tablets explicitamente estão otimizados em torno maximizando a duração da bateria. São, de preferência desativar parcialmente quando não imediatamente a interagir com uma pessoa ou quando não fornecer serviços como o reprodução de música ou ao servir pelos respetivos proprietário tooa determinado local. Numa perspetiva de sistemas, estes dispositivos de tecnologia de informações principalmente atuam como proxies para as pessoas. São "actuators pessoas" sugerindo ações e "sensores de pessoas" recolha de entrada. 

Dispositivos com objetivos especiais, de linhas produção fábrica de toocomplex de sensores de temperatura simples com milhares de componentes dentro deles, são diferentes. Estes dispositivos estão abrangidas pelo âmbito muito mais no objetivo e mesmo que fornecem algumas interface de utilizador, são amplamente âmbito toointerfacing com ou ser integradas nos recursos de Olá mundo físico. Estes medem e comunicam circunstâncias ambientais, ative valves, controlam servos, alarmes de som, mudar lights e realizar muitas outras tarefas. Ajudam toodo funciona para os quais um dispositivo de informações é demasiado genérico, demasiado caro, demasiado grande ou demasiado brittle. objetivo concreto Olá dita imediatamente respetiva estrutura técnica como disponíveis atribuição monetário Olá bem de produção e de operação agendada duração. combinação de Olá destes dois fatores chaves restringe Olá operacional atribuição de energia, os requisitos de espaço físico e, consequentemente, disponível armazenamento, computação disponíveis e as capacidades de segurança.  

Se algo "ficar errado" dispositivos controllable automatizada ou remoto, por exemplo, defeitos físicos ou controlo lógica defeitos toowillful não autorizado intrusões e manipulação. Muitas de produção Olá poderão ser destruídas, edifícios podem estar looted ou gravados para baixo e pessoas poderão die injured ou até mesmo. Isto é, obviamente, uma classe todo diferente de danos que alguém maxing fora do limite de um cartão crédito roubado. Olá barra de segurança para dispositivos que tornam coisas mover e também para dados de sensores que eventualmente resultados nos comandos que causam toomove coisas, tem de ser superior em qualquer cenário de banca de comércio eletrónico ou. 

### <a name="device-control-and-device-data-interactions"></a>Controlo de dispositivo e as interações de dados do dispositivo
Dispositivos com objetivos especiais ligados tem um número significativo de potenciais áreas de interação superfície e padrões de interação, todos os de que tem de ser considerados tooprovide uma arquitetura para proteger o acesso digital toothose dispositivos. o termo de Olá "acesso digital" é utilizado toodistinguish aqui de quaisquer operações que são executadas através da interação do dispositivo direta onde a segurança de acesso é fornecida através de controlo de acesso físico. Por exemplo, colocar o dispositivo Olá para uma sala de um bloqueio na porta Olá. Enquanto o acesso físico não pode ser negado utilizando o software e hardware, medidas podem ser tomadas tooprevent acesso físico da esquerda toosystem interferências. 

Como podemos explorar padrões de interação Olá, veremos "controlo de dispositivo" e "dados de dispositivo" com Olá mesmo nível de atenção ao modelação de ameaça. "Controlo de dispositivo" pode ser classificado como todas as informações que são fornecidas tooa dispositivo por quaisquer terceiros com o objetivo de Olá de alterar ou que influencia as respetivo comportamento para o respetivo estado ou Olá do seu ambiente. "Dados de dispositivo" podem ser classificados como quaisquer informações que um dispositivo emite tooany outro interveniente sobre o estado e Olá observado o estado do respetivo ambiente. 

## <a name="threat-modeling-hello-azure-iot-reference-architecture"></a>Arquitetura de referência do IoT do Azure Olá de modelação de ameaça
A Microsoft utiliza framework Olá descrito acima ameaça toodo modelling para o Azure IoT. Secção de Olá abaixo, por conseguinte, utilizamos exemplo concreto Olá toodemonstrate de arquitetura de referência do IoT do Azure como toothink sobre ameaças modelling para IoT e como tooaddress Olá ameaças identificado. No nosso caso, identificámos quatro áreas principais do foco:

* Dispositivos e as origens de dados
* Transporte de dados
* Dispositivo e o processamento de eventos, e
* Apresentação

![Para o Azure IoT de modelação de ameaça](media/iot-security-architecture/iot-security-architecture-fig2.png) 

Diagrama de Olá abaixo fornece uma visão simplificada da Microsoft arquitetura do IoT através de um modelo de diagrama de fluxo de dados que é utilizado pelo Olá ferramenta de modelação de ameaça do Microsoft:

![IoT do Azure utilizando a ferramenta de modelação de ameaça do MS de modelação de ameaça](media/iot-security-architecture/iot-security-architecture-fig3.png)

É importante toonote Olá arquitetura separa as capacidades do dispositivo e o gateway do Olá. Isto permite que a dispositivos de gateway que são mais seguros de Olá utilizador tooleverage: são capazes de comunicar com o gateway de nuvem de Olá utiliza protocolos segurados, que requer, normalmente, o processamento superior dos custos gerais que um dispositivo nativo - por exemplo, um thermostat - foi Forneça no seu próprio. Na zona de serviços do Azure Olá, presumimos que Olá que gateway de nuvem é representado por Olá serviço IoT Hub do Azure.

### <a name="device-and-data-sourcesdata-transport"></a>Origens/dados de dispositivos e dados de transporte
Esta secção explicar arquitetura Olá descrita acima, através da lente Olá de modelação de ameaça e fornece uma descrição geral de como podemos envolvido algumas das preocupações inerente Olá. Iremos focar-em elementos de core Olá de um modelo de ameaça:

* Processos (as nossos controlo e a itens externas)
* Comunicação (também denominada de fluxos de dados)
* Armazenamento (também denominado arquivos de dados)

#### <a name="processes"></a>Processos
Em cada uma das categorias de Olá descritas em Olá arquitetura do IoT do Azure, vamos tentar toomitigate existe um número de ameaças diferentes em dados de diferentes fases Olá, as informações no: processo, a comunicação e o armazenamento. Abaixo que lhe damos uma descrição geral de Olá aqueles mais comuns para a categoria de "processo" Olá, seguido de uma descrição geral de como estas foi ser melhor mitigadas: 

**(S) de spoofing**: um atacante poderá extrair material de chaves criptográfica a partir de um dispositivo, ao nível de software ou hardware Olá e, subsequentemente, aceder ao sistema Olá com um dispositivo físico ou virtual diferente na identidade de Olá de Olá de dispositivo Olá já foi tomado material de chaves do. Uma boa ilustração é remoto controlos que pode ativar qualquer TV e que estejam ferramentas prankster populares.

**Recusa de serviço (D)**: um dispositivo pode ser composto incapacidade de funcionar ou comunicar por interferir com frequências de botões de opção ou cablagem corte. Por exemplo, uma câmaras de vigilância que tinha a ligação de rede ou de energia intencionalmente knocked não comunicarão dados, de todo.

**Adulteração (T)**: detida ou parcialmente um atacante poderá substituir software Olá em execução no dispositivo Olá, potencialmente, permitindo Olá substituído software tooleverage Olá genuíno identidade de dispositivo Olá se hello material de chave ou Olá criptográfico instalações que contém a chaves materiais foram programa ilícito toohello disponíveis. Por exemplo, um atacante pode tirar partido de extraídos toointercept materiais chave e suprimir os dados do dispositivo de Olá no caminho de comunicação de Olá e substituí-lo com dados falsos, que são autenticados com material de chaves Olá roubado.

**Divulgação de informações (I)**: se o dispositivo de Olá executar software manipulado, esse software manipulated potencialmente foi fuga partes de toounauthorized de dados. Por exemplo, um atacante pode tirar partido extraído chave materiais tooinject próprio no caminho de comunicação de Olá entre o dispositivo Olá e um gateway de campo ou controlador ou na nuvem gateway toosiphon desativar informações.

**Elevação de privilégio (E)**: o dispositivo que suporta a função específica pode ser forçada toodo algo pessoa. Por exemplo, um valve que é tooopen programados e metade forma possível induzidos tooopen todas Olá forma.

| **Componente** | **Ameaças** | **Atenuação** | **Risco** | **Implementação** |
| --- | --- | --- | --- | --- |
| Dispositivo |S |Atribuir dispositivos toohello de identidade e autenticação de dispositivo Olá |Substituir o dispositivo ou parte do dispositivo Olá com alguns outros dispositivos. Como é que podemos saber que estão a comunicar o dispositivo correto toohello? |Autenticar o dispositivo de Olá, com a segurança de camada de transporte (TLS) ou IPSec. Infraestrutura deve suportar a utilização de chave pré-partilhada (PSK) nesses dispositivos que não é possível processar a criptografia completa assimétrica. Tirar partido do Azure AD, [OAuth](http://www.rfc-editor.org/in-notes/internet-drafts/draft-ietf-ace-oauth-authz-01.txt) |
| TRID |Aplica o dispositivo de toohello tamperproof mecanismos por exemplo, tornando tooimpossible muito difícil tooextract chaves e outro material de criptografia do dispositivo Olá. |risco Olá é se alguém a adulteração é dispositivo Olá (interferências físicos). Como são, certifique-se, que o dispositivo não adulterado. |mitigação mais eficaz Olá é uma capacidade de module (TPM) de plataforma fidedignos que lhe permite armazenar chaves numa especial no chip circuitry, do qual Olá chaves não não possível ler, mas só podem ser utilizadas para operações de criptografia que utilizam a chave de Olá mas nunca divulgar chave Olá . Encriptação de memória do dispositivo Olá. Gestão de chaves para o dispositivo de Olá. Olá código de assinatura. | |
| I |Controlo de acesso do dispositivo hello a ter. Esquema de autorização. |Se o dispositivo de Olá permite para ações individuais toobe efetuada com base em comandos de uma origem externa, ou mesmo comprometido sensores, será permitido ataque Olá tooperform operações caso contrário, não está acessível. |Ter o esquema de autorização para o dispositivo de Olá | |
| Gateway de campo |S |Autenticar tooCloud de gateway de campo Olá Gateway (cert com base, PSK, a afirmação com base,..) |Se alguém pode falsificar Gateway de campo, em seguida,-lo pode apresentar-se automaticamente como qualquer dispositivo. |TLS RSA/PSK, IPSec, [RFC 4279](https://tools.ietf.org/html/rfc4279). Todos os Olá mesmo armazenamento de chaves e preocupações de atestado de dispositivos no geral – caso melhor está a utilizar o TPM. Extensão de 6LowPAN para IPSec toosupport sem fios Sensor redes (WSN). |
| TRID |Proteger Olá Gateway de campo contra adulteração (TPM)? |O spoofing de ataques enganar o gateway de nuvem Olá pensar está a comunicar toofield gateway pode resultar em divulgação de informações e a adulteração de dados |Do memória encriptação, TPM, a autenticação. | |
| I |Mecanismo de controlo de acesso para o Gateway de campo | | | |

Seguem-se alguns exemplos de ameaças nesta categoria:

Spoofing: Um intruso poderá extrair material de chaves criptográfica de um dispositivo, ou ao nível de software ou hardware de Olá e, subsequentemente, o acesso foi sistema Olá com um dispositivo físico ou virtual diferente na identidade de Olá de material de chaves Olá dispositivo Olá é retirado do.

**Recusa de serviço**: um dispositivo pode ser composto incapacidade de funcionar ou comunicar por interferir com frequências de botões de opção ou cablagem corte. Por exemplo, uma câmaras de vigilância que tinha a ligação de rede ou de energia intencionalmente knocked não comunicarão dados, de todo.

**Adulteração**: detida ou parcialmente um atacante poderá substituir software Olá em execução no dispositivo Olá, potencialmente, permitindo Olá substituído software tooleverage Olá genuíno identidade de dispositivo Olá se hello material de chave ou Olá criptográfico instalações que contém a chaves materiais foram programa ilícito toohello disponíveis.

**Adulteração**: uma câmaras de vigilância que está a ser mostrada uma fotografia espetro visível um hallway vazio foi diversificada de uma fotografia de um hallway deste tipo. Um sensor smoke ou fire foi reporting alguém que contém um mais ligeira sob a mesma. Em ambos os casos, Olá o dispositivo pode estar tecnicamente totalmente fidedigno para o sistema de Olá, mas irá reportar manipular informações.

**Adulteração**: um atacante pode tirar partido de extraídos toointercept materiais chave e suprimir os dados do dispositivo de Olá no caminho de comunicação de Olá e substituí-lo com dados falsos, que são autenticados com material de chaves Olá roubado.

**Adulteração**: completamente ou parcialmente um atacante poderá substituir software Olá em execução no dispositivo Olá, potencialmente, permitindo Olá substituído software tooleverage Olá genuíno identidade de dispositivo Olá se hello material de chave ou Olá criptográfico instalações que contém a chaves materiais foram programa ilícito toohello disponíveis.

**Divulgação de informações**: se o dispositivo de Olá executar software manipulado, esse software manipulated potencialmente foi fuga partes de toounauthorized de dados.

**Divulgação de informações**: um atacante pode tirar partido extraído chave materiais tooinject próprio no caminho de comunicação de Olá entre o dispositivo Olá e um gateway de campo ou controlador ou na nuvem gateway toosiphon desativar informações.

**Recusa de serviço**: dispositivo Olá pode ser desativado ou ativado num modo em que a comunicação não é possível (que é intencional no número de máquinas industriais).

**Adulteração**: dispositivo Olá pode ser reconfigurada toooperate num Estado desconhecido toohello controlar system (fora parâmetros calibration conhecidos) e, por conseguinte, fornecer dados que podem ser mal interpretados

**Elevação de privilégios**: o dispositivo que suporta a função específica pode ser forçada toodo algo pessoa. Por exemplo, um valve que é tooopen programados e metade forma possível induzidos tooopen todas Olá forma.

**Recusa de serviço**: dispositivo Olá pode ser ativado num Estado em que a comunicação não seja possível.

**Adulteração**: dispositivo Olá pode ser reconfigurada toooperate num Estado desconhecido toohello controlar system (fora parâmetros calibration conhecidos) e, por conseguinte, fornecer dados que podem ser mal interpretados.

**Spoofing/violação/rejeição**: Se não estão protegidos (que raramente é caso Olá com controlos de remoto de consumidor) um atacante pode manipular Estado Olá de um dispositivo de forma anónima. Uma boa ilustração é remoto controlos que pode ativar qualquer TV e que estejam ferramentas prankster populares.

#### <a name="communication"></a>Comunicação
Ameaças à volta do caminho de comunicação entre dispositivos, dispositivos e gateways de campo e gateway de nuvem e de dispositivos. tabela de Olá abaixo tem algumas orientações à volta de sockets abra Olá dispositivos/VPN:

| **Componente** | **Ameaças** | **Atenuação** | **Risco** | **Implementação** |
| --- | --- | --- | --- | --- |
| Dispositivo IoT Hub |TID |(D) Tráfego de Olá de tooencrypt TLS (PSK/RSA) |Escutas ou interferir comunicação Olá entre o dispositivo de Olá e gateway de Olá |Segurança no nível de protocolo de Olá. Com protocolos personalizados, precisamos toofigure como tooprotect-los. Na maioria dos casos, a comunicação de Olá ocorre de Olá dispositivo toohello IoT Hub (dispositivo inicia a ligação de Olá). |
| Dispositivo do dispositivo |TID |(D) Tráfego de Olá tooencrypt TLS (PSK/RSA). |Leitura de dados em trânsito entre dispositivos. Adulteração dos dados de Olá. A sobrecarga de dispositivo Olá com novas ligações |Segurança no nível de protocolo de Olá (MQTT/AMQP/HTTP/CoAP. Com protocolos personalizados, precisamos toofigure como tooprotect-los. mitigação de Olá para Olá ameaça DoS é toopeer dispositivos através de um gateway de nuvem ou campo e possuam act apenas como clientes para a rede de Olá. Olá peering pode resultar numa ligação direta entre elementos de Olá após ter sido mediadas pelo gateway de Olá |
| Dispositivo de entidade externa |TID |O emparelhamento segura de dispositivos de toohello Olá entidade externa |Espionagem Olá ligação toohello o dispositivo. Comunicação de Olá interferir com dispositivo Olá |O emparelhamento com segurança do dispositivo de toohello Olá entidade externa LE NFC/Bluetooth. Controlar o painel de operacional Olá do dispositivo Olá (físico) |
| Gateway de nuvem do Gateway de campo |TID |Tráfego de Olá tooencrypt TLS (PSK/RSA). |Escutas ou interferir comunicação Olá entre o dispositivo de Olá e gateway de Olá |Segurança no nível de protocolo de Olá (MQTT/AMQP/HTTP/CoAP). Com protocolos personalizados, precisamos toofigure como tooprotect-los. |
| Gateway de nuvem do dispositivo |TID |Tráfego de Olá tooencrypt TLS (PSK/RSA). |Escutas ou interferir comunicação Olá entre o dispositivo de Olá e gateway de Olá |Segurança no nível de protocolo de Olá (MQTT/AMQP/HTTP/CoAP). Com protocolos personalizados, precisamos toofigure como tooprotect-los. |

Seguem-se alguns exemplos de ameaças nesta categoria:

**Recusa de serviço**: restrita dispositivos são, geralmente, em ameaça DoS quando estes ativamente escutam ligações de entrada ou não solicitados datagramas numa rede, porque um atacante pode abrir várias ligações em paralelo e não-los de serviço ou de serviço -los muito lentamente ou hello dispositivo pode ser flooded com tráfego não solicitado. Em ambos os casos, o dispositivo de Olá eficazmente pode ser composto inoperáveis na rede de Olá.

**Spoofing, divulgação de informações**: dispositivos restrita e dispositivos com objetivos especiais tem muitas vezes, instalações de segurança de um-para-all como palavra-passe ou proteção de PIN ou detida dependem do fidedigna rede Olá, o que significa que irão conceder acesso tooinformation quando um dispositivo estiver numa Olá mesma rede e essa rede muitas vezes, só está protegido por uma chave partilhada. Que significa que quando Olá partilhado toodevice secreta ou rede das é divulgada, é possível toocontrol Olá dispositivo existe ou observar os dados emitidos a partir do dispositivo Olá.  

**Spoofing**: um intruso poderá intercetar ou parcialmente substituir Olá difusão e spoof Olá originador (man no meio de Olá)

**Adulteração**: um intruso poderá intercetar ou parcialmente substituir Olá difusão e enviar informações falsas 

**Divulgação de informações:** um atacante pode eavesdrop na difusão e obter informações sem autorização **Denial of Service:** um atacante pode encravado Olá broadcast sinal e distribuição de informações de negação

#### <a name="storage"></a>Armazenamento
Todos os gateway de dispositivo e o campo tem alguma forma de armazenamento (temporário para colocação Olá dados de armazenamento de imagem do sistema operativo (SO)).

| **Componente** | **Ameaças** | **Atenuação** | **Risco** | **Implementação** |
| --- | --- | --- | --- | --- |
| Dispositivo de armazenamento |TRID |Encriptação de armazenamento, Olá registos de assinatura |Ler dados a partir do armazenamento de Olá (dados PII), adulteração dos dados de telemetria. Adulteração colocados em fila ou colocada em cache os dados de controlo de comando. Adulteração dos pacotes de atualização de firmware ou de configuração ao colocar em cache ou colocada em fila localmente pode levar componentes tooOS e/ou sistema que está a ser comprometidos |Encriptação, o código de autenticação de mensagem (MAC) ou a assinatura digital. Em que o controlo de acesso segura possível através de acesso a recursos controlar listas (ACLs) ou permissões. |
| Imagem de SO do dispositivo |TRID | |Adulteração com um SO / substituir componentes Olá SO |Partição de SO só de leitura, iniciada a imagem do SO, encriptação |
| Armazenamento de Gateway de campo (colocação Olá dados) |TRID |Encriptação de armazenamento, Olá registos de assinatura |Leitura de dados do armazenamento de Olá (dados PII), a adulteração dos dados de telemetria, adulteração colocados em fila ou colocada em cache os dados de controlo de comando. Adulteração dos pacotes de atualização de firmware ou de configuração (destinados a dispositivos ou gateway de campo) ao colocar em cache ou colocada em fila localmente pode levar componentes tooOS e/ou sistema que está a ser comprometidos |BitLocker |
| Imagem do SO do Gateway de campo |TRID | |Adulteração com um SO / substituir componentes Olá SO |Partição de SO só de leitura, iniciada a imagem do SO, encriptação |

### <a name="device-and-event-processingcloud-gateway-zone"></a>Zona de gateway de processamento/nuvem e eventos de dispositivos
Um gateway de nuvem é sistema que permite a comunicação remota do e gateways toodevices ou o campo de vários sites diferentes em espaço de rede pública, normalmente, para um baseado na nuvem controlo e dados de Analysis Services sistema, Federação destes sistemas. Em alguns casos, um gateway de nuvem imediatamente poderá facilitar acesso toospecial finalidade dispositivos terminals como tablets ou telemóveis. No contexto de Olá abordado aqui, "nuvem" destina-se toorefer tooa dedicada de sistema de processamento de dados que não se encontra vinculada toohello do mesmo site Olá anexado dispositivos ou gateways de campo e, em que medidas operacionais impedem direcionados acesso físico, mas não é necessariamente infraestrutura de "nuvem pública" tooa.  Um gateway de nuvem, potencialmente, pode ser mapeado para um rede sobreposição tooinsulate Olá nuvem gateway de Virtualização de e para todos os respetivos dispositivos ligados ou gateways de campo de qualquer outro tráfego de rede. Olá nuvem próprio gateway é nem um sistema de controlo de dispositivos nem um processamento ou um local de armazenamento para dados de dispositivo as instalações de interface com o gateway de nuvem Olá. zona de gateway de nuvem Olá inclui Olá gateway de nuvem própria juntamente com todos os gateways de campo e dispositivos direta ou indiretamente ligadas tooit.

Gateway de nuvem é principalmente peça incorporada personalizada de software em execução como um serviço com o gateway de campo toowhich expostas pontos finais e os dispositivos ligados. Como tal, têm de ser concebido com segurança em mente. Siga [SDL](http://www.microsoft.com/sdl) processos para estruturação e criação deste serviço. 

#### <a name="services-zone"></a>Zona de serviços
Um sistema de controlo (ou controlador) é uma solução de software que interaja com um dispositivo, ou um gateway de campo ou o gateway de nuvem para efeitos de Olá de controlar um ou vários dispositivos e/ou toocollect e/ou arquivo de e/ou analisar dados de dispositivo para a apresentação, ou efeitos de controlo subsequentes. Sistemas de controlo são entidades de apenas Olá no âmbito de Olá deste debate que imediatamente pode facilitar a interação com pessoas. Exceção de Olá são intermédia analisa controlo física em dispositivos, como um comutador que permite que uma pessoa tooturn Olá dispositivo desligar ou alterar outras propriedades, e para o qual não existe nenhum equivalente funcional que pode ser acedido digitalmente. 

Intermédia analisa controlo físicas são aquelas em que qualquer ordenação dos que rege lógica restringe função Olá da Olá físico superfície de controlo de forma a que uma função equivalente pode ser iniciada remotamente ou conflitos de entrada com entrada remoto podem ser evitadas – este tipo intermediated controlo analisa são sistema de controlo local tooa anexado, essencialmente, que tira partido Olá a mesma funcionalidade subjacente como qualquer outro sistema de controlo remoto Olá dispositivo pode ser anexado tooin paralela. Principais ameaças toohello informática em nuvem pode ser lido no [Alliance de segurança de nuvem (CSA)](https://cloudsecurityalliance.org/research/top-threats/) página.

## <a name="additional-resources"></a>Recursos adicionais
Consulte toohello seguintes artigos para obter informações adicionais:

* [Ferramenta de modelação de ameaça do SDL](https://www.microsoft.com/sdl/adopt/threatmodeling.aspx)
* [Arquitetura de referência do IoT do Microsoft Azure](https://azure.microsoft.com/updates/microsoft-azure-iot-reference-architecture-available/)

