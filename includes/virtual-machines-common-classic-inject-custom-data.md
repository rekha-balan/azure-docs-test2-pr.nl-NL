


<span data-ttu-id="b2e9f-101">This topic describes how to:</span><span class="sxs-lookup"><span data-stu-id="b2e9f-101">This topic describes how to:</span></span>

* <span data-ttu-id="b2e9f-102">Inject data into an Azure virtual machine (VM) when it is being provisioned.</span><span class="sxs-lookup"><span data-stu-id="b2e9f-102">Inject data into an Azure virtual machine (VM) when it is being provisioned.</span></span>
* <span data-ttu-id="b2e9f-103">Retrieve it for both Windows and Linux.</span><span class="sxs-lookup"><span data-stu-id="b2e9f-103">Retrieve it for both Windows and Linux.</span></span>
* <span data-ttu-id="b2e9f-104">Use special tools available on some systems to detect and handle custom data automatically.</span><span class="sxs-lookup"><span data-stu-id="b2e9f-104">Use special tools available on some systems to detect and handle custom data automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="b2e9f-105">This article describes how custom data can be injected by using a VM created with the Azure Service Management API.</span><span class="sxs-lookup"><span data-stu-id="b2e9f-105">This article describes how custom data can be injected by using a VM created with the Azure Service Management API.</span></span> <span data-ttu-id="b2e9f-106">To see how to use the Azure Resource Management API, see [the example template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span><span class="sxs-lookup"><span data-stu-id="b2e9f-106">To see how to use the Azure Resource Management API, see [the example template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span></span>
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a><span data-ttu-id="b2e9f-107">Injecting custom data into your Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="b2e9f-107">Injecting custom data into your Azure virtual machine</span></span>
<span data-ttu-id="b2e9f-108">This feature is currently supported only in the [Azure Command-Line Interface](https://github.com/Azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="b2e9f-108">This feature is currently supported only in the [Azure Command-Line Interface](https://github.com/Azure/azure-xplat-cli).</span></span> <span data-ttu-id="b2e9f-109">Here we create a `custom-data.txt` file that contains our data, then inject that in to the VM during provisioning.</span><span class="sxs-lookup"><span data-stu-id="b2e9f-109">Here we create a `custom-data.txt` file that contains our data, then inject that in to the VM during provisioning.</span></span> <span data-ttu-id="b2e9f-110">Although you may use any of the options for the `azure vm create` command, the following demonstrates one very basic approach:</span><span class="sxs-lookup"><span data-stu-id="b2e9f-110">Although you may use any of the options for the `azure vm create` command, the following demonstrates one very basic approach:</span></span>

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-the-virtual-machine"></a><span data-ttu-id="b2e9f-111">Using custom data in the virtual machine</span><span class="sxs-lookup"><span data-stu-id="b2e9f-111">Using custom data in the virtual machine</span></span>
* <span data-ttu-id="b2e9f-112">If your Azure VM is a Windows-based VM, then the custom data file is saved to `%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span><span class="sxs-lookup"><span data-stu-id="b2e9f-112">If your Azure VM is a Windows-based VM, then the custom data file is saved to `%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span></span> <span data-ttu-id="b2e9f-113">Although it was base64-encoded to transfer from the local computer to the new VM, it is automatically decoded and can be opened or used immediately.</span><span class="sxs-lookup"><span data-stu-id="b2e9f-113">Although it was base64-encoded to transfer from the local computer to the new VM, it is automatically decoded and can be opened or used immediately.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="b2e9f-114">If the file exists, it is overwritten.</span><span class="sxs-lookup"><span data-stu-id="b2e9f-114">If the file exists, it is overwritten.</span></span> <span data-ttu-id="b2e9f-115">The security on the directory is set to **System:Full Control** and **Administrators:Full Control**.</span><span class="sxs-lookup"><span data-stu-id="b2e9f-115">The security on the directory is set to **System:Full Control** and **Administrators:Full Control**.</span></span>
  > 
  > 
* <span data-ttu-id="b2e9f-116">If your Azure VM is a Linux-based VM, then the custom data file will be located in one of the following places depending on your distro.</span><span class="sxs-lookup"><span data-stu-id="b2e9f-116">If your Azure VM is a Linux-based VM, then the custom data file will be located in one of the following places depending on your distro.</span></span> <span data-ttu-id="b2e9f-117">The data may be base64-encoded, so you may need to decode the data first:</span><span class="sxs-lookup"><span data-stu-id="b2e9f-117">The data may be base64-encoded, so you may need to decode the data first:</span></span>
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a><span data-ttu-id="b2e9f-118">Cloud-init on Azure</span><span class="sxs-lookup"><span data-stu-id="b2e9f-118">Cloud-init on Azure</span></span>
<span data-ttu-id="b2e9f-119">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData to send a cloud-config to cloud-init.</span><span class="sxs-lookup"><span data-stu-id="b2e9f-119">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData to send a cloud-config to cloud-init.</span></span> <span data-ttu-id="b2e9f-120">Or if your custom data file is a script, then cloud-init can simply execute it.</span><span class="sxs-lookup"><span data-stu-id="b2e9f-120">Or if your custom data file is a script, then cloud-init can simply execute it.</span></span>

### <a name="ubuntu-cloud-images"></a><span data-ttu-id="b2e9f-121">Ubuntu Cloud Images</span><span class="sxs-lookup"><span data-stu-id="b2e9f-121">Ubuntu Cloud Images</span></span>
<span data-ttu-id="b2e9f-122">In most Azure Linux images, you would edit "/etc/waagent.conf" to configure the temporary resource disk and swap file.</span><span class="sxs-lookup"><span data-stu-id="b2e9f-122">In most Azure Linux images, you would edit "/etc/waagent.conf" to configure the temporary resource disk and swap file.</span></span> <span data-ttu-id="b2e9f-123">See [Azure Linux Agent user guide](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information.</span><span class="sxs-lookup"><span data-stu-id="b2e9f-123">See [Azure Linux Agent user guide](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information.</span></span>

<span data-ttu-id="b2e9f-124">However, on the Ubuntu Cloud Images, you must use cloud-init to configure the resource disk (that is, the "ephemeral" disk) and swap partition.</span><span class="sxs-lookup"><span data-stu-id="b2e9f-124">However, on the Ubuntu Cloud Images, you must use cloud-init to configure the resource disk (that is, the "ephemeral" disk) and swap partition.</span></span> <span data-ttu-id="b2e9f-125">See the following page on the Ubuntu wiki for more details: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span><span class="sxs-lookup"><span data-stu-id="b2e9f-125">See the following page on the Ubuntu wiki for more details: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps-using-cloud-init"></a><span data-ttu-id="b2e9f-126">Next steps: Using cloud-init</span><span class="sxs-lookup"><span data-stu-id="b2e9f-126">Next steps: Using cloud-init</span></span>
<span data-ttu-id="b2e9f-127">For further information, see the [cloud-init documentation for Ubuntu](https://help.ubuntu.com/community/CloudInit).</span><span class="sxs-lookup"><span data-stu-id="b2e9f-127">For further information, see the [cloud-init documentation for Ubuntu](https://help.ubuntu.com/community/CloudInit).</span></span>

<span data-ttu-id="b2e9f-128"><!--Link references-->
[Add Role Service Management REST API Reference](http://msdn.microsoft.com/library/azure/jj157186.aspx)</span><span class="sxs-lookup"><span data-stu-id="b2e9f-128"><!--Link references-->
[Add Role Service Management REST API Reference](http://msdn.microsoft.com/library/azure/jj157186.aspx)</span></span>

[<span data-ttu-id="b2e9f-129">Azure Command-line Interface</span><span class="sxs-lookup"><span data-stu-id="b2e9f-129">Azure Command-line Interface</span></span>](https://github.com/Azure/azure-xplat-cli)

