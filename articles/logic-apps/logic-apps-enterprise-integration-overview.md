---
title: B2B enterprise integration overview - Azure Logic Apps | Microsoft Docs
description: Build automated B2B workflows for enterprise integration solutions with Azure Logic Apps and Enterprise Integration Pack
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: divyaswarnkar
ms.author: divswa
ms.reviewer: jonfan, estfan, LADocs
ms.topic: article
ms.assetid: dd517c4d-1701-4247-b83c-183c4d8d8aae
ms.date: 09/08/2016
ms.openlocfilehash: b2e2c81914e8c0440b358d59c7f0248db46b6c50
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44826605"
---
# <a name="overview-b2b-enterprise-integration-scenarios-in-azure-logic-apps-with-enterprise-integration-pack"></a><span data-ttu-id="237f3-103">Overview: B2B enterprise integration scenarios in Azure Logic Apps with Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="237f3-103">Overview: B2B enterprise integration scenarios in Azure Logic Apps with Enterprise Integration Pack</span></span>

<span data-ttu-id="237f3-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, the Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="237f3-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, the Enterprise Integration Pack.</span></span> <span data-ttu-id="237f3-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span><span class="sxs-lookup"><span data-stu-id="237f3-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span></span> <span data-ttu-id="237f3-106">The pack transforms different formats into a format that organizations' systems can interpret and process.</span><span class="sxs-lookup"><span data-stu-id="237f3-106">The pack transforms different formats into a format that organizations' systems can interpret and process.</span></span> <span data-ttu-id="237f3-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="237f3-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span></span> <span data-ttu-id="237f3-108">You can also secure messages with both encryption and digital signatures.</span><span class="sxs-lookup"><span data-stu-id="237f3-108">You can also secure messages with both encryption and digital signatures.</span></span>

<span data-ttu-id="237f3-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, the Enterprise Integration features are easy to use because most concepts are similar.</span><span class="sxs-lookup"><span data-stu-id="237f3-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, the Enterprise Integration features are easy to use because most concepts are similar.</span></span> <span data-ttu-id="237f3-110">One major difference is that Enterprise Integration uses integration accounts to simplify the storage and management of artifacts used in B2B communications.</span><span class="sxs-lookup"><span data-stu-id="237f3-110">One major difference is that Enterprise Integration uses integration accounts to simplify the storage and management of artifacts used in B2B communications.</span></span> 

<span data-ttu-id="237f3-111">Architecturally, the Enterprise Integration Pack is based on "integration accounts".</span><span class="sxs-lookup"><span data-stu-id="237f3-111">Architecturally, the Enterprise Integration Pack is based on "integration accounts".</span></span> <span data-ttu-id="237f3-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span><span class="sxs-lookup"><span data-stu-id="237f3-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span></span> <span data-ttu-id="237f3-113">You can use these artifacts to design, deploy, and maintain your B2B apps and also to build B2B workflows for logic apps.</span><span class="sxs-lookup"><span data-stu-id="237f3-113">You can use these artifacts to design, deploy, and maintain your B2B apps and also to build B2B workflows for logic apps.</span></span> <span data-ttu-id="237f3-114">But before you can use these artifacts, you must first link your integration account to your logic app.</span><span class="sxs-lookup"><span data-stu-id="237f3-114">But before you can use these artifacts, you must first link your integration account to your logic app.</span></span> <span data-ttu-id="237f3-115">After that, your logic app can access your integration account's artifacts.</span><span class="sxs-lookup"><span data-stu-id="237f3-115">After that, your logic app can access your integration account's artifacts.</span></span>

## <a name="why-should-you-use-enterprise-integration"></a><span data-ttu-id="237f3-116">Why should you use enterprise integration?</span><span class="sxs-lookup"><span data-stu-id="237f3-116">Why should you use enterprise integration?</span></span>

* <span data-ttu-id="237f3-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span><span class="sxs-lookup"><span data-stu-id="237f3-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span></span>
* <span data-ttu-id="237f3-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using the Azure Logic Apps engine and all its connectors.</span><span class="sxs-lookup"><span data-stu-id="237f3-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using the Azure Logic Apps engine and all its connectors.</span></span>
* <span data-ttu-id="237f3-119">You can create custom code for your logic apps with Azure functions.</span><span class="sxs-lookup"><span data-stu-id="237f3-119">You can create custom code for your logic apps with Azure functions.</span></span>

## <a name="how-to-get-started-with-enterprise-integration"></a><span data-ttu-id="237f3-120">How to get started with enterprise integration?</span><span class="sxs-lookup"><span data-stu-id="237f3-120">How to get started with enterprise integration?</span></span>

<span data-ttu-id="237f3-121">You can build and manage B2B apps with the Enterprise Integration Pack through the Logic App Designer in the **Azure portal**.</span><span class="sxs-lookup"><span data-stu-id="237f3-121">You can build and manage B2B apps with the Enterprise Integration Pack through the Logic App Designer in the **Azure portal**.</span></span> <span data-ttu-id="237f3-122">You can also manage your logic apps with [PowerShell](https://docs.microsoft.com/powershell/module/azurerm.logicapp "Logic apps PowerShell").</span><span class="sxs-lookup"><span data-stu-id="237f3-122">You can also manage your logic apps with [PowerShell](https://docs.microsoft.com/powershell/module/azurerm.logicapp "Logic apps PowerShell").</span></span>

<span data-ttu-id="237f3-123">Here are the high-level steps you must take before you can create apps in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="237f3-123">Here are the high-level steps you must take before you can create apps in the Azure portal:</span></span>

![overview image](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a><span data-ttu-id="237f3-125">What are some common scenarios?</span><span class="sxs-lookup"><span data-stu-id="237f3-125">What are some common scenarios?</span></span>

<span data-ttu-id="237f3-126">Enterprise Integration supports these industry standards:</span><span class="sxs-lookup"><span data-stu-id="237f3-126">Enterprise Integration supports these industry standards:</span></span>

* <span data-ttu-id="237f3-127">EDI - Electronic Data Interchange</span><span class="sxs-lookup"><span data-stu-id="237f3-127">EDI - Electronic Data Interchange</span></span>
* <span data-ttu-id="237f3-128">EAI - Enterprise Application Integration</span><span class="sxs-lookup"><span data-stu-id="237f3-128">EAI - Enterprise Application Integration</span></span>

## <a name="heres-what-you-need-to-get-started"></a><span data-ttu-id="237f3-129">Here's what you need to get started</span><span class="sxs-lookup"><span data-stu-id="237f3-129">Here's what you need to get started</span></span>

* <span data-ttu-id="237f3-130">An Azure subscription with an integration account</span><span class="sxs-lookup"><span data-stu-id="237f3-130">An Azure subscription with an integration account</span></span>
* <span data-ttu-id="237f3-131">Visual Studio 2015 to create maps and schemas</span><span class="sxs-lookup"><span data-stu-id="237f3-131">Visual Studio 2015 to create maps and schemas</span></span>
* [<span data-ttu-id="237f3-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span><span class="sxs-lookup"><span data-stu-id="237f3-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span></span>](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a><span data-ttu-id="237f3-133">Try it now</span><span class="sxs-lookup"><span data-stu-id="237f3-133">Try it now</span></span>

<span data-ttu-id="237f3-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses the B2B features for Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="237f3-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses the B2B features for Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="237f3-135">Learn more</span><span class="sxs-lookup"><span data-stu-id="237f3-135">Learn more</span></span>
* [<span data-ttu-id="237f3-136">Agreements</span><span class="sxs-lookup"><span data-stu-id="237f3-136">Agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Learn about enterprise integration agreements")
* [<span data-ttu-id="237f3-137">Business to Business (B2B) scenarios</span><span class="sxs-lookup"><span data-stu-id="237f3-137">Business to Business (B2B) scenarios</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b.md "Learn how to create Logic apps with B2B features ")  
* [<span data-ttu-id="237f3-138">Certificates</span><span class="sxs-lookup"><span data-stu-id="237f3-138">Certificates</span></span>](logic-apps-enterprise-integration-certificates.md "Learn about enterprise integration certificates")
* [<span data-ttu-id="237f3-139">Flat file encoding/decoding</span><span class="sxs-lookup"><span data-stu-id="237f3-139">Flat file encoding/decoding</span></span>](logic-apps-enterprise-integration-flatfile.md "Learn how to encode and decode flat file contents")  
* [<span data-ttu-id="237f3-140">Integration accounts</span><span class="sxs-lookup"><span data-stu-id="237f3-140">Integration accounts</span></span>](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn about integration accounts")
* [<span data-ttu-id="237f3-141">Maps</span><span class="sxs-lookup"><span data-stu-id="237f3-141">Maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Learn about enterprise integration maps")
* [<span data-ttu-id="237f3-142">Partners</span><span class="sxs-lookup"><span data-stu-id="237f3-142">Partners</span></span>](logic-apps-enterprise-integration-partners.md "Learn about enterprise integration partners")
* [<span data-ttu-id="237f3-143">Schemas</span><span class="sxs-lookup"><span data-stu-id="237f3-143">Schemas</span></span>](logic-apps-enterprise-integration-schemas.md "Learn about enterprise integration schemas")
* [<span data-ttu-id="237f3-144">XML message validation</span><span class="sxs-lookup"><span data-stu-id="237f3-144">XML message validation</span></span>](logic-apps-enterprise-integration-xml.md "Learn how to validate XML messages with Logic apps")
* [<span data-ttu-id="237f3-145">XML transform</span><span class="sxs-lookup"><span data-stu-id="237f3-145">XML transform</span></span>](logic-apps-enterprise-integration-transform.md "Learn about enterprise integration maps")
* [<span data-ttu-id="237f3-146">Enterprise Integration Connectors</span><span class="sxs-lookup"><span data-stu-id="237f3-146">Enterprise Integration Connectors</span></span>](../connectors/apis-list.md "Learn about enterprise integration pack connectors")
* [<span data-ttu-id="237f3-147">Integration Account Metadata</span><span class="sxs-lookup"><span data-stu-id="237f3-147">Integration Account Metadata</span></span>](../logic-apps/logic-apps-enterprise-integration-metadata.md "Learn about integration account metadata")
* [<span data-ttu-id="237f3-148">Monitor B2B messages</span><span class="sxs-lookup"><span data-stu-id="237f3-148">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md "Learn more about monitoring B2B messages")
* [<span data-ttu-id="237f3-149">Tracking B2B messages in OMS portal</span><span class="sxs-lookup"><span data-stu-id="237f3-149">Tracking B2B messages in OMS portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "Learn more about tracking B2B messages in OMS portal")

