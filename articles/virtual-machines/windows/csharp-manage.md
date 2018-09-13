---
title: Manage VMs using Azure Resource Manager and C# | Microsoft Docs
description: Manage virtual machines using Azure Resource Manager and C#.
services: virtual-machines-windows
documentationcenter: ''
author: davidmu1
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 93898bad-b861-4359-9a4b-348e1d491822
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: davidmu
ms.openlocfilehash: 7726b80e2cc9f6179ed6af3865c4c360232b5d9d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554919"
---
# <a name="manage-azure-virtual-machines-using-azure-resource-manager-and-c"></a><span data-ttu-id="cd294-103">Manage Azure Virtual Machines using Azure Resource Manager and C#</span><span class="sxs-lookup"><span data-stu-id="cd294-103">Manage Azure Virtual Machines using Azure Resource Manager and C#</span></span> #

<span data-ttu-id="cd294-104">The tasks in this article show you how to manage virtual machines, such as starting, stopping, and updating.</span><span class="sxs-lookup"><span data-stu-id="cd294-104">The tasks in this article show you how to manage virtual machines, such as starting, stopping, and updating.</span></span>

## <a name="set-up-visual-studio"></a><span data-ttu-id="cd294-105">Set up Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cd294-105">Set up Visual Studio</span></span>

### <a name="create-a-project"></a><span data-ttu-id="cd294-106">Create a project</span><span class="sxs-lookup"><span data-stu-id="cd294-106">Create a project</span></span>

<span data-ttu-id="cd294-107">Make sure Visual Studio is installed and create a console application used to manage your virtual machines.</span><span class="sxs-lookup"><span data-stu-id="cd294-107">Make sure Visual Studio is installed and create a console application used to manage your virtual machines.</span></span>

1. <span data-ttu-id="cd294-108">If you haven't already, install [Visual Studio](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="cd294-108">If you haven't already, install [Visual Studio](https://www.visualstudio.com/).</span></span>
2. <span data-ttu-id="cd294-109">In Visual Studio, click **File** > **New** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="cd294-109">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="cd294-110">In **Templates** > **Visual C#**, select **Console Application**, enter the name and location of the project, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="cd294-110">In **Templates** > **Visual C#**, select **Console Application**, enter the name and location of the project, and then click **OK**.</span></span>

### <a name="install-libraries"></a><span data-ttu-id="cd294-111">Install libraries</span><span class="sxs-lookup"><span data-stu-id="cd294-111">Install libraries</span></span>

<span data-ttu-id="cd294-112">NuGet packages are the easiest way to install the libraries that you need to perform the actions in this article.</span><span class="sxs-lookup"><span data-stu-id="cd294-112">NuGet packages are the easiest way to install the libraries that you need to perform the actions in this article.</span></span> <span data-ttu-id="cd294-113">To get the libraries that you need in Visual Studio, do these steps:</span><span class="sxs-lookup"><span data-stu-id="cd294-113">To get the libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="cd294-114">Right-click the project name in the Solution Explorer, click **Manage NuGet Packages**, and then click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="cd294-114">Right-click the project name in the Solution Explorer, click **Manage NuGet Packages**, and then click **Browse**.</span></span>
2. <span data-ttu-id="cd294-115">Type *Microsoft.IdentityModel.Clients.ActiveDirectory* in the search box, click **Install**, and then follow the instructions to install the package.</span><span class="sxs-lookup"><span data-stu-id="cd294-115">Type *Microsoft.IdentityModel.Clients.ActiveDirectory* in the search box, click **Install**, and then follow the instructions to install the package.</span></span>
3. <span data-ttu-id="cd294-116">At the top of the page, select **Include Prerelease**.</span><span class="sxs-lookup"><span data-stu-id="cd294-116">At the top of the page, select **Include Prerelease**.</span></span> <span data-ttu-id="cd294-117">Type *Microsoft.Azure.Management.Compute* in the search box, click **Install**, and then follow the instructions to install the package.</span><span class="sxs-lookup"><span data-stu-id="cd294-117">Type *Microsoft.Azure.Management.Compute* in the search box, click **Install**, and then follow the instructions to install the package.</span></span>

<span data-ttu-id="cd294-118">Now you're ready to start using the libraries to manage your virtual machines.</span><span class="sxs-lookup"><span data-stu-id="cd294-118">Now you're ready to start using the libraries to manage your virtual machines.</span></span>

### <a name="create-credentials-and-add-variables"></a><span data-ttu-id="cd294-119">Create credentials and add variables</span><span class="sxs-lookup"><span data-stu-id="cd294-119">Create credentials and add variables</span></span>

<span data-ttu-id="cd294-120">To interact with Azure Resource Manager, make sure that you have access to an [Active Directory service principal](../../resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="cd294-120">To interact with Azure Resource Manager, make sure that you have access to an [Active Directory service principal](../../resource-group-authenticate-service-principal.md).</span></span> <span data-ttu-id="cd294-121">From the service principal, you acquire a token for authenticating requests to Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cd294-121">From the service principal, you acquire a token for authenticating requests to Azure Resource Manager.</span></span>

1. <span data-ttu-id="cd294-122">Open the Program.cs file for the project that you created, and then add these using statements to the top of the file:</span><span class="sxs-lookup"><span data-stu-id="cd294-122">Open the Program.cs file for the project that you created, and then add these using statements to the top of the file:</span></span>

    ```   
    using Microsoft.Azure;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Azure.Management.Compute;
    using Microsoft.Azure.Management.Compute.Models;
    using Microsoft.Rest;
    ```

2. <span data-ttu-id="cd294-123">Add variables to the Main method of the Program class to specify the name of the resource group, the name of the virtual machine, and your subscription identifier:</span><span class="sxs-lookup"><span data-stu-id="cd294-123">Add variables to the Main method of the Program class to specify the name of the resource group, the name of the virtual machine, and your subscription identifier:</span></span>

    ```   
    var groupName = "myResourceGroup";
    var vmName = "myVM";  
    var subscriptionId = "subsciptionId";
    ```

    <span data-ttu-id="cd294-124">You can find the subscription identifier on the Subscriptions blade of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cd294-124">You can find the subscription identifier on the Subscriptions blade of the Azure portal.</span></span>    

3. <span data-ttu-id="cd294-125">To get the token that is needed to create the credentials, add this method to the Program class:</span><span class="sxs-lookup"><span data-stu-id="cd294-125">To get the token that is needed to create the credentials, add this method to the Program class:</span></span>
   
    ```    
    private static async Task<AuthenticationResult> GetAccessTokenAsync()
    {
      var cc = new ClientCredential("{client-id}", "{client-secret}");
      var context = new AuthenticationContext("https://login.windows.net/{tenant-id}");
      var token = await context.AcquireTokenAsync("https://management.azure.com/", cc);
      if (token == null)
      {
        throw new InvalidOperationException("Could not get the token");
      }
      return token;
    }
    ```

    <span data-ttu-id="cd294-126">Replace these values:</span><span class="sxs-lookup"><span data-stu-id="cd294-126">Replace these values:</span></span>
    
    - <span data-ttu-id="cd294-127">*{client-id}* with the identifier of the Azure Active Directory application.</span><span class="sxs-lookup"><span data-stu-id="cd294-127">*{client-id}* with the identifier of the Azure Active Directory application.</span></span> <span data-ttu-id="cd294-128">You can find this identifier on the Properties blade of your AD application.</span><span class="sxs-lookup"><span data-stu-id="cd294-128">You can find this identifier on the Properties blade of your AD application.</span></span> <span data-ttu-id="cd294-129">To find your AD application in the Azure portal, click **Azure Active Directory** in the resource menu, and then click **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="cd294-129">To find your AD application in the Azure portal, click **Azure Active Directory** in the resource menu, and then click **App registrations**.</span></span>
    - <span data-ttu-id="cd294-130">*{client-secret}* with the access key of the AD application.</span><span class="sxs-lookup"><span data-stu-id="cd294-130">*{client-secret}* with the access key of the AD application.</span></span> <span data-ttu-id="cd294-131">You can find this identifier on the Properties blade of your AD application.</span><span class="sxs-lookup"><span data-stu-id="cd294-131">You can find this identifier on the Properties blade of your AD application.</span></span>
    - <span data-ttu-id="cd294-132">*{tenant-id}* with the tenant identifier of your subscription.</span><span class="sxs-lookup"><span data-stu-id="cd294-132">*{tenant-id}* with the tenant identifier of your subscription.</span></span> <span data-ttu-id="cd294-133">You can find the tenant identifier on the Properties blade for Azure Active Directory in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cd294-133">You can find the tenant identifier on the Properties blade for Azure Active Directory in the Azure portal.</span></span> <span data-ttu-id="cd294-134">It is labeled *Directory ID*.</span><span class="sxs-lookup"><span data-stu-id="cd294-134">It is labeled *Directory ID*.</span></span>

4. <span data-ttu-id="cd294-135">To call the method that you previously added, add this code to the Main method in the Program.cs file:</span><span class="sxs-lookup"><span data-stu-id="cd294-135">To call the method that you previously added, add this code to the Main method in the Program.cs file:</span></span>
   
    ```
    var token = GetAccessTokenAsync();
    var credential = new TokenCredentials(token.Result.AccessToken);
    ```

5. <span data-ttu-id="cd294-136">Save the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="cd294-136">Save the Program.cs file.</span></span>

## <a name="display-information-about-a-virtual-machine"></a><span data-ttu-id="cd294-137">Display information about a virtual machine</span><span class="sxs-lookup"><span data-stu-id="cd294-137">Display information about a virtual machine</span></span>

1. <span data-ttu-id="cd294-138">Add this method to the Program class in the project that you previously created:</span><span class="sxs-lookup"><span data-stu-id="cd294-138">Add this method to the Program class in the project that you previously created:</span></span>

    ```   
    public static async void GetVirtualMachineAsync(
      TokenCredentials credential, 
      string groupName, 
      string vmName, 
      string subscriptionId)
    {
      Console.WriteLine("Getting information about the virtual machine...");
   
      var computeManagementClient = new ComputeManagementClient(credential)
        { SubscriptionId = subscriptionId };
      var vmResult = await computeManagementClient.VirtualMachines.GetAsync(
        groupName, 
        vmName, 
        InstanceViewTypes.InstanceView);
   
      Console.WriteLine("hardwareProfile");
      Console.WriteLine("   vmSize: " + vmResult.HardwareProfile.VmSize);
   
      Console.WriteLine("\nstorageProfile");
      Console.WriteLine("  imageReference");
      Console.WriteLine("    publisher: " + vmResult.StorageProfile.ImageReference.Publisher);
      Console.WriteLine("    offer: " + vmResult.StorageProfile.ImageReference.Offer);
      Console.WriteLine("    sku: " + vmResult.StorageProfile.ImageReference.Sku);
      Console.WriteLine("    version: " + vmResult.StorageProfile.ImageReference.Version);
      Console.WriteLine("  osDisk");
      Console.WriteLine("    osType: " + vmResult.StorageProfile.OsDisk.OsType);
      Console.WriteLine("    name: " + vmResult.StorageProfile.OsDisk.Name);
      Console.WriteLine("    createOption: " + vmResult.StorageProfile.OsDisk.CreateOption);
      Console.WriteLine("    uri: " + vmResult.StorageProfile.OsDisk.Vhd.Uri);
      Console.WriteLine("    caching: " + vmResult.StorageProfile.OsDisk.Caching);
      Console.WriteLine("\nosProfile");
      Console.WriteLine("  computerName: " + vmResult.OsProfile.ComputerName);
      Console.WriteLine("  adminUsername: " + vmResult.OsProfile.AdminUsername);
      Console.WriteLine("  provisionVMAgent: " + vmResult.OsProfile.WindowsConfiguration.ProvisionVMAgent.Value);
      Console.WriteLine("  enableAutomaticUpdates: " + vmResult.OsProfile.WindowsConfiguration.EnableAutomaticUpdates.Value);
   
      Console.WriteLine("\nnetworkProfile");
      foreach (NetworkInterfaceReference nic in vmResult.NetworkProfile.NetworkInterfaces)
      {
        Console.WriteLine("  networkInterface id: " + nic.Id);
      }
   
      Console.WriteLine("\nvmAgent");
      Console.WriteLine("  vmAgentVersion" + vmResult.InstanceView.VmAgent.VmAgentVersion);
      Console.WriteLine("    statuses");
      foreach (InstanceViewStatus stat in vmResult.InstanceView.VmAgent.Statuses)
      {
        Console.WriteLine("    code: " + stat.Code);
        Console.WriteLine("    level: " + stat.Level);
        Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
        Console.WriteLine("    message: " + stat.Message);
        Console.WriteLine("    time: " + stat.Time);
      }
   
      Console.WriteLine("\ndisks");
      foreach (DiskInstanceView idisk in vmResult.InstanceView.Disks)
      {
        Console.WriteLine("  name: " + idisk.Name);
        Console.WriteLine("  statuses");
        foreach (InstanceViewStatus istat in idisk.Statuses)
        {
          Console.WriteLine("    code: " + istat.Code);
          Console.WriteLine("    level: " + istat.Level);
          Console.WriteLine("    displayStatus: " + istat.DisplayStatus);
          Console.WriteLine("    time: " + istat.Time);
        }
      }
   
      Console.WriteLine("\nVM general status");
      Console.WriteLine("  provisioningStatus: " + vmResult.ProvisioningState);
      Console.WriteLine("  id: " + vmResult.Id);
      Console.WriteLine("  name: " + vmResult.Name);
      Console.WriteLine("  type: " + vmResult.Type);
      Console.WriteLine("  location: " + vmResult.Location);
      Console.WriteLine("\nVM instance status");
      foreach (InstanceViewStatus istat in vmResult.InstanceView.Statuses)
      {
        Console.WriteLine("\n  code: " + istat.Code);
        Console.WriteLine("  level: " + istat.Level);
        Console.WriteLine("  displayStatus: " + istat.DisplayStatus);
      }
    }
    ```

2. <span data-ttu-id="cd294-139">To call the method that you just added, add this code to the Main method:</span><span class="sxs-lookup"><span data-stu-id="cd294-139">To call the method that you just added, add this code to the Main method:</span></span>

    ```   
    GetVirtualMachineAsync(
      credential,
      groupName,
      vmName,
      subscriptionId);
    Console.WriteLine("\nPress enter to continue...");
    Console.ReadLine();
    ```

3. <span data-ttu-id="cd294-140">Save the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="cd294-140">Save the Program.cs file.</span></span>

4. <span data-ttu-id="cd294-141">Click **Start** in Visual Studio, and then sign in to Azure AD using the same username and password that you use with your subscription.</span><span class="sxs-lookup"><span data-stu-id="cd294-141">Click **Start** in Visual Studio, and then sign in to Azure AD using the same username and password that you use with your subscription.</span></span>
   
    <span data-ttu-id="cd294-142">When you run this method, you should see something like this example:</span><span class="sxs-lookup"><span data-stu-id="cd294-142">When you run this method, you should see something like this example:</span></span>
   
        Getting information about the virtual machine...
        hardwareProfile
          vmSize: Standard_D1_v2
   
        storageProfile
          imageReference
            publisher: MicrosoftWindowsServer
            offer: WindowsServer
            sku: 2012-R2-Datacenter
            version: latest
          osDisk
            osType: Windows
            name: myosdisk
            createOption: FromImage
            uri: http://store1.blob.core.windows.net/vhds/myosdisk.vhd
            caching: ReadWrite
   
          osProfile
            computerName: vm1
            adminUsername: account1
            provisionVMAgent: True
            enableAutomaticUpdates: True
   
          networkProfile
            networkInterface 
              id: /subscriptions/{subscription-id}
                /resourceGroups/rg1/providers/Microsoft.Network/networkInterfaces/nc1
   
          vmAgent
            vmAgentVersion2.7.1198.766
            statuses
            code: ProvisioningState/succeeded
            level: Info
            displayStatus: Ready
            message: GuestAgent is running and accepting new configurations.
            time: 4/13/2016 8:35:32 PM
   
          disks
            name: myosdisk
            statuses
              code: ProvisioningState/succeeded
              level: Info
              displayStatus: Provisioning succeeded
              time: 4/13/2016 8:04:36 PM
   
          VM general status
            provisioningStatus: Succeeded
            id: /subscriptions/{subscription-id}
              /resourceGroups/rg1/providers/Microsoft.Compute/virtualMachines/vm1
            name: vm1
            type: Microsoft.Compute/virtualMachines
            location: centralus
   
          VM instance status
            code: ProvisioningState/succeeded
              level: Info
              displayStatus: Provisioning succeeded
            code: PowerState/running
              level: Info
              displayStatus: VM running

## <a name="stop-a-virtual-machine"></a><span data-ttu-id="cd294-143">Stop a virtual machine</span><span class="sxs-lookup"><span data-stu-id="cd294-143">Stop a virtual machine</span></span>

<span data-ttu-id="cd294-144">You can stop a virtual machine in two ways.</span><span class="sxs-lookup"><span data-stu-id="cd294-144">You can stop a virtual machine in two ways.</span></span> <span data-ttu-id="cd294-145">You can stop a virtual machine and keep all its settings, but continue to be charged for it, or you can stop a virtual machine and deallocate it.</span><span class="sxs-lookup"><span data-stu-id="cd294-145">You can stop a virtual machine and keep all its settings, but continue to be charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="cd294-146">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span><span class="sxs-lookup"><span data-stu-id="cd294-146">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

1. <span data-ttu-id="cd294-147">Comment out any code that you previously added to the Main method, except the code to get the credentials.</span><span class="sxs-lookup"><span data-stu-id="cd294-147">Comment out any code that you previously added to the Main method, except the code to get the credentials.</span></span>

2. <span data-ttu-id="cd294-148">Add this method to the Program class:</span><span class="sxs-lookup"><span data-stu-id="cd294-148">Add this method to the Program class:</span></span>

    ```   
    public static async void StopVirtualMachineAsync(
      TokenCredentials credential, 
      string groupName, 
      string vmName, 
      string subscriptionId)
    {
      Console.WriteLine("Stopping the virtual machine...");
      var computeManagementClient = new ComputeManagementClient(credential)
        { SubscriptionId = subscriptionId };
      await computeManagementClient.VirtualMachines.PowerOffAsync(groupName, vmName);
    }
    ```

    <span data-ttu-id="cd294-149">If you want to deallocate the virtual machine, change the PowerOff call to this code:</span><span class="sxs-lookup"><span data-stu-id="cd294-149">If you want to deallocate the virtual machine, change the PowerOff call to this code:</span></span>
    
    ```
    computeManagementClient.VirtualMachines.Deallocate(groupName, vmName);
    ```

3. <span data-ttu-id="cd294-150">To call the method that you just added, add this code to the Main method:</span><span class="sxs-lookup"><span data-stu-id="cd294-150">To call the method that you just added, add this code to the Main method:</span></span>
    
    ```
    StopVirtualMachineAsync(
      credential,
      groupName,
      vmName,
      subscriptionId);
    Console.WriteLine("\nPress enter to continue...");
    Console.ReadLine();
    ```

4. <span data-ttu-id="cd294-151">Save the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="cd294-151">Save the Program.cs file.</span></span>

5. <span data-ttu-id="cd294-152">Click **Start** in Visual Studio, and then sign in to Azure AD using the same username and password that you use with your subscription.</span><span class="sxs-lookup"><span data-stu-id="cd294-152">Click **Start** in Visual Studio, and then sign in to Azure AD using the same username and password that you use with your subscription.</span></span>
   
    <span data-ttu-id="cd294-153">You should see the status of the virtual machine change to Stopped.</span><span class="sxs-lookup"><span data-stu-id="cd294-153">You should see the status of the virtual machine change to Stopped.</span></span> <span data-ttu-id="cd294-154">If you ran the method calling Deallocate, the status is Stopped (deallocated).</span><span class="sxs-lookup"><span data-stu-id="cd294-154">If you ran the method calling Deallocate, the status is Stopped (deallocated).</span></span>

## <a name="start-a-virtual-machine"></a><span data-ttu-id="cd294-155">Start a virtual machine</span><span class="sxs-lookup"><span data-stu-id="cd294-155">Start a virtual machine</span></span>

1. <span data-ttu-id="cd294-156">Comment out any code that you previously added to the Main method, except the code to get the credentials.</span><span class="sxs-lookup"><span data-stu-id="cd294-156">Comment out any code that you previously added to the Main method, except the code to get the credentials.</span></span>

2. <span data-ttu-id="cd294-157">Add this method to the Program class:</span><span class="sxs-lookup"><span data-stu-id="cd294-157">Add this method to the Program class:</span></span>

    ```   
    public static async void StartVirtualMachineAsync(
      TokenCredentials credential, 
      string groupName, 
      string vmName, 
      string subscriptionId)
    {
      Console.WriteLine("Starting the virtual machine...");
      var computeManagementClient = new ComputeManagementClient(credential)
        { SubscriptionId = subscriptionId };
      await computeManagementClient.VirtualMachines.StartAsync(groupName, vmName);
    }
    ```

3. <span data-ttu-id="cd294-158">To call the method that you just added, add this code to the Main method:</span><span class="sxs-lookup"><span data-stu-id="cd294-158">To call the method that you just added, add this code to the Main method:</span></span>

    ```   
    StartVirtualMachineAsync(
      credential,
      groupName,
      vmName,
      subscriptionId);
    Console.WriteLine("\nPress enter to continue...");
    Console.ReadLine();
    ```

4. <span data-ttu-id="cd294-159">Save the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="cd294-159">Save the Program.cs file.</span></span>

5. <span data-ttu-id="cd294-160">Click **Start** in Visual Studio, and then sign in to Azure AD using the same username and password that you use with your subscription.</span><span class="sxs-lookup"><span data-stu-id="cd294-160">Click **Start** in Visual Studio, and then sign in to Azure AD using the same username and password that you use with your subscription.</span></span>
   
    <span data-ttu-id="cd294-161">You should see the status of the virtual machine change to Running.</span><span class="sxs-lookup"><span data-stu-id="cd294-161">You should see the status of the virtual machine change to Running.</span></span>

## <a name="restart-a-running-virtual-machine"></a><span data-ttu-id="cd294-162">Restart a running virtual machine</span><span class="sxs-lookup"><span data-stu-id="cd294-162">Restart a running virtual machine</span></span>

1. <span data-ttu-id="cd294-163">Comment out any code that you previously added to the Main method, except the code to get the credentials.</span><span class="sxs-lookup"><span data-stu-id="cd294-163">Comment out any code that you previously added to the Main method, except the code to get the credentials.</span></span>

2. <span data-ttu-id="cd294-164">Add this method to the Program class:</span><span class="sxs-lookup"><span data-stu-id="cd294-164">Add this method to the Program class:</span></span>

    ```   
    public static async void RestartVirtualMachineAsync(
      TokenCredentials credential,
      string groupName,
      string vmName,
      string subscriptionId)
    {
      Console.WriteLine("Restarting the virtual machine...");
      var computeManagementClient = new ComputeManagementClient(credential)
        { SubscriptionId = subscriptionId };
      await computeManagementClient.VirtualMachines.RestartAsync(groupName, vmName);
    }
    ```

3. <span data-ttu-id="cd294-165">To call the method that you just added, add this code to the Main method:</span><span class="sxs-lookup"><span data-stu-id="cd294-165">To call the method that you just added, add this code to the Main method:</span></span>

    ```   
    RestartVirtualMachineAsync(
      credential,
      groupName,
      vmName,
      subscriptionId);
    Console.WriteLine("\nPress enter to continue...");
    Console.ReadLine();
    ```

4. <span data-ttu-id="cd294-166">Save the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="cd294-166">Save the Program.cs file.</span></span>

5. <span data-ttu-id="cd294-167">Click **Start** in Visual Studio, and then sign in to Azure AD using the same username and password that you use with your subscription.</span><span class="sxs-lookup"><span data-stu-id="cd294-167">Click **Start** in Visual Studio, and then sign in to Azure AD using the same username and password that you use with your subscription.</span></span>

## <a name="resize-a-virtual-machine"></a><span data-ttu-id="cd294-168">Resize a virtual machine</span><span class="sxs-lookup"><span data-stu-id="cd294-168">Resize a virtual machine</span></span>

<span data-ttu-id="cd294-169">This example shows you how to change the size of a running virtual machine.</span><span class="sxs-lookup"><span data-stu-id="cd294-169">This example shows you how to change the size of a running virtual machine.</span></span>

1. <span data-ttu-id="cd294-170">Comment out any code that you previously added to the Main method, except the code to get the credentials.</span><span class="sxs-lookup"><span data-stu-id="cd294-170">Comment out any code that you previously added to the Main method, except the code to get the credentials.</span></span>

2. <span data-ttu-id="cd294-171">Add this method to the Program class:</span><span class="sxs-lookup"><span data-stu-id="cd294-171">Add this method to the Program class:</span></span>

    ```   
    public static async void UpdateVirtualMachineAsync(
      TokenCredentials credential, 
      string groupName, 
      string vmName, 
      string subscriptionId)
    {
      Console.WriteLine("Updating the virtual machine...");
      var computeManagementClient = new ComputeManagementClient(credential)
        { SubscriptionId = subscriptionId };
      var vmResult = await computeManagementClient.VirtualMachines.GetAsync(groupName, vmName);
      vmResult.HardwareProfile.VmSize = "Standard_D2_v2";
      await computeManagementClient.VirtualMachines.CreateOrUpdateAsync(groupName, vmName, vmResult);
    }
    ```

3. <span data-ttu-id="cd294-172">To call the method that you just added, add this code to the Main method:</span><span class="sxs-lookup"><span data-stu-id="cd294-172">To call the method that you just added, add this code to the Main method:</span></span>

    ```   
    UpdateVirtualMachineAsync(
      credential,
      groupName,
      vmName,
      subscriptionId);
    Console.WriteLine("\nPress enter to continue...");
    Console.ReadLine();
    ```

4. <span data-ttu-id="cd294-173">Save the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="cd294-173">Save the Program.cs file.</span></span>

5. <span data-ttu-id="cd294-174">Click **Start** in Visual Studio, and then sign in to Azure AD using the same username and password that you use with your subscription.</span><span class="sxs-lookup"><span data-stu-id="cd294-174">Click **Start** in Visual Studio, and then sign in to Azure AD using the same username and password that you use with your subscription.</span></span>
   
    <span data-ttu-id="cd294-175">You should see the size of the virtual machine change to Standard_D2_v2.</span><span class="sxs-lookup"><span data-stu-id="cd294-175">You should see the size of the virtual machine change to Standard_D2_v2.</span></span>

## <a name="add-a-data-disk-to-a-virtual-machine"></a><span data-ttu-id="cd294-176">Add a data disk to a virtual machine</span><span class="sxs-lookup"><span data-stu-id="cd294-176">Add a data disk to a virtual machine</span></span>

<span data-ttu-id="cd294-177">This example shows you how to add a data disk to a running virtual machine.</span><span class="sxs-lookup"><span data-stu-id="cd294-177">This example shows you how to add a data disk to a running virtual machine.</span></span>

1. <span data-ttu-id="cd294-178">Comment out any code that you previously added to the Main method, except the code to get the credentials.</span><span class="sxs-lookup"><span data-stu-id="cd294-178">Comment out any code that you previously added to the Main method, except the code to get the credentials.</span></span>

2. <span data-ttu-id="cd294-179">Add this method to the Program class:</span><span class="sxs-lookup"><span data-stu-id="cd294-179">Add this method to the Program class:</span></span>

    ```   
    public static async void AddDataDiskAsync(
      TokenCredentials credential, 
      string groupName, 
      string vmName, 
      string subscriptionId)
    {
      Console.WriteLine("Adding the disk to the virtual machine...");
      var computeManagementClient = new ComputeManagementClient(credential)
        { SubscriptionId = subscriptionId };
      var vmResult = await computeManagementClient.VirtualMachines.GetAsync(groupName, vmName);
      vmResult.StorageProfile.DataDisks.Add(
        new DataDisk
          {
            Lun = 0,
            Name = "mydatadisk1",
            Vhd = new VirtualHardDisk
              {
                Uri = "https://mystorage1.blob.core.windows.net/vhds/mydatadisk1.vhd"
              },
            CreateOption = DiskCreateOptionTypes.Empty,
            DiskSizeGB = 2,
            Caching = CachingTypes.ReadWrite
          });
      await computeManagementClient.VirtualMachines.CreateOrUpdateAsync(groupName, vmName, vmResult);
    }
    ```

    <span data-ttu-id="cd294-180">Replace mystorage1 with the name of the storage account where disks are stored for your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="cd294-180">Replace mystorage1 with the name of the storage account where disks are stored for your virtual machine.</span></span>

3. <span data-ttu-id="cd294-181">To call the method that you just added, add this code to the Main method:</span><span class="sxs-lookup"><span data-stu-id="cd294-181">To call the method that you just added, add this code to the Main method:</span></span>
    
    ```
    AddDataDiskAsync(
      credential,
      groupName,
      vmName,
      subscriptionId);
    Console.WriteLine("\nPress enter to continue...");
    Console.ReadLine();
    ```

4. <span data-ttu-id="cd294-182">Save the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="cd294-182">Save the Program.cs file.</span></span>

5. <span data-ttu-id="cd294-183">Click **Start** in Visual Studio, and then sign in to Azure AD using the same username and password that you use with your subscription.</span><span class="sxs-lookup"><span data-stu-id="cd294-183">Click **Start** in Visual Studio, and then sign in to Azure AD using the same username and password that you use with your subscription.</span></span>

## <a name="delete-a-virtual-machine"></a><span data-ttu-id="cd294-184">Delete a virtual machine</span><span class="sxs-lookup"><span data-stu-id="cd294-184">Delete a virtual machine</span></span>

1. <span data-ttu-id="cd294-185">Comment out any code that you previously added to the Main method, except the code to get the credentials.</span><span class="sxs-lookup"><span data-stu-id="cd294-185">Comment out any code that you previously added to the Main method, except the code to get the credentials.</span></span>

2. <span data-ttu-id="cd294-186">Add this method to the Program class:</span><span class="sxs-lookup"><span data-stu-id="cd294-186">Add this method to the Program class:</span></span>
   
    ```
    public static async void DeleteVirtualMachineAsync(
      TokenCredentials credential, 
      string groupName, 
      string vmName, 
      string subscriptionId)
    {
      Console.WriteLine("Deleting the virtual machine...");
      var computeManagementClient = new ComputeManagementClient(credential)
        { SubscriptionId = subscriptionId };
      await computeManagementClient.VirtualMachines.DeleteAsync(groupName, vmName);
    }
    ```

3. <span data-ttu-id="cd294-187">To call the method that you just added, add this code to the Main method:</span><span class="sxs-lookup"><span data-stu-id="cd294-187">To call the method that you just added, add this code to the Main method:</span></span>
    
    ```
    DeleteVirtualMachineAsync(
      credential,
      groupName,
      vmName,
      subscriptionId);
    Console.WriteLine("\nPress enter to continue...");
    Console.ReadLine();
    ```

4. <span data-ttu-id="cd294-188">Save the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="cd294-188">Save the Program.cs file.</span></span>

5. <span data-ttu-id="cd294-189">Click **Start** in Visual Studio, and then sign in to Azure AD using the same username and password that you use with your subscription.</span><span class="sxs-lookup"><span data-stu-id="cd294-189">Click **Start** in Visual Studio, and then sign in to Azure AD using the same username and password that you use with your subscription.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd294-190">Next Steps</span><span class="sxs-lookup"><span data-stu-id="cd294-190">Next Steps</span></span>

- <span data-ttu-id="cd294-191">If there were issues with a deployment, you might look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="cd294-191">If there were issues with a deployment, you might look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
- <span data-ttu-id="cd294-192">Learn how to deploy a virtual machine and its supporting resources by reviewing [Deploy an Azure Virtual Machine Using C#](csharp.md).</span><span class="sxs-lookup"><span data-stu-id="cd294-192">Learn how to deploy a virtual machine and its supporting resources by reviewing [Deploy an Azure Virtual Machine Using C#](csharp.md).</span></span>
- <span data-ttu-id="cd294-193">Take advantage of using a template to create a virtual machine by using the information in [Deploy an Azure Virtual Machine using C# and a Resource Manager template](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cd294-193">Take advantage of using a template to create a virtual machine by using the information in [Deploy an Azure Virtual Machine using C# and a Resource Manager template](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


