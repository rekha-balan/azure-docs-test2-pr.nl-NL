---
title: Use the Python SDK to get started with Azure Data Lake Store | Microsoft Docs
description: Learn how to use Python SDK to work with Data Lake Store accounts and the file system.
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 75f6de6f-6fd8-48f4-8707-cb27d22d27a6
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/03/2017
ms.author: nitinme
ms.openlocfilehash: 9e4efc9de7979c98fcb4afbe530c73e9013326c3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563766"
---
# <a name="get-started-with-azure-data-lake-store-using-python"></a><span data-ttu-id="8b80d-103">Get started with Azure Data Lake Store using Python</span><span class="sxs-lookup"><span data-stu-id="8b80d-103">Get started with Azure Data Lake Store using Python</span></span>

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

<span data-ttu-id="8b80d-113">Learn how to use the Python SDK for Azure and Azure Data Lake Store to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8b80d-113">Learn how to use the Python SDK for Azure and Azure Data Lake Store to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b80d-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8b80d-114">Prerequisites</span></span>

* <span data-ttu-id="8b80d-115">**Python**.</span><span class="sxs-lookup"><span data-stu-id="8b80d-115">**Python**.</span></span> <span data-ttu-id="8b80d-116">You can download Python from [here](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8b80d-116">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="8b80d-117">This article uses Python 3.5.2.</span><span class="sxs-lookup"><span data-stu-id="8b80d-117">This article uses Python 3.5.2.</span></span>

* <span data-ttu-id="8b80d-118">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="8b80d-118">**An Azure subscription**.</span></span> <span data-ttu-id="8b80d-119">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8b80d-119">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="8b80d-120">**Create an Azure Active Directory Application**.</span><span class="sxs-lookup"><span data-stu-id="8b80d-120">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="8b80d-121">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b80d-121">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="8b80d-122">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span><span class="sxs-lookup"><span data-stu-id="8b80d-122">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="8b80d-123">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="8b80d-123">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="install-the-modules"></a><span data-ttu-id="8b80d-124">Install the modules</span><span class="sxs-lookup"><span data-stu-id="8b80d-124">Install the modules</span></span>

<span data-ttu-id="8b80d-125">To work with Data Lake Store using Python, you need to install three modules.</span><span class="sxs-lookup"><span data-stu-id="8b80d-125">To work with Data Lake Store using Python, you need to install three modules.</span></span>

* <span data-ttu-id="8b80d-126">The `azure-mgmt-resource` module.</span><span class="sxs-lookup"><span data-stu-id="8b80d-126">The `azure-mgmt-resource` module.</span></span> <span data-ttu-id="8b80d-127">This includes Azure modules for Active Directory, etc..</span><span class="sxs-lookup"><span data-stu-id="8b80d-127">This includes Azure modules for Active Directory, etc..</span></span>
* <span data-ttu-id="8b80d-128">The `azure-mgmt-datalake-store` module.</span><span class="sxs-lookup"><span data-stu-id="8b80d-128">The `azure-mgmt-datalake-store` module.</span></span> <span data-ttu-id="8b80d-129">This includes the Azure Data Lake Store account management operations.</span><span class="sxs-lookup"><span data-stu-id="8b80d-129">This includes the Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="8b80d-130">For more information on this module, see [Azure Data Lake Store Management module reference](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span><span class="sxs-lookup"><span data-stu-id="8b80d-130">For more information on this module, see [Azure Data Lake Store Management module reference](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span></span>
* <span data-ttu-id="8b80d-131">The `azure-datalake-store` module.</span><span class="sxs-lookup"><span data-stu-id="8b80d-131">The `azure-datalake-store` module.</span></span> <span data-ttu-id="8b80d-132">This includes the Azure Data Lake Store filesystem operations.</span><span class="sxs-lookup"><span data-stu-id="8b80d-132">This includes the Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="8b80d-133">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span><span class="sxs-lookup"><span data-stu-id="8b80d-133">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="8b80d-134">Use the following commands to install the modules.</span><span class="sxs-lookup"><span data-stu-id="8b80d-134">Use the following commands to install the modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="8b80d-135">Create a new Python application</span><span class="sxs-lookup"><span data-stu-id="8b80d-135">Create a new Python application</span></span>

1. <span data-ttu-id="8b80d-136">In the IDE of your choice create a new Python application, for example, **mysample.py**.</span><span class="sxs-lookup"><span data-stu-id="8b80d-136">In the IDE of your choice create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="8b80d-137">Add the following lines to import the required modules</span><span class="sxs-lookup"><span data-stu-id="8b80d-137">Add the following lines to import the required modules</span></span>

    ```
    ## Use this only for Azure AD service-to-service authentication
    from azure.common.credentials import ServicePrincipalCredentials

    ## Use this only for Azure AD end-user authentication
    from azure.common.credentials import UserPassCredentials

    ## Use this only for Azure AD multi-factor authentication
    from msrestazure.azure_active_directory import AADTokenCredentials

    ## Required for Azure Data Lake Store account management
    from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
    from azure.mgmt.datalake.store.models import DataLakeStoreAccount

    ## Required for Azure Data Lake Store filesystem management
    from azure.datalake.store import core, lib, multithread

    # Common Azure imports
    from azure.mgmt.resource.resources import ResourceManagementClient
    from azure.mgmt.resource.resources.models import ResourceGroup

    ## Use these as needed for your application
    import logging, getpass, pprint, uuid, time
    ```

3. <span data-ttu-id="8b80d-138">Save changes to mysample.py.</span><span class="sxs-lookup"><span data-stu-id="8b80d-138">Save changes to mysample.py.</span></span>

## <a name="authentication"></a><span data-ttu-id="8b80d-139">Authentication</span><span class="sxs-lookup"><span data-stu-id="8b80d-139">Authentication</span></span>

<span data-ttu-id="8b80d-140">In this section, we talk about the different ways to authenticate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b80d-140">In this section, we talk about the different ways to authenticate with Azure AD.</span></span> <span data-ttu-id="8b80d-141">The options available are:</span><span class="sxs-lookup"><span data-stu-id="8b80d-141">The options available are:</span></span>

* <span data-ttu-id="8b80d-142">End-user authentication</span><span class="sxs-lookup"><span data-stu-id="8b80d-142">End-user authentication</span></span>
* <span data-ttu-id="8b80d-143">Service-to-service authentication</span><span class="sxs-lookup"><span data-stu-id="8b80d-143">Service-to-service authentication</span></span>
* <span data-ttu-id="8b80d-144">Multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="8b80d-144">Multi-factor authentication</span></span>

<span data-ttu-id="8b80d-145">You must use these authentication options for both account management and filesystem management modules.</span><span class="sxs-lookup"><span data-stu-id="8b80d-145">You must use these authentication options for both account management and filesystem management modules.</span></span>

### <a name="end-user-authentication-for-account-management"></a><span data-ttu-id="8b80d-146">End-user authentication for account management</span><span class="sxs-lookup"><span data-stu-id="8b80d-146">End-user authentication for account management</span></span>

<span data-ttu-id="8b80d-147">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span><span class="sxs-lookup"><span data-stu-id="8b80d-147">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="8b80d-148">You must provide username and password for an Azure AD user.</span><span class="sxs-lookup"><span data-stu-id="8b80d-148">You must provide username and password for an Azure AD user.</span></span> <span data-ttu-id="8b80d-149">Note that the user should not be configured for multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="8b80d-149">Note that the user should not be configured for multi-factor authentication.</span></span>

    user = input('Enter the user to authenticate with that has permission to subscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a><span data-ttu-id="8b80d-150">End-user authentication for filesystem operations</span><span class="sxs-lookup"><span data-stu-id="8b80d-150">End-user authentication for filesystem operations</span></span>

<span data-ttu-id="8b80d-151">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span><span class="sxs-lookup"><span data-stu-id="8b80d-151">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="8b80d-152">Use this with an existing Azure AD **native client** application.</span><span class="sxs-lookup"><span data-stu-id="8b80d-152">Use this with an existing Azure AD **native client** application.</span></span> <span data-ttu-id="8b80d-153">The Azure AD user you provide credentials for should not be configured for multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="8b80d-153">The Azure AD user you provide credentials for should not be configured for multi-factor authentication.</span></span>

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter the user to authenticate with that has permission to subscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a><span data-ttu-id="8b80d-154">Service-to-service authentication with client secret for account management</span><span class="sxs-lookup"><span data-stu-id="8b80d-154">Service-to-service authentication with client secret for account management</span></span>

<span data-ttu-id="8b80d-155">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span><span class="sxs-lookup"><span data-stu-id="8b80d-155">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="8b80d-156">The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal.</span><span class="sxs-lookup"><span data-stu-id="8b80d-156">The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal.</span></span> <span data-ttu-id="8b80d-157">Use this with an existing Azure AD "Web App" application.</span><span class="sxs-lookup"><span data-stu-id="8b80d-157">Use this with an existing Azure AD "Web App" application.</span></span>

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a><span data-ttu-id="8b80d-158">Service-to-service authentication with client secret for filesystem operations</span><span class="sxs-lookup"><span data-stu-id="8b80d-158">Service-to-service authentication with client secret for filesystem operations</span></span>

<span data-ttu-id="8b80d-159">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span><span class="sxs-lookup"><span data-stu-id="8b80d-159">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="8b80d-160">The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal.</span><span class="sxs-lookup"><span data-stu-id="8b80d-160">The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal.</span></span> <span data-ttu-id="8b80d-161">Use this with an existing Azure AD "Web App" application.</span><span class="sxs-lookup"><span data-stu-id="8b80d-161">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a><span data-ttu-id="8b80d-162">Multi-factor authentication for account management</span><span class="sxs-lookup"><span data-stu-id="8b80d-162">Multi-factor authentication for account management</span></span>

<span data-ttu-id="8b80d-163">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span><span class="sxs-lookup"><span data-stu-id="8b80d-163">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="8b80d-164">The following snippet can be used to authenticate your application using multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="8b80d-164">The following snippet can be used to authenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="8b80d-165">Use this with an existing Azure AD "Web App" application.</span><span class="sxs-lookup"><span data-stu-id="8b80d-165">Use this with an existing Azure AD "Web App" application.</span></span>

    authority_host_url = "https://login.microsoftonline.com"
    tenant = "FILL-IN-HERE"
    authority_url = authority_host_url + '/' + tenant
    client_id = 'FILL-IN-HERE'
    redirect = 'urn:ietf:wg:oauth:2.0:oob'
    RESOURCE = 'https://management.core.windows.net/'
    
    context = adal.AuthenticationContext(authority_url)
    code = context.acquire_user_code(RESOURCE, client_id)
    print(code['message'])
    mgmt_token = context.acquire_token_with_device_code(RESOURCE, code, client_id)
    credentials = AADTokenCredentials(mgmt_token, client_id)

### <a name="multi-factor-authentication-for-filesystem-management"></a><span data-ttu-id="8b80d-166">Multi-factor authentication for filesystem management</span><span class="sxs-lookup"><span data-stu-id="8b80d-166">Multi-factor authentication for filesystem management</span></span>

<span data-ttu-id="8b80d-167">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span><span class="sxs-lookup"><span data-stu-id="8b80d-167">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="8b80d-168">The following snippet can be used to authenticate your application using multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="8b80d-168">The following snippet can be used to authenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="8b80d-169">Use this with an existing Azure AD "Web App" application.</span><span class="sxs-lookup"><span data-stu-id="8b80d-169">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="8b80d-170">Create an Azure Resource Group</span><span class="sxs-lookup"><span data-stu-id="8b80d-170">Create an Azure Resource Group</span></span>

<span data-ttu-id="8b80d-171">Use the following code snippet to create an Azure Resource Group:</span><span class="sxs-lookup"><span data-stu-id="8b80d-171">Use the following code snippet to create an Azure Resource Group:</span></span>

    ## Declare variables
    subscriptionId= 'FILL-IN-HERE'
    resourceGroup = 'FILL-IN-HERE'
    location = 'eastus2'
    
    ## Create management client object
    resourceClient = ResourceManagementClient(
        credentials,
        subscriptionId
    )
    
    ## Create an Azure Resource Group
    resourceClient.resource_groups.create_or_update(
        resourceGroup,
        ResourceGroup(
            location=location
        )
    )

## <a name="create-clients-and-data-lake-store-account"></a><span data-ttu-id="8b80d-172">Create clients and Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="8b80d-172">Create clients and Data Lake Store account</span></span>

<span data-ttu-id="8b80d-173">The following snippet first creates the Data Lake Store account client.</span><span class="sxs-lookup"><span data-stu-id="8b80d-173">The following snippet first creates the Data Lake Store account client.</span></span> <span data-ttu-id="8b80d-174">It uses the client object to create a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="8b80d-174">It uses the client object to create a Data Lake Store account.</span></span> <span data-ttu-id="8b80d-175">Finally, the snippet creates a filesystem client object.</span><span class="sxs-lookup"><span data-stu-id="8b80d-175">Finally, the snippet creates a filesystem client object.</span></span>

    ## Declare variables
    subscriptionId = 'FILL-IN-HERE'
    adlsAccountName = 'FILL-IN-HERE'

    ## Create management client object
    adlsAcctClient = DataLakeStoreAccountManagementClient(credentials, subscriptionId)

    ## Create a Data Lake Store account
    adlsAcctResult = adlsAcctClient.account.create(
        resourceGroup,
        adlsAccountName,
        DataLakeStoreAccount(
            location=location
        )
    ).wait()

    ## Create a filesystem client object
    adlsFileSystemClient = core.AzureDLFileSystem(token, store_name=adlsAccountName)

## <a name="list-the-data-lake-store-accounts"></a><span data-ttu-id="8b80d-176">List the Data Lake Store accounts</span><span class="sxs-lookup"><span data-stu-id="8b80d-176">List the Data Lake Store accounts</span></span>

    ## List the existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a><span data-ttu-id="8b80d-177">Create a directory</span><span class="sxs-lookup"><span data-stu-id="8b80d-177">Create a directory</span></span>

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a><span data-ttu-id="8b80d-178">Upload a file</span><span class="sxs-lookup"><span data-stu-id="8b80d-178">Upload a file</span></span>


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a><span data-ttu-id="8b80d-179">Download a file</span><span class="sxs-lookup"><span data-stu-id="8b80d-179">Download a file</span></span>

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a><span data-ttu-id="8b80d-180">Delete a directory</span><span class="sxs-lookup"><span data-stu-id="8b80d-180">Delete a directory</span></span>

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a><span data-ttu-id="8b80d-181">See also</span><span class="sxs-lookup"><span data-stu-id="8b80d-181">See also</span></span>

- [<span data-ttu-id="8b80d-182">Secure data in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8b80d-182">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
- [<span data-ttu-id="8b80d-183">Use Azure Data Lake Analytics with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8b80d-183">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [<span data-ttu-id="8b80d-184">Use Azure HDInsight with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8b80d-184">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
- [<span data-ttu-id="8b80d-185">Data Lake Store .NET SDK Reference</span><span class="sxs-lookup"><span data-stu-id="8b80d-185">Data Lake Store .NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt581387.aspx)
- [<span data-ttu-id="8b80d-186">Data Lake Store REST Reference</span><span class="sxs-lookup"><span data-stu-id="8b80d-186">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
