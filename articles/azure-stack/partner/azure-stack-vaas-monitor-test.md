---
title: Monitor a test with Azure Stack validation as a service | Microsoft Docs
description: Monitor a test with Azure Stack validation as a service.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 07/24/2018
ms.author: mabrigg
ms.reviewer: johnhas
ms.openlocfilehash: 2dc4d3f2855864ff80648b5b9635ff28c0dacbb7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864952"
---
# <a name="monitor-a-test-with-azure-stack-validation-as-a-service"></a><span data-ttu-id="938c3-103">Monitor a test with Azure Stack validation as a service</span><span class="sxs-lookup"><span data-stu-id="938c3-103">Monitor a test with Azure Stack validation as a service</span></span>

[!INCLUDE [Azure_Stack_Partner](./includes/azure-stack-partner-appliesto.md)]

<span data-ttu-id="938c3-104">The execution of a test can be monitored by viewing the **Operations** page for test suites that are in progress or completed.</span><span class="sxs-lookup"><span data-stu-id="938c3-104">The execution of a test can be monitored by viewing the **Operations** page for test suites that are in progress or completed.</span></span> <span data-ttu-id="938c3-105">This page details the status of the test and its operations.</span><span class="sxs-lookup"><span data-stu-id="938c3-105">This page details the status of the test and its operations.</span></span>

## <a name="monitor-a-test"></a><span data-ttu-id="938c3-106">Monitor a test</span><span class="sxs-lookup"><span data-stu-id="938c3-106">Monitor a test</span></span>

1. <span data-ttu-id="938c3-107">Select a solution.</span><span class="sxs-lookup"><span data-stu-id="938c3-107">Select a solution.</span></span>

2. <span data-ttu-id="938c3-108">Select **Manage** on any workflow tile.</span><span class="sxs-lookup"><span data-stu-id="938c3-108">Select **Manage** on any workflow tile.</span></span>

3. <span data-ttu-id="938c3-109">Click a workflow to open its test summary page.</span><span class="sxs-lookup"><span data-stu-id="938c3-109">Click a workflow to open its test summary page.</span></span>

4. <span data-ttu-id="938c3-110">Expand the context menu **[...]** for any test suite instance.</span><span class="sxs-lookup"><span data-stu-id="938c3-110">Expand the context menu **[...]** for any test suite instance.</span></span>

5. <span data-ttu-id="938c3-111">Select **View Operations**</span><span class="sxs-lookup"><span data-stu-id="938c3-111">Select **View Operations**</span></span>

![Alt text](media\image4.png)

<span data-ttu-id="938c3-113">For tests that have finished running, logs can be downloaded from the test summary page by clicking on **Download logs** in a test's context menu **[...]**. Azure Stack partners can use these logs to debug issues for failed tests.</span><span class="sxs-lookup"><span data-stu-id="938c3-113">For tests that have finished running, logs can be downloaded from the test summary page by clicking on **Download logs** in a test's context menu **[...]**. Azure Stack partners can use these logs to debug issues for failed tests.</span></span>

## <a name="open-the-test-pass-summary"></a><span data-ttu-id="938c3-114">Open the test pass summary</span><span class="sxs-lookup"><span data-stu-id="938c3-114">Open the test pass summary</span></span>

1. <span data-ttu-id="938c3-115">Open the portal.</span><span class="sxs-lookup"><span data-stu-id="938c3-115">Open the portal.</span></span> 
2. <span data-ttu-id="938c3-116">Select the name of an existing solution that contains previously run or scheduled tests.</span><span class="sxs-lookup"><span data-stu-id="938c3-116">Select the name of an existing solution that contains previously run or scheduled tests.</span></span>

    ![Manage test passes](media/managetestpasses.png)

3. <span data-ttu-id="938c3-118">Select **Manage** in the **Test Passes** panel.</span><span class="sxs-lookup"><span data-stu-id="938c3-118">Select **Manage** in the **Test Passes** panel.</span></span>
4. <span data-ttu-id="938c3-119">Select the test pass to open the Test pass summary.</span><span class="sxs-lookup"><span data-stu-id="938c3-119">Select the test pass to open the Test pass summary.</span></span> <span data-ttu-id="938c3-120">You can review the test name, date created, run, how long the test took, and the result (succeeded or failed).</span><span class="sxs-lookup"><span data-stu-id="938c3-120">You can review the test name, date created, run, how long the test took, and the result (succeeded or failed).</span></span>
5. <span data-ttu-id="938c3-121">Select [ **. .  .**</span><span class="sxs-lookup"><span data-stu-id="938c3-121">Select [ **. .  .**</span></span> <span data-ttu-id="938c3-122">].</span><span class="sxs-lookup"><span data-stu-id="938c3-122">].</span></span>

### <a name="test-pass-summary"></a><span data-ttu-id="938c3-123">Test pass summary</span><span class="sxs-lookup"><span data-stu-id="938c3-123">Test pass summary</span></span>

| <span data-ttu-id="938c3-124">Column</span><span class="sxs-lookup"><span data-stu-id="938c3-124">Column</span></span> | <span data-ttu-id="938c3-125">Description</span><span class="sxs-lookup"><span data-stu-id="938c3-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="938c3-126">Test name</span><span class="sxs-lookup"><span data-stu-id="938c3-126">Test name</span></span> | <span data-ttu-id="938c3-127">The name of the test.</span><span class="sxs-lookup"><span data-stu-id="938c3-127">The name of the test.</span></span> <span data-ttu-id="938c3-128">References the validation number.</span><span class="sxs-lookup"><span data-stu-id="938c3-128">References the validation number.</span></span> |
| <span data-ttu-id="938c3-129">Created</span><span class="sxs-lookup"><span data-stu-id="938c3-129">Created</span></span> | <span data-ttu-id="938c3-130">Time the test pass was created.</span><span class="sxs-lookup"><span data-stu-id="938c3-130">Time the test pass was created.</span></span> |
| <span data-ttu-id="938c3-131">Started</span><span class="sxs-lookup"><span data-stu-id="938c3-131">Started</span></span> | <span data-ttu-id="938c3-132">Time the test past ran.</span><span class="sxs-lookup"><span data-stu-id="938c3-132">Time the test past ran.</span></span> |
| <span data-ttu-id="938c3-133">Duration</span><span class="sxs-lookup"><span data-stu-id="938c3-133">Duration</span></span> | <span data-ttu-id="938c3-134">Length of time the time it took the test pass to run.</span><span class="sxs-lookup"><span data-stu-id="938c3-134">Length of time the time it took the test pass to run.</span></span> |
| <span data-ttu-id="938c3-135">Status</span><span class="sxs-lookup"><span data-stu-id="938c3-135">Status</span></span> | <span data-ttu-id="938c3-136">The result (Succeeded or Failed) for the rest pass.</span><span class="sxs-lookup"><span data-stu-id="938c3-136">The result (Succeeded or Failed) for the rest pass.</span></span> |
| <span data-ttu-id="938c3-137">Agent Name</span><span class="sxs-lookup"><span data-stu-id="938c3-137">Agent Name</span></span> | <span data-ttu-id="938c3-138">The fully qualified domain name of the agent.</span><span class="sxs-lookup"><span data-stu-id="938c3-138">The fully qualified domain name of the agent.</span></span> |
| <span data-ttu-id="938c3-139">Total operations</span><span class="sxs-lookup"><span data-stu-id="938c3-139">Total operations</span></span> | <span data-ttu-id="938c3-140">The total number of operations attempted in the test pass.</span><span class="sxs-lookup"><span data-stu-id="938c3-140">The total number of operations attempted in the test pass.</span></span> |
| <span data-ttu-id="938c3-141">Passed operations</span><span class="sxs-lookup"><span data-stu-id="938c3-141">Passed operations</span></span> | <span data-ttu-id="938c3-142">The number of operations that passed in the test pass.</span><span class="sxs-lookup"><span data-stu-id="938c3-142">The number of operations that passed in the test pass.</span></span> |
|  <span data-ttu-id="938c3-143">Failed Operations</span><span class="sxs-lookup"><span data-stu-id="938c3-143">Failed Operations</span></span> | <span data-ttu-id="938c3-144">The number of operations that failed.</span><span class="sxs-lookup"><span data-stu-id="938c3-144">The number of operations that failed.</span></span> |

### <a name="group-columns-in-the-test-pass-summary"></a><span data-ttu-id="938c3-145">Group columns in the test pass summary</span><span class="sxs-lookup"><span data-stu-id="938c3-145">Group columns in the test pass summary</span></span>

<span data-ttu-id="938c3-146">You can select and drag a column into the header to create a group on the column value.</span><span class="sxs-lookup"><span data-stu-id="938c3-146">You can select and drag a column into the header to create a group on the column value.</span></span>

## <a name="reschedule-a-test"></a><span data-ttu-id="938c3-147">Reschedule a test</span><span class="sxs-lookup"><span data-stu-id="938c3-147">Reschedule a test</span></span>

1. <span data-ttu-id="938c3-148">[Open the test pass summary](#open-the-test-pass-summary).</span><span class="sxs-lookup"><span data-stu-id="938c3-148">[Open the test pass summary](#open-the-test-pass-summary).</span></span>
2. <span data-ttu-id="938c3-149">Select **Reschedule** to reschedule the test pass.</span><span class="sxs-lookup"><span data-stu-id="938c3-149">Select **Reschedule** to reschedule the test pass.</span></span>
3. <span data-ttu-id="938c3-150">Enter the Cloud Admin password for your Azure Stack instance.</span><span class="sxs-lookup"><span data-stu-id="938c3-150">Enter the Cloud Admin password for your Azure Stack instance.</span></span>
4. <span data-ttu-id="938c3-151">Enter the Diagnostics Storage Connection string you defined when you set up your account.</span><span class="sxs-lookup"><span data-stu-id="938c3-151">Enter the Diagnostics Storage Connection string you defined when you set up your account.</span></span>
5. <span data-ttu-id="938c3-152">Reschedule the test.</span><span class="sxs-lookup"><span data-stu-id="938c3-152">Reschedule the test.</span></span>

## <a name="cancel-a-test"></a><span data-ttu-id="938c3-153">Cancel a test</span><span class="sxs-lookup"><span data-stu-id="938c3-153">Cancel a test</span></span>

1. <span data-ttu-id="938c3-154">[Open the test pass summary](#open-the-test-pass-summary).</span><span class="sxs-lookup"><span data-stu-id="938c3-154">[Open the test pass summary](#open-the-test-pass-summary).</span></span>
2. <span data-ttu-id="938c3-155">Select **Cancel**.</span><span class="sxs-lookup"><span data-stu-id="938c3-155">Select **Cancel**.</span></span>

## <a name="get-test-information"></a><span data-ttu-id="938c3-156">Get test information</span><span class="sxs-lookup"><span data-stu-id="938c3-156">Get test information</span></span>

1. <span data-ttu-id="938c3-157">[Open the test pass summary](#open-the-test-pass-summary).</span><span class="sxs-lookup"><span data-stu-id="938c3-157">[Open the test pass summary](#open-the-test-pass-summary).</span></span>
2. <span data-ttu-id="938c3-158">Select **View information** to reschedule the test pass.</span><span class="sxs-lookup"><span data-stu-id="938c3-158">Select **View information** to reschedule the test pass.</span></span>

<span data-ttu-id="938c3-159">**Test information**</span><span class="sxs-lookup"><span data-stu-id="938c3-159">**Test information**</span></span>

| <span data-ttu-id="938c3-160">Name</span><span class="sxs-lookup"><span data-stu-id="938c3-160">Name</span></span> | <span data-ttu-id="938c3-161">Description</span><span class="sxs-lookup"><span data-stu-id="938c3-161">Description</span></span> |
| -- | -- |
| <span data-ttu-id="938c3-162">Test name</span><span class="sxs-lookup"><span data-stu-id="938c3-162">Test name</span></span> | <span data-ttu-id="938c3-163">The name of the test, for example, OEM Update on Azure Stack 1806 RC Validation.</span><span class="sxs-lookup"><span data-stu-id="938c3-163">The name of the test, for example, OEM Update on Azure Stack 1806 RC Validation.</span></span> |
| <span data-ttu-id="938c3-164">Test version</span><span class="sxs-lookup"><span data-stu-id="938c3-164">Test version</span></span> | <span data-ttu-id="938c3-165">The version of the test, for example, 5.1.4.0.</span><span class="sxs-lookup"><span data-stu-id="938c3-165">The version of the test, for example, 5.1.4.0.</span></span> |
| <span data-ttu-id="938c3-166">Publisher</span><span class="sxs-lookup"><span data-stu-id="938c3-166">Publisher</span></span> | <span data-ttu-id="938c3-167">The test publisher, such as Microsoft.</span><span class="sxs-lookup"><span data-stu-id="938c3-167">The test publisher, such as Microsoft.</span></span> |
| <span data-ttu-id="938c3-168">Category</span><span class="sxs-lookup"><span data-stu-id="938c3-168">Category</span></span> | <span data-ttu-id="938c3-169">The category of test, such as **Functional** or **Reliability**.</span><span class="sxs-lookup"><span data-stu-id="938c3-169">The category of test, such as **Functional** or **Reliability**.</span></span> |
| <span data-ttu-id="938c3-170">Target services</span><span class="sxs-lookup"><span data-stu-id="938c3-170">Target services</span></span> | <span data-ttu-id="938c3-171">The services being tested, such as VirtualMachines</span><span class="sxs-lookup"><span data-stu-id="938c3-171">The services being tested, such as VirtualMachines</span></span> |
| <span data-ttu-id="938c3-172">Description</span><span class="sxs-lookup"><span data-stu-id="938c3-172">Description</span></span> | <span data-ttu-id="938c3-173">The description of the test.</span><span class="sxs-lookup"><span data-stu-id="938c3-173">The description of the test.</span></span> |
| <span data-ttu-id="938c3-174">Estimated duration (minutes)</span><span class="sxs-lookup"><span data-stu-id="938c3-174">Estimated duration (minutes)</span></span> | <span data-ttu-id="938c3-175">The length of time in minutes the test took to run.</span><span class="sxs-lookup"><span data-stu-id="938c3-175">The length of time in minutes the test took to run.</span></span> |
| <span data-ttu-id="938c3-176">Links</span><span class="sxs-lookup"><span data-stu-id="938c3-176">Links</span></span> | <span data-ttu-id="938c3-177">A link to GitHub Issue Tracker.</span><span class="sxs-lookup"><span data-stu-id="938c3-177">A link to GitHub Issue Tracker.</span></span> |

## <a name="get-test-parameters"></a><span data-ttu-id="938c3-178">Get test parameters</span><span class="sxs-lookup"><span data-stu-id="938c3-178">Get test parameters</span></span>

1. <span data-ttu-id="938c3-179">[Open the test pass summary](#open-the-test-pass-summary).</span><span class="sxs-lookup"><span data-stu-id="938c3-179">[Open the test pass summary](#open-the-test-pass-summary).</span></span>
2. <span data-ttu-id="938c3-180">Select **View parameters** to reschedule the test pass.</span><span class="sxs-lookup"><span data-stu-id="938c3-180">Select **View parameters** to reschedule the test pass.</span></span>

<span data-ttu-id="938c3-181">**Parameters**</span><span class="sxs-lookup"><span data-stu-id="938c3-181">**Parameters**</span></span>

| <span data-ttu-id="938c3-182">Name</span><span class="sxs-lookup"><span data-stu-id="938c3-182">Name</span></span> | <span data-ttu-id="938c3-183">Description</span><span class="sxs-lookup"><span data-stu-id="938c3-183">Description</span></span> |
| -- | -- |
| <span data-ttu-id="938c3-184">Test name</span><span class="sxs-lookup"><span data-stu-id="938c3-184">Test name</span></span> | <span data-ttu-id="938c3-185">The name of the test, for example, oemupdate1806test.</span><span class="sxs-lookup"><span data-stu-id="938c3-185">The name of the test, for example, oemupdate1806test.</span></span> |
| <span data-ttu-id="938c3-186">Test version</span><span class="sxs-lookup"><span data-stu-id="938c3-186">Test version</span></span> | <span data-ttu-id="938c3-187">The version of the rest, for example, 5.1.4.0.</span><span class="sxs-lookup"><span data-stu-id="938c3-187">The version of the rest, for example, 5.1.4.0.</span></span> |
| <span data-ttu-id="938c3-188">Test instance ID</span><span class="sxs-lookup"><span data-stu-id="938c3-188">Test instance ID</span></span> | <span data-ttu-id="938c3-189">A GUID identifying the specific instance of the test, for example, 20b20645-b400-4f0d-bf6f-1264d866ada9.</span><span class="sxs-lookup"><span data-stu-id="938c3-189">A GUID identifying the specific instance of the test, for example, 20b20645-b400-4f0d-bf6f-1264d866ada9.</span></span> |
| <span data-ttu-id="938c3-190">cloudAdminUser</span><span class="sxs-lookup"><span data-stu-id="938c3-190">cloudAdminUser</span></span> | <span data-ttu-id="938c3-191">The name of the account used as the cloud administrator, for example, **cloudadmin**.</span><span class="sxs-lookup"><span data-stu-id="938c3-191">The name of the account used as the cloud administrator, for example, **cloudadmin**.</span></span> |
| <span data-ttu-id="938c3-192">DiagnosticsContainerName</span><span class="sxs-lookup"><span data-stu-id="938c3-192">DiagnosticsContainerName</span></span> | <span data-ttu-id="938c3-193">The ID of the diagnostic container, for example, 04dd3815-5f35-4158-92ea-698027693080.</span><span class="sxs-lookup"><span data-stu-id="938c3-193">The ID of the diagnostic container, for example, 04dd3815-5f35-4158-92ea-698027693080.</span></span> |

## <a name="get-test-operations"></a><span data-ttu-id="938c3-194">Get test operations</span><span class="sxs-lookup"><span data-stu-id="938c3-194">Get test operations</span></span>

1. <span data-ttu-id="938c3-195">[Open the test pass summary](#open-the-test-pass-summary).</span><span class="sxs-lookup"><span data-stu-id="938c3-195">[Open the test pass summary](#open-the-test-pass-summary).</span></span>
2. <span data-ttu-id="938c3-196">Select **View operations** to reschedule the test pass.</span><span class="sxs-lookup"><span data-stu-id="938c3-196">Select **View operations** to reschedule the test pass.</span></span> <span data-ttu-id="938c3-197">The operations summary pane opens.</span><span class="sxs-lookup"><span data-stu-id="938c3-197">The operations summary pane opens.</span></span>

## <a name="get-test-logs"></a><span data-ttu-id="938c3-198">Get test logs</span><span class="sxs-lookup"><span data-stu-id="938c3-198">Get test logs</span></span>

1. <span data-ttu-id="938c3-199">[Open the test pass summary](#open-the-test-pass-summary).</span><span class="sxs-lookup"><span data-stu-id="938c3-199">[Open the test pass summary](#open-the-test-pass-summary).</span></span>
2. <span data-ttu-id="938c3-200">Select **Download logs** to reschedule the test pass.</span><span class="sxs-lookup"><span data-stu-id="938c3-200">Select **Download logs** to reschedule the test pass.</span></span>  
    <span data-ttu-id="938c3-201">A zip file named ReleaseYYYY-MM-DD.zip containing the logs downloads.</span><span class="sxs-lookup"><span data-stu-id="938c3-201">A zip file named ReleaseYYYY-MM-DD.zip containing the logs downloads.</span></span>

## <a name="next-steps"></a><span data-ttu-id="938c3-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="938c3-202">Next steps</span></span>

- <span data-ttu-id="938c3-203">To learn more about [Azure Stack validation as a service](https://docs.microsoft.com/azure/azure-stack/partner).</span><span class="sxs-lookup"><span data-stu-id="938c3-203">To learn more about [Azure Stack validation as a service](https://docs.microsoft.com/azure/azure-stack/partner).</span></span>
