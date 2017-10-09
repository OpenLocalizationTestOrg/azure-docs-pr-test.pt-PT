---
title: "aaaManaging recomendações de segurança no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento explica como como recomendações no Centro de segurança do Azure ajudam a proteger os recursos do Azure e a manter em conformidade com as políticas de segurança."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 86c50c9f-eb6b-4d97-acb3-6d599c06133e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: f6bbe36a7a5636095b339b3e9765b87cc0ab669a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-security-recommendations-in-azure-security-center"></a>Gerir recomendações de segurança no Centro de segurança do Azure
Este documento explica-lhe como toouse recomendações no Centro de segurança do Azure toohelp proteger os recursos do Azure.

> [!NOTE]
> Este documento apresenta serviço Olá utilizando um exemplo de implementação.  Este documento não é um guia passo a passo.
>
>

## <a name="what-are-security-recommendations"></a>Quais são recomendações de segurança?
Centro de segurança analisa periodicamente o estado de segurança de Olá dos seus recursos Azure. Quando o Centro de Segurança identifica potenciais vulnerabilidades de segurança, cria recomendações. recomendações de Olá ajudá-lo através do processo de Olá de configurar os controlos de Olá necessário.

## <a name="implementing-security-recommendations"></a>Implementar recomendações de segurança
### <a name="set-recommendations"></a>Recomendações de conjunto
No [definir políticas de segurança no Centro de segurança do Azure](security-center-policies.md), saiba como:

* Configure políticas de segurança.
* Ative a recolha de dados.
* Escolha qual toosee recomendações como parte da sua política de segurança.

System center de recomendações de política em torno de atualizações do sistema, as regras de linha de base, programas antimalware, [grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md) em sub-redes e interfaces de rede, a auditoria de base de dados SQL, encriptação de dados transparente de base de dados do SQL Server, e firewalls de aplicação web.  [Definir políticas de segurança](security-center-policies.md) fornece uma descrição de cada opção de recomendação.

### <a name="monitor-recommendations"></a>Recomendações de monitor
Depois de definir uma política de segurança, o Centro de segurança analisa o estado de segurança de Olá dos seus recursos tooidentify potenciais vulnerabilidades. Olá **recomendações** mosaico Olá **Centro de segurança** painel permite-lhe saber o número total de Olá recomendações identificadas pelo centro de segurança.

![Recomendações de mosaico][1]

detalhes de Olá toosee cada recomendação:

Selecione Olá **recomendações mosaico** no Olá **Centro de segurança** painel. Olá **recomendações** abre o painel.

recomendações de Olá são apresentadas num formato de tabela em que cada linha representa uma recomendação específica. Olá colunas desta tabela estão:

* **Descrição**: explica recomendação Olá e de que precisa de toobe feito tooaddress-lo.
* **RECURSO**: apresenta uma lista de Olá recursos toowhich se aplica esta recomendação.
* **ESTADO**: descreve Olá estado atual da recomendação Olá:
  * **Abra**: Olá recomendação ainda não foi tratada.
  * **Em curso**: recomendação Olá está atualmente a ser aplicada toohello recursos e é necessária nenhuma ação por si.
  * **Resolvido**: recomendação Olá já foi concluída (neste caso, linha Olá fica a cinzento).
* **GRAVIDADE**: descreve Olá gravidade dessa recomendação específica:
  * **Elevada**: uma vulnerabilidade existe com um recurso significativo (por exemplo, uma aplicação, uma VM ou um grupo de segurança de rede) e necessita de atenção.
  * **Média**: uma vulnerabilidade existe e passos não críticos ou adicionais são necessária tooeliminate-lo ou toocomplete um processo.
  * **Baixa**: uma vulnerabilidade existe que deve ser tratada, mas não necessita de atenção imediata. (Por predefinição, as recomendações baixas não são apresentadas, mas pode filtrar por recomendações baixas se pretender toosee-los.)

Tabela de Olá de utilização abaixo como uma referência toohelp compreender recomendações disponíveis Olá e que cada um faz se aplicá-lo.

> [!NOTE]
> Pretende que toounderstand Olá [clássica e modelos de implementação do Resource Manager](../azure-classic-rm.md) para recursos do Azure.
>
>

| Recomendação | Descrição |
| --- | --- |
| [Ativar a recolha de dados para subscrições](security-center-enable-data-collection.md) |Recomenda-se que ative a recolha de dados na política de segurança de Olá para cada uma das suas subscrições e todas as máquinas virtuais (VMs) nas suas subscrições. |
| [Remediar vulnerabilidades do SO](security-center-remediate-os-vulnerabilities.md) |Recomenda que cumprir as configurações de SO Olá recomendada as regras de configuração, por exemplo, não permitir toobe de palavras-passe guardada. |
| [Aplicar atualizações do sistema](security-center-apply-system-updates.md) |Recomenda-se de que implemente tooVMs atualizações críticas e de segurança de sistema em falta. |
| [Aplicar um Just-In-Time controlo de acesso de rede](security-center-just-in-time.md) | Recomenda-se de que se aplicam apenas no acesso VM de tempo. Olá apenas na funcionalidade de tempo está em pré-visualização e está disponível no Olá escalão Standard do Centro de segurança. Consulte [preços](security-center-pricing.md) toolearn mais acerca do Centro de segurança do escalões de preço. |
| [Reiniciar após atualizações do sistema](security-center-apply-system-updates.md#reboot-after-system-updates) |Recomenda-se de que reiniciar um processo de Olá toocomplete VM de aplicar atualizações do sistema. |
| [Adicionar uma firewall de aplicação Web](security-center-add-web-application-firewall.md) |Recomenda-se de que irá implementar uma firewall de aplicação web (WAF) para pontos finais do web. É apresentada uma recomendação WAF para qualquer destinado ao IP público (IP de nível de instância ou IP com balanceamento de carga) que tenha um grupo de segurança de rede associada com portas web de entrada aberta (80,443). </br>Centro de segurança recomenda que aprovisionar um toohelp WAF se Defender contra ataques direcionada para as aplicações web em máquinas virtuais e no ambiente de serviço de aplicações. Aplicação serviço de ambiente (ASE) é um [Premium](https://azure.microsoft.com/pricing/details/app-service/) service opção plano do App Service do Azure fornece um ambiente completamente isolado e dedicado para execução segura de aplicações do App Service do Azure. toolearn mais informações sobre ASE, consulte Olá [a documentação de ambiente de serviço de aplicação](../app-service/app-service-app-service-environments-readme.md).</br>Pode proteger várias aplicações web no Centro de segurança ao adicionar estas aplicações tooyour WAF as implementações existentes. |
| [Finalizar a proteção das aplicações](security-center-add-web-application-firewall.md#finalize-application-protection) |configuração de Olá de toocomplete de uma WAF, o tráfego deve ser reencaminhado toohello WAF aplicação. Seguir esta recomendação conclui as alterações de configuração necessários de Olá. |
| [Adicionar uma Firewall da Próxima Geração](security-center-add-next-generation-firewall.md) |Recomenda-se de que adiciona uma Firewall seguinte de geração (NGFW) de um tooincrease de parceiro da Microsoft proteções de segurança. |
| [Encaminhar o tráfego apenas através da NGFW](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |Recomenda-se de que configura regras de grupo (NSG) de segurança de rede forçar o tráfego de entrada tooyour VM através do seu NGFW. |
| [Instalar o Endpoint Protection](security-center-install-endpoint-protection.md) |Recomenda-se de que aprovisionar tooVMs de programas antimalware (apenas para VMs do Windows). |
| [Resolver alertas de estado de funcionamento do Endpoint Protection](security-center-resolve-endpoint-protection-health-alerts.md) |Recomenda-se que resolva falhas de proteção do ponto final. |
| [Ativar grupos de segurança de rede em sub-redes ou máquinas virtuais](security-center-enable-network-security-groups.md) |Recomenda-se que ative NSGs em sub-redes ou VMs. |
| [Restringir o acesso através da Internet com o ponto final](security-center-restrict-access-through-internet-facing-endpoints.md) |Recomenda-se de que configura as regras de tráfego de entrada para os NSGs. |
| [Ativar a auditoria e a deteção de ameaças em servidores SQL](security-center-enable-auditing-on-sql-servers.md) |Recomenda-se que ative a auditoria e deteção de ameaças para servidores SQL do Azure. (Apenas para serviço do SQL do azure. Não inclui o SQL Server em execução em máquinas virtuais.) |
| [Ativar a auditoria e a deteção de ameaças nas bases de dados SQL](security-center-enable-auditing-on-sql-databases.md) |Recomenda-se que ative a auditoria e deteção de ameaças para bases de dados SQL do Azure. (Apenas para serviço do SQL do azure. Não inclui o SQL Server em execução em máquinas virtuais.) |
| [Ativar a encriptação transparente de dados nas bases de dados do SQL Server](security-center-enable-transparent-data-encryption.md) |Recomenda-se de que permitem a encriptação de bases de dados do SQL Server. (Apenas serviço SQL do azure.) |
| [Ativar o Agente de VM](security-center-enable-vm-agent.md) |Permite toosee que necessite de VMs Olá agente da VM. Olá agente da VM tem de ser instalado em VMs tooprovision patch análise, a linha de base de análise e programas antimalware. Olá agente VM está instalado por predefinição para as VMs que são implementadas a partir de Olá Azure Marketplace. artigo de Olá [extensões – parte 2 e o agente da VM](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) fornece informações sobre como tooinstall Olá agente da VM. |
| [Aplicar encriptação de discos](security-center-apply-disk-encryption.md) |Recomenda-se que encripte os discos da VM com o Azure Disk Encryption (VMs Windows e Linux). Encriptação é recomendada para Olá SO e volumes de dados na VM. |
| [Disponibilizar detalhes de contacto de segurança](security-center-provide-security-contact-details.md) |Recomenda que fornece segurança de informações de contacto para cada uma das suas subscrições. Informações de contacto são um número de telefone e endereço de e-mail. Olá informações são toocontact utilizado se a nossa equipa de segurança localiza a que os recursos sejam comprometidos. |
| [Atualizar a versão do SO](security-center-update-os-version.md) |Recomenda-se de que atualizar a versão do sistema operativo (SO) de Olá para o serviço em nuvem toohello versão mais recente disponível para a sua família de SO.  toolearn mais informações sobre serviços em nuvem, consulte Olá [descrição geral dos serviços de nuvem](../cloud-services/cloud-services-choose-me.md). |
| [Avaliação de vulnerabilidades não instalada](security-center-vulnerability-assessment-recommendations.md) |Recomenda-se de que instala uma solução de avaliação de vulnerabilidades na sua VM. |
| [Remediar vulnerabilidades](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Permite-lhe a vulnerabilidades de sistema e de aplicações do toosee detetadas pela solução de avaliação de vulnerabilidade de Olá instalada na VM. |
| [Ativar a encriptação da conta de armazenamento do Azure](security-center-enable-encryption-for-storage-account.md) | Recomenda-se de ativar a encriptação do serviço de armazenamento do Azure para dados inativos. Encriptação de serviço de armazenamento (SSE) funciona ao encriptar dados Olá quando é escrito tooAzure armazenamento e desencripta antes de obtenção. SSE atualmente só está disponível para Olá serviço Blob do Azure e pode ser utilizado para blobs de blocos, blobs de páginas e blobs de acréscimo. toolearn mais, consulte [encriptação do serviço de armazenamento para dados Inativos](../storage/common/storage-service-encryption.md).</br>SSE só é suportado em contas de armazenamento do Resource Manager. |

Pode filtrar e dispensar recomendações.

1. Selecione **filtro** no Olá **recomendações** painel. Olá **filtro** abre painel e selecionar valores de gravidade e estado de Olá desejar toosee.

    ![Recomendações de filtro][2]
2. Se determinar que uma recomendação não é aplicável, pode ignorar a recomendação de Olá e, em seguida, filtrá-lo da vista. Existem duas formas toodismiss uma recomendação. Uma forma é tooright clique num item e, em seguida, selecione **dispensar**. Olá, outro é toohover sobre um item, clique em pontos de Olá três apresentados toohello direito e, em seguida, selecione **dispensar**. Pode ver as recomendações dispensadas ao clicar **filtro**e, em seguida, selecionar **dispensados**.

    ![Ignorar a recomendação][3]

### <a name="apply-recommendations"></a>Aplicar recomendações
Depois de rever todas as recomendações, decida que um deve ser aplicada primeiro. Recomendamos que utilize classificação de gravidade Olá como Olá tooevaluate parâmetro principal que recomendações devem ser aplicadas pela primeira vez.

Na tabela de Olá recomendações acima, selecione uma recomendação e guiá-lo como um exemplo de como tooapply uma recomendação.

## <a name="next-steps"></a>Passos seguintes
Neste documento, foram introduzidas toosecurity recomendações no Centro de segurança. toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:

* [Definir políticas de segurança no Centro de segurança do Azure](security-center-policies.md) — Saiba como as políticas de segurança de tooconfigure às suas subscrições do Azure e os grupos de recursos.
* [Monitorização de estado de funcionamento de segurança no Centro de segurança do Azure](security-center-monitoring.md) — Saiba como toomonitor Olá estado de funcionamento dos seus recursos Azure.
* [Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md) — Saiba como alertas de toosecurity toomanage e respondeu.
* [Monitorizar soluções de parceiros com o Centro de segurança do Azure](security-center-partner-solutions.md) — Saiba como toomonitor Olá estado de funcionamento das suas soluções de parceiros.
* [FAQ do Centro de segurança do Azure](security-center-faq.md) – encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.
* [Blogue de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – Encontre mensagens do blogue acerca da segurança e conformidade do Azure.

<!--Image references-->
[1]: ./media/security-center-recommendations/recommendations-tile.png
[2]: ./media/security-center-recommendations/filter-recommendations.png
[3]: ./media/security-center-recommendations/dismiss-recommendations.png
