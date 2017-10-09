---
title: "aaaCreating uma imagem de máquina virtual para Olá Azure Marketplace | Microsoft Docs"
description: "Instruções detalhadas sobre como toocreate uma máquina virtual de imagem para Olá Azure Marketplace para outros toopurchase."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5c937b8e-e28d-4007-9fef-624046bca2ae
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio; v-divte
ms.openlocfilehash: 65e1c0530bb050fb379a52544e36c55faacd84df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-virtual-machine-image-for-hello-azure-marketplace"></a>Guia toocreate uma imagem de máquina virtual para Olá Azure Marketplace
Neste artigo, **passo 2**, explica como preparar Olá de discos rígidos virtuais (VHDs) que irão implementar toohello Azure Marketplace. Os VHDs estão foundation Olá do seu SKU. processo de Olá difere dependendo se está a fornecer um SKU baseado em Windows ou baseado em Linux. Este artigo abrange ambos os cenários. Este processo pode ser executado em paralelo com [conta criação e registo][link-acct-creation].

## <a name="1-define-offers-and-skus"></a>1. Definir ofertas e SKUs
Nesta secção, saiba toodefine Olá ofertas e os respetivos SKUs associados.

Uma oferta é tooall um "principal" do respetivos SKUs. Pode ter várias ofertas. Como decidir toostructure suas ofertas está ativo tooyou. Quando é emitida uma oferta toostaging, é enviada juntamente com todos os SKUs. Considere cuidadosamente os identificadores SKU, porque estará visíveis no URL Olá:

* Azure.com: http://azure.microsoft.com/marketplace/partners/ {PartnerNamespace} / {OfferIdentifier}-{SKUidentifier}
* Portal de pré-visualização do Azure: https://portal.azure.com/#gallery/ {PublisherNamespace}. {OfferIdentifier} {SKUIDdentifier}  

Um SKU é Olá nome comerciais uma imagem de VM. Uma imagem de VM contém disco de um sistema operativo e zero ou mais discos de dados. É, essencialmente, Olá concluída perfil de armazenamento para uma máquina virtual. É necessário um VHD por disco. Os discos de dados, mesmo em branco requerem um toobe VHD criado.

Independentemente do sistema operativo que utiliza, adicione apenas Olá número mínimo de discos de dados necessários para Olá SKU. Os clientes não é possível remover discos que fazem parte de uma imagem momento Olá da implementação, mas podem sempre adicionar discos durante ou após a implementação se precisam.

> [!IMPORTANT]
> **Não altere a contagem de discos de uma nova versão da imagem.** Se tem de reconfigurar os discos de dados na imagem de Olá, defina um SKU de novo. Publicar uma nova versão de imagem com as contagens de outro disco tem o potencial de Olá da nova implementação com base na versão de nova imagem Olá em casos de dimensionamento automático, automáticas implementações das soluções através de modelos ARM e outros cenários de última hora.
>
>

### <a name="11-add-an-offer"></a>1.1 adicionar uma oferta
1. Inicie sessão no toohello [Portal publicação] [ link-pubportal] utilizando a sua conta vendedor.
2. Selecione Olá **máquinas virtuais** separador de Olá Portal de publicação. No campo do pedido de entrada de Olá, introduza o nome da oferta. Olá oferta é normalmente Olá nome de produto de Olá ou serviço que planear toosell no Olá Azure Marketplace.
3. Selecione **Criar**.

### <a name="12-define-a-sku"></a>1.2 definir um SKU
Depois de ter adicionado uma oferta, que precisa toodefine e identificar os SKUs. Pode ter vários ofertas e cada oferta pode ter vários SKUs sob a mesma. Quando é emitida uma oferta toostaging, é enviada juntamente com todos os SKUs.

1. **Adicione um SKU.** Olá SKU requer um identificador, o que é utilizado no URL Olá. Identificador de Olá tem de ser exclusivo no seu perfil de publicação, mas não existe nenhum risco de colisão identificador com outros fabricantes.

   > [!NOTE]
   > oferta de Olá e identificadores SKU são apresentados no URL de oferta Olá no Olá Marketplace.
   >
   >
2. **Adicione uma descrição sumária para o SKU.** Descrições de resumidas são toocustomers visíveis, pelo que deve efetuá-los facilmente legível. Estas informações não precisam de toobe bloqueada até que a fase de "Push tooStaging" Olá. Até lá, estiver livre tooedit-lo.
3. Se estiver a utilizar SKUs baseado no Windows, siga as ligações sugeridos Olá tooacquire Olá aprovados versões do Windows Server.

## <a name="2-create-an-azure-compatible-vhd-linux-based"></a>2. Criar um VHD compatível com o Azure (baseado em Linux)
Esta secção está centrado nas melhores práticas para criar uma imagem VM baseadas em Linux para Olá Azure Marketplace. Para obter instruções passo a passo, consulte toohello a seguinte documentação: [criar e carregar um disco rígido Virtual que contém Olá sistema operativo Linux](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="3-create-an-azure-compatible-vhd-windows-based"></a>3. Criar um VHD compatível com o Azure (baseado no Windows)
Esta secção está centrado nas Olá passos toocreate um SKU baseado no Windows Server para Olá Azure Marketplace.

### <a name="31-ensure-that-you-are-using-hello-correct-base-vhds"></a>Certifique-se 3.1 que está a utilizar Olá corrigir base VHDs
VHD de sistema de operativo Olá para a imagem VM tem de ser baseada em imagem base aprovado do Azure que contém o Windows Server ou SQL Server.

toobegin, crie uma VM a partir de um Olá seguintes imagens, localizadas em Olá [portal do Microsoft Azure][link-azure-portal]:

* Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1] [link-datactr-2008-r2])
* SQL Server 2014 ([Enterprise][link-sql-2014-ent], [padrão][link-sql-2014-std], [Web] [ link-sql-2014-web])
* SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent], [padrão][link-sql-2012-std], [Web] [ link-sql-2012-web])

Estas ligações também podem ser encontradas no Olá Portal de publicação na página SKU Olá.

> [!TIP]
> Se estiver a utilizar o portal do Azure atual de Olá ou PowerShell, imagens do Windows Server publicadas no 8 de Setembro de 2014 e posteriores são aprovadas.
>
>

### <a name="32-create-your-windows-based-vm"></a>3.2 criar a VM com base no Windows
No portal do Microsoft Azure Olá, pode criar a VM com base numa imagem base aprovada em apenas alguns passos simples. Olá segue-se uma descrição geral do processo de Olá:

1. Na página de imagem base Olá, selecione **criar Máquina Virtual** toobe direcionado toohello novo [portal do Microsoft Azure][link-azure-portal].

    ![desenho][img-acom-1]
2. Inicie sessão no portal de toohello com Olá conta Microsoft e a palavra-passe para Olá pretende toouse de subscrição do Azure.
3. Siga Olá pede toocreate uma VM utilizando a imagem base Olá que selecionou. Precisa de tooprovide um nome de anfitrião (nome do computador Olá), o nome de utilizador (registado como administrador) e a palavra-passe para Olá VM.

    ![desenho][img-portal-vm-create]
4. Selecione o tamanho de Olá da Olá VM toodeploy:

    a.    Se planear toodevelop Olá VHD no local, tamanho de Olá não importa. Considere a utilização de um dos Olá VMs mais pequenas.

    b.    Se planear imagem de Olá toodevelop no Azure, considere utilizar um dos Olá recomendado tamanhos de VM para a imagem selecionada Olá.

    c.    Para obter informações sobre preços, consulte toohello **recomendado escalões de preço** Seletor apresentado no portal de Olá. Este relatório irá fornecer Olá três tamanhos recomendados fornecidos pelo fabricante de Olá. (Neste caso, o publicador de Olá é Microsoft.)

    ![desenho][img-portal-vm-size]
5. Defina as propriedades:

    a.    Para uma implementação rápida, pode deixar Olá valores predefinidos das propriedades de Olá em **configuração opcional** e **grupo de recursos**.

    b.    Em **conta de armazenamento**, opcionalmente, pode selecionar a conta de armazenamento de Olá que Olá sistema operativo VHD será armazenado.

    c.    Em **grupo de recursos**, opcionalmente, pode selecionar grupo lógico Olá no qual tooplace Olá VM.
6. Selecione Olá **localização** para a implementação:

    a.    Se planear toodevelop Olá VHD no local, a localização de Olá não importa o porque irá carregar Olá imagem tooAzure mais tarde.

    b.    Se planear imagem de Olá toodevelop no Azure, considere utilizar uma das regiões do Microsoft Azure com base em E.U.A. Olá desde o início de Olá. Isto acelera Olá VHD cópia processo que executa a Microsoft em seu nome ao submeter a imagem de certificação.

    ![desenho][img-portal-vm-location]
7. Clique em **Criar**. Olá VM inicia toodeploy. Dentro de minutos, terá uma implementação com êxito e pode começar a imagem de Olá toocreate para o SKU.

### <a name="33-develop-your-vhd-in-hello-cloud"></a>3.3 desenvolver o VHD na nuvem de Olá
Recomendamos vivamente que desenvolver o VHD na nuvem de Olá utilizando o protocolo RDP (Remote Desktop Protocol). Ligar tooRDP com o nome de utilizador de Olá e a palavra-passe especificada durante o aprovisionamento.

> [!IMPORTANT]
> Se desenvolver o VHD no local (que não seja recomendado), consulte [criar uma imagem de máquina virtual no local](marketplace-publishing-vm-image-creation-on-premise.md). Não é necessário se estiver a desenvolver na nuvem de Olá transferir o VHD.
>
>

**Ligar através de RDP com Olá [portal do Microsoft Azure][link-azure-portal]**

1. Selecione **procurar** > **VMs**.
2. é aberto o painel de máquinas virtuais de Olá. Certifique-se de que Olá VM que pretende que sejam tooconnect com está em execução e, em seguida, selecione-o na lista de Olá de VMs implementadas.
3. Abre um painel que descreve Olá selecionado VM. Na parte superior do Olá, clique em **Connect**.
4. É o nome de utilizador de Olá tooenter pedido e a palavra-passe que especificou durante o aprovisionamento.

**Ligar através de RDP com o PowerShell**

toodownload um ficheiro de ambiente de trabalho remoto tooa computador local, utilizar Olá [cmdlet Get-AzureRemoteDesktopFile][link-technet-2]. Ordenar toouse este cmdlet, terá de nome de Olá tooknow do serviço de Olá e nome de Olá VM. Se tiver criado Olá VM de Olá [portal do Microsoft Azure][link-azure-portal], pode encontrar estas informações em propriedades VM:

1. No portal do Microsoft Azure Olá, selecione **procurar** > **VMs**.
2. é aberto o painel de máquinas virtuais de Olá. Selecione Olá VM que tenha implementado.
3. Abre um painel que descreve Olá selecionado VM.
4. Clique em **Propriedades**.
5. primeira parte de Olá Olá do nome de domínio é o nome de serviço de Olá. nome de anfitrião Olá é o nome da VM Olá.

    ![desenho][img-portal-vm-rdp]
6. ficheiro do Olá cmdlet toodownload Olá RDP para ambiente de trabalho do administrador do Olá criado VM toohello local é a seguinte.

        Get‐AzureRemoteDesktopFile ‐ServiceName “baseimagevm‐6820cq00” ‐Name “BaseImageVM” –LocalPath “C:\Users\Administrator\Desktop\BaseImageVM.rdp”

Podem encontrar mais informações sobre RDP no MSDN artigo Olá [ligar tooan VM do Azure com RDP ou SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx).

**Configurar uma VM e criar o SKU**

Depois de sistema de operativo Olá que VHD é transferido, utilize o Hyper-v e configurar um toobegin VM criar o SKU. Os passos detalhados podem ser encontrados em Olá seguir TechNet ligação: [instalar o Hyper-v e configurar uma VM](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="34-choose-hello-correct-vhd-size"></a>3.4 Escolha o tamanho VHD correto Olá
Olá Windows VHD de sistema operativo da imagem do VM deve ser criado como um VHD de formato fixo de 128 GB.  

Se o tamanho físico Olá for inferior a 128 GB, Olá VHD deve ser disperso. Olá base do SQL Server imagens do Windows e fornecidas já cumpra estes requisitos, por isso, não altere o tamanho de formato ou Olá de Olá de Olá obtido do VHD.  

Os discos de dados podem ser igual a 1 TB. Ao decidir no tamanho do disco Olá, lembre-se de que os clientes não podem redimensionar os VHDs dentro de uma imagem momento Olá da implementação. VHDs de disco de dados devem ser criados como um VHD de formato fixo. Também deve ser dispersos. Os discos de dados podem estar vazios ou conter dados.

### <a name="35-install-hello-latest-windows-patches"></a>3.5 instalar patches de Windows mais recentes Olá
Olá base imagens contêm o correções mais recentes Olá segurança tootheir publicados data. Antes de publicar o sistema de operativo Olá VHD que criou, certifique-se de que o Windows Update foi executada e de que todos os Olá crítico mais recente e atualizações de segurança importante tem sido instaladas.

### <a name="36-perform-additional-configuration-and-schedule-tasks-as-necessary"></a>3.6 efetuar tarefas adicionais de configuração e a agenda conforme necessário
Se não for necessária configuração adicional, considere a utilização de uma tarefa agendada que executa no arranque toomake toohello quaisquer alterações final VM após foi implementada:

* É uma tarefa de Olá de toohave prática melhor eliminar-se automaticamente após a execução com êxito.
* Nenhuma configuração deverá confiar em unidades diferentes unidades C ou D, porque são apenas duas unidades de Olá sempre garantidos tooexist. Unidade C é o disco do sistema operativo Olá, não sendo unidade D disco local temporário de Olá.

### <a name="37-generalize-hello-image"></a>3.7 generalize a imagem de Olá
Todas as imagens no Olá Azure Marketplace tem de ser reutilizáveis de forma genérica. Por outras palavras, deve ser generalizado VHD de sistema de operativo Olá:

* Para o Windows, imagem de Olá deve ser "processado pelo Sysprep" e devem ser efetuadas não configurações que não suportam Olá **sysprep** comando.
* Pode executar Olá seguintes comandos de Olá diretório % windir%\System32\Sysprep.

        sysprep.exe /generalize /oobe /shutdown

  Orientações sobre como o sistema de operativo toosysprep Olá é fornecido no passo de Olá seguinte artigo do MSDN: [criar e carregar um VHD do Windows Server tooAzure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="4-deploy-a-vm-from-your-vhds"></a>4. Implementar uma VM a partir do seu VHDs
Depois de carregou o VHD (VHD de sistema de operativo Olá generalizado e zero ou mais dados em disco VHDs) tooan conta do storage do Azure, pode registá-los como uma imagem VM de utilizador. Em seguida, pode testar essa imagem. Tenha em atenção que porque o sistema operativo VHD seja generalizado, não é possível diretamente implemente Olá VM fornecendo Olá URL de VHD.

toolearn mais informações sobre imagens VM, Olá revisão seguintes mensagens de blogue:

* [Imagem de VM](https://azure.microsoft.com/blog/vm-image-blog-post/)
* [VM imagem do PowerShell como](https://azure.microsoft.com/blog/vm-image-powershell-how-to-blog-post/)
* [Sobre as imagens VM no Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)

### <a name="set-up-hello-necessary-tools-powershell-and-azure-cli"></a>Configurar ferramentas necessário Olá, PowerShell e da CLI do Azure
* [Como toosetup PowerShell](/powershell/azure/overview)
* [Como toosetup CLI do Azure](../cli-install-nodejs.md)

### <a name="41-create-a-user-vm-image"></a>4.1 criar uma imagem VM de utilizador
#### <a name="capture-vm"></a>Captura de VM
Leia as ligações de Olá indicadas abaixo para obter orientações sobre a captura Olá VM ao utilizar a CLI do PowerShell/API/Azure.

* [API](https://msdn.microsoft.com/library/mt163560.aspx)
* [PowerShell](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [CLI do Azure](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="generalize-image"></a>Generalize a imagem
Leia as ligações de Olá indicadas abaixo para obter orientações sobre a captura Olá VM ao utilizar a CLI do PowerShell/API/Azure.

* [API](https://msdn.microsoft.com/library/mt269439.aspx)
* [PowerShell](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [CLI do Azure](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="42-deploy-a-vm-from-a-user-vm-image"></a>4.2 implementar uma VM a partir de uma imagem VM de utilizador
toodeploy uma VM a partir de uma imagem de VM de utilizador, pode utilizar Olá atual [portal do Azure](https://manage.windowsazure.com) ou PowerShell.

**Implementar uma VM a partir do portal do Azure atual Olá**

1. Aceda demasiado**novo** > **computação** > **Máquina Virtual** > **da galeria**.

    ![desenho][img-manage-vm-new]
2. Aceda demasiado**minhas imagens**, e, em seguida, selecione Olá imagem VM a partir do qual toodeploy uma VM:

   1. Imagem de toowhich pay especial atenção selecionar, porque Olá **minhas imagens** vista apresenta uma lista de imagens do sistema operativo e imagens VM.
   2. Observar o número de Olá de discos pode ajudar a determinar o tipo de imagem que estiver a implementar, porque a maioria de Olá das imagens da VM tem mais de um disco. No entanto, é possível toohave uma imagem de VM com apenas um único disco de sistema operativo, que, em seguida, teria **número de discos** definir too1.

      ![desenho][img-manage-vm-select]
3. Siga o Assistente de criação de VM Olá e especifique o nome da VM Olá, tamanho VM, localização, nome de utilizador e palavra-passe.

**Implementar uma VM a partir do PowerShell**

toodeploy que uma VM grande de Olá generalizado imagem de VM que acabou de criar, pode utilizar Olá os seguintes cmdlets.

    $img = Get-AzureVMImage -ImageName "myVMImage"
    $user = "user123"
    $pass = "adminPassword123"
    $myVM = New-AzureVMConfig -Name "VMImageVM" -InstanceSize "Large" -ImageName $img.ImageName | Add-AzureProvisioningConfig -Windows -AdminUsername $user -Password $pass
    New-AzureVM -ServiceName "VMImageCloudService" -VMs $myVM -Location "West US" -WaitForBoot

> [!IMPORTANT]
> Consulte [Resolução de problemas comuns quais os problemas encontrados durante a criação do VHD] para obter assistência adicional.
>
>

## <a name="5-obtain-certification-for-your-vm-image"></a>5. Obter a certificação para a imagem VM
passo seguinte Olá preparar a imagem VM para Olá Azure Marketplace é toohave que este certificado.

Este processo inclui a executar uma ferramenta de certificação especial, carregar toohello de resultados de verificação Olá contentor do Azure onde residem os VHDs, adicionar uma oferta, definir o SKU e submeter a VM de imagem de certificação.

### <a name="51-download-and-run-hello-certification-test-tool-for-azure-certified"></a>5.1 Transferir e executar Olá ferramenta de teste de certificação para o certificado do Azure
ferramenta de certificação Olá é executado numa VM em execução, aprovisionada a partir da imagem de VM de utilizador, tooensure Olá imagem de VM é compatível com o Microsoft Azure. Irá verificar que tiverem sido cumpridos orientações Olá e requisitos sobre a preparação do VHD. Olá o resultado da ferramenta de Olá é um relatório de compatibilidade, que deve ser carregado no Olá Portal de publicação ao requerente de certificação.

ferramenta de certificação de Olá pode ser utilizada com o Windows e VMs com Linux. Liga-se as VMs baseadas em tooWindows através do PowerShell e liga tooLinux VMs através de SSH.Net:

1. Em primeiro lugar, transfira a ferramenta de certificação de Olá no Olá [site de transferências da Microsoft][link-msft-download].
2. Abrir a ferramenta de certificação Olá e, em seguida, clique em Olá **Iniciar novo teste** botão.
3. De Olá **testar informações** ecrã, introduza um nome para a execução do teste Olá.
4. Indique se a VM reporta ao Linux ou ao Windows. Dependendo do que escolher, selecione opções subsequentes Olá.

### <a name="connect-hello-certification-tool-tooa-linux-vm-image"></a>**Ligar Olá certificação ferramenta tooa imagem de VM com Linux**
1. Modo de autenticação SSH Olá selecione: palavra-passe ou chave de ficheiro.
2. Se utilizar autenticação baseada em palavra-passe, introduza o nome de sistema de nomes de domínio (DNS) Olá, nome de utilizador e palavra-passe.
3. Se utilizar a autenticação de ficheiro de chave, introduza o nome DNS de Olá, nome de utilizador e a localização da chave privada.

   ![Autenticação de palavra-passe da imagem de VM do Linux][img-cert-vm-pswd-lnx]

   ![Autenticação de chave de ficheiro de imagem de VM do Linux][img-cert-vm-key-lnx]

### <a name="connect-hello-certification-tool-tooa-windows-based-vm-image"></a>**Ligar a imagem de VM baseadas em Windows hello certificação ferramenta tooa**
1. Introduza o nome DNS de VM de Olá totalmente qualificado (por exemplo, MyVMName.Cloudapp.net).
2. Introduza o nome de utilizador Olá e a palavra-passe.

   ![Autenticação de palavra-passe da imagem de VM do Windows][img-cert-vm-pswd-win]

Depois de selecionar opções corretas Olá para a imagem VM de baseados em Windows ou Linux, selecione **Testar ligação** tooensure que SSH.Net ou o PowerShell tem uma ligação válida para fins de teste. Depois de é estabelecida uma ligação, selecione **seguinte** teste de Olá toostart.

Quando Olá teste estiver concluído, irá receber resultados de Olá (passagem/falhar/aviso) para cada elemento de teste.

![Casos de teste para a imagem de VM do Linux][img-cert-vm-test-lnx]

![Casos de teste para a imagem de VM do Windows][img-cert-vm-test-win]

Se algum dos testes de Olá falhar, a imagem não irá ser certificada. Se isto ocorrer, reveja os requisitos de Olá e efetue as alterações necessárias.

Depois de Olá automatizada teste, é-lhe perguntado tooprovide de entrada adicionais na sua imagem VM através de um ecrã questionário.  Conclua perguntas Olá e, em seguida, selecione **seguinte**.

![Questionário da ferramenta de certificação][img-cert-vm-questionnaire]

![Questionário da ferramenta de certificação][img-cert-vm-questionnaire-2]

Depois de concluir questionário Olá, pode fornecer informações adicionais, tais como informações de acesso SSH para Olá imagem de VM com Linux e uma explicação para qualquer avaliações de falha. Pode transferir os resultados do teste Olá e ficheiros de registo para casos de teste de Olá executada no questionário de toohello adição tooyour respostas. Guardar resultados de Olá no Olá mesmo contentor que os VHDs.

![Guardar resultados do teste de certificação][img-cert-vm-results]

### <a name="52-get-hello-shared-access-signature-uri-for-your-vm-images"></a>5.2 obter assinatura de acesso partilhado Olá URI para as imagens VM
Durante o processo de publicação de Olá, especifique os identificadores de recurso uniforme Olá (URI) que conduzem tooeach de Olá VHDs que criou para o SKU. Microsoft necessita de acesso toothese VHDs durante o processo de certificação Olá. Por conseguinte, terá de toocreate uma URI de assinatura de acesso partilhado para cada VHD. Este é Olá URI que deve ser introduzido no **imagens** separador Olá Portal de publicação.

assinatura de acesso partilhado Olá URI criado deve cumprir os requisitos de toohello:

* Quando a gerar a assinatura de acesso partilhado URIs para os seus VHDs, permissões de leitura e de lista são suficientes. Não forneça acesso de Escrita ou de Eliminação.
* duração de Olá para acesso deve ser um mínimo de três (3) semanas a partir do quando é criada a assinatura de acesso partilhado Olá URI.
* toosafeguard para a hora UTC, dia Olá selecione antes Olá data atual. Por exemplo, se Olá data atual for 6 de Outubro de 2014, selecione 5/10/2014.

URL de SAS que podem ser gerados por várias formas tooshare o VHD para o Azure Marketplace.
Seguintes são Olá 3 ferramentas recomendadas:

1.  Explorador do Storage do Azure
2.  Explorador de armazenamento da Microsoft
3.  CLI do Azure

**Explorador de armazenamento do Azure (recomendado para utilizadores do Windows)**

Seguem-se passos de Olá para gerar o SAS URL utilizando o Explorador de armazenamento do Azure

1. Transferir [pré-visualização 6 do Explorador de armazenamento do Azure 3](https://azurestorageexplorer.codeplex.com/) de CodePlex. Aceda demasiado[pré-visualização de 6 do Explorador de armazenamento de Azure](https://azurestorageexplorer.codeplex.com/) e clique em **"Transferir"**.

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_01.png)

2. Transferir [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) e instalar após unzipping-lo.

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_02.png)

3. Depois de ser instalado, abra a aplicação Olá.
4. Clique em **adicionar conta**.

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_03.png)

5. Especifique o nome de conta do storage Olá, a chave de conta de armazenamento e o domínio de pontos finais de armazenamento. Este é conta do storage Olá na sua subscrição do Azure onde tiver mantido o VHD no portal do Azure.

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_04.png)

6. Depois do Explorador de armazenamento do Azure está ligado tooyour conta de armazenamento específico, será iniciada Mostrar todos os Olá contém na conta do storage Olá. Selecione o contentor de olá onde copiou o ficheiro de VHD de disco de sistema operativo de Olá (também discos de dados se estas forem aplicáveis para o seu cenário).

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_05.png)

7. Depois de selecionar o contentor de blob Olá, o Explorador de armazenamento do Azure inicia que mostra os ficheiros de Olá dentro do contentor de Olá. Selecione o ficheiro de imagem de Olá (. vhd) que tem toobe submetido.

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_06.png)

8.  Depois de selecionar o ficheiro. vhd Olá no contentor de Olá, clique em Olá **segurança** separador.

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_07.png)

9.  No Olá **segurança de contentor do Blob** caixa de diálogo, deixe as predefinições de Olá no Olá **nível de acesso** separador e, em seguida, clique em **assinaturas de acesso partilhado** separador.

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_08.png)

10. Siga os passos de Olá abaixo toogenerate uma assinatura de acesso partilhado URI para a imagem. vhd Olá:

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_09.png)

    a. **Permissão de acesso do:** toosafeguard para a hora UTC, dia Olá selecione antes Olá data atual. Por exemplo, se Olá data atual for 6 de Outubro de 2014, selecione 5/10/2014.

    b. **Permissão de acesso à entidade:** Selecione uma data que seja, pelo menos, 3 semanas após Olá **permissão de acesso do** data.

    c. **As ações permitidas:** Olá selecione **lista** e **leitura** permissões.

    d. Se tiver selecionado corretamente o ficheiro. vhd, em seguida, o ficheiro é apresentado no **tooaccess do nome do Blob** com extensão VHD.

    e. Clique em **gerar a assinatura**.

    f. No **gerado partilhado acesso assinatura URI neste contentor**, verifique a existência de Olá seguir conforme realçado acima:

       - Certifique-se de que a imagem de nome de ficheiro e **". vhd"** em Olá URI.
       - No final de Olá da assinatura de Olá, certifique-se de que **"= rl"** aparece. Isto demonstra que o acesso de leitura e lista foi fornecido com êxito.
       - No meio da assinatura de Olá, certifique-se de que **"sr = c"** aparece. Isto demonstra que tem acesso ao nível do contentor

11. tooensure Olá gerado partilhado funciona URI de assinatura de acesso, clique em **teste no Browser**. Este deve iniciar o processo de transferência Olá.

12. Copie a assinatura de acesso partilhado Olá URI. Este é Olá URI toopaste para Olá Portal de publicação.

13. Repita os passos 6-10 para cada VHD no Olá SKU.

**Explorador de armazenamento do Microsoft Azure (Windows/MAC/Linux)**

Seguem-se passos de Olá para gerar o SAS URL utilizando o Explorador de armazenamento do Microsoft Azure

1.  Transferir o formulário do Explorador de armazenamento do Microsoft Azure [http://storageexplorer.com/](http://storageexplorer.com/) Web site. Aceda demasiado[Explorador de armazenamento do Microsoft Azure](http://storageexplorer.com/releasenotes.html) e clique em **"Transferir para Windows"**.

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_10.png)

2.  Depois de ser instalado, abra a aplicação Olá.

3.  Clique em **adicionar conta**.

4.  Configurar a subscrição do Explorador de armazenamento do Microsoft Azure tooyour pelo início de sessão na conta tooyour

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_11.png)

5.  Aceda toostorage conta e selecione Olá contentor

6.  Selecione **"Obter assinatura de acesso de partilha.."** ao utilizar clique direito de Olá **contentor**

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_12.png)

7.  Hora de início de atualização, a hora de expiração e as permissões de acordo com o seguinte

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_13.png)

    a.  **Hora de início:** toosafeguard para a hora UTC, dia Olá selecione antes Olá data atual. Por exemplo, se Olá data atual for 6 de Outubro de 2014, selecione 5/10/2014.

    b.  **Hora de expiração:** Selecione uma data que seja, pelo menos, 3 semanas após Olá **hora de início** data.

    c.  **Permissões:** Olá selecione **lista** e **leitura** permissões

8.  Copie a assinatura de acesso partilhado do contentor URI

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_14.png)

    É gerado URL SAS para o contentor de nível e agora é necessário o nome do VHD tooadd no mesmo.

    Formato do URL de SAS ao nível do contentor:`https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    Insira o nome do VHD após o nome do contentor Olá no SAS URL tal como indicado abaixo`https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    Exemplo:

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_15.png)

    TestRGVM201631920152.vhd é Olá nome do VHD, será o URL de SAS do VHD`https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    - Certifique-se de que a imagem de nome de ficheiro e **". vhd"** em Olá URI.
    - No meio da assinatura de Olá, certifique-se de que **"SP2 = rl"** aparece. Isto demonstra que o acesso de leitura e lista foi fornecido com êxito.
    - No meio da assinatura de Olá, certifique-se de que **"sr = c"** aparece. Isto demonstra que tem acesso ao nível do contentor

9.  tooensure Olá funciona URI de assinatura de acesso partilhado gerado, testá-la no browser. Este deve iniciar o processo de transferência Olá

10. Copie a assinatura de acesso partilhado Olá URI. Este é Olá URI toopaste para Olá Portal de publicação.

11. Repita estes passos para cada VHD no Olá SKU.

**CLI do Azure (recomendado para a integração contínua & de não Windows)**

Seguem-se passos de Olá para gerar o URL de SAS, utilizando a CLI do Azure

1.  Transferir o Microsoft Azure CLI de [aqui](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/). Também pode encontrar ligações diferentes para  **[Windows](http://aka.ms/webpi-azure-cli)**  e  **[MAC OS](http://aka.ms/mac-azure-cli)**.

2.  Uma vez é transferido, instale o

3.  Criar um ficheiro de PowerShell com o seguinte código e guardá-lo no local

          $conn="DefaultEndpointsProtocol=https;AccountName=<StorageAccountName>;AccountKey=<Storage Account Key>"
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl <Permission End Date> -c $conn --start <Permission Start Date>  

    Atualizar seguinte Olá parâmetros acima

    a. **`<StorageAccountName>`**: Dê o nome da sua conta de armazenamento

    b. **`<Storage Account Key>`**: Dê a sua chave de conta do storage

    c. **`<Permission Start Date>`**: toosafeguard para a hora UTC, dia Olá selecione antes Olá data atual. Por exemplo, se hello data atual for 26 de Outubro de 2016, em seguida, o valor deve ser 25/10/2016

    d. **`<Permission End Date>`**: Selecione uma data que seja, pelo menos, 3 semanas após Olá **data de início**. Em seguida, o valor deve ser **11/02/2016**.

    Segue-se o código de exemplo de Olá depois de atualizar os parâmetros corretos

          $conn="DefaultEndpointsProtocol=https;AccountName=st20151;AccountKey=TIQE5QWMKHpT5q2VnF1bb+NUV7NVMY2xmzVx1rdgIVsw7h0pcI5nMM6+DVFO65i4bQevx21dmrflA91r0Vh2Yw=="
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl 11/02/2016 -c $conn --start 10/25/2016  

4.  Abra o editor de Powershell com o modo de "Executar como administrador" e abra o ficheiro no passo 3 de #.

5.  Script de execução Olá e irão fornecer que Olá SAS URL para o acesso ao nível do contentor

    Seguinte será resultado Olá Olá SAS assinatura e copie Olá realçado parte um bloco de notas

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_16.png)

6.  Agora, irá obter SAS URL ao nível do contentor e tem o nome do VHD tooadd no mesmo.

    URL do contentor de nível SAS #

    `https://st20151.blob.core.windows.net/vhds?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

7.  Insira o nome do VHD após o nome do contentor Olá no URL de SAS conforme mostrado abaixo`https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    Exemplo:

    TestRGVM201631920152.vhd é Olá nome do VHD, será o URL de SAS do VHD

    `https://st20151.blob.core.windows.net/vhds/ TestRGVM201631920152.vhd?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    - Certifique-se que o nome de ficheiro de imagem e ". vhd" Olá URI.
    -   No meio da assinatura de Olá, certifique-se de que "SP2 = rl" aparece. Isto demonstra que o acesso de leitura e lista foi fornecido com êxito.
    -   No meio da assinatura de Olá, certifique-se de que "sr = c" é apresentada. Isto demonstra que tem acesso ao nível do contentor

8.  tooensure Olá funciona URI de assinatura de acesso partilhado gerado, testá-la no browser. Este deve iniciar o processo de transferência Olá

9.  Copie a assinatura de acesso partilhado Olá URI. Este é Olá URI toopaste para Olá Portal de publicação.

10. Repita estes passos para cada VHD no Olá SKU.


### <a name="53-provide-information-about-hello-vm-image-and-request-certification-in-hello-publishing-portal"></a>5.3 fornecem informações sobre a imagem de VM Olá e solicitar certificação no Olá Portal de publicação
Depois de ter criado a sua oferta e SKU, deverá introduzir os detalhes da imagem Olá associados com essa SKU:

1. Aceda toohello [Portal publicação][link-pubportal]e, em seguida, inicie sessão com a sua conta vendedor.
2. Selecione Olá **imagens da VM** separador.
3. Identificador de Olá listado em Olá parte superior da página Olá é, na verdade, identificador de oferta de Olá e identificador SKU não Olá.
4. Preencha as propriedades de Olá em Olá **SKUs** secção.
5. Em **família de sistemas operativos**, clique em tipo de sistema operativo Olá associado VHD de sistema de operativo Olá.
6. No Olá **sistema operativo** caixa, descrevem o sistema de operativo Olá. Considere um formato como família do sistema operativo, tipo, versão e atualizações. Um exemplo é "Windows Server Datacenter 2014 R2".
7. Selecione a cópia de segurança toosix recomendado tamanhos de máquina virtual. Estes são recomendações obtém cliente toohello apresentados no painel de escalão de preço Olá no Olá Portal do Azure quando decidir toopurchase e implementar a imagem. **Estes são apenas recomendações. cliente de Olá é tooselect capaz de qualquer tamanho da VM que permite a discos de Olá especificado na imagem.**
8. Introduza a versão de Olá. campo de versão Olá encapsula um produto de Olá tooidentify versão semântica e respetivas atualizações:
   * Versões devem ter o formato de Olá X.Y.Z, onde X, Y e Z são números inteiros.
   * Imagens de SKUs diferentes podem ter diferentes versões principais e secundárias.
   * Versões dentro de um SKU só devem ser as alterações incrementais, aumentam a versão de patch Olá (Z do X.Y.Z).
9. No Olá **URL de VHD de SO** box, introduza a assinatura de acesso partilhado Olá URI criado para VHD de sistema de operativo Olá.
10. Se existirem discos de dados associados este SKU, selecione Olá unidade lógica número (LUN) toowhich que gostaria este toobe de disco de dados montada após a implementação.
11. No Olá **LUN X VHD URL** box, introduza a assinatura de acesso partilhado Olá URI criado para dados de primeiro Olá VHD.

    ![desenho](media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-3.png)


## <a name="common-sas-url-issues--fixes"></a>URL de SAS comum emite & corrige

|Problema|Mensagem de falha|Corrigir|Ligação de documentação|
|---|---|---|---|
|Falha ao copiar imagens - "?" não foi encontrado no SAS url|Falha: Copiar as imagens. Toodownload não é possível utilizar o blob fornecido Uri de SAS.|Atualização Olá SAS Url utilizando recomendado ferramentas|[https://Azure.microsoft.com/en-us/Documentation/articles/Storage-DotNet-Shared-Access-Signature-Part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Falha ao copiar imagens - "st" e "zar" parâmetros não SAS url|Falha: Copiar as imagens. Toodownload não é possível utilizar o blob fornecido Uri de SAS.|Atualizar Olá SAS Url com datas de início e fim no mesmo|[https://Azure.microsoft.com/en-us/Documentation/articles/Storage-DotNet-Shared-Access-Signature-Part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Falha ao copiar imagens - "SP2 = rl" não está num SAS url|Falha: Copiar as imagens. Toodownload não é possível utilizar o blob fornecido Uri de SAS|Atualizar Olá SAS Url com definido como "Leitura" & "lista de permissões|[https://Azure.microsoft.com/en-us/Documentation/articles/Storage-DotNet-Shared-Access-Signature-Part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Falha ao copiar imagens - SAS url tem espaços em branco no nome do vhd|Falha: Copiar as imagens. Toodownload não é possível utilizar o blob fornecido Uri de SAS.|Atualizar Olá SAS Url, sem espaços em branco|[https://Azure.microsoft.com/en-us/Documentation/articles/Storage-DotNet-Shared-Access-Signature-Part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Falha ao copiar imagens – erro de autorização de Url SAS|Falha: Copiar as imagens. Blob toodownload não é possível devido a erro de tooauthorization|Regenerar Olá SAS Url|[https://Azure.microsoft.com/en-us/Documentation/articles/Storage-DotNet-Shared-Access-Signature-Part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|


## <a name="next-step"></a>Passo seguinte
Depois de terminar com detalhes SKU Olá, pode mover toohello reencaminhar [Guia do Azure Marketplace marketing conteúdo][link-pushstaging]. Esse passo do processo de publicação de Olá, deve fornecer Olá marketing conteúdo, preço e antes de necessárias outras informações demasiado**passo 3: testar a sua VM oferecem no modo de transição**, onde testar vários cenários de caso de utilização antes de implementar Olá oferta toohello Azure Marketplace para visibilidade pública e compra.  

## <a name="see-also"></a>Consultar também
* [Introdução: como toopublish toohello uma oferta Azure Marketplace](marketplace-publishing-getting-started.md)

[img-acom-1]:media/marketplace-publishing-vm-image-creation/vm-image-acom-datacenter.png
[img-portal-vm-size]:media/marketplace-publishing-vm-image-creation/vm-image-portal-size.png
[img-portal-vm-create]:media/marketplace-publishing-vm-image-creation/vm-image-portal-create-vm.png
[img-portal-vm-location]:media/marketplace-publishing-vm-image-creation/vm-image-portal-location.png
[img-portal-vm-rdp]:media/marketplace-publishing-vm-image-creation/vm-image-portal-rdp.png
[img-azstg-add]:media/marketplace-publishing-vm-image-creation/vm-image-storage-add.png
[img-manage-vm-new]:media/marketplace-publishing-vm-image-creation/vm-image-manage-new.png
[img-manage-vm-select]:media/marketplace-publishing-vm-image-creation/vm-image-manage-select.png
[img-cert-vm-key-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-keyfile-linux.png
[img-cert-vm-pswd-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-linux.png
[img-cert-vm-pswd-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-win.png
[img-cert-vm-test-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-linux.png
[img-cert-vm-test-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-win.png
[img-cert-vm-results]:media/marketplace-publishing-vm-image-creation/vm-image-certification-results.png
[img-cert-vm-questionnaire]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire.png
[img-cert-vm-questionnaire-2]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire-2.png
[img-pubportal-vm-skus]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus.png
[img-pubportal-vm-skus-2]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-2.png

[link-pushstaging]:marketplace-publishing-push-to-staging.md
[link-github-waagent]:https://github.com/Azure/WALinuxAgent
[link-azure-codeplex]:https://azurestorageexplorer.codeplex.com/
[link-azure-2]:../storage/blobs/storage-dotnet-shared-access-signature-part-2.md
[link-azure-1]:../storage/common/storage-dotnet-shared-access-signature-part-1.md
[link-msft-download]:http://www.microsoft.com/download/details.aspx?id=44299
[link-technet-3]:https://technet.microsoft.com/library/hh846766.aspx
[link-technet-2]:https://msdn.microsoft.com/library/dn495261.aspx
[link-azure-portal]:https://portal.azure.com
[link-pubportal]:https://publish.windowsazure.com
[link-sql-2014-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014enterprisewindowsserver2012r2/
[link-sql-2014-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014standardwindowsserver2012r2/
[link-sql-2014-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014webwindowsserver2012r2/
[link-sql-2012-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2enterprisewindowsserver2012/
[link-sql-2012-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2standardwindowsserver2012/
[link-sql-2012-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2webwindowsserver2012/
[link-datactr-2012-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012r2datacenter/
[link-datactr-2012]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012datacenter/
[link-datactr-2008-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2008r2sp1/
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-technet-1]:https://technet.microsoft.com/library/hh848454.aspx
[link-azure-vm-2]:./virtual-machines-linux-agent-user-guide/
[link-openssl]:https://www.openssl.org/
[link-intsvc]:http://www.microsoft.com/download/details.aspx?id=41554
[link-python]:https://www.python.org/
