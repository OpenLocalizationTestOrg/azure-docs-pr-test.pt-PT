## <a name="application-gateway"></a><span data-ttu-id="8b576-101">Gateway de Aplicação</span><span class="sxs-lookup"><span data-stu-id="8b576-101">Application Gateway</span></span>
<span data-ttu-id="8b576-102">Gateway de aplicação fornece uma solução baseada em camada 7 balanceamento de carga de balanceamento de carga HTTP gerida do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b576-102">Application Gateway provides an Azure-managed HTTP load balancing solution based on layer 7 load balancing.</span></span> <span data-ttu-id="8b576-103">Balanceamento de carga de aplicações permite a utilização de Olá de regras de encaminhamento de tráfego de rede com base em HTTP.</span><span class="sxs-lookup"><span data-stu-id="8b576-103">Application load balancing allows hello use of routing rules for network traffic based on HTTP.</span></span> 
<BR>

| <span data-ttu-id="8b576-104">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b576-104">Property</span></span> | <span data-ttu-id="8b576-105">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b576-105">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8b576-106">**backendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="8b576-106">**backendAddressPools**</span></span> |<span data-ttu-id="8b576-107">lista de Olá de endereços IP dos servidores de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="8b576-107">hello list of IP addresses of hello back end servers.</span></span> <span data-ttu-id="8b576-108">endereços IP Olá listados devem pertencer toohello sub-rede da rede virtual, ou devem ser um IP/VIP público ou IP privado</span><span class="sxs-lookup"><span data-stu-id="8b576-108">hello IP addresses listed should either belong toohello virtual network subnet, or should be a public IP/VIP or private IP</span></span> |
| <span data-ttu-id="8b576-109">**backendHttpSettingsCollection**</span><span class="sxs-lookup"><span data-stu-id="8b576-109">**backendHttpSettingsCollection**</span></span> |<span data-ttu-id="8b576-110">Cada conjunto tem definições como a porta, protocolo e a afinidade de cookie com base.</span><span class="sxs-lookup"><span data-stu-id="8b576-110">Every pool has settings like port, protocol, and cookie based affinity.</span></span> <span data-ttu-id="8b576-111">Estas definições estão associada tooa conjunto e são aplicados tooall servidores dentro do conjunto de Olá</span><span class="sxs-lookup"><span data-stu-id="8b576-111">These settings are tied tooa pool and are applied tooall servers within hello pool</span></span> |
| <span data-ttu-id="8b576-112">**frontendPorts**</span><span class="sxs-lookup"><span data-stu-id="8b576-112">**frontendPorts**</span></span> |<span data-ttu-id="8b576-113">Esta porta é a porta pública Olá aberta no gateway de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="8b576-113">This port is hello public port opened on hello application gateway.</span></span> <span data-ttu-id="8b576-114">O tráfego chega a esta porta e, em seguida, obtém redirecionado tooone dos servidores de back-end Olá</span><span class="sxs-lookup"><span data-stu-id="8b576-114">Traffic hits this port, and then gets redirected tooone of hello back end servers</span></span> |
| <span data-ttu-id="8b576-115">**httpListeners**</span><span class="sxs-lookup"><span data-stu-id="8b576-115">**httpListeners**</span></span> |<span data-ttu-id="8b576-116">Serviço de escuta possui uma porta de front-end, um protocolo (Http ou Https, estes são maiúsculas e minúsculas) e Olá nome do certificado SSL (se configurar o SSL offload)</span><span class="sxs-lookup"><span data-stu-id="8b576-116">Listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload)</span></span> |
| <span data-ttu-id="8b576-117">**requestRoutingRules**</span><span class="sxs-lookup"><span data-stu-id="8b576-117">**requestRoutingRules**</span></span> |<span data-ttu-id="8b576-118">regra de Olá vincula Olá Olá e serviço de escuta de back-end agrupamento de servidores e define o tráfego de Olá do agrupamento de servidor back-end deve ser direcionado.</span><span class="sxs-lookup"><span data-stu-id="8b576-118">hello rule binds hello listener and hello back end server pool and defines which back end server pool hello traffic should be directed.</span></span> <span data-ttu-id="8b576-119">Atualmente, funciona apenas como Round robin</span><span class="sxs-lookup"><span data-stu-id="8b576-119">Currently works only as Round-robin</span></span> |

<span data-ttu-id="8b576-120">Exemplo de um modelo de Json do gateway de aplicação:</span><span class="sxs-lookup"><span data-stu-id="8b576-120">Example of an application gateway Json template:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "location": {
          "type": "string",
          "metadata": {
            "description": "Location toodeploy to"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address prefix for hello Virtual Network"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/28",
          "metadata": {
            "description": "Subnet prefix"
          }
        },
        "skuName": {
          "type": "string",
          "allowedValues": [
            "Standard_Small",
            "Standard_Medium",
            "Standard_Large"
          ],
          "defaultValue": "Standard_Medium",
          "metadata": {
            "description": "Sku Name"
          }
        },
        "capacity": {
          "type": "int",
          "defaultValue": 2,
          "metadata": {
            "description": "Number of instances"
          }
        },
        "backendIpAddress1": {
          "type": "string",
          "metadata": {
            "description": "IP Address for Backend Server 1"
          }
        },
        "backendIpAddress2": {
          "type": "string",
          "metadata": {
            "description": "IP Address for Backend Server 2"
          }
        }
      },
      "variables": {
        "applicationGatewayName": "applicationGateway1",
        "publicIPAddressName": "publicIp1",
        "virtualNetworkName": "virtualNetwork1",
        "subnetName": "appGatewaySubnet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPRef": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "applicationGatewayID": "[resourceId('Microsoft.Network/applicationGateways',variables('applicationGatewayName'))]",
        "apiVersion": "2015-05-01-preview"
      },
      "resources": [
        {
          "apiVersion": "[variables('apiVersion')]",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "[variables('publicIPAddressName')]",
          "location": "[parameters('location')]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic"
          }
        },
        {
          "apiVersion": "[variables('apiVersion')]",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "[variables('virtualNetworkName')]",
          "location": "[parameters('location')]",
          "properties": {
            "addressSpace": {
              "addressPrefixes": [
                "[parameters('addressPrefix')]"
              ]
            },
            "subnets": [
              {
                "name": "[variables('subnetName')]",
                "properties": {
                  "addressPrefix": "[parameters('subnetPrefix')]"
                }
              }
            ]
          }
        },
        {
          "apiVersion": "[variables('apiVersion')]",
          "name": "[variables('applicationGatewayName')]",
          "type": "Microsoft.Network/applicationGateways",
          "location": "[parameters('location')]",
          "dependsOn": [
            "[concat('Microsoft.Network/virtualNetworks/', variables    ('virtualNetworkName'))]",
            "[concat('Microsoft.Network/publicIPAddresses/', variables    ('publicIPAddressName'))]"
          ],
          "properties": {
            "sku": {
              "name": "[parameters('skuName')]",
              "tier": "Standard",
              "capacity": "[parameters('capacity')]"
            },
            "gatewayIPConfigurations": [
              {
                "name": "appGatewayIpConfig",
                "properties": {
                  "subnet": {
                    "id": "[variables('subnetRef')]"
                  }
                }
              }
            ],
            "frontendIPConfigurations": [
              {
                "name": "appGatewayFrontendIP",
                "properties": {
                  "PublicIPAddress": {
                    "id": "[variables('publicIPRef')]"
                  }
                }
              }
            ],
            "frontendPorts": [
              {
                "name": "appGatewayFrontendPort",
                "properties": {
                  "Port": 80
                }
              }
            ],
            "backendAddressPools": [
              {
                "name": "appGatewayBackendPool",
                "properties": {
                  "BackendAddresses": [
                    {
                      "IpAddress": "[parameters('backendIpAddress1')]"
                    },
                    {
                      "IpAddress": "[parameters('backendIpAddress2')]"
                    }
                  ]
                }
              }
            ],
            "backendHttpSettingsCollection": [
              {
                "name": "appGatewayBackendHttpSettings",
                "properties": {
                  "Port": 80,
                  "Protocol": "Http",
                  "CookieBasedAffinity": "Disabled"
                }
              }
            ],
            "httpListeners": [
              {
                "name": "appGatewayHttpListener",
                "properties": {
                  "FrontendIPConfiguration": {
                    "Id": "[concat(variables('applicationGatewayID'), '/    frontendIPConfigurations/appGatewayFrontendIP')]"
                  },
                  "FrontendPort": {
                    "Id": "[concat(variables('applicationGatewayID'), '/    frontendPorts/appGatewayFrontendPort')]"
                  },
                  "Protocol": "Http",
                  "SslCertificate": null
                }
              }
            ],
            "requestRoutingRules": [
              {
                "Name": "rule1",
                "properties": {
                  "RuleType": "Basic",
                  "httpListener": {
                    "id": "[concat(variables('applicationGatewayID'), '/    httpListeners/appGatewayHttpListener')]"
                  },
                  "backendAddressPool": {
                    "id": "[concat(variables('applicationGatewayID'), '/    backendAddressPools/appGatewayBackendPool')]"
                  },
                  "backendHttpSettings": {
                    "id": "[concat(variables('applicationGatewayID'), '/    backendHttpSettingsCollection/    appGatewayBackendHttpSettings')]"
                  }
                }
              }
            ]
          }
        }
      ]    
    }


### <a name="additional-resources"></a><span data-ttu-id="8b576-121">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8b576-121">Additional resources</span></span>
<span data-ttu-id="8b576-122">Leitura [ gateway de aplicação API de REST](https://msdn.microsoft.com/library/azure/mt299388.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="8b576-122">Read [ application gateway REST API](https://msdn.microsoft.com/library/azure/mt299388.aspx) for more information.</span></span>

