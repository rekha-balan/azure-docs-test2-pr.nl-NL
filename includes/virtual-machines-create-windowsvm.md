1. <span data-ttu-id="90cf5-101">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="90cf5-101">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="90cf5-102">Starting in the upper left, click **New > Compute > Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="90cf5-102">Starting in the upper left, click **New > Compute > Windows Server 2016 Datacenter**.</span></span>

    ![Navigate to the Azure VM images in the portal](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. <span data-ttu-id="90cf5-104">On the Windows Server 2016 Datacenter, select the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="90cf5-104">On the Windows Server 2016 Datacenter, select the Classic deployment model.</span></span> <span data-ttu-id="90cf5-105">Click Create.</span><span class="sxs-lookup"><span data-stu-id="90cf5-105">Click Create.</span></span>

    ![Screenshot that shows the Azure VM images available in the portal](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a><span data-ttu-id="90cf5-107">1. Basics blade</span><span class="sxs-lookup"><span data-stu-id="90cf5-107">1. Basics blade</span></span>

<span data-ttu-id="90cf5-108">The Basics blade requests administrative information for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="90cf5-108">The Basics blade requests administrative information for the virtual machine.</span></span>

1. <span data-ttu-id="90cf5-109">Enter a **Name** for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="90cf5-109">Enter a **Name** for the virtual machine.</span></span> <span data-ttu-id="90cf5-110">In the example, _HeroVM_ is the name of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="90cf5-110">In the example, _HeroVM_ is the name of the virtual machine.</span></span> <span data-ttu-id="90cf5-111">The name must be 1-15 characters long and it cannot contain special characters.</span><span class="sxs-lookup"><span data-stu-id="90cf5-111">The name must be 1-15 characters long and it cannot contain special characters.</span></span>

2. <span data-ttu-id="90cf5-112">Enter a **User name** and a strong **Password** that are used to create a local account on the VM.</span><span class="sxs-lookup"><span data-stu-id="90cf5-112">Enter a **User name** and a strong **Password** that are used to create a local account on the VM.</span></span> <span data-ttu-id="90cf5-113">The local account is used to sign in to and manage the VM.</span><span class="sxs-lookup"><span data-stu-id="90cf5-113">The local account is used to sign in to and manage the VM.</span></span> <span data-ttu-id="90cf5-114">In the example, _azureuser_ is the user name.</span><span class="sxs-lookup"><span data-stu-id="90cf5-114">In the example, _azureuser_ is the user name.</span></span>

 <span data-ttu-id="90cf5-115">The password must be 8-123 characters long and meet three out of the four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span><span class="sxs-lookup"><span data-stu-id="90cf5-115">The password must be 8-123 characters long and meet three out of the four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="90cf5-116">See more about [username and password requirements](../articles/virtual-machines/windows/faq.md).</span><span class="sxs-lookup"><span data-stu-id="90cf5-116">See more about [username and password requirements](../articles/virtual-machines/windows/faq.md).</span></span>

3. <span data-ttu-id="90cf5-117">The **Subscription** is optional.</span><span class="sxs-lookup"><span data-stu-id="90cf5-117">The **Subscription** is optional.</span></span> <span data-ttu-id="90cf5-118">One common setting is "Pay-As-You-Go".</span><span class="sxs-lookup"><span data-stu-id="90cf5-118">One common setting is "Pay-As-You-Go".</span></span>

4. <span data-ttu-id="90cf5-119">Select an existing **Resource group** or type the name for a new one.</span><span class="sxs-lookup"><span data-stu-id="90cf5-119">Select an existing **Resource group** or type the name for a new one.</span></span> <span data-ttu-id="90cf5-120">In the example, _HeroVMRG_ is the name of the resource group.</span><span class="sxs-lookup"><span data-stu-id="90cf5-120">In the example, _HeroVMRG_ is the name of the resource group.</span></span>

5. <span data-ttu-id="90cf5-121">Select an Azure datacenter **Location** where you want the VM to run.</span><span class="sxs-lookup"><span data-stu-id="90cf5-121">Select an Azure datacenter **Location** where you want the VM to run.</span></span> <span data-ttu-id="90cf5-122">In the example, **East US** is the location.</span><span class="sxs-lookup"><span data-stu-id="90cf5-122">In the example, **East US** is the location.</span></span>

6. <span data-ttu-id="90cf5-123">When you are done, click **Next** to continue to the next blade.</span><span class="sxs-lookup"><span data-stu-id="90cf5-123">When you are done, click **Next** to continue to the next blade.</span></span>

    ![Screenshot that shows the settings on the Basics blade for configuring an Azure VM](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a><span data-ttu-id="90cf5-125">2. Size blade</span><span class="sxs-lookup"><span data-stu-id="90cf5-125">2. Size blade</span></span>

<span data-ttu-id="90cf5-126">The Size blade identifies the configuration details of the VM, and lists various choices that include OS, number of processors, disk storage type, and estimated monthly usage costs.</span><span class="sxs-lookup"><span data-stu-id="90cf5-126">The Size blade identifies the configuration details of the VM, and lists various choices that include OS, number of processors, disk storage type, and estimated monthly usage costs.</span></span>  

<span data-ttu-id="90cf5-127">Choose a VM size, and then click **Select** to continue.</span><span class="sxs-lookup"><span data-stu-id="90cf5-127">Choose a VM size, and then click **Select** to continue.</span></span> <span data-ttu-id="90cf5-128">In this example, _DS1_\__V2 Standard_ is the VM size.</span><span class="sxs-lookup"><span data-stu-id="90cf5-128">In this example, _DS1_\__V2 Standard_ is the VM size.</span></span>

  ![Screenshot of the Size blade that shows the Azure VM sizes that you can select](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a><span data-ttu-id="90cf5-130">3. Settings blade</span><span class="sxs-lookup"><span data-stu-id="90cf5-130">3. Settings blade</span></span>

<span data-ttu-id="90cf5-131">The Settings blade requests storage and network options.</span><span class="sxs-lookup"><span data-stu-id="90cf5-131">The Settings blade requests storage and network options.</span></span> <span data-ttu-id="90cf5-132">You can accept the default settings.</span><span class="sxs-lookup"><span data-stu-id="90cf5-132">You can accept the default settings.</span></span> <span data-ttu-id="90cf5-133">Azure creates appropriate entries where necessary.</span><span class="sxs-lookup"><span data-stu-id="90cf5-133">Azure creates appropriate entries where necessary.</span></span>

<span data-ttu-id="90cf5-134">If you selected a virtual machine size that supports it, you can try Azure Premium Storage by selecting Premium (SSD) in Disk type.</span><span class="sxs-lookup"><span data-stu-id="90cf5-134">If you selected a virtual machine size that supports it, you can try Azure Premium Storage by selecting Premium (SSD) in Disk type.</span></span>

<span data-ttu-id="90cf5-135">When you're done making changes, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="90cf5-135">When you're done making changes, click **OK**.</span></span>

## <a name="4-summary-blade"></a><span data-ttu-id="90cf5-136">4. Summary blade</span><span class="sxs-lookup"><span data-stu-id="90cf5-136">4. Summary blade</span></span>

<span data-ttu-id="90cf5-137">The Summary blade lists the settings specified in the previous blades.</span><span class="sxs-lookup"><span data-stu-id="90cf5-137">The Summary blade lists the settings specified in the previous blades.</span></span> <span data-ttu-id="90cf5-138">Click **OK** when you're ready to make the image.</span><span class="sxs-lookup"><span data-stu-id="90cf5-138">Click **OK** when you're ready to make the image.</span></span>

 ![Summary blade report giving specified settings of the virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

<span data-ttu-id="90cf5-140">After the virtual machine is created, the portal lists the new virtual machine under **All resources**, and displays a tile of the virtual machine on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="90cf5-140">After the virtual machine is created, the portal lists the new virtual machine under **All resources**, and displays a tile of the virtual machine on the dashboard.</span></span> <span data-ttu-id="90cf5-141">The corresponding cloud service and storage account also are created and listed.</span><span class="sxs-lookup"><span data-stu-id="90cf5-141">The corresponding cloud service and storage account also are created and listed.</span></span> <span data-ttu-id="90cf5-142">Both the virtual machine and cloud service are started automatically and their status is listed as **Running**.</span><span class="sxs-lookup"><span data-stu-id="90cf5-142">Both the virtual machine and cloud service are started automatically and their status is listed as **Running**.</span></span>

 ![Configure VM Agent and the endpoints of the virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)






