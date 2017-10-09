---
title: problemas de Data Management Gateway aaaTroubleshoot | Microsoft Docs
description: "Fornece sugestões tootroubleshoot problemas relacionados tooData Management Gateway."
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a>Utilizar o Data Management Gateway para resolver problemas
Este artigo fornece informações sobre como resolver problemas com a utilização do Data Management Gateway.

> [!NOTE]
> Consulte Olá [Data Management Gateway](data-factory-data-management-gateway.md) artigo para obter informações detalhadas sobre o gateway de Olá. Consulte Olá [mover dados entre no local e na nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo para obter instruções de mover dados de um tooMicrosoft de base de dados do SQL Server no local Blob storage do Azure utilizando o gateway de Olá.
>
>

## <a name="failed-tooinstall-or-register-gateway"></a>Gateway de tooinstall ou registar com falhas
### <a name="1-problem"></a>1. Problema
Pode ver esta mensagem de erro quando instalar e registar um gateway, especificamente, ao transferir o ficheiro de instalação do gateway Olá.

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a>Causa
Olá da máquina em que está a tentar o gateway de Olá tooinstall falhou toodownload Olá mais recente gateway ficheiro de instalação do Centro de transferências Olá devido tooa problema de rede.

#### <a name="resolution"></a>Resolução
Verifique a sua toosee de definições de servidor de proxy de firewall se as definições de Olá bloqueiam a ligação de rede Olá do Olá computador toohello [Centro de transferências](https://download.microsoft.com/)e atualizar as definições de Olá em conformidade.

Em alternativa, pode transferir o ficheiro de instalação Olá gateway mais recente Olá da Olá [Centro de transferências](https://www.microsoft.com/download/details.aspx?id=39717) nas outras máquinas que podem aceder ao centro de transferências Olá. Pode, em seguida, o gateway de toohello do ficheiro de instalador do cópia Olá computador anfitrião e executá-la manualmente tooinstall e a atualização de gateway de Olá.

### <a name="2-problem"></a>2. Problema
Este erro ocorrer quando está a tentar tooinstall um gateway clicando **instalar diretamente neste computador** no Olá portal do Azure.

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a>Causa
Já existe um gateway instalado na máquina de Olá.

#### <a name="resolution"></a>Resolução
Desinstalar o gateway existente do Olá na máquina de Olá e clique em Olá **instalar diretamente neste computador** ligar novamente.

### <a name="3-problem"></a>3. Problema
Poderá ver este erro ao registar um novo gateway.

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a>Causa
Poderá ver esta mensagem para uma das Olá seguintes motivos:

* formato de Olá da chave de gateway Olá é inválido.
* chave do gateway Olá foi invalidado.
* a chave de gateway Olá tem foi regenerada do portal de Olá.  

#### <a name="resolution"></a>Resolução
Certifique-se de que o se estiver a utilizar a chave de gateway correto de Olá partir Olá do portal. Se for necessário, voltar a gerar uma chave e utilizar Olá tooregister chave Olá gateway.

### <a name="4-problem"></a>4. Problema
Poderá ver Olá seguir a mensagem de erro quando está a registar um gateway.

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![Conteúdo ou formato de chave é inválido](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a>Causa
Olá conteúdo ou formato de chave do gateway de entrada de Olá está incorreto. Uma das razões Olá pode ser que copiou apenas uma parte da chave de Olá do portal de Olá ou estiver a utilizar uma chave inválida.

#### <a name="resolution"></a>Resolução
Gerar uma chave de gateway no portal de Olá e utilize Olá cópia botão toocopy Olá todo chave. Em seguida, cole-o no gateway de Olá de tooregister janela.

### <a name="5-problem"></a>5. Problema
Poderá ver Olá seguir a mensagem de erro quando está a registar um gateway.

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![Chave do gateway é inválido ou está vazio](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a>Causa
chave do gateway Olá foi regenerada ou gateway Olá foi eliminada no Olá portal do Azure. Também pode acontecer se a configuração do Data Management Gateway Olá não é mais recente.

#### <a name="resolution"></a>Resolução
Verifique se a configuração do Data Management Gateway Olá é uma versão mais recente Olá, pode encontrar a versão mais recente do Olá no Olá Microsoft [Centro de transferências](https://go.microsoft.com/fwlink/p/?LinkId=271260).

Se a configuração atual / mais recente e gateway ainda existe no Portal, regenerar a chave de gateway Olá no Olá portal do Azure e utilizar Olá cópia botão toocopy Olá todo chave e, em seguida, cole-o no gateway de Olá de tooregister janela. Caso contrário, recriar o gateway de Olá e comece de novo.

### <a name="6-problem"></a>6. Problema
Poderá ver Olá seguir a mensagem de erro quando está a registar um gateway.

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![Chave do gateway é inválido ou está vazio](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a>Causa
Este erro pode ter acontecido porque o gateway Olá foi eliminado ou chave de gateway associado Olá foi regenerada.

#### <a name="resolution"></a>Resolução
Se tiverem sido eliminado gateway Olá, voltar a criar gateway de Olá a partir do portal de Olá, clique em **registar**, copie a chave de Olá portal Olá, cole-o e tente o gateway de Olá tooregister.

Se o gateway de Olá ainda existe mas a chave foi regenerada, utilize Olá novo tooregister chave Olá gateway. Se não tiver chave Olá, regenere a chave de Olá novamente a partir do portal de Olá.

### <a name="7-problem"></a>7. Problema
Quando estiver a registar um gateway, poderá ser necessário tooenter caminho e a palavra-passe de um certificado.

![Especifique o certificado](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a>Causa
gateway de Olá foi registado em outras máquinas antes. Durante o registo do Olá inicial de um gateway, um certificado de encriptação foi associado ao gateway Olá. certificado Olá pode ser personalizada gerado pelo gateway de Olá ou fornecido pelo utilizador Olá.  Este certificado é utilizado tooencrypt credenciais Olá do arquivo de dados (serviço ligado).  

![Exportar certificado](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

Quando restaurar gateway Olá no outro computador anfitrião, o Assistente de registo de Olá pede-lhe para toodecrypt este certificado de credenciais anteriormente encriptados com este certificado.  Sem este certificado não não possível desencriptar as credenciais de Olá ao novo gateway de Olá e execuções de atividade de cópia subsequentes associadas a este novo gateway falhará.  

#### <a name="resolution"></a>Resolução
Se exportou certificado da credencial Olá da máquina de gateway original Olá utilizando Olá **exportar** botão Olá **definições** separador no Data Management Gateway do Configuration Manager, utilize Olá certificado aqui.

Não é possível ignorar esta fase ao recuperar um gateway. Se o certificado de Olá está em falta, precisa de gateway de Olá toodelete do portal de Olá e voltar a criar um novo gateway.  Além disso, atualize todos os serviços ligados que estão relacionados toohello gateway por reentering as respetivas credenciais.

### <a name="8-problem"></a>8. Problema
Poderá ver Olá seguir a mensagem de erro.

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a>Causa
Este erro ocorre quando o gateway está num ambiente que requer um tooaccess de proxy HTTP recursos da Internet, ou palavra-passe de autenticação do proxy é alterado, mas não é atualizado em conformidade no seu gateway.

#### <a name="resolution"></a>Resolução
Siga as instruções de Olá Olá [considerações de servidor Proxy](#proxy-server-considerations) secção deste artigo e configurar as definições de proxy com o Data Management Gateway Configuration Manager.

## <a name="gateway-is-online-with-limited-functionality"></a>Gateway está online com funcionalidade limitada
### <a name="1-problem"></a>1. Problema
Ver o estado de Olá do gateway de Olá como online com funcionalidade limitada.

#### <a name="cause"></a>Causa
Ver estado Olá do gateway de Olá como online com funcionalidade limitada para uma das Olá seguintes motivos:

* Gateway não é possível ligar o serviço de toocloud através do Service Bus do Azure.
* Serviço em nuvem não é possível ligar toogateway através do Service Bus.

Quando o gateway de Olá está online com funcionalidade limitada, poderá não ser pipelines de dados do toocreate do toouse capaz de Olá Assistente de cópia do Data Factory para copiar dados tooor de arquivos de dados no local. Como solução, pode utilizar o Editor do Data Factory no portal de Olá, Visual Studio ou o Azure PowerShell.

#### <a name="resolution"></a>Resolução
Resolução para este problema (online com funcionalidade limitada) baseia-se no se o gateway de Olá não é possível ligar o serviço em nuvem toohello ou Olá outra forma. Olá seguintes secções fornece estas resoluções.

### <a name="2-problem"></a>2. Problema
Consulte Olá seguir o erro.

`Error: Gateway cannot connect toocloud service through service bus`

![Gateway não é possível ligar o serviço de toocloud](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a>Causa
Gateway não é possível ligar o serviço em nuvem toohello através do Service Bus.

#### <a name="resolution"></a>Resolução
Siga estes gateway de Olá de tooget de passos online:

1. Permitir o endereço IP no computador do gateway de Olá e de firewall da empresa Olá as regras de saída. Pode localizar endereços IP de Olá registo de eventos do Windows (ID = = 401): uma tentativa de foi efetuada tooaccess um socket de forma proibida pelo respetivos permissões de acesso XX. XX. XX. XX:9350.
* Configure definições de proxy no gateway de Olá. Consulte Olá [considerações de servidor Proxy](#proxy-server-considerations) secção para obter detalhes.
* Ative portas de saída 5671 e 9350-9354 em ambos os Olá Firewall do Windows no computador do gateway de Olá e firewall Olá da empresa. Consulte Olá [portas e firewall](#ports-and-firewall) secção para obter detalhes. Este passo é opcional, mas recomendamos por razões de desempenho de.

### <a name="3-problem"></a>3. Problema
Consulte Olá seguir o erro.

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a>Causa
Um erro transitório na conectividade de rede.

#### <a name="resolution"></a>Resolução
Siga estes gateway de Olá de tooget de passos online:

1. Aguarde alguns minutos, conectividade Olá irá ser recuperada automaticamente quando o erro de Olá é removido.
* Se Olá erro persistir, reinicie o serviço de gateway Olá.

## <a name="failed-tooauthor-linked-service"></a>Serviço de falha tooauthor ligado
### <a name="problem"></a>Problema
Poderá ver este erro quando tentar toouse Gestor de credenciais em credenciais de portal tooinput Olá para um novo serviço ligado ou atualizar as credenciais de um serviço ligado existente.

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

Quando vir este erro, página de definições de Olá do Data Management Gateway Configuration Manager aspeto que poderá ter Olá seguinte captura de ecrã.

![Não é possível contactar a base de dados](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a>Causa
certificado SSL Olá pode ter sido perdido no computador do gateway de Olá. computador do gateway Olá não é possível carregar Olá certificado atualmente que é utilizado para encriptação SSL. Também poderá ver uma mensagem de erro no registo de eventos de Olá que é semelhante toohello seguir a mensagem.

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a>Resolução
Siga o problema de Olá de toosolve estes passos:

1. Inicie o Gestor de configuração do Data Management Gateway.
2. Comutador toohello **definições** separador.  
3. Clique em Olá **alteração** certificado SSL do botão toochange Olá.

   ![Botão de certificado de alteração](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. Selecione um novo certificado como certificado SSL Olá. Pode utilizar qualquer certificado SSL que é gerado por si ou qualquer organização.

   ![Especifique o certificado](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a>Falha da atividade de cópia
### <a name="problem"></a>Problema
É possível que repare Olá seguintes "UserErrorFailedToConnectToSqlserver" falha depois de configurar um pipeline no portal de Olá.

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a>Causa
Isto pode acontecer por diferentes motivos e atenuação varia em conformidade.

#### <a name="resolution"></a>Resolução
Permita ligações de TCP de saída através da porta TCP/1433 no Olá do lado do cliente do Data Management Gateway antes de ligar tooan SQL da base de dados.

Se a base de dados de destino de Olá é uma base de dados SQL do Azure, verifique o SQL Server as definições da firewall para o Azure também.

Consulte Olá seguinte secção tootest Olá ligação toohello no local dados arquivo.

## <a name="data-store-connection-or-driver-related-errors"></a>Ligação de arquivo de dados ou erros relacionados com o controlador
Se vir armazenar erros relacionados com o controlador ou de ligação de dados, conclua Olá os seguintes passos:

1. Inicie o Gestor de configuração do Data Management Gateway no computador do gateway de Olá.
2. Comutador toohello **diagnóstico** separador.
3. No **Testar ligação**, adicione os valores de grupo do Olá gateway.
4. Clique em **teste** toosee se pode ligar toohello no local origem de dados do computador do gateway de Olá utilizando as informações da ligação Olá e as credenciais. Se continuar a ligação de teste de Olá falhar depois de instalar um controlador, reinício Olá gateway para o mesmo toopick segurança alteração mais recente Olá.

![Ligação de teste no separador de diagnóstico](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a>Registos do gateway
### <a name="send-gateway-logs-toomicrosoft"></a>Enviar tooMicrosoft de registos do gateway
Quando contactar a ajuda de tooget Support da Microsoft com a resolução de problemas de gateway, poderá ser-lhe pedido tooshare os registos do gateway. Com a versão de Olá do gateway de Olá, pode partilhar os registos de gateway necessária com dois cliques de botão no Data Management Gateway do Configuration Manager.    

1. Comutador toohello **diagnóstico** separador no Data Management Gateway do Configuration Manager.

    ![Separador de diagnóstico do Gateway de gestão de dados](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. Clique em **enviar registos de** Olá toosee seguintes da caixa de diálogo.

    ![Registos de envio de Gateway de gestão de dados](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. (Opcional) Clique em **ver registos** tooreview registos no Visualizador de eventos de Olá.
4. (Opcional) Clique em **privacidade** tooreview web da Microsoft dos serviços de declaração de privacidade.
5. Quando estiver satisfeito com o que está prestes a tooupload, clique em **enviar registos de** tooactually enviar registos de Olá dos últimos sete dias tooMicrosoft Olá para resolução de problemas. Deverá ver o estado Olá da operação de envio registos Olá conforme mostrado na seguinte captura de ecrã de Olá.

    ![Data Management Gateway enviar registos de estado](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. Depois de concluída a operação de Olá, verá uma caixa de diálogo conforme mostrado na seguinte captura de ecrã de Olá.

    ![Data Management Gateway enviar registos de estado](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. Guardar Olá **relatório ID** e partilhá-las com Support da Microsoft. Olá relatório ID é utilizado toolocate Olá gateway os registos que carregou para resolução de problemas.  ID de relatório Olá também é guardada no Visualizador de eventos de Olá.  Pode encontrá-lo ao observar o ID de evento "25" Olá e verifique Olá data e hora.

    ![Data Management Gateway enviar registos de ID de relatório](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a>Gateway de arquivo os registos de computador do anfitrião de gateway
Existem alguns cenários em que tiver problemas de gateway e não pode partilhar os registos do gateway diretamente:

* Se instalar manualmente o gateway de Olá e registar o gateway de Olá.
* Repita o gateway de Olá tooregister com uma chave gerada novamente no Data Management Gateway do Configuration Manager.
* Tente toosend registos e não é possível ligar o serviço de anfitrião de gateway Olá.

Nestes cenários, pode guardar registos de gateway como um ficheiro zip e partilhá-las quando contactar o suporte da Microsoft. Por exemplo, se receber um erro ao registar o gateway de Olá como mostrado na seguinte captura de ecrã de Olá.   

![Erro de registo de Gateway de gestão de dados](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

Clique em Olá **arquivar registos do gateway** associar tooarchive e guarde os registos e, em seguida, partilhar o ficheiro zip Olá com suporte da Microsoft.

![Registos de arquivo de Gateway de gestão de dados](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a>Localize os registos do gateway
Pode encontrar informações de registo de gateway detalhadas nos registos de eventos do Windows hello.

1. Iniciar o Windows **Visualizador de eventos**.
2. Localize os registos no Olá **registos de serviços e aplicações** > **Data Management Gateway** pasta.

 Quando estiver a resolver problemas relacionados com o gateway, procure eventos ao nível de erro no Visualizador de eventos de Olá.

![O Data Management Gateway se regista no Visualizador de eventos](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
