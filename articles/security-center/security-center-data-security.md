---
title: "Segurança de Dados do Centro de Segurança do Azure | Microsoft Docs"
description: "Este documento explica como os dados são geridos e salvaguardados no Centro de Segurança do Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 33f2c9f4-21aa-4f0c-9e5e-4cd1223e39d7
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: yurid
ms.openlocfilehash: 6f95cf7631664f4630edbbcdadfd1d98105fdb98
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/11/2017
---
# <a name="azure-security-center-data-security"></a>Segurança de Dados do Centro de Segurança do Azure
Para ajudar os clientes a evitar, detetar e responder a ameaças, o Centro de Segurança do Azure recolhe e processa dados relacionados com segurança, incluindo informações de configuração, metadados, registos de eventos, ficheiros de informação de falha de sistema e mais. A Microsoft respeita diretrizes rigorosas de conformidade e segurança, desde a codificação à operação de um serviço.

Este artigo explica como os dados são geridos e salvaguardados no Centro de Segurança do Azure.

>[!NOTE] 
>A partir do início de junho de 2017, o Centro de Segurança irá utilizar o Microsoft Monitoring Agent para recolher e armazenar dados. Veja [Azure Security Center Platform Migration](security-center-platform-migration.md) (Migração da Plataforma do Centro de Segurança do Azure) para saber mais. As informações neste artigo representam a funcionalidade do Centro de Segurança após a transição para o Agente de Monitorização da Microsoft.
>


## <a name="data-sources"></a>Origens de dados
O Centro de Segurança do Azure analisa dados das origens seguintes para proporcionar visibilidade para o estado da segurança, identificar vulnerabilidades e recomendar mitigações e detetar ameaças ativas:

- Serviços do Azure: utiliza informações sobre a configuração dos serviços do Azure que implementou através da comunicação com o fornecedor de recursos desses serviços.
- Tráfego de Rede: utiliza metadados de tráfego de rede de amostragem da infraestrutura da Microsoft, tais como porta/IP de origem/destino, tamanho do pacote e protocolo de rede.
- Soluções de Parceiros: utiliza alertas de segurança das soluções de parceiros integradas, tais como firewalls e soluções antimalware. 
- As suas Máquinas Virtuais e Servidores: utiliza informações de configuração e informações sobre eventos de segurança, tais como eventos do Windows e registos de auditoria, registos do IIS, mensagens do syslog e ficheiros de informação de falha de sistema das suas máquinas virtuais. Além disso, quando é criado um alerta, o Centro de Segurança do Azure pode gerar um instantâneo do disco da VM afetada e extrair artefactos da máquina relacionados com o alerta desse disco, como o ficheiro de registo, para fins forenses.


## <a name="data-protection"></a>Proteção de dados
**Segregação de dados**: os dados são mantidos separados de forma lógica em cada componente em todo o serviço. Todos os dados são etiquetados por organização. Este tipo de etiquetagem persiste por todo o ciclo de vida dos dados e é imposto em cada camada do serviço.

**Acesso a dados**: para disponibilizar recomendações de segurança e investigar potenciais ameaças de segurança, os técnicos da Microsoft podem aceder a informações recolhidas ou analisadas pelos serviços do Azure, incluindo ficheiros de informação de falha de sistema, eventos de criação de processos, instantâneos e artefactos do disco da VM, que pode incluir, de forma não intencional, Dados do Cliente ou dados pessoais das suas máquinas virtuais. Respeitamos os [Termos e a Declaração de Privacidade do Microsoft Online Services](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31), os quais estipulam que a Microsoft não utilizará Dados do Cliente ou derivará informações dos mesmos para qualquer fim publicitário ou comercial semelhante. Apenas utilizamos os Dados do Cliente conforme necessário para lhe fornecer os serviços do Azure, incluindo fins compatíveis com o fornecimento desses serviços. O utilizador retém todos os direitos sobre os Dados do Cliente.

**Utilização de dados**: a Microsoft utiliza os padrões e as informações sobre ameaças presentes em vários inquilinos para melhorar as nossas capacidades de prevenção e deteção. Fazemo-lo em conformidade com os compromissos de privacidade descritos na nossa [Declaração de Privacidade](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).

## <a name="data-location"></a>Localização dos dados

**As suas Áreas de Trabalho**: uma área de trabalho é especificada para as seguintes Áreas Geográficas e os dados recolhidos das suas máquinas virtuais do Azure, incluindo informações de falhas e alguns tipos de dados de alerta, são armazenados na área de trabalho mais próxima. 

| Área Geográfica da VM                        | Área Geográfica da Área de Trabalho |
|-------------------------------|---------------|
| Estados Unidos, Brasil, Canadá | Estados Unidos |
| Europa, Reino Unido        | Europa        |
| Ásia-Pacífico, Japão, Índia    | Ásia-Pacífico  |
| Austrália                     | Austrália     |

 
Instantâneos de disco da VM são armazenados na mesma conta de armazenamento como disco de VM.
 
Para máquinas virtuais e servidores em execução noutros ambientes, por exemplo, no local, pode especificar a área de trabalho e a região onde são armazenados os dados recolhidos. 

**Armazenamento do Centro de Segurança do Azure**: as informações sobre alertas de segurança, incluindo alertas de parceiros, são armazenadas regionalmente de acordo com a localização do recurso do Azure relacionado, enquanto que as informações sobre o estado de funcionamento de segurança e recomendações são armazenadas centralmente nos Estados Unidos ou na Europa, em conformidade com a localização do cliente.
O Centro de Segurança do Azure recolhe cópias efémeras dos ficheiros de informação de falha de sistema e analisa-as para encontrar sinais de tentativas de exploração e casos em que a segurança tenha sido comprometida. O Centro de Segurança do Azure faz esta análise na mesma Geografia que a área de trabalho e elimina as cópias efémeras quando a análise estiver concluída.

Os artefactos das máquinas são armazenados centralmente na mesma região que as VMs. 


## <a name="managing-data-collection-from-virtual-machines"></a>Gestão da recolha de dados provenientes de máquinas virtuais

Quando ativar o Centro de Segurança do Azure, a recolha de dados é ativada para cada uma das suas subscrições do Azure. Também pode ativar a recolha de dados para as suas subscrições na secção Política de Segurança do Centro de Segurança do Azure. Quando a Recolha de Dados é ativada, o Centro de Segurança do Azure aprovisiona o Agente de Monitorização da Microsoft em todas as máquinas virtuais do Azure existentes suportadas e quaisquer máquinas novas criadas. O Agente de Monitorização da Microsoft analisa várias configurações e eventos relacionados com a segurança em rastreios de [Rastreio de Eventos para o Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW). Além disso, o sistema operativo irá gerar eventos do registo de eventos durante a execução da máquina. Os exemplos destes dados incluem: tipo e versão do sistema operativo, registos de sistema operativo (registos de eventos do Windows), processos em execução, nome da máquina, endereços IP, utilizador com sessão iniciada e ID do inquilino. O Agente de Monitorização da Microsoft lê as entradas de registo de eventos e rastreios ETW e copia-as para as suas áreas de trabalho para análise. O Agente de Monitorização da Microsoft também copia os ficheiros de informação de falha de sistema para as suas áreas de trabalho.

Se estiver a utilizar o Centro de Segurança do Azure gratuito, também pode desativar a recolha de dados das máquinas virtuais na Política de Segurança. A Recolha de Dados é necessária para as subscrições no escalão Standard. A recolha de instantâneos e artefactos de discos de VM continua ativada, mesmo que a recolha de dados tenha sido desativada.


## <a name="see-also"></a>Consultar também
Através deste documento aprendeu como os dados são geridos e salvaguardados no Centro de Segurança do Azure. Para saber mais acerca do Centro de Segurança do Azure, veja:

* [Guia de Operações e Planeamento do Centro de Segurança do Azure](security-center-planning-and-operations-guide.md) – Saiba como planear e compreender as considerações de conceção para adoção do Centro de Segurança do Azure.
* [Monitorização de estado de funcionamento de segurança no Centro de Segurança do Azure](security-center-monitoring.md) – Saiba como monitorizar o estado de funcionamento dos seus recursos do Azure
* [Gerir e responder a alertas de segurança no Centro de Segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como gerir e responder a alertas de segurança
* [Monitorizar soluções de parceiros com o Centro de Segurança do Azure](security-center-partner-solutions.md) – Saiba como monitorizar o estado de funcionamento das suas soluções de parceiros.
* [Azure Security Center FAQ (FAQ do Centro de Segurança do Azure)](security-center-faq.md) – Encontre as perguntas mais frequentes acerca de como utilizar o serviço
* [Blogue de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – Encontre mensagens do blogue acerca da segurança e conformidade do Azure
