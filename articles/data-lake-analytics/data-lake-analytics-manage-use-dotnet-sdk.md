---
title: Manage Azure Data Lake Analytics using Azure .NET SDK | Microsoft Docs
description: 'Learn how to manage Data Lake Analytics jobs, data sources, users. '
services: data-lake-analytics
documentationcenter: ''
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 811d172d-9873-4ce9-a6d5-c1a26b374c79
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/3/2017
ms.author: jgao
ms.openlocfilehash: bed6fa355f3b32bb53aee002e34ca61f2ea2aa5b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540677"
---
# <a name="manage-azure-data-lake-analytics-using-azure-net-sdk"></a><span data-ttu-id="94a44-103">Manage Azure Data Lake Analytics using Azure .NET SDK</span><span class="sxs-lookup"><span data-stu-id="94a44-103">Manage Azure Data Lake Analytics using Azure .NET SDK</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="94a44-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="94a44-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure .NET SDK.</span></span> <span data-ttu-id="94a44-105">To see management topics using other tools, click the tab select above.</span><span class="sxs-lookup"><span data-stu-id="94a44-105">To see management topics using other tools, click the tab select above.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94a44-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="94a44-106">Prerequisites</span></span>

* <span data-ttu-id="94a44-107">**Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed**.</span><span class="sxs-lookup"><span data-stu-id="94a44-107">**Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed**.</span></span>
* <span data-ttu-id="94a44-108">**Microsoft Azure SDK for .NET version 2.5 or above**.</span><span class="sxs-lookup"><span data-stu-id="94a44-108">**Microsoft Azure SDK for .NET version 2.5 or above**.</span></span>  <span data-ttu-id="94a44-109">Install it using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="94a44-109">Install it using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="94a44-110">**Required Nuget Packages**</span><span class="sxs-lookup"><span data-stu-id="94a44-110">**Required Nuget Packages**</span></span>

### <a name="install-nuget-packages"></a><span data-ttu-id="94a44-111">Install Nuget packages</span><span class="sxs-lookup"><span data-stu-id="94a44-111">Install Nuget packages</span></span>
   
   1. <span data-ttu-id="94a44-112">In Visual Studio, right-click the project name in the Solution Explorer and click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="94a44-112">In Visual Studio, right-click the project name in the Solution Explorer and click **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="94a44-113">In the **Nuget Package Manager** tab, make sure that **Package source** is set to **nuget.org** and that **Include prerelease** check box is selected.</span><span class="sxs-lookup"><span data-stu-id="94a44-113">In the **Nuget Package Manager** tab, make sure that **Package source** is set to **nuget.org** and that **Include prerelease** check box is selected.</span></span>

   3. <span data-ttu-id="94a44-114">Search for and install the following NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="94a44-114">Search for and install the following NuGet packages:</span></span>

    - <span data-ttu-id="94a44-115">Microsoft.Rest.ClientRuntime.Azure.Authentication - This tutorial uses V2.2.12</span><span class="sxs-lookup"><span data-stu-id="94a44-115">Microsoft.Rest.ClientRuntime.Azure.Authentication - This tutorial uses V2.2.12</span></span>
    - <span data-ttu-id="94a44-116">Microsoft.Azure.Management.DataLake.Analytics - This tutorial uses V2.1.0 preview</span><span class="sxs-lookup"><span data-stu-id="94a44-116">Microsoft.Azure.Management.DataLake.Analytics - This tutorial uses V2.1.0 preview</span></span>
    - <span data-ttu-id="94a44-117">Microsoft.Azure.Management.DataLake.Store - This tutorial uses V2.1.0 preview</span><span class="sxs-lookup"><span data-stu-id="94a44-117">Microsoft.Azure.Management.DataLake.Store - This tutorial uses V2.1.0 preview</span></span>

   4. <span data-ttu-id="94a44-118">Close the **Nuget Package Manager**.</span><span class="sxs-lookup"><span data-stu-id="94a44-118">Close the **Nuget Package Manager**.</span></span>

## <a name="client-management-objects"></a><span data-ttu-id="94a44-119">Client management objects</span><span class="sxs-lookup"><span data-stu-id="94a44-119">Client management objects</span></span>
<span data-ttu-id="94a44-120">The Azure Data Lake Analytics and Azure Data Lake Store APIs include sets of client management objects from which you do most of your programming.</span><span class="sxs-lookup"><span data-stu-id="94a44-120">The Azure Data Lake Analytics and Azure Data Lake Store APIs include sets of client management objects from which you do most of your programming.</span></span> <span data-ttu-id="94a44-121">These objects are in these two namespaces:</span><span class="sxs-lookup"><span data-stu-id="94a44-121">These objects are in these two namespaces:</span></span>
* <span data-ttu-id="94a44-122">Microsoft.Azure.Management.DataLake.Analytics</span><span class="sxs-lookup"><span data-stu-id="94a44-122">Microsoft.Azure.Management.DataLake.Analytics</span></span>
* <span data-ttu-id="94a44-123">Microsoft.Azure.Management.DataLake.Store</span><span class="sxs-lookup"><span data-stu-id="94a44-123">Microsoft.Azure.Management.DataLake.Store</span></span>

<span data-ttu-id="94a44-124">The following table shows the client management objects, with variables that used for their code examples throughout this article.</span><span class="sxs-lookup"><span data-stu-id="94a44-124">The following table shows the client management objects, with variables that used for their code examples throughout this article.</span></span>

| <span data-ttu-id="94a44-125">Client Management Object</span><span class="sxs-lookup"><span data-stu-id="94a44-125">Client Management Object</span></span>                  | <span data-ttu-id="94a44-126">Code Variable</span><span class="sxs-lookup"><span data-stu-id="94a44-126">Code Variable</span></span>        |
| ----------------------------------------- | -------------------- |
| <span data-ttu-id="94a44-127">DataLakeStoreAccountManagementClient</span><span class="sxs-lookup"><span data-stu-id="94a44-127">DataLakeStoreAccountManagementClient</span></span>      | <span data-ttu-id="94a44-128">adlsClient</span><span class="sxs-lookup"><span data-stu-id="94a44-128">adlsClient</span></span>           |
| <span data-ttu-id="94a44-129">DataLakeAnalyticsAccountManagementClient</span><span class="sxs-lookup"><span data-stu-id="94a44-129">DataLakeAnalyticsAccountManagementClient</span></span>  | <span data-ttu-id="94a44-130">adlaClient</span><span class="sxs-lookup"><span data-stu-id="94a44-130">adlaClient</span></span>           |
| <span data-ttu-id="94a44-131">DataLakeStoreFileSystemManagementClient</span><span class="sxs-lookup"><span data-stu-id="94a44-131">DataLakeStoreFileSystemManagementClient</span></span>   | <span data-ttu-id="94a44-132">adlsFileSystemClient</span><span class="sxs-lookup"><span data-stu-id="94a44-132">adlsFileSystemClient</span></span> |
| <span data-ttu-id="94a44-133">DataLakeAnalyticsCatalogManagementClient</span><span class="sxs-lookup"><span data-stu-id="94a44-133">DataLakeAnalyticsCatalogManagementClient</span></span>  | <span data-ttu-id="94a44-134">adlaCatalogClient</span><span class="sxs-lookup"><span data-stu-id="94a44-134">adlaCatalogClient</span></span>    |
| <span data-ttu-id="94a44-135">DataLakeAnalyticsJobManagementClient</span><span class="sxs-lookup"><span data-stu-id="94a44-135">DataLakeAnalyticsJobManagementClient</span></span>      | <span data-ttu-id="94a44-136">adlaJobClient</span><span class="sxs-lookup"><span data-stu-id="94a44-136">adlaJobClient</span></span>        |

### <a name="data-lake-store-management-client-objects"></a><span data-ttu-id="94a44-137">Data Lake Store management client objects:</span><span class="sxs-lookup"><span data-stu-id="94a44-137">Data Lake Store management client objects:</span></span>
* <span data-ttu-id="94a44-138">DataLakeStoreAccountManagementClient - Use to create and manage Data Lake Store accounts.</span><span class="sxs-lookup"><span data-stu-id="94a44-138">DataLakeStoreAccountManagementClient - Use to create and manage Data Lake Store accounts.</span></span>
* <span data-ttu-id="94a44-139">DataLakeFileSystemAccountManagementClient - Use for file system tasks such as to create folders and files, upload files, list files, access ACL's and credentials, and add links to Azure Storage blobs.</span><span class="sxs-lookup"><span data-stu-id="94a44-139">DataLakeFileSystemAccountManagementClient - Use for file system tasks such as to create folders and files, upload files, list files, access ACL's and credentials, and add links to Azure Storage blobs.</span></span>

<span data-ttu-id="94a44-140">Although you can create links to Azure Storage from Data Lake, you cannot access its content.</span><span class="sxs-lookup"><span data-stu-id="94a44-140">Although you can create links to Azure Storage from Data Lake, you cannot access its content.</span></span> <span data-ttu-id="94a44-141">To do so, you must use the Azure Storage SDK APIs.</span><span class="sxs-lookup"><span data-stu-id="94a44-141">To do so, you must use the Azure Storage SDK APIs.</span></span> <span data-ttu-id="94a44-142">You can, however, run U-SQL scripts on Azure Storage blobs.</span><span class="sxs-lookup"><span data-stu-id="94a44-142">You can, however, run U-SQL scripts on Azure Storage blobs.</span></span>

### <a name="data-lake-analytics-management-client-objects"></a><span data-ttu-id="94a44-143">Data Lake Analytics management client objects:</span><span class="sxs-lookup"><span data-stu-id="94a44-143">Data Lake Analytics management client objects:</span></span>
* <span data-ttu-id="94a44-144">DataLakeAnalyticsAccountManagementClient - Use to create and manage Data Lake Analytics accounts.</span><span class="sxs-lookup"><span data-stu-id="94a44-144">DataLakeAnalyticsAccountManagementClient - Use to create and manage Data Lake Analytics accounts.</span></span>
* <span data-ttu-id="94a44-145">DataLakeAnalyticsCatalogManagementClient - Use to explore the catalog items in Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="94a44-145">DataLakeAnalyticsCatalogManagementClient - Use to explore the catalog items in Data Lake Analytics.</span></span>
* <span data-ttu-id="94a44-146">DataLakeAnalyticsJobManagementClient - Submit and manage jobs in Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="94a44-146">DataLakeAnalyticsJobManagementClient - Submit and manage jobs in Data Lake Analytics.</span></span>

### <a name="example"></a><span data-ttu-id="94a44-147">Example</span><span class="sxs-lookup"><span data-stu-id="94a44-147">Example</span></span>

<span data-ttu-id="94a44-148">Initialize client management objects using your credentials (creds) as obtained by your preferred authentication method, described next in this article.</span><span class="sxs-lookup"><span data-stu-id="94a44-148">Initialize client management objects using your credentials (creds) as obtained by your preferred authentication method, described next in this article.</span></span> 

    // Only the Data Lake Analytics and Data Lake Store  
    // objects need a subscription ID.
    adlsClient = new DataLakeStoreAccountManagementClient(creds);
    adlsClient.SubscriptionId = <Subscription-ID>;

    adlaClient = new DataLakeAnalyticsAccountManagementClient(creds);
    adlaClient.SubscriptionId = <Subscription-ID>;

    adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);
    adlaCatalogClient = new DataLakeAnalyticsCatalogManagementClient(creds);
    adlaJobClient = new DataLakeAnalyticsJobManagementClient(creds);


    // Methods to create and manage Data Lake Analytics
    . . .

## <a name="authenticate-and-connect-to-azure-data-lake-analytics"></a><span data-ttu-id="94a44-149">Authenticate and connect to Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="94a44-149">Authenticate and connect to Azure Data Lake Analytics</span></span>
<span data-ttu-id="94a44-150">You have multiple options for logging on to Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="94a44-150">You have multiple options for logging on to Azure Data Lake Analytics.</span></span>

### <a name="interactive-with-provided-credentials"></a><span data-ttu-id="94a44-151">Interactive with provided credentials</span><span class="sxs-lookup"><span data-stu-id="94a44-151">Interactive with provided credentials</span></span>
<span data-ttu-id="94a44-152">The following snippet shows the easiest authentication by the user providing credentials, such as a username and password or a pin number.</span><span class="sxs-lookup"><span data-stu-id="94a44-152">The following snippet shows the easiest authentication by the user providing credentials, such as a username and password or a pin number.</span></span>

    // User login via interactive popup
    // Use the client ID of an existing AAD "native nlient" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenantId = "<Tenant ID>"; // Replace this string with the user's Azure Active Directory tenant ID.
    var clientId = "1950a258-227b-4e31-a9cf-717495945fc2"; // Sample client ID
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(_tenantId, activeDirectoryClientSettings).Result;

<span data-ttu-id="94a44-153">We recommend creating your own application and service principal within your Azure Active Directory tenant, then using the client ID for that application, rather than the sample ID used here.</span><span class="sxs-lookup"><span data-stu-id="94a44-153">We recommend creating your own application and service principal within your Azure Active Directory tenant, then using the client ID for that application, rather than the sample ID used here.</span></span>

### <a name="non-interactive-with-a-client-secret"></a><span data-ttu-id="94a44-154">Non-interactive with a client secret</span><span class="sxs-lookup"><span data-stu-id="94a44-154">Non-interactive with a client secret</span></span>
<span data-ttu-id="94a44-155">You can use the following snippet to authenticate your application non-interactively, using the client secret / key for an application / service principal.</span><span class="sxs-lookup"><span data-stu-id="94a44-155">You can use the following snippet to authenticate your application non-interactively, using the client secret / key for an application / service principal.</span></span> <span data-ttu-id="94a44-156">Use this authentication option with an existing [Azure AD "Web App" Application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="94a44-156">Use this authentication option with an existing [Azure AD "Web App" Application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

    // Service principal / application authentication with client secret / key
    // Use the client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenantId = "<Azure tenant ID>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = ApplicationTokenProvider.LoginSilentAsync(tenantId, clientCredential).Result;

### <a name="non-interactive-with-a-service-principal"></a><span data-ttu-id="94a44-157">Non-interactive with a service principal</span><span class="sxs-lookup"><span data-stu-id="94a44-157">Non-interactive with a service principal</span></span>
<span data-ttu-id="94a44-158">As a third option, the following snippet can be used to authenticate your application non-interactively, using the certificate for an application / service principal.</span><span class="sxs-lookup"><span data-stu-id="94a44-158">As a third option, the following snippet can be used to authenticate your application non-interactively, using the certificate for an application / service principal.</span></span> <span data-ttu-id="94a44-159">Use this authentication option with an existing [Azure AD "Web App" Application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="94a44-159">Use this authentication option with an existing [Azure AD "Web App" Application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

    // Service principal / application authentication with certificate
    // Use the client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenantId = "<Azure tenant ID>";
    var webApp_clientId = "<AAD-application-clientid>";
    System.Security.Cryptography.X509Certificates.X509Certificate2 clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = ApplicationTokenProvider.LoginSilentWithCertificateAsync(tenantId, clientAssertionCertificate).Result;

## <a name="create-accounts"></a><span data-ttu-id="94a44-160">Create accounts</span><span class="sxs-lookup"><span data-stu-id="94a44-160">Create accounts</span></span>
<span data-ttu-id="94a44-161">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="94a44-161">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="94a44-162">Also, a Data Lake Analytics account requires at least one Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="94a44-162">Also, a Data Lake Analytics account requires at least one Data Lake Store account.</span></span> <span data-ttu-id="94a44-163">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md)</span><span class="sxs-lookup"><span data-stu-id="94a44-163">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md)</span></span>

### <a name="create-an-azure-resource-group"></a><span data-ttu-id="94a44-164">Create an Azure Resource Group</span><span class="sxs-lookup"><span data-stu-id="94a44-164">Create an Azure Resource Group</span></span>
<span data-ttu-id="94a44-165">If you haven't already created one, you must have an Azure Resource Group to create your Data Lake Analytics components.</span><span class="sxs-lookup"><span data-stu-id="94a44-165">If you haven't already created one, you must have an Azure Resource Group to create your Data Lake Analytics components.</span></span> <span data-ttu-id="94a44-166">You will need your authentication credentials, subscription ID, and a location.</span><span class="sxs-lookup"><span data-stu-id="94a44-166">You will need your authentication credentials, subscription ID, and a location.</span></span> <span data-ttu-id="94a44-167">The following code shows how to create a resource group:</span><span class="sxs-lookup"><span data-stu-id="94a44-167">The following code shows how to create a resource group:</span></span>

    string rgName == "<value>"; // specify name for the new resrouce group
    var resourceManagementClient = new ResourceManagementClient(credential) { SubscriptionId = subscriptionId };
    var resourceGroup = new ResourceGroup { Location = location };
    resourceManagementClient.ResourceGroups.CreateOrUpdate(groupName, rgName);

<span data-ttu-id="94a44-168">For more information, see [Azure Resource Groups and Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span><span class="sxs-lookup"><span data-stu-id="94a44-168">For more information, see [Azure Resource Groups and Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span></span>


### <a name="create-a-data-lake-store-account"></a><span data-ttu-id="94a44-169">Create a Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="94a44-169">Create a Data Lake Store account</span></span>
<span data-ttu-id="94a44-170">The following code shows how to create a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="94a44-170">The following code shows how to create a Data Lake Store account.</span></span> <span data-ttu-id="94a44-171">Before you use the Create method, you must define its parameters by specifying a location.</span><span class="sxs-lookup"><span data-stu-id="94a44-171">Before you use the Create method, you must define its parameters by specifying a location.</span></span>

    var adlsParameters = new DataLakeStoreAccount(location: _location);
    adlsClient.Account.Create(_resourceGroupName, _adlsAccountName, adlsParameters);

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="94a44-172">Create a Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="94a44-172">Create a Data Lake Analytics account</span></span>
<span data-ttu-id="94a44-173">The following code shows how to create a Data Lake Analytics account, using the asynchronous method.</span><span class="sxs-lookup"><span data-stu-id="94a44-173">The following code shows how to create a Data Lake Analytics account, using the asynchronous method.</span></span> <span data-ttu-id="94a44-174">The CreateAsync method takes a collection of Data Lake Store accounts as one of its parameters.</span><span class="sxs-lookup"><span data-stu-id="94a44-174">The CreateAsync method takes a collection of Data Lake Store accounts as one of its parameters.</span></span> <span data-ttu-id="94a44-175">This collection must be populated with instances of DataLakeStoreAccountInfo objects.</span><span class="sxs-lookup"><span data-stu-id="94a44-175">This collection must be populated with instances of DataLakeStoreAccountInfo objects.</span></span> <span data-ttu-id="94a44-176">In this example, these DataLakeStoreAccountInfo objects are obtained from a helper method (AdlaFromAdlsStoreAccounts).</span><span class="sxs-lookup"><span data-stu-id="94a44-176">In this example, these DataLakeStoreAccountInfo objects are obtained from a helper method (AdlaFromAdlsStoreAccounts).</span></span>

<span data-ttu-id="94a44-177">For any Data Lake Analytics account, you only need to include the Data Lake Store accounts that you need to perform the needed analytics.</span><span class="sxs-lookup"><span data-stu-id="94a44-177">For any Data Lake Analytics account, you only need to include the Data Lake Store accounts that you need to perform the needed analytics.</span></span> <span data-ttu-id="94a44-178">One of these Data Lake Store accounts, must be the default Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="94a44-178">One of these Data Lake Store accounts, must be the default Data Lake Store account.</span></span>

    try
    {
        var adlaAccount = new DataLakeAnalyticsAccount()
        {
            DefaultDataLakeStoreAccount = “Accounting”,
            Location = _location,
            DataLakeStoreAccounts = new DataLakeStoreAccountInfo[]{
                new DataLakeStoreAccountInfo(“Expenditures”),
                new DataLakeStoreAccountInfo(“Accounting”)
            }
        };
        adlaClient.Account.Create(_resourceGroupName, newAccountName, adlaAccount);
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.Message);
    }

## <a name="manage-accounts"></a><span data-ttu-id="94a44-179">Manage accounts</span><span class="sxs-lookup"><span data-stu-id="94a44-179">Manage accounts</span></span>

### <a name="list-data-lake-store-and-data-lake-analytics-accounts"></a><span data-ttu-id="94a44-180">List Data Lake Store and Data Lake Analytics accounts</span><span class="sxs-lookup"><span data-stu-id="94a44-180">List Data Lake Store and Data Lake Analytics accounts</span></span>
<span data-ttu-id="94a44-181">The following code lists the Data Lake Store accounts in a subscription.</span><span class="sxs-lookup"><span data-stu-id="94a44-181">The following code lists the Data Lake Store accounts in a subscription.</span></span> <span data-ttu-id="94a44-182">List operations do not always provide all the properties of an object and that in some cases you need to do a Get operation on the object.</span><span class="sxs-lookup"><span data-stu-id="94a44-182">List operations do not always provide all the properties of an object and that in some cases you need to do a Get operation on the object.</span></span>

    var adlsAccounts = adlsClient.Account.List().ToList();
    foreach (var adls in adlsAccounts)
    {
        Console.WriteLine($"\t{adls.Name});

    }

    var adlaAccounts = adlaClient.Account.List().ToList();
    for (var adla in AdlaAccounts)
    {
        Console.WriteLine($"\t{adla.Name}");
    }



### <a name="get-an-account"></a><span data-ttu-id="94a44-183">Get an account</span><span class="sxs-lookup"><span data-stu-id="94a44-183">Get an account</span></span>
<span data-ttu-id="94a44-184">The following code uses a DataLakeAnalyticsAccountManagementClient to get a Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="94a44-184">The following code uses a DataLakeAnalyticsAccountManagementClient to get a Data Lake Analytics account.</span></span> <span data-ttu-id="94a44-185">First a check is made to see if the account exists.</span><span class="sxs-lookup"><span data-stu-id="94a44-185">First a check is made to see if the account exists.</span></span>

    DataLakeAnalyticsAccount adlaGet;
    if (adlaClient.Account.Exists(_resourceGroupName, accountName))
    {
        adlaGet = adlaClient.Account.Get(_resourceGroupName, accountName);
        Console.WriteLine($"{adlaGet.Name}\tCreated: {adlaGet.CreationTime}");
    }

<span data-ttu-id="94a44-186">Similarly, you can use DataLakeStoreAccountManagementClient (adlsClient) in the same way to get a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="94a44-186">Similarly, you can use DataLakeStoreAccountManagementClient (adlsClient) in the same way to get a Data Lake Store account.</span></span>

### <a name="delete-an-account"></a><span data-ttu-id="94a44-187">Delete an account</span><span class="sxs-lookup"><span data-stu-id="94a44-187">Delete an account</span></span>
<span data-ttu-id="94a44-188">The following code deletes a Data Lake Analytics account if it exists.</span><span class="sxs-lookup"><span data-stu-id="94a44-188">The following code deletes a Data Lake Analytics account if it exists.</span></span>

    if (adlaClient.Account.Exists(_resourceGroupName, accountName))
    {
        adlaClient.Account.Delete(_resourceGroupName, accountName);
        Console.WriteLine($"{accountName} Deleted");
    }
    else
    {
        Console.WriteLine($"{accountName} does not exist.");
    }

<span data-ttu-id="94a44-189">You can also delete a Data Lake Store account in the same way with a DataLakeStoreAccountManagementClient.</span><span class="sxs-lookup"><span data-stu-id="94a44-189">You can also delete a Data Lake Store account in the same way with a DataLakeStoreAccountManagementClient.</span></span>

### <a name="get-the-default-data-lake-store-account"></a><span data-ttu-id="94a44-190">Get the default Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="94a44-190">Get the default Data Lake Store account</span></span>
<span data-ttu-id="94a44-191">Every Data Lake Analytics account requires a default Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="94a44-191">Every Data Lake Analytics account requires a default Data Lake Store account.</span></span> <span data-ttu-id="94a44-192">Use this code to determine the default Store account for an Analytics account.</span><span class="sxs-lookup"><span data-stu-id="94a44-192">Use this code to determine the default Store account for an Analytics account.</span></span>

    if (adlaClient.Account.Exists(_resourceGroupName, accountName))
    {
        DataLakeAnalyticsAccount adlaGet = adlaClient.Account.Get(_resourceGroupName, accountName);
        Console.WriteLine($"{adlaGet.Name} default DL store account: {adlaGet.DefaultDataLakeStoreAccount}");
    }


## <a name="manage-data-sources"></a><span data-ttu-id="94a44-193">Manage data sources</span><span class="sxs-lookup"><span data-stu-id="94a44-193">Manage data sources</span></span>
<span data-ttu-id="94a44-194">Data Lake Analytics currently supports the following data sources:</span><span class="sxs-lookup"><span data-stu-id="94a44-194">Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="94a44-195">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="94a44-195">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="94a44-196">Azure Storage Account</span><span class="sxs-lookup"><span data-stu-id="94a44-196">Azure Storage Account</span></span>](../storage/storage-introduction.md)

<span data-ttu-id="94a44-197">When you create an Analytics account, you must designate an Azure Data Lake Store account to be the default Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="94a44-197">When you create an Analytics account, you must designate an Azure Data Lake Store account to be the default Data Lake Store account.</span></span> <span data-ttu-id="94a44-198">The default Data Lake Store account is used to store job metadata and job audit logs.</span><span class="sxs-lookup"><span data-stu-id="94a44-198">The default Data Lake Store account is used to store job metadata and job audit logs.</span></span> <span data-ttu-id="94a44-199">After you have created an Analytics account, you can add additional Data Lake Store and links to Azure Storage (blobs) accounts.</span><span class="sxs-lookup"><span data-stu-id="94a44-199">After you have created an Analytics account, you can add additional Data Lake Store and links to Azure Storage (blobs) accounts.</span></span>

### <a name="link-to-an-azure-storage-account-from-a-data-lake-analytics-account"></a><span data-ttu-id="94a44-200">Link to an Azure Storage account from a Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="94a44-200">Link to an Azure Storage account from a Data Lake Analytics account</span></span>
<span data-ttu-id="94a44-201">You can create links to Azure Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="94a44-201">You can create links to Azure Storage accounts.</span></span>

    AddStorageAccountParameters addParams = new AddStorageAccountParameters(<storage key value>);            
    adlaClient.StorageAccounts.Add(_resourceGroupName, _adlaAccountName, "<Azure Storage Account Name>", addParams);

### <a name="list-data-lake-store-data-sources"></a><span data-ttu-id="94a44-202">List Data Lake Store data sources</span><span class="sxs-lookup"><span data-stu-id="94a44-202">List Data Lake Store data sources</span></span>
<span data-ttu-id="94a44-203">The following code lists the Data Lake Store accounts and the Azure Storage accounts used for a specified Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="94a44-203">The following code lists the Data Lake Store accounts and the Azure Storage accounts used for a specified Data Lake Analytics account.</span></span>

    var sAccnts = adlaClient.StorageAccounts.ListByAccount(_resourceGroupName, acctName);

    if (sAccnts != null)
    {
        Console.WriteLine("Azure Storage accounts:");
        foreach (var a in sAccnts)
        {
            Console.WriteLine($"\t{a.Name}");
        }
    }

    var stores = adlsClient.Account.List();
    if (stores != null)
    {
        Console.WriteLine("\nData stores:");
        foreach (var s in stores)
        {
            Console.WriteLine($"\t{s.Name}");
        }
    }

### <a name="upload-and-download-folders-and-files"></a><span data-ttu-id="94a44-204">Upload and download folders and files</span><span class="sxs-lookup"><span data-stu-id="94a44-204">Upload and download folders and files</span></span>
<span data-ttu-id="94a44-205">You can use the Data Lake Store file system client management object to upload and download individual files or folders from Azure to your local computer, using the following methods:</span><span class="sxs-lookup"><span data-stu-id="94a44-205">You can use the Data Lake Store file system client management object to upload and download individual files or folders from Azure to your local computer, using the following methods:</span></span>

- <span data-ttu-id="94a44-206">UploadFolder</span><span class="sxs-lookup"><span data-stu-id="94a44-206">UploadFolder</span></span>
- <span data-ttu-id="94a44-207">UploadFile</span><span class="sxs-lookup"><span data-stu-id="94a44-207">UploadFile</span></span>
- <span data-ttu-id="94a44-208">DownloadFolder</span><span class="sxs-lookup"><span data-stu-id="94a44-208">DownloadFolder</span></span>
- <span data-ttu-id="94a44-209">DownloadFile</span><span class="sxs-lookup"><span data-stu-id="94a44-209">DownloadFile</span></span>

<span data-ttu-id="94a44-210">The first parameter for these methods is the name of the Data Lake Store Account, followed by parameters for the source path and the destination path.</span><span class="sxs-lookup"><span data-stu-id="94a44-210">The first parameter for these methods is the name of the Data Lake Store Account, followed by parameters for the source path and the destination path.</span></span>

<span data-ttu-id="94a44-211">The following example shows how to download a folder in the Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="94a44-211">The following example shows how to download a folder in the Data Lake Store.</span></span>


    try
    {
        if (adlsFileSystemClient.FileSystem.PathExists(account, sourcePath))
        {
            adlsFileSystemClient.FileSystem.DownloadFolder(account, sourcePath, destinationPath);
        }
        else
        {
            Console.WriteLine("Path does not exist");
        }
    }
    catch (IOException ioex)
    {
        Console.WriteLine(ioex.Message);
    }


### <a name="create-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="94a44-212">Create a file in a Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="94a44-212">Create a file in a Data Lake Store account</span></span>
<span data-ttu-id="94a44-213">You can use .NET Framework IO operations to create content for a file in a Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="94a44-213">You can use .NET Framework IO operations to create content for a file in a Data Lake Store.</span></span> <span data-ttu-id="94a44-214">The following code writes the first four values of 100 random byte arrays to .csv file.</span><span class="sxs-lookup"><span data-stu-id="94a44-214">The following code writes the first four values of 100 random byte arrays to .csv file.</span></span>

    MemoryStream azMem = new MemoryStream();
    StreamWriter sw = new StreamWriter(azMem, UTF8Encoding.UTF8);

    for (int i = 0; i < 100; i++)
    {
        byte[] gA = Guid.NewGuid().ToByteArray();
        string dataLine = string.Format($"{gA[0].ToString()},{gA[1].ToString()},{gA[2].ToString()},{gA[3].ToString()},{gA[4].ToString()}");
        sw.WriteLine(dataLine);
    }
    sw.Flush();
    azMem.Position = 0;

    adlsFileSystemClient.FileSystem.Create(adlsAccoutName, "/Samples/Output/randombytes.csv", azMem);

    sw.Dispose();
    azMem.Dispose();

### <a name="list-blob-containers-of-an-azure-storage-account"></a><span data-ttu-id="94a44-215">List blob containers of an Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="94a44-215">List blob containers of an Azure Storage account</span></span>
<span data-ttu-id="94a44-216">The following code lists the containers for a specified Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="94a44-216">The following code lists the containers for a specified Azure Storage account.</span></span>

    string ADLAName = "<specify Data Lake Analytics account name>";
    string azStorageName = "<specify Azure Storage account name>";
    var containers = adlaClient.StorageAccounts.ListStorageContainers(_resourceGroupName, ADLAName, azStorageName);
    foreach (var c in containers)
    {
       Console.WriteLine(c.Name);
    }

### <a name="verify-azure-storage-account-paths"></a><span data-ttu-id="94a44-217">Verify Azure Storage account paths</span><span class="sxs-lookup"><span data-stu-id="94a44-217">Verify Azure Storage account paths</span></span>
<span data-ttu-id="94a44-218">The following code checks if an Azure Storage account (storageAccntName) exists in a Data Lake Analytics account (analyticsAccountName), and if a container (containerName) exists in the Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="94a44-218">The following code checks if an Azure Storage account (storageAccntName) exists in a Data Lake Analytics account (analyticsAccountName), and if a container (containerName) exists in the Azure Storage account.</span></span>

    bool accountExists = adlaClient.Account.StorageAccountExists(_resourceGroupName, analyticsAccountName, storageAccntName));
    bool containerExists = adlaClient.Account.StorageContainerExists(_resourceGroupName, analyticsAccountName, storageAccntName, containerName));

## <a name="manage-catalog-and-jobs"></a><span data-ttu-id="94a44-219">Manage catalog and jobs</span><span class="sxs-lookup"><span data-stu-id="94a44-219">Manage catalog and jobs</span></span>
<span data-ttu-id="94a44-220">The DataLakeAnalyticsCatalogManagementClient object provides methods for managing the SQL database provided for each Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="94a44-220">The DataLakeAnalyticsCatalogManagementClient object provides methods for managing the SQL database provided for each Azure Data Lake Store.</span></span> <span data-ttu-id="94a44-221">The DataLakeAnalyticsJobManagementClient provides methods to submit and manage jobs run on the database with U-SQL scripts.</span><span class="sxs-lookup"><span data-stu-id="94a44-221">The DataLakeAnalyticsJobManagementClient provides methods to submit and manage jobs run on the database with U-SQL scripts.</span></span>

### <a name="list-databases-and-schemas"></a><span data-ttu-id="94a44-222">List databases and schemas</span><span class="sxs-lookup"><span data-stu-id="94a44-222">List databases and schemas</span></span>
<span data-ttu-id="94a44-223">Among the several things, you can list, the most common are databases and their schema.</span><span class="sxs-lookup"><span data-stu-id="94a44-223">Among the several things, you can list, the most common are databases and their schema.</span></span> <span data-ttu-id="94a44-224">The following code obtains a collection of databases, and then enumerates the schema for each database.</span><span class="sxs-lookup"><span data-stu-id="94a44-224">The following code obtains a collection of databases, and then enumerates the schema for each database.</span></span>

    var databases = adlaCatalogClient.Catalog.ListDatabases(adlaAccountName);
    foreach (var db in databases)
    {
        Console.WriteLine($"Database: {db.Name}");
        Console.WriteLine(" - Schemas:");
        var schemas = adlaCatalogClient.Catalog.ListSchemas(dlaAccountName, db.Name);
        foreach (var schm in schemas)
        {
            Console.WriteLine($"\t{schm.Name}");
        }
    }

<span data-ttu-id="94a44-225">Run on the default master database, the output of this example is as follows:</span><span class="sxs-lookup"><span data-stu-id="94a44-225">Run on the default master database, the output of this example is as follows:</span></span>

    Database: master
    - Schemas:
            dbo
            INFORMATION_SCHEMA
            sys
            usql

### <a name="list-table-columns"></a><span data-ttu-id="94a44-226">List table columns</span><span class="sxs-lookup"><span data-stu-id="94a44-226">List table columns</span></span>
<span data-ttu-id="94a44-227">The following code shows how to access the database with a Data Lake Analytics Catalog management client to list the columns in a specified table.</span><span class="sxs-lookup"><span data-stu-id="94a44-227">The following code shows how to access the database with a Data Lake Analytics Catalog management client to list the columns in a specified table.</span></span>

    var tbl = adlaCatalogClient.Catalog.GetTable(_adlaAnalyticsAccountTest, "master", "dbo", "MyTableName");
    IEnumerable<USqlTableColumn> columns = tbl.ColumnList;

    foreach (USqlTableColumn utc in columns)
    {
        string scriptPath = "/Samples/Scripts/SearchResults_Wikipedia_Script.txt";
        Stream scriptStrm = adlsFileSystemClient.FileSystem.Open(_adlsAccountName, scriptPath);
        string scriptTxt = string.Empty;
        using (StreamReader sr = new StreamReader(scriptStrm))
        {
            scriptTxt = sr.ReadToEnd();
        }

        var jobName = "SR_Wikipedia";
        var jobId = Guid.NewGuid();
        var properties = new USqlJobProperties(scriptTxt);
        var parameters = new JobInformation(jobName, JobType.USql, properties, priority: 1, degreeOfParallelism: 1, jobId: jobId);
        var jobInfo = adlaJobClient.Job.Create(_adlaAnalyticsAccountTest, jobId, parameters);
        Console.WriteLine($"Job {jobName} submitted.");

    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.Message);
    }


### <a name="list-failed-jobs"></a><span data-ttu-id="94a44-228">List failed jobs</span><span class="sxs-lookup"><span data-stu-id="94a44-228">List failed jobs</span></span>
<span data-ttu-id="94a44-229">The following code lists information about jobs that failed.</span><span class="sxs-lookup"><span data-stu-id="94a44-229">The following code lists information about jobs that failed.</span></span>

    var jobs = adlaJobClient.Job.List(adlaClient,
        new ODataQuery<JobInformation> { Filter = "result eq 'Failed'" });
    foreach (var j in jobs)
    {
        Console.WriteLine($"{j.Name}\t{j.JobId}\t{j.Type}\t{j.StartTime}\t{j.EndTime}");
    }


## <a name="see-also"></a><span data-ttu-id="94a44-230">See also</span><span class="sxs-lookup"><span data-stu-id="94a44-230">See also</span></span>
* [<span data-ttu-id="94a44-231">Overview of Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="94a44-231">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="94a44-232">Get started with Data Lake Analytics using Azure portal</span><span class="sxs-lookup"><span data-stu-id="94a44-232">Get started with Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="94a44-233">Manage Azure Data Lake Analytics using Azure portal</span><span class="sxs-lookup"><span data-stu-id="94a44-233">Manage Azure Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="94a44-234">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span><span class="sxs-lookup"><span data-stu-id="94a44-234">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
