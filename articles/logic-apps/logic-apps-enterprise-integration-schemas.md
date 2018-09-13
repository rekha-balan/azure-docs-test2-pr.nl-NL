---
title: Schemas for XML validation - Azure Logic Apps | Microsoft Docs
description: Validate XML documents with schemas for Azure Logic Apps and Enterprise Integration Pack
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 56c5846c-5d8c-4ad4-9652-60b07aa8fc3b
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: estfan
ms.openlocfilehash: a5fb2aaccf5599c7a60972ff5f7c4ed459d3c1e7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550814"
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-the-enterprise-integration-pack"></a><span data-ttu-id="942df-103">Validate XML with schemas for Azure Logic Apps and the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="942df-103">Validate XML with schemas for Azure Logic Apps and the Enterprise Integration Pack</span></span>

<span data-ttu-id="942df-104">Schemas confirm that the XML documents you receive are valid and have the expected data in a predefined format.</span><span class="sxs-lookup"><span data-stu-id="942df-104">Schemas confirm that the XML documents you receive are valid and have the expected data in a predefined format.</span></span> <span data-ttu-id="942df-105">Schemas also help validate messages that are exchanged in a B2B scenario.</span><span class="sxs-lookup"><span data-stu-id="942df-105">Schemas also help validate messages that are exchanged in a B2B scenario.</span></span>

## <a name="add-a-schema"></a><span data-ttu-id="942df-106">Add a schema</span><span class="sxs-lookup"><span data-stu-id="942df-106">Add a schema</span></span>

1. <span data-ttu-id="942df-107">In the Azure portal, select **More services**.</span><span class="sxs-lookup"><span data-stu-id="942df-107">In the Azure portal, select **More services**.</span></span>

    ![Azure portal, "More services"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. <span data-ttu-id="942df-109">In the filter search box, enter **integration**, and select **Integration Accounts** from the results list.</span><span class="sxs-lookup"><span data-stu-id="942df-109">In the filter search box, enter **integration**, and select **Integration Accounts** from the results list.</span></span>

    ![Filter search box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. <span data-ttu-id="942df-111">Select the **integration account** where you want to add the schema.</span><span class="sxs-lookup"><span data-stu-id="942df-111">Select the **integration account** where you want to add the schema.</span></span>

    ![List of integration accounts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. <span data-ttu-id="942df-113">Choose the **Schemas** tile.</span><span class="sxs-lookup"><span data-stu-id="942df-113">Choose the **Schemas** tile.</span></span>

    ![Example integration account, "Schemas"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a><span data-ttu-id="942df-115">Add a schema file smaller than 2 MB</span><span class="sxs-lookup"><span data-stu-id="942df-115">Add a schema file smaller than 2 MB</span></span>

1. <span data-ttu-id="942df-116">In the **Schemas** blade that opens (from the preceding steps), choose **Add**.</span><span class="sxs-lookup"><span data-stu-id="942df-116">In the **Schemas** blade that opens (from the preceding steps), choose **Add**.</span></span>

    ![Schemas blade, "Add"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. <span data-ttu-id="942df-118">Enter a name for your schema.</span><span class="sxs-lookup"><span data-stu-id="942df-118">Enter a name for your schema.</span></span> <span data-ttu-id="942df-119">Upload the schema file by selecting the folder icon next to the **Schema** box.</span><span class="sxs-lookup"><span data-stu-id="942df-119">Upload the schema file by selecting the folder icon next to the **Schema** box.</span></span> <span data-ttu-id="942df-120">After the upload process completes, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="942df-120">After the upload process completes, select **OK**.</span></span>

    ![Screenshot of "Add Schema", with "Small file" highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-to-8-mb-maximum"></a><span data-ttu-id="942df-122">Add a schema file larger than 2 MB (up to 8 MB maximum)</span><span class="sxs-lookup"><span data-stu-id="942df-122">Add a schema file larger than 2 MB (up to 8 MB maximum)</span></span>

<span data-ttu-id="942df-123">These steps differ based on the blob container access level: **Public** or **No anonymous access**.</span><span class="sxs-lookup"><span data-stu-id="942df-123">These steps differ based on the blob container access level: **Public** or **No anonymous access**.</span></span>

<span data-ttu-id="942df-124">**To determine this access level**</span><span class="sxs-lookup"><span data-stu-id="942df-124">**To determine this access level**</span></span>

1.  <span data-ttu-id="942df-125">Open **Azure Storage Explorer**.</span><span class="sxs-lookup"><span data-stu-id="942df-125">Open **Azure Storage Explorer**.</span></span> 

2.  <span data-ttu-id="942df-126">Under **Blob Containers**, select the blob container you want.</span><span class="sxs-lookup"><span data-stu-id="942df-126">Under **Blob Containers**, select the blob container you want.</span></span> 

3.  <span data-ttu-id="942df-127">Select **Security**, **Access Level**.</span><span class="sxs-lookup"><span data-stu-id="942df-127">Select **Security**, **Access Level**.</span></span>

<span data-ttu-id="942df-128">If the blob security access level is **Public**, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="942df-128">If the blob security access level is **Public**, follow these steps.</span></span>

![Azure Storage Explorer, with "Blob Containers", "Security", and "Public" highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. <span data-ttu-id="942df-130">Upload the schema to your storage account, and copy the URI.</span><span class="sxs-lookup"><span data-stu-id="942df-130">Upload the schema to your storage account, and copy the URI.</span></span>

    ![Storage account, with URI highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. <span data-ttu-id="942df-132">In **Add Schema**, select **Large file**, and provide the URI in the **Content URI** text box.</span><span class="sxs-lookup"><span data-stu-id="942df-132">In **Add Schema**, select **Large file**, and provide the URI in the **Content URI** text box.</span></span>

    ![Schemas, with "Add" button and "Large file" highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

<span data-ttu-id="942df-134">If the blob security access level is **No anonymous access**, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="942df-134">If the blob security access level is **No anonymous access**, follow these steps.</span></span>

![Azure Storage Explorer, with "Blob Containers", "Security", and "No anonymous access" highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. <span data-ttu-id="942df-136">Upload the schema to your storage account.</span><span class="sxs-lookup"><span data-stu-id="942df-136">Upload the schema to your storage account.</span></span>

    ![Storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. <span data-ttu-id="942df-138">Generate a shared access signature for the schema.</span><span class="sxs-lookup"><span data-stu-id="942df-138">Generate a shared access signature for the schema.</span></span>

    ![Storage account, with shared access signatures tab highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. <span data-ttu-id="942df-140">In **Add Schema**, select **Large file**, and provide the shared access signature URI in the **Content URI** text box.</span><span class="sxs-lookup"><span data-stu-id="942df-140">In **Add Schema**, select **Large file**, and provide the shared access signature URI in the **Content URI** text box.</span></span>

    ![Schemas, with "Add" button and "Large file" highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. <span data-ttu-id="942df-142">In the **Schemas** blade of your integration account, your newly added schema should appear.</span><span class="sxs-lookup"><span data-stu-id="942df-142">In the **Schemas** blade of your integration account, your newly added schema should appear.</span></span>

    ![Your integration account, with "Schemas" and the new schema highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a><span data-ttu-id="942df-144">Edit schemas</span><span class="sxs-lookup"><span data-stu-id="942df-144">Edit schemas</span></span>

1. <span data-ttu-id="942df-145">Choose the **Schemas** tile.</span><span class="sxs-lookup"><span data-stu-id="942df-145">Choose the **Schemas** tile.</span></span>

2. <span data-ttu-id="942df-146">After the **Schemas** blade opens, select the schema that you want to edit.</span><span class="sxs-lookup"><span data-stu-id="942df-146">After the **Schemas** blade opens, select the schema that you want to edit.</span></span>

3. <span data-ttu-id="942df-147">On the **Schemas** blade, choose **Edit**.</span><span class="sxs-lookup"><span data-stu-id="942df-147">On the **Schemas** blade, choose **Edit**.</span></span>

    ![Schemas blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. <span data-ttu-id="942df-149">Select the schema file that you want to edit, then select **Open**.</span><span class="sxs-lookup"><span data-stu-id="942df-149">Select the schema file that you want to edit, then select **Open**.</span></span>

    ![Open schema file to edit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-schemas/edit-31.png)

<span data-ttu-id="942df-151">Azure shows a message that the schema uploaded successfully.</span><span class="sxs-lookup"><span data-stu-id="942df-151">Azure shows a message that the schema uploaded successfully.</span></span>

## <a name="delete-schemas"></a><span data-ttu-id="942df-152">Delete schemas</span><span class="sxs-lookup"><span data-stu-id="942df-152">Delete schemas</span></span>

1. <span data-ttu-id="942df-153">Choose the **Schemas** tile.</span><span class="sxs-lookup"><span data-stu-id="942df-153">Choose the **Schemas** tile.</span></span>

2. <span data-ttu-id="942df-154">After the **Schemas** blade opens, select the schema you want to delete.</span><span class="sxs-lookup"><span data-stu-id="942df-154">After the **Schemas** blade opens, select the schema you want to delete.</span></span>

3. <span data-ttu-id="942df-155">On the **Schemas** blade, choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="942df-155">On the **Schemas** blade, choose **Delete**.</span></span>

    ![Schemas blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. <span data-ttu-id="942df-157">To confirm that you want to delete the selected schema, choose **Yes**.</span><span class="sxs-lookup"><span data-stu-id="942df-157">To confirm that you want to delete the selected schema, choose **Yes**.</span></span>

    !["Delete schema" confirmation message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-schemas/delete-21.png)

    <span data-ttu-id="942df-159">In the **Schemas** blade, the schema list refreshes  and no longer includes the schema that you deleted.</span><span class="sxs-lookup"><span data-stu-id="942df-159">In the **Schemas** blade, the schema list refreshes  and no longer includes the schema that you deleted.</span></span>

    ![Your integration Account, with "Schemas" highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a><span data-ttu-id="942df-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="942df-161">Next steps</span></span>
* <span data-ttu-id="942df-162">[Learn more about the Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack").</span><span class="sxs-lookup"><span data-stu-id="942df-162">[Learn more about the Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack").</span></span>  




















