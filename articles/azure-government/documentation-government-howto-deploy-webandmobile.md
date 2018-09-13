---
title: Deploy to Azure App Services using Visual Studio 2015 | Microsoft Docs
description: This article describes how to deploy a Web App, API App or Mobile App to Azure Government using Visual Studio 2015 and Azure SDK.
services: azure-government
cloud: gov
documentationcenter: ''
author: sdubeymsft
manager: zakramer
ms.assetid: 8f9a3700-b9ee-43b7-b64d-2e6c3b57d4c0
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 01/03/2016
ms.author: sdubeymsft
ms.openlocfilehash: 7b332230e534a3b1ba8ae73c695b7aa69d662a85
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550596"
---
# <a name="deploy-to-azure-app-services-using-visual-studio-2015"></a><span data-ttu-id="15a6f-103">Deploy to Azure App Services using Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="15a6f-103">Deploy to Azure App Services using Visual Studio 2015</span></span>
<span data-ttu-id="15a6f-104">This article describes how to deploy an Azure App Services app (API App, Web App, Mobile App) to Azure Government using Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="15a6f-104">This article describes how to deploy an Azure App Services app (API App, Web App, Mobile App) to Azure Government using Visual Studio 2015.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15a6f-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="15a6f-105">Prerequisites</span></span>
* <span data-ttu-id="15a6f-106">See [Visual Studio prerequisites] (../app-service-api/app-service-api-dotnet-get-started.md#prerequisites) to install and configure Visual Studio 2015 and Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="15a6f-106">See [Visual Studio prerequisites] (../app-service-api/app-service-api-dotnet-get-started.md#prerequisites) to install and configure Visual Studio 2015 and Azure SDK.</span></span>
* <span data-ttu-id="15a6f-107">Follow [these instructions] (documentation-government-manage-subscriptions.md) to configure Visual Studio to connect to Azure Government account.</span><span class="sxs-lookup"><span data-stu-id="15a6f-107">Follow [these instructions] (documentation-government-manage-subscriptions.md) to configure Visual Studio to connect to Azure Government account.</span></span>

## <a name="open-app-project-in-visual-studio"></a><span data-ttu-id="15a6f-108">Open App project in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="15a6f-108">Open App project in Visual Studio</span></span>
* <span data-ttu-id="15a6f-109">Open existing app solution\project in Visual Studio, create a project by following [these instructions] (../app-service-web/app-service-web-get-started-dotnet.md), or download sample app by following [these steps] (../app-service-api/app-service-api-dotnet-get-started.md#download-the-sample-application).</span><span class="sxs-lookup"><span data-stu-id="15a6f-109">Open existing app solution\project in Visual Studio, create a project by following [these instructions] (../app-service-web/app-service-web-get-started-dotnet.md), or download sample app by following [these steps] (../app-service-api/app-service-api-dotnet-get-started.md#download-the-sample-application).</span></span>
* <span data-ttu-id="15a6f-110">Run the app in Visual Studio to make sure it works locally.</span><span class="sxs-lookup"><span data-stu-id="15a6f-110">Run the app in Visual Studio to make sure it works locally.</span></span>

## <a name="deploy-to-azure-government"></a><span data-ttu-id="15a6f-111">Deploy to Azure Government</span><span class="sxs-lookup"><span data-stu-id="15a6f-111">Deploy to Azure Government</span></span>
* <span data-ttu-id="15a6f-112">Once **Visual Studio is configured to connect to Azure Government account** (already done in prerequisites section), instructions to deploy to app services are exactly same as for Azure Public.</span><span class="sxs-lookup"><span data-stu-id="15a6f-112">Once **Visual Studio is configured to connect to Azure Government account** (already done in prerequisites section), instructions to deploy to app services are exactly same as for Azure Public.</span></span>
* <span data-ttu-id="15a6f-113">To deploy the app, follow [these steps] (../app-service-api/app-service-api-dotnet-get-started.md#a-idcreateapiappa-create-an-api-app-in-azure-and-deploy-code-to-it).</span><span class="sxs-lookup"><span data-stu-id="15a6f-113">To deploy the app, follow [these steps] (../app-service-api/app-service-api-dotnet-get-started.md#a-idcreateapiappa-create-an-api-app-in-azure-and-deploy-code-to-it).</span></span>

### <a name="references"></a><span data-ttu-id="15a6f-114">References</span><span class="sxs-lookup"><span data-stu-id="15a6f-114">References</span></span>
* <span data-ttu-id="15a6f-115">[Deploy an ASP.NET web app to Azure App Service, using Visual Studio] (../app-service-web/app-service-web-get-started-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="15a6f-115">[Deploy an ASP.NET web app to Azure App Service, using Visual Studio] (../app-service-web/app-service-web-get-started-dotnet.md)</span></span>
* <span data-ttu-id="15a6f-116">For other ways to deploy, see [Deploy your app to Azure App Service] (../app-service-web/web-sites-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="15a6f-116">For other ways to deploy, see [Deploy your app to Azure App Service] (../app-service-web/web-sites-deploy.md)</span></span>
* <span data-ttu-id="15a6f-117">For general App Service documentation, see [App Service - API Apps Documentation] (../app-service-api/index.md)</span><span class="sxs-lookup"><span data-stu-id="15a6f-117">For general App Service documentation, see [App Service - API Apps Documentation] (../app-service-api/index.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="15a6f-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="15a6f-118">Next steps</span></span>
<span data-ttu-id="15a6f-119">For supplemental information and updates, subscribe to the [Microsoft Azure Government Blog](https://blogs.msdn.microsoft.com/azuregov/).</span><span class="sxs-lookup"><span data-stu-id="15a6f-119">For supplemental information and updates, subscribe to the [Microsoft Azure Government Blog](https://blogs.msdn.microsoft.com/azuregov/).</span></span>
