


## <a name="using-vm-extensions"></a><span data-ttu-id="a9476-101">Using VM Extensions</span><span class="sxs-lookup"><span data-stu-id="a9476-101">Using VM Extensions</span></span>
<span data-ttu-id="a9476-102">Azure VM Extensions implement behaviors or features that either help other programs work on Azure VMs (for example, the **WebDeployForVSDevTest** extension allows Visual Studio to Web Deploy solutions on your Azure VM) or provide the ability for you to interact with the VM to support some other behavior (for example, you can use the VM Access extensions from PowerShell, the Azure CLI, and REST clients to reset or modify remote access values on your Azure VM).</span><span class="sxs-lookup"><span data-stu-id="a9476-102">Azure VM Extensions implement behaviors or features that either help other programs work on Azure VMs (for example, the **WebDeployForVSDevTest** extension allows Visual Studio to Web Deploy solutions on your Azure VM) or provide the ability for you to interact with the VM to support some other behavior (for example, you can use the VM Access extensions from PowerShell, the Azure CLI, and REST clients to reset or modify remote access values on your Azure VM).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9476-103">For a complete list of extensions by the features they support, see [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a9476-103">For a complete list of extensions by the features they support, see [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="a9476-104">Because each VM extension supports a specific feature, exactly what you can and cannot do with an extension depends on the extension.</span><span class="sxs-lookup"><span data-stu-id="a9476-104">Because each VM extension supports a specific feature, exactly what you can and cannot do with an extension depends on the extension.</span></span> <span data-ttu-id="a9476-105">Therefore, before modifying your VM, make sure you have read the documentation for the VM Extension you want to use.</span><span class="sxs-lookup"><span data-stu-id="a9476-105">Therefore, before modifying your VM, make sure you have read the documentation for the VM Extension you want to use.</span></span> <span data-ttu-id="a9476-106">Removing some VM Extensions is not supported; others have properties that can be set that change VM behavior radically.</span><span class="sxs-lookup"><span data-stu-id="a9476-106">Removing some VM Extensions is not supported; others have properties that can be set that change VM behavior radically.</span></span>
> 
> 

<span data-ttu-id="a9476-107">The most common tasks are:</span><span class="sxs-lookup"><span data-stu-id="a9476-107">The most common tasks are:</span></span>

1. <span data-ttu-id="a9476-108">Finding Available Extensions</span><span class="sxs-lookup"><span data-stu-id="a9476-108">Finding Available Extensions</span></span>
2. <span data-ttu-id="a9476-109">Updating Loaded Extensions</span><span class="sxs-lookup"><span data-stu-id="a9476-109">Updating Loaded Extensions</span></span>
3. <span data-ttu-id="a9476-110">Adding Extensions</span><span class="sxs-lookup"><span data-stu-id="a9476-110">Adding Extensions</span></span>
4. <span data-ttu-id="a9476-111">Removing Extensions</span><span class="sxs-lookup"><span data-stu-id="a9476-111">Removing Extensions</span></span>

## <a name="find-available-extensions"></a><span data-ttu-id="a9476-112">Find Available Extensions</span><span class="sxs-lookup"><span data-stu-id="a9476-112">Find Available Extensions</span></span>
<span data-ttu-id="a9476-113">You can locate extension and extended information using:</span><span class="sxs-lookup"><span data-stu-id="a9476-113">You can locate extension and extended information using:</span></span>

* <span data-ttu-id="a9476-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9476-114">PowerShell</span></span>
* <span data-ttu-id="a9476-115">Azure Cross-Platform Command Line Interface (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="a9476-115">Azure Cross-Platform Command Line Interface (Azure CLI)</span></span>
* <span data-ttu-id="a9476-116">Service Management REST API</span><span class="sxs-lookup"><span data-stu-id="a9476-116">Service Management REST API</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="a9476-117">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9476-117">Azure PowerShell</span></span>
<span data-ttu-id="a9476-118">Some extensions have PowerShell cmdlets that are specific to them, which may make their configuration from PowerShell easier; but the following cmdlets work for all VM extensions.</span><span class="sxs-lookup"><span data-stu-id="a9476-118">Some extensions have PowerShell cmdlets that are specific to them, which may make their configuration from PowerShell easier; but the following cmdlets work for all VM extensions.</span></span>

<span data-ttu-id="a9476-119">You can use the following cmdlets to obtain information about available extensions:</span><span class="sxs-lookup"><span data-stu-id="a9476-119">You can use the following cmdlets to obtain information about available extensions:</span></span>

* <span data-ttu-id="a9476-120">For instances of web roles or worker roles, you can use the [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a9476-120">For instances of web roles or worker roles, you can use the [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span></span>
* <span data-ttu-id="a9476-121">For instances of Virtual Machines, you can use the [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a9476-121">For instances of Virtual Machines, you can use the [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span></span>
  
   <span data-ttu-id="a9476-122">For example, the following code example shows how to list the information for the **IaaSDiagnostics** extension using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9476-122">For example, the following code example shows how to list the information for the **IaaSDiagnostics** extension using PowerShell.</span></span>
  
      PS C:\> Get-AzureVMAvailableExtension -ExtensionName IaaSDiagnostics
  
      Publisher                   : Microsoft.Azure.Diagnostics
      ExtensionName               : IaaSDiagnostics
      Version                     : 1.2
      Label                       : Microsoft Monitoring Agent Diagnostics
      Description                 : Microsoft Monitoring Agent Extension
      PublicConfigurationSchema   :
      PrivateConfigurationSchema  :
      IsInternalExtension         : False
      SampleConfig                :
      ReplicationCompleted        : True
      Eula                        :
      PrivacyUri                  :
      HomepageUri                 :
      IsJsonExtension             : True
      DisallowMajorVersionUpgrade : False
      SupportedOS                 :
      PublishedDate               :
      CompanyName                 :

### <a name="azure-command-line-interface-azure-cli"></a><span data-ttu-id="a9476-123">Azure Command Line Interface (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="a9476-123">Azure Command Line Interface (Azure CLI)</span></span>
<span data-ttu-id="a9476-124">Some extensions have Azure CLI commands that are specific to them (the Docker VM Extension is one example), which may make their configuration easier; but the following commands work for all VM extensions.</span><span class="sxs-lookup"><span data-stu-id="a9476-124">Some extensions have Azure CLI commands that are specific to them (the Docker VM Extension is one example), which may make their configuration easier; but the following commands work for all VM extensions.</span></span>

<span data-ttu-id="a9476-125">You can use the **azure vm extension list** command to obtain information about available extensions, and use the **–-json** option to display all available information about one or more extensions.</span><span class="sxs-lookup"><span data-stu-id="a9476-125">You can use the **azure vm extension list** command to obtain information about available extensions, and use the **–-json** option to display all available information about one or more extensions.</span></span> <span data-ttu-id="a9476-126">If you do not use an extension name, the command returns a JSON description of all available extensions.</span><span class="sxs-lookup"><span data-stu-id="a9476-126">If you do not use an extension name, the command returns a JSON description of all available extensions.</span></span>

<span data-ttu-id="a9476-127">For example, the following code example shows how to list the information for the **IaaSDiagnostics** extension using the Azure CLI **azure vm extension list** command and uses the **–-json** option to return complete information.</span><span class="sxs-lookup"><span data-stu-id="a9476-127">For example, the following code example shows how to list the information for the **IaaSDiagnostics** extension using the Azure CLI **azure vm extension list** command and uses the **–-json** option to return complete information.</span></span>

    $ azure vm extension list -n IaaSDiagnostics --json
    [
      {
        "publisher": "Microsoft.Azure.Diagnostics",
        "name": "IaaSDiagnostics",
        "version": "1.2",
        "label": "Microsoft Monitoring Agent Diagnostics",
        "description": "Microsoft Monitoring Agent Extension",
        "replicationCompleted": true,
        "isJsonExtension": true
      }
    ]



### <a name="service-management-rest-apis"></a><span data-ttu-id="a9476-128">Service Management REST APIs</span><span class="sxs-lookup"><span data-stu-id="a9476-128">Service Management REST APIs</span></span>
<span data-ttu-id="a9476-129">You can use the following REST APIs to obtain information about available extensions:</span><span class="sxs-lookup"><span data-stu-id="a9476-129">You can use the following REST APIs to obtain information about available extensions:</span></span>

* <span data-ttu-id="a9476-130">For instances of web roles or worker roles, you can use the [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span><span class="sxs-lookup"><span data-stu-id="a9476-130">For instances of web roles or worker roles, you can use the [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span> <span data-ttu-id="a9476-131">To list the versions of available extensions, you can use [List Extension Versions](https://msdn.microsoft.com/library/dn495437.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9476-131">To list the versions of available extensions, you can use [List Extension Versions](https://msdn.microsoft.com/library/dn495437.aspx).</span></span>
* <span data-ttu-id="a9476-132">For instances of Virtual Machines, you can use the [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span><span class="sxs-lookup"><span data-stu-id="a9476-132">For instances of Virtual Machines, you can use the [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span> <span data-ttu-id="a9476-133">To list the versions of available extensions, you can use [List Resource Extension Versions](https://msdn.microsoft.com/library/dn495440.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9476-133">To list the versions of available extensions, you can use [List Resource Extension Versions](https://msdn.microsoft.com/library/dn495440.aspx).</span></span>

## <a name="add-update-or-disable-extensions"></a><span data-ttu-id="a9476-134">Add, Update, or Disable Extensions</span><span class="sxs-lookup"><span data-stu-id="a9476-134">Add, Update, or Disable Extensions</span></span>
<span data-ttu-id="a9476-135">Extensions can be added when an instance is created or they can be added to a running instance.</span><span class="sxs-lookup"><span data-stu-id="a9476-135">Extensions can be added when an instance is created or they can be added to a running instance.</span></span> <span data-ttu-id="a9476-136">Extensions can be updated, disabled, or removed.</span><span class="sxs-lookup"><span data-stu-id="a9476-136">Extensions can be updated, disabled, or removed.</span></span> <span data-ttu-id="a9476-137">You can perform these actions by using Azure PowerShell cmdlets or by using the Service Management REST API operations.</span><span class="sxs-lookup"><span data-stu-id="a9476-137">You can perform these actions by using Azure PowerShell cmdlets or by using the Service Management REST API operations.</span></span> <span data-ttu-id="a9476-138">Parameters are required to install and set up some extensions.</span><span class="sxs-lookup"><span data-stu-id="a9476-138">Parameters are required to install and set up some extensions.</span></span> <span data-ttu-id="a9476-139">Public and private parameters are supported for extensions.</span><span class="sxs-lookup"><span data-stu-id="a9476-139">Public and private parameters are supported for extensions.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="a9476-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9476-140">Azure PowerShell</span></span>
<span data-ttu-id="a9476-141">Using Azure PowerShell cmdlets is the easiest way to add and update extensions.</span><span class="sxs-lookup"><span data-stu-id="a9476-141">Using Azure PowerShell cmdlets is the easiest way to add and update extensions.</span></span> <span data-ttu-id="a9476-142">When you use the extension cmdlets, most of the configuration of the extension is done for you.</span><span class="sxs-lookup"><span data-stu-id="a9476-142">When you use the extension cmdlets, most of the configuration of the extension is done for you.</span></span> <span data-ttu-id="a9476-143">At times, you may need to programmatically add an extension.</span><span class="sxs-lookup"><span data-stu-id="a9476-143">At times, you may need to programmatically add an extension.</span></span> <span data-ttu-id="a9476-144">When you need to do this, you must provide the configuration of the extension.</span><span class="sxs-lookup"><span data-stu-id="a9476-144">When you need to do this, you must provide the configuration of the extension.</span></span>

<span data-ttu-id="a9476-145">You can use the following cmdlets to know whether an extension requires a configuration of public and private parameters:</span><span class="sxs-lookup"><span data-stu-id="a9476-145">You can use the following cmdlets to know whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="a9476-146">For instances of web roles or worker roles, you can use the **Get-AzureServiceAvailableExtension** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a9476-146">For instances of web roles or worker roles, you can use the **Get-AzureServiceAvailableExtension** cmdlet.</span></span>
* <span data-ttu-id="a9476-147">For instances of Virtual Machines, you can use the **Get-AzureVMAvailableExtension** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a9476-147">For instances of Virtual Machines, you can use the **Get-AzureVMAvailableExtension** cmdlet.</span></span>

### <a name="service-management-rest-apis"></a><span data-ttu-id="a9476-148">Service Management REST APIs</span><span class="sxs-lookup"><span data-stu-id="a9476-148">Service Management REST APIs</span></span>
<span data-ttu-id="a9476-149">When you retrieve a listing of available extensions by using the REST APIs, you receive information about how the extension is to be configured.</span><span class="sxs-lookup"><span data-stu-id="a9476-149">When you retrieve a listing of available extensions by using the REST APIs, you receive information about how the extension is to be configured.</span></span> <span data-ttu-id="a9476-150">The information that is returned might show parameter information represented by a public schema and private schema.</span><span class="sxs-lookup"><span data-stu-id="a9476-150">The information that is returned might show parameter information represented by a public schema and private schema.</span></span> <span data-ttu-id="a9476-151">Public parameter values are returned in queries about the instances.</span><span class="sxs-lookup"><span data-stu-id="a9476-151">Public parameter values are returned in queries about the instances.</span></span> <span data-ttu-id="a9476-152">Private parameter values are not returned.</span><span class="sxs-lookup"><span data-stu-id="a9476-152">Private parameter values are not returned.</span></span>

<span data-ttu-id="a9476-153">You can use the following REST APIs to know whether an extension requires a configuration of public and private parameters:</span><span class="sxs-lookup"><span data-stu-id="a9476-153">You can use the following REST APIs to know whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="a9476-154">For instances of web roles or worker roles, the **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain the information in the response from the [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span><span class="sxs-lookup"><span data-stu-id="a9476-154">For instances of web roles or worker roles, the **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain the information in the response from the [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span>
* <span data-ttu-id="a9476-155">For instances of Virtual Machines, the **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain the information in the response from the [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span><span class="sxs-lookup"><span data-stu-id="a9476-155">For instances of Virtual Machines, the **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain the information in the response from the [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="a9476-156">Extensions can also use configurations that are defined with JSON.</span><span class="sxs-lookup"><span data-stu-id="a9476-156">Extensions can also use configurations that are defined with JSON.</span></span> <span data-ttu-id="a9476-157">When these types of extensions are used, only the **SampleConfig** element is used.</span><span class="sxs-lookup"><span data-stu-id="a9476-157">When these types of extensions are used, only the **SampleConfig** element is used.</span></span>
> 
> 

