---
title: Manage logic apps in Visual Studio - Azure Logic Apps | Microsoft Docs
description: Manage logic apps and other Azure assets with Visual Studio Cloud Explorer
author: klam
manager: anneta
editor: ''
services: logic-apps
documentationcenter: ''
ms.assetid: ''
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 12/19/2016
ms.author: klam
ms.openlocfilehash: c6daeeff4ec463d070cac15aa11aeff35d75d217
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550342"
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a><span data-ttu-id="5cc07-103">Manage your logic apps with Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="5cc07-103">Manage your logic apps with Visual Studio Cloud Explorer</span></span>

<span data-ttu-id="5cc07-104">Although the [Azure portal](https://portal.azure.com/) offers a great way for you to design and manage Azure Logic Apps, you can manage many Azure assets, including logic apps, in Visual Studio when you use Visual Studio Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="5cc07-104">Although the [Azure portal](https://portal.azure.com/) offers a great way for you to design and manage Azure Logic Apps, you can manage many Azure assets, including logic apps, in Visual Studio when you use Visual Studio Cloud Explorer.</span></span> <span data-ttu-id="5cc07-105">You can browse published logic apps, and perform tasks like enable and disable your logic apps or edit and view run histories.</span><span class="sxs-lookup"><span data-stu-id="5cc07-105">You can browse published logic apps, and perform tasks like enable and disable your logic apps or edit and view run histories.</span></span> 

## <a name="installation-steps"></a><span data-ttu-id="5cc07-106">Installation steps</span><span class="sxs-lookup"><span data-stu-id="5cc07-106">Installation steps</span></span>

<span data-ttu-id="5cc07-107">To install and configure Visual Studio tools for Azure Logic Apps, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="5cc07-107">To install and configure Visual Studio tools for Azure Logic Apps, follow these steps.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="5cc07-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5cc07-108">Prerequisites</span></span>

* [<span data-ttu-id="5cc07-109">Visual Studio 2015 or Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="5cc07-109">Visual Studio 2015 or Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="5cc07-110">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span><span class="sxs-lookup"><span data-stu-id="5cc07-110">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="5cc07-111">Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="5cc07-111">Visual Studio Cloud Explorer</span></span>](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* <span data-ttu-id="5cc07-112">Access to the web when using the embedded designer</span><span class="sxs-lookup"><span data-stu-id="5cc07-112">Access to the web when using the embedded designer</span></span>

### <a name="install-visual-studio-tools-for-logic-apps"></a><span data-ttu-id="5cc07-113">Install Visual Studio tools for Logic Apps</span><span class="sxs-lookup"><span data-stu-id="5cc07-113">Install Visual Studio tools for Logic Apps</span></span>

<span data-ttu-id="5cc07-114">After you install the prerequisites:</span><span class="sxs-lookup"><span data-stu-id="5cc07-114">After you install the prerequisites:</span></span>

1. <span data-ttu-id="5cc07-115">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5cc07-115">Open Visual Studio.</span></span> <span data-ttu-id="5cc07-116">On the **Tools** menu, select **Extensions and Updates**.</span><span class="sxs-lookup"><span data-stu-id="5cc07-116">On the **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="5cc07-117">Expand the **Online** category so you can search online.</span><span class="sxs-lookup"><span data-stu-id="5cc07-117">Expand the **Online** category so you can search online.</span></span>
3. <span data-ttu-id="5cc07-118">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="5cc07-118">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="5cc07-119">To download and install the extension, click **Download**.</span><span class="sxs-lookup"><span data-stu-id="5cc07-119">To download and install the extension, click **Download**.</span></span>
5. <span data-ttu-id="5cc07-120">Restart Visual Studio after installation.</span><span class="sxs-lookup"><span data-stu-id="5cc07-120">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="5cc07-121">You can also download Azure Logic Apps Tools for Visual Studio directly from the [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span><span class="sxs-lookup"><span data-stu-id="5cc07-121">You can also download Azure Logic Apps Tools for Visual Studio directly from the [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span></span>

## <a name="browse-for-logic-apps-in-cloud-explorer"></a><span data-ttu-id="5cc07-122">Browse for logic apps in Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="5cc07-122">Browse for logic apps in Cloud Explorer</span></span>

1.  <span data-ttu-id="5cc07-123">To open Cloud Explorer, on the **View** menu, choose **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="5cc07-123">To open Cloud Explorer, on the **View** menu, choose **Cloud Explorer**.</span></span>
2.  <span data-ttu-id="5cc07-124">Browse for your logic app, either by resource group or by resource type.</span><span class="sxs-lookup"><span data-stu-id="5cc07-124">Browse for your logic app, either by resource group or by resource type.</span></span> 

    <span data-ttu-id="5cc07-125">If you browse by resource type, select your Azure subscription, expand the Logic Apps section, then select a Logic App.</span><span class="sxs-lookup"><span data-stu-id="5cc07-125">If you browse by resource type, select your Azure subscription, expand the Logic Apps section, then select a Logic App.</span></span> 
    <span data-ttu-id="5cc07-126">You can either right-click a logic app, choose from the **Actions** menu at the bottom of Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="5cc07-126">You can either right-click a logic app, choose from the **Actions** menu at the bottom of Cloud Explorer.</span></span>

    ![Browse for your logic app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-app-designer"></a><span data-ttu-id="5cc07-128">Edit your logic app with Logic App Designer</span><span class="sxs-lookup"><span data-stu-id="5cc07-128">Edit your logic app with Logic App Designer</span></span>

<span data-ttu-id="5cc07-129">To open a currently deployed logic app in the same designer that you use in the Azure portal, right-click your logic app, and select **Open with Logic App Editor**.</span><span class="sxs-lookup"><span data-stu-id="5cc07-129">To open a currently deployed logic app in the same designer that you use in the Azure portal, right-click your logic app, and select **Open with Logic App Editor**.</span></span> 

<span data-ttu-id="5cc07-130">In the designer, you can edit your logic app, save your updates to the cloud, and start a new run by choosing **Run Trigger**.</span><span class="sxs-lookup"><span data-stu-id="5cc07-130">In the designer, you can edit your logic app, save your updates to the cloud, and start a new run by choosing **Run Trigger**.</span></span>

![Logic App Designer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-manage-from-vs/designer.png)

## <a name="browse-your-logic-app-run-history"></a><span data-ttu-id="5cc07-132">Browse your logic app run history</span><span class="sxs-lookup"><span data-stu-id="5cc07-132">Browse your logic app run history</span></span>

<span data-ttu-id="5cc07-133">To view the run history for your logic app, right-click your logic app, and select **Open run history**.</span><span class="sxs-lookup"><span data-stu-id="5cc07-133">To view the run history for your logic app, right-click your logic app, and select **Open run history**.</span></span> <span data-ttu-id="5cc07-134">To reorder your run history based on any of the properties shown, select the column header.</span><span class="sxs-lookup"><span data-stu-id="5cc07-134">To reorder your run history based on any of the properties shown, select the column header.</span></span>

![Run history](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-manage-from-vs/runs.png)

<span data-ttu-id="5cc07-136">To show the run history for an instance so you can see the run results, including the inputs and outputs from each step, double-click one of the run instances.</span><span class="sxs-lookup"><span data-stu-id="5cc07-136">To show the run history for an instance so you can see the run results, including the inputs and outputs from each step, double-click one of the run instances.</span></span>

![Run history results, inputs and outputs from steps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a><span data-ttu-id="5cc07-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="5cc07-138">Next steps</span></span>

*   <span data-ttu-id="5cc07-139">To get started with Azure Logic Apps, learn [how to create your first logic app in the Azure portal](logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="5cc07-139">To get started with Azure Logic Apps, learn [how to create your first logic app in the Azure portal](logic-apps-create-a-logic-app.md)</span></span>
* [<span data-ttu-id="5cc07-140">Design, build, and deploy logic apps in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5cc07-140">Design, build, and deploy logic apps in Visual Studio</span></span>](logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="5cc07-141">View common examples and scenarios</span><span class="sxs-lookup"><span data-stu-id="5cc07-141">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="5cc07-142">Learn how to automate business processes with Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="5cc07-142">Learn how to automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="5cc07-143">Learn how to integrate your systems with Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="5cc07-143">Learn how to integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)




