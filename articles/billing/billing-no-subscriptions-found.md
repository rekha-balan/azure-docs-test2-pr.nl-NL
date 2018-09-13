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
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a><span data-ttu-id="ee820-103">No subscriptions found error in Azure portal or Azure account center</span><span class="sxs-lookup"><span data-stu-id="ee820-103">No subscriptions found error in Azure portal or Azure account center</span></span>

<span data-ttu-id="ee820-104">You might receive a "No subscriptions found" error message when you try to sign in to the [Azure portal](https://portal.azure.com/) or the [Azure Account Center](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="ee820-104">You might receive a "No subscriptions found" error message when you try to sign in to the [Azure portal](https://portal.azure.com/) or the [Azure Account Center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="ee820-105">This article provides a solution for this problem.</span><span class="sxs-lookup"><span data-stu-id="ee820-105">This article provides a solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="ee820-106">Symptom</span><span class="sxs-lookup"><span data-stu-id="ee820-106">Symptom</span></span>

<span data-ttu-id="ee820-107">When you try to sign in to the [Azure portal](https://portal.azure.com/) or the [Azure account center](https://account.windowsazure.com/Subscriptions), you receive the following error message: "No subscriptions found".</span><span class="sxs-lookup"><span data-stu-id="ee820-107">When you try to sign in to the [Azure portal](https://portal.azure.com/) or the [Azure account center](https://account.windowsazure.com/Subscriptions), you receive the following error message: "No subscriptions found".</span></span>

## <a name="cause"></a><span data-ttu-id="ee820-108">Cause</span><span class="sxs-lookup"><span data-stu-id="ee820-108">Cause</span></span>

<span data-ttu-id="ee820-109">This problem occurs if you selected at the wrong directory, or if your account doesn’t have sufficient permissions.</span><span class="sxs-lookup"><span data-stu-id="ee820-109">This problem occurs if you selected at the wrong directory, or if your account doesn’t have sufficient permissions.</span></span> 

## <a name="solution"></a><span data-ttu-id="ee820-110">Solution</span><span class="sxs-lookup"><span data-stu-id="ee820-110">Solution</span></span>

### <a name="scenario-1-error-message-is-received-in-the-azure-portalhttpsportalazurecom"></a><span data-ttu-id="ee820-111">Scenario 1: Error message is received in the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="ee820-111">Scenario 1: Error message is received in the [Azure portal](https://portal.azure.com)</span></span>

<span data-ttu-id="ee820-112">To fix this issue:</span><span class="sxs-lookup"><span data-stu-id="ee820-112">To fix this issue:</span></span>

* <span data-ttu-id="ee820-113">Make sure that the correct Azure directory is selected by clicking your account at the top right.</span><span class="sxs-lookup"><span data-stu-id="ee820-113">Make sure that the correct Azure directory is selected by clicking your account at the top right.</span></span>

  ![Select the directory at the top right of the Azure portal](./media/billing-no-subscriptions-found/directory-switch.png)
* <span data-ttu-id="ee820-115">If the right Azure directory is selected but you still receive the error message, [assign the Owner role to your account](../role-based-access-control/role-assignments-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ee820-115">If the right Azure directory is selected but you still receive the error message, [assign the Owner role to your account](../role-based-access-control/role-assignments-portal.md).</span></span>

### <a name="scenario-2-error-message-is-received-in-the-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a><span data-ttu-id="ee820-116">Scenario 2: Error message is received in the [Azure Account Center](https://account.windowsazure.com/Subscriptions)</span><span class="sxs-lookup"><span data-stu-id="ee820-116">Scenario 2: Error message is received in the [Azure Account Center](https://account.windowsazure.com/Subscriptions)</span></span>

<span data-ttu-id="ee820-117">Check whether the account that you used is the Account Administrator.</span><span class="sxs-lookup"><span data-stu-id="ee820-117">Check whether the account that you used is the Account Administrator.</span></span> <span data-ttu-id="ee820-118">To verify who the Account Administrator is, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="ee820-118">To verify who the Account Administrator is, follow these steps:</span></span>

1. <span data-ttu-id="ee820-119">Sign in to the [Subscriptions view in the Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span><span class="sxs-lookup"><span data-stu-id="ee820-119">Sign in to the [Subscriptions view in the Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span></span>
1. <span data-ttu-id="ee820-120">Select the subscription you want to check, and then look under **Settings**.</span><span class="sxs-lookup"><span data-stu-id="ee820-120">Select the subscription you want to check, and then look under **Settings**.</span></span>
1. <span data-ttu-id="ee820-121">Select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="ee820-121">Select **Properties**.</span></span> <span data-ttu-id="ee820-122">The account administrator of the subscription is displayed in the **Account Admin** box.</span><span class="sxs-lookup"><span data-stu-id="ee820-122">The account administrator of the subscription is displayed in the **Account Admin** box.</span></span>  

## <a name="need-help-contact-support"></a><span data-ttu-id="ee820-123">Need help?</span><span class="sxs-lookup"><span data-stu-id="ee820-123">Need help?</span></span> <span data-ttu-id="ee820-124">Contact support.</span><span class="sxs-lookup"><span data-stu-id="ee820-124">Contact support.</span></span>

<span data-ttu-id="ee820-125">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) to get your issue resolved quickly.</span><span class="sxs-lookup"><span data-stu-id="ee820-125">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) to get your issue resolved quickly.</span></span> 
