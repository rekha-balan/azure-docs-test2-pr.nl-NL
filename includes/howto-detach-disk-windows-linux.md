<span data-ttu-id="7e59c-101">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span><span class="sxs-lookup"><span data-stu-id="7e59c-101">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="7e59c-102">Detaching a disk removes the disk from the virtual machine, but doesn't delete the disk from the Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="7e59c-102">Detaching a disk removes the disk from the virtual machine, but doesn't delete the disk from the Azure storage account.</span></span>

<span data-ttu-id="7e59c-103">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span><span class="sxs-lookup"><span data-stu-id="7e59c-103">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="7e59c-104">To detach an operating system disk, you first need to delete the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="7e59c-104">To detach an operating system disk, you first need to delete the virtual machine.</span></span>
>

## <a name="find-the-disk"></a><span data-ttu-id="7e59c-105">Find the disk</span><span class="sxs-lookup"><span data-stu-id="7e59c-105">Find the disk</span></span>
<span data-ttu-id="7e59c-106">If you don't know the name of the disk or want to verify it before you detach it, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="7e59c-106">If you don't know the name of the disk or want to verify it before you detach it, follow these steps.</span></span>

1. <span data-ttu-id="7e59c-107">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7e59c-107">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="7e59c-108">Click **Virtual Machines**, and then select the appropriate VM.</span><span class="sxs-lookup"><span data-stu-id="7e59c-108">Click **Virtual Machines**, and then select the appropriate VM.</span></span>

3. <span data-ttu-id="7e59c-109">Click **Disks** along the left edge of the virtual machine dashboard, under **Settings**.</span><span class="sxs-lookup"><span data-stu-id="7e59c-109">Click **Disks** along the left edge of the virtual machine dashboard, under **Settings**.</span></span>

 <span data-ttu-id="7e59c-110">The virtual machine dashboard lists the name and type of all attached disks.</span><span class="sxs-lookup"><span data-stu-id="7e59c-110">The virtual machine dashboard lists the name and type of all attached disks.</span></span> <span data-ttu-id="7e59c-111">For example, this screen shows a virtual machine with one operating system (OS) disk and one data disk:</span><span class="sxs-lookup"><span data-stu-id="7e59c-111">For example, this screen shows a virtual machine with one operating system (OS) disk and one data disk:</span></span>

    ![Find data disk](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-the-disk"></a><span data-ttu-id="7e59c-113">Detach the disk</span><span class="sxs-lookup"><span data-stu-id="7e59c-113">Detach the disk</span></span>
1. <span data-ttu-id="7e59c-114">From the Azure portal, click **Virtual Machines**, and then click the name of the virtual machine that has the data disk you want to detach.</span><span class="sxs-lookup"><span data-stu-id="7e59c-114">From the Azure portal, click **Virtual Machines**, and then click the name of the virtual machine that has the data disk you want to detach.</span></span>

2. <span data-ttu-id="7e59c-115">Click **Disks** along the left edge of the virtual machine dashboard, under **Settings**.</span><span class="sxs-lookup"><span data-stu-id="7e59c-115">Click **Disks** along the left edge of the virtual machine dashboard, under **Settings**.</span></span>

3. <span data-ttu-id="7e59c-116">Click the disk you want to detach.</span><span class="sxs-lookup"><span data-stu-id="7e59c-116">Click the disk you want to detach.</span></span>

  ![Identify the disk to detach](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/howto-detach-disk-windows-linux/DiskList.png)

4. <span data-ttu-id="7e59c-118">From the command bar, click **Detach**.</span><span class="sxs-lookup"><span data-stu-id="7e59c-118">From the command bar, click **Detach**.</span></span>

  ![Locate the detach command](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. <span data-ttu-id="7e59c-120">In the confirmation window, click **Yes** to detach the disk.</span><span class="sxs-lookup"><span data-stu-id="7e59c-120">In the confirmation window, click **Yes** to detach the disk.</span></span>

  ![Confirm detaching the disk](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/howto-detach-disk-windows-linux/confirmdetach.png)

<span data-ttu-id="7e59c-122">The disk remains in storage but is no longer attached to a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="7e59c-122">The disk remains in storage but is no longer attached to a virtual machine.</span></span>




