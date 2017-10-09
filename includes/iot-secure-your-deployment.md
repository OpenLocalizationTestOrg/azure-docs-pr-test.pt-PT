# <a name="secure-your-iot-deployment"></a>Proteger a sua implementação de IoT
Este artigo fornece patamares Olá de detalhe para proteger a infraestrutura do Olá baseado no Azure IoT Internet das coisas (IoT). Hiperligações-detalhes de nível de tooimplementation para configurar e implementar cada componente. Também fornece comparações e opções de entre vários métodos concorrentes.

Proteger a implementação do Azure IoT Olá pode ser dividido em Olá seguintes três áreas de segurança:

* **Segurança de dispositivos**: Proteger dispositivos de IoT Olá enquanto está implementada numa Olá universal.
* **Segurança de ligação**: garantir que todos os dados transmitidos entre dispositivos de IoT Olá e IoT Hub é confidencial e prova de adulteração.
* **Segurança de nuvem**: a fornecer um meio toosecure os dados enquanto se desloca pelas e são armazenado na nuvem de Olá.

![Três áreas de segurança][img-overview]

## <a name="secure-device-provisioning-and-authentication"></a>Proteger o aprovisionamento de dispositivos e autenticação
Olá, Azure IoT Suite protege os dispositivos de IoT por Olá seguintes dois métodos:

* Ao fornecer uma chave de identidade exclusiva (tokens de segurança) para cada dispositivo, o que pode ser utilizado por Olá dispositivo toocommunicate com Olá IoT Hub.
* Ao utilizar um dispositivo [certificado x. 509] [ lnk-x509] e a chave privada como um meio tooauthenticate Olá dispositivo toohello IoT Hub. Este método de autenticação garante que Olá chave privada no dispositivo Olá não é conhecido fora Olá dispositivo em qualquer altura, fornecer um nível mais elevado de segurança.

método de token de segurança de Olá fornece autenticação para cada chamada efetuada pelo Olá dispositivo tooIoT Hub ao associar a chamada de tooeach chave simétrica Olá. Autenticação baseada em x. 509 permite a autenticação de um dispositivo IoT na camada física de Olá como parte do estabelecimento de ligação do Olá TLS. método baseado em tokens de segurança de Olá pode ser utilizado sem a autenticação de x. 509 Olá, que é um padrão menos seguro. Olá escolha entre os métodos de Olá dois é principalmente ditada pelo Olá como protegem a autenticação do dispositivo precisa de toobe e disponibilidade de armazenamento segura no dispositivo Olá (toostore Olá chave privada com segurança).

## <a name="iot-hub-security-tokens"></a>Tokens de segurança do Hub IoT
IoT Hub utiliza segurança tokens tooauthenticate dispositivos e serviços tooavoid enviar chaves na rede de Olá. Além disso, tokens de segurança estão limitados a validade de tempo e o âmbito. Os SDKs IoT do Azure gerar automaticamente tokens sem necessidade de nenhuma configuração especial. No entanto, alguns cenários, requerem Olá utilizador toogenerate e utilizam tokens de segurança diretamente. Estes incluem a utilização direta do Olá de analisa MQTT, AMQP ou HTTP hello, ou a implementação de Olá padrão do serviço de tokens de Olá.

Obter mais detalhes sobre a estrutura de Olá do token de segurança de Olá e respetiva utilização podem ser encontrados na Olá seguintes artigos:

* [Estrutura de token de segurança][lnk-security-tokens]
* [Utilização de tokens SAS como um dispositivo][lnk-sas-tokens]

Cada IoT Hub tem um [registo de identidade] [ lnk-identity-registry] que podem ser utilizados toocreate por dispositivo recursos no serviço de Olá, tal como uma fila que contém mensagens da nuvem para o dispositivo em trânsito e tooallow acesso toohello pontos finais de orientado para o dispositivo. Olá registo de identidade do IoT Hub fornece armazenamento seguro de identidades de dispositivo e as chaves de segurança para uma solução. Individuais ou grupos de identidades de dispositivo podem ser adicionados tooan permitem lista ou uma lista de bloqueios, ativar o controlo total sobre o acesso ao dispositivo. Olá artigos que se seguem fornecem mais detalhes na estrutura de Olá de registo de identidade Olá e operações suportadas.

[IoT Hub suporta os protocolos, como MQTT, AMQP e HTTP][lnk-protocols]. Cada um destes protocolos de forma diferente, utilize tokens de segurança de tooIoT de dispositivo Olá IoT Hub:

* AMQP: SASL simples e baseada em afirmações AMQP segurança ({policyName}@sas.root. { iothubName} no caso de Olá dos tokens de nível do hub IoT; {"deviceId"} em caso de tokens no âmbito do dispositivo).
* MQTT: Ligar utiliza pacotes {"deviceId"} como Olá {ClientId}, {IoThubhostname} / {"deviceId"} no Olá **Username** token de campo e uma SAS no Olá **palavra-passe** campo.
* HTTP: Token válido está no cabeçalho de pedido de autorização de Olá.

Registo de identidade do IoT Hub pode ser as credenciais de segurança do tooconfigure utilizados por dispositivo e controlo de acesso. No entanto, se uma solução de IoT que já tem um investimento significativo num [esquema de registo e/ou a autenticação de identidade do dispositivo personalizada][lnk-custom-auth], podem ser integrados para uma infraestrutura existente com o IoT Hub através da criação de um serviço de tokens.

### <a name="x509-certificate-based-device-authentication"></a>Autenticação de dispositivos baseada em certificado x. 509
Olá, utilização de um [certificado baseado nos dispositivos de x. 509] [ lnk-use-x509] e respetivos associado pública e privada par de chaves permite a autenticação adicional na camada física Olá. chave privada Olá é armazenado em segurança no dispositivo Olá, não sendo detetável fora Olá dispositivo. certificado x. 509 de Olá contém informações sobre o dispositivo de Olá, tal como ID de dispositivo e outros detalhes organizacionais. Uma assinatura de certificado de Olá é gerada utilizando a chave privada Olá.

Fluxo de aprovisionamento de dispositivos de alto nível:

* Associar um dispositivo físico do identificador tooa – identidade de dispositivo e/ou os x. 509 do certificado dispositivo toohello associados durante o dispositivo de fabrico ou commissioning.
* Crie uma entrada correspondente de identidade do IoT Hub – identidade de dispositivo e informações de dispositivo associados no Olá registo de identidade do IoT Hub.
* Armazene de maneira segura o thumbprint do certificado x. 509 no registo de identidade do IoT Hub.

### <a name="root-certificate-on-device"></a>Certificado de raiz no dispositivo
Ao estabelecer uma ligação de TLS segura com o IoT Hub, dispositivos de IoT Olá autentica o IoT Hub com um certificado de raiz que faz parte do dispositivo Olá SDK. Para o cliente de Olá C SDK certificado Olá está localizado na pasta Olá "\\c\\certificados" na raiz de Olá do repositório de Olá. Embora estes certificados de raiz longa duração, ainda pode expirarem ou ser revogados. Se não existir nenhuma forma de atualizar o certificado de Olá no dispositivo Olá, hello dispositivo não conseguir ligar toosubsequently toohello IoT Hub (ou qualquer outro serviço de nuvem). Ter um certificado de raiz do meio tooupdate Olá depois de dispositivos de IoT Olá é implementado será eficazmente mitigar este risco.

## <a name="securing-hello-connection"></a>Proteger a ligação de Olá
Ligação à Internet entre dispositivos de IoT Olá e IoT Hub é protegida através de Olá Transport Layer Security (TLS) padrão. Azure IoT suporta [TLS 1.2][lnk-tls12], TLS 1.1 e TLS 1.0, esta ordem. Suporte para TLS 1.0 é fornecido para apenas a compatibilidade com versões anteriores. É recomendado toouse TLS 1.2, uma vez que fornece maior segurança Olá.

Azure IoT Suite suporta Olá os seguintes conjuntos de cifras, por esta ordem.

| Conjunto de cifras | comprimento |
| --- | --- |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA384 (0xc028) ECDH secp384r1 (eq. FS 7680 bits RSA) |256 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0xc027) ECDH secp256r1 (eq. FS 3072 bits RSA) |128 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA (0xc014) ECDH secp384r1 (eq. FS 7680 bits RSA) |256 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA (0xc013) ECDH secp256r1 (eq. FS 3072 bits RSA) |128 |
| TLS\_RSA\_WITH\_AES\_256\_GCM\_SHA384 (0x9d) |256 |
| TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256 (0x9c) |128 |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA256 (0x3d) |256 |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0x3c) |128 |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA (0x35) |256 |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA (0x2f) |128 |
| TLS\_RSA\_WITH\_3DES\_EDE\_CBC\_SHA (0xa) |112 |

## <a name="securing-hello-cloud"></a>Proteger a nuvem de Olá
IoT Hub do Azure permite a definição de [políticas de controlo de acesso] [ lnk-protocols] para cada chave de segurança. Utiliza Olá seguinte conjunto de permissões toogrant acesso tooeach de pontos finais do IoT Hub. Permissões limitam Olá acesso tooan que IOT Hub com base na funcionalidade.

* **RegistryRead**. Registo de identidade do concede acesso de leitura toohello. Para obter mais informações, consulte [registo de identidade][lnk-identity-registry].
* **RegistryReadWrite**. Concede acesso de escrita e leitura toohello registo de identidade. Para obter mais informações, consulte [registo de identidade][lnk-identity-registry].
* **ServiceConnect**. Concede acesso toocloud orientado para o serviço comunicação e os pontos finais de monitorização. Por exemplo, atribui acesso nuvem tooback-end de permissão mensagens do dispositivo para nuvem de tooreceive de serviços, enviar mensagens da nuvem para o dispositivo e obter Olá correspondente entrega em que as confirmações.
* **DeviceConnect**. Concede acesso pontos finais de toodevice orientada. Por exemplo, concede permissão de mensagens do dispositivo para a nuvem de toosend e receber mensagens da nuvem para o dispositivo. Esta permissão é utilizado pelos dispositivos.

Existem duas formas tooobtain **DeviceConnect** permissões com o IoT Hub com [tokens de segurança][lnk-sas-tokens]: utilizar uma chave de identidade de dispositivo, ou uma chave de acesso partilhado. Além disso, é importante toonote que todas as funcionalidades acessível a partir de dispositivos é exposta pela estrutura em pontos finais com o prefixo `/devices/{deviceId}`.

[Componentes do serviço só é possível gerar tokens de segurança] [ lnk-service-tokens] utilizar partilhado conceder as permissões adequadas Olá as políticas de acesso.

IoT Hub do Azure e outros serviços que podem ser parte da solução de Olá permitem a gestão de utilizadores utilizando Olá do Azure Active Directory.

Dados ingeridos pelo IoT Hub do Azure podem ser utilizados por uma variedade de serviços como o Azure Stream Analytics e armazenamento de Blobs do Azure. Estes serviços permitem o acesso de gestão. Leia mais sobre estes serviços e as opções disponíveis abaixo:

* [O Azure DocumentDB][lnk-docdb]: um serviço de base de dados dimensionável e totalmente indexado para dados semiestruturados que gere os metadados para dispositivos Olá aprovisionar, como atributos, configuração e propriedades de segurança. O DocumentDB oferece processamento elevado desempenho e débito elevado, o esquema agnóstico a indexação de dados e uma interface de consulta avançada do SQL Server.
* [O Azure Stream Analytics][lnk-asa]: fluxo em tempo real de processamento na nuvem de Olá que permite toorapidly desenvolver e implementar uma análise de baixo custo solução toouncover em tempo real das informações dos dispositivos, sensores, infraestrutura e aplicações. dados Olá deste serviço completamente gerido podem dimensionar o volume de tooany um débito elevado, latência baixa e resiliência.
* [Serviços de aplicações do Azure][lnk-appservices]: uma cloud platform toobuild poderosas web apps e móveis que se ligam toodata em qualquer lugar; na nuvem de Olá ou no local. Crie aplicações móveis cativantes para iOS, Android e Windows. Integre com o seu Software como serviço (SaaS) e o enterprise aplicações com toodozens out of box conectividade dos serviços baseados na nuvem e de aplicações da empresa. Código no seu idioma favorito e IDE (.NET, Node.js, PHP, Python ou Java) toobuild as web apps e APIs mais rápidas do que nunca.
* [As Logic Apps][lnk-logicapps]: funcionalidade de Logic Apps Olá do App Service do Azure ajuda a integrar os seus sistemas de linha de negócio existentes do IoT solução tooyour e automatizar os processos de fluxo de trabalho. As Logic Apps permite aos programadores toodesign os fluxos de trabalho que começam com acionadores e, em seguida, executam uma série de passos — regras e ações que utilizar conectores poderosas toointegrate com os processos empresariais. As Logic Apps oferece ecossistema de grande tooa out of box conectividade do SaaS, baseado na nuvem e aplicações no local.
* [Armazenamento de Blobs do Azure][lnk-blob]: armazenamento de nuvem fiável e económica para dados de Olá que os dispositivos as enviam toohello nuvem.

## <a name="conclusion"></a>Conclusão
Este artigo fornece detalhes de nível para estruturar e implementar uma infraestrutura de IoT utilizando o Azure IoT de descrição geral da implementação. Configurar cada toobe componente segura é infraestrutura geral do IoT Olá de chave proteger. Opções de design de Olá disponíveis no Azure IoT fornecem algum nível de flexibilidade e escolha; No entanto, cada escolha pode ter implicações de segurança. Recomenda-se que cada uma destas opções ser avaliadas através de uma avaliação de risco/custo.

[img-overview]: media/iot-secure-your-deployment/overview.png

[lnk-security-tokens]: ../articles/iot-hub/iot-hub-devguide-security.md#security-token-structure
[lnk-sas-tokens]: ../articles/iot-hub/iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-identity-registry]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-protocols]: ../articles/iot-hub/iot-hub-devguide-security.md
[lnk-custom-auth]: ../articles/iot-hub/iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: http://www.itu.int/rec/T-REC-X.509-201210-I/en
[lnk-use-x509]: ../articles/iot-hub/iot-hub-devguide-security.md
[lnk-tls12]: https://tools.ietf.org/html/rfc5246
[lnk-service-tokens]: ../articles/iot-hub/iot-hub-devguide-security.md#use-security-tokens-from-service-components
[lnk-docdb]: https://azure.microsoft.com/services/documentdb/
[lnk-asa]: https://azure.microsoft.com/services/stream-analytics/
[lnk-appservices]: https://azure.microsoft.com/services/app-service/
[lnk-logicapps]: https://azure.microsoft.com/services/app-service/logic/
[lnk-blob]: https://azure.microsoft.com/services/storage/
