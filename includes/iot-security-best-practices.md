# <a name="internet-of-things-security-best-practices"></a>Práticas recomendadas de segurança de Internet das coisas

Proteger uma infraestrutura de Internet das coisas (IoT) requer uma estratégia de segurança-na profundidade rigorosas. Esta estratégia requer a proteger os dados na nuvem, proteger a integridade dos dados em trânsito através da internet pública e em segurança aprovisionar dispositivos. Cada camada baseia-se a garantia de segurança superior na infraestrutura global.

## <a name="secure-an-iot-infrastructure"></a>Proteger uma infraestrutura de IoT

Esta estratégia de segurança-na profundidade pode ser desenvolvida e executada com o Active Directory participação de vários jogadores envolvidos no fabrico, desenvolvimento e implementação de infraestrutura e de dispositivos de IoT. Segue-se uma descrição de alto nível destes jogadores.

* **Fabricante de hardware de IoT/integrador**: normalmente, estes jogadores são fabricantes de hardware de IoT que está a ser implementado, integradores reuni hardware a partir de vários fabricantes ou fornecedores de hardware a fornecer para uma implementação de IoT fabricado ou integrado por outros fornecedores.
* **Para programadores de solução IoT**: O desenvolvimento de uma solução de IoT é geralmente feito por um programador de solução. Este programador pode faz parte de uma equipa interna ou integrador de sistema (TAMA) especificar melhor nesta atividade. O Programador de solução IoT pode desenvolver vários componentes da solução IoT a partir do zero, integrar vários componentes off-the-shelf ou open source ou adotar soluções pré-configuradas com adaptation secundária.
* **Implementador de solução IoT**: depois de um IoT solução for desenvolvida, tem de ser implementado no campo. Este processo envolve a implementação de hardware, interconnection de dispositivos e a implementação de soluções em dispositivos de hardware ou a nuvem.
* **Operador de solução IoT**: depois de IoT solução for implementada, necessita de operações de longa duração, monitorização, atualizações e manutenção. Estas tarefas podem ser realizadas por uma equipa interna que compreende especialistas de tecnologia de informação, operações de hardware e as equipas de manutenção e especialistas de domínio que monitorizar o comportamento correto de infraestrutura geral do IoT.

As secções que se seguem fornecem as melhores práticas para cada um destes jogadores para ajudar a desenvolver, implementar e operar uma infraestrutura de IoT segura.

## <a name="iot-hardware-manufacturerintegrator"></a>Fabricante de hardware de IoT/integrador

Seguem-se as melhores práticas para os fabricantes de hardware de IoT e integradores de hardware.

* **Definir o âmbito de hardware para os requisitos mínimos**: A estrutura de hardware deve incluir as funcionalidades mínimas necessárias para a operação de hardware e nada mais. Um exemplo é para incluir a portas USB apenas se for necessário para a operação do dispositivo. Estas funcionalidades adicionais abrir o dispositivo para vetores de ataque indesejável que devem ser evitados.
* **Efetuar uma prova de adulteração de hardware**: criar no mecanismos para detetar a adulteração física, tais como abrir de abrange o dispositivo ou remover uma parte do dispositivo. Estes adulteração sinais pode fazer parte do fluxo de dados carregado para a nuvem, o que foi operadores destes eventos de alertas.
* **Criar em torno de hardware seguro**: COGS se permite, compilar funcionalidades de segurança, como o armazenamento segura e encriptada ou funcionalidade com base no Trusted Platform Module (TPM) de arranque. Estas funcionalidades tornam os dispositivos mais seguro e ajudam a proteger a infraestrutura geral do IoT.
* **Efetuar atualizações segura**: atualizações de Firmware durante o período de vida do dispositivo são inevitável. Criação de dispositivos com caminhos segurados para as atualizações e garantia criptográfica das versões de firmware irá permitir que o dispositivo ser seguro durante e após as atualizações.

## <a name="iot-solution-developer"></a>Para programadores de solução IoT

Seguem-se as melhores práticas para os programadores de solução IoT:

* **Siga a metodologia de desenvolvimento de software segura**: necessita de desenvolvimento de software segura zero pensar sobre a segurança, da inception do projeto para a implementação, teste e a implementação. As escolhas de plataformas, idiomas e as ferramentas são todos deve influenciadas com este metodologia. O ciclo de vida de desenvolvimento de segurança Microsoft fornece uma abordagem de passo a passo para criação de software segura.
* **Escolha o software open source com cuidado**: software Open source fornece uma oportunidade para rapidamente desenvolver soluções. Quando estiver a escolher software open source, considere o nível de atividade da Comunidade para cada componente de open source. Uma Comunidade de Active Directory assegura que o software é suportado e que os problemas são detetados e resolvidos. Em alternativa, poderá não ser suportado um projeto de software de open source obscura e inativa, e provavelmente não ser detetados problemas.
* **Integrar com cuidado**: Existem várias falhas de segurança de software, o limite de bibliotecas e APIs. Funcionalidade não poderá ser necessária para a implementação atual poderá estar ainda disponível através de uma camada de API. Para garantir a segurança geral, certifique-se todas as interfaces de componentes que está a ser integrados para falhas de segurança.

## <a name="iot-solution-deployer"></a>Implementador de solução IoT

Seguem-se as melhores práticas para os implementadores de solução IoT:

* **Implementar hardware de forma segura**: implementações de IoT podem necessitar de hardware para ser implementados em localizações não seguros, tais como espaços públicos ou regiões supervisionados. Estas situações, certifique-se de que a implementação de hardware é à prova na máxima extensão. Se o USB ou outras portas estão disponíveis no hardware, certifique-se de que estes são abordadas em segurança. Muitos vetores de ataque podem utilizá-los como pontos de entrada.
* **Manter as chaves de autenticação seguros**: durante a implementação, cada dispositivo requer IDs de dispositivo e chaves de autenticação geradas pelo serviço de nuvem associadas. Manter estas chaves fisicamente seguro, mesmo após a implementação. Qualquer tecla comprometida pode ser utilizada por um dispositivo malicioso para representação como um dispositivo existente.

## <a name="iot-solution-operator"></a>Operador de solução IoT

Seguem-se as melhores práticas para operadores de solução IoT:

* **Manter o sistema atualizados**: Certifique-se de que os sistemas operativos de dispositivos e todos os controladores de dispositivo são atualizados para as versões mais recentes. Se ativar as atualizações automáticas no Windows 10 (IoT ou outros SKUs), Microsoft mantém-atualizadas, fornecendo um sistema operativo seguro para dispositivos de IoT. Manter a outros sistemas operativos (por exemplo, o Linux) ajuda atualizadas Certifique-se de que também estão protegidos contra ataques maliciosos.
* **Proteger contra atividade maliciosa**: se permite que o sistema operativo, instale as capacidades de antivírus e antimalware mais recentes em cada sistema operativo do dispositivo. Esta prática pode ajudar a mitigar ameaças mais externas. Pode proteger os sistemas operativos mais modernos contra ameaças, efetuando os passos adequados.
* **Auditoria frequentemente**: auditoria IoT infraestrutura para problemas relacionados com a segurança é chave quando a responder a incidentes de segurança. A maioria dos sistemas de operativos fornecem o registo de eventos incorporado que deve ser revisto com frequência para se certificar de que não violação de segurança ocorreu. Informações de auditoria podem ser enviadas como um fluxo de telemetria separada para o serviço em nuvem em que pode ser analisado.
* **Fisicamente proteger a infraestrutura de IoT**: os pior ataques de segurança em relação a infraestrutura de IoT são iniciados utilizando o acesso físico aos dispositivos. É uma prática de segurança importante proteger contra utilização mal-intencionada de portas USB e outro acesso físico. Uma chave para falhas uncovering que poderá ter ocorrido é o registo de acesso físico, como a utilização de uma porta USB. Novamente, o Windows 10 (IoT e outros SKUs) ativa o registo detalhado destes eventos.
* **Proteger credenciais na nuvem**: credenciais de autenticação em nuvem utilizadas para configurar e utilizar uma implementação de IoT possivelmente são a forma mais fácil de obter acesso e comprometer um sistema de IoT. Proteger as credenciais ao alterar a palavra-passe com frequência e de não utilizar estas credenciais em máquinas públicas.

Capacidades de diferentes dispositivos de IoT variam. Alguns dispositivos podem ser computadores com sistemas operativos de ambiente de trabalho comuns e alguns dispositivos sistemas de operativos muito claro ponderação poderão estar em execução. Os procedimentos recomendados de segurança descritos anteriormente podem ser aplicáveis a dispositivos estas variando graus. Se for indicado, devem ser seguidas adicionais implementação melhores práticas de segurança e de fabricantes destes dispositivos.

Alguns dispositivos legados e restrita não poderão foi concebidos especificamente para a implementação de IoT. Estes dispositivos podem não têm a capacidade de encriptar dados, estabelecer ligação com a Internet ou fornecer de auditoria avançada. Nestes casos, um gateway de campo moderna e segura pode agregar dados a partir dos dispositivos legados e fornecer a segurança necessária para ligar estes dispositivos através da Internet. Gateways de campo podem fornecer autenticação segura, a negociação de sessões encriptadas, a receção de comandos a partir da nuvem e muitas outras funcionalidades de segurança.