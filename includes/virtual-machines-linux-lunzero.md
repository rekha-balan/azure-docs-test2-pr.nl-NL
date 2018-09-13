<span data-ttu-id="4c05f-101">When adding data disks to a Linux VM, you may encounter errors if a disk does not exist at LUN 0.</span><span class="sxs-lookup"><span data-stu-id="4c05f-101">When adding data disks to a Linux VM, you may encounter errors if a disk does not exist at LUN 0.</span></span> <span data-ttu-id="4c05f-102">If you are adding a disk manually using the `azure vm disk attach-new` command and you specify a LUN (`--lun`) rather than allowing the Azure platform to determine the appropriate LUN, take care that a disk already exists / will exist at LUN 0.</span><span class="sxs-lookup"><span data-stu-id="4c05f-102">If you are adding a disk manually using the `azure vm disk attach-new` command and you specify a LUN (`--lun`) rather than allowing the Azure platform to determine the appropriate LUN, take care that a disk already exists / will exist at LUN 0.</span></span> 

<span data-ttu-id="4c05f-103">Consider the following example showing a snippet of the output from `lsscsi`:</span><span class="sxs-lookup"><span data-stu-id="4c05f-103">Consider the following example showing a snippet of the output from `lsscsi`:</span></span>

```bash
[5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc 
[5:0:0:1]    disk    Msft     Virtual Disk     1.0   /dev/sdd 
```

<span data-ttu-id="4c05f-104">The two data disks exist at LUN 0 and LUN 1 (the first column in the `lsscsi` output details `[host:channel:target:lun]`).</span><span class="sxs-lookup"><span data-stu-id="4c05f-104">The two data disks exist at LUN 0 and LUN 1 (the first column in the `lsscsi` output details `[host:channel:target:lun]`).</span></span> <span data-ttu-id="4c05f-105">Both disks should be accessbile from within the VM.</span><span class="sxs-lookup"><span data-stu-id="4c05f-105">Both disks should be accessbile from within the VM.</span></span> <span data-ttu-id="4c05f-106">If you had manually specified the first disk to be added at LUN 1 and the second disk at LUN 2, you may not see the disks correctly from within your VM.</span><span class="sxs-lookup"><span data-stu-id="4c05f-106">If you had manually specified the first disk to be added at LUN 1 and the second disk at LUN 2, you may not see the disks correctly from within your VM.</span></span>

> [!NOTE]
> <span data-ttu-id="4c05f-107">The Azure `host` value is 5 in these examples, but this may vary depending on the type of storage you select.</span><span class="sxs-lookup"><span data-stu-id="4c05f-107">The Azure `host` value is 5 in these examples, but this may vary depending on the type of storage you select.</span></span>
> 
> 

<span data-ttu-id="4c05f-108">This disk behavior is not an Azure problem, but the way in which the Linux kernel follows the SCSI specifications.</span><span class="sxs-lookup"><span data-stu-id="4c05f-108">This disk behavior is not an Azure problem, but the way in which the Linux kernel follows the SCSI specifications.</span></span> <span data-ttu-id="4c05f-109">When the Linux kernel scans the SCSI bus for attached devices, a device must be found at LUN 0 in order for the system to continue scanning for additional devices.</span><span class="sxs-lookup"><span data-stu-id="4c05f-109">When the Linux kernel scans the SCSI bus for attached devices, a device must be found at LUN 0 in order for the system to continue scanning for additional devices.</span></span> <span data-ttu-id="4c05f-110">As such:</span><span class="sxs-lookup"><span data-stu-id="4c05f-110">As such:</span></span>

* <span data-ttu-id="4c05f-111">Review the output of `lsscsi` after adding a data disk to verify that you have a disk at LUN 0.</span><span class="sxs-lookup"><span data-stu-id="4c05f-111">Review the output of `lsscsi` after adding a data disk to verify that you have a disk at LUN 0.</span></span>
* <span data-ttu-id="4c05f-112">If your disk does not show up correctly within your VM, verify a disk exists at LUN 0.</span><span class="sxs-lookup"><span data-stu-id="4c05f-112">If your disk does not show up correctly within your VM, verify a disk exists at LUN 0.</span></span>

