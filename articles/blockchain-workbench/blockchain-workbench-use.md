---
title: Using applications in Azure Blockchain Workbench
description: How to use application contracts in Azure Blockchain Workbench.
services: azure-blockchain
keywords: ''
author: PatAltimore
ms.author: patricka
ms.date: 5/16/2018
ms.topic: article
ms.service: azure-blockchain
ms.reviewer: zeyadr
manager: femila
ms.openlocfilehash: e17a9275792e3a7fdbea6e3b95e596eaa15f4359
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864415"
---
# <a name="using-applications-in-azure-blockchain-workbench"></a><span data-ttu-id="0bf6c-103">Using applications in Azure Blockchain Workbench</span><span class="sxs-lookup"><span data-stu-id="0bf6c-103">Using applications in Azure Blockchain Workbench</span></span>

<span data-ttu-id="0bf6c-104">You can use Blockchain Workbench to create and take actions on contracts.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-104">You can use Blockchain Workbench to create and take actions on contracts.</span></span> <span data-ttu-id="0bf6c-105">You can also view contract details such as status and transaction history.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-105">You can also view contract details such as status and transaction history.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0bf6c-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0bf6c-106">Prerequisites</span></span>

* <span data-ttu-id="0bf6c-107">A Blockchain Workbench deployment.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-107">A Blockchain Workbench deployment.</span></span> <span data-ttu-id="0bf6c-108">For more information, see [Azure Blockchain Workbench deployment](blockchain-workbench-deploy.md) for details on deployment</span><span class="sxs-lookup"><span data-stu-id="0bf6c-108">For more information, see [Azure Blockchain Workbench deployment](blockchain-workbench-deploy.md) for details on deployment</span></span>
* <span data-ttu-id="0bf6c-109">A deployed blockchain application in Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-109">A deployed blockchain application in Blockchain Workbench.</span></span> <span data-ttu-id="0bf6c-110">See [Create a blockchain application in Azure Blockchain Workbench](blockchain-workbench-create-app.md)</span><span class="sxs-lookup"><span data-stu-id="0bf6c-110">See [Create a blockchain application in Azure Blockchain Workbench](blockchain-workbench-create-app.md)</span></span>

<span data-ttu-id="0bf6c-111">[Open the Blockchain Workbench](blockchain-workbench-deploy.md#blockchain-workbench-web-url) in your browser.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-111">[Open the Blockchain Workbench](blockchain-workbench-deploy.md#blockchain-workbench-web-url) in your browser.</span></span>

![Blockchain Workbench](media/blockchain-workbench-use/workbench.png)

<span data-ttu-id="0bf6c-113">You need to sign in as a member of the Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-113">You need to sign in as a member of the Blockchain Workbench.</span></span> <span data-ttu-id="0bf6c-114">If there are no applications listed, you are a member of Blockchain Workbench but not a member of any applications.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-114">If there are no applications listed, you are a member of Blockchain Workbench but not a member of any applications.</span></span> <span data-ttu-id="0bf6c-115">The Blockchain Workbench administrator can assign members to applications.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-115">The Blockchain Workbench administrator can assign members to applications.</span></span>

## <a name="create-new-contract"></a><span data-ttu-id="0bf6c-116">Create new contract</span><span class="sxs-lookup"><span data-stu-id="0bf6c-116">Create new contract</span></span> 

<span data-ttu-id="0bf6c-117">To create a new contract, you need to be a member specified as an contract **initiator**.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-117">To create a new contract, you need to be a member specified as an contract **initiator**.</span></span> <span data-ttu-id="0bf6c-118">For information defining application roles and initiators for the contract, see [workflows in the configuration overview](blockchain-workbench-configuration-overview.md#workflows).</span><span class="sxs-lookup"><span data-stu-id="0bf6c-118">For information defining application roles and initiators for the contract, see [workflows in the configuration overview](blockchain-workbench-configuration-overview.md#workflows).</span></span> <span data-ttu-id="0bf6c-119">For information on assigning members to application roles, see [add a member to application](blockchain-workbench-manage-users.md#add-member-to-application).</span><span class="sxs-lookup"><span data-stu-id="0bf6c-119">For information on assigning members to application roles, see [add a member to application](blockchain-workbench-manage-users.md#add-member-to-application).</span></span>

1. <span data-ttu-id="0bf6c-120">In Blockchain Workbench application section, select the application tile that contains the contract you want to create.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-120">In Blockchain Workbench application section, select the application tile that contains the contract you want to create.</span></span> <span data-ttu-id="0bf6c-121">A list of active contracts are displayed.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-121">A list of active contracts are displayed.</span></span>

2. <span data-ttu-id="0bf6c-122">To create a new contract, select **New contract**.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-122">To create a new contract, select **New contract**.</span></span>

    ![New contract button](media/blockchain-workbench-use/contract-list.png)

3. <span data-ttu-id="0bf6c-124">The **New contract** pane is displayed.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-124">The **New contract** pane is displayed.</span></span> <span data-ttu-id="0bf6c-125">Specify the initial parameters values.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-125">Specify the initial parameters values.</span></span> <span data-ttu-id="0bf6c-126">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-126">Select **Create**.</span></span>

    ![New contract pane](media/blockchain-workbench-use/new-contract.png)

    <span data-ttu-id="0bf6c-128">The newly created contract is displayed in the list with the other active contracts.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-128">The newly created contract is displayed in the list with the other active contracts.</span></span>

    ![Active contracts list](media/blockchain-workbench-use/active-contracts.png)

## <a name="take-action-on-contract"></a><span data-ttu-id="0bf6c-130">Take action on contract</span><span class="sxs-lookup"><span data-stu-id="0bf6c-130">Take action on contract</span></span>

<span data-ttu-id="0bf6c-131">Depending on the state the contract is in, members can take actions to transition to the next state of the contract.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-131">Depending on the state the contract is in, members can take actions to transition to the next state of the contract.</span></span> <span data-ttu-id="0bf6c-132">Actions are defined as [transitions](blockchain-workbench-configuration-overview.md#transitions) within a [state](blockchain-workbench-configuration-overview.md#states).</span><span class="sxs-lookup"><span data-stu-id="0bf6c-132">Actions are defined as [transitions](blockchain-workbench-configuration-overview.md#transitions) within a [state](blockchain-workbench-configuration-overview.md#states).</span></span> <span data-ttu-id="0bf6c-133">Members belonging to an allowed application or instance role for the transition can take the action.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-133">Members belonging to an allowed application or instance role for the transition can take the action.</span></span> 

1. <span data-ttu-id="0bf6c-134">In Blockchain Workbench application section, select the application tile that contains the contract to take the action.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-134">In Blockchain Workbench application section, select the application tile that contains the contract to take the action.</span></span>
2. <span data-ttu-id="0bf6c-135">Select the contract in the list.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-135">Select the contract in the list.</span></span> <span data-ttu-id="0bf6c-136">Details about the contract are displayed in different sections.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-136">Details about the contract are displayed in different sections.</span></span> 

    ![Contract details](media/blockchain-workbench-use/contract-details.png)

    | <span data-ttu-id="0bf6c-138">Section</span><span class="sxs-lookup"><span data-stu-id="0bf6c-138">Section</span></span>  | <span data-ttu-id="0bf6c-139">Description</span><span class="sxs-lookup"><span data-stu-id="0bf6c-139">Description</span></span>  |
    |---------|---------|
    | <span data-ttu-id="0bf6c-140">Status</span><span class="sxs-lookup"><span data-stu-id="0bf6c-140">Status</span></span> | <span data-ttu-id="0bf6c-141">Lists the current progress within the contract stages</span><span class="sxs-lookup"><span data-stu-id="0bf6c-141">Lists the current progress within the contract stages</span></span> |
    | <span data-ttu-id="0bf6c-142">Details</span><span class="sxs-lookup"><span data-stu-id="0bf6c-142">Details</span></span> | <span data-ttu-id="0bf6c-143">The current values of the contract</span><span class="sxs-lookup"><span data-stu-id="0bf6c-143">The current values of the contract</span></span> |
    | <span data-ttu-id="0bf6c-144">Action</span><span class="sxs-lookup"><span data-stu-id="0bf6c-144">Action</span></span> | <span data-ttu-id="0bf6c-145">Details about the last action</span><span class="sxs-lookup"><span data-stu-id="0bf6c-145">Details about the last action</span></span> |
    | <span data-ttu-id="0bf6c-146">Activity</span><span class="sxs-lookup"><span data-stu-id="0bf6c-146">Activity</span></span> | <span data-ttu-id="0bf6c-147">Transaction history of the contract</span><span class="sxs-lookup"><span data-stu-id="0bf6c-147">Transaction history of the contract</span></span> |
    
3. <span data-ttu-id="0bf6c-148">In the **Action** section, select **Take action**.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-148">In the **Action** section, select **Take action**.</span></span>

4. <span data-ttu-id="0bf6c-149">The details about the current state of the contract are displayed in a pane.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-149">The details about the current state of the contract are displayed in a pane.</span></span> <span data-ttu-id="0bf6c-150">Choose the action you want to take in the drop-down.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-150">Choose the action you want to take in the drop-down.</span></span> 

    ![Choose action](media/blockchain-workbench-use/choose-action.png)

5. <span data-ttu-id="0bf6c-152">Select **Take action** to initiate the action.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-152">Select **Take action** to initiate the action.</span></span>
6. <span data-ttu-id="0bf6c-153">If parameters are required for the action, specify the values for the action.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-153">If parameters are required for the action, specify the values for the action.</span></span>

    ![Take action](media/blockchain-workbench-use/take-action.png)

7. <span data-ttu-id="0bf6c-155">Select **Take action** to execute the action.</span><span class="sxs-lookup"><span data-stu-id="0bf6c-155">Select **Take action** to execute the action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0bf6c-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="0bf6c-156">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0bf6c-157">How to troubleshoot Azure Blockchain Workbench</span><span class="sxs-lookup"><span data-stu-id="0bf6c-157">How to troubleshoot Azure Blockchain Workbench</span></span>](blockchain-workbench-troubleshooting.md)
