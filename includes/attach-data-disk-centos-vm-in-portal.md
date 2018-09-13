1. <span data-ttu-id="aaac2-101">In the Azure [Management Portal](http://manage.windowsazure.com), click **Virtual Machines** and then select the virtual machine you just created (**testlinuxvm**).</span><span class="sxs-lookup"><span data-stu-id="aaac2-101">In the Azure [Management Portal](http://manage.windowsazure.com), click **Virtual Machines** and then select the virtual machine you just created (**testlinuxvm**).</span></span>
2. <span data-ttu-id="aaac2-102">On the command bar click **Attach** and then click **Attach Empty Disk**.</span><span class="sxs-lookup"><span data-stu-id="aaac2-102">On the command bar click **Attach** and then click **Attach Empty Disk**.</span></span>
   
    <span data-ttu-id="aaac2-103">The **Attach Empty Disk** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="aaac2-103">The **Attach Empty Disk** dialog box appears.</span></span>
3. <span data-ttu-id="aaac2-104">The **Virtual Machine Name**, **Storage Location**, and **File Name** are already defined for you.</span><span class="sxs-lookup"><span data-stu-id="aaac2-104">The **Virtual Machine Name**, **Storage Location**, and **File Name** are already defined for you.</span></span> <span data-ttu-id="aaac2-105">All you have to do is enter the size that you want for the disk.</span><span class="sxs-lookup"><span data-stu-id="aaac2-105">All you have to do is enter the size that you want for the disk.</span></span> <span data-ttu-id="aaac2-106">Type **5** in the **Size** field.</span><span class="sxs-lookup"><span data-stu-id="aaac2-106">Type **5** in the **Size** field.</span></span>
   
    ![Attach Empty Disk][Image2]
   
    <span data-ttu-id="aaac2-108">**Note:** All disks are created from a .vhd file in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="aaac2-108">**Note:** All disks are created from a .vhd file in Azure storage.</span></span> <span data-ttu-id="aaac2-109">You can provide a name for the .vhd file that is added to storage, but Azure generates the name of the disk automatically.</span><span class="sxs-lookup"><span data-stu-id="aaac2-109">You can provide a name for the .vhd file that is added to storage, but Azure generates the name of the disk automatically.</span></span>
4. <span data-ttu-id="aaac2-110">Click the check mark to attach the data disk to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="aaac2-110">Click the check mark to attach the data disk to the virtual machine.</span></span>
5. <span data-ttu-id="aaac2-111">Click the name of the virtual machine to display the dashboard so you can verify that the data disk was successfully attached to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="aaac2-111">Click the name of the virtual machine to display the dashboard so you can verify that the data disk was successfully attached to the virtual machine.</span></span> <span data-ttu-id="aaac2-112">The disk that you attached is listed in the **Disks** table.</span><span class="sxs-lookup"><span data-stu-id="aaac2-112">The disk that you attached is listed in the **Disks** table.</span></span>
   
    <span data-ttu-id="aaac2-113">When you attach a data disk, it's not ready for use until you log in to complete the setup.</span><span class="sxs-lookup"><span data-stu-id="aaac2-113">When you attach a data disk, it's not ready for use until you log in to complete the setup.</span></span>

## <a name="connect-to-the-virtual-machine-using-ssh-or-putty-and-complete-setup"></a><span data-ttu-id="aaac2-114">Connect to the Virtual Machine Using SSH or PuTTY and Complete Setup</span><span class="sxs-lookup"><span data-stu-id="aaac2-114">Connect to the Virtual Machine Using SSH or PuTTY and Complete Setup</span></span>
<span data-ttu-id="aaac2-115">Log on to the virtual machine to complete setup of the disk so you can use it to store data.</span><span class="sxs-lookup"><span data-stu-id="aaac2-115">Log on to the virtual machine to complete setup of the disk so you can use it to store data.</span></span>

1. <span data-ttu-id="aaac2-116">After the virtual machine is provisioned, connect using SSH or PuTTY and login as **newuser** (as described in the steps above).</span><span class="sxs-lookup"><span data-stu-id="aaac2-116">After the virtual machine is provisioned, connect using SSH or PuTTY and login as **newuser** (as described in the steps above).</span></span>    
2. <span data-ttu-id="aaac2-117">In the SSH or PuTTY window type the following command and then enter the account password:</span><span class="sxs-lookup"><span data-stu-id="aaac2-117">In the SSH or PuTTY window type the following command and then enter the account password:</span></span>
   
    `$ sudo grep SCSI /var/log/messages`
   
    <span data-ttu-id="aaac2-118">You can find the identifier of the last data disk that was added in the messages that are displayed (**sdc**, in this example).</span><span class="sxs-lookup"><span data-stu-id="aaac2-118">You can find the identifier of the last data disk that was added in the messages that are displayed (**sdc**, in this example).</span></span>
   
    ![GREP][Image4]
3. <span data-ttu-id="aaac2-120">In the SSH or PuTTY window, enter the following command to partition the disk **/dev/sdc**:</span><span class="sxs-lookup"><span data-stu-id="aaac2-120">In the SSH or PuTTY window, enter the following command to partition the disk **/dev/sdc**:</span></span>
   
    `$ sudo fdisk /dev/sdc`
4. <span data-ttu-id="aaac2-121">Enter **n** to create a new partition.</span><span class="sxs-lookup"><span data-stu-id="aaac2-121">Enter **n** to create a new partition.</span></span>
   
    ![FDISK][Image5]
5. <span data-ttu-id="aaac2-123">Type **p** to make the partition the primary partition, type **1** to make it the first partition, and then type enter to accept the default value (1) for the cylinder.</span><span class="sxs-lookup"><span data-stu-id="aaac2-123">Type **p** to make the partition the primary partition, type **1** to make it the first partition, and then type enter to accept the default value (1) for the cylinder.</span></span>
   
    ![FDISK][Image6]
6. <span data-ttu-id="aaac2-125">Type **p** to see the details about the disk that is being partitioned.</span><span class="sxs-lookup"><span data-stu-id="aaac2-125">Type **p** to see the details about the disk that is being partitioned.</span></span>
   
    ![FDISK][Image7]
7. <span data-ttu-id="aaac2-127">Type **w** to write the settings for the disk.</span><span class="sxs-lookup"><span data-stu-id="aaac2-127">Type **w** to write the settings for the disk.</span></span>
   
    ![FDISK][Image8]
8. <span data-ttu-id="aaac2-129">Format the new disk using the **mkfs** command:</span><span class="sxs-lookup"><span data-stu-id="aaac2-129">Format the new disk using the **mkfs** command:</span></span>
   
    `$ sudo mkfs -t ext4 /dev/sdc1`
9. <span data-ttu-id="aaac2-130">Next you must have a directory available to mount the new file system.</span><span class="sxs-lookup"><span data-stu-id="aaac2-130">Next you must have a directory available to mount the new file system.</span></span> <span data-ttu-id="aaac2-131">As an example, type the following command to make a new directory for mounting the drive, and then enter the account password:</span><span class="sxs-lookup"><span data-stu-id="aaac2-131">As an example, type the following command to make a new directory for mounting the drive, and then enter the account password:</span></span>
   
    `sudo mkdir /datadrive`
10. <span data-ttu-id="aaac2-132">Type the following command to mount the drive:</span><span class="sxs-lookup"><span data-stu-id="aaac2-132">Type the following command to mount the drive:</span></span>
    
    `sudo mount /dev/sdc1 /datadrive`
    
    <span data-ttu-id="aaac2-133">The data disk is now ready to use as **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="aaac2-133">The data disk is now ready to use as **/datadrive**.</span></span>
11. <span data-ttu-id="aaac2-134">Add the new drive to /etc/fstab:</span><span class="sxs-lookup"><span data-stu-id="aaac2-134">Add the new drive to /etc/fstab:</span></span>
    
    <span data-ttu-id="aaac2-135">To ensure the drive is re-mounted automatically after a reboot it must be added to the /etc/fstab file.</span><span class="sxs-lookup"><span data-stu-id="aaac2-135">To ensure the drive is re-mounted automatically after a reboot it must be added to the /etc/fstab file.</span></span> <span data-ttu-id="aaac2-136">In addition, it is highly recommended that the UUID (Universally Unique IDentifier) is used in /etc/fstab to refer to the drive rather than just the device name (i.e. /dev/sdc1).</span><span class="sxs-lookup"><span data-stu-id="aaac2-136">In addition, it is highly recommended that the UUID (Universally Unique IDentifier) is used in /etc/fstab to refer to the drive rather than just the device name (i.e. /dev/sdc1).</span></span> <span data-ttu-id="aaac2-137">To find the UUID of the new drive you can use the **blkid** utility:</span><span class="sxs-lookup"><span data-stu-id="aaac2-137">To find the UUID of the new drive you can use the **blkid** utility:</span></span>
    
        `sudo -i blkid`
    
    <span data-ttu-id="aaac2-138">The output will look similar to the following:</span><span class="sxs-lookup"><span data-stu-id="aaac2-138">The output will look similar to the following:</span></span>
    
        `/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"`
        `/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"`
        `/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"`
    
    > [!NOTE]
    > <span data-ttu-id="aaac2-139">blkid may not require sudo access in all cases, however, it may be easier to run with `sudo -i` on some distributions if /sbin or /usr/sbin are not in your `$PATH`.</span><span class="sxs-lookup"><span data-stu-id="aaac2-139">blkid may not require sudo access in all cases, however, it may be easier to run with `sudo -i` on some distributions if /sbin or /usr/sbin are not in your `$PATH`.</span></span>
    > 
    > 
    
    <span data-ttu-id="aaac2-140">**Caution:** Improperly editing the /etc/fstab file could result in an unbootable system.</span><span class="sxs-lookup"><span data-stu-id="aaac2-140">**Caution:** Improperly editing the /etc/fstab file could result in an unbootable system.</span></span> <span data-ttu-id="aaac2-141">If unsure, please refer to the distribution's documentation for information on how to properly edit this file.</span><span class="sxs-lookup"><span data-stu-id="aaac2-141">If unsure, please refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="aaac2-142">It is also recommended that a backup of the /etc/fstab file is created before editing.</span><span class="sxs-lookup"><span data-stu-id="aaac2-142">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>
    
    <span data-ttu-id="aaac2-143">Using a text editor, enter the information about the new file system at the end of the /etc/fstab file.</span><span class="sxs-lookup"><span data-stu-id="aaac2-143">Using a text editor, enter the information about the new file system at the end of the /etc/fstab file.</span></span>  <span data-ttu-id="aaac2-144">In this example we will use the UUID value for the new **/dev/sdc1** device that was created in the previous steps, and the mountpoint **/datadrive**:</span><span class="sxs-lookup"><span data-stu-id="aaac2-144">In this example we will use the UUID value for the new **/dev/sdc1** device that was created in the previous steps, and the mountpoint **/datadrive**:</span></span>
    
        `UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2`
    
    <span data-ttu-id="aaac2-145">If additional data drives or partitions are created you will need to enter them into /etc/fstab separately as well.</span><span class="sxs-lookup"><span data-stu-id="aaac2-145">If additional data drives or partitions are created you will need to enter them into /etc/fstab separately as well.</span></span>
    
    <span data-ttu-id="aaac2-146">You can now test that the file system is mounted properly by simply unmounting and then re-mounting the file system, i.e. using the example mount point `/datadrive` created in the earlier steps:</span><span class="sxs-lookup"><span data-stu-id="aaac2-146">You can now test that the file system is mounted properly by simply unmounting and then re-mounting the file system, i.e. using the example mount point `/datadrive` created in the earlier steps:</span></span> 
    
        `sudo umount /datadrive`
        `sudo mount /datadrive`
    
    <span data-ttu-id="aaac2-147">If the second command produces an error, check the /etc/fstab file for correct syntax.</span><span class="sxs-lookup"><span data-stu-id="aaac2-147">If the second command produces an error, check the /etc/fstab file for correct syntax.</span></span>

    >[AZURE.NOTE] <span data-ttu-id="aaac2-148">Subsequently removing a data disk without editing fstab could cause the VM to fail to boot.</span><span class="sxs-lookup"><span data-stu-id="aaac2-148">Subsequently removing a data disk without editing fstab could cause the VM to fail to boot.</span></span> <span data-ttu-id="aaac2-149">If this is a common occurrence, then most distributions provide either the `nofail` and/or `nobootwait` fstab options that will allow a system to boot even if the disk is not present.</span><span class="sxs-lookup"><span data-stu-id="aaac2-149">If this is a common occurrence, then most distributions provide either the `nofail` and/or `nobootwait` fstab options that will allow a system to boot even if the disk is not present.</span></span> <span data-ttu-id="aaac2-150">Please consult your distribution's documentation for more information on these parameters.</span><span class="sxs-lookup"><span data-stu-id="aaac2-150">Please consult your distribution's documentation for more information on these parameters.</span></span>


[Image2]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/attach-data-disk-centos-vm-in-portal/AttachDataDiskLinuxVM2.png
[Image4]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/attach-data-disk-centos-vm-in-portal/GrepScsiMessages.png
[Image5]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/attach-data-disk-centos-vm-in-portal/fdisk1.png
[Image6]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/attach-data-disk-centos-vm-in-portal/fdisk2.png
[Image7]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/attach-data-disk-centos-vm-in-portal/fdisk3.png
[Image8]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/attach-data-disk-centos-vm-in-portal/fdisk4.png
[Image9]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/attach-data-disk-centos-vm-in-portal/mkfs.png








