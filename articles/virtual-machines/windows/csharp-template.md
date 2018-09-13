---
title: Deploy a VM using C# and a Resource Manager template | Microsoft Docs
description: Learn to how to use C# and a Resource Manager template to deploy an Azure VM.
services: virtual-machines-windows
documentationcenter: ''
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: bfba66e8-c923-4df2-900a-0c2643b81240
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: davidmu
ms.openlocfilehash: ea3c95c9a7cdf488f3f444069de3902b6f31604c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549679"
---
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a><span data-ttu-id="1e681-103">Deploy an Azure Virtual Machine using C# and a Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="1e681-103">Deploy an Azure Virtual Machine using C# and a Resource Manager template</span></span>
<span data-ttu-id="1e681-104">This article shows you how to deploy an Azure Resource Manager template using C#.</span><span class="sxs-lookup"><span data-stu-id="1e681-104">This article shows you how to deploy an Azure Resource Manager template using C#.</span></span> <span data-ttu-id="1e681-105">The [template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-windows/azuredeploy.json) deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span><span class="sxs-lookup"><span data-stu-id="1e681-105">The [template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-windows/azuredeploy.json) deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="1e681-106">For a detailed description of the virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="1e681-106">For a detailed description of the virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="1e681-107">For more information about all the resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="1e681-107">For more information about all the resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="1e681-108">It takes about 10 minutes to do these steps.</span><span class="sxs-lookup"><span data-stu-id="1e681-108">It takes about 10 minutes to do these steps.</span></span>

## <a name="step-1-create-a-visual-studio-project"></a><span data-ttu-id="1e681-109">Step 1: Create a Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="1e681-109">Step 1: Create a Visual Studio project</span></span>

<span data-ttu-id="1e681-110">In this step, you make sure that Visual Studio is installed and you create a console application used to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="1e681-110">In this step, you make sure that Visual Studio is installed and you create a console application used to deploy the template.</span></span>

1. <span data-ttu-id="1e681-111">If you haven't already, install [Visual Studio](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="1e681-111">If you haven't already, install [Visual Studio](https://www.visualstudio.com/).</span></span>
2. <span data-ttu-id="1e681-112">In Visual Studio, click **File** > **New** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="1e681-112">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="1e681-113">In **Templates** > **Visual C#**, select **Console Application**, enter the name and location of the project, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1e681-113">In **Templates** > **Visual C#**, select **Console Application**, enter the name and location of the project, and then click **OK**.</span></span>

## <a name="step-2-install-libraries"></a><span data-ttu-id="1e681-114">Step 2: Install libraries</span><span class="sxs-lookup"><span data-stu-id="1e681-114">Step 2: Install libraries</span></span>

<span data-ttu-id="1e681-115">NuGet packages are the easiest way to install the libraries that you need to finish these steps.</span><span class="sxs-lookup"><span data-stu-id="1e681-115">NuGet packages are the easiest way to install the libraries that you need to finish these steps.</span></span> <span data-ttu-id="1e681-116">You need the Azure Resource Manager Library and the Active Directory Authentication Library to create the resources.</span><span class="sxs-lookup"><span data-stu-id="1e681-116">You need the Azure Resource Manager Library and the Active Directory Authentication Library to create the resources.</span></span> <span data-ttu-id="1e681-117">To get these libraries in Visual Studio, do these steps:</span><span class="sxs-lookup"><span data-stu-id="1e681-117">To get these libraries in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="1e681-118">Right-click the project name in the Solution Explorer, click **Manage NuGet Packages**, and then click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="1e681-118">Right-click the project name in the Solution Explorer, click **Manage NuGet Packages**, and then click **Browse**.</span></span>
2. <span data-ttu-id="1e681-119">Type *Microsoft.IdentityModel.Clients.ActiveDirectory* in the search box, click **Install**, and then follow the instructions to install the package.</span><span class="sxs-lookup"><span data-stu-id="1e681-119">Type *Microsoft.IdentityModel.Clients.ActiveDirectory* in the search box, click **Install**, and then follow the instructions to install the package.</span></span>
3. <span data-ttu-id="1e681-120">At the top of the page, select **Include Prerelease**.</span><span class="sxs-lookup"><span data-stu-id="1e681-120">At the top of the page, select **Include Prerelease**.</span></span> <span data-ttu-id="1e681-121">Type *Microsoft.Azure.Management.ResourceManager* in the search box, click **Install**, and then follow the instructions to install the package.</span><span class="sxs-lookup"><span data-stu-id="1e681-121">Type *Microsoft.Azure.Management.ResourceManager* in the search box, click **Install**, and then follow the instructions to install the package.</span></span>

<span data-ttu-id="1e681-122">Now you're ready to start using the libraries to create your application.</span><span class="sxs-lookup"><span data-stu-id="1e681-122">Now you're ready to start using the libraries to create your application.</span></span>

## <a name="step-3-create-credentials-used-to-authenticate-requests"></a><span data-ttu-id="1e681-123">Step 3: Create credentials used to authenticate requests</span><span class="sxs-lookup"><span data-stu-id="1e681-123">Step 3: Create credentials used to authenticate requests</span></span>

<span data-ttu-id="1e681-124">Before you start this step, make sure that you have access to an [Active Directory service principal](../../resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="1e681-124">Before you start this step, make sure that you have access to an [Active Directory service principal](../../resource-group-authenticate-service-principal.md).</span></span> <span data-ttu-id="1e681-125">From the service principal, you acquire a token for authenticating requests to Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1e681-125">From the service principal, you acquire a token for authenticating requests to Azure Resource Manager.</span></span>

1. <span data-ttu-id="1e681-126">Open the Program.cs file for the project that you created, and then add these using statements to the top of the file:</span><span class="sxs-lookup"><span data-stu-id="1e681-126">Open the Program.cs file for the project that you created, and then add these using statements to the top of the file:</span></span>

    ```
    using Microsoft.Azure;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.Rest;
    using System.IO;
    ```

2. <span data-ttu-id="1e681-127">Add this method to the Program class to get the token that's needed to create the credentials:</span><span class="sxs-lookup"><span data-stu-id="1e681-127">Add this method to the Program class to get the token that's needed to create the credentials:</span></span>

    ```
    private static async Task<AuthenticationResult> GetAccessTokenAsync()
    {
      var cc = new ClientCredential("{client-id}", "{client-secret}");
      var context = new AuthenticationContext("https://login.windows.net/{tenant-id}");
      var token = await context.AcquireTokenAsync("https://management.azure.com/", cc);
      if (token == null)
      {
        throw new InvalidOperationException("Could not get the token.");
      } 
      return token;
    }
    ```

    <span data-ttu-id="1e681-128">Replace these values:</span><span class="sxs-lookup"><span data-stu-id="1e681-128">Replace these values:</span></span>
    
    - <span data-ttu-id="1e681-129">*{client-id}* with the identifier of the Azure Active Directory application.</span><span class="sxs-lookup"><span data-stu-id="1e681-129">*{client-id}* with the identifier of the Azure Active Directory application.</span></span> <span data-ttu-id="1e681-130">You can find this identifier on the Properties blade of your AD application.</span><span class="sxs-lookup"><span data-stu-id="1e681-130">You can find this identifier on the Properties blade of your AD application.</span></span> <span data-ttu-id="1e681-131">To find your AD application in the Azure portal, click **Azure Active Directory** in the resource menu, and then click **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="1e681-131">To find your AD application in the Azure portal, click **Azure Active Directory** in the resource menu, and then click **App registrations**.</span></span>
    - <span data-ttu-id="1e681-132">*{client-secret}* with the access key of the AD application.</span><span class="sxs-lookup"><span data-stu-id="1e681-132">*{client-secret}* with the access key of the AD application.</span></span> <span data-ttu-id="1e681-133">You can find this identifier on the Properties blade of your AD application.</span><span class="sxs-lookup"><span data-stu-id="1e681-133">You can find this identifier on the Properties blade of your AD application.</span></span>
    - <span data-ttu-id="1e681-134">*{tenant-id}* with the tenant identifier of your subscription.</span><span class="sxs-lookup"><span data-stu-id="1e681-134">*{tenant-id}* with the tenant identifier of your subscription.</span></span> <span data-ttu-id="1e681-135">You can find the tenant identifier on the Properties blade for Azure Active Directory in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1e681-135">You can find the tenant identifier on the Properties blade for Azure Active Directory in the Azure portal.</span></span> <span data-ttu-id="1e681-136">It is labeled *Directory ID*.</span><span class="sxs-lookup"><span data-stu-id="1e681-136">It is labeled *Directory ID*.</span></span>

3. <span data-ttu-id="1e681-137">To call the method that you just added, add this code to the Main method:</span><span class="sxs-lookup"><span data-stu-id="1e681-137">To call the method that you just added, add this code to the Main method:</span></span>

    ```
    var token = GetAccessTokenAsync();
    var credential = new TokenCredentials(token.Result.AccessToken);
    ```

4. <span data-ttu-id="1e681-138">Save the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="1e681-138">Save the Program.cs file.</span></span>

## <a name="step-4-create-a-resource-group"></a><span data-ttu-id="1e681-139">Step 4: Create a resource group</span><span class="sxs-lookup"><span data-stu-id="1e681-139">Step 4: Create a resource group</span></span>

<span data-ttu-id="1e681-140">Although you can create a resource group from a template, the template that you use from the gallery doesn't create one.</span><span class="sxs-lookup"><span data-stu-id="1e681-140">Although you can create a resource group from a template, the template that you use from the gallery doesn't create one.</span></span> <span data-ttu-id="1e681-141">In this step, you add the code to create a resource group.</span><span class="sxs-lookup"><span data-stu-id="1e681-141">In this step, you add the code to create a resource group.</span></span>

1. <span data-ttu-id="1e681-142">To specify values for the application, add variables to the Main method of the Program class:</span><span class="sxs-lookup"><span data-stu-id="1e681-142">To specify values for the application, add variables to the Main method of the Program class:</span></span>

    ```
    var groupName = "myResourceGroup";
    var subscriptionId = "subsciptionId";
    var deploymentName = "deploymentName;
    var location = "location";
    ```

    <span data-ttu-id="1e681-143">Replace these values:</span><span class="sxs-lookup"><span data-stu-id="1e681-143">Replace these values:</span></span>
    
    - <span data-ttu-id="1e681-144">*myResourceGroup* with the name of the resource group being created.</span><span class="sxs-lookup"><span data-stu-id="1e681-144">*myResourceGroup* with the name of the resource group being created.</span></span>
    - <span data-ttu-id="1e681-145">*subscriptionId* with your subscription identifier.</span><span class="sxs-lookup"><span data-stu-id="1e681-145">*subscriptionId* with your subscription identifier.</span></span> <span data-ttu-id="1e681-146">You can find the subscription identifier on the Subscriptions blade of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1e681-146">You can find the subscription identifier on the Subscriptions blade of the Azure portal.</span></span>
    - <span data-ttu-id="1e681-147">*deploymentName* with the name of the deployment.</span><span class="sxs-lookup"><span data-stu-id="1e681-147">*deploymentName* with the name of the deployment.</span></span>
    - <span data-ttu-id="1e681-148">*location* with the [Azure region](https://azure.microsoft.com/regions/) where you want to create the resources.</span><span class="sxs-lookup"><span data-stu-id="1e681-148">*location* with the [Azure region](https://azure.microsoft.com/regions/) where you want to create the resources.</span></span>

2. <span data-ttu-id="1e681-149">To create the resource group, add this method to the Program class:</span><span class="sxs-lookup"><span data-stu-id="1e681-149">To create the resource group, add this method to the Program class:</span></span>

    ```
    public static async Task<ResourceGroup> CreateResourceGroupAsync(
      TokenCredentials credential,
      string groupName,
      string subscriptionId,
      string location)
    {
      var resourceManagementClient = new ResourceManagementClient(credential)
        { SubscriptionId = subscriptionId };

      Console.WriteLine("Creating the resource group...");
      var resourceGroup = new ResourceGroup { Location = location };
      return await resourceManagementClient.ResourceGroups.CreateOrUpdateAsync(
        groupName, 
        resourceGroup);
    }
    ```

3. <span data-ttu-id="1e681-150">To call the method that you just added, add this code to the Main method:</span><span class="sxs-lookup"><span data-stu-id="1e681-150">To call the method that you just added, add this code to the Main method:</span></span>

    ```
    var rgResult = CreateResourceGroupAsync(
      credential,
      groupName,
      subscriptionId,
      location);
    Console.WriteLine(rgResult.Result.Properties.ProvisioningState);
    Console.ReadLine();
    ```

## <a name="step-5-create-a-parameters-file"></a><span data-ttu-id="1e681-151">Step 5: Create a parameters file</span><span class="sxs-lookup"><span data-stu-id="1e681-151">Step 5: Create a parameters file</span></span>

<span data-ttu-id="1e681-152">To specify values for the resource parameters that are defined in the template, you create a parameters file that contains the values.</span><span class="sxs-lookup"><span data-stu-id="1e681-152">To specify values for the resource parameters that are defined in the template, you create a parameters file that contains the values.</span></span> <span data-ttu-id="1e681-153">The parameters file is used when you deploy the template.</span><span class="sxs-lookup"><span data-stu-id="1e681-153">The parameters file is used when you deploy the template.</span></span> <span data-ttu-id="1e681-154">The template that you are using from the gallery expects values for *adminUserName*, *adminPassword*, and *dnsLabelPrefix* parameters.</span><span class="sxs-lookup"><span data-stu-id="1e681-154">The template that you are using from the gallery expects values for *adminUserName*, *adminPassword*, and *dnsLabelPrefix* parameters.</span></span>

<span data-ttu-id="1e681-155">In Visual Studio, do these steps:</span><span class="sxs-lookup"><span data-stu-id="1e681-155">In Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="1e681-156">Right-click the project name in Solution Explorer, click **Add** > **New Item**.</span><span class="sxs-lookup"><span data-stu-id="1e681-156">Right-click the project name in Solution Explorer, click **Add** > **New Item**.</span></span>
2. <span data-ttu-id="1e681-157">Click **Web**, select **JSON File**, enter *Parameters.json* for the name, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="1e681-157">Click **Web**, select **JSON File**, enter *Parameters.json* for the name, and then click **Add**.</span></span>
3. <span data-ttu-id="1e681-158">Open the Parameters.json file and then add this JSON content:</span><span class="sxs-lookup"><span data-stu-id="1e681-158">Open the Parameters.json file and then add this JSON content:</span></span>

    ```
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUserName": { "value": "mytestacct1" },
        "adminPassword": { "value": "mytestpass1" },
        "dnsLabelPrefix": { "value": "mydns1" }
      }
    }
    ```

    <span data-ttu-id="1e681-159">Replace the parameter values with values that work in your environment.</span><span class="sxs-lookup"><span data-stu-id="1e681-159">Replace the parameter values with values that work in your environment.</span></span>

4. <span data-ttu-id="1e681-160">Save the Parameters.json file.</span><span class="sxs-lookup"><span data-stu-id="1e681-160">Save the Parameters.json file.</span></span>

## <a name="step-6-deploy-a-template"></a><span data-ttu-id="1e681-161">Step 6: Deploy a template</span><span class="sxs-lookup"><span data-stu-id="1e681-161">Step 6: Deploy a template</span></span>

<span data-ttu-id="1e681-162">In this example, you deploy a template from the Azure template gallery and supply parameter values to it from the local file that you created.</span><span class="sxs-lookup"><span data-stu-id="1e681-162">In this example, you deploy a template from the Azure template gallery and supply parameter values to it from the local file that you created.</span></span> 

1. <span data-ttu-id="1e681-163">To deploy the template, add this method to the Program class:</span><span class="sxs-lookup"><span data-stu-id="1e681-163">To deploy the template, add this method to the Program class:</span></span>

    ```
    public static async Task<DeploymentExtended> CreateTemplateDeploymentAsync(
      TokenCredentials credential,
      string groupName,
      string deploymentName,
      string subscriptionId)
    {
    
      var resourceManagementClient = new ResourceManagementClient(credential)
        { SubscriptionId = subscriptionId };

      Console.WriteLine("Creating the template deployment...");
      var deployment = new Deployment();
      deployment.Properties = new DeploymentProperties
        {
          Mode = DeploymentMode.Incremental,
          TemplateLink = new TemplateLink("https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-windows/azuredeploy.json"),
          Parameters = File.ReadAllText("..\\..\\Parameters.json")
        };
      
      return await resourceManagementClient.Deployments.CreateOrUpdateAsync(
        groupName,
        deploymentName,
        deployment
      );
    }
    ```

    <span data-ttu-id="1e681-164">You could also deploy a template from a local folder by using the Template property instead of the TemplateLink property.</span><span class="sxs-lookup"><span data-stu-id="1e681-164">You could also deploy a template from a local folder by using the Template property instead of the TemplateLink property.</span></span>

2. <span data-ttu-id="1e681-165">To call the method that you just added, add this code to the Main method:</span><span class="sxs-lookup"><span data-stu-id="1e681-165">To call the method that you just added, add this code to the Main method:</span></span>

    ```
    var dpResult = CreateTemplateDeploymentAsync(
      credential,
      groupName,
      deploymentName,
      subscriptionId);
    Console.WriteLine(dpResult.Result.Properties.ProvisioningState);
    Console.ReadLine();
    ```

## <a name="step-7-delete-the-resources"></a><span data-ttu-id="1e681-166">Step 7: Delete the resources</span><span class="sxs-lookup"><span data-stu-id="1e681-166">Step 7: Delete the resources</span></span>

<span data-ttu-id="1e681-167">Because you are charged for resources used in Azure, it is always good practice to delete resources that are no longer needed.</span><span class="sxs-lookup"><span data-stu-id="1e681-167">Because you are charged for resources used in Azure, it is always good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="1e681-168">You don’t need to delete each resource separately from a resource group.</span><span class="sxs-lookup"><span data-stu-id="1e681-168">You don’t need to delete each resource separately from a resource group.</span></span> <span data-ttu-id="1e681-169">Delete the resource group and all its resources are automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="1e681-169">Delete the resource group and all its resources are automatically deleted.</span></span>

1. <span data-ttu-id="1e681-170">To delete the resource group, add this method to the Program class:</span><span class="sxs-lookup"><span data-stu-id="1e681-170">To delete the resource group, add this method to the Program class:</span></span>

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

2. <span data-ttu-id="1e681-171">To call the method that you just added, add this code to the Main method:</span><span class="sxs-lookup"><span data-stu-id="1e681-171">To call the method that you just added, add this code to the Main method:</span></span>

   ```
   DeleteResourceGroupAsync(
     credential,
     groupName,
     subscriptionId);
   Console.ReadLine();
   ```

## <a name="step-8-run-the-console-application"></a><span data-ttu-id="1e681-172">Step 8: Run the console application</span><span class="sxs-lookup"><span data-stu-id="1e681-172">Step 8: Run the console application</span></span>

<span data-ttu-id="1e681-173">It should take about five minutes for this console application to run completely from start to finish.</span><span class="sxs-lookup"><span data-stu-id="1e681-173">It should take about five minutes for this console application to run completely from start to finish.</span></span> 

1. <span data-ttu-id="1e681-174">To run the console application, click **Start** in Visual Studio, and then sign in to Azure AD using the same credentials that you use with your subscription.</span><span class="sxs-lookup"><span data-stu-id="1e681-174">To run the console application, click **Start** in Visual Studio, and then sign in to Azure AD using the same credentials that you use with your subscription.</span></span>

2. <span data-ttu-id="1e681-175">Press **Enter** after the *Succeeded* status appears.</span><span class="sxs-lookup"><span data-stu-id="1e681-175">Press **Enter** after the *Succeeded* status appears.</span></span> 

    <span data-ttu-id="1e681-176">You should also see **1 Succeeded** under Deployments on the Overview blade for your resource group in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1e681-176">You should also see **1 Succeeded** under Deployments on the Overview blade for your resource group in the Azure portal.</span></span>

3. <span data-ttu-id="1e681-177">Before you press **Enter** to start deleting resources, you could take a few minutes to verify the creation of the resources in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1e681-177">Before you press **Enter** to start deleting resources, you could take a few minutes to verify the creation of the resources in the Azure portal.</span></span> <span data-ttu-id="1e681-178">Click the deployment status to see information about the deployment.</span><span class="sxs-lookup"><span data-stu-id="1e681-178">Click the deployment status to see information about the deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e681-179">Next Steps</span><span class="sxs-lookup"><span data-stu-id="1e681-179">Next Steps</span></span>
* <span data-ttu-id="1e681-180">If there were issues with the deployment, a next step would be to look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="1e681-180">If there were issues with the deployment, a next step would be to look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="1e681-181">Learn how to deploy a virtual machine and its supporting resources by reviewing [Deploy an Azure Virtual Machine Using C#](csharp.md).</span><span class="sxs-lookup"><span data-stu-id="1e681-181">Learn how to deploy a virtual machine and its supporting resources by reviewing [Deploy an Azure Virtual Machine Using C#](csharp.md).</span></span>
* <span data-ttu-id="1e681-182">Learn how to manage the virtual machine that you created by reviewing [Manage Azure Virtual Machines using Azure Resource Manager and C#](csharp-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1e681-182">Learn how to manage the virtual machine that you created by reviewing [Manage Azure Virtual Machines using Azure Resource Manager and C#](csharp-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
