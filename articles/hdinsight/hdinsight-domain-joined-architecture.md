---
title: arquitetura do Azure HDInsight associados a um aaaDomain | Microsoft Docs
description: "Saiba como tooplan associados a um domínio HDInsight."
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7dc6847d-10d4-4b5c-9c83-cc513cf91965
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: saurinsh
ms.openlocfilehash: 1c3ecedf3739b4f8fa54160225be9c1d6e2ca6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="plan-azure-domain-joined-hadoop-clusters-in-hdinsight"></a>Planear clusters do Hadoop associados a um domínio do Azure no HDInsight

Olá Hadoop tradicional é um cluster de utilizador único. É adequado à maioria das empresas em que as cargas de trabalho de dados de grande dimensão são criadas por pequenas equipas de aplicações. À medida que a popularidade do Hadoop aumenta, muitas empresas estão a migrar para um modelo no qual os clusters são geridos pelas equipas de TI e em que várias equipas de aplicações partilham esses clusters. Assim, as funcionalidades que envolvem clusters multiuser estão entre Olá mais pedidas funcionalidades no Azure HDInsight.

Em vez de criar a sua própria multiuser autenticação e autorização, HDInsight depende do fornecedor de identidade mais popular Olá – do Active Directory (AD). funcionalidade de segurança poderosas Olá no AD pode ser utilizado toomanage autorização multiuser no HDInsight. Ao integrar o HDInsight com o AD, pode comunicar com clusters de Olá com as suas credenciais do AD. HDInsight mapeia um utilizador tooa local Hadoop utilizador do AD, para que todos os serviços em execução no HDInsight de Olá (Ambari, thrift de Spark do servidor, Ranger, de ramo de registo do servidor e outros) funcionam perfeitamente para utilizador Olá autenticado.

## <a name="integrate-hdinsight-with-ad-and-ad-on-iaas-vm"></a>Integrar o HDInsight com o AD e AD na VM do IaaS

Ao integrar o HDInsight com o Azure AD ou AD na VM do Iaas, nós de cluster do HDInsight Olá estão associados a um domínio tooa domínio. HDInsight cria principais de serviço para Olá serviços do Hadoop em execução no cluster de Olá e coloca-os dentro de uma unidade organizacional (UO) especificada no Azure AD ou AD na VM do IaaS. HDInsight também cria mapeamentos inversas de DNS no domínio de Olá para Olá endereços IP de nós Olá toohello associado ao domínio.

Para obter esta configuração, pode utilizar várias arquiteturas. Pode escolher entre Olá arquiteturas a seguir.

**HDInsight integrado com o AD em execução no IaaS do Azure**

Esta é a arquitetura mais simples de Olá para integrar HDInsight com o Active Directory. Olá controlador de domínio do AD é executado num (ou vários) máquinas de virtuais (VMs) no Azure. Normalmente, estas VMs estão dentro de uma rede virtual. Configurar a outra rede virtual de cluster do HDInsight Olá. Para o HDInsight toohave tooActive uma linha de visão diretório, terá de toopeer estas redes virtuais utilizando [vnet para VNet peering](../virtual-network/virtual-network-create-peering.md). Se criar hello do Active Directory no ARM, em seguida, pode criar Olá do Active Directory e o HDInsight no Olá mesma VNet e não precisa de toodo peering. 

![Topologia do cluster do HDInsight associado a domínio](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_1.png)

> [!NOTE]
> Nesta arquitetura, não é possível utilizar o Azure Data Lake Store com o cluster do HDInsight Olá.


Pré-requisitos para o Active Directory:

* Um [unidade organizacional](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) tem de ser criado, no qual é colocar Olá VMs de cluster do HDInsight e Olá principais de serviço utilizados pelo cluster Olá.
* [Protocolos de acesso do Lightweight Directory](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) (LDAPs) tem de ser configurados para comunicar com o AD. Olá certificado utilizado tooset segurança LDAPS tem de ser um certificado real (não um certificado autoassinado).
* Zonas DNS inversas têm de ser criadas no domínio Olá para o intervalo de endereços IP Olá da sub-rede de HDInsight Olá (por exemplo, 10.2.0.0/24 na imagem anterior Olá).
* É necessária uma conta de serviço ou uma conta de utilizador. Utilize o cluster do HDInsight toocreate Olá esta conta. Esta conta tem de ter Olá as seguintes permissões:

    - Objetos de principais de serviço do permissões toocreate e objetos de máquina numa unidade organizacional Olá
    - Permissões toocreate inversas DNS proxy as regras
    - Domínio do permissões toojoin máquinas toohello do Active Directory

**HDInsight integrado num Azure AD apenas na cloud**

Para um Azure AD apenas na cloud, configure um controlador de domínio para que o HDInsight possa ser integrado no Azure AD. Isto é conseguido utilizando [do Azure Active Directory Domain Services](../active-directory-domain-services/active-directory-ds-overview.md) (Azure AD DS). Azure AD DS cria as máquinas do controlador de domínio na nuvem de Olá e fornece endereços IP para os mesmos. Cria dois controladores de domínio, para elevada disponibilidade.

Atualmente, o Azure AD DS só existe em redes virtuais clássicas. Só é acessível através da utilização de Olá portal clássico do Azure. Olá HDInsight rede virtual existe no Olá portal do Azure, o que precisa de toobe em modo de peering com a rede virtual clássica de Olá através da utilização de VNet a VNet peering.

> [!NOTE]
> Peering entre uma rede virtual clássica e uma rede virtual requer que ambas as redes virtuais estão do Azure Resource Manager Olá mesma região e em Olá mesma subscrição do Azure.

![Topologia do cluster do HDInsight associado a domínio](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_2.png)

Pré-requisitos para o Azure AD:

* Um [unidade organizacional](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) tem de ser criada dentro do qual é colocar Olá VMs de cluster do HDInsight e Olá principais de serviço utilizados pelo cluster Olá.
* O [LDAPS](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) tem de ser configurado quando configurar o Azure AD DS. Olá certificado utilizado tooset segurança LDAPS tem de ser um certificado real (não um certificado autoassinado).
* Zonas DNS inversas têm de ser criadas no domínio Olá para o intervalo de endereços IP Olá da sub-rede de HDInsight Olá (por exemplo, 10.2.0.0/24 na imagem anterior Olá).
* [Os hashes de palavra-passe](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md) tem de ser sincronizados a partir do Azure AD tooAzure do AD DS.
* É necessária uma conta de serviço ou uma conta de utilizador. Utilize o cluster do HDInsight toocreate Olá esta conta. Esta conta tem de ter Olá as seguintes permissões:

    - Objetos de principais de serviço do permissões toocreate e objetos de máquina numa unidade organizacional Olá
    - Permissões toocreate inversas DNS proxy as regras
    - Domínio do permissões toojoin máquinas toohello do Azure AD

## <a name="next-steps"></a>Passos seguintes
* tooconfigure um cluster do HDInsight associados a um domínio, consulte [configurar clusters do HDInsight associados a um domínio](hdinsight-domain-joined-configure.md).
* toomanage associados a um domínio os clusters do HDInsight, consulte [gerir clusters do HDInsight associados a um domínio](hdinsight-domain-joined-manage.md).
* políticas de ramo de registo tooconfigure e executadas consultas do Hive, consulte [configurar Hive políticas associados a um domínio para clusters do HDInsight](hdinsight-domain-joined-run-hive.md).
* consultas do Hive toorun utilizando SSH nos clusters do HDInsight associados a um domínio, consulte [utilizar o SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
