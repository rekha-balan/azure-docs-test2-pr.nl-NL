## <a name="overview"></a><span data-ttu-id="b8348-101">Overview</span><span class="sxs-lookup"><span data-stu-id="b8348-101">Overview</span></span>
<span data-ttu-id="b8348-102">When you create a new virtual machine (VM) in a Resource Group by deploying an image from [Azure Marketplace](https://azure.microsoft.com/marketplace/), the default OS drive is 127 GB.</span><span class="sxs-lookup"><span data-stu-id="b8348-102">When you create a new virtual machine (VM) in a Resource Group by deploying an image from [Azure Marketplace](https://azure.microsoft.com/marketplace/), the default OS drive is 127 GB.</span></span> <span data-ttu-id="b8348-103">Even though it’s possible to add data disks to the VM (how many depending upon the SKU you’ve chosen) and moreover it’s recommended to install applications and CPU intensive workloads on these addendum disks, oftentimes customers need to expand the OS drive to support certain scenarios such as following:</span><span class="sxs-lookup"><span data-stu-id="b8348-103">Even though it’s possible to add data disks to the VM (how many depending upon the SKU you’ve chosen) and moreover it’s recommended to install applications and CPU intensive workloads on these addendum disks, oftentimes customers need to expand the OS drive to support certain scenarios such as following:</span></span>

1. <span data-ttu-id="b8348-104">Support legacy applications that install components on OS drive.</span><span class="sxs-lookup"><span data-stu-id="b8348-104">Support legacy applications that install components on OS drive.</span></span>
2. <span data-ttu-id="b8348-105">Migrate a physical PC or virtual machine from on-premises with a larger OS drive.</span><span class="sxs-lookup"><span data-stu-id="b8348-105">Migrate a physical PC or virtual machine from on-premises with a larger OS drive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8348-106">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span><span class="sxs-lookup"><span data-stu-id="b8348-106">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="b8348-107">This article covers using the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="b8348-107">This article covers using the Resource Manager model.</span></span> <span data-ttu-id="b8348-108">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="b8348-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> 
> 

## <a name="resize-the-os-drive"></a><span data-ttu-id="b8348-109">Resize the OS drive</span><span class="sxs-lookup"><span data-stu-id="b8348-109">Resize the OS drive</span></span>
<span data-ttu-id="b8348-110">In this article we’ll accomplish the task of resizing the OS drive using resource manager modules of [Azure Powershell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="b8348-110">In this article we’ll accomplish the task of resizing the OS drive using resource manager modules of [Azure Powershell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="b8348-111">Open your Powershell ISE or Powershell window in administrative mode and follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="b8348-111">Open your Powershell ISE or Powershell window in administrative mode and follow the steps below:</span></span>

1. <span data-ttu-id="b8348-112">Sign-in to your Microsoft Azure account in resource management mode and select your subscription as follows:</span><span class="sxs-lookup"><span data-stu-id="b8348-112">Sign-in to your Microsoft Azure account in resource management mode and select your subscription as follows:</span></span>
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. <span data-ttu-id="b8348-113">Set your resource group name and VM name as follows:</span><span class="sxs-lookup"><span data-stu-id="b8348-113">Set your resource group name and VM name as follows:</span></span>
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. <span data-ttu-id="b8348-114">Obtain a reference to your VM as follows:</span><span class="sxs-lookup"><span data-stu-id="b8348-114">Obtain a reference to your VM as follows:</span></span>
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. <span data-ttu-id="b8348-115">Stop the VM before resizing the disk as follows:</span><span class="sxs-lookup"><span data-stu-id="b8348-115">Stop the VM before resizing the disk as follows:</span></span>
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. <span data-ttu-id="b8348-116">And here comes the moment we’ve been waiting for!</span><span class="sxs-lookup"><span data-stu-id="b8348-116">And here comes the moment we’ve been waiting for!</span></span> <span data-ttu-id="b8348-117">Set the size of the OS disk to the desired value and update the VM as follows:</span><span class="sxs-lookup"><span data-stu-id="b8348-117">Set the size of the OS disk to the desired value and update the VM as follows:</span></span>
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > <span data-ttu-id="b8348-118">The new size should be greater than the existing disk size.</span><span class="sxs-lookup"><span data-stu-id="b8348-118">The new size should be greater than the existing disk size.</span></span> <span data-ttu-id="b8348-119">The maximum allowed is 1023 GB.</span><span class="sxs-lookup"><span data-stu-id="b8348-119">The maximum allowed is 1023 GB.</span></span>
   > 
   > 
6. <span data-ttu-id="b8348-120">Updating the VM may take a few seconds.</span><span class="sxs-lookup"><span data-stu-id="b8348-120">Updating the VM may take a few seconds.</span></span> <span data-ttu-id="b8348-121">Once the command finishes executing, restart the VM as follows:</span><span class="sxs-lookup"><span data-stu-id="b8348-121">Once the command finishes executing, restart the VM as follows:</span></span>
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

<span data-ttu-id="b8348-122">And that’s it!</span><span class="sxs-lookup"><span data-stu-id="b8348-122">And that’s it!</span></span> <span data-ttu-id="b8348-123">Now RDP into the VM, open Computer Management (or Disk Management) and expand the drive using the newly allocated space.</span><span class="sxs-lookup"><span data-stu-id="b8348-123">Now RDP into the VM, open Computer Management (or Disk Management) and expand the drive using the newly allocated space.</span></span>

## <a name="summary"></a><span data-ttu-id="b8348-124">Summary</span><span class="sxs-lookup"><span data-stu-id="b8348-124">Summary</span></span>
<span data-ttu-id="b8348-125">In this article, we used Azure Resource Manager modules of Powershell to expand the OS drive of an IaaS virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b8348-125">In this article, we used Azure Resource Manager modules of Powershell to expand the OS drive of an IaaS virtual machine.</span></span> <span data-ttu-id="b8348-126">Reproduced below is the complete script for your reference:</span><span class="sxs-lookup"><span data-stu-id="b8348-126">Reproduced below is the complete script for your reference:</span></span>

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a><span data-ttu-id="b8348-127">Next Steps</span><span class="sxs-lookup"><span data-stu-id="b8348-127">Next Steps</span></span>
<span data-ttu-id="b8348-128">Though in this article, we focused primarily on expanding the OS disk of the VM, the developed script may also be used for expanding the data disks attached to the VM by changing a single line of code.</span><span class="sxs-lookup"><span data-stu-id="b8348-128">Though in this article, we focused primarily on expanding the OS disk of the VM, the developed script may also be used for expanding the data disks attached to the VM by changing a single line of code.</span></span> <span data-ttu-id="b8348-129">For example, to expand the first data disk attached to the VM, replace the ```OSDisk``` object of ```StorageProfile``` with ```DataDisks``` array and use a numeric index to obtain a reference to first attached data disk, as shown below:</span><span class="sxs-lookup"><span data-stu-id="b8348-129">For example, to expand the first data disk attached to the VM, replace the ```OSDisk``` object of ```StorageProfile``` with ```DataDisks``` array and use a numeric index to obtain a reference to first attached data disk, as shown below:</span></span>

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
<span data-ttu-id="b8348-130">Similarly you may reference other data disks attached to the VM, either by using an index as shown above or the ```Name``` property of the disk as illustrated below:</span><span class="sxs-lookup"><span data-stu-id="b8348-130">Similarly you may reference other data disks attached to the VM, either by using an index as shown above or the ```Name``` property of the disk as illustrated below:</span></span>

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

<span data-ttu-id="b8348-131">If you want to find out how to attach disks to an Azure Resource Manager VM, check this [article](../articles/virtual-machines/windows/attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b8348-131">If you want to find out how to attach disks to an Azure Resource Manager VM, check this [article](../articles/virtual-machines/windows/attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

