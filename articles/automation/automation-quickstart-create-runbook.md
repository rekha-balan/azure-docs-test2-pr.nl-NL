---
title: Azure Quickstart - Create an Azure Automation runbook | Microsoft Docs
description: Learn how to create an Azure Automation runbook
services: automation
author: csand-msft
ms.author: csand
ms.date: 12/14/2017
ms.topic: quickstart
ms.service: automation
ms.component: process-automation
ms.custom: mvc
ms.openlocfilehash: 4aafff81957943fc19f0f6d2fce8a41f7be58d16
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865199"
---
# <a name="create-an-azure-automation-runbook"></a><span data-ttu-id="ece23-103">Create an Azure Automation runbook</span><span class="sxs-lookup"><span data-stu-id="ece23-103">Create an Azure Automation runbook</span></span>

<span data-ttu-id="ece23-104">Azure Automation runbooks can be created through Azure.</span><span class="sxs-lookup"><span data-stu-id="ece23-104">Azure Automation runbooks can be created through Azure.</span></span> <span data-ttu-id="ece23-105">This method provides a browser-based user interface for creating Automation runbooks.</span><span class="sxs-lookup"><span data-stu-id="ece23-105">This method provides a browser-based user interface for creating Automation runbooks.</span></span> <span data-ttu-id="ece23-106">In this quickstart you walk through creating, editing, testing, and publishing an Automation PowerShell runbook.</span><span class="sxs-lookup"><span data-stu-id="ece23-106">In this quickstart you walk through creating, editing, testing, and publishing an Automation PowerShell runbook.</span></span>

<span data-ttu-id="ece23-107">If you don't have an Azure subscription, create a [free Azure account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="ece23-107">If you don't have an Azure subscription, create a [free Azure account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="ece23-108">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="ece23-108">Log in to Azure</span></span>

<span data-ttu-id="ece23-109">Log in to Azure at https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="ece23-109">Log in to Azure at https://portal.azure.com</span></span>

## <a name="create-runbook"></a><span data-ttu-id="ece23-110">Create runbook</span><span class="sxs-lookup"><span data-stu-id="ece23-110">Create runbook</span></span>

<span data-ttu-id="ece23-111">First, create a runbook.</span><span class="sxs-lookup"><span data-stu-id="ece23-111">First, create a runbook.</span></span> <span data-ttu-id="ece23-112">The sample runbook created in this quickstart outputs `Hello World` by default.</span><span class="sxs-lookup"><span data-stu-id="ece23-112">The sample runbook created in this quickstart outputs `Hello World` by default.</span></span>

1. <span data-ttu-id="ece23-113">Open your Automation account.</span><span class="sxs-lookup"><span data-stu-id="ece23-113">Open your Automation account.</span></span>

1. <span data-ttu-id="ece23-114">Click **Runbooks** under **PROCESS AUTOMATION**.</span><span class="sxs-lookup"><span data-stu-id="ece23-114">Click **Runbooks** under **PROCESS AUTOMATION**.</span></span> <span data-ttu-id="ece23-115">The list of runbooks is displayed.</span><span class="sxs-lookup"><span data-stu-id="ece23-115">The list of runbooks is displayed.</span></span>

1. <span data-ttu-id="ece23-116">Click the **Add a runbook** button found at the top of the list.</span><span class="sxs-lookup"><span data-stu-id="ece23-116">Click the **Add a runbook** button found at the top of the list.</span></span> <span data-ttu-id="ece23-117">On the **Add Runbook** page, select **Quick Create**.</span><span class="sxs-lookup"><span data-stu-id="ece23-117">On the **Add Runbook** page, select **Quick Create**.</span></span>

1. <span data-ttu-id="ece23-118">Enter "Hello-World" for the runbook **Name**, and select **PowerShell** for **Runbook type**.</span><span class="sxs-lookup"><span data-stu-id="ece23-118">Enter "Hello-World" for the runbook **Name**, and select **PowerShell** for **Runbook type**.</span></span> <span data-ttu-id="ece23-119">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ece23-119">Click **Create**.</span></span>

   ![Enter information about your Automation runbook in the page](./media/automation-quickstart-create-runbook/automation-create-runbook-configure.png)

1. <span data-ttu-id="ece23-121">The runbook is created and the **Edit PowerShell Runbook** page opens.</span><span class="sxs-lookup"><span data-stu-id="ece23-121">The runbook is created and the **Edit PowerShell Runbook** page opens.</span></span>

    ![Author PowerShell script in the runbook editor](./media/automation-quickstart-create-runbook/automation-edit-runbook-empty.png)

1. <span data-ttu-id="ece23-123">Type or copy and paste the following code into the edit pane.</span><span class="sxs-lookup"><span data-stu-id="ece23-123">Type or copy and paste the following code into the edit pane.</span></span> <span data-ttu-id="ece23-124">It creates an optional input parameter called "Name" with a default value of "World", and outputs a string that uses this input value:</span><span class="sxs-lookup"><span data-stu-id="ece23-124">It creates an optional input parameter called "Name" with a default value of "World", and outputs a string that uses this input value:</span></span>
   
   ```powershell-interactive
   param
   (
       [Parameter(Mandatory=$false)]
       [String] $Name = "World"
   )

   "Hello $Name!"
   ```

1. <span data-ttu-id="ece23-125">Click **Save**, to save a draft copy of the runbook.</span><span class="sxs-lookup"><span data-stu-id="ece23-125">Click **Save**, to save a draft copy of the runbook.</span></span>

    ![Author PowerShell script in the runbook editor](./media/automation-quickstart-create-runbook/automation-edit-runbook.png)

## <a name="test-the-runbook"></a><span data-ttu-id="ece23-127">Test the runbook</span><span class="sxs-lookup"><span data-stu-id="ece23-127">Test the runbook</span></span>

<span data-ttu-id="ece23-128">Once the runbook is created, you test the runbook to validate that it works.</span><span class="sxs-lookup"><span data-stu-id="ece23-128">Once the runbook is created, you test the runbook to validate that it works.</span></span>

1. <span data-ttu-id="ece23-129">Click **Test pane** to open the **Test** page.</span><span class="sxs-lookup"><span data-stu-id="ece23-129">Click **Test pane** to open the **Test** page.</span></span>

1. <span data-ttu-id="ece23-130">Enter a value for **Name**, and click **Start**.</span><span class="sxs-lookup"><span data-stu-id="ece23-130">Enter a value for **Name**, and click **Start**.</span></span> <span data-ttu-id="ece23-131">The test job starts and the job status and output display.</span><span class="sxs-lookup"><span data-stu-id="ece23-131">The test job starts and the job status and output display.</span></span>

    ![Runbook test job](./media/automation-quickstart-create-runbook/automation-test-runbook.png)

1. <span data-ttu-id="ece23-133">Close the **Test** page by clicking the **X** in the upper right corner.</span><span class="sxs-lookup"><span data-stu-id="ece23-133">Close the **Test** page by clicking the **X** in the upper right corner.</span></span> <span data-ttu-id="ece23-134">Select **OK** in the popup that appears.</span><span class="sxs-lookup"><span data-stu-id="ece23-134">Select **OK** in the popup that appears.</span></span>

1. <span data-ttu-id="ece23-135">In the **Edit PowerShell Runbook** page, click **Publish** to publish the runbook as the official version of the runbook in the account.</span><span class="sxs-lookup"><span data-stu-id="ece23-135">In the **Edit PowerShell Runbook** page, click **Publish** to publish the runbook as the official version of the runbook in the account.</span></span>

   ![Runbook test job](./media/automation-quickstart-create-runbook/automation-hello-world-runbook-job.png)

## <a name="run-the-runbook"></a><span data-ttu-id="ece23-137">Run the runbook</span><span class="sxs-lookup"><span data-stu-id="ece23-137">Run the runbook</span></span>

<span data-ttu-id="ece23-138">Once the runbook is published, the overview page is shown.</span><span class="sxs-lookup"><span data-stu-id="ece23-138">Once the runbook is published, the overview page is shown.</span></span>

1. <span data-ttu-id="ece23-139">In the runbook overview page, click **Start** to open the **Start Runbook** configuration page for this runbook.</span><span class="sxs-lookup"><span data-stu-id="ece23-139">In the runbook overview page, click **Start** to open the **Start Runbook** configuration page for this runbook.</span></span>

   ![Runbook test job](./media/automation-quickstart-create-runbook/automation-hello-world-runbook-start.png)

1. <span data-ttu-id="ece23-141">Leave **Name** blank, so that the default value is used, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ece23-141">Leave **Name** blank, so that the default value is used, and click **OK**.</span></span> <span data-ttu-id="ece23-142">The runbook job is submitted, and the job page appears.</span><span class="sxs-lookup"><span data-stu-id="ece23-142">The runbook job is submitted, and the job page appears.</span></span>

   ![Runbook test job](./media/automation-quickstart-create-runbook/automation-job-page.png)

1. <span data-ttu-id="ece23-144">When the **Job status** is **Running** or **Completed**, click **Output** to open the **Output** pane and view the runbook output.</span><span class="sxs-lookup"><span data-stu-id="ece23-144">When the **Job status** is **Running** or **Completed**, click **Output** to open the **Output** pane and view the runbook output.</span></span>

   ![Runbook test job](./media/automation-quickstart-create-runbook/automation-hello-world-runbook-job-output.png)

## <a name="clean-up-resources"></a><span data-ttu-id="ece23-146">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="ece23-146">Clean up resources</span></span>

<span data-ttu-id="ece23-147">When no longer needed, delete the runbook.</span><span class="sxs-lookup"><span data-stu-id="ece23-147">When no longer needed, delete the runbook.</span></span> <span data-ttu-id="ece23-148">To do so, select the runbook in the runbook list, and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="ece23-148">To do so, select the runbook in the runbook list, and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ece23-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="ece23-149">Next steps</span></span>

<span data-ttu-id="ece23-150">In this quickstart, you’ve created, edited, tested, and published a runbook and started a runbook job.</span><span class="sxs-lookup"><span data-stu-id="ece23-150">In this quickstart, you’ve created, edited, tested, and published a runbook and started a runbook job.</span></span> <span data-ttu-id="ece23-151">To learn more about Automation runbooks, continue to the article on the different runbook types that you can create and use in Automation.</span><span class="sxs-lookup"><span data-stu-id="ece23-151">To learn more about Automation runbooks, continue to the article on the different runbook types that you can create and use in Automation.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ece23-152">Automation How To - Runbook Types</span><span class="sxs-lookup"><span data-stu-id="ece23-152">Automation How To - Runbook Types</span></span>](./automation-runbook-types.md)
