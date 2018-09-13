---
title: PowerShell in Azure Cloud Shell (Preview) Quickstart | Microsoft Docs
description: Quickstart for PowerShell in Cloud Shell
services: Azure
documentationcenter: ''
author: maertendmsft
manager: timlt
tags: azure-resource-manager
ms.assetid: ''
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/27/2018
ms.author: damaerte
ms.openlocfilehash: cb4b7f8851c6c891ca43f6c215ba812a0c784d28
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857662"
---
# <a name="quickstart-for-powershell-in-azure-cloud-shell-preview"></a><span data-ttu-id="e2419-103">Quickstart for PowerShell in Azure Cloud Shell (Preview)</span><span class="sxs-lookup"><span data-stu-id="e2419-103">Quickstart for PowerShell in Azure Cloud Shell (Preview)</span></span>

<span data-ttu-id="e2419-104">This document details how to use the PowerShell in Cloud Shell in the [Azure portal](https://aka.ms/PSCloudPreview).</span><span class="sxs-lookup"><span data-stu-id="e2419-104">This document details how to use the PowerShell in Cloud Shell in the [Azure portal](https://aka.ms/PSCloudPreview).</span></span>

> [!NOTE]
> <span data-ttu-id="e2419-105">A [Bash in Azure Cloud Shell](quickstart.md) Quickstart is also available.</span><span class="sxs-lookup"><span data-stu-id="e2419-105">A [Bash in Azure Cloud Shell](quickstart.md) Quickstart is also available.</span></span>

## <a name="start-cloud-shell"></a><span data-ttu-id="e2419-106">Start Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="e2419-106">Start Cloud Shell</span></span>

1. <span data-ttu-id="e2419-107">Click on **Cloud Shell** button from the top navigation bar of the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e2419-107">Click on **Cloud Shell** button from the top navigation bar of the Azure portal</span></span>

  ![](media/quickstart-powershell/shell-icon.png)

2. <span data-ttu-id="e2419-108">Select the PowerShell environment from the drop-down and you will be in Azure drive `(Azure:)`</span><span class="sxs-lookup"><span data-stu-id="e2419-108">Select the PowerShell environment from the drop-down and you will be in Azure drive `(Azure:)`</span></span>

  ![](media/quickstart-powershell/environment-ps.png)

## <a name="run-powershell-commands"></a><span data-ttu-id="e2419-109">Run PowerShell commands</span><span class="sxs-lookup"><span data-stu-id="e2419-109">Run PowerShell commands</span></span>

<span data-ttu-id="e2419-110">Run regular PowerShell commands in the Cloud Shell, such as:</span><span class="sxs-lookup"><span data-stu-id="e2419-110">Run regular PowerShell commands in the Cloud Shell, such as:</span></span>

```azurepowershell-interactive
PS Azure:\> Get-Date

# Expected Output
Friday, July 27, 2018 7:08:48 AM

PS Azure:\> Get-AzureRmVM -Status

# Expected Output
ResourceGroupName       Name       Location                VmSize   OsType     ProvisioningState  PowerState
-----------------       ----       --------                ------   ------     -----------------  ----------
MyResourceGroup2        Demo        westus         Standard_DS1_v2  Windows    Succeeded           running
MyResourceGroup         MyVM1       eastus            Standard_DS1  Windows    Succeeded           running
MyResourceGroup         MyVM2       eastus   Standard_DS2_v2_Promo  Windows    Succeeded           deallocated
```

## <a name="navigate-azure-resources"></a><span data-ttu-id="e2419-111">Navigate Azure resources</span><span class="sxs-lookup"><span data-stu-id="e2419-111">Navigate Azure resources</span></span>

 1. <span data-ttu-id="e2419-112">List all your subscriptions from `Azure` drive</span><span class="sxs-lookup"><span data-stu-id="e2419-112">List all your subscriptions from `Azure` drive</span></span>

    ```azurepowershell-interactive
    PS Azure:\> dir
    ```

 2. <span data-ttu-id="e2419-113">`cd` to your preferred subscription</span><span class="sxs-lookup"><span data-stu-id="e2419-113">`cd` to your preferred subscription</span></span>

    ```azurepowershell-interactive
    PS Azure:\> cd MySubscriptionName
    PS Azure:\MySubscriptionName>
    ```

 3. <span data-ttu-id="e2419-114">View all your Azure resources under the current subscription</span><span class="sxs-lookup"><span data-stu-id="e2419-114">View all your Azure resources under the current subscription</span></span>

    <span data-ttu-id="e2419-115">Type `dir` to list multiple views of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="e2419-115">Type `dir` to list multiple views of your Azure resources.</span></span>

    ```azurepowershell-interactive
    PS Azure:\MySubscriptionName> dir

        Directory: azure:\MySubscriptionName

    Mode Name
    ---- ----
    +    AllResources
    +    ResourceGroups
    +    StorageAccounts
    +    VirtualMachines
    +    WebApps
    ```

### <a name="allresources-view"></a><span data-ttu-id="e2419-116">AllResources view</span><span class="sxs-lookup"><span data-stu-id="e2419-116">AllResources view</span></span>

<span data-ttu-id="e2419-117">Type `dir` under `AllResources` directory to view your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="e2419-117">Type `dir` under `AllResources` directory to view your Azure resources.</span></span>

```azurepowershell-interactive
PS Azure:\MySubscriptionName> dir AllResources
```

### <a name="explore-resource-groups"></a><span data-ttu-id="e2419-118">Explore resource groups</span><span class="sxs-lookup"><span data-stu-id="e2419-118">Explore resource groups</span></span>

 <span data-ttu-id="e2419-119">You can go to the `ResourceGroups` directory and inside a specific resource group you can find virtual machines.</span><span class="sxs-lookup"><span data-stu-id="e2419-119">You can go to the `ResourceGroups` directory and inside a specific resource group you can find virtual machines.</span></span>

```azureowershell-interactive
PS Azure:\MySubscriptionName> cd ResourceGroups\MyResourceGroup1\Microsoft.Compute\virtualMachines

PS Azure:\MySubscriptionName\ResourceGroups\MyResourceGroup1\Microsoft.Compute\virtualMachines> dir


    Directory: Azure:\MySubscriptionName\ResourceGroups\MyResourceGroup1\Microsoft.Compute\virtualMachines


VMName    Location   ProvisioningState VMSize          OS            SKU             OSVersion AdminUserName  NetworkInterfaceName
------    --------   ----------------- ------          --            ---             --------- -------------  --------------------
TestVm1   westus     Succeeded         Standard_DS2_v2 WindowsServer 2016-Datacenter Latest    AdminUser      demo371
TestVm2   westus     Succeeded         Standard_DS1_v2 WindowsServer 2016-Datacenter Latest    AdminUser      demo271
```

> [!NOTE]
> <span data-ttu-id="e2419-120">You may notice that the second time when you type `dir`, the Cloud Shell is able to display the items much faster.</span><span class="sxs-lookup"><span data-stu-id="e2419-120">You may notice that the second time when you type `dir`, the Cloud Shell is able to display the items much faster.</span></span>
> <span data-ttu-id="e2419-121">This is because the child items are cached in memory for a better user experience.</span><span class="sxs-lookup"><span data-stu-id="e2419-121">This is because the child items are cached in memory for a better user experience.</span></span>
<span data-ttu-id="e2419-122">However, you can always use `dir -Force` to get fresh data.</span><span class="sxs-lookup"><span data-stu-id="e2419-122">However, you can always use `dir -Force` to get fresh data.</span></span>

### <a name="navigate-storage-resources"></a><span data-ttu-id="e2419-123">Navigate storage resources</span><span class="sxs-lookup"><span data-stu-id="e2419-123">Navigate storage resources</span></span>

<span data-ttu-id="e2419-124">By entering into the `StorageAccounts` directory, you can easily navigate all your storage resources</span><span class="sxs-lookup"><span data-stu-id="e2419-124">By entering into the `StorageAccounts` directory, you can easily navigate all your storage resources</span></span>

```azureowershell-interactive
PS Azure:\MySubscriptionName\StorageAccounts\MyStorageAccountName\Files> dir

    Directory: Azure:\MySubscriptionNameStorageAccounts\MyStorageAccountName\Files

Name          ConnectionString
----          ----------------
MyFileShare1  \\MyStorageAccountName.file.core.windows.net\MyFileShare1;AccountName=MyStorageAccountName AccountKey=<key>
MyFileShare2  \\MyStorageAccountName.file.core.windows.net\MyFileShare2;AccountName=MyStorageAccountName AccountKey=<key>
MyFileShare3  \\MyStorageAccountName.file.core.windows.net\MyFileShare3;AccountName=MyStorageAccountName AccountKey=<key>
```

<span data-ttu-id="e2419-125">With the connection string, you can use the following command to mount the Azure Files share.</span><span class="sxs-lookup"><span data-stu-id="e2419-125">With the connection string, you can use the following command to mount the Azure Files share.</span></span>

```azurepowershell-interactive
net use <DesiredDriveLetter>: \\<MyStorageAccountName>.file.core.windows.net\<MyFileShareName> <AccountKey> /user:Azure\<MyStorageAccountName>
```

<span data-ttu-id="e2419-126">For details, see [Mount an Azure Files share and access the share in Windows][azmount].</span><span class="sxs-lookup"><span data-stu-id="e2419-126">For details, see [Mount an Azure Files share and access the share in Windows][azmount].</span></span>

<span data-ttu-id="e2419-127">You can also navigate the directories under the Azure Files share as follows:</span><span class="sxs-lookup"><span data-stu-id="e2419-127">You can also navigate the directories under the Azure Files share as follows:</span></span>

```azurepowershell-interactive
PS Azure:\MySubscriptionName\StorageAccounts\MyStorageAccountName\Files> cd .\MyFileShare1\
PS Azure:\MySubscriptionName\StorageAccounts\MyStorageAccountName\Files\MyFileShare1> dir

Mode  Name
----  ----
+     TestFolder
.     hello.ps1
```

### <a name="interact-with-virtual-machines"></a><span data-ttu-id="e2419-128">Interact with virtual machines</span><span class="sxs-lookup"><span data-stu-id="e2419-128">Interact with virtual machines</span></span>

<span data-ttu-id="e2419-129">You can find all your virtual machines under the current subscription via `VirtualMachines` directory.</span><span class="sxs-lookup"><span data-stu-id="e2419-129">You can find all your virtual machines under the current subscription via `VirtualMachines` directory.</span></span>

```azurepowershell-interactive
PS Azure:\MySubscriptionName\VirtualMachines> dir

    Directory: Azure:\MySubscriptionName\VirtualMachines


Name       ResourceGroupName  Location  VmSize          OsType              NIC ProvisioningState  PowerState
----       -----------------  --------  ------          ------              --- -----------------  ----------
TestVm1    MyResourceGroup1   westus    Standard_DS2_v2 Windows       my2008r213         Succeeded     stopped
TestVm2    MyResourceGroup1   westus    Standard_DS1_v2 Windows          jpstest         Succeeded deallocated
TestVm10   MyResourceGroup2   eastus    Standard_DS1_v2 Windows           mytest         Succeeded     running
```

#### <a name="invoke-powershell-script-across-remote-vms"></a><span data-ttu-id="e2419-130">Invoke PowerShell script across remote VMs</span><span class="sxs-lookup"><span data-stu-id="e2419-130">Invoke PowerShell script across remote VMs</span></span>

 > [!WARNING]
 > <span data-ttu-id="e2419-131">Please refer to [Troubleshooting remote management of Azure VMs](troubleshooting.md#troubleshooting-remote-management-of-azure-vms).</span><span class="sxs-lookup"><span data-stu-id="e2419-131">Please refer to [Troubleshooting remote management of Azure VMs](troubleshooting.md#troubleshooting-remote-management-of-azure-vms).</span></span>

  <span data-ttu-id="e2419-132">Assuming you have a VM, MyVM1, let's use `Invoke-AzureRmVMCommand` to invoke a PowerShell script block on the remote machine.</span><span class="sxs-lookup"><span data-stu-id="e2419-132">Assuming you have a VM, MyVM1, let's use `Invoke-AzureRmVMCommand` to invoke a PowerShell script block on the remote machine.</span></span>

  ```azurepowershell-interactive
  Invoke-AzureRmVMCommand -Name MyVM1 -ResourceGroupName MyResourceGroup -Scriptblock {Get-ComputerInfo} -EnableRemoting
  ```

  <span data-ttu-id="e2419-133">You can also navigate to the VirtualMachines directory first and run `Invoke-AzureRmVMCommand` as follows.</span><span class="sxs-lookup"><span data-stu-id="e2419-133">You can also navigate to the VirtualMachines directory first and run `Invoke-AzureRmVMCommand` as follows.</span></span>

  ```azurepowershell-interactive
  PS Azure:\> cd MySubscriptionName\MyResourceGroup\Microsoft.Compute\virtualMachines
  PS Azure:\MySubscriptionName\MyResourceGroup\Microsoft.Compute\virtualMachines> Get-Item MyVM1 | Invoke-AzureRmVMCommand -Scriptblock {Get-ComputerInfo}

  # You will see output similar to the following:

  PSComputerName                                          : 65.52.28.207
  RunspaceId                                              : 2c2b60da-f9b9-4f42-a282-93316cb06fe1
  WindowsBuildLabEx                                       : 14393.1066.amd64fre.rs1_release_sec.170327-1835
  WindowsCurrentVersion                                   : 6.3
  WindowsEditionId                                        : ServerDatacenter
  WindowsInstallationType                                 : Server
  WindowsInstallDateFromRegistry                          : 5/18/2017 11:26:08 PM
  WindowsProductId                                        : 00376-40000-00000-AA947
  WindowsProductName                                      : Windows Server 2016 Datacenter
  WindowsRegisteredOrganization                           :
   ...
  ```

#### <a name="interactively-log-on-to-a-remote-vm"></a><span data-ttu-id="e2419-134">Interactively log on to a remote VM</span><span class="sxs-lookup"><span data-stu-id="e2419-134">Interactively log on to a remote VM</span></span>

<span data-ttu-id="e2419-135">You can use `Enter-AzureRmVM` to interactively log into a VM running in Azure.</span><span class="sxs-lookup"><span data-stu-id="e2419-135">You can use `Enter-AzureRmVM` to interactively log into a VM running in Azure.</span></span>

  ```azurepowershell-interactive
  PS Azure:\> Enter-AzureRmVM -Name MyVM1 -ResourceGroupName MyResourceGroup -EnableRemoting
  ```

<span data-ttu-id="e2419-136">You can also navigate to the `VirtualMachines` directory first and run `Enter-AzureRmVM` as follows</span><span class="sxs-lookup"><span data-stu-id="e2419-136">You can also navigate to the `VirtualMachines` directory first and run `Enter-AzureRmVM` as follows</span></span>

  ```azurepowershell-interactive
 PS Azure:\MySubscriptionName\ResourceGroups\MyResourceGroup\Microsoft.Compute\virtualMachines> Get-Item MyVM1 | Enter-AzureRmVM
 ```

### <a name="discover-webapps"></a><span data-ttu-id="e2419-137">Discover WebApps</span><span class="sxs-lookup"><span data-stu-id="e2419-137">Discover WebApps</span></span>

<span data-ttu-id="e2419-138">By entering into the `WebApps` directory, you can easily navigate your web apps resources</span><span class="sxs-lookup"><span data-stu-id="e2419-138">By entering into the `WebApps` directory, you can easily navigate your web apps resources</span></span>

```azurepowershell-interactive
PS Azure:\MySubscriptionName> dir .\WebApps\

    Directory: Azure:\MySubscriptionName\WebApps

Name            State    ResourceGroup      EnabledHostNames                  Location
----            -----    -------------      ----------------                  --------
mywebapp1       Stopped  MyResourceGroup1   {mywebapp1.azurewebsites.net...   West US
mywebapp2       Running  MyResourceGroup2   {mywebapp2.azurewebsites.net...   West Europe
mywebapp3       Running  MyResourceGroup3   {mywebapp3.azurewebsites.net...   South Central US

# You can use Azure cmdlets to Start/Stop your web apps
PS Azure:\MySubscriptionName\WebApps> Start-AzureRmWebApp -Name mywebapp1 -ResourceGroupName MyResourceGroup1

Name           State    ResourceGroup        EnabledHostNames                   Location
----           -----    -------------        ----------------                   --------
mywebapp1      Running  MyResourceGroup1     {mywebapp1.azurewebsites.net ...   West US

# Refresh the current state with -Force
PS Azure:\MySubscriptionName\WebApps> dir -Force

    Directory: Azure:\MySubscriptionName\WebApps

Name            State    ResourceGroup      EnabledHostNames                  Location
----            -----    -------------      ----------------                  --------
mywebapp1       Running  MyResourceGroup1   {mywebapp1.azurewebsites.net...   West US
mywebapp2       Running  MyResourceGroup2   {mywebapp2.azurewebsites.net...   West Europe
mywebapp3       Running  MyResourceGroup3   {mywebapp3.azurewebsites.net...   South Central US
```

## <a name="ssh"></a><span data-ttu-id="e2419-139">SSH</span><span class="sxs-lookup"><span data-stu-id="e2419-139">SSH</span></span>

<span data-ttu-id="e2419-140">To authenticate to servers or VMs using SSH, generate the public-private key pair in Cloud Shell and publish the public key to `authorized_keys` on the remote machine, such as `/home/user/.ssh/authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="e2419-140">To authenticate to servers or VMs using SSH, generate the public-private key pair in Cloud Shell and publish the public key to `authorized_keys` on the remote machine, such as `/home/user/.ssh/authorized_keys`.</span></span>

> [!NOTE]
> <span data-ttu-id="e2419-141">You can create SSH private-public keys using `ssh-keygen` and publish them to `$env:USERPROFILE\.ssh` in Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="e2419-141">You can create SSH private-public keys using `ssh-keygen` and publish them to `$env:USERPROFILE\.ssh` in Cloud Shell.</span></span>

### <a name="using-ssh"></a><span data-ttu-id="e2419-142">Using SSH</span><span class="sxs-lookup"><span data-stu-id="e2419-142">Using SSH</span></span>

<span data-ttu-id="e2419-143">Follow instructions [here](https://docs.microsoft.com/azure/virtual-machines/linux/quick-create-powershell) to create a new VM configuration using AzureRM cmdlets.</span><span class="sxs-lookup"><span data-stu-id="e2419-143">Follow instructions [here](https://docs.microsoft.com/azure/virtual-machines/linux/quick-create-powershell) to create a new VM configuration using AzureRM cmdlets.</span></span>
<span data-ttu-id="e2419-144">Before calling into `New-AzureRmVM` to kick off the deployment, add SSH public key to the VM configuration.</span><span class="sxs-lookup"><span data-stu-id="e2419-144">Before calling into `New-AzureRmVM` to kick off the deployment, add SSH public key to the VM configuration.</span></span>
<span data-ttu-id="e2419-145">The newly created VM will contain the public key in the `~\.ssh\authorized_keys` location, thereby enabling credential-free SSH session to the VM.</span><span class="sxs-lookup"><span data-stu-id="e2419-145">The newly created VM will contain the public key in the `~\.ssh\authorized_keys` location, thereby enabling credential-free SSH session to the VM.</span></span>

```azurepowershell-interactive
# Create VM config object - $vmConfig using instructions on linked page above

# Generate SSH keys in Cloud Shell
ssh-keygen -t rsa -b 2048 -f $HOME\.ssh\id_rsa 

# Ensure VM config is updated with SSH keys
$sshPublicKey = Get-Content "$HOME\.ssh\id_rsa.pub"
Add-AzureRmVMSshPublicKey -VM $vmConfig -KeyData $sshPublicKey -Path "/home/azureuser/.ssh/authorized_keys"

# Create a virtual machine
New-AzureRmVM -ResourceGroupName <yourResourceGroup> -Location <vmLocation> -VM $vmConfig

# SSH to the VM
ssh azureuser@MyVM.Domain.Com
```

## <a name="list-available-commands"></a><span data-ttu-id="e2419-146">List available commands</span><span class="sxs-lookup"><span data-stu-id="e2419-146">List available commands</span></span>

<span data-ttu-id="e2419-147">Under `Azure` drive, type `Get-AzureRmCommand` to get context-specific Azure commands.</span><span class="sxs-lookup"><span data-stu-id="e2419-147">Under `Azure` drive, type `Get-AzureRmCommand` to get context-specific Azure commands.</span></span>

<span data-ttu-id="e2419-148">Alternatively, you can always use `Get-Command *azurerm* -Module AzureRM.*` to find out the available Azure commands.</span><span class="sxs-lookup"><span data-stu-id="e2419-148">Alternatively, you can always use `Get-Command *azurerm* -Module AzureRM.*` to find out the available Azure commands.</span></span>

## <a name="install-custom-modules"></a><span data-ttu-id="e2419-149">Install custom modules</span><span class="sxs-lookup"><span data-stu-id="e2419-149">Install custom modules</span></span>

<span data-ttu-id="e2419-150">You can run `Install-Module` to install modules from the [PowerShell Gallery][gallery].</span><span class="sxs-lookup"><span data-stu-id="e2419-150">You can run `Install-Module` to install modules from the [PowerShell Gallery][gallery].</span></span>

## <a name="get-help"></a><span data-ttu-id="e2419-151">Get-Help</span><span class="sxs-lookup"><span data-stu-id="e2419-151">Get-Help</span></span>

<span data-ttu-id="e2419-152">Type `Get-Help` to get information about PowerShell in Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="e2419-152">Type `Get-Help` to get information about PowerShell in Azure Cloud Shell.</span></span>

```azurepowershell-interactive
Get-Help
```

<span data-ttu-id="e2419-153">For a specific command, you can still do `Get-Help` followed by a cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e2419-153">For a specific command, you can still do `Get-Help` followed by a cmdlet.</span></span>

```azurepowershell-interactive
Get-Help Get-AzureRmVM
```

## <a name="use-azure-files-to-store-your-data"></a><span data-ttu-id="e2419-154">Use Azure Files to store your data</span><span class="sxs-lookup"><span data-stu-id="e2419-154">Use Azure Files to store your data</span></span>

<span data-ttu-id="e2419-155">You can create a script, say `helloworld.ps1`, and save it to your `clouddrive` to use it across shell sessions.</span><span class="sxs-lookup"><span data-stu-id="e2419-155">You can create a script, say `helloworld.ps1`, and save it to your `clouddrive` to use it across shell sessions.</span></span>

```azurepowershell-interactive
cd $HOME\clouddrive
code .\helloworld.ps1
# Add the content, such as 'Hello World!'
.\helloworld.ps1
Hello World!
```

<span data-ttu-id="e2419-156">Next time when you use PowerShell in Cloud Shell, the `helloworld.ps1` file will exist under the `$HOME\clouddrive` directory that mounts your Azure Files share.</span><span class="sxs-lookup"><span data-stu-id="e2419-156">Next time when you use PowerShell in Cloud Shell, the `helloworld.ps1` file will exist under the `$HOME\clouddrive` directory that mounts your Azure Files share.</span></span>

## <a name="use-custom-profile"></a><span data-ttu-id="e2419-157">Use custom profile</span><span class="sxs-lookup"><span data-stu-id="e2419-157">Use custom profile</span></span>

<span data-ttu-id="e2419-158">You can customize your PowerShell environment, by creating PowerShell profile(s) - `profile.ps1` (or `Microsoft.PowerShell_profile.ps1`).</span><span class="sxs-lookup"><span data-stu-id="e2419-158">You can customize your PowerShell environment, by creating PowerShell profile(s) - `profile.ps1` (or `Microsoft.PowerShell_profile.ps1`).</span></span>
<span data-ttu-id="e2419-159">Save it under `$profile.CurrentUserAllHosts` (or `$profile.CurrentUserAllHosts`), so that it can be loaded in every PowerShell in Cloud Shell session.</span><span class="sxs-lookup"><span data-stu-id="e2419-159">Save it under `$profile.CurrentUserAllHosts` (or `$profile.CurrentUserAllHosts`), so that it can be loaded in every PowerShell in Cloud Shell session.</span></span>

<span data-ttu-id="e2419-160">For how to create a profile, refer to [About Profiles][profile].</span><span class="sxs-lookup"><span data-stu-id="e2419-160">For how to create a profile, refer to [About Profiles][profile].</span></span>

## <a name="use-git"></a><span data-ttu-id="e2419-161">Use Git</span><span class="sxs-lookup"><span data-stu-id="e2419-161">Use Git</span></span>

<span data-ttu-id="e2419-162">To clone a Git repo in the Cloud Shell, you need to create a [personal access token][githubtoken] and use it as the username.</span><span class="sxs-lookup"><span data-stu-id="e2419-162">To clone a Git repo in the Cloud Shell, you need to create a [personal access token][githubtoken] and use it as the username.</span></span> <span data-ttu-id="e2419-163">Once you have your token, clone the repository as follows:</span><span class="sxs-lookup"><span data-stu-id="e2419-163">Once you have your token, clone the repository as follows:</span></span>

```azurepowershell-interactive
  git clone https://<your-access-token>@github.com/username/repo.git
```

## <a name="exit-the-shell"></a><span data-ttu-id="e2419-164">Exit the shell</span><span class="sxs-lookup"><span data-stu-id="e2419-164">Exit the shell</span></span>

<span data-ttu-id="e2419-165">Type `exit` to terminate the session.</span><span class="sxs-lookup"><span data-stu-id="e2419-165">Type `exit` to terminate the session.</span></span>

[bashqs]:quickstart.md
[gallery]:https://www.powershellgallery.com/
[customex]:https://docs.microsoft.com/azure/virtual-machines/windows/extensions-customscript
[profile]: https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_profiles
[azmount]: https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-windows
[githubtoken]: https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/
