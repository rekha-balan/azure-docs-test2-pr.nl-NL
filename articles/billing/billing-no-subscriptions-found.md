---
title: No subscriptions found error when try to sign in to Azure portal or Azure account center | Microsoft Docs
description: Provides the solution for a problem in which No subscriptions found error occurs when sign in to Azure portal or Azure account center.
services: ''
documentationcenter: ''
author: genlin
manager: jlian
editor: ''
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: troubleshooting
ms.date: 05/11/2018
ms.author: genli
ms.openlocfilehash: b5fd1db06d13ce0c12a80752e64a6f5c64867761
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966991"
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a>No subscriptions found error in Azure portal or Azure account center

You might receive a "No subscriptions found" error message when you try to sign in to the [Azure portal](https://portal.azure.com/) or the [Azure Account Center](https://account.windowsazure.com/Subscriptions). This article provides a solution for this problem.

## <a name="symptom"></a>Symptom

When you try to sign in to the [Azure portal](https://portal.azure.com/) or the [Azure account center](https://account.windowsazure.com/Subscriptions), you receive the following error message: "No subscriptions found".

## <a name="cause"></a>Cause

This problem occurs if you selected at the wrong directory, or if your account doesn’t have sufficient permissions. 

## <a name="solution"></a>Solution

### <a name="scenario-1-error-message-is-received-in-the-azure-portalhttpsportalazurecom"></a>Scenario 1: Error message is received in the [Azure portal](https://portal.azure.com)

To fix this issue:

* Make sure that the correct Azure directory is selected by clicking your account at the top right.

  ![Select the directory at the top right of the Azure portal](./media/billing-no-subscriptions-found/directory-switch.png)
* If the right Azure directory is selected but you still receive the error message, [assign the Owner role to your account](../role-based-access-control/role-assignments-portal.md).

### <a name="scenario-2-error-message-is-received-in-the-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a>Scenario 2: Error message is received in the [Azure Account Center](https://account.windowsazure.com/Subscriptions)

Check whether the account that you used is the Account Administrator. To verify who the Account Administrator is, follow these steps:

1. Sign in to the [Subscriptions view in the Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).
1. Select the subscription you want to check, and then look under **Settings**.
1. Select **Properties**. The account administrator of the subscription is displayed in the **Account Admin** box.  

## <a name="need-help-contact-support"></a>Need help? Contact support.

If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) to get your issue resolved quickly. 
