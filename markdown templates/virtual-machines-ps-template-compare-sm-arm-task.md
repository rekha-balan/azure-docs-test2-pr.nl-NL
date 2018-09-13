<!--save a copy of this file to your local repo. It's important that you follow the naming conventions by starting with the service name, and use lowercase only for the file name. See "file-names-and-locations.md" under the "contributor-guide" folder in your repo.

Info to help you use the template are enclosed in the Markdown comments using the caret, hyphen, dash syntax. Delete these from your file.

Text not wrapped in comment syntax is intended to be used as is, or with updates enclosed in [  ]. Add the info and delete the bracket. 

Pay attention to spacing and indents. They affect formatting. 

--> 

<!--replace this with Properties and Tags sections. These are required sections. See "article-metadata.md" in under the "contributor-guide" folder in your repo. Attributes in each section can be placed on separate lines to make them easier to read and check-->

# <a name="use-azure-powershell-to-task"></a><span data-ttu-id="5a5d8-101">Use Azure PowerShell to [task]</span><span class="sxs-lookup"><span data-stu-id="5a5d8-101">Use Azure PowerShell to [task]</span></span>
<span data-ttu-id="5a5d8-102">This article shows you how to [task], using commands from both the Azure module and the Azure Resource Manager module.</span><span class="sxs-lookup"><span data-stu-id="5a5d8-102">This article shows you how to [task], using commands from both the Azure module and the Azure Resource Manager module.</span></span> <span data-ttu-id="5a5d8-103">This is intended to help you learn the new commands as well as migrate existing scripts to the new commands.</span><span class="sxs-lookup"><span data-stu-id="5a5d8-103">This is intended to help you learn the new commands as well as migrate existing scripts to the new commands.</span></span>

## <a name="prerequisite-install-a-recent-version-of-azure-powershell"></a><span data-ttu-id="5a5d8-104">Prerequisite: Install a Recent Version of Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a5d8-104">Prerequisite: Install a Recent Version of Azure PowerShell</span></span>
<span data-ttu-id="5a5d8-105">If you haven't done so already, install at least the [version number] version of Azure PowerShell on your local computer.</span><span class="sxs-lookup"><span data-stu-id="5a5d8-105">If you haven't done so already, install at least the [version number] version of Azure PowerShell on your local computer.</span></span> <span data-ttu-id="5a5d8-106">If you use an earlier version, it won't have the Azure Resource Manager cmdlets described in this article.</span><span class="sxs-lookup"><span data-stu-id="5a5d8-106">If you use an earlier version, it won't have the Azure Resource Manager cmdlets described in this article.</span></span> <span data-ttu-id="5a5d8-107">For details, see:</span><span class="sxs-lookup"><span data-stu-id="5a5d8-107">For details, see:</span></span>

* <span data-ttu-id="5a5d8-108">[How to install and configure Azure PowerShell](install-configure-powershell.md) for instructions on setting up Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5a5d8-108">[How to install and configure Azure PowerShell](install-configure-powershell.md) for instructions on setting up Azure PowerShell.</span></span>
* <span data-ttu-id="5a5d8-109">[Using Windows PowerShell with Resource Manager](powershell-azure-resource-manager.md) for basics on using Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5a5d8-109">[Using Windows PowerShell with Resource Manager](powershell-azure-resource-manager.md) for basics on using Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="5a5d8-110">Most tasks require you to use an administrator-level Azure PowerShell command prompt.</span><span class="sxs-lookup"><span data-stu-id="5a5d8-110">Most tasks require you to use an administrator-level Azure PowerShell command prompt.</span></span>
> 
> 

## <a name="command-comparison"></a><span data-ttu-id="5a5d8-111">Command Comparison</span><span class="sxs-lookup"><span data-stu-id="5a5d8-111">Command Comparison</span></span>
<span data-ttu-id="5a5d8-112">This [table | section] shows the command syntax.</span><span class="sxs-lookup"><span data-stu-id="5a5d8-112">This [table | section] shows the command syntax.</span></span>

<!--[optional image - to use an image in this article, add a folder with the same name as the article file name without extension, inside the Media folder of the repo. Use only this folder to store the images. Don't attempt to use a common folder to share images you want to use in more than 1 file.]
Then, use the following syntax to add a reference to the image in your article:
![](./media/name-of-file-without-extension/image-name-no-spaces.png)
-->

<!--if a command string uses variables, define the variables first, using the  following construction. In some cases the variable is straightforward and doesn't need much explanation. But parameters such as location and size can benefit from brief explanation or listing all accepted values:--> 

<span data-ttu-id="5a5d8-113">These command examples use the following variables:</span><span class="sxs-lookup"><span data-stu-id="5a5d8-113">These command examples use the following variables:</span></span>

<span data-ttu-id="5a5d8-114">$FriendlyName"<Describe value>"</span><span class="sxs-lookup"><span data-stu-id="5a5d8-114">$FriendlyName"<Describe value>"</span></span>

<!-- if it makes more sense to present this in a table, use this. Otherwise, delete. The table won't render until it's in GitHub or published to Sandbox.-->

| <span data-ttu-id="5a5d8-115">Service Management</span><span class="sxs-lookup"><span data-stu-id="5a5d8-115">Service Management</span></span> | <span data-ttu-id="5a5d8-116">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5a5d8-116">Resource Manager</span></span> |
| --- | --- |
| `syntax` |`syntax` |

<!--if it makes more sense to present this one command block after the other instead of a table, use this. Otherwise, delete-->

<span data-ttu-id="5a5d8-117">[Short intro sentence about the command.</span><span class="sxs-lookup"><span data-stu-id="5a5d8-117">[Short intro sentence about the command.</span></span> <span data-ttu-id="5a5d8-118">Omit if there's really nothing to say.</span><span class="sxs-lookup"><span data-stu-id="5a5d8-118">Omit if there's really nothing to say.</span></span> <span data-ttu-id="5a5d8-119">But if it uses approaches such a the pipeline, explain that]:</span><span class="sxs-lookup"><span data-stu-id="5a5d8-119">But if it uses approaches such a the pipeline, explain that]:</span></span>

    [command string]

## <a name="script-examples"></a><span data-ttu-id="5a5d8-120">Script Examples</span><span class="sxs-lookup"><span data-stu-id="5a5d8-120">Script Examples</span></span>
<span data-ttu-id="5a5d8-121">Here's an example that uses [cmdlet names)] to [task].</span><span class="sxs-lookup"><span data-stu-id="5a5d8-121">Here's an example that uses [cmdlet names)] to [task].</span></span> <span data-ttu-id="5a5d8-122">It includes commands that:</span><span class="sxs-lookup"><span data-stu-id="5a5d8-122">It includes commands that:</span></span>

* <span data-ttu-id="5a5d8-123">[short verb, uses, has, is, etc]</span><span class="sxs-lookup"><span data-stu-id="5a5d8-123">[short verb, uses, has, is, etc]</span></span>
* <span data-ttu-id="5a5d8-124">[next short verb]</span><span class="sxs-lookup"><span data-stu-id="5a5d8-124">[next short verb]</span></span> 

<span data-ttu-id="5a5d8-125"><!--include this statement if it uses variables that weren't introduced earlier--> It includes the following variables:</span><span class="sxs-lookup"><span data-stu-id="5a5d8-125"><!--include this statement if it uses variables that weren't introduced earlier--> It includes the following variables:</span></span>

* <span data-ttu-id="5a5d8-126">[variable 1]</span><span class="sxs-lookup"><span data-stu-id="5a5d8-126">[variable 1]</span></span>
* <span data-ttu-id="5a5d8-127">[variable 2]</span><span class="sxs-lookup"><span data-stu-id="5a5d8-127">[variable 2]</span></span>

<!--This shows you how a recent example was presented as well as how it was formatted. Preceding each line with one tab or four spaces to format in a code block-->

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type the name and password of the local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="additional-resources"></a><span data-ttu-id="5a5d8-128">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="5a5d8-128">Additional Resources</span></span>
<span data-ttu-id="5a5d8-129"><!--At a minimum, include a link back to the migration task list article. Use the formats shown below. See create-links-markdown.md for more info -->
<!--use this format for links to other articles, such as the migration task list. -->
[Manage Availability](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="5a5d8-129"><!--At a minimum, include a link back to the migration task list article. Use the formats shown below. See create-links-markdown.md for more info -->
<!--use this format for links to other articles, such as the migration task list. -->
[Manage Availability](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<!--To link to an ACOM page outside the /documentation/ subdomain (such as a pricing page, SLA page or anything else that is not a documentation article), use an absolute URL, but omit the locale:

    [link text](http://azure.microsoft.com/pricing/details/virtual-machines/)-->

<span data-ttu-id="5a5d8-130"><!--use this for URLs outside of ACOM. Be sure to locale, and if you're linking to the Azure library on MSDN, include the '/azure/' part of the URL-->
[Virtual machines documentation](https://msdn.microsoft.com/library/azure/jj156003.aspx)</span><span class="sxs-lookup"><span data-stu-id="5a5d8-130"><!--use this for URLs outside of ACOM. Be sure to locale, and if you're linking to the Azure library on MSDN, include the '/azure/' part of the URL-->
[Virtual machines documentation](https://msdn.microsoft.com/library/azure/jj156003.aspx)</span></span>

