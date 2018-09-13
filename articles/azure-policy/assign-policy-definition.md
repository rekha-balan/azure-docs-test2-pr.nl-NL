---
title: Create a policy assignment to identify non-compliant resources in your Azure environment
description: This article walks you through the steps to create a policy definition to identify non-compliant resources.
services: azure-policy
author: DCtheGeek
ms.author: dacoulte
ms.date: 05/24/2018
ms.topic: quickstart
ms.service: azure-policy
ms.custom: mvc
manager: carmonm
ms.openlocfilehash: 43f069fbd8f4fcc13bbc4d9e75763fa98aec1065
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868847"
---
# <a name="create-a-policy-assignment-to-identify-non-compliant-resources-in-your-azure-environment"></a><span data-ttu-id="19c04-103">Create a policy assignment to identify non-compliant resources in your Azure environment</span><span class="sxs-lookup"><span data-stu-id="19c04-103">Create a policy assignment to identify non-compliant resources in your Azure environment</span></span>

<span data-ttu-id="19c04-104">The first step in understanding compliance in Azure is to identify the status of your resources.</span><span class="sxs-lookup"><span data-stu-id="19c04-104">The first step in understanding compliance in Azure is to identify the status of your resources.</span></span> <span data-ttu-id="19c04-105">This quickstart steps you through the process of creating a policy assignment to identify virtual machines that are not using managed disks.</span><span class="sxs-lookup"><span data-stu-id="19c04-105">This quickstart steps you through the process of creating a policy assignment to identify virtual machines that are not using managed disks.</span></span>

<span data-ttu-id="19c04-106">At the end of this process, you will successfully identify virtual machines that are not using managed disks.</span><span class="sxs-lookup"><span data-stu-id="19c04-106">At the end of this process, you will successfully identify virtual machines that are not using managed disks.</span></span> <span data-ttu-id="19c04-107">They are *non-compliant* with the policy assignment.</span><span class="sxs-lookup"><span data-stu-id="19c04-107">They are *non-compliant* with the policy assignment.</span></span>

<span data-ttu-id="19c04-108">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="19c04-108">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="create-a-policy-assignment"></a><span data-ttu-id="19c04-109">Create a policy assignment</span><span class="sxs-lookup"><span data-stu-id="19c04-109">Create a policy assignment</span></span>

<span data-ttu-id="19c04-110">In this quickstart, you create a policy assignment and assign the *Audit Virtual Machines without Managed Disks* policy definition.</span><span class="sxs-lookup"><span data-stu-id="19c04-110">In this quickstart, you create a policy assignment and assign the *Audit Virtual Machines without Managed Disks* policy definition.</span></span>

1. <span data-ttu-id="19c04-111">Launch the Azure Policy service in the Azure portal by clicking **All services**, then searching for and selecting **Policy**.</span><span class="sxs-lookup"><span data-stu-id="19c04-111">Launch the Azure Policy service in the Azure portal by clicking **All services**, then searching for and selecting **Policy**.</span></span>

   ![Search for policy](media/assign-policy-definition/search-policy.png)

2. <span data-ttu-id="19c04-113">Select **Assignments** on the left side of the Azure Policy page.</span><span class="sxs-lookup"><span data-stu-id="19c04-113">Select **Assignments** on the left side of the Azure Policy page.</span></span> <span data-ttu-id="19c04-114">An assignment is a policy that has been assigned to take place within a specific scope.</span><span class="sxs-lookup"><span data-stu-id="19c04-114">An assignment is a policy that has been assigned to take place within a specific scope.</span></span>
3. <span data-ttu-id="19c04-115">Select **Assign Policy** from the top of the **Policy - Assignments** page.</span><span class="sxs-lookup"><span data-stu-id="19c04-115">Select **Assign Policy** from the top of the **Policy - Assignments** page.</span></span>

   ![Assign a policy definition](media/assign-policy-definition/select-assign-policy.png)

4. <span data-ttu-id="19c04-117">On the **Assign Policy** page, select the **Scope** by clicking the ellipsis and selecting a subscription (required) and resource group (optional).</span><span class="sxs-lookup"><span data-stu-id="19c04-117">On the **Assign Policy** page, select the **Scope** by clicking the ellipsis and selecting a subscription (required) and resource group (optional).</span></span> <span data-ttu-id="19c04-118">A scope determines what resources or grouping of resources the policy assignment gets enforced on.</span><span class="sxs-lookup"><span data-stu-id="19c04-118">A scope determines what resources or grouping of resources the policy assignment gets enforced on.</span></span>  <span data-ttu-id="19c04-119">Then click **Select** at the bottom of the **Scope** page.</span><span class="sxs-lookup"><span data-stu-id="19c04-119">Then click **Select** at the bottom of the **Scope** page.</span></span>

   <span data-ttu-id="19c04-120">This example uses the **Contoso Subscription**.</span><span class="sxs-lookup"><span data-stu-id="19c04-120">This example uses the **Contoso Subscription**.</span></span> <span data-ttu-id="19c04-121">Your subscription will differ.</span><span class="sxs-lookup"><span data-stu-id="19c04-121">Your subscription will differ.</span></span>

5. <span data-ttu-id="19c04-122">If you wanted to exclude one or more resource groups (if you only scoped a subscription) or specific resources within a resource group (either scoping case), you could configure **Exclusions** from the policy assignment.</span><span class="sxs-lookup"><span data-stu-id="19c04-122">If you wanted to exclude one or more resource groups (if you only scoped a subscription) or specific resources within a resource group (either scoping case), you could configure **Exclusions** from the policy assignment.</span></span> <span data-ttu-id="19c04-123">Leave it blank for now.</span><span class="sxs-lookup"><span data-stu-id="19c04-123">Leave it blank for now.</span></span>

6. <span data-ttu-id="19c04-124">Select the **Policy definition** ellipsis to open the list of available definitions.</span><span class="sxs-lookup"><span data-stu-id="19c04-124">Select the **Policy definition** ellipsis to open the list of available definitions.</span></span> <span data-ttu-id="19c04-125">Azure Policy comes with already built-in policy definitions you can use.</span><span class="sxs-lookup"><span data-stu-id="19c04-125">Azure Policy comes with already built-in policy definitions you can use.</span></span> <span data-ttu-id="19c04-126">Many built-in policy definitions are available, such as:</span><span class="sxs-lookup"><span data-stu-id="19c04-126">Many built-in policy definitions are available, such as:</span></span>

   - <span data-ttu-id="19c04-127">Enforce tag and its value</span><span class="sxs-lookup"><span data-stu-id="19c04-127">Enforce tag and its value</span></span>
   - <span data-ttu-id="19c04-128">Apply tag and its value</span><span class="sxs-lookup"><span data-stu-id="19c04-128">Apply tag and its value</span></span>
   - <span data-ttu-id="19c04-129">Require SQL Server version 12.0</span><span class="sxs-lookup"><span data-stu-id="19c04-129">Require SQL Server version 12.0</span></span>

    <span data-ttu-id="19c04-130">For a complete list of all the available built-in polices, see [Policy samples](json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="19c04-130">For a complete list of all the available built-in polices, see [Policy samples](json-samples.md).</span></span>

7. <span data-ttu-id="19c04-131">Search through the policy definitions list to find the *Audit VMs that do not use managed disks* definition.</span><span class="sxs-lookup"><span data-stu-id="19c04-131">Search through the policy definitions list to find the *Audit VMs that do not use managed disks* definition.</span></span> <span data-ttu-id="19c04-132">Click on that policy and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="19c04-132">Click on that policy and click **Select**.</span></span>

   ![Find the correct policy definition](media/assign-policy-definition/select-available-definition.png)

8. <span data-ttu-id="19c04-134">The **Assignment name** is automatically populated with the policy name you selected, but you can change it.</span><span class="sxs-lookup"><span data-stu-id="19c04-134">The **Assignment name** is automatically populated with the policy name you selected, but you can change it.</span></span> <span data-ttu-id="19c04-135">For this example, leave *Audit VMs that do not use managed disks*.</span><span class="sxs-lookup"><span data-stu-id="19c04-135">For this example, leave *Audit VMs that do not use managed disks*.</span></span> <span data-ttu-id="19c04-136">You can also add an optional **Description**.</span><span class="sxs-lookup"><span data-stu-id="19c04-136">You can also add an optional **Description**.</span></span> <span data-ttu-id="19c04-137">The description provides details about this policy assignment.</span><span class="sxs-lookup"><span data-stu-id="19c04-137">The description provides details about this policy assignment.</span></span>

9. <span data-ttu-id="19c04-138">Click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="19c04-138">Click **Assign**.</span></span>

<span data-ttu-id="19c04-139">You’re now ready to identify non-compliant resources to understand the compliance state of your environment.</span><span class="sxs-lookup"><span data-stu-id="19c04-139">You’re now ready to identify non-compliant resources to understand the compliance state of your environment.</span></span>

## <a name="identify-non-compliant-resources"></a><span data-ttu-id="19c04-140">Identify non-compliant resources</span><span class="sxs-lookup"><span data-stu-id="19c04-140">Identify non-compliant resources</span></span>

<span data-ttu-id="19c04-141">Select **Compliance** in the left side of the page and locate the **Audit VMs that do not use managed disks** policy assignment you created.</span><span class="sxs-lookup"><span data-stu-id="19c04-141">Select **Compliance** in the left side of the page and locate the **Audit VMs that do not use managed disks** policy assignment you created.</span></span>

![Policy compliance](media/assign-policy-definition/policy-compliance.png)

<span data-ttu-id="19c04-143">If there are any existing resources that are not compliant with this new assignment, they appear under **Non-compliant resources**.</span><span class="sxs-lookup"><span data-stu-id="19c04-143">If there are any existing resources that are not compliant with this new assignment, they appear under **Non-compliant resources**.</span></span>

<span data-ttu-id="19c04-144">When a condition is evaluated against your existing resources and found true, then those resources are marked as non-compliant with the policy.</span><span class="sxs-lookup"><span data-stu-id="19c04-144">When a condition is evaluated against your existing resources and found true, then those resources are marked as non-compliant with the policy.</span></span> <span data-ttu-id="19c04-145">The following table shows how different policy effects work with the condition evaluation for the resulting compliance state.</span><span class="sxs-lookup"><span data-stu-id="19c04-145">The following table shows how different policy effects work with the condition evaluation for the resulting compliance state.</span></span> <span data-ttu-id="19c04-146">Although you don’t see the evaluation logic in the Azure portal, the compliance state results are shown.</span><span class="sxs-lookup"><span data-stu-id="19c04-146">Although you don’t see the evaluation logic in the Azure portal, the compliance state results are shown.</span></span> <span data-ttu-id="19c04-147">The compliance state result is either compliant or non-compliant.</span><span class="sxs-lookup"><span data-stu-id="19c04-147">The compliance state result is either compliant or non-compliant.</span></span>

| <span data-ttu-id="19c04-148">**Resource State**</span><span class="sxs-lookup"><span data-stu-id="19c04-148">**Resource State**</span></span> | <span data-ttu-id="19c04-149">**Effect**</span><span class="sxs-lookup"><span data-stu-id="19c04-149">**Effect**</span></span> | <span data-ttu-id="19c04-150">**Policy Evaluation**</span><span class="sxs-lookup"><span data-stu-id="19c04-150">**Policy Evaluation**</span></span> | <span data-ttu-id="19c04-151">**Compliance State**</span><span class="sxs-lookup"><span data-stu-id="19c04-151">**Compliance State**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="19c04-152">Exists</span><span class="sxs-lookup"><span data-stu-id="19c04-152">Exists</span></span> | <span data-ttu-id="19c04-153">Deny, Audit, Append\*, DeployIfNotExist\*, AuditIfNotExist\*</span><span class="sxs-lookup"><span data-stu-id="19c04-153">Deny, Audit, Append\*, DeployIfNotExist\*, AuditIfNotExist\*</span></span> | <span data-ttu-id="19c04-154">True</span><span class="sxs-lookup"><span data-stu-id="19c04-154">True</span></span> | <span data-ttu-id="19c04-155">Non-Compliant</span><span class="sxs-lookup"><span data-stu-id="19c04-155">Non-Compliant</span></span> |
| <span data-ttu-id="19c04-156">Exists</span><span class="sxs-lookup"><span data-stu-id="19c04-156">Exists</span></span> | <span data-ttu-id="19c04-157">Deny, Audit, Append\*, DeployIfNotExist\*, AuditIfNotExist\*</span><span class="sxs-lookup"><span data-stu-id="19c04-157">Deny, Audit, Append\*, DeployIfNotExist\*, AuditIfNotExist\*</span></span> | <span data-ttu-id="19c04-158">False</span><span class="sxs-lookup"><span data-stu-id="19c04-158">False</span></span> | <span data-ttu-id="19c04-159">Compliant</span><span class="sxs-lookup"><span data-stu-id="19c04-159">Compliant</span></span> |
| <span data-ttu-id="19c04-160">New</span><span class="sxs-lookup"><span data-stu-id="19c04-160">New</span></span> | <span data-ttu-id="19c04-161">Audit, AuditIfNotExist\*</span><span class="sxs-lookup"><span data-stu-id="19c04-161">Audit, AuditIfNotExist\*</span></span> | <span data-ttu-id="19c04-162">True</span><span class="sxs-lookup"><span data-stu-id="19c04-162">True</span></span> | <span data-ttu-id="19c04-163">Non-Compliant</span><span class="sxs-lookup"><span data-stu-id="19c04-163">Non-Compliant</span></span> |
| <span data-ttu-id="19c04-164">New</span><span class="sxs-lookup"><span data-stu-id="19c04-164">New</span></span> | <span data-ttu-id="19c04-165">Audit, AuditIfNotExist\*</span><span class="sxs-lookup"><span data-stu-id="19c04-165">Audit, AuditIfNotExist\*</span></span> | <span data-ttu-id="19c04-166">False</span><span class="sxs-lookup"><span data-stu-id="19c04-166">False</span></span> | <span data-ttu-id="19c04-167">Compliant</span><span class="sxs-lookup"><span data-stu-id="19c04-167">Compliant</span></span> |

<span data-ttu-id="19c04-168">\* The Append, DeployIfNotExist, and AuditIfNotExist effects require the IF statement to be TRUE.</span><span class="sxs-lookup"><span data-stu-id="19c04-168">\* The Append, DeployIfNotExist, and AuditIfNotExist effects require the IF statement to be TRUE.</span></span> <span data-ttu-id="19c04-169">The effects also require the existence condition to be FALSE to be non-compliant.</span><span class="sxs-lookup"><span data-stu-id="19c04-169">The effects also require the existence condition to be FALSE to be non-compliant.</span></span> <span data-ttu-id="19c04-170">When TRUE, the IF condition triggers evaluation of the existence condition for the related resources.</span><span class="sxs-lookup"><span data-stu-id="19c04-170">When TRUE, the IF condition triggers evaluation of the existence condition for the related resources.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="19c04-171">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="19c04-171">Clean up resources</span></span>

<span data-ttu-id="19c04-172">Other guides in this collection build upon this quickstart.</span><span class="sxs-lookup"><span data-stu-id="19c04-172">Other guides in this collection build upon this quickstart.</span></span> <span data-ttu-id="19c04-173">If you plan to continue to work with subsequent tutorials, do not clean up the resources created in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="19c04-173">If you plan to continue to work with subsequent tutorials, do not clean up the resources created in this quickstart.</span></span> <span data-ttu-id="19c04-174">If you do not plan to continue, use the following steps to delete all resources created by this quickstart in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="19c04-174">If you do not plan to continue, use the following steps to delete all resources created by this quickstart in the Azure portal.</span></span>

1. <span data-ttu-id="19c04-175">Select **Compliance** (or **Assignments**) in the left side of the Azure Policy page and locate the **Audit VMs that do not use managed disks** policy assignment you created.</span><span class="sxs-lookup"><span data-stu-id="19c04-175">Select **Compliance** (or **Assignments**) in the left side of the Azure Policy page and locate the **Audit VMs that do not use managed disks** policy assignment you created.</span></span>

2. <span data-ttu-id="19c04-176">Right-click the **Audit VMs that do not use managed disks** policy assignment and select **Delete assignment**</span><span class="sxs-lookup"><span data-stu-id="19c04-176">Right-click the **Audit VMs that do not use managed disks** policy assignment and select **Delete assignment**</span></span>

   ![Delete an assignment](media/assign-policy-definition/delete-assignment.png)

## <a name="next-steps"></a><span data-ttu-id="19c04-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="19c04-178">Next steps</span></span>

<span data-ttu-id="19c04-179">In this quickstart, you assigned a policy definition to a scope and evaluated its compliance report.</span><span class="sxs-lookup"><span data-stu-id="19c04-179">In this quickstart, you assigned a policy definition to a scope and evaluated its compliance report.</span></span> <span data-ttu-id="19c04-180">The policy definition ensures that all the resources in the scope are compliant and identifies which ones aren’t.</span><span class="sxs-lookup"><span data-stu-id="19c04-180">The policy definition ensures that all the resources in the scope are compliant and identifies which ones aren’t.</span></span>

<span data-ttu-id="19c04-181">To learn more about assigning policies to ensure that **future** resources that get created are compliant, continue to the tutorial for:</span><span class="sxs-lookup"><span data-stu-id="19c04-181">To learn more about assigning policies to ensure that **future** resources that get created are compliant, continue to the tutorial for:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="19c04-182">Creating and managing policies</span><span class="sxs-lookup"><span data-stu-id="19c04-182">Creating and managing policies</span></span>](create-manage-policy.md)