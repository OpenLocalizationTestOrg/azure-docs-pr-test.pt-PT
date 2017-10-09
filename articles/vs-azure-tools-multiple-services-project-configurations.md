---
title: "aaaConfiguring o projeto do Azure através de várias configurações de serviço | Microsoft Docs"
description: "Saiba como tooconfigure um Azure cloud projeto de serviço alterando Olá servicedefinition. Csdef e serviceconfiguration. Cscfg os ficheiros."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a4fb79ed-384f-4183-9f74-5cac257206b9
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 14222266093eb876db0ac9ce8d3d17a04c65d1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-your-azure-project-using-multiple-service-configurations"></a>Configurar o projeto do Azure através de várias configurações de serviço
Um projeto de serviço em nuvem do Azure inclui dois ficheiros de configuração: servicedefinition. Csdef e serviceconfiguration. Cscfg. Estes ficheiros são reunidos com a sua aplicação de serviço em nuvem do Azure e implementado tooAzure.

* Olá **servicedefinition. Csdef** ficheiro contém os metadados de Olá que é exigido pelo ambiente do Azure para os requisitos de Olá da sua aplicação de serviço em nuvem, incluindo as funções às quais contém de Olá. Este ficheiro também contém as definições de configuração que se aplicam tooall instâncias. Estas definições de configuração podem ser lidos durante a execução Olá API de tempo de execução do alojamento de serviço da Azure a utilizar. Não é possível atualizar este ficheiro enquanto o serviço está em execução no Azure.
* Olá **serviceconfiguration. Cscfg** ficheiro define valores para definições de configuração de Olá definidas no ficheiro de definição de serviço Olá e especifica o número de Olá de instâncias toorun para cada função. Este ficheiro pode ser atualizado enquanto o serviço em nuvem está em execução no Azure.

Ferramentas do Azure Olá para Microsoft Visual Studio fornecem as páginas de propriedade que pode utilizar definições de configuração de tooset armazenadas nesses ficheiros. tooaccess Olá páginas de propriedades, faça duplo clique em referência de função Olá por baixo do projeto de serviço em nuvem do Azure Olá no Explorador de soluções, ou com o botão direito referência Olá da função e escolha **propriedades**, conforme apresentado na Olá figura a seguir.

![VS_Solution_Explorer_Roles_Properties](./media/vs-azure-tools-multiple-services-project-configurations/IC784076.png)

Para obter informações sobre Olá subjacente esquemas para a definição de serviço Olá e ficheiros de configuração de serviço, consulte Olá [esquema referência](https://msdn.microsoft.com/library/azure/dd179398.aspx). Para obter mais informações sobre a configuração do serviço, consulte [como tooConfigure Cloud Services](cloud-services/cloud-services-how-to-configure.md).

## <a name="configuring-role-properties"></a>Configurar as propriedades da função
páginas de propriedades de Olá para uma função da web e uma função de trabalho são semelhantes, embora existam algumas diferenças, indicadas no Olá secções a seguir.

De Olá **colocação em cache** página, pode configurar Olá colocação em cache dos serviços do Azure.

### <a name="configuration-page"></a>Página de configuração
No Olá **configuração** página, pode definir estas propriedades:

**Instâncias**

Conjunto Olá **instância** número da contagem propriedade toohello de instâncias de serviço de Olá deve ser executado para esta função.

Conjunto Olá **tamanho da VM** propriedade demasiado**Extra pequena**, **pequeno**, **média**, **grande**, ou **Extra grande**.  Para obter mais informações, consulte [tamanhos para serviços em nuvem](cloud-services/cloud-services-sizes-specs.md).

**Ação de arranque** (Web função apenas)

Defina este toospecify de propriedade que o Visual Studio deve iniciar um browser para pontos finais de Olá HTTP ou pontos finais HTTPS de hello ou ambos, quando iniciar a depuração.

Olá opção do ponto final HTTPS está disponível apenas se já definiu um ponto final de HTTPS para a sua função. Pode definir um ponto final de HTTPS no Olá **pontos finais** página de propriedades.

Se já tiver adicionado um ponto final de HTTPS, Olá opção do ponto final HTTPS está ativada por predefinição e o Visual Studio irá iniciar um browser para este ponto final quando iniciar depuração, além disso, tooa browser para o ponto final HTTP. Esta parte do princípio de que ambas as opções de arranque estão ativadas.

**Diagnóstico**

Por predefinição, o diagnóstico está ativado para a função da Web Olá. Olá projeto do serviço em nuvem do Azure e a conta de armazenamento estão definidas emulador de armazenamento local toouse Olá. Quando estiver pronto toodeploy tooAzure, pode selecionar o botão de construtor de Olá (**...** ) toouse de conta de armazenamento do tooupdate Olá storage do Azure na nuvem de Olá. Pode transferir a conta de armazenamento de toohello de dados de diagnóstico de Olá a pedido ou em intervalos agendados automaticamente. Para obter mais informações sobre o diagnóstico do Azure, consulte [ativar diagnósticos no Cloud Services do Azure e máquinas virtuais](cloud-services/cloud-services-dotnet-diagnostics.md).

## <a name="settings-page"></a>Página de definições
No Olá **definições** página, pode adicionar as definições de configuração para o seu serviço. Definições de configuração são pares nome-valor. Código em execução numa função de Olá pode ler os valores de Olá das definições de configuração em tempo de execução a utilizar classes fornecidas pelo Olá [biblioteca gerida do Azure](http://go.microsoft.com/fwlink?LinkID=171026). Especificamente, Olá [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx) método devolve o valor de Olá de uma definição de configuração com o nome no tempo de execução.

### <a name="configuring-a-connection-string-tooa-storage-account"></a>Configurar uma conta de armazenamento de tooa de cadeia de ligação
Uma cadeia de ligação é uma definição de configuração que fornece informações de ligação e a autenticação para o emulador do storage Olá ou para uma conta de armazenamento do Azure. Sempre que o seu código tem aceder a dados de serviços de armazenamento do Azure – isto é, blob, fila ou os dados da tabela – a partir do código em execução numa função, tem de toodefine uma cadeia de ligação para essa conta de armazenamento.

Uma cadeia de ligação que aponta a conta de armazenamento do Azure tooan tem de utilizar um formato definido. Para obter informações sobre como ver cadeias de ligação de toocreate [configurar cadeias de ligação de armazenamento do Azure](storage/common/storage-configure-connection-string.md).

Quando estiver pronto tootest seu serviço nos serviços de armazenamento do Azure Olá, ou quando estiver pronto toodeploy sua tooAzure do serviço de nuvem, pode alterar o valor de Olá de qualquer tooyour de toopoint de cadeias de ligação conta do storage do Azure. Selecione (**...** ), selecione **introduza as credenciais da conta de armazenamento**. Introduza as suas informações de conta que inclui o nome da conta e a chave de conta. No Olá **cadeia de ligação de conta de armazenamento** caixa de diálogo, também pode indicar se pretende que toouse Olá predefinido pontos finais de HTTPS (opção predefinida de Olá), pontos finais HTTP do Olá predefinidos ou os pontos finais personalizados. Poderá decidir os pontos finais personalizados toouse se tiver registado um nome de domínio personalizado para o seu serviço, conforme descrito em [configurar um nome de domínio personalizado para dados de BLOBs numa conta de armazenamento do Azure](storage/blobs/storage-custom-domain-name.md).

> [!IMPORTANT]
> Tem de modificar o tooan de toopoint de cadeias de ligação conta do storage do Azure antes de implementar o serviço. A falhar toodo Isto pode fazer com que a função não toostart ou toocycle através de Olá Estados de inicialização, ocupados e parar.
> 
> 

## <a name="endpoints-page"></a>Página pontos finais
Uma função de trabalho pode ter qualquer número de pontos finais HTTP, HTTPS ou TCP. Pontos finais podem ser pontos finais de entrada, que são clientes tooexternal disponível, ou pontos finais internos, que são funções de tooother disponíveis que estão em execução no serviço de Olá.

* clientes do toomake um HTTP endpoint tooexternal disponíveis e browsers da Web, altere tooinput de tipo de ponto final de Olá e especifique um nome e um número de porta pública.
* toomake um HTTPS clientes do endpoint tooexternal disponíveis e browsers da Web, altere o tipo de ponto final de Olá demasiado**entrada**e especifique um nome, um número de porta pública e um nome de certificado de gestão.
  
    Tenha em atenção que antes de especificar um certificado de gestão, tem de definir o certificado de Olá no Olá **certificados** página de propriedades.
* toomake um ponto final disponível para acesso interno por outras funções no serviço de nuvem Olá, altere toointernal de tipo de ponto final de Olá e especifique um nome e portas privadas possíveis para este ponto final.

## <a name="local-storage-page"></a>Página de armazenamento local
Pode utilizar Olá **armazenamento Local** propriedade página tooreserve um ou mais recursos de armazenamento local para uma função. Um recurso de armazenamento local é um diretório reservado no sistema de ficheiros de Olá do Olá máquina virtual do Azure no qual uma instância de uma função está em execução.

## <a name="certificates-page"></a>Página Certificados
No Olá **certificados** página, pode associar certificados a sua função. certificados de Olá que adicionar podem ser utilizado tooconfigure os pontos finais de HTTPS no Olá **pontos finais** página de propriedades.

Olá **certificados** página de propriedades adiciona informações sobre a configuração de serviço de tooyour de certificados. Tenha em atenção que os certificados não são reunidos com o serviço; tem de carregar os certificados em separado tooAzure através de Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).

tooassociate um certificado com a função, forneça um nome para o certificado de Olá. Utilizar este certificado do nome toorefer toohello quando configurar um ponto final de HTTPS no Olá **pontos finais** página de propriedades. Em seguida, especifique se o arquivo de certificados de Olá é **máquina Local** ou **utilizador atual** e nome de Olá do arquivo de Olá. Por fim, introduza o thumbprint do certificado Olá. Se tiver o certificado de Olá Olá User\Personal atual arquivo (meu), pode introduzir o thumbprint do certificado Olá selecionando certificado Olá a partir de uma lista povoada. Se residir em qualquer outra localização, introduza o valor do thumbprint Olá manualmente.

Quando adiciona um certificado do arquivo de certificados de Olá, todos os certificados intermédios são automaticamente adicionados toohello definições de configuração para si. Estes certificados intermédios também é necessário carregar tooAzure na ordem toocorrectly configurar o seu serviço para SSL.

Quaisquer certificados de gestão que associa o seu serviço aplicam serviço tooyour apenas quando está a ser executado na nuvem de Olá. Quando o serviço está em execução no ambiente de desenvolvimento local Olá, utiliza um certificado padrão que é gerido pelo emulador de computação Olá.

## <a name="configuring-hello-azure-cloud-service-project"></a>Configurar o projeto de serviço em nuvem do Azure Olá
definições de tooconfigure que se aplicam projeto de serviço em nuvem do Azure completo tooan, primeiro abrir menu de atalho Olá para esse nó do projeto e, em seguida, escolha Propriedades tooopen respetivas páginas de propriedades. Olá, a tabela seguinte mostra as páginas de propriedades.

| Página de propriedades | Descrição |
| --- | --- |
| Aplicação |Nesta página, pode apresentar informações sobre a versão de Olá das ferramentas do Azure que utiliza este projeto de serviço de nuvem e pode atualizar a versão atual do toohello das ferramentas de Olá. |
| Criar eventos |Nesta página, pode definir os eventos de compilação pré e pós-implementação compilação. |
| Desenvolvimento |Nesta página, pode especificar as instruções de configuração de compilação e condições de Olá sob a qual são executados quaisquer eventos de compilação pós-implementação. |
| Web |Nesta página, pode configurar as definições relacionadas com o servidor de web toohello. |

