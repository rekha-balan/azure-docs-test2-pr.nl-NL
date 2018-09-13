---
title: Secure APIs using client certificate authentication in API Management - Azure API Management | Microsoft Docs
description: Learn how to secure access to APIs using client certificates
services: api-management
documentationcenter: ''
author: miaojiang
manager: erikre
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: apimpm
ms.openlocfilehash: 7f1d55b90af4e5397d74a8e37b44b5a88530897d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555602"
---
# <a name="how-to-secure-apis-using-client-certificate-authentication-in-api-management"></a><span data-ttu-id="8e769-103">How to secure APIs using client certificate authentication in API Management</span><span class="sxs-lookup"><span data-stu-id="8e769-103">How to secure APIs using client certificate authentication in API Management</span></span>

<span data-ttu-id="8e769-104">API Management provides the capability to secure access to APIs (i.e., client to API Management) using client certificates.</span><span class="sxs-lookup"><span data-stu-id="8e769-104">API Management provides the capability to secure access to APIs (i.e., client to API Management) using client certificates.</span></span> <span data-ttu-id="8e769-105">Currently, you can check the thumbprint of a client certificate against a desired value.</span><span class="sxs-lookup"><span data-stu-id="8e769-105">Currently, you can check the thumbprint of a client certificate against a desired value.</span></span> <span data-ttu-id="8e769-106">You can also check the thumbprint against existing certificates uploaded to API Management.</span><span class="sxs-lookup"><span data-stu-id="8e769-106">You can also check the thumbprint against existing certificates uploaded to API Management.</span></span>  

<span data-ttu-id="8e769-107">For information about securing access to the back-end service of an API using client certificates (i.e., API Management to back-end), see [How to secure back-end services using client certificate authentication](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span><span class="sxs-lookup"><span data-stu-id="8e769-107">For information about securing access to the back-end service of an API using client certificates (i.e., API Management to back-end), see [How to secure back-end services using client certificate authentication](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span></span>

## <a name="checking-the-expiration-date"></a><span data-ttu-id="8e769-108">Checking the expiration date</span><span class="sxs-lookup"><span data-stu-id="8e769-108">Checking the expiration date</span></span>

<span data-ttu-id="8e769-109">Below policies can be configured to check if the certificate is expired:</span><span class="sxs-lookup"><span data-stu-id="8e769-109">Below policies can be configured to check if the certificate is expired:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter > DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-issuer-and-subject"></a><span data-ttu-id="8e769-110">Checking the issuer and subject</span><span class="sxs-lookup"><span data-stu-id="8e769-110">Checking the issuer and subject</span></span>

<span data-ttu-id="8e769-111">Below policies can be configured to check the issuer and subject of a client certificate:</span><span class="sxs-lookup"><span data-stu-id="8e769-111">Below policies can be configured to check the issuer and subject of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-thumbprint"></a><span data-ttu-id="8e769-112">Checking the thumbprint</span><span class="sxs-lookup"><span data-stu-id="8e769-112">Checking the thumbprint</span></span>

<span data-ttu-id="8e769-113">Below policies can be configured to check the thumbprint of a client certificate:</span><span class="sxs-lookup"><span data-stu-id="8e769-113">Below policies can be configured to check the thumbprint of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-to-api-management"></a><span data-ttu-id="8e769-114">Checking a thumbprint against certificates uploaded to API Management</span><span class="sxs-lookup"><span data-stu-id="8e769-114">Checking a thumbprint against certificates uploaded to API Management</span></span>

<span data-ttu-id="8e769-115">The following example shows how to check the thumbprint of a client certificate against certificates uploaded to API Management:</span><span class="sxs-lookup"><span data-stu-id="8e769-115">The following example shows how to check the thumbprint of a client certificate against certificates uploaded to API Management:</span></span> 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a><span data-ttu-id="8e769-116">Next step</span><span class="sxs-lookup"><span data-stu-id="8e769-116">Next step</span></span>

*  [<span data-ttu-id="8e769-117">How to secure back-end services using client certificate authentication</span><span class="sxs-lookup"><span data-stu-id="8e769-117">How to secure back-end services using client certificate authentication</span></span>](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [<span data-ttu-id="8e769-118">How to upload certificates</span><span class="sxs-lookup"><span data-stu-id="8e769-118">How to upload certificates</span></span>](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

