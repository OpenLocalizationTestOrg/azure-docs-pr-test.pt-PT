---
title: "aaaConfigure redes modos de serviços de contentor do Azure Service Fabric | Microsoft Docs"
description: "Saiba como modos de rede diferentes toosetup Olá suporta esse Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 5c5dd4c590c7698a947503cbe8ef66ff7d6b503a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-container-networking-modes"></a><span data-ttu-id="0ad47-103">Modos de funcionamento em rede de contentor do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0ad47-103">Service Fabric container networking modes</span></span>

<span data-ttu-id="0ad47-104">Olá modo predefinido de rede oferecido na Olá recursos de infraestrutura do serviço de cluster para serviços de contentor é Olá `nat` modo de funcionamento em rede.</span><span class="sxs-lookup"><span data-stu-id="0ad47-104">hello default networking mode offered in hello Service Fabric cluster for container services is hello `nat` networking mode.</span></span> <span data-ttu-id="0ad47-105">Com Olá `nat` modo, ter mais do que um serviço contentores da toohello do serviço de escuta de rede mesma porta resultados erros de implementação.</span><span class="sxs-lookup"><span data-stu-id="0ad47-105">With hello `nat` networking mode, having more than one containers service listening toohello same port results in deployment errors.</span></span> <span data-ttu-id="0ad47-106">Para executar vários serviços que escutar Olá suporta a mesma porta, o Service Fabric Olá `open` modo de funcionamento em rede (versão 5.7 ou superior).</span><span class="sxs-lookup"><span data-stu-id="0ad47-106">For running several services that listen on hello same port, Service Fabric supports hello `open` networking mode (version 5.7 or higher).</span></span> <span data-ttu-id="0ad47-107">Com Olá `open` modo de funcionamento em rede, cada serviço de contentor obtém um endereço IP atribuído dinamicamente internamente, permitindo várias toohello de toolisten serviços mesma porta.</span><span class="sxs-lookup"><span data-stu-id="0ad47-107">With hello `open` networking mode, each container service gets a dynamically assigned IP address internally allowing multiple services toolisten toohello same port.</span></span>   

<span data-ttu-id="0ad47-108">Assim, com um tipo de serviço única com um ponto de final estático definido no manifesto do serviço de Olá, novos serviços podem ser criados e eliminados sem erros de implementação utilizando Olá `open` modo de funcionamento em rede.</span><span class="sxs-lookup"><span data-stu-id="0ad47-108">Thus, with a single service type with a static endpoint defined in hello service manifest, new services may be created and deleted without deployment errors using hello `open` networking mode.</span></span> <span data-ttu-id="0ad47-109">Da mesma forma, pode utilizar um Olá mesmo `docker-compose.yml` ficheiro com os mapeamentos de porta estática para criar vários serviços.</span><span class="sxs-lookup"><span data-stu-id="0ad47-109">Similarly, one can use hello same `docker-compose.yml` file with static port mappings for creating multiple services.</span></span>

<span data-ttu-id="0ad47-110">Utilizar Olá atribuídas dinamicamente serviços toodiscover IP não é recomendado desde Olá alterações do endereço IP quando o serviço de Olá reinicia ou move o nó de tooanother.</span><span class="sxs-lookup"><span data-stu-id="0ad47-110">Using hello dynamically assigned IP toodiscover services is not advisable since hello IP address changes when hello service restarts or moves tooanother node.</span></span> <span data-ttu-id="0ad47-111">Utilize apenas Olá **serviço Service Fabric Naming** ou Olá **serviço DNS** para a deteção do serviço.</span><span class="sxs-lookup"><span data-stu-id="0ad47-111">Only use hello **Service Fabric Naming Service**  or hello **DNS Service** for service discovery.</span></span> 


> [!WARNING]
> <span data-ttu-id="0ad47-112">Apenas um total de 4096 IPs são permitidas por vNET no Azure.</span><span class="sxs-lookup"><span data-stu-id="0ad47-112">Only a total of 4096 IPs are allowed per vNET in Azure.</span></span> <span data-ttu-id="0ad47-113">Assim, Olá a soma de número de Olá de nós e número de Olá de instâncias de serviço de contentor (com `open` redes) não pode exceder 4096 numa vNET.</span><span class="sxs-lookup"><span data-stu-id="0ad47-113">Thus, hello sum of hello number of nodes and hello number of container service instances (with `open` networking) cannot exceed 4096 within a vNET.</span></span> <span data-ttu-id="0ad47-114">Para esses cenários high-density, Olá `nat` recomenda-se o modo de funcionamento em rede.</span><span class="sxs-lookup"><span data-stu-id="0ad47-114">For such high-density scenarios, hello `nat` networking mode is recommended.</span></span>
>

## <a name="setting-up-open-networking-mode"></a><span data-ttu-id="0ad47-115">Configurar o modo de funcionamento em rede aberto</span><span class="sxs-lookup"><span data-stu-id="0ad47-115">Setting up open networking mode</span></span>

1. <span data-ttu-id="0ad47-116">Configurar o modelo do Azure Resource Manager Olá ao ativar o serviço DNS e Olá IP de fornecedor em `fabricSettings`.</span><span class="sxs-lookup"><span data-stu-id="0ad47-116">Set up hello Azure Resource Manager template by enabling DNS Service and hello IP Provider under `fabricSettings`.</span></span> 

    ```json
    "fabricSettings": [
                {
                    "name": "DnsService",
                    "parameters": [
                       {
                            "name": "IsEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name": "Hosting",
                    "parameters": [
                      { 
                            "name": "IPProviderEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name":  "Trace/Etw", 
                    "parameters": [
                    {
                            "name": "Level",
                            "value": "5"
                    }
                    ]
                },
                {
                    "name": "Setup",
                    "parameters": [
                    {
                            "name": "ContainerNetworkSetup",
                            "value": "true"
                    }
                    ]
                }
            ],
    ```

2. <span data-ttu-id="0ad47-117">Configure Olá rede perfil secção tooallow toobe configurada em cada nó do cluster de Olá de endereços de IP de vários.</span><span class="sxs-lookup"><span data-stu-id="0ad47-117">Set up hello network profile section tooallow multiple IP addresses toobe configured on each node of hello cluster.</span></span> <span data-ttu-id="0ad47-118">Olá exemplo a seguir configura a cinco endereços IP por nó (assim tiver cinco instâncias do serviço de escuta a porta toohello em cada nó) para um cluster do Windows Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0ad47-118">hello following example sets up five IP addresses per node (thus you can have five service instances listening toohello port on each node) for a Windows Service Fabric cluster.</span></span>

    ```json
    "variables": {
        "nicName": "NIC",
        "vmName": "vm",
        "virtualNetworkName": "VNet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "vmNodeType0Name": "[toLower(concat('NT1', variables('vmName')))]",
        "subnet0Name": "Subnet-0",
        "subnet0Prefix": "10.0.0.0/24",
        "subnet0Ref": "[concat(variables('vnetID'),'/subnets/',variables('subnet0Name'))]",
        "lbID0": "[resourceId('Microsoft.Network/loadBalancers',concat('LB','-', parameters('clusterName'),'-',variables('vmNodeType0Name')))]",
        "lbIPConfig0": "[concat(variables('lbID0'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
        "lbPoolID0": "[concat(variables('lbID0'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
        "lbProbeID0": "[concat(variables('lbID0'),'/probes/FabricGatewayProbe')]",
        "lbHttpProbeID0": "[concat(variables('lbID0'),'/probes/FabricHttpGatewayProbe')]",
        "lbNatPoolID0": "[concat(variables('lbID0'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]"
    }
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

    <span data-ttu-id="0ad47-119">Para os clusters do Linux, uma configuração de IP pública adicional é adicionada tooallow conectividade de saída.</span><span class="sxs-lookup"><span data-stu-id="0ad47-119">For Linux clusters, an additional public IP configuration is added tooallow outbound connectivity.</span></span> <span data-ttu-id="0ad47-120">Olá seguinte fragmento configura cinco endereços IP por nó para um cluster do Linux:</span><span class="sxs-lookup"><span data-stu-id="0ad47-120">hello following snippet sets up five IP addresses per node for a Linux cluster:</span></span>

    ```json
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "publicipaddressconfiguration": {
                              "name": "devpub",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 1)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 2)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 3)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 4)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 5)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

3. <span data-ttu-id="0ad47-121">Para o Windows clusters só, configurar-se um NSG regra abrir a porta UDP/53 Olá vnet com Olá os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="0ad47-121">For Windows clusters only, set up an NSG rule opening up port UDP/53 for hello vNET with hello following values:</span></span>

   | <span data-ttu-id="0ad47-122">Prioridade</span><span class="sxs-lookup"><span data-stu-id="0ad47-122">Priority</span></span> |    <span data-ttu-id="0ad47-123">Nome</span><span class="sxs-lookup"><span data-stu-id="0ad47-123">Name</span></span>    |    <span data-ttu-id="0ad47-124">Origem</span><span class="sxs-lookup"><span data-stu-id="0ad47-124">Source</span></span>      |  <span data-ttu-id="0ad47-125">Destino</span><span class="sxs-lookup"><span data-stu-id="0ad47-125">Destination</span></span>   |   <span data-ttu-id="0ad47-126">Serviço</span><span class="sxs-lookup"><span data-stu-id="0ad47-126">Service</span></span>    | <span data-ttu-id="0ad47-127">Ação</span><span class="sxs-lookup"><span data-stu-id="0ad47-127">Action</span></span> |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     <span data-ttu-id="0ad47-128">2000</span><span class="sxs-lookup"><span data-stu-id="0ad47-128">2000</span></span> | <span data-ttu-id="0ad47-129">Custom_Dns</span><span class="sxs-lookup"><span data-stu-id="0ad47-129">Custom_Dns</span></span> | <span data-ttu-id="0ad47-130">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="0ad47-130">VirtualNetwork</span></span> | <span data-ttu-id="0ad47-131">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="0ad47-131">VirtualNetwork</span></span> | <span data-ttu-id="0ad47-132">DNS (UDP/53)</span><span class="sxs-lookup"><span data-stu-id="0ad47-132">DNS (UDP/53)</span></span> | <span data-ttu-id="0ad47-133">Permitir</span><span class="sxs-lookup"><span data-stu-id="0ad47-133">Allow</span></span>  |


4. <span data-ttu-id="0ad47-134">Especifique o modo de funcionamento em rede Olá no manifesto da aplicação Olá para cada serviço `<NetworkConfig NetworkType="open">`.</span><span class="sxs-lookup"><span data-stu-id="0ad47-134">Specify hello networking mode in hello app manifest for each service `<NetworkConfig NetworkType="open">`.</span></span>  <span data-ttu-id="0ad47-135">modo de Olá `open` resulta no serviço de Olá obter um endereço IP dedicado.</span><span class="sxs-lookup"><span data-stu-id="0ad47-135">hello mode `open` results in hello service getting a dedicated IP address.</span></span> <span data-ttu-id="0ad47-136">Se um modo não está especificado, será assumida toohello básico `nat` modo.</span><span class="sxs-lookup"><span data-stu-id="0ad47-136">If a mode isn't specified, it defaults toohello basic `nat` mode.</span></span> <span data-ttu-id="0ad47-137">Assim, no seguinte exemplo de manifesto de Olá `NodeContainerServicePackage1` e `NodeContainerServicePackage2` pode cada toohello escuta mesma porta (ambos os serviços estão à escuta em `Endpoint1`).</span><span class="sxs-lookup"><span data-stu-id="0ad47-137">Thus, in hello following manifest example, `NodeContainerServicePackage1` and `NodeContainerServicePackage2` can each listen toohello same port (both services are listening on `Endpoint1`).</span></span>

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <ApplicationManifest ApplicationTypeName="NodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <Description>Calculator Application</Description>
      <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
        <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
      </Parameters>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage1" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService1.Code" Isolation="hyperv">
           <NetworkConfig NetworkType="open"/>
           <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage2" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService2.Code" Isolation="default">
            <NetworkConfig NetworkType="open"/>
            <PortBinding ContainerPort="8910" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
    </ApplicationManifest>
    ```
<span data-ttu-id="0ad47-138">Pode combinar e misturar os modos de rede diferentes nos vários serviços dentro de uma aplicação para um cluster do Windows.</span><span class="sxs-lookup"><span data-stu-id="0ad47-138">You can mix and match different networking modes across services within an application for a Windows cluster.</span></span> <span data-ttu-id="0ad47-139">Assim, pode ter alguns serviços no `open` modo e alguns no `nat` modo de funcionamento em rede.</span><span class="sxs-lookup"><span data-stu-id="0ad47-139">Thus, you can have some services on `open` mode and some on `nat` networking mode.</span></span> <span data-ttu-id="0ad47-140">Quando um serviço está configurado com `nat`, Olá é toomust escuta a porta de ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="0ad47-140">When a service is configured with `nat`, hello port it is listening toomust be unique.</span></span> <span data-ttu-id="0ad47-141">A combinação de modos de funcionamento em rede para serviços diferentes não é suportada nos clusters do Linux.</span><span class="sxs-lookup"><span data-stu-id="0ad47-141">Mixing networking modes for different services isn't supported on Linux clusters.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="0ad47-142">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0ad47-142">Next steps</span></span>
<span data-ttu-id="0ad47-143">Neste artigo, aprendeu sobre modos oferecidos pelo serviço de recursos de infraestrutura de rede.</span><span class="sxs-lookup"><span data-stu-id="0ad47-143">In this article, you learned about networking modes offered by Service Fabric.</span></span>  

* [<span data-ttu-id="0ad47-144">Modelo de aplicação de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0ad47-144">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="0ad47-145">Recursos manifesto do serviço do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0ad47-145">Service Fabric service manifest resources</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="0ad47-146">Implementar um tooService de contentor do Windows Fabric no Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="0ad47-146">Deploy a Windows container tooService Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="0ad47-147">Implementar um tooService de contentor do Docker recursos de infraestrutura no Linux</span><span class="sxs-lookup"><span data-stu-id="0ad47-147">Deploy a Docker container tooService Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
