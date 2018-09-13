---
title: Deploy and call web APIs & REST APIs from Azure Logic Apps | Microsoft Docs
description: Deploy and call web APIs & REST APIs for system integratio workflows in Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, stepsic, LADocs
ms.topic: article
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.date: 05/26/2017
ms.openlocfilehash: 0d53c8355fadf53c81676a1fe3c71f8e0b046630
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856152"
---
# <a name="deploy-and-call-custom-apis-from-workflows-in-azure-logic-apps"></a><span data-ttu-id="8c296-103">Deploy and call custom APIs from workflows in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="8c296-103">Deploy and call custom APIs from workflows in Azure Logic Apps</span></span>

<span data-ttu-id="8c296-104">After you [create custom APIs](./logic-apps-create-api-app.md) for use in logic app workflows, you must deploy your APIs before you can call them.</span><span class="sxs-lookup"><span data-stu-id="8c296-104">After you [create custom APIs](./logic-apps-create-api-app.md) for use in logic app workflows, you must deploy your APIs before you can call them.</span></span> <span data-ttu-id="8c296-105">You can deploy your APIs as [web apps](../app-service/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service/app-service-web-tutorial-rest-api.md), which make your job easier when you build, host, and consume APIs in the cloud and on premises.</span><span class="sxs-lookup"><span data-stu-id="8c296-105">You can deploy your APIs as [web apps](../app-service/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service/app-service-web-tutorial-rest-api.md), which make your job easier when you build, host, and consume APIs in the cloud and on premises.</span></span> <span data-ttu-id="8c296-106">You don't have to change any code in your APIs - just deploy your code to an API app.</span><span class="sxs-lookup"><span data-stu-id="8c296-106">You don't have to change any code in your APIs - just deploy your code to an API app.</span></span> <span data-ttu-id="8c296-107">You can host your APIs on [Azure App Service](../app-service/app-service-web-overview.md), a platform-as-a-service (PaaS) offering that provides highly scalable, easy API hosting.</span><span class="sxs-lookup"><span data-stu-id="8c296-107">You can host your APIs on [Azure App Service](../app-service/app-service-web-overview.md), a platform-as-a-service (PaaS) offering that provides highly scalable, easy API hosting.</span></span>

<span data-ttu-id="8c296-108">Although you can call any API from a logic app, for the best experience, add [OpenAPI (previously Swagger) metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span><span class="sxs-lookup"><span data-stu-id="8c296-108">Although you can call any API from a logic app, for the best experience, add [OpenAPI (previously Swagger) metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span></span> <span data-ttu-id="8c296-109">This OpenAPI file helps your API integrate more easily and work better with logic apps.</span><span class="sxs-lookup"><span data-stu-id="8c296-109">This OpenAPI file helps your API integrate more easily and work better with logic apps.</span></span>

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a><span data-ttu-id="8c296-110">Deploy your API as a web app or API app</span><span class="sxs-lookup"><span data-stu-id="8c296-110">Deploy your API as a web app or API app</span></span>

<span data-ttu-id="8c296-111">Before you can call your custom API from a logic app, deploy your API as a web app or API app to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="8c296-111">Before you can call your custom API from a logic app, deploy your API as a web app or API app to Azure App Service.</span></span> <span data-ttu-id="8c296-112">Also, to make your OpenAPI file readable by the Logic Apps Designer, set the API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service/app-service-web-overview.md) for your web app or API app.</span><span class="sxs-lookup"><span data-stu-id="8c296-112">Also, to make your OpenAPI file readable by the Logic Apps Designer, set the API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service/app-service-web-overview.md) for your web app or API app.</span></span>

1. <span data-ttu-id="8c296-113">In the [Azure portal](https://portal.azure.com), select your web app or API app.</span><span class="sxs-lookup"><span data-stu-id="8c296-113">In the [Azure portal](https://portal.azure.com), select your web app or API app.</span></span>

2. <span data-ttu-id="8c296-114">In the app menu that opens, under **API**, choose **API definition**.</span><span class="sxs-lookup"><span data-stu-id="8c296-114">In the app menu that opens, under **API**, choose **API definition**.</span></span> <span data-ttu-id="8c296-115">Set the **API definition location** to the URL for your OpenAPI swagger.json file.</span><span class="sxs-lookup"><span data-stu-id="8c296-115">Set the **API definition location** to the URL for your OpenAPI swagger.json file.</span></span>

   <span data-ttu-id="8c296-116">Usually, the URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span><span class="sxs-lookup"><span data-stu-id="8c296-116">Usually, the URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span></span>

   ![Link to OpenAPI file for your custom API](./media/logic-apps-custom-api-deploy-call/custom-api-swagger-url.png)

3. <span data-ttu-id="8c296-118">Under **API**, choose **CORS**.</span><span class="sxs-lookup"><span data-stu-id="8c296-118">Under **API**, choose **CORS**.</span></span> <span data-ttu-id="8c296-119">Set the CORS policy for **Allowed origins** to **'\*'** (allow all).</span><span class="sxs-lookup"><span data-stu-id="8c296-119">Set the CORS policy for **Allowed origins** to **'\*'** (allow all).</span></span>

   <span data-ttu-id="8c296-120">This setting permits requests from Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="8c296-120">This setting permits requests from Logic App Designer.</span></span>

   ![Permit requests from Logic App Designer to your custom API](./media/logic-apps-custom-api-deploy-call/custom-api-cors.png)

<span data-ttu-id="8c296-122">For more information, see [Host a RESTful API with CORS in Azure App Service](../app-service/app-service-web-tutorial-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="8c296-122">For more information, see [Host a RESTful API with CORS in Azure App Service](../app-service/app-service-web-tutorial-rest-api.md).</span></span>

## <a name="call-your-custom-api-from-logic-app-workflows"></a><span data-ttu-id="8c296-123">Call your custom API from logic app workflows</span><span class="sxs-lookup"><span data-stu-id="8c296-123">Call your custom API from logic app workflows</span></span>

<span data-ttu-id="8c296-124">After you set up the API definition properties and CORS, your custom API's triggers and actions should be available for you to include in your logic app workflow.</span><span class="sxs-lookup"><span data-stu-id="8c296-124">After you set up the API definition properties and CORS, your custom API's triggers and actions should be available for you to include in your logic app workflow.</span></span> 

*  <span data-ttu-id="8c296-125">To view websites that have OpenAPI URLs, you can browse your subscription websites in the Logic Apps Designer.</span><span class="sxs-lookup"><span data-stu-id="8c296-125">To view websites that have OpenAPI URLs, you can browse your subscription websites in the Logic Apps Designer.</span></span>

*  <span data-ttu-id="8c296-126">To view available actions and inputs by pointing at an OpenAPI document, use the [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span><span class="sxs-lookup"><span data-stu-id="8c296-126">To view available actions and inputs by pointing at an OpenAPI document, use the [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span></span>

*  <span data-ttu-id="8c296-127">To call any API, including APIs that don't have or expose an OpenAPI document, you can always create a request with the [HTTP action](../connectors/connectors-native-http.md).</span><span class="sxs-lookup"><span data-stu-id="8c296-127">To call any API, including APIs that don't have or expose an OpenAPI document, you can always create a request with the [HTTP action](../connectors/connectors-native-http.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c296-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="8c296-128">Next steps</span></span>

* [<span data-ttu-id="8c296-129">Custom connector overview</span><span class="sxs-lookup"><span data-stu-id="8c296-129">Custom connector overview</span></span>](../logic-apps/custom-connector-overview.md)