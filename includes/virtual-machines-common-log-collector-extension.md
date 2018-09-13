
<span data-ttu-id="68121-101">Diagnosing issues with an Microsoft Azure cloud service requires collecting the service’s log files on virtual machines as the issues occur.</span><span class="sxs-lookup"><span data-stu-id="68121-101">Diagnosing issues with an Microsoft Azure cloud service requires collecting the service’s log files on virtual machines as the issues occur.</span></span> <span data-ttu-id="68121-102">You can use the AzureLogCollector extension on-demand to perfom one-time collection of logs from one or more Cloud Service VMs (from both web roles and worker roles) and transfer the collected files to an Azure storage account – all without remotely logging on to any of the VMs.</span><span class="sxs-lookup"><span data-stu-id="68121-102">You can use the AzureLogCollector extension on-demand to perfom one-time collection of logs from one or more Cloud Service VMs (from both web roles and worker roles) and transfer the collected files to an Azure storage account – all without remotely logging on to any of the VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="68121-103">Descriptions for most of the logged information can be found at http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span><span class="sxs-lookup"><span data-stu-id="68121-103">Descriptions for most of the logged information can be found at http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span></span>
> 
> 

<span data-ttu-id="68121-104">There are two modes of collection dependent on the types of files to be collected.</span><span class="sxs-lookup"><span data-stu-id="68121-104">There are two modes of collection dependent on the types of files to be collected.</span></span>

* <span data-ttu-id="68121-105">Azure Guest Agent Logs only (GA).</span><span class="sxs-lookup"><span data-stu-id="68121-105">Azure Guest Agent Logs only (GA).</span></span> <span data-ttu-id="68121-106">This collection mode includes all the logs related to Azure guest agents and other Azure components.</span><span class="sxs-lookup"><span data-stu-id="68121-106">This collection mode includes all the logs related to Azure guest agents and other Azure components.</span></span>
* <span data-ttu-id="68121-107">All Logs (Full).</span><span class="sxs-lookup"><span data-stu-id="68121-107">All Logs (Full).</span></span> <span data-ttu-id="68121-108">This collection mode will collect all files in GA mode plus:</span><span class="sxs-lookup"><span data-stu-id="68121-108">This collection mode will collect all files in GA mode plus:</span></span>
  
  * <span data-ttu-id="68121-109">system and application event logs</span><span class="sxs-lookup"><span data-stu-id="68121-109">system and application event logs</span></span>
  * <span data-ttu-id="68121-110">HTTP error logs</span><span class="sxs-lookup"><span data-stu-id="68121-110">HTTP error logs</span></span>
  * <span data-ttu-id="68121-111">IIS Logs</span><span class="sxs-lookup"><span data-stu-id="68121-111">IIS Logs</span></span>
  * <span data-ttu-id="68121-112">Setup logs</span><span class="sxs-lookup"><span data-stu-id="68121-112">Setup logs</span></span>
  * <span data-ttu-id="68121-113">other system logs</span><span class="sxs-lookup"><span data-stu-id="68121-113">other system logs</span></span>

<span data-ttu-id="68121-114">In both collection modes, additional data collection folders can be specified by using a collection of the following structure:</span><span class="sxs-lookup"><span data-stu-id="68121-114">In both collection modes, additional data collection folders can be specified by using a collection of the following structure:</span></span>

* <span data-ttu-id="68121-115">**Name**: The name of the collection, which will be used as the name of subfolder inside the zip file to be collected.</span><span class="sxs-lookup"><span data-stu-id="68121-115">**Name**: The name of the collection, which will be used as the name of subfolder inside the zip file to be collected.</span></span>
* <span data-ttu-id="68121-116">**Location**: The path to the folder on the virtual machine where file will be collected.</span><span class="sxs-lookup"><span data-stu-id="68121-116">**Location**: The path to the folder on the virtual machine where file will be collected.</span></span>
* <span data-ttu-id="68121-117">**SearchPattern**: The pattern of the names of files to be collected.</span><span class="sxs-lookup"><span data-stu-id="68121-117">**SearchPattern**: The pattern of the names of files to be collected.</span></span> <span data-ttu-id="68121-118">Default is “\*”</span><span class="sxs-lookup"><span data-stu-id="68121-118">Default is “\*”</span></span>
* <span data-ttu-id="68121-119">**Recursive**: if the files will be collected recursively under the folder.</span><span class="sxs-lookup"><span data-stu-id="68121-119">**Recursive**: if the files will be collected recursively under the folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68121-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="68121-120">Prerequisites</span></span>
* <span data-ttu-id="68121-121">You need to have a storage account for extension to save generated zip files.</span><span class="sxs-lookup"><span data-stu-id="68121-121">You need to have a storage account for extension to save generated zip files.</span></span>
* <span data-ttu-id="68121-122">You must make sure that you are using Azure PowerShell Cmdlets V0.8.0 or above.</span><span class="sxs-lookup"><span data-stu-id="68121-122">You must make sure that you are using Azure PowerShell Cmdlets V0.8.0 or above.</span></span> <span data-ttu-id="68121-123">For more information, see [Azure Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="68121-123">For more information, see [Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>

## <a name="add-the-extension"></a><span data-ttu-id="68121-124">Add the extension</span><span class="sxs-lookup"><span data-stu-id="68121-124">Add the extension</span></span>
<span data-ttu-id="68121-125">You can use [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets or [Service Management REST APIs](https://msdn.microsoft.com/library/ee460799.aspx) to add the AzureLogCollector extension.</span><span class="sxs-lookup"><span data-stu-id="68121-125">You can use [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets or [Service Management REST APIs](https://msdn.microsoft.com/library/ee460799.aspx) to add the AzureLogCollector extension.</span></span>

<span data-ttu-id="68121-126">For Cloud Services, the existing Azure Powershell cmdlet, **Set-AzureServiceExtension**, can be used to enable the extension on Cloud Service role instances.</span><span class="sxs-lookup"><span data-stu-id="68121-126">For Cloud Services, the existing Azure Powershell cmdlet, **Set-AzureServiceExtension**, can be used to enable the extension on Cloud Service role instances.</span></span> <span data-ttu-id="68121-127">Every time this extension is enabled through this cmdlet, log collection is triggered on the selected role instances of selected roles.</span><span class="sxs-lookup"><span data-stu-id="68121-127">Every time this extension is enabled through this cmdlet, log collection is triggered on the selected role instances of selected roles.</span></span>

<span data-ttu-id="68121-128">For Virtual Machines, the existing Azure Powershell cmdlet, **Set-AzureVMExtension**, can be used to enable the extension on Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="68121-128">For Virtual Machines, the existing Azure Powershell cmdlet, **Set-AzureVMExtension**, can be used to enable the extension on Virtual Machines.</span></span> <span data-ttu-id="68121-129">Every time this extension is enabled through the cmdlets, log collection is triggered on each instance.</span><span class="sxs-lookup"><span data-stu-id="68121-129">Every time this extension is enabled through the cmdlets, log collection is triggered on each instance.</span></span>

<span data-ttu-id="68121-130">Internally, this extension uses the JSON-based PublicConfiguration and PrivateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="68121-130">Internally, this extension uses the JSON-based PublicConfiguration and PrivateConfiguration.</span></span> <span data-ttu-id="68121-131">The following is the layout of a sample JSON for public and private configuration.</span><span class="sxs-lookup"><span data-stu-id="68121-131">The following is the layout of a sample JSON for public and private configuration.</span></span>

### <a name="publicconfiguration"></a><span data-ttu-id="68121-132">PublicConfiguration</span><span class="sxs-lookup"><span data-stu-id="68121-132">PublicConfiguration</span></span>
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri to your storage account with sp=wl",
        "AdditionalData":
        [
          {
                  "Name":  "StorageData",
                  "Location":  "%roleroot%storage",
                  "SearchPattern":  "*.*",
                  "Recursive":  "true"
          },
          {
                "Name":  "CustomDataFolder2",
                "Location":  "c:\customFolder",
                "SearchPattern":  "*.log",
                "Recursive":  "false"
          },
        ]
    }

### <a name="privateconfiguration"></a><span data-ttu-id="68121-133">PrivateConfiguration</span><span class="sxs-lookup"><span data-stu-id="68121-133">PrivateConfiguration</span></span>
    {

    }

> [!NOTE]
> <span data-ttu-id="68121-134">This extension doesn’t need **privateConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="68121-134">This extension doesn’t need **privateConfiguration**.</span></span> <span data-ttu-id="68121-135">You can just provide an empty structure for the **–PrivateConfiguration** argument.</span><span class="sxs-lookup"><span data-stu-id="68121-135">You can just provide an empty structure for the **–PrivateConfiguration** argument.</span></span>
> 
> 

<span data-ttu-id="68121-136">You can follow one of the two following steps to add the AzureLogCollector to one or more instances of a Cloud Service or Virtual Machine of selected roles, which triggers the collections on each VM to run and send the collected files to Azure account specified.</span><span class="sxs-lookup"><span data-stu-id="68121-136">You can follow one of the two following steps to add the AzureLogCollector to one or more instances of a Cloud Service or Virtual Machine of selected roles, which triggers the collections on each VM to run and send the collected files to Azure account specified.</span></span>

## <a name="adding-as-a-service-extension"></a><span data-ttu-id="68121-137">Adding as a Service Extension</span><span class="sxs-lookup"><span data-stu-id="68121-137">Adding as a Service Extension</span></span>
1. <span data-ttu-id="68121-138">Follow the instructions to connect Azure PowerShell to your subscription.</span><span class="sxs-lookup"><span data-stu-id="68121-138">Follow the instructions to connect Azure PowerShell to your subscription.</span></span>
2. <span data-ttu-id="68121-139">Specify the service name, slot, roles, and role instances to which you want to add and enable the AzureLogCollector extension.</span><span class="sxs-lookup"><span data-stu-id="68121-139">Specify the service name, slot, roles, and role instances to which you want to add and enable the AzureLogCollector extension.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify the slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified the roles on which the extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify the instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify the collection mode, "Full" or "GA"
        $mode = "GA"
3. <span data-ttu-id="68121-140">Specify the additional data folder for which files will be collected (this step is optional).</span><span class="sxs-lookup"><span data-stu-id="68121-140">Specify the additional data folder for which files will be collected (this step is optional).</span></span>
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > <span data-ttu-id="68121-141">You can use token `%roleroot%` to specify the role root drive since it doesn’t use a fixed drive.</span><span class="sxs-lookup"><span data-stu-id="68121-141">You can use token `%roleroot%` to specify the role root drive since it doesn’t use a fixed drive.</span></span>
   > 
   > 
4. <span data-ttu-id="68121-142">Provide the Azure storage account name and key to which collected files will be uploaded.</span><span class="sxs-lookup"><span data-stu-id="68121-142">Provide the Azure storage account name and key to which collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. <span data-ttu-id="68121-143">Call the SetAzureServiceLogCollector.ps1 (included at the end of the article) as follows to enable the AzureLogCollector extension for a Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="68121-143">Call the SetAzureServiceLogCollector.ps1 (included at the end of the article) as follows to enable the AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="68121-144">Once the execution is completed, you can find the uploaded file under `https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span><span class="sxs-lookup"><span data-stu-id="68121-144">Once the execution is completed, you can find the uploaded file under `https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span></span>
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

<span data-ttu-id="68121-145">The following is the definition of the parameters passed to the script.</span><span class="sxs-lookup"><span data-stu-id="68121-145">The following is the definition of the parameters passed to the script.</span></span> <span data-ttu-id="68121-146">(This is copied below as well.)</span><span class="sxs-lookup"><span data-stu-id="68121-146">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
      [Parameter(Mandatory=$true)]
    [string]   $ServiceName,

    [Parameter(Mandatory=$false)]
    [string[]] $Roles ,

    [Parameter(Mandatory=$false)]
    [string[]] $Instances,

    [Parameter(Mandatory=$false)]
    [string]   $Slot = 'Production',

    [Parameter(Mandatory=$false)]
    [string]   $Mode = 'Full',

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountName,

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountKey,

    [Parameter(Mandatory=$false)]
    [PSObject[]] $AdditionDataLocationList = $null
    )

* <span data-ttu-id="68121-147">*ServiceName*: Your cloud service name.</span><span class="sxs-lookup"><span data-stu-id="68121-147">*ServiceName*: Your cloud service name.</span></span>
* <span data-ttu-id="68121-148">*Roles*: A list of roles, such as “WebRole1” or ”WorkerRole1”.</span><span class="sxs-lookup"><span data-stu-id="68121-148">*Roles*: A list of roles, such as “WebRole1” or ”WorkerRole1”.</span></span>
* <span data-ttu-id="68121-149">*Instances*: A list of the names of role instances separated by comma -- use the wildcard string (“\*”) for all role instances.</span><span class="sxs-lookup"><span data-stu-id="68121-149">*Instances*: A list of the names of role instances separated by comma -- use the wildcard string (“\*”) for all role instances.</span></span>
* <span data-ttu-id="68121-150">*Slot*: Slot name.</span><span class="sxs-lookup"><span data-stu-id="68121-150">*Slot*: Slot name.</span></span> <span data-ttu-id="68121-151">“Production” or “Staging”.</span><span class="sxs-lookup"><span data-stu-id="68121-151">“Production” or “Staging”.</span></span>
* <span data-ttu-id="68121-152">*Mode*: Collection mode.</span><span class="sxs-lookup"><span data-stu-id="68121-152">*Mode*: Collection mode.</span></span> <span data-ttu-id="68121-153">“Full” or “GA”.</span><span class="sxs-lookup"><span data-stu-id="68121-153">“Full” or “GA”.</span></span>
* <span data-ttu-id="68121-154">*StorageAccountName*: Name of Azure storage account for storing collected data.</span><span class="sxs-lookup"><span data-stu-id="68121-154">*StorageAccountName*: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="68121-155">*StorageAccountKey*: Name of Azure storage account key.</span><span class="sxs-lookup"><span data-stu-id="68121-155">*StorageAccountKey*: Name of Azure storage account key.</span></span>
* <span data-ttu-id="68121-156">*AdditionalDataLocationList*: A list of the following structure:</span><span class="sxs-lookup"><span data-stu-id="68121-156">*AdditionalDataLocationList*: A list of the following structure:</span></span>
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a><span data-ttu-id="68121-157">Adding as a VM Extension</span><span class="sxs-lookup"><span data-stu-id="68121-157">Adding as a VM Extension</span></span>
<span data-ttu-id="68121-158">Follow the instructions to connect Azure PowerShell to your subscription.</span><span class="sxs-lookup"><span data-stu-id="68121-158">Follow the instructions to connect Azure PowerShell to your subscription.</span></span>

1. <span data-ttu-id="68121-159">Specify the service name, VM, and the collection mode.</span><span class="sxs-lookup"><span data-stu-id="68121-159">Specify the service name, VM, and the collection mode.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify the VM name
        $VMName = "'YourVMName'"
   
        #Specify the collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify the additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. <span data-ttu-id="68121-160">Provide the Azure storage account name and key to which collected files will be uploaded.</span><span class="sxs-lookup"><span data-stu-id="68121-160">Provide the Azure storage account name and key to which collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. <span data-ttu-id="68121-161">Call the SetAzureVMLogCollector.ps1 (included at the end of the article) as follows to enable the AzureLogCollector extension for a Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="68121-161">Call the SetAzureVMLogCollector.ps1 (included at the end of the article) as follows to enable the AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="68121-162">Once the execution is completed, you can find the uploaded file under https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span><span class="sxs-lookup"><span data-stu-id="68121-162">Once the execution is completed, you can find the uploaded file under https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span></span>

<span data-ttu-id="68121-163">The following is the definition of the parameters passed to the script.</span><span class="sxs-lookup"><span data-stu-id="68121-163">The following is the definition of the parameters passed to the script.</span></span> <span data-ttu-id="68121-164">(This is copied below as well.)</span><span class="sxs-lookup"><span data-stu-id="68121-164">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
        [Parameter(Mandatory=$true)]
      [string]   $ServiceName,

      [Parameter(Mandatory=$false)]
      [string] $VMName ,

        [Parameter(Mandatory=$false)]
      [string]   $Mode = 'Full',

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountName,

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountKey,

      [Parameter(Mandatory=$false)]
      [PSObject[]] $AdditionDataLocationList = $null
      )

* <span data-ttu-id="68121-165">ServiceName: Your cloud service name.</span><span class="sxs-lookup"><span data-stu-id="68121-165">ServiceName: Your cloud service name.</span></span>
* <span data-ttu-id="68121-166">VMName The name of the VM.</span><span class="sxs-lookup"><span data-stu-id="68121-166">VMName The name of the VM.</span></span>
* <span data-ttu-id="68121-167">Mode: Collection mode.</span><span class="sxs-lookup"><span data-stu-id="68121-167">Mode: Collection mode.</span></span> <span data-ttu-id="68121-168">“Full” or “GA”.</span><span class="sxs-lookup"><span data-stu-id="68121-168">“Full” or “GA”.</span></span>
* <span data-ttu-id="68121-169">StorageAccountName: Name of Azure storage account for storing collected data.</span><span class="sxs-lookup"><span data-stu-id="68121-169">StorageAccountName: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="68121-170">StorageAccountKey: Name of Azure storage account key.</span><span class="sxs-lookup"><span data-stu-id="68121-170">StorageAccountKey: Name of Azure storage account key.</span></span>
* <span data-ttu-id="68121-171">AdditionalDataLocationList: A list of the following structure:</span><span class="sxs-lookup"><span data-stu-id="68121-171">AdditionalDataLocationList: A list of the following structure:</span></span>

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a><span data-ttu-id="68121-172">Extention PowerShell Script files</span><span class="sxs-lookup"><span data-stu-id="68121-172">Extention PowerShell Script files</span></span>
<span data-ttu-id="68121-173">SetAzureServiceLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="68121-173">SetAzureServiceLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Roles ,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Instances = '*',

                  [Parameter(Mandatory=$false)]
                  [string]   $Slot = 'Production',

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject

    if ($Instances -ne $null -and $Instances.Count -gt 0)  #Instances should be seperated by ,
    {
        $instanceText = $Instances[0]
        for ($i = 1;$i -lt $Instances.Count;$i++)
        {
              $instanceText = $instanceText+ "," + $Instances[$i]
          }
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value $instanceText
    }
    else  #For all instances if not specified.  The value should be a space or *
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value " "
    }

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need to get the Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData to collect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it to JSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json
    "publicConfig is:  $publicConfigJSON"

    #we just provide a empty privateConfig object
    $privateconfig = "{
    }"

    if ($Roles -ne $null)
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot -Role $Roles -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }
    else
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot  -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }

    #
    #This is an optional step: generate a sasUri to the container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "The container for uploaded file can be accessed using this link:`r`n$sasuri"


<span data-ttu-id="68121-174">SetAzureVMLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="68121-174">SetAzureVMLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string] $VMName ,

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject
    $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value "*"

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need to get the Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(90).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData to collect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it to JSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json

    Write-Output "PublicConfigurtion is: \r\n$publicConfigJSON"

    #
    #we just provide a empty privateConfig object
    #
    $privateconfig = "{
    }"

    if ($VMName -ne $null )
    {
          $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
          $VM.VM.OSVirtualHardDisk.OS

          if ($VM.VM.OSVirtualHardDisk.OS -like '*Windows*')
          {
                Set-AzureVMExtension -VM $VM -ExtensionName "AzureLogCollector" -Publisher Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.* | Update-AzureVM -Verbose

                #
                #We will check the VM status to find if operation by extension has been completed or not. The completion of the operation,either succeed or fail, can be indicated by
                #the presence of SubstatusList field.
                #
                $Completed = $false
                while ($Completed -ne $true)
                {
                        $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
                        $status = $VM.ResourceExtensionStatusList | Where-Object {$_.HandlerName -eq "Microsoft.WindowsAzure.Compute.AzureLogCollector"}

                        if ( ($status.Code -ne 0) -and ($status.Status -like '*error*'))
                        {
                            Write-Output "Error status is returned: $($Status.ExtensionSettingStatus.FormattedMessage.Message)."
                              $Completed = $true
                        }
                        elseif (($status.ExtensionSettingStatus.SubstatusList -eq $null -or $status.ExtensionSettingStatus.SubstatusList.Count -lt 1))
                        {
                              $Completed = $false
                              Write-Output "Waiting for operation to complete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access to the file, we can generate a read-only SasUri directly to the file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "The uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove the extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, the extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, the extension cannot be enabled"
    }

## <a name="next-steps"></a><span data-ttu-id="68121-175">Next Steps</span><span class="sxs-lookup"><span data-stu-id="68121-175">Next Steps</span></span>
<span data-ttu-id="68121-176">Now you can examine or copy your logs from one very simple location.</span><span class="sxs-lookup"><span data-stu-id="68121-176">Now you can examine or copy your logs from one very simple location.</span></span>

