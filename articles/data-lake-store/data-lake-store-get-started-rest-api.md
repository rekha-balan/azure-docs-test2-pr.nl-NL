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
# <a name="account-management-operations-on-azure-data-lake-store-using-rest-api"></a><span data-ttu-id="1b0bb-103">Account management operations on Azure Data Lake Store using REST API</span><span class="sxs-lookup"><span data-stu-id="1b0bb-103">Account management operations on Azure Data Lake Store using REST API</span></span>
> [!div class="op_single_selector"]
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="1b0bb-107">In this article, you learn how to perform account management operations on Data Lake Store using the REST API.</span><span class="sxs-lookup"><span data-stu-id="1b0bb-107">In this article, you learn how to perform account management operations on Data Lake Store using the REST API.</span></span> <span data-ttu-id="1b0bb-108">Account management operations include creating a Data Lake Store account, deleting a Data Lake Store account, etc. For instructions on how to perform filesystem operations on Data Lake Store using REST API, see [Filesystem operations on Data Lake Store using REST API](data-lake-store-data-operations-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="1b0bb-108">Account management operations include creating a Data Lake Store account, deleting a Data Lake Store account, etc. For instructions on how to perform filesystem operations on Data Lake Store using REST API, see [Filesystem operations on Data Lake Store using REST API](data-lake-store-data-operations-rest-api.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b0bb-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1b0bb-109">Prerequisites</span></span>
* <span data-ttu-id="1b0bb-110">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="1b0bb-110">**An Azure subscription**.</span></span> <span data-ttu-id="1b0bb-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1b0bb-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="1b0bb-112">**[cURL](http://curl.haxx.se/)**.</span><span class="sxs-lookup"><span data-stu-id="1b0bb-112">**[cURL](http://curl.haxx.se/)**.</span></span> <span data-ttu-id="1b0bb-113">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="1b0bb-113">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Store account.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="1b0bb-114">How do I authenticate using Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1b0bb-114">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="1b0bb-115">You can use two approaches to authenticate using Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b0bb-115">You can use two approaches to authenticate using Azure Active Directory.</span></span>

* <span data-ttu-id="1b0bb-116">For end-user authentication for your application (interactive), see [End-user authentication with Data Lake Store using .NET SDK](data-lake-store-end-user-authenticate-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="1b0bb-116">For end-user authentication for your application (interactive), see [End-user authentication with Data Lake Store using .NET SDK](data-lake-store-end-user-authenticate-rest-api.md).</span></span>
* <span data-ttu-id="1b0bb-117">For service-to-service authentication for your application (non-interactive), see [Service-to-service authentication with Data Lake Store using .NET SDK](data-lake-store-service-to-service-authenticate-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="1b0bb-117">For service-to-service authentication for your application (non-interactive), see [Service-to-service authentication with Data Lake Store using .NET SDK](data-lake-store-service-to-service-authenticate-rest-api.md).</span></span>


## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="1b0bb-118">Create a Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="1b0bb-118">Create a Data Lake Store account</span></span>
<span data-ttu-id="1b0bb-119">This operation is based on the REST API call defined [here](https://docs.microsoft.com/en-us/rest/api/datalakestore/accounts/create).</span><span class="sxs-lookup"><span data-stu-id="1b0bb-119">This operation is based on the REST API call defined [here](https://docs.microsoft.com/en-us/rest/api/datalakestore/accounts/create).</span></span>

<span data-ttu-id="1b0bb-120">Use the following cURL command.</span><span class="sxs-lookup"><span data-stu-id="1b0bb-120">Use the following cURL command.</span></span> <span data-ttu-id="1b0bb-121">Replace **\<yourstorename>** with your Data Lake Store name.</span><span class="sxs-lookup"><span data-stu-id="1b0bb-121">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

<span data-ttu-id="1b0bb-122">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span><span class="sxs-lookup"><span data-stu-id="1b0bb-122">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span> <span data-ttu-id="1b0bb-123">The request payload for this command is contained in the **input.json** file that is provided for the `-d` parameter above.</span><span class="sxs-lookup"><span data-stu-id="1b0bb-123">The request payload for this command is contained in the **input.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="1b0bb-124">The contents of the input.json file resemble the following snippet:</span><span class="sxs-lookup"><span data-stu-id="1b0bb-124">The contents of the input.json file resemble the following snippet:</span></span>

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="1b0bb-125">Delete a Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="1b0bb-125">Delete a Data Lake Store account</span></span>
<span data-ttu-id="1b0bb-126">This operation is based on the REST API call defined [here](https://docs.microsoft.com/en-us/rest/api/datalakestore/accounts/delete).</span><span class="sxs-lookup"><span data-stu-id="1b0bb-126">This operation is based on the REST API call defined [here](https://docs.microsoft.com/en-us/rest/api/datalakestore/accounts/delete).</span></span>

<span data-ttu-id="1b0bb-127">Use the following cURL command to delete a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="1b0bb-127">Use the following cURL command to delete a Data Lake Store account.</span></span> <span data-ttu-id="1b0bb-128">Replace **\<yourstorename>** with your Data Lake Store name.</span><span class="sxs-lookup"><span data-stu-id="1b0bb-128">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

<span data-ttu-id="1b0bb-129">You should see an output like the following snippet:</span><span class="sxs-lookup"><span data-stu-id="1b0bb-129">You should see an output like the following snippet:</span></span>

    HTTP/1.1 200 OK
    ...
    ...

## <a name="next-steps"></a><span data-ttu-id="1b0bb-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="1b0bb-130">Next steps</span></span>
* <span data-ttu-id="1b0bb-131">[Filesystem operations on Data Lake Store using REST API](data-lake-store-data-operations-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="1b0bb-131">[Filesystem operations on Data Lake Store using REST API](data-lake-store-data-operations-rest-api.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="1b0bb-132">See also</span><span class="sxs-lookup"><span data-stu-id="1b0bb-132">See also</span></span>
* [<span data-ttu-id="1b0bb-133">Azure Data Lake Store REST API Reference</span><span class="sxs-lookup"><span data-stu-id="1b0bb-133">Azure Data Lake Store REST API Reference</span></span>](https://docs.microsoft.com/rest/api/datalakestore/)
* [<span data-ttu-id="1b0bb-134">Open Source Big Data applications compatible with Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1b0bb-134">Open Source Big Data applications compatible with Azure Data Lake Store</span></span>](data-lake-store-compatible-oss-other-applications.md)

