---
title: Create workflows from templates - Azure Logic Apps | Microsoft Docs
description: Get started - create workflows quickly by using Azure Logic App templates to connect apps and integrate data.
author: kevinlam1
manager: anneta
editor: ''
services: logic-apps
documentationcenter: ''
ms.assetid: 3656acfb-eefd-4e75-b5d2-73da56c424c9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: klam
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b44d231c629df7729c78a97a570886df7b28fb77
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660706"
---
# <a name="configure-a-workflow-using-a-pre-built-template-or-pattern-to-get-started-quickly"></a><span data-ttu-id="c44f4-103">Configure a workflow using a pre-built template or pattern to get started quickly</span><span class="sxs-lookup"><span data-stu-id="c44f4-103">Configure a workflow using a pre-built template or pattern to get started quickly</span></span>

## <a name="what-are-logic-app-templates"></a><span data-ttu-id="c44f4-104">What are logic app templates</span><span class="sxs-lookup"><span data-stu-id="c44f4-104">What are logic app templates</span></span>
<span data-ttu-id="c44f4-105">A logic app template is a pre-built logic app that you can use to quickly get started creating your own workflow.</span><span class="sxs-lookup"><span data-stu-id="c44f4-105">A logic app template is a pre-built logic app that you can use to quickly get started creating your own workflow.</span></span> 

<span data-ttu-id="c44f4-106">These templates are a good way to discover various patterns that can be built using logic apps.</span><span class="sxs-lookup"><span data-stu-id="c44f4-106">These templates are a good way to discover various patterns that can be built using logic apps.</span></span> <span data-ttu-id="c44f4-107">You can either use these templates as-is or modify them to fit your scenario.</span><span class="sxs-lookup"><span data-stu-id="c44f4-107">You can either use these templates as-is or modify them to fit your scenario.</span></span>

## <a name="overview-of-available-templates"></a><span data-ttu-id="c44f4-108">Overview of available templates</span><span class="sxs-lookup"><span data-stu-id="c44f4-108">Overview of available templates</span></span>
<span data-ttu-id="c44f4-109">There are many available templates currently published in the logic app platform.</span><span class="sxs-lookup"><span data-stu-id="c44f4-109">There are many available templates currently published in the logic app platform.</span></span> <span data-ttu-id="c44f4-110">Some example categories, as well as the type of connectors used in them, are listed below.</span><span class="sxs-lookup"><span data-stu-id="c44f4-110">Some example categories, as well as the type of connectors used in them, are listed below.</span></span>

### <a name="enterprise-cloud-templates"></a><span data-ttu-id="c44f4-111">Enterprise cloud templates</span><span class="sxs-lookup"><span data-stu-id="c44f4-111">Enterprise cloud templates</span></span>
<span data-ttu-id="c44f4-112">Templates that integrate Dynamics CRM, Salesforce, Box, Azure Blob, and other connectors for your enterprise cloud needs.</span><span class="sxs-lookup"><span data-stu-id="c44f4-112">Templates that integrate Dynamics CRM, Salesforce, Box, Azure Blob, and other connectors for your enterprise cloud needs.</span></span> <span data-ttu-id="c44f4-113">Some examples of what can be done with these templates include organizing your leads and backing up your corporate file data.</span><span class="sxs-lookup"><span data-stu-id="c44f4-113">Some examples of what can be done with these templates include organizing your leads and backing up your corporate file data.</span></span>

### <a name="enterprise-integration-pack-templates"></a><span data-ttu-id="c44f4-114">Enterprise integration pack templates</span><span class="sxs-lookup"><span data-stu-id="c44f4-114">Enterprise integration pack templates</span></span>
<span data-ttu-id="c44f4-115">Configurations of VETER (validate, extract, transform, enrich, route) pipelines, receiving an X12 EDI document over AS2 and transforming it to XML, as well as X12 and AS2 message handling.</span><span class="sxs-lookup"><span data-stu-id="c44f4-115">Configurations of VETER (validate, extract, transform, enrich, route) pipelines, receiving an X12 EDI document over AS2 and transforming it to XML, as well as X12 and AS2 message handling.</span></span>

### <a name="protocol-pattern-templates"></a><span data-ttu-id="c44f4-116">Protocol pattern templates</span><span class="sxs-lookup"><span data-stu-id="c44f4-116">Protocol pattern templates</span></span>
<span data-ttu-id="c44f4-117">These templates consist of logic apps that contain protocol patterns such as request-response over HTTP as well as integrations across FTP and SFTP.</span><span class="sxs-lookup"><span data-stu-id="c44f4-117">These templates consist of logic apps that contain protocol patterns such as request-response over HTTP as well as integrations across FTP and SFTP.</span></span> <span data-ttu-id="c44f4-118">Use these as they exist, or as a basis for creating more complex protocol patterns.</span><span class="sxs-lookup"><span data-stu-id="c44f4-118">Use these as they exist, or as a basis for creating more complex protocol patterns.</span></span>  

### <a name="personal-productivity-templates"></a><span data-ttu-id="c44f4-119">Personal productivity templates</span><span class="sxs-lookup"><span data-stu-id="c44f4-119">Personal productivity templates</span></span>
<span data-ttu-id="c44f4-120">Patterns to help improve personal productivity include templates that set daily reminders, turn important work items into to-do lists, and automate lengthy tasks down to a single user approval step.</span><span class="sxs-lookup"><span data-stu-id="c44f4-120">Patterns to help improve personal productivity include templates that set daily reminders, turn important work items into to-do lists, and automate lengthy tasks down to a single user approval step.</span></span>

### <a name="consumer-cloud-templates"></a><span data-ttu-id="c44f4-121">Consumer cloud templates</span><span class="sxs-lookup"><span data-stu-id="c44f4-121">Consumer cloud templates</span></span>
<span data-ttu-id="c44f4-122">Simple templates that integrate with social media services such as Twitter, Slack, and email, ultimately capable of strengthening social media marketing initiatives.</span><span class="sxs-lookup"><span data-stu-id="c44f4-122">Simple templates that integrate with social media services such as Twitter, Slack, and email, ultimately capable of strengthening social media marketing initiatives.</span></span> <span data-ttu-id="c44f4-123">These also include templates such as cloudy copying, which can help increase productivity by saving time spent on traditionally repetitive tasks.</span><span class="sxs-lookup"><span data-stu-id="c44f4-123">These also include templates such as cloudy copying, which can help increase productivity by saving time spent on traditionally repetitive tasks.</span></span> 

## <a name="how-to-create-a-logic-app-using-a-template"></a><span data-ttu-id="c44f4-124">How to create a logic app using a template</span><span class="sxs-lookup"><span data-stu-id="c44f4-124">How to create a logic app using a template</span></span>
<span data-ttu-id="c44f4-125">To get started using a logic app template, go into the logic app designer.</span><span class="sxs-lookup"><span data-stu-id="c44f4-125">To get started using a logic app template, go into the logic app designer.</span></span> <span data-ttu-id="c44f4-126">If you're entering the designer by opening an existing logic app, the logic app automatically loads in your designer view.</span><span class="sxs-lookup"><span data-stu-id="c44f4-126">If you're entering the designer by opening an existing logic app, the logic app automatically loads in your designer view.</span></span> <span data-ttu-id="c44f4-127">However, if you're creating a new logic app, you see the screen below.</span><span class="sxs-lookup"><span data-stu-id="c44f4-127">However, if you're creating a new logic app, you see the screen below.</span></span>  
 ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-logic-templates/template7.png)  

<span data-ttu-id="c44f4-128">From this screen, you can either choose to start with a blank logic app or a pre-built template.</span><span class="sxs-lookup"><span data-stu-id="c44f4-128">From this screen, you can either choose to start with a blank logic app or a pre-built template.</span></span> <span data-ttu-id="c44f4-129">If you select one of the templates, you are provided with additional information.</span><span class="sxs-lookup"><span data-stu-id="c44f4-129">If you select one of the templates, you are provided with additional information.</span></span> <span data-ttu-id="c44f4-130">In this example, we use the *When a new file is created in Dropbox, copy it to OneDrive* template.</span><span class="sxs-lookup"><span data-stu-id="c44f4-130">In this example, we use the *When a new file is created in Dropbox, copy it to OneDrive* template.</span></span>  
 ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-logic-templates/template2.png)  

<span data-ttu-id="c44f4-131">If you choose to use the template, just select the *use this template* button.</span><span class="sxs-lookup"><span data-stu-id="c44f4-131">If you choose to use the template, just select the *use this template* button.</span></span> <span data-ttu-id="c44f4-132">You'll be asked to sign in to your accounts based on which connectors the template utilizes.</span><span class="sxs-lookup"><span data-stu-id="c44f4-132">You'll be asked to sign in to your accounts based on which connectors the template utilizes.</span></span> <span data-ttu-id="c44f4-133">Or, if you've previously established a connection with these connectors, you can select continue as seen below.</span><span class="sxs-lookup"><span data-stu-id="c44f4-133">Or, if you've previously established a connection with these connectors, you can select continue as seen below.</span></span>  
 ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-logic-templates/template3.png)  

<span data-ttu-id="c44f4-134">After establishing the connection and selecting *continue*, the logic app opens in designer view.</span><span class="sxs-lookup"><span data-stu-id="c44f4-134">After establishing the connection and selecting *continue*, the logic app opens in designer view.</span></span>  
 ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-logic-templates/template4.png)  

<span data-ttu-id="c44f4-135">In the example above, as is the case with many templates, some of the mandatory property fields may be filled out within the connectors; however, some might still require a value before being able to properly deploy the logic app.</span><span class="sxs-lookup"><span data-stu-id="c44f4-135">In the example above, as is the case with many templates, some of the mandatory property fields may be filled out within the connectors; however, some might still require a value before being able to properly deploy the logic app.</span></span> <span data-ttu-id="c44f4-136">If you try to deploy without entering some of the missing fields, you'll be notified with an error message.</span><span class="sxs-lookup"><span data-stu-id="c44f4-136">If you try to deploy without entering some of the missing fields, you'll be notified with an error message.</span></span>

<span data-ttu-id="c44f4-137">If you wish to return to the template viewer, select the *Templates* button in the top navigation bar.</span><span class="sxs-lookup"><span data-stu-id="c44f4-137">If you wish to return to the template viewer, select the *Templates* button in the top navigation bar.</span></span> <span data-ttu-id="c44f4-138">By switching back to the template viewer, you lose any unsaved progress.</span><span class="sxs-lookup"><span data-stu-id="c44f4-138">By switching back to the template viewer, you lose any unsaved progress.</span></span> <span data-ttu-id="c44f4-139">Prior to switching back into template viewer, you'll see a warning message notifying you of this.</span><span class="sxs-lookup"><span data-stu-id="c44f4-139">Prior to switching back into template viewer, you'll see a warning message notifying you of this.</span></span>  
 ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-logic-templates/template5.png)  

## <a name="how-to-deploy-a-logic-app-created-from-a-template"></a><span data-ttu-id="c44f4-140">How to deploy a logic app created from a template</span><span class="sxs-lookup"><span data-stu-id="c44f4-140">How to deploy a logic app created from a template</span></span>
<span data-ttu-id="c44f4-141">Once you have loaded your template and made any desired changes, select the save button in the upper left corner.</span><span class="sxs-lookup"><span data-stu-id="c44f4-141">Once you have loaded your template and made any desired changes, select the save button in the upper left corner.</span></span> <span data-ttu-id="c44f4-142">This saves and publishes your logic app.</span><span class="sxs-lookup"><span data-stu-id="c44f4-142">This saves and publishes your logic app.</span></span>  
 ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-logic-templates/template6.png)  

<span data-ttu-id="c44f4-143">If you would like more information on how to add more steps into an existing logic app template, or make edits in general, read more at [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c44f4-143">If you would like more information on how to add more steps into an existing logic app template, or make edits in general, read more at [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>







