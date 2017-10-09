---
title: aaaLearn sobre hello mais recente do Azure SO convidado | Microsoft Docs
description: "Hello mais recentes notícias de versão e a compatibilidade SDK para o SO de convidado de serviços de nuvem do Azure."
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 6306cafe-1153-44c7-8554-623b03d59a34
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 8/24/2017
ms.author: raiye
ms.openlocfilehash: 7274f5a68a32ce91bdede77e1443cdb8053c07ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-guest-os-releases-and-sdk-compatibility-matrix"></a>Versões de SO convidado do Azure e matriz de compatibilidade SDK
Fornece informações atualizadas sobre Olá que versões de SO de convidado do Azure mais recente para serviços em nuvem. Estas informações ajudam a planear o caminho de atualização antes de um SO convidado está desativado. Se configurar o seu toouse funções *automática* atualizações de SO convidado, conforme descrito em [definições de atualização de SO de convidado do Azure][Azure Guest OS Update Settings], não é vital que leia esta página.

> [!IMPORTANT]
> Esta página é aplicável tooCloud serviços web e de trabalho funções, que são executados sobre um SO convidado. Faz **não aplicar** tooIaaS máquinas virtuais.
>
>


> [!NOTE]
> Olá RSS Feed recentemente foi preterido. Procurar as atualizações de um feed novo disponível em breve!
>
>

Não souber sobre que Olá é de SO convidado ou como Olá versões do SO convidado trabalho? Leitura [isto](#how-it-works) secção.

## <a name="news-updates"></a>Atualizações de notícias de última hora

###### <a name="august-24-2017"></a>**24 de Agosto de 2017**
SO de convidado de Agosto foi libertado.

###### <a name="august-3-2017"></a>**3 de Agosto de 2017**
SO de convidado de Julho foi libertado.

###### <a name="july-19-2017"></a>**19 de Julho de 2017**
Implementação de SO convidado de Julho está a iniciar 19 de Julho e tem uma versão 8 de Agosto prevista.

###### <a name="july-7-2017"></a>**7 de Julho de 2017**
SO de convidado de Junho foi libertado.

###### <a name="june-16-2017"></a>**16 de Junho de 2017**
Implementação de SO convidado de Junho está a iniciar 16 de Junho e tem uma versão 11 de Julho prevista.

###### <a name="june-5-2017"></a>**5 de Junho de 2017**
Pode foi libertada SO convidado.

###### <a name="may-17-2017"></a>**17 de Maio de 2017**
Devido a erros de segurança tooa, iremos desativação Olá após Dezembro de 2016 e Janeiro de 2017 versões de SO que não tenham Olá [corrigir] do portal de Olá: WA-convidado-so-5.4_201612-01, WA-convidado-SO-4.39_201612-01, WA-convidado-SO-3.46_ 201612-01, WA-CONVIDADO-SO-2.59_201701-01

###### <a name="may-12-2017"></a>**12 de Maio de 2017**
Implementação de Maio de SO convidado está a iniciar 12 de Maio e tem uma versão 13 de Junho prevista.

###### <a name="april-18-2017"></a>**18 de Abril de 2017**
Implementação de SO convidado de Abril está a iniciar 18 de Abril e tem uma versão 9 de Maio prevista.

###### <a name="april-10-2017"></a>**10 de Abril de 2017**
Implementação de SO convidado de Março iniciada 14 de Março de 2017 e lançadas 10 de Abril de 2017.

###### <a name="january-10-2017"></a>**10 de Janeiro de 2017**
SO de convidado de Janeiro de Olá contém patches que afetam apenas família de SO 2 (Windows 2008 Server R2). Iremos tenham publicadas, por conseguinte, apenas a imagem de Olá 2 da família de SO (WA-convidado-SO-2.59_201701-01) para o mês. Todas as outras famílias de SO, SO de Dezembro de Olá (201612 - 01) permanecem hello mais recente.


## <a name="releases"></a>Versões
## <a name="family-5-releases"></a>Versões de família 5
**Windows Server, 2016**

.NET framework instalado: 4.0, 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2

> [!NOTE]
> As datas com uma * são toochange do requerente.
>
> Olá palavra-passe RDP para 5 da família de SO tem de ser no mínimo 10 carateres.
>

| Cadeia de configuração | Data da versão | Desativar data | Data expirada |
| --- | --- | --- | --- |
| WA-CONVIDADO-SO-5.10_201708-01 |24 de Agosto de 2017 |Post 5.12 |TBD |
| WA-CONVIDADO-SO-5.9_201707-01 |3 de Agosto de 2017 |Post 5.11 |TBD |
| WA-CONVIDADO-SO-5.8_201706-01 |7 de Julho de 2017 |Post à versão 5.10 |TBD |
|~~WA-CONVIDADO-SO-5.7_201705-01~~ |5 de Junho de 2017 |24 de Agosto de 2017 |TBD |
|~~WA-CONVIDADO-SO-5.6_201704-01~~ |9 de Maio de 2017 |3 de Agosto de 2017 |TBD |
|~~WA-CONVIDADO-SO-5.5_201703-01~~ |10 de Abril de 2017 |7 de Julho de 2017 |TBD |
|~~WA-CONVIDADO-SO-5.4_201612-01~~ |10 de janeiro de 2017 |5 de Junho de 2017|TBD |
|~~WA-CONVIDADO-SO-5.3_201611-01~~ |14 de Dezembro de 2016 |9 de Maio de 2017 |TBD |
|~~WA-CONVIDADO-SO-5.2_201610-02~~ |1 de Novembro de 2016 |10 de Abril de 2017 |TBD |

## <a name="family-4-releases"></a>Versões de família 4
**Windows Server 2012 R2**

Suporta o .NET 4.0, 4.5, 4.5.1, 4.5.2

> [!NOTE]
> As datas com uma * são toochange do requerente
>
>

| Cadeia de configuração | Data da versão | Desativar data | Data expirada |
| --- | --- | --- | --- |
| WA-CONVIDADO-SO-4.45_201708-01 |24 de Agosto de 2017 |Post 4.47 |TBD |
| WA-CONVIDADO-SO-4.44_201707-01 |3 de Agosto de 2017 |Post 4.46 |TBD |
| WA-CONVIDADO-SO-4.43_201706-01 |7 de Julho de 2017 |Post 4.45 |TBD |
|~~WA-CONVIDADO-SO-4.42_201705-01~~ |5 de Junho de 2017 |24 de Agosto de 2017 |TBD |
|~~WA-CONVIDADO-SO-4.41_201704-01~~ |9 de Maio de 2017 |3 de Agosto de 2017 |TBD |
|~~WA-CONVIDADO-SO-4.40_201703-01~~ |10 de Abril de 2017 |7 de Julho de 2017 |TBD |
|~~WA-CONVIDADO-SO-4.39_201612-01~~ |10 de janeiro de 2017 |5 de Junho de 2017 |TBD |
|~~WA-CONVIDADO-SO-4.38_201611-01~~ |14 de Dezembro de 2016 |9 de Maio de 2017 |TBD |
|~~WA-CONVIDADO-SO-4.37_201610-02~~ |16 de novembro de 2016 |10 de Abril de 2017 |TBD |
|~~WA-CONVIDADO-SO-4.36_201609-01~~ |13 de Outubro de 2016 |14 de Janeiro de 2017 |TBD |
|~~WA-CONVIDADO-SO-4.35_201608-01~~ |13 de Setembro de 2016 |16 de Dezembro de 2016 |TBD |
|~~WA-CONVIDADO-SO-4.34_201607-01~~ |8 de agosto de 2016 |13 de Novembro de 2016 |TBD |


## <a name="family-3-releases"></a>Versões da família 3
**Windows Server 2012**

Suporta o .NET 4.0, 4.5, 4.5.1, 4.5.2

> [!NOTE]
> As datas com uma * são toochange do requerente
>
>

| Cadeia de configuração | Data da versão | Desativar data | Data expirada |
| --- | --- | --- | --- |
| WA-CONVIDADO-SO-3.52_201708-01 |24 de Agosto de 2017 |Post 3.54 |TBD |
| WA-CONVIDADO-SO-3.51_201707-01 |3 de Agosto de 2017 |Post 3.53 |TBD |
| WA-CONVIDADO-SO-3.50_201706-01 |7 de Julho de 2017 |Post 3.52 |TBD |
|~~WA-CONVIDADO-SO-3.49_201705-01~~ |5 de Junho de 2017 |24 de Agosto de 2017 |TBD |
|~~WA-CONVIDADO-SO-3.48_201704-01~~ |9 de Maio de 2017 |3 de Agosto de 2017 |TBD |
|~~WA-CONVIDADO-SO-3.47_201703-01~~ |10 de Abril de 2017 |7 de Julho de 2017 |TBD |
|~~WA-CONVIDADO-SO-3.46_201612-01~~ |10 de janeiro de 2017 |5 de Junho de 2017 |TBD |
|~~WA-CONVIDADO-SO-3.45_201611-01~~ |14 de Dezembro de 2016 |9 de Maio de 2017 |TBD |
|~~WA-CONVIDADO-SO-3.44_201610-02~~ |16 de novembro de 2016 |1 de Maio de 2017 |TBD |
|~~WA-CONVIDADO-SO-3.43_201609-01~~ |13 de Outubro de 2016 |14 de Janeiro de 2017 |TBD |
|~~WA-CONVIDADO-SO-3.42_201608-01~~ |13 de Setembro de 2016 |16 de Dezembro de 2016 |TBD |
|~~WA-CONVIDADO-SO-3.41_201607-01~~ |8 de agosto de 2016 |13 de Novembro de 2016 |TBD |


## <a name="family-2-releases"></a>Versões de família 2
**Windows Server 2008 R2 SP1**

Suporta o .NET 3.5, 4.0, 4.5, 4.5.1, 4.5.2

> [!NOTE]
> As datas com uma * são toochange do requerente
>
>

| Cadeia de configuração | Data da versão | Desativar data | Data expirada |
| --- | --- | --- | --- |
| WA-CONVIDADO-SO-2.65_201708-01 |24 de Agosto de 2017 |Post 2.67 |TBD |
| WA-CONVIDADO-SO-2.64_201707-01 |3 de Agosto de 2017 |Post 2.66 |TBD |
| WA-CONVIDADO-SO-2.63_201706-01 |7 de Julho de 2017 |Post 2.65 |TBD |
|~~WA-CONVIDADO-SO-2.62_201705-01~~ |5 de Junho de 2017 |24 de Agosto de 2017 |TBD |
|~~WA-CONVIDADO-SO-2.61_201704-01~~ |9 de Maio de 2017 |3 de Agosto de 2017 |TBD |
|~~WA-CONVIDADO-SO-2.60_201703-01~~ |10 de Abril de 2017 |7 de Julho de 2017 |TBD |
|~~WA-CONVIDADO-SO-2.59_201701-01~~ |10 de janeiro de 2017 |5 de Junho de 2017 |TBD |
|~~WA-CONVIDADO-SO-2.58_201612-01~~ |10 de janeiro de 2017 |9 de Maio de 2017|TBD |
|~~WA-CONVIDADO-SO-2.57_201611-01~~ |14 de Dezembro de 2016 |10 de Abril de 2017 |TBD |
|~~WA-CONVIDADO-SO-2.56_201610-02~~ |16 de novembro de 2016 |10 de Fevereiro de 2017 |TBD |
|~~WA-CONVIDADO-SO-2.55_201609-01~~ |13 de Outubro de 2016 |14 de Janeiro de 2017 |TBD |
|~~WA-CONVIDADO-SO-2.54_201608-01~~ |13 de Setembro de 2016 |16 de Dezembro de 2016 |TBD |
|~~WA-CONVIDADO-SO-2.53_201607-01~~ |8 de agosto de 2016 |13 de Novembro de 2016 |TBD |



## <a name="msrc-patch-updates"></a>Atualizações de correção MSRC
Olá lista de patches que estão incluídas com cada versão de SO convidado mensal está disponível [aqui][patches].

## <a name="sdk-support"></a>Suporte SDK
Embora Olá [política de extinção para Olá Azure SDK] [ retire policy sdk] indica que apenas versões acima 2.2 são suportadas e específica famílias de SO convidado permitem-lhe toouse versões anteriores. Deve sempre utilizar Olá mais recente suportada SDK.

| Família de SO convidado | Versões do SDK compatível |
| --- | --- |
| 5 |Versão 2.9.5.1+ |
| 4 |Versão 2.1 + |
| 3 |Versão 1.8 + |
| 2 |Versão 1.3 + |
| 1 |Versão 1.0 + |

## <a name="guest-os-release-information"></a>Informações de versão de SO convidado
Existem três datas que são importantes tooGuest SO versões: **versão** data, **desativada** data, e **expiração** data. Um SO convidado é considerado disponível quando se está a ser Olá Portal e pode ser selecionado como destino de Olá SO convidado. Quando um SO convidado atingir Olá **desativada** data, este é removido do Azure. No entanto, qualquer serviço de nuvem nesse SO convidado ainda funcionará como normal.

janela de Olá entre Olá **desativada** data e Olá **expiração** data disponibiliza uma transição de tooeasily de memória intermédia de um tooone de SO convidado mais recente. Se estiver a utilizar *automática* como o SO convidado, poderá sempre na versão mais recente Olá e não tiver tooworry acerca do mesmo prestes a expirar.

Quando Olá **expiração** data transmite, qualquer serviço de nuvem utilizar ainda nesse SO convidado será parado, tooupgrade eliminada ou forçada. Pode ler mais sobre a política de extinção de Olá [aqui][retirepolicy].

## <a name="guest-os-family-version-explanation"></a>Explicação da família de SO convidado
famílias de SO convidado Olá baseiam-se em versões de lançamento do Microsoft Windows Server. Olá SO convidado é o sistema operativo subjacente Olá que Cloud Services do Azure é executado. Cada SO convidado possui um família, a versão e a versão número.

* **Família de SO convidado**  
  Um sistema operativo Windows Server de versão baseiam um SO convidado. Por exemplo, *família 3* é baseado no Windows Server 2012.
* **Versão de SO convidado**  
  Imagem específica tooa família de SO convidado mais relevantes [Microsoft Security Response Center (MSRC)] [ msrc] é produzido patches que estão disponíveis na versão de SO convidado Olá data Olá novo. Nem todos os patches podem ser incluídos.

    Os números começam em 0 e incrementados por 1 sempre que é adicionado um novo conjunto de atualizações. Só são mostradas zeros à direita se importantes. Ou seja, versão 2.10 é uma versão diferente, muito posterior à versão 2.1.
* **Versão de SO convidado**  
  Um rerelease de uma versão de SO convidado. Um rerelease ocorre se o Microsoft localiza problemas durante o teste; necessidade de alterações. Olá versão mais recente sempre substitui quaisquer anterior versões, público ou não. Olá portal do Azure irá permitir apenas utilizadores toopick versão mais recente do Olá para uma determinada versão. Implementações em execução uma versão anterior são normalmente não force atualizada dependendo da gravidade Olá de erros de Olá.

Exemplo de Olá abaixo, 2 é família Olá, 12 é versão de Olá e "rel2" é a versão de Olá.

**Versão de SO convidado** - 2.12 rel2

**Cadeia de configuração para esta versão** -WA-convidado-SO-2.12_201208-02

Olá a cadeia de configuração para um SO convidado tem esta mesma informação incorporada, juntamente com uma data que mostra os patches MSRC foram considerados para essa versão. Neste exemplo, patches MSRC produzidos para o Windows Server 2008 R2 segurança tooand incluindo Agosto de 2012 foram contemplados para inclusão. Apenas os patches especificamente aplicar toothat versão do Windows Server estão incluídos. Por exemplo, se uma correção MSRC aplica-se tooMicrosoft Office, não será incluído porque esse produto não faz parte da imagem base do servidor do Windows hello.

## <a name="guest-os-system-update-process"></a>Processo de atualização do sistema de SO convidado
Esta página inclui informações sobre os lançamentos de SO convidado. Os clientes indicou que querem tooknow quando uma versão ocorre porque as respetivas funções de serviço em nuvem serão reiniciado se forem definidos atualização demasiado "automática". Versões de SO convidado normalmente ocorrerem, pelo menos, cinco (5) dias após hello MSRC lançamento de atualização que ocorre no Olá segunda Terça-feira de cada mês. Novos lançamentos incluem todos os Olá relevantes MSRC patches para cada família de SO convidado.

Microsoft Azure está constantemente lançar atualizações. Olá SO convidado é apenas um desse atualização no pipeline de Olá. Uma versão pode ser afetada por vários fatores demasiado numerosos toolist aqui. Além disso, o Azure é executado na literalmente centenas de milhares de máquinas. Isto significa que é impossível toogive uma data e hora exatas quando as funções selecionadas serão reiniciado. Estamos a trabalhar para um plano toolimit ou tempo reinícios.

Quando uma nova versão do Olá que SO convidado é publicado, pode demorar tempo toofully propagam entre o Azure. Como os serviços são atualizado toohello SO convidado novas, estão reinicializada para respeitar domínios de atualização. Serviços toouse de conjunto de atualizações "Automático" irá obter uma versão primeiro. Após a atualização de Olá, irá ver a nova versão de SO convidado Olá listados para o seu serviço na Olá portal do Azure. Rereleases poderão ocorrer durante este período. Algumas versões podem ser implementados ao longo de períodos mais longos de tempo e reinícios de atualização automáticos poderão não ocorrer para muitos semanas após a data de lançamento oficial de Olá. Depois de um SO convidado está disponível, pode, em seguida, explicitamente escolher essa versão do portal de Olá ou no ficheiro de configuração.

Para uma grande quantidade de informações importantes sobre reinicia e ponteiros toomore informações detalhes técnicos de atualizações do convidado e sistema operativo anfitrião, consulte Olá MSDN blogue post intitulada [função instância reinicia devida tooOS atualizações] [ restarts].

Se atualizar manualmente o SO convidado, consulte Olá [política de extinção de SO convidado] [ retirepolicy] para obter informações adicionais.

## <a name="guest-os-supportability-and-retirement-policy"></a>Suporte de SO convidado e a política de extinção
Olá política de Suportabilidade e extinção de SO convidado é explicado [aqui][retirepolicy].

[Install .NET on a Cloud Service Role]: https://azure.microsoft.com/en-us/documentation/articles/cloud-services-dotnet-install-dotnet/?WT.mc_id=azurebg_email_Trans_963_RevisedNET_Update
[Azure Guest OS Update Settings]: cloud-services-how-to-configure.md
[ssl3 announcement]: http://azure.microsoft.com/blog/2014/12/09/azure-security-ssl-3-0-update/
[Microsoft Security Advisory 3009008]: https://technet.microsoft.com/library/security/3009008.aspx
[ssl3-fixit]: http://go.microsoft.com/?linkid=9863266
[MS14-066]: https://technet.microsoft.com/library/security/ms14-066.aspx
[MS14-046]: https://technet.microsoft.com/library/security/ms14-046.aspx
[retire policy sdk]: https://msdn.microsoft.com/library/dn479282.aspx
[server and gos]: https://msdn.microsoft.com/library/dn775043.aspx
[azuresupport]: http://azure.microsoft.com/support/options/
[net install pkg]: http://www.microsoft.com/download/details.aspx?id=42643
[msrc]: http://www.microsoft.com/security/msrc/default.aspx
[update guest os portal]: https://msdn.microsoft.com/library/gg433101.aspx
[update guest os svc]: https://msdn.microsoft.com/library/gg456324.aspx
[restarts]: http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx
[patches]: cloud-services-guestos-msrc-releases.md
[retirepolicy]: cloud-services-guestos-retirement-policy.md
[fam1retire]: cloud-services-guestos-family1-retirement.md
[corrigir]: https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
