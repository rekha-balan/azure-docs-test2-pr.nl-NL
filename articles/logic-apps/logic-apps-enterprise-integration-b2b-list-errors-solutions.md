---
title: Errors and solutions for B2B scenarios - Azure Logic Apps | Microsoft Docs
description: Find errors and solutions for B2B scenarios in Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: divyaswarnkar
ms.author: divswa
ms.reviewer: jonfan, estfan, LADocs
ms.topic: article
ms.date: 06/02/2017
ms.openlocfilehash: 11fbec81e88eec6c7daa9136eb5421387b79d71c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857492"
---
# <a name="b2b-errors-and-solutions-for-azure-logic-apps"></a><span data-ttu-id="e5e3d-103">B2B errors and solutions for Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="e5e3d-103">B2B errors and solutions for Azure Logic Apps</span></span>

<span data-ttu-id="e5e3d-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>

## <a name="agreement-resolution"></a><span data-ttu-id="e5e3d-105">Agreement resolution</span><span class="sxs-lookup"><span data-stu-id="e5e3d-105">Agreement resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="e5e3d-106">No agreement found</span><span class="sxs-lookup"><span data-stu-id="e5e3d-106">No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="e5e3d-107">Error description</span><span class="sxs-lookup"><span data-stu-id="e5e3d-107">Error description</span></span> | <span data-ttu-id="e5e3d-108">No agreement found with Agreement Resolution Parameters.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-108">No agreement found with Agreement Resolution Parameters.</span></span> | 
| <span data-ttu-id="e5e3d-109">User action</span><span class="sxs-lookup"><span data-stu-id="e5e3d-109">User action</span></span> | <span data-ttu-id="e5e3d-110">The agreement should be added to the integration account with agreed business identities.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-110">The agreement should be added to the integration account with agreed business identities.</span></span> </br><span data-ttu-id="e5e3d-111">The business identities should match to the input message IDs.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-111">The business identities should match to the input message IDs.</span></span> |  
|   |   |

### <a name="no-agreement-found-with-identities"></a><span data-ttu-id="e5e3d-112">No agreement found with identities</span><span class="sxs-lookup"><span data-stu-id="e5e3d-112">No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="e5e3d-113">Error description</span><span class="sxs-lookup"><span data-stu-id="e5e3d-113">Error description</span></span> | <span data-ttu-id="e5e3d-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span><span class="sxs-lookup"><span data-stu-id="e5e3d-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span> | 
| <span data-ttu-id="e5e3d-115">User action</span><span class="sxs-lookup"><span data-stu-id="e5e3d-115">User action</span></span> | <span data-ttu-id="e5e3d-116">Invalid AS2-From or AS2-To configured for agreement.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-116">Invalid AS2-From or AS2-To configured for agreement.</span></span> </br><span data-ttu-id="e5e3d-117">Correct the AS2 message's "AS2-From" or "AS2-To" headers or the agreement to match the AS2 IDs in the AS2 message headers with agreement configurations.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-117">Correct the AS2 message's "AS2-From" or "AS2-To" headers or the agreement to match the AS2 IDs in the AS2 message headers with agreement configurations.</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="e5e3d-118">AS2</span><span class="sxs-lookup"><span data-stu-id="e5e3d-118">AS2</span></span>

### <a name="missing-as2-message-headers"></a><span data-ttu-id="e5e3d-119">Missing AS2 message headers</span><span class="sxs-lookup"><span data-stu-id="e5e3d-119">Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="e5e3d-120">Error description</span><span class="sxs-lookup"><span data-stu-id="e5e3d-120">Error description</span></span> | <span data-ttu-id="e5e3d-121">Invalid AS2 headers.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-121">Invalid AS2 headers.</span></span> <span data-ttu-id="e5e3d-122">One of the "AS2-To" or "AS2-From" headers is empty.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-122">One of the "AS2-To" or "AS2-From" headers is empty.</span></span> | 
| <span data-ttu-id="e5e3d-123">User action</span><span class="sxs-lookup"><span data-stu-id="e5e3d-123">User action</span></span> | <span data-ttu-id="e5e3d-124">An AS2 message was received that did not contain the AS2-From or AS2-To or both headers.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-124">An AS2 message was received that did not contain the AS2-From or AS2-To or both headers.</span></span> </br> <span data-ttu-id="e5e3d-125">Check AS2 message AS2-From and AS2-To headers and correct them based on agreement configuration.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-125">Check AS2 message AS2-From and AS2-To headers and correct them based on agreement configuration.</span></span> |
|  |  | 

### <a name="missing-as2-message-body-and-headers"></a><span data-ttu-id="e5e3d-126">Missing AS2 message body and headers</span><span class="sxs-lookup"><span data-stu-id="e5e3d-126">Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="e5e3d-127">Error description</span><span class="sxs-lookup"><span data-stu-id="e5e3d-127">Error description</span></span> | <span data-ttu-id="e5e3d-128">The request content is null or empty.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-128">The request content is null or empty.</span></span> | 
| <span data-ttu-id="e5e3d-129">User action</span><span class="sxs-lookup"><span data-stu-id="e5e3d-129">User action</span></span> | <span data-ttu-id="e5e3d-130">An AS2 message was received that did not contain the message body.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-130">An AS2 message was received that did not contain the message body.</span></span> |
|  |  | 

### <a name="as2-message-decryption-failure"></a><span data-ttu-id="e5e3d-131">AS2 message decryption failure</span><span class="sxs-lookup"><span data-stu-id="e5e3d-131">AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="e5e3d-132">Error description</span><span class="sxs-lookup"><span data-stu-id="e5e3d-132">Error description</span></span> |  <span data-ttu-id="e5e3d-133">[processed/Error: decryption-failed]</span><span class="sxs-lookup"><span data-stu-id="e5e3d-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="e5e3d-134">User action</span><span class="sxs-lookup"><span data-stu-id="e5e3d-134">User action</span></span> | <span data-ttu-id="e5e3d-135">Add @base64ToBinary to AS2Message before sending to partner.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-135">Add @base64ToBinary to AS2Message before sending to partner.</span></span> |
|||

<span data-ttu-id="e5e3d-136">For example:</span><span class="sxs-lookup"><span data-stu-id="e5e3d-136">For example:</span></span>

```json
"HTTP": {
   "inputs": {
   "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
   "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
   "method": "POST",
   "uri": "xxxxx.xxx"
},
``` 

### <a name="mdn-decryption-failure"></a><span data-ttu-id="e5e3d-137">MDN decryption failure</span><span class="sxs-lookup"><span data-stu-id="e5e3d-137">MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="e5e3d-138">Error description</span><span class="sxs-lookup"><span data-stu-id="e5e3d-138">Error description</span></span> |  <span data-ttu-id="e5e3d-139">[processed/Error: decryption-failed]</span><span class="sxs-lookup"><span data-stu-id="e5e3d-139">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="e5e3d-140">User action</span><span class="sxs-lookup"><span data-stu-id="e5e3d-140">User action</span></span> | <span data-ttu-id="e5e3d-141">Add @base64ToBinary to MDN before sending to partner.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-141">Add @base64ToBinary to MDN before sending to partner.</span></span> | 
|||

<span data-ttu-id="e5e3d-142">For example:</span><span class="sxs-lookup"><span data-stu-id="e5e3d-142">For example:</span></span>

```json
"Response": {
   "inputs": {
   "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
   "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
   "statusCode": 200
},               
``` 

### <a name="missing-signing-certificate"></a><span data-ttu-id="e5e3d-143">Missing signing certificate</span><span class="sxs-lookup"><span data-stu-id="e5e3d-143">Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="e5e3d-144">Error description</span><span class="sxs-lookup"><span data-stu-id="e5e3d-144">Error description</span></span>| <span data-ttu-id="e5e3d-145">The Signing Certificate has not been configured for AS2 party.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-145">The Signing Certificate has not been configured for AS2 party.</span></span> </br><span data-ttu-id="e5e3d-146">AS2-From: partner1 AS2-To: partner2</span><span class="sxs-lookup"><span data-stu-id="e5e3d-146">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="e5e3d-147">User action</span><span class="sxs-lookup"><span data-stu-id="e5e3d-147">User action</span></span> | <span data-ttu-id="e5e3d-148">Configure AS2 agreement settings with correct certificate for signature.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-148">Configure AS2 agreement settings with correct certificate for signature.</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="e5e3d-149">X12 and EDIFACT</span><span class="sxs-lookup"><span data-stu-id="e5e3d-149">X12 and EDIFACT</span></span>

### <a name="leading-or-trailing-space-found"></a><span data-ttu-id="e5e3d-150">Leading or trailing space found</span><span class="sxs-lookup"><span data-stu-id="e5e3d-150">Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="e5e3d-151">Error description</span><span class="sxs-lookup"><span data-stu-id="e5e3d-151">Error description</span></span> | <span data-ttu-id="e5e3d-152">Error encountered during parsing.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-152">Error encountered during parsing.</span></span> <span data-ttu-id="e5e3d-153">The EDIFACT transaction set with ID '123456' contained in interchange (without group) with ID '987654', with sender ID 'Partner1', receiver ID 'Partner2' is being suspended with following errors:</span><span class="sxs-lookup"><span data-stu-id="e5e3d-153">The EDIFACT transaction set with ID '123456' contained in interchange (without group) with ID '987654', with sender ID 'Partner1', receiver ID 'Partner2' is being suspended with following errors:</span></span> <p><span data-ttu-id="e5e3d-154">"Leading Trailing separator found"</span><span class="sxs-lookup"><span data-stu-id="e5e3d-154">"Leading Trailing separator found"</span></span> |
| <span data-ttu-id="e5e3d-155">User action</span><span class="sxs-lookup"><span data-stu-id="e5e3d-155">User action</span></span> | <span data-ttu-id="e5e3d-156">The agreement settings to be configured to allow leading and trailing space.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-156">The agreement settings to be configured to allow leading and trailing space.</span></span> </br><span data-ttu-id="e5e3d-157">Edit agreement settings to allow leading and trailing space.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-157">Edit agreement settings to allow leading and trailing space.</span></span> |
|   |   |

![allow space](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="duplicate-check-has-enabled-in-the-agreement"></a><span data-ttu-id="e5e3d-159">Duplicate check has enabled in the agreement</span><span class="sxs-lookup"><span data-stu-id="e5e3d-159">Duplicate check has enabled in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="e5e3d-160">Error description</span><span class="sxs-lookup"><span data-stu-id="e5e3d-160">Error description</span></span> | <span data-ttu-id="e5e3d-161">Duplicate Control Number</span><span class="sxs-lookup"><span data-stu-id="e5e3d-161">Duplicate Control Number</span></span> |
| <span data-ttu-id="e5e3d-162">User action</span><span class="sxs-lookup"><span data-stu-id="e5e3d-162">User action</span></span> | <span data-ttu-id="e5e3d-163">This error indicates the received message has duplicate control numbers.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-163">This error indicates the received message has duplicate control numbers.</span></span> </br><span data-ttu-id="e5e3d-164">Correct the control number and resend the message.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-164">Correct the control number and resend the message.</span></span> |
|   |   |

### <a name="missing-schema-in-the-agreement"></a><span data-ttu-id="e5e3d-165">Missing schema in the agreement</span><span class="sxs-lookup"><span data-stu-id="e5e3d-165">Missing schema in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="e5e3d-166">Error description</span><span class="sxs-lookup"><span data-stu-id="e5e3d-166">Error description</span></span> | <span data-ttu-id="e5e3d-167">Error encountered during parsing.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-167">Error encountered during parsing.</span></span> <span data-ttu-id="e5e3d-168">The X12 transaction set with ID '564220001' contained in functional group with ID '56422', in interchange with ID '000056422', with sender ID '12345678', receiver ID '87654321' is being suspended with following errors:</span><span class="sxs-lookup"><span data-stu-id="e5e3d-168">The X12 transaction set with ID '564220001' contained in functional group with ID '56422', in interchange with ID '000056422', with sender ID '12345678', receiver ID '87654321' is being suspended with following errors:</span></span> <p><span data-ttu-id="e5e3d-169">"The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement"</span><span class="sxs-lookup"><span data-stu-id="e5e3d-169">"The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement"</span></span> |
| <span data-ttu-id="e5e3d-170">User action</span><span class="sxs-lookup"><span data-stu-id="e5e3d-170">User action</span></span> | <span data-ttu-id="e5e3d-171">Configure schema in the agreement settings.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-171">Configure schema in the agreement settings.</span></span>  |
|   |   |

### <a name="incorrect-schema-in-the-agreement"></a><span data-ttu-id="e5e3d-172">Incorrect schema in the agreement</span><span class="sxs-lookup"><span data-stu-id="e5e3d-172">Incorrect schema in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="e5e3d-173">Error description</span><span class="sxs-lookup"><span data-stu-id="e5e3d-173">Error description</span></span> | <span data-ttu-id="e5e3d-174">The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-174">The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement.</span></span> |
| <span data-ttu-id="e5e3d-175">User action</span><span class="sxs-lookup"><span data-stu-id="e5e3d-175">User action</span></span> | <span data-ttu-id="e5e3d-176">Configure correct schema in the agreement settings.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-176">Configure correct schema in the agreement settings.</span></span> |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="e5e3d-177">Flat file</span><span class="sxs-lookup"><span data-stu-id="e5e3d-177">Flat file</span></span>

### <a name="input-message-with-no-body"></a><span data-ttu-id="e5e3d-178">Input message with no body</span><span class="sxs-lookup"><span data-stu-id="e5e3d-178">Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="e5e3d-179">Error description</span><span class="sxs-lookup"><span data-stu-id="e5e3d-179">Error description</span></span> | <span data-ttu-id="e5e3d-180">InvalidTemplate.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-180">InvalidTemplate.</span></span> <span data-ttu-id="e5e3d-181">Unable to process template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-181">Unable to process template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="e5e3d-182">Path ''.'.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-182">Path ''.'.</span></span> |
| <span data-ttu-id="e5e3d-183">User action</span><span class="sxs-lookup"><span data-stu-id="e5e3d-183">User action</span></span> | <span data-ttu-id="e5e3d-184">This error indicates the input message does not contain a body.</span><span class="sxs-lookup"><span data-stu-id="e5e3d-184">This error indicates the input message does not contain a body.</span></span> |
|   |   | 

