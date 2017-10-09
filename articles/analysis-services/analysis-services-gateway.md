---
title: gateway de dados de aaaOn local | Microsoft Docs
description: "Um gateway no local é necessário se o servidor de Analysis Services no Azure irá ligar a origens de dados de tooon local."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: cd596155-b608-4a34-935e-e45c95d884a9
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: fc7b9c69e6f81b41deb7a5d6d963225593845d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-tooon-premises-data-sources-with-azure-on-premises-data-gateway"></a>Ligar a origens de dados de tooon local com o Gateway de dados do Azure no local
gateway de dados no local Olá atua como uma ponte, fornecer transferência de proteger os dados entre origens de dados no local e os servidores de serviços de análise do Azure na nuvem de Olá. Adição tooworking com vários servidores do Azure Analysis Services Olá mesma região, a versão mais recente do Olá do gateway de Olá também funciona com Azure Logic Apps, Power BI, aplicações de energia e Flow Microsoft. Pode associar vários serviços no Olá mesma região com um único gateway. 

 Serviços de análise do Azure necessita de um recurso de gateway no Olá mesma região. Por exemplo, se tiver servidores do Azure Analysis Services na região de EUA Leste 2 Olá, precisa de um recurso de gateway na região de EUA Leste 2 Olá. Vários servidores nos EUA Leste 2 podem utilizar Olá mesmo gateway.

Obter a configuração com Olá de gateway Olá pela primeira vez é um processo de quatro partes:

- **Transfira e execute a configuração** -este passo instala um serviço de gateway num computador na sua organização.

- **Registar o gateway** - neste passo, especifique um nome e a chave do seu gateway de recuperação e selecione uma região, registar o gateway Olá serviço em nuvem Gateway.

- **Crie um recurso de gateway no Azure** -neste passo, cria um recurso de gateway na sua subscrição do Azure.

- **Ligar o seu recurso de gateway de tooyour servidores** -depois de ter um recurso de gateway na sua subscrição, pode começar a ligar a sua tooit de servidores.

Depois de ter um recurso de gateway configurado para a sua subscrição, pode ligar vários servidores e outro tooit de serviços. Só precisa de tooinstall um gateway diferentes e criar recursos de gateway adicionais, se tiver servidores ou outros serviços numa região diferente.

tooget os primeiros, consulte [instalar e configurar o gateway de dados no local](analysis-services-gateway-install.md).

## <a name="how-it-works"></a>Como funciona
gateway de Olá instalar num computador na sua organização é executado como um serviço do Windows, **gateway de dados no local**. Este serviço local está registado no Olá serviço em nuvem do Gateway através do Service Bus do Azure. Em seguida, crie um recurso do gateway de serviço em nuvem Gateway para a sua subscrição do Azure. Os serviços de análise do Azure, servidores, em seguida, são ligados tooyour recurso do gateway. Quando os modelos no seu tooyour de tooconnect de necessidade de servidor no local origens de dados para consultas ou processamento, Olá uma consulta e dados fluxo traverses Olá recurso do gateway, Service Bus do Azure, o serviço de gateway de dados local no local e as origens de dados. 

![Como funciona](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

Fluxo de dados e consultas:

1. Uma consulta é criada pelo serviço de nuvem Olá com credenciais de Olá encriptado para a origem de dados do Olá no local. Em seguida, enviou tooa fila para Olá tooprocess de gateway.
2. o serviço de nuvem do gateway Olá analisa a consulta de Olá e pushes Olá pedido toohello [Service Bus do Azure](https://azure.microsoft.com/documentation/services/service-bus/).
3. gateway de dados no local Olá consulta Olá Service Bus do Azure para pedidos pendentes.
4. gateway de Olá obtém consulta Olá, desencripta credenciais Olá e liga toohello origens de dados com essas credenciais.
5. gateway de Olá envia a origem de dados do Olá consulta toohello para execução.
6. resultados de Olá são enviados da origem de dados de Olá, gateway de back-toohello e, em seguida, no serviço de nuvem Olá e o seu servidor.

## <a name="windows-service-account"></a>Conta de serviço do Windows
Olá gateway de dados no local é configurado toouse *NT SERVICE\PBIEgwService* para credenciais de início de sessão de serviço de Windows hello. Por predefinição, ela tem Olá direito de início de sessão como um serviço; no contexto de Olá da máquina de Olá que estiver a instalar o gateway de Olá no. Esta credencial não é Olá mesma conta utilizada tooconnect tooon local as origens de dados ou a sua conta do Azure.  

Se ocorrerem problemas com o seu servidor proxy que devem estar tooauthentication, poderá ser útil toochange hello Windows tooa utilizador de domínio da conta de serviço ou geridos por conta de serviço.

## <a name="ports"></a>Portas
gateway de Olá cria uma ligação de saída de tooAzure Service Bus. Comunica nas portas de saída: TCP 443 (predefinição), 5671, 5672, 9350 através de 9354.  gateway de Olá não necessita de porta de entrada.

Recomendamos que endereços IP de Olá de lista de permissões para a região de dados na sua firewall. Pode transferir Olá [lista IP de centro de dados do Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653). Esta lista é atualizada semanalmente.

> [!NOTE]
> Endereços de IP de Olá listado na lista de IP de Datacenter do Azure Olá estão em notação CIDR. Por exemplo, 10.0.0.0/24 não significa 10.0.0.0 através de 10.0.0.24. Saiba mais sobre Olá [notação CIDR](http://whatismyipaddress.com/cidr).
>
>

Olá seguem-se os nomes de domínio Olá totalmente qualificado utilizados pelo Olá gateway.

| Nomes de domínio | Portas de saída | Descrição |
| --- | --- | --- |
| *. powerbi.com |80 |HTTP utilizado toodownload Olá instalador. |
| *. powerbi.com |443 |HTTPS |
| *. analysis.windows.net |443 |HTTPS |
| *. login.windows.net |443 |HTTPS |
| *. servicebus.windows.net |5671-5672 |(AMQP) do protocolo de colocação de mensagens de avançadas |
| *. servicebus.windows.net |443, 9350-9354 |Serviços de escuta barramento de serviço de reencaminhamento através de TCP (443 é necessária para a aquisição de token de controlo de acesso) |
| *. frontend.clouddatahub.net |443 |HTTPS |
| *. core.windows.net |443 |HTTPS |
| login.microsoftonline.com |443 |HTTPS |
| *. msftncsi.com |443 |Utilizar a conectividade à internet tootest esteja inacessível por Olá serviço Power BI gateway Olá. |
| *.microsoftonline p.com |443 |Utilizado para autenticação, dependendo da configuração. |

### <a name="force-https"></a>Forçar a comunicação HTTPS com o Service Bus do Azure
Pode forçar Olá toocommunicate de gateway com o Service Bus do Azure através de HTTPS em vez do TCP direto; No entanto, fazê-lo, por isso, pode reduzir significativamente desempenho. Pode modificar Olá *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* ficheiro alterando o valor Olá `AutoDetect` demasiado`Https`. Este ficheiro está normalmente localizado em *gateway de dados do local com o c:\Programas\Microsoft Files\On*.

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <a name="faq"></a>Perguntas mais frequentes

### <a name="general"></a>Geral

**Q**: É necessário um gateway para origens de dados na nuvem de Olá, tais como SQL Database do Azure? <br/>
**A**: não. Um gateway se ligar a origens de dados de tooon local apenas.

**Q**: gateway de Olá possui toobe instalado no mesmo computador como origem de dados de Olá de Olá? <br/>
**A**: não. gateway de Olá liga-se a origem de dados de toohello utilizando as informações da ligação de Olá foi fornecidas. Considere gateway Olá como uma aplicação de cliente neste sentido. Olá gateway apenas tem de ser Olá capacidade tooconnect toohello nome do servidor que foi fornecida, normalmente em Olá mesma rede.

<a name="why-azure-work-school-account"></a>

**Q**: por que motivo precisa toouse escolar ou profissional toosign de conta no? <br/>
**A**: pode apenas utilizar um trabalho do Azure conta escolar ou profissional ao instalar o gateway de dados do Olá no local. A conta de início de sessão é armazenada num inquilino gerida pelo Azure Active Directory (Azure AD). Normalmente, o nome de principal de utilizador (UPN) da sua conta do Azure AD corresponde ao endereço de correio eletrónico Olá.

**Q**: onde são as minhas credenciais armazenadas? <br/>
**A**: credenciais de Olá que introduziu para uma origem de dados são encriptadas e armazenadas em Olá serviço em nuvem Gateway. credenciais de Olá são desencriptadas no gateway de dados do Olá no local.

**Q**: existem quaisquer requisitos de largura de banda de rede? <br/>
**A**: recomendada a sua rede de ligação tem boa débito. Cada ambiente é diferente e resultados de Olá afeta a quantidade de Olá de dados que está a ser enviados. Com o ExpressRoute pode ajudar a tooguarantee um nível de débito no local e Olá centros de dados do Azure.
Pode utilizar Olá ferramenta de terceiros Azure velocidade teste aplicação toohelp medidor o débito.

**Q**: o que é a latência de Olá executar consultas tooa origem de dados do gateway de Olá? O que é a arquitetura de melhor Olá? <br/>
**A**: tooreduce latência de rede, instalar o gateway de Olá como origem de dados de fecho toohello quanto possível. Se pode instalar o gateway de Olá na origem de dados real de Olá, este proximidade minimiza a latência de Olá introduzida. Considere demasiado Olá centros de dados. Por exemplo, se o serviço utiliza o Centro de dados do Olá EUA oeste e tiver o SQL Server alojado numa VM do Azure, a VM do Azure deve estar no Olá EUA oeste demasiado. Este proximidade minimiza a latência e evita os encargos associados à saída no Olá VM do Azure.

**Q**: como são resultados enviados back toohello nuvem? <br/>
**A**: os resultados são enviados através de Olá Service Bus do Azure.

**Q**: existem qualquer gateway toohello de ligações de entrada da nuvem Olá? <br/>
**A**: não. gateway de Olá utiliza ligações de saída tooAzure Service Bus.

**Q**: E se bloquear o ligações de saída? O que fazer necessário tooopen? <br/>
**A**: consulte as portas de Olá e os anfitriões que Olá utiliza de gateway.

**Q**: O serviço do Windows real Olá denomina?<br/>
**A**: nos serviços de gateway Olá denomina-se o serviço de gateway de dados no local.

**Q**: pode Olá o serviço de gateway do Windows são executado com uma conta do Azure Active Directory? <br/>
**A**: não. Olá serviço do Windows tem de ter uma conta do Windows válida. Por predefinição, o serviço de Olá é executado com Olá SID de serviço, NT SERVICE\PBIEgwService.

### <a name="high-availability"></a>Elevada disponibilidade e recuperação após desastre

**Q**: que opções estão disponíveis para recuperação após desastre? <br/>
**A**: pode utilizar toorestore de chave de recuperação de Olá ou mover um gateway. Quando instalar o gateway de Olá, especifique a chave de recuperação Olá.

**Q**: o que é a vantagem de Olá da chave de recuperação Olá? <br/>
**A**: chave de recuperação Olá fornece uma forma toomigrate ou recuperar as definições do gateway após desastres.

## <a name="troubleshooting"></a>Resolução de problemas

**Q**: como posso ver quais as consultas estão a ser enviadas a origem de dados no local toohello? <br/>
**A**: pode ativar o rastreio de consulta, que inclui as consultas de Olá que são enviadas. Lembre-se a consulta de toochange rastreio novamente toohello valor original quando terminar de resolução de problemas. Abandonar o fileparser o rastreio de consulta ativado cria registos de maior.

Também pode ver as ferramentas que tenha a sua origem de dados para consultas de rastreio. Por exemplo, pode utilizar o evento expandido ou gerador de perfis do SQL Server para o SQL Server e do Analysis Services.

**Q**: onde estão os registos do gateway de Olá? <br/>
**A**: consulte os registos mais tarde deste tópico.

### <a name="update"></a>Atualizar a versão mais recente toohello

Muitos problemas podem superfície quando a versão do gateway Olá fica desatualizado. Como boa prática geral, certifique-se de que utiliza a versão mais recente Olá. Se ainda não atualizado gateway Olá durante um mês ou mais, que considere instalar Olá a versão mais recente do gateway de Olá e veja se pode reproduzir o problema de Olá.

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a>Erro: Falha tooadd toogroup de utilizador. (-2147463168 PBIEgwService desempenho registo utilizadores)

Pode obter este erro se tentar gateway de Olá tooinstall num controlador de domínio, que não é suportado. Certifique-se de que implementa o gateway de Olá num computador que não é um controlador de domínio.

## <a name="logs"></a>Registos

Ficheiros de registo são um recurso importante quando a resolução de problemas.

#### <a name="enterprise-gateway-service-logs"></a>Registos do serviço de gateway de empresa

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a>Registos de configuração

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a>Registos de eventos

Pode encontrar Olá Data Management Gateway e PowerBIGateway registos em **registos de serviços e aplicações**.


## <a name="telemetry"></a>Telemetria
Telemetria pode ser utilizada para monitorização e resolução de problemas. Por predefinição

**tooturn telemetria**

1.  Verifique o diretório de cliente do gateway do Olá no local dados no computador de Olá. Normalmente, é **gateway de dados de %systemdrive%\Program Files\On local**. Em alternativa, pode abrir uma consola de serviços e verifique Olá caminho tooexecutable: uma propriedade do serviço de gateway de dados do Olá no local.
2.  No ficheiro de Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config Olá do directory do cliente. Altere Olá SendTelemetry definição tootrue.
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  Guarde as alterações e reinicie o serviço do Windows hello: o serviço de gateway de dados no local.




## <a name="next-steps"></a>Passos seguintes
* [Gerir do Analysis Services](analysis-services-manage.md)
* [Obter dados a partir do Azure Analysis Services](analysis-services-connect.md)
