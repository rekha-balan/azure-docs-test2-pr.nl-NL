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
# <a name="filesystem-operations-on-azure-data-lake-storage-gen1-using-python"></a>Filesystem operations on Azure Data Lake Storage Gen1 using Python
> [!div class="op_single_selector"]
> * [.NET SDK](data-lake-store-data-operations-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-data-operations-rest-api.md)
> * [Python](data-lake-store-data-operations-python.md)
>
> 

In this article, you learn how to use Python SDK to perform filesystem operations on Azure Data Lake Storage Gen1. For instructions on how to perform account management operations on Data Lake Storage Gen1 using Python, see [Account management operations on Data Lake Storage Gen1 using Python](data-lake-store-get-started-python.md).

## <a name="prerequisites"></a>Prerequisites

* **Python**. You can download Python from [here](https://www.python.org/downloads/). This article uses Python 3.6.2.

* **An Azure subscription**. See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).

* **Azure Data Lake Storage Gen1 account**. Follow the instructions at [Get started with Azure Data Lake Storage Gen1 using the Azure portal](data-lake-store-get-started-portal.md).

## <a name="install-the-modules"></a>Install the modules

To work with Data Lake Storage Gen1 using Python, you need to install three modules.

* The `azure-mgmt-resource` module, which includes Azure modules for Active Directory, etc.
* The `azure-mgmt-datalake-store` module, which includes the Azure Data Lake Storage Gen1 account management operations. For more information on this module, see the [azure-mgmt-datalake-store module reference](https://docs.microsoft.com/python/api/azure.mgmt.datalake.store?view=azure-python).
* The `azure-datalake-store` module, which includes the Azure Data Lake Storage Gen1 filesystem operations. For more information on this module, see the [azure-datalake-store file-system module reference](http://azure-datalake-store.readthedocs.io/en/latest/).

Use the following commands to install the modules.

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a>Create a new Python application

1. In the IDE of your choice create a new Python application, for example, **mysample.py**.

2. Add the following lines to import the required modules

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

3. Save changes to mysample.py.

## <a name="authentication"></a>Authentication

In this section, we talk about the different ways to authenticate with Azure AD. The options available are:

* For end-user authentication for your application, see [End-user authentication with Data Lake Storage Gen1 using Python](data-lake-store-end-user-authenticate-python.md).
* For service-to-service authentication for your application, see [Service-to-service authentication with Data Lake Storage Gen1 using Python](data-lake-store-service-to-service-authenticate-python.md).

## <a name="create-filesystem-client"></a>Create filesystem client

The following snippet first creates the Data Lake Storage Gen1 account client. It uses the client object to create a Data Lake Storage Gen1 account. Finally, the snippet creates a filesystem client object.

    ## Declare variables
    subscriptionId = 'FILL-IN-HERE'
    adlsAccountName = 'FILL-IN-HERE'

    ## Create a filesystem client object
    adlsFileSystemClient = core.AzureDLFileSystem(adlCreds, store_name=adlsAccountName)

## <a name="create-a-directory"></a>Create a directory

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a>Upload a file


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a>Download a file

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a>Delete a directory

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="next-steps"></a>Next steps
* [Account management operations on Data Lake Storage Gen1 using Python](data-lake-store-get-started-python.md).

## <a name="see-also"></a>See also

* [Azure Data Lake Storage Gen1 Python (Filesystem) Reference](http://azure-datalake-store.readthedocs.io/en/latest)
* [Open Source Big Data applications compatible with Azure Data Lake Storage Gen1](data-lake-store-compatible-oss-other-applications.md)