

## <a name="azure-cli-20"></a><span data-ttu-id="d3e68-101">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d3e68-101">Azure CLI 2.0</span></span>

<span data-ttu-id="d3e68-102">Once you have [installed the Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2), use the `az vm image list` command to see a cached list of popular VM images.</span><span class="sxs-lookup"><span data-stu-id="d3e68-102">Once you have [installed the Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2), use the `az vm image list` command to see a cached list of popular VM images.</span></span> <span data-ttu-id="d3e68-103">For example, the following example of the command `az vm image list -o table` displays:</span><span class="sxs-lookup"><span data-stu-id="d3e68-103">For example, the following example of the command `az vm image list -o table` displays:</span></span>

```
You are viewing an offline list of images, use --all to retrieve an up-to-date list
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               14.04.4-LTS         Canonical:UbuntuServer:14.04.4-LTS:latest                       UbuntuLTS            latest
CentOS         OpenLogic               7.2                 OpenLogic:CentOS:7.2:latest                                     CentOS               latest
openSUSE       SUSE                    13.2                SUSE:openSUSE:13.2:latest                                       openSUSE             latest
RHEL           RedHat                  7.2                 RedHat:RHEL:7.2:latest                                          RHEL                 latest
SLES           SUSE                    12-SP1              SUSE:SLES:12-SP1:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

### <a name="finding-all-current-images"></a><span data-ttu-id="d3e68-104">Finding all current images</span><span class="sxs-lookup"><span data-stu-id="d3e68-104">Finding all current images</span></span>

<span data-ttu-id="d3e68-105">To obtain the current list of all images, use the `az vm image list` command with the `--all` option.</span><span class="sxs-lookup"><span data-stu-id="d3e68-105">To obtain the current list of all images, use the `az vm image list` command with the `--all` option.</span></span> <span data-ttu-id="d3e68-106">Unlike the Azure CLI 1.0 commands, the `az vm image list --all` command returns all images in **westus** by default (unless you specify a particular `--location` argument), so the `--all` command takes some time to complete.</span><span class="sxs-lookup"><span data-stu-id="d3e68-106">Unlike the Azure CLI 1.0 commands, the `az vm image list --all` command returns all images in **westus** by default (unless you specify a particular `--location` argument), so the `--all` command takes some time to complete.</span></span> <span data-ttu-id="d3e68-107">If you intend to investigate interactively, use `az vm image list --all > allImages.json`, which returns a list of all images currently available on Azure and stores it as a file for local use.</span><span class="sxs-lookup"><span data-stu-id="d3e68-107">If you intend to investigate interactively, use `az vm image list --all > allImages.json`, which returns a list of all images currently available on Azure and stores it as a file for local use.</span></span> 

<span data-ttu-id="d3e68-108">You can specify one of several options to restrict your search to a specific location, offer, publisher, or sku if you already have one or more in mind.</span><span class="sxs-lookup"><span data-stu-id="d3e68-108">You can specify one of several options to restrict your search to a specific location, offer, publisher, or sku if you already have one or more in mind.</span></span> <span data-ttu-id="d3e68-109">If you do not specify a location, the values for **westus** are returned.</span><span class="sxs-lookup"><span data-stu-id="d3e68-109">If you do not specify a location, the values for **westus** are returned.</span></span>

### <a name="find-specific-images"></a><span data-ttu-id="d3e68-110">Find specific images</span><span class="sxs-lookup"><span data-stu-id="d3e68-110">Find specific images</span></span>

<span data-ttu-id="d3e68-111">Use `az vm image list` with a [JMESPATH query filter](https://docs.microsoft.com/cli/azure/query-az-cli2) to find specific information.</span><span class="sxs-lookup"><span data-stu-id="d3e68-111">Use `az vm image list` with a [JMESPATH query filter](https://docs.microsoft.com/cli/azure/query-az-cli2) to find specific information.</span></span> <span data-ttu-id="d3e68-112">For example, the following displays the **sku**s that are available for **Debian** (remember that without the `--all` switch, it only searches the local cache of common images):</span><span class="sxs-lookup"><span data-stu-id="d3e68-112">For example, the following displays the **sku**s that are available for **Debian** (remember that without the `--all` switch, it only searches the local cache of common images):</span></span>

```azurecli
az vm image list --query '[?contains(offer,`Debian`)]' -o table --all
```

<span data-ttu-id="d3e68-113">The output is something like:</span><span class="sxs-lookup"><span data-stu-id="d3e68-113">The output is something like:</span></span> 
```
You are viewing an offline list of images, use --all to retrieve an up-to-date list
  Sku  Publisher    Offer    Urn                       Version    UrnAlias
-----  -----------  -------  ------------------------  ---------  ----------
    8  credativ     Debian   credativ:Debian:8:latest  latest     Debian

<list shortened for the example>
```

<span data-ttu-id="d3e68-114">If you know where you are deploying, you can use the general image search results along with the `az vm image list-skus`, `az vm image list-offers`, and `az vm image list-publishers` commands to find exactly what you want and where it can be deployed.</span><span class="sxs-lookup"><span data-stu-id="d3e68-114">If you know where you are deploying, you can use the general image search results along with the `az vm image list-skus`, `az vm image list-offers`, and `az vm image list-publishers` commands to find exactly what you want and where it can be deployed.</span></span> <span data-ttu-id="d3e68-115">For example, if from the preceding example you know that `credativ` has a Debian offer, you can then use the `--location` and other options to find exactly what you want.</span><span class="sxs-lookup"><span data-stu-id="d3e68-115">For example, if from the preceding example you know that `credativ` has a Debian offer, you can then use the `--location` and other options to find exactly what you want.</span></span> <span data-ttu-id="d3e68-116">The following example looks for a Debian 8 image in **westeurope**:</span><span class="sxs-lookup"><span data-stu-id="d3e68-116">The following example looks for a Debian 8 image in **westeurope**:</span></span>

```azurecli 
az vm image show -l westeurope -f debian -p credativ --skus 8 --version 8.0.201701180
```

<span data-ttu-id="d3e68-117">and the output is:</span><span class="sxs-lookup"><span data-stu-id="d3e68-117">and the output is:</span></span>

```json
{
  "dataDiskImages": [],
  "id": "/Subscriptions/<guid>/Providers/Microsoft.Compute/Locations/westeurope/Publishers/credativ/ArtifactTypes/VMImage/Offers/debian/Skus/8/Versions/8.0.201701180",
  "location": "westeurope",
  "name": "8.0.201701180",
  "osDiskImage": {
    "operatingSystem": "Linux"
  },
  "plan": null,
  "tags": null
}
```

## <a name="azure-cli-10"></a><span data-ttu-id="d3e68-118">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d3e68-118">Azure CLI 1.0</span></span> 

> [!NOTE]
> <span data-ttu-id="d3e68-119">This article describes how to navigate and select virtual machine images, using an installation of either the Azure CLI 1.0 or Azure PowerShell that supports the Azure resource manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="d3e68-119">This article describes how to navigate and select virtual machine images, using an installation of either the Azure CLI 1.0 or Azure PowerShell that supports the Azure resource manager deployment model.</span></span> <span data-ttu-id="d3e68-120">As a prerequisite, change to the Resource Manager mode.</span><span class="sxs-lookup"><span data-stu-id="d3e68-120">As a prerequisite, change to the Resource Manager mode.</span></span> <span data-ttu-id="d3e68-121">With the Azure CLI, enter that mode by typing `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="d3e68-121">With the Azure CLI, enter that mode by typing `azure config mode arm`.</span></span> 
> 

<span data-ttu-id="d3e68-122">The quickest way to locate an image is to call the `azure vm image list` command and pass the location, the publisher name (it's not case-sensitive!), and an offer -- if you know the offer.</span><span class="sxs-lookup"><span data-stu-id="d3e68-122">The quickest way to locate an image is to call the `azure vm image list` command and pass the location, the publisher name (it's not case-sensitive!), and an offer -- if you know the offer.</span></span> <span data-ttu-id="d3e68-123">For example, the following list is only a short example -- many lists are quite long -- if you know that "Canonical" is a publisher for the "UbuntuServer" offer.</span><span class="sxs-lookup"><span data-stu-id="d3e68-123">For example, the following list is only a short example -- many lists are quite long -- if you know that "Canonical" is a publisher for the "UbuntuServer" offer.</span></span>

```azurecli
azure vm image list westus canonical ubuntuserver
info:    Executing command vm image list
warn:    The parameter --sku if specified will be ignored
+ Getting virtual machine image skus (Publisher:"canonical" Offer:"ubuntuserver" Location:"westus")
data:    Publisher  Offer         Sku                OS     Version          Location  Urn
data:    ---------  ------------  -----------------  -----  ---------------  --------  --------------------------------------------------------
data:    canonical  ubuntuserver  16.04.0-LTS        Linux  16.04.201604203  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201604203
data:    canonical  ubuntuserver  16.04.0-LTS        Linux  16.04.201605161  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201605161
data:    canonical  ubuntuserver  16.04.0-LTS        Linux  16.04.201606100  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201606100
data:    canonical  ubuntuserver  16.04.0-LTS        Linux  16.04.201606270  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201606270
data:    canonical  ubuntuserver  16.04.0-LTS        Linux  16.04.201607210  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201607210
data:    canonical  ubuntuserver  16.04.0-LTS        Linux  16.04.201608150  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201608150
data:    canonical  ubuntuserver  16.10-DAILY        Linux  16.10.201607220  westus    canonical:ubuntuserver:16.10-DAILY:16.10.201607220
data:    canonical  ubuntuserver  16.10-DAILY        Linux  16.10.201607230  westus    canonical:ubuntuserver:16.10-DAILY:16.10.201607230
data:    canonical  ubuntuserver  16.10-DAILY        Linux  16.10.201607240  westus    canonical:ubuntuserver:16.10-DAILY:16.10.201607240
```

<span data-ttu-id="d3e68-124">The **Urn** column will be the form you pass to `azure vm quick-create`.</span><span class="sxs-lookup"><span data-stu-id="d3e68-124">The **Urn** column will be the form you pass to `azure vm quick-create`.</span></span>

<span data-ttu-id="d3e68-125">Often, however, you don't yet know what is available.</span><span class="sxs-lookup"><span data-stu-id="d3e68-125">Often, however, you don't yet know what is available.</span></span> <span data-ttu-id="d3e68-126">In this case, you can navigate images by using the `azure vm image list-publishers` command and specifying a data center location at the prompt.</span><span class="sxs-lookup"><span data-stu-id="d3e68-126">In this case, you can navigate images by using the `azure vm image list-publishers` command and specifying a data center location at the prompt.</span></span> <span data-ttu-id="d3e68-127">For example, the following lists all image publishers in the West US location (pass the location argument by lowercasing and removing spaces from the standard locations)</span><span class="sxs-lookup"><span data-stu-id="d3e68-127">For example, the following lists all image publishers in the West US location (pass the location argument by lowercasing and removing spaces from the standard locations)</span></span>

```azurecli
azure vm image list-publishers
info:    Executing command vm image list-publishers
Location: westus
+ Getting virtual machine and/or extension image publishers (Location: "westus")
data:    Publisher                                       Location
data:    ----------------------------------------------  --------
data:    a10networks                                     westus  
data:    aiscaler-cache-control-ddos-and-url-rewriting-  westus  
data:    alertlogic                                      westus  
data:    AlertLogic.Extension                            westus  
```

<span data-ttu-id="d3e68-128">These lists can be quite long, so the example list preceding is just a snippet.</span><span class="sxs-lookup"><span data-stu-id="d3e68-128">These lists can be quite long, so the example list preceding is just a snippet.</span></span> <span data-ttu-id="d3e68-129">Let's say that I noticed that Canonical is, indeed, an image publisher in the West US location.</span><span class="sxs-lookup"><span data-stu-id="d3e68-129">Let's say that I noticed that Canonical is, indeed, an image publisher in the West US location.</span></span> <span data-ttu-id="d3e68-130">You can now find their offers by calling `azure vm image list-offers` and pass the location and the publisher at the prompts, like the following example:</span><span class="sxs-lookup"><span data-stu-id="d3e68-130">You can now find their offers by calling `azure vm image list-offers` and pass the location and the publisher at the prompts, like the following example:</span></span>

```azurecli
azure vm image list-offers
info:    Executing command vm image list-offers
Location: westus
Publisher: canonical
+ Getting virtual machine image offers (Publisher: "canonical" Location:"westus")
data:    Publisher  Offer                      Location
data:    ---------  -------------------------  --------
data:    canonical  Ubuntu15.04Snappy          westus
data:    canonical  Ubuntu15.04SnappyDocker    westus
data:    canonical  UbunturollingSnappy        westus
data:    canonical  UbuntuServer               westus
data:    canonical  Ubuntu_Snappy_Core         westus
data:    canonical  Ubuntu_Snappy_Core_Docker  westus
info:    vm image list-offers command OK
```

<span data-ttu-id="d3e68-131">Now we know that in the West US region, Canonical publishes the **UbuntuServer** offer on Azure.</span><span class="sxs-lookup"><span data-stu-id="d3e68-131">Now we know that in the West US region, Canonical publishes the **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="d3e68-132">But what SKUs?</span><span class="sxs-lookup"><span data-stu-id="d3e68-132">But what SKUs?</span></span> <span data-ttu-id="d3e68-133">To get those values, you call `azure vm image list-skus` and respond to the prompt with the location, publisher, and offer that you have discovered.</span><span class="sxs-lookup"><span data-stu-id="d3e68-133">To get those values, you call `azure vm image list-skus` and respond to the prompt with the location, publisher, and offer that you have discovered.</span></span>

```azurecli
azure vm image list-skus
info:    Executing command vm image list-skus
Location: westus
Publisher: canonical
Offer: ubuntuserver
+ Getting virtual machine image skus (Publisher:"canonical" Offer:"ubuntuserver" Location:"westus")
data:    Publisher  Offer         sku                Location
data:    ---------  ------------  -----------------  --------
data:    canonical  ubuntuserver  12.04.2-LTS        westus
data:    canonical  ubuntuserver  12.04.3-LTS        westus
data:    canonical  ubuntuserver  12.04.4-LTS        westus
data:    canonical  ubuntuserver  12.04.5-DAILY-LTS  westus
data:    canonical  ubuntuserver  12.04.5-LTS        westus
data:    canonical  ubuntuserver  12.10              westus
data:    canonical  ubuntuserver  14.04-beta         westus
data:    canonical  ubuntuserver  14.04.0-LTS        westus
data:    canonical  ubuntuserver  14.04.1-LTS        westus
data:    canonical  ubuntuserver  14.04.2-LTS        westus
data:    canonical  ubuntuserver  14.04.3-LTS        westus
data:    canonical  ubuntuserver  14.04.4-DAILY-LTS  westus
data:    canonical  ubuntuserver  14.04.4-LTS        westus
data:    canonical  ubuntuserver  14.04.5-DAILY-LTS  westus
data:    canonical  ubuntuserver  14.04.5-LTS        westus
data:    canonical  ubuntuserver  14.10              westus
data:    canonical  ubuntuserver  14.10-beta         westus
data:    canonical  ubuntuserver  14.10-DAILY        westus
data:    canonical  ubuntuserver  15.04              westus
data:    canonical  ubuntuserver  15.04-beta         westus
data:    canonical  ubuntuserver  15.04-DAILY        westus
data:    canonical  ubuntuserver  15.10              westus
data:    canonical  ubuntuserver  15.10-alpha        westus
data:    canonical  ubuntuserver  15.10-beta         westus
data:    canonical  ubuntuserver  15.10-DAILY        westus
data:    canonical  ubuntuserver  16.04-alpha        westus
data:    canonical  ubuntuserver  16.04-beta         westus
data:    canonical  ubuntuserver  16.04.0-DAILY-LTS  westus
data:    canonical  ubuntuserver  16.04.0-LTS        westus
data:    canonical  ubuntuserver  16.10-DAILY        westus
info:    vm image list-skus command OK
```

<span data-ttu-id="d3e68-134">With this information, you can now find exactly the image you want by calling the original call at the top.</span><span class="sxs-lookup"><span data-stu-id="d3e68-134">With this information, you can now find exactly the image you want by calling the original call at the top.</span></span>

```azurecli
azure vm image list westus canonical ubuntuserver 16.04.0-LTS
info:    Executing command vm image list
+ Getting virtual machine images (Publisher:"canonical" Offer:"ubuntuserver" Sku: "16.04.0-LTS" Location:"westus")
data:    Publisher  Offer         Sku          OS     Version          Location  Urn
data:    ---------  ------------  -----------  -----  ---------------  --------  --------------------------------------------------
data:    canonical  ubuntuserver  16.04.0-LTS  Linux  16.04.201604203  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201604203
data:    canonical  ubuntuserver  16.04.0-LTS  Linux  16.04.201605161  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201605161
data:    canonical  ubuntuserver  16.04.0-LTS  Linux  16.04.201606100  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201606100
data:    canonical  ubuntuserver  16.04.0-LTS  Linux  16.04.201606270  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201606270
data:    canonical  ubuntuserver  16.04.0-LTS  Linux  16.04.201607210  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201607210
data:    canonical  ubuntuserver  16.04.0-LTS  Linux  16.04.201608150  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201608150
info:    vm image list command OK
```

<span data-ttu-id="d3e68-135">Now you can choose precisely the image you want to use.</span><span class="sxs-lookup"><span data-stu-id="d3e68-135">Now you can choose precisely the image you want to use.</span></span> <span data-ttu-id="d3e68-136">To create a virtual machine quickly by using the URN information, which you just found, or to use a template with that URN information, see [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="d3e68-136">To create a virtual machine quickly by using the URN information, which you just found, or to use a template with that URN information, see [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="d3e68-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3e68-137">PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="d3e68-138">Install and configure the [latest Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="d3e68-138">Install and configure the [latest Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="d3e68-139">If you are using Azure PowerShell modules below 1.0, you still use the following commands but you must first `Switch-AzureMode AzureResourceManager`.</span><span class="sxs-lookup"><span data-stu-id="d3e68-139">If you are using Azure PowerShell modules below 1.0, you still use the following commands but you must first `Switch-AzureMode AzureResourceManager`.</span></span> 
> 
> 

<span data-ttu-id="d3e68-140">When creating a new virtual machine with Azure Resource Manager, in some cases you need to specify an image with the combination of the following image properties:</span><span class="sxs-lookup"><span data-stu-id="d3e68-140">When creating a new virtual machine with Azure Resource Manager, in some cases you need to specify an image with the combination of the following image properties:</span></span>

* <span data-ttu-id="d3e68-141">Publisher</span><span class="sxs-lookup"><span data-stu-id="d3e68-141">Publisher</span></span>
* <span data-ttu-id="d3e68-142">Offer</span><span class="sxs-lookup"><span data-stu-id="d3e68-142">Offer</span></span>
* <span data-ttu-id="d3e68-143">SKU</span><span class="sxs-lookup"><span data-stu-id="d3e68-143">SKU</span></span>

<span data-ttu-id="d3e68-144">For example, these values are needed for the `Set-AzureRMVMSourceImage` PowerShell cmdlet or with a resource group template file in which you must specify the type of virtual machine to be created.</span><span class="sxs-lookup"><span data-stu-id="d3e68-144">For example, these values are needed for the `Set-AzureRMVMSourceImage` PowerShell cmdlet or with a resource group template file in which you must specify the type of virtual machine to be created.</span></span>

<span data-ttu-id="d3e68-145">If you need to determine these values, you can navigate the images to determine these values:</span><span class="sxs-lookup"><span data-stu-id="d3e68-145">If you need to determine these values, you can navigate the images to determine these values:</span></span>

1. <span data-ttu-id="d3e68-146">List the image publishers.</span><span class="sxs-lookup"><span data-stu-id="d3e68-146">List the image publishers.</span></span>
2. <span data-ttu-id="d3e68-147">For a given publisher, list their offers.</span><span class="sxs-lookup"><span data-stu-id="d3e68-147">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="d3e68-148">For a given offer, list their SKUs.</span><span class="sxs-lookup"><span data-stu-id="d3e68-148">For a given offer, list their SKUs.</span></span>

<span data-ttu-id="d3e68-149">First, list the publishers with the following commands:</span><span class="sxs-lookup"><span data-stu-id="d3e68-149">First, list the publishers with the following commands:</span></span>

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

<span data-ttu-id="d3e68-150">Fill in your chosen publisher name and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="d3e68-150">Fill in your chosen publisher name and run the following commands:</span></span>

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="d3e68-151">Fill in your chosen offer name and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="d3e68-151">Fill in your chosen offer name and run the following commands:</span></span>

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="d3e68-152">From the display of the `Get-AzureRMVMImageSku` command, you have all the information you need to specify the image for a new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="d3e68-152">From the display of the `Get-AzureRMVMImageSku` command, you have all the information you need to specify the image for a new virtual machine.</span></span>

<span data-ttu-id="d3e68-153">The following shows a full example:</span><span class="sxs-lookup"><span data-stu-id="d3e68-153">The following shows a full example:</span></span>

```powershell
PS C:\> $locName="West US"
PS C:\> Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

<span data-ttu-id="d3e68-154">For the "MicrosoftWindowsServer" publisher:</span><span class="sxs-lookup"><span data-stu-id="d3e68-154">For the "MicrosoftWindowsServer" publisher:</span></span>

```powershell
PS C:\> $pubName="MicrosoftWindowsServer"
PS C:\> Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer

Offer
-----
WindowsServer
```

<span data-ttu-id="d3e68-155">For the "WindowsServer" offer:</span><span class="sxs-lookup"><span data-stu-id="d3e68-155">For the "WindowsServer" offer:</span></span>

```powershell
PS C:\> $offerName="WindowsServer"
PS C:\> Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus

Skus
----
2008-R2-SP1
2012-Datacenter
2012-R2-Datacenter
2016-Nano-Server-Technical-Previe
2016-Technical-Preview-with-Conta
Windows-Server-Technical-Preview
```

<span data-ttu-id="d3e68-156">From this list, copy the chosen SKU name, and you have all the information for the `Set-AzureRMVMSourceImage` PowerShell cmdlet or for a resource group template.</span><span class="sxs-lookup"><span data-stu-id="d3e68-156">From this list, copy the chosen SKU name, and you have all the information for the `Set-AzureRMVMSourceImage` PowerShell cmdlet or for a resource group template.</span></span>

<!--Image references-->
[5]: ./media/markdown-template-for-new-articles/octocats.png
[6]: ./media/markdown-template-for-new-articles/pretty49.png
[7]: ./media/markdown-template-for-new-articles/channel-9.png
[8]: ./media/markdown-template-for-new-articles/copytemplate.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[gog]: http://google.com/
[yah]: http://search.yahoo.com/  
[msn]: http://search.msn.com/