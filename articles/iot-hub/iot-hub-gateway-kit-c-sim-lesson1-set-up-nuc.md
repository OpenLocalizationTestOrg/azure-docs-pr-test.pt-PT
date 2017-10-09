---
title: 'Simulated dispositivo & Gateway do IoT do Azure - Lesson 1: Configurar NUC | Microsoft Docs'
description: "Configurar Intel NUC toowork como um gateway de IoT entre um sensor e informações de sensores de toocollect do IoT Hub do Azure e enviá-lo tooIoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: gateway de IOT intel nuc, nuc computador, DE3815TYKE
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Configurar Intel NUC como um gateway de IoT

## <a name="what-you-will-do"></a>O que irá fazer

- Configure Intel NUC como um gateway de IoT.
- Instale o pacote de limite de IoT do Azure de Olá no Intel NUC.
- Execute uma aplicação de exemplo "hello_world" sobre a funcionalidade de gateway do Intel NUC tooverify Olá.
Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que aprenderá

Este lesson, irá aprender:

- Como tooconnect Intel NUC com periféricos.
- Como tooinstall e atualização Olá necessário pacotes a utilizar Intel NUC Olá inteligente Gestor de pacotes.
- Como toorun Olá "hello_world" exemplo funcionalidade de gateway tooverify Olá da aplicação.

## <a name="what-you-need"></a>Do que precisa

- Um DE3815TYKE do Kit de NUC Intel com Olá Intel IoT Suite de Software do Gateway (Linux vento River * 7.0.0.13) pré-instalado.
- Um cabo de Ethernet.
- Um teclado.
- Um cabo HDMI ou VGA.
- Monitor com uma porta HDMI ou VGA.

![Kit de gateway](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a>Ligar Intel NUC com periféricos Olá

imagem de Olá abaixo está um exemplo de NUC Intel que está ligada à periféricos vários:

1. Teclado tooa ligado.
2. Ligado toohello monitor por um cabo VGA ou um cabo HDMI.
3. Ligado tooa rede com fios através de um cabo de Ethernet.
4. Ligado toohello fonte de alimentação com um cabo de energia.

![Intel NUC ligado tooperipherals](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>Ligar o sistema de Intel NUC toohello do computador anfitrião através de Secure Shell (SSH)

Aqui tem de teclado e monitor tooget Olá endereço IP do seu dispositivo NUC. Se já conhece o IP de Olá endereço, pode ignorar toostep 3 nesta secção.

1. Ative o Intel NUC, premindo o botão de energia Olá e registo no sistema Olá.

   nome de utilizador predefinido Olá e a palavra-passe são ambos `root`.

2. Obtenha o endereço IP Olá NUC executando Olá `ifconfig` comando. Este passo é realizado no dispositivo NUC Olá.

   Eis um exemplo de saída do comando Olá.

   ![saída de ifconfig Mostrar NUC IP](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   Neste exemplo, Olá valor que se segue `inet addr:` é o endereço IP Olá que necessita quando planeia tooconnect remotamente a partir de um tooIntel do computador anfitrião NUC.

3. Utilize um dos seguintes clientes SSH de tooIntel de tooconnect máquina do anfitrião NUC de Olá.

   - [PuTTY](http://www.putty.org/) para Windows.
   - Olá compilação no cliente SSH no Ubuntu ou macOS.

   É mais eficiente e produtiva toooperate no Intel NUC de um computador anfitrião. Terá de endereço IP de Olá Olá, nome de utilizador e palavra-passe tooconnect Olá NUC através do cliente SSH. Segue-se o cliente SSH de utilização de exemplo de Olá no macOS.
   ![Cliente SSH em execução no macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-hello-azure-iot-edge-package"></a>Instalar o pacote de limite de IoT do Azure Olá

pacote de limite de IoT do Azure Olá contém binários previamente compilados Olá Olá SDK e as respetivas dependências. Estes binários são Azure IoT Edge, Olá SDK do Azure IoT e ferramentas correspondente Olá. pacote de Olá também contém uma aplicação de exemplo de "hello_world" que é a funcionalidade de gateway de Olá toovalidate utilizados. Limite de IoT faz parte de núcleos de Olá do gateway de Olá. Olá tooinstall do pacote, siga estes passos:

1. Adicione o repositório de nuvem do IoT Olá executando Olá os seguintes comandos numa janela de terminal:

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   Olá `rpm` comando importa Olá chave rpm. Olá `smart channel` comando adiciona rpm Olá canal toohello inteligente Gestor de pacotes. Antes de executar Olá `smart update` comando, verá um resultado como abaixo.

   ![rpm e de saída de comandos do canal inteligente](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. Instale o pacote de Olá executando Olá os seguintes comandos:

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`é Olá nome do pacote de Olá. Olá `smart install` comando é o pacote de Olá tooinstall utilizado.

   Após a instalação do pacote de Olá, Intel NUC é esperado toowork como um gateway.

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a>Executar a aplicação de exemplo Olá Azure IoT Edge "hello_world"

Aceda demasiado`azureiotgatewaysdk/samples` e execute a aplicação de exemplo Olá exemplo "hello_world". Esta aplicação de exemplo cria um gateway de Olá `hello_world.json` do ficheiro e utiliza componentes fundamentais do Olá de Olá Azure IoT Edge arquitetura toolog um ficheiro de tooa Olá mundo mensagem a cada cinco segundos.

Pode executar a aplicação de exemplo de "hello_world" de exemplo de Olá executando Olá os seguintes comandos:

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

aplicação de exemplo de Olá produz seguinte Olá saída se a funcionalidade de gateway Olá está a funcionar corretamente:

![saída da aplicação](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="summary"></a>Resumo

Parabéns! Concluiu a cópia de segurança Intel NUC como um gateway. Agora está pronto toomove no seguinte lesson tooset toohello cópia de segurança do computador anfitrião, criar um hub IoT do Azure e registar o seu dispositivo lógico do Azure IoT hub.

## <a name="next-steps"></a>Passos seguintes
[Preparar o seu computador anfitrião e o hub IoT do Azure](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
