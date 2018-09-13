---
title: Handle EDIFACT messages with UNH 2.5 segements - Azure Logic Apps | Microsoft Docs
description: Resolve EDIFACT documents with UNH2.5 segments in Azure Logic Apps with Enterprise Integration Pack
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: divyaswarnkar
ms.author: divswa
ms.reviewer: jonfan, estfan, LADocs
ms.topic: article
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.date: 04/27/2017
ms.openlocfilehash: 9c8b8611347840dcf49759dac51fb506815cd782
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870957"
---
# <a name="handle-edifact-documents-with-unh25-segments-in-azure-logic-apps"></a><span data-ttu-id="6b8f0-103">Handle EDIFACT documents with UNH2.5 segments in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="6b8f0-103">Handle EDIFACT documents with UNH2.5 segments in Azure Logic Apps</span></span>

<span data-ttu-id="6b8f0-104">When UNH2.5 is present in the EDIFACT document, it is being used for schema lookup.</span><span class="sxs-lookup"><span data-stu-id="6b8f0-104">When UNH2.5 is present in the EDIFACT document, it is being used for schema lookup.</span></span> 

<span data-ttu-id="6b8f0-105">Example: The UNH field is **EAN008** in the EDIFACT message</span><span class="sxs-lookup"><span data-stu-id="6b8f0-105">Example: The UNH field is **EAN008** in the EDIFACT message</span></span>  
<span data-ttu-id="6b8f0-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span><span class="sxs-lookup"><span data-stu-id="6b8f0-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span></span>  

<span data-ttu-id="6b8f0-107">Steps to follow to handle the message</span><span class="sxs-lookup"><span data-stu-id="6b8f0-107">Steps to follow to handle the message</span></span> 
1. <span data-ttu-id="6b8f0-108">Update the schema</span><span class="sxs-lookup"><span data-stu-id="6b8f0-108">Update the schema</span></span>
2. <span data-ttu-id="6b8f0-109">Check the agreement settings</span><span class="sxs-lookup"><span data-stu-id="6b8f0-109">Check the agreement settings</span></span>  

## <a name="update-the-schema"></a><span data-ttu-id="6b8f0-110">Update the schema</span><span class="sxs-lookup"><span data-stu-id="6b8f0-110">Update the schema</span></span>
<span data-ttu-id="6b8f0-111">To process the message, you need to deploy a schema with the UNH2.5 root node name.</span><span class="sxs-lookup"><span data-stu-id="6b8f0-111">To process the message, you need to deploy a schema with the UNH2.5 root node name.</span></span>  <span data-ttu-id="6b8f0-112">For given an example, the schema root name would be **EFACT_D03B_ORDERS_EAN008**</span><span class="sxs-lookup"><span data-stu-id="6b8f0-112">For given an example, the schema root name would be **EFACT_D03B_ORDERS_EAN008**</span></span>  

<span data-ttu-id="6b8f0-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have to deploy an individual schema.</span><span class="sxs-lookup"><span data-stu-id="6b8f0-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have to deploy an individual schema.</span></span>  

## <a name="add-schema-to-the-edifact-agreement"></a><span data-ttu-id="6b8f0-114">Add schema to the EDIFACT agreement</span><span class="sxs-lookup"><span data-stu-id="6b8f0-114">Add schema to the EDIFACT agreement</span></span>
### <a name="edifact-decode"></a><span data-ttu-id="6b8f0-115">EDIFACT Decode</span><span class="sxs-lookup"><span data-stu-id="6b8f0-115">EDIFACT Decode</span></span>
<span data-ttu-id="6b8f0-116">To Decode the incoming message, configure the schema in the EDIFACT agreement receive settings</span><span class="sxs-lookup"><span data-stu-id="6b8f0-116">To Decode the incoming message, configure the schema in the EDIFACT agreement receive settings</span></span>
1. <span data-ttu-id="6b8f0-117">Add the schema to the integration account</span><span class="sxs-lookup"><span data-stu-id="6b8f0-117">Add the schema to the integration account</span></span>    
2. <span data-ttu-id="6b8f0-118">Configure the schema in the EDIFACT agreement receive settings.</span><span class="sxs-lookup"><span data-stu-id="6b8f0-118">Configure the schema in the EDIFACT agreement receive settings.</span></span> 
3. <span data-ttu-id="6b8f0-119">Select EDIFACT agreement and click **Edit as JSON**.</span><span class="sxs-lookup"><span data-stu-id="6b8f0-119">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="6b8f0-120">Add UNH2.5 value in the Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6b8f0-120">Add UNH2.5 value in the Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span></span>

### <a name="edifact-encode"></a><span data-ttu-id="6b8f0-121">EDIFACT Encode</span><span class="sxs-lookup"><span data-stu-id="6b8f0-121">EDIFACT Encode</span></span>
<span data-ttu-id="6b8f0-122">To Encode the incoming message, configure the schema in the EDIFACT agreement send settings</span><span class="sxs-lookup"><span data-stu-id="6b8f0-122">To Encode the incoming message, configure the schema in the EDIFACT agreement send settings</span></span>
1. <span data-ttu-id="6b8f0-123">Add the schema to the integration account</span><span class="sxs-lookup"><span data-stu-id="6b8f0-123">Add the schema to the integration account</span></span>    
2. <span data-ttu-id="6b8f0-124">Configure the schema in the EDIFACT agreement send settings.</span><span class="sxs-lookup"><span data-stu-id="6b8f0-124">Configure the schema in the EDIFACT agreement send settings.</span></span> 
3. <span data-ttu-id="6b8f0-125">Select EDIFACT agreement and click **Edit as JSON**.</span><span class="sxs-lookup"><span data-stu-id="6b8f0-125">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="6b8f0-126">Add UNH2.5 value in the Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span><span class="sxs-lookup"><span data-stu-id="6b8f0-126">Add UNH2.5 value in the Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b8f0-127">Next Steps</span><span class="sxs-lookup"><span data-stu-id="6b8f0-127">Next Steps</span></span>
* [<span data-ttu-id="6b8f0-128">Learn more about integration account agreements</span><span class="sxs-lookup"><span data-stu-id="6b8f0-128">Learn more about integration account agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Learn about enterprise integration agreements")  