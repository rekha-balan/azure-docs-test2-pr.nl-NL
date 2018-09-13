---
title: Connect to Box - Azure Logic Apps | Microsoft Docs
description: Create and manage files with Box REST APIs and Azure Logic Apps
author: ecfan
manager: jeconnoc
ms.author: estfan
ms.date: 11/07/2016
ms.topic: article
ms.service: logic-apps
services: logic-apps
ms.reviewer: klam, LADocs
ms.suite: integration
tags: connectors
ms.openlocfilehash: b5c8c18c6d02710646560f29d4bc7b5784f730a2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44803444"
---
# <a name="create-and-manage-files-in-box-with-azure-logic-apps"></a><span data-ttu-id="5358b-103">Create and manage files in Box with Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="5358b-103">Create and manage files in Box with Azure Logic Apps</span></span>

<span data-ttu-id="5358b-104">This article shows how you can create and manage your files in Box from inside a logic app with the Box connector.</span><span class="sxs-lookup"><span data-stu-id="5358b-104">This article shows how you can create and manage your files in Box from inside a logic app with the Box connector.</span></span> <span data-ttu-id="5358b-105">That way, you can create logic apps that automate tasks and workflows for managing your files and other actions, for example:</span><span class="sxs-lookup"><span data-stu-id="5358b-105">That way, you can create logic apps that automate tasks and workflows for managing your files and other actions, for example:</span></span>

* <span data-ttu-id="5358b-106">Build your business flow based on the data you get from Box.</span><span class="sxs-lookup"><span data-stu-id="5358b-106">Build your business flow based on the data you get from Box.</span></span> 

* <span data-ttu-id="5358b-107">Trigger automated tasks and workflow when a file is created or updated.</span><span class="sxs-lookup"><span data-stu-id="5358b-107">Trigger automated tasks and workflow when a file is created or updated.</span></span>

* <span data-ttu-id="5358b-108">Run actions that copies a file, deletes a file, and more.</span><span class="sxs-lookup"><span data-stu-id="5358b-108">Run actions that copies a file, deletes a file, and more.</span></span> 

  <span data-ttu-id="5358b-109">When these actions get a response, they make the output available for other actions.</span><span class="sxs-lookup"><span data-stu-id="5358b-109">When these actions get a response, they make the output available for other actions.</span></span> 
  <span data-ttu-id="5358b-110">For example, when a file is changed on Box, you can send that file in email using Office 365.</span><span class="sxs-lookup"><span data-stu-id="5358b-110">For example, when a file is changed on Box, you can send that file in email using Office 365.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5358b-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5358b-111">Prerequisites</span></span>

* <span data-ttu-id="5358b-112">A [Box account](https://www.box.com/home)</span><span class="sxs-lookup"><span data-stu-id="5358b-112">A [Box account](https://www.box.com/home)</span></span>

* <span data-ttu-id="5358b-113">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5358b-113">An Azure subscription.</span></span> <span data-ttu-id="5358b-114">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="5358b-114">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span> 

* <span data-ttu-id="5358b-115">The logic app where you want to access your Box account.</span><span class="sxs-lookup"><span data-stu-id="5358b-115">The logic app where you want to access your Box account.</span></span> <span data-ttu-id="5358b-116">To start your logic app with a Box trigger, you need a [blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="5358b-116">To start your logic app with a Box trigger, you need a [blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span> 

* <span data-ttu-id="5358b-117">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="5358b-117">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span>
<span data-ttu-id="5358b-118">If you're new to logic apps, review [What is Azure Logic Apps](../logic-apps/logic-apps-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5358b-118">If you're new to logic apps, review [What is Azure Logic Apps](../logic-apps/logic-apps-overview.md).</span></span>

## <a name="connector-reference"></a><span data-ttu-id="5358b-119">Connector reference</span><span class="sxs-lookup"><span data-stu-id="5358b-119">Connector reference</span></span>

<span data-ttu-id="5358b-120">For technical details, such as triggers, actions, and limits, as described by the connector's Swagger file, see the [connector's reference page](/connectors/box/).</span><span class="sxs-lookup"><span data-stu-id="5358b-120">For technical details, such as triggers, actions, and limits, as described by the connector's Swagger file, see the [connector's reference page](/connectors/box/).</span></span> 

## <a name="get-support"></a><span data-ttu-id="5358b-121">Get support</span><span class="sxs-lookup"><span data-stu-id="5358b-121">Get support</span></span>

* <span data-ttu-id="5358b-122">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="5358b-122">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="5358b-123">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="5358b-123">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5358b-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="5358b-124">Next steps</span></span>

* <span data-ttu-id="5358b-125">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="5358b-125">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span></span>