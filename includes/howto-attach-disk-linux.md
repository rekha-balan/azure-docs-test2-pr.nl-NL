
<span data-ttu-id="7315e-101">For more information about disks, see [About Disks and VHDs for Virtual Machines](../articles/storage/storage-about-disks-and-vhds-linux.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7315e-101">For more information about disks, see [About Disks and VHDs for Virtual Machines](../articles/storage/storage-about-disks-and-vhds-linux.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a><span data-ttu-id="7315e-102">Attach an empty disk</span><span class="sxs-lookup"><span data-stu-id="7315e-102">Attach an empty disk</span></span>
1. <span data-ttu-id="7315e-103">Open Azure CLI 1.0 and [connect to your Azure subscription](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="7315e-103">Open Azure CLI 1.0 and [connect to your Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="7315e-104">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="7315e-104">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="7315e-105">Enter `azure vm disk attach-new` to create and attach a new disk as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="7315e-105">Enter `azure vm disk attach-new` to create and attach a new disk as shown in the following example.</span></span> <span data-ttu-id="7315e-106">Replace *myVM* with the name of your Linux Virtual Machine and specify the size of the disk in GB, which is *100GB* in this example:</span><span class="sxs-lookup"><span data-stu-id="7315e-106">Replace *myVM* with the name of your Linux Virtual Machine and specify the size of the disk in GB, which is *100GB* in this example:</span></span>

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. <span data-ttu-id="7315e-107">After the data disk is created and attached, it's listed in the output of `azure vm disk list <virtual-machine-name>` as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="7315e-107">After the data disk is created and attached, it's listed in the output of `azure vm disk list <virtual-machine-name>` as shown in the following example:</span></span>
   
    ```azurecli
    azure vm disk list TestVM
    ```

    <span data-ttu-id="7315e-108">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="7315e-108">The output is similar to the following example:</span></span>

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a><span data-ttu-id="7315e-109">Attach an existing disk</span><span class="sxs-lookup"><span data-stu-id="7315e-109">Attach an existing disk</span></span>
<span data-ttu-id="7315e-110">Attaching an existing disk requires that you have a .vhd available in a storage account.</span><span class="sxs-lookup"><span data-stu-id="7315e-110">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span>

1. <span data-ttu-id="7315e-111">Open Azure CLI 1.0 and [connect to your Azure subscription](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="7315e-111">Open Azure CLI 1.0 and [connect to your Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="7315e-112">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="7315e-112">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="7315e-113">Check if the VHD you want to attach is already uploaded to your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="7315e-113">Check if the VHD you want to attach is already uploaded to your Azure subscription:</span></span>
   
    ```azurecli
    azure vm disk list
    ```

    <span data-ttu-id="7315e-114">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="7315e-114">The output is similar to the following example:</span></span>

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. <span data-ttu-id="7315e-115">If you don't find the disk that you want to use, you may upload a local VHD to your subscription by using `azure vm disk create` or `azure vm disk upload`.</span><span class="sxs-lookup"><span data-stu-id="7315e-115">If you don't find the disk that you want to use, you may upload a local VHD to your subscription by using `azure vm disk create` or `azure vm disk upload`.</span></span> <span data-ttu-id="7315e-116">An example of `disk create` would be as in the following example:</span><span class="sxs-lookup"><span data-stu-id="7315e-116">An example of `disk create` would be as in the following example:</span></span>
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    <span data-ttu-id="7315e-117">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="7315e-117">The output is similar to the following example:</span></span>

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   <span data-ttu-id="7315e-118">You may also use `azure vm disk upload` to upload a VHD to a specific storage account.</span><span class="sxs-lookup"><span data-stu-id="7315e-118">You may also use `azure vm disk upload` to upload a VHD to a specific storage account.</span></span> <span data-ttu-id="7315e-119">Read more about the commands to manage your Azure virtual machine data disks [over here](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="7315e-119">Read more about the commands to manage your Azure virtual machine data disks [over here](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

4. <span data-ttu-id="7315e-120">Now you attach the desired VHD to your virtual machine:</span><span class="sxs-lookup"><span data-stu-id="7315e-120">Now you attach the desired VHD to your virtual machine:</span></span>
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   <span data-ttu-id="7315e-121">Make sure to replace *myVM* with the name of your virtual machine, and *myVHD* with your desired VHD.</span><span class="sxs-lookup"><span data-stu-id="7315e-121">Make sure to replace *myVM* with the name of your virtual machine, and *myVHD* with your desired VHD.</span></span>

5. <span data-ttu-id="7315e-122">You can verify the disk is attached to the virtual machine with `azure vm disk list <virtual-machine-name>`:</span><span class="sxs-lookup"><span data-stu-id="7315e-122">You can verify the disk is attached to the virtual machine with `azure vm disk list <virtual-machine-name>`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="7315e-123">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="7315e-123">The output is similar to the following example:</span></span>

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> <span data-ttu-id="7315e-124">After you add a data disk, you'll need to log on to the virtual machine and initialize the disk so the virtual machine can use the disk for storage (see the following steps for more information on how to do initialize the disk).</span><span class="sxs-lookup"><span data-stu-id="7315e-124">After you add a data disk, you'll need to log on to the virtual machine and initialize the disk so the virtual machine can use the disk for storage (see the following steps for more information on how to do initialize the disk).</span></span>
> 
> 

