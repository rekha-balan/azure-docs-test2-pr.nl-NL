## <a name="load-balancer"></a><span data-ttu-id="1e6bf-101">Load Balancer</span><span class="sxs-lookup"><span data-stu-id="1e6bf-101">Load Balancer</span></span>
<span data-ttu-id="1e6bf-102">A load balancer is used when you want to scale your applications.</span><span class="sxs-lookup"><span data-stu-id="1e6bf-102">A load balancer is used when you want to scale your applications.</span></span> <span data-ttu-id="1e6bf-103">Typical deployment scenarios involve applications running on multiple VM instances.</span><span class="sxs-lookup"><span data-stu-id="1e6bf-103">Typical deployment scenarios involve applications running on multiple VM instances.</span></span> <span data-ttu-id="1e6bf-104">The VM instances are fronted by a load balancer that helps to distribute network traffic to the various instances.</span><span class="sxs-lookup"><span data-stu-id="1e6bf-104">The VM instances are fronted by a load balancer that helps to distribute network traffic to the various instances.</span></span> 

![NIC's on a single VM](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/resource-groups-networking/figure8.png)

| <span data-ttu-id="1e6bf-106">Property</span><span class="sxs-lookup"><span data-stu-id="1e6bf-106">Property</span></span> | <span data-ttu-id="1e6bf-107">Description</span><span class="sxs-lookup"><span data-stu-id="1e6bf-107">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1e6bf-108">*frontendIPConfigurations*</span><span class="sxs-lookup"><span data-stu-id="1e6bf-108">*frontendIPConfigurations*</span></span> |<span data-ttu-id="1e6bf-109">a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span><span class="sxs-lookup"><span data-stu-id="1e6bf-109">a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="1e6bf-110">These IP addresses serve as ingress for the traffic and can be public IP or private IP</span><span class="sxs-lookup"><span data-stu-id="1e6bf-110">These IP addresses serve as ingress for the traffic and can be public IP or private IP</span></span> |
| <span data-ttu-id="1e6bf-111">*backendAddressPools*</span><span class="sxs-lookup"><span data-stu-id="1e6bf-111">*backendAddressPools*</span></span> |<span data-ttu-id="1e6bf-112">these are IP addresses associated with the VM NICs to which load will be distributed</span><span class="sxs-lookup"><span data-stu-id="1e6bf-112">these are IP addresses associated with the VM NICs to which load will be distributed</span></span> |
| <span data-ttu-id="1e6bf-113">*loadBalancingRules*</span><span class="sxs-lookup"><span data-stu-id="1e6bf-113">*loadBalancingRules*</span></span> |<span data-ttu-id="1e6bf-114">a rule property maps a given front end IP and port combination to a set of back end IP addresses and port combination.</span><span class="sxs-lookup"><span data-stu-id="1e6bf-114">a rule property maps a given front end IP and port combination to a set of back end IP addresses and port combination.</span></span> <span data-ttu-id="1e6bf-115">With a single definition of a load balancer resource, you can define multiple load balancing rules, each rule reflecting a combination of a front end IP and port and back end IP and port associated with virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1e6bf-115">With a single definition of a load balancer resource, you can define multiple load balancing rules, each rule reflecting a combination of a front end IP and port and back end IP and port associated with virtual machines.</span></span> <span data-ttu-id="1e6bf-116">The rule is one port in the front end pool to many virtual machines in the back end pool</span><span class="sxs-lookup"><span data-stu-id="1e6bf-116">The rule is one port in the front end pool to many virtual machines in the back end pool</span></span> |
| <span data-ttu-id="1e6bf-117">*Probes*</span><span class="sxs-lookup"><span data-stu-id="1e6bf-117">*Probes*</span></span> |<span data-ttu-id="1e6bf-118">probes enable you to keep track of the health of VM instances.</span><span class="sxs-lookup"><span data-stu-id="1e6bf-118">probes enable you to keep track of the health of VM instances.</span></span> <span data-ttu-id="1e6bf-119">If a health probe fails, the virtual machine instance will be taken out of rotation automatically</span><span class="sxs-lookup"><span data-stu-id="1e6bf-119">If a health probe fails, the virtual machine instance will be taken out of rotation automatically</span></span> |
| <span data-ttu-id="1e6bf-120">*inboundNatRules*</span><span class="sxs-lookup"><span data-stu-id="1e6bf-120">*inboundNatRules*</span></span> |<span data-ttu-id="1e6bf-121">NAT rules defining the inbound traffic flowing through the front end IP and distributed to the back end IP to a specific virtual machine instance.</span><span class="sxs-lookup"><span data-stu-id="1e6bf-121">NAT rules defining the inbound traffic flowing through the front end IP and distributed to the back end IP to a specific virtual machine instance.</span></span> <span data-ttu-id="1e6bf-122">NAT rule is one port in the front end pool to one virtual machine in the back end pool</span><span class="sxs-lookup"><span data-stu-id="1e6bf-122">NAT rule is one port in the front end pool to one virtual machine in the back end pool</span></span> |

<span data-ttu-id="1e6bf-123">Example of load balancer template in Json format:</span><span class="sxs-lookup"><span data-stu-id="1e6bf-123">Example of load balancer template in Json format:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "dnsNameforLBIP": {
          "type": "string",
          "metadata": {
            "description": "Unique DNS name"
          }
        },
        "location": {
          "type": "string",
          "allowedValues": [
            "East US",
            "West US",
            "West Europe",
            "East Asia",
            "Southeast Asia"
          ],
          "metadata": {
            "description": "Location to deploy"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address Prefix"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/24",
          "metadata": {
            "description": "Subnet Prefix"
          }
        },
        "publicIPAddressType": {
          "type": "string",
          "defaultValue": "Dynamic",
          "allowedValues": [
            "Dynamic",
            "Static"
          ],
          "metadata": {
            "description": "Public IP type"
          }
        }
      },
      "variables": {
        "virtualNetworkName": "virtualNetwork1",
        "publicIPAddressName": "publicIp1",
        "subnetName": "subnet1",
        "loadBalancerName": "loadBalancer1",
        "nicName": "networkInterface1",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
        "nicId": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
        "backEndIPConfigID": "[concat(variables('nicId'),'/ipConfigurations/ipconfig1')]"
      },
      "resources": [
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[parameters('location')]",
      "properties": {
        "publicIPAllocationMethod": "[parameters('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsNameforLBIP')]"
        }
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
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
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "subnet": {
                "id": "[variables('subnetRef')]"
              },
              "loadBalancerBackendAddressPools": [
                {
                  "id": "[concat(variables('lbID'), '/backendAddressPools/LoadBalancerBackend')]"
                }
              ],
              "loadBalancerInboundNatRules": [
                {
                  "id": "[concat(variables('lbID'),'/inboundNatRules/RDP')]"
                }
              ]
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[variables('publicIPAddressID')]"
              }
            }
          }
        ],
        "backendAddressPools": [
          {
            "name": "loadBalancerBackEnd"
          }
        ],
        "inboundNatRules": [
          {
            "name": "RDP",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPort": 3389,
              "backendPort": 3389,
              "enableFloatingIP": false
            }
          }
        ]
      }
    }
      ]
    }

### <a name="additional-resources"></a><span data-ttu-id="1e6bf-124">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1e6bf-124">Additional resources</span></span>
<span data-ttu-id="1e6bf-125">Read [load balancer REST API](https://msdn.microsoft.com/library/azure/mt163651.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="1e6bf-125">Read [load balancer REST API](https://msdn.microsoft.com/library/azure/mt163651.aspx) for more information.</span></span>


