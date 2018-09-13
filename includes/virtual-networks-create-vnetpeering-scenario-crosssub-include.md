## <a name="x-sub"></a><span data-ttu-id="0d443-101">Peering across subscriptions</span><span class="sxs-lookup"><span data-stu-id="0d443-101">Peering across subscriptions</span></span>
<span data-ttu-id="0d443-102">In this scenario you will create a peering between two VNets that exist in different subscriptions.</span><span class="sxs-lookup"><span data-stu-id="0d443-102">In this scenario you will create a peering between two VNets that exist in different subscriptions.</span></span>

![cross sub scenario](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-networks-create-vnetpeering-scenario-crosssub-include/figure01.PNG)

<span data-ttu-id="0d443-104">VNet peering relies on role-based access control (RBAC) for authorization.</span><span class="sxs-lookup"><span data-stu-id="0d443-104">VNet peering relies on role-based access control (RBAC) for authorization.</span></span> <span data-ttu-id="0d443-105">For cross-subscriptions scenario, you first need to grant sufficient permission to users who will create the peering link.</span><span class="sxs-lookup"><span data-stu-id="0d443-105">For cross-subscriptions scenario, you first need to grant sufficient permission to users who will create the peering link.</span></span>

> [!NOTE]
> <span data-ttu-id="0d443-106">If the same user has the privilege over both subscriptions, then you can skip steps 1-4 that follow.</span><span class="sxs-lookup"><span data-stu-id="0d443-106">If the same user has the privilege over both subscriptions, then you can skip steps 1-4 that follow.</span></span>
> 
> 


