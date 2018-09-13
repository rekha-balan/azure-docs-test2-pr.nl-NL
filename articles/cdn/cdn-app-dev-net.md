---
title: Get started with the Azure CDN Library for .NET | Microsoft Docs
description: Learn how to write .NET applications to manage Azure CDN using Visual Studio.
services: cdn
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: ''
ms.assetid: 63cf4101-92e7-49dd-a155-a90e54a792ca
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a96ed9941bb21c182125ebc2b6ca33426ae8ba2e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564492"
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="e2a34-103">Get started with Azure CDN development</span><span class="sxs-lookup"><span data-stu-id="e2a34-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [Node.js](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="e2a34-106">You can use the [Azure CDN Library for .NET](https://msdn.microsoft.com/library/mt657769.aspx) to automate creation and management of CDN profiles and endpoints.</span><span class="sxs-lookup"><span data-stu-id="e2a34-106">You can use the [Azure CDN Library for .NET](https://msdn.microsoft.com/library/mt657769.aspx) to automate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="e2a34-107">This tutorial walks through the creation of a simple .NET console application that demonstrates several of the available operations.</span><span class="sxs-lookup"><span data-stu-id="e2a34-107">This tutorial walks through the creation of a simple .NET console application that demonstrates several of the available operations.</span></span>  <span data-ttu-id="e2a34-108">This tutorial is not intended to describe all aspects of the Azure CDN Library for .NET in detail.</span><span class="sxs-lookup"><span data-stu-id="e2a34-108">This tutorial is not intended to describe all aspects of the Azure CDN Library for .NET in detail.</span></span>

<span data-ttu-id="e2a34-109">You need Visual Studio 2015 to complete this tutorial.</span><span class="sxs-lookup"><span data-stu-id="e2a34-109">You need Visual Studio 2015 to complete this tutorial.</span></span>  <span data-ttu-id="e2a34-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is freely available for download.</span><span class="sxs-lookup"><span data-stu-id="e2a34-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is freely available for download.</span></span>

> [!TIP]
> The [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is available for download on MSDN.
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a><span data-ttu-id="e2a34-112">Create your project and add Nuget packages</span><span class="sxs-lookup"><span data-stu-id="e2a34-112">Create your project and add Nuget packages</span></span>
<span data-ttu-id="e2a34-113">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span><span class="sxs-lookup"><span data-stu-id="e2a34-113">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="e2a34-114">From within Visual Studio 2015, click **File**, **New**, **Project...** to open the new project dialog.</span><span class="sxs-lookup"><span data-stu-id="e2a34-114">From within Visual Studio 2015, click **File**, **New**, **Project...** to open the new project dialog.</span></span>  <span data-ttu-id="e2a34-115">Expand **Visual C#**, then select **Windows** in the pane on the left.</span><span class="sxs-lookup"><span data-stu-id="e2a34-115">Expand **Visual C#**, then select **Windows** in the pane on the left.</span></span>  <span data-ttu-id="e2a34-116">Click **Console Application** in the center pane.</span><span class="sxs-lookup"><span data-stu-id="e2a34-116">Click **Console Application** in the center pane.</span></span>  <span data-ttu-id="e2a34-117">Name your project, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="e2a34-117">Name your project, then click **OK**.</span></span>  

![New Project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-app-dev-net/cdn-new-project.png)

<span data-ttu-id="e2a34-119">Our project is going to use some Azure libraries contained in Nuget packages.</span><span class="sxs-lookup"><span data-stu-id="e2a34-119">Our project is going to use some Azure libraries contained in Nuget packages.</span></span>  <span data-ttu-id="e2a34-120">Let's add those to the project.</span><span class="sxs-lookup"><span data-stu-id="e2a34-120">Let's add those to the project.</span></span>

1. <span data-ttu-id="e2a34-121">Click the **Tools** menu, **Nuget Package Manager**, then **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="e2a34-121">Click the **Tools** menu, **Nuget Package Manager**, then **Package Manager Console**.</span></span>
   
    ![Manage Nuget Packages](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-app-dev-net/cdn-manage-nuget.png)
2. <span data-ttu-id="e2a34-123">In the Package Manager Console, execute the following command to install the **Active Directory Authentication Library (ADAL)**:</span><span class="sxs-lookup"><span data-stu-id="e2a34-123">In the Package Manager Console, execute the following command to install the **Active Directory Authentication Library (ADAL)**:</span></span>
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. <span data-ttu-id="e2a34-124">Execute the following to install the **Azure CDN Management Library**:</span><span class="sxs-lookup"><span data-stu-id="e2a34-124">Execute the following to install the **Azure CDN Management Library**:</span></span>
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a><span data-ttu-id="e2a34-125">Directives, constants, main method, and helper methods</span><span class="sxs-lookup"><span data-stu-id="e2a34-125">Directives, constants, main method, and helper methods</span></span>
<span data-ttu-id="e2a34-126">Let's get the basic structure of our program written.</span><span class="sxs-lookup"><span data-stu-id="e2a34-126">Let's get the basic structure of our program written.</span></span>

1. <span data-ttu-id="e2a34-127">Back in the Program.cs tab, replace the `using` directives at the top with the following:</span><span class="sxs-lookup"><span data-stu-id="e2a34-127">Back in the Program.cs tab, replace the `using` directives at the top with the following:</span></span>
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using Microsoft.Azure.Management.Cdn;
    using Microsoft.Azure.Management.Cdn.Models;
    using Microsoft.Azure.Management.Resources;
    using Microsoft.Azure.Management.Resources.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```
2. <span data-ttu-id="e2a34-128">We need to define some constants our methods will use.</span><span class="sxs-lookup"><span data-stu-id="e2a34-128">We need to define some constants our methods will use.</span></span>  <span data-ttu-id="e2a34-129">In the `Program` class, but before the `Main` method, add the following.</span><span class="sxs-lookup"><span data-stu-id="e2a34-129">In the `Program` class, but before the `Main` method, add the following.</span></span>  <span data-ttu-id="e2a34-130">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span><span class="sxs-lookup"><span data-stu-id="e2a34-130">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
    ```csharp
    //Tenant app constants
    private const string clientID = "<YOUR CLIENT ID>";
    private const string clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    private const string authority = "https://login.microsoftonline.com/<YOUR TENANT ID>/<YOUR TENANT DOMAIN NAME>";
   
    //Application constants
    private const string subscriptionId = "<YOUR SUBSCRIPTION ID>";
    private const string profileName = "CdnConsoleApp";
    private const string endpointName = "<A UNIQUE NAME FOR YOUR CDN ENDPOINT>";
    private const string resourceGroupName = "CdnConsoleTutorial";
    private const string resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. <span data-ttu-id="e2a34-131">Also at the class level, define these two variables.</span><span class="sxs-lookup"><span data-stu-id="e2a34-131">Also at the class level, define these two variables.</span></span>  <span data-ttu-id="e2a34-132">We'll use these later to determine if our profile and endpoint already exist.</span><span class="sxs-lookup"><span data-stu-id="e2a34-132">We'll use these later to determine if our profile and endpoint already exist.</span></span>
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. <span data-ttu-id="e2a34-133">Replace the `Main` method as follows:</span><span class="sxs-lookup"><span data-stu-id="e2a34-133">Replace the `Main` method as follows:</span></span>
   
   ```csharp
   static void Main(string[] args)
   {
       //Get a token
       AuthenticationResult authResult = GetAccessToken();
   
       // Create CDN client
       CdnManagementClient cdn = new CdnManagementClient(new TokenCredentials(authResult.AccessToken))
           { SubscriptionId = subscriptionId };
   
       ListProfilesAndEndpoints(cdn);
   
       // Create CDN Profile
       CreateCdnProfile(cdn);
   
       // Create CDN Endpoint
       CreateCdnEndpoint(cdn);
   
       Console.WriteLine();
   
       // Purge CDN Endpoint
       PromptPurgeCdnEndpoint(cdn);
   
       // Delete CDN Endpoint
       PromptDeleteCdnEndpoint(cdn);
   
       // Delete CDN Profile
       PromptDeleteCdnProfile(cdn);
   
       Console.WriteLine("Press Enter to end program.");
       Console.ReadLine();
   }
   ```
5. <span data-ttu-id="e2a34-134">Some of our other methods are going to prompt the user with "Yes/No" questions.</span><span class="sxs-lookup"><span data-stu-id="e2a34-134">Some of our other methods are going to prompt the user with "Yes/No" questions.</span></span>  <span data-ttu-id="e2a34-135">Add the following method to make that a little easier:</span><span class="sxs-lookup"><span data-stu-id="e2a34-135">Add the following method to make that a little easier:</span></span>
   
    ```csharp
    private static bool PromptUser(string Question)
    {
        Console.Write(Question + " (Y/N): ");
        var response = Console.ReadKey();
        Console.WriteLine();
        if (response.Key == ConsoleKey.Y)
        {
            return true;
        }
        else if (response.Key == ConsoleKey.N)
        {
            return false;
        }
        else
        {
            // They pressed something other than Y or N.  Let's ask them again.
            return PromptUser(Question);
        }
    }
    ```

<span data-ttu-id="e2a34-136">Now that the basic structure of our program is written, we should create the methods called by the `Main` method.</span><span class="sxs-lookup"><span data-stu-id="e2a34-136">Now that the basic structure of our program is written, we should create the methods called by the `Main` method.</span></span>

## <a name="authentication"></a><span data-ttu-id="e2a34-137">Authentication</span><span class="sxs-lookup"><span data-stu-id="e2a34-137">Authentication</span></span>
<span data-ttu-id="e2a34-138">Before we can use the Azure CDN Management Library, we need to authenticate our service principal and obtain an authentication token.</span><span class="sxs-lookup"><span data-stu-id="e2a34-138">Before we can use the Azure CDN Management Library, we need to authenticate our service principal and obtain an authentication token.</span></span>  <span data-ttu-id="e2a34-139">This method uses ADAL to retrieve the token.</span><span class="sxs-lookup"><span data-stu-id="e2a34-139">This method uses ADAL to retrieve the token.</span></span>

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority); 
    ClientCredential credential = new ClientCredential(clientID, clientSecret);
    AuthenticationResult authResult = 
        authContext.AcquireTokenAsync("https://management.core.windows.net/", credential).Result;

    return authResult;
}
```

<span data-ttu-id="e2a34-140">If you are using individual user authentication, the `GetAccessToken` method will look slightly different.</span><span class="sxs-lookup"><span data-stu-id="e2a34-140">If you are using individual user authentication, the `GetAccessToken` method will look slightly different.</span></span>

> [!IMPORTANT]
> Only use this code sample if you are choosing to have individual user authentication instead of a service principal.
> 
> 

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority);
    AuthenticationResult authResult = authContext.AcquireTokenAsync("https://management.core.windows.net/",
        clientID, new Uri("http://<redirect URI>"), new PlatformParameters(PromptBehavior.RefreshSession)).Result;

    return authResult;
}
```

<span data-ttu-id="e2a34-142">Be sure to replace `<redirect URI>` with the redirect URI you entered when you registered the application in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2a34-142">Be sure to replace `<redirect URI>` with the redirect URI you entered when you registered the application in Azure AD.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="e2a34-143">List CDN profiles and endpoints</span><span class="sxs-lookup"><span data-stu-id="e2a34-143">List CDN profiles and endpoints</span></span>
<span data-ttu-id="e2a34-144">Now we're ready to perform CDN operations.</span><span class="sxs-lookup"><span data-stu-id="e2a34-144">Now we're ready to perform CDN operations.</span></span>  <span data-ttu-id="e2a34-145">The first thing our method does is list all the profiles and endpoints in our resource group, and if it finds a match for the profile and endpoint names specified in our constants, makes a note of that for later so we don't try to create duplicates.</span><span class="sxs-lookup"><span data-stu-id="e2a34-145">The first thing our method does is list all the profiles and endpoints in our resource group, and if it finds a match for the profile and endpoint names specified in our constants, makes a note of that for later so we don't try to create duplicates.</span></span>

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all the CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's the name of the CDN profile we want to create!
            profileAlreadyExists = true;
        }

        //List all the CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // The unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="e2a34-146">Create CDN profiles and endpoints</span><span class="sxs-lookup"><span data-stu-id="e2a34-146">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="e2a34-147">Next, we'll create a profile.</span><span class="sxs-lookup"><span data-stu-id="e2a34-147">Next, we'll create a profile.</span></span>

```csharp
private static void CreateCdnProfile(CdnManagementClient cdn)
{
    if (profileAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating profile {0}.", profileName);
        ProfileCreateParameters profileParms =
            new ProfileCreateParameters() { Location = resourceLocation, Sku = new Sku(SkuName.StandardVerizon) };
        cdn.Profiles.Create(profileName, profileParms, resourceGroupName);
    }
}
```

<span data-ttu-id="e2a34-148">Once the profile is created, we'll create an endpoint.</span><span class="sxs-lookup"><span data-stu-id="e2a34-148">Once the profile is created, we'll create an endpoint.</span></span>

```csharp
private static void CreateCdnEndpoint(CdnManagementClient cdn)
{
    if (endpointAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating endpoint {0} on profile {1}.", endpointName, profileName);
        EndpointCreateParameters endpointParms =
            new EndpointCreateParameters()
            {
                Origins = new List<DeepCreatedOrigin>() { new DeepCreatedOrigin("Contoso", "www.contoso.com") },
                IsHttpAllowed = true,
                IsHttpsAllowed = true,
                Location = resourceLocation
            };
        cdn.Endpoints.Create(endpointName, endpointParms, profileName, resourceGroupName);
    }
}
```

> [!NOTE]
> The example above assigns the endpoint an origin named *Contoso* with a hostname `www.contoso.com`.  You should change this to point to your own origin's hostname.
> 
> 

## <a name="purge-an-endpoint"></a><span data-ttu-id="e2a34-151">Purge an endpoint</span><span class="sxs-lookup"><span data-stu-id="e2a34-151">Purge an endpoint</span></span>
<span data-ttu-id="e2a34-152">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging the content in our endpoint.</span><span class="sxs-lookup"><span data-stu-id="e2a34-152">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging the content in our endpoint.</span></span>

```csharp
private static void PromptPurgeCdnEndpoint(CdnManagementClient cdn)
{
    if (PromptUser(String.Format("Purge CDN endpoint {0}?", endpointName)))
    {
        Console.WriteLine("Purging endpoint. Please wait...");
        cdn.Endpoints.PurgeContent(endpointName, profileName, resourceGroupName, new List<string>() { "/*" });
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

> [!NOTE]
> In the example above, the string `/*` denotes that I want to purge everything in the root of the endpoint path.  This is equivalent to checking **Purge All** in the Azure portal's "purge" dialog. In the `CreateCdnProfile` method, I created our profile as an **Azure CDN from Verizon** profile using the code `Sku = new Sku(SkuName.StandardVerizon)`, so this will be successful.  However, **Azure CDN from Akamai** profiles do not support **Purge All**, so if I was using an Akamai profile for this tutorial, I would need to include specific paths to purge.
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="e2a34-157">Delete CDN profiles and endpoints</span><span class="sxs-lookup"><span data-stu-id="e2a34-157">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="e2a34-158">The last methods will delete our endpoint and profile.</span><span class="sxs-lookup"><span data-stu-id="e2a34-158">The last methods will delete our endpoint and profile.</span></span>

```csharp
private static void PromptDeleteCdnEndpoint(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN endpoint {0} on profile {1}?", endpointName, profileName)))
    {
        Console.WriteLine("Deleting endpoint. Please wait...");
        cdn.Endpoints.DeleteIfExists(endpointName, profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}

private static void PromptDeleteCdnProfile(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN profile {0}?", profileName)))
    {
        Console.WriteLine("Deleting profile. Please wait...");
        cdn.Profiles.DeleteIfExists(profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

## <a name="running-the-program"></a><span data-ttu-id="e2a34-159">Running the program</span><span class="sxs-lookup"><span data-stu-id="e2a34-159">Running the program</span></span>
<span data-ttu-id="e2a34-160">We can now compile and run the program by clicking the **Start** button in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e2a34-160">We can now compile and run the program by clicking the **Start** button in Visual Studio.</span></span>

![Program running](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-app-dev-net/cdn-program-running-1.png)

<span data-ttu-id="e2a34-162">When the program reaches the above prompt, you should be able to return to your resource group in the Azure portal and see that the profile has been created.</span><span class="sxs-lookup"><span data-stu-id="e2a34-162">When the program reaches the above prompt, you should be able to return to your resource group in the Azure portal and see that the profile has been created.</span></span>

![Success!](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-app-dev-net/cdn-success.png)

<span data-ttu-id="e2a34-164">We can then confirm the prompts to run the rest of the program.</span><span class="sxs-lookup"><span data-stu-id="e2a34-164">We can then confirm the prompts to run the rest of the program.</span></span>

![Program completing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a><span data-ttu-id="e2a34-166">Next Steps</span><span class="sxs-lookup"><span data-stu-id="e2a34-166">Next Steps</span></span>
<span data-ttu-id="e2a34-167">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span><span class="sxs-lookup"><span data-stu-id="e2a34-167">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span></span>

<span data-ttu-id="e2a34-168">To find additional documentation on the Azure CDN Management Library for .NET, view the [reference on MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2a34-168">To find additional documentation on the Azure CDN Management Library for .NET, view the [reference on MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span></span>

<span data-ttu-id="e2a34-169">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e2a34-169">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>






