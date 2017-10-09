---
title: "tooAzure de VMware/físico de falhas de proteção aaaTroubleshoot | Microsoft Docs"
description: "Este artigo descreve falhas de replicação de máquina Olá comuns VMware e como tootroubleshoot-las"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/26/2017
ms.author: asgang
ms.openlocfilehash: b821e9aa2610482ba1900645fb75e75744dc442f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a><span data-ttu-id="922a5-103">Resolver problemas de replicação do servidor de VMware/físico no local</span><span class="sxs-lookup"><span data-stu-id="922a5-103">Troubleshoot on-premises VMware/Physical server replication issues</span></span>
<span data-ttu-id="922a5-104">Poderá receber uma mensagem de erro específico ao proteger as máquinas virtuais VMware ou servidores físicos, utilizando o Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="922a5-104">You may receive a specific error message when protecting your VMware virtual machines or physical servers using Azure Site Recovery.</span></span> <span data-ttu-id="922a5-105">Detalhes deste artigo Olá algumas das mensagens de erro mais comuns encontradas, juntamente com tooresolve passos de resolução de problemas-los.</span><span class="sxs-lookup"><span data-stu-id="922a5-105">This article details some of hello more common error messages encountered, along with troubleshooting steps tooresolve them.</span></span>


## <a name="initial-replication-is-stuck-at-0"></a><span data-ttu-id="922a5-106">A replicação inicial está encravada % 0</span><span class="sxs-lookup"><span data-stu-id="922a5-106">Initial replication is stuck at 0%</span></span>
<span data-ttu-id="922a5-107">A maioria das falhas de replicação inicial de Olá que estamos a encontrar no suporte são devido a problemas de tooconnectivity entre o servidor de processo do servidor de origem ou processo servidor para o Azure.</span><span class="sxs-lookup"><span data-stu-id="922a5-107">Most of hello initial replication failures that we encounter at support are due tooconnectivity issues between source server-to-process server or process server-to-Azure.</span></span>
<span data-ttu-id="922a5-108">Para a maioria dos casos, pode Self-resolver estes problemas, seguindo os passos de Olá listados abaixo.</span><span class="sxs-lookup"><span data-stu-id="922a5-108">For most cases, you can self troubleshoot these issues by following hello steps listed below.</span></span>

###<a name="check-hello-following-on-source-machine"></a><span data-ttu-id="922a5-109">Verifique o seguinte Olá na máquina de origem</span><span class="sxs-lookup"><span data-stu-id="922a5-109">Check hello following on SOURCE MACHINE</span></span>
* <span data-ttu-id="922a5-110">A partir de linha de comandos de máquina do servidor de origem, utilize Telnet tooping Olá servidor de processos com a porta https (predefinição 9443) conforme mostrado abaixo toosee se existem quaisquer problemas de conectividade de rede ou a porta de firewall a bloquear problemas.</span><span class="sxs-lookup"><span data-stu-id="922a5-110">From Source Server machine command line, use Telnet tooping hello Process Server with https port (default 9443) as shown below toosee if there are any network connectivity issues or firewall port blocking issues.</span></span>
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > <span data-ttu-id="922a5-111">Utilizar o Telnet, não utilize a conectividade de tootest PING.</span><span class="sxs-lookup"><span data-stu-id="922a5-111">Use Telnet, don’t use PING tootest connectivity.</span></span>  <span data-ttu-id="922a5-112">Se o Telnet não estiver instalado, siga a lista de passos Olá [aqui](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="922a5-112">If Telnet is not installed, follow hello steps list [here](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span></span>

<span data-ttu-id="922a5-113">Se não é possível tooconnect, permitir que a porta de entrada 9443 no servidor de processos de Olá e verifique se o hello problema ainda sai.</span><span class="sxs-lookup"><span data-stu-id="922a5-113">If unable tooconnect, allow inbound port 9443 on hello Process Server and check if hello problem still exits.</span></span> <span data-ttu-id="922a5-114">Foi alguns casos em que o servidor de processos foi atrás de rede de Perímetro, o qual foi fazendo com que este problema.</span><span class="sxs-lookup"><span data-stu-id="922a5-114">There has been some cases where process server was behind DMZ, which was causing this problem.</span></span>

* <span data-ttu-id="922a5-115">Verificar estado Olá de serviço `InMage Scout VX Agent – Sentinel/OutpostStart` se não estiver em execução e verifique se o problema de Olá ainda existe.</span><span class="sxs-lookup"><span data-stu-id="922a5-115">Check hello status of service `InMage Scout VX Agent – Sentinel/OutpostStart` if it is not running and check if hello problem still exists.</span></span>   
 
###<a name="check-hello-following-on-process-server"></a><span data-ttu-id="922a5-116">Verifique Olá seguinte no servidor de processos</span><span class="sxs-lookup"><span data-stu-id="922a5-116">Check hello following on PROCESS SERVER</span></span>

* <span data-ttu-id="922a5-117">**Verifique se o servidor de processos é enviar ativamente tooAzure de dados**</span><span class="sxs-lookup"><span data-stu-id="922a5-117">**Check if process server is actively pushing data tooAzure**</span></span> 

<span data-ttu-id="922a5-118">A partir da máquina do servidor de processos, abra Olá Gestor de tarefas (prima Ctrl-Shift-Esc).</span><span class="sxs-lookup"><span data-stu-id="922a5-118">From Process Server machine, open hello Task Manager (press Ctrl-Shift-Esc ).</span></span> <span data-ttu-id="922a5-119">Aceda toohello separador de desempenho e clique em ligação de 'Abra Monitor de recursos'.</span><span class="sxs-lookup"><span data-stu-id="922a5-119">Go toohello Performance tab and click ‘Open Resource Monitor’ link.</span></span> <span data-ttu-id="922a5-120">No Gestor de recursos, visite tooNetwork separador. Verifique se cbengine.exe em 'Processos com a atividade de rede' está a enviar ativamente grande volume (em MB) de dados.</span><span class="sxs-lookup"><span data-stu-id="922a5-120">From Resource Manager, go tooNetwork tab. Check if cbengine.exe in ‘Processes with Network Activity’ is actively sending large volume (in Mbs) of data.</span></span>

![Ativar a replicação](./media/site-recovery-protection-common-errors/cbengine.png)

<span data-ttu-id="922a5-122">Se não siga os passos de Olá listados abaixo:</span><span class="sxs-lookup"><span data-stu-id="922a5-122">If not follow hello steps listed below:</span></span>

* <span data-ttu-id="922a5-123">**Verifique se o servidor de processos é capaz de tooconnect Blob do Azure**: selecione e verifique cbengine.exe tooview Olá 'Ligações TCP' toosee se existir conectividade do servidor de processo tooAzure URL de blob de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="922a5-123">**Check if Process server is able tooconnect Azure Blob**: Select and check cbengine.exe tooview hello ‘TCP Connections’ toosee if there is connectivity from Process server tooAzure Storage blob URL.</span></span>

![Ativar a replicação](./media/site-recovery-protection-common-errors/rmonitor.png)

<span data-ttu-id="922a5-125">Se não for, em seguida, aceda tooControl painel > serviços, verifique se Olá os seguintes serviços está em execução:</span><span class="sxs-lookup"><span data-stu-id="922a5-125">If not then go tooControl Panel > Services, check if hello following services are up and running:</span></span>

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
<span data-ttu-id="922a5-126">(Re) Inicie a qualquer serviço que não está em execução e verifique se o problema de Olá ainda existe.</span><span class="sxs-lookup"><span data-stu-id="922a5-126">(Re)Start any service which is not running and check if hello problem still exists.</span></span>

* <span data-ttu-id="922a5-127">**Verifique se o servidor de processos está endereço de IP público tooconnect capaz de tooAzure através da porta 443**</span><span class="sxs-lookup"><span data-stu-id="922a5-127">**Check if Process server is able tooconnect tooAzure Public IP address using port 443**</span></span>

<span data-ttu-id="922a5-128">Abra Olá CBEngineCurr.errlog mais recente do `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` e procure: 443 e ligação tentativa falhada.</span><span class="sxs-lookup"><span data-stu-id="922a5-128">Open hello latest CBEngineCurr.errlog from `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` and search for :443  and connection attempt failed.</span></span>

![Ativar a replicação](./media/site-recovery-protection-common-errors/logdetails1.png)

<span data-ttu-id="922a5-130">Se existirem problemas, em seguida, a partir de linha de comandos do servidor de processos, utilize telnet tooping seu endereço de IP público do Azure (mascarado nos acima imagem) foi encontrado no Olá CBEngineCurr.currLog através da porta 443.</span><span class="sxs-lookup"><span data-stu-id="922a5-130">If there are issues, then from Process Server command line, use telnet tooping your Azure Public IP address (masked in above image) found in hello CBEngineCurr.currLog using port 443.</span></span>

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
<span data-ttu-id="922a5-131">Se forem tooconnect não é possível, em seguida, verifique se o problema de acesso de Olá for devido toofirewall ou Proxy, tal como descrito no passo seguinte.</span><span class="sxs-lookup"><span data-stu-id="922a5-131">If you are unable tooconnect, then check if hello access issue is due toofirewall or Proxy as described in next step.</span></span>


* <span data-ttu-id="922a5-132">**Verifique se firewall de baseadas no endereço IP no servidor de processos não estão a bloquear o acesso**: Se estiver a utilizar um regras de firewall baseadas no endereço IP no servidor de Olá, em seguida, transferir a lista completa de Olá do Microsoft Azure Datacenter intervalos de IP do [aqui ](https://www.microsoft.com/download/details.aspx?id=41653) e adicioná-los tooensure de configuração de firewall de tooyour permitem comunicação tooAzure (e Olá porta HTTPS (443)).</span><span class="sxs-lookup"><span data-stu-id="922a5-132">**Check if IP address-based firewall on Process server are not blocking access**: If you are using an IP address-based firewall rules on hello server, then download hello complete list of Microsoft Azure Datacenter IP Ranges from [here](https://www.microsoft.com/download/details.aspx?id=41653) and add them tooyour firewall configuration tooensure they allow communication tooAzure (and hello HTTPS (443) port).</span></span>  <span data-ttu-id="922a5-133">Permita intervalos de endereços IP para Olá região do Azure da sua subscrição e para EUA oeste (utilizado para gestão de identidade e controlo de acesso).</span><span class="sxs-lookup"><span data-stu-id="922a5-133">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

* <span data-ttu-id="922a5-134">**Verifique se firewall baseada no URL no servidor de processos não está a bloquear o acesso**: Se estiver a utilizar as regras de firewall um URL com base no servidor de Olá, certifique-se de Olá os seguintes URLs é adicionado toofirewall configuração.</span><span class="sxs-lookup"><span data-stu-id="922a5-134">**Check if URL-based firewall on Process server is not blocking access**:  If you are using a URL based firewall rules on hello server, ensure hello following URLs are added toofirewall configuration.</span></span> 
     
  <span data-ttu-id="922a5-135">`*.accesscontrol.windows.net:` Utilizado para controlo de acesso e gestão de identidades</span><span class="sxs-lookup"><span data-stu-id="922a5-135">`*.accesscontrol.windows.net:` Used for access control and identity management</span></span>

  <span data-ttu-id="922a5-136">`*.backup.windowsazure.com:` Utilizado para transferência de dados de replicação e orquestração</span><span class="sxs-lookup"><span data-stu-id="922a5-136">`*.backup.windowsazure.com:` Used for replication data transfer and orchestration</span></span>

  <span data-ttu-id="922a5-137">`*.blob.core.windows.net:`Utilizado para acesso toohello conta de armazenamento que armazena os dados replicados</span><span class="sxs-lookup"><span data-stu-id="922a5-137">`*.blob.core.windows.net:` Used for access toohello storage account that stores replicated data</span></span>

  <span data-ttu-id="922a5-138">`*.hypervrecoverymanager.windowsazure.com:` Utilizado para operações e gestão de replicação e orquestração</span><span class="sxs-lookup"><span data-stu-id="922a5-138">`*.hypervrecoverymanager.windowsazure.com:` Used for replication management operations and orchestration</span></span>

  <span data-ttu-id="922a5-139">`time.nist.gov`e `time.windows.com`: utilizar a sincronização de hora toocheck entre sistema e a hora global.</span><span class="sxs-lookup"><span data-stu-id="922a5-139">`time.nist.gov` and `time.windows.com`: Used toocheck time synchronization between system and global time.</span></span>

<span data-ttu-id="922a5-140">URLs para **Cloud do Azure Government**:</span><span class="sxs-lookup"><span data-stu-id="922a5-140">URLs for **Azure Government Cloud**:</span></span>

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* <span data-ttu-id="922a5-141">**Verifique se as definições de Proxy no servidor de processos não estão a bloquear o acesso**.</span><span class="sxs-lookup"><span data-stu-id="922a5-141">**Check if Proxy Settings on Process server are not blocking access**.</span></span>  <span data-ttu-id="922a5-142">Se estiver a utilizar um servidor Proxy, certifique-se de que está a resolver nome do servidor proxy Olá pelo servidor DNS Olá.</span><span class="sxs-lookup"><span data-stu-id="922a5-142">If you are using a Proxy Server, ensure hello proxy server name is resolving by hello DNS server.</span></span>
<span data-ttu-id="922a5-143">toocheck tiver sido fornecido no momento de Olá do programa de configuração do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="922a5-143">toocheck what you have provided at hello time of Configuration Server setup.</span></span> <span data-ttu-id="922a5-144">Aceda a chave de tooregistry</span><span class="sxs-lookup"><span data-stu-id="922a5-144">Go tooregistry key</span></span>

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

<span data-ttu-id="922a5-145">Certifique-se que Olá as mesmas definições estão a ser utilizadas os dados de toosend de agente do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="922a5-145">Now ensure that hello same settings are being used by Azure Site Recovery agent toosend data.</span></span>
<span data-ttu-id="922a5-146">Cópia de segurança do Microsoft Azure Search</span><span class="sxs-lookup"><span data-stu-id="922a5-146">Search Microsoft Azure  Backup</span></span> 

![Ativar a replicação](./media/site-recovery-protection-common-errors/mab.png)

<span data-ttu-id="922a5-148">Abra-o e clique na ação > alterar propriedades.</span><span class="sxs-lookup"><span data-stu-id="922a5-148">Open it and click on Action > Change Properties.</span></span> <span data-ttu-id="922a5-149">No separador de configuração de Proxy, deverá ver o endereço de proxy de Olá, que deve ser a mesmo, conforme ilustrado pelas definições de registo Olá.</span><span class="sxs-lookup"><span data-stu-id="922a5-149">Under Proxy Configuration tab, you should see hello proxy address, which should be same as shown by hello registry settings.</span></span> <span data-ttu-id="922a5-150">Se não estiver, altere-toohello mesmo endereço.</span><span class="sxs-lookup"><span data-stu-id="922a5-150">If not, please change it toohello same address.</span></span>

![Ativar a replicação](./media/site-recovery-protection-common-errors/mabproxy.png)

* <span data-ttu-id="922a5-152">**Verifique se a largura de banda de limitação não é restrita no servidor de processos**: aumentar Olá largura de banda e verifique se o problema de Olá ainda existe.</span><span class="sxs-lookup"><span data-stu-id="922a5-152">**Check if Throttle bandwidth is not constrained on Process server**:  Increase hello bandwidth  and check if hello problem still exists.</span></span>

##<a name="next-steps"></a><span data-ttu-id="922a5-153">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="922a5-153">Next steps</span></span>
<span data-ttu-id="922a5-154">Se precisar de mais ajuda, em seguida, após a sua consulta demasiado[fórum de ASR](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="922a5-154">If you need more help, then post your query too[ASR forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span></span> <span data-ttu-id="922a5-155">Temos uma Comunidade de Active Directory e um dos nossos engenheiros será capaz de tooassist.</span><span class="sxs-lookup"><span data-stu-id="922a5-155">We have an active community and one of our engineers will be able tooassist you.</span></span>
