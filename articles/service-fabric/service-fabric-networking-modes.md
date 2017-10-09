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
# <a name="service-fabric-container-networking-modes"></a>Modos de funcionamento em rede de contentor do Service Fabric

Olá modo predefinido de rede oferecido na Olá recursos de infraestrutura do serviço de cluster para serviços de contentor é Olá `nat` modo de funcionamento em rede. Com Olá `nat` modo, ter mais do que um serviço contentores da toohello do serviço de escuta de rede mesma porta resultados erros de implementação. Para executar vários serviços que escutar Olá suporta a mesma porta, o Service Fabric Olá `open` modo de funcionamento em rede (versão 5.7 ou superior). Com Olá `open` modo de funcionamento em rede, cada serviço de contentor obtém um endereço IP atribuído dinamicamente internamente, permitindo várias toohello de toolisten serviços mesma porta.   

Assim, com um tipo de serviço única com um ponto de final estático definido no manifesto do serviço de Olá, novos serviços podem ser criados e eliminados sem erros de implementação utilizando Olá `open` modo de funcionamento em rede. Da mesma forma, pode utilizar um Olá mesmo `docker-compose.yml` ficheiro com os mapeamentos de porta estática para criar vários serviços.

Utilizar Olá atribuídas dinamicamente serviços toodiscover IP não é recomendado desde Olá alterações do endereço IP quando o serviço de Olá reinicia ou move o nó de tooanother. Utilize apenas Olá **serviço Service Fabric Naming** ou Olá **serviço DNS** para a deteção do serviço. 


> [!WARNING]
> Apenas um total de 4096 IPs são permitidas por vNET no Azure. Assim, Olá a soma de número de Olá de nós e número de Olá de instâncias de serviço de contentor (com `open` redes) não pode exceder 4096 numa vNET. Para esses cenários high-density, Olá `nat` recomenda-se o modo de funcionamento em rede.
>

## <a name="setting-up-open-networking-mode"></a>Configurar o modo de funcionamento em rede aberto

1. Configurar o modelo do Azure Resource Manager Olá ao ativar o serviço DNS e Olá IP de fornecedor em `fabricSettings`. 

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

2. Configure Olá rede perfil secção tooallow toobe configurada em cada nó do cluster de Olá de endereços de IP de vários. Olá exemplo a seguir configura a cinco endereços IP por nó (assim tiver cinco instâncias do serviço de escuta a porta toohello em cada nó) para um cluster do Windows Service Fabric.

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

    Para os clusters do Linux, uma configuração de IP pública adicional é adicionada tooallow conectividade de saída. Olá seguinte fragmento configura cinco endereços IP por nó para um cluster do Linux:

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

3. Para o Windows clusters só, configurar-se um NSG regra abrir a porta UDP/53 Olá vnet com Olá os seguintes valores:

   | Prioridade |    Nome    |    Origem      |  Destino   |   Serviço    | Ação |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     2000 | Custom_Dns | VirtualNetwork | VirtualNetwork | DNS (UDP/53) | Permitir  |


4. Especifique o modo de funcionamento em rede Olá no manifesto da aplicação Olá para cada serviço `<NetworkConfig NetworkType="open">`.  modo de Olá `open` resulta no serviço de Olá obter um endereço IP dedicado. Se um modo não está especificado, será assumida toohello básico `nat` modo. Assim, no seguinte exemplo de manifesto de Olá `NodeContainerServicePackage1` e `NodeContainerServicePackage2` pode cada toohello escuta mesma porta (ambos os serviços estão à escuta em `Endpoint1`).

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
Pode combinar e misturar os modos de rede diferentes nos vários serviços dentro de uma aplicação para um cluster do Windows. Assim, pode ter alguns serviços no `open` modo e alguns no `nat` modo de funcionamento em rede. Quando um serviço está configurado com `nat`, Olá é toomust escuta a porta de ser exclusivo. A combinação de modos de funcionamento em rede para serviços diferentes não é suportada nos clusters do Linux. 


## <a name="next-steps"></a>Passos seguintes
Neste artigo, aprendeu sobre modos oferecidos pelo serviço de recursos de infraestrutura de rede.  

* [Modelo de aplicação de Service Fabric](service-fabric-application-model.md)
* [Recursos manifesto do serviço do Service Fabric](service-fabric-application-model.md)
* [Implementar um tooService de contentor do Windows Fabric no Windows Server 2016](service-fabric-get-started-containers.md)
* [Implementar um tooService de contentor do Docker recursos de infraestrutura no Linux](service-fabric-get-started-containers-linux.md)
