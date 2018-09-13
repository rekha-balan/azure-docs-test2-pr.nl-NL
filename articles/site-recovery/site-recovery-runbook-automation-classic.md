---
title: Add Azure automation runbooks to recovery plans in the classic portal | Microsoft Docs
description: This article describes how Azure Site Recovery now enables you to extend recovery plans using Azure Automation to complete complex tasks during recovery to Azure
services: site-recovery
documentationcenter: ''
author: ruturaj
manager: gauravd
editor: ''
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: required
ms.date: 02/06/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: f392f967e42399ce256a834153da7dff3dfeff7a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669407"
---
# <a name="add-azure-automation-runbooks-to-recovery-plans-in-the-classic-portal"></a><span data-ttu-id="24e55-103">Add Azure automation runbooks to recovery plans in the classic portal</span><span class="sxs-lookup"><span data-stu-id="24e55-103">Add Azure automation runbooks to recovery plans in the classic portal</span></span>
<span data-ttu-id="24e55-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation to provide extensibility to recovery plans.</span><span class="sxs-lookup"><span data-stu-id="24e55-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation to provide extensibility to recovery plans.</span></span> <span data-ttu-id="24e55-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication to secondary cloud and replication to Azure scenarios.</span><span class="sxs-lookup"><span data-stu-id="24e55-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication to secondary cloud and replication to Azure scenarios.</span></span> <span data-ttu-id="24e55-106">They also help in making the recovery **consistently accurate**, **repeatable**, and **automated**.</span><span class="sxs-lookup"><span data-stu-id="24e55-106">They also help in making the recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="24e55-107">If you are failing over your virtual machines to Azure, integration with Azure Automation extends the recovery plans and gives you capability to execute runbooks, thus allowing powerful automation tasks.</span><span class="sxs-lookup"><span data-stu-id="24e55-107">If you are failing over your virtual machines to Azure, integration with Azure Automation extends the recovery plans and gives you capability to execute runbooks, thus allowing powerful automation tasks.</span></span>

<span data-ttu-id="24e55-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="24e55-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="24e55-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how to orchestrate recovery to Azure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span><span class="sxs-lookup"><span data-stu-id="24e55-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how to orchestrate recovery to Azure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span></span>

<span data-ttu-id="24e55-110">In this short tutorial, we will look at how you can integrate Azure Automation runbooks into recovery plans.</span><span class="sxs-lookup"><span data-stu-id="24e55-110">In this short tutorial, we will look at how you can integrate Azure Automation runbooks into recovery plans.</span></span> <span data-ttu-id="24e55-111">We will automate simple tasks that earlier required manual intervention and see how to convert a multi step recovery into a single-click recovery action.</span><span class="sxs-lookup"><span data-stu-id="24e55-111">We will automate simple tasks that earlier required manual intervention and see how to convert a multi step recovery into a single-click recovery action.</span></span> <span data-ttu-id="24e55-112">We will also look at how you can troubleshoot a simple script if it goes wrong.</span><span class="sxs-lookup"><span data-stu-id="24e55-112">We will also look at how you can troubleshoot a simple script if it goes wrong.</span></span>

## <a name="protect-the-application-to-azure"></a><span data-ttu-id="24e55-113">Protect the application to Azure</span><span class="sxs-lookup"><span data-stu-id="24e55-113">Protect the application to Azure</span></span>
<span data-ttu-id="24e55-114">Let us begin with a simple application consisting of two virtual machines.</span><span class="sxs-lookup"><span data-stu-id="24e55-114">Let us begin with a simple application consisting of two virtual machines.</span></span> <span data-ttu-id="24e55-115">Here, we have a HRweb application of Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="24e55-115">Here, we have a HRweb application of Fabrikam.</span></span> <span data-ttu-id="24e55-116">Fabrikam-HRweb-frontend and Fabrikam-Hrweb-backend are the two virtual machines protected to Azure using Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="24e55-116">Fabrikam-HRweb-frontend and Fabrikam-Hrweb-backend are the two virtual machines protected to Azure using Azure Site Recovery.</span></span> <span data-ttu-id="24e55-117">To protect the virtual machines using Azure Site Recovery, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="24e55-117">To protect the virtual machines using Azure Site Recovery, follow the steps below.</span></span>

1. <span data-ttu-id="24e55-118">Enable protection for your virtual machines.</span><span class="sxs-lookup"><span data-stu-id="24e55-118">Enable protection for your virtual machines.</span></span>
2. <span data-ttu-id="24e55-119">Ensure that the virtual machines have completed initial replication and are replicating.</span><span class="sxs-lookup"><span data-stu-id="24e55-119">Ensure that the virtual machines have completed initial replication and are replicating.</span></span>
3. <span data-ttu-id="24e55-120">Wait till the initial replication completes and the Replication status says Protected.</span><span class="sxs-lookup"><span data-stu-id="24e55-120">Wait till the initial replication completes and the Replication status says Protected.</span></span>

## ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/01.png)
<span data-ttu-id="24e55-121">In this tutorial, we will create a recovery plan for the Fabrikam HRweb application to failover the application to Azure.</span><span class="sxs-lookup"><span data-stu-id="24e55-121">In this tutorial, we will create a recovery plan for the Fabrikam HRweb application to failover the application to Azure.</span></span> <span data-ttu-id="24e55-122">Then we will integrate it with a runbook that will create an endpoint on the failed over Azure virtual machine to serve web pages at port 80.</span><span class="sxs-lookup"><span data-stu-id="24e55-122">Then we will integrate it with a runbook that will create an endpoint on the failed over Azure virtual machine to serve web pages at port 80.</span></span>

<span data-ttu-id="24e55-123">First, let's create a recovery plan for our application.</span><span class="sxs-lookup"><span data-stu-id="24e55-123">First, let's create a recovery plan for our application.</span></span>

## <a name="create-the-recovery-plan"></a><span data-ttu-id="24e55-124">Create the recovery plan</span><span class="sxs-lookup"><span data-stu-id="24e55-124">Create the recovery plan</span></span>
<span data-ttu-id="24e55-125">To recover the application to Azure, you need to create a recovery plan.</span><span class="sxs-lookup"><span data-stu-id="24e55-125">To recover the application to Azure, you need to create a recovery plan.</span></span>
<span data-ttu-id="24e55-126">Using a recovery plan you can specify the order of recovery of the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="24e55-126">Using a recovery plan you can specify the order of recovery of the virtual machines.</span></span> <span data-ttu-id="24e55-127">The virtual machine placed in group 1 will recover and start first, and then the virtual machine in group 2 will follow.</span><span class="sxs-lookup"><span data-stu-id="24e55-127">The virtual machine placed in group 1 will recover and start first, and then the virtual machine in group 2 will follow.</span></span>

<span data-ttu-id="24e55-128">Create a Recovery Plan that looks like below.</span><span class="sxs-lookup"><span data-stu-id="24e55-128">Create a Recovery Plan that looks like below.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/12.png)

<span data-ttu-id="24e55-129">To read more about recovery plans, read documentation [here](https://msdn.microsoft.com/library/azure/dn788799.aspx "here").</span><span class="sxs-lookup"><span data-stu-id="24e55-129">To read more about recovery plans, read documentation [here](https://msdn.microsoft.com/library/azure/dn788799.aspx "here").</span></span>

<span data-ttu-id="24e55-130">Next, let's create the necessary artifacts in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="24e55-130">Next, let's create the necessary artifacts in Azure Automation.</span></span>

## <a name="create-the-automation-account-and-its-assets"></a><span data-ttu-id="24e55-131">Create the automation account and its assets</span><span class="sxs-lookup"><span data-stu-id="24e55-131">Create the automation account and its assets</span></span>
<span data-ttu-id="24e55-132">You need an Azure Automation account to create runbooks.</span><span class="sxs-lookup"><span data-stu-id="24e55-132">You need an Azure Automation account to create runbooks.</span></span> <span data-ttu-id="24e55-133">If you do not already have an account, navigate to Azure Automation tab denoted by ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/02.png)and create a new account.</span><span class="sxs-lookup"><span data-stu-id="24e55-133">If you do not already have an account, navigate to Azure Automation tab denoted by ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/02.png)and create a new account.</span></span>

1. <span data-ttu-id="24e55-134">Give the account a name to identify with.</span><span class="sxs-lookup"><span data-stu-id="24e55-134">Give the account a name to identify with.</span></span>
2. <span data-ttu-id="24e55-135">Specify a geographical region where you want to place the account.</span><span class="sxs-lookup"><span data-stu-id="24e55-135">Specify a geographical region where you want to place the account.</span></span>

<span data-ttu-id="24e55-136">It is recommended to place the account in the same region as the ASR vault.</span><span class="sxs-lookup"><span data-stu-id="24e55-136">It is recommended to place the account in the same region as the ASR vault.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/03.png)

<span data-ttu-id="24e55-137">Next, create the following assets in the Account.</span><span class="sxs-lookup"><span data-stu-id="24e55-137">Next, create the following assets in the Account.</span></span>

### <a name="add-a-subscription-name-as-asset"></a><span data-ttu-id="24e55-138">Add a subscription name as asset</span><span class="sxs-lookup"><span data-stu-id="24e55-138">Add a subscription name as asset</span></span>
1. <span data-ttu-id="24e55-139">Add a new setting ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/04.png) in the Azure Automation Assets and select to ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/05.png)</span><span class="sxs-lookup"><span data-stu-id="24e55-139">Add a new setting ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/04.png) in the Azure Automation Assets and select to ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/05.png)</span></span>
2. <span data-ttu-id="24e55-140">Select the variable type as **String**</span><span class="sxs-lookup"><span data-stu-id="24e55-140">Select the variable type as **String**</span></span>
3. <span data-ttu-id="24e55-141">Specify variable name as **AzureSubscriptionName**</span><span class="sxs-lookup"><span data-stu-id="24e55-141">Specify variable name as **AzureSubscriptionName**</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/06.png)
4. <span data-ttu-id="24e55-142">Specify your actual Azure Subscription name as the variable value.</span><span class="sxs-lookup"><span data-stu-id="24e55-142">Specify your actual Azure Subscription name as the variable value.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/07_1.png)

<span data-ttu-id="24e55-143">You can identify the name of your subscription from the settings page of your account on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="24e55-143">You can identify the name of your subscription from the settings page of your account on the Azure portal.</span></span>

### <a name="add-an-azure-login-credential-as-asset"></a><span data-ttu-id="24e55-144">Add an Azure login credential as asset</span><span class="sxs-lookup"><span data-stu-id="24e55-144">Add an Azure login credential as asset</span></span>
<span data-ttu-id="24e55-145">Azure Automation uses Azure PowerShell to connect to the subscription and operates on the artifacts there.</span><span class="sxs-lookup"><span data-stu-id="24e55-145">Azure Automation uses Azure PowerShell to connect to the subscription and operates on the artifacts there.</span></span> <span data-ttu-id="24e55-146">For this, you need to authenticate using your Microsoft account or a work or school account.</span><span class="sxs-lookup"><span data-stu-id="24e55-146">For this, you need to authenticate using your Microsoft account or a work or school account.</span></span>
<span data-ttu-id="24e55-147">You can store the account credentials in an asset to be used securely by the runbook.</span><span class="sxs-lookup"><span data-stu-id="24e55-147">You can store the account credentials in an asset to be used securely by the runbook.</span></span>

1. <span data-ttu-id="24e55-148">Add a new setting ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/04.png) in the Azure Automation Assets and select ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/09.png)</span><span class="sxs-lookup"><span data-stu-id="24e55-148">Add a new setting ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/04.png) in the Azure Automation Assets and select ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/09.png)</span></span>
2. <span data-ttu-id="24e55-149">Select the Credential type as **Windows PowerShell Credential**</span><span class="sxs-lookup"><span data-stu-id="24e55-149">Select the Credential type as **Windows PowerShell Credential**</span></span>
3. <span data-ttu-id="24e55-150">Specify the name as **AzureCredential**</span><span class="sxs-lookup"><span data-stu-id="24e55-150">Specify the name as **AzureCredential**</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/10.png)
4. <span data-ttu-id="24e55-151">Specify the username and password to sign-in with.</span><span class="sxs-lookup"><span data-stu-id="24e55-151">Specify the username and password to sign-in with.</span></span>

<span data-ttu-id="24e55-152">Now both these settings are available in your assets.</span><span class="sxs-lookup"><span data-stu-id="24e55-152">Now both these settings are available in your assets.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/11.png)

<span data-ttu-id="24e55-153">More information about how to connect to your subscription via PowerShell is given [here](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="24e55-153">More information about how to connect to your subscription via PowerShell is given [here](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="24e55-154">Next, you will create a runbook in Azure Automation that can add an endpoint for the front-end virtual machine after failover.</span><span class="sxs-lookup"><span data-stu-id="24e55-154">Next, you will create a runbook in Azure Automation that can add an endpoint for the front-end virtual machine after failover.</span></span>

## <a name="azure-automation-context"></a><span data-ttu-id="24e55-155">Azure automation context</span><span class="sxs-lookup"><span data-stu-id="24e55-155">Azure automation context</span></span>
<span data-ttu-id="24e55-156">ASR passes a context variable to the runbook to help you write deterministic scripts.</span><span class="sxs-lookup"><span data-stu-id="24e55-156">ASR passes a context variable to the runbook to help you write deterministic scripts.</span></span> <span data-ttu-id="24e55-157">One could argue that the names of the Cloud Service and the Virtual Machine are predictable, but happens that it is not always the case owing to certain scenarios such as the one where the name of the virtual machine name might have changed due to unsupported characters in Azure.</span><span class="sxs-lookup"><span data-stu-id="24e55-157">One could argue that the names of the Cloud Service and the Virtual Machine are predictable, but happens that it is not always the case owing to certain scenarios such as the one where the name of the virtual machine name might have changed due to unsupported characters in Azure.</span></span> <span data-ttu-id="24e55-158">Hence this information is passed to the ASR recovery plan as part of the *context*.</span><span class="sxs-lookup"><span data-stu-id="24e55-158">Hence this information is passed to the ASR recovery plan as part of the *context*.</span></span>

<span data-ttu-id="24e55-159">Below is an example of how the context variable looks.</span><span class="sxs-lookup"><span data-stu-id="24e55-159">Below is an example of how the context variable looks.</span></span>

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


<span data-ttu-id="24e55-160">The table below contains name and description for each variable in the context.</span><span class="sxs-lookup"><span data-stu-id="24e55-160">The table below contains name and description for each variable in the context.</span></span>

| <span data-ttu-id="24e55-161">**Variable name**</span><span class="sxs-lookup"><span data-stu-id="24e55-161">**Variable name**</span></span> | <span data-ttu-id="24e55-162">**Description**</span><span class="sxs-lookup"><span data-stu-id="24e55-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="24e55-163">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="24e55-163">RecoveryPlanName</span></span> |<span data-ttu-id="24e55-164">Name of plan being run.</span><span class="sxs-lookup"><span data-stu-id="24e55-164">Name of plan being run.</span></span> <span data-ttu-id="24e55-165">Helps you take action based on name using the same script</span><span class="sxs-lookup"><span data-stu-id="24e55-165">Helps you take action based on name using the same script</span></span> |
| <span data-ttu-id="24e55-166">FailoverType</span><span class="sxs-lookup"><span data-stu-id="24e55-166">FailoverType</span></span> |<span data-ttu-id="24e55-167">Specifies whether the failover is test, planned, or unplanned.</span><span class="sxs-lookup"><span data-stu-id="24e55-167">Specifies whether the failover is test, planned, or unplanned.</span></span> |
| <span data-ttu-id="24e55-168">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="24e55-168">FailoverDirection</span></span> |<span data-ttu-id="24e55-169">Specify whether recovery is to primary or secondary</span><span class="sxs-lookup"><span data-stu-id="24e55-169">Specify whether recovery is to primary or secondary</span></span> |
| <span data-ttu-id="24e55-170">GroupID</span><span class="sxs-lookup"><span data-stu-id="24e55-170">GroupID</span></span> |<span data-ttu-id="24e55-171">Identify the group number within the recovery plan when the plan is running</span><span class="sxs-lookup"><span data-stu-id="24e55-171">Identify the group number within the recovery plan when the plan is running</span></span> |
| <span data-ttu-id="24e55-172">VmMap</span><span class="sxs-lookup"><span data-stu-id="24e55-172">VmMap</span></span> |<span data-ttu-id="24e55-173">Array of all the virtual machines in the group</span><span class="sxs-lookup"><span data-stu-id="24e55-173">Array of all the virtual machines in the group</span></span> |
| <span data-ttu-id="24e55-174">VMMap key</span><span class="sxs-lookup"><span data-stu-id="24e55-174">VMMap key</span></span> |<span data-ttu-id="24e55-175">Unique key (GUID) for each VM.</span><span class="sxs-lookup"><span data-stu-id="24e55-175">Unique key (GUID) for each VM.</span></span> <span data-ttu-id="24e55-176">It's the same as the VMM ID of the virtual machine where applicable.</span><span class="sxs-lookup"><span data-stu-id="24e55-176">It's the same as the VMM ID of the virtual machine where applicable.</span></span> |
| <span data-ttu-id="24e55-177">RoleName</span><span class="sxs-lookup"><span data-stu-id="24e55-177">RoleName</span></span> |<span data-ttu-id="24e55-178">Name of the Azure VM that's being recovered</span><span class="sxs-lookup"><span data-stu-id="24e55-178">Name of the Azure VM that's being recovered</span></span> |
| <span data-ttu-id="24e55-179">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="24e55-179">CloudServiceName</span></span> |<span data-ttu-id="24e55-180">Azure Cloud Service name under which the virtual machine is created.</span><span class="sxs-lookup"><span data-stu-id="24e55-180">Azure Cloud Service name under which the virtual machine is created.</span></span> |

<span data-ttu-id="24e55-181">To identify the VmMap Key in the context you could also go to the VM properties page in ASR and look at the VM GUID property.</span><span class="sxs-lookup"><span data-stu-id="24e55-181">To identify the VmMap Key in the context you could also go to the VM properties page in ASR and look at the VM GUID property.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a><span data-ttu-id="24e55-182">Author an Automation runbook</span><span class="sxs-lookup"><span data-stu-id="24e55-182">Author an Automation runbook</span></span>
<span data-ttu-id="24e55-183">Now create the runbook to open port 80 on the front-end virtual machine.</span><span class="sxs-lookup"><span data-stu-id="24e55-183">Now create the runbook to open port 80 on the front-end virtual machine.</span></span>

1. <span data-ttu-id="24e55-184">Create a new runbook in the Azure Automation account with the name **OpenPort80**</span><span class="sxs-lookup"><span data-stu-id="24e55-184">Create a new runbook in the Azure Automation account with the name **OpenPort80**</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/14.png)
2. <span data-ttu-id="24e55-185">Navigate to the Author view of the runbook and enter the draft mode.</span><span class="sxs-lookup"><span data-stu-id="24e55-185">Navigate to the Author view of the runbook and enter the draft mode.</span></span>
3. <span data-ttu-id="24e55-186">First specify the variable to use as the recovery plan context</span><span class="sxs-lookup"><span data-stu-id="24e55-186">First specify the variable to use as the recovery plan context</span></span>

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. <span data-ttu-id="24e55-187">Next connect to the subscription using the credential and subscription name</span><span class="sxs-lookup"><span data-stu-id="24e55-187">Next connect to the subscription using the credential and subscription name</span></span>

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect to Azure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   <span data-ttu-id="24e55-188">Note that you use the Azure assets – **AzureCredential** and **AzureSubscriptionName** here.</span><span class="sxs-lookup"><span data-stu-id="24e55-188">Note that you use the Azure assets – **AzureCredential** and **AzureSubscriptionName** here.</span></span>
5. <span data-ttu-id="24e55-189">Now specify the endpoint details and the GUID of the virtual machine for which you want to expose the endpoint.</span><span class="sxs-lookup"><span data-stu-id="24e55-189">Now specify the endpoint details and the GUID of the virtual machine for which you want to expose the endpoint.</span></span> <span data-ttu-id="24e55-190">In this case the front-end virtual machine.</span><span class="sxs-lookup"><span data-stu-id="24e55-190">In this case the front-end virtual machine.</span></span>

   ```
       # Specify the parameters to be used by the script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   <span data-ttu-id="24e55-191">This specifies the Azure endpoint protocol, local port on the VM and its mapped public port.</span><span class="sxs-lookup"><span data-stu-id="24e55-191">This specifies the Azure endpoint protocol, local port on the VM and its mapped public port.</span></span> <span data-ttu-id="24e55-192">These variables are parameters     required by the Azure commands that add endpoints to VMs.</span><span class="sxs-lookup"><span data-stu-id="24e55-192">These variables are parameters     required by the Azure commands that add endpoints to VMs.</span></span> <span data-ttu-id="24e55-193">The VMGUID holds the GUID of the virtual machine you need to operate on.</span><span class="sxs-lookup"><span data-stu-id="24e55-193">The VMGUID holds the GUID of the virtual machine you need to operate on.</span></span>
6. <span data-ttu-id="24e55-194">The script will now extract the context for the given VM GUID and create an endpoint on the virtual machine referenced by it.</span><span class="sxs-lookup"><span data-stu-id="24e55-194">The script will now extract the context for the given VM GUID and create an endpoint on the virtual machine referenced by it.</span></span>

   ```
       #Read the VM GUID from the context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke the necessary pipeline commands to add a Azure Endpoint to a specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. <span data-ttu-id="24e55-195">Once this is complete, hit Publish ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/20.png) to allow your script to be available for execution.</span><span class="sxs-lookup"><span data-stu-id="24e55-195">Once this is complete, hit Publish ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/20.png) to allow your script to be available for execution.</span></span>

<span data-ttu-id="24e55-196">The complete script is given below for your reference</span><span class="sxs-lookup"><span data-stu-id="24e55-196">The complete script is given below for your reference</span></span>

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect to Azure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify the parameters to be used by the script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read the VM GUID from the context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke the necessary pipeline commands to add an Azure Endpoint to a specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-the-script-to-the-recovery-plan"></a><span data-ttu-id="24e55-197">Add the script to the recovery plan</span><span class="sxs-lookup"><span data-stu-id="24e55-197">Add the script to the recovery plan</span></span>
<span data-ttu-id="24e55-198">Once the script is ready, you can add it to the recovery plan that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="24e55-198">Once the script is ready, you can add it to the recovery plan that you created earlier.</span></span>

1. <span data-ttu-id="24e55-199">In the recovery plan you created, choose to add a script after the group 2.</span><span class="sxs-lookup"><span data-stu-id="24e55-199">In the recovery plan you created, choose to add a script after the group 2.</span></span> ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/15.png)
2. <span data-ttu-id="24e55-200">Specify a script name.</span><span class="sxs-lookup"><span data-stu-id="24e55-200">Specify a script name.</span></span> <span data-ttu-id="24e55-201">This is just a friendly name for this script for showing within the Recovery plan.</span><span class="sxs-lookup"><span data-stu-id="24e55-201">This is just a friendly name for this script for showing within the Recovery plan.</span></span>
3. <span data-ttu-id="24e55-202">In the failover to Azure script – Select the Azure Automation Account name.</span><span class="sxs-lookup"><span data-stu-id="24e55-202">In the failover to Azure script – Select the Azure Automation Account name.</span></span>
4. <span data-ttu-id="24e55-203">In the Azure Runbooks, select the runbook you authored.</span><span class="sxs-lookup"><span data-stu-id="24e55-203">In the Azure Runbooks, select the runbook you authored.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a><span data-ttu-id="24e55-204">Primary side scripts</span><span class="sxs-lookup"><span data-stu-id="24e55-204">Primary side scripts</span></span>
<span data-ttu-id="24e55-205">When you are executing a failover to Azure, you can also choose to execute primary side scripts.</span><span class="sxs-lookup"><span data-stu-id="24e55-205">When you are executing a failover to Azure, you can also choose to execute primary side scripts.</span></span> <span data-ttu-id="24e55-206">These scripts will run on the VMM server during failover.</span><span class="sxs-lookup"><span data-stu-id="24e55-206">These scripts will run on the VMM server during failover.</span></span>
<span data-ttu-id="24e55-207">Primary side scripts are only available only for pre-shutdown and post shutdown stages.</span><span class="sxs-lookup"><span data-stu-id="24e55-207">Primary side scripts are only available only for pre-shutdown and post shutdown stages.</span></span> <span data-ttu-id="24e55-208">This is because we expect the primary site to be typically unavailable when a disaster strikes.</span><span class="sxs-lookup"><span data-stu-id="24e55-208">This is because we expect the primary site to be typically unavailable when a disaster strikes.</span></span>
<span data-ttu-id="24e55-209">During an unplanned failover, only if you opt in for primary site operations, it will attempt to run the primary side scripts.</span><span class="sxs-lookup"><span data-stu-id="24e55-209">During an unplanned failover, only if you opt in for primary site operations, it will attempt to run the primary side scripts.</span></span> <span data-ttu-id="24e55-210">If they are not reachable or timeout, the failover will continue to recover the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="24e55-210">If they are not reachable or timeout, the failover will continue to recover the virtual machines.</span></span>
<span data-ttu-id="24e55-211">Primary side scripts are un-available for VMware/Physical/Hyper-v Sites without VMM protected to Azure - while you failover to Azure.</span><span class="sxs-lookup"><span data-stu-id="24e55-211">Primary side scripts are un-available for VMware/Physical/Hyper-v Sites without VMM protected to Azure - while you failover to Azure.</span></span>
<span data-ttu-id="24e55-212">However, when you failback from Azure to on-premises, primary side scripts (Runbooks) can be used for all targets except VMware.</span><span class="sxs-lookup"><span data-stu-id="24e55-212">However, when you failback from Azure to on-premises, primary side scripts (Runbooks) can be used for all targets except VMware.</span></span>

## <a name="test-the-recovery-plan"></a><span data-ttu-id="24e55-213">Test the recovery plan</span><span class="sxs-lookup"><span data-stu-id="24e55-213">Test the recovery plan</span></span>
<span data-ttu-id="24e55-214">Once you have added the runbook to the plan you can initiate a test failover and see it in action.</span><span class="sxs-lookup"><span data-stu-id="24e55-214">Once you have added the runbook to the plan you can initiate a test failover and see it in action.</span></span> <span data-ttu-id="24e55-215">It is always recommended to run a test failover to test your application and the recovery plan to ensure that there are no errors.</span><span class="sxs-lookup"><span data-stu-id="24e55-215">It is always recommended to run a test failover to test your application and the recovery plan to ensure that there are no errors.</span></span>

1. <span data-ttu-id="24e55-216">Select the recovery plan and initiate a test failover.</span><span class="sxs-lookup"><span data-stu-id="24e55-216">Select the recovery plan and initiate a test failover.</span></span>
2. <span data-ttu-id="24e55-217">During the plan execution, you can see whether the runbook has executed or not via its status.</span><span class="sxs-lookup"><span data-stu-id="24e55-217">During the plan execution, you can see whether the runbook has executed or not via its status.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/17.png)
3. <span data-ttu-id="24e55-218">You can also see the detailed runbook execution status on the Azure Automation jobs page for the runbook.</span><span class="sxs-lookup"><span data-stu-id="24e55-218">You can also see the detailed runbook execution status on the Azure Automation jobs page for the runbook.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/18.png)
4. <span data-ttu-id="24e55-219">After the failover completes, apart from the runbook execution result, you can see whether the execution is successful or not by visiting the Azure virtual machine page and looking at the endpoints.</span><span class="sxs-lookup"><span data-stu-id="24e55-219">After the failover completes, apart from the runbook execution result, you can see whether the execution is successful or not by visiting the Azure virtual machine page and looking at the endpoints.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a><span data-ttu-id="24e55-220">Sample scripts</span><span class="sxs-lookup"><span data-stu-id="24e55-220">Sample scripts</span></span>
<span data-ttu-id="24e55-221">While we walked through automating one commonly used task of adding an endpoint to an Azure virtual machine in this tutorial, you could do a number of other powerful automation tasks using Azure automation.</span><span class="sxs-lookup"><span data-stu-id="24e55-221">While we walked through automating one commonly used task of adding an endpoint to an Azure virtual machine in this tutorial, you could do a number of other powerful automation tasks using Azure automation.</span></span> <span data-ttu-id="24e55-222">Microsoft and the Azure Automation community provide sample runbooks which can help you get started creating your own solutions, and utility runbooks, which you can use as building blocks for larger automation tasks.</span><span class="sxs-lookup"><span data-stu-id="24e55-222">Microsoft and the Azure Automation community provide sample runbooks which can help you get started creating your own solutions, and utility runbooks, which you can use as building blocks for larger automation tasks.</span></span> <span data-ttu-id="24e55-223">Start using them from the gallery and build  powerful one-click recovery plans for your applications using Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="24e55-223">Start using them from the gallery and build  powerful one-click recovery plans for your applications using Azure Site Recovery.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="24e55-224">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="24e55-224">Additional Resources</span></span>
[<span data-ttu-id="24e55-225">Azure Automation Overview</span><span class="sxs-lookup"><span data-stu-id="24e55-225">Azure Automation Overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure Automation Overview")

[<span data-ttu-id="24e55-226">Sample Azure Automation Scripts</span><span class="sxs-lookup"><span data-stu-id="24e55-226">Sample Azure Automation Scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Sample Azure Automation Scripts")




















