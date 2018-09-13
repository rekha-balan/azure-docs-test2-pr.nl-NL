---
title: Vertically scale Azure virtual machine with Azure Automation | Microsoft Docs
description: How to vertically scale a Linux Virtual Machine in response to monitoring alerts with Azure Automation
services: virtual-machines-linux
documentationcenter: ''
author: singhkays
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: dcee199e-fa25-44d5-9b25-df564cee9b45
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: singhkay
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a71da2d56628f30790abdc426984fa8f68863505
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661818"
---
# <a name="vertically-scale-azure-linux-virtual-machine-with-azure-automation"></a><span data-ttu-id="1bdb2-103">Vertically scale Azure Linux virtual machine with Azure Automation</span><span class="sxs-lookup"><span data-stu-id="1bdb2-103">Vertically scale Azure Linux virtual machine with Azure Automation</span></span>
<span data-ttu-id="1bdb2-104">Vertical scaling is the process of increasing or decreasing the resources of a machine in response to the workload.</span><span class="sxs-lookup"><span data-stu-id="1bdb2-104">Vertical scaling is the process of increasing or decreasing the resources of a machine in response to the workload.</span></span> <span data-ttu-id="1bdb2-105">In Azure this can be accomplished by changing the size of the Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="1bdb2-105">In Azure this can be accomplished by changing the size of the Virtual Machine.</span></span> <span data-ttu-id="1bdb2-106">This can help in the following scenarios</span><span class="sxs-lookup"><span data-stu-id="1bdb2-106">This can help in the following scenarios</span></span>

* <span data-ttu-id="1bdb2-107">If the Virtual Machine is not being used frequently, you can resize it down to a smaller size to reduce your monthly costs</span><span class="sxs-lookup"><span data-stu-id="1bdb2-107">If the Virtual Machine is not being used frequently, you can resize it down to a smaller size to reduce your monthly costs</span></span>
* <span data-ttu-id="1bdb2-108">If the Virtual Machine is seeing a peak load, it can be resized to a larger size to increase its capacity</span><span class="sxs-lookup"><span data-stu-id="1bdb2-108">If the Virtual Machine is seeing a peak load, it can be resized to a larger size to increase its capacity</span></span>

<span data-ttu-id="1bdb2-109">The outline for the steps to accomplish this is as below</span><span class="sxs-lookup"><span data-stu-id="1bdb2-109">The outline for the steps to accomplish this is as below</span></span>

1. <span data-ttu-id="1bdb2-110">Setup Azure Automation to access your Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="1bdb2-110">Setup Azure Automation to access your Virtual Machines</span></span>
2. <span data-ttu-id="1bdb2-111">Import the Azure Automation Vertical Scale runbooks into your subscription</span><span class="sxs-lookup"><span data-stu-id="1bdb2-111">Import the Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="1bdb2-112">Add a webhook to your runbook</span><span class="sxs-lookup"><span data-stu-id="1bdb2-112">Add a webhook to your runbook</span></span>
4. <span data-ttu-id="1bdb2-113">Add an alert to your Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="1bdb2-113">Add an alert to your Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="1bdb2-114">Because of the size of the first Virtual Machine, the sizes it can be scaled to, may be limited due to the availability of the other sizes in the cluster current Virtual Machine is deployed in.</span><span class="sxs-lookup"><span data-stu-id="1bdb2-114">Because of the size of the first Virtual Machine, the sizes it can be scaled to, may be limited due to the availability of the other sizes in the cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="1bdb2-115">In the published automation runbooks used in this article we take care of this case and only scale within the below VM size pairs.</span><span class="sxs-lookup"><span data-stu-id="1bdb2-115">In the published automation runbooks used in this article we take care of this case and only scale within the below VM size pairs.</span></span> <span data-ttu-id="1bdb2-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up to Standard_G5 or scaled down to Basic_A0.</span><span class="sxs-lookup"><span data-stu-id="1bdb2-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up to Standard_G5 or scaled down to Basic_A0.</span></span>
> 
> | <span data-ttu-id="1bdb2-117">VM sizes scaling pair</span><span class="sxs-lookup"><span data-stu-id="1bdb2-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="1bdb2-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="1bdb2-118">Basic_A0</span></span> |<span data-ttu-id="1bdb2-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="1bdb2-119">Basic_A4</span></span> |
> | <span data-ttu-id="1bdb2-120">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="1bdb2-120">Standard_A0</span></span> |<span data-ttu-id="1bdb2-121">Standard_A4</span><span class="sxs-lookup"><span data-stu-id="1bdb2-121">Standard_A4</span></span> |
> | <span data-ttu-id="1bdb2-122">Standard_A5</span><span class="sxs-lookup"><span data-stu-id="1bdb2-122">Standard_A5</span></span> |<span data-ttu-id="1bdb2-123">Standard_A7</span><span class="sxs-lookup"><span data-stu-id="1bdb2-123">Standard_A7</span></span> |
> | <span data-ttu-id="1bdb2-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="1bdb2-124">Standard_A8</span></span> |<span data-ttu-id="1bdb2-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="1bdb2-125">Standard_A9</span></span> |
> | <span data-ttu-id="1bdb2-126">Standard_A10</span><span class="sxs-lookup"><span data-stu-id="1bdb2-126">Standard_A10</span></span> |<span data-ttu-id="1bdb2-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="1bdb2-127">Standard_A11</span></span> |
> | <span data-ttu-id="1bdb2-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="1bdb2-128">Standard_D1</span></span> |<span data-ttu-id="1bdb2-129">Standard_D4</span><span class="sxs-lookup"><span data-stu-id="1bdb2-129">Standard_D4</span></span> |
> | <span data-ttu-id="1bdb2-130">Standard_D11</span><span class="sxs-lookup"><span data-stu-id="1bdb2-130">Standard_D11</span></span> |<span data-ttu-id="1bdb2-131">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="1bdb2-131">Standard_D14</span></span> |
> | <span data-ttu-id="1bdb2-132">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="1bdb2-132">Standard_DS1</span></span> |<span data-ttu-id="1bdb2-133">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="1bdb2-133">Standard_DS4</span></span> |
> | <span data-ttu-id="1bdb2-134">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="1bdb2-134">Standard_DS11</span></span> |<span data-ttu-id="1bdb2-135">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="1bdb2-135">Standard_DS14</span></span> |
> | <span data-ttu-id="1bdb2-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="1bdb2-136">Standard_D1v2</span></span> |<span data-ttu-id="1bdb2-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="1bdb2-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="1bdb2-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="1bdb2-138">Standard_D11v2</span></span> |<span data-ttu-id="1bdb2-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="1bdb2-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="1bdb2-140">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="1bdb2-140">Standard_G1</span></span> |<span data-ttu-id="1bdb2-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="1bdb2-141">Standard_G5</span></span> |
> | <span data-ttu-id="1bdb2-142">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="1bdb2-142">Standard_GS1</span></span> |<span data-ttu-id="1bdb2-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="1bdb2-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-to-access-your-virtual-machines"></a><span data-ttu-id="1bdb2-144">Setup Azure Automation to access your Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="1bdb2-144">Setup Azure Automation to access your Virtual Machines</span></span>
<span data-ttu-id="1bdb2-145">The first thing you need to do is create an Azure Automation account that will host the runbooks used to scale the VM Scale Set instances.</span><span class="sxs-lookup"><span data-stu-id="1bdb2-145">The first thing you need to do is create an Azure Automation account that will host the runbooks used to scale the VM Scale Set instances.</span></span> <span data-ttu-id="1bdb2-146">Recently the Automation service introduced the "Run As account" feature which makes setting up the Service Principal for automatically running the runbooks on the user's behalf very easy.</span><span class="sxs-lookup"><span data-stu-id="1bdb2-146">Recently the Automation service introduced the "Run As account" feature which makes setting up the Service Principal for automatically running the runbooks on the user's behalf very easy.</span></span> <span data-ttu-id="1bdb2-147">You can read more about this in the article below:</span><span class="sxs-lookup"><span data-stu-id="1bdb2-147">You can read more about this in the article below:</span></span>

* [<span data-ttu-id="1bdb2-148">Authenticate Runbooks with Azure Run As account</span><span class="sxs-lookup"><span data-stu-id="1bdb2-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-the-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="1bdb2-149">Import the Azure Automation Vertical Scale runbooks into your subscription</span><span class="sxs-lookup"><span data-stu-id="1bdb2-149">Import the Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="1bdb2-150">The runbooks that are needed for Vertically Scaling your Virtual Machine are already published in the Azure Automation Runbook Gallery.</span><span class="sxs-lookup"><span data-stu-id="1bdb2-150">The runbooks that are needed for Vertically Scaling your Virtual Machine are already published in the Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="1bdb2-151">You will need to import them into your subscription.</span><span class="sxs-lookup"><span data-stu-id="1bdb2-151">You will need to import them into your subscription.</span></span> <span data-ttu-id="1bdb2-152">You can learn how to import runbooks by reading the following article.</span><span class="sxs-lookup"><span data-stu-id="1bdb2-152">You can learn how to import runbooks by reading the following article.</span></span>

* [<span data-ttu-id="1bdb2-153">Runbook and module galleries for Azure Automation</span><span class="sxs-lookup"><span data-stu-id="1bdb2-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="1bdb2-154">The runbooks that need to be imported are shown in the image below</span><span class="sxs-lookup"><span data-stu-id="1bdb2-154">The runbooks that need to be imported are shown in the image below</span></span>

![Import runbooks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-to-your-runbook"></a><span data-ttu-id="1bdb2-156">Add a webhook to your runbook</span><span class="sxs-lookup"><span data-stu-id="1bdb2-156">Add a webhook to your runbook</span></span>
<span data-ttu-id="1bdb2-157">Once you've imported the runbooks you'll need to add a webhook to the runbook so it can be triggered by an alert from a Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="1bdb2-157">Once you've imported the runbooks you'll need to add a webhook to the runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="1bdb2-158">The details of creating a webhook for your Runbook can be read here</span><span class="sxs-lookup"><span data-stu-id="1bdb2-158">The details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="1bdb2-159">Azure Automation webhooks</span><span class="sxs-lookup"><span data-stu-id="1bdb2-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="1bdb2-160">Make sure you copy the webhook before closing the webhook dialog as you will need this in the next section.</span><span class="sxs-lookup"><span data-stu-id="1bdb2-160">Make sure you copy the webhook before closing the webhook dialog as you will need this in the next section.</span></span>

## <a name="add-an-alert-to-your-virtual-machine"></a><span data-ttu-id="1bdb2-161">Add an alert to your Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="1bdb2-161">Add an alert to your Virtual Machine</span></span>
1. <span data-ttu-id="1bdb2-162">Select Virtual Machine settings</span><span class="sxs-lookup"><span data-stu-id="1bdb2-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="1bdb2-163">Select "Alert rules"</span><span class="sxs-lookup"><span data-stu-id="1bdb2-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="1bdb2-164">Select "Add alert"</span><span class="sxs-lookup"><span data-stu-id="1bdb2-164">Select "Add alert"</span></span>
4. <span data-ttu-id="1bdb2-165">Select a metric to fire the alert on</span><span class="sxs-lookup"><span data-stu-id="1bdb2-165">Select a metric to fire the alert on</span></span>
5. <span data-ttu-id="1bdb2-166">Select a condition, which when fulfilled will cause the alert to fire</span><span class="sxs-lookup"><span data-stu-id="1bdb2-166">Select a condition, which when fulfilled will cause the alert to fire</span></span>
6. <span data-ttu-id="1bdb2-167">Select a threshold for the condition in Step 5.</span><span class="sxs-lookup"><span data-stu-id="1bdb2-167">Select a threshold for the condition in Step 5.</span></span> <span data-ttu-id="1bdb2-168">to be fulfilled</span><span class="sxs-lookup"><span data-stu-id="1bdb2-168">to be fulfilled</span></span>
7. <span data-ttu-id="1bdb2-169">Select a period over which the monitoring service will check for the condition and threshold in Steps 5 & 6</span><span class="sxs-lookup"><span data-stu-id="1bdb2-169">Select a period over which the monitoring service will check for the condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="1bdb2-170">Paste in the webhook you copied from the previous section.</span><span class="sxs-lookup"><span data-stu-id="1bdb2-170">Paste in the webhook you copied from the previous section.</span></span>

![Add Alert to Virtual Machine 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/vertical-scaling-automation/add-alert-webhook-1.png)

![Add Alert to Virtual Machine 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/vertical-scaling-automation/add-alert-webhook-2.png)




