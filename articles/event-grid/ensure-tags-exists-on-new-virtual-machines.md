---
title: Integrate Azure Automation with Event Grid | Microsoft Docs
description: Learn how to automatically add a tag when a new VM is created and send a notification to Microsoft Teams.
keywords: automation, runbook, teams, event grid, virtual machine, VM
services: automation
author: eamonoreilly
manager: ''
ms.service: automation
ms.topic: tutorial
ms.workload: infrastructure-services
ms.date: 08/14/2018
ms.author: eamono
ms.openlocfilehash: a4356f38df017901ab219318463538003d3a979e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865991"
---
# <a name="integrate-azure-automation-with-event-grid-and-microsoft-teams"></a><span data-ttu-id="9d878-104">Integrate Azure Automation with Event Grid and Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="9d878-104">Integrate Azure Automation with Event Grid and Microsoft Teams</span></span>

<span data-ttu-id="9d878-105">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="9d878-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9d878-106">Import an Event Grid sample runbook.</span><span class="sxs-lookup"><span data-stu-id="9d878-106">Import an Event Grid sample runbook.</span></span>
> * <span data-ttu-id="9d878-107">Create an optional Microsoft Teams webhook.</span><span class="sxs-lookup"><span data-stu-id="9d878-107">Create an optional Microsoft Teams webhook.</span></span>
> * <span data-ttu-id="9d878-108">Create a webhook for the runbook.</span><span class="sxs-lookup"><span data-stu-id="9d878-108">Create a webhook for the runbook.</span></span>
> * <span data-ttu-id="9d878-109">Create an Event Grid subscription.</span><span class="sxs-lookup"><span data-stu-id="9d878-109">Create an Event Grid subscription.</span></span>
> * <span data-ttu-id="9d878-110">Create a VM that triggers the runbook.</span><span class="sxs-lookup"><span data-stu-id="9d878-110">Create a VM that triggers the runbook.</span></span>

<span data-ttu-id="9d878-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="9d878-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d878-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9d878-112">Prerequisites</span></span>

<span data-ttu-id="9d878-113">To complete this tutorial, an [Azure Automation account](../automation/automation-offering-get-started.md) is required to hold the runbook that is triggered from the Azure Event Grid subscription.</span><span class="sxs-lookup"><span data-stu-id="9d878-113">To complete this tutorial, an [Azure Automation account](../automation/automation-offering-get-started.md) is required to hold the runbook that is triggered from the Azure Event Grid subscription.</span></span>

* <span data-ttu-id="9d878-114">The `AzureRM.Tags` module needs to be loaded in your Automation Account, see [How to import modules in Azure Automation](../automation/automation-update-azure-modules.md) to learn how to import modules into Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="9d878-114">The `AzureRM.Tags` module needs to be loaded in your Automation Account, see [How to import modules in Azure Automation](../automation/automation-update-azure-modules.md) to learn how to import modules into Azure Automation.</span></span>

## <a name="import-an-event-grid-sample-runbook"></a><span data-ttu-id="9d878-115">Import an Event Grid sample runbook</span><span class="sxs-lookup"><span data-stu-id="9d878-115">Import an Event Grid sample runbook</span></span>

1. <span data-ttu-id="9d878-116">Select your Automation account, and select the **Runbooks** page.</span><span class="sxs-lookup"><span data-stu-id="9d878-116">Select your Automation account, and select the **Runbooks** page.</span></span>

   ![Select runbooks](./media/ensure-tags-exists-on-new-virtual-machines/select-runbooks.png)

2. <span data-ttu-id="9d878-118">Select the **Browse gallery** button.</span><span class="sxs-lookup"><span data-stu-id="9d878-118">Select the **Browse gallery** button.</span></span>

3. <span data-ttu-id="9d878-119">Search for **Event Grid**, and select **Integrating Azure Automation with Event grid**.</span><span class="sxs-lookup"><span data-stu-id="9d878-119">Search for **Event Grid**, and select **Integrating Azure Automation with Event grid**.</span></span>

    ![Import gallery runbook](media/ensure-tags-exists-on-new-virtual-machines/gallery-event-grid.png)

4. <span data-ttu-id="9d878-121">Select **Import** and name it **Watch-VMWrite**.</span><span class="sxs-lookup"><span data-stu-id="9d878-121">Select **Import** and name it **Watch-VMWrite**.</span></span>

5. <span data-ttu-id="9d878-122">After it has imported, select **Edit** to view the runbook source.</span><span class="sxs-lookup"><span data-stu-id="9d878-122">After it has imported, select **Edit** to view the runbook source.</span></span> <span data-ttu-id="9d878-123">Select the **Publish** button.</span><span class="sxs-lookup"><span data-stu-id="9d878-123">Select the **Publish** button.</span></span>

> [!NOTE]
> <span data-ttu-id="9d878-124">Line 74 in the script needs to have the line changed to `Update-AzureRmVM -ResourceGroupName $VMResourceGroup -VM $VM -Tag $Tag | Write-Verbose`.</span><span class="sxs-lookup"><span data-stu-id="9d878-124">Line 74 in the script needs to have the line changed to `Update-AzureRmVM -ResourceGroupName $VMResourceGroup -VM $VM -Tag $Tag | Write-Verbose`.</span></span> <span data-ttu-id="9d878-125">The `-Tags` parameter is now `-Tag`.</span><span class="sxs-lookup"><span data-stu-id="9d878-125">The `-Tags` parameter is now `-Tag`.</span></span>

## <a name="create-an-optional-microsoft-teams-webhook"></a><span data-ttu-id="9d878-126">Create an optional Microsoft Teams webhook</span><span class="sxs-lookup"><span data-stu-id="9d878-126">Create an optional Microsoft Teams webhook</span></span>

1. <span data-ttu-id="9d878-127">In Microsoft Teams, select **More Options** next to the channel name, and then select **Connectors**.</span><span class="sxs-lookup"><span data-stu-id="9d878-127">In Microsoft Teams, select **More Options** next to the channel name, and then select **Connectors**.</span></span>

    ![Microsoft Teams connections](media/ensure-tags-exists-on-new-virtual-machines/teams-webhook.png)

2. <span data-ttu-id="9d878-129">Scroll through the list of connectors to **Incoming Webhook**, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="9d878-129">Scroll through the list of connectors to **Incoming Webhook**, and select **Add**.</span></span>

3. <span data-ttu-id="9d878-130">Enter **AzureAutomationIntegration** for the name, and select **Create**.</span><span class="sxs-lookup"><span data-stu-id="9d878-130">Enter **AzureAutomationIntegration** for the name, and select **Create**.</span></span>

4. <span data-ttu-id="9d878-131">Copy the webhook to the clipboard, and save it.</span><span class="sxs-lookup"><span data-stu-id="9d878-131">Copy the webhook to the clipboard, and save it.</span></span> <span data-ttu-id="9d878-132">The webhook URL is used to send information to Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="9d878-132">The webhook URL is used to send information to Microsoft Teams.</span></span>

5. <span data-ttu-id="9d878-133">Select **Done** to save the webhook.</span><span class="sxs-lookup"><span data-stu-id="9d878-133">Select **Done** to save the webhook.</span></span>

## <a name="create-a-webhook-for-the-runbook"></a><span data-ttu-id="9d878-134">Create a webhook for the runbook</span><span class="sxs-lookup"><span data-stu-id="9d878-134">Create a webhook for the runbook</span></span>

1. <span data-ttu-id="9d878-135">Open the Watch-VMWrite runbook.</span><span class="sxs-lookup"><span data-stu-id="9d878-135">Open the Watch-VMWrite runbook.</span></span>

2. <span data-ttu-id="9d878-136">Select **Webhooks**, and select the **Add Webhook** button.</span><span class="sxs-lookup"><span data-stu-id="9d878-136">Select **Webhooks**, and select the **Add Webhook** button.</span></span>

3. <span data-ttu-id="9d878-137">Enter **WatchVMEventGrid** for the name.</span><span class="sxs-lookup"><span data-stu-id="9d878-137">Enter **WatchVMEventGrid** for the name.</span></span> <span data-ttu-id="9d878-138">Copy the URL to the clipboard, and save it.</span><span class="sxs-lookup"><span data-stu-id="9d878-138">Copy the URL to the clipboard, and save it.</span></span>

    ![Configure webhook name](media/ensure-tags-exists-on-new-virtual-machines/copy-url.png)

4. <span data-ttu-id="9d878-140">Select **Configure parameters and run settings**, and enter the Microsoft Teams webhook URL for **CHANNELURL**.</span><span class="sxs-lookup"><span data-stu-id="9d878-140">Select **Configure parameters and run settings**, and enter the Microsoft Teams webhook URL for **CHANNELURL**.</span></span> <span data-ttu-id="9d878-141">Leave **WEBHOOKDATA** blank.</span><span class="sxs-lookup"><span data-stu-id="9d878-141">Leave **WEBHOOKDATA** blank.</span></span>

    ![Configure webhook parameters](media/ensure-tags-exists-on-new-virtual-machines/configure-webhook-parameters.png)

5. <span data-ttu-id="9d878-143">Select **Create** to create the Automation runbook webhook.</span><span class="sxs-lookup"><span data-stu-id="9d878-143">Select **Create** to create the Automation runbook webhook.</span></span>

## <a name="create-an-event-grid-subscription"></a><span data-ttu-id="9d878-144">Create an Event Grid subscription</span><span class="sxs-lookup"><span data-stu-id="9d878-144">Create an Event Grid subscription</span></span>

1. <span data-ttu-id="9d878-145">On the **Automation Account** overview page, select **Event grid**.</span><span class="sxs-lookup"><span data-stu-id="9d878-145">On the **Automation Account** overview page, select **Event grid**.</span></span>

    ![Select Event Grid](media/ensure-tags-exists-on-new-virtual-machines/select-event-grid.png)

2. <span data-ttu-id="9d878-147">Click **+ Event Subscription**.</span><span class="sxs-lookup"><span data-stu-id="9d878-147">Click **+ Event Subscription**.</span></span>

3. <span data-ttu-id="9d878-148">Configure the subscription with the following information:</span><span class="sxs-lookup"><span data-stu-id="9d878-148">Configure the subscription with the following information:</span></span>

   * <span data-ttu-id="9d878-149">For **Topic Type**, select **Azure Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="9d878-149">For **Topic Type**, select **Azure Subscriptions**.</span></span>
   * <span data-ttu-id="9d878-150">Uncheck the **Subscribe to all event types** check box.</span><span class="sxs-lookup"><span data-stu-id="9d878-150">Uncheck the **Subscribe to all event types** check box.</span></span>
   * <span data-ttu-id="9d878-151">Enter **AzureAutomation** for the name.</span><span class="sxs-lookup"><span data-stu-id="9d878-151">Enter **AzureAutomation** for the name.</span></span>
   * <span data-ttu-id="9d878-152">In the **Defined Event Types** drop-down, uncheck all options except **Resource Write Success**.</span><span class="sxs-lookup"><span data-stu-id="9d878-152">In the **Defined Event Types** drop-down, uncheck all options except **Resource Write Success**.</span></span>
   * <span data-ttu-id="9d878-153">For **Endpoint Type**, select **Webhook**.</span><span class="sxs-lookup"><span data-stu-id="9d878-153">For **Endpoint Type**, select **Webhook**.</span></span>
   * <span data-ttu-id="9d878-154">Click **Select an endpoint**.</span><span class="sxs-lookup"><span data-stu-id="9d878-154">Click **Select an endpoint**.</span></span> <span data-ttu-id="9d878-155">On the **Select Web Hook** page that opens up, paste the webhook url you created for the Watch-VMWrite runbook.</span><span class="sxs-lookup"><span data-stu-id="9d878-155">On the **Select Web Hook** page that opens up, paste the webhook url you created for the Watch-VMWrite runbook.</span></span>
   * <span data-ttu-id="9d878-156">Under **FILTERS**, enter the subscription and resource group where you want to look for the new VMs created.</span><span class="sxs-lookup"><span data-stu-id="9d878-156">Under **FILTERS**, enter the subscription and resource group where you want to look for the new VMs created.</span></span> <span data-ttu-id="9d878-157">It should look like: `/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines`</span><span class="sxs-lookup"><span data-stu-id="9d878-157">It should look like: `/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines`</span></span>

4. <span data-ttu-id="9d878-158">Select **Create** to save the Event Grid subscription.</span><span class="sxs-lookup"><span data-stu-id="9d878-158">Select **Create** to save the Event Grid subscription.</span></span>

## <a name="create-a-vm-that-triggers-the-runbook"></a><span data-ttu-id="9d878-159">Create a VM that triggers the runbook</span><span class="sxs-lookup"><span data-stu-id="9d878-159">Create a VM that triggers the runbook</span></span>

1. <span data-ttu-id="9d878-160">Create a new VM in the resource group you specified in the Event Grid subscription prefix filter.</span><span class="sxs-lookup"><span data-stu-id="9d878-160">Create a new VM in the resource group you specified in the Event Grid subscription prefix filter.</span></span>

2. <span data-ttu-id="9d878-161">The Watch-VMWrite runbook should be called and a new tag added to the VM.</span><span class="sxs-lookup"><span data-stu-id="9d878-161">The Watch-VMWrite runbook should be called and a new tag added to the VM.</span></span>

    ![VM tag](media/ensure-tags-exists-on-new-virtual-machines/vm-tag.png)

3. <span data-ttu-id="9d878-163">A new message is sent to the Microsoft Teams channel.</span><span class="sxs-lookup"><span data-stu-id="9d878-163">A new message is sent to the Microsoft Teams channel.</span></span>

    ![Microsoft Teams notification](media/ensure-tags-exists-on-new-virtual-machines/teams-vm-message.png)

## <a name="next-steps"></a><span data-ttu-id="9d878-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="9d878-165">Next steps</span></span>

<span data-ttu-id="9d878-166">In this tutorial, you set up integration between Event Grid and Automation.</span><span class="sxs-lookup"><span data-stu-id="9d878-166">In this tutorial, you set up integration between Event Grid and Automation.</span></span> <span data-ttu-id="9d878-167">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="9d878-167">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9d878-168">Import an Event Grid sample runbook.</span><span class="sxs-lookup"><span data-stu-id="9d878-168">Import an Event Grid sample runbook.</span></span>
> * <span data-ttu-id="9d878-169">Create an optional Microsoft Teams webhook.</span><span class="sxs-lookup"><span data-stu-id="9d878-169">Create an optional Microsoft Teams webhook.</span></span>
> * <span data-ttu-id="9d878-170">Create a webhook for the runbook.</span><span class="sxs-lookup"><span data-stu-id="9d878-170">Create a webhook for the runbook.</span></span>
> * <span data-ttu-id="9d878-171">Create an Event Grid subscription.</span><span class="sxs-lookup"><span data-stu-id="9d878-171">Create an Event Grid subscription.</span></span>
> * <span data-ttu-id="9d878-172">Create a VM that triggers the runbook.</span><span class="sxs-lookup"><span data-stu-id="9d878-172">Create a VM that triggers the runbook.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9d878-173">Create and route custom events with Event Grid</span><span class="sxs-lookup"><span data-stu-id="9d878-173">Create and route custom events with Event Grid</span></span>](../event-grid/custom-event-quickstart.md)
