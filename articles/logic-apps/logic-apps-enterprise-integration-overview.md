---
title: Enterprise Integration for B2B - Azure Logic Apps | Microsoft Docs
description: Build B2B workflows and support enterprise integration scenarios for logic apps with the Enterprise Integration Pack
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: dd517c4d-1701-4247-b83c-183c4d8d8aae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/08/2016
ms.author: estfan
ms.openlocfilehash: 8c4dc4476c9a83e806ad74371bb6fcf2f93e7ac1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555735"
---
# <a name="overview-b2b-scenarios-and-communication-with-the-enterprise-integration-pack"></a><span data-ttu-id="a9dfb-103">Overview: B2B scenarios and communication with the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="a9dfb-103">Overview: B2B scenarios and communication with the Enterprise Integration Pack</span></span>

<span data-ttu-id="a9dfb-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, the Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, the Enterprise Integration Pack.</span></span> <span data-ttu-id="a9dfb-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span></span> <span data-ttu-id="a9dfb-106">The pack transforms different formats into a format that organizations' systems can interpret and process.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-106">The pack transforms different formats into a format that organizations' systems can interpret and process.</span></span> <span data-ttu-id="a9dfb-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="a9dfb-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span></span> <span data-ttu-id="a9dfb-108">You can also secure messages with both encryption and digital signatures.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-108">You can also secure messages with both encryption and digital signatures.</span></span>

<span data-ttu-id="a9dfb-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, the Enterprise Integration features are easy to use because most concepts are similar.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, the Enterprise Integration features are easy to use because most concepts are similar.</span></span> <span data-ttu-id="a9dfb-110">One major difference is that Enterprise Integration uses integration accounts to simplify the storage and management of artifacts used in B2B communications.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-110">One major difference is that Enterprise Integration uses integration accounts to simplify the storage and management of artifacts used in B2B communications.</span></span> 

<span data-ttu-id="a9dfb-111">Architecturally, the Enterprise Integration Pack is based on "integration accounts".</span><span class="sxs-lookup"><span data-stu-id="a9dfb-111">Architecturally, the Enterprise Integration Pack is based on "integration accounts".</span></span> <span data-ttu-id="a9dfb-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span></span> <span data-ttu-id="a9dfb-113">You can use these artifacts to design, deploy, and maintain your B2B apps and also to build B2B workflows for logic apps.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-113">You can use these artifacts to design, deploy, and maintain your B2B apps and also to build B2B workflows for logic apps.</span></span> <span data-ttu-id="a9dfb-114">But before you can use these artifacts, you must first link your integration account to your logic app.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-114">But before you can use these artifacts, you must first link your integration account to your logic app.</span></span> <span data-ttu-id="a9dfb-115">After that, your logic app can access your integration account's artifacts.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-115">After that, your logic app can access your integration account's artifacts.</span></span>

## <a name="why-should-you-use-enterprise-integration"></a><span data-ttu-id="a9dfb-116">Why should you use enterprise integration?</span><span class="sxs-lookup"><span data-stu-id="a9dfb-116">Why should you use enterprise integration?</span></span>

* <span data-ttu-id="a9dfb-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span></span>
* <span data-ttu-id="a9dfb-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using the Azure Logic Apps engine and all its connectors.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using the Azure Logic Apps engine and all its connectors.</span></span>
* <span data-ttu-id="a9dfb-119">You can create custom code for your logic apps with Azure functions.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-119">You can create custom code for your logic apps with Azure functions.</span></span>

## <a name="how-to-get-started-with-enterprise-integration"></a><span data-ttu-id="a9dfb-120">How to get started with enterprise integration?</span><span class="sxs-lookup"><span data-stu-id="a9dfb-120">How to get started with enterprise integration?</span></span>

<span data-ttu-id="a9dfb-121">You can build and manage B2B apps with the Enterprise Integration Pack through the Logic App Designer in the **Azure portal**.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-121">You can build and manage B2B apps with the Enterprise Integration Pack through the Logic App Designer in the **Azure portal**.</span></span> <span data-ttu-id="a9dfb-122">You can also manage your logic apps with [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell topics").</span><span class="sxs-lookup"><span data-stu-id="a9dfb-122">You can also manage your logic apps with [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell topics").</span></span>

<span data-ttu-id="a9dfb-123">Here are the high-level steps you must take before you can create apps in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="a9dfb-123">Here are the high-level steps you must take before you can create apps in the Azure portal:</span></span>

![overview image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a><span data-ttu-id="a9dfb-125">What are some common scenarios?</span><span class="sxs-lookup"><span data-stu-id="a9dfb-125">What are some common scenarios?</span></span>

<span data-ttu-id="a9dfb-126">Enterprise Integration supports these industry standards:</span><span class="sxs-lookup"><span data-stu-id="a9dfb-126">Enterprise Integration supports these industry standards:</span></span>

* <span data-ttu-id="a9dfb-127">EDI - Electronic Data Interchange</span><span class="sxs-lookup"><span data-stu-id="a9dfb-127">EDI - Electronic Data Interchange</span></span>
* <span data-ttu-id="a9dfb-128">EAI - Enterprise Application Integration</span><span class="sxs-lookup"><span data-stu-id="a9dfb-128">EAI - Enterprise Application Integration</span></span>

## <a name="heres-what-you-need-to-get-started"></a><span data-ttu-id="a9dfb-129">Here's what you need to get started</span><span class="sxs-lookup"><span data-stu-id="a9dfb-129">Here's what you need to get started</span></span>

* <span data-ttu-id="a9dfb-130">An Azure subscription with an integration account</span><span class="sxs-lookup"><span data-stu-id="a9dfb-130">An Azure subscription with an integration account</span></span>
* <span data-ttu-id="a9dfb-131">Visual Studio 2015 to create maps and schemas</span><span class="sxs-lookup"><span data-stu-id="a9dfb-131">Visual Studio 2015 to create maps and schemas</span></span>
* [<span data-ttu-id="a9dfb-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span><span class="sxs-lookup"><span data-stu-id="a9dfb-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span></span>](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a><span data-ttu-id="a9dfb-133">Try it now</span><span class="sxs-lookup"><span data-stu-id="a9dfb-133">Try it now</span></span>

<span data-ttu-id="a9dfb-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses the B2B features for Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses the B2B features for Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="a9dfb-135">Learn more</span><span class="sxs-lookup"><span data-stu-id="a9dfb-135">Learn more</span></span>
* [<span data-ttu-id="a9dfb-136">Agreements</span><span class="sxs-lookup"><span data-stu-id="a9dfb-136">Agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Learn about enterprise integration agreements")
* [<span data-ttu-id="a9dfb-137">Business to Business (B2B) scenarios</span><span class="sxs-lookup"><span data-stu-id="a9dfb-137">Business to Business (B2B) scenarios</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b.md "Learn how to create Logic apps with B2B features ")  
* [<span data-ttu-id="a9dfb-138">Certificates</span><span class="sxs-lookup"><span data-stu-id="a9dfb-138">Certificates</span></span>](logic-apps-enterprise-integration-certificates.md "Learn about enterprise integration certificates")
* [<span data-ttu-id="a9dfb-139">Flat file encoding/decoding</span><span class="sxs-lookup"><span data-stu-id="a9dfb-139">Flat file encoding/decoding</span></span>](logic-apps-enterprise-integration-flatfile.md "Learn how to encode and decode flat file contents")  
* [<span data-ttu-id="a9dfb-140">Integration accounts</span><span class="sxs-lookup"><span data-stu-id="a9dfb-140">Integration accounts</span></span>](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn about integration accounts")
* [<span data-ttu-id="a9dfb-141">Maps</span><span class="sxs-lookup"><span data-stu-id="a9dfb-141">Maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Learn about enterprise integration maps")
* [<span data-ttu-id="a9dfb-142">Partners</span><span class="sxs-lookup"><span data-stu-id="a9dfb-142">Partners</span></span>](logic-apps-enterprise-integration-partners.md "Learn about enterprise integration partners")
* [<span data-ttu-id="a9dfb-143">Schemas</span><span class="sxs-lookup"><span data-stu-id="a9dfb-143">Schemas</span></span>](logic-apps-enterprise-integration-schemas.md "Learn about enterprise integration schemas")
* [<span data-ttu-id="a9dfb-144">XML message validation</span><span class="sxs-lookup"><span data-stu-id="a9dfb-144">XML message validation</span></span>](logic-apps-enterprise-integration-xml.md "Learn how to validate XML messages with Logic apps")
* [<span data-ttu-id="a9dfb-145">XML transform</span><span class="sxs-lookup"><span data-stu-id="a9dfb-145">XML transform</span></span>](logic-apps-enterprise-integration-transform.md "Learn about enterprise integration maps")
* [<span data-ttu-id="a9dfb-146">Enterprise Integration Connectors</span><span class="sxs-lookup"><span data-stu-id="a9dfb-146">Enterprise Integration Connectors</span></span>](../connectors/apis-list.md "Learn about enterprise integration pack connectors")
* [<span data-ttu-id="a9dfb-147">Integration Account Metadata</span><span class="sxs-lookup"><span data-stu-id="a9dfb-147">Integration Account Metadata</span></span>](../logic-apps/logic-apps-enterprise-integration-metadata.md "Learn about integration account metadata")
* [<span data-ttu-id="a9dfb-148">Monitor B2B messages</span><span class="sxs-lookup"><span data-stu-id="a9dfb-148">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md "Learn more about monitoring B2B messages")
* [<span data-ttu-id="a9dfb-149">Tracking B2B messages in OMS portal</span><span class="sxs-lookup"><span data-stu-id="a9dfb-149">Tracking B2B messages in OMS portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "Learn more about tracking B2B messages in OMS portal")


