


## <a name="tagging-a-virtual-machine-through-templates"></a><span data-ttu-id="07896-101">Tagging a Virtual Machine through Templates</span><span class="sxs-lookup"><span data-stu-id="07896-101">Tagging a Virtual Machine through Templates</span></span>
<span data-ttu-id="07896-102">First, let’s look at tagging through templates.</span><span class="sxs-lookup"><span data-stu-id="07896-102">First, let’s look at tagging through templates.</span></span> <span data-ttu-id="07896-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on the following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span><span class="sxs-lookup"><span data-stu-id="07896-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on the following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span></span> <span data-ttu-id="07896-104">This template is for a Windows VM but can be adapted for Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="07896-104">This template is for a Windows VM but can be adapted for Linux VMs.</span></span>

<span data-ttu-id="07896-105">Click the **Deploy to Azure** button from the [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span><span class="sxs-lookup"><span data-stu-id="07896-105">Click the **Deploy to Azure** button from the [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span></span> <span data-ttu-id="07896-106">This will navigate to the [Azure portal](https://portal.azure.com/) where you can deploy this template.</span><span class="sxs-lookup"><span data-stu-id="07896-106">This will navigate to the [Azure portal](https://portal.azure.com/) where you can deploy this template.</span></span>

![Simple deployment with Tags](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-tag/deploy-to-azure-tags.png)

<span data-ttu-id="07896-108">This template includes the following tags: *Department*, *Application*, and *Created By*.</span><span class="sxs-lookup"><span data-stu-id="07896-108">This template includes the following tags: *Department*, *Application*, and *Created By*.</span></span> <span data-ttu-id="07896-109">You can add/edit these tags directly in the template if you would like different tag names.</span><span class="sxs-lookup"><span data-stu-id="07896-109">You can add/edit these tags directly in the template if you would like different tag names.</span></span>

![Azure tags in a template](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-tag/azure-tags-in-a-template.png)

<span data-ttu-id="07896-111">As you can see, the tags are defined as key/value pairs, separated by a colon (:).</span><span class="sxs-lookup"><span data-stu-id="07896-111">As you can see, the tags are defined as key/value pairs, separated by a colon (:).</span></span> <span data-ttu-id="07896-112">The tags must be defined in this format:</span><span class="sxs-lookup"><span data-stu-id="07896-112">The tags must be defined in this format:</span></span>

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

<span data-ttu-id="07896-113">Save the template file after you finish editing it with the tags of your choice.</span><span class="sxs-lookup"><span data-stu-id="07896-113">Save the template file after you finish editing it with the tags of your choice.</span></span>

<span data-ttu-id="07896-114">Next, in the **Edit Parameters** section, you can fill out the values for your tags.</span><span class="sxs-lookup"><span data-stu-id="07896-114">Next, in the **Edit Parameters** section, you can fill out the values for your tags.</span></span>

![Edit Tags in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

<span data-ttu-id="07896-116">Click **Create** to deploy this template with your tag values.</span><span class="sxs-lookup"><span data-stu-id="07896-116">Click **Create** to deploy this template with your tag values.</span></span>

## <a name="tagging-through-the-portal"></a><span data-ttu-id="07896-117">Tagging through the Portal</span><span class="sxs-lookup"><span data-stu-id="07896-117">Tagging through the Portal</span></span>
<span data-ttu-id="07896-118">After creating your resources with tags, you can view, add, and delete tags in the portal.</span><span class="sxs-lookup"><span data-stu-id="07896-118">After creating your resources with tags, you can view, add, and delete tags in the portal.</span></span>

<span data-ttu-id="07896-119">Select the tags icon to view your tags:</span><span class="sxs-lookup"><span data-stu-id="07896-119">Select the tags icon to view your tags:</span></span>

![Tags icon in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-tag/azure-portal-tags-icon.png)

<span data-ttu-id="07896-121">Add a new tag through the portal by defining your own Key/Value pair, and save it.</span><span class="sxs-lookup"><span data-stu-id="07896-121">Add a new tag through the portal by defining your own Key/Value pair, and save it.</span></span>

![Add new Tag in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

<span data-ttu-id="07896-123">Your new tag should now appear in the list of tags for your resource.</span><span class="sxs-lookup"><span data-stu-id="07896-123">Your new tag should now appear in the list of tags for your resource.</span></span>

![New Tag saved in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)







