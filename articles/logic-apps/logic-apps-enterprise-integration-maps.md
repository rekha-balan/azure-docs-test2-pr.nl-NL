---
title: Transform XML with XSLT maps - Azure Logic Apps | Microsoft Docs
description: Add XSLT maps that transform XML in Azure Logic Apps with Enterprise Integration Pack
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: divyaswarnkar
ms.author: divswa
ms.reviewer: jonfan, estfan, LADocs
ms.topic: article
ms.assetid: 90f5cfc4-46b2-4ef7-8ac4-486bb0e3f289
ms.date: 07/08/2016
ms.openlocfilehash: c5e5e0a0a3f8bd5feedc00d5bbfb76a1453ccc84
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44774520"
---
# <a name="add-maps-for-xml-transformation-in-azure-logic-apps-with-enterprise-integration-pack"></a><span data-ttu-id="7e41f-103">Add maps for XML transformation in Azure Logic Apps with Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="7e41f-103">Add maps for XML transformation in Azure Logic Apps with Enterprise Integration Pack</span></span>

<span data-ttu-id="7e41f-104">Enterprise integration uses maps to transform XML data between formats.</span><span class="sxs-lookup"><span data-stu-id="7e41f-104">Enterprise integration uses maps to transform XML data between formats.</span></span> <span data-ttu-id="7e41f-105">A map is an XML document that defines the data in a document that should be transformed into another format.</span><span class="sxs-lookup"><span data-stu-id="7e41f-105">A map is an XML document that defines the data in a document that should be transformed into another format.</span></span> 

## <a name="why-use-maps"></a><span data-ttu-id="7e41f-106">Why use maps?</span><span class="sxs-lookup"><span data-stu-id="7e41f-106">Why use maps?</span></span>

<span data-ttu-id="7e41f-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses the YYYMMDD format for dates.</span><span class="sxs-lookup"><span data-stu-id="7e41f-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses the YYYMMDD format for dates.</span></span> <span data-ttu-id="7e41f-108">However, in your organization, you store dates in the MMDDYYY format.</span><span class="sxs-lookup"><span data-stu-id="7e41f-108">However, in your organization, you store dates in the MMDDYYY format.</span></span> <span data-ttu-id="7e41f-109">You can use a map to *transform* the YYYMMDD date format into the MMDDYYY before storing the order or invoice details in your customer activity database.</span><span class="sxs-lookup"><span data-stu-id="7e41f-109">You can use a map to *transform* the YYYMMDD date format into the MMDDYYY before storing the order or invoice details in your customer activity database.</span></span>


## <a name="how-do-i-create-a-map"></a><span data-ttu-id="7e41f-110">How do I create a map?</span><span class="sxs-lookup"><span data-stu-id="7e41f-110">How do I create a map?</span></span>

<span data-ttu-id="7e41f-111">You can create BizTalk Integration projects with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack") for Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="7e41f-111">You can create BizTalk Integration projects with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack") for Visual Studio 2015.</span></span> <span data-ttu-id="7e41f-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span><span class="sxs-lookup"><span data-stu-id="7e41f-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span></span> <span data-ttu-id="7e41f-113">After you build this project, you will have an XSLT document.</span><span class="sxs-lookup"><span data-stu-id="7e41f-113">After you build this project, you will have an XSLT document.</span></span>

<span data-ttu-id="7e41f-114">If the map has a reference to an external assembly, then both must be uploaded to the integration account.</span><span class="sxs-lookup"><span data-stu-id="7e41f-114">If the map has a reference to an external assembly, then both must be uploaded to the integration account.</span></span> <span data-ttu-id="7e41f-115">They should be uploaded in a specific order, first the assembly and then the map that references the assembly.</span><span class="sxs-lookup"><span data-stu-id="7e41f-115">They should be uploaded in a specific order, first the assembly and then the map that references the assembly.</span></span>


## <a name="how-do-i-add-a-map"></a><span data-ttu-id="7e41f-116">How do I add a map?</span><span class="sxs-lookup"><span data-stu-id="7e41f-116">How do I add a map?</span></span>

1. <span data-ttu-id="7e41f-117">In the Azure portal, select **Browse**.</span><span class="sxs-lookup"><span data-stu-id="7e41f-117">In the Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="7e41f-118">In the filter search box, enter **integration**, then select **Integration Accounts** from the results list.</span><span class="sxs-lookup"><span data-stu-id="7e41f-118">In the filter search box, enter **integration**, then select **Integration Accounts** from the results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="7e41f-119">Select the integration account where you want to add the map.</span><span class="sxs-lookup"><span data-stu-id="7e41f-119">Select the integration account where you want to add the map.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="7e41f-120">Select the **Maps** tile.</span><span class="sxs-lookup"><span data-stu-id="7e41f-120">Select the **Maps** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. <span data-ttu-id="7e41f-121">After the Maps page opens, choose **Add**.</span><span class="sxs-lookup"><span data-stu-id="7e41f-121">After the Maps page opens, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. <span data-ttu-id="7e41f-122">Enter a **Name** for your map.</span><span class="sxs-lookup"><span data-stu-id="7e41f-122">Enter a **Name** for your map.</span></span> <span data-ttu-id="7e41f-123">To upload the map file, choose the folder icon on the right side of the **Map** text box.</span><span class="sxs-lookup"><span data-stu-id="7e41f-123">To upload the map file, choose the folder icon on the right side of the **Map** text box.</span></span> <span data-ttu-id="7e41f-124">After the upload process completes, choose **OK**.</span><span class="sxs-lookup"><span data-stu-id="7e41f-124">After the upload process completes, choose **OK**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. <span data-ttu-id="7e41f-125">After Azure adds the map to your integration account, you get an onscreen message that shows whether your map file was added or not.</span><span class="sxs-lookup"><span data-stu-id="7e41f-125">After Azure adds the map to your integration account, you get an onscreen message that shows whether your map file was added or not.</span></span> <span data-ttu-id="7e41f-126">After you get this message, choose the **Maps** tile so you can view the newly added map.</span><span class="sxs-lookup"><span data-stu-id="7e41f-126">After you get this message, choose the **Maps** tile so you can view the newly added map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)


## <a name="how-do-i-add-an-assembly"></a><span data-ttu-id="7e41f-127">How do I add an assembly?</span><span class="sxs-lookup"><span data-stu-id="7e41f-127">How do I add an assembly?</span></span>
<span data-ttu-id="7e41f-128">Open the integration account where you want to upload the assembly.</span><span class="sxs-lookup"><span data-stu-id="7e41f-128">Open the integration account where you want to upload the assembly.</span></span>

1. <span data-ttu-id="7e41f-129">Choose the **Assemblies** tile.</span><span class="sxs-lookup"><span data-stu-id="7e41f-129">Choose the **Assemblies** tile.</span></span>

    ![integrationaccount-assembly-tile](./media/logic-apps-enterprise-integration-maps/assemblytile.png)

2. <span data-ttu-id="7e41f-131">After the Assemblies page opens, choose **Add**.</span><span class="sxs-lookup"><span data-stu-id="7e41f-131">After the Assemblies page opens, choose **Add**.</span></span> <span data-ttu-id="7e41f-132">Enter a **Name** for your assembly.</span><span class="sxs-lookup"><span data-stu-id="7e41f-132">Enter a **Name** for your assembly.</span></span> <span data-ttu-id="7e41f-133">To upload the assembly file, choose the folder icon on the right side of the **Assembly** text box.</span><span class="sxs-lookup"><span data-stu-id="7e41f-133">To upload the assembly file, choose the folder icon on the right side of the **Assembly** text box.</span></span> <span data-ttu-id="7e41f-134">After the upload process completes, choose **OK**.</span><span class="sxs-lookup"><span data-stu-id="7e41f-134">After the upload process completes, choose **OK**.</span></span>

    ![add-assembly](./media/logic-apps-enterprise-integration-maps/assemblyfile.png)


## <a name="how-do-i-edit-a-map"></a><span data-ttu-id="7e41f-136">How do I edit a map?</span><span class="sxs-lookup"><span data-stu-id="7e41f-136">How do I edit a map?</span></span>

<span data-ttu-id="7e41f-137">You must upload a new map file with the changes that you want.</span><span class="sxs-lookup"><span data-stu-id="7e41f-137">You must upload a new map file with the changes that you want.</span></span> <span data-ttu-id="7e41f-138">You can first download the map for editing.</span><span class="sxs-lookup"><span data-stu-id="7e41f-138">You can first download the map for editing.</span></span>

<span data-ttu-id="7e41f-139">To upload a new map that replaces the existing map, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="7e41f-139">To upload a new map that replaces the existing map, follow these steps.</span></span>

1. <span data-ttu-id="7e41f-140">Choose the **Maps** tile.</span><span class="sxs-lookup"><span data-stu-id="7e41f-140">Choose the **Maps** tile.</span></span>

2. <span data-ttu-id="7e41f-141">After the Maps page opens, select the map that you want to edit.</span><span class="sxs-lookup"><span data-stu-id="7e41f-141">After the Maps page opens, select the map that you want to edit.</span></span>

3. <span data-ttu-id="7e41f-142">On the **Maps** page, choose **Update**.</span><span class="sxs-lookup"><span data-stu-id="7e41f-142">On the **Maps** page, choose **Update**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. <span data-ttu-id="7e41f-143">In the file picker, select the map file that you want to upload, then select **Open**.</span><span class="sxs-lookup"><span data-stu-id="7e41f-143">In the file picker, select the map file that you want to upload, then select **Open**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-to-delete-a-map"></a><span data-ttu-id="7e41f-144">How to delete a map?</span><span class="sxs-lookup"><span data-stu-id="7e41f-144">How to delete a map?</span></span>

1. <span data-ttu-id="7e41f-145">Choose the **Maps** tile.</span><span class="sxs-lookup"><span data-stu-id="7e41f-145">Choose the **Maps** tile.</span></span>

2. <span data-ttu-id="7e41f-146">After the Maps page opens, select the map you want to delete.</span><span class="sxs-lookup"><span data-stu-id="7e41f-146">After the Maps page opens, select the map you want to delete.</span></span>

3. <span data-ttu-id="7e41f-147">Choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="7e41f-147">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. <span data-ttu-id="7e41f-148">Confirm that you want to delete the map.</span><span class="sxs-lookup"><span data-stu-id="7e41f-148">Confirm that you want to delete the map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a><span data-ttu-id="7e41f-149">Next Steps</span><span class="sxs-lookup"><span data-stu-id="7e41f-149">Next Steps</span></span>
* [<span data-ttu-id="7e41f-150">Learn more about the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="7e41f-150">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack")  
* [<span data-ttu-id="7e41f-151">Learn more about agreements</span><span class="sxs-lookup"><span data-stu-id="7e41f-151">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Learn about enterprise integration agreements")  
* [<span data-ttu-id="7e41f-152">Learn more about transforms</span><span class="sxs-lookup"><span data-stu-id="7e41f-152">Learn more about transforms</span></span>](logic-apps-enterprise-integration-transform.md "Learn about enterprise integration transforms")  

