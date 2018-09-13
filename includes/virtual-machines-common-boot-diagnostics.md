<span data-ttu-id="d4528-101">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure virtual machines Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="d4528-101">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure virtual machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="d4528-102">When bringing your own image to Azure or even booting one of the platform images, there can be many reasons why a virtual machine gets into a non-bootable state.</span><span class="sxs-lookup"><span data-stu-id="d4528-102">When bringing your own image to Azure or even booting one of the platform images, there can be many reasons why a virtual machine gets into a non-bootable state.</span></span> <span data-ttu-id="d4528-103">These features enable you to easily diagnose and recover your virtual machines from boot failures.</span><span class="sxs-lookup"><span data-stu-id="d4528-103">These features enable you to easily diagnose and recover your virtual machines from boot failures.</span></span>

<span data-ttu-id="d4528-104">For Linux virtual machines, you can easily view the output of your console log from the Portal:</span><span class="sxs-lookup"><span data-stu-id="d4528-104">For Linux virtual machines, you can easily view the output of your console log from the Portal:</span></span>

![Azure portal](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="d4528-106">However, for both Windows and Linux virtual machines, Azure also enables you to see a screenshot of the VM from the hypervisor:</span><span class="sxs-lookup"><span data-stu-id="d4528-106">However, for both Windows and Linux virtual machines, Azure also enables you to see a screenshot of the VM from the hypervisor:</span></span>

![Error](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

<span data-ttu-id="d4528-108">Both of these features are supported for Azure virtual machines in all regions.</span><span class="sxs-lookup"><span data-stu-id="d4528-108">Both of these features are supported for Azure virtual machines in all regions.</span></span> <span data-ttu-id="d4528-109">Note, screenshots, and output can take up to 10 minutes to appear in your storage account.</span><span class="sxs-lookup"><span data-stu-id="d4528-109">Note, screenshots, and output can take up to 10 minutes to appear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="d4528-110">Common boot errors</span><span class="sxs-lookup"><span data-stu-id="d4528-110">Common boot errors</span></span>

- [<span data-ttu-id="d4528-111">0xC000000E</span><span class="sxs-lookup"><span data-stu-id="d4528-111">0xC000000E</span></span>](https://support.microsoft.com/help/4010129)
- [<span data-ttu-id="d4528-112">0xC000000F</span><span class="sxs-lookup"><span data-stu-id="d4528-112">0xC000000F</span></span>](https://support.microsoft.com/help/4010130)
- [<span data-ttu-id="d4528-113">0xC0000011</span><span class="sxs-lookup"><span data-stu-id="d4528-113">0xC0000011</span></span>](https://support.microsoft.com/help/4010134)
- [<span data-ttu-id="d4528-114">0xC0000034</span><span class="sxs-lookup"><span data-stu-id="d4528-114">0xC0000034</span></span>](https://support.microsoft.com/help/4010140)
- [<span data-ttu-id="d4528-115">0xC0000098</span><span class="sxs-lookup"><span data-stu-id="d4528-115">0xC0000098</span></span>](https://support.microsoft.com/help/4010137)
- [<span data-ttu-id="d4528-116">0xC00000BA</span><span class="sxs-lookup"><span data-stu-id="d4528-116">0xC00000BA</span></span>](https://support.microsoft.com/help/4010136)
- [<span data-ttu-id="d4528-117">0xC000014C</span><span class="sxs-lookup"><span data-stu-id="d4528-117">0xC000014C</span></span>](https://support.microsoft.com/help/4010141)
- [<span data-ttu-id="d4528-118">0xC0000221</span><span class="sxs-lookup"><span data-stu-id="d4528-118">0xC0000221</span></span>](https://support.microsoft.com/help/4010132)
- [<span data-ttu-id="d4528-119">0xC0000225</span><span class="sxs-lookup"><span data-stu-id="d4528-119">0xC0000225</span></span>](https://support.microsoft.com/help/4010138)
- [<span data-ttu-id="d4528-120">0xC0000359</span><span class="sxs-lookup"><span data-stu-id="d4528-120">0xC0000359</span></span>](https://support.microsoft.com/help/4010135)
- [<span data-ttu-id="d4528-121">0xC0000605</span><span class="sxs-lookup"><span data-stu-id="d4528-121">0xC0000605</span></span>](https://support.microsoft.com/help/4010131)
- [<span data-ttu-id="d4528-122">An operating system wasn't found</span><span class="sxs-lookup"><span data-stu-id="d4528-122">An operating system wasn't found</span></span>](https://support.microsoft.com/help/4010142)
- [<span data-ttu-id="d4528-123">Boot failure or INACCESSIBLE_BOOT_DEVICE</span><span class="sxs-lookup"><span data-stu-id="d4528-123">Boot failure or INACCESSIBLE_BOOT_DEVICE</span></span>](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="d4528-124">Enable diagnostics on a new virtual machine</span><span class="sxs-lookup"><span data-stu-id="d4528-124">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="d4528-125">When creating a new virtual machine from the Azure Portal, select the **Azure Resource Manager** from the deployment model dropdown:</span><span class="sxs-lookup"><span data-stu-id="d4528-125">When creating a new virtual machine from the Azure Portal, select the **Azure Resource Manager** from the deployment model dropdown:</span></span>
 
    ![Resource Manager](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="d4528-127">In **Settings**, enable the **Boot diagnostics**, and then select a storage account that you would like to place these diagnostic files.</span><span class="sxs-lookup"><span data-stu-id="d4528-127">In **Settings**, enable the **Boot diagnostics**, and then select a storage account that you would like to place these diagnostic files.</span></span>
 
    ![Create VM](./media/virtual-machines-common-boot-diagnostics/create-storage-account.png)

    > [!NOTE]
    > <span data-ttu-id="d4528-129">The Boot diagnostics feature does not support premium storage account.</span><span class="sxs-lookup"><span data-stu-id="d4528-129">The Boot diagnostics feature does not support premium storage account.</span></span> <span data-ttu-id="d4528-130">If you use the premium storage account for Boot diagnostics, you might receive the StorageAccountTypeNotSupported error when you start the VM.</span><span class="sxs-lookup"><span data-stu-id="d4528-130">If you use the premium storage account for Boot diagnostics, you might receive the StorageAccountTypeNotSupported error when you start the VM.</span></span>
    >
    > 

3. <span data-ttu-id="d4528-131">If you are deploying from an Azure Resource Manager template, navigate to your virtual machine resource and append the diagnostics profile section.</span><span class="sxs-lookup"><span data-stu-id="d4528-131">If you are deploying from an Azure Resource Manager template, navigate to your virtual machine resource and append the diagnostics profile section.</span></span> <span data-ttu-id="d4528-132">Remember to use the “2015-06-15” API version header.</span><span class="sxs-lookup"><span data-stu-id="d4528-132">Remember to use the “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="d4528-133">The diagnostics profile enables you to select the storage account where you want to put these logs.</span><span class="sxs-lookup"><span data-stu-id="d4528-133">The diagnostics profile enables you to select the storage account where you want to put these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

<span data-ttu-id="d4528-134">To deploy a sample virtual machine with boot diagnostics enabled, check out our repo here.</span><span class="sxs-lookup"><span data-stu-id="d4528-134">To deploy a sample virtual machine with boot diagnostics enabled, check out our repo here.</span></span>

## <a name="enable-boot-diagnostics-on-existing-virtual-machine"></a><span data-ttu-id="d4528-135">Enable Boot diagnostics on existing virtual machine</span><span class="sxs-lookup"><span data-stu-id="d4528-135">Enable Boot diagnostics on existing virtual machine</span></span> 

<span data-ttu-id="d4528-136">To enable Boot diagnostics on an existing virtual machine, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="d4528-136">To enable Boot diagnostics on an existing virtual machine, follow these steps:</span></span>

1. <span data-ttu-id="d4528-137">Sign in to the [Azure portal](https://portal.azure.com), and then select the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="d4528-137">Sign in to the [Azure portal](https://portal.azure.com), and then select the virtual machine.</span></span>
2. <span data-ttu-id="d4528-138">In **Support + troubleshooting**, select **Boot diagnostics** > **Settings**, change the status to **On**, and then select a storage account.</span><span class="sxs-lookup"><span data-stu-id="d4528-138">In **Support + troubleshooting**, select **Boot diagnostics** > **Settings**, change the status to **On**, and then select a storage account.</span></span> 
4. <span data-ttu-id="d4528-139">Make sure that the Boot diagnostics option is selected and then save the change.</span><span class="sxs-lookup"><span data-stu-id="d4528-139">Make sure that the Boot diagnostics option is selected and then save the change.</span></span>

    ![Update Existing VM](./media/virtual-machines-common-boot-diagnostics/enable-for-existing-vm.png)

3. <span data-ttu-id="d4528-141">Restart the VM to take effect.</span><span class="sxs-lookup"><span data-stu-id="d4528-141">Restart the VM to take effect.</span></span>


