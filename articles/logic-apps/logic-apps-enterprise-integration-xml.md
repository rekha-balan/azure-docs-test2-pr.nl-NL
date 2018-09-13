---
title: Working with XML messages in your workflows - Azure Logic Apps | Microsoft Docs
description: Process, validate, transform, and enrich XML messages in logic apps and business-to scenarios using the Enterprise Integration Pack
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: ''
ms.assetid: 47672dc4-1caa-44e5-b8cb-68ec3a76b7dc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: mandia
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9d40c5028fd8b3ab20f7562dce9274664e4e56ac
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548874"
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a><span data-ttu-id="78b3a-103">Validate and transform XML, encode and decode flat files, and enrich messages features in logic apps</span><span class="sxs-lookup"><span data-stu-id="78b3a-103">Validate and transform XML, encode and decode flat files, and enrich messages features in logic apps</span></span>

<span data-ttu-id="78b3a-104">Using logic apps, you have the ability to process XML messages that you send and receive.</span><span class="sxs-lookup"><span data-stu-id="78b3a-104">Using logic apps, you have the ability to process XML messages that you send and receive.</span></span> <span data-ttu-id="78b3a-105">This feature is included with the Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="78b3a-105">This feature is included with the Enterprise Integration Pack.</span></span> <span data-ttu-id="78b3a-106">For those users with a BizTalk Server background, the Enterprise Integration Pack gives you similar abilities to transform and validate messages, work with flat files, and even use XPath to enrich or extract specific properties from a message.</span><span class="sxs-lookup"><span data-stu-id="78b3a-106">For those users with a BizTalk Server background, the Enterprise Integration Pack gives you similar abilities to transform and validate messages, work with flat files, and even use XPath to enrich or extract specific properties from a message.</span></span> 

<span data-ttu-id="78b3a-107">For those users who are new to this space, these features expand how you process messages within your workflow.</span><span class="sxs-lookup"><span data-stu-id="78b3a-107">For those users who are new to this space, these features expand how you process messages within your workflow.</span></span> <span data-ttu-id="78b3a-108">For example, if you are in a business-to-business scenario, and work with specific XML schemas, then you can use the Enterprise Integration Pack to enhance how your company processes these messages.</span><span class="sxs-lookup"><span data-stu-id="78b3a-108">For example, if you are in a business-to-business scenario, and work with specific XML schemas, then you can use the Enterprise Integration Pack to enhance how your company processes these messages.</span></span> 

<span data-ttu-id="78b3a-109">The Enterprise Integration Pack includes:</span><span class="sxs-lookup"><span data-stu-id="78b3a-109">The Enterprise Integration Pack includes:</span></span> 

* <span data-ttu-id="78b3a-110">[XML validation](logic-apps-enterprise-integration-xml-validation.md "Learn about XML message validation") - Validate an incoming or outgoing XML message against a specific schema.</span><span class="sxs-lookup"><span data-stu-id="78b3a-110">[XML validation](logic-apps-enterprise-integration-xml-validation.md "Learn about XML message validation") - Validate an incoming or outgoing XML message against a specific schema.</span></span>
* <span data-ttu-id="78b3a-111">[XML transform](../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about XML message transformations and maps") - Convert or customize an XML message based on your requirements, or the requirements of a partner.</span><span class="sxs-lookup"><span data-stu-id="78b3a-111">[XML transform](../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about XML message transformations and maps") - Convert or customize an XML message based on your requirements, or the requirements of a partner.</span></span>
* <span data-ttu-id="78b3a-112">[Flat file encoding and flat file decoding](logic-apps-enterprise-integration-flatfile.md "Learn about flat file encoding/decoding") - Encode or decode a flat file.</span><span class="sxs-lookup"><span data-stu-id="78b3a-112">[Flat file encoding and flat file decoding](logic-apps-enterprise-integration-flatfile.md "Learn about flat file encoding/decoding") - Encode or decode a flat file.</span></span> <span data-ttu-id="78b3a-113">For example, SAP accepts and sends IDOC files in flat file format.</span><span class="sxs-lookup"><span data-stu-id="78b3a-113">For example, SAP accepts and sends IDOC files in flat file format.</span></span> <span data-ttu-id="78b3a-114">Many integration platforms create XML messages, including Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="78b3a-114">Many integration platforms create XML messages, including Logic Apps.</span></span> <span data-ttu-id="78b3a-115">So, you can create a logic app that uses the flat file encoder to "convert" XML files to flat files.</span><span class="sxs-lookup"><span data-stu-id="78b3a-115">So, you can create a logic app that uses the flat file encoder to "convert" XML files to flat files.</span></span> 
* <span data-ttu-id="78b3a-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - Enrich a message and extract specific properties from the message.</span><span class="sxs-lookup"><span data-stu-id="78b3a-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - Enrich a message and extract specific properties from the message.</span></span> <span data-ttu-id="78b3a-117">You can then use the extracted properties to route the message to a destination, or an intermediary endpoint.</span><span class="sxs-lookup"><span data-stu-id="78b3a-117">You can then use the extracted properties to route the message to a destination, or an intermediary endpoint.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="78b3a-118">Try it out</span><span class="sxs-lookup"><span data-stu-id="78b3a-118">Try it out</span></span>
<span data-ttu-id="78b3a-119">[Deploy a fully operational logic app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub sample) by using the XML features in Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="78b3a-119">[Deploy a fully operational logic app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub sample) by using the XML features in Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="78b3a-120">Learn more</span><span class="sxs-lookup"><span data-stu-id="78b3a-120">Learn more</span></span>
[<span data-ttu-id="78b3a-121">Learn more about the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="78b3a-121">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack")
