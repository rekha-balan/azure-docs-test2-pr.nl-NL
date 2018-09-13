---
title: 'Python: Account management operations on Azure Data Lake Store | Microsoft Docs'
description: Learn how to use Python SDK to work with Data Lake Store account management operations.
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 75f6de6f-6fd8-48f4-8707-cb27d22d27a6
ms.service: data-lake-store
ms.devlang: na
ms.topic: conceptual
ms.date: 05/29/2018
ms.author: nitinme
ms.openlocfilehash: e5b04a4cfbf26011753715f02baea689ec3065b6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44775794"
---
# <a name="account-management-operations-on-azure-data-lake-store-using-python"></a><span data-ttu-id="e5757-103">Account management operations on Azure Data Lake Store using Python</span><span class="sxs-lookup"><span data-stu-id="e5757-103">Account management operations on Azure Data Lake Store using Python</span></span>
> [!div class="op_single_selector"]
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="e5757-107">Learn how to use the Python SDK for Azure Data Lake Store to perform basic account management operations such as create Data Lake Store account, list Data Lake Store account, etc. For instructions on how to perform filesystem operations on Data Lake Store using Python, see [Filesystem operations on Data Lake Store using Python](data-lake-store-data-operations-python.md).</span><span class="sxs-lookup"><span data-stu-id="e5757-107">Learn how to use the Python SDK for Azure Data Lake Store to perform basic account management operations such as create Data Lake Store account, list Data Lake Store account, etc. For instructions on how to perform filesystem operations on Data Lake Store using Python, see [Filesystem operations on Data Lake Store using Python](data-lake-store-data-operations-python.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5757-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e5757-108">Prerequisites</span></span>

* <span data-ttu-id="e5757-109">**Python**.</span><span class="sxs-lookup"><span data-stu-id="e5757-109">**Python**.</span></span> <span data-ttu-id="e5757-110">You can download Python from [here](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e5757-110">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="e5757-111">This article uses Python 3.6.2.</span><span class="sxs-lookup"><span data-stu-id="e5757-111">This article uses Python 3.6.2.</span></span>

* <span data-ttu-id="e5757-112">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="e5757-112">**An Azure subscription**.</span></span> <span data-ttu-id="e5757-113">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e5757-113">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="e5757-114">**An Azure resource group**.</span><span class="sxs-lookup"><span data-stu-id="e5757-114">**An Azure resource group**.</span></span> <span data-ttu-id="e5757-115">For instructions, see [Create an Azure resource group](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e5757-115">For instructions, see [Create an Azure resource group](../azure-resource-manager/resource-group-portal.md).</span></span>

## <a name="install-the-modules"></a><span data-ttu-id="e5757-116">Install the modules</span><span class="sxs-lookup"><span data-stu-id="e5757-116">Install the modules</span></span>

<span data-ttu-id="e5757-117">To work with Data Lake Store using Python, you need to install three modules.</span><span class="sxs-lookup"><span data-stu-id="e5757-117">To work with Data Lake Store using Python, you need to install three modules.</span></span>

* <span data-ttu-id="e5757-118">The `azure-mgmt-resource` module, which includes Azure modules for Active Directory, etc.</span><span class="sxs-lookup"><span data-stu-id="e5757-118">The `azure-mgmt-resource` module, which includes Azure modules for Active Directory, etc.</span></span>
* <span data-ttu-id="e5757-119">The `azure-mgmt-datalake-store` module, which includes the Azure Data Lake Store account management operations.</span><span class="sxs-lookup"><span data-stu-id="e5757-119">The `azure-mgmt-datalake-store` module, which includes the Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="e5757-120">For more information on this module, see [Azure Data Lake Store Management module reference](https://docs.microsoft.com/python/api/azure.mgmt.datalake.store?view=azure-python).</span><span class="sxs-lookup"><span data-stu-id="e5757-120">For more information on this module, see [Azure Data Lake Store Management module reference](https://docs.microsoft.com/python/api/azure.mgmt.datalake.store?view=azure-python).</span></span>
* <span data-ttu-id="e5757-121">The `azure-datalake-store` module, which includes the Azure Data Lake Store filesystem operations.</span><span class="sxs-lookup"><span data-stu-id="e5757-121">The `azure-datalake-store` module, which includes the Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="e5757-122">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span><span class="sxs-lookup"><span data-stu-id="e5757-122">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="e5757-123">Use the following commands to install the modules.</span><span class="sxs-lookup"><span data-stu-id="e5757-123">Use the following commands to install the modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="e5757-124">Create a new Python application</span><span class="sxs-lookup"><span data-stu-id="e5757-124">Create a new Python application</span></span>

1. <span data-ttu-id="e5757-125">In the IDE of your choice create a new Python application, for example, **mysample.py**.</span><span class="sxs-lookup"><span data-stu-id="e5757-125">In the IDE of your choice create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="e5757-126">Add the following snippet to import the required modules</span><span class="sxs-lookup"><span data-stu-id="e5757-126">Add the following snippet to import the required modules</span></span>

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

3. <span data-ttu-id="e5757-127">Save changes to mysample.py.</span><span class="sxs-lookup"><span data-stu-id="e5757-127">Save changes to mysample.py.</span></span>

## <a name="authentication"></a><span data-ttu-id="e5757-128">Authentication</span><span class="sxs-lookup"><span data-stu-id="e5757-128">Authentication</span></span>

<span data-ttu-id="e5757-129">In this section, we talk about the different ways to authenticate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5757-129">In this section, we talk about the different ways to authenticate with Azure AD.</span></span> <span data-ttu-id="e5757-130">The options available are:</span><span class="sxs-lookup"><span data-stu-id="e5757-130">The options available are:</span></span>

* <span data-ttu-id="e5757-131">For end-user authentication for your application, see [End-user authentication with Data Lake Store using Python](data-lake-store-end-user-authenticate-python.md).</span><span class="sxs-lookup"><span data-stu-id="e5757-131">For end-user authentication for your application, see [End-user authentication with Data Lake Store using Python](data-lake-store-end-user-authenticate-python.md).</span></span>
* <span data-ttu-id="e5757-132">For service-to-service authentication for your application, see [Service-to-service authentication with Data Lake Store using Python](data-lake-store-service-to-service-authenticate-python.md).</span><span class="sxs-lookup"><span data-stu-id="e5757-132">For service-to-service authentication for your application, see [Service-to-service authentication with Data Lake Store using Python](data-lake-store-service-to-service-authenticate-python.md).</span></span>

## <a name="create-client-and-data-lake-store-account"></a><span data-ttu-id="e5757-133">Create client and Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="e5757-133">Create client and Data Lake Store account</span></span>

<span data-ttu-id="e5757-134">The following snippet first creates the Data Lake Store account client.</span><span class="sxs-lookup"><span data-stu-id="e5757-134">The following snippet first creates the Data Lake Store account client.</span></span> <span data-ttu-id="e5757-135">It uses the client object to create a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="e5757-135">It uses the client object to create a Data Lake Store account.</span></span> <span data-ttu-id="e5757-136">Finally, the snippet creates a filesystem client object.</span><span class="sxs-lookup"><span data-stu-id="e5757-136">Finally, the snippet creates a filesystem client object.</span></span>

    ## Declare variables
    subscriptionId = 'FILL-IN-HERE'
    adlsAccountName = 'FILL-IN-HERE'
    resourceGroup = 'FILL-IN-HERE'
    location = 'eastus2'

    ## Create data lake store account management client object
    adlsAcctClient = DataLakeStoreAccountManagementClient(armCreds, subscriptionId)

    ## Create a Data Lake Store account
    adlsAcctResult = adlsAcctClient.account.create(
        resourceGroup,
        adlsAccountName,
        DataLakeStoreAccount(
            location=location
        )
    ).wait()

    
## <a name="list-the-data-lake-store-accounts"></a><span data-ttu-id="e5757-137">List the Data Lake Store accounts</span><span class="sxs-lookup"><span data-stu-id="e5757-137">List the Data Lake Store accounts</span></span>

    ## List the existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="delete-the-data-lake-store-account"></a><span data-ttu-id="e5757-138">Delete the Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="e5757-138">Delete the Data Lake Store account</span></span>

    ## Delete the existing Data Lake Store accounts
    adlsAcctClient.account.delete(adlsAccountName)
    

## <a name="next-steps"></a><span data-ttu-id="e5757-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="e5757-139">Next steps</span></span>
* <span data-ttu-id="e5757-140">[Filesystem operations on Data Lake Store using Python](data-lake-store-data-operations-python.md).</span><span class="sxs-lookup"><span data-stu-id="e5757-140">[Filesystem operations on Data Lake Store using Python](data-lake-store-data-operations-python.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="e5757-141">See also</span><span class="sxs-lookup"><span data-stu-id="e5757-141">See also</span></span>

* [<span data-ttu-id="e5757-142">Azure Data Lake Store Python (Filesystem) Reference</span><span class="sxs-lookup"><span data-stu-id="e5757-142">Azure Data Lake Store Python (Filesystem) Reference</span></span>](http://azure-datalake-store.readthedocs.io/en/latest)
* [<span data-ttu-id="e5757-143">Open Source Big Data applications compatible with Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e5757-143">Open Source Big Data applications compatible with Azure Data Lake Store</span></span>](data-lake-store-compatible-oss-other-applications.md)
