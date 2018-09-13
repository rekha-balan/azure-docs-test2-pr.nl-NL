---
title: 'Service-to-service authentication: REST API with Data Lake Store using Azure Active Directory | Microsoft Docs'
description: Learn how to achieve service-to-service authentication with Data Lake Store using Azure Active Directory using REST API
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
ms.openlocfilehash: ffa9b7408475820735e35a82edc0b1751abeb08a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868780"
---
# <a name="service-to-service-authentication-with-data-lake-store-using-rest-api"></a><span data-ttu-id="21304-103">Service-to-service authentication with Data Lake Store using REST API</span><span class="sxs-lookup"><span data-stu-id="21304-103">Service-to-service authentication with Data Lake Store using REST API</span></span>
> [!div class="op_single_selector"]
> * [Using Java](data-lake-store-service-to-service-authenticate-java.md)
> * [Using .NET SDK](data-lake-store-service-to-service-authenticate-net-sdk.md)
> * [Using Python](data-lake-store-service-to-service-authenticate-python.md)
> * [Using REST API](data-lake-store-service-to-service-authenticate-rest-api.md)
> 
> 

<span data-ttu-id="21304-108">In this article, you learn about how to use the REST API to do service-to-service authentication with Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="21304-108">In this article, you learn about how to use the REST API to do service-to-service authentication with Azure Data Lake Store.</span></span> <span data-ttu-id="21304-109">For end-user authentication with Data Lake Store using REST API, see [End-user authentication with Data Lake Store using REST API](data-lake-store-end-user-authenticate-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="21304-109">For end-user authentication with Data Lake Store using REST API, see [End-user authentication with Data Lake Store using REST API](data-lake-store-end-user-authenticate-rest-api.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21304-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="21304-110">Prerequisites</span></span>
* <span data-ttu-id="21304-111">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="21304-111">**An Azure subscription**.</span></span> <span data-ttu-id="21304-112">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="21304-112">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="21304-113">**Create an Azure Active Directory "Web" Application**.</span><span class="sxs-lookup"><span data-stu-id="21304-113">**Create an Azure Active Directory "Web" Application**.</span></span> <span data-ttu-id="21304-114">You must have completed the steps in [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-service-to-service-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="21304-114">You must have completed the steps in [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-service-to-service-authenticate-using-active-directory.md).</span></span>

## <a name="service-to-service-authentication"></a><span data-ttu-id="21304-115">Service-to-service authentication</span><span class="sxs-lookup"><span data-stu-id="21304-115">Service-to-service authentication</span></span>
<span data-ttu-id="21304-116">In this scenario, the application provides its own credentials to perform the operations.</span><span class="sxs-lookup"><span data-stu-id="21304-116">In this scenario, the application provides its own credentials to perform the operations.</span></span> <span data-ttu-id="21304-117">For this, you must issue a POST request like the one shown in the following snippet:</span><span class="sxs-lookup"><span data-stu-id="21304-117">For this, you must issue a POST request like the one shown in the following snippet:</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="21304-118">The output of the request includes an authorization token (denoted by `access-token` in the output below) that you subsequently pass with your REST API calls.</span><span class="sxs-lookup"><span data-stu-id="21304-118">The output of the request includes an authorization token (denoted by `access-token` in the output below) that you subsequently pass with your REST API calls.</span></span> <span data-ttu-id="21304-119">Save the authentication token in a text file; you will need it when making REST calls to the Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="21304-119">Save the authentication token in a text file; you will need it when making REST calls to the Data Lake Store.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="21304-120">This article uses the **non-interactive** approach.</span><span class="sxs-lookup"><span data-stu-id="21304-120">This article uses the **non-interactive** approach.</span></span> <span data-ttu-id="21304-121">For more information on non-interactive (service-to-service calls), see [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="21304-121">For more information on non-interactive (service-to-service calls), see [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="21304-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="21304-122">Next steps</span></span>
<span data-ttu-id="21304-123">In this article, you learned how to use service-to-service authentication to authenticate with Azure Data Lake Store using REST API.</span><span class="sxs-lookup"><span data-stu-id="21304-123">In this article, you learned how to use service-to-service authentication to authenticate with Azure Data Lake Store using REST API.</span></span> <span data-ttu-id="21304-124">You can now look at the following articles that talk about how to use the REST API to work with Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="21304-124">You can now look at the following articles that talk about how to use the REST API to work with Azure Data Lake Store.</span></span>

* [<span data-ttu-id="21304-125">Account management operations on Data Lake Store using REST API</span><span class="sxs-lookup"><span data-stu-id="21304-125">Account management operations on Data Lake Store using REST API</span></span>](data-lake-store-get-started-rest-api.md)
* [<span data-ttu-id="21304-126">Data operations on Data Lake Store using REST API</span><span class="sxs-lookup"><span data-stu-id="21304-126">Data operations on Data Lake Store using REST API</span></span>](data-lake-store-data-operations-rest-api.md)

