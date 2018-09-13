---
title: 'Service-to-service authentication: Python with Data Lake Store using Azure Active Directory | Microsoft Docs'
description: Learn how to achieve service-to-service authentication with Data Lake Store using Azure Active Directory using Python
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
ms.openlocfilehash: f2ebd9228b9fa7861527dab20277ceb09f61b544
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857358"
---
# <a name="service-to-service-authentication-with-data-lake-store-using-python"></a><span data-ttu-id="b8157-103">Service-to-service authentication with Data Lake Store using Python</span><span class="sxs-lookup"><span data-stu-id="b8157-103">Service-to-service authentication with Data Lake Store using Python</span></span>
> [!div class="op_single_selector"]
> * [Using Java](data-lake-store-service-to-service-authenticate-java.md)
> * [Using .NET SDK](data-lake-store-service-to-service-authenticate-net-sdk.md)
> * [Using Python](data-lake-store-service-to-service-authenticate-python.md)
> * [Using REST API](data-lake-store-service-to-service-authenticate-rest-api.md)
> 
>  

<span data-ttu-id="b8157-108">In this article, you learn about how to use the Python SDK to do service-to-service authentication with Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b8157-108">In this article, you learn about how to use the Python SDK to do service-to-service authentication with Azure Data Lake Store.</span></span> <span data-ttu-id="b8157-109">For end-user authentication with Data Lake Store using Python, see [End-user authentication with Data Lake Store using Python](data-lake-store-end-user-authenticate-python.md).</span><span class="sxs-lookup"><span data-stu-id="b8157-109">For end-user authentication with Data Lake Store using Python, see [End-user authentication with Data Lake Store using Python](data-lake-store-end-user-authenticate-python.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b8157-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b8157-110">Prerequisites</span></span>

* <span data-ttu-id="b8157-111">**Python**.</span><span class="sxs-lookup"><span data-stu-id="b8157-111">**Python**.</span></span> <span data-ttu-id="b8157-112">You can download Python from [here](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="b8157-112">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="b8157-113">This article uses Python 3.6.2.</span><span class="sxs-lookup"><span data-stu-id="b8157-113">This article uses Python 3.6.2.</span></span>

* <span data-ttu-id="b8157-114">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="b8157-114">**An Azure subscription**.</span></span> <span data-ttu-id="b8157-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b8157-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="b8157-116">**Create an Azure Active Directory "Web" Application**.</span><span class="sxs-lookup"><span data-stu-id="b8157-116">**Create an Azure Active Directory "Web" Application**.</span></span> <span data-ttu-id="b8157-117">You must have completed the steps in [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-service-to-service-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="b8157-117">You must have completed the steps in [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-service-to-service-authenticate-using-active-directory.md).</span></span>

## <a name="install-the-modules"></a><span data-ttu-id="b8157-118">Install the modules</span><span class="sxs-lookup"><span data-stu-id="b8157-118">Install the modules</span></span>

<span data-ttu-id="b8157-119">To work with Data Lake Store using Python, you need to install three modules.</span><span class="sxs-lookup"><span data-stu-id="b8157-119">To work with Data Lake Store using Python, you need to install three modules.</span></span>

* <span data-ttu-id="b8157-120">The `azure-mgmt-resource` module, which includes Azure modules for Active Directory, etc.</span><span class="sxs-lookup"><span data-stu-id="b8157-120">The `azure-mgmt-resource` module, which includes Azure modules for Active Directory, etc.</span></span>
* <span data-ttu-id="b8157-121">The `azure-mgmt-datalake-store` module, which includes the Azure Data Lake Store account management operations.</span><span class="sxs-lookup"><span data-stu-id="b8157-121">The `azure-mgmt-datalake-store` module, which includes the Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="b8157-122">For more information on this module, see [Azure Data Lake Store Management module reference](https://docs.microsoft.com/python/api/azure.mgmt.datalake.store?view=azure-python).</span><span class="sxs-lookup"><span data-stu-id="b8157-122">For more information on this module, see [Azure Data Lake Store Management module reference](https://docs.microsoft.com/python/api/azure.mgmt.datalake.store?view=azure-python).</span></span>
* <span data-ttu-id="b8157-123">The `azure-datalake-store` module, which includes the Azure Data Lake Store filesystem operations.</span><span class="sxs-lookup"><span data-stu-id="b8157-123">The `azure-datalake-store` module, which includes the Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="b8157-124">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span><span class="sxs-lookup"><span data-stu-id="b8157-124">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="b8157-125">Use the following commands to install the modules.</span><span class="sxs-lookup"><span data-stu-id="b8157-125">Use the following commands to install the modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="b8157-126">Create a new Python application</span><span class="sxs-lookup"><span data-stu-id="b8157-126">Create a new Python application</span></span>

1. <span data-ttu-id="b8157-127">In the IDE of your choice create a new Python application, for example, **mysample.py**.</span><span class="sxs-lookup"><span data-stu-id="b8157-127">In the IDE of your choice create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="b8157-128">Add the following snippet to import the required modules</span><span class="sxs-lookup"><span data-stu-id="b8157-128">Add the following snippet to import the required modules</span></span>

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
    import logging, getpass, pprint, uuid, time
    ```

3. <span data-ttu-id="b8157-129">Save changes to mysample.py.</span><span class="sxs-lookup"><span data-stu-id="b8157-129">Save changes to mysample.py.</span></span>

## <a name="service-to-service-authentication-with-client-secret-for-account-management"></a><span data-ttu-id="b8157-130">Service-to-service authentication with client secret for account management</span><span class="sxs-lookup"><span data-stu-id="b8157-130">Service-to-service authentication with client secret for account management</span></span>

<span data-ttu-id="b8157-131">Use this snippet to authenticate with Azure AD for account management operations on Data Lake Store such as create Data Lake Store account, delete Data Lake Store account, etc. The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal of an existing Azure AD "Web App" application.</span><span class="sxs-lookup"><span data-stu-id="b8157-131">Use this snippet to authenticate with Azure AD for account management operations on Data Lake Store such as create Data Lake Store account, delete Data Lake Store account, etc. The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal of an existing Azure AD "Web App" application.</span></span>

    authority_host_uri = 'https://login.microsoftonline.com'
    tenant = '<TENANT>'
    authority_uri = authority_host_uri + '/' + tenant
    RESOURCE = 'https://management.core.windows.net/'
    client_id = '<CLIENT_ID>'
    client_secret = '<CLIENT_SECRET>'
    
    context = adal.AuthenticationContext(authority_uri, api_version=None)
    mgmt_token = context.acquire_token_with_client_credentials(RESOURCE, client_id, client_secret)
    armCreds = AADTokenCredentials(mgmt_token, client_id, resource=RESOURCE)

## <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a><span data-ttu-id="b8157-132">Service-to-service authentication with client secret for filesystem operations</span><span class="sxs-lookup"><span data-stu-id="b8157-132">Service-to-service authentication with client secret for filesystem operations</span></span>

<span data-ttu-id="b8157-133">Use the following snippet to authenticate with Azure AD for filesystem operations on Data Lake Store such as create folder, upload file, etc. The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal.</span><span class="sxs-lookup"><span data-stu-id="b8157-133">Use the following snippet to authenticate with Azure AD for filesystem operations on Data Lake Store such as create folder, upload file, etc. The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal.</span></span> <span data-ttu-id="b8157-134">Use this with an existing Azure AD "Web App" application.</span><span class="sxs-lookup"><span data-stu-id="b8157-134">Use this with an existing Azure AD "Web App" application.</span></span>

    tenant = '<TENANT>'
    RESOURCE = 'https://datalake.azure.net/'
    client_id = '<CLIENT_ID>'
    client_secret = '<CLIENT_SECRET>'
    
    adlCreds = lib.auth(tenant_id = tenant,
                    client_secret = client_secret,
                    client_id = client_id,
                    resource = RESOURCE)

<!-- ## Service-to-service authentication with certificate for account management

Use this snippet to authenticate with Azure AD for account management operations on Data Lake Store such as create Data Lake Store account, delete Data Lake Store account, etc. The following snippet can be used to authenticate your application non-interactively, using the certificate of an existing Azure AD "Web App" application. For instructions on how to create an Azure AD application, see [Create service principal with certificates](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).

    authority_host_uri = 'https://login.microsoftonline.com'
    tenant = '<TENANT>'
    authority_uri = authority_host_uri + '/' + tenant
    resource_uri = 'https://management.core.windows.net/'
    client_id = '<CLIENT_ID>'
    client_cert = '<CLIENT_CERT>'
    client_cert_thumbprint = '<CLIENT_CERT_THUMBPRINT>'

    context = adal.AuthenticationContext(authority_uri, api_version=None)
    mgmt_token = context.acquire_token_with_client_certificate(resource_uri, client_id, client_cert, client_cert_thumbprint)
    credentials = AADTokenCredentials(mgmt_token, client_id) -->

## <a name="next-steps"></a><span data-ttu-id="b8157-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="b8157-135">Next steps</span></span>
<span data-ttu-id="b8157-136">In this article, you learned how to use service-to-service authentication to authenticate with Azure Data Lake Store using Python.</span><span class="sxs-lookup"><span data-stu-id="b8157-136">In this article, you learned how to use service-to-service authentication to authenticate with Azure Data Lake Store using Python.</span></span> <span data-ttu-id="b8157-137">You can now look at the following articles that talk about how to use Python to work with Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b8157-137">You can now look at the following articles that talk about how to use Python to work with Azure Data Lake Store.</span></span>

* [<span data-ttu-id="b8157-138">Account management operations on Data Lake Store using Python</span><span class="sxs-lookup"><span data-stu-id="b8157-138">Account management operations on Data Lake Store using Python</span></span>](data-lake-store-get-started-python.md)
* [<span data-ttu-id="b8157-139">Data operations on Data Lake Store using Python</span><span class="sxs-lookup"><span data-stu-id="b8157-139">Data operations on Data Lake Store using Python</span></span>](data-lake-store-data-operations-python.md)


