---
title: "aaaPowerShell para gestão de dispositivos do StorSimple | Microsoft Docs"
description: Saiba como toouse do Windows PowerShell para StorSimple toomanage o dispositivo StorSimple.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/03/2017
ms.author: alkohli@microsoft.com
ms.openlocfilehash: e9e4bd025933cdef68b861d93749a107d1689536
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-for-storsimple-tooadminister-your-device"></a>Utilizar o Windows PowerShell para StorSimple tooadminister o dispositivo

## <a name="overview"></a>Descrição geral

O Windows PowerShell para StorSimple fornece uma interface de linha de comandos que é possível utilizar toomanage dispositivo Microsoft Azure StorSimple. Como o nome de Olá sugere, é uma interface de linha de comandos baseada no Windows PowerShell, que é criada num espaço de execução restrita. Perspetiva Olá do utilizador Olá na linha de comandos Olá, um espaço de execução restrita aparece como uma versão restrita do Windows PowerShell. Enquanto mantém algumas das funcionalidades básicas do Olá do Windows PowerShell, esta interface tem cmdlets dedicados adicionais que são adaptados para gerir o seu dispositivo do Microsoft Azure StorSimple.

Este artigo descreve Olá do Windows PowerShell para StorSimple funcionalidades, incluindo a forma como pode ligar toothis interface e contém procedimentos de toostep-a-passo de ligações ou fluxos de trabalho que pode realizar com esta interface. fluxos de trabalho Olá incluem como tooregister seu dispositivo, configure a interface de rede de Olá no seu dispositivo, as atualizações de instalação que necessitem de Olá toobe de dispositivo em modo de manutenção, alterar o estado do dispositivo Olá, e resolva quaisquer problemas que podem ocorrer.

Depois de ler este artigo, será capaz de:

* Ligue o dispositivo StorSimple tooyour através do Windows PowerShell para StorSimple.
* Administrar o dispositivo StorSimple com o Windows PowerShell para StorSimple.
* Obter ajuda do Windows PowerShell para StorSimple.

> [!NOTE]
> * O Windows PowerShell para StorSimple cmdlets permitem-lhe toomanage o dispositivo StorSimple da consola de série ou remotamente através da gestão remota do Windows PowerShell. Para mais informações sobre cada um dos cmdlets individuais Olá que pode ser utilizados nesta interface, visite demasiado[referência de cmdlets do Windows PowerShell para StorSimple](https://technet.microsoft.com/library/dn688168.aspx).
> * cmdlets do Azure PowerShell StorSimple Olá são uma coleção diferente de cmdlets que permitem que tooautomate nível de serviço do StorSimple e tarefas de migração a partir da linha de comandos Olá. Para mais informações sobre Olá cmdlets Azure PowerShell para StorSimple, visite toohello [referência de cmdlets do Azure StorSimple](https://docs.microsoft.com/powershell/servicemanagement/azure.storsimple/v3.1.0/azure.storsimple).


Pode aceder ao hello do Windows PowerShell para StorSimple utilizando um dos seguintes métodos de Olá:

* [Ligar a consola de série do dispositivo de tooStorSimple](#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)
* [Ligar remotamente tooStorSimple através do Windows PowerShell](#connect-remotely-to-storsimple-using-windows-powershell-for-storsimple)

## <a name="connect-toowindows-powershell-for-storsimple-via-hello-device-serial-console"></a>Ligar tooWindows do PowerShell para StorSimple através da consola de série do dispositivo de Olá

Pode [transfira o PuTTY](http://www.putty.org/) ou semelhante tooWindows de tooconnect de software de emulação do terminal do PowerShell para StorSimple. Terá de tooconfigure PuTTY especificamente tooaccess Olá dispositivo Microsoft Azure StorSimple. Olá tópicos seguintes contêm os passos detalhados sobre como tooconfigure PuTTy e ligar toohello dispositivo. Também são explicados com várias opções de menu na consola de série de Olá.

### <a name="putty-settings"></a>Definições do PuTTY

Certifique-se de que utiliza Olá seguir interface do PuTTY definições tooconnect toohello do Windows PowerShell a partir da consola de série de Olá.

#### <a name="tooconfigure-putty"></a>tooconfigure PuTTY

1. No Olá PuTTY **reconfiguração** Olá caixa de diálogo **categoria** painel, selecione **teclado**.
2. Certifique-se de que Olá opções a seguir são selecionadas (estas são as definições predefinidas da Olá quando iniciar uma nova sessão).
   
   | Item de teclado | Selecione |
   | --- | --- |
   | Chave de retrocesso |Controlo-? (127) |
   | Chaves inicial e final |Standard |
   | Teclas de função e de teclado |ESC [n ~ |
   | Estado inicial de chaves do cursor |Normal |
   | Estado inicial do teclado numérico |Normal |
   | Ativar funcionalidades adicionais de teclado |Controlo Alt é diferente do AltGr |
   
    ![Definições de Putty suportadas](./media/storsimple-windows-powershell-administration/IC740877.png)
3. Clique em **Aplicar**.
4. No Olá **categoria** painel, selecione **tradução**.
5. No Olá **conjunto de carateres remoto** caixa de lista, selecione **UTF-8**.
6. Em **processamento de carateres de desenho de linha**, selecione **pontos de código de desenho de linha de utilização Unicode**. Olá seguinte captura de ecrã mostra as seleções de PuTTY correto Olá.
   
    ![Definições do Putty UTF](./media/storsimple-windows-powershell-administration/IC740878.png)
7. Clique em **Aplicar**.

Agora, pode utilizar a consola de série do dispositivo PuTTY tooconnect toohello efetuando Olá os seguintes passos.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="about-hello-serial-console"></a>Sobre a consola de série de Olá

Quando aceder à interface do Windows PowerShell Olá do dispositivo StorSimple através da consola de série de Olá, é apresentada uma mensagem de faixa, seguido de opções de menu.

mensagem de faixa de saudação contém informações de dispositivo StorSimple básicas, tais como o modelo de Olá, nome, versão do software instalado e estado do controlador de Olá que estão a aceder. Olá imagem a seguir mostra um exemplo de uma mensagem de faixa.

![Mensagem de faixa de série](./media/storsimple-windows-powershell-administration/IC741098.png)

> [!IMPORTANT]
> Pode utilizar tooidentify de mensagem de faixa Olá quer Olá controlador seja ligado toois _Active Directory_ ou _passivo_.

Olá a seguir mostra imagem Olá várias opções de espaço de execução que estão disponíveis no menu da consola de série de Olá.

![Registar o seu dispositivo 2](./media/storsimple-windows-powershell-administration/IC740906.png)

Pode escolher entre Olá seguintes definições:

1. **Iniciar sessão com acesso total** esta opção permite-lhe tooconnect (com as credenciais corretas Olá) toohello **SSAdminConsole** espaço de execução num controlador de locais de Olá. (o controlador de locais de Olá é controlador de Olá que atualmente estão a aceder através da consola de série de Olá do dispositivo StorSimple.) Esta opção também pode ser utilizada tooallow tooaccess Support da Microsoft sem restrições tootroubleshoot de espaço de execução (uma sessão de suporte) para quaisquer problemas com dispositivos possíveis. Depois de utilizar a opção 1 toolog no, pode permitir que engenheiro de Microsoft Support Olá espaço de execução tooaccess sem restrições ao executar um cmdlet específico. Para obter detalhes, consulte demasiado[iniciar uma sessão de suporte](storsimple-8000-contact-microsoft-support.md#start-a-support-session-in-windows-powershell-for-storsimple).
   
2. **Inicie sessão no controlador de toopeer com acesso total** esta opção é Olá mesmo como opção 1, exceto que se possa ligar (com as credenciais corretas Olá) toohello **SSAdminConsole** espaço de execução num controlador de ponto a ponto Olá. Porque o dispositivo StorSimple Olá é um dispositivo de elevada disponibilidade com dois controladores de uma configuração de ativo-passivo, ponto a ponto refere-se toohello outro controlador de dispositivo de Olá que estão a aceder através da consola de série de Olá).
   Semelhante toooption 1, esta opção também pode ser o espaço de execução do tooallow utilizados Microsoft Support tooaccess irrestrito num controlador de ponto a ponto.

3. **Estabelecer ligação com acesso limitado** esta opção é utilizado tooaccess interface do Windows PowerShell no modo limitado. Não lhe forem pedidas as credenciais de acesso. Esta opção se liga tooa mais restringida espaço de execução em comparação comparado toooptions 1 e 2.  Algumas das tarefas de Olá que estão disponíveis através da opção 1 que **não é possível* ser efetuada neste espaço de execução são:
   
   * Repor as definições de fábrica toohello
   * Alterar a palavra-passe do Olá
   * Ativar ou desativar o acesso de suporte
   * Aplicar atualizações
   * Instalar correções

    > [!NOTE]
    > Esta é a opção de Olá preferido se tenha esquecido palavra-passe de administrador de dispositivo Olá e não é possível ligar através da opção 1 ou 2.

4. **Alterar idioma** esta opção permite-lhe idioma de apresentação de Olá toochange na interface do Windows PowerShell de Olá. idiomas Olá suportados são inglês, japonês, russo, francês, coreano Sul, espanhol, italiano, alemão, chinês e Português-Brasil.

## <a name="connect-remotely-toostorsimple-using-windows-powershell-for-storsimple"></a>Ligar remotamente tooStorSimple através do Windows PowerShell para StorSimple

Pode utilizar o dispositivo do Windows PowerShell remota tooconnect tooyour StorSimple. Quando se liga desta forma, não verá um menu. (Pode ver um menu apenas se utilizar a consola de série de Olá no Olá tooconnect de dispositivo. Ligar remotamente leva-o diretamente toohello equivalente a "opção 1 – acesso total" na consola de série de Olá.) Com comunicação remota do Windows PowerShell, ligar específico tooa de espaço de execução. Também pode especificar o idioma de apresentação de Olá.

Olá idioma de apresentação é independente de idioma de Olá defina utilizando Olá **alterar idioma** opção no menu da consola de série de Olá. PowerShell remoto selecionará automaticamente região da Olá do dispositivo Olá que está a ligar de se não for especificado nenhum.

> [!NOTE]
> Se estiver a trabalhar com anfitriões virtuais do Microsoft Azure e aplicações de nuvem do StorSimple, pode utilizar o Windows PowerShell remota e Olá anfitrião virtual tooconnect toohello dispositivo de nuvem. Se tiver configurado uma localização de partilha no anfitrião de Olá nas informações que toosave da sessão do Windows PowerShell Olá, deve ter em mente que Olá _todas as pessoas_ principal inclui apenas os utilizadores autenticados. Por conseguinte, se configurou Olá acesso partilha tooallow por _todas as pessoas_ e ligar sem especificar as credenciais, principal anónimo não autenticados de Olá será utilizado e verá um erro. toofix este problema, no Olá partilhar o anfitrião tem de ativar a conta de convidado Olá e, em seguida, atribua a partilha de toohello de acesso total de conta de convidado de Olá ou tem de especificar credenciais válidas juntamente com Olá cmdlet do Windows PowerShell.


Pode utilizar HTTP ou HTTPS tooconnect através de comunicação remota do Windows PowerShell. Utilize as instruções de Olá Olá seguintes tutoriais:

* [Ligar remotamente utilizando HTTP](storsimple-remote-connect.md#connect-through-http)
* [Ligar remotamente através de HTTPS](storsimple-remote-connect.md#connect-through-https)

## <a name="connection-security-considerations"></a>Considerações de segurança de ligação

Quando decidir como tooconnect tooWindows do PowerShell para StorSimple, considere o seguinte Olá:

* Ligar diretamente toohello a consola de série do dispositivo é segura, mas a ligação consola de série de toohello através de comutadores de rede não está. Tenha cuidado Olá riscos de segurança ao ligar toodevice série através de comutadores de rede.
* Ligar através de uma sessão HTTP poderá oferecem mais segurança ao que ligam através da consola de série de Olá através de rede. Embora não seja método mais seguro Olá, é aceitável em redes fidedignas.
* Ligar através de uma sessão HTTPS é Olá mais segura e Olá opção recomendada.

## <a name="administer-your-storsimple-device-using-windows-powershell-for-storsimple"></a>Administrar o dispositivo StorSimple com o Windows PowerShell para StorSimple

Olá tabela seguinte mostra um resumo de todas as tarefas de gestão comuns do Olá e fluxos de trabalho complexos que podem ser executados dentro da interface do Windows PowerShell Olá do dispositivo StorSimple. Para obter mais informações sobre cada fluxo de trabalho, clique em entrada adequada de Olá na tabela de Olá.

#### <a name="windows-powershell-for-storsimple-workflows"></a>Windows PowerShell para StorSimple fluxos de trabalho

| Se quiser toodo isto... | Utilize este procedimento. |
| --- | --- |
| Registar o seu dispositivo |[Configurar e registar o dispositivo de Olá através do Windows PowerShell para StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |
| Configurar proxy Web</br>Ver definições de proxy web |[Configurar o proxy web para o dispositivo StorSimple](storsimple-8000-configure-web-proxy.md) |
| Modificar as definições da interface de rede 0 dados no seu dispositivo |[Modificar interface rede DATA 0 para o dispositivo StorSimple](storsimple-8000-modify-data-0.md) |
| Parar um controlador </br> Reiniciar ou encerrar um controlador </br> Encerrar um dispositivo</br>Repor as predefinições do Olá dispositivo toofactory |[Gerir controladores de dispositivo](storsimple-8000-manage-device-controller.md) |
| Instalar atualizações de modo de manutenção e as correções |[Atualizar o seu dispositivo](storsimple-update-device.md) |
| Introduza o modo de manutenção </br>Modo de manutenção de saída |[Modos de dispositivo do StorSimple](storsimple-8000-device-modes.md) |
| Criar um pacote de suporte</br>Desencriptar e editar um pacote de suporte |[Criar e gerir um pacote de suporte](storsimple-8000-create-manage-support-package.md) |
| Iniciar uma sessão de suporte</br> |[Iniciar uma sessão de suporte no Windows PowerShell para StorSimple](storsimple-8000-create-manage-support-package.md#create-a-support-package) |

## <a name="get-help-in-windows-powershell-for-storsimple"></a>Obter ajuda do Windows PowerShell para StorSimple

No Windows PowerShell para StorSimple, a ajuda do cmdlet está disponível. Uma versão atualizada online desta ajuda também está disponível, que pode utilizar tooupdate Olá ajuda no seu sistema.

Obter ajuda nesta interface é semelhante toothat no Windows PowerShell e, na maioria das Olá relacionadas com a ajuda de cmdlets irá funcionar. Pode encontrar ajuda para o Windows PowerShell online na Biblioteca TechNet do Olá: [Scripting com o Windows PowerShell](http://go.microsoft.com/fwlink/?LinkID=108518).

Olá segue-se uma breve descrição dos tipos de Olá de ajuda para esta interface do Windows PowerShell, incluindo como tooupdate Olá ajuda.

### <a name="tooget-help-for-a-cmdlet"></a>tooget ajuda para um cmdlet

* tooget ajuda para qualquer cmdlet ou uma função, Olá utilize os seguintes comandos:`Get-Help <cmdlet-name>`
* tooget ajuda online para qualquer cmdlet, utilize o cmdlet anterior Olá com Olá `-Online` parâmetro:`Get-Help <cmdlet-name> -Online`
* Para obter ajuda completa, pode utilizar Olá `–Full` parâmetro e para obter exemplos, utilize Olá `–Examples` parâmetro.

### <a name="tooupdate-help"></a>tooupdate ajuda

Pode facilmente atualizar Olá ajuda na interface do Windows PowerShell de Olá. Efetue Olá os seguintes passos tooupdate Olá ajuda no seu sistema.

#### <a name="tooupdate-cmdlet-help"></a>cmdlet tooupdate ajuda
1. Inicie o Windows PowerShell com Olá **executar como administrador** opção.
2. Na linha de comandos Olá, escreva:`Update-Help`
3. Olá atualizados serão instalados os ficheiros de ajuda.
4. Depois de instalar ficheiros de ajuda de Olá, escreva: `Get-Help Get-Command`. Esta ação apresenta uma lista de cmdlets para o qual ajuda está disponível.

> [!NOTE]
> tooget uma lista de todos os cmdlets disponíveis Olá num espaço de execução, inicie sessão toohello opção de menu correspondente e execute Olá `Get-Command` cmdlet.


## <a name="next-steps"></a>Passos seguintes

Se ocorrer algum problema com o dispositivo StorSimple ao efetuar uma das Olá acima fluxos de trabalho, consulte demasiado[ferramentas para resolução de problemas de implementações do StorSimple](storsimple-troubleshoot-deployment.md#tools-for-troubleshooting-storsimple-deployments).

