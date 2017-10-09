---
title: aaaHow redirecionar a dispositivos USB no Azure RemoteApp? | Microsoft Docs
description: Saiba como toouse redirecionamento para dispositivos USB no Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 191d98af-2f5a-4307-9042-aae0e4049f9f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 661b90c0910167d76ac3886b5af7a32d00b3943f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-redirect-usb-devices-in-azure-remoteapp"></a>Como redireciona dispositivos USB no Azure RemoteApp?
> [!IMPORTANT]
> O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017. Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.
> 
> 

Redirecionamento do dispositivo permite aos utilizadores utilizar o Olá USB dispositivos tootheir ligado ao computador ou tablet com aplicações Olá no Azure RemoteApp. Por exemplo, se partilhado Skype através do Azure RemoteApp, os utilizadores tem de toouse capaz de toobe câmaras os respetivos dispositivos.

Antes de ir adicional, certifique-se ler informações de redirecionamento USB Olá no [redirecionamento a utilizar no Azure RemoteApp](remoteapp-redirection.md). No entanto Olá recomendado nusbdevicestoredirect:s: * não vai funcionar câmaras web USB e poderão não funcionar para algumas impressoras USB ou dispositivos multifunctional USB. Por predefinição e por motivos de segurança, o administrador do Azure RemoteApp Olá tem tooenable redirecionamento, de pela classe de dispositivo GUID ou por ID de instância do dispositivo antes dos utilizadores podem utilizar esses dispositivos.

Embora este artigo aborda o redirecionamento de câmara web, pode utilizar um impressoras USB de tooredirect abordagem semelhante e outros dispositivos de multifunctional USB que não são redirecionados pelo Olá **nusbdevicestoredirect:s:*** comando.

## <a name="redirection-options-for-usb-devices"></a>Opções de redirecionamento para dispositivos USB
O Azure RemoteApp utiliza mecanismos muito semelhantes para o redireccionamento de dispositivos USB como Olá aqueles disponíveis para os serviços de ambiente de trabalho remoto. Olá tecnologia subjacente permite-lhe escolher método de redirecionamento correto Olá para um determinado dispositivo, tooget Olá melhor de alto nível ambos e redirecionamento de dispositivo RemoteFX USB utilizando Olá **usbdevicestoredirect:s:** comando. Existem quatro elementos toothis comando:

| Ordem de processamento | Parâmetro | Descrição |
| --- | --- | --- |
| 1 |* |Seleciona todos os dispositivos que não são captados ao redirecionamento de alto nível. Nota: por predefinição, * não funciona para as câmaras web USB. |
| {Classe de dispositivo GUID} |Seleciona todos os dispositivos que correspondem ao hello especificado classe de programa de configuração do dispositivo. | |
| USB\InstanceID |Seleciona um dispositivo USB especificado para Olá fornecido ID de instância. | |
| 2 |-USB\Instance ID |Remove as definições de redirecionamento de Olá para o dispositivo especificado Olá. |

## <a name="redirecting-a-usb-device-by-using-hello-device-class-guid"></a>Redirecionar um dispositivo USB utilizando a classe de dispositivo Olá GUID
Existem duas formas classe de dispositivo toofind Olá GUID que pode ser utilizado para o redirecionamento. 

opção de primeiro Olá é toouse Olá [tooVendors System-Defined dispositivo configuração Classes disponíveis](https://msdn.microsoft.com/library/windows/hardware/ff553426.aspx). Escolha a classe de Olá que mais se aproxima do computador local do Olá dispositivo toohello anexado. Para as câmaras digitais, isto pode ser uma classe de dispositivo de processamento de imagens ou a classe de dispositivo de captura de vídeo. Terá de toodo algumas experimentação com Olá dispositivo classes toofind Olá correto classe GUID que funciona com Olá localmente anexados dispositivo USB (no nosso câmara web de Olá maiúsculas).

Uma melhor forma, ou a segunda opção Olá, é toofollow GUID de classe estes passos toofind Olá específica do dispositivo:

1. Abra o Gestor de dispositivos de Olá, localize o dispositivo Olá será redirecionado e faça duplo clique nele e, em seguida, abra as propriedades de Olá.
   ![Olá abra o Gestor de dispositivos](./media/remoteapp-usbredir/ra-devicemanager.png)
2. No Olá **detalhes** separador, escolha a propriedade Olá **classe Guid**. o valor de Olá que aparece é Olá GUID de classe para esse tipo de dispositivo.
   ![Propriedades da câmara](./media/remoteapp-usbredir/ra-classguid.png)
3. Utilize dispositivos tooredirect de valor de Guid de classe de Olá que correspondem ao mesmo.

Por exemplo:

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s:<Class Guid value>"

Pode combinar vários redirecionamentos de dispositivo no Olá mesmo cmdlet. Por exemplo: tooredirect de armazenamento local e uma USB web câmara, cmdlet tem o seguinte aspeto:

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:<Class Guid value>"

Quando definir o redirecionamento do dispositivo por classe GUID são redirecionados todos os dispositivos que correspondem ao que a classe GUID Olá especificado coleção. Por exemplo, se existirem vários computadores na rede local Olá que tenham Olá mesmo câmaras web USB, pode executar um cmdlet único tooredirect todas as câmaras web Olá.

## <a name="redirecting-a-usb-device-by-using-hello-device-instance-id"></a>Redirecionar um dispositivo USB com o ID de instância de dispositivo Olá
Se pretender um controlo mais detalhado e quiser toocontrol redirecionamento por dispositivo, pode utilizar Olá **USB\InstanceID** parâmetro de redirecionamento.

Olá hardest parte este método é ao localizar o ID de instância de dispositivo Olá USB. Irá precisar de aceder toohello computador e de dispositivo USB específico do Olá. Em seguida, siga estes passos:

1. Ativar o redirecionamento de dispositivo Olá numa sessão de ambiente de trabalho remoto conforme descrito em [como posso utilizar os meus dispositivos e recursos numa sessão de ambiente de trabalho remoto?](http://windows.microsoft.com/en-us/windows7/How-can-I-use-my-devices-and-resources-in-a-Remote-Desktop-session)
2. Abrir uma ligação de ambiente de trabalho remoto e clique em **Mostrar opções**.
3. Clique em **guardar como** toosave Olá atual ligação definições tooan ficheiro RDP.  
    ![Guardar definições de Olá como um ficheiro RDP](./media/remoteapp-usbredir/ra-saveasrdp.png)
4. Escolha um nome de ficheiro e uma localização, por exemplo, MyConnection.rdp e este PC\Documents e guarde o ficheiro de Olá.
5. Abra Olá MyConnection.rdp com um editor de texto do ficheiro e localizar o ID de instância de Olá do dispositivo Olá pretende tooredirect.

Agora, utilize ID de instância de Olá Olá seguinte cmdlet:

    Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s: USB\<Device InstanceID value>"



### <a name="help-us-help-you"></a>Ajude-nos para o podermos ajudar
Sabia que na adição toorating neste artigo e deixar um comentário abaixo, pode efetuar alterações toohello próprio artigo? Falta algo? Algo errado? Escrevi algo que é simplesmente confuso? Desloque o ecrã para cima e clique em **editar no GitHub** toomake alterações - os ficará toous para revisão e, em seguida, depois, termine a sessão nos mesmos, irá ver as suas alterações e melhorias apresentadas aqui.

