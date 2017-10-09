---
title: "aaaRed infraestrutura de atualização de Hat (RHUI) | Microsoft Docs"
description: "Saiba mais sobre o Red Hat atualização infraestrutura (RHUI) para instâncias do Red Hat Enterprise Linux a pedido no Microsoft Azure"
services: virtual-machines-linux
documentationcenter: 
author: BorisB2015
manager: timlt
editor: 
ms.assetid: f495f1b4-ae24-46b9-8d26-c617ce3daf3a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: borisb
ms.openlocfilehash: cc244857104b25e4e61862c518db77e915e137ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a><span data-ttu-id="d4fbd-103">Infraestrutura de atualização do Red Hat (RHUI) para a pedido Red Hat Enterprise Linux VMs no Azure</span><span class="sxs-lookup"><span data-stu-id="d4fbd-103">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>
<span data-ttu-id="d4fbd-104">Máquinas virtuais criadas a partir de Olá a pedido Red Hat Enterprise Linux (RHEL) imagens disponíveis no Azure Marketplace são registados tooaccess Olá Red Hat atualização infraestrutura (RHUI) implementados no Azure.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-104">Virtual machines created from hello on-demand Red Hat Enterprise Linux (RHEL) images available in Azure Marketplace are registered tooaccess hello Red Hat Update Infrastructure (RHUI) deployed in Azure.</span></span>  <span data-ttu-id="d4fbd-105">Olá a pedido RHEL instâncias de ter repositório do acesso tooa regional yum e tooreceive capaz das atualizações incrementais.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-105">hello on-demand RHEL instances have access tooa regional yum repository and able tooreceive incremental updates.</span></span>

<span data-ttu-id="d4fbd-106">lista de repositório do Olá yum, que é gerida pelo RHUI, é configurada na sua instância RHEL durante o aprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-106">hello yum repository list, which is managed by RHUI, is configured in your RHEL instance during provisioning.</span></span> <span data-ttu-id="d4fbd-107">Não precisa de toodo qualquer configuração adicional - executar `yum update` após a sua instância RHEL atualizações mais recentes do Olá tooget pronto.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-107">You don't need toodo any additional configuration - run `yum update` after your RHEL instance is ready tooget hello latest updates.</span></span>

> [!NOTE]
> <span data-ttu-id="d4fbd-108">Setembro de 2016 foi implementada uma RHUI atualizado do Azure e em Janeiro de 2017 iniciamos encerramento faseado do Olá RHUI mais antiga do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-108">In September 2016 we deployed an updated Azure RHUI and in January 2017 we started phased shutdown of hello older Azure RHUI.</span></span> <span data-ttu-id="d4fbd-109">Se tiver utilizado Olá RHEL imagens (ou os respetivos instantâneos) a partir de Setembro de 2016 ou posterior - provavelmente não é necessária nenhuma ação.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-109">If you have been using hello RHEL images (or their snapshots) from September 2016 or later - likely no action is required.</span></span> <span data-ttu-id="d4fbd-110">Se, no entanto, que tem instantâneos/VMs anteriores, a configuração tem toobe atualizado com acesso ininterrupta toohello RHUI do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-110">If, however, you have older snapshots/VMs, their configuration needs toobe updated for uninterrupted access toohello Azure RHUI.</span></span>
> 

## <a name="rhui-azure-infrastructure-update"></a><span data-ttu-id="d4fbd-111">Atualização da infraestrutura do Azure de RHUI</span><span class="sxs-lookup"><span data-stu-id="d4fbd-111">RHUI Azure Infrastructure Update</span></span>
<span data-ttu-id="d4fbd-112">A partir de Setembro de 2016, o Azure tem um novo conjunto de servidores Red Hat atualização infraestrutura (RHUI).</span><span class="sxs-lookup"><span data-stu-id="d4fbd-112">As of September 2016, Azure has a new set of Red Hat Update Infrastructure (RHUI) servers.</span></span> <span data-ttu-id="d4fbd-113">Estes servidores são implementados com [Traffic Manager do Azure](https://azure.microsoft.com/services/traffic-manager/) para que um único ponto final (rhui 1.microsoft.com) pode ser utilizado por qualquer VM, independentemente da região.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-113">These servers are deployed with [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) so that a single endpoint (rhui-1.microsoft.com) can be used by any VM regardless of region.</span></span> <span data-ttu-id="d4fbd-114">Olá novas imagens de RHEL pay as you go (PAYG) Olá (versões com a data de Setembro de 2016 ou posteriores) do Azure Marketplace ponto toohello novos Azure RHUI servidores e não requerem qualquer ação adicional.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-114">hello new RHEL Pay-As-You-Go (PAYG) images in hello Azure Marketplace (versions dated September 2016 or later) point toohello new Azure RHUI servers and do not require any additional action.</span></span>

### <a name="determine-if-action-is-required"></a><span data-ttu-id="d4fbd-115">Determinar se é necessária ação</span><span class="sxs-lookup"><span data-stu-id="d4fbd-115">Determine if action is required</span></span>
<span data-ttu-id="d4fbd-116">Se ocorrerem problemas de ligação tooAzure RHUI da sua VM do Azure RHEL PAYG, siga estes passos</span><span class="sxs-lookup"><span data-stu-id="d4fbd-116">If you are experiencing problems connecting tooAzure RHUI from your Azure RHEL PAYG VM, follow these steps</span></span>
1. <span data-ttu-id="d4fbd-117">Verifique a configuração de VM para o ponto final de RHUI do Azure</span><span class="sxs-lookup"><span data-stu-id="d4fbd-117">Inspect VM configuration for Azure RHUI endpoint</span></span>

    <span data-ttu-id="d4fbd-118">Verifique se o `/etc/yum.repos.d/rh-cloud.repo` ficheiro contém referência demasiado`rhui-[1-3].microsoft.com` no baseurl de `[rhui-microsoft-azure-rhel*]` secção do ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-118">Check if `/etc/yum.repos.d/rh-cloud.repo` file contains reference too`rhui-[1-3].microsoft.com` in baseurl of `[rhui-microsoft-azure-rhel*]` section of hello file.</span></span> <span data-ttu-id="d4fbd-119">Se for - estiver a utilizar Olá novo RHUI do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-119">If it is - you are using hello new Azure RHUI.</span></span>

    <span data-ttu-id="d4fbd-120">Se este apontar tooa localização com Olá seguir o padrão `mirrorlist.*cds[1-4].cloudapp.net` -Olá configuração atualização é necessária.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-120">If it pointing tooa location with hello following pattern `mirrorlist.*cds[1-4].cloudapp.net` - hello configuration update is required.</span></span>

    <span data-ttu-id="d4fbd-121">Se estiver a utilizar configuração de novo Olá e ainda não é possível ligar tooAzure RHUI - ficheiro um incidente de suporte com a Microsoft ou Red Hat.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-121">If you are using hello new configuration and still cannot connect tooAzure RHUI - file a support case with Microsoft or Red Hat.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d4fbd-122">Acesso alojadas tooAzure RHUI é limitado toohello VMs dentro [intervalos de IP de centro de dados do Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="d4fbd-122">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
    > 

2. <span data-ttu-id="d4fbd-123">Se hello antigo Azure RHUI ainda está disponível quando efetuar esta verificação e gostaria de configuração de Olá tooautomatically atualização, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d4fbd-123">If hello old Azure RHUI is still available when you do this check and you would like tooautomatically update hello configuration, execute hello following command:</span></span>

    <span data-ttu-id="d4fbd-124">`sudo yum update RHEL6`ou `sudo yum update RHEL7` consoante Olá família do rhel.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-124">`sudo yum update RHEL6` or `sudo yum update RHEL7` depending on hello RHEL family version.</span></span>

3. <span data-ttu-id="d4fbd-125">Se já não pode ligar toohello antigo RHUI do Azure, siga Olá manual os passos descritos na secção seguinte, Olá.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-125">If you can no longer connect toohello old Azure RHUI, follow hello manual steps described in hello next section.</span></span>

4. <span data-ttu-id="d4fbd-126">Certifique-se a configuração de Olá tooupdate/instantâneo de imagem de origem de Olá afetados VM aprovisionado a partir de.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-126">Make sure tooupdate hello configuration on hello source image/snapshot affected VM was provisioned from.</span></span>

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a><span data-ttu-id="d4fbd-127">Encerramento faseado do Olá RHUI antigo do Azure</span><span class="sxs-lookup"><span data-stu-id="d4fbd-127">Phased shutdown of hello old Azure RHUI</span></span>
<span data-ttu-id="d4fbd-128">Durante o encerramento de Olá de Olá antigo Azure RHUI, iremos restringir acesso tooit da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="d4fbd-128">During hello shutdown of hello old Azure RHUI we restrict access tooit as follows:</span></span>

1. <span data-ttu-id="d4fbd-129">Restringir mais o tooset de acesso (ACL) de endereços IP que já se ligarem tooit.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-129">Further restrict access (ACL) tooset of IP addresses that are already connecting tooit.</span></span> <span data-ttu-id="d4fbd-130">Possíveis de atribuição de efeitos secundários: Se continuar a utilizar Olá RHUI antigo do Azure – as suas VMs novas podem não ser capaz de tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-130">Possible side-effects: if you continue using hello old Azure RHUI - your new VMs may not be able tooconnect tooit.</span></span> <span data-ttu-id="d4fbd-131">VMs de RHEL com IPs dinâmicos que podem passar através de sequência de encerramento/desalocar/início poderá receber novas IP e, por conseguinte, também foi começam a falhar tooconnect toohello RHUI antigo do Azure</span><span class="sxs-lookup"><span data-stu-id="d4fbd-131">RHEL VMs with dynamic IPs that go through shutdown/deallocate/start sequence may receive new IP and hence also could start failing tooconnect toohello old Azure RHUI</span></span>

2. <span data-ttu-id="d4fbd-132">Encerramento de servidores de entrega de conteúdos do espelho.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-132">Shutdown of mirror content delivery servers.</span></span> <span data-ttu-id="d4fbd-133">Possíveis de atribuição de efeitos secundários: como é encerrado CDSes mais poderá ver já `yum update` tempo de manutenção, tempos limite mais até Olá ponto quando já não pode ligar toohello RHUI antigo do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-133">Possible side-effects: as we shut down more CDSes you may see longer `yum update` servicing time, more timeouts up until hello point when you can no longer connect toohello old Azure RHUI.</span></span>

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a><span data-ttu-id="d4fbd-134">Olá IPs para servidores de entrega de conteúdos de RHUI Olá novos são</span><span class="sxs-lookup"><span data-stu-id="d4fbd-134">hello IPs for hello new RHUI content delivery servers are</span></span>
<span data-ttu-id="d4fbd-135">Se estiver a utilizar toofurther de configuração de rede restringir o acesso de RHEL PAYG VMs, certifique-se Olá seguintes IPs é permitida para `yum update` toowork dependendo do ambiente de Olá estiver no.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-135">If you are using network configuration toofurther restrict access from RHEL PAYG VMs, make sure hello following IPs are allowed for `yum update` toowork depending on hello environment you are in.</span></span> 

```
# Azure Global
13.91.47.76
40.85.190.91
52.187.75.218
52.174.163.213

# Azure US Government
13.72.186.193

# Azure Germany
51.5.243.77
51.4.228.145
```

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a><span data-ttu-id="d4fbd-136">Atualização manual procedimento toouse Olá novo Azure RHUI servidores</span><span class="sxs-lookup"><span data-stu-id="d4fbd-136">Manual update procedure toouse hello new Azure RHUI servers</span></span>
<span data-ttu-id="d4fbd-137">Assinatura de chave pública Olá transferências (através de curl)</span><span class="sxs-lookup"><span data-stu-id="d4fbd-137">Download (via curl) hello public key signature</span></span>

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

<span data-ttu-id="d4fbd-138">Certifique-se a chave Olá transferido</span><span class="sxs-lookup"><span data-stu-id="d4fbd-138">Verify hello downloaded key</span></span>

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="d4fbd-139">Verifique a saída de Olá, certifique-se `keyid` e `user ID packet`:</span><span class="sxs-lookup"><span data-stu-id="d4fbd-139">Check hello output, verify `keyid` and `user ID packet`:</span></span>

```bash
Version: GnuPG v1.4.7 (GNU/Linux)
:public key packet:
        version 4, algo 1, created 1446074508, expires 0
        pkey[0]: [2048 bits]
        pkey[1]: [17 bits]
        keyid: EB3E94ADBE1229CF
:user ID packet: "Microsoft (Release signing) <gpgsecurity@microsoft.com>"
:signature packet: algo 1, keyid EB3E94ADBE1229CF
        version 4, created 1446074508, md5len 0, sigclass 0x13
        digest algo 2, begin of digest 1a 9b
        hashed subpkt 2 len 4 (sig created 2015-10-28)
        hashed subpkt 27 len 1 (key flags: 03)
        hashed subpkt 11 len 5 (pref-sym-algos: 9 8 7 3 2)
        hashed subpkt 21 len 3 (pref-hash-algos: 2 8 3)
        hashed subpkt 22 len 2 (pref-zip-algos: 2 1)
        hashed subpkt 30 len 1 (features: 01)
        hashed subpkt 23 len 1 (key server preferences: 80)
        subpkt 16 len 8 (issuer key ID EB3E94ADBE1229CF)
        data: [2047 bits]
```

<span data-ttu-id="d4fbd-140">Instale a chave pública Olá</span><span class="sxs-lookup"><span data-stu-id="d4fbd-140">Install hello public key</span></span>

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="d4fbd-141">Transferir, certifique-se e instalar o cliente RPM</span><span class="sxs-lookup"><span data-stu-id="d4fbd-141">Download, Verify, and Install Client RPM</span></span>

<span data-ttu-id="d4fbd-142">Transferir: Para RHEL 6</span><span class="sxs-lookup"><span data-stu-id="d4fbd-142">Download: For RHEL 6</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

<span data-ttu-id="d4fbd-143">Para RHEL 7</span><span class="sxs-lookup"><span data-stu-id="d4fbd-143">For RHEL 7</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

<span data-ttu-id="d4fbd-144">Certifique-se:</span><span class="sxs-lookup"><span data-stu-id="d4fbd-144">Verify:</span></span>

```bash
rpm -Kv azureclient.rpm
```

<span data-ttu-id="d4fbd-145">Verifique no resultado dessa assinatura Olá pacote é OK</span><span class="sxs-lookup"><span data-stu-id="d4fbd-145">Check in output that signature of hello package is OK</span></span>

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

<span data-ttu-id="d4fbd-146">Instalar Olá RPM</span><span class="sxs-lookup"><span data-stu-id="d4fbd-146">Install hello RPM</span></span>

```bash
sudo rpm -U azureclient.rpm
```

<span data-ttu-id="d4fbd-147">Após a conclusão, verifique se pode aceder Olá de formulário de Azure RHUI VM</span><span class="sxs-lookup"><span data-stu-id="d4fbd-147">Upon completion, verify that you can access Azure RHUI form hello VM</span></span>

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a><span data-ttu-id="d4fbd-148">Tudo-em-um script para Olá anterior a tarefa de automatização</span><span class="sxs-lookup"><span data-stu-id="d4fbd-148">All-in-one script for automating hello preceding task</span></span>
<span data-ttu-id="d4fbd-149">Utilize Olá seguinte script como tarefa de Olá tooautomate necessários de atualização VMs toohello novo Azure RHUI servidores afetados.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-149">Use hello following script as needed tooautomate hello task of updating affected VMs toohello new Azure RHUI servers.</span></span>

```sh
# Download key
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 

# Validate key
if ! gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release | grep -q "keyid: EB3E94ADBE1229CF"; then
    echo "Keyfile azure.asc NOT valid. Exiting."
    exit 1
fi

# Install Key
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release

# Download RPM package
if grep -q "release 7" /etc/redhat-release; then
    ver=7
elif  grep -q "release 6" /etc/redhat-release; then
    ver=6
else
    echo "Version not supported, exiting"
    exit 1
fi

url=https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel$ver/rhui-azure-rhel$ver-2.0-2.noarch.rpm
curl -o azureclient.rpm "$url"

# Verify package
if ! rpm -Kv azureclient.rpm | grep -q "key ID be1229cf: OK"; then
    echo "RPM failed validation ($url)"
    exit 1
fi

# Install package
sudo rpm -U azureclient.rpm
```

## <a name="rhui-overview"></a><span data-ttu-id="d4fbd-150">Descrição geral RHUI</span><span class="sxs-lookup"><span data-stu-id="d4fbd-150">RHUI overview</span></span>
<span data-ttu-id="d4fbd-151">[Infraestrutura de atualização do Red Hat](https://access.redhat.com/products/red-hat-update-infrastructure) oferece um conteúdo do repositório de yum toomanage solução altamente dimensionável para as instâncias de cloud do Red Hat Enterprise Linux que estão alojados pelos fornecedores de nuvem de certificados do Red Hat.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-151">[Red Hat Update Infrastructure](https://access.redhat.com/products/red-hat-update-infrastructure) offers a highly scalable solution toomanage yum repository content for Red Hat Enterprise Linux cloud instances that are hosted by Red Hat-certified cloud providers.</span></span> <span data-ttu-id="d4fbd-152">Com base no projeto de Pulp montante Olá, RHUI permite que os fornecedores de nuvem toolocally espelho alojadas Red Hat repositório conteúdo, crie repositórios personalizados com os seus próprios conteúdos e tornar esses repositórios tooa disponíveis grande grupo dos utilizadores finais através de com balanceamento de carga conteúdo de entrega de sistema.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-152">Based on hello upstream Pulp project, RHUI allows cloud providers toolocally mirror Red Hat-hosted repository content, create custom repositories with their own content, and make those repositories available tooa large group of end users through a load-balanced content delivery system.</span></span>

## <a name="regions-where-rhui-is-available"></a><span data-ttu-id="d4fbd-153">Regiões onde RHUI está disponível</span><span class="sxs-lookup"><span data-stu-id="d4fbd-153">Regions where RHUI is available</span></span>
<span data-ttu-id="d4fbd-154">RHUI está disponível em todas as regiões onde as imagens do RHEL a pedido estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-154">RHUI is available in all regions where RHEL on-demand images are available.</span></span> <span data-ttu-id="d4fbd-155">Inclui atualmente públicas todas as regiões listadas no Olá [dashboard de estado do Azure](https://azure.microsoft.com/status/) página, regiões do Azure US Government e Datacenters do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-155">It currently includes all public regions listed on hello [Azure status dashboard](https://azure.microsoft.com/status/) page, Azure US Government and Azure Germany regions.</span></span> <span data-ttu-id="d4fbd-156">Acesso RHUI para VMs aprovisionado a partir de imagens do RHEL a pedido está incluído no respetivo preços.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-156">RHUI access for VMs provisioned from RHEL on-demand images is included in their price.</span></span> <span data-ttu-id="d4fbd-157">Disponibilidade de nuvem de regionais/national adicionais será atualizada como podemos expanda RHEL a pedido obter disponibilidade em Olá futura.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-157">Additional regional/national cloud availability will be updated as we expand RHEL on-demand availability in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="d4fbd-158">Acesso alojadas tooAzure RHUI é limitado toohello VMs dentro [intervalos de IP de centro de dados do Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="d4fbd-158">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
> 
> 

## <a name="get-updates-from-another-update-repository"></a><span data-ttu-id="d4fbd-159">Obter atualizações a partir do repositório de atualização de outro</span><span class="sxs-lookup"><span data-stu-id="d4fbd-159">Get updates from another update repository</span></span>
<span data-ttu-id="d4fbd-160">Se precisar de atualizações de tooget a partir de um repositório de atualizações diferente (em vez de RHUI alojado no Azure), primeiro é necessário toounregister as instâncias de RHUI.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-160">If you need tooget updates from a different update repository (instead of Azure-hosted RHUI), first you need toounregister your instances from RHUI.</span></span> <span data-ttu-id="d4fbd-161">Em seguida, terá de registar toore-las com a infraestrutura de atualização pretendido Olá (como Red Hat satélite ou CDN de Portal de cliente do Red Hat).</span><span class="sxs-lookup"><span data-stu-id="d4fbd-161">Then you need toore-register them with hello desired update infrastructure (such as Red Hat Satellite or Red Hat Customer Portal CDN).</span></span> <span data-ttu-id="d4fbd-162">É necessário adequado subscrições do Red Hat para estes serviços e o registo para [Red Hat acesso à nuvem, no Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="d4fbd-162">You will need appropriate Red Hat subscriptions for these services and registration for [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span></span>

<span data-ttu-id="d4fbd-163">toounregister RHUI e registe novamente tooyour atualização infraestrutura siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="d4fbd-163">toounregister RHUI and reregister tooyour update infrastructure follow these steps:</span></span>

1. <span data-ttu-id="d4fbd-164">Editar /etc/yum.repos.d/rh-cloud.repo e altere todos os `enabled=1` demasiado`enabled=0`.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-164">Edit /etc/yum.repos.d/rh-cloud.repo and change all `enabled=1` too`enabled=0`.</span></span> <span data-ttu-id="d4fbd-165">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d4fbd-165">For example:</span></span>
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. <span data-ttu-id="d4fbd-166">Editar /etc/yum/pluginconf.d/rhnplugin.conf e alterar `enabled=0` demasiado`enabled=1`.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-166">Edit /etc/yum/pluginconf.d/rhnplugin.conf and change `enabled=0` too`enabled=1`.</span></span>
3. <span data-ttu-id="d4fbd-167">Em seguida, registe a infraestrutura pretendido Olá, tais como o Portal de cliente do Red Hat.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-167">Then register with hello desired infrastructure, such as Red Hat Customer Portal.</span></span> <span data-ttu-id="d4fbd-168">Siga o guia de soluções do Red Hat [como tooregister e subscrever um toohello sistema Portal de cliente do Red Hat](https://access.redhat.com/solutions/253273).</span><span class="sxs-lookup"><span data-stu-id="d4fbd-168">Follow Red Hat solution guide on [how tooregister and subscribe a system toohello Red Hat Customer Portal](https://access.redhat.com/solutions/253273).</span></span>

> [!NOTE]
> <span data-ttu-id="d4fbd-169">Acesso toohello RHUI alojado no Azure está incluído no preço de imagem Olá RHEL pay as you go (PAYG).</span><span class="sxs-lookup"><span data-stu-id="d4fbd-169">Access toohello Azure-hosted RHUI is included in hello RHEL Pay-As-You-Go (PAYG) image price.</span></span> <span data-ttu-id="d4fbd-170">Uma VM RHEL PAYG Olá RHUI alojado no Azure ao anular o registo não converter máquina virtual de Olá numa VM do tipo de Bring-Your-proprietário-licença (BYOL).</span><span class="sxs-lookup"><span data-stu-id="d4fbd-170">Unregistering a PAYG RHEL VM from hello Azure-hosted RHUI does not convert hello virtual machine into Bring-Your-Own-License (BYOL) type VM.</span></span> <span data-ttu-id="d4fbd-171">Se registar Olá mesma VM com outra origem das atualizações pode ser incorrer em custos duplos: primeiro de tempo de taxa de software do Azure RHEL e Olá segunda vez para subscrições do Red Hat.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-171">If you register hello same VM with another source of updates you may be incurring double charges: first time for Azure RHEL software fee, and hello second time for Red Hat subscription(s).</span></span> 
> 
> <span data-ttu-id="d4fbd-172">Se precisar de forma consistente toouse uma infraestrutura de atualização que não seja alojado no Azure RHUI considere criar e implementar as suas próprias imagens (BYOL-type), conforme descrito em [criar e carregar Red Hat com base em máquina virtual para o Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artigo.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-172">If you consistently need toouse an update infrastructure other than Azure-hosted RHUI consider creating and deploying your own (BYOL-type) images as described in [Create and Upload Red Hat-based virtual machine for Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article.</span></span>
> 

## <a name="next-steps"></a><span data-ttu-id="d4fbd-173">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d4fbd-173">Next steps</span></span>
<span data-ttu-id="d4fbd-174">toocreate uma VM do Red Hat Enterprise Linux da imagem do Azure pay as you go de Marketplace e tire partido alojado no Azure RHUI aceda demasiado[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span><span class="sxs-lookup"><span data-stu-id="d4fbd-174">toocreate a Red Hat Enterprise Linux VM from Azure Marketplace Pay-As-You-Go image and leverage Azure-hosted RHUI go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span></span> <span data-ttu-id="d4fbd-175">Será capaz de toouse `yum update` na sua instância RHEL sem qualquer configuração adicional.</span><span class="sxs-lookup"><span data-stu-id="d4fbd-175">You will be able toouse `yum update` in your RHEL instance without any additional setup.</span></span>

