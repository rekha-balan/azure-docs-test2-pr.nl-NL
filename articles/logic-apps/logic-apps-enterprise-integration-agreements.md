---
title: Agreements for B2B communication - Azure Logic Apps | Microsoft Docs
description: Create agreements so partners can communicate in B2B scenarios for Azure Logic Apps and the Enterprise Integration Pack
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 447ffb8e-3e91-4403-872b-2f496495899d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: estfan
ms.openlocfilehash: 1068b5bd5f2c86de0c82f5a96cb2718645c0a3d3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551677"
---
# <a name="partner-agreements-for-b2b-communication-with-azure-logic-apps-and-enterprise-integration-pack"></a><span data-ttu-id="21176-103">Partner agreements for B2B communication with Azure Logic Apps and Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="21176-103">Partner agreements for B2B communication with Azure Logic Apps and Enterprise Integration Pack</span></span>

<span data-ttu-id="21176-104">Agreements let business entities communicate seamlessly using industry standard protocols and are the cornerstone for business-to-business (B2B) communication.</span><span class="sxs-lookup"><span data-stu-id="21176-104">Agreements let business entities communicate seamlessly using industry standard protocols and are the cornerstone for business-to-business (B2B) communication.</span></span> <span data-ttu-id="21176-105">When enabling B2B scenarios for logic apps with the Enterprise Integration Pack, an agreement is a communications arrangement between B2B trading partners.</span><span class="sxs-lookup"><span data-stu-id="21176-105">When enabling B2B scenarios for logic apps with the Enterprise Integration Pack, an agreement is a communications arrangement between B2B trading partners.</span></span> <span data-ttu-id="21176-106">This agreement is based on the communications that the partners want to establish and is protocol or transport-specific.</span><span class="sxs-lookup"><span data-stu-id="21176-106">This agreement is based on the communications that the partners want to establish and is protocol or transport-specific.</span></span>

<span data-ttu-id="21176-107">Enterprise integration supports these protocol or transport standards:</span><span class="sxs-lookup"><span data-stu-id="21176-107">Enterprise integration supports these protocol or transport standards:</span></span>

* [<span data-ttu-id="21176-108">AS2</span><span class="sxs-lookup"><span data-stu-id="21176-108">AS2</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="21176-109">X12</span><span class="sxs-lookup"><span data-stu-id="21176-109">X12</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="21176-110">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="21176-110">EDIFACT</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="why-use-agreements"></a><span data-ttu-id="21176-111">Why use agreements</span><span class="sxs-lookup"><span data-stu-id="21176-111">Why use agreements</span></span>

<span data-ttu-id="21176-112">Here are some common benefits when using agreements:</span><span class="sxs-lookup"><span data-stu-id="21176-112">Here are some common benefits when using agreements:</span></span>

* <span data-ttu-id="21176-113">Enables different organizations and businesses to exchange information in a well-known format.</span><span class="sxs-lookup"><span data-stu-id="21176-113">Enables different organizations and businesses to exchange information in a well-known format.</span></span>
* <span data-ttu-id="21176-114">Improves efficiency when conducting B2B transactions</span><span class="sxs-lookup"><span data-stu-id="21176-114">Improves efficiency when conducting B2B transactions</span></span>
* <span data-ttu-id="21176-115">Easy to create, manage, and use when creating enterprise integration apps</span><span class="sxs-lookup"><span data-stu-id="21176-115">Easy to create, manage, and use when creating enterprise integration apps</span></span>

## <a name="how-to-create-agreements"></a><span data-ttu-id="21176-116">How to create agreements</span><span class="sxs-lookup"><span data-stu-id="21176-116">How to create agreements</span></span>

* [<span data-ttu-id="21176-117">Create an AS2 agreement</span><span class="sxs-lookup"><span data-stu-id="21176-117">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="21176-118">Create an X12 agreement</span><span class="sxs-lookup"><span data-stu-id="21176-118">Create an X12 agreement</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="21176-119">Create an EDIFACT agreement</span><span class="sxs-lookup"><span data-stu-id="21176-119">Create an EDIFACT agreement</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="how-to-use-an-agreement"></a><span data-ttu-id="21176-120">How to use an agreement</span><span class="sxs-lookup"><span data-stu-id="21176-120">How to use an agreement</span></span>

<span data-ttu-id="21176-121">You can create [logic apps](logic-apps-what-are-logic-apps.md "Learn about Logic apps") with B2B capabilities by using an agreement that you created.</span><span class="sxs-lookup"><span data-stu-id="21176-121">You can create [logic apps](logic-apps-what-are-logic-apps.md "Learn about Logic apps") with B2B capabilities by using an agreement that you created.</span></span>

## <a name="how-to-edit-an-agreement"></a><span data-ttu-id="21176-122">How to edit an agreement</span><span class="sxs-lookup"><span data-stu-id="21176-122">How to edit an agreement</span></span>

<span data-ttu-id="21176-123">You can edit any agreement by following these steps:</span><span class="sxs-lookup"><span data-stu-id="21176-123">You can edit any agreement by following these steps:</span></span>

1. <span data-ttu-id="21176-124">Select the integration account that has the agreement you want to update.</span><span class="sxs-lookup"><span data-stu-id="21176-124">Select the integration account that has the agreement you want to update.</span></span>

2. <span data-ttu-id="21176-125">Choose the **Agreements** tile.</span><span class="sxs-lookup"><span data-stu-id="21176-125">Choose the **Agreements** tile.</span></span>

3. <span data-ttu-id="21176-126">On the **Agreements** blade, select the agreement.</span><span class="sxs-lookup"><span data-stu-id="21176-126">On the **Agreements** blade, select the agreement.</span></span>

4. <span data-ttu-id="21176-127">Choose **Edit**.</span><span class="sxs-lookup"><span data-stu-id="21176-127">Choose **Edit**.</span></span> <span data-ttu-id="21176-128">Make your changes.</span><span class="sxs-lookup"><span data-stu-id="21176-128">Make your changes.</span></span>

5. <span data-ttu-id="21176-129">To save your changes, choose **OK**.</span><span class="sxs-lookup"><span data-stu-id="21176-129">To save your changes, choose **OK**.</span></span>

## <a name="how-to-delete-an-agreement"></a><span data-ttu-id="21176-130">How to delete an agreement</span><span class="sxs-lookup"><span data-stu-id="21176-130">How to delete an agreement</span></span>

<span data-ttu-id="21176-131">You can delete any agreement by following these steps:</span><span class="sxs-lookup"><span data-stu-id="21176-131">You can delete any agreement by following these steps:</span></span>

1. <span data-ttu-id="21176-132">Select the integration account that has the agreement you want to delete.</span><span class="sxs-lookup"><span data-stu-id="21176-132">Select the integration account that has the agreement you want to delete.</span></span>
2. <span data-ttu-id="21176-133">Choose the **Agreements** tile.</span><span class="sxs-lookup"><span data-stu-id="21176-133">Choose the **Agreements** tile.</span></span>
3. <span data-ttu-id="21176-134">On the **Agreements** blade, select the agreement.</span><span class="sxs-lookup"><span data-stu-id="21176-134">On the **Agreements** blade, select the agreement.</span></span>
4. <span data-ttu-id="21176-135">Choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="21176-135">Choose **Delete**.</span></span>
5. <span data-ttu-id="21176-136">Confirm that you want to delete the selected agreement.</span><span class="sxs-lookup"><span data-stu-id="21176-136">Confirm that you want to delete the selected agreement.</span></span>

    <span data-ttu-id="21176-137">The Agreements blade no longer shows the deleted agreement.</span><span class="sxs-lookup"><span data-stu-id="21176-137">The Agreements blade no longer shows the deleted agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21176-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="21176-138">Next steps</span></span>
* [<span data-ttu-id="21176-139">Create an AS2 agreement</span><span class="sxs-lookup"><span data-stu-id="21176-139">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
