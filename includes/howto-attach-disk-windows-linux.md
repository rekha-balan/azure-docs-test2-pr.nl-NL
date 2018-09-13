


## <a name="attach-an-empty-disk"></a><span data-ttu-id="aa7f2-101">Attach an empty disk</span><span class="sxs-lookup"><span data-stu-id="aa7f2-101">Attach an empty disk</span></span>
<span data-ttu-id="aa7f2-102">Attaching an empty disk is a simple way to add a data disk, because Azure creates the .vhd file for you and stores it in the storage account.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-102">Attaching an empty disk is a simple way to add a data disk, because Azure creates the .vhd file for you and stores it in the storage account.</span></span>

1. <span data-ttu-id="aa7f2-103">Click **Virtual Machines (classic)**, and then select the appropriate VM.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-103">Click **Virtual Machines (classic)**, and then select the appropriate VM.</span></span>

2. <span data-ttu-id="aa7f2-104">In the Settings menu, click **Disks**.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-104">In the Settings menu, click **Disks**.</span></span>

   ![Attach a new empty disk](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. <span data-ttu-id="aa7f2-106">On the command bar, click **Attach new**.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-106">On the command bar, click **Attach new**.</span></span>  
    <span data-ttu-id="aa7f2-107">The **Attach new disk** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-107">The **Attach new disk** dialog box appears.</span></span>

    ![Attach a new disk](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/howto-attach-disk-windows-linux/newdiskdetail.png)

    <span data-ttu-id="aa7f2-109">Fill in the following information:</span><span class="sxs-lookup"><span data-stu-id="aa7f2-109">Fill in the following information:</span></span>
    - <span data-ttu-id="aa7f2-110">In **File Name**, accept the default name or type another one for the .vhd file.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-110">In **File Name**, accept the default name or type another one for the .vhd file.</span></span> <span data-ttu-id="aa7f2-111">The data disk uses an automatically generated name, even if you type another name for the .vhd file.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-111">The data disk uses an automatically generated name, even if you type another name for the .vhd file.</span></span>
    - <span data-ttu-id="aa7f2-112">Select the **Type** of the data disk.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-112">Select the **Type** of the data disk.</span></span> <span data-ttu-id="aa7f2-113">All virtual machines support standard disks.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-113">All virtual machines support standard disks.</span></span> <span data-ttu-id="aa7f2-114">Many virtual machines also support premium disks.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-114">Many virtual machines also support premium disks.</span></span>
    - <span data-ttu-id="aa7f2-115">Select the **Size (GB)** of the data disk.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-115">Select the **Size (GB)** of the data disk.</span></span>
    - <span data-ttu-id="aa7f2-116">For **Host caching**, choose none or Read Only.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-116">For **Host caching**, choose none or Read Only.</span></span>
    - <span data-ttu-id="aa7f2-117">Click OK to finish.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-117">Click OK to finish.</span></span>

4. <span data-ttu-id="aa7f2-118">After the data disk is created and attached, it's listed in the disks section of the VM.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-118">After the data disk is created and attached, it's listed in the disks section of the VM.</span></span>

   ![New and empty data disk successfully attached](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> <span data-ttu-id="aa7f2-120">After you add a data disk, you need to log on to the VM and initialize the disk so that it can be used.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-120">After you add a data disk, you need to log on to the VM and initialize the disk so that it can be used.</span></span>

## <a name="how-to-attach-an-existing-disk"></a><span data-ttu-id="aa7f2-121">How to: Attach an existing disk</span><span class="sxs-lookup"><span data-stu-id="aa7f2-121">How to: Attach an existing disk</span></span>
<span data-ttu-id="aa7f2-122">Attaching an existing disk requires that you have a .vhd available in a storage account.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-122">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span> <span data-ttu-id="aa7f2-123">Use the [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet to upload the .vhd file to the storage account.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-123">Use the [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet to upload the .vhd file to the storage account.</span></span> <span data-ttu-id="aa7f2-124">After you've created and uploaded the .vhd file, you can attach it to a VM.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-124">After you've created and uploaded the .vhd file, you can attach it to a VM.</span></span>

1. <span data-ttu-id="aa7f2-125">Click **Virtual Machines (classic)**, and then select the appropriate virtual machine.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-125">Click **Virtual Machines (classic)**, and then select the appropriate virtual machine.</span></span>

2. <span data-ttu-id="aa7f2-126">In the Settings menu, click **Disks**.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-126">In the Settings menu, click **Disks**.</span></span>

3. <span data-ttu-id="aa7f2-127">On the command bar, click **Attach existing**.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-127">On the command bar, click **Attach existing**.</span></span>

    ![Attach data disk](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. <span data-ttu-id="aa7f2-129">Click **Location**.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-129">Click **Location**.</span></span> <span data-ttu-id="aa7f2-130">The available storage accounts display.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-130">The available storage accounts display.</span></span> <span data-ttu-id="aa7f2-131">Next, select an appropriate storage account from those listed.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-131">Next, select an appropriate storage account from those listed.</span></span>

    ![Provide disk storage account](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. <span data-ttu-id="aa7f2-133">A **Storage account** holds one or more containers that contain disk drives (vhds).</span><span class="sxs-lookup"><span data-stu-id="aa7f2-133">A **Storage account** holds one or more containers that contain disk drives (vhds).</span></span> <span data-ttu-id="aa7f2-134">Select the appropriate container from those listed.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-134">Select the appropriate container from those listed.</span></span>

    ![Provide container of virtual-machines-windows](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. <span data-ttu-id="aa7f2-136">The **vhds** panel lists the disk drives held in the container.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-136">The **vhds** panel lists the disk drives held in the container.</span></span> <span data-ttu-id="aa7f2-137">Click one of the disks, and then click Select.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-137">Click one of the disks, and then click Select.</span></span>

    ![Provide disk image for virtual-machines-windows](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. <span data-ttu-id="aa7f2-139">The **Attach existing disk** panel displays again, with the location containing the storage account, container, and selected hard disk (vhd) to add to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-139">The **Attach existing disk** panel displays again, with the location containing the storage account, container, and selected hard disk (vhd) to add to the virtual machine.</span></span>

  <span data-ttu-id="aa7f2-140">Set **Host caching** to none or Read only, then click OK.</span><span class="sxs-lookup"><span data-stu-id="aa7f2-140">Set **Host caching** to none or Read only, then click OK.</span></span>

    ![Data disk successfully attached](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)








