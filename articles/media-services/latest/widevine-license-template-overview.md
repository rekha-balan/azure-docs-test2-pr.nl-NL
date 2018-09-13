---
title: Azure Media Services with Widevine license template overview | Microsoft Docs
description: This topic gives an overview of a Widevine license template that is used to configure Widevine licenses.
author: juliako
manager: cfowler
editor: ''
services: media-services
documentationcenter: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2018
ms.author: juliako
ms.openlocfilehash: e54aff6e42d19755d274393d4221578cf5595cc5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869274"
---
# <a name="widevine-license-template-overview"></a><span data-ttu-id="e81fd-103">Widevine license template overview</span><span class="sxs-lookup"><span data-stu-id="e81fd-103">Widevine license template overview</span></span> 

<span data-ttu-id="e81fd-104">Azure Media Services enables you to encrypt your content with **Google Widevine**.</span><span class="sxs-lookup"><span data-stu-id="e81fd-104">Azure Media Services enables you to encrypt your content with **Google Widevine**.</span></span> <span data-ttu-id="e81fd-105">Media Services also provides a service for delivering Widevine licenses.</span><span class="sxs-lookup"><span data-stu-id="e81fd-105">Media Services also provides a service for delivering Widevine licenses.</span></span> <span data-ttu-id="e81fd-106">You can use Azure Media Services APIs to configure Widevine licenses.</span><span class="sxs-lookup"><span data-stu-id="e81fd-106">You can use Azure Media Services APIs to configure Widevine licenses.</span></span> <span data-ttu-id="e81fd-107">When a player tries to play your Widevine-protected content, a request is sent to the license delivery service to obtain the license.</span><span class="sxs-lookup"><span data-stu-id="e81fd-107">When a player tries to play your Widevine-protected content, a request is sent to the license delivery service to obtain the license.</span></span> <span data-ttu-id="e81fd-108">If the license service approves the request, the service issues the license.</span><span class="sxs-lookup"><span data-stu-id="e81fd-108">If the license service approves the request, the service issues the license.</span></span> <span data-ttu-id="e81fd-109">It's sent to the client and is used to decrypt and play the specified content.</span><span class="sxs-lookup"><span data-stu-id="e81fd-109">It's sent to the client and is used to decrypt and play the specified content.</span></span>

<span data-ttu-id="e81fd-110">A Widevine license request is formatted as a JSON message.</span><span class="sxs-lookup"><span data-stu-id="e81fd-110">A Widevine license request is formatted as a JSON message.</span></span>  

>[!NOTE]
> <span data-ttu-id="e81fd-111">You can create an empty message with no values, just "{}."</span><span class="sxs-lookup"><span data-stu-id="e81fd-111">You can create an empty message with no values, just "{}."</span></span> <span data-ttu-id="e81fd-112">Then a license template is created with defaults.</span><span class="sxs-lookup"><span data-stu-id="e81fd-112">Then a license template is created with defaults.</span></span> <span data-ttu-id="e81fd-113">The default works for most cases.</span><span class="sxs-lookup"><span data-stu-id="e81fd-113">The default works for most cases.</span></span> <span data-ttu-id="e81fd-114">Microsoft-based license-delivery scenarios should always use the defaults.</span><span class="sxs-lookup"><span data-stu-id="e81fd-114">Microsoft-based license-delivery scenarios should always use the defaults.</span></span> <span data-ttu-id="e81fd-115">If you need to set the "provider" and "content_id" values, a provider must match Widevine credentials.</span><span class="sxs-lookup"><span data-stu-id="e81fd-115">If you need to set the "provider" and "content_id" values, a provider must match Widevine credentials.</span></span>

    {  
       "payload":"<license challenge>",
       "content_id": "<content id>"
       "provider": "<provider>"
       "allowed_track_types":"<types>",
       "content_key_specs":[  
          {  
             "track_type":"<track type 1>"
          },
          {  
             "track_type":"<track type 2>"
          },
          …
       ],
       "policy_overrides":{  
          "can_play":<can play>,
          "can persist":<can persist>,
          "can_renew":<can renew>,
          "rental_duration_seconds":<rental duration>,
          "playback_duration_seconds":<playback duration>,
          "license_duration_seconds":<license duration>,
          "renewal_recovery_duration_seconds":<renewal recovery duration>,
          "renewal_server_url":"<renewal server url>",
          "renewal_delay_seconds":<renewal delay>,
          "renewal_retry_interval_seconds":<renewal retry interval>,
          "renew_with_usage”:<renew with usage>
       }
    }

## <a name="json-message"></a><span data-ttu-id="e81fd-116">JSON message</span><span class="sxs-lookup"><span data-stu-id="e81fd-116">JSON message</span></span>

| <span data-ttu-id="e81fd-117">Name</span><span class="sxs-lookup"><span data-stu-id="e81fd-117">Name</span></span> | <span data-ttu-id="e81fd-118">Value</span><span class="sxs-lookup"><span data-stu-id="e81fd-118">Value</span></span> | <span data-ttu-id="e81fd-119">Description</span><span class="sxs-lookup"><span data-stu-id="e81fd-119">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e81fd-120">payload</span><span class="sxs-lookup"><span data-stu-id="e81fd-120">payload</span></span> |<span data-ttu-id="e81fd-121">Base64-encoded string</span><span class="sxs-lookup"><span data-stu-id="e81fd-121">Base64-encoded string</span></span> |<span data-ttu-id="e81fd-122">The license request sent by a client.</span><span class="sxs-lookup"><span data-stu-id="e81fd-122">The license request sent by a client.</span></span> |
| <span data-ttu-id="e81fd-123">content_id</span><span class="sxs-lookup"><span data-stu-id="e81fd-123">content_id</span></span> |<span data-ttu-id="e81fd-124">Base64-encoded string</span><span class="sxs-lookup"><span data-stu-id="e81fd-124">Base64-encoded string</span></span> |<span data-ttu-id="e81fd-125">Identifier used to derive the key ID and content key for each content_key_specs.track_type.</span><span class="sxs-lookup"><span data-stu-id="e81fd-125">Identifier used to derive the key ID and content key for each content_key_specs.track_type.</span></span> |
| <span data-ttu-id="e81fd-126">provider</span><span class="sxs-lookup"><span data-stu-id="e81fd-126">provider</span></span> |<span data-ttu-id="e81fd-127">string</span><span class="sxs-lookup"><span data-stu-id="e81fd-127">string</span></span> |<span data-ttu-id="e81fd-128">Used to look up content keys and policies.</span><span class="sxs-lookup"><span data-stu-id="e81fd-128">Used to look up content keys and policies.</span></span> <span data-ttu-id="e81fd-129">If Microsoft key delivery is used for Widevine license delivery, this parameter is ignored.</span><span class="sxs-lookup"><span data-stu-id="e81fd-129">If Microsoft key delivery is used for Widevine license delivery, this parameter is ignored.</span></span> |
| <span data-ttu-id="e81fd-130">policy_name</span><span class="sxs-lookup"><span data-stu-id="e81fd-130">policy_name</span></span> |<span data-ttu-id="e81fd-131">string</span><span class="sxs-lookup"><span data-stu-id="e81fd-131">string</span></span> |<span data-ttu-id="e81fd-132">Name of a previously registered policy.</span><span class="sxs-lookup"><span data-stu-id="e81fd-132">Name of a previously registered policy.</span></span> <span data-ttu-id="e81fd-133">Optional.</span><span class="sxs-lookup"><span data-stu-id="e81fd-133">Optional.</span></span> |
| <span data-ttu-id="e81fd-134">allowed_track_types</span><span class="sxs-lookup"><span data-stu-id="e81fd-134">allowed_track_types</span></span> |<span data-ttu-id="e81fd-135">enum</span><span class="sxs-lookup"><span data-stu-id="e81fd-135">enum</span></span> |<span data-ttu-id="e81fd-136">SD_ONLY or SD_HD.</span><span class="sxs-lookup"><span data-stu-id="e81fd-136">SD_ONLY or SD_HD.</span></span> <span data-ttu-id="e81fd-137">Controls which content keys are included in a license.</span><span class="sxs-lookup"><span data-stu-id="e81fd-137">Controls which content keys are included in a license.</span></span> |
| <span data-ttu-id="e81fd-138">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="e81fd-138">content_key_specs</span></span> |<span data-ttu-id="e81fd-139">Array of JSON structures, see the section "Content key specs."</span><span class="sxs-lookup"><span data-stu-id="e81fd-139">Array of JSON structures, see the section "Content key specs."</span></span>  |<span data-ttu-id="e81fd-140">A finer-grained control on which content keys to return.</span><span class="sxs-lookup"><span data-stu-id="e81fd-140">A finer-grained control on which content keys to return.</span></span> <span data-ttu-id="e81fd-141">For more information, see the section "Content key specs."</span><span class="sxs-lookup"><span data-stu-id="e81fd-141">For more information, see the section "Content key specs."</span></span> <span data-ttu-id="e81fd-142">Only one of the allowed_track_types and content_key_specs values can be specified.</span><span class="sxs-lookup"><span data-stu-id="e81fd-142">Only one of the allowed_track_types and content_key_specs values can be specified.</span></span> |
| <span data-ttu-id="e81fd-143">use_policy_overrides_exclusively</span><span class="sxs-lookup"><span data-stu-id="e81fd-143">use_policy_overrides_exclusively</span></span> |<span data-ttu-id="e81fd-144">Boolean, true or false</span><span class="sxs-lookup"><span data-stu-id="e81fd-144">Boolean, true or false</span></span> |<span data-ttu-id="e81fd-145">Use policy attributes specified by policy_overrides, and omit all previously stored policy.</span><span class="sxs-lookup"><span data-stu-id="e81fd-145">Use policy attributes specified by policy_overrides, and omit all previously stored policy.</span></span> |
| <span data-ttu-id="e81fd-146">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="e81fd-146">policy_overrides</span></span> |<span data-ttu-id="e81fd-147">JSON structure, see the section "Policy overrides."</span><span class="sxs-lookup"><span data-stu-id="e81fd-147">JSON structure, see the section "Policy overrides."</span></span> |<span data-ttu-id="e81fd-148">Policy settings for this license.</span><span class="sxs-lookup"><span data-stu-id="e81fd-148">Policy settings for this license.</span></span>  <span data-ttu-id="e81fd-149">In the event this asset has a predefined policy, these specified values are used.</span><span class="sxs-lookup"><span data-stu-id="e81fd-149">In the event this asset has a predefined policy, these specified values are used.</span></span> |
| <span data-ttu-id="e81fd-150">session_init</span><span class="sxs-lookup"><span data-stu-id="e81fd-150">session_init</span></span> |<span data-ttu-id="e81fd-151">JSON structure, see the section "Session initialization."</span><span class="sxs-lookup"><span data-stu-id="e81fd-151">JSON structure, see the section "Session initialization."</span></span> |<span data-ttu-id="e81fd-152">Optional data is passed to the license.</span><span class="sxs-lookup"><span data-stu-id="e81fd-152">Optional data is passed to the license.</span></span> |
| <span data-ttu-id="e81fd-153">parse_only</span><span class="sxs-lookup"><span data-stu-id="e81fd-153">parse_only</span></span> |<span data-ttu-id="e81fd-154">Boolean, true or false</span><span class="sxs-lookup"><span data-stu-id="e81fd-154">Boolean, true or false</span></span> |<span data-ttu-id="e81fd-155">The license request is parsed, but no license is issued.</span><span class="sxs-lookup"><span data-stu-id="e81fd-155">The license request is parsed, but no license is issued.</span></span> <span data-ttu-id="e81fd-156">However, values from the license request are returned in the response.</span><span class="sxs-lookup"><span data-stu-id="e81fd-156">However, values from the license request are returned in the response.</span></span> |

## <a name="content-key-specs"></a><span data-ttu-id="e81fd-157">Content key specs</span><span class="sxs-lookup"><span data-stu-id="e81fd-157">Content key specs</span></span>
<span data-ttu-id="e81fd-158">If a pre-existing policy exists, there is no need to specify any of the values in the content key spec. The pre-existing policy associated with this content is used to determine the output protection, such as High-bandwidth Digital Content Protection (HDCP) and the Copy General Management System (CGMS).</span><span class="sxs-lookup"><span data-stu-id="e81fd-158">If a pre-existing policy exists, there is no need to specify any of the values in the content key spec. The pre-existing policy associated with this content is used to determine the output protection, such as High-bandwidth Digital Content Protection (HDCP) and the Copy General Management System (CGMS).</span></span> <span data-ttu-id="e81fd-159">If a pre-existing policy isn't registered with the Widevine license server, the content provider can inject the values into the license request.</span><span class="sxs-lookup"><span data-stu-id="e81fd-159">If a pre-existing policy isn't registered with the Widevine license server, the content provider can inject the values into the license request.</span></span>   

<span data-ttu-id="e81fd-160">Each content_key_specs value must be specified for all tracks, regardless of the use_policy_overrides_exclusively option.</span><span class="sxs-lookup"><span data-stu-id="e81fd-160">Each content_key_specs value must be specified for all tracks, regardless of the use_policy_overrides_exclusively option.</span></span> 

| <span data-ttu-id="e81fd-161">Name</span><span class="sxs-lookup"><span data-stu-id="e81fd-161">Name</span></span> | <span data-ttu-id="e81fd-162">Value</span><span class="sxs-lookup"><span data-stu-id="e81fd-162">Value</span></span> | <span data-ttu-id="e81fd-163">Description</span><span class="sxs-lookup"><span data-stu-id="e81fd-163">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e81fd-164">content_key_specs.</span><span class="sxs-lookup"><span data-stu-id="e81fd-164">content_key_specs.</span></span> <span data-ttu-id="e81fd-165">track_type</span><span class="sxs-lookup"><span data-stu-id="e81fd-165">track_type</span></span> |<span data-ttu-id="e81fd-166">string</span><span class="sxs-lookup"><span data-stu-id="e81fd-166">string</span></span> |<span data-ttu-id="e81fd-167">A track type name.</span><span class="sxs-lookup"><span data-stu-id="e81fd-167">A track type name.</span></span> <span data-ttu-id="e81fd-168">If content_key_specs is specified in the license request, make sure to specify all track types explicitly.</span><span class="sxs-lookup"><span data-stu-id="e81fd-168">If content_key_specs is specified in the license request, make sure to specify all track types explicitly.</span></span> <span data-ttu-id="e81fd-169">Failure to do so results in failure to play back past 10 seconds.</span><span class="sxs-lookup"><span data-stu-id="e81fd-169">Failure to do so results in failure to play back past 10 seconds.</span></span> |
| <span data-ttu-id="e81fd-170">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="e81fd-170">content_key_specs</span></span>  <br/> <span data-ttu-id="e81fd-171">security_level</span><span class="sxs-lookup"><span data-stu-id="e81fd-171">security_level</span></span> |<span data-ttu-id="e81fd-172">uint32</span><span class="sxs-lookup"><span data-stu-id="e81fd-172">uint32</span></span> |<span data-ttu-id="e81fd-173">Defines client robustness requirements for playback.</span><span class="sxs-lookup"><span data-stu-id="e81fd-173">Defines client robustness requirements for playback.</span></span> <br/> <span data-ttu-id="e81fd-174">- Software-based white-box cryptography is required.</span><span class="sxs-lookup"><span data-stu-id="e81fd-174">- Software-based white-box cryptography is required.</span></span> <br/> <span data-ttu-id="e81fd-175">- Software cryptography and an obfuscated decoder are required.</span><span class="sxs-lookup"><span data-stu-id="e81fd-175">- Software cryptography and an obfuscated decoder are required.</span></span> <br/> <span data-ttu-id="e81fd-176">- The key material and cryptography operations must be performed within a hardware-backed trusted execution environment.</span><span class="sxs-lookup"><span data-stu-id="e81fd-176">- The key material and cryptography operations must be performed within a hardware-backed trusted execution environment.</span></span> <br/> <span data-ttu-id="e81fd-177">- The cryptography and decoding of content must be performed within a hardware-backed trusted execution environment.</span><span class="sxs-lookup"><span data-stu-id="e81fd-177">- The cryptography and decoding of content must be performed within a hardware-backed trusted execution environment.</span></span>  <br/> <span data-ttu-id="e81fd-178">- The cryptography, decoding, and all handling of the media (compressed and uncompressed) must be handled within a hardware-backed trusted execution environment.</span><span class="sxs-lookup"><span data-stu-id="e81fd-178">- The cryptography, decoding, and all handling of the media (compressed and uncompressed) must be handled within a hardware-backed trusted execution environment.</span></span> |
| <span data-ttu-id="e81fd-179">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="e81fd-179">content_key_specs</span></span> <br/> <span data-ttu-id="e81fd-180">required_output_protection.hdc</span><span class="sxs-lookup"><span data-stu-id="e81fd-180">required_output_protection.hdc</span></span> |<span data-ttu-id="e81fd-181">string, one of HDCP_NONE, HDCP_V1, HDCP_V2</span><span class="sxs-lookup"><span data-stu-id="e81fd-181">string, one of HDCP_NONE, HDCP_V1, HDCP_V2</span></span> |<span data-ttu-id="e81fd-182">Indicates whether HDCP is required.</span><span class="sxs-lookup"><span data-stu-id="e81fd-182">Indicates whether HDCP is required.</span></span> |
| <span data-ttu-id="e81fd-183">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="e81fd-183">content_key_specs</span></span> <br/><span data-ttu-id="e81fd-184">key</span><span class="sxs-lookup"><span data-stu-id="e81fd-184">key</span></span> |<span data-ttu-id="e81fd-185">Base64-</span><span class="sxs-lookup"><span data-stu-id="e81fd-185">Base64-</span></span><br/><span data-ttu-id="e81fd-186">encoded string</span><span class="sxs-lookup"><span data-stu-id="e81fd-186">encoded string</span></span> |<span data-ttu-id="e81fd-187">Content key to use for this track. If specified, the track_type or key_id is required.</span><span class="sxs-lookup"><span data-stu-id="e81fd-187">Content key to use for this track. If specified, the track_type or key_id is required.</span></span> <span data-ttu-id="e81fd-188">The content provider can use this option to inject the content key for this track instead of letting the Widevine license server generate or look up a key.</span><span class="sxs-lookup"><span data-stu-id="e81fd-188">The content provider can use this option to inject the content key for this track instead of letting the Widevine license server generate or look up a key.</span></span> |
| <span data-ttu-id="e81fd-189">content_key_specs.key_id</span><span class="sxs-lookup"><span data-stu-id="e81fd-189">content_key_specs.key_id</span></span> |<span data-ttu-id="e81fd-190">Base64-encoded string binary, 16 bytes</span><span class="sxs-lookup"><span data-stu-id="e81fd-190">Base64-encoded string binary, 16 bytes</span></span> |<span data-ttu-id="e81fd-191">Unique identifier for the key.</span><span class="sxs-lookup"><span data-stu-id="e81fd-191">Unique identifier for the key.</span></span> |

## <a name="policy-overrides"></a><span data-ttu-id="e81fd-192">Policy overrides</span><span class="sxs-lookup"><span data-stu-id="e81fd-192">Policy overrides</span></span>
| <span data-ttu-id="e81fd-193">Name</span><span class="sxs-lookup"><span data-stu-id="e81fd-193">Name</span></span> | <span data-ttu-id="e81fd-194">Value</span><span class="sxs-lookup"><span data-stu-id="e81fd-194">Value</span></span> | <span data-ttu-id="e81fd-195">Description</span><span class="sxs-lookup"><span data-stu-id="e81fd-195">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e81fd-196">policy_overrides&#46;can_play</span><span class="sxs-lookup"><span data-stu-id="e81fd-196">policy_overrides&#46;can_play</span></span> |<span data-ttu-id="e81fd-197">Boolean, true or false</span><span class="sxs-lookup"><span data-stu-id="e81fd-197">Boolean, true or false</span></span> |<span data-ttu-id="e81fd-198">Indicates that playback of the content is allowed.</span><span class="sxs-lookup"><span data-stu-id="e81fd-198">Indicates that playback of the content is allowed.</span></span> <span data-ttu-id="e81fd-199">Default is false.</span><span class="sxs-lookup"><span data-stu-id="e81fd-199">Default is false.</span></span> |
| <span data-ttu-id="e81fd-200">policy_overrides&#46;can_persist</span><span class="sxs-lookup"><span data-stu-id="e81fd-200">policy_overrides&#46;can_persist</span></span> |<span data-ttu-id="e81fd-201">Boolean, true or false</span><span class="sxs-lookup"><span data-stu-id="e81fd-201">Boolean, true or false</span></span> |<span data-ttu-id="e81fd-202">Indicates that the license might be persisted to nonvolatile storage for offline use.</span><span class="sxs-lookup"><span data-stu-id="e81fd-202">Indicates that the license might be persisted to nonvolatile storage for offline use.</span></span> <span data-ttu-id="e81fd-203">Default is false.</span><span class="sxs-lookup"><span data-stu-id="e81fd-203">Default is false.</span></span> |
| <span data-ttu-id="e81fd-204">policy_overrides&#46;can_renew</span><span class="sxs-lookup"><span data-stu-id="e81fd-204">policy_overrides&#46;can_renew</span></span> |<span data-ttu-id="e81fd-205">Boolean, true or false</span><span class="sxs-lookup"><span data-stu-id="e81fd-205">Boolean, true or false</span></span> |<span data-ttu-id="e81fd-206">Indicates that renewal of this license is allowed.</span><span class="sxs-lookup"><span data-stu-id="e81fd-206">Indicates that renewal of this license is allowed.</span></span> <span data-ttu-id="e81fd-207">If true, the duration of the license can be extended by heartbeat.</span><span class="sxs-lookup"><span data-stu-id="e81fd-207">If true, the duration of the license can be extended by heartbeat.</span></span> <span data-ttu-id="e81fd-208">Default is false.</span><span class="sxs-lookup"><span data-stu-id="e81fd-208">Default is false.</span></span> |
| <span data-ttu-id="e81fd-209">policy_overrides&#46;license_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="e81fd-209">policy_overrides&#46;license_duration_seconds</span></span> |<span data-ttu-id="e81fd-210">int64</span><span class="sxs-lookup"><span data-stu-id="e81fd-210">int64</span></span> |<span data-ttu-id="e81fd-211">Indicates the time window for this specific license.</span><span class="sxs-lookup"><span data-stu-id="e81fd-211">Indicates the time window for this specific license.</span></span> <span data-ttu-id="e81fd-212">A value of 0 indicates that there is no limit to the duration.</span><span class="sxs-lookup"><span data-stu-id="e81fd-212">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="e81fd-213">Default is 0.</span><span class="sxs-lookup"><span data-stu-id="e81fd-213">Default is 0.</span></span> |
| <span data-ttu-id="e81fd-214">policy_overrides&#46;rental_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="e81fd-214">policy_overrides&#46;rental_duration_seconds</span></span> |<span data-ttu-id="e81fd-215">int64</span><span class="sxs-lookup"><span data-stu-id="e81fd-215">int64</span></span> |<span data-ttu-id="e81fd-216">Indicates the time window while playback is permitted.</span><span class="sxs-lookup"><span data-stu-id="e81fd-216">Indicates the time window while playback is permitted.</span></span> <span data-ttu-id="e81fd-217">A value of 0 indicates that there is no limit to the duration.</span><span class="sxs-lookup"><span data-stu-id="e81fd-217">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="e81fd-218">Default is 0.</span><span class="sxs-lookup"><span data-stu-id="e81fd-218">Default is 0.</span></span> |
| <span data-ttu-id="e81fd-219">policy_overrides&#46;playback_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="e81fd-219">policy_overrides&#46;playback_duration_seconds</span></span> |<span data-ttu-id="e81fd-220">int64</span><span class="sxs-lookup"><span data-stu-id="e81fd-220">int64</span></span> |<span data-ttu-id="e81fd-221">The viewing window of time after playback starts within the license duration.</span><span class="sxs-lookup"><span data-stu-id="e81fd-221">The viewing window of time after playback starts within the license duration.</span></span> <span data-ttu-id="e81fd-222">A value of 0 indicates that there is no limit to the duration.</span><span class="sxs-lookup"><span data-stu-id="e81fd-222">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="e81fd-223">Default is 0.</span><span class="sxs-lookup"><span data-stu-id="e81fd-223">Default is 0.</span></span> |
| <span data-ttu-id="e81fd-224">policy_overrides&#46;renewal_server_url</span><span class="sxs-lookup"><span data-stu-id="e81fd-224">policy_overrides&#46;renewal_server_url</span></span> |<span data-ttu-id="e81fd-225">string</span><span class="sxs-lookup"><span data-stu-id="e81fd-225">string</span></span> |<span data-ttu-id="e81fd-226">All heartbeat (renewal) requests for this license is directed to the specified URL.</span><span class="sxs-lookup"><span data-stu-id="e81fd-226">All heartbeat (renewal) requests for this license is directed to the specified URL.</span></span> <span data-ttu-id="e81fd-227">This field is used only if can_renew is true.</span><span class="sxs-lookup"><span data-stu-id="e81fd-227">This field is used only if can_renew is true.</span></span> |
| <span data-ttu-id="e81fd-228">policy_overrides&#46;renewal_delay_seconds</span><span class="sxs-lookup"><span data-stu-id="e81fd-228">policy_overrides&#46;renewal_delay_seconds</span></span> |<span data-ttu-id="e81fd-229">int64</span><span class="sxs-lookup"><span data-stu-id="e81fd-229">int64</span></span> |<span data-ttu-id="e81fd-230">How many seconds after license_start_time before renewal is first attempted.</span><span class="sxs-lookup"><span data-stu-id="e81fd-230">How many seconds after license_start_time before renewal is first attempted.</span></span> <span data-ttu-id="e81fd-231">This field is used only if can_renew is true.</span><span class="sxs-lookup"><span data-stu-id="e81fd-231">This field is used only if can_renew is true.</span></span> <span data-ttu-id="e81fd-232">Default is 0.</span><span class="sxs-lookup"><span data-stu-id="e81fd-232">Default is 0.</span></span> |
| <span data-ttu-id="e81fd-233">policy_overrides&#46;renewal_retry_interval_seconds</span><span class="sxs-lookup"><span data-stu-id="e81fd-233">policy_overrides&#46;renewal_retry_interval_seconds</span></span> |<span data-ttu-id="e81fd-234">int64</span><span class="sxs-lookup"><span data-stu-id="e81fd-234">int64</span></span> |<span data-ttu-id="e81fd-235">Specifies the delay in seconds between subsequent license renewal requests, in case of failure.</span><span class="sxs-lookup"><span data-stu-id="e81fd-235">Specifies the delay in seconds between subsequent license renewal requests, in case of failure.</span></span> <span data-ttu-id="e81fd-236">This field is used only if can_renew is true.</span><span class="sxs-lookup"><span data-stu-id="e81fd-236">This field is used only if can_renew is true.</span></span> |
| <span data-ttu-id="e81fd-237">policy_overrides&#46;renewal_recovery_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="e81fd-237">policy_overrides&#46;renewal_recovery_duration_seconds</span></span> |<span data-ttu-id="e81fd-238">int64</span><span class="sxs-lookup"><span data-stu-id="e81fd-238">int64</span></span> |<span data-ttu-id="e81fd-239">The window of time in which playback can continue while renewal is attempted, yet unsuccessful due to back-end problems with the license server.</span><span class="sxs-lookup"><span data-stu-id="e81fd-239">The window of time in which playback can continue while renewal is attempted, yet unsuccessful due to back-end problems with the license server.</span></span> <span data-ttu-id="e81fd-240">A value of 0 indicates that there is no limit to the duration.</span><span class="sxs-lookup"><span data-stu-id="e81fd-240">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="e81fd-241">This field is used only if can_renew is true.</span><span class="sxs-lookup"><span data-stu-id="e81fd-241">This field is used only if can_renew is true.</span></span> |
| <span data-ttu-id="e81fd-242">policy_overrides&#46;renew_with_usage</span><span class="sxs-lookup"><span data-stu-id="e81fd-242">policy_overrides&#46;renew_with_usage</span></span> |<span data-ttu-id="e81fd-243">Boolean, true or false</span><span class="sxs-lookup"><span data-stu-id="e81fd-243">Boolean, true or false</span></span> |<span data-ttu-id="e81fd-244">Indicates that the license is sent for renewal when usage starts.</span><span class="sxs-lookup"><span data-stu-id="e81fd-244">Indicates that the license is sent for renewal when usage starts.</span></span> <span data-ttu-id="e81fd-245">This field is used only if can_renew is true.</span><span class="sxs-lookup"><span data-stu-id="e81fd-245">This field is used only if can_renew is true.</span></span> |

## <a name="session-initialization"></a><span data-ttu-id="e81fd-246">Session initialization</span><span class="sxs-lookup"><span data-stu-id="e81fd-246">Session initialization</span></span>
| <span data-ttu-id="e81fd-247">Name</span><span class="sxs-lookup"><span data-stu-id="e81fd-247">Name</span></span> | <span data-ttu-id="e81fd-248">Value</span><span class="sxs-lookup"><span data-stu-id="e81fd-248">Value</span></span> | <span data-ttu-id="e81fd-249">Description</span><span class="sxs-lookup"><span data-stu-id="e81fd-249">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e81fd-250">provider_session_token</span><span class="sxs-lookup"><span data-stu-id="e81fd-250">provider_session_token</span></span> |<span data-ttu-id="e81fd-251">Base64-encoded string</span><span class="sxs-lookup"><span data-stu-id="e81fd-251">Base64-encoded string</span></span> |<span data-ttu-id="e81fd-252">This session token is passed back in the license and exists in subsequent renewals.</span><span class="sxs-lookup"><span data-stu-id="e81fd-252">This session token is passed back in the license and exists in subsequent renewals.</span></span> <span data-ttu-id="e81fd-253">The session token doesn't persist beyond sessions.</span><span class="sxs-lookup"><span data-stu-id="e81fd-253">The session token doesn't persist beyond sessions.</span></span> |
| <span data-ttu-id="e81fd-254">provider_client_token</span><span class="sxs-lookup"><span data-stu-id="e81fd-254">provider_client_token</span></span> |<span data-ttu-id="e81fd-255">Base64-encoded string</span><span class="sxs-lookup"><span data-stu-id="e81fd-255">Base64-encoded string</span></span> |<span data-ttu-id="e81fd-256">Client token to send back in the license response.</span><span class="sxs-lookup"><span data-stu-id="e81fd-256">Client token to send back in the license response.</span></span> <span data-ttu-id="e81fd-257">If the license request contains a client token, this value is ignored.</span><span class="sxs-lookup"><span data-stu-id="e81fd-257">If the license request contains a client token, this value is ignored.</span></span> <span data-ttu-id="e81fd-258">The client token persists beyond license sessions.</span><span class="sxs-lookup"><span data-stu-id="e81fd-258">The client token persists beyond license sessions.</span></span> |
| <span data-ttu-id="e81fd-259">override_provider_client_token</span><span class="sxs-lookup"><span data-stu-id="e81fd-259">override_provider_client_token</span></span> |<span data-ttu-id="e81fd-260">Boolean, true or false</span><span class="sxs-lookup"><span data-stu-id="e81fd-260">Boolean, true or false</span></span> |<span data-ttu-id="e81fd-261">If false and the license request contains a client token, use the token from the request even if a client token was specified in this structure.</span><span class="sxs-lookup"><span data-stu-id="e81fd-261">If false and the license request contains a client token, use the token from the request even if a client token was specified in this structure.</span></span> <span data-ttu-id="e81fd-262">If true, always use the token specified in this structure.</span><span class="sxs-lookup"><span data-stu-id="e81fd-262">If true, always use the token specified in this structure.</span></span> |

## <a name="configure-your-widevine-license-with-net"></a><span data-ttu-id="e81fd-263">Configure your Widevine license with .NET</span><span class="sxs-lookup"><span data-stu-id="e81fd-263">Configure your Widevine license with .NET</span></span> 

<span data-ttu-id="e81fd-264">Media Services provides a class that lets you configure a Widevine license.</span><span class="sxs-lookup"><span data-stu-id="e81fd-264">Media Services provides a class that lets you configure a Widevine license.</span></span> <span data-ttu-id="e81fd-265">To construct the license, pass JSON to [WidevineTemplate](https://docs.microsoft.com/dotnet/api/microsoft.azure.management.media.models.contentkeypolicywidevineconfiguration.widevinetemplate?view=azure-dotnet#Microsoft_Azure_Management_Media_Models_ContentKeyPolicyWidevineConfiguration_WidevineTemplate).</span><span class="sxs-lookup"><span data-stu-id="e81fd-265">To construct the license, pass JSON to [WidevineTemplate](https://docs.microsoft.com/dotnet/api/microsoft.azure.management.media.models.contentkeypolicywidevineconfiguration.widevinetemplate?view=azure-dotnet#Microsoft_Azure_Management_Media_Models_ContentKeyPolicyWidevineConfiguration_WidevineTemplate).</span></span>

<span data-ttu-id="e81fd-266">To configure the template, you can:</span><span class="sxs-lookup"><span data-stu-id="e81fd-266">To configure the template, you can:</span></span>

### <a name="directly-construct-a-json-string"></a><span data-ttu-id="e81fd-267">Directly construct a JSON string</span><span class="sxs-lookup"><span data-stu-id="e81fd-267">Directly construct a JSON string</span></span>

<span data-ttu-id="e81fd-268">This method may be error-prone.</span><span class="sxs-lookup"><span data-stu-id="e81fd-268">This method may be error-prone.</span></span> <span data-ttu-id="e81fd-269">It is recommended to use other method, described in [Define needed classes and serialize to JSON](#classes).</span><span class="sxs-lookup"><span data-stu-id="e81fd-269">It is recommended to use other method, described in [Define needed classes and serialize to JSON](#classes).</span></span>

    ```csharp
    ContentKeyPolicyWidevineConfiguration objContentKeyPolicyWidevineConfiguration = new ContentKeyPolicyWidevineConfiguration
    {
        WidevineTemplate = @"{""allowed_track_types"":""SD_HD"",""content_key_specs"":[{""track_type"":""SD"",""security_level"":1,""required_output_protection"":{""hdcp"":""HDCP_V2""}}],""policy_overrides"":{""can_play"":true,""can_persist"":true,""can_renew"":false}}"
    };
    ```

### <a id="classes"></a> <span data-ttu-id="e81fd-270">Define needed classes and serialize to JSON</span><span class="sxs-lookup"><span data-stu-id="e81fd-270">Define needed classes and serialize to JSON</span></span>

#### <a name="define-classes"></a><span data-ttu-id="e81fd-271">Define classes</span><span class="sxs-lookup"><span data-stu-id="e81fd-271">Define classes</span></span>

<span data-ttu-id="e81fd-272">The following example shows an example of definitions of classes that map to Widevine JSON schema.</span><span class="sxs-lookup"><span data-stu-id="e81fd-272">The following example shows an example of definitions of classes that map to Widevine JSON schema.</span></span> <span data-ttu-id="e81fd-273">You can instantiate the classes before serializing them to JSON string.</span><span class="sxs-lookup"><span data-stu-id="e81fd-273">You can instantiate the classes before serializing them to JSON string.</span></span>  

    ```csharp
    public class PolicyOverrides
    {
        public bool CanPlay { get; set; }
        public bool CanPersist { get; set; }
        public bool CanRenew { get; set; }
        public int RentalDurationSeconds { get; set; }    //Indicates the time window while playback is permitted. A value of 0 indicates that there is no limit to the duration. Default is 0.
        public int PlaybackDurationSeconds { get; set; }  //The viewing window of time after playback starts within the license duration. A value of 0 indicates that there is no limit to the duration. Default is 0.
        public int LicenseDurationSeconds { get; set; }   //Indicates the time window for this specific license. A value of 0 indicates that there is no limit to the duration. Default is 0.
    }

    public class ContentKeySpec
    {
        public string TrackType { get; set; }
        public int SecurityLevel { get; set; }
        public OutputProtection RequiredOutputProtection { get; set; }
    }

    public class OutputProtection
    {
        public string HDCP { get; set; }
    }

    public class WidevineTemplate
    {
        public string AllowedTrackTypes { get; set; }
        public ContentKeySpec[] ContentKeySpecs { get; set; }
        public PolicyOverrides PolicyOverrides { get; set; }
    }
    ```

#### <a name="configure-the-license"></a><span data-ttu-id="e81fd-274">Configure the license</span><span class="sxs-lookup"><span data-stu-id="e81fd-274">Configure the license</span></span>

<span data-ttu-id="e81fd-275">Use classes defined in the previous section to create JSON that is used to configure [WidevineTemplate](https://docs.microsoft.com/dotnet/api/microsoft.azure.management.media.models.contentkeypolicywidevineconfiguration.widevinetemplate?view=azure-dotnet#Microsoft_Azure_Management_Media_Models_ContentKeyPolicyWidevineConfiguration_WidevineTemplate):</span><span class="sxs-lookup"><span data-stu-id="e81fd-275">Use classes defined in the previous section to create JSON that is used to configure [WidevineTemplate](https://docs.microsoft.com/dotnet/api/microsoft.azure.management.media.models.contentkeypolicywidevineconfiguration.widevinetemplate?view=azure-dotnet#Microsoft_Azure_Management_Media_Models_ContentKeyPolicyWidevineConfiguration_WidevineTemplate):</span></span>

```csharp
private static ContentKeyPolicyWidevineConfiguration ConfigureWidevineLicenseTempate()
{
    WidevineTemplate template = new WidevineTemplate()
    {
        AllowedTrackTypes = "SD_HD",
        ContentKeySpecs = new ContentKeySpec[]
        {
            new ContentKeySpec()
            {
                TrackType = "SD",
                SecurityLevel = 1,
                RequiredOutputProtection = new OutputProtection()
                {
                    HDCP = "HDCP_V2"
                }
            }
        },
        PolicyOverrides = new PolicyOverrides()
        {
            CanPlay = true,
            CanPersist = true,
            CanRenew = false,
            RentalDurationSeconds = 2592000,
            PlaybackDurationSeconds = 10800,
            LicenseDurationSeconds = 604800,
        }
    };

    ContentKeyPolicyWidevineConfiguration objContentKeyPolicyWidevineConfiguration = new ContentKeyPolicyWidevineConfiguration
    {
        WidevineTemplate = Newtonsoft.Json.JsonConvert.SerializeObject(template)
    };
    return objContentKeyPolicyWidevineConfiguration;
}
```

## <a name="next-steps"></a><span data-ttu-id="e81fd-276">Next steps</span><span class="sxs-lookup"><span data-stu-id="e81fd-276">Next steps</span></span>

<span data-ttu-id="e81fd-277">Check out how to [protect with DRM](protect-with-drm.md)</span><span class="sxs-lookup"><span data-stu-id="e81fd-277">Check out how to [protect with DRM](protect-with-drm.md)</span></span>