---
title: "aaaWhat é o Gestor de tráfego | Microsoft Docs"
description: "Este artigo irá ajudá-lo a compreender o que é o Gestor de tráfego e se é Olá opção Encaminhamento do tráfego direita para a sua aplicação"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 75d5ff9a-f4b9-4b05-af32-700e7bdfea5a
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: kumud
ms.openlocfilehash: 8e63ed11cdcdc03ae9cd28f88f0d1f9dc2cd44ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-traffic-manager"></a>Descrição Geral do Gestor de Tráfego

Gestor de tráfego do Microsoft Azure permite-lhe distribuição de Olá toocontrol tráfego do utilizador para pontos finais do serviço em datacenters diferentes. Pontos finais de serviço suportados pelo Gestor de tráfego incluem as VMs do Azure, as aplicações Web e serviços em nuvem. Também pode utilizar o Gestor de Tráfego com pontos finais externos, não pertencentes ao Azure.

Gestor de tráfego utiliza Olá sistema de nomes de domínio (DNS) toodirect cliente pedidos toohello mais adequado ponto final com base num método de encaminhamento de tráfego e estado de funcionamento de Olá de pontos finais de Olá. Gestor de tráfego fornece uma variedade de [métodos de encaminhamento de tráfego](traffic-manager-routing-methods.md) e [ponto final de opções de monitorização](traffic-manager-monitoring.md) toosuit diferente da aplicação necessidades e modelos de ativação pós-falha automática. Gestor de tráfego é resiliente toofailure, incluindo a falha de Olá de uma região do Azure completa.

## <a name="traffic-manager-benefits"></a>Vantagens do Gestor de tráfego

Gestor de tráfego pode ajudá-lo:

* **Melhorar a disponibilidade de aplicações críticas**

    Gestor de tráfego fornece elevada disponibilidade para as suas aplicações através da monitorização de pontos finais da sua e fornecer ativação pós-falha automática quando um ponto final fica inativo.

* **Melhorar a capacidade de resposta para aplicações de elevado desempenho**

    Azure permite-lhe os Web sites ou serviços de cloud toorun nos centros de dados localizados em torno Olá mundo. Gestor de tráfego melhora a capacidade de resposta da aplicação ao instruir o ponto final do tráfego toohello com Olá menor rede latência para cliente Olá.

* **Executar a manutenção do serviço sem períodos de indisponibilidade**

    Pode efetuar operações de manutenção planeada sobre as aplicações sem períodos de indisponibilidade. Gestor de tráfego direciona pontos finais de tooalternative tráfego enquanto manutenção Olá está em curso.

* **Combinar as aplicações baseadas na nuvem e no local**

    O Traffic Manager suporta externo, pontos finais do Azure não ativar toobe utilizado com híbridos na nuvem e no local implementações, incluindo Olá "rajada para a nuvem," "migrar para a nuvem," e "ativação pós-falha para a nuvem" cenários.

* **Distribuir o tráfego para implementações grandes, complexas**

    Utilizar [aninhada perfis do Traffic Manager](traffic-manager-nested-profiles.md), métodos de encaminhamento de tráfego podem ser combinado toocreate sofisticadas e tem de Olá de toosupport flexível de regras de implementações maiores, mais complexas.

## <a name="how-traffic-manager-works"></a>Como funciona o Gestor de Tráfego

Traffic Manager do Azure permite-lhe toocontrol distribuição Olá tráfego entre pontos finais da sua aplicação. Um ponto final é qualquer serviço de acesso à Internet alojada dentro ou fora do Azure.

Gestor de tráfego proporciona duas vantagens chave:

1. Distribuição de tráfego de acordo com tooone de vários [métodos de encaminhamento de tráfego](traffic-manager-routing-methods.md)
2. [Monitorização contínua de estado de funcionamento do ponto final](traffic-manager-monitoring.md) e ativação pós-falha automática quando não conseguem pontos finais

Quando um cliente tenta tooconnect tooa serviço, deve resolver primeiro o nome DNS de Olá do endereço IP do Olá serviço tooan. Olá estabelece ligação, em seguida, serviço de Olá de tooaccess de endereço IP toothat.

**Olá mais importantes ponto toounderstand é que o Gestor de tráfego funciona ao nível do Olá DNS.**  Pontos finais com base nas regras de Olá do método de encaminhamento de tráfego de Olá de serviço do Gestor de tráfego utiliza DNS toodirect clientes toospecific. Os clientes ligam toohello selecionado endpoint **diretamente**. Gestor de tráfego não é um proxy ou de um gateway. Gestor de tráfego não consegue ver o tráfego de Olá passar entre Olá cliente e o serviço de Olá.

### <a name="traffic-manager-example"></a>Exemplo de Gestor de tráfego

Contoso Corp ter programado um novo portal de parceiros. URL de Olá para este portal é https://partners.contoso.com/login.aspx. aplicação de Olá fique alojada em três regiões do Azure. disponibilidade de tooimprove e maximizar o desempenho global, que utilizam o Gestor de tráfego toodistribute cliente tráfego toohello mais próximo ponto final disponível.

tooachieve nesta configuração, concluírem Olá os seguintes passos:

1. Implemente três instâncias do seu serviço. os nomes DNS de Olá estas implementações são 'contoso us.cloudapp .net', 'contoso eu.cloudapp .net' e 'contoso asia.cloudapp .net'.
2. Criar um perfil do Traffic Manager, com o nome 'contoso.trafficmanager.net' e configure-o método de encaminhamento de tráfego 'Desempenho' de Olá toouse nos pontos finais de Olá três.
* Configurar o respetivo nome de domínio intuitivos, "partners.contoso.com", toopoint too'contoso.trafficmanager.net', através de um registo CNAME no DNS.

![Configuração de DNS do Gestor de tráfego][1]

> [!NOTE]
> Ao utilizar um domínio do com o Gestor de tráfego do Azure, tem de utilizar um CNAME toopoint seu nome de domínio do Traffic Manager do intuitivos domínio nome tooyour. Normas DNS não permitem-lhe toocreate um CNAME em Olá 'vértice' (ou raiz) de um domínio. Deste modo, não é possível criar um CNAME para "contoso.com" (por vezes, designado por um 'naked' domínio). Só pode criar um CNAME para o domínio em 'contoso.com', por exemplo, "www.contoso.com". toowork em torno esta limitação, recomendamos que utilize um pedidos de toodirect de redirecionamento HTTP simples para 'contoso.com' tooan nome alternativo, tais como "www.contoso.com".

### <a name="how-clients-connect-using-traffic-manager"></a>Como os clientes ligam utilizando o Gestor de tráfego

Continuar a partir do exemplo anterior Olá, quando um cliente solicita Olá página https://partners.contoso.com/login.aspx, o cliente Olá efetua Olá seguir o nome DNS do passos tooresolve Olá e estabelecer uma ligação:

![Estabelecimento de ligação utilizando o Gestor de tráfego][2]

1. cliente de Olá envia uma recursiva de tooits configurado de consulta DNS DNS serviço tooresolve Olá nome "partners.contoso.com". Um serviço DNS recursiva, por vezes denominado um serviço de 'local DNS', não aloja domínios DNS diretamente. Em vez disso, o cliente de Olá off-loads trabalho Olá de contactar Olá DNS autoritativos vários serviços em Olá Internet necessária tooresolve um nome DNS.
2. nome DNS do tooresolve Olá, serviço DNS recursiva Olá localiza os servidores de nomes de Olá para o domínio de "contoso.com" Olá. -Lo, em seguida, contacta os registo DNS do nome servidores toorequest Olá "partners.contoso.com". servidores DNS de contoso.com Olá devolvem Olá Registro CNAME que aponta toocontoso.trafficmanager.net.
3. Em seguida, o serviço DNS recursiva Olá localiza os servidores de nomes de Olá para domínio de "trafficmanager.net" Olá, que são fornecidas por Olá serviço Gestor de tráfego do Azure. Em seguida, envia um pedido para Olá 'contoso.trafficmanager.net' DNS registo toothose servidores DNS.
4. servidores de nomes do Gestor de tráfego de Olá recebem o pedido de Olá. Escolherem um ponto final com base em:

    - Estado de Olá configurado de cada ponto final (desativados pontos finais não são devolvidos)
    - verifica o estado de funcionamento atual do Olá de cada ponto final, conforme determinado pelo Estado de funcionamento do Olá Gestor de tráfego. Para obter mais informações, consulte [monitorização de ponto final do Gestor de tráfego](traffic-manager-monitoring.md).
    - Olá escolhido o método de encaminhamento de tráfego. Para obter mais informações, consulte [métodos de encaminhamento do Traffic Manager](traffic-manager-routing-methods.md).

5. ponto final de Olá escolhido é devolvido como outro registo CNAME no DNS. Neste caso, informe-nos suponha que contoso-us.cloudapp.net é devolvido.
6. Em seguida, serviço DNS recursiva Olá localiza os servidores de nomes de Olá para o domínio de 'cloudapp.net' Olá. Entra em contacto com essas Olá de toorequest de servidores de nome 'contoso-us.cloudapp .net' registo DNS. Um registo DNS 'A' que contém o endereço IP Olá do ponto final de serviço com base em E.U.A. Olá é devolvido.
7. serviço DNS recursiva Olá consolida resultados Olá e devolve um único cliente de toohello de resposta DNS.
8. cliente de Olá recebe resultados DNS Olá e liga toohello especificado o endereço IP. Olá cliente liga ao ponto final do serviço de aplicações toohello diretamente, não através do Gestor de tráfego. Porque se trata de um ponto final de HTTPS, o cliente de Olá efetua o handshake SSL/TLS necessário Olá e, em seguida, faz com que um pedido HTTP GET Olá ' / login.aspx' página.

serviço DNS recursiva Olá coloca em cache as respostas DNS de Olá recebe. resolução DNS Olá no dispositivo de cliente Olá também coloca em cache resultado Olá. A colocação em cache permite subsequente toobe de consultas DNS respondida mais rapidamente, utilizando os dados da cache de Olá, em vez de consulta de outros servidores de nome. duração de Olá da cache de Olá é determinada pelo Olá 'time-to-live' (TTL) propriedade de cada registo DNS. Valores mais curtos resultam em rápida expiração de cache e, por conseguinte, mais ida e volta toohello Gestor de tráfego nome servidores. Os valores mais significam que pode demorar mais tráfego toodirect sair de um ponto final de falha. Gestor de tráfego permite-lhe tooconfigure Olá TTL utilizado no Gestor de tráfego DNS respostas toobe como tão baixo como 0 segundos e tão elevado como 2,147,483,647 segundos (Olá intervalo máximo em conformidade com [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt)), permitindo-lhe valor de Olá toochoose melhor que equilibra a Olá às necessidades da sua aplicação.

## <a name="pricing"></a>Preços

Para obter informações sobre preços, consulte [preços do Gestor de tráfego](https://azure.microsoft.com/pricing/details/traffic-manager/).

## <a name="faq"></a>FAQ

Para perguntas mais frequentes sobre o Gestor de tráfego, consulte [perguntas frequentes do Gestor de tráfego](traffic-manager-FAQs.md)

## <a name="next-steps"></a>Passos seguintes

Saiba mais sobre o Gestor de tráfego [ativação pós-falha automática e monitorização do ponto final](traffic-manager-monitoring.md).

Saiba mais sobre o Gestor de tráfego [métodos de encaminhamento de tráfego](traffic-manager-routing-methods.md).

Saiba mais sobre algumas das Olá outra chave [capacidades de rede](../networking/networking-overview.md) do Azure.

<!--Image references-->
[1]: ./media/traffic-manager-how-traffic-manager-works/dns-configuration.png
[2]: ./media/traffic-manager-how-traffic-manager-works/flow.png

