---
title: Refine query results with the Bing Autosuggest API | Microsoft Docs
description: Get started with the Bing Autosuggest API, and use the API Testing Console to test API requests.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.service: cognitive-services
ms.technology: bing-autosuggest
ms.topic: article
ms.date: 01/12/2017
ms.author: scottwhi
ms.openlocfilehash: 2c74af572449ca12717f2cfa4e676f06087d274e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552474"
---
# <a name="bing-autosuggest-api"></a><span data-ttu-id="a30ba-103">Bing Autosuggest API</span><span class="sxs-lookup"><span data-stu-id="a30ba-103">Bing Autosuggest API</span></span>

<span data-ttu-id="a30ba-104">The Bing Autosuggest API lets partners send a partial search query to Bing and get back a list of suggested queries that other users have searched on (overview on [MSDN](https://msdn.microsoft.com/en-us/library/mt711406.aspx)).</span><span class="sxs-lookup"><span data-stu-id="a30ba-104">The Bing Autosuggest API lets partners send a partial search query to Bing and get back a list of suggested queries that other users have searched on (overview on [MSDN](https://msdn.microsoft.com/en-us/library/mt711406.aspx)).</span></span> <span data-ttu-id="a30ba-105">In addition to including searches that other users have made, the list may include suggestions based on user intent.</span><span class="sxs-lookup"><span data-stu-id="a30ba-105">In addition to including searches that other users have made, the list may include suggestions based on user intent.</span></span> <span data-ttu-id="a30ba-106">For example, if the query string is "*weather in Lo*", the list will include relevant weather suggestions.</span><span class="sxs-lookup"><span data-stu-id="a30ba-106">For example, if the query string is "*weather in Lo*", the list will include relevant weather suggestions.</span></span>

<span data-ttu-id="a30ba-107">Typically, you use this API to support an auto-suggest search box feature.</span><span class="sxs-lookup"><span data-stu-id="a30ba-107">Typically, you use this API to support an auto-suggest search box feature.</span></span> <span data-ttu-id="a30ba-108">For example, as the user types a query into the search box, you would call this API to populate a drop-down list of suggested query strings.</span><span class="sxs-lookup"><span data-stu-id="a30ba-108">For example, as the user types a query into the search box, you would call this API to populate a drop-down list of suggested query strings.</span></span> <span data-ttu-id="a30ba-109">If the user selects a query from the list, you would either send the user to the Bing search results page for the selected query or call the [Web Search API](https://msdn.microsoft.com/en-us/library/mt711415(v=bsynd.50).aspx) to get the search results and display the results yourself.</span><span class="sxs-lookup"><span data-stu-id="a30ba-109">If the user selects a query from the list, you would either send the user to the Bing search results page for the selected query or call the [Web Search API](https://msdn.microsoft.com/en-us/library/mt711415(v=bsynd.50).aspx) to get the search results and display the results yourself.</span></span>

<span data-ttu-id="a30ba-110">To get started, read our [Getting Started](https://msdn.microsoft.com/en-US/library/mt712546.aspx) guide, which describes how you can obtain your own subscription keys and start making calls to the API.</span><span class="sxs-lookup"><span data-stu-id="a30ba-110">To get started, read our [Getting Started](https://msdn.microsoft.com/en-US/library/mt712546.aspx) guide, which describes how you can obtain your own subscription keys and start making calls to the API.</span></span> <span data-ttu-id="a30ba-111">If you already have a subscription, try our API Testing Console [API Testing Console](https://dev.cognitive.microsoft.com/docs/services/56c7694ecf5ff801a090fbd1/operations/56c769a2cf5ff801a090fbd2/console) where you can easily craft API requests in a sandbox environment.</span><span class="sxs-lookup"><span data-stu-id="a30ba-111">If you already have a subscription, try our API Testing Console [API Testing Console](https://dev.cognitive.microsoft.com/docs/services/56c7694ecf5ff801a090fbd1/operations/56c769a2cf5ff801a090fbd2/console) where you can easily craft API requests in a sandbox environment.</span></span>

<span data-ttu-id="a30ba-112">For information that shows you how to use the Autosuggest API, see [Autosuggest Guide](https://msdn.microsoft.com/en-us/library/mt711401(v=bsynd.50).aspx).</span><span class="sxs-lookup"><span data-stu-id="a30ba-112">For information that shows you how to use the Autosuggest API, see [Autosuggest Guide](https://msdn.microsoft.com/en-us/library/mt711401(v=bsynd.50).aspx).</span></span>

<span data-ttu-id="a30ba-113">For information about the programming elements that you'd use to request and consume the search results, see [Autosuggest Reference](https://msdn.microsoft.com/en-us/library/mt711395(v=bsynd.50).aspx).</span><span class="sxs-lookup"><span data-stu-id="a30ba-113">For information about the programming elements that you'd use to request and consume the search results, see [Autosuggest Reference](https://msdn.microsoft.com/en-us/library/mt711395(v=bsynd.50).aspx).</span></span>

<span data-ttu-id="a30ba-114">For additional guide and reference content that is common to all Bing APIs, such as Paging Results and Error Codes, see [Shared Guides](https://msdn.microsoft.com/en-us/library/mt711404(v=bsynd.50).aspx) and [Shared Reference](https://msdn.microsoft.com/en-us/library/mt711403(v=bsynd.50).aspx).</span><span class="sxs-lookup"><span data-stu-id="a30ba-114">For additional guide and reference content that is common to all Bing APIs, such as Paging Results and Error Codes, see [Shared Guides](https://msdn.microsoft.com/en-us/library/mt711404(v=bsynd.50).aspx) and [Shared Reference](https://msdn.microsoft.com/en-us/library/mt711403(v=bsynd.50).aspx).</span></span>
