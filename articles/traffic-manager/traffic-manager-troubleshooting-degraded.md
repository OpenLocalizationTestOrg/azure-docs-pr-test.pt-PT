---
title: "aaaTroubleshooting degradado Estado no Gestor de tráfego do Azure"
description: "Como os perfis do Gestor de tráfego de tootroubleshoot quando mostra como degradada estado."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
ms.assetid: 8af0433d-e61b-4761-adcc-7bc9b8142fc6
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: kumud
ms.openlocfilehash: fd95697781472b52e98d856e66beb7b89dfeaf23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a>Resolução de problemas degradado Estado no Gestor de tráfego do Azure

Este artigo descreve como tootroubleshoot um perfil do Traffic Manager do Azure que aparece um Estado degradado. Para este cenário, considere que tiver configurado um perfil do Traffic Manager apontar toosome dos seus serviços cloudapp.net alojado. Se o estado de funcionamento Olá do Gestor de tráfego apresenta um **Degraded** estado e estado de Olá de um ou mais pontos finais poderá **Degraded**:

![Estado de degradada ponto final](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

Se apresenta o estado de funcionamento Olá do Gestor de tráfego um **inativo** Estado, em seguida, ambos os pontos finais poderá **desativado**:

![Estado inativo do Gestor de tráfego](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a>Compreender o Gestor de tráfego

* Gestor de tráfego considera um toobe de ponto final ONLINE apenas quando a pesquisa de Olá recebe uma resposta HTTP 200 fazer uma cópia do caminho de pesquisa de Olá. Quaisquer outra resposta 200 não é uma falha.
* Falha um redirecionamento 30 x, mesmo se Olá redirecionado URL devolve um 200.
* Para as pesquisas de HTTPs, erros de certificado são ignorados.
* conteúdo do real Olá do caminho de pesquisa de Olá irrelevante, desde que é devolvido um 200. Pesquisar um tipo de conteúdo estático do URL toosome "/ favicon.ico" é uma técnica comuns. Conteúdo dinâmico, como as páginas ASP de Olá, poderá não sempre devolver 200, mesmo quando a aplicação Olá está em bom estada.
* Uma melhor prática é tooset Olá sonda toosomething de caminho que tem suficiente toodetermine de lógica Olá site é cima ou para baixo. No Olá anterior exemplo, definindo Olá caminho too"/favicon.ico", só são testar essa w3wp.exe está a responder. Esta pesquisa não pode indicar que a sua aplicação web está em bom estada. Uma opção melhor seria tooset tooa um caminho algo como "/ Probe.aspx" que tem o estado de funcionamento do lógica toodetermine Olá do site de Olá. Por exemplo, pode utilizar utilização de tooCPU de contadores de desempenho ou medidas Olá número de pedidos falhados. Ou pode tentar tooaccess recursos de base de dados ou toomake de estado de sessão se a aplicação web de Olá está a funcionar.
* Se todos os pontos finais num perfil estão degradados, em seguida, o Gestor de tráfego processa todos os pontos finais como bom estado de funcionamento e pontos finais de tooall de tráfego de rotas. Este comportamento garante que problemas com Olá pesquisar mecanismo resulta numa falha completa do seu serviço.

## <a name="troubleshooting"></a>Resolução de problemas

tootroubleshoot uma falha de pesquisa, precisa de uma ferramenta que mostra o código de estado HTTP Olá retorno do URL de sonda de Olá. Existem várias ferramentas disponíveis que mostram Olá resposta HTTP não processada.

* [Fiddler](http://www.telerik.com/fiddler)
* [curl](https://curl.haxx.se/)
* [wget](http://gnuwin32.sourceforge.net/packages/wget.htm)

Além disso, pode utilizar o separador de rede Olá de Olá ferramentas de depuração F12 nas respostas HTTP do Internet Explorer tooview Olá.

Para este exemplo queremos resposta de Olá toosee do nosso URL de sonda: http://watestsdp2008r2.cloudapp.net:80/sonda. Olá PowerShell de exemplo a seguir ilustra o problema de Olá.

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

Exemplo de saída:

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

Tenha em atenção que recebemos uma resposta de redirecionamento. Conforme indicado anteriormente, qualquer StatusCode diferente de 200 é considerado uma falha. Alterações do Traffic Manager Olá tooOffline de estado do ponto final. problema de Olá tooresolve, tooensure configuração de Web site de Olá de verificação que Olá StatusCode adequada pode ser devolvido a partir do caminho de pesquisa de Olá. Reconfigure Olá Gestor de tráfego sonda toopoint tooa caminho que devolva uma 200.

Se a sua pesquisa utilizar Olá protocolo HTTPS, poderá ser necessário certificado toodisable verificar erros SSL/TLS tooavoid durante o teste. Olá seguintes declarações de PowerShell desativar a validação de certificado para a sessão atual do PowerShell Olá:

```powershell
add-type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;
public class TrustAllCertsPolicy : ICertificatePolicy {
    public bool CheckValidationResult(
    ServicePoint srvPoint, X509Certificate certificate,
    WebRequest request, int certificateProblem) {
    return true;
    }
}
"@
[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy
```

## <a name="next-steps"></a>Passos Seguintes

[Sobre os métodos de encaminhamento de tráfego do Gestor de tráfego](traffic-manager-routing-methods.md)

[O que é o Gestor de tráfego](traffic-manager-overview.md)

[Serviços Cloud](http://go.microsoft.com/fwlink/?LinkId=314074)

[Aplicações Web do Azure](https://azure.microsoft.com/documentation/services/app-service/web/)

[Operações do Gestor de Tráfego (Referência da API REST)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Cmdlets do Gestor de tráfego do Azure][1]

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
