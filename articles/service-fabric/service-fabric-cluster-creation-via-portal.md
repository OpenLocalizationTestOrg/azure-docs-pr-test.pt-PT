---
title: "cluster de aaaCreate Service Fabric no Olá portal do Azure | Microsoft Docs"
description: "Este artigo descreve como tooset configurar um cluster do Service Fabric seguro no Azure com Olá portal do Azure e o Cofre de chaves do Azure."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a>Criar um cluster do Service Fabric no Azure utilizando o Olá portal do Azure
> [!div class="op_single_selector"]
> * [Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
> * [Portal do Azure](service-fabric-cluster-creation-via-portal.md)
> 
> 

Este é um guia passo a passo que explica Olá passos de configuração de um cluster do Service Fabric seguro no Azure utilizando o Olá portal do Azure. Este guia explica Olá os seguintes passos:

* Configure as chaves de toomanage do Cofre de chaves de segurança do cluster.
* Crie um cluster protegido no Azure através de Olá portal do Azure.
* Autentica os administradores a utilização de certificados.

> [!NOTE]
> Para opções de segurança mais avançadas, como a autenticação de utilizador no Azure Active Directory e como configurar certificados para a segurança da aplicação, [criar o cluster com o Azure Resource Manager][create-cluster-arm].
> 
> 

Um cluster seguro é um cluster que impede que as operações de acesso não autorizado toomanagement, que inclui implementar, atualizar e eliminar dados de Olá contêm, serviços e aplicações. Um cluster não seguro é um cluster que qualquer pessoa pode ligar tooat qualquer altura e efetuar operações de gestão. Embora seja possível toocreate um cluster não seguro, é **altamente recomendado toocreate um cluster seguro**. Um cluster não seguro **não pode ser protegida mais tarde** -tem de ser criado um novo cluster.

conceitos de Olá são Olá iguais para a criação de clusters seguros, quer clusters Olá clusters do Linux ou clusters do Windows. Para mais informações e do programa auxiliar de scripts para a criação de clusters seguros do Linux, consulte [criação de clusters seguros no Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters). Olá parâmetros obtidos pelo script de programa auxiliar de Olá fornecida podem ser introduzidos diretamente no portal de Olá conforme descrito na secção de Olá [cria um cluster no portal do Azure de Olá](#create-cluster-portal).

## <a name="log-in-tooazure"></a>Inicie sessão no tooAzure
Este guia utiliza [Azure PowerShell][azure-powershell]. Ao iniciar uma nova sessão do PowerShell, inicie sessão no tooyour a conta do Azure e selecionar a sua subscrição antes de executar os comandos do Azure.

Inicie sessão na conta tooyour do azure:

```powershell
Login-AzureRmAccount
```

Selecione a sua subscrição:

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a>Configurar o Cofre de Chaves
Esta parte do guia de Olá explica como criar um cofre de chave para um cluster do Service Fabric no Azure e para aplicações de Service Fabric. Para obter um guia completo no Cofre de chaves, consulte Olá [Cofre de chaves guia de introdução][key-vault-get-started].

O Service Fabric utiliza toosecure de certificados x. 509 um cluster. O Cofre de chaves do Azure é toomanage utilizados certificados para clusters de Service Fabric no Azure. Quando um cluster é implementado no Azure, o fornecedor de recursos do Azure de Olá responsável pela criação de clusters de Service Fabric obtém certificados a partir do Cofre de chaves e instala-los num cluster de Olá VMs.

Olá diagrama seguinte ilustra Olá relação entre o Cofre de chaves, um cluster do Service Fabric e fornecedor de recursos do Azure de Olá que utiliza certificados armazenados no Cofre de chaves quando cria um cluster:

![Instalação do certificado][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>Criar um Grupo de Recursos
Step-by-Olá primeiro passo é toocreate um novo grupo de recursos especificamente para o Cofre de chaves. Colocar o Cofre de chaves ao seu próprio grupo de recursos é recomendado, para que possa remover grupos de recursos de computação e armazenamento - como grupo de recursos de Olá que tenha o seu cluster do Service Fabric - sem perder as chaves e segredos. grupo de recursos de Olá que tenha o seu Cofre de chaves tem de constar Olá mesma região que o cluster de Olá que está a ser utilizado.

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a>Criar Cofre de chaves
Crie um cofre de chaves no novo grupo de recursos Olá. Olá Cofre de chaves **tem de estar ativado para a implementação** tooallow Olá certificados tooget de fornecedor de recursos do Service Fabric do mesmo e instalar em nós de cluster:

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```

Se tiver um cofre de chaves existente, pode ativá-la para implementação utilizando a CLI do Azure:

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a>Adicione certificados tooKey Cofre
Os certificados são utilizados no Service Fabric tooprovide autenticação e encriptação toosecure diferentes aspetos de um cluster e respetivas aplicações. Para obter mais informações sobre como os certificados são utilizados no Service Fabric, consulte [cenários de segurança de cluster do Service Fabric][service-fabric-cluster-security].

### <a name="cluster-and-server-certificate-required"></a>Cluster e servidor de certificado (obrigatório)
Este certificado é necessário toosecure um cluster e impedir o acesso não autorizado tooit. Fornece segurança de cluster de algumas formas:

* **Autenticação do cluster:** autentica o nó de nó de comunicação para a Federação de cluster. Apenas nós que podem provar a sua identidade com este certificado podem associar cluster Olá.
* **Autenticação de servidor:** autentica Olá cluster pontos finais tooa gestão cliente de gestão, para hello cliente de gestão sabe que está a falar com toohello real cluster. Este certificado fornece também SSL para Olá API de gestão HTTPS e para o Service Fabric Explorer através de HTTPS.

tooserve estes fins, certificado Olá têm de cumprir os requisitos de Olá:

* certificado de Olá tem de conter uma chave privada.
* certificado de Olá tem de ser criado para a troca de chaves, tooa exportável ficheiro Personal Information Exchange (. pfx).
* Olá nome do requerente do certificado deve corresponder ao cluster do Service Fabric Olá domínio utilizado tooaccess Olá. Este é necessário tooprovide SSL para do cluster Olá pontos finais de gestão HTTPS e Service Fabric Explorer. Não é possível obter um certificado SSL a partir de uma autoridade de certificação (AC) para Olá `.cloudapp.azure.com` domínio. Adquirir um nome de domínio personalizado para o cluster. Quando solicita um certificado do nome do requerente de um certificado de Olá de AC tem de corresponder ao nome de domínio personalizado de Olá utilizado para o cluster.

### <a name="client-authentication-certificates"></a>Certificados de autenticação de cliente
Certificados de cliente adicionais autenticar os administradores para tarefas de gestão do cluster. Serviço de recursos de infraestrutura tem dois níveis de acesso: **admin** e **utilizador só de leitura**. No mínimo, um único certificado para acesso administrativo deve ser utilizado. Para acesso de nível de utilizador adicionais, tem de ser fornecido um certificado diferente. Para obter mais informações sobre funções de acesso, consulte [controlo de acesso baseado em funções para clientes de Service Fabric][service-fabric-cluster-security-roles].

Não é necessário tooupload cliente autenticação certificados tooKey cofre toowork com o Service Fabric. Estes certificados basta toobe fornecido toousers que têm autorização para gestão de clusters. 

> [!NOTE]
> Azure Active Directory é Olá recomendado clientes tooauthenticate de forma para o cluster operações de gestão. toouse do Azure Active Directory, tem de [criar um cluster com o Azure Resource Manager][create-cluster-arm].
> 
> 

### <a name="application-certificates-optional"></a>Certificados de aplicação (opcionais)
Qualquer número de certificados adicionais pode ser instalado num cluster por motivos de segurança da aplicação. Antes de criar o cluster, considere os cenários de segurança de aplicação Olá que requerem toobe um certificado instalado em nós de Olá, tal como:

* Encriptação e desencriptação de valores de configuração de aplicação
* Encriptação dos dados em nós durante a replicação 

Certificados de aplicação não podem ser configurados quando criar um cluster através de Olá portal do Azure. certificados de aplicação tooconfigure no momento da configuração de cluster, tem de [criar um cluster com o Azure Resource Manager][create-cluster-arm]. Também pode adicionar o cluster de toohello de certificados de aplicação depois de terem sido criadas.

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>Formatação certificados para utilização do fornecedor de recursos do Azure
Ficheiros de chave privados (. pfx) podem ser adicionados e podem ser utilizados diretamente através do Cofre de chaves. No entanto, o fornecedor de recursos do Azure de Olá requer toobe chaves armazenada no formato JSON especial que inclui. pfx de Olá como uma base-64 codificada cadeia e Olá privada chave palavra-passe. tooaccommodate estes requisitos, as chaves têm de ser colocados numa cadeia JSON e, em seguida, armazenados como *segredos* no Cofre de chaves.

toomake este processo mais fácil, um módulo do PowerShell está [está disponível no GitHub][service-fabric-rp-helpers]. Siga o módulo de Olá de toouse estes passos:

1. Transferir o conteúdo completo de Olá do repositório de Olá para um diretório local. 
2. Importe o módulo Olá na janela do PowerShell:

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

Olá `Invoke-AddCertToKeyVault` comando neste módulo PowerShell automaticamente formatos uma chave privada do certificado numa cadeia JSON e carrega-tooKey cofre. Utilize-o certificado de cluster de Olá tooadd e qualquer tooKey de certificados de aplicação adicional cofre. Repita este passo para todos os certificados adicionais que pretende tooinstall no seu cluster.

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

Estes são todos os pré-requisitos do Cofre de chaves de Olá para configurar um modelo de Gestor de recursos de cluster de Service Fabric que instala os certificados para autenticação de nó, segurança ponto a ponto de gestão e a autenticação e qualquer segurança adicional das aplicações funcionalidades que utilizam certificados x. 509. Neste momento, agora, deve ter Olá a seguinte configuração no Azure:

* Grupo de recursos do Cofre de chaves
  * Cofre de Chaves
    * Certificado de autenticação de servidor de cluster

< /a "Criar-cluster-portal" ></a>

## <a name="create-cluster-in-hello-azure-portal"></a>Criar cluster no Olá portal do Azure
### <a name="search-for-hello-service-fabric-cluster-resource"></a>Procurar Olá recurso de cluster do Service Fabric
![Procure o modelo de cluster do Service Fabric no Olá portal do Azure.][SearchforServiceFabricClusterTemplate]

1. Inicie sessão no toohello [portal do Azure][azure-portal].
2. Clique em **novo** tooadd um novo modelo de recursos. Pesquisa para o modelo de Cluster do Service Fabric Olá no Olá **Marketplace** em **tudo**.
3. Selecione **Cluster do Service Fabric** da lista de Olá.
4. Navegue toohello **Cluster do Service Fabric** painel, clique em **criar**,
5. Olá **cluster do Service Fabric criar** painel tem Olá quatro passos a seguir.

#### <a name="1-basics"></a>1. Noções básicas
![Captura de ecrã da criação de um novo grupo de recursos.][CreateRG]

No painel de noções básicas de Olá terá detalhes básicos do tooprovide Olá para o cluster.

1. Introduza o nome de Olá do cluster.
2. Introduza um **nome de utilizador** e **palavra-passe** para ambiente de trabalho remoto para Olá VMs.
3. Certifique-se de que tooselect Olá **subscrição** que pretende que o toobe cluster implementada, especialmente se tiver várias subscrições.
4. Criar um **novo grupo de recursos**. É melhor toogive-Olá mesmo nome do cluster de Olá, uma vez que o ajuda a localizar mais tarde, especialmente quando estiver a tentar toomake alterações tooyour implementação ou eliminar o cluster.
   
   > [!NOTE]
   > Embora, pode decidir toouse um grupo de recursos existente, é uma boa prática toocreate um novo grupo de recursos. Isto torna toodelete fácil clusters que não é necessário.
   > 
   > 
5. Selecione Olá **região** do qual pretende que o cluster de Olá toocreate. Tem de utilizar Olá consta mesma região que a chave do cofre.

#### <a name="2-cluster-configuration"></a>2. Configuração de cluster
![Criar um tipo de nó][CreateNodeType]

Configure os nós do cluster. Definem os tipos de nó tamanhos de VM Olá, Olá número de VMs e as respetivas propriedades. O cluster pode ter mais do que um tipo de nó, mas o tipo de nó principal Olá (Olá primeiro uma por si no portal de Olá) tem de ter, pelo menos, cinco VMs, que é o tipo de nó olá onde são colocados serviços do sistema de Service Fabric. Não configure **as propriedades de colocação** porque uma propriedade de posicionamento predefinido de "NodeTypeName" é adicionada automaticamente.

> [!NOTE]
> Um cenário comum para vários tipos de nó é uma aplicação que contém um serviço front-end e um serviço de back-end. Pretende que o serviço de front-end Olá tooput em VMs mais pequenos (tamanhos de VM, como D2) com portas abertas toohello Internet, mas quiser o serviço de back-end de Olá tooput em VMs maior (com tamanhos de VM, como D4, D6, D15 e assim sucessivamente) com não abrir as portas para a Internet.
> 
> 

1. Escolha um nome para o seu tipo de nó (1 too12 carateres apenas letras e números).
2. Olá mínimo **tamanho** de VMs para o nó principal Olá, tipo é suscitada pelo departamento por Olá **durabilidade** camada que escolher para cluster Olá. predefinição de Olá para o escalão de durabilidade Olá é bronze. Para obter mais informações sobre a durabilidade, consulte [como toochoose Olá Service Fabric fiabilidade e cluster durabilidade][service-fabric-cluster-capacity].
3. Selecione o tamanho da VM Olá e escalão de preço. VMs de série D tem unidades SSD e são altamente recomendadas para aplicações com monitorização de estado. Não utilizar qualquer SKU de VM que tenha núcleos parciais ou de ter menos de 7 GB de capacidade de disco disponível. 
4. Olá mínimo **número** de VMs para o nó principal Olá, tipo é suscitada pelo departamento por Olá **fiabilidade** camada que escolher. predefinição de Olá para o escalão de fiabilidade Olá é Silver. Para obter mais informações sobre a fiabilidade, consulte [como toochoose Olá Service Fabric fiabilidade e cluster durabilidade][service-fabric-cluster-capacity].
5. Escolha o número de Olá de VMs para o tipo de nó Olá. Pode aumentar ou reduzir verticalmente o número de Olá de VMs num tipo de nó mais tarde, mas no tipo de nó principal Olá, Olá mínimo é controlada por nível de fiabilidade Olá que escolheu. Outros tipos de nó podem ter um mínimo de 1 VM.
6. Configure pontos finais personalizados. Este campo permite-lhe tooenter uma lista separada por vírgulas de portas que pretende que o tooexpose Olá toohello de Balanceador de carga do Azure através da Internet pública para as suas aplicações. Por exemplo, se planear toodeploy um cluster de tooyour de aplicação web, introduza "80" aqui tooallow tráfego na porta 80 para o cluster. Para obter mais informações sobre os pontos finais, consulte [comunicar com aplicações][service-fabric-connect-and-communicate-with-services]
7. Configurar o cluster **diagnóstico**. Por predefinição, o diagnóstico está ativado no seu tooassist de cluster com a resolução de problemas. Se quiser toodisable diagnóstico alterar Olá **estado** alternar demasiado**desativar**. Desativar diagnostics é **não** recomendado.
8. Selecione Olá pretende que o cluster de conjunto o modo de atualização de recursos de infraestrutura. Selecione **automática**, se pretende Olá sistema tooautomatically escolha segurança Olá versão mais recente disponível e tente tooupgrade tooit o cluster. Definir o modo de Olá demasiado**Manual**, se pretender toochoose uma versão suportada.

> [!NOTE]
> Suportamos apenas os clusters que executam versões suportadas do serviço de recursos de infraestrutura. Ao selecionar Olá **Manual** modo, que está a efetuar no Olá responsabilidade tooupgrade a versão de tooa suportada do cluster. Para obter mais detalhes sobre o modo de atualização de recursos de infraestrutura do Olá Consulte Olá [documento de serviço--cluster-atualização do fabric.][service-fabric-cluster-upgrade]
> 
> 

#### <a name="3-security"></a>3. Segurança
![Captura de ecrã das configurações de segurança no portal do Azure.][SecurityConfigs]

passo final Olá é tooprovide certificado informações toosecure Olá de cluster utilizando Olá Cofre de chaves e certificados informações criada anteriormente.

* Preencher os campos de certificados primários de Olá com a saída de Olá obtida a partir do carregamento Olá **certificado de cluster** tooKey cofre utilizando Olá `Invoke-AddCertToKeyVault` comando do PowerShell.

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* Verifique Olá **configurar as definições avançada** caixa tooenter certificados de cliente para **admin cliente** e **clientes apenas de leitura**. Nestes campos, introduza o thumbprint Olá do seu certificado de cliente de administrador e thumbprint Olá do seu certificado de cliente de utilizador só de leitura, se aplicável. Quando os administradores tentam tooconnect toohello cluster, são concedidos acesso apenas se tiverem um certificado com um thumbprint que corresponda a valores de thumbprint Olá introduzido aqui.  

#### <a name="4-summary"></a>4. Resumo
![Captura de ecrã do painel de início de Olá apresentar "Implementar Cluster do Service Fabric." ][Notifications]

criação do cluster de toocomplete Olá, clique em **resumo** configurações de Olá toosee que forneceu ou transferir Olá modelo Azure Resource Manager que que utilizado toodeploy o cluster. Depois de ter fornecido definições obrigatórias Olá, Olá **OK** botão fica verde e pode iniciar o processo de criação do cluster Olá clicando nela.

Pode ver o progresso da criação Olá em notificações Olá. (Clique ícone de campainha"Olá" junto da barra de estado de Olá na Olá canto superior direito do ecrã). Se clicou em **Pin tooStartboard** ao criar o cluster de Olá, verá **implementação de Cluster do Service Fabric** afixado toohello **iniciar** quadro.

### <a name="view-your-cluster-status"></a>Ver o estado do cluster
![Captura de ecrã dos detalhes de cluster no dashboard de Olá.][ClusterDashboard]

Depois do cluster foi criado, pode inspecionar o seu cluster no portal de Olá:

1. Aceda demasiado**procurar** e clique em **Clusters de recursos de infraestrutura de serviço**.
2. Localize o seu cluster e clique no mesmo.
3. Agora, pode ver os detalhes de Olá do cluster no dashboard de Olá, incluindo o ponto de final público do cluster Olá e tooService uma ligação Explorador de recursos de infraestrutura.

Olá **Monitor nó** secção no painel de dashboard do cluster Olá indica o número de Olá de VMs que fazem o bom estado de funcionamento e não em bom estado. Pode encontrar mais detalhes sobre o estado de funcionamento do cluster Olá em [introdução de modelo de estado de funcionamento do Service Fabric][service-fabric-health-introduction].

> [!NOTE]
> Clusters de Service Fabric necessitam de um determinado número de nós toobe segurança sempre toomaintain disponibilidade e preservar o estado - tooas referenciado "manter o quórum". Therfore, normalmente, não é seguro tooshut baixo todas as máquinas do cluster de Olá, exceto se tiver efetuado primeiro um [cópia de segurança completa do seu estado][service-fabric-reliable-services-backup-restore].
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a>Remoto ligar a instância de conjunto de dimensionamento da Máquina Virtual tooa ou um nó de cluster
Cada um dos Olá NodeTypes especificou nos resultados de cluster num conjunto de dimensionamento de Máquina Virtual ao obter a configuração. Consulte [remoto ligar a instância de conjunto de dimensionamento da Máquina Virtual tooa] [ remote-connect-to-a-vm-scale-set] para obter mais detalhes.

## <a name="next-steps"></a>Passos seguintes
Neste momento, tiver um cluster seguro que utilizar certificados para autenticação de gestão. Em seguida, [ligar tooyour cluster](service-fabric-connect-to-secure-cluster.md) e saber como demasiado[gerir segredos de aplicação](service-fabric-application-secret-management.md).  Além disso, saiba mais sobre [as opções de suporte do Service Fabric](service-fabric-support.md).

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
