---
title: Transform XML with XSLT maps - Azure Logic Apps | Microsoft Docs
description: Add XSLT maps to transform XML data with Azure Logic Apps and the Enterprise Integration Pack
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 90f5cfc4-46b2-4ef7-8ac4-486bb0e3f289
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: estfan
ms.openlocfilehash: ccaefe1cfa58096f6a83c202d00a17501fa07881
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563051"
---
# <a name="add-maps-for-xml-data-transform"></a><span data-ttu-id="d222a-103">Add maps for XML data transform</span><span class="sxs-lookup"><span data-stu-id="d222a-103">Add maps for XML data transform</span></span>

<span data-ttu-id="d222a-104">Enterprise integration uses maps to transform XML data between formats.</span><span class="sxs-lookup"><span data-stu-id="d222a-104">Enterprise integration uses maps to transform XML data between formats.</span></span> <span data-ttu-id="d222a-105">A map is an XML document that defines the data in a document that should be transformed into another format.</span><span class="sxs-lookup"><span data-stu-id="d222a-105">A map is an XML document that defines the data in a document that should be transformed into another format.</span></span> 

## <a name="why-use-maps"></a><span data-ttu-id="d222a-106">Why use maps?</span><span class="sxs-lookup"><span data-stu-id="d222a-106">Why use maps?</span></span>

<span data-ttu-id="d222a-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses the YYYMMDD format for dates.</span><span class="sxs-lookup"><span data-stu-id="d222a-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses the YYYMMDD format for dates.</span></span> <span data-ttu-id="d222a-108">However, in your organization, you store dates in the MMDDYYY format.</span><span class="sxs-lookup"><span data-stu-id="d222a-108">However, in your organization, you store dates in the MMDDYYY format.</span></span> <span data-ttu-id="d222a-109">You can use a map to *transform* the YYYMMDD date format into the MMDDYYY before storing the order or invoice details in your customer activity database.</span><span class="sxs-lookup"><span data-stu-id="d222a-109">You can use a map to *transform* the YYYMMDD date format into the MMDDYYY before storing the order or invoice details in your customer activity database.</span></span>

## <a name="how-do-i-create-a-map"></a><span data-ttu-id="d222a-110">How do I create a map?</span><span class="sxs-lookup"><span data-stu-id="d222a-110">How do I create a map?</span></span>

<span data-ttu-id="d222a-111">You can create BizTalk Integration projects with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack") for Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="d222a-111">You can create BizTalk Integration projects with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack") for Visual Studio 2015.</span></span> <span data-ttu-id="d222a-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span><span class="sxs-lookup"><span data-stu-id="d222a-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span></span> <span data-ttu-id="d222a-113">After you build this project, you will have an XSLT document.</span><span class="sxs-lookup"><span data-stu-id="d222a-113">After you build this project, you will have an XSLT document.</span></span>

## <a name="how-do-i-add-a-map"></a><span data-ttu-id="d222a-114">How do I add a map?</span><span class="sxs-lookup"><span data-stu-id="d222a-114">How do I add a map?</span></span>

1. <span data-ttu-id="d222a-115">In the Azure portal, select **Browse**.</span><span class="sxs-lookup"><span data-stu-id="d222a-115">In the Azure portal, select **Browse**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="d222a-116">In the filter search box, enter **integration**, then select **Integration Accounts** from the results list.</span><span class="sxs-lookup"><span data-stu-id="d222a-116">In the filter search box, enter **integration**, then select **Integration Accounts** from the results list.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="d222a-117">Select the integration account where you want to add the map.</span><span class="sxs-lookup"><span data-stu-id="d222a-117">Select the integration account where you want to add the map.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="d222a-118">Select the **Maps** tile.</span><span class="sxs-lookup"><span data-stu-id="d222a-118">Select the **Maps** tile.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-maps/map-1.png)

5. <span data-ttu-id="d222a-119">After the Maps blade opens, choose **Add**.</span><span class="sxs-lookup"><span data-stu-id="d222a-119">After the Maps blade opens, choose **Add**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-maps/map-2.png)  

6. <span data-ttu-id="d222a-120">Enter a **Name** for your map.</span><span class="sxs-lookup"><span data-stu-id="d222a-120">Enter a **Name** for your map.</span></span> <span data-ttu-id="d222a-121">To upload the map file, choose the folder icon on the right side of the **Map** text box.</span><span class="sxs-lookup"><span data-stu-id="d222a-121">To upload the map file, choose the folder icon on the right side of the **Map** text box.</span></span> <span data-ttu-id="d222a-122">After the upload process completes, choose **OK**.</span><span class="sxs-lookup"><span data-stu-id="d222a-122">After the upload process completes, choose **OK**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-maps/map-3.png)

7. <span data-ttu-id="d222a-123">After Azure adds the map to your integration account, you get an onscreen message that shows whether your map file was added or not.</span><span class="sxs-lookup"><span data-stu-id="d222a-123">After Azure adds the map to your integration account, you get an onscreen message that shows whether your map file was added or not.</span></span> <span data-ttu-id="d222a-124">After you get this message, choose the **Maps** tile so you can view the newly added map.</span><span class="sxs-lookup"><span data-stu-id="d222a-124">After you get this message, choose the **Maps** tile so you can view the newly added map.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a><span data-ttu-id="d222a-125">How do I edit a map?</span><span class="sxs-lookup"><span data-stu-id="d222a-125">How do I edit a map?</span></span>

<span data-ttu-id="d222a-126">You must upload a new map file with the changes that you want.</span><span class="sxs-lookup"><span data-stu-id="d222a-126">You must upload a new map file with the changes that you want.</span></span> <span data-ttu-id="d222a-127">You can first download the map for editing.</span><span class="sxs-lookup"><span data-stu-id="d222a-127">You can first download the map for editing.</span></span>

<span data-ttu-id="d222a-128">To upload a new map that replaces the existing map, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="d222a-128">To upload a new map that replaces the existing map, follow these steps.</span></span>

1. <span data-ttu-id="d222a-129">Choose the **Maps** tile.</span><span class="sxs-lookup"><span data-stu-id="d222a-129">Choose the **Maps** tile.</span></span>

2. <span data-ttu-id="d222a-130">After the Maps blade opens, select the map that you want to edit.</span><span class="sxs-lookup"><span data-stu-id="d222a-130">After the Maps blade opens, select the map that you want to edit.</span></span>

3. <span data-ttu-id="d222a-131">On the **Maps** blade, choose **Update**.</span><span class="sxs-lookup"><span data-stu-id="d222a-131">On the **Maps** blade, choose **Update**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-maps/edit-1.png)

4. <span data-ttu-id="d222a-132">In the file picker, select the map file that you want to upload, then select **Open**.</span><span class="sxs-lookup"><span data-stu-id="d222a-132">In the file picker, select the map file that you want to upload, then select **Open**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-to-delete-a-map"></a><span data-ttu-id="d222a-133">How to delete a map?</span><span class="sxs-lookup"><span data-stu-id="d222a-133">How to delete a map?</span></span>

1. <span data-ttu-id="d222a-134">Choose the **Maps** tile.</span><span class="sxs-lookup"><span data-stu-id="d222a-134">Choose the **Maps** tile.</span></span>

2. <span data-ttu-id="d222a-135">After the Maps blade opens, select the map you want to delete.</span><span class="sxs-lookup"><span data-stu-id="d222a-135">After the Maps blade opens, select the map you want to delete.</span></span>

3. <span data-ttu-id="d222a-136">Choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="d222a-136">Choose **Delete**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-maps/delete.png)

4. <span data-ttu-id="d222a-137">Confirm that you want to delete the map.</span><span class="sxs-lookup"><span data-stu-id="d222a-137">Confirm that you want to delete the map.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a><span data-ttu-id="d222a-138">Next Steps</span><span class="sxs-lookup"><span data-stu-id="d222a-138">Next Steps</span></span>
* [<span data-ttu-id="d222a-139">Learn more about the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="d222a-139">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack")  
* [<span data-ttu-id="d222a-140">Learn more about agreements</span><span class="sxs-lookup"><span data-stu-id="d222a-140">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Learn about enterprise integration agreements")  
* [<span data-ttu-id="d222a-141">Learn more about transforms</span><span class="sxs-lookup"><span data-stu-id="d222a-141">Learn more about transforms</span></span>](logic-apps-enterprise-integration-transform.md "Learn about enterprise integration transforms")  












