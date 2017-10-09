---
title: "resolução de recuperação de Site aaaAzure do VMware tooAzure | Microsoft Docs"
description: "Resolução de problemas de erros quando replicar máquinas virtuais do Azure"
services: site-recovery
documentationcenter: 
author: asgang
manager: srinathv
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/24/2017
ms.author: asgang
ms.openlocfilehash: 912097c8892540dd798ba025e0b10374ca51d664
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-mobility-service-push-install-issues"></a>Resolução de problemas de instalação de push do serviço de mobilidade

Este artigo fornece detalhes sobre problemas comuns de Olá deparam quando tenta tooinstall Olá serviço de mobilidade no servidor de toosource para ativar a proteção.

## <a name="error-code-95107-protection-could-not-be-enabled"></a>(Código de erro 95107) Não foi possível ativar a proteção.
**Código de erro** | **Causas possíveis** | **Recomendações de erro específico**
--- | --- | ---
95107 </br>***Mensagem -*** falha na instalação de Push Olá mobilidade serviço toohello da máquina de origem com o código de erro ***EP0858***. <br> O que as credenciais de Olá fornecido tooinstall serviço de mobilidade está incorreto ou conta de utilizador Olá tem privilégios insuficientes | As credenciais de utilizador fornecido tooinstall o serviço de mobilidade na máquina de origem está incorreto | Certifique-se de que as credenciais de utilizador de Olá fornecidas Olá máquina de origem no servidor de configuração estão corretas. <br> tooadd/editar credenciais de utilizador: servidor tooconfiguration aceda > Cspsconfigtool ícone > Gerir a conta. </br> Além disso, certifique-se abaixo pré-requisitos são toosuccessfully marcada completas de instalação de emissão.

## <a name="error-code-95015-protection-could-not-be-enabled"></a>(Código de erro 95015) Não foi possível ativar a proteção.
**Código de erro** | **Causas possíveis** | **Recomendações de erro específico**
--- | --- | ---
95105 </br>***Mensagem -*** falha na instalação de Push Olá mobilidade serviço toohello da máquina de origem com o código de erro ***EP0856***. <br> Não "E impressoras da partilha de ficheiros" permitido na máquina de origem hello, ou existem problemas de conectividade de rede entre o servidor de processos de Olá e a máquina de origem Olá| Impressão de partilha de ficheiros e não está ativado | Permitir "E impressoras da partilha de ficheiros" na máquina de origem Olá Olá Firewall do Windows, aceda máquina de origem de toohello > definições da Firewall do Windows em > "Permitir que uma aplicação ou funcionalidade através da Firewall" > selecione "Ficheiros e partilha de impressoras para todos os perfis". </br> Além disso, certifique-se abaixo pré-requisitos são toosuccessfully marcada completas de instalação de emissão.

## <a name="error-code-95117-protection-could-not-be-enabled"></a>(Código de erro 95117) Não foi possível ativar a proteção.
**Código de erro** | **Causas possíveis** | **Recomendações de erro específico**
--- | --- | ---
95117 </br>***Mensagem -*** falha na instalação de Push Olá mobilidade serviço toohello da máquina de origem com o código de erro ***EP0865***. <br> A máquina de origem Olá não está em execução ou existem problemas de conectividade de rede entre o servidor de processos de Olá e a máquina de origem Olá | Conectividade de rede entre o servidor de processos e o servidor de origem | Verifique a conectividade entre o servidor de processos e o servidor de origem. </br> Além disso, certifique-se abaixo pré-requisitos são toosuccessfully marcada completas de instalação de emissão.

## <a name="error-code-95103-protection-could-not-be-enabled"></a>(Código de erro 95103) Não foi possível ativar a proteção.
**Código de erro** | **Causas possíveis** | **Recomendações de erro específico**
--- | --- | ---
95103 </br>***Mensagem -*** falha na instalação de Push Olá mobilidade serviço toohello da máquina de origem com o código de erro ***EP0854***. <br> "Windows Management Instrumentation (WMI)" não é permitida na máquina de origem hello, ou existem problemas de conectividade de rede entre o servidor de processos de Olá e a máquina de origem Olá| Windows Management Instrumentation (WMI) bloqueadas no Olá Firewall do Windows | Permitir que o Windows Management Instrumentation (WMI) no Olá Firewall do Windows. Em definições de Firewall do Windows > "Permitir que uma aplicação ou funcionalidade através da Firewall" > "selecionar WMI em todos os perfis". </br> Além disso, certifique-se abaixo pré-requisitos são toosuccessfully marcada completas de instalação de emissão.

## <a name="check-push-install-logs-for-errors"></a>Verifique se existem erros registos de instalação Push

No servidor de configuração/processe Olá, navegue até toofile 'PushinstallService' localizado em <Microsoft Azure Site Recovery Install Location>\home\svsystems\pushinstallsvc\ toounderstand Olá origem problema Olá e utilize abaixo problema de Olá tooresolve de passos de resolução de problemas.</br>
![pushiinstalllogs](./media/site-recovery-protection-common-errors/pushinstalllogs.png)

## <a name="push-install-pre-requisites-for-windows"></a>Instalação de push pré-requisitos para o Windows
### <a name="ensure-file-and-printer-sharing-is-enabled"></a>Certifique-se de que "E impressoras da partilha de ficheiros" está ativada
Permitir "E impressoras da partilha de ficheiros" e "Windows Management Instrumentation" na máquina de origem Olá no Olá Firewall do Windows </br>
#### <a name="if-source-machine-is-domain-joined-br"></a>Se a máquina de origem estiver associado a um domínio: </br>
Configure as definições da firewall utilizando a consola de gestão de políticas de grupo (GPMC).
1. Domínio do início de sessão tooActive do computador como administrador e abra a consola de gestão de políticas de grupo (GPMC. MSC, execute a partir de um início > executar).</br>
3. Se o GPMC não estiver instalado, siga a ligação de Olá demasiado[instalação Olá GPMC](https://technet.microsoft.com/library/cc725932.aspx) </br>
4. Na árvore de consola do Olá GPMC, faça duplo clique em objetos de política de grupo no domínio e floresta Olá e navegue demasiado "Política de domínio predefinida". </br>
![gpmc1](./media/site-recovery-protection-common-errors/gpmc1.png) </br>
</br>
5. Faça duplo clique em "Política de domínio predefinida" > Editar > será aberta uma nova janela de "Editor de gestão de políticas de grupo". </br>
![gpmc2](./media/site-recovery-protection-common-errors/gpmc2.png) </br>
</br>
6. No Editor de gestão de políticas de grupo de Olá navegue tooComputer configuração > políticas > modelos administrativos > rede > ligações de rede > Firewall do Windows. </br>
![gpmc3](./media/site-recovery-protection-common-errors/gpmc3.png) </br>
</br>
7. Ativar Olá seguir as definições de perfil de domínio e o perfil padrão </br>
a) faça duplo clique na exceção de "Firewall do Windows: permitir exceção de partilha de impressoras e ficheiros de entrada". Selecione ativado e clique em OK. </br>
b) faça duplo clique na exceção de "Firewall do Windows: permitir exceção de entrada de administração remota". Selecione ativado e clique em OK. </br>
![gpmc4](./media/site-recovery-protection-common-errors/gpmc4.png) </br>
</br>

###### <a name="if-source-machine-is-not-domain-joined-and-part-of-workgroup-br"></a>Se a máquina de origem não está associado a um domínio e parte do grupo de trabalho </br>
Configure as definições da firewall no computador remoto (para o grupo de trabalho):
1. Aceda a máquina de origem toohello,</br>
2. Em definições de Firewall do Windows > "Permitir que uma aplicação ou funcionalidade através da Firewall" > selecione "Ficheiros e partilha de impressoras para todos os perfis". </br>
3. Em definições de Firewall do Windows > "Permitir que uma aplicação ou funcionalidade através da Firewall" > "selecionar WMI em todos os perfis". </br>

#### <a name="disable-remote-user-account-control-uac"></a>Desative o controlo remoto de conta de utilizador (UAC)
Desative UAC com o serviço de mobilidade de Olá de toopush chave de registo.
1. Clique em Iniciar > executar > escreva regedit > ENTER
2. Localize e, em seguida, clique em Olá seguinte subchave de registo: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System
3. Se não existir Olá LocalAccountTokenFilterPolicy entrada de registo, siga estes passos:
4. No menu de edição Olá > novo > clique valor DWORD.
5. Escreva LocalAccountTokenFilterPolicy e, em seguida, prima ENTER.
6. Faça duplo clique LocalAccountTokenFilterPolicy e, em seguida, clique em modificar.
7. Na caixa de dados de valor de Olá, escreva a 1 e, em seguida, clique em OK.
8. Editor de registo de saída.


## <a name="push-install-pre-requisites-for-linux"></a>Push instalar pré-requisitos para Linux:

1. Crie um utilizador de raiz no servidor de Linux Olá origem. (Utilize esta conta apenas para a instalação de push Olá e para atualizações)</br>
2. Verifique se o ficheiro /etc/hosts Olá na origem de Olá Linux server tem entradas que mapeiam os endereços de tooIP Olá local hostname associados a todas as placas de rede. </br>
3. Certifique-se de pacotes de openssh, servidor openssh e openssl mais recentes no Olá estão instalados no servidor de Linux de origem. </br>
Verifique se o ssh porta 22 está ativado e em execução. </br>
4. Verifique se obsoleta entradas de agentes já estejam presentes no servidor de origem Olá, desinstalar agentes de mais antigos do Olá e reinicie o servidor de Olá, reinstale o agente. </br>

#### <a name="enable-sftp-subsystem-and-password-authentication-in-hello-sshdconfig-file"></a>Ativar a autenticação de subsistema e a palavra-passe SFTP no ficheiro de sshd_config Olá
1. No servidor de origem, inicie sessão como raiz. </br>
2. No ficheiro de /etc/ssh/sshd_config de ficheiro Olá,</br> Localize Olá linha que começa com PasswordAuthentication. </br>
3. d.   Anule os comentários linha Olá e altere o valor de Olá de "não" demasiado "Sim". </br>
![Linux1](./media/site-recovery-protection-common-errors/linux1.png)
4. Localize a linha Olá que comece com ". o subsistema" e anule os comentários linha Olá. </br>
![Linux2](./media/site-recovery-protection-common-errors/linux2.png)
5. Guardar as alterações de Olá e reinicie o serviço de sshd Olá. </br>

## <a name="push-installation-checks-on-configurationprocess-server"></a>Verificações de instalação no servidor de configuração/processe de emissão.
#### <a name="validate-credentials-for-discovery-and-installation"></a>Validar as credenciais para deteção e instalação

1. Servidor de configuração, iniciar Cspsconfigtool</br>
![WMItestConnect5](./media/site-recovery-protection-common-errors/wmitestconnect5.png) </br>

2. Certifique-se de que conta Olá utilizada para proteção com direitos de administrador na máquina de origem Olá. </br>

#### <a name="check-connectivity-between-process-server-and-source-server"></a>Verifique a conectividade entre o servidor de processos e o servidor de origem
1. Certifique-se de que o servidor de processos tem ligação à internet.
2. Certifique-se a ligação ao WMI wbemtest.exe a utilizar. </br>
No servidor de processos de Olá, clique em Iniciar > executar > wbemtest.exe > será possível abrir a janela de recurso de teste do Windows Management Instrumentation conforme mostrado.</br>
   ![WMItestConnect1](./media/site-recovery-protection-common-errors/wmitestconnect1.png) </br>
   </br>
Clique em ligar > introduza Olá IP do servidor de origem no nome de utilizador de entrada do espaço de nomes de Olá e a palavra-passe (se o computador de origem estiver associado a um domínio, forneça Olá o nome de domínio, juntamente com o nome de utilizador como "domainName\username". Se a máquina de origem no grupo de trabalho, fornecer apenas o nome de utilizador Olá.) Selecione o nível de autenticação de Olá como privacidade de pacote. </br>
![WMItestConnect2](./media/site-recovery-protection-common-errors/wmitestconnect2.png) </br>
   </br>
   Clique em ligar. Agora a ligação ao WMI Olá deve ser efetuada com êxito com Olá fornecida dados e deverá ser apresentada a janela de recurso de teste do Windows Management Instrumentation Olá conforme mostrado abaixo: </br>
   ![WMItestConnect3](./media/site-recovery-protection-common-errors/wmitestconnect3.png) </br>
</br>
   Se não for bem sucedida ligação ao WMI haverá uma mensagem de erro pop-up. Olá abaixo captura de ecrã mostra uma tentativa sem êxito se administração WMI/remota não está ativada na firewall do Windows permitido aplicação. </br>
   ![WMItestConnect4](./media/site-recovery-protection-common-errors/wmitestconnect4.png) </br>
</br>

3. Verificar o estado do WMI Olá e conectividade.</br>
No servidor de configuração/processe Olá, </br>
Clique em Iniciar > executar > wmimgmt.msc > ações > mais ações > ligar computador tooanother (máquina de origem). </br>
Introduza as credenciais de Olá de Olá da conta utilizada para proteção e verifique se a conectividade for adequada. </br>

#### <a name="verify-network-shared-folders-of-source-machine-is-accessible-from-process-server-ps-remotely-using-specified-credentials"></a>Certifique-se de que as pastas partilhadas na rede da máquina de origem está acessível a partir do processo de servidor (PS) remotamente utilizando as credenciais especificadas.
  1. Computador de servidor (PS) tooProcess de início de sessão, abra o Explorador de ficheiros > no tipo de barra de endereço Olá > "\\\source-machine-ip\C$" > clique em Enter. </br>
  ![Fileshare1](./media/site-recovery-protection-common-errors/fileshare1.png) </br>
  2. Explorador de ficheiros irá solicitar credenciais. Introduza Olá nome de utilizador e palavra-passe > clique em OK.</br>
   Se a máquina de origem estiver associado a um domínio, forneça o nome de domínio de Olá, juntamente com o nome de utilizador como "domainName\username".</br>
   Se a máquina de origem no grupo de trabalho, fornecem apenas Olá "nomedeutilizador". </br>
  ![Fileshare2](./media/site-recovery-protection-common-errors/fileshare2.png) </br>
  3. Se a ligação for bem-sucedida, pode ver pastas Olá da máquina de origem remotamente do processo de servidor (PS) </br>
  ![Fileshare3](./media/site-recovery-protection-common-errors/fileshare3.png) </br>

> [!NOTE] 
> Se a ligação for bem-sucedida, verifique se todos os pré-requisitos são cumpridos.
>

Se não quiser tooopen "Windows Management Instrumentation", também pode instalar o serviço de mobilidade manualmente na máquina de origem Olá.</br> [Instalar o serviço de mobilidade manualmente através da GUI](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) </br>
[Instalação através da documentação de orientação do configuration manager](site-recovery-install-mobility-service-using-sccm.md) </br>

## <a name="next-steps"></a>Passos seguintes
- [Ativar a replicação para máquinas virtuais VMware](vmware-walkthrough-enable-replication.md)
