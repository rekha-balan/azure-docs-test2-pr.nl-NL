---
title: 'End-user authentication: Python with Data Lake Store using Azure Active Directory | Microsoft Docs'
description: Learn how to achieve end-user authentication with Data Lake Store using Azure Active Directory with Python
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: conceptual
ms.date: 05/29/2018
ms.author: nitinme
ms.openlocfilehash: 60cdcc2c12272b48d61de0afcdd3c361f1795f37
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867212"
---
# <a name="end-user-authentication-with-data-lake-store-using-python"></a><span data-ttu-id="e6e7a-103">End-user authentication with Data Lake Store using Python</span><span class="sxs-lookup"><span data-stu-id="e6e7a-103">End-user authentication with Data Lake Store using Python</span></span>
> [!div class="op_single_selector"]
> * [Using Java](data-lake-store-end-user-authenticate-java-sdk.md)
> * [Using .NET SDK](data-lake-store-end-user-authenticate-net-sdk.md)
> * [Using Python](data-lake-store-end-user-authenticate-python.md)
> * [Using REST API](data-lake-store-end-user-authenticate-rest-api.md)
> 
> 

<span data-ttu-id="e6e7a-108">In this article, you learn about how to use the Python SDK to do end-user authentication with Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-108">In this article, you learn about how to use the Python SDK to do end-user authentication with Azure Data Lake Store.</span></span> <span data-ttu-id="e6e7a-109">End-user authentication can further be split into two categories:</span><span class="sxs-lookup"><span data-stu-id="e6e7a-109">End-user authentication can further be split into two categories:</span></span>

* <span data-ttu-id="e6e7a-110">End-user authentication without multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="e6e7a-110">End-user authentication without multi-factor authentication</span></span>
* <span data-ttu-id="e6e7a-111">End-user authentication with multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="e6e7a-111">End-user authentication with multi-factor authentication</span></span>

<span data-ttu-id="e6e7a-112">Both these options are discussed in this article.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-112">Both these options are discussed in this article.</span></span> <span data-ttu-id="e6e7a-113">For service-to-service authentication with Data Lake Store using Python, see [Service-to-service authentication with Data Lake Store using Python](data-lake-store-service-to-service-authenticate-python.md).</span><span class="sxs-lookup"><span data-stu-id="e6e7a-113">For service-to-service authentication with Data Lake Store using Python, see [Service-to-service authentication with Data Lake Store using Python](data-lake-store-service-to-service-authenticate-python.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6e7a-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e6e7a-114">Prerequisites</span></span>

* <span data-ttu-id="e6e7a-115">**Python**.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-115">**Python**.</span></span> <span data-ttu-id="e6e7a-116">You can download Python from [here](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e6e7a-116">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="e6e7a-117">This article uses Python 3.6.2.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-117">This article uses Python 3.6.2.</span></span>

* <span data-ttu-id="e6e7a-118">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-118">**An Azure subscription**.</span></span> <span data-ttu-id="e6e7a-119">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e6e7a-119">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="e6e7a-120">**Create an Azure Active Directory "Native" Application**.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-120">**Create an Azure Active Directory "Native" Application**.</span></span> <span data-ttu-id="e6e7a-121">You must have completed the steps in [End-user authentication with Data Lake Store using Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="e6e7a-121">You must have completed the steps in [End-user authentication with Data Lake Store using Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

## <a name="install-the-modules"></a><span data-ttu-id="e6e7a-122">Install the modules</span><span class="sxs-lookup"><span data-stu-id="e6e7a-122">Install the modules</span></span>

<span data-ttu-id="e6e7a-123">To work with Data Lake Store using Python, you need to install three modules.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-123">To work with Data Lake Store using Python, you need to install three modules.</span></span>

* <span data-ttu-id="e6e7a-124">The `azure-mgmt-resource` module, which includes Azure modules for Active Directory, etc.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-124">The `azure-mgmt-resource` module, which includes Azure modules for Active Directory, etc.</span></span>
* <span data-ttu-id="e6e7a-125">The `azure-mgmt-datalake-store` module, which includes the Azure Data Lake Store account management operations.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-125">The `azure-mgmt-datalake-store` module, which includes the Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="e6e7a-126">For more information on this module, see [Azure Data Lake Store Management module reference](https://docs.microsoft.com/python/api/azure.mgmt.datalake.store?view=azure-python).</span><span class="sxs-lookup"><span data-stu-id="e6e7a-126">For more information on this module, see [Azure Data Lake Store Management module reference](https://docs.microsoft.com/python/api/azure.mgmt.datalake.store?view=azure-python).</span></span>
* <span data-ttu-id="e6e7a-127">The `azure-datalake-store` module, which includes the Azure Data Lake Store filesystem operations.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-127">The `azure-datalake-store` module, which includes the Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="e6e7a-128">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span><span class="sxs-lookup"><span data-stu-id="e6e7a-128">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="e6e7a-129">Use the following commands to install the modules.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-129">Use the following commands to install the modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="e6e7a-130">Create a new Python application</span><span class="sxs-lookup"><span data-stu-id="e6e7a-130">Create a new Python application</span></span>

1. <span data-ttu-id="e6e7a-131">In the IDE of your choice, create a new Python application, for example, **mysample.py**.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-131">In the IDE of your choice, create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="e6e7a-132">Add the following snippet to import the required modules</span><span class="sxs-lookup"><span data-stu-id="e6e7a-132">Add the following snippet to import the required modules</span></span>

    ```
    ## Use this for Azure AD authentication
    from msrestazure.azure_active_directory import AADTokenCredentials

    ## Required for Azure Data Lake Store account management
    from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
    from azure.mgmt.datalake.store.models import DataLakeStoreAccount

    ## Required for Azure Data Lake Store filesystem management
    from azure.datalake.store import core, lib, multithread

    # Common Azure imports
    import adal
    from azure.mgmt.resource.resources import ResourceManagementClient
    from azure.mgmt.resource.resources.models import ResourceGroup

    ## Use these as needed for your application
    import logging, pprint, uuid, time
    ```

3. <span data-ttu-id="e6e7a-133">Save changes to mysample.py.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-133">Save changes to mysample.py.</span></span>

## <a name="end-user-authentication-with-multi-factor-authentication"></a><span data-ttu-id="e6e7a-134">End-user authentication with multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="e6e7a-134">End-user authentication with multi-factor authentication</span></span>

### <a name="for-account-management"></a><span data-ttu-id="e6e7a-135">For account management</span><span class="sxs-lookup"><span data-stu-id="e6e7a-135">For account management</span></span>

<span data-ttu-id="e6e7a-136">Use the following snippet to authenticate with Azure AD for account management operations on a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-136">Use the following snippet to authenticate with Azure AD for account management operations on a Data Lake Store account.</span></span> <span data-ttu-id="e6e7a-137">The following snippet can be used to authenticate your application using multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-137">The following snippet can be used to authenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="e6e7a-138">Provide the values below for  an existing Azure AD **native** application.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-138">Provide the values below for  an existing Azure AD **native** application.</span></span>

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
    armCreds = AADTokenCredentials(mgmt_token, client_id, resource = RESOURCE)

### <a name="for-filesystem-operations"></a><span data-ttu-id="e6e7a-139">For filesystem operations</span><span class="sxs-lookup"><span data-stu-id="e6e7a-139">For filesystem operations</span></span>

<span data-ttu-id="e6e7a-140">Use this to authenticate with Azure AD for filesystem operations on a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-140">Use this to authenticate with Azure AD for filesystem operations on a Data Lake Store account.</span></span> <span data-ttu-id="e6e7a-141">The following snippet can be used to authenticate your application using multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-141">The following snippet can be used to authenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="e6e7a-142">Provide the values below for  an existing Azure AD **native** application.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-142">Provide the values below for  an existing Azure AD **native** application.</span></span>

    adlCreds = lib.auth(tenant_id='FILL-IN-HERE', resource = 'https://datalake.azure.net/')

## <a name="end-user-authentication-without-multi-factor-authentication"></a><span data-ttu-id="e6e7a-143">End-user authentication without multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="e6e7a-143">End-user authentication without multi-factor authentication</span></span>

<span data-ttu-id="e6e7a-144">This is deprecated.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-144">This is deprecated.</span></span> <span data-ttu-id="e6e7a-145">For more information, see [Azure Authentication using Python SDK](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate?view=azure-python#mgmt-auth-token).</span><span class="sxs-lookup"><span data-stu-id="e6e7a-145">For more information, see [Azure Authentication using Python SDK](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate?view=azure-python#mgmt-auth-token).</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="e6e7a-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="e6e7a-146">Next steps</span></span>
<span data-ttu-id="e6e7a-147">In this article, you learned how to use end-user authentication to authenticate with Azure Data Lake Store using Python.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-147">In this article, you learned how to use end-user authentication to authenticate with Azure Data Lake Store using Python.</span></span> <span data-ttu-id="e6e7a-148">You can now look at the following articles that talk about how to use Python to work with Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e6e7a-148">You can now look at the following articles that talk about how to use Python to work with Azure Data Lake Store.</span></span>

* [<span data-ttu-id="e6e7a-149">Account management operations on Data Lake Store using Python</span><span class="sxs-lookup"><span data-stu-id="e6e7a-149">Account management operations on Data Lake Store using Python</span></span>](data-lake-store-get-started-python.md)
* [<span data-ttu-id="e6e7a-150">Data operations on Data Lake Store using Python</span><span class="sxs-lookup"><span data-stu-id="e6e7a-150">Data operations on Data Lake Store using Python</span></span>](data-lake-store-data-operations-python.md)

