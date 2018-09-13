
* [<span data-ttu-id="679e4-101">Quick-create a virtual machine in Azure</span><span class="sxs-lookup"><span data-stu-id="679e4-101">Quick-create a virtual machine in Azure</span></span>](#quick-create-a-vm-in-azure)
* [<span data-ttu-id="679e4-102">Deploy a virtual machine in Azure from a template</span><span class="sxs-lookup"><span data-stu-id="679e4-102">Deploy a virtual machine in Azure from a template</span></span>](#deploy-a-vm-in-azure-from-a-template)
* [<span data-ttu-id="679e4-103">Create a virtual machine from a custom image</span><span class="sxs-lookup"><span data-stu-id="679e4-103">Create a virtual machine from a custom image</span></span>](#create-a-custom-vm-image)
* [<span data-ttu-id="679e4-104">Deploy a virtual machine that uses a virtual network and a load balancer</span><span class="sxs-lookup"><span data-stu-id="679e4-104">Deploy a virtual machine that uses a virtual network and a load balancer</span></span>](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [<span data-ttu-id="679e4-105">Remove a resource group</span><span class="sxs-lookup"><span data-stu-id="679e4-105">Remove a resource group</span></span>](#remove-a-resource-group)
* [<span data-ttu-id="679e4-106">Show the log for a resource group deployment</span><span class="sxs-lookup"><span data-stu-id="679e4-106">Show the log for a resource group deployment</span></span>](#show-the-log-for-a-resource-group-deployment)
* [<span data-ttu-id="679e4-107">Display information about a virtual machine</span><span class="sxs-lookup"><span data-stu-id="679e4-107">Display information about a virtual machine</span></span>](#display-information-about-a-virtual-machine)
* [<span data-ttu-id="679e4-108">Connect to a Linux-based virtual machine</span><span class="sxs-lookup"><span data-stu-id="679e4-108">Connect to a Linux-based virtual machine</span></span>](#log-on-to-a-linux-based-virtual-machine)
* [<span data-ttu-id="679e4-109">Stop a virtual machine</span><span class="sxs-lookup"><span data-stu-id="679e4-109">Stop a virtual machine</span></span>](#stop-a-virtual-machine)
* [<span data-ttu-id="679e4-110">Start a virtual machine</span><span class="sxs-lookup"><span data-stu-id="679e4-110">Start a virtual machine</span></span>](#start-a-virtual-machine)
* [<span data-ttu-id="679e4-111">Attach a data disk</span><span class="sxs-lookup"><span data-stu-id="679e4-111">Attach a data disk</span></span>](#attach-a-data-disk)

## <a name="getting-ready"></a><span data-ttu-id="679e4-112">Getting ready</span><span class="sxs-lookup"><span data-stu-id="679e4-112">Getting ready</span></span>
<span data-ttu-id="679e4-113">Before you can use the Azure CLI with Azure resource groups, you need to have the right Azure CLI version and an Azure account.</span><span class="sxs-lookup"><span data-stu-id="679e4-113">Before you can use the Azure CLI with Azure resource groups, you need to have the right Azure CLI version and an Azure account.</span></span> <span data-ttu-id="679e4-114">If you don't have the Azure CLI, [install it](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="679e4-114">If you don't have the Azure CLI, [install it](../articles/cli-install-nodejs.md).</span></span>

### <a name="update-your-azure-cli-version-to-090-or-later"></a><span data-ttu-id="679e4-115">Update your Azure CLI version to 0.9.0 or later</span><span class="sxs-lookup"><span data-stu-id="679e4-115">Update your Azure CLI version to 0.9.0 or later</span></span>
<span data-ttu-id="679e4-116">Type `azure --version` to see whether you have already installed version 0.9.0 or later.</span><span class="sxs-lookup"><span data-stu-id="679e4-116">Type `azure --version` to see whether you have already installed version 0.9.0 or later.</span></span>

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

<span data-ttu-id="679e4-117">If your version is not 0.9.0 or later, you need to update it by using one of the native installers or through **npm** by typing `npm update -g azure-cli`.</span><span class="sxs-lookup"><span data-stu-id="679e4-117">If your version is not 0.9.0 or later, you need to update it by using one of the native installers or through **npm** by typing `npm update -g azure-cli`.</span></span>

<span data-ttu-id="679e4-118">You can also run Azure CLI as a Docker container by using the following [Docker image](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span><span class="sxs-lookup"><span data-stu-id="679e4-118">You can also run Azure CLI as a Docker container by using the following [Docker image](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span></span> <span data-ttu-id="679e4-119">From a Docker host, run the following command:</span><span class="sxs-lookup"><span data-stu-id="679e4-119">From a Docker host, run the following command:</span></span>

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="679e4-120">Set your Azure account and subscription</span><span class="sxs-lookup"><span data-stu-id="679e4-120">Set your Azure account and subscription</span></span>
<span data-ttu-id="679e4-121">If you don't already have an Azure subscription but you do have an MSDN subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="679e4-121">If you don't already have an Azure subscription but you do have an MSDN subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="679e4-122">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="679e4-122">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="679e4-123">Now [log in to your Azure account interactively](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) by typing `azure login` and following the prompts for an interactive login experience to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="679e4-123">Now [log in to your Azure account interactively](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) by typing `azure login` and following the prompts for an interactive login experience to your Azure account.</span></span> 

> [!NOTE]
> <span data-ttu-id="679e4-124">If you have a work or school ID and you know you do not have two-factor authentication enabled, you can **also** use `azure login -u` along with the work or school ID to log in *without* an interactive session.</span><span class="sxs-lookup"><span data-stu-id="679e4-124">If you have a work or school ID and you know you do not have two-factor authentication enabled, you can **also** use `azure login -u` along with the work or school ID to log in *without* an interactive session.</span></span> <span data-ttu-id="679e4-125">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to log in the same way.</span><span class="sxs-lookup"><span data-stu-id="679e4-125">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to log in the same way.</span></span>
>
>

<span data-ttu-id="679e4-126">Your account may have more than one subscription.</span><span class="sxs-lookup"><span data-stu-id="679e4-126">Your account may have more than one subscription.</span></span> <span data-ttu-id="679e4-127">You can list your subscriptions by typing `azure account list`, which might look something like this:</span><span class="sxs-lookup"><span data-stu-id="679e4-127">You can list your subscriptions by typing `azure account list`, which might look something like this:</span></span>

```azurecli
azure account list
info:    Executing command account list
data:    Name                              Id                                    Tenant Id                            Current
data:    --------------------------------  ------------------------------------  ------------------------------------  -------
data:    Contoso Admin                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  true
data:    Fabrikam dev                      xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Fabrikam test                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Contoso production                xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
```

<span data-ttu-id="679e4-128">You can set the current Azure subscription by typing the following.</span><span class="sxs-lookup"><span data-stu-id="679e4-128">You can set the current Azure subscription by typing the following.</span></span> <span data-ttu-id="679e4-129">Use the subscription name or the ID that has the resources you want to manage.</span><span class="sxs-lookup"><span data-stu-id="679e4-129">Use the subscription name or the ID that has the resources you want to manage.</span></span>

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-to-the-azure-cli-resource-group-mode"></a><span data-ttu-id="679e4-130">Switch to the Azure CLI resource group mode</span><span class="sxs-lookup"><span data-stu-id="679e4-130">Switch to the Azure CLI resource group mode</span></span>
<span data-ttu-id="679e4-131">By default, the Azure CLI starts in the service management mode (**asm** mode).</span><span class="sxs-lookup"><span data-stu-id="679e4-131">By default, the Azure CLI starts in the service management mode (**asm** mode).</span></span> <span data-ttu-id="679e4-132">Type the following to switch to resource group mode.</span><span class="sxs-lookup"><span data-stu-id="679e4-132">Type the following to switch to resource group mode.</span></span>

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a><span data-ttu-id="679e4-133">Understanding Azure resource templates and resource groups</span><span class="sxs-lookup"><span data-stu-id="679e4-133">Understanding Azure resource templates and resource groups</span></span>
<span data-ttu-id="679e4-134">Most applications are built from a combination of different resource types (such as one or more VMs and storage accounts, a SQL database, a virtual network, or a content delivery network).</span><span class="sxs-lookup"><span data-stu-id="679e4-134">Most applications are built from a combination of different resource types (such as one or more VMs and storage accounts, a SQL database, a virtual network, or a content delivery network).</span></span> <span data-ttu-id="679e4-135">The default Azure service management API and the Azure classic portal represented these items by using a service-by-service approach.</span><span class="sxs-lookup"><span data-stu-id="679e4-135">The default Azure service management API and the Azure classic portal represented these items by using a service-by-service approach.</span></span> <span data-ttu-id="679e4-136">This approach requires you to deploy and manage the individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span><span class="sxs-lookup"><span data-stu-id="679e4-136">This approach requires you to deploy and manage the individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span></span>

<span data-ttu-id="679e4-137">*Azure Resource Manager templates*, however, make it possible for you to deploy and manage these different resources as one logical deployment unit in a declarative fashion.</span><span class="sxs-lookup"><span data-stu-id="679e4-137">*Azure Resource Manager templates*, however, make it possible for you to deploy and manage these different resources as one logical deployment unit in a declarative fashion.</span></span> <span data-ttu-id="679e4-138">Instead of imperatively telling Azure what to deploy one command after another, you describe your entire deployment in a JSON file -- all of the resources and associated configuration and deployment parameters -- and tell Azure to deploy those resources as one group.</span><span class="sxs-lookup"><span data-stu-id="679e4-138">Instead of imperatively telling Azure what to deploy one command after another, you describe your entire deployment in a JSON file -- all of the resources and associated configuration and deployment parameters -- and tell Azure to deploy those resources as one group.</span></span>

<span data-ttu-id="679e4-139">You can then manage the overall life cycle of the group's resources by using Azure CLI resource management commands to:</span><span class="sxs-lookup"><span data-stu-id="679e4-139">You can then manage the overall life cycle of the group's resources by using Azure CLI resource management commands to:</span></span>

* <span data-ttu-id="679e4-140">Stop, start, or delete all of the resources within the group at once.</span><span class="sxs-lookup"><span data-stu-id="679e4-140">Stop, start, or delete all of the resources within the group at once.</span></span>
* <span data-ttu-id="679e4-141">Apply Role-Based Access Control (RBAC) rules to lock down security permissions on them.</span><span class="sxs-lookup"><span data-stu-id="679e4-141">Apply Role-Based Access Control (RBAC) rules to lock down security permissions on them.</span></span>
* <span data-ttu-id="679e4-142">Audit operations.</span><span class="sxs-lookup"><span data-stu-id="679e4-142">Audit operations.</span></span>
* <span data-ttu-id="679e4-143">Tag resources with additional metadata for better tracking.</span><span class="sxs-lookup"><span data-stu-id="679e4-143">Tag resources with additional metadata for better tracking.</span></span>

<span data-ttu-id="679e4-144">You can learn lots more about Azure resource groups and what they can do for you in the [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="679e4-144">You can learn lots more about Azure resource groups and what they can do for you in the [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="679e4-145">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../articles/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="679e4-145">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../articles/resource-group-authoring-templates.md).</span></span>

## <a id="quick-create-a-vm-in-azure"></a><span data-ttu-id="679e4-146">Task: Quick-create a VM in Azure</span><span class="sxs-lookup"><span data-stu-id="679e4-146">Task: Quick-create a VM in Azure</span></span>
<span data-ttu-id="679e4-147">Sometimes you know what image you need, and you need a VM from that image right now and you don't care too much about the infrastructure -- maybe you have to test something on a clean VM.</span><span class="sxs-lookup"><span data-stu-id="679e4-147">Sometimes you know what image you need, and you need a VM from that image right now and you don't care too much about the infrastructure -- maybe you have to test something on a clean VM.</span></span> <span data-ttu-id="679e4-148">That's when you want to use the `azure vm quick-create` command, and pass the arguments necessary to create a VM and its infrastructure.</span><span class="sxs-lookup"><span data-stu-id="679e4-148">That's when you want to use the `azure vm quick-create` command, and pass the arguments necessary to create a VM and its infrastructure.</span></span>

<span data-ttu-id="679e4-149">First, create your resource group.</span><span class="sxs-lookup"><span data-stu-id="679e4-149">First, create your resource group.</span></span>

```azurecli
azure group create coreos-quick westus
info:    Executing command group create
+ Getting resource group coreos-quick
+ Creating resource group coreos-quick
info:    Created resource group coreos-quick
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick
data:    Name:                coreos-quick
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="679e4-150">Second, you'll need an image.</span><span class="sxs-lookup"><span data-stu-id="679e4-150">Second, you'll need an image.</span></span> <span data-ttu-id="679e4-151">To find an image with the Azure CLI, see [Navigating and selecting Azure virtual machine images with PowerShell and the Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="679e4-151">To find an image with the Azure CLI, see [Navigating and selecting Azure virtual machine images with PowerShell and the Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="679e4-152">But for this article, here's a short list of popular images.</span><span class="sxs-lookup"><span data-stu-id="679e4-152">But for this article, here's a short list of popular images.</span></span> <span data-ttu-id="679e4-153">We'll use CoreOS's Stable image for this quick-create.</span><span class="sxs-lookup"><span data-stu-id="679e4-153">We'll use CoreOS's Stable image for this quick-create.</span></span>

> [!NOTE]
> <span data-ttu-id="679e4-154">For ComputeImageVersion, you can also simply supply 'latest' as the parameter in both the template language and in the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="679e4-154">For ComputeImageVersion, you can also simply supply 'latest' as the parameter in both the template language and in the Azure CLI.</span></span> <span data-ttu-id="679e4-155">This will allow you to always use the latest and patched version of the image without having to modify your scripts or templates.</span><span class="sxs-lookup"><span data-stu-id="679e4-155">This will allow you to always use the latest and patched version of the image without having to modify your scripts or templates.</span></span> <span data-ttu-id="679e4-156">This is shown below.</span><span class="sxs-lookup"><span data-stu-id="679e4-156">This is shown below.</span></span>
>
>

| <span data-ttu-id="679e4-157">PublisherName</span><span class="sxs-lookup"><span data-stu-id="679e4-157">PublisherName</span></span> | <span data-ttu-id="679e4-158">Offer</span><span class="sxs-lookup"><span data-stu-id="679e4-158">Offer</span></span> | <span data-ttu-id="679e4-159">Sku</span><span class="sxs-lookup"><span data-stu-id="679e4-159">Sku</span></span> | <span data-ttu-id="679e4-160">Version</span><span class="sxs-lookup"><span data-stu-id="679e4-160">Version</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="679e4-161">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="679e4-161">OpenLogic</span></span> |<span data-ttu-id="679e4-162">CentOS</span><span class="sxs-lookup"><span data-stu-id="679e4-162">CentOS</span></span> |<span data-ttu-id="679e4-163">7</span><span class="sxs-lookup"><span data-stu-id="679e4-163">7</span></span> |<span data-ttu-id="679e4-164">7.0.201503</span><span class="sxs-lookup"><span data-stu-id="679e4-164">7.0.201503</span></span> |
| <span data-ttu-id="679e4-165">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="679e4-165">OpenLogic</span></span> |<span data-ttu-id="679e4-166">CentOS</span><span class="sxs-lookup"><span data-stu-id="679e4-166">CentOS</span></span> |<span data-ttu-id="679e4-167">7.1</span><span class="sxs-lookup"><span data-stu-id="679e4-167">7.1</span></span> |<span data-ttu-id="679e4-168">7.1.201504</span><span class="sxs-lookup"><span data-stu-id="679e4-168">7.1.201504</span></span> |
| <span data-ttu-id="679e4-169">CoreOS</span><span class="sxs-lookup"><span data-stu-id="679e4-169">CoreOS</span></span> |<span data-ttu-id="679e4-170">CoreOS</span><span class="sxs-lookup"><span data-stu-id="679e4-170">CoreOS</span></span> |<span data-ttu-id="679e4-171">Beta</span><span class="sxs-lookup"><span data-stu-id="679e4-171">Beta</span></span> |<span data-ttu-id="679e4-172">647.0.0</span><span class="sxs-lookup"><span data-stu-id="679e4-172">647.0.0</span></span> |
| <span data-ttu-id="679e4-173">CoreOS</span><span class="sxs-lookup"><span data-stu-id="679e4-173">CoreOS</span></span> |<span data-ttu-id="679e4-174">CoreOS</span><span class="sxs-lookup"><span data-stu-id="679e4-174">CoreOS</span></span> |<span data-ttu-id="679e4-175">Stable</span><span class="sxs-lookup"><span data-stu-id="679e4-175">Stable</span></span> |<span data-ttu-id="679e4-176">633.1.0</span><span class="sxs-lookup"><span data-stu-id="679e4-176">633.1.0</span></span> |
| <span data-ttu-id="679e4-177">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="679e4-177">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="679e4-178">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="679e4-178">DynamicsNAV</span></span> |<span data-ttu-id="679e4-179">2015</span><span class="sxs-lookup"><span data-stu-id="679e4-179">2015</span></span> |<span data-ttu-id="679e4-180">8.0.40459</span><span class="sxs-lookup"><span data-stu-id="679e4-180">8.0.40459</span></span> |
| <span data-ttu-id="679e4-181">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="679e4-181">MicrosoftSharePoint</span></span> |<span data-ttu-id="679e4-182">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="679e4-182">MicrosoftSharePointServer</span></span> |<span data-ttu-id="679e4-183">2013</span><span class="sxs-lookup"><span data-stu-id="679e4-183">2013</span></span> |<span data-ttu-id="679e4-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="679e4-184">1.0.0</span></span> |
| <span data-ttu-id="679e4-185">msopentech</span><span class="sxs-lookup"><span data-stu-id="679e4-185">msopentech</span></span> |<span data-ttu-id="679e4-186">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="679e4-186">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="679e4-187">Standard</span><span class="sxs-lookup"><span data-stu-id="679e4-187">Standard</span></span> |<span data-ttu-id="679e4-188">1.0.0</span><span class="sxs-lookup"><span data-stu-id="679e4-188">1.0.0</span></span> |
| <span data-ttu-id="679e4-189">msopentech</span><span class="sxs-lookup"><span data-stu-id="679e4-189">msopentech</span></span> |<span data-ttu-id="679e4-190">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="679e4-190">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="679e4-191">Enterprise</span><span class="sxs-lookup"><span data-stu-id="679e4-191">Enterprise</span></span> |<span data-ttu-id="679e4-192">1.0.0</span><span class="sxs-lookup"><span data-stu-id="679e4-192">1.0.0</span></span> |
| <span data-ttu-id="679e4-193">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="679e4-193">MicrosoftSQLServer</span></span> |<span data-ttu-id="679e4-194">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="679e4-194">SQL2014-WS2012R2</span></span> |<span data-ttu-id="679e4-195">Enterprise-Optimized-for-DW</span><span class="sxs-lookup"><span data-stu-id="679e4-195">Enterprise-Optimized-for-DW</span></span> |<span data-ttu-id="679e4-196">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="679e4-196">12.0.2430</span></span> |
| <span data-ttu-id="679e4-197">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="679e4-197">MicrosoftSQLServer</span></span> |<span data-ttu-id="679e4-198">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="679e4-198">SQL2014-WS2012R2</span></span> |<span data-ttu-id="679e4-199">Enterprise-Optimized-for-OLTP</span><span class="sxs-lookup"><span data-stu-id="679e4-199">Enterprise-Optimized-for-OLTP</span></span> |<span data-ttu-id="679e4-200">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="679e4-200">12.0.2430</span></span> |
| <span data-ttu-id="679e4-201">Canonical</span><span class="sxs-lookup"><span data-stu-id="679e4-201">Canonical</span></span> |<span data-ttu-id="679e4-202">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="679e4-202">UbuntuServer</span></span> |<span data-ttu-id="679e4-203">12.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="679e4-203">12.04.5-LTS</span></span> |<span data-ttu-id="679e4-204">12.04.201504230</span><span class="sxs-lookup"><span data-stu-id="679e4-204">12.04.201504230</span></span> |
| <span data-ttu-id="679e4-205">Canonical</span><span class="sxs-lookup"><span data-stu-id="679e4-205">Canonical</span></span> |<span data-ttu-id="679e4-206">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="679e4-206">UbuntuServer</span></span> |<span data-ttu-id="679e4-207">14.04.2-LTS</span><span class="sxs-lookup"><span data-stu-id="679e4-207">14.04.2-LTS</span></span> |<span data-ttu-id="679e4-208">14.04.201503090</span><span class="sxs-lookup"><span data-stu-id="679e4-208">14.04.201503090</span></span> |
| <span data-ttu-id="679e4-209">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="679e4-209">MicrosoftWindowsServer</span></span> |<span data-ttu-id="679e4-210">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="679e4-210">WindowsServer</span></span> |<span data-ttu-id="679e4-211">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="679e4-211">2012-Datacenter</span></span> |<span data-ttu-id="679e4-212">3.0.201503</span><span class="sxs-lookup"><span data-stu-id="679e4-212">3.0.201503</span></span> |
| <span data-ttu-id="679e4-213">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="679e4-213">MicrosoftWindowsServer</span></span> |<span data-ttu-id="679e4-214">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="679e4-214">WindowsServer</span></span> |<span data-ttu-id="679e4-215">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="679e4-215">2012-R2-Datacenter</span></span> |<span data-ttu-id="679e4-216">4.0.201503</span><span class="sxs-lookup"><span data-stu-id="679e4-216">4.0.201503</span></span> |
| <span data-ttu-id="679e4-217">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="679e4-217">MicrosoftWindowsServer</span></span> |<span data-ttu-id="679e4-218">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="679e4-218">WindowsServer</span></span> |<span data-ttu-id="679e4-219">Windows-Server-Technical-Preview</span><span class="sxs-lookup"><span data-stu-id="679e4-219">Windows-Server-Technical-Preview</span></span> |<span data-ttu-id="679e4-220">5.0.201504</span><span class="sxs-lookup"><span data-stu-id="679e4-220">5.0.201504</span></span> |
| <span data-ttu-id="679e4-221">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="679e4-221">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="679e4-222">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="679e4-222">WindowsServerEssentials</span></span> |<span data-ttu-id="679e4-223">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="679e4-223">WindowsServerEssentials</span></span> |<span data-ttu-id="679e4-224">1.0.141204</span><span class="sxs-lookup"><span data-stu-id="679e4-224">1.0.141204</span></span> |
| <span data-ttu-id="679e4-225">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="679e4-225">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="679e4-226">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="679e4-226">WindowsServerHPCPack</span></span> |<span data-ttu-id="679e4-227">2012R2</span><span class="sxs-lookup"><span data-stu-id="679e4-227">2012R2</span></span> |<span data-ttu-id="679e4-228">4.3.4665</span><span class="sxs-lookup"><span data-stu-id="679e4-228">4.3.4665</span></span> |

<span data-ttu-id="679e4-229">Just create your VM by entering the `azure vm quick-create` command and being ready for the prompts.</span><span class="sxs-lookup"><span data-stu-id="679e4-229">Just create your VM by entering the `azure vm quick-create` command and being ready for the prompts.</span></span> <span data-ttu-id="679e4-230">It should look something like this:</span><span class="sxs-lookup"><span data-stu-id="679e4-230">It should look something like this:</span></span>

```azurecli
azure vm quick-create
info:    Executing command vm quick-create
Resource group name: coreos-quick
Virtual machine name: coreos
Location name: westus
Operating system Type [Windows, Linux]: linux
ImageURN (format: "publisherName:offer:skus:version"): coreos:coreos:stable:latest
User name: ops
Password: *********
Confirm password: *********
+ Looking up the VM "coreos"
info:    Using the VM Size "Standard_A1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in the region "westus", trying to create new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up the storage account cli9fd3fce49e9a9b3d14302
+ Looking up the NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up the virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing to create new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up the virtual network "coreo-westu-1430261891570-vnet"
+ Looking up the subnet "coreo-westu-1430261891570-snet" under the virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying to setup PublicIP profile
+ Looking up the public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up the public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up the NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up the VM "coreos"
+ Looking up the NIC "coreo-westu-1430261891570-nic"
+ Looking up the public ip "coreo-westu-1430261891570-pip"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Compute/virtualMachines/coreos
data:    ProvisioningState               :Succeeded
data:    Name                            :coreos
data:    Location                        :westus
data:    FQDN                            :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :coreos
data:        Offer                       :coreos
data:        Sku                         :stable
data:        Version                     :633.1.0
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :cli9fd3fce49e9a9b3d-os-1430261892283
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli9fd3fce49e9a9b3d14302.blob.core.windows.net/vhds/cli9fd3fce49e9a9b3d-os-1430261892283.vhd
data:
data:    OS Profile:
data:      Computer Name                 :coreos
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :false
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Network/networkInterfaces/coreo-westu-1430261891570-nic
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-30-72-E3
data:          Provisioning State        :Succeeded
data:          Name                      :coreo-westu-1430261891570-nic
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.1.4
data:            Public IP address       :104.40.24.124
data:            FQDN                    :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
info:    vm quick-create command OK
```

<span data-ttu-id="679e4-231">And away you go with your new VM.</span><span class="sxs-lookup"><span data-stu-id="679e4-231">And away you go with your new VM.</span></span>

## <a id="deploy-a-vm-in-azure-from-a-template"></a><span data-ttu-id="679e4-232">Task: Deploy a VM in Azure from a template</span><span class="sxs-lookup"><span data-stu-id="679e4-232">Task: Deploy a VM in Azure from a template</span></span>
<span data-ttu-id="679e4-233">Use the instructions in these sections to deploy a new Azure VM by using a template with the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="679e4-233">Use the instructions in these sections to deploy a new Azure VM by using a template with the Azure CLI.</span></span> <span data-ttu-id="679e4-234">This template creates a single virtual machine in a new virtual network with a single subnet, and unlike `azure vm quick-create`, enables you to describe what you want precisely and repeat it without errors.</span><span class="sxs-lookup"><span data-stu-id="679e4-234">This template creates a single virtual machine in a new virtual network with a single subnet, and unlike `azure vm quick-create`, enables you to describe what you want precisely and repeat it without errors.</span></span> <span data-ttu-id="679e4-235">Here's what this template creates:</span><span class="sxs-lookup"><span data-stu-id="679e4-235">Here's what this template creates:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-the-json-file-for-the-template-parameters"></a><span data-ttu-id="679e4-236">Step 1: Examine the JSON file for the template parameters</span><span class="sxs-lookup"><span data-stu-id="679e4-236">Step 1: Examine the JSON file for the template parameters</span></span>
<span data-ttu-id="679e4-237">Here are the contents of the JSON file for the template.</span><span class="sxs-lookup"><span data-stu-id="679e4-237">Here are the contents of the JSON file for the template.</span></span> <span data-ttu-id="679e4-238">(The template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="679e4-238">(The template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span></span>

<span data-ttu-id="679e4-239">Templates are flexible, so the designer may have chosen to give you lots of parameters or chosen to offer only a few by creating a template that is more fixed.</span><span class="sxs-lookup"><span data-stu-id="679e4-239">Templates are flexible, so the designer may have chosen to give you lots of parameters or chosen to offer only a few by creating a template that is more fixed.</span></span> <span data-ttu-id="679e4-240">In order to collect the information you need to pass the template as parameters, open the template file (this topic has a template inline, below) and examine the **parameters** values.</span><span class="sxs-lookup"><span data-stu-id="679e4-240">In order to collect the information you need to pass the template as parameters, open the template file (this topic has a template inline, below) and examine the **parameters** values.</span></span>

<span data-ttu-id="679e4-241">In this case, the template below will ask for:</span><span class="sxs-lookup"><span data-stu-id="679e4-241">In this case, the template below will ask for:</span></span>

* <span data-ttu-id="679e4-242">A unique storage account name.</span><span class="sxs-lookup"><span data-stu-id="679e4-242">A unique storage account name.</span></span>
* <span data-ttu-id="679e4-243">An admin user name for the VM.</span><span class="sxs-lookup"><span data-stu-id="679e4-243">An admin user name for the VM.</span></span>
* <span data-ttu-id="679e4-244">A password.</span><span class="sxs-lookup"><span data-stu-id="679e4-244">A password.</span></span>
* <span data-ttu-id="679e4-245">A domain name for the outside world to use.</span><span class="sxs-lookup"><span data-stu-id="679e4-245">A domain name for the outside world to use.</span></span>
* <span data-ttu-id="679e4-246">An Ubuntu Server version number -- but it will accept only one of a list.</span><span class="sxs-lookup"><span data-stu-id="679e4-246">An Ubuntu Server version number -- but it will accept only one of a list.</span></span>

<span data-ttu-id="679e4-247">See more about [username and password requirements](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="679e4-247">See more about [username and password requirements](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span>

<span data-ttu-id="679e4-248">Once you decide on these values, you're ready to create a group for and deploy this template into your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="679e4-248">Once you decide on these values, you're ready to create a group for and deploy this template into your Azure subscription.</span></span>

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for the storage account where the virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for the virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for the virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for the public IP used to access the virtual machine."
    }
    },
    "ubuntuOSVersion": {
    "type": "string",
    "defaultValue": "14.04.2-LTS",
    "allowedValues": [
        "12.04.5-LTS",
        "14.04.2-LTS",
        "15.04"
    ],
    "metadata": {
        "description": "The Ubuntu version for the VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
    }
    }
},
"variables": {
    "location": "West US",
    "imagePublisher": "Canonical",
    "imageOffer": "UbuntuServer",
    "OSDiskName": "osdiskforlinuxsimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyUbuntuVM",
    "vmSize": "Standard_D1",
    "virtualNetworkName": "MyVNET",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
},
"resources": [
    {
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[parameters('newStorageAccountName')]",
    "apiVersion": "2015-05-01-preview",
    "location": "[variables('location')]",
    "properties": {
        "accountType": "[variables('storageAccountType')]"
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/publicIPAddresses",
    "name": "[variables('publicIPAddressName')]",
    "location": "[variables('location')]",
    "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
        "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
        }
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[variables('virtualNetworkName')]",
    "location": "[variables('location')]",
    "properties": {
        "addressSpace": {
        "addressPrefixes": [
            "[variables('addressPrefix')]"
        ]
        },
        "subnets": [
        {
            "name": "[variables('subnetName')]",
            "properties": {
            "addressPrefix": "[variables('subnetPrefix')]"
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('nicName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
    ],
    "properties": {
        "ipConfigurations": [
        {
            "name": "ipconfig1",
            "properties": {
            "privateIPAllocationMethod": "Dynamic",
            "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
            },
            "subnet": {
                "id": "[variables('subnetRef')]"
            }
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', parameters('newStorageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
        "computername": "[variables('vmName')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
        "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('ubuntuOSVersion')]",
            "version": "latest"
        },
        "osDisk": {
            "name": "osdisk",
            "vhd": {
            "uri": "[concat('http://',parameters('newStorageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
        }
        },
        "networkProfile": {
        "networkInterfaces": [
            {
            "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
        ]
        }
    }
    }
]
}
```

### <a name="step-2-create-the-virtual-machine-by-using-the-template"></a><span data-ttu-id="679e4-249">Step 2: Create the virtual machine by using the template</span><span class="sxs-lookup"><span data-stu-id="679e4-249">Step 2: Create the virtual machine by using the template</span></span>
<span data-ttu-id="679e4-250">Once you have your parameter values ready, you must create a resource group for your template deployment and then deploy the template.</span><span class="sxs-lookup"><span data-stu-id="679e4-250">Once you have your parameter values ready, you must create a resource group for your template deployment and then deploy the template.</span></span>

<span data-ttu-id="679e4-251">To create the resource group, type `azure group create <group name> <location>` with the name of the group you want and the datacenter location into which you want to deploy.</span><span class="sxs-lookup"><span data-stu-id="679e4-251">To create the resource group, type `azure group create <group name> <location>` with the name of the group you want and the datacenter location into which you want to deploy.</span></span> <span data-ttu-id="679e4-252">This happens quickly:</span><span class="sxs-lookup"><span data-stu-id="679e4-252">This happens quickly:</span></span>

```azurecli
azure group create myResourceGroup westus
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="679e4-253">Now to create the deployment, call `azure group deployment create` and pass:</span><span class="sxs-lookup"><span data-stu-id="679e4-253">Now to create the deployment, call `azure group deployment create` and pass:</span></span>

* <span data-ttu-id="679e4-254">The template file (if you saved the above JSON template to a local file).</span><span class="sxs-lookup"><span data-stu-id="679e4-254">The template file (if you saved the above JSON template to a local file).</span></span>
* <span data-ttu-id="679e4-255">A template URI (if you want to point at the file in GitHub or some other web address).</span><span class="sxs-lookup"><span data-stu-id="679e4-255">A template URI (if you want to point at the file in GitHub or some other web address).</span></span>
* <span data-ttu-id="679e4-256">The resource group into which you want to deploy.</span><span class="sxs-lookup"><span data-stu-id="679e4-256">The resource group into which you want to deploy.</span></span>
* <span data-ttu-id="679e4-257">An optional deployment name.</span><span class="sxs-lookup"><span data-stu-id="679e4-257">An optional deployment name.</span></span>

<span data-ttu-id="679e4-258">You will be prompted to supply the values of parameters in the "parameters" section of the JSON file.</span><span class="sxs-lookup"><span data-stu-id="679e4-258">You will be prompted to supply the values of parameters in the "parameters" section of the JSON file.</span></span> <span data-ttu-id="679e4-259">When you have specified all the parameter values, your deployment will begin.</span><span class="sxs-lookup"><span data-stu-id="679e4-259">When you have specified all the parameter values, your deployment will begin.</span></span>

<span data-ttu-id="679e4-260">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="679e4-260">Here is an example:</span></span>

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for the following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

<span data-ttu-id="679e4-261">You will receive the following type of information:</span><span class="sxs-lookup"><span data-stu-id="679e4-261">You will receive the following type of information:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment to complete
data:    DeploymentName     : firstDeployment
data:    ResourceGroupName  : myResourceGroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T07:53:55.1828878Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  -------------
data:    newStorageAccountName  String        storageaccount
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameForPublicIP     String        newdomainname
data:    ubuntuOSVersion        String        14.10
info:    group deployment create command OK
```


## <a id="create-a-custom-vm-image"></a><span data-ttu-id="679e4-262">Task: Create a custom VM image</span><span class="sxs-lookup"><span data-stu-id="679e4-262">Task: Create a custom VM image</span></span>
<span data-ttu-id="679e4-263">You've seen the basic usage of templates above, so now we can use similar instructions to create a custom VM from a specific .vhd file in Azure by using a template via the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="679e4-263">You've seen the basic usage of templates above, so now we can use similar instructions to create a custom VM from a specific .vhd file in Azure by using a template via the Azure CLI.</span></span> <span data-ttu-id="679e4-264">The difference here is that this template creates a single virtual machine from a specified virtual hard disk (VHD).</span><span class="sxs-lookup"><span data-stu-id="679e4-264">The difference here is that this template creates a single virtual machine from a specified virtual hard disk (VHD).</span></span>

### <a name="step-1-examine-the-json-file-for-the-template"></a><span data-ttu-id="679e4-265">Step 1: Examine the JSON file for the template</span><span class="sxs-lookup"><span data-stu-id="679e4-265">Step 1: Examine the JSON file for the template</span></span>
<span data-ttu-id="679e4-266">Here are the contents of the JSON file for the template that this section uses as an example.</span><span class="sxs-lookup"><span data-stu-id="679e4-266">Here are the contents of the JSON file for the template that this section uses as an example.</span></span> <span data-ttu-id="679e4-267">(The template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="679e4-267">(The template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span></span>

<span data-ttu-id="679e4-268">Again, you will need to find the values you want to enter for the parameters that do not have default values.</span><span class="sxs-lookup"><span data-stu-id="679e4-268">Again, you will need to find the values you want to enter for the parameters that do not have default values.</span></span> <span data-ttu-id="679e4-269">When you run the `azure group deployment create` command, the Azure CLI will prompt you to enter those values.</span><span class="sxs-lookup"><span data-stu-id="679e4-269">When you run the `azure group deployment create` command, the Azure CLI will prompt you to enter those values.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters" : {
        "userImageStorageAccountName": {
            "type": "string",
            "defaultValue" : "userImageStorageAccountName"
        },
        "userImageStorageContainerName" : {
            "type" : "string",
            "defaultValue" : "userImageStorageContainerName"
        },
        "userImageVhdName" : {
            "type" : "string",
            "defaultValue" : "userImageVhdName"
        },
        "dnsNameForPublicIP" : {
            "type" : "string",
            "defaultValue": "uniqueDnsNameForPublicIP"
        },
        "adminUserName": {
            "type": "string"
        },
        "adminPassword": {
            "type": "securestring"
        },
        "osType" : {
            "type" : "string",
            "allowedValues" : [
                "windows",
                "linux"
            ]
        },
        "subscriptionId":{
            "type" : "string"
        },
        "location": {
            "type": "String",
            "defaultValue" : "West US"
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A2"
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue" : "myPublicIP"
        },
        "vmName": {
            "type": "string",
            "defaultValue" : "myVM"
        },
        "virtualNetworkName":{
            "type" : "string",
            "defaultValue" : "myVNET"
        },
        "nicName":{
            "type" : "string",
            "defaultValue":"myNIC"
        }
    },
    "variables": {
        "addressPrefix":"10.0.0.0/16",
        "subnet1Name": "Subnet-1",
        "subnet2Name": "Subnet-2",
        "subnet1Prefix" : "10.0.0.0/24",
        "subnet2Prefix" : "10.0.1.0/24",
        "publicIPAddressType" : "Dynamic",
        "vnetID":"[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",
        "subnet1Ref" : "[concat(variables('vnetID'),'/subnets/',variables('subnet1Name'))]",
        "userImageName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('userImageVhdName'))]",
        "osDiskVhdName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('vmName'),'osDisk.vhd')]"
    },
    "resources": [
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[parameters('publicIPAddressName')]",
        "location": "[parameters('location')]",
        "properties": {
            "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
            }
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/virtualNetworks",
        "name": "[parameters('virtualNetworkName')]",
        "location": "[parameters('location')]",
        "properties": {
        "addressSpace": {
            "addressPrefixes": [
            "[variables('addressPrefix')]"
            ]
        },
        "subnets": [
            {
            "name": "[variables('subnet1Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet1Prefix')]"
            }
            },
            {
            "name": "[variables('subnet2Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet2Prefix')]"
            }
            }
        ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/networkInterfaces",
        "name": "[parameters('nicName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]",
            "[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]"
        ],
        "properties": {
            "ipConfigurations": [
            {
                "name": "ipconfig1",
                "properties": {
                    "privateIPAllocationMethod": "Dynamic",
                    "publicIPAddress": {
                        "id": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]"
                    },
                    "subnet": {
                        "id": "[variables('subnet1Ref')]"
                    }
                }
            }
            ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Compute/virtualMachines",
        "name": "[parameters('vmName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/networkInterfaces/', parameters('nicName'))]"
        ],
        "properties": {
            "hardwareProfile": {
                "vmSize": "[parameters('vmSize')]"
            },
            "osProfile": {
                "computername": "[parameters('vmName')]",
                "adminUsername": "[parameters('adminUsername')]",
                "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
                "osDisk" : {
                    "name" : "[concat(parameters('vmName'),'-osDisk')]",
                    "osType" : "[parameters('osType')]",
                    "caching" : "ReadWrite",
                    "image" : {
                        "uri" : "[variables('userImageName')]"
                    },
                    "vhd" : {
                        "uri" : "[variables('osDiskVhdName')]"
                    }
                }
            },
            "networkProfile": {
                "networkInterfaces" : [
                {
                    "id": "[resourceId('Microsoft.Network/networkInterfaces',parameters('nicName'))]"
                }
                ]
            }
        }
    }
    ]
}
```

### <a name="step-2-obtain-the-vhd"></a><span data-ttu-id="679e4-270">Step 2: Obtain the VHD</span><span class="sxs-lookup"><span data-stu-id="679e4-270">Step 2: Obtain the VHD</span></span>
<span data-ttu-id="679e4-271">Obviously, you'll need a .vhd for this.</span><span class="sxs-lookup"><span data-stu-id="679e4-271">Obviously, you'll need a .vhd for this.</span></span> <span data-ttu-id="679e4-272">You can use one you already have in Azure, or you can upload one.</span><span class="sxs-lookup"><span data-stu-id="679e4-272">You can use one you already have in Azure, or you can upload one.</span></span>

<span data-ttu-id="679e4-273">For a Windows-based virtual machine, see [Create and upload a Windows Server VHD to Azure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="679e4-273">For a Windows-based virtual machine, see [Create and upload a Windows Server VHD to Azure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="679e4-274">For a Linux-based virtual machine, see [Creating and uploading a virtual hard disk that contains the Linux operating system](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="679e4-274">For a Linux-based virtual machine, see [Creating and uploading a virtual hard disk that contains the Linux operating system](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

### <a name="step-3-create-the-virtual-machine-by-using-the-template"></a><span data-ttu-id="679e4-275">Step 3: Create the virtual machine by using the template</span><span class="sxs-lookup"><span data-stu-id="679e4-275">Step 3: Create the virtual machine by using the template</span></span>
<span data-ttu-id="679e4-276">Now you're ready to create a new virtual machine based on the .vhd.</span><span class="sxs-lookup"><span data-stu-id="679e4-276">Now you're ready to create a new virtual machine based on the .vhd.</span></span> <span data-ttu-id="679e4-277">Create a group to deploy into, by using `azure group create <location>`:</span><span class="sxs-lookup"><span data-stu-id="679e4-277">Create a group to deploy into, by using `azure group create <location>`:</span></span>

```azurecli
azure group create myResourceGroupUser eastus
info:    Executing command group create
+ Getting resource group myResourceGroupUser
+ Creating resource group myResourceGroupUser
info:    Created resource group myResourceGroupUser
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupUser
data:    Name:                myResourceGroupUser
data:    Location:            eastus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="679e4-278">Then create the deployment by using the `--template-uri` option to call in the template directly (or you can use the `--template-file` option to use a file that you have saved locally).</span><span class="sxs-lookup"><span data-stu-id="679e4-278">Then create the deployment by using the `--template-uri` option to call in the template directly (or you can use the `--template-file` option to use a file that you have saved locally).</span></span> <span data-ttu-id="679e4-279">Note that because the template has defaults specified, you are prompted for only a few things.</span><span class="sxs-lookup"><span data-stu-id="679e4-279">Note that because the template has defaults specified, you are prompted for only a few things.</span></span> <span data-ttu-id="679e4-280">If you deploy the template in different places, you may find that some naming collisions occur with the default values (particularly the DNS name you create).</span><span class="sxs-lookup"><span data-stu-id="679e4-280">If you deploy the template in different places, you may find that some naming collisions occur with the default values (particularly the DNS name you create).</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for the following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

<span data-ttu-id="679e4-281">Output looks something like the following:</span><span class="sxs-lookup"><span data-stu-id="679e4-281">Output looks something like the following:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment to complete
error:   Deployment provisioning state was not successful
data:    DeploymentName     : customVhdDeployment
data:    ResourceGroupName  : myResourceGroupUser
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T14:55:48.0963829Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                           Type          Value
data:    -----------------------------  ------------  ------------------------------------
data:    userImageStorageAccountName    String        userImageStorageAccountName
data:    userImageStorageContainerName  String        userImageStorageContainerName
data:    userImageVhdName               String        userImageVhdName
data:    dnsNameForPublicIP             String        uniqueDnsNameForPublicIP
data:    adminUserName                  String        ops
data:    adminPassword                  SecureString  undefined
data:    osType                         String        linux
data:    subscriptionId                 String        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
data:    location                       String        West US
data:    vmSize                         String        Standard_A2
data:    publicIPAddressName            String        myPublicIP
data:    vmName                         String        myVM
data:    virtualNetworkName             String        myVNET
data:    nicName                        String        myNIC
info:    group deployment create command OK
```

## <a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a><span data-ttu-id="679e4-282">Task: Deploy a multi-VM application that uses a virtual network and an external load balancer</span><span class="sxs-lookup"><span data-stu-id="679e4-282">Task: Deploy a multi-VM application that uses a virtual network and an external load balancer</span></span>
<span data-ttu-id="679e4-283">This template allows you to create two virtual machines under a load balancer and configure a load-balancing rule on Port 80.</span><span class="sxs-lookup"><span data-stu-id="679e4-283">This template allows you to create two virtual machines under a load balancer and configure a load-balancing rule on Port 80.</span></span> <span data-ttu-id="679e4-284">This template also deploys a storage account, virtual network, public IP address, availability set, and network interfaces.</span><span class="sxs-lookup"><span data-stu-id="679e4-284">This template also deploys a storage account, virtual network, public IP address, availability set, and network interfaces.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

<span data-ttu-id="679e4-285">Follow these steps to deploy a multi-VM application that uses a virtual network and a load balancer by using a Resource Manager template in the GitHub template repository via Azure PowerShell commands.</span><span class="sxs-lookup"><span data-stu-id="679e4-285">Follow these steps to deploy a multi-VM application that uses a virtual network and a load balancer by using a Resource Manager template in the GitHub template repository via Azure PowerShell commands.</span></span>

### <a name="step-1-examine-the-json-file-for-the-template"></a><span data-ttu-id="679e4-286">Step 1: Examine the JSON file for the template</span><span class="sxs-lookup"><span data-stu-id="679e4-286">Step 1: Examine the JSON file for the template</span></span>
<span data-ttu-id="679e4-287">Here are the contents of the JSON file for the template.</span><span class="sxs-lookup"><span data-stu-id="679e4-287">Here are the contents of the JSON file for the template.</span></span> <span data-ttu-id="679e4-288">If you want the most recent version, it's located [at the GitHub repository for templates](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="679e4-288">If you want the most recent version, it's located [at the GitHub repository for templates](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span></span> <span data-ttu-id="679e4-289">This topic uses the `--template-uri` switch to call in the template, but you can also use the `--template-file` switch to pass a local version.</span><span class="sxs-lookup"><span data-stu-id="679e4-289">This topic uses the `--template-uri` switch to call in the template, but you can also use the `--template-file` switch to pass a local version.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location of resources"
            }
        },
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of storage account"
            }
        },
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "Admin user name"
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Admin password"
            }
        },
        "dnsNameforLBIP": {
            "type": "string",
            "metadata": {
                "description": "DNS for load balancer IP"
            }
        },
        "backendPort": {
            "type": "int",
            "defaultValue": 3389,
            "metadata": {
                "description": "Back-end port"
            }
        },
        "vmNamePrefix": {
            "type": "string",
            "defaultValue": "myVM",
            "metadata": {
                "description": "Prefix to use for VM names"
            }
        },
        "vmSourceImageName": {
            "type": "string",
            "defaultValue": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201412.01-en.us-127GB.vhd"
        },
        "lbName": {
            "type": "string",
            "defaultValue": "myLB",
            "metadata": {
                "description": "Load balancer name"
            }
        },
        "nicNamePrefix": {
            "type": "string",
            "defaultValue": "nic",
            "metadata": {
                "description": "Network interface name prefix"
            }
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue": "myPublicIP",
            "metadata": {
                "description": "Public IP name"
            }
        },
        "vnetName": {
            "type": "string",
            "defaultValue": "myVNET",
            "metadata": {
                "description": "Virtual network name"
            }
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A1",
            "metadata": {
                "description": "Size of the VM"
            }
        }
    },
    "variables": {
        "storageAccountType": "Standard_LRS",
        "vmStorageAccountContainerName": "vhds",
        "availabilitySetName": "myAvSet",
        "addressPrefix": "10.0.0.0/16",
        "subnetName": "Subnet-1",
        "subnetPrefix": "10.0.0.0/24",
        "publicIPAddressType": "Dynamic",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('vnetName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables ('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',parameters('lbName'))]",
        "numberOfInstances": 2,
        "nicId1": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 0))]",
        "nicId2": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 1))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/LBFE')]",
        "backEndIPConfigID1": "[concat(variables('nicId1'),'/ipConfigurations/ipconfig1')]",
        "backEndIPConfigID2": "[concat(variables('nicId2'),'/ipConfigurations/ipconfig1')]",
        "sourceImageName": "[concat('/', subscription().subscriptionId,'/services/images/',parameters('vmSourceImageName'))]",
        "lbPoolID": "[concat(variables('lbID'),'/backendAddressPools/LBBE')]",
        "lbProbeID": "[concat(variables('lbID'),'/probes/tcpProbe')]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('storageAccountName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": { }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/publicIPAddresses",
            "name": "[parameters('publicIPAddressName')]",
            "location": "[parameters('location')]",
            "properties": {
                "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
                "dnsSettings": {
                    "domainNameLabel": "[parameters('dnsNameforLBIP')]"
                }
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/virtualNetworks",
            "name": "[parameters('vnetName')]",
            "location": "[parameters('location')]",
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "[variables('addressPrefix')]"
                    ]
                },
                "subnets": [
                    {
                        "name": "[variables('subnetName')]",
                        "properties": {
                            "addressPrefix": "[variables('subnetPrefix')]"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/networkInterfaces",
            "name": "[concat(parameters('nicNamePrefix'), copyindex())]",
            "location": "[parameters('location')]",
            "copy": {
                "name": "nicLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "dependsOn": [
                "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
            ],
            "properties": {
                "ipConfigurations": [
                    {
                        "name": "ipconfig1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "subnet": {
                                "id": "[variables('subnetRef')]"
                            }
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/backendAddressPools/LBBE')]"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/inboundNatRule/RDP-VM', copyindex())]"
                            }
                        ]


                    }
                ]

            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "name": "[parameters('lbName')]",
            "type": "Microsoft.Network/loadBalancers",
            "location": "[parameters('location')]",
            "dependsOn": [
                "nicLoop",
                "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]"
            ],
            "properties": {
                "frontendIPConfigurations": [
                    {
                        "name": "LBFE",
                        "properties": {
                            "publicIPAddress": {
                                "id": "[variables('publicIPAddressID')]"
                            }
                        }
                    }
                ],
                "backendAddressPools": [
                    {
                        "name": "LBBE"

                    }
                ],
                "inboundNatRules": [
                    {
                        "name": "RDP-VM1",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50001,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    },
                    {
                        "name": "RDP-VM2",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50002,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    }
                ],
                "loadBalancingRules": [
                    {
                        "name": "LBRule",
                        "properties": {
                            "frontendIPConfiguration": {
                                "id": "[variables('frontEndIPConfigID')]"
                            },
                            "backendAddressPool": {
                                "id": "[variables('lbPoolID')]"
                            },
                            "protocol": "tcp",
                            "frontendPort": 80,
                            "backendPort": 80,
                            "enableFloatingIP": false,
                            "idleTimeoutInMinutes": 5,
                            "probe": {
                                "id": "[variables('lbProbeID')]"
                            }
                        }
                    }
                ],
                "probes": [
                    {
                        "name": "tcpProbe",
                        "properties": {
                            "protocol": "tcp",
                            "port": 80,
                            "intervalInSeconds": "5",
                            "numberOfProbes": "2"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[concat(parameters('vmNamePrefix'), copyindex())]",
            "copy": {
                "name": "virtualMachineLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "location": "[parameters('location')]",
            "dependsOn": [
                "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]",
                "[concat('Microsoft.Network/networkInterfaces/', parameters('nicNamePrefix'), copyindex())]",
                "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]"
            ],
            "properties": {
                "availabilitySet": {
                    "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
                },
                "hardwareProfile": {
                    "vmSize": "[parameters('vmSize')]"
                },
                "osProfile": {
                    "computername": "[concat(parameters('vmNamePrefix'), copyIndex())]",
                    "adminUsername": "[parameters('adminUsername')]",
                    "adminPassword": "[parameters('adminPassword')]"
                },
                "storageProfile": {
                    "sourceImage": {
                        "id": "[variables('sourceImageName')]"
                    },
                    "destinationVhdsContainer": "[concat('http://',parameters('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/')]"
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'),copyindex()))]"
                        }
                    ]
                }
            }
        }
    ]
}
```

### <a name="step-2-create-the-deployment-by-using-the-template"></a><span data-ttu-id="679e4-290">Step 2: Create the deployment by using the template</span><span class="sxs-lookup"><span data-stu-id="679e4-290">Step 2: Create the deployment by using the template</span></span>
<span data-ttu-id="679e4-291">Create a resource group for the template by using `azure group create <location>`.</span><span class="sxs-lookup"><span data-stu-id="679e4-291">Create a resource group for the template by using `azure group create <location>`.</span></span> <span data-ttu-id="679e4-292">Then, create a deployment into that resource group by using `azure group deployment create` and passing the resource group, passing a deployment name, and answering the prompts for parameters in the template that did not have default values.</span><span class="sxs-lookup"><span data-stu-id="679e4-292">Then, create a deployment into that resource group by using `azure group deployment create` and passing the resource group, passing a deployment name, and answering the prompts for parameters in the template that did not have default values.</span></span>

```azurecli
azure group create lbgroup westus
info:    Executing command group create
+ Getting resource group lbgroup
+ Creating resource group lbgroup
info:    Created resource group lbgroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/lbgroup
data:    Name:                lbgroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="679e4-293">Now use the `azure group deployment create` command and the `--template-uri` option to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="679e4-293">Now use the `azure group deployment create` command and the `--template-uri` option to deploy the template.</span></span> <span data-ttu-id="679e4-294">Be ready with your parameter values when it prompts you, as shown below.</span><span class="sxs-lookup"><span data-stu-id="679e4-294">Be ready with your parameter values when it prompts you, as shown below.</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for the following parameters
location: westus
newStorageAccountName: storagename
adminUsername: ops
adminPassword: password
dnsNameforLBIP: lbdomainname
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "newdeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.compute
info:    Registering provider microsoft.network
+ Waiting for deployment to complete
data:    DeploymentName     : newdeployment
data:    ResourceGroupName  : lbgroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T20:58:40.1678876Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  ----------------------
data:    location               String        westus
data:    newStorageAccountName  String        storagename
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameforLBIP         String        lbdomainname
data:    backendPort            Int           3389
data:    vmNamePrefix           String        myVM
data:    imagePublisher         String        MicrosoftWindowsServer
data:    imageOffer             String        WindowsServer
data:    imageSKU               String        2012-R2-Datacenter
data:    lbName                 String        myLB
data:    nicNamePrefix          String        nic
data:    publicIPAddressName    String        myPublicIP
data:    vnetName               String        myVNET
data:    vmSize                 String        Standard_A1
info:    group deployment create command OK
```

<span data-ttu-id="679e4-295">Note that this template deploys a Windows Server image; however, it could easily be replaced by any Linux image.</span><span class="sxs-lookup"><span data-stu-id="679e4-295">Note that this template deploys a Windows Server image; however, it could easily be replaced by any Linux image.</span></span> <span data-ttu-id="679e4-296">Want to create a Docker cluster with multiple swarm managers?</span><span class="sxs-lookup"><span data-stu-id="679e4-296">Want to create a Docker cluster with multiple swarm managers?</span></span> <span data-ttu-id="679e4-297">[You can do it](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span><span class="sxs-lookup"><span data-stu-id="679e4-297">[You can do it](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span></span>

## <a id="remove-a-resource-group"></a><span data-ttu-id="679e4-298">Task: Remove a resource group</span><span class="sxs-lookup"><span data-stu-id="679e4-298">Task: Remove a resource group</span></span>
<span data-ttu-id="679e4-299">Remember that you can redeploy to a resource group, but if you are done with one, you can delete it by using `azure group delete <group name>`.</span><span class="sxs-lookup"><span data-stu-id="679e4-299">Remember that you can redeploy to a resource group, but if you are done with one, you can delete it by using `azure group delete <group name>`.</span></span>

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <a id="show-the-log-for-a-resource-group-deployment"></a><span data-ttu-id="679e4-300">Task: Show the log for a resource group deployment</span><span class="sxs-lookup"><span data-stu-id="679e4-300">Task: Show the log for a resource group deployment</span></span>
<span data-ttu-id="679e4-301">This one is common while you're creating or using templates.</span><span class="sxs-lookup"><span data-stu-id="679e4-301">This one is common while you're creating or using templates.</span></span> <span data-ttu-id="679e4-302">The call to display the deployment logs for a group is `azure group log show <groupname>`, which displays quite a bit of information that's useful for understanding why something happened -- or didn't.</span><span class="sxs-lookup"><span data-stu-id="679e4-302">The call to display the deployment logs for a group is `azure group log show <groupname>`, which displays quite a bit of information that's useful for understanding why something happened -- or didn't.</span></span> <span data-ttu-id="679e4-303">(For more information on troubleshooting your deployments, as well as other information about issues, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span><span class="sxs-lookup"><span data-stu-id="679e4-303">(For more information on troubleshooting your deployments, as well as other information about issues, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span></span>

<span data-ttu-id="679e4-304">To target specific failures, for example, you might use tools like **jq** to query things a bit more precisely, such as which individual failures you need to correct.</span><span class="sxs-lookup"><span data-stu-id="679e4-304">To target specific failures, for example, you might use tools like **jq** to query things a bit more precisely, such as which individual failures you need to correct.</span></span> <span data-ttu-id="679e4-305">The following example uses **jq** to parse a deployment log for **lbgroup**, looking for failures.</span><span class="sxs-lookup"><span data-stu-id="679e4-305">The following example uses **jq** to parse a deployment log for **lbgroup**, looking for failures.</span></span>

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
<span data-ttu-id="679e4-306">You can discover very quickly what went wrong, fix, and retry.</span><span class="sxs-lookup"><span data-stu-id="679e4-306">You can discover very quickly what went wrong, fix, and retry.</span></span> <span data-ttu-id="679e4-307">In the following case, the template had been creating two VMs at the same time, which created a lock on the .vhd.</span><span class="sxs-lookup"><span data-stu-id="679e4-307">In the following case, the template had been creating two VMs at the same time, which created a lock on the .vhd.</span></span> <span data-ttu-id="679e4-308">(After we modified the template, the deployment succeeded quickly.)</span><span class="sxs-lookup"><span data-stu-id="679e4-308">(After we modified the template, the deployment succeeded quickly.)</span></span>

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"The resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed to acquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <a id="display-information-about-a-virtual-machine"></a><span data-ttu-id="679e4-309">Task: Display information about a virtual machine</span><span class="sxs-lookup"><span data-stu-id="679e4-309">Task: Display information about a virtual machine</span></span>
<span data-ttu-id="679e4-310">You can see information about specific VMs in your resource group by using the `azure vm show <groupname> <vmname>` command.</span><span class="sxs-lookup"><span data-stu-id="679e4-310">You can see information about specific VMs in your resource group by using the `azure vm show <groupname> <vmname>` command.</span></span> <span data-ttu-id="679e4-311">If you have more than one VM in your group, you might first need to list the VMs in a group by using `azure vm list <groupname>`.</span><span class="sxs-lookup"><span data-stu-id="679e4-311">If you have more than one VM in your group, you might first need to list the VMs in a group by using `azure vm list <groupname>`.</span></span>

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

<span data-ttu-id="679e4-312">And then, looking up myVM1:</span><span class="sxs-lookup"><span data-stu-id="679e4-312">And then, looking up myVM1:</span></span>

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up the VM "myVM1"
+ Looking up the NIC "nic1"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Failed
data:    Name                            :myVM1
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :MicrosoftWindowsServer
data:        Offer                       :WindowsServer
data:        Sku                         :2012-R2-Datacenter
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Windows
data:        Name                        :osdisk
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :http://zoostorageralph.blob.core.windows.net/vhds/osdisk.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Windows Configuration:
data:        Provision VM Agent          :true
data:        Enable automatic updates    :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Network/networkInterfaces/nic1
data:          Primary                   :false
data:          Provisioning State        :Succeeded
data:          Name                      :nic1
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.0.5
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/availabilitySets/MYAVSET
info:    vm show command OK
```

> [!NOTE]
> <span data-ttu-id="679e4-313">If you want to programmatically store and manipulate the output of your console commands, you may want to use a JSON parsing tool such as **[jq](https://github.com/stedolan/jq)** or **[jsawk](https://github.com/micha/jsawk)**, or language libraries that are good for the task.</span><span class="sxs-lookup"><span data-stu-id="679e4-313">If you want to programmatically store and manipulate the output of your console commands, you may want to use a JSON parsing tool such as **[jq](https://github.com/stedolan/jq)** or **[jsawk](https://github.com/micha/jsawk)**, or language libraries that are good for the task.</span></span>
>
>

## <a id="log-on-to-a-linux-based-virtual-machine"></a><span data-ttu-id="679e4-314">Task: Log on to a Linux-based virtual machine</span><span class="sxs-lookup"><span data-stu-id="679e4-314">Task: Log on to a Linux-based virtual machine</span></span>
<span data-ttu-id="679e4-315">Typically Linux machines are connected to through SSH.</span><span class="sxs-lookup"><span data-stu-id="679e4-315">Typically Linux machines are connected to through SSH.</span></span> <span data-ttu-id="679e4-316">For more information, see [How to use SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="679e4-316">For more information, see [How to use SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a id="stop-a-virtual-machine"></a><span data-ttu-id="679e4-317">Task: Stop a VM</span><span class="sxs-lookup"><span data-stu-id="679e4-317">Task: Stop a VM</span></span>
<span data-ttu-id="679e4-318">Run this command:</span><span class="sxs-lookup"><span data-stu-id="679e4-318">Run this command:</span></span>

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> <span data-ttu-id="679e4-319">Use this parameter to keep the virtual IP (VIP) of the vnet in case it's the last VM in that vnet.</span><span class="sxs-lookup"><span data-stu-id="679e4-319">Use this parameter to keep the virtual IP (VIP) of the vnet in case it's the last VM in that vnet.</span></span> <br><br> <span data-ttu-id="679e4-320">If you use the `StayProvisioned` parameter, you'll still be billed for the VM.</span><span class="sxs-lookup"><span data-stu-id="679e4-320">If you use the `StayProvisioned` parameter, you'll still be billed for the VM.</span></span>
>
>

## <a id="start-a-virtual-machine"></a><span data-ttu-id="679e4-321">Task: Start a VM</span><span class="sxs-lookup"><span data-stu-id="679e4-321">Task: Start a VM</span></span>
<span data-ttu-id="679e4-322">Run this command:</span><span class="sxs-lookup"><span data-stu-id="679e4-322">Run this command:</span></span>

```azurecli
azure vm start <group name> <virtual machine name>
```

## <a id="attach-a-data-disk"></a><span data-ttu-id="679e4-323">Task: Attach a data disk</span><span class="sxs-lookup"><span data-stu-id="679e4-323">Task: Attach a data disk</span></span>
<span data-ttu-id="679e4-324">You'll also need to decide whether to attach a new disk or one that contains data.</span><span class="sxs-lookup"><span data-stu-id="679e4-324">You'll also need to decide whether to attach a new disk or one that contains data.</span></span> <span data-ttu-id="679e4-325">For a new disk, the command creates the .vhd file and attaches it in the same command.</span><span class="sxs-lookup"><span data-stu-id="679e4-325">For a new disk, the command creates the .vhd file and attaches it in the same command.</span></span>

<span data-ttu-id="679e4-326">To attach a new disk, run this command:</span><span class="sxs-lookup"><span data-stu-id="679e4-326">To attach a new disk, run this command:</span></span>

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

<span data-ttu-id="679e4-327">To attach an existing data disk, run this command:</span><span class="sxs-lookup"><span data-stu-id="679e4-327">To attach an existing data disk, run this command:</span></span>

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

<span data-ttu-id="679e4-328">Then you'll need to mount the disk, as you normally would in Linux.</span><span class="sxs-lookup"><span data-stu-id="679e4-328">Then you'll need to mount the disk, as you normally would in Linux.</span></span>

## <a name="next-steps"></a><span data-ttu-id="679e4-329">Next steps</span><span class="sxs-lookup"><span data-stu-id="679e4-329">Next steps</span></span>
<span data-ttu-id="679e4-330">For far more examples of Azure CLI usage with the **arm** mode, see [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="679e4-330">For far more examples of Azure CLI usage with the **arm** mode, see [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span></span> <span data-ttu-id="679e4-331">To learn more about Azure resources and their concepts, see [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="679e4-331">To learn more about Azure resources and their concepts, see [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="679e4-332">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/) and [Application frameworks using templates](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="679e4-332">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/) and [Application frameworks using templates](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


