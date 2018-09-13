## <a name="nic"></a><span data-ttu-id="0ae4e-101">NIC</span><span class="sxs-lookup"><span data-stu-id="0ae4e-101">NIC</span></span>
<span data-ttu-id="0ae4e-102">A network interface card (NIC) resource provides network connectivity to an existing subnet in a VNet resource.</span><span class="sxs-lookup"><span data-stu-id="0ae4e-102">A network interface card (NIC) resource provides network connectivity to an existing subnet in a VNet resource.</span></span> <span data-ttu-id="0ae4e-103">Although you can create a NIC as a stand alone object, you need to associate it to another object to actually provide connectivity.</span><span class="sxs-lookup"><span data-stu-id="0ae4e-103">Although you can create a NIC as a stand alone object, you need to associate it to another object to actually provide connectivity.</span></span> <span data-ttu-id="0ae4e-104">A NIC can be used to connect a VM to a subnet, a public IP address, or a load balancer.</span><span class="sxs-lookup"><span data-stu-id="0ae4e-104">A NIC can be used to connect a VM to a subnet, a public IP address, or a load balancer.</span></span>  

| <span data-ttu-id="0ae4e-105">Property</span><span class="sxs-lookup"><span data-stu-id="0ae4e-105">Property</span></span> | <span data-ttu-id="0ae4e-106">Description</span><span class="sxs-lookup"><span data-stu-id="0ae4e-106">Description</span></span> | <span data-ttu-id="0ae4e-107">Sample values</span><span class="sxs-lookup"><span data-stu-id="0ae4e-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ae4e-108">**virtualMachine**</span><span class="sxs-lookup"><span data-stu-id="0ae4e-108">**virtualMachine**</span></span> |<span data-ttu-id="0ae4e-109">VM the NIC is associated with.</span><span class="sxs-lookup"><span data-stu-id="0ae4e-109">VM the NIC is associated with.</span></span> |<span data-ttu-id="0ae4e-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span><span class="sxs-lookup"><span data-stu-id="0ae4e-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span></span> |
| <span data-ttu-id="0ae4e-111">**macAddress**</span><span class="sxs-lookup"><span data-stu-id="0ae4e-111">**macAddress**</span></span> |<span data-ttu-id="0ae4e-112">MAC address for the NIC</span><span class="sxs-lookup"><span data-stu-id="0ae4e-112">MAC address for the NIC</span></span> |<span data-ttu-id="0ae4e-113">any value between 4 and 30</span><span class="sxs-lookup"><span data-stu-id="0ae4e-113">any value between 4 and 30</span></span> |
| <span data-ttu-id="0ae4e-114">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="0ae4e-114">**networkSecurityGroup**</span></span> |<span data-ttu-id="0ae4e-115">NSG associated to the NIC</span><span class="sxs-lookup"><span data-stu-id="0ae4e-115">NSG associated to the NIC</span></span> |<span data-ttu-id="0ae4e-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span><span class="sxs-lookup"><span data-stu-id="0ae4e-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span></span> |
| <span data-ttu-id="0ae4e-117">**dnsSettings**</span><span class="sxs-lookup"><span data-stu-id="0ae4e-117">**dnsSettings**</span></span> |<span data-ttu-id="0ae4e-118">DNS settings for the NIC</span><span class="sxs-lookup"><span data-stu-id="0ae4e-118">DNS settings for the NIC</span></span> |<span data-ttu-id="0ae4e-119">see [PIP](#Public-IP-address)</span><span class="sxs-lookup"><span data-stu-id="0ae4e-119">see [PIP](#Public-IP-address)</span></span> |

<span data-ttu-id="0ae4e-120">A Network Interface Card, or NIC, represents a network interface that can be associated to a virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="0ae4e-120">A Network Interface Card, or NIC, represents a network interface that can be associated to a virtual machine (VM).</span></span> <span data-ttu-id="0ae4e-121">A VM can have one or more NICs.</span><span class="sxs-lookup"><span data-stu-id="0ae4e-121">A VM can have one or more NICs.</span></span>

![NIC's on a single VM](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a><span data-ttu-id="0ae4e-123">IP configurations</span><span class="sxs-lookup"><span data-stu-id="0ae4e-123">IP configurations</span></span>
<span data-ttu-id="0ae4e-124">NICs have a child object named **ipConfigurations** containing the following properties:</span><span class="sxs-lookup"><span data-stu-id="0ae4e-124">NICs have a child object named **ipConfigurations** containing the following properties:</span></span>

| <span data-ttu-id="0ae4e-125">Property</span><span class="sxs-lookup"><span data-stu-id="0ae4e-125">Property</span></span> | <span data-ttu-id="0ae4e-126">Description</span><span class="sxs-lookup"><span data-stu-id="0ae4e-126">Description</span></span> | <span data-ttu-id="0ae4e-127">Sample values</span><span class="sxs-lookup"><span data-stu-id="0ae4e-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ae4e-128">**subnet**</span><span class="sxs-lookup"><span data-stu-id="0ae4e-128">**subnet**</span></span> |<span data-ttu-id="0ae4e-129">Subnet the NIC is onnected to.</span><span class="sxs-lookup"><span data-stu-id="0ae4e-129">Subnet the NIC is onnected to.</span></span> |<span data-ttu-id="0ae4e-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span><span class="sxs-lookup"><span data-stu-id="0ae4e-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span></span> |
| <span data-ttu-id="0ae4e-131">**privateIPAddress**</span><span class="sxs-lookup"><span data-stu-id="0ae4e-131">**privateIPAddress**</span></span> |<span data-ttu-id="0ae4e-132">IP address for the NIC in the subnet</span><span class="sxs-lookup"><span data-stu-id="0ae4e-132">IP address for the NIC in the subnet</span></span> |<span data-ttu-id="0ae4e-133">10.0.0.8</span><span class="sxs-lookup"><span data-stu-id="0ae4e-133">10.0.0.8</span></span> |
| <span data-ttu-id="0ae4e-134">**privateIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="0ae4e-134">**privateIPAllocationMethod**</span></span> |<span data-ttu-id="0ae4e-135">IP allocation method</span><span class="sxs-lookup"><span data-stu-id="0ae4e-135">IP allocation method</span></span> |<span data-ttu-id="0ae4e-136">Dynamic or Static</span><span class="sxs-lookup"><span data-stu-id="0ae4e-136">Dynamic or Static</span></span> |
| <span data-ttu-id="0ae4e-137">**enableIPForwarding**</span><span class="sxs-lookup"><span data-stu-id="0ae4e-137">**enableIPForwarding**</span></span> |<span data-ttu-id="0ae4e-138">Whether the NIC can be used for routing</span><span class="sxs-lookup"><span data-stu-id="0ae4e-138">Whether the NIC can be used for routing</span></span> |<span data-ttu-id="0ae4e-139">true or false</span><span class="sxs-lookup"><span data-stu-id="0ae4e-139">true or false</span></span> |
| <span data-ttu-id="0ae4e-140">**primary**</span><span class="sxs-lookup"><span data-stu-id="0ae4e-140">**primary**</span></span> |<span data-ttu-id="0ae4e-141">Whether the NIC is the primary NIC for the VM</span><span class="sxs-lookup"><span data-stu-id="0ae4e-141">Whether the NIC is the primary NIC for the VM</span></span> |<span data-ttu-id="0ae4e-142">true or false</span><span class="sxs-lookup"><span data-stu-id="0ae4e-142">true or false</span></span> |
| <span data-ttu-id="0ae4e-143">**publicIPAddress**</span><span class="sxs-lookup"><span data-stu-id="0ae4e-143">**publicIPAddress**</span></span> |<span data-ttu-id="0ae4e-144">PIP associated with the NIC</span><span class="sxs-lookup"><span data-stu-id="0ae4e-144">PIP associated with the NIC</span></span> |<span data-ttu-id="0ae4e-145">see [DNS Settings](#DNS-settings)</span><span class="sxs-lookup"><span data-stu-id="0ae4e-145">see [DNS Settings](#DNS-settings)</span></span> |
| <span data-ttu-id="0ae4e-146">**loadBalancerBackendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="0ae4e-146">**loadBalancerBackendAddressPools**</span></span> |<span data-ttu-id="0ae4e-147">Back end address pools the NIC is associated with</span><span class="sxs-lookup"><span data-stu-id="0ae4e-147">Back end address pools the NIC is associated with</span></span> | |
| <span data-ttu-id="0ae4e-148">**loadBalancerInboundNatRules**</span><span class="sxs-lookup"><span data-stu-id="0ae4e-148">**loadBalancerInboundNatRules**</span></span> |<span data-ttu-id="0ae4e-149">Inbound load balancer NAT rules the NIC is associated with</span><span class="sxs-lookup"><span data-stu-id="0ae4e-149">Inbound load balancer NAT rules the NIC is associated with</span></span> | |

<span data-ttu-id="0ae4e-150">Sample public IP address in JSON format:</span><span class="sxs-lookup"><span data-stu-id="0ae4e-150">Sample public IP address in JSON format:</span></span>

    {
        "name": "lb-nic1-be",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkInterfaces",
        "location": "eastus",
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "ipConfigurations": [
                {
                    "name": "NIC-config",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/NIC-config",
                    "etag": "W/\"0027f1a2-3ac8-49de-b5d5-fd46550500b1\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "privateIPAddress": "10.0.0.4",
                        "privateIPAllocationMethod": "Dynamic",
                        "subnet": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet"
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1"
                            }
                        ]
                    }
                }
            ],
            "dnsSettings": { ... },
            "macAddress": "00-0D-3A-10-F1-29",
            "enableIPForwarding": false,
            "primary": true,
            "virtualMachine": {
                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Compute/virtualMachines/web1"
            }
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="0ae4e-151">Additional resources</span><span class="sxs-lookup"><span data-stu-id="0ae4e-151">Additional resources</span></span>
* <span data-ttu-id="0ae4e-152">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163579.aspx) for NICs.</span><span class="sxs-lookup"><span data-stu-id="0ae4e-152">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163579.aspx) for NICs.</span></span>


