---
title: aaaDeploy ligado do Azure IoT Suite factory gateway | Microsoft Docs
description: "Como toodeploy um gateway no Windows ou Linux toohello de conectividade tooenable ligadas fábrica solução pré-configurada."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 72436dec60eda0de20143f362fe740b0c4412f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-gateway-on-windows-or-linux-for-hello-connected-factory-preconfigured-solution"></a>Implementar um gateway no Windows ou Linux para a solução de fábrica pré-configurada Olá ligado

Olá software necessário toodeploy um gateway para a solução de fábrica pré-configurada Olá ligado tem dois componentes:

* Olá *OPC Proxy* estabelece uma ligação tooIoT Hub. Olá *OPC Proxy* , em seguida, aguarda para mensagens de comando e controlo de Olá integrado OPC Browser, que é executado no portal de solução Olá fábrica ligado.
* Olá *OPC publicador* liga os servidores OPC UA tooexisting no local e reencaminha as mensagens de telemetria dos mesmos tooIoT Hub.

Ambos os componentes são open source e estão disponíveis como origem no GitHub e como contentores de Docker:

| GitHub | DockerHub |
| ------ | --------- |
| [Publicador OPC][lnk-publisher-github] | [Publicador OPC][lnk-publisher-docker] |
| [OPC Proxy][lnk-proxy-github] | [OPC Proxy][lnk-proxy-docker] |

Nenhum destinado ao público endereço IP ou holes na firewall do gateway Olá são necessários para o componente. Olá OPC Proxy e o publicador OPC utilizam apenas saídas portas 443, 5671 e 8883.

Olá passos neste artigo mostram-lhe como toodeploy um gateway com o Docker numa [Windows](#windows-deployment) ou [Linux](#linux-deployment). gateway de Olá permite conectividade toohello ligado fábrica pré-configurada solução.

> [!NOTE]
> Olá gateway software que é executado no contentor de Docker Olá é [Azure IoT Edge].

## <a name="windows-deployment"></a>Implementação do Windows

> [!NOTE]
> Se ainda não tiver um dispositivo de gateway, a Microsoft recomenda que comprar um gateway comercial a partir de um dos nossos parceiros. Visite Olá [catálogo de dispositivos do IoT do Azure] para obter uma lista de dispositivos de gateway compatíveis com Olá ligado solução de fábrica. Siga as instruções de Olá que vêm com Olá dispositivo tooset segurança gateway Olá. Em alternativa, utilize Olá toomanually instruções dos gateways de existentes configurar os seguintes.

### <a name="install-docker"></a>Instalar Docker

Instalar [Docker para Windows] no seu dispositivo de gateway baseado no Windows. Durante a configuração do Windows Docker, selecione uma unidade no seu tooshare da máquina de anfitrião com o Docker. Olá seguinte captura de ecrã mostra a partilha de unidade de Olá D no seu sistema do Windows:

![Instalar Docker][img-install-docker]

Em seguida, crie uma pasta denominada **docker** na raiz de Olá da Olá as unidades partilhadas.
Também pode efetuar este passo depois de instalar o docker de Olá **definições** menu.

### <a name="configure-hello-gateway"></a>Configurar o gateway de Olá

1. Terá de Olá **iothubowner** cadeia de ligação do seu Azure IoT Suite ligado a implementação do factory implementação toocomplete Olá gateway. No Olá [portal do Azure], navegue até tooyour IoT Hub no grupo de recursos de Olá criado quando implementou a solução de fábrica Olá ligado. Clique em **políticas de acesso partilhado** tooaccess Olá **iothubowner** cadeia de ligação:

    ![Determinar Olá cadeia de ligação do IoT Hub][img-hub-connection]

    Olá cópia **cadeia de ligação - chave primária** valor.

1. Configurar o gateway de Olá para o seu IoT Hub através da execução de módulos de gateway Olá dois **depois** numa linha de comandos com:

    `docker run -it --rm -h <ApplicationName> -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt;**  é Olá nome toogive tooyour OPC UA publicador no formato de Olá **publicador.&lt; o nome de domínio completamente qualificado&gt;**. Por exemplo, se denomina-se a sua rede de fábrica **myfactorynetwork.com**, Olá **ApplicationName** valor é **publisher.myfactorynetwork.com**.
    * **&lt;IoTHubOwnerConnectionString&gt;**  é Olá **iothubowner** cadeia de ligação que copiou no passo anterior Olá. Esta cadeia de ligação é apenas utilizada neste passo, não precisa, no Olá os seguintes passos:

    Utilizar Olá mapeado d:\\pasta docker (Olá `-v` argumento) toopersist posterior Olá dois certificados x. 509 que utilizam módulos de gateway Olá.

### <a name="run-hello-gateway"></a>Executar Olá gateway

1. Reinicie o gateway de Olá utilizando Olá os seguintes comandos:

    `docker run -it --rm -h <ApplicationName> --expose 62222 -p 62222:62222 -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/shared -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. Por motivos de segurança, certificados de x. 509 Olá dois continuada no Olá d:\\pasta docker contém a chave privada Olá. Limitar acesso toothis pasta toohello credenciais (normalmente **administradores**) utilizar o contentor de Docker toorun Olá. Contexto Olá d:\\pasta docker, escolha **propriedades**, em seguida, **segurança**e, em seguida, **editar**. Dê **administradores** controlo total e remover todas as pessoas pessoa:

    ![Partilha de tooDocker conceder permissões][img-docker-share]

1. Verifique a conectividade de rede. Numa linha de comandos, introduza o comando de Olá `ping publisher.<your fully qualified domain name>` tooping o gateway. Se o destino de Olá está inacessível, adicione endereço IP de Olá e o nome do seu ficheiro de anfitriões do gateway toohello no seu gateway. ficheiro de anfitriões de Olá está localizado na Olá **Windows\\System32\\controladores\\etc** pasta.

1. Em seguida, tente tooconnect toohello publicador utilizando um cliente de OPC UA local em execução no gateway de Olá. Olá ponto final de OPC UA URL é `opc.tcp://publisher.<your fully qualified domain name>:62222`. Se não tiver um cliente de OPC UA, pode transferir e utilizar um [cliente de OPC UA open source].

1. Quando tiver concluído com êxito estes testes locais, procurar toohello **ligar o seu próprio servidor de UA OPC** página no portal de solução Olá fábrica ligado. Introduza o URL de ponto final do publicador Olá (`tcp://publisher.<your fully qualified domain name>:62222`) e clique em **Connect**. Receber um aviso de certificado, em seguida, clique em **continuar.** Em seguida obtiver um erro que Olá publicador não confia Olá UA Web cliente. tooresolve este erro, Olá cópia **UA Web cliente** certificado Olá **D:\\docker\\rejeitado certificados\\certificados** pasta toohello **D:\\docker\\UA aplicações\\certificados** pasta no gateway de Olá. Não é necessário toorestart do gateway de Olá. Repita este passo. Pode agora ligar toohello gateway de nuvem Olá e estiver pronto tooadd solução de toohello OPC UA servidores.

### <a name="add-your-opc-ua-servers"></a>Adicionar os servidores de OPC UA

1. Procurar toohello **ligar o seu próprio servidor de UA OPC** página no portal de solução Olá fábrica ligado. Siga os passos da Olá anterior a secção tooestablish ends confiam entre o Olá portal fábrica ligado e hello do servidor de OPC UA de Olá. Este passo estabelece uma confiança de certificados de Olá da Olá mútua ligado portal de fábrica e Olá servidor OPC UA e cria uma ligação.

1. Procurar Olá árvore de nós de OPC UA do seu servidor de OPC UA, nós OPC Olá com o botão direito e selecione **publicar**. Para publicação toowork desta forma, Olá servidor OPC UA e Olá publicador tem de ser no Olá mesma rede. Por outras palavras, se Olá totalmente qualificado o nome de domínio do publicador Olá é **publisher.mydomain.com** , em seguida, nome de domínio completamente qualificado Olá de Olá OPC UA servidor tem de ser, por exemplo, **myopcuaserver.mydomain.com**. Se o programa de configuração for diferente, pode adicionar manualmente ficheiros publishesnodes.json toohello de nós encontrado no Olá **D:\\docker** pasta. Olá publishesnodes.json ficheiro é gerado automaticamente no Olá primeiro bem-sucedida publicar de um nó OPC.

1. Agora flui de telemetria do dispositivo de gateway Olá. Pode ver a telemetria Olá no Olá **fábrica localizações** vista do portal de fábrica ligado Olá em **nova fábrica**.

## <a name="linux-deployment"></a>Implementação do Linux

> [!NOTE]
> Se ainda não tiver um dispositivo de gateway, a Microsoft recomenda que comprar um gateway comercial a partir de um dos nossos parceiros. Visite Olá [catálogo de dispositivos do IoT do Azure] para obter uma lista de dispositivos de gateway compatíveis com Olá ligado solução de fábrica. Siga as instruções de Olá que vêm com Olá dispositivo tooset segurança gateway Olá. Em alternativa, utilize Olá toomanually instruções dos gateways de existentes configurar os seguintes.

[Instalar Docker] no seu dispositivo de gateway do Linux.

### <a name="configure-hello-gateway"></a>Configurar o gateway de Olá

1. Terá de Olá **iothubowner** cadeia de ligação do seu Azure IoT Suite ligado a implementação do factory implementação toocomplete Olá gateway. No Olá [portal do Azure], navegue até tooyour IoT Hub no grupo de recursos de Olá criado quando implementou a solução de fábrica Olá ligado. Clique em **políticas de acesso partilhado** tooaccess Olá **iothubowner** cadeia de ligação:

    ![Determinar Olá cadeia de ligação do IoT Hub][img-hub-connection]

    Olá cópia **cadeia de ligação - chave primária** valor.

1. Configurar o gateway de Olá para o seu IoT Hub através da execução de módulos de gateway Olá dois **depois** de uma shell com:

    `sudo docker run -it --rm -h <ApplicationName> -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/ -v /shared:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `sudo docker run --rm -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt;**  é Olá nome de Olá gateway de Olá OPC UA aplicação cria no formato de Olá **publicador.&lt; o nome de domínio completamente qualificado&gt;**. Por exemplo, **publisher.microsoft.com**.
    * **&lt;IoTHubOwnerConnectionString&gt;**  é Olá **iothubowner** cadeia de ligação que copiou no passo anterior Olá. Esta cadeia de ligação é apenas utilizada neste passo, não precisa, no Olá os seguintes passos:

    Utilizar Olá **/ partilhado** pasta (Olá `-v` argumento) toopersist posterior Olá dois certificados x. 509 que utilizam módulos de gateway Olá.

### <a name="run-hello-gateway"></a>Executar Olá gateway

1. Reinicie o gateway de Olá utilizando Olá os seguintes comandos:

    `sudo docker run -it -h <ApplicationName> --expose 62222 -p 62222:62222 –-rm -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v /shared:/shared -v /shared:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `sudo docker run -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. Por motivos de segurança, certificados de x. 509 Olá dois continuada no Olá **/ partilhado** pasta contém a chave privada Olá. Limite acesso toothis pasta toohello credenciais a utilizar toorun Olá contentor de Docker. permissões de Olá tooset para **raiz** apenas, utilize Olá `chmod` shell de comandos na pasta Olá.

1. Verifique a conectividade de rede. A partir de uma shell, introduza o comando de Olá `ping publisher.<your fully qualified domain name>` tooping o gateway. Se o destino de Olá está inacessível, adicione endereço IP de Olá e o nome do seu ficheiro de anfitriões do gateway tooyour no seu gateway. ficheiro de anfitriões de Olá está localizado na Olá **/etc** pasta.

1. Em seguida, tente tooconnect toohello publicador utilizando um cliente de OPC UA local em execução no gateway de Olá. Olá ponto final de OPC UA URL é `opc.tcp://publisher.<your fully qualified domain name>:62222`. Se não tiver um cliente de OPC UA, pode transferir e utilizar um [cliente de OPC UA open source].

1. Quando tiver concluído com êxito estes testes locais, procurar toohello **ligar o seu próprio servidor de UA OPC** página no portal de solução Olá fábrica ligado. Introduza o URL de ponto final do publicador Olá (`tcp://publisher.<your fully qualified domain name>:62222`) e clique em **Connect**. Receber um aviso de certificado, em seguida, clique em **continuar.** Em seguida obtiver um erro que Olá publicador não confia Olá UA Web cliente. tooresolve este erro, Olá cópia **UA Web cliente** certificado Olá **partilhado/rejeitado certificados/certificados** pasta toohello **/shared/UA aplicações/certificados** pasta no gateway de Olá. Não é necessário toorestart do gateway de Olá. Repita este passo. Pode agora ligar toohello gateway de nuvem Olá e estiver pronto tooadd solução de toohello OPC UA servidores.

### <a name="add-your-opc-ua-servers"></a>Adicionar os servidores de OPC UA

1. Procurar toohello **ligar o seu próprio servidor de UA OPC** página no portal de solução Olá fábrica ligado. Siga os passos da Olá anterior a secção tooestablish ends confiam entre o Olá portal fábrica ligado e hello do servidor de OPC UA de Olá. Este passo estabelece uma confiança de certificados de Olá da Olá mútua ligado portal de fábrica e Olá servidor OPC UA e cria uma ligação.

1. Procurar Olá árvore de nós de OPC UA do seu servidor de OPC UA, nós OPC Olá com o botão direito e selecione **publicar**. Para publicação toowork desta forma, Olá servidor OPC UA e Olá publicador tem de ser no Olá mesma rede. Por outras palavras, se Olá totalmente qualificado o nome de domínio do publicador Olá é **publisher.mydomain.com** , em seguida, nome de domínio completamente qualificado Olá de Olá OPC UA servidor tem de ser, por exemplo, **myopcuaserver.mydomain.com**. Se o programa de configuração for diferente, pode adicionar manualmente ficheiros publishesnodes.json toohello de nós encontrado no Olá **/ partilhado** pasta. Olá publishesnodes.json é gerado automaticamente no Olá primeiro bem-sucedida publicar de um nó OPC.

1. Agora flui de telemetria do dispositivo de gateway Olá. Pode ver a telemetria Olá no Olá **fábrica localizações** vista do portal de fábrica ligado Olá em **nova fábrica**.

## <a name="next-steps"></a>Passos seguintes

toolearn mais informações sobre a arquitetura de Olá do factory ligado Olá solução pré-configurada, consulte [instruções sobre a solução pré-configurada de fábrica ligada][lnk-walkthrough].

[img-install-docker]: ./media/iot-suite-connected-factory-gateway-deployment/image1.png
[img-hub-connection]: ./media/iot-suite-connected-factory-gateway-deployment/image2.png
[img-docker-share]: ./media/iot-suite-connected-factory-gateway-deployment/image3.png

[Docker para Windows]: https://www.docker.com/docker-windows
[catálogo de dispositivos do IoT do Azure]: https://catalog.azureiotsuite.com/?q=opc
[portal do Azure]: http://portal.azure.com/
[cliente de OPC UA open source]: https://github.com/OPCFoundation/UA-.NETStandardLibrary/tree/master/SampleApplications/Samples/Client.Net4
[Instalar Docker]: https://www.docker.com/community-edition#/download
[lnk-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[Azure IoT Edge]: https://github.com/Azure/iot-edge

[lnk-publisher-github]: https://github.com/Azure/iot-edge-opc-publisher
[lnk-publisher-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua
[lnk-proxy-github]: https://github.com/Azure/iot-edge-opc-proxy
[lnk-proxy-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua-proxy