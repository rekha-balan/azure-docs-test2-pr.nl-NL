<span data-ttu-id="16aab-101">When you no longer need a data disk that's attached to a virtual machine (VM), you can easily detach it.</span><span class="sxs-lookup"><span data-stu-id="16aab-101">When you no longer need a data disk that's attached to a virtual machine (VM), you can easily detach it.</span></span> <span data-ttu-id="16aab-102">When you detach a disk from the VM, the disk is not removed it from storage.</span><span class="sxs-lookup"><span data-stu-id="16aab-102">When you detach a disk from the VM, the disk is not removed it from storage.</span></span> <span data-ttu-id="16aab-103">If you want to use the existing data on the disk again, you can reattach it to the same VM, or another one.</span><span class="sxs-lookup"><span data-stu-id="16aab-103">If you want to use the existing data on the disk again, you can reattach it to the same VM, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="16aab-104">A VM in Azure uses different types of disks - an operating system disk, a local temporary disk, and optional data disks.</span><span class="sxs-lookup"><span data-stu-id="16aab-104">A VM in Azure uses different types of disks - an operating system disk, a local temporary disk, and optional data disks.</span></span> <span data-ttu-id="16aab-105">For details, see [About Disks and VHDs for Virtual Machines](../articles/storage/storage-about-disks-and-vhds-linux.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="16aab-105">For details, see [About Disks and VHDs for Virtual Machines](../articles/storage/storage-about-disks-and-vhds-linux.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="16aab-106">You cannot detach an operating system disk unless you also delete the VM.</span><span class="sxs-lookup"><span data-stu-id="16aab-106">You cannot detach an operating system disk unless you also delete the VM.</span></span>

## <a name="find-the-disk"></a><span data-ttu-id="16aab-107">Find the disk</span><span class="sxs-lookup"><span data-stu-id="16aab-107">Find the disk</span></span>
<span data-ttu-id="16aab-108">Before you can detach a disk from a VM you need to find out the LUN number, which is an identifier for the disk to be detached.</span><span class="sxs-lookup"><span data-stu-id="16aab-108">Before you can detach a disk from a VM you need to find out the LUN number, which is an identifier for the disk to be detached.</span></span> <span data-ttu-id="16aab-109">To do that, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="16aab-109">To do that, follow these steps:</span></span>

1. <span data-ttu-id="16aab-110">Open Azure CLI and [connect to your Azure subscription](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="16aab-110">Open Azure CLI and [connect to your Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="16aab-111">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="16aab-111">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="16aab-112">Find out which disks are attached to your VM.</span><span class="sxs-lookup"><span data-stu-id="16aab-112">Find out which disks are attached to your VM.</span></span> <span data-ttu-id="16aab-113">The following example lists disks for the VM named `myVM`:</span><span class="sxs-lookup"><span data-stu-id="16aab-113">The following example lists disks for the VM named `myVM`:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="16aab-114">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="16aab-114">The output is similar to the following example:</span></span>

    ```azurecli
    * Fetching disk images
    * Getting virtual machines
    * Getting VM disks
      data:    Lun  Size(GB)  Blob-Name                         OS
      data:    ---  --------  --------------------------------  -----
      data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
      data:    0    30        myDataDisk.vhd
      info:    vm disk list command OK
    ```

3. <span data-ttu-id="16aab-115">Note the LUN or the **logical unit number** for the disk that you want to detach.</span><span class="sxs-lookup"><span data-stu-id="16aab-115">Note the LUN or the **logical unit number** for the disk that you want to detach.</span></span>

## <a name="remove-operating-system-references-to-the-disk"></a><span data-ttu-id="16aab-116">Remove operating system references to the disk</span><span class="sxs-lookup"><span data-stu-id="16aab-116">Remove operating system references to the disk</span></span>
<span data-ttu-id="16aab-117">Before detaching the disk from the Linux guest, you should make sure that all partitions on the disk are not in use.</span><span class="sxs-lookup"><span data-stu-id="16aab-117">Before detaching the disk from the Linux guest, you should make sure that all partitions on the disk are not in use.</span></span> <span data-ttu-id="16aab-118">Ensure that the operating system does not attempt to remount them after a reboot.</span><span class="sxs-lookup"><span data-stu-id="16aab-118">Ensure that the operating system does not attempt to remount them after a reboot.</span></span> <span data-ttu-id="16aab-119">These steps undo the configuration you likely created when [attaching](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) the disk.</span><span class="sxs-lookup"><span data-stu-id="16aab-119">These steps undo the configuration you likely created when [attaching](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) the disk.</span></span>

1. <span data-ttu-id="16aab-120">Use the `lsscsi` command to discover the disk identifier.</span><span class="sxs-lookup"><span data-stu-id="16aab-120">Use the `lsscsi` command to discover the disk identifier.</span></span> <span data-ttu-id="16aab-121">`lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span><span class="sxs-lookup"><span data-stu-id="16aab-121">`lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="16aab-122">You can find the disk identifier you are looking for by using the LUN number.</span><span class="sxs-lookup"><span data-stu-id="16aab-122">You can find the disk identifier you are looking for by using the LUN number.</span></span> <span data-ttu-id="16aab-123">The last number in the tuple in each row is the LUN.</span><span class="sxs-lookup"><span data-stu-id="16aab-123">The last number in the tuple in each row is the LUN.</span></span> <span data-ttu-id="16aab-124">In the following example from `lsscsi`, LUN 0 maps to */dev/sdc*</span><span class="sxs-lookup"><span data-stu-id="16aab-124">In the following example from `lsscsi`, LUN 0 maps to */dev/sdc*</span></span>

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. <span data-ttu-id="16aab-125">Use `fdisk -l <disk>` to discover the partitions associated with the disk to be detached.</span><span class="sxs-lookup"><span data-stu-id="16aab-125">Use `fdisk -l <disk>` to discover the partitions associated with the disk to be detached.</span></span> <span data-ttu-id="16aab-126">The following example shows the output for `/dev/sdc`:</span><span class="sxs-lookup"><span data-stu-id="16aab-126">The following example shows the output for `/dev/sdc`:</span></span>

    ```bash
    Disk /dev/sdc: 1098.4 GB, 1098437885952 bytes, 2145386496 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x5a1d2a1a
    
        Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1            2048  2145386495  1072692224   83  Linux
    ```

3. <span data-ttu-id="16aab-127">Unmount each partition listed for the disk.</span><span class="sxs-lookup"><span data-stu-id="16aab-127">Unmount each partition listed for the disk.</span></span> <span data-ttu-id="16aab-128">The following example unmounts `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="16aab-128">The following example unmounts `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

4. <span data-ttu-id="16aab-129">Use the `blkid` command to discovery the UUIDs for all partitions.</span><span class="sxs-lookup"><span data-stu-id="16aab-129">Use the `blkid` command to discovery the UUIDs for all partitions.</span></span> <span data-ttu-id="16aab-130">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="16aab-130">The output is similar to the following example:</span></span>

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. <span data-ttu-id="16aab-131">Remove entries in the **/etc/fstab** file associated with either the device paths or UUIDs for all partitions for the disk to be detached.</span><span class="sxs-lookup"><span data-stu-id="16aab-131">Remove entries in the **/etc/fstab** file associated with either the device paths or UUIDs for all partitions for the disk to be detached.</span></span>  <span data-ttu-id="16aab-132">Entries for this example might be:</span><span class="sxs-lookup"><span data-stu-id="16aab-132">Entries for this example might be:</span></span>

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    <span data-ttu-id="16aab-133">or</span><span class="sxs-lookup"><span data-stu-id="16aab-133">or</span></span>
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-the-disk"></a><span data-ttu-id="16aab-134">Detach the disk</span><span class="sxs-lookup"><span data-stu-id="16aab-134">Detach the disk</span></span>
<span data-ttu-id="16aab-135">After you find the LUN number of the disk and removed the operating system references, you're ready to detach it:</span><span class="sxs-lookup"><span data-stu-id="16aab-135">After you find the LUN number of the disk and removed the operating system references, you're ready to detach it:</span></span>

1. <span data-ttu-id="16aab-136">Detach the selected disk from the virtual machine by running the command `azure vm disk detach
   <virtual-machine-name> <LUN>`.</span><span class="sxs-lookup"><span data-stu-id="16aab-136">Detach the selected disk from the virtual machine by running the command `azure vm disk detach
<virtual-machine-name> <LUN>`.</span></span> <span data-ttu-id="16aab-137">The following example detaches LUN `0` from the VM named `myVM`:</span><span class="sxs-lookup"><span data-stu-id="16aab-137">The following example detaches LUN `0` from the VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. <span data-ttu-id="16aab-138">You can check if the disk got detached by running `azure vm disk list` again.</span><span class="sxs-lookup"><span data-stu-id="16aab-138">You can check if the disk got detached by running `azure vm disk list` again.</span></span> <span data-ttu-id="16aab-139">The following example checks the VM named `myVM`:</span><span class="sxs-lookup"><span data-stu-id="16aab-139">The following example checks the VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="16aab-140">The output is similar to the following example, which shows the data disk is no longer attached:</span><span class="sxs-lookup"><span data-stu-id="16aab-140">The output is similar to the following example, which shows the data disk is no longer attached:</span></span>

    ```azurecli
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
     info:    vm disk list command OK
    ```

<span data-ttu-id="16aab-141">The detached disk remains in storage but is no longer attached to a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="16aab-141">The detached disk remains in storage but is no longer attached to a virtual machine.</span></span>

