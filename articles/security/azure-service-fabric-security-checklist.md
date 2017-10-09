---
title: "aaaAzure a lista de verificação de segurança de recursos de infraestrutura do serviço | Microsoft Docs"
description: "Este artigo fornece um conjunto de lista de verificação de segurança de segurança de recursos de infraestrutura do Azure."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: 10ffaea9e7e4de6d758b0a57a79e269c87bfd14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-checklist"></a>Lista de verificação de segurança do Azure Service Fabric
Este artigo fornece uma lista de verificação de fácil utilização que irão ajudar a proteger o seu ambiente do Azure Service Fabric.

## <a name="introduction"></a>Introdução
Azure Service Fabric é uma plataforma de sistemas distribuídos que torna mais fácil toopackage, implementar e gerir micro-serviços escaláveis e fiáveis. Service Fabric também aborda os desafios significativos de Olá no desenvolvimento e gestão de aplicações em nuvem. Permite, assim, que os programadores e administradores evitem problemas complexos de infraestrutura e se concentrem na implementação de cargas de trabalho exigentes e fundamentais que sejam dimensionáveis, fiáveis e geríveis.

## <a name="checklist"></a>Lista de verificação
Utilize Olá seguir toohelp de lista de verificação, certifique-se de que ainda não ignoradas problemas importantes na gestão e configuração de uma solução de Azure Service Fabric segura.


|Categoria de lista de verificação| Descrição |
| ------------ | -------- |
|[Controlo de acesso baseado em funções (RBAC)](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security-roles) | <ul><li>Controlo de acesso permite Olá administrador toolimit acesso toocertain cluster operações de cluster para diferentes grupos de utilizadores, tornando o cluster de Olá mais segura.</li><li>Os administradores têm capacidades de toomanagement acesso total (incluindo as capacidades de leitura/escrita). </li><li>   Por predefinição, os utilizadores, tem apenas capacidades de toomanagement de acesso de leitura (por exemplo, capacidades de consulta) e Olá capacidade tooresolve serviços e aplicações.</li></ul>|
|[Certificados x. 509 e o Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security) | <ul><li>[Certificados](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/working-with-certificates) utilizados em clusters de cargas de trabalho de produção em execução devem ser criadas utilizando um serviço de certificado de servidor Windows corretamente configurado ou obtidas a partir de um aprovados [autoridade de certificação (CA)](https://en.wikipedia.org/wiki/Certificate_authority).</li><li>Nunca utilize qualquer [temporário ou testar certificados](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development) na produção que são criados com ferramentas como [MakeCert.exe](https://msdn.microsoft.com/library/windows/desktop/aa386968.aspx). </li><li>Pode utilizar um [certificado autoassinado](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security) mas, deve apenas fazer para clusters de teste e não na produção.</li></ul>|
|[Segurança do cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security) | <ul><li>cenários de segurança do cluster Olá incluem a segurança do nó para o nó, segurança de nó de cliente, [controlo de acesso baseado em funções (RBAC)](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security-roles).</li></ul>|
|[Autenticação do cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) | <ul><li>Autentica [comunicação de nó de nó](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/service-fabric/service-fabric-cluster-security.md) para Federação de cluster. </li></ul>|
|[Autenticação de servidor](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) | <ul><li>Autentica Olá [pontos finais de gestão de cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-portal) tooa cliente de gestão.</li></ul>|
|[Segurança da aplicação](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm)| <ul><li>A encriptação e desencriptação de valores de configuração de aplicação.</li><li> Encriptação dos dados em nós durante a replicação.</li></ul>|
|[Certificado de cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security) | <ul><li>Este certificado é necessário toosecure Olá comunicação entre nós Olá num cluster.</li><li>  Definir o thumbprint Olá Olá primário do certificado de no Olá secção Thumbprint e que Olá secundária em variáveis de ThumbprintSecondary Olá.</li></ul>|
|[ServerCertificate](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security)| <ul><li>Este certificado é apresentado toohello cliente quando este tenta tooconnect toothis cluster. Pode utilizar dois certificados de servidor diferente, um servidor principal e secundária para a atualização.</li></ul>|
|ClientCertificateThumbprints| <ul><li>Este é um conjunto de certificados que pretende que o tooinstall nos clientes Olá autenticado. </li></ul>|
|ClientCertificateCommonNames| <ul><li>Definir Olá nome comum do certificado de cliente primeiro Olá para Olá CertificateCommonName. Olá CertificateIssuerThumbprint é Olá impressão digital para emissor Olá deste certificado. </li></ul>|
|ReverseProxyCertificate| <ul><li>Este é um certificado opcional que pode ser especificado se quiser toosecure sua [Proxy inverso](https://docs.microsoft.com/en-in/azure/service-fabric/service-fabric-reverseproxy). </li></ul>|
|Cofre de Chaves| <ul><li>Utilizadas toomanage certificados em clusters de Service Fabric no Azure.  </li></ul>|


## <a name="next-steps"></a>Passos seguintes
- [Processo de atualização de Cluster do Service Fabric e as expectativas do utilizador](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-upgrade)
- [Gerir as aplicações de Service Fabric no Visual Studio](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-manage-application-in-visual-studio).
- [Introdução de modelo de estado de funcionamento do serviço Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-health-introduction).
