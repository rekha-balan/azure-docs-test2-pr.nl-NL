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
# <a name="using-applications-in-azure-blockchain-workbench"></a>Using applications in Azure Blockchain Workbench

You can use Blockchain Workbench to create and take actions on contracts. You can also view contract details such as status and transaction history.

## <a name="prerequisites"></a>Prerequisites

* A Blockchain Workbench deployment. For more information, see [Azure Blockchain Workbench deployment](blockchain-workbench-deploy.md) for details on deployment
* A deployed blockchain application in Blockchain Workbench. See [Create a blockchain application in Azure Blockchain Workbench](blockchain-workbench-create-app.md)

[Open the Blockchain Workbench](blockchain-workbench-deploy.md#blockchain-workbench-web-url) in your browser.

![Blockchain Workbench](media/blockchain-workbench-use/workbench.png)

You need to sign in as a member of the Blockchain Workbench. If there are no applications listed, you are a member of Blockchain Workbench but not a member of any applications. The Blockchain Workbench administrator can assign members to applications.

## <a name="create-new-contract"></a>Create new contract 

To create a new contract, you need to be a member specified as an contract **initiator**. For information defining application roles and initiators for the contract, see [workflows in the configuration overview](blockchain-workbench-configuration-overview.md#workflows). For information on assigning members to application roles, see [add a member to application](blockchain-workbench-manage-users.md#add-member-to-application).

1. In Blockchain Workbench application section, select the application tile that contains the contract you want to create. A list of active contracts are displayed.

2. To create a new contract, select **New contract**.

    ![New contract button](media/blockchain-workbench-use/contract-list.png)

3. The **New contract** pane is displayed. Specify the initial parameters values. Select **Create**.

    ![New contract pane](media/blockchain-workbench-use/new-contract.png)

    The newly created contract is displayed in the list with the other active contracts.

    ![Active contracts list](media/blockchain-workbench-use/active-contracts.png)

## <a name="take-action-on-contract"></a>Take action on contract

Depending on the state the contract is in, members can take actions to transition to the next state of the contract. Actions are defined as [transitions](blockchain-workbench-configuration-overview.md#transitions) within a [state](blockchain-workbench-configuration-overview.md#states). Members belonging to an allowed application or instance role for the transition can take the action. 

1. In Blockchain Workbench application section, select the application tile that contains the contract to take the action.
2. Select the contract in the list. Details about the contract are displayed in different sections. 

    ![Contract details](media/blockchain-workbench-use/contract-details.png)

    | Section  | Description  |
    |---------|---------|
    | Status | Lists the current progress within the contract stages |
    | Details | The current values of the contract |
    | Action | Details about the last action |
    | Activity | Transaction history of the contract |
    
3. In the **Action** section, select **Take action**.

4. The details about the current state of the contract are displayed in a pane. Choose the action you want to take in the drop-down. 

    ![Choose action](media/blockchain-workbench-use/choose-action.png)

5. Select **Take action** to initiate the action.
6. If parameters are required for the action, specify the values for the action.

    ![Take action](media/blockchain-workbench-use/take-action.png)

7. Select **Take action** to execute the action.

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [How to troubleshoot Azure Blockchain Workbench](blockchain-workbench-troubleshooting.md)