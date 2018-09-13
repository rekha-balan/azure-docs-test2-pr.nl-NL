---
title: Connect to Excel Online - Azure Logic Apps | Microsoft Docs
description: Manage data with Excel Online REST APIs and Azure Logic Apps
ms.service: logic-apps
services: logic-apps
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.suite: integration
tags: connectors
ms.topic: article
ms.date: 08/23/2018
ms.openlocfilehash: ceef6c5f32372bb69f6ce789e755bc540cb12ba1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44825415"
---
# <a name="manage-excel-online-data-with-azure-logic-apps"></a><span data-ttu-id="f7619-103">Manage Excel Online data with Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="f7619-103">Manage Excel Online data with Azure Logic Apps</span></span>

<span data-ttu-id="f7619-104">With Azure Logic Apps and the Excel Online connector, you can create automated tasks and workflows based on your data in Excel Online for Business or OneDrive.</span><span class="sxs-lookup"><span data-stu-id="f7619-104">With Azure Logic Apps and the Excel Online connector, you can create automated tasks and workflows based on your data in Excel Online for Business or OneDrive.</span></span> <span data-ttu-id="f7619-105">This connector provides actions that help you work with your data and manage spreadsheets, for example:</span><span class="sxs-lookup"><span data-stu-id="f7619-105">This connector provides actions that help you work with your data and manage spreadsheets, for example:</span></span> 

* <span data-ttu-id="f7619-106">Create new worksheets and tables.</span><span class="sxs-lookup"><span data-stu-id="f7619-106">Create new worksheets and tables.</span></span>
* <span data-ttu-id="f7619-107">Get and manage worksheets, tables, and rows.</span><span class="sxs-lookup"><span data-stu-id="f7619-107">Get and manage worksheets, tables, and rows.</span></span>
* <span data-ttu-id="f7619-108">Add single rows and key columns.</span><span class="sxs-lookup"><span data-stu-id="f7619-108">Add single rows and key columns.</span></span>

<span data-ttu-id="f7619-109">You can then use the outputs from these actions with actions for other services.</span><span class="sxs-lookup"><span data-stu-id="f7619-109">You can then use the outputs from these actions with actions for other services.</span></span> <span data-ttu-id="f7619-110">For example, if you use an action that creates worksheets each week, you can use another action that sends confirmation email by using the Office 365 Outlook connector.</span><span class="sxs-lookup"><span data-stu-id="f7619-110">For example, if you use an action that creates worksheets each week, you can use another action that sends confirmation email by using the Office 365 Outlook connector.</span></span>

<span data-ttu-id="f7619-111">If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f7619-111">If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)</span></span>

> [!NOTE]
> <span data-ttu-id="f7619-112">The [Excel Online for Business](/connectors/excelonlinebusiness/) and [Excel Online for OneDrive](/connectors/excelonline/) connectors work with Azure Logic Apps and differ from the [Excel connector for PowerApps](/connectors/excel/).</span><span class="sxs-lookup"><span data-stu-id="f7619-112">The [Excel Online for Business](/connectors/excelonlinebusiness/) and [Excel Online for OneDrive](/connectors/excelonline/) connectors work with Azure Logic Apps and differ from the [Excel connector for PowerApps](/connectors/excel/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7619-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f7619-113">Prerequisites</span></span>

* <span data-ttu-id="f7619-114">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f7619-114">An Azure subscription.</span></span> <span data-ttu-id="f7619-115">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="f7619-115">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span> 

* <span data-ttu-id="f7619-116">An [Office 365 account](https://www.office.com/) for your work account or personal Microsoft account</span><span class="sxs-lookup"><span data-stu-id="f7619-116">An [Office 365 account](https://www.office.com/) for your work account or personal Microsoft account</span></span> 

  <span data-ttu-id="f7619-117">Your Excel data can exist as a comma-separated value (CSV) file in a storage folder, for example, in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="f7619-117">Your Excel data can exist as a comma-separated value (CSV) file in a storage folder, for example, in OneDrive.</span></span> 
  <span data-ttu-id="f7619-118">You can also use the same CSV file with the [flat-file connector](../logic-apps/logic-apps-enterprise-integration-flatfile.md).</span><span class="sxs-lookup"><span data-stu-id="f7619-118">You can also use the same CSV file with the [flat-file connector](../logic-apps/logic-apps-enterprise-integration-flatfile.md).</span></span>

* <span data-ttu-id="f7619-119">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="f7619-119">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span></span>

* <span data-ttu-id="f7619-120">The logic app where you want to access your Excel Online data.</span><span class="sxs-lookup"><span data-stu-id="f7619-120">The logic app where you want to access your Excel Online data.</span></span> <span data-ttu-id="f7619-121">This connector provides only actions, so to start your logic app, select a separate trigger, for example, the **Recurrence** trigger.</span><span class="sxs-lookup"><span data-stu-id="f7619-121">This connector provides only actions, so to start your logic app, select a separate trigger, for example, the **Recurrence** trigger.</span></span>

## <a name="add-excel-action"></a><span data-ttu-id="f7619-122">Add Excel action</span><span class="sxs-lookup"><span data-stu-id="f7619-122">Add Excel action</span></span>

1. <span data-ttu-id="f7619-123">In the [Azure portal](https://portal.azure.com), open your logic app in the Logic App Designer, if not already open.</span><span class="sxs-lookup"><span data-stu-id="f7619-123">In the [Azure portal](https://portal.azure.com), open your logic app in the Logic App Designer, if not already open.</span></span>

1. <span data-ttu-id="f7619-124">Under the trigger, choose **New step**.</span><span class="sxs-lookup"><span data-stu-id="f7619-124">Under the trigger, choose **New step**.</span></span>

1. <span data-ttu-id="f7619-125">In the search box, enter "excel" as your filter.</span><span class="sxs-lookup"><span data-stu-id="f7619-125">In the search box, enter "excel" as your filter.</span></span> <span data-ttu-id="f7619-126">Under the actions list, select the action you want.</span><span class="sxs-lookup"><span data-stu-id="f7619-126">Under the actions list, select the action you want.</span></span>

1. <span data-ttu-id="f7619-127">If prompted to sign in to your Office 365 account, choose **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="f7619-127">If prompted to sign in to your Office 365 account, choose **Sign in**.</span></span> 

   <span data-ttu-id="f7619-128">Your credentials authorize your logic app to create a connection to Excel Online and access your data.</span><span class="sxs-lookup"><span data-stu-id="f7619-128">Your credentials authorize your logic app to create a connection to Excel Online and access your data.</span></span>

1. <span data-ttu-id="f7619-129">Continue providing the necessary details for the selected action and building your logic app's workflow.</span><span class="sxs-lookup"><span data-stu-id="f7619-129">Continue providing the necessary details for the selected action and building your logic app's workflow.</span></span>

## <a name="connector-reference"></a><span data-ttu-id="f7619-130">Connector reference</span><span class="sxs-lookup"><span data-stu-id="f7619-130">Connector reference</span></span>

<span data-ttu-id="f7619-131">For technical details, such as actions and limits, described by the connectors' Swagger files, see these connector reference pages:</span><span class="sxs-lookup"><span data-stu-id="f7619-131">For technical details, such as actions and limits, described by the connectors' Swagger files, see these connector reference pages:</span></span>

* [<span data-ttu-id="f7619-132">Excel Online for Business</span><span class="sxs-lookup"><span data-stu-id="f7619-132">Excel Online for Business</span></span>](/connectors/excelonlinebusiness/) 
* [<span data-ttu-id="f7619-133">Excel Online for OneDrive</span><span class="sxs-lookup"><span data-stu-id="f7619-133">Excel Online for OneDrive</span></span>](/connectors/excelonline/) 

## <a name="get-support"></a><span data-ttu-id="f7619-134">Get support</span><span class="sxs-lookup"><span data-stu-id="f7619-134">Get support</span></span>

* <span data-ttu-id="f7619-135">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="f7619-135">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="f7619-136">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="f7619-136">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7619-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="f7619-137">Next steps</span></span>

* <span data-ttu-id="f7619-138">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="f7619-138">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span></span>
