---
title: Create data pipelines by using Azure .NET SDK | Microsoft Docs
description: Learn how to programmatically create, monitor, and manage Azure data factories by using Data Factory SDK.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/22/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: de892afee57b9a39b841f6cfc93f8470d831c2a6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870815"
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="2d9d7-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2d9d7-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
> [!NOTE]
> <span data-ttu-id="2d9d7-104">This article applies to version 1 of Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-104">This article applies to version 1 of Data Factory.</span></span> <span data-ttu-id="2d9d7-105">If you are using the current version of the Data Factory service, see [copy activity tutorial](../quickstart-create-data-factory-dot-net.md).</span><span class="sxs-lookup"><span data-stu-id="2d9d7-105">If you are using the current version of the Data Factory service, see [copy activity tutorial](../quickstart-create-data-factory-dot-net.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="2d9d7-106">Overview</span><span class="sxs-lookup"><span data-stu-id="2d9d7-106">Overview</span></span>
<span data-ttu-id="2d9d7-107">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-107">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="2d9d7-108">This article contains a walkthrough that you can follow to create a sample .NET console application that creates and monitors a data factory.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-108">This article contains a walkthrough that you can follow to create a sample .NET console application that creates and monitors a data factory.</span></span> 

> [!NOTE]
> <span data-ttu-id="2d9d7-109">This article does not cover all the Data Factory .NET API.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-109">This article does not cover all the Data Factory .NET API.</span></span> <span data-ttu-id="2d9d7-110">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-110">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2d9d7-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2d9d7-111">Prerequisites</span></span>
* <span data-ttu-id="2d9d7-112">Visual Studio 2012 or 2013 or 2015</span><span class="sxs-lookup"><span data-stu-id="2d9d7-112">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="2d9d7-113">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2d9d7-113">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="2d9d7-114">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-114">Azure PowerShell.</span></span> <span data-ttu-id="2d9d7-115">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install Azure PowerShell on your computer.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-115">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install Azure PowerShell on your computer.</span></span> <span data-ttu-id="2d9d7-116">You use Azure PowerShell to create an Azure Active Directory application.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-116">You use Azure PowerShell to create an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="2d9d7-117">Create an application in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d9d7-117">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="2d9d7-118">Create an Azure Active Directory application, create a service principal for the application, and assign it to the **Data Factory Contributor** role.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-118">Create an Azure Active Directory application, create a service principal for the application, and assign it to the **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="2d9d7-119">Launch **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-119">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="2d9d7-120">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-120">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>

    ```PowerShell
    Connect-AzureRmAccount
    ```
3. <span data-ttu-id="2d9d7-121">Run the following command to view all the subscriptions for this account.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-121">Run the following command to view all the subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="2d9d7-122">Run the following command to select the subscription that you want to work with.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-122">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="2d9d7-123">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-123">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="2d9d7-124">Note down **SubscriptionId** and **TenantId** from the output of this command.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-124">Note down **SubscriptionId** and **TenantId** from the output of this command.</span></span>

5. <span data-ttu-id="2d9d7-125">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-125">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="2d9d7-126">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span><span class="sxs-lookup"><span data-stu-id="2d9d7-126">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="2d9d7-127">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-127">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="2d9d7-128">Create an Azure Active Directory application.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-128">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="2d9d7-129">If you get the following error, specify a different URL and run the command again.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-129">If you get the following error, specify a different URL and run the command again.</span></span>
    
    ```PowerShell
    Another object with the same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="2d9d7-130">Create the AD service principal.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-130">Create the AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="2d9d7-131">Add service principal to the **Data Factory Contributor** role.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-131">Add service principal to the **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="2d9d7-132">Get the application ID.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-132">Get the application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="2d9d7-133">Note down the application ID (applicationID) from the output.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-133">Note down the application ID (applicationID) from the output.</span></span>

<span data-ttu-id="2d9d7-134">You should have following four values from these steps:</span><span class="sxs-lookup"><span data-stu-id="2d9d7-134">You should have following four values from these steps:</span></span>

* <span data-ttu-id="2d9d7-135">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="2d9d7-135">Tenant ID</span></span>
* <span data-ttu-id="2d9d7-136">Subscription ID</span><span class="sxs-lookup"><span data-stu-id="2d9d7-136">Subscription ID</span></span>
* <span data-ttu-id="2d9d7-137">Application ID</span><span class="sxs-lookup"><span data-stu-id="2d9d7-137">Application ID</span></span>
* <span data-ttu-id="2d9d7-138">Password (specified in the first command)</span><span class="sxs-lookup"><span data-stu-id="2d9d7-138">Password (specified in the first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="2d9d7-139">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="2d9d7-139">Walkthrough</span></span>
<span data-ttu-id="2d9d7-140">In the walkthrough, you create a data factory with a pipeline that contains a copy activity.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-140">In the walkthrough, you create a data factory with a pipeline that contains a copy activity.</span></span> <span data-ttu-id="2d9d7-141">The copy activity copies data from a folder in your Azure blob storage to another folder in the same blob storage.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-141">The copy activity copies data from a folder in your Azure blob storage to another folder in the same blob storage.</span></span> 

<span data-ttu-id="2d9d7-142">The Copy Activity performs the data movement in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-142">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="2d9d7-143">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-143">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="2d9d7-144">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-144">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>

1. <span data-ttu-id="2d9d7-145">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-145">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="2d9d7-146">Launch **Visual Studio** 2012/2013/2015.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-146">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="2d9d7-147">Click **File**, point to **New**, and click **Project**.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-147">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="2d9d7-148">Expand **Templates**, and select **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-148">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="2d9d7-149">In this walkthrough, you use C#, but you can use any .NET language.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-149">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="2d9d7-150">Select **Console Application** from the list of project types on the right.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-150">Select **Console Application** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="2d9d7-151">Enter **DataFactoryAPITestApp** for the Name.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-151">Enter **DataFactoryAPITestApp** for the Name.</span></span>
   6. <span data-ttu-id="2d9d7-152">Select **C:\ADFGetStarted** for the Location.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-152">Select **C:\ADFGetStarted** for the Location.</span></span>
   7. <span data-ttu-id="2d9d7-153">Click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-153">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="2d9d7-154">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-154">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="2d9d7-155">In the **Package Manager Console**, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="2d9d7-155">In the **Package Manager Console**, do the following steps:</span></span>
   1. <span data-ttu-id="2d9d7-156">Run the following command to install Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="2d9d7-156">Run the following command to install Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="2d9d7-157">Run the following command to install Azure Active Directory package (you use Active Directory API in the code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="2d9d7-157">Run the following command to install Azure Active Directory package (you use Active Directory API in the code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="2d9d7-158">Replace the contents of **App.config** file in the project with the following content:</span><span class="sxs-lookup"><span data-stu-id="2d9d7-158">Replace the contents of **App.config** file in the project with the following content:</span></span> 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating the AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. <span data-ttu-id="2d9d7-159">In the App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-159">In the App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>
6. <span data-ttu-id="2d9d7-160">Add the following **using** statements to the **Program.cs** file in the project.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-160">Add the following **using** statements to the **Program.cs** file in the project.</span></span>

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```
6. <span data-ttu-id="2d9d7-161">Add the following code that creates an instance of **DataPipelineManagementClient** class to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-161">Add the following code that creates an instance of **DataPipelineManagementClient** class to the **Main** method.</span></span> <span data-ttu-id="2d9d7-162">You use this object to create a data factory, a linked service, input and output datasets, and a pipeline.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-162">You use this object to create a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="2d9d7-163">You also use this object to monitor slices of a dataset at runtime.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-163">You also use this object to monitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client

    //IMPORTANT: specify the name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: the name of the data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="2d9d7-164">Replace the value of **resourceGroupName** with the name of your Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-164">Replace the value of **resourceGroupName** with the name of your Azure resource group.</span></span> <span data-ttu-id="2d9d7-165">You can create a resource group using the [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-165">You can create a resource group using the [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span>
   >
   > <span data-ttu-id="2d9d7-166">Update name of the data factory (dataFactoryName) to be unique.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-166">Update name of the data factory (dataFactoryName) to be unique.</span></span> <span data-ttu-id="2d9d7-167">Name of the data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-167">Name of the data factory must be globally unique.</span></span> <span data-ttu-id="2d9d7-168">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-168">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
7. <span data-ttu-id="2d9d7-169">Add the following code that creates a **data factory** to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-169">Add the following code that creates a **data factory** to the **Main** method.</span></span>

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```
8. <span data-ttu-id="2d9d7-170">Add the following code that creates an **Azure Storage linked service** to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-170">Add the following code that creates an **Azure Storage linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="2d9d7-171">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-171">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

    ```csharp
    // create a linked service for input data store: Azure Storage
    Console.WriteLine("Creating Azure Storage linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureStorageLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```
9. <span data-ttu-id="2d9d7-172">Add the following code that creates **input and output datasets** to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-172">Add the following code that creates **input and output datasets** to the **Main** method.</span></span>

    <span data-ttu-id="2d9d7-173">The **FolderPath** for the input blob is set to **adftutorial/** where **adftutorial** is the name of the container in your blob storage.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-173">The **FolderPath** for the input blob is set to **adftutorial/** where **adftutorial** is the name of the container in your blob storage.</span></span> <span data-ttu-id="2d9d7-174">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file to the container.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-174">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file to the container.</span></span>

    <span data-ttu-id="2d9d7-175">The FolderPath for the output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on the value of **SliceStart** (start date-time of each slice.)</span><span class="sxs-lookup"><span data-stu-id="2d9d7-175">The FolderPath for the output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on the value of **SliceStart** (start date-time of each slice.)</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
    
                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
                },
    
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
            }
        }
    });
    ```
10. <span data-ttu-id="2d9d7-176">Add the following code that **creates and activates a pipeline** to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-176">Add the following code that **creates and activates a pipeline** to the **Main** method.</span></span> <span data-ttu-id="2d9d7-177">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-177">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="2d9d7-178">The Copy Activity performs the data movement in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-178">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="2d9d7-179">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-179">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="2d9d7-180">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-180">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new PipelineCreateOrUpdateParameters()
    {
        Pipeline = new Pipeline()
        {
            Name = PipelineName,
            Properties = new PipelineProperties()
            {
                Description = "Demo Pipeline for data transfer between blobs",
    
                // Initial value for pipeline's active period. With this, you won't need to set slice status
                Start = PipelineActivePeriodStartTime,
                End = PipelineActivePeriodEndTime,
    
                Activities = new List<Activity>()
                {
                    new Activity()
                    {
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
                                Name = Dataset_Source
                            }
                        },
                        Outputs = new List<ActivityOutput>()
                        {
                            new ActivityOutput()
                            {
                                Name = Dataset_Destination
                            }
                        },
                        TypeProperties = new CopyActivity()
                        {
                            Source = new BlobSource(),
                            Sink = new BlobSink()
                            {
                                WriteBatchSize = 10000,
                                WriteBatchTimeout = TimeSpan.FromMinutes(10)
                            }
                        }
                    }
    
                },
            }
        }
    });
    ```
12. <span data-ttu-id="2d9d7-181">Add the following code to the **Main** method to get the status of a data slice of the output dataset.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-181">Add the following code to the **Main** method to get the status of a data slice of the output dataset.</span></span> <span data-ttu-id="2d9d7-182">There is only one slice expected in this sample.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-182">There is only one slice expected in this sample.</span></span>

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling the slice status");
        // wait before the next status check
        Thread.Sleep(1000 * 12);
    
        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });
    
        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```
13. <span data-ttu-id="2d9d7-183">**(optional)** Add the following code to get run details for a data slice to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-183">**(optional)** Add the following code to get run details for a data slice to the **Main** method.</span></span>

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for the output slice to be ready
    Console.WriteLine("\nGive it a few minutes for the output slice to be ready and press any key.");
    Console.ReadKey();
    
    var datasliceRunListResponse = client.DataSliceRuns.List(
        resourceGroupName,
        dataFactoryName,
        Dataset_Destination,
        new DataSliceRunListParameters()
        {
            DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
        });
    
    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }
    
    Console.WriteLine("\nPress any key to exit.");
    Console.ReadKey();
    ```
14. <span data-ttu-id="2d9d7-184">Add the following helper method used by the **Main** method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-184">Add the following helper method used by the **Main** method to the **Program** class.</span></span> <span data-ttu-id="2d9d7-185">This method pops a dialog box that lets you provide **user name** and **password** that you use to log in to Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-185">This method pops a dialog box that lets you provide **user name** and **password** that you use to log in to Azure portal.</span></span>

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        ClientCredential credential = new ClientCredential(
            ConfigurationManager.AppSettings["ApplicationId"],
            ConfigurationManager.AppSettings["Password"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientCredential: credential);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed to acquire token");
    }
    ```

15. <span data-ttu-id="2d9d7-186">In the Solution Explorer, expand the project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-186">In the Solution Explorer, expand the project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="2d9d7-187">Select check box for `System.Configuration` assembly and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-187">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="2d9d7-188">Build the console application.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-188">Build the console application.</span></span> <span data-ttu-id="2d9d7-189">Click **Build** on the menu and click **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-189">Click **Build** on the menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="2d9d7-190">Confirm that there is at least one file in the adftutorial container in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-190">Confirm that there is at least one file in the adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="2d9d7-191">If not, create Emp.txt file in Notepad with the following content and upload it to the adftutorial container.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-191">If not, create Emp.txt file in Notepad with the following content and upload it to the adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="2d9d7-192">Run the sample by clicking **Debug** -> **Start Debugging** on the menu.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-192">Run the sample by clicking **Debug** -> **Start Debugging** on the menu.</span></span> <span data-ttu-id="2d9d7-193">When you see the **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-193">When you see the **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="2d9d7-194">Use the Azure portal to verify that the data factory **APITutorialFactory** is created with the following artifacts:</span><span class="sxs-lookup"><span data-stu-id="2d9d7-194">Use the Azure portal to verify that the data factory **APITutorialFactory** is created with the following artifacts:</span></span>
    * <span data-ttu-id="2d9d7-195">Linked service: **AzureStorageLinkedService**</span><span class="sxs-lookup"><span data-stu-id="2d9d7-195">Linked service: **AzureStorageLinkedService**</span></span>
    * <span data-ttu-id="2d9d7-196">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-196">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="2d9d7-197">Pipeline: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="2d9d7-197">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="2d9d7-198">Verify that an output file is created in the **apifactoryoutput** folder in the **adftutorial** container.</span><span class="sxs-lookup"><span data-stu-id="2d9d7-198">Verify that an output file is created in the **apifactoryoutput** folder in the **adftutorial** container.</span></span>

## <a name="get-a-list-of-failed-data-slices"></a><span data-ttu-id="2d9d7-199">Get a list of failed data slices</span><span class="sxs-lookup"><span data-stu-id="2d9d7-199">Get a list of failed data slices</span></span> 

```csharp
// Parse the resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a><span data-ttu-id="2d9d7-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="2d9d7-200">Next steps</span></span>
<span data-ttu-id="2d9d7-201">See the following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage to an Azure SQL database:</span><span class="sxs-lookup"><span data-stu-id="2d9d7-201">See the following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage to an Azure SQL database:</span></span> 

- [<span data-ttu-id="2d9d7-202">Create a pipeline to copy data from Blob Storage to SQL Database</span><span class="sxs-lookup"><span data-stu-id="2d9d7-202">Create a pipeline to copy data from Blob Storage to SQL Database</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
