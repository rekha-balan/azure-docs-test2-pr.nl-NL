---
title: Connect to SendGrid from Azure Logic Apps | Microsoft Docs
description: Automate tasks and workflows that send emails and manage mailing lists in SendGrid by using Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.assetid: bc4f1fc2-824c-4ed7-8de8-e82baff3b746
ms.topic: article
tags: connectors
ms.date: 08/24/2018
ms.openlocfilehash: c8747210a77879d551e323a7c0e46a9ab013fa3f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44775781"
---
# <a name="send-emails-and-manage-mailing-lists-in-sendgrid-by-using-azure-logic-apps"></a><span data-ttu-id="4bc10-103">Send emails and manage mailing lists in SendGrid by using Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="4bc10-103">Send emails and manage mailing lists in SendGrid by using Azure Logic Apps</span></span>

<span data-ttu-id="4bc10-104">With Azure Logic Apps and the SendGrid connector, you can create automated tasks and workflows that send emails and manage your recipient lists, for example:</span><span class="sxs-lookup"><span data-stu-id="4bc10-104">With Azure Logic Apps and the SendGrid connector, you can create automated tasks and workflows that send emails and manage your recipient lists, for example:</span></span>

* <span data-ttu-id="4bc10-105">Send email.</span><span class="sxs-lookup"><span data-stu-id="4bc10-105">Send email.</span></span>
* <span data-ttu-id="4bc10-106">Add recipients to lists.</span><span class="sxs-lookup"><span data-stu-id="4bc10-106">Add recipients to lists.</span></span>
* <span data-ttu-id="4bc10-107">Get, add, and manage global suppression.</span><span class="sxs-lookup"><span data-stu-id="4bc10-107">Get, add, and manage global suppression.</span></span>

<span data-ttu-id="4bc10-108">You can use SendGrid actions in your logic apps to perform these tasks.</span><span class="sxs-lookup"><span data-stu-id="4bc10-108">You can use SendGrid actions in your logic apps to perform these tasks.</span></span> <span data-ttu-id="4bc10-109">You can also have other actions use the output from SendGrid actions.</span><span class="sxs-lookup"><span data-stu-id="4bc10-109">You can also have other actions use the output from SendGrid actions.</span></span> 

<span data-ttu-id="4bc10-110">This connector provides only actions, so to start your logic app, use a separate trigger, such as a **Recurrence** trigger.</span><span class="sxs-lookup"><span data-stu-id="4bc10-110">This connector provides only actions, so to start your logic app, use a separate trigger, such as a **Recurrence** trigger.</span></span> <span data-ttu-id="4bc10-111">For example, if you regularly add recipients to your lists, you can send email about recipients and lists using the Office 365 Outlook connector or Outlook.com connector.</span><span class="sxs-lookup"><span data-stu-id="4bc10-111">For example, if you regularly add recipients to your lists, you can send email about recipients and lists using the Office 365 Outlook connector or Outlook.com connector.</span></span>
<span data-ttu-id="4bc10-112">If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)</span><span class="sxs-lookup"><span data-stu-id="4bc10-112">If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4bc10-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4bc10-113">Prerequisites</span></span>

* <span data-ttu-id="4bc10-114">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="4bc10-114">An Azure subscription.</span></span> <span data-ttu-id="4bc10-115">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="4bc10-115">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span> 

* <span data-ttu-id="4bc10-116">A [SendGrid account](https://www.sendgrid.com/) and a [SendGrid API key](https://sendgrid.com/docs/ui/account-and-settings/api-keys/)</span><span class="sxs-lookup"><span data-stu-id="4bc10-116">A [SendGrid account](https://www.sendgrid.com/) and a [SendGrid API key](https://sendgrid.com/docs/ui/account-and-settings/api-keys/)</span></span>

   <span data-ttu-id="4bc10-117">Your API key authorizes your logic app to create  a connection and access your SendGrid account.</span><span class="sxs-lookup"><span data-stu-id="4bc10-117">Your API key authorizes your logic app to create  a connection and access your SendGrid account.</span></span>

* <span data-ttu-id="4bc10-118">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="4bc10-118">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span></span>

* <span data-ttu-id="4bc10-119">The logic app where you want to access your SendGrid account.</span><span class="sxs-lookup"><span data-stu-id="4bc10-119">The logic app where you want to access your SendGrid account.</span></span> <span data-ttu-id="4bc10-120">To use a SendGrid action, start your logic app with another trigger, for example, the **Recurrence** trigger.</span><span class="sxs-lookup"><span data-stu-id="4bc10-120">To use a SendGrid action, start your logic app with another trigger, for example, the **Recurrence** trigger.</span></span>

## <a name="connect-to-sendgrid"></a><span data-ttu-id="4bc10-121">Connect to SendGrid</span><span class="sxs-lookup"><span data-stu-id="4bc10-121">Connect to SendGrid</span></span>

[!INCLUDE [Create connection general intro](../../includes/connectors-create-connection-general-intro.md)]

1. <span data-ttu-id="4bc10-122">Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.</span><span class="sxs-lookup"><span data-stu-id="4bc10-122">Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.</span></span>

1. <span data-ttu-id="4bc10-123">Choose a path:</span><span class="sxs-lookup"><span data-stu-id="4bc10-123">Choose a path:</span></span> 

   * <span data-ttu-id="4bc10-124">Under the last step where you want to add an action, choose **New step**.</span><span class="sxs-lookup"><span data-stu-id="4bc10-124">Under the last step where you want to add an action, choose **New step**.</span></span> 

     <span data-ttu-id="4bc10-125">-or-</span><span class="sxs-lookup"><span data-stu-id="4bc10-125">-or-</span></span>

   * <span data-ttu-id="4bc10-126">Between the steps where you want to add an action, move your pointer over the arrow between steps.</span><span class="sxs-lookup"><span data-stu-id="4bc10-126">Between the steps where you want to add an action, move your pointer over the arrow between steps.</span></span> 
   <span data-ttu-id="4bc10-127">Choose the plus sign (**+**) that appears, and then select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="4bc10-127">Choose the plus sign (**+**) that appears, and then select **Add an action**.</span></span>

1. <span data-ttu-id="4bc10-128">In the search box, enter "sendgrid" as your filter.</span><span class="sxs-lookup"><span data-stu-id="4bc10-128">In the search box, enter "sendgrid" as your filter.</span></span> <span data-ttu-id="4bc10-129">Under the actions list, select the action you want.</span><span class="sxs-lookup"><span data-stu-id="4bc10-129">Under the actions list, select the action you want.</span></span>

1. <span data-ttu-id="4bc10-130">Provide a name for your connection.</span><span class="sxs-lookup"><span data-stu-id="4bc10-130">Provide a name for your connection.</span></span> 

1. <span data-ttu-id="4bc10-131">Enter your SendGrid API key, and then choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="4bc10-131">Enter your SendGrid API key, and then choose **Create**.</span></span>

1. <span data-ttu-id="4bc10-132">Provide the necessary details for your selected action and continue building your logic app's workflow.</span><span class="sxs-lookup"><span data-stu-id="4bc10-132">Provide the necessary details for your selected action and continue building your logic app's workflow.</span></span>

## <a name="connector-reference"></a><span data-ttu-id="4bc10-133">Connector reference</span><span class="sxs-lookup"><span data-stu-id="4bc10-133">Connector reference</span></span>

<span data-ttu-id="4bc10-134">For technical details about triggers, actions, and limits, which are described by the connector's OpenAPI (formerly Swagger) description, review the connector's [reference page](/connectors/sendgrid/).</span><span class="sxs-lookup"><span data-stu-id="4bc10-134">For technical details about triggers, actions, and limits, which are described by the connector's OpenAPI (formerly Swagger) description, review the connector's [reference page](/connectors/sendgrid/).</span></span>

## <a name="get-support"></a><span data-ttu-id="4bc10-135">Get support</span><span class="sxs-lookup"><span data-stu-id="4bc10-135">Get support</span></span>

* <span data-ttu-id="4bc10-136">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="4bc10-136">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="4bc10-137">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="4bc10-137">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bc10-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="4bc10-138">Next steps</span></span>

* <span data-ttu-id="4bc10-139">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="4bc10-139">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span></span>