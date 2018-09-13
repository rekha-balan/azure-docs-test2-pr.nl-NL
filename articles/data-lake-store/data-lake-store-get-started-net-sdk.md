---
title: Use the .NET SDK to develop applications in Azure Data Lake Store | Microsoft Docs
description: Use Azure Data Lake Store .NET SDK to create a Data Lake Store account and perform basic operations in the Data Lake Store
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ea57d5a9-2929-4473-9d30-08227912aba7
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/07/2017
ms.author: nitinme
ms.openlocfilehash: eaa1df0a7efe4431b27c78f90ae6e0198b9340c5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564502"
---
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a><span data-ttu-id="88708-103">Get started with Azure Data Lake Store using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="88708-103">Get started with Azure Data Lake Store using .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI](data-lake-store-get-started-cli.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="88708-113">Learn how to use the [Azure Data Lake Store .NET SDK](https://msdn.microsoft.com/library/mt581387.aspx) to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="88708-113">Learn how to use the [Azure Data Lake Store .NET SDK](https://msdn.microsoft.com/library/mt581387.aspx) to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88708-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="88708-114">Prerequisites</span></span>
* <span data-ttu-id="88708-115">**Visual Studio 2013, 2015, or 2017**.</span><span class="sxs-lookup"><span data-stu-id="88708-115">**Visual Studio 2013, 2015, or 2017**.</span></span> <span data-ttu-id="88708-116">The instructions below use Visual Studio 2015 Update 2.</span><span class="sxs-lookup"><span data-stu-id="88708-116">The instructions below use Visual Studio 2015 Update 2.</span></span>

* <span data-ttu-id="88708-117">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="88708-117">**An Azure subscription**.</span></span> <span data-ttu-id="88708-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88708-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="88708-119">**Azure Data Lake Store account**.</span><span class="sxs-lookup"><span data-stu-id="88708-119">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="88708-120">For instructions on how to create an account, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="88708-120">For instructions on how to create an account, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

* <span data-ttu-id="88708-121">**Create an Azure Active Directory Application**.</span><span class="sxs-lookup"><span data-stu-id="88708-121">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="88708-122">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88708-122">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="88708-123">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span><span class="sxs-lookup"><span data-stu-id="88708-123">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="88708-124">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="88708-124">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-a-net-application"></a><span data-ttu-id="88708-125">Create a .NET application</span><span class="sxs-lookup"><span data-stu-id="88708-125">Create a .NET application</span></span>
1. <span data-ttu-id="88708-126">Open Visual Studio and create a console application.</span><span class="sxs-lookup"><span data-stu-id="88708-126">Open Visual Studio and create a console application.</span></span>
2. <span data-ttu-id="88708-127">From the **File** menu, click **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="88708-127">From the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="88708-128">From **New Project**, type or select the following values:</span><span class="sxs-lookup"><span data-stu-id="88708-128">From **New Project**, type or select the following values:</span></span>

   | <span data-ttu-id="88708-129">Property</span><span class="sxs-lookup"><span data-stu-id="88708-129">Property</span></span> | <span data-ttu-id="88708-130">Value</span><span class="sxs-lookup"><span data-stu-id="88708-130">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="88708-131">Category</span><span class="sxs-lookup"><span data-stu-id="88708-131">Category</span></span> |<span data-ttu-id="88708-132">Templates/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="88708-132">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="88708-133">Template</span><span class="sxs-lookup"><span data-stu-id="88708-133">Template</span></span> |<span data-ttu-id="88708-134">Console Application</span><span class="sxs-lookup"><span data-stu-id="88708-134">Console Application</span></span> |
   | <span data-ttu-id="88708-135">Name</span><span class="sxs-lookup"><span data-stu-id="88708-135">Name</span></span> |<span data-ttu-id="88708-136">CreateADLApplication</span><span class="sxs-lookup"><span data-stu-id="88708-136">CreateADLApplication</span></span> |
4. <span data-ttu-id="88708-137">Click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="88708-137">Click **OK** to create the project.</span></span>
5. <span data-ttu-id="88708-138">Add the Nuget packages to your project.</span><span class="sxs-lookup"><span data-stu-id="88708-138">Add the Nuget packages to your project.</span></span>

   1. <span data-ttu-id="88708-139">Right-click the project name in the Solution Explorer and click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="88708-139">Right-click the project name in the Solution Explorer and click **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="88708-140">In the **Nuget Package Manager** tab, make sure that **Package source** is set to **nuget.org** and that **Include prerelease** check box is selected.</span><span class="sxs-lookup"><span data-stu-id="88708-140">In the **Nuget Package Manager** tab, make sure that **Package source** is set to **nuget.org** and that **Include prerelease** check box is selected.</span></span>
   3. <span data-ttu-id="88708-141">Search for and install the following NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="88708-141">Search for and install the following NuGet packages:</span></span>

      * <span data-ttu-id="88708-142">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v1.0.4.</span><span class="sxs-lookup"><span data-stu-id="88708-142">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v1.0.4.</span></span>
      * <span data-ttu-id="88708-143">`Microsoft.Azure.Management.DataLake.StoreUploader` - This tutorial uses v1.0.1-preview.</span><span class="sxs-lookup"><span data-stu-id="88708-143">`Microsoft.Azure.Management.DataLake.StoreUploader` - This tutorial uses v1.0.1-preview.</span></span>
      * <span data-ttu-id="88708-144">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.11.</span><span class="sxs-lookup"><span data-stu-id="88708-144">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.11.</span></span>

        <span data-ttu-id="88708-145">![Add a Nuget source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-get-started-net-sdk/ADL.Install.Nuget.Package.png "Create a new Azure Data Lake account")</span><span class="sxs-lookup"><span data-stu-id="88708-145">![Add a Nuget source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-get-started-net-sdk/ADL.Install.Nuget.Package.png "Create a new Azure Data Lake account")</span></span>
   4. <span data-ttu-id="88708-146">Close the **Nuget Package Manager**.</span><span class="sxs-lookup"><span data-stu-id="88708-146">Close the **Nuget Package Manager**.</span></span>
6. <span data-ttu-id="88708-147">Open **Program.cs**, delete the existing code, and then include the following statements to add references to namespaces.</span><span class="sxs-lookup"><span data-stu-id="88708-147">Open **Program.cs**, delete the existing code, and then include the following statements to add references to namespaces.</span></span>

        using System;
        using System.IO;
    <span data-ttu-id="88708-148">using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates      using System.Threading;</span><span class="sxs-lookup"><span data-stu-id="88708-148">using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates      using System.Threading;</span></span>

        using Microsoft.Azure.Management.DataLake.Store;
    <span data-ttu-id="88708-149">using Microsoft.Azure.Management.DataLake.Store.Models;  using Microsoft.Azure.Management.DataLake.StoreUploader;  using Microsoft.IdentityModel.Clients.ActiveDirectory;  using Microsoft.Rest.Azure.Authentication;</span><span class="sxs-lookup"><span data-stu-id="88708-149">using Microsoft.Azure.Management.DataLake.Store.Models;  using Microsoft.Azure.Management.DataLake.StoreUploader;  using Microsoft.IdentityModel.Clients.ActiveDirectory;  using Microsoft.Rest.Azure.Authentication;</span></span>

7. <span data-ttu-id="88708-150">Declare the variables as shown below, and provide the values for Data Lake Store name and the resource group name that already exist.</span><span class="sxs-lookup"><span data-stu-id="88708-150">Declare the variables as shown below, and provide the values for Data Lake Store name and the resource group name that already exist.</span></span> <span data-ttu-id="88708-151">Also, make sure the local path and file name you provide here must exist on the computer.</span><span class="sxs-lookup"><span data-stu-id="88708-151">Also, make sure the local path and file name you provide here must exist on the computer.</span></span> <span data-ttu-id="88708-152">Add the following code snippet after the namespace declarations.</span><span class="sxs-lookup"><span data-stu-id="88708-152">Add the following code snippet after the namespace declarations.</span></span>

        namespace SdkSample
        {
            class Program
            {
                private static DataLakeStoreAccountManagementClient _adlsClient;
                private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;

                private static string _adlsAccountName;
                private static string _resourceGroupName;
                private static string _location;
                private static string _subId;

                private static void Main(string[] args)
                {
                    _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; // TODO: Replace this value with the name of your existing Data Lake Store account.
                    _resourceGroupName = "<RESOURCE-GROUP-NAME>"; // TODO: Replace this value with the name of the resource group containing your Data Lake Store account.
                    _location = "East US 2";
                    _subId = "<SUBSCRIPTION-ID>";

                    string localFolderPath = @"C:\local_path\"; // TODO: Make sure this exists and can be overwritten.
                    string localFilePath = Path.Combine(localFolderPath, "file.txt"); // TODO: Make sure this exists and can be overwritten.
                    string remoteFolderPath = "/data_lake_path/";
                    string remoteFilePath = Path.Combine(remoteFolderPath, "file.txt");
                }
            }
        }

<span data-ttu-id="88708-153">In the remaining sections of the article, you can see how to use the available .NET methods to perform operations such as authentication, file upload, etc.</span><span class="sxs-lookup"><span data-stu-id="88708-153">In the remaining sections of the article, you can see how to use the available .NET methods to perform operations such as authentication, file upload, etc.</span></span>

## <a name="authentication"></a><span data-ttu-id="88708-154">Authentication</span><span class="sxs-lookup"><span data-stu-id="88708-154">Authentication</span></span>

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a><span data-ttu-id="88708-155">If you are using end-user authentication (recommended for this tutorial)</span><span class="sxs-lookup"><span data-stu-id="88708-155">If you are using end-user authentication (recommended for this tutorial)</span></span>

<span data-ttu-id="88708-156">Use this with an existing Azure AD native application to authenticate your application **interactively**, which means you will be prompted to enter your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="88708-156">Use this with an existing Azure AD native application to authenticate your application **interactively**, which means you will be prompted to enter your Azure credentials.</span></span>

<span data-ttu-id="88708-157">For ease of use, the snippet below uses default values for client ID and redirect URI that will work with any Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="88708-157">For ease of use, the snippet below uses default values for client ID and redirect URI that will work with any Azure subscription.</span></span> <span data-ttu-id="88708-158">To help you complete this tutorial faster, we recommend you use this approach.</span><span class="sxs-lookup"><span data-stu-id="88708-158">To help you complete this tutorial faster, we recommend you use this approach.</span></span> <span data-ttu-id="88708-159">In the snippet below, just provide the value for your tenant ID.</span><span class="sxs-lookup"><span data-stu-id="88708-159">In the snippet below, just provide the value for your tenant ID.</span></span> <span data-ttu-id="88708-160">You can retrieve it using the instructions provided at [Create an Active Directory Application](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="88708-160">You can retrieve it using the instructions provided at [Create an Active Directory Application](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

    // User login via interactive popup
    // Use the client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with the user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

<span data-ttu-id="88708-161">Couple of things to know about this snippet above.</span><span class="sxs-lookup"><span data-stu-id="88708-161">Couple of things to know about this snippet above.</span></span>

* <span data-ttu-id="88708-162">To help you complete the tutorial faster, this snippet uses an an Azure AD domain and client ID that is available by default for all Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="88708-162">To help you complete the tutorial faster, this snippet uses an an Azure AD domain and client ID that is available by default for all Azure subscriptions.</span></span> <span data-ttu-id="88708-163">So, you can **use this snippet as-is in your application**.</span><span class="sxs-lookup"><span data-stu-id="88708-163">So, you can **use this snippet as-is in your application**.</span></span>
* <span data-ttu-id="88708-164">However, if you do want to use your own Azure AD domain and application client ID, you must create an Azure AD native application and then use the Azure AD tenant ID, client ID, and redirect URI for the application you created.</span><span class="sxs-lookup"><span data-stu-id="88708-164">However, if you do want to use your own Azure AD domain and application client ID, you must create an Azure AD native application and then use the Azure AD tenant ID, client ID, and redirect URI for the application you created.</span></span> <span data-ttu-id="88708-165">See [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="88708-165">See [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) for instructions.</span></span>

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a><span data-ttu-id="88708-166">If you are using service-to-service authentication with client secret</span><span class="sxs-lookup"><span data-stu-id="88708-166">If you are using service-to-service authentication with client secret</span></span>
<span data-ttu-id="88708-167">The following snippet can be used to authenticate your application **non-interactively**, using the client secret / key for an application / service principal.</span><span class="sxs-lookup"><span data-stu-id="88708-167">The following snippet can be used to authenticate your application **non-interactively**, using the client secret / key for an application / service principal.</span></span> <span data-ttu-id="88708-168">Use this with an existing Azure AD "Web App" Application.</span><span class="sxs-lookup"><span data-stu-id="88708-168">Use this with an existing Azure AD "Web App" Application.</span></span> <span data-ttu-id="88708-169">For instructions on how to create the Azure AD web application and how to retrieve the client ID and client secret required in the snippet below, see [Create an Active Directory Application for service-to-service authentication with Data Lake Store](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="88708-169">For instructions on how to create the Azure AD web application and how to retrieve the client ID and client secret required in the snippet below, see [Create an Active Directory Application for service-to-service authentication with Data Lake Store](data-lake-store-authenticate-using-active-directory.md).</span></span>

    // Service principal / appplication authentication with client secret / key
    // Use the client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a><span data-ttu-id="88708-170">If you are using service-to-service authentication with certificate</span><span class="sxs-lookup"><span data-stu-id="88708-170">If you are using service-to-service authentication with certificate</span></span>

<span data-ttu-id="88708-171">As a third option, the following snippet can be used to authenticate your application **non-interactively**, using the certificate for an Azure Active Directory application / service principal.</span><span class="sxs-lookup"><span data-stu-id="88708-171">As a third option, the following snippet can be used to authenticate your application **non-interactively**, using the certificate for an Azure Active Directory application / service principal.</span></span> <span data-ttu-id="88708-172">Use this with an existing [Azure AD Application with certificates](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="88708-172">Use this with an existing [Azure AD Application with certificates](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    // Service principal / application authentication with certificate
    // Use the client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a><span data-ttu-id="88708-173">Create client objects</span><span class="sxs-lookup"><span data-stu-id="88708-173">Create client objects</span></span>
<span data-ttu-id="88708-174">The following snippet creates the Data Lake Store account and filesystem client objects, which are used to issue requests to the service.</span><span class="sxs-lookup"><span data-stu-id="88708-174">The following snippet creates the Data Lake Store account and filesystem client objects, which are used to issue requests to the service.</span></span>

    // Create client objects and set the subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a><span data-ttu-id="88708-175">List all Data Lake Store accounts within a subscription</span><span class="sxs-lookup"><span data-stu-id="88708-175">List all Data Lake Store accounts within a subscription</span></span>
<span data-ttu-id="88708-176">The following snippet lists all Data Lake Store accounts within a given Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="88708-176">The following snippet lists all Data Lake Store accounts within a given Azure subscription.</span></span>

    // List all ADLS accounts within the subscription
    public static async Task<List<DataLakeStoreAccount>> ListAdlStoreAccounts()
    {
        var response = await _adlsClient.Account.ListAsync();
        var accounts = new List<DataLakeStoreAccount>(response);

        while (response.NextPageLink != null)
        {
            response = _adlsClient.Account.ListNext(response.NextPageLink);
            accounts.AddRange(response);
        }

        return accounts;
    }

## <a name="create-a-directory"></a><span data-ttu-id="88708-177">Create a directory</span><span class="sxs-lookup"><span data-stu-id="88708-177">Create a directory</span></span>
<span data-ttu-id="88708-178">The following snippet shows a `CreateDirectory` method that you can use to create a directory within a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="88708-178">The following snippet shows a `CreateDirectory` method that you can use to create a directory within a Data Lake Store account.</span></span>

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a><span data-ttu-id="88708-179">Upload a file</span><span class="sxs-lookup"><span data-stu-id="88708-179">Upload a file</span></span>
<span data-ttu-id="88708-180">The following snippet shows an `UploadFile` method that you can use to upload files to a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="88708-180">The following snippet shows an `UploadFile` method that you can use to upload files to a Data Lake Store account.</span></span>

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        var parameters = new UploadParameters(srcFilePath, destFilePath, _adlsAccountName, isOverwrite: force);
        var frontend = new DataLakeStoreFrontEndAdapter(_adlsAccountName, _adlsFileSystemClient);
        var uploader = new DataLakeStoreUploader(parameters, frontend);
        uploader.Execute();
    }

<span data-ttu-id="88708-181">`DataLakeStoreUploader` supports recursive upload and download between a local file path and a Data Lake Store file path.</span><span class="sxs-lookup"><span data-stu-id="88708-181">`DataLakeStoreUploader` supports recursive upload and download between a local file path and a Data Lake Store file path.</span></span>    

## <a name="get-file-or-directory-info"></a><span data-ttu-id="88708-182">Get file or directory info</span><span class="sxs-lookup"><span data-stu-id="88708-182">Get file or directory info</span></span>
<span data-ttu-id="88708-183">The following snippet shows a `GetItemInfo` method that you can use to retrieve information about a file or directory available in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="88708-183">The following snippet shows a `GetItemInfo` method that you can use to retrieve information about a file or directory available in Data Lake Store.</span></span>

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a><span data-ttu-id="88708-184">List file or directories</span><span class="sxs-lookup"><span data-stu-id="88708-184">List file or directories</span></span>
<span data-ttu-id="88708-185">The following snippet shows a `ListItem` method that can use to list the file and directories in a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="88708-185">The following snippet shows a `ListItem` method that can use to list the file and directories in a Data Lake Store account.</span></span>

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a><span data-ttu-id="88708-186">Concatenate files</span><span class="sxs-lookup"><span data-stu-id="88708-186">Concatenate files</span></span>
<span data-ttu-id="88708-187">The following snippet shows a `ConcatenateFiles` method that you use to concatenate files.</span><span class="sxs-lookup"><span data-stu-id="88708-187">The following snippet shows a `ConcatenateFiles` method that you use to concatenate files.</span></span>

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-to-a-file"></a><span data-ttu-id="88708-188">Append to a file</span><span class="sxs-lookup"><span data-stu-id="88708-188">Append to a file</span></span>
<span data-ttu-id="88708-189">The following snippet shows a `AppendToFile` method that you use append data to a file already stored in a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="88708-189">The following snippet shows a `AppendToFile` method that you use append data to a file already stored in a Data Lake Store account.</span></span>

    // Append to file
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a><span data-ttu-id="88708-190">Download a file</span><span class="sxs-lookup"><span data-stu-id="88708-190">Download a file</span></span>
<span data-ttu-id="88708-191">The following snippet shows a `DownloadFile` method that you use to download a file from a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="88708-191">The following snippet shows a `DownloadFile` method that you use to download a file from a Data Lake Store account.</span></span>

    // Download file
    public static async Task DownloadFile(string srcPath, string destPath)
    {
        using (var stream = await _adlsFileSystemClient.FileSystem.OpenAsync(_adlsAccountName, srcPath))
        using (var fileStream = new FileStream(destPath, FileMode.Create))
        {
            await stream.CopyToAsync(fileStream);
        }
    }

## <a name="next-steps"></a><span data-ttu-id="88708-192">Next steps</span><span class="sxs-lookup"><span data-stu-id="88708-192">Next steps</span></span>
* [<span data-ttu-id="88708-193">Secure data in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="88708-193">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="88708-194">Use Azure Data Lake Analytics with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="88708-194">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="88708-195">Use Azure HDInsight with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="88708-195">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="88708-196">Data Lake Store .NET SDK Reference</span><span class="sxs-lookup"><span data-stu-id="88708-196">Data Lake Store .NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt581387.aspx)
* [<span data-ttu-id="88708-197">Data Lake Store REST Reference</span><span class="sxs-lookup"><span data-stu-id="88708-197">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)

