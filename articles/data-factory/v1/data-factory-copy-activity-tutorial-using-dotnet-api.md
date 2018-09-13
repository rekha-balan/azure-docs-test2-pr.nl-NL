---
title: 'Tutorial: Create a pipeline with Copy Activity using .NET API | Microsoft Docs'
description: In this tutorial, you create an Azure Data Factory pipeline with a Copy Activity by using .NET API.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: 58fc4007-b46d-4c8e-a279-cb9e479b3e2b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/22/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 991dc661c40f96a1c167821d76c01ea62d62dc52
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865581"
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a><span data-ttu-id="0f153-103">Tutorial: Create a pipeline with Copy Activity using .NET API</span><span class="sxs-lookup"><span data-stu-id="0f153-103">Tutorial: Create a pipeline with Copy Activity using .NET API</span></span>
> [!div class="op_single_selector"]
> * [Overview and prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Copy Wizard](data-factory-copy-data-wizard-tutorial.md)
> * [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [copy activity tutorial](../quickstart-create-data-factory-dot-net.md). 

<span data-ttu-id="0f153-114">In this article, you learn how to use [.NET API](https://portal.azure.com) to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="0f153-114">In this article, you learn how to use [.NET API](https://portal.azure.com) to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="0f153-115">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span><span class="sxs-lookup"><span data-stu-id="0f153-115">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="0f153-116">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="0f153-116">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="0f153-117">The copy activity copies data from a supported data store to a supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="0f153-117">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="0f153-118">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="0f153-118">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="0f153-119">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span><span class="sxs-lookup"><span data-stu-id="0f153-119">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="0f153-120">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="0f153-120">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="0f153-121">A pipeline can have more than one activity.</span><span class="sxs-lookup"><span data-stu-id="0f153-121">A pipeline can have more than one activity.</span></span> <span data-ttu-id="0f153-122">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span><span class="sxs-lookup"><span data-stu-id="0f153-122">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="0f153-123">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="0f153-123">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).
> 
> The data pipeline in this tutorial copies data from a source data store to a destination data store. For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a><span data-ttu-id="0f153-127">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0f153-127">Prerequisites</span></span>
* <span data-ttu-id="0f153-128">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to get an overview of the tutorial and complete the **prerequisite** steps.</span><span class="sxs-lookup"><span data-stu-id="0f153-128">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to get an overview of the tutorial and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="0f153-129">Visual Studio 2012 or 2013 or 2015</span><span class="sxs-lookup"><span data-stu-id="0f153-129">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="0f153-130">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="0f153-130">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span></span>
* <span data-ttu-id="0f153-131">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f153-131">Azure PowerShell.</span></span> <span data-ttu-id="0f153-132">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps) article to install Azure PowerShell on your computer.</span><span class="sxs-lookup"><span data-stu-id="0f153-132">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps) article to install Azure PowerShell on your computer.</span></span> <span data-ttu-id="0f153-133">You use Azure PowerShell to create an Azure Active Directory application.</span><span class="sxs-lookup"><span data-stu-id="0f153-133">You use Azure PowerShell to create an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="0f153-134">Create an application in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f153-134">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="0f153-135">Create an Azure Active Directory application, create a service principal for the application, and assign it to the **Data Factory Contributor** role.</span><span class="sxs-lookup"><span data-stu-id="0f153-135">Create an Azure Active Directory application, create a service principal for the application, and assign it to the **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="0f153-136">Launch **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="0f153-136">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="0f153-137">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0f153-137">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>

    ```PowerShell
    Connect-AzureRmAccount
    ```
3. <span data-ttu-id="0f153-138">Run the following command to view all the subscriptions for this account.</span><span class="sxs-lookup"><span data-stu-id="0f153-138">Run the following command to view all the subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="0f153-139">Run the following command to select the subscription that you want to work with.</span><span class="sxs-lookup"><span data-stu-id="0f153-139">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="0f153-140">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0f153-140">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > Note down **SubscriptionId** and **TenantId** from the output of this command.

5. <span data-ttu-id="0f153-142">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f153-142">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="0f153-143">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span><span class="sxs-lookup"><span data-stu-id="0f153-143">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="0f153-144">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="0f153-144">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="0f153-145">Create an Azure Active Directory application.</span><span class="sxs-lookup"><span data-stu-id="0f153-145">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="0f153-146">If you get the following error, specify a different URL and run the command again.</span><span class="sxs-lookup"><span data-stu-id="0f153-146">If you get the following error, specify a different URL and run the command again.</span></span>
    
    ```PowerShell
    Another object with the same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="0f153-147">Create the AD service principal.</span><span class="sxs-lookup"><span data-stu-id="0f153-147">Create the AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="0f153-148">Add service principal to the **Data Factory Contributor** role.</span><span class="sxs-lookup"><span data-stu-id="0f153-148">Add service principal to the **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="0f153-149">Get the application ID.</span><span class="sxs-lookup"><span data-stu-id="0f153-149">Get the application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="0f153-150">Note down the application ID (applicationID) from the output.</span><span class="sxs-lookup"><span data-stu-id="0f153-150">Note down the application ID (applicationID) from the output.</span></span>

<span data-ttu-id="0f153-151">You should have following four values from these steps:</span><span class="sxs-lookup"><span data-stu-id="0f153-151">You should have following four values from these steps:</span></span>

* <span data-ttu-id="0f153-152">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="0f153-152">Tenant ID</span></span>
* <span data-ttu-id="0f153-153">Subscription ID</span><span class="sxs-lookup"><span data-stu-id="0f153-153">Subscription ID</span></span>
* <span data-ttu-id="0f153-154">Application ID</span><span class="sxs-lookup"><span data-stu-id="0f153-154">Application ID</span></span>
* <span data-ttu-id="0f153-155">Password (specified in the first command)</span><span class="sxs-lookup"><span data-stu-id="0f153-155">Password (specified in the first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="0f153-156">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="0f153-156">Walkthrough</span></span>
1. <span data-ttu-id="0f153-157">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span><span class="sxs-lookup"><span data-stu-id="0f153-157">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="0f153-158">Launch **Visual Studio** 2012/2013/2015.</span><span class="sxs-lookup"><span data-stu-id="0f153-158">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="0f153-159">Click **File**, point to **New**, and click **Project**.</span><span class="sxs-lookup"><span data-stu-id="0f153-159">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="0f153-160">Expand **Templates**, and select **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="0f153-160">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="0f153-161">In this walkthrough, you use C#, but you can use any .NET language.</span><span class="sxs-lookup"><span data-stu-id="0f153-161">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="0f153-162">Select **Console Application** from the list of project types on the right.</span><span class="sxs-lookup"><span data-stu-id="0f153-162">Select **Console Application** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="0f153-163">Enter **DataFactoryAPITestApp** for the Name.</span><span class="sxs-lookup"><span data-stu-id="0f153-163">Enter **DataFactoryAPITestApp** for the Name.</span></span>
   6. <span data-ttu-id="0f153-164">Select **C:\ADFGetStarted** for the Location.</span><span class="sxs-lookup"><span data-stu-id="0f153-164">Select **C:\ADFGetStarted** for the Location.</span></span>
   7. <span data-ttu-id="0f153-165">Click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="0f153-165">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="0f153-166">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="0f153-166">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="0f153-167">In the **Package Manager Console**, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="0f153-167">In the **Package Manager Console**, do the following steps:</span></span>
   1. <span data-ttu-id="0f153-168">Run the following command to install Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="0f153-168">Run the following command to install Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="0f153-169">Run the following command to install Azure Active Directory package (you use Active Directory API in the code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="0f153-169">Run the following command to install Azure Active Directory package (you use Active Directory API in the code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="0f153-170">Add the following **appSetttings** section to the **App.config** file.</span><span class="sxs-lookup"><span data-stu-id="0f153-170">Add the following **appSetttings** section to the **App.config** file.</span></span> <span data-ttu-id="0f153-171">These settings are used by the helper method: **GetAuthorizationHeader**.</span><span class="sxs-lookup"><span data-stu-id="0f153-171">These settings are used by the helper method: **GetAuthorizationHeader**.</span></span>

    <span data-ttu-id="0f153-172">Replace values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span><span class="sxs-lookup"><span data-stu-id="0f153-172">Replace values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>

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

5. <span data-ttu-id="0f153-173">Add the following **using** statements to the source file (Program.cs) in the project.</span><span class="sxs-lookup"><span data-stu-id="0f153-173">Add the following **using** statements to the source file (Program.cs) in the project.</span></span>

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

6. <span data-ttu-id="0f153-174">Add the following code that creates an instance of **DataPipelineManagementClient** class to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="0f153-174">Add the following code that creates an instance of **DataPipelineManagementClient** class to the **Main** method.</span></span> <span data-ttu-id="0f153-175">You use this object to create a data factory, a linked service, input and output datasets, and a pipeline.</span><span class="sxs-lookup"><span data-stu-id="0f153-175">You use this object to create a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="0f153-176">You also use this object to monitor slices of a dataset at runtime.</span><span class="sxs-lookup"><span data-stu-id="0f153-176">You also use this object to monitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client
    string resourceGroupName = "ADFTutorialResourceGroup";
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > Replace the value of **resourceGroupName** with the name of your Azure resource group.
   >
   > Update name of the data factory (dataFactoryName) to be unique. Name of the data factory must be globally unique. See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.

7. <span data-ttu-id="0f153-181">Add the following code that creates a **data factory** to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="0f153-181">Add the following code that creates a **data factory** to the **Main** method.</span></span>

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

    <span data-ttu-id="0f153-182">A data factory can have one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="0f153-182">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="0f153-183">A pipeline can have one or more activities in it.</span><span class="sxs-lookup"><span data-stu-id="0f153-183">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="0f153-184">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span><span class="sxs-lookup"><span data-stu-id="0f153-184">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="0f153-185">Let's start with creating the data factory in this step.</span><span class="sxs-lookup"><span data-stu-id="0f153-185">Let's start with creating the data factory in this step.</span></span>
8. <span data-ttu-id="0f153-186">Add the following code that creates an **Azure Storage linked service** to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="0f153-186">Add the following code that creates an **Azure Storage linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.

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

    <span data-ttu-id="0f153-188">You create linked services in a data factory to link your data stores and compute services to the data factory.</span><span class="sxs-lookup"><span data-stu-id="0f153-188">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="0f153-189">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0f153-189">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="0f153-190">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span><span class="sxs-lookup"><span data-stu-id="0f153-190">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

    <span data-ttu-id="0f153-191">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="0f153-191">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

    <span data-ttu-id="0f153-192">The AzureStorageLinkedService links your Azure storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="0f153-192">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="0f153-193">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="0f153-193">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
9. <span data-ttu-id="0f153-194">Add the following code that creates an **Azure SQL linked service** to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="0f153-194">Add the following code that creates an **Azure SQL linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > Replace **servername**, **databasename**, **username**, and **password** with names of your Azure SQL server, database, user, and password.

    ```csharp
    // create a linked service for output data store: Azure SQL Database
    Console.WriteLine("Creating Azure SQL Database linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureSqlLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureSqlDatabaseLinkedService("Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30")
                )
            }
        }
    );
    ```

    <span data-ttu-id="0f153-196">AzureSqlLinkedService links your Azure SQL database to the data factory.</span><span class="sxs-lookup"><span data-stu-id="0f153-196">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="0f153-197">The data that is copied from the blob storage is stored in this database.</span><span class="sxs-lookup"><span data-stu-id="0f153-197">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="0f153-198">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="0f153-198">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
10. <span data-ttu-id="0f153-199">Add the following code that creates **input and output datasets** to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="0f153-199">Add the following code that creates **input and output datasets** to the **Main** method.</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "InputDataset";
    string Dataset_Destination = "OutputDataset";

    Console.WriteLine("Creating input dataset of type: Azure Blob");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                Structure = new List<DataElement>()
                {
                    new DataElement() { Name = "FirstName", Type = "String" },
                    new DataElement() { Name = "LastName", Type = "String" }
                },
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

    Console.WriteLine("Creating output dataset of type: Azure SQL");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new DatasetCreateOrUpdateParameters()
        {
            Dataset = new Dataset()
            {
                Name = Dataset_Destination,
                Properties = new DatasetProperties()
                {
                    Structure = new List<DataElement>()
                    {
                        new DataElement() { Name = "FirstName", Type = "String" },
                        new DataElement() { Name = "LastName", Type = "String" }
                    },
                    LinkedServiceName = "AzureSqlLinkedService",
                    TypeProperties = new AzureSqlTableDataset()
                    {
                        TableName = "emp"
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
    
    <span data-ttu-id="0f153-200">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span><span class="sxs-lookup"><span data-stu-id="0f153-200">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="0f153-201">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span><span class="sxs-lookup"><span data-stu-id="0f153-201">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

    <span data-ttu-id="0f153-202">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="0f153-202">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="0f153-203">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span><span class="sxs-lookup"><span data-stu-id="0f153-203">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="0f153-204">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="0f153-204">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="0f153-205">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span><span class="sxs-lookup"><span data-stu-id="0f153-205">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span>

    <span data-ttu-id="0f153-206">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span><span class="sxs-lookup"><span data-stu-id="0f153-206">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="0f153-207">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="0f153-207">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="0f153-208">In this tutorial, you specify a value for the fileName.</span><span class="sxs-lookup"><span data-stu-id="0f153-208">In this tutorial, you specify a value for the fileName.</span></span>    

    <span data-ttu-id="0f153-209">In this step, you create an output dataset named **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="0f153-209">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="0f153-210">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="0f153-210">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService**.</span></span>
11. <span data-ttu-id="0f153-211">Add the following code that **creates and activates a pipeline** to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="0f153-211">Add the following code that **creates and activates a pipeline** to the **Main** method.</span></span> <span data-ttu-id="0f153-212">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span><span class="sxs-lookup"><span data-stu-id="0f153-212">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2017, 5, 11, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = new DateTime(2017, 5, 12, 0, 0, 0, 0, DateTimeKind.Utc);
    string PipelineName = "ADFTutorialPipeline";

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
                            Name = "BlobToAzureSql",
                            Inputs = new List<ActivityInput>()
                            {
                                new ActivityInput() {
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
                    }
                }
            }
        });
    ```

    <span data-ttu-id="0f153-213">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="0f153-213">Note the following points:</span></span>
   
    - <span data-ttu-id="0f153-214">In the activities section, there is only one activity whose **type** is set to **Copy**.</span><span class="sxs-lookup"><span data-stu-id="0f153-214">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="0f153-215">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="0f153-215">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="0f153-216">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="0f153-216">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="0f153-217">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="0f153-217">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="0f153-218">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span><span class="sxs-lookup"><span data-stu-id="0f153-218">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="0f153-219">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="0f153-219">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="0f153-220">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span><span class="sxs-lookup"><span data-stu-id="0f153-220">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
   
    <span data-ttu-id="0f153-221">Currently, output dataset is what drives the schedule.</span><span class="sxs-lookup"><span data-stu-id="0f153-221">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="0f153-222">In this tutorial, output dataset is configured to produce a slice once an hour.</span><span class="sxs-lookup"><span data-stu-id="0f153-222">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="0f153-223">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span><span class="sxs-lookup"><span data-stu-id="0f153-223">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="0f153-224">Therefore, 24 slices of output dataset are produced by the pipeline.</span><span class="sxs-lookup"><span data-stu-id="0f153-224">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span>
12. <span data-ttu-id="0f153-225">Add the following code to the **Main** method to get the status of a data slice of the output dataset.</span><span class="sxs-lookup"><span data-stu-id="0f153-225">Add the following code to the **Main** method to get the status of a data slice of the output dataset.</span></span> <span data-ttu-id="0f153-226">There is only slice expected in this sample.</span><span class="sxs-lookup"><span data-stu-id="0f153-226">There is only slice expected in this sample.</span></span>

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

13. <span data-ttu-id="0f153-227">Add the following code to get run details for a data slice to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="0f153-227">Add the following code to get run details for a data slice to the **Main** method.</span></span>

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
            }
        );

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

14. <span data-ttu-id="0f153-228">Add the following helper method used by the **Main** method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="0f153-228">Add the following helper method used by the **Main** method to the **Program** class.</span></span>

    > [!NOTE] 
    > When you copy and paste the following code, make sure that the copied code is at the same level as the Main method.

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

15. <span data-ttu-id="0f153-230">In the Solution Explorer, expand the project (DataFactoryAPITestApp), right-click **References**, and click **Add Reference**.</span><span class="sxs-lookup"><span data-stu-id="0f153-230">In the Solution Explorer, expand the project (DataFactoryAPITestApp), right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="0f153-231">Select check box for **System.Configuration** assembly.</span><span class="sxs-lookup"><span data-stu-id="0f153-231">Select check box for **System.Configuration** assembly.</span></span> <span data-ttu-id="0f153-232">and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="0f153-232">and click **OK**.</span></span>
16. <span data-ttu-id="0f153-233">Build the console application.</span><span class="sxs-lookup"><span data-stu-id="0f153-233">Build the console application.</span></span> <span data-ttu-id="0f153-234">Click **Build** on the menu and click **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="0f153-234">Click **Build** on the menu and click **Build Solution**.</span></span>
17. <span data-ttu-id="0f153-235">Confirm that there is at least one file in the **adftutorial** container in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="0f153-235">Confirm that there is at least one file in the **adftutorial** container in your Azure blob storage.</span></span> <span data-ttu-id="0f153-236">If not, create **Emp.txt** file in Notepad with the following content and upload it to the adftutorial container.</span><span class="sxs-lookup"><span data-stu-id="0f153-236">If not, create **Emp.txt** file in Notepad with the following content and upload it to the adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
18. <span data-ttu-id="0f153-237">Run the sample by clicking **Debug** -> **Start Debugging** on the menu.</span><span class="sxs-lookup"><span data-stu-id="0f153-237">Run the sample by clicking **Debug** -> **Start Debugging** on the menu.</span></span> <span data-ttu-id="0f153-238">When you see the **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="0f153-238">When you see the **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
19. <span data-ttu-id="0f153-239">Use the Azure portal to verify that the data factory **APITutorialFactory** is created with the following artifacts:</span><span class="sxs-lookup"><span data-stu-id="0f153-239">Use the Azure portal to verify that the data factory **APITutorialFactory** is created with the following artifacts:</span></span>
   * <span data-ttu-id="0f153-240">Linked service: **LinkedService_AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="0f153-240">Linked service: **LinkedService_AzureStorage**</span></span>
   * <span data-ttu-id="0f153-241">Dataset: **InputDataset** and **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="0f153-241">Dataset: **InputDataset** and **OutputDataset**.</span></span>
   * <span data-ttu-id="0f153-242">Pipeline: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="0f153-242">Pipeline: **PipelineBlobSample**</span></span>
20. <span data-ttu-id="0f153-243">Verify that the two employee records are created in the **emp** table in the specified Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="0f153-243">Verify that the two employee records are created in the **emp** table in the specified Azure SQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f153-244">Next steps</span><span class="sxs-lookup"><span data-stu-id="0f153-244">Next steps</span></span>
<span data-ttu-id="0f153-245">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="0f153-245">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>

<span data-ttu-id="0f153-246">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span><span class="sxs-lookup"><span data-stu-id="0f153-246">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="0f153-247">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span><span class="sxs-lookup"><span data-stu-id="0f153-247">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="0f153-248">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span><span class="sxs-lookup"><span data-stu-id="0f153-248">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>

