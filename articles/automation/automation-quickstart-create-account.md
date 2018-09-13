---
title: Azure Quickstart - Create an Azure Automation account | Microsoft Docs
description: Learn how to create an Azure Automation account and run a runbook
services: automation
author: csand-msft
ms.author: csand
ms.date: 08/22/2018
ms.topic: quickstart
ms.service: automation
ms.component: process-automation
ms.custom: mvc
ms.openlocfilehash: 81dbcb4f77708f9f679d146b1db83ddecc30629d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966936"
---
# <a name="create-an-azure-automation-account"></a><span data-ttu-id="cb2e6-103">Create an Azure Automation account</span><span class="sxs-lookup"><span data-stu-id="cb2e6-103">Create an Azure Automation account</span></span>

<span data-ttu-id="cb2e6-104">Azure Automation accounts can be created through Azure.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-104">Azure Automation accounts can be created through Azure.</span></span> <span data-ttu-id="cb2e6-105">This method provides a browser-based user interface for creating and configuring Automation accounts and related resources.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-105">This method provides a browser-based user interface for creating and configuring Automation accounts and related resources.</span></span> <span data-ttu-id="cb2e6-106">This quickstart steps through creating an Automation account and running a runbook in the account.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-106">This quickstart steps through creating an Automation account and running a runbook in the account.</span></span>

<span data-ttu-id="cb2e6-107">If you don't have an Azure subscription, create a [free Azure account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-107">If you don't have an Azure subscription, create a [free Azure account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="cb2e6-108">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="cb2e6-108">Sign in to Azure</span></span>

<span data-ttu-id="cb2e6-109">Sign in to Azure at https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="cb2e6-109">Sign in to Azure at https://portal.azure.com</span></span>

## <a name="create-automation-account"></a><span data-ttu-id="cb2e6-110">Create Automation account</span><span class="sxs-lookup"><span data-stu-id="cb2e6-110">Create Automation account</span></span>

1. <span data-ttu-id="cb2e6-111">Click the **Create a resource** button found on the upper left-hand corner of Azure.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-111">Click the **Create a resource** button found on the upper left-hand corner of Azure.</span></span>

1. <span data-ttu-id="cb2e6-112">Select **Management Tools**, and then select **Automation**.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-112">Select **Management Tools**, and then select **Automation**.</span></span>

1. <span data-ttu-id="cb2e6-113">Enter the account information.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-113">Enter the account information.</span></span> <span data-ttu-id="cb2e6-114">For **Create Azure Run As account**, choose **Yes** so that the artifacts to simplify authentication to Azure are enabled automatically.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-114">For **Create Azure Run As account**, choose **Yes** so that the artifacts to simplify authentication to Azure are enabled automatically.</span></span> <span data-ttu-id="cb2e6-115">It is important to note, that when creating an Automation Account, the name cannot be changed after it is chosen.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-115">It is important to note, that when creating an Automation Account, the name cannot be changed after it is chosen.</span></span> <span data-ttu-id="cb2e6-116">When complete, click **Create**, to start the Automation account deployment.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-116">When complete, click **Create**, to start the Automation account deployment.</span></span>

    ![Enter information about your Automation account in the page](./media/automation-quickstart-create-account/create-automation-account-portal-blade.png)  

1. <span data-ttu-id="cb2e6-118">When the deployment has completed, click \*\* **All Services**, select **Automation Accounts** and select the Automation Account you created.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-118">When the deployment has completed, click \*\* **All Services**, select **Automation Accounts** and select the Automation Account you created.</span></span>

    ![Automation account overview](./media/automation-quickstart-create-account/automation-account-overview.png)

## <a name="run-a-runbook"></a><span data-ttu-id="cb2e6-120">Run a runbook</span><span class="sxs-lookup"><span data-stu-id="cb2e6-120">Run a runbook</span></span>

<span data-ttu-id="cb2e6-121">Run one of the tutorial runbooks.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-121">Run one of the tutorial runbooks.</span></span>

1. <span data-ttu-id="cb2e6-122">Click **Runbooks** under **PROCESS AUTOMATION**.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-122">Click **Runbooks** under **PROCESS AUTOMATION**.</span></span> <span data-ttu-id="cb2e6-123">The list of runbooks is displayed.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-123">The list of runbooks is displayed.</span></span> <span data-ttu-id="cb2e6-124">By default several tutorial runbooks are enabled in the account.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-124">By default several tutorial runbooks are enabled in the account.</span></span>

    ![Automation account runbooks list](./media/automation-quickstart-create-account/automation-runbooks-overview.png)

1. <span data-ttu-id="cb2e6-126">Select the **AzureAutomationTutorialScript** runbook.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-126">Select the **AzureAutomationTutorialScript** runbook.</span></span> <span data-ttu-id="cb2e6-127">This action opens the runbook overview page.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-127">This action opens the runbook overview page.</span></span>

    ![Runbook overview](./media/automation-quickstart-create-account/automation-tutorial-script-runbook-overview.png)

1. <span data-ttu-id="cb2e6-129">Click **Start**, and on the **Start Runbook** page, click **OK** to start the runbook.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-129">Click **Start**, and on the **Start Runbook** page, click **OK** to start the runbook.</span></span>

    ![Runbook job page](./media/automation-quickstart-create-account/automation-tutorial-script-job.png)

1. <span data-ttu-id="cb2e6-131">After the **Job status** becomes **Running**, click **Output** or **All Logs** to view the runbook job output.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-131">After the **Job status** becomes **Running**, click **Output** or **All Logs** to view the runbook job output.</span></span> <span data-ttu-id="cb2e6-132">For this tutorial runbook, the output is a list of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-132">For this tutorial runbook, the output is a list of your Azure resources.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="cb2e6-133">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="cb2e6-133">Clean up resources</span></span>

<span data-ttu-id="cb2e6-134">When no longer needed, delete the resource group, Automation account, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-134">When no longer needed, delete the resource group, Automation account, and all related resources.</span></span> <span data-ttu-id="cb2e6-135">To do so, select the resource group for the Automation account and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-135">To do so, select the resource group for the Automation account and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb2e6-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="cb2e6-136">Next steps</span></span>

<span data-ttu-id="cb2e6-137">In this quickstart, you’ve deployed an Automation account, started a runbook job, and viewed the job results.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-137">In this quickstart, you’ve deployed an Automation account, started a runbook job, and viewed the job results.</span></span> <span data-ttu-id="cb2e6-138">To learn more about Azure Automation, continue to the quickstart for creating your first runbook.</span><span class="sxs-lookup"><span data-stu-id="cb2e6-138">To learn more about Azure Automation, continue to the quickstart for creating your first runbook.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cb2e6-139">Automation Quickstart - Create Runbook</span><span class="sxs-lookup"><span data-stu-id="cb2e6-139">Automation Quickstart - Create Runbook</span></span>](./automation-quickstart-create-runbook.md)
