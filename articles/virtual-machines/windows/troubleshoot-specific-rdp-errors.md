---
title: mensagens de erro aaaSpecific RDP para as VMs do Azure | Microsoft Docs
description: "Compreender as mensagens de erro específicas que poderá receber quando tenta utilizam a máquina virtual do ambiente de trabalho remoto ligação tooa Windows no Azure"
keywords: "Erro de ambiente de trabalho remoto, erro de ligação de ambiente de trabalho remoto, não é possível ligar tooVM, resolução de ambiente de trabalho remoto"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 5feb1d64-ee6f-4907-949a-a7cffcbc6153
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 8e1551be23e696bd60adbd76c3e1ea86d9dd11aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-specific-rdp-error-messages-tooa-windows-vm-in-azure"></a>Resolução de problemas específico RDP erro mensagens tooa VM do Windows no Azure
Poderá receber uma mensagem de erro específico ao utilizar a máquina de virtual do Windows de tooa de ligação de ambiente de trabalho remoto (VM) no Azure. Detalhes deste artigo Olá algumas das mensagens de erro mais comuns encontradas, juntamente com tooresolve passos de resolução de problemas-los. Se estiver a ter problemas em ligar tooyour VM através de RDP mas efetue não encontrar uma mensagem de erro específica, consulte Olá [guia para o ambiente de trabalho remoto de resolução de problemas](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Para informações sobre mensagens de erro específicas, consulte o seguinte Olá:

* [a sessão remota Olá foi desligada porque não existem nenhum tooprovide disponível de servidores de licenciamento de ambiente de trabalho remotos uma licença](#rdplicense).
* [Ambiente de trabalho remoto não é possível localizar Olá "" nome do computador](#rdpname).
* [Ocorreu um erro de autenticação. Olá autoridade de segurança Local não pode ser contactada](#rdpauth).
* [Erro de segurança do Windows: as suas credenciais não foi possível funcionar](#wincred).
* [Este computador não é possível ligar o computador remoto toohello](#rdpconnect).

<a id="rdplicense"></a>

## <a name="hello-remote-session-was-disconnected-because-there-are-no-remote-desktop-license-servers-available-tooprovide-a-license"></a>a sessão remota Olá foi desligada porque não existem nenhum tooprovide disponível uma licença de servidores de licenciamento de ambiente de trabalho remoto.
Causa: o período de tolerância de licenciamento de 120 dias do Olá para a função de servidor de ambiente de trabalho remoto Olá expirou e tem de tooinstall licenças.

Como solução, guarde uma cópia local do ficheiro RDP Olá do portal de Olá e execute este comando um tooconnect de linha de comandos do PowerShell. Este passo desativa o licenciamento de apenas essa ligação:

        mstsc <File name>.RDP /admin

Se, na verdade, não precisa de mais de dois em simultâneo ambiente de trabalho remoto ligações toohello VM, pode utilizar a função de servidor de ambiente de trabalho remoto do Gestor de servidor tooremove Olá.

Para obter mais informações, consulte a mensagem de blogue de Olá [VM do Azure falha com "Nenhum ambiente de trabalho licenças servidores remotos disponíveis"](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).

<a id="rdpname"></a>

## <a name="remote-desktop-cant-find-hello-computer-name"></a>Ambiente de trabalho remoto não é possível localizar o computador de Olá "name".
Causa: cliente de ambiente de trabalho remoto Olá no seu computador não é possível resolver o nome de Olá do computador de Olá nas definições de Olá dos ficheiros RDP Olá.

Possíveis soluções:

* Se estiver na intranet da organização, certifique-se de que o computador tem acesso toohello proxy servidor e pode enviar tooit de tráfego HTTPS.
* Se estiver a utilizar um ficheiro RDP armazenado localmente, experimente utilizar Olá um que é gerado pelo portal Olá. Este passo garante que tem Olá nome de DNS correto para Olá máquina virtual ou serviço em nuvem de Olá e a porta de ponto final de Olá de Olá VM. Segue-se um ficheiro RDP de exemplo gerado pelo portal Olá:
  
        full address:s:tailspin-azdatatier.cloudapp.net:55919
        prompt for credentials:i:1

Tem a parte do endereço Olá deste ficheiro RDP:

* Olá nome de domínio do serviço em nuvem Olá que contém Olá VM ("tailspin-azdatatier.cloudapp.net" neste exemplo) completamente qualificado.
* Olá externa a porta TCP de Olá ponto final para o tráfego de ambiente de trabalho remoto (55919).

<a id="rdpauth"></a>

## <a name="an-authentication-error-has-occurred-hello-local-security-authority-cannot-be-contacted"></a>Ocorreu um erro de autenticação. Não é possível contactar o Olá autoridade de segurança Local.
Causa: o destino de Olá VM não é possível localizar autoridade de segurança de Olá na parte de nome de utilizador Olá das credenciais.

Quando o seu nome de utilizador está no formato de Olá *SecurityAuthority*\\*UserName* (exemplo: CORP\User1), Olá *SecurityAuthority* parte é o Olá VM nome do computador (para a autoridade de segurança local Olá) ou um nome de domínio do Active Directory.

Possíveis soluções:

* Se a conta de Olá local toohello VM, certifique-se de que nome da VM Olá está escrito corretamente.
* Se a conta de Olá estiver num domínio do Active Directory, verifique a ortografia Olá Olá do nome de domínio.
* Se for uma conta de domínio do Active Directory e Olá nome de domínio está escrito corretamente, certifique-se de que está disponível um controlador de domínio nesse domínio. É um problema comum verificado em redes virtuais do Azure que contém os controladores de domínio que um controlador de domínio está indisponível porque não foi iniciado. Como solução, pode utilizar uma conta de administrador local em vez de uma conta de domínio.

<a id="wincred"></a>

## <a name="windows-security-error-your-credentials-did-not-work"></a>Erro de segurança do Windows: não foi possível funcionar as suas credenciais.
Causa: o destino de Olá VM não é possível validar o nome de conta e palavra-passe.

Um computador baseado em Windows pode validar Olá as credenciais de uma conta local ou uma conta de domínio.

* Para contas locais, utilize Olá *ComputerName*\\*UserName* sintaxe (exemplo: SQL1\Admin4798).
* Para contas de domínio, utilize Olá *DomainName*\\*UserName* sintaxe (exemplo: CONTOSO\peterodman).

Se tiver promovido a controlador de domínio de tooa VM numa nova floresta do Active Directory, a conta de administrador local Olá que iniciou sessão com é convertida tooan equivalente conta com Olá mesma palavra-passe no Olá nova floresta e domínio. conta local Olá, em seguida, é eliminada.

Por exemplo, se tiver iniciado sessão com a conta local do Olá DC1\DCAdmin e, em seguida, promovido Olá máquina como um controlador de domínio numa floresta nova para o domínio da corp.contoso.com de Olá, Olá DC1\DCAdmin conta local é eliminada e uma nova conta de domínio (CORP\DCAdmin ) é criado com Olá mesma palavra-passe.

Certifique-se de que nome da conta Olá é um nome que a máquina virtual de Olá pode verificar como uma conta válida, e essa palavra-passe de Olá está correto.

Se precisar de palavra-passe de Olá de toochange da conta de administrador local Olá, consulte [como serviço tooreset uma palavra-passe ou Olá ambiente de trabalho remoto para máquinas virtuais Windows](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

<a id="rdpconnect"></a>

## <a name="this-computer-cant-connect-toohello-remote-computer"></a>Este computador não é possível ligar o computador remoto toohello.
Causa: a conta Olá que tenha utilizado tooconnect não tem direitos de início de sessão de ambiente de trabalho remoto.

Cada computador com o Windows tem um grupo de local da utilizadores ambiente de trabalho remoto, que contém as contas de Olá e grupos que podem iniciar sessão no-lo remotamente. Os membros do grupo de administradores locais Olá têm também acesso, mesmo que essas contas não estão listadas no grupo local de utilizadores do ambiente de trabalho remoto de Olá. Para máquinas associados a um domínio, o grupo de administradores locais Olá também contém os administradores do domínio Olá para o domínio de Olá.

Certifique-se de que a conta de Olá que estiver a utilizar tooconnect com tem direitos de início de sessão de ambiente de trabalho remoto. Como solução, utilize um domínio ou tooconnect de conta de administrador local através de ambiente de trabalho remoto. tooadd Olá o grupo de utilizadores de ambiente de trabalho remoto toohello do pretendido conta local, utilizar o snap-in Consola de gestão da Microsoft de Olá (**ferramentas do sistema > utilizadores e grupos locais > grupos > Remote Desktop Users**).

## <a name="next-steps"></a>Passos seguintes
Se nenhum destes erros ocorreu e tem um problema com a ligação através de RDP desconhecido, consulte Olá [guia para o ambiente de trabalho remoto de resolução de problemas](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* Para aceder a aplicações em execução numa VM passos de resolução de problemas, consulte [aplicação tooan acesso de resolução de problemas em execução numa VM do Azure](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Se estiver a ter problemas utilizando Secure Shell (SSH) tooconnect tooa VM com Linux no Azure, consulte [resolver problemas de SSH ligações tooa VM com Linux no Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

