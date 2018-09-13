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
# <a name="service-to-service-authentication-with-data-lake-store-using-rest-api"></a>Service-to-service authentication with Data Lake Store using REST API
> [!div class="op_single_selector"]
> * [Using Java](data-lake-store-service-to-service-authenticate-java.md)
> * [Using .NET SDK](data-lake-store-service-to-service-authenticate-net-sdk.md)
> * [Using Python](data-lake-store-service-to-service-authenticate-python.md)
> * [Using REST API](data-lake-store-service-to-service-authenticate-rest-api.md)
> 
> 

In this article, you learn about how to use the REST API to do service-to-service authentication with Azure Data Lake Store. For end-user authentication with Data Lake Store using REST API, see [End-user authentication with Data Lake Store using REST API](data-lake-store-end-user-authenticate-rest-api.md).

## <a name="prerequisites"></a>Prerequisites
* **An Azure subscription**. See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).

* **Create an Azure Active Directory "Web" Application**. You must have completed the steps in [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-service-to-service-authenticate-using-active-directory.md).

## <a name="service-to-service-authentication"></a>Service-to-service authentication
In this scenario, the application provides its own credentials to perform the operations. For this, you must issue a POST request like the one shown in the following snippet: 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

The output of the request includes an authorization token (denoted by `access-token` in the output below) that you subsequently pass with your REST API calls. Save the authentication token in a text file; you will need it when making REST calls to the Data Lake Store.

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

This article uses the **non-interactive** approach. For more information on non-interactive (service-to-service calls), see [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx). 

## <a name="next-steps"></a>Next steps
In this article, you learned how to use service-to-service authentication to authenticate with Azure Data Lake Store using REST API. You can now look at the following articles that talk about how to use the REST API to work with Azure Data Lake Store.

* [Account management operations on Data Lake Store using REST API](data-lake-store-get-started-rest-api.md)
* [Data operations on Data Lake Store using REST API](data-lake-store-data-operations-rest-api.md)

