---
title: Widevine license template overview | Microsoft Docs
description: This topic gives an overview of a Widevine license template that is used to configure Widevine licenses.
author: juliako
manager: cfowler
editor: ''
services: media-services
documentationcenter: ''
ms.assetid: 0e6f1f05-7ed6-4ed6-82a0-0cc2182b075a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: eefe82eb022584029b7afb0f2c3524d400c700bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864319"
---
# <a name="widevine-license-template-overview"></a><span data-ttu-id="1e7df-103">Widevine license template overview</span><span class="sxs-lookup"><span data-stu-id="1e7df-103">Widevine license template overview</span></span>
<span data-ttu-id="1e7df-104">You can use Azure Media Services to configure and request Google Widevine licenses.</span><span class="sxs-lookup"><span data-stu-id="1e7df-104">You can use Azure Media Services to configure and request Google Widevine licenses.</span></span> <span data-ttu-id="1e7df-105">When the player tries to play your Widevine-protected content, a request is sent to the license delivery service to obtain a license.</span><span class="sxs-lookup"><span data-stu-id="1e7df-105">When the player tries to play your Widevine-protected content, a request is sent to the license delivery service to obtain a license.</span></span> <span data-ttu-id="1e7df-106">If the license service approves the request, the service issues the license.</span><span class="sxs-lookup"><span data-stu-id="1e7df-106">If the license service approves the request, the service issues the license.</span></span> <span data-ttu-id="1e7df-107">It's sent to the client and is used to decrypt and play the specified content.</span><span class="sxs-lookup"><span data-stu-id="1e7df-107">It's sent to the client and is used to decrypt and play the specified content.</span></span>

<span data-ttu-id="1e7df-108">A Widevine license request is formatted as a JSON message.</span><span class="sxs-lookup"><span data-stu-id="1e7df-108">A Widevine license request is formatted as a JSON message.</span></span>  

>[!NOTE]
> <span data-ttu-id="1e7df-109">You can create an empty message with no values, just "{}."</span><span class="sxs-lookup"><span data-stu-id="1e7df-109">You can create an empty message with no values, just "{}."</span></span> <span data-ttu-id="1e7df-110">Then a license template is created with defaults.</span><span class="sxs-lookup"><span data-stu-id="1e7df-110">Then a license template is created with defaults.</span></span> <span data-ttu-id="1e7df-111">The default works for most cases.</span><span class="sxs-lookup"><span data-stu-id="1e7df-111">The default works for most cases.</span></span> <span data-ttu-id="1e7df-112">Microsoft-based license-delivery scenarios should always use the defaults.</span><span class="sxs-lookup"><span data-stu-id="1e7df-112">Microsoft-based license-delivery scenarios should always use the defaults.</span></span> <span data-ttu-id="1e7df-113">If you need to set the "provider" and "content_id" values, a provider must match Widevine credentials.</span><span class="sxs-lookup"><span data-stu-id="1e7df-113">If you need to set the "provider" and "content_id" values, a provider must match Widevine credentials.</span></span>

    {  
       “payload”:“<license challenge>”,
       “content_id”: “<content id>” 
       “provider”: ”<provider>”
       “allowed_track_types”:“<types>”,
       “content_key_specs”:[  
          {  
             “track_type”:“<track type 1>”
          },
          {  
             “track_type”:“<track type 2>”
          },
          …
       ],
       “policy_overrides”:{  
          “can_play”:<can play>,
          “can persist”:<can persist>,
          “can_renew”:<can renew>,
          “rental_duration_seconds”:<rental duration>,
          “playback_duration_seconds”:<playback duration>,
          “license_duration_seconds”:<license duration>,
          “renewal_recovery_duration_seconds”:<renewal recovery duration>,
          “renewal_server_url”:”<renewal server url>”,
          “renewal_delay_seconds”:<renewal delay>,
          “renewal_retry_interval_seconds”:<renewal retry interval>,
          “renew_with_usage”:<renew with usage>
       }
    }

## <a name="json-message"></a><span data-ttu-id="1e7df-114">JSON message</span><span class="sxs-lookup"><span data-stu-id="1e7df-114">JSON message</span></span>
| <span data-ttu-id="1e7df-115">Name</span><span class="sxs-lookup"><span data-stu-id="1e7df-115">Name</span></span> | <span data-ttu-id="1e7df-116">Value</span><span class="sxs-lookup"><span data-stu-id="1e7df-116">Value</span></span> | <span data-ttu-id="1e7df-117">Description</span><span class="sxs-lookup"><span data-stu-id="1e7df-117">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1e7df-118">payload</span><span class="sxs-lookup"><span data-stu-id="1e7df-118">payload</span></span> |<span data-ttu-id="1e7df-119">Base64-encoded string</span><span class="sxs-lookup"><span data-stu-id="1e7df-119">Base64-encoded string</span></span> |<span data-ttu-id="1e7df-120">The license request sent by a client.</span><span class="sxs-lookup"><span data-stu-id="1e7df-120">The license request sent by a client.</span></span> |
| <span data-ttu-id="1e7df-121">content_id</span><span class="sxs-lookup"><span data-stu-id="1e7df-121">content_id</span></span> |<span data-ttu-id="1e7df-122">Base64-encoded string</span><span class="sxs-lookup"><span data-stu-id="1e7df-122">Base64-encoded string</span></span> |<span data-ttu-id="1e7df-123">Identifier used to derive the key ID and content key for each content_key_specs.track_type.</span><span class="sxs-lookup"><span data-stu-id="1e7df-123">Identifier used to derive the key ID and content key for each content_key_specs.track_type.</span></span> |
| <span data-ttu-id="1e7df-124">provider</span><span class="sxs-lookup"><span data-stu-id="1e7df-124">provider</span></span> |<span data-ttu-id="1e7df-125">string</span><span class="sxs-lookup"><span data-stu-id="1e7df-125">string</span></span> |<span data-ttu-id="1e7df-126">Used to look up content keys and policies.</span><span class="sxs-lookup"><span data-stu-id="1e7df-126">Used to look up content keys and policies.</span></span> <span data-ttu-id="1e7df-127">If Microsoft key delivery is used for Widevine license delivery, this parameter is ignored.</span><span class="sxs-lookup"><span data-stu-id="1e7df-127">If Microsoft key delivery is used for Widevine license delivery, this parameter is ignored.</span></span> |
| <span data-ttu-id="1e7df-128">policy_name</span><span class="sxs-lookup"><span data-stu-id="1e7df-128">policy_name</span></span> |<span data-ttu-id="1e7df-129">string</span><span class="sxs-lookup"><span data-stu-id="1e7df-129">string</span></span> |<span data-ttu-id="1e7df-130">Name of a previously registered policy.</span><span class="sxs-lookup"><span data-stu-id="1e7df-130">Name of a previously registered policy.</span></span> <span data-ttu-id="1e7df-131">Optional.</span><span class="sxs-lookup"><span data-stu-id="1e7df-131">Optional.</span></span> |
| <span data-ttu-id="1e7df-132">allowed_track_types</span><span class="sxs-lookup"><span data-stu-id="1e7df-132">allowed_track_types</span></span> |<span data-ttu-id="1e7df-133">enum</span><span class="sxs-lookup"><span data-stu-id="1e7df-133">enum</span></span> |<span data-ttu-id="1e7df-134">SD_ONLY or SD_HD.</span><span class="sxs-lookup"><span data-stu-id="1e7df-134">SD_ONLY or SD_HD.</span></span> <span data-ttu-id="1e7df-135">Controls which content keys are included in a license.</span><span class="sxs-lookup"><span data-stu-id="1e7df-135">Controls which content keys are included in a license.</span></span> |
| <span data-ttu-id="1e7df-136">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="1e7df-136">content_key_specs</span></span> |<span data-ttu-id="1e7df-137">Array of JSON structures, see the section "Content key specs."</span><span class="sxs-lookup"><span data-stu-id="1e7df-137">Array of JSON structures, see the section "Content key specs."</span></span>  |<span data-ttu-id="1e7df-138">A finer-grained control on which content keys to return.</span><span class="sxs-lookup"><span data-stu-id="1e7df-138">A finer-grained control on which content keys to return.</span></span> <span data-ttu-id="1e7df-139">For more information, see the section "Content key specs."</span><span class="sxs-lookup"><span data-stu-id="1e7df-139">For more information, see the section "Content key specs."</span></span> <span data-ttu-id="1e7df-140">Only one of the allowed_track_types and content_key_specs values can be specified.</span><span class="sxs-lookup"><span data-stu-id="1e7df-140">Only one of the allowed_track_types and content_key_specs values can be specified.</span></span> |
| <span data-ttu-id="1e7df-141">use_policy_overrides_exclusively</span><span class="sxs-lookup"><span data-stu-id="1e7df-141">use_policy_overrides_exclusively</span></span> |<span data-ttu-id="1e7df-142">Boolean, true or false</span><span class="sxs-lookup"><span data-stu-id="1e7df-142">Boolean, true or false</span></span> |<span data-ttu-id="1e7df-143">Use policy attributes specified by policy_overrides, and omit all previously stored policy.</span><span class="sxs-lookup"><span data-stu-id="1e7df-143">Use policy attributes specified by policy_overrides, and omit all previously stored policy.</span></span> |
| <span data-ttu-id="1e7df-144">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="1e7df-144">policy_overrides</span></span> |<span data-ttu-id="1e7df-145">JSON structure, see the section "Policy overrides."</span><span class="sxs-lookup"><span data-stu-id="1e7df-145">JSON structure, see the section "Policy overrides."</span></span> |<span data-ttu-id="1e7df-146">Policy settings for this license.</span><span class="sxs-lookup"><span data-stu-id="1e7df-146">Policy settings for this license.</span></span>  <span data-ttu-id="1e7df-147">In the event this asset has a predefined policy, these specified values are used.</span><span class="sxs-lookup"><span data-stu-id="1e7df-147">In the event this asset has a predefined policy, these specified values are used.</span></span> |
| <span data-ttu-id="1e7df-148">session_init</span><span class="sxs-lookup"><span data-stu-id="1e7df-148">session_init</span></span> |<span data-ttu-id="1e7df-149">JSON structure, see the section "Session initialization."</span><span class="sxs-lookup"><span data-stu-id="1e7df-149">JSON structure, see the section "Session initialization."</span></span> |<span data-ttu-id="1e7df-150">Optional data is passed to the license.</span><span class="sxs-lookup"><span data-stu-id="1e7df-150">Optional data is passed to the license.</span></span> |
| <span data-ttu-id="1e7df-151">parse_only</span><span class="sxs-lookup"><span data-stu-id="1e7df-151">parse_only</span></span> |<span data-ttu-id="1e7df-152">Boolean, true or false</span><span class="sxs-lookup"><span data-stu-id="1e7df-152">Boolean, true or false</span></span> |<span data-ttu-id="1e7df-153">The license request is parsed, but no license is issued.</span><span class="sxs-lookup"><span data-stu-id="1e7df-153">The license request is parsed, but no license is issued.</span></span> <span data-ttu-id="1e7df-154">However, values from the license request are returned in the response.</span><span class="sxs-lookup"><span data-stu-id="1e7df-154">However, values from the license request are returned in the response.</span></span> |

## <a name="content-key-specs"></a><span data-ttu-id="1e7df-155">Content key specs</span><span class="sxs-lookup"><span data-stu-id="1e7df-155">Content key specs</span></span>
<span data-ttu-id="1e7df-156">If a preexisting policy exists, there is no need to specify any of the values in the content key spec. The preexisting policy associated with this content is used to determine the output protection, such as High-bandwidth Digital Content Protection (HDCP) and the Copy General Management System (CGMS).</span><span class="sxs-lookup"><span data-stu-id="1e7df-156">If a preexisting policy exists, there is no need to specify any of the values in the content key spec. The preexisting policy associated with this content is used to determine the output protection, such as High-bandwidth Digital Content Protection (HDCP) and the Copy General Management System (CGMS).</span></span> <span data-ttu-id="1e7df-157">If a preexisting policy isn't registered with the Widevine license server, the content provider can inject the values into the license request.</span><span class="sxs-lookup"><span data-stu-id="1e7df-157">If a preexisting policy isn't registered with the Widevine license server, the content provider can inject the values into the license request.</span></span>   

<span data-ttu-id="1e7df-158">Each content_key_specs value must be specified for all tracks, regardless of the use_policy_overrides_exclusively option.</span><span class="sxs-lookup"><span data-stu-id="1e7df-158">Each content_key_specs value must be specified for all tracks, regardless of the use_policy_overrides_exclusively option.</span></span> 

| <span data-ttu-id="1e7df-159">Name</span><span class="sxs-lookup"><span data-stu-id="1e7df-159">Name</span></span> | <span data-ttu-id="1e7df-160">Value</span><span class="sxs-lookup"><span data-stu-id="1e7df-160">Value</span></span> | <span data-ttu-id="1e7df-161">Description</span><span class="sxs-lookup"><span data-stu-id="1e7df-161">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1e7df-162">content_key_specs.</span><span class="sxs-lookup"><span data-stu-id="1e7df-162">content_key_specs.</span></span> <span data-ttu-id="1e7df-163">track_type</span><span class="sxs-lookup"><span data-stu-id="1e7df-163">track_type</span></span> |<span data-ttu-id="1e7df-164">string</span><span class="sxs-lookup"><span data-stu-id="1e7df-164">string</span></span> |<span data-ttu-id="1e7df-165">A track type name.</span><span class="sxs-lookup"><span data-stu-id="1e7df-165">A track type name.</span></span> <span data-ttu-id="1e7df-166">If content_key_specs is specified in the license request, make sure to specify all track types explicitly.</span><span class="sxs-lookup"><span data-stu-id="1e7df-166">If content_key_specs is specified in the license request, make sure to specify all track types explicitly.</span></span> <span data-ttu-id="1e7df-167">Failure to do so results in failure to play back past 10 seconds.</span><span class="sxs-lookup"><span data-stu-id="1e7df-167">Failure to do so results in failure to play back past 10 seconds.</span></span> |
| <span data-ttu-id="1e7df-168">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="1e7df-168">content_key_specs</span></span>  <br/> <span data-ttu-id="1e7df-169">security_level</span><span class="sxs-lookup"><span data-stu-id="1e7df-169">security_level</span></span> |<span data-ttu-id="1e7df-170">uint32</span><span class="sxs-lookup"><span data-stu-id="1e7df-170">uint32</span></span> |<span data-ttu-id="1e7df-171">Defines client robustness requirements for playback.</span><span class="sxs-lookup"><span data-stu-id="1e7df-171">Defines client robustness requirements for playback.</span></span> <br/> <span data-ttu-id="1e7df-172">- Software-based white-box cryptography is required.</span><span class="sxs-lookup"><span data-stu-id="1e7df-172">- Software-based white-box cryptography is required.</span></span> <br/> <span data-ttu-id="1e7df-173">- Software cryptography and an obfuscated decoder are required.</span><span class="sxs-lookup"><span data-stu-id="1e7df-173">- Software cryptography and an obfuscated decoder are required.</span></span> <br/> <span data-ttu-id="1e7df-174">- The key material and cryptography operations must be performed within a hardware-backed trusted execution environment.</span><span class="sxs-lookup"><span data-stu-id="1e7df-174">- The key material and cryptography operations must be performed within a hardware-backed trusted execution environment.</span></span> <br/> <span data-ttu-id="1e7df-175">- The cryptography and decoding of content must be performed within a hardware-backed trusted execution environment.</span><span class="sxs-lookup"><span data-stu-id="1e7df-175">- The cryptography and decoding of content must be performed within a hardware-backed trusted execution environment.</span></span>  <br/> <span data-ttu-id="1e7df-176">- The cryptography, decoding, and all handling of the media (compressed and uncompressed) must be handled within a hardware-backed trusted execution environment.</span><span class="sxs-lookup"><span data-stu-id="1e7df-176">- The cryptography, decoding, and all handling of the media (compressed and uncompressed) must be handled within a hardware-backed trusted execution environment.</span></span> |
| <span data-ttu-id="1e7df-177">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="1e7df-177">content_key_specs</span></span> <br/> <span data-ttu-id="1e7df-178">required_output_protection.hdc</span><span class="sxs-lookup"><span data-stu-id="1e7df-178">required_output_protection.hdc</span></span> |<span data-ttu-id="1e7df-179">string, one of HDCP_NONE, HDCP_V1, HDCP_V2</span><span class="sxs-lookup"><span data-stu-id="1e7df-179">string, one of HDCP_NONE, HDCP_V1, HDCP_V2</span></span> |<span data-ttu-id="1e7df-180">Indicates whether HDCP is required.</span><span class="sxs-lookup"><span data-stu-id="1e7df-180">Indicates whether HDCP is required.</span></span> |
| <span data-ttu-id="1e7df-181">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="1e7df-181">content_key_specs</span></span> <br/><span data-ttu-id="1e7df-182">key</span><span class="sxs-lookup"><span data-stu-id="1e7df-182">key</span></span> |<span data-ttu-id="1e7df-183">Base64-</span><span class="sxs-lookup"><span data-stu-id="1e7df-183">Base64-</span></span><br/><span data-ttu-id="1e7df-184">encoded string</span><span class="sxs-lookup"><span data-stu-id="1e7df-184">encoded string</span></span> |<span data-ttu-id="1e7df-185">Content key to use for this track. If specified, the track_type or key_id is required.</span><span class="sxs-lookup"><span data-stu-id="1e7df-185">Content key to use for this track. If specified, the track_type or key_id is required.</span></span> <span data-ttu-id="1e7df-186">The content provider can use this option to inject the content key for this track instead of letting the Widevine license server generate or look up a key.</span><span class="sxs-lookup"><span data-stu-id="1e7df-186">The content provider can use this option to inject the content key for this track instead of letting the Widevine license server generate or look up a key.</span></span> |
| <span data-ttu-id="1e7df-187">content_key_specs.key_id</span><span class="sxs-lookup"><span data-stu-id="1e7df-187">content_key_specs.key_id</span></span> |<span data-ttu-id="1e7df-188">Base64-encoded string binary, 16 bytes</span><span class="sxs-lookup"><span data-stu-id="1e7df-188">Base64-encoded string binary, 16 bytes</span></span> |<span data-ttu-id="1e7df-189">Unique identifier for the key.</span><span class="sxs-lookup"><span data-stu-id="1e7df-189">Unique identifier for the key.</span></span> |

## <a name="policy-overrides"></a><span data-ttu-id="1e7df-190">Policy overrides</span><span class="sxs-lookup"><span data-stu-id="1e7df-190">Policy overrides</span></span>
| <span data-ttu-id="1e7df-191">Name</span><span class="sxs-lookup"><span data-stu-id="1e7df-191">Name</span></span> | <span data-ttu-id="1e7df-192">Value</span><span class="sxs-lookup"><span data-stu-id="1e7df-192">Value</span></span> | <span data-ttu-id="1e7df-193">Description</span><span class="sxs-lookup"><span data-stu-id="1e7df-193">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1e7df-194">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1e7df-194">policy_overrides.</span></span> <span data-ttu-id="1e7df-195">can_play</span><span class="sxs-lookup"><span data-stu-id="1e7df-195">can_play</span></span> |<span data-ttu-id="1e7df-196">Boolean, true or false</span><span class="sxs-lookup"><span data-stu-id="1e7df-196">Boolean, true or false</span></span> |<span data-ttu-id="1e7df-197">Indicates that playback of the content is allowed.</span><span class="sxs-lookup"><span data-stu-id="1e7df-197">Indicates that playback of the content is allowed.</span></span> <span data-ttu-id="1e7df-198">Default is false.</span><span class="sxs-lookup"><span data-stu-id="1e7df-198">Default is false.</span></span> |
| <span data-ttu-id="1e7df-199">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1e7df-199">policy_overrides.</span></span> <span data-ttu-id="1e7df-200">can_persist</span><span class="sxs-lookup"><span data-stu-id="1e7df-200">can_persist</span></span> |<span data-ttu-id="1e7df-201">Boolean, true or false</span><span class="sxs-lookup"><span data-stu-id="1e7df-201">Boolean, true or false</span></span> |<span data-ttu-id="1e7df-202">Indicates that the license might be persisted to nonvolatile storage for offline use.</span><span class="sxs-lookup"><span data-stu-id="1e7df-202">Indicates that the license might be persisted to nonvolatile storage for offline use.</span></span> <span data-ttu-id="1e7df-203">Default is false.</span><span class="sxs-lookup"><span data-stu-id="1e7df-203">Default is false.</span></span> |
| <span data-ttu-id="1e7df-204">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1e7df-204">policy_overrides.</span></span> <span data-ttu-id="1e7df-205">can_renew</span><span class="sxs-lookup"><span data-stu-id="1e7df-205">can_renew</span></span> |<span data-ttu-id="1e7df-206">Boolean, true or false</span><span class="sxs-lookup"><span data-stu-id="1e7df-206">Boolean, true or false</span></span> |<span data-ttu-id="1e7df-207">Indicates that renewal of this license is allowed.</span><span class="sxs-lookup"><span data-stu-id="1e7df-207">Indicates that renewal of this license is allowed.</span></span> <span data-ttu-id="1e7df-208">If true, the duration of the license can be extended by heartbeat.</span><span class="sxs-lookup"><span data-stu-id="1e7df-208">If true, the duration of the license can be extended by heartbeat.</span></span> <span data-ttu-id="1e7df-209">Default is false.</span><span class="sxs-lookup"><span data-stu-id="1e7df-209">Default is false.</span></span> |
| <span data-ttu-id="1e7df-210">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1e7df-210">policy_overrides.</span></span> <span data-ttu-id="1e7df-211">license_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="1e7df-211">license_duration_seconds</span></span> |<span data-ttu-id="1e7df-212">int64</span><span class="sxs-lookup"><span data-stu-id="1e7df-212">int64</span></span> |<span data-ttu-id="1e7df-213">Indicates the time window for this specific license.</span><span class="sxs-lookup"><span data-stu-id="1e7df-213">Indicates the time window for this specific license.</span></span> <span data-ttu-id="1e7df-214">A value of 0 indicates that there is no limit to the duration.</span><span class="sxs-lookup"><span data-stu-id="1e7df-214">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="1e7df-215">Default is 0.</span><span class="sxs-lookup"><span data-stu-id="1e7df-215">Default is 0.</span></span> |
| <span data-ttu-id="1e7df-216">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1e7df-216">policy_overrides.</span></span> <span data-ttu-id="1e7df-217">rental_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="1e7df-217">rental_duration_seconds</span></span> |<span data-ttu-id="1e7df-218">int64</span><span class="sxs-lookup"><span data-stu-id="1e7df-218">int64</span></span> |<span data-ttu-id="1e7df-219">Indicates the time window while playback is permitted.</span><span class="sxs-lookup"><span data-stu-id="1e7df-219">Indicates the time window while playback is permitted.</span></span> <span data-ttu-id="1e7df-220">A value of 0 indicates that there is no limit to the duration.</span><span class="sxs-lookup"><span data-stu-id="1e7df-220">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="1e7df-221">Default is 0.</span><span class="sxs-lookup"><span data-stu-id="1e7df-221">Default is 0.</span></span> |
| <span data-ttu-id="1e7df-222">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1e7df-222">policy_overrides.</span></span> <span data-ttu-id="1e7df-223">playback_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="1e7df-223">playback_duration_seconds</span></span> |<span data-ttu-id="1e7df-224">int64</span><span class="sxs-lookup"><span data-stu-id="1e7df-224">int64</span></span> |<span data-ttu-id="1e7df-225">The viewing window of time after playback starts within the license duration.</span><span class="sxs-lookup"><span data-stu-id="1e7df-225">The viewing window of time after playback starts within the license duration.</span></span> <span data-ttu-id="1e7df-226">A value of 0 indicates that there is no limit to the duration.</span><span class="sxs-lookup"><span data-stu-id="1e7df-226">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="1e7df-227">Default is 0.</span><span class="sxs-lookup"><span data-stu-id="1e7df-227">Default is 0.</span></span> |
| <span data-ttu-id="1e7df-228">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1e7df-228">policy_overrides.</span></span> <span data-ttu-id="1e7df-229">renewal_server_url</span><span class="sxs-lookup"><span data-stu-id="1e7df-229">renewal_server_url</span></span> |<span data-ttu-id="1e7df-230">string</span><span class="sxs-lookup"><span data-stu-id="1e7df-230">string</span></span> |<span data-ttu-id="1e7df-231">All heartbeat (renewal) requests for this license are directed to the specified URL.</span><span class="sxs-lookup"><span data-stu-id="1e7df-231">All heartbeat (renewal) requests for this license are directed to the specified URL.</span></span> <span data-ttu-id="1e7df-232">This field is used only if can_renew is true.</span><span class="sxs-lookup"><span data-stu-id="1e7df-232">This field is used only if can_renew is true.</span></span> |
| <span data-ttu-id="1e7df-233">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1e7df-233">policy_overrides.</span></span> <span data-ttu-id="1e7df-234">renewal_delay_seconds</span><span class="sxs-lookup"><span data-stu-id="1e7df-234">renewal_delay_seconds</span></span> |<span data-ttu-id="1e7df-235">int64</span><span class="sxs-lookup"><span data-stu-id="1e7df-235">int64</span></span> |<span data-ttu-id="1e7df-236">How many seconds after license_start_time before renewal is first attempted.</span><span class="sxs-lookup"><span data-stu-id="1e7df-236">How many seconds after license_start_time before renewal is first attempted.</span></span> <span data-ttu-id="1e7df-237">This field is used only if can_renew is true.</span><span class="sxs-lookup"><span data-stu-id="1e7df-237">This field is used only if can_renew is true.</span></span> <span data-ttu-id="1e7df-238">Default is 0.</span><span class="sxs-lookup"><span data-stu-id="1e7df-238">Default is 0.</span></span> |
| <span data-ttu-id="1e7df-239">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1e7df-239">policy_overrides.</span></span> <span data-ttu-id="1e7df-240">renewal_retry_interval_seconds</span><span class="sxs-lookup"><span data-stu-id="1e7df-240">renewal_retry_interval_seconds</span></span> |<span data-ttu-id="1e7df-241">int64</span><span class="sxs-lookup"><span data-stu-id="1e7df-241">int64</span></span> |<span data-ttu-id="1e7df-242">Specifies the delay in seconds between subsequent license renewal requests, in case of failure.</span><span class="sxs-lookup"><span data-stu-id="1e7df-242">Specifies the delay in seconds between subsequent license renewal requests, in case of failure.</span></span> <span data-ttu-id="1e7df-243">This field is used only if can_renew is true.</span><span class="sxs-lookup"><span data-stu-id="1e7df-243">This field is used only if can_renew is true.</span></span> |
| <span data-ttu-id="1e7df-244">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1e7df-244">policy_overrides.</span></span> <span data-ttu-id="1e7df-245">renewal_recovery_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="1e7df-245">renewal_recovery_duration_seconds</span></span> |<span data-ttu-id="1e7df-246">int64</span><span class="sxs-lookup"><span data-stu-id="1e7df-246">int64</span></span> |<span data-ttu-id="1e7df-247">The window of time in which playback can continue while renewal is attempted, yet unsuccessful due to back-end problems with the license server.</span><span class="sxs-lookup"><span data-stu-id="1e7df-247">The window of time in which playback can continue while renewal is attempted, yet unsuccessful due to back-end problems with the license server.</span></span> <span data-ttu-id="1e7df-248">A value of 0 indicates that there is no limit to the duration.</span><span class="sxs-lookup"><span data-stu-id="1e7df-248">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="1e7df-249">This field is used only if can_renew is true.</span><span class="sxs-lookup"><span data-stu-id="1e7df-249">This field is used only if can_renew is true.</span></span> |
| <span data-ttu-id="1e7df-250">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1e7df-250">policy_overrides.</span></span> <span data-ttu-id="1e7df-251">renew_with_usage</span><span class="sxs-lookup"><span data-stu-id="1e7df-251">renew_with_usage</span></span> |<span data-ttu-id="1e7df-252">Boolean, true or false</span><span class="sxs-lookup"><span data-stu-id="1e7df-252">Boolean, true or false</span></span> |<span data-ttu-id="1e7df-253">Indicates that the license is sent for renewal when usage starts.</span><span class="sxs-lookup"><span data-stu-id="1e7df-253">Indicates that the license is sent for renewal when usage starts.</span></span> <span data-ttu-id="1e7df-254">This field is used only if can_renew is true.</span><span class="sxs-lookup"><span data-stu-id="1e7df-254">This field is used only if can_renew is true.</span></span> |

## <a name="session-initialization"></a><span data-ttu-id="1e7df-255">Session initialization</span><span class="sxs-lookup"><span data-stu-id="1e7df-255">Session initialization</span></span>
| <span data-ttu-id="1e7df-256">Name</span><span class="sxs-lookup"><span data-stu-id="1e7df-256">Name</span></span> | <span data-ttu-id="1e7df-257">Value</span><span class="sxs-lookup"><span data-stu-id="1e7df-257">Value</span></span> | <span data-ttu-id="1e7df-258">Description</span><span class="sxs-lookup"><span data-stu-id="1e7df-258">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1e7df-259">provider_session_token</span><span class="sxs-lookup"><span data-stu-id="1e7df-259">provider_session_token</span></span> |<span data-ttu-id="1e7df-260">Base64-encoded string</span><span class="sxs-lookup"><span data-stu-id="1e7df-260">Base64-encoded string</span></span> |<span data-ttu-id="1e7df-261">This session token is passed back in the license and exists in subsequent renewals.</span><span class="sxs-lookup"><span data-stu-id="1e7df-261">This session token is passed back in the license and exists in subsequent renewals.</span></span> <span data-ttu-id="1e7df-262">The session token doesn't persist beyond sessions.</span><span class="sxs-lookup"><span data-stu-id="1e7df-262">The session token doesn't persist beyond sessions.</span></span> |
| <span data-ttu-id="1e7df-263">provider_client_token</span><span class="sxs-lookup"><span data-stu-id="1e7df-263">provider_client_token</span></span> |<span data-ttu-id="1e7df-264">Base64-encoded string</span><span class="sxs-lookup"><span data-stu-id="1e7df-264">Base64-encoded string</span></span> |<span data-ttu-id="1e7df-265">Client token to send back in the license response.</span><span class="sxs-lookup"><span data-stu-id="1e7df-265">Client token to send back in the license response.</span></span> <span data-ttu-id="1e7df-266">If the license request contains a client token, this value is ignored.</span><span class="sxs-lookup"><span data-stu-id="1e7df-266">If the license request contains a client token, this value is ignored.</span></span> <span data-ttu-id="1e7df-267">The client token persists beyond license sessions.</span><span class="sxs-lookup"><span data-stu-id="1e7df-267">The client token persists beyond license sessions.</span></span> |
| <span data-ttu-id="1e7df-268">override_provider_client_token</span><span class="sxs-lookup"><span data-stu-id="1e7df-268">override_provider_client_token</span></span> |<span data-ttu-id="1e7df-269">Boolean, true or false</span><span class="sxs-lookup"><span data-stu-id="1e7df-269">Boolean, true or false</span></span> |<span data-ttu-id="1e7df-270">If false and the license request contains a client token, use the token from the request even if a client token was specified in this structure.</span><span class="sxs-lookup"><span data-stu-id="1e7df-270">If false and the license request contains a client token, use the token from the request even if a client token was specified in this structure.</span></span> <span data-ttu-id="1e7df-271">If true, always use the token specified in this structure.</span><span class="sxs-lookup"><span data-stu-id="1e7df-271">If true, always use the token specified in this structure.</span></span> |

## <a name="configure-your-widevine-licenses-by-using-net-types"></a><span data-ttu-id="1e7df-272">Configure your Widevine licenses by using .NET types</span><span class="sxs-lookup"><span data-stu-id="1e7df-272">Configure your Widevine licenses by using .NET types</span></span>
<span data-ttu-id="1e7df-273">Media Services provides .NET APIs that you can use to configure your Widevine licenses.</span><span class="sxs-lookup"><span data-stu-id="1e7df-273">Media Services provides .NET APIs that you can use to configure your Widevine licenses.</span></span> 

### <a name="classes-as-defined-in-the-media-services-net-sdk"></a><span data-ttu-id="1e7df-274">Classes as defined in the Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="1e7df-274">Classes as defined in the Media Services .NET SDK</span></span>
<span data-ttu-id="1e7df-275">The following classes are the definitions of these types:</span><span class="sxs-lookup"><span data-stu-id="1e7df-275">The following classes are the definitions of these types:</span></span>

    public class WidevineMessage
    {
        public WidevineMessage();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public AllowedTrackTypes? allowed_track_types { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public ContentKeySpecs[] content_key_specs { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public object policy_overrides { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum AllowedTrackTypes
    {
        SD_ONLY = 0,
        SD_HD = 1
    }
    public class ContentKeySpecs
    {
        public ContentKeySpecs();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string key_id { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public RequiredOutputProtection required_output_protection { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public int? security_level { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string track_type { get; set; }
    }

    public class RequiredOutputProtection
    {
        public RequiredOutputProtection();

        public Hdcp hdcp { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum Hdcp
    {
        HDCP_NONE = 0,
        HDCP_V1 = 1,
        HDCP_V2 = 2
    }

### <a name="example"></a><span data-ttu-id="1e7df-276">Example</span><span class="sxs-lookup"><span data-stu-id="1e7df-276">Example</span></span>
<span data-ttu-id="1e7df-277">The following example shows how to use .NET APIs to configure a simple Widevine license:</span><span class="sxs-lookup"><span data-stu-id="1e7df-277">The following example shows how to use .NET APIs to configure a simple Widevine license:</span></span>

    private static string ConfigureWidevineLicenseTemplate()
    {
        var template = new WidevineMessage
        {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                new ContentKeySpecs
                {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                }
            },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
        };

        string configuration = JsonConvert.SerializeObject(template);
        return configuration;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="1e7df-278">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="1e7df-278">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1e7df-279">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="1e7df-279">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="1e7df-280">See also</span><span class="sxs-lookup"><span data-stu-id="1e7df-280">See also</span></span>
[<span data-ttu-id="1e7df-281">Use PlayReady and/or Widevine dynamic common encryption</span><span class="sxs-lookup"><span data-stu-id="1e7df-281">Use PlayReady and/or Widevine dynamic common encryption</span></span>](media-services-protect-with-playready-widevine.md)

