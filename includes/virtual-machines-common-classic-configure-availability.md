


<span data-ttu-id="c798c-101">An availability set helps keep your virtual machines available during downtime, such as during maintenance.</span><span class="sxs-lookup"><span data-stu-id="c798c-101">An availability set helps keep your virtual machines available during downtime, such as during maintenance.</span></span> <span data-ttu-id="c798c-102">Placing two or more similarly configured virtual machines in an availability set creates the redundancy needed to maintain availability of the applications or services that your virtual machine runs.</span><span class="sxs-lookup"><span data-stu-id="c798c-102">Placing two or more similarly configured virtual machines in an availability set creates the redundancy needed to maintain availability of the applications or services that your virtual machine runs.</span></span> <span data-ttu-id="c798c-103">For details about how this works, see [Manage the availability of virtual machines][Manage the availability of virtual machines].</span><span class="sxs-lookup"><span data-stu-id="c798c-103">For details about how this works, see [Manage the availability of virtual machines][Manage the availability of virtual machines].</span></span>

<span data-ttu-id="c798c-104">It's a best practice to use both availability sets and load-balancing endpoints to help ensure that your application is always available and running efficiently.</span><span class="sxs-lookup"><span data-stu-id="c798c-104">It's a best practice to use both availability sets and load-balancing endpoints to help ensure that your application is always available and running efficiently.</span></span> <span data-ttu-id="c798c-105">For details about load-balanced endpoints, see [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services].</span><span class="sxs-lookup"><span data-stu-id="c798c-105">For details about load-balanced endpoints, see [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services].</span></span>

<span data-ttu-id="c798c-106">You can add classic virtual machines into an availability set by using one of two options:</span><span class="sxs-lookup"><span data-stu-id="c798c-106">You can add classic virtual machines into an availability set by using one of two options:</span></span>

* <span data-ttu-id="c798c-107">[Option 1: Create a virtual machine and an availability set at the same time][Option 1: Create a virtual machine and an availability set at the same time].</span><span class="sxs-lookup"><span data-stu-id="c798c-107">[Option 1: Create a virtual machine and an availability set at the same time][Option 1: Create a virtual machine and an availability set at the same time].</span></span> <span data-ttu-id="c798c-108">Then, add new virtual machines to the set when you create those virtual machines.</span><span class="sxs-lookup"><span data-stu-id="c798c-108">Then, add new virtual machines to the set when you create those virtual machines.</span></span>
* <span data-ttu-id="c798c-109">[Option 2: Add an existing virtual machine to an availability set][Option 2: Add an existing virtual machine to an availability set].</span><span class="sxs-lookup"><span data-stu-id="c798c-109">[Option 2: Add an existing virtual machine to an availability set][Option 2: Add an existing virtual machine to an availability set].</span></span>

> [!NOTE]
> <span data-ttu-id="c798c-110">In the classic model, virtual machines that you want to put in the same availability set must belong to the same cloud service.</span><span class="sxs-lookup"><span data-stu-id="c798c-110">In the classic model, virtual machines that you want to put in the same availability set must belong to the same cloud service.</span></span>
> 
> 

## <span data-ttu-id="c798c-111"><a id="createset"> </a>Option 1: Create a virtual machine and an availability set at the same time</span><span class="sxs-lookup"><span data-stu-id="c798c-111"><a id="createset"> </a>Option 1: Create a virtual machine and an availability set at the same time</span></span>
<span data-ttu-id="c798c-112">You can use either the Azure portal or Azure PowerShell commands to do this.</span><span class="sxs-lookup"><span data-stu-id="c798c-112">You can use either the Azure portal or Azure PowerShell commands to do this.</span></span>

<span data-ttu-id="c798c-113">To use the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="c798c-113">To use the Azure portal:</span></span>

1. <span data-ttu-id="c798c-114">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c798c-114">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c798c-115">On the hub menu, click **+ New**, and then click **Virtual Machine**.</span><span class="sxs-lookup"><span data-stu-id="c798c-115">On the hub menu, click **+ New**, and then click **Virtual Machine**.</span></span>
   
    ![Alt image text](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. <span data-ttu-id="c798c-117">Select the Marketplace virtual machine image you wish to use.</span><span class="sxs-lookup"><span data-stu-id="c798c-117">Select the Marketplace virtual machine image you wish to use.</span></span> <span data-ttu-id="c798c-118">You can choose to create a Linux or Windows virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c798c-118">You can choose to create a Linux or Windows virtual machine.</span></span>
4. <span data-ttu-id="c798c-119">For the selected virtual machine, verify that the deployment model is set to **Classic** and then click **Create**</span><span class="sxs-lookup"><span data-stu-id="c798c-119">For the selected virtual machine, verify that the deployment model is set to **Classic** and then click **Create**</span></span>
   
    ![Alt image text](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. <span data-ttu-id="c798c-121">Enter a virtual machine name, user name and password (for Windows machines) or SSH public key (for Linux machines).</span><span class="sxs-lookup"><span data-stu-id="c798c-121">Enter a virtual machine name, user name and password (for Windows machines) or SSH public key (for Linux machines).</span></span> 
6. <span data-ttu-id="c798c-122">Choose the VM size and then click **Select** to continue.</span><span class="sxs-lookup"><span data-stu-id="c798c-122">Choose the VM size and then click **Select** to continue.</span></span>
7. <span data-ttu-id="c798c-123">Choose **Optional Configuration > Availability set**, and select the availability set you wish to add the virtual machine to.</span><span class="sxs-lookup"><span data-stu-id="c798c-123">Choose **Optional Configuration > Availability set**, and select the availability set you wish to add the virtual machine to.</span></span>
   
    ![Alt image text](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. <span data-ttu-id="c798c-125">Review your configuration settings.</span><span class="sxs-lookup"><span data-stu-id="c798c-125">Review your configuration settings.</span></span> <span data-ttu-id="c798c-126">When you're done, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c798c-126">When you're done, click **Create**.</span></span>
9. <span data-ttu-id="c798c-127">While Azure creates your virtual machine, you can track the progress under **Virtual Machines** in the hub menu.</span><span class="sxs-lookup"><span data-stu-id="c798c-127">While Azure creates your virtual machine, you can track the progress under **Virtual Machines** in the hub menu.</span></span>

<span data-ttu-id="c798c-128">To use Azure PowerShell commands to create an Azure virtual machine and add it to a new or existing availability set, see [Use Azure PowerShell to create and preconfigure Windows-based virtual machines](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c798c-128">To use Azure PowerShell commands to create an Azure virtual machine and add it to a new or existing availability set, see [Use Azure PowerShell to create and preconfigure Windows-based virtual machines](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="c798c-129"><a id="addmachine"> </a>Option 2: Add an existing virtual machine to an availability set</span><span class="sxs-lookup"><span data-stu-id="c798c-129"><a id="addmachine"> </a>Option 2: Add an existing virtual machine to an availability set</span></span>
<span data-ttu-id="c798c-130">In the Azure portal, you can add existing classic virtual machines to an existing availability set or create a new one for them.</span><span class="sxs-lookup"><span data-stu-id="c798c-130">In the Azure portal, you can add existing classic virtual machines to an existing availability set or create a new one for them.</span></span> <span data-ttu-id="c798c-131">(Keep in mind that the virtual machines in the same availability set must belong to the same cloud service.) The steps are almost the same.</span><span class="sxs-lookup"><span data-stu-id="c798c-131">(Keep in mind that the virtual machines in the same availability set must belong to the same cloud service.) The steps are almost the same.</span></span> <span data-ttu-id="c798c-132">With Azure PowerShell, you can add the virtual machine to an existing availability set.</span><span class="sxs-lookup"><span data-stu-id="c798c-132">With Azure PowerShell, you can add the virtual machine to an existing availability set.</span></span>

1. <span data-ttu-id="c798c-133">If you have not already done so, sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c798c-133">If you have not already done so, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c798c-134">On the Hub menu, click **Virtual Machines (classic)**.</span><span class="sxs-lookup"><span data-stu-id="c798c-134">On the Hub menu, click **Virtual Machines (classic)**.</span></span>
   
    ![Alt image text](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. <span data-ttu-id="c798c-136">From the list of virtual machines, select the name of the virtual machine that you want to add to the set.</span><span class="sxs-lookup"><span data-stu-id="c798c-136">From the list of virtual machines, select the name of the virtual machine that you want to add to the set.</span></span>
4. <span data-ttu-id="c798c-137">Choose **Availability set** from the virtual machine **Settings**.</span><span class="sxs-lookup"><span data-stu-id="c798c-137">Choose **Availability set** from the virtual machine **Settings**.</span></span>
   
    ![Alt image text](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. <span data-ttu-id="c798c-139">Select the availability set you wish to add the virtual machine to.</span><span class="sxs-lookup"><span data-stu-id="c798c-139">Select the availability set you wish to add the virtual machine to.</span></span> <span data-ttu-id="c798c-140">The virtual machine must belong to the same cloud service as the availability set.</span><span class="sxs-lookup"><span data-stu-id="c798c-140">The virtual machine must belong to the same cloud service as the availability set.</span></span>
   
    ![Alt image text](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. <span data-ttu-id="c798c-142">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c798c-142">Click **Save**.</span></span>

<span data-ttu-id="c798c-143">To use Azure PowerShell commands, open an administrator-level Azure PowerShell session and run the following command.</span><span class="sxs-lookup"><span data-stu-id="c798c-143">To use Azure PowerShell commands, open an administrator-level Azure PowerShell session and run the following command.</span></span> <span data-ttu-id="c798c-144">For the placeholders (such as &lt;VmCloudServiceName&gt;), replace everything within the quotes, including the < and > characters, with the correct names.</span><span class="sxs-lookup"><span data-stu-id="c798c-144">For the placeholders (such as &lt;VmCloudServiceName&gt;), replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> <span data-ttu-id="c798c-145">The virtual machine might have to be restarted to finish adding it to the availability set.</span><span class="sxs-lookup"><span data-stu-id="c798c-145">The virtual machine might have to be restarted to finish adding it to the availability set.</span></span>
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at the same time]: #createset
[Option 2: Add an existing virtual machine to an availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage the availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md







