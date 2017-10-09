
# <a name="azure-and-internet-of-things"></a>Azure e Internet das Coisas

Bem-vindo tooMicrosoft do Azure e Olá Internet das coisas (IoT). Este artigo apresenta uma arquitetura de solução IoT que descreve as características comuns de Olá de uma solução de IoT que poderá implementar com serviços do Azure. As soluções IoT exigem a proteger a comunicação bidirecional entre dispositivos, possivelmente numeração Olá milhões e um solução de back-end. Por exemplo, um solução de back-end poderá utilizar a Análise Preditiva automatizada toouncover insights a partir da sua sequência de eventos de dispositivo para a nuvem.

O Hub IoT do Azure é um bloco modular fundamental ao implementar esta arquitetura de solução de IoT com os serviços do Azure. O IoT Suite fornece implementações completas de ponta a ponta desta arquitetura para cenários de IoT específicos. Por exemplo:

* Olá *monitorização remota* solução permite-lhe toomonitor Olá estado de dispositivos como Distribuidores automáticos.
* Olá *manutenção preditiva* solução ajuda-o a tooanticipate necessidades de manutenção dos dispositivos como bombas em estações de bombagem remotas e tooavoid período de indisponibilidade.
* Olá *fábrica ligada* solução ajuda-o a tooconnect e monitorizar os seus dispositivos industriais.

## <a name="iot-solution-architecture"></a>Arquitetura da solução de IoT

Olá seguinte diagrama mostra uma arquitetura de solução IoT típica. Diagrama de Olá não inclui nomes de Olá de quaisquer serviços específicos do Azure, mas descreve Olá entre os principais elementos numa arquitetura de solução IoT genérica. Nesta arquitetura, os dispositivos IoT recolhem dados que enviam tooa gateway de nuvem. gateway de nuvem Olá disponibiliza dados Olá para processamento por outros serviços de back-end a partir de onde os dados são entregues tooother aplicações de linha de negócio ou operadores de toohuman através de um dashboard ou outro dispositivo de apresentação.

![Arquitetura da solução de IoT][img-solution-architecture]

> [!NOTE]
> Para um debate aprofundado da arquitetura do IoT, consulte Olá [arquitetura de referência do Microsoft Azure IoT][lnk-refarch].

### <a name="device-connectivity"></a>Conectividade dos dispositivos

Nesta arquitetura de solução IoT, os dispositivos enviam telemetria, tais como as leituras dos sensores de uma estação de bombagem, tooa ponto final da nuvem para armazenamento e processamento. Num cenário de manutenção preditiva, Olá solução de back-end poderá utilizar o fluxo de Olá de toodetermine de dados de sensor quando uma bomba específica precisa de manutenção. Dispositivos também podem receber e responder a mensagens toocloud para o dispositivo, lendo as mensagens a partir de um ponto final da nuvem. Por exemplo, numa solução de Olá de cenário de manutenção preditiva Olá back-end poderá enviar mensagens tooother bombas na Olá gerar toobegin estação redirecionamento fluxos imediatamente antes de manutenção toostart. Este procedimento seria Certifique-se de que o engenheiro de manutenção de Olá foi começar assim que chegar.

Uma das Olá maiores desafios que enfrentam os projetos IoT é como tooreliably e ligar dispositivos toohello solução de back-end de forma segura. Os dispositivos IoT têm características diferentes como tooother em comparação com clientes, como browsers e aplicações móveis. Dispositivos IoT:

* São frequentemente sistemas integrados sem nenhum operador humano.
* Podem ser implementados em localizações remotas, onde o acesso físico é dispendioso.
* Podem apenas ser acessíveis através de Olá solução de back-end. Não há outro toointeract de forma com dispositivo Olá.
* Podem recursos de processamento e um poder limitados.
* Podem ter uma conectividade de rede intermitente, lente ou dispendiosa.
* Poderá ter toouse protocolos de aplicação proprietários, personalizados ou específicos da indústria.
* Podem ser criados utilizando um grande conjunto de plataformas de hardware e software populares.

Além disso toohello os requisitos de acima, qualquer solução IoT tem também entregar o dimensionamento, segurança e fiabilidade. Olá conjunto resultante dos requisitos de conectividade é difícil e moroso tooimplement com tecnologias tradicionais, como contentores web e mediadores de mensagens. IoT Hub do Azure e Olá SDKs do dispositivo IoT do Azure tornam mais fácil soluções tooimplement que cumpram estes requisitos.

Um dispositivo pode comunicar diretamente com um ponto final de gateway de nuvem ou, se o dispositivo de Olá não é possível utilizar qualquer um dos protocolos de comunicações de Olá Olá suporta de gateway de nuvem, pode ligar através de um gateway intermédio. Por exemplo, Olá [gateway de protocolo do Azure IoT] [ lnk-protocol-gateway] pode efetuar a tradução de protocolos se dispositivos não é possível utilizar qualquer um dos protocolos Olá que suporta o IoT Hub.

### <a name="data-processing-and-analytics"></a>Processamento e análise dos dados

Na nuvem de Olá, uma solução back-end do IoT é onde Olá de processamento de dados ocorre a maior parte, como a filtragem e telemetria de agregação e encaminhamento tooother serviços. Olá solução back-end do IoT:

* Recebe a telemetria à escala dos seus dispositivos e determina como tooprocess e armazenar esses dados. 
* Pode permitir-lhe toosend comandos de Olá nuvem toospecific dispositivo.
* Fornece capacidades de registo de dispositivos que lhe permitem tooprovision dispositivos e toocontrol que dispositivos estão autorizados a tooconnect tooyour infraestrutura.
* Ativa tootrack Olá estado dos seus dispositivos e monitorizar as respetivas atividades.

No cenário de manutenção preventiva Olá, Olá solução de back-end armazena dados históricos de telemetria. Olá solução de back-end pode utilizar este padrões tooidentify toouse de dados que indicam manutenção numa bomba específica.

As soluções de IoT podem incluir ciclos de feedback automáticos. Por exemplo, um módulo de análise no Olá solução de back-end pode identificar de telemetria de temperatura Olá de um dispositivo específico está acima dos níveis de funcionamento normais. solução Olá, em seguida, pode enviar um dispositivo de toohello do comando, instruindo-tootake as medidas corretivas.

### <a name="presentation-and-business-connectivity"></a>Apresentação e conectividade empresarial

camada de conectividade de apresentação e o negócio Olá permite aos utilizadores finais, dispositivos de Olá e toointeract com Olá solução IoT. -Permite que os utilizadores tooview e analisar dados de Olá recolhidos a partir dos seus dispositivos. Estas vistas podem ter o formato de Olá de dashboards ou de relatórios do BI e podem apresentar dados históricos ou perto dados em tempo real. Por exemplo, um operador pode verificar estado de Olá da estação de bombagem específica e ver todos os alertas gerados pelo sistema Olá. Esta camada também permite a integração de Olá solução back-end do IoT com tootie de aplicações de linha de negócio existentes para processos de negócio empresariais ou fluxos de trabalho. Por exemplo, a solução de manutenção preditiva Olá pode integrar com um sistema de agendamento que books toovisit um engenheiro uma estação de bombagem quando a solução de Olá identifica uma bomba a precisar de manutenção.

![Dashboard da solução de IoT][img-dashboard]

[img-solution-architecture]: ./media/iot-azure-and-iot/iot-reference-architecture.png
[img-dashboard]: ./media/iot-azure-and-iot/iot-suite.png

[lnk-machinelearning]: http://azure.microsoft.com/documentation/services/machine-learning/
[Azure IoT Suite]: http://azure.microsoft.com/solutions/iot
[lnk-protocol-gateway]:  ../articles/iot-hub/iot-hub-protocol-gateway.md
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
