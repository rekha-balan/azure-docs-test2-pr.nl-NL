---
title: Restrictions and known issues in Azure API Management API import | Microsoft Docs
description: Details of known issues and restrictions on import into Azure API Management using the Open API, WSDL or WADL formats.
services: api-management
documentationcenter: ''
author: mattfarm
manager: vlvinogr
editor: ''
ms.assetid: 7a5a63f0-3e72-49d3-a28c-1bb23ab495e2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: apipm
ms.openlocfilehash: 09cebaec1c370761ec2f87e30da381287b495f38
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564162"
---
# <a name="api-import-restrictions-and-known-issues"></a><span data-ttu-id="3c909-103">API import restrictions and known issues</span><span class="sxs-lookup"><span data-stu-id="3c909-103">API import restrictions and known issues</span></span>
## <a name="about-this-list"></a><span data-ttu-id="3c909-104">About this list</span><span class="sxs-lookup"><span data-stu-id="3c909-104">About this list</span></span>
<span data-ttu-id="3c909-105">While every effort is made to ensure that importing your API into Azure API Management is as seamless and problem-free as possible, we do occasionally impose restrictions or identify issues that will need to be rectified before you can successfully import.</span><span class="sxs-lookup"><span data-stu-id="3c909-105">While every effort is made to ensure that importing your API into Azure API Management is as seamless and problem-free as possible, we do occasionally impose restrictions or identify issues that will need to be rectified before you can successfully import.</span></span> <span data-ttu-id="3c909-106">This article documents these, organised by the import format of the API.</span><span class="sxs-lookup"><span data-stu-id="3c909-106">This article documents these, organised by the import format of the API.</span></span>

## <span data-ttu-id="3c909-107"><a name="open-api"> </a>Open API/Swagger</span><span class="sxs-lookup"><span data-stu-id="3c909-107"><a name="open-api"> </a>Open API/Swagger</span></span>
<span data-ttu-id="3c909-108">In general, if you are receiving errors importing your Open API document, please ensure you have validated it - either using the designer in the new Azure Portal (Design - Front End - Open API Specification Editor), or with a 3rd party tool such as <a href="http://www.swagger.io">Swagger Editor</a>.</span><span class="sxs-lookup"><span data-stu-id="3c909-108">In general, if you are receiving errors importing your Open API document, please ensure you have validated it - either using the designer in the new Azure Portal (Design - Front End - Open API Specification Editor), or with a 3rd party tool such as <a href="http://www.swagger.io">Swagger Editor</a>.</span></span>

* <span data-ttu-id="3c909-109">**Host Name** we require a host name attribute.</span><span class="sxs-lookup"><span data-stu-id="3c909-109">**Host Name** we require a host name attribute.</span></span>
* <span data-ttu-id="3c909-110">**Base Path** we require a base path attribute.</span><span class="sxs-lookup"><span data-stu-id="3c909-110">**Base Path** we require a base path attribute.</span></span>
* <span data-ttu-id="3c909-111">**Schemes** we require a scheme array.</span><span class="sxs-lookup"><span data-stu-id="3c909-111">**Schemes** we require a scheme array.</span></span> 

## <span data-ttu-id="3c909-112"><a name="wsdl"> </a>WSDL</span><span class="sxs-lookup"><span data-stu-id="3c909-112"><a name="wsdl"> </a>WSDL</span></span>
<span data-ttu-id="3c909-113">WSDL files are used to generate SOAP Pass-through APIs, or serve as the backend of a SOAP-to-REST API.</span><span class="sxs-lookup"><span data-stu-id="3c909-113">WSDL files are used to generate SOAP Pass-through APIs, or serve as the backend of a SOAP-to-REST API.</span></span>

* <span data-ttu-id="3c909-114">**WSDL:Import** we do not currently support APIs using this attribute.</span><span class="sxs-lookup"><span data-stu-id="3c909-114">**WSDL:Import** we do not currently support APIs using this attribute.</span></span> <span data-ttu-id="3c909-115">Customers should merge the imported elements into one document.</span><span class="sxs-lookup"><span data-stu-id="3c909-115">Customers should merge the imported elements into one document.</span></span>
* <span data-ttu-id="3c909-116">**Messages with multiple parts** are currently not supported.</span><span class="sxs-lookup"><span data-stu-id="3c909-116">**Messages with multiple parts** are currently not supported.</span></span>
* <span data-ttu-id="3c909-117">**WCF wsHttpBinding** SOAP services created with Windows Communication Foundation should use basicHttpBinding - wsHttpBinding is not supported.</span><span class="sxs-lookup"><span data-stu-id="3c909-117">**WCF wsHttpBinding** SOAP services created with Windows Communication Foundation should use basicHttpBinding - wsHttpBinding is not supported.</span></span>
* <span data-ttu-id="3c909-118">**MTOM** Services using MTOM <em>may</em> work.</span><span class="sxs-lookup"><span data-stu-id="3c909-118">**MTOM** Services using MTOM <em>may</em> work.</span></span> <span data-ttu-id="3c909-119">Official support is not offered at this time.</span><span class="sxs-lookup"><span data-stu-id="3c909-119">Official support is not offered at this time.</span></span>
* <span data-ttu-id="3c909-120">**Recursion** types that are defined recursively (e.g. refer to an array of themselves) are not supported.</span><span class="sxs-lookup"><span data-stu-id="3c909-120">**Recursion** types that are defined recursively (e.g. refer to an array of themselves) are not supported.</span></span>

## <span data-ttu-id="3c909-121"><a name="wadl"> </a>WADL</span><span class="sxs-lookup"><span data-stu-id="3c909-121"><a name="wadl"> </a>WADL</span></span>
<span data-ttu-id="3c909-122">There are no known WADL import issues currently.</span><span class="sxs-lookup"><span data-stu-id="3c909-122">There are no known WADL import issues currently.</span></span>


[api-management-management-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to cache operation results in Azure API Management]: api-management-howto-cache.md













