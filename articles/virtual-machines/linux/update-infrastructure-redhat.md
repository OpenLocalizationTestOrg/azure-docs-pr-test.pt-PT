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
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a>Infraestrutura de atualização do Red Hat (RHUI) para a pedido Red Hat Enterprise Linux VMs no Azure
Máquinas virtuais criadas a partir de Olá a pedido Red Hat Enterprise Linux (RHEL) imagens disponíveis no Azure Marketplace são registados tooaccess Olá Red Hat atualização infraestrutura (RHUI) implementados no Azure.  Olá a pedido RHEL instâncias de ter repositório do acesso tooa regional yum e tooreceive capaz das atualizações incrementais.

lista de repositório do Olá yum, que é gerida pelo RHUI, é configurada na sua instância RHEL durante o aprovisionamento. Não precisa de toodo qualquer configuração adicional - executar `yum update` após a sua instância RHEL atualizações mais recentes do Olá tooget pronto.

> [!NOTE]
> Setembro de 2016 foi implementada uma RHUI atualizado do Azure e em Janeiro de 2017 iniciamos encerramento faseado do Olá RHUI mais antiga do Azure. Se tiver utilizado Olá RHEL imagens (ou os respetivos instantâneos) a partir de Setembro de 2016 ou posterior - provavelmente não é necessária nenhuma ação. Se, no entanto, que tem instantâneos/VMs anteriores, a configuração tem toobe atualizado com acesso ininterrupta toohello RHUI do Azure.
> 

## <a name="rhui-azure-infrastructure-update"></a>Atualização da infraestrutura do Azure de RHUI
A partir de Setembro de 2016, o Azure tem um novo conjunto de servidores Red Hat atualização infraestrutura (RHUI). Estes servidores são implementados com [Traffic Manager do Azure](https://azure.microsoft.com/services/traffic-manager/) para que um único ponto final (rhui 1.microsoft.com) pode ser utilizado por qualquer VM, independentemente da região. Olá novas imagens de RHEL pay as you go (PAYG) Olá (versões com a data de Setembro de 2016 ou posteriores) do Azure Marketplace ponto toohello novos Azure RHUI servidores e não requerem qualquer ação adicional.

### <a name="determine-if-action-is-required"></a>Determinar se é necessária ação
Se ocorrerem problemas de ligação tooAzure RHUI da sua VM do Azure RHEL PAYG, siga estes passos
1. Verifique a configuração de VM para o ponto final de RHUI do Azure

    Verifique se o `/etc/yum.repos.d/rh-cloud.repo` ficheiro contém referência demasiado`rhui-[1-3].microsoft.com` no baseurl de `[rhui-microsoft-azure-rhel*]` secção do ficheiro de Olá. Se for - estiver a utilizar Olá novo RHUI do Azure.

    Se este apontar tooa localização com Olá seguir o padrão `mirrorlist.*cds[1-4].cloudapp.net` -Olá configuração atualização é necessária.

    Se estiver a utilizar configuração de novo Olá e ainda não é possível ligar tooAzure RHUI - ficheiro um incidente de suporte com a Microsoft ou Red Hat.

    > [!NOTE]
    > Acesso alojadas tooAzure RHUI é limitado toohello VMs dentro [intervalos de IP de centro de dados do Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).
    > 

2. Se hello antigo Azure RHUI ainda está disponível quando efetuar esta verificação e gostaria de configuração de Olá tooautomatically atualização, execute Olá os seguintes comandos:

    `sudo yum update RHEL6`ou `sudo yum update RHEL7` consoante Olá família do rhel.

3. Se já não pode ligar toohello antigo RHUI do Azure, siga Olá manual os passos descritos na secção seguinte, Olá.

4. Certifique-se a configuração de Olá tooupdate/instantâneo de imagem de origem de Olá afetados VM aprovisionado a partir de.

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a>Encerramento faseado do Olá RHUI antigo do Azure
Durante o encerramento de Olá de Olá antigo Azure RHUI, iremos restringir acesso tooit da seguinte forma:

1. Restringir mais o tooset de acesso (ACL) de endereços IP que já se ligarem tooit. Possíveis de atribuição de efeitos secundários: Se continuar a utilizar Olá RHUI antigo do Azure – as suas VMs novas podem não ser capaz de tooconnect tooit. VMs de RHEL com IPs dinâmicos que podem passar através de sequência de encerramento/desalocar/início poderá receber novas IP e, por conseguinte, também foi começam a falhar tooconnect toohello RHUI antigo do Azure

2. Encerramento de servidores de entrega de conteúdos do espelho. Possíveis de atribuição de efeitos secundários: como é encerrado CDSes mais poderá ver já `yum update` tempo de manutenção, tempos limite mais até Olá ponto quando já não pode ligar toohello RHUI antigo do Azure.

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a>Olá IPs para servidores de entrega de conteúdos de RHUI Olá novos são
Se estiver a utilizar toofurther de configuração de rede restringir o acesso de RHEL PAYG VMs, certifique-se Olá seguintes IPs é permitida para `yum update` toowork dependendo do ambiente de Olá estiver no. 

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

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a>Atualização manual procedimento toouse Olá novo Azure RHUI servidores
Assinatura de chave pública Olá transferências (através de curl)

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

Certifique-se a chave Olá transferido

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

Verifique a saída de Olá, certifique-se `keyid` e `user ID packet`:

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

Instale a chave pública Olá

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

Transferir, certifique-se e instalar o cliente RPM

Transferir: Para RHEL 6

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

Para RHEL 7

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

Certifique-se:

```bash
rpm -Kv azureclient.rpm
```

Verifique no resultado dessa assinatura Olá pacote é OK

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

Instalar Olá RPM

```bash
sudo rpm -U azureclient.rpm
```

Após a conclusão, verifique se pode aceder Olá de formulário de Azure RHUI VM

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a>Tudo-em-um script para Olá anterior a tarefa de automatização
Utilize Olá seguinte script como tarefa de Olá tooautomate necessários de atualização VMs toohello novo Azure RHUI servidores afetados.

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

## <a name="rhui-overview"></a>Descrição geral RHUI
[Infraestrutura de atualização do Red Hat](https://access.redhat.com/products/red-hat-update-infrastructure) oferece um conteúdo do repositório de yum toomanage solução altamente dimensionável para as instâncias de cloud do Red Hat Enterprise Linux que estão alojados pelos fornecedores de nuvem de certificados do Red Hat. Com base no projeto de Pulp montante Olá, RHUI permite que os fornecedores de nuvem toolocally espelho alojadas Red Hat repositório conteúdo, crie repositórios personalizados com os seus próprios conteúdos e tornar esses repositórios tooa disponíveis grande grupo dos utilizadores finais através de com balanceamento de carga conteúdo de entrega de sistema.

## <a name="regions-where-rhui-is-available"></a>Regiões onde RHUI está disponível
RHUI está disponível em todas as regiões onde as imagens do RHEL a pedido estão disponíveis. Inclui atualmente públicas todas as regiões listadas no Olá [dashboard de estado do Azure](https://azure.microsoft.com/status/) página, regiões do Azure US Government e Datacenters do Azure. Acesso RHUI para VMs aprovisionado a partir de imagens do RHEL a pedido está incluído no respetivo preços. Disponibilidade de nuvem de regionais/national adicionais será atualizada como podemos expanda RHEL a pedido obter disponibilidade em Olá futura.

> [!NOTE]
> Acesso alojadas tooAzure RHUI é limitado toohello VMs dentro [intervalos de IP de centro de dados do Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).
> 
> 

## <a name="get-updates-from-another-update-repository"></a>Obter atualizações a partir do repositório de atualização de outro
Se precisar de atualizações de tooget a partir de um repositório de atualizações diferente (em vez de RHUI alojado no Azure), primeiro é necessário toounregister as instâncias de RHUI. Em seguida, terá de registar toore-las com a infraestrutura de atualização pretendido Olá (como Red Hat satélite ou CDN de Portal de cliente do Red Hat). É necessário adequado subscrições do Red Hat para estes serviços e o registo para [Red Hat acesso à nuvem, no Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).

toounregister RHUI e registe novamente tooyour atualização infraestrutura siga estes passos:

1. Editar /etc/yum.repos.d/rh-cloud.repo e altere todos os `enabled=1` demasiado`enabled=0`. Por exemplo:
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. Editar /etc/yum/pluginconf.d/rhnplugin.conf e alterar `enabled=0` demasiado`enabled=1`.
3. Em seguida, registe a infraestrutura pretendido Olá, tais como o Portal de cliente do Red Hat. Siga o guia de soluções do Red Hat [como tooregister e subscrever um toohello sistema Portal de cliente do Red Hat](https://access.redhat.com/solutions/253273).

> [!NOTE]
> Acesso toohello RHUI alojado no Azure está incluído no preço de imagem Olá RHEL pay as you go (PAYG). Uma VM RHEL PAYG Olá RHUI alojado no Azure ao anular o registo não converter máquina virtual de Olá numa VM do tipo de Bring-Your-proprietário-licença (BYOL). Se registar Olá mesma VM com outra origem das atualizações pode ser incorrer em custos duplos: primeiro de tempo de taxa de software do Azure RHEL e Olá segunda vez para subscrições do Red Hat. 
> 
> Se precisar de forma consistente toouse uma infraestrutura de atualização que não seja alojado no Azure RHUI considere criar e implementar as suas próprias imagens (BYOL-type), conforme descrito em [criar e carregar Red Hat com base em máquina virtual para o Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artigo.
> 

## <a name="next-steps"></a>Passos seguintes
toocreate uma VM do Red Hat Enterprise Linux da imagem do Azure pay as you go de Marketplace e tire partido alojado no Azure RHUI aceda demasiado[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/). Será capaz de toouse `yum update` na sua instância RHEL sem qualquer configuração adicional.

