---
title: 'REST API: Account management operations on Azure Data Lake Store | Microsoft Docs'
description: Use Azure Data Lake Store and WebHDFS REST API to perform account management operations in the Data Lake Store
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57ac6501-cb71-4f75-82c2-acc07c562889
ms.service: data-lake-store
ms.devlang: na
ms.topic: conceptual
ms.date: 05/29/2018
ms.author: nitinme
ms.openlocfilehash: 5b31188eb5618d0ec5ac1f89c590913e4e284d9f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44808111"
---
# <a name="account-management-operations-on-azure-data-lake-store-using-rest-api"></a>Account management operations on Azure Data Lake Store using REST API
> [!div class="op_single_selector"]
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

In this article, you learn how to perform account management operations on Data Lake Store using the REST API. Account management operations include creating a Data Lake Store account, deleting a Data Lake Store account, etc. For instructions on how to perform filesystem operations on Data Lake Store using REST API, see [Filesystem operations on Data Lake Store using REST API](data-lake-store-data-operations-rest-api.md).

## <a name="prerequisites"></a>Prerequisites
* **An Azure subscription**. See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).

* **[cURL](http://curl.haxx.se/)**. This article uses cURL to demonstrate how to make REST API calls against a Data Lake Store account.

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>How do I authenticate using Azure Active Directory?
You can use two approaches to authenticate using Azure Active Directory.

* For end-user authentication for your application (interactive), see [End-user authentication with Data Lake Store using .NET SDK](data-lake-store-end-user-authenticate-rest-api.md).
* For service-to-service authentication for your application (non-interactive), see [Service-to-service authentication with Data Lake Store using .NET SDK](data-lake-store-service-to-service-authenticate-rest-api.md).


## <a name="create-a-data-lake-store-account"></a>Create a Data Lake Store account
This operation is based on the REST API call defined [here](https://docs.microsoft.com/en-us/rest/api/datalakestore/accounts/create).

Use the following cURL command. Replace **\<yourstorename>** with your Data Lake Store name.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier. The request payload for this command is contained in the **input.json** file that is provided for the `-d` parameter above. The contents of the input.json file resemble the following snippet:

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="delete-a-data-lake-store-account"></a>Delete a Data Lake Store account
This operation is based on the REST API call defined [here](https://docs.microsoft.com/en-us/rest/api/datalakestore/accounts/delete).

Use the following cURL command to delete a Data Lake Store account. Replace **\<yourstorename>** with your Data Lake Store name.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

You should see an output like the following snippet:

    HTTP/1.1 200 OK
    ...
    ...

## <a name="next-steps"></a>Next steps
* [Filesystem operations on Data Lake Store using REST API](data-lake-store-data-operations-rest-api.md).

## <a name="see-also"></a>See also
* [Azure Data Lake Store REST API Reference](https://docs.microsoft.com/rest/api/datalakestore/)
* [Open Source Big Data applications compatible with Azure Data Lake Store](data-lake-store-compatible-oss-other-applications.md)

