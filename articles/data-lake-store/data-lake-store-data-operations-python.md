---
title: 'Python: Filesystem operations on Azure Data Lake Storage Gen1 | Microsoft Docs'
description: Learn how to use Python SDK to work with the Data Lake Storage Gen1 file system.
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
ms.openlocfilehash: 33abaf7488579a501dc7e2d0b63645726b86c28b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867655"
---
# <a name="filesystem-operations-on-azure-data-lake-storage-gen1-using-python"></a><span data-ttu-id="69cdf-103">Filesystem operations on Azure Data Lake Storage Gen1 using Python</span><span class="sxs-lookup"><span data-stu-id="69cdf-103">Filesystem operations on Azure Data Lake Storage Gen1 using Python</span></span>
> [!div class="op_single_selector"]
> * [.NET SDK](data-lake-store-data-operations-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-data-operations-rest-api.md)
> * [Python](data-lake-store-data-operations-python.md)
>
> 

<span data-ttu-id="69cdf-108">In this article, you learn how to use Python SDK to perform filesystem operations on Azure Data Lake Storage Gen1.</span><span class="sxs-lookup"><span data-stu-id="69cdf-108">In this article, you learn how to use Python SDK to perform filesystem operations on Azure Data Lake Storage Gen1.</span></span> <span data-ttu-id="69cdf-109">For instructions on how to perform account management operations on Data Lake Storage Gen1 using Python, see [Account management operations on Data Lake Storage Gen1 using Python](data-lake-store-get-started-python.md).</span><span class="sxs-lookup"><span data-stu-id="69cdf-109">For instructions on how to perform account management operations on Data Lake Storage Gen1 using Python, see [Account management operations on Data Lake Storage Gen1 using Python](data-lake-store-get-started-python.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69cdf-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="69cdf-110">Prerequisites</span></span>

* <span data-ttu-id="69cdf-111">**Python**.</span><span class="sxs-lookup"><span data-stu-id="69cdf-111">**Python**.</span></span> <span data-ttu-id="69cdf-112">You can download Python from [here](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="69cdf-112">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="69cdf-113">This article uses Python 3.6.2.</span><span class="sxs-lookup"><span data-stu-id="69cdf-113">This article uses Python 3.6.2.</span></span>

* <span data-ttu-id="69cdf-114">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="69cdf-114">**An Azure subscription**.</span></span> <span data-ttu-id="69cdf-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="69cdf-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="69cdf-116">**Azure Data Lake Storage Gen1 account**.</span><span class="sxs-lookup"><span data-stu-id="69cdf-116">**Azure Data Lake Storage Gen1 account**.</span></span> <span data-ttu-id="69cdf-117">Follow the instructions at [Get started with Azure Data Lake Storage Gen1 using the Azure portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="69cdf-117">Follow the instructions at [Get started with Azure Data Lake Storage Gen1 using the Azure portal](data-lake-store-get-started-portal.md).</span></span>

## <a name="install-the-modules"></a><span data-ttu-id="69cdf-118">Install the modules</span><span class="sxs-lookup"><span data-stu-id="69cdf-118">Install the modules</span></span>

<span data-ttu-id="69cdf-119">To work with Data Lake Storage Gen1 using Python, you need to install three modules.</span><span class="sxs-lookup"><span data-stu-id="69cdf-119">To work with Data Lake Storage Gen1 using Python, you need to install three modules.</span></span>

* <span data-ttu-id="69cdf-120">The `azure-mgmt-resource` module, which includes Azure modules for Active Directory, etc.</span><span class="sxs-lookup"><span data-stu-id="69cdf-120">The `azure-mgmt-resource` module, which includes Azure modules for Active Directory, etc.</span></span>
* <span data-ttu-id="69cdf-121">The `azure-mgmt-datalake-store` module, which includes the Azure Data Lake Storage Gen1 account management operations.</span><span class="sxs-lookup"><span data-stu-id="69cdf-121">The `azure-mgmt-datalake-store` module, which includes the Azure Data Lake Storage Gen1 account management operations.</span></span> <span data-ttu-id="69cdf-122">For more information on this module, see the [azure-mgmt-datalake-store module reference](https://docs.microsoft.com/python/api/azure.mgmt.datalake.store?view=azure-python).</span><span class="sxs-lookup"><span data-stu-id="69cdf-122">For more information on this module, see the [azure-mgmt-datalake-store module reference](https://docs.microsoft.com/python/api/azure.mgmt.datalake.store?view=azure-python).</span></span>
* <span data-ttu-id="69cdf-123">The `azure-datalake-store` module, which includes the Azure Data Lake Storage Gen1 filesystem operations.</span><span class="sxs-lookup"><span data-stu-id="69cdf-123">The `azure-datalake-store` module, which includes the Azure Data Lake Storage Gen1 filesystem operations.</span></span> <span data-ttu-id="69cdf-124">For more information on this module, see the [azure-datalake-store file-system module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span><span class="sxs-lookup"><span data-stu-id="69cdf-124">For more information on this module, see the [azure-datalake-store file-system module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="69cdf-125">Use the following commands to install the modules.</span><span class="sxs-lookup"><span data-stu-id="69cdf-125">Use the following commands to install the modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="69cdf-126">Create a new Python application</span><span class="sxs-lookup"><span data-stu-id="69cdf-126">Create a new Python application</span></span>

1. <span data-ttu-id="69cdf-127">In the IDE of your choice create a new Python application, for example, **mysample.py**.</span><span class="sxs-lookup"><span data-stu-id="69cdf-127">In the IDE of your choice create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="69cdf-128">Add the following lines to import the required modules</span><span class="sxs-lookup"><span data-stu-id="69cdf-128">Add the following lines to import the required modules</span></span>

    ```
    ## Use this only for Azure AD service-to-service authentication
    from azure.common.credentials import ServicePrincipalCredentials

    ## Use this only for Azure AD end-user authentication
    from azure.common.credentials import UserPassCredentials

    ## Use this only for Azure AD multi-factor authentication
    from msrestazure.azure_active_directory import AADTokenCredentials

    ## Required for Azure Data Lake Storage Gen1 account management
    from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
    from azure.mgmt.datalake.store.models import DataLakeStoreAccount

    ## Required for Azure Data Lake Storage Gen1 filesystem management
    from azure.datalake.store import core, lib, multithread

    # Common Azure imports
    from azure.mgmt.resource.resources import ResourceManagementClient
    from azure.mgmt.resource.resources.models import ResourceGroup

    ## Use these as needed for your application
    import logging, getpass, pprint, uuid, time
    ```

3. <span data-ttu-id="69cdf-129">Save changes to mysample.py.</span><span class="sxs-lookup"><span data-stu-id="69cdf-129">Save changes to mysample.py.</span></span>

## <a name="authentication"></a><span data-ttu-id="69cdf-130">Authentication</span><span class="sxs-lookup"><span data-stu-id="69cdf-130">Authentication</span></span>

<span data-ttu-id="69cdf-131">In this section, we talk about the different ways to authenticate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="69cdf-131">In this section, we talk about the different ways to authenticate with Azure AD.</span></span> <span data-ttu-id="69cdf-132">The options available are:</span><span class="sxs-lookup"><span data-stu-id="69cdf-132">The options available are:</span></span>

* <span data-ttu-id="69cdf-133">For end-user authentication for your application, see [End-user authentication with Data Lake Storage Gen1 using Python](data-lake-store-end-user-authenticate-python.md).</span><span class="sxs-lookup"><span data-stu-id="69cdf-133">For end-user authentication for your application, see [End-user authentication with Data Lake Storage Gen1 using Python](data-lake-store-end-user-authenticate-python.md).</span></span>
* <span data-ttu-id="69cdf-134">For service-to-service authentication for your application, see [Service-to-service authentication with Data Lake Storage Gen1 using Python](data-lake-store-service-to-service-authenticate-python.md).</span><span class="sxs-lookup"><span data-stu-id="69cdf-134">For service-to-service authentication for your application, see [Service-to-service authentication with Data Lake Storage Gen1 using Python](data-lake-store-service-to-service-authenticate-python.md).</span></span>

## <a name="create-filesystem-client"></a><span data-ttu-id="69cdf-135">Create filesystem client</span><span class="sxs-lookup"><span data-stu-id="69cdf-135">Create filesystem client</span></span>

<span data-ttu-id="69cdf-136">The following snippet first creates the Data Lake Storage Gen1 account client.</span><span class="sxs-lookup"><span data-stu-id="69cdf-136">The following snippet first creates the Data Lake Storage Gen1 account client.</span></span> <span data-ttu-id="69cdf-137">It uses the client object to create a Data Lake Storage Gen1 account.</span><span class="sxs-lookup"><span data-stu-id="69cdf-137">It uses the client object to create a Data Lake Storage Gen1 account.</span></span> <span data-ttu-id="69cdf-138">Finally, the snippet creates a filesystem client object.</span><span class="sxs-lookup"><span data-stu-id="69cdf-138">Finally, the snippet creates a filesystem client object.</span></span>

    ## Declare variables
    subscriptionId = 'FILL-IN-HERE'
    adlsAccountName = 'FILL-IN-HERE'

    ## Create a filesystem client object
    adlsFileSystemClient = core.AzureDLFileSystem(adlCreds, store_name=adlsAccountName)

## <a name="create-a-directory"></a><span data-ttu-id="69cdf-139">Create a directory</span><span class="sxs-lookup"><span data-stu-id="69cdf-139">Create a directory</span></span>

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a><span data-ttu-id="69cdf-140">Upload a file</span><span class="sxs-lookup"><span data-stu-id="69cdf-140">Upload a file</span></span>


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a><span data-ttu-id="69cdf-141">Download a file</span><span class="sxs-lookup"><span data-stu-id="69cdf-141">Download a file</span></span>

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a><span data-ttu-id="69cdf-142">Delete a directory</span><span class="sxs-lookup"><span data-stu-id="69cdf-142">Delete a directory</span></span>

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="next-steps"></a><span data-ttu-id="69cdf-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="69cdf-143">Next steps</span></span>
* <span data-ttu-id="69cdf-144">[Account management operations on Data Lake Storage Gen1 using Python](data-lake-store-get-started-python.md).</span><span class="sxs-lookup"><span data-stu-id="69cdf-144">[Account management operations on Data Lake Storage Gen1 using Python](data-lake-store-get-started-python.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="69cdf-145">See also</span><span class="sxs-lookup"><span data-stu-id="69cdf-145">See also</span></span>

* [<span data-ttu-id="69cdf-146">Azure Data Lake Storage Gen1 Python (Filesystem) Reference</span><span class="sxs-lookup"><span data-stu-id="69cdf-146">Azure Data Lake Storage Gen1 Python (Filesystem) Reference</span></span>](http://azure-datalake-store.readthedocs.io/en/latest)
* [<span data-ttu-id="69cdf-147">Open Source Big Data applications compatible with Azure Data Lake Storage Gen1</span><span class="sxs-lookup"><span data-stu-id="69cdf-147">Open Source Big Data applications compatible with Azure Data Lake Storage Gen1</span></span>](data-lake-store-compatible-oss-other-applications.md)
