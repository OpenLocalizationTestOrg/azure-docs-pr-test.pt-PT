---
title: "aaaIntroduction tooAzure serviço de contentor para Kubernetes | Microsoft Docs"
description: "Serviço de contentor do Azure para Kubernetes torna simple toodeploy e gerir as aplicações baseadas no contentor no Azure."
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kubernetes, Docker, Containers, Microsserviços, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a>Introdução tooAzure serviço de contentor para Kubernetes
Serviço de contentor do Azure para Kubernetes torna simple toocreate, configurar e gerir um cluster de máquinas virtuais que estão pré-configuradas toorun de aplicações. Isto permite-lhe toouse suas competências existentes, ou desenhar após um corpo de grande e crescente de conhecimentos de Comunidade, toodeploy e gerir as aplicações baseadas no contentor no Microsoft Azure.

Ao utilizar o serviço de contentor do Azure, pode tirar partido das Olá funcionalidades de nível empresarial do Azure, mantendo ainda portabilidade de aplicações através de Kubernetes e Olá formato de imagem de Docker.

## <a name="using-azure-container-service-for-kubernetes"></a>Utilizar o Azure Container Service para Kubernetes
O nosso objetivo com o serviço de contentor do Azure é tooprovide num ambiente de alojamento do contentor utilizando ferramentas open source e tecnologias que estão atualmente populares entre os nossos clientes. fim de toothis, expomos pontos finais da API de Kubernetes padrão Olá. Utilizando estes pontos finais padrão, pode tirar partido do software que seja capaz de comunicar tooa Kubernetes cluster. Por exemplo, pode escolher [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/) ou [draft](https://github.com/Azure/draft).

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a>Criar um cluster do Kubernetes com o Azure Container Service
toobegin utilizando o serviço de contentor do Azure, implementar um cluster do serviço de contentor do Azure com Olá [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) ou através do portal Olá (Olá pesquisa Marketplace para **serviço de contentor Azure**). Se um utilizador avançado que necessitam de mais controlo sobre os modelos do Azure Resource Manager Olá, pode utilizar open source para Olá [motor de acs](https://github.com/Azure/acs-engine) projeto toobuild os seus próprios Kubernetes personalizados do cluster e implementá-la através de Olá `az` CLI.

### <a name="using-kubernetes"></a>Utilizar Kubernetes
O Kubernetes automatiza a implementação, o dimensionamento e a gestão de aplicações no contentor. Tem um conjunto avançado de funcionalidades, incluindo:
* Empacotamento automático
* Autorrecuperação
* Dimensionamento horizontal
* Deteção do serviço e balanceamento de carga
* Implementações e reversões automáticas
* Gestão de segredos e de configurações
* Orquestração de armazenamento
* Execução de lotes

Diagrama da arquitetura de Kubernetes implementado através do Azure Container Service:

![Serviço de contentor do Azure configurada toouse Kubernetes.](media/acs-intro/kubernetes.png)

## <a name="videos"></a>Vídeos

Suporte de Kubernetes no Azure Container Service (Azure Friday, janeiro de 2017):

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

Ferramentas para Programar e Implementar Aplicações no Kubernetes (Azure OpenDev, junho de 2017):

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a>Passos seguintes

Explorar Olá [início rápido de Kubernetes](container-service-kubernetes-walkthrough.md) toobegin explorar o serviço de contentor do Azure hoje.
