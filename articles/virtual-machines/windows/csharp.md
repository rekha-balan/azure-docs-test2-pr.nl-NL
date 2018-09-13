---
title: Deploy an Azure Virtual Machine Using C# | Microsoft Docs
description: Use C# and Azure Resource Manager to deploy a virtual machine and all its supporting resources.
services: virtual-machines-windows
documentationcenter: ''
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 87524373-5f52-4f4b-94af-50bf7b65c277
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: davidmu
ms.openlocfilehash: 5b90e961377ec9d3d88715bb29b39dfc2fe20115
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550581"
---
# <a name="deploy-an-azure-virtual-machine-using-c"></a><span data-ttu-id="a85a2-103">Deploy an Azure Virtual Machine Using C#</span><span class="sxs-lookup"><span data-stu-id="a85a2-103">Deploy an Azure Virtual Machine Using C#</span></span> #

<span data-ttu-id="a85a2-104">This article shows you how use C# to create an Azure virtual machine and its supporting resources.</span><span class="sxs-lookup"><span data-stu-id="a85a2-104">This article shows you how use C# to create an Azure virtual machine and its supporting resources.</span></span>

<span data-ttu-id="a85a2-105">It takes about 20 minutes to do these steps.</span><span class="sxs-lookup"><span data-stu-id="a85a2-105">It takes about 20 minutes to do these steps.</span></span>

## <a name="step-1-create-a-visual-studio-project"></a><span data-ttu-id="a85a2-106">Step 1: Create a Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="a85a2-106">Step 1: Create a Visual Studio project</span></span>

<span data-ttu-id="a85a2-107">In this step, you make sure that Visual Studio is installed and you create a console application used to create the resources.</span><span class="sxs-lookup"><span data-stu-id="a85a2-107">In this step, you make sure that Visual Studio is installed and you create a console application used to create the resources.</span></span>

1. <span data-ttu-id="a85a2-108">If you haven't already, install [Visual Studio](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="a85a2-108">If you haven't already, install [Visual Studio](https://www.visualstudio.com/).</span></span>
2. <span data-ttu-id="a85a2-109">In Visual Studio, click **File** > **New** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="a85a2-109">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="a85a2-110">In **Templates** > **Visual C#**, select **Console Application**, enter the name and location of the project, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="a85a2-110">In **Templates** > **Visual C#**, select **Console Application**, enter the name and location of the project, and then click **OK**.</span></span>

## <a name="step-2-install-libraries"></a><span data-ttu-id="a85a2-111">Step 2: Install libraries</span><span class="sxs-lookup"><span data-stu-id="a85a2-111">Step 2: Install libraries</span></span>

<span data-ttu-id="a85a2-112">NuGet packages are the easiest way to install the libraries that you need to finish these steps.</span><span class="sxs-lookup"><span data-stu-id="a85a2-112">NuGet packages are the easiest way to install the libraries that you need to finish these steps.</span></span> <span data-ttu-id="a85a2-113">To get the libraries that you need in Visual Studio, do these steps:</span><span class="sxs-lookup"><span data-stu-id="a85a2-113">To get the libraries that you need in Visual Studio, do these steps:</span></span>


1. <span data-ttu-id="a85a2-114">Right-click the project name in the Solution Explorer, click **Manage NuGet Packages**, and then click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="a85a2-114">Right-click the project name in the Solution Explorer, click **Manage NuGet Packages**, and then click **Browse**.</span></span>
2. <span data-ttu-id="a85a2-115">Type *Microsoft.IdentityModel.Clients.ActiveDirectory* in the search box, click **Install**, and then follow the instructions to install the package.</span><span class="sxs-lookup"><span data-stu-id="a85a2-115">Type *Microsoft.IdentityModel.Clients.ActiveDirectory* in the search box, click **Install**, and then follow the instructions to install the package.</span></span>
3. <span data-ttu-id="a85a2-116">At the top of the page, select **Include Prerelease**.</span><span class="sxs-lookup"><span data-stu-id="a85a2-116">At the top of the page, select **Include Prerelease**.</span></span> <span data-ttu-id="a85a2-117">Type *Microsoft.Azure.Management.Compute* in the search box, click **Install**, and then follow the instructions to install the package.</span><span class="sxs-lookup"><span data-stu-id="a85a2-117">Type *Microsoft.Azure.Management.Compute* in the search box, click **Install**, and then follow the instructions to install the package.</span></span>
4. <span data-ttu-id="a85a2-118">Type *Microsoft.Azure.Management.Network* in the search box, click **Install**, and then follow the instructions to install the package.</span><span class="sxs-lookup"><span data-stu-id="a85a2-118">Type *Microsoft.Azure.Management.Network* in the search box, click **Install**, and then follow the instructions to install the package.</span></span>
5. <span data-ttu-id="a85a2-119">Type *Microsoft.Azure.Management.Storage* in the search box, click **Install**, and then follow the instructions to install the package.</span><span class="sxs-lookup"><span data-stu-id="a85a2-119">Type *Microsoft.Azure.Management.Storage* in the search box, click **Install**, and then follow the instructions to install the package.</span></span>
6. <span data-ttu-id="a85a2-120">Type *Microsoft.Azure.Management.ResourceManager* in the search box, click **Install**, and then follow the instructions to install the package.</span><span class="sxs-lookup"><span data-stu-id="a85a2-120">Type *Microsoft.Azure.Management.ResourceManager* in the search box, click **Install**, and then follow the instructions to install the package.</span></span>

<span data-ttu-id="a85a2-121">Now you're ready to start using the libraries to create your application.</span><span class="sxs-lookup"><span data-stu-id="a85a2-121">Now you're ready to start using the libraries to create your application.</span></span>

## <a name="step-3-create-the-credentials-used-to-authenticate-requests"></a><span data-ttu-id="a85a2-122">Step 3: Create the credentials used to authenticate requests</span><span class="sxs-lookup"><span data-stu-id="a85a2-122">Step 3: Create the credentials used to authenticate requests</span></span>

<span data-ttu-id="a85a2-123">Before you start this step, make sure that you have access to an [Active Directory service principal](../../resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="a85a2-123">Before you start this step, make sure that you have access to an [Active Directory service principal](../../resource-group-authenticate-service-principal.md).</span></span> <span data-ttu-id="a85a2-124">From the service principal, you acquire a token for authenticating requests to Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a85a2-124">From the service principal, you acquire a token for authenticating requests to Azure Resource Manager.</span></span>

1. <span data-ttu-id="a85a2-125">Open the Program.cs file for the project that you created, and then add these using statements to the top of the file:</span><span class="sxs-lookup"><span data-stu-id="a85a2-125">Open the Program.cs file for the project that you created, and then add these using statements to the top of the file:</span></span>
   
    ```
    using Microsoft.Azure;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.Azure.Management.Storage;
    using Microsoft.Azure.Management.Storage.Models;
    using Microsoft.Azure.Management.Network;
    using Microsoft.Azure.Management.Network.Models;
    using Microsoft.Azure.Management.Compute;
    using Microsoft.Azure.Management.Compute.Models;
    using Microsoft.Rest;
    ```

2. <span data-ttu-id="a85a2-126">To get the token that's needed to create the credentials, add this method to the Program class:</span><span class="sxs-lookup"><span data-stu-id="a85a2-126">To get the token that's needed to create the credentials, add this method to the Program class:</span></span>
   
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

    <span data-ttu-id="a85a2-127">Replace these values:</span><span class="sxs-lookup"><span data-stu-id="a85a2-127">Replace these values:</span></span>
    
    - <span data-ttu-id="a85a2-128">*{client-id}* with the identifier of the Azure Active Directory application.</span><span class="sxs-lookup"><span data-stu-id="a85a2-128">*{client-id}* with the identifier of the Azure Active Directory application.</span></span> <span data-ttu-id="a85a2-129">You can find this identifier on the Properties blade of your AD application.</span><span class="sxs-lookup"><span data-stu-id="a85a2-129">You can find this identifier on the Properties blade of your AD application.</span></span> <span data-ttu-id="a85a2-130">To find your AD application in the Azure portal, click **Azure Active Directory** in the resource menu, and then click **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="a85a2-130">To find your AD application in the Azure portal, click **Azure Active Directory** in the resource menu, and then click **App registrations**.</span></span>
    - <span data-ttu-id="a85a2-131">*{client-secret}* with the access key of the AD application.</span><span class="sxs-lookup"><span data-stu-id="a85a2-131">*{client-secret}* with the access key of the AD application.</span></span> <span data-ttu-id="a85a2-132">You can find this identifier on the Properties blade of your AD application.</span><span class="sxs-lookup"><span data-stu-id="a85a2-132">You can find this identifier on the Properties blade of your AD application.</span></span>
    - <span data-ttu-id="a85a2-133">*{tenant-id}* with the tenant identifier of your subscription.</span><span class="sxs-lookup"><span data-stu-id="a85a2-133">*{tenant-id}* with the tenant identifier of your subscription.</span></span> <span data-ttu-id="a85a2-134">You can find the tenant identifier on the Properties blade for Azure Active Directory in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a85a2-134">You can find the tenant identifier on the Properties blade for Azure Active Directory in the Azure portal.</span></span> <span data-ttu-id="a85a2-135">It is labeled *Directory ID*.</span><span class="sxs-lookup"><span data-stu-id="a85a2-135">It is labeled *Directory ID*.</span></span>

3. <span data-ttu-id="a85a2-136">To call the method that you previously added, add this code to the Main method in the Program.cs file:</span><span class="sxs-lookup"><span data-stu-id="a85a2-136">To call the method that you previously added, add this code to the Main method in the Program.cs file:</span></span>
   
    ```
    var token = GetAccessTokenAsync();
    var credential = new TokenCredentials(token.Result.AccessToken);
    ```

4. <span data-ttu-id="a85a2-137">Save the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="a85a2-137">Save the Program.cs file.</span></span>

## <a name="step-3-create-the-resources"></a><span data-ttu-id="a85a2-138">Step 3: Create the resources</span><span class="sxs-lookup"><span data-stu-id="a85a2-138">Step 3: Create the resources</span></span>

### <a name="register-the-providers-and-create-a-resource-group"></a><span data-ttu-id="a85a2-139">Register the providers and create a resource group</span><span class="sxs-lookup"><span data-stu-id="a85a2-139">Register the providers and create a resource group</span></span>

<span data-ttu-id="a85a2-140">All resources must be contained in a resource group.</span><span class="sxs-lookup"><span data-stu-id="a85a2-140">All resources must be contained in a resource group.</span></span> <span data-ttu-id="a85a2-141">Before you can add resources to a group, your subscription must be registered with the resource providers.</span><span class="sxs-lookup"><span data-stu-id="a85a2-141">Before you can add resources to a group, your subscription must be registered with the resource providers.</span></span>

1. <span data-ttu-id="a85a2-142">Add variables to the Main method of the Program class to specify the names that you want to use for the resources:</span><span class="sxs-lookup"><span data-stu-id="a85a2-142">Add variables to the Main method of the Program class to specify the names that you want to use for the resources:</span></span>

    ```   
    var groupName = "myResourceGroup";
    var subscriptionId = "subsciptionId";
    var storageName = "myStorageAccount";
    var ipName = "myPublicIP";
    var subnetName = "mySubnet";
    var vnetName = "myVnet";
    var nicName = "myNIC";
    var avSetName = "myAVSet";
    var vmName = "myVM";  
    var location = "location";
    var adminName = "adminName";
    var adminPassword = "adminPassword";
    ```

    <span data-ttu-id="a85a2-143">Replace these values:</span><span class="sxs-lookup"><span data-stu-id="a85a2-143">Replace these values:</span></span>

    - <span data-ttu-id="a85a2-144">All resource names that start with *my*, with names that make sense for your environment.</span><span class="sxs-lookup"><span data-stu-id="a85a2-144">All resource names that start with *my*, with names that make sense for your environment.</span></span>
    - <span data-ttu-id="a85a2-145">*subscriptionId* with your subscription identifier.</span><span class="sxs-lookup"><span data-stu-id="a85a2-145">*subscriptionId* with your subscription identifier.</span></span> <span data-ttu-id="a85a2-146">You can find the subscription identifier on the Subscriptions blade of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a85a2-146">You can find the subscription identifier on the Subscriptions blade of the Azure portal.</span></span>
    - <span data-ttu-id="a85a2-147">*location* with the [Azure region](https://azure.microsoft.com/regions/) where you want to create the resources.</span><span class="sxs-lookup"><span data-stu-id="a85a2-147">*location* with the [Azure region](https://azure.microsoft.com/regions/) where you want to create the resources.</span></span>
    - <span data-ttu-id="a85a2-148">*adminName* with the name of the administrator account on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a85a2-148">*adminName* with the name of the administrator account on the virtual machine.</span></span>
    - <span data-ttu-id="a85a2-149">*adminPassword* with the password of the administrator account.</span><span class="sxs-lookup"><span data-stu-id="a85a2-149">*adminPassword* with the password of the administrator account.</span></span>

2. <span data-ttu-id="a85a2-150">To create the resource group and register the providers, add this method to the Program class:</span><span class="sxs-lookup"><span data-stu-id="a85a2-150">To create the resource group and register the providers, add this method to the Program class:</span></span>
   
    ```
    public static async Task<ResourceGroup> CreateResourceGroupAsync(
      TokenCredentials credential,
      string groupName,
      string subscriptionId,
      string location)
    {
      var resourceManagementClient = new ResourceManagementClient(credential)
        { SubscriptionId = subscriptionId };
   
      Console.WriteLine("Registering the providers...");
      var rpResult = resourceManagementClient.Providers.Register("Microsoft.Storage");
      Console.WriteLine(rpResult.RegistrationState);
      rpResult = resourceManagementClient.Providers.Register("Microsoft.Network");
      Console.WriteLine(rpResult.RegistrationState);
      rpResult = resourceManagementClient.Providers.Register("Microsoft.Compute");
      Console.WriteLine(rpResult.RegistrationState);
   
      Console.WriteLine("Creating the resource group...");
      var resourceGroup = new ResourceGroup { Location = location };
      return await resourceManagementClient.ResourceGroups.CreateOrUpdateAsync(
        groupName, 
        resourceGroup);
    }
    ```

3. <span data-ttu-id="a85a2-151">To call the method that you previously added, add this code to the Main method:</span><span class="sxs-lookup"><span data-stu-id="a85a2-151">To call the method that you previously added, add this code to the Main method:</span></span>
   
    ```   
    var rgResult = CreateResourceGroupAsync(
      credential,
      groupName,
      subscriptionId,
      location);
    Console.WriteLine(rgResult.Result.Properties.ProvisioningState);
    Console.ReadLine();
    ```

### <a name="create-a-storage-account"></a><span data-ttu-id="a85a2-152">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="a85a2-152">Create a storage account</span></span>

<span data-ttu-id="a85a2-153">When using an unmanaged disk, a [storage account](../../storage/storage-create-storage-account.md) is needed to store the virtual hard disk file that is created for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a85a2-153">When using an unmanaged disk, a [storage account](../../storage/storage-create-storage-account.md) is needed to store the virtual hard disk file that is created for the virtual machine.</span></span>

1. <span data-ttu-id="a85a2-154">To create the storage account, add this method to the Program class:</span><span class="sxs-lookup"><span data-stu-id="a85a2-154">To create the storage account, add this method to the Program class:</span></span>

    ```   
    public static async Task<StorageAccount> CreateStorageAccountAsync(
      TokenCredentials credential,       
      string groupName,
      string subscriptionId,
      string location,
      string storageName)
    {
      var storageManagementClient = new StorageManagementClient(credential)
        { SubscriptionId = subscriptionId };
      
      Console.WriteLine("Creating the storage account...");

      return await storageManagementClient.StorageAccounts.CreateAsync(
        groupName,
        storageName,
        new StorageAccountCreateParameters()
          {
            Sku = new Microsoft.Azure.Management.Storage.Models.Sku() 
              { Name = SkuName.StandardLRS},
            Kind = Kind.Storage,
            Location = location
          }
      );
    }
    ```

2. <span data-ttu-id="a85a2-155">To call the method that you previously added, add this code to the Main method:</span><span class="sxs-lookup"><span data-stu-id="a85a2-155">To call the method that you previously added, add this code to the Main method:</span></span>
   
    ```
    var stResult = CreateStorageAccountAsync(
      credential,
      groupName,
      subscriptionId,
      location,
      storageName);
    Console.WriteLine(stResult.Result.ProvisioningState);  
    Console.ReadLine();
    ```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="a85a2-156">Create a public IP address</span><span class="sxs-lookup"><span data-stu-id="a85a2-156">Create a public IP address</span></span>

<span data-ttu-id="a85a2-157">A public IP address is needed to communicate with the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a85a2-157">A public IP address is needed to communicate with the virtual machine.</span></span>

1. <span data-ttu-id="a85a2-158">To create the public IP address for the virtual machine, add this method to the Program class:</span><span class="sxs-lookup"><span data-stu-id="a85a2-158">To create the public IP address for the virtual machine, add this method to the Program class:</span></span>
   
    ```
    public static async Task<PublicIPAddress> CreatePublicIPAddressAsync(
      TokenCredentials credential,  
      string groupName,
      string subscriptionId,
      string location,
      string ipName)
    {
      var networkManagementClient = new NetworkManagementClient(credential)
        { SubscriptionId = subscriptionId };
      
      Console.WriteLine("Creating the public ip...");

      return await networkManagementClient.PublicIPAddresses.CreateOrUpdateAsync(
        groupName,
        ipName,
        new PublicIPAddress
          {
            Location = location,
            PublicIPAllocationMethod = "Dynamic"
          }
      );
    }
    ```

2. <span data-ttu-id="a85a2-159">To call the method that you previously added, add this code to the Main method:</span><span class="sxs-lookup"><span data-stu-id="a85a2-159">To call the method that you previously added, add this code to the Main method:</span></span>
   
    ```   
    var ipResult = CreatePublicIPAddressAsync(
      credential,
      groupName,
      subscriptionId,
      location,
      ipName);
    Console.WriteLine(ipResult.Result.ProvisioningState);  
    Console.ReadLine();
    ```

### <a name="create-a-virtual-network"></a><span data-ttu-id="a85a2-160">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="a85a2-160">Create a virtual network</span></span>

<span data-ttu-id="a85a2-161">A virtual machine that's created with the Resource Manager deployment model must be in a virtual network.</span><span class="sxs-lookup"><span data-stu-id="a85a2-161">A virtual machine that's created with the Resource Manager deployment model must be in a virtual network.</span></span>

1. <span data-ttu-id="a85a2-162">To create a subnet and a virtual network, add this method to the Program class:</span><span class="sxs-lookup"><span data-stu-id="a85a2-162">To create a subnet and a virtual network, add this method to the Program class:</span></span>

    ```   
    public static async Task<VirtualNetwork> CreateVirtualNetworkAsync(
      TokenCredentials credential,
      string groupName,
      string subscriptionId,
      string location,
      string vnetName,
      string subnetName)
    {
      var networkManagementClient = new NetworkManagementClient(credential)
        { SubscriptionId = subscriptionId };
   
      var subnet = new Subnet
        {
          Name = subnetName,
          AddressPrefix = "10.0.0.0/24"
        };
   
      var address = new AddressSpace 
        {
          AddressPrefixes = new List<string> { "10.0.0.0/16" }
        };
         
      Console.WriteLine("Creating the virtual network...");
      return await networkManagementClient.VirtualNetworks.CreateOrUpdateAsync(
        groupName,
        vnetName,
        new VirtualNetwork
          {
            Location = location,
            AddressSpace = address,
            Subnets = new List<Subnet> { subnet }
          }
      );
    }
    ```

2. <span data-ttu-id="a85a2-163">To call the method that you previously added, add this code to the Main method:</span><span class="sxs-lookup"><span data-stu-id="a85a2-163">To call the method that you previously added, add this code to the Main method:</span></span>

    ```   
    var vnResult = CreateVirtualNetworkAsync(
      credential,
      groupName,
      subscriptionId,
      location,
      vnetName,
      subnetName);
    Console.WriteLine(vnResult.Result.ProvisioningState);  
    Console.ReadLine();
    ```

### <a name="create-a-network-interface"></a><span data-ttu-id="a85a2-164">Create a network interface</span><span class="sxs-lookup"><span data-stu-id="a85a2-164">Create a network interface</span></span>

<span data-ttu-id="a85a2-165">A virtual machine needs a network interface to communicate on the virtual network.</span><span class="sxs-lookup"><span data-stu-id="a85a2-165">A virtual machine needs a network interface to communicate on the virtual network.</span></span>

1. <span data-ttu-id="a85a2-166">To create a network interface, add this method to the Program class:</span><span class="sxs-lookup"><span data-stu-id="a85a2-166">To create a network interface, add this method to the Program class:</span></span>

    ```   
    public static async Task<NetworkInterface> CreateNetworkInterfaceAsync(
      TokenCredentials credential,
      string groupName,
      string subscriptionId,
      string location,
      string subnetName,
      string vnetName,
      string ipName,
      string nicName)
    {
      var networkManagementClient = new NetworkManagementClient(credential)
        { SubscriptionId = subscriptionId };
      var subnet = await networkManagementClient.Subnets.GetAsync(
        groupName,
        vnetName,
        subnetName
      );
      var publicIP = await networkManagementClient.PublicIPAddresses.GetAsync(
        groupName, 
        ipName
      );
   
      Console.WriteLine("Creating the network interface...");
      return await networkManagementClient.NetworkInterfaces.CreateOrUpdateAsync(
        groupName,
        nicName,
        new NetworkInterface
          {
            Location = location,
            IpConfigurations = new List<NetworkInterfaceIPConfiguration>
              {
                new NetworkInterfaceIPConfiguration
                  {
                    Name = nicName,
                    PublicIPAddress = pubipResponse,
                    Subnet = subnetResponse
                  }
              }
          }
      );
    }
    ```

2. <span data-ttu-id="a85a2-167">To call the method that you previously added, add this code to the Main method:</span><span class="sxs-lookup"><span data-stu-id="a85a2-167">To call the method that you previously added, add this code to the Main method:</span></span>
   
    ```
    var ncResult = CreateNetworkInterfaceAsync(
      credential,
      groupName,
      subscriptionId,
      location,
      subnetName,
      vnetName,
      ipName,
      nicName);
    Console.WriteLine(ncResult.Result.ProvisioningState);  
    Console.ReadLine();
    ```

### <a name="create-an-availability-set"></a><span data-ttu-id="a85a2-168">Create an availability set</span><span class="sxs-lookup"><span data-stu-id="a85a2-168">Create an availability set</span></span>

<span data-ttu-id="a85a2-169">Availability sets make it easier for you to manage the maintenance of the virtual machines used by your application.</span><span class="sxs-lookup"><span data-stu-id="a85a2-169">Availability sets make it easier for you to manage the maintenance of the virtual machines used by your application.</span></span>

1. <span data-ttu-id="a85a2-170">To create the availability set, add this method to the Program class:</span><span class="sxs-lookup"><span data-stu-id="a85a2-170">To create the availability set, add this method to the Program class:</span></span>

    ```   
    public static async Task<AvailabilitySet> CreateAvailabilitySetAsync(
      TokenCredentials credential,
      string groupName,
      string subscriptionId,
      string location,
      string avsetName)
    {
      var computeManagementClient = new ComputeManagementClient(credential)
        { SubscriptionId = subscriptionId };
        
      Console.WriteLine("Creating the availability set...");
      return await computeManagementClient.AvailabilitySets.CreateOrUpdateAsync(
        groupName,
        avsetName,
        new AvailabilitySet()
          { Location = location }
      );
    }
    ```

2. <span data-ttu-id="a85a2-171">To call the method that you previously added, add this code to the Main method:</span><span class="sxs-lookup"><span data-stu-id="a85a2-171">To call the method that you previously added, add this code to the Main method:</span></span>
   
    ```
    var avResult = CreateAvailabilitySetAsync(
      credential,  
      groupName,
      subscriptionId,
      location,
      avSetName);
    Console.ReadLine();
    ```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="a85a2-172">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="a85a2-172">Create a virtual machine</span></span>

<span data-ttu-id="a85a2-173">Now that you created all the supporting resources, you can create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a85a2-173">Now that you created all the supporting resources, you can create a virtual machine.</span></span>

1. <span data-ttu-id="a85a2-174">To create the virtual machine, add this method to the Program class:</span><span class="sxs-lookup"><span data-stu-id="a85a2-174">To create the virtual machine, add this method to the Program class:</span></span>

    ```   
    public static async Task<VirtualMachine> CreateVirtualMachineAsync(
      TokenCredentials credential, 
      string groupName,
      string subscriptionId,
      string location,
      string nicName,
      string avsetName,
      string storageName,
      string adminName,
      string adminPassword,
      string vmName)
    {
      var networkManagementClient = new NetworkManagementClient(credential)
        { SubscriptionId = subscriptionId };
      var computeManagementClient = new ComputeManagementClient(credential)
        { SubscriptionId = subscriptionId };  
      var nic = await networkManagementClient.NetworkInterfaces.GetAsync(
        groupName, 
        nicName);
      var avSet = await computeManagementClient.AvailabilitySets.GetAsync(
        groupName, 
        avsetName);
   
      Console.WriteLine("Creating the virtual machine...");
      return await computeManagementClient.VirtualMachines.CreateOrUpdateAsync(
        groupName,
        vmName,
        new VirtualMachine
          {
            Location = location,
            AvailabilitySet = new Microsoft.Azure.Management.Compute.Models.SubResource
              {
                Id = avSet.Id
              },
            HardwareProfile = new HardwareProfile
              {
                VmSize = "Standard_A0"
              },
            OsProfile = new OSProfile
              {
                AdminUsername = adminName,
                AdminPassword = adminPassword,
                ComputerName = vmName,
                WindowsConfiguration = new WindowsConfiguration
                  {
                    ProvisionVMAgent = true
                  }
              },
            NetworkProfile = new NetworkProfile
              {
                NetworkInterfaces = new List<NetworkInterfaceReference>
                  {
                    new NetworkInterfaceReference { Id = nic.Id }
                  }
              },
            StorageProfile = new StorageProfile
              {
                ImageReference = new ImageReference
                  {
                    Publisher = "MicrosoftWindowsServer",
                    Offer = "WindowsServer",
                    Sku = "2012-R2-Datacenter",
                    Version = "latest"
                  },
                OsDisk = new OSDisk
                  {
                    Name = "mytestod1",
                    CreateOption = DiskCreateOptionTypes.FromImage,
                    Vhd = new VirtualHardDisk
                      {
                        Uri = "http://" + storageName + ".blob.core.windows.net/vhds/mytestod1.vhd"
                      }
                  }
              }
          }
      );
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="a85a2-175">This tutorial creates a virtual machine running a version of the Windows Server operating system.</span><span class="sxs-lookup"><span data-stu-id="a85a2-175">This tutorial creates a virtual machine running a version of the Windows Server operating system.</span></span> <span data-ttu-id="a85a2-176">To learn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and the Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a85a2-176">To learn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and the Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    >

2. <span data-ttu-id="a85a2-177">To call the method that you previously added, add this code to the Main method:</span><span class="sxs-lookup"><span data-stu-id="a85a2-177">To call the method that you previously added, add this code to the Main method:</span></span>
   
    ```
    var vmResult = CreateVirtualMachineAsync(
      credential,
      groupName,
      subscriptionId,
      location,
      nicName,
      avSetName,
      storageName,
      adminName,
      adminPassword,
      vmName);
    Console.WriteLine(vmResult.Result.ProvisioningState);
    Console.ReadLine();
    ```

## <a name="step-4-delete-the-resources"></a><span data-ttu-id="a85a2-178">Step 4: Delete the resources</span><span class="sxs-lookup"><span data-stu-id="a85a2-178">Step 4: Delete the resources</span></span>

<span data-ttu-id="a85a2-179">Because you are charged for resources used in Azure, it is always good practice to delete resources that are no longer needed.</span><span class="sxs-lookup"><span data-stu-id="a85a2-179">Because you are charged for resources used in Azure, it is always good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="a85a2-180">If you want to delete the virtual machines and all the supporting resources, all you have to do is delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="a85a2-180">If you want to delete the virtual machines and all the supporting resources, all you have to do is delete the resource group.</span></span>

1. <span data-ttu-id="a85a2-181">To delete the resource group, add this method to the Program class:</span><span class="sxs-lookup"><span data-stu-id="a85a2-181">To delete the resource group, add this method to the Program class:</span></span>
   
    ```
    public static async void DeleteResourceGroupAsync(
      TokenCredentials credential,
      string groupName,
      string subscriptionId)
    {
      Console.WriteLine("Deleting resource group...");
      var resourceManagementClient = new ResourceManagementClient(credential)
        { SubscriptionId = subscriptionId };
      await resourceManagementClient.ResourceGroups.DeleteAsync(groupName);
    }
    ```

2. <span data-ttu-id="a85a2-182">To call the method that you previously added, add this code to the Main method:</span><span class="sxs-lookup"><span data-stu-id="a85a2-182">To call the method that you previously added, add this code to the Main method:</span></span>
   
    ```   
    DeleteResourceGroupAsync(
      credential,
      groupName,
      subscriptionId);
    Console.ReadLine();
    ```

## <a name="step-5-run-the-console-application"></a><span data-ttu-id="a85a2-183">Step 5: Run the console application</span><span class="sxs-lookup"><span data-stu-id="a85a2-183">Step 5: Run the console application</span></span>

1. <span data-ttu-id="a85a2-184">To run the console application, click **Start** in Visual Studio, and then sign in to Azure AD using the same username and password that you use with your subscription.</span><span class="sxs-lookup"><span data-stu-id="a85a2-184">To run the console application, click **Start** in Visual Studio, and then sign in to Azure AD using the same username and password that you use with your subscription.</span></span>

2. <span data-ttu-id="a85a2-185">Press **Enter** after the *Succeeded* status appears.</span><span class="sxs-lookup"><span data-stu-id="a85a2-185">Press **Enter** after the *Succeeded* status appears.</span></span> 
   
3. <span data-ttu-id="a85a2-186">After the virtual machine is created and before you press **Enter** to start deleting resources, you could take a few minutes to inspect the resources in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a85a2-186">After the virtual machine is created and before you press **Enter** to start deleting resources, you could take a few minutes to inspect the resources in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a85a2-187">Next Steps</span><span class="sxs-lookup"><span data-stu-id="a85a2-187">Next Steps</span></span>
* <span data-ttu-id="a85a2-188">Take advantage of using a template to create a virtual machine by using the information in [Deploy an Azure Virtual Machine using C# and a Resource Manager template](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a85a2-188">Take advantage of using a template to create a virtual machine by using the information in [Deploy an Azure Virtual Machine using C# and a Resource Manager template](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="a85a2-189">Learn how to manage the virtual machine that you created by reviewing [Manage Azure Virtual Machines using Azure Resource Manager and C#](csharp-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a85a2-189">Learn how to manage the virtual machine that you created by reviewing [Manage Azure Virtual Machines using Azure Resource Manager and C#](csharp-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

