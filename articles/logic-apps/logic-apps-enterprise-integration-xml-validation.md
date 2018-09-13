---
title: Validate XML - Azure Logic Apps | Microsoft Docs
description: Validate XML with schemas for Azure Logic Apps and B2B scenarios by using the Enterprise Integration Pack
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: estfan
ms.openlocfilehash: bb3077301a4c1e388dc413711c3a0ccb2fcbfb44
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556511"
---
# <a name="validate-xml-for-enterprise-integration"></a><span data-ttu-id="086e5-103">Validate XML for enterprise integration</span><span class="sxs-lookup"><span data-stu-id="086e5-103">Validate XML for enterprise integration</span></span>

<span data-ttu-id="086e5-104">Often in B2B scenarios, the partners in an agreement must make sure that the messages they exchange are valid before data processing can start.</span><span class="sxs-lookup"><span data-stu-id="086e5-104">Often in B2B scenarios, the partners in an agreement must make sure that the messages they exchange are valid before data processing can start.</span></span> <span data-ttu-id="086e5-105">You can validate documents against a predefined schema by using the use the XML Validation connector in the Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="086e5-105">You can validate documents against a predefined schema by using the use the XML Validation connector in the Enterprise Integration Pack.</span></span>

## <a name="validate-a-document-with-the-xml-validation-connector"></a><span data-ttu-id="086e5-106">Validate a document with the XML Validation connector</span><span class="sxs-lookup"><span data-stu-id="086e5-106">Validate a document with the XML Validation connector</span></span>

1. <span data-ttu-id="086e5-107">Create a logic app, and [link the app to the integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that has the schema you want to use for validating XML data.</span><span class="sxs-lookup"><span data-stu-id="086e5-107">Create a logic app, and [link the app to the integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that has the schema you want to use for validating XML data.</span></span>

2. <span data-ttu-id="086e5-108">Add a **Request - When an HTTP request is received** trigger to your logic app.</span><span class="sxs-lookup"><span data-stu-id="086e5-108">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-xml/xml-1.png)

3. <span data-ttu-id="086e5-109">To add the **XML Validation** action, choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="086e5-109">To add the **XML Validation** action, choose **Add an action**.</span></span>

4. <span data-ttu-id="086e5-110">To filter all the actions to the one that you want, enter *xml* in the search box.</span><span class="sxs-lookup"><span data-stu-id="086e5-110">To filter all the actions to the one that you want, enter *xml* in the search box.</span></span> <span data-ttu-id="086e5-111">Choose **XML Validation**.</span><span class="sxs-lookup"><span data-stu-id="086e5-111">Choose **XML Validation**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-xml/xml-2.png)

5. <span data-ttu-id="086e5-112">To specify the XML content that you want to validate, select **CONTENT**.</span><span class="sxs-lookup"><span data-stu-id="086e5-112">To specify the XML content that you want to validate, select **CONTENT**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. <span data-ttu-id="086e5-113">Select the body tag as the content that you want to validate.</span><span class="sxs-lookup"><span data-stu-id="086e5-113">Select the body tag as the content that you want to validate.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-xml/xml-3.png)

7. <span data-ttu-id="086e5-114">To specify the schema you want to use for validating the previous *content* input, choose **SCHEMA NAME**.</span><span class="sxs-lookup"><span data-stu-id="086e5-114">To specify the schema you want to use for validating the previous *content* input, choose **SCHEMA NAME**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-xml/xml-4.png)

8. <span data-ttu-id="086e5-115">Save your work</span><span class="sxs-lookup"><span data-stu-id="086e5-115">Save your work</span></span>  

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-xml/xml-5.png)

<span data-ttu-id="086e5-116">You are now done with setting up your validation connector.</span><span class="sxs-lookup"><span data-stu-id="086e5-116">You are now done with setting up your validation connector.</span></span> <span data-ttu-id="086e5-117">In a real world application, you might want to store the validated data in a line-of-business (LOB) app like SalesForce.</span><span class="sxs-lookup"><span data-stu-id="086e5-117">In a real world application, you might want to store the validated data in a line-of-business (LOB) app like SalesForce.</span></span> <span data-ttu-id="086e5-118">To send the validated output to Salesforce, add an action.</span><span class="sxs-lookup"><span data-stu-id="086e5-118">To send the validated output to Salesforce, add an action.</span></span>

<span data-ttu-id="086e5-119">To test your validation action, make a request to the HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="086e5-119">To test your validation action, make a request to the HTTP endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="086e5-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="086e5-120">Next steps</span></span>
[<span data-ttu-id="086e5-121">Learn more about the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="086e5-121">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack")   







