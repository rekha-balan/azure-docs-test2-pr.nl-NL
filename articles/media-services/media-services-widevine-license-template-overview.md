---
title: Widevine license template overview | Microsoft Docs
description: This topic gives an overview of a Widevine license template that used to configure Widevine licenses.
author: juliako
manager: erikre
editor: ''
services: media-services
documentationcenter: ''
ms.assetid: 0e6f1f05-7ed6-4ed6-82a0-0cc2182b075a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: juliako
ms.openlocfilehash: 5ef6e368a170816b7000c23cdf686644690fca45
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551540"
---
# <a name="widevine-license-template-overview"></a><span data-ttu-id="db790-103">Widevine license template overview</span><span class="sxs-lookup"><span data-stu-id="db790-103">Widevine license template overview</span></span>
## <a name="overview"></a><span data-ttu-id="db790-104">Overview</span><span class="sxs-lookup"><span data-stu-id="db790-104">Overview</span></span>
<span data-ttu-id="db790-105">Azure Media Services now enables you to configure and request Widevine licenses.</span><span class="sxs-lookup"><span data-stu-id="db790-105">Azure Media Services now enables you to configure and request Widevine licenses.</span></span> <span data-ttu-id="db790-106">When the end user player tries to play your Widevine protected content, a request is sent to the license delivery service to obtain a license.</span><span class="sxs-lookup"><span data-stu-id="db790-106">When the end user player tries to play your Widevine protected content, a request is sent to the license delivery service to obtain a license.</span></span> <span data-ttu-id="db790-107">If the license service approves the request, it issues the license which is sent to the client and can be used to decrypt and play the specified content.</span><span class="sxs-lookup"><span data-stu-id="db790-107">If the license service approves the request, it issues the license which is sent to the client and can be used to decrypt and play the specified content.</span></span>

<span data-ttu-id="db790-108">Widevine license request is formatted as a JSON message.</span><span class="sxs-lookup"><span data-stu-id="db790-108">Widevine license request is formatted as a JSON message.</span></span>  

>[!NOTE]
> <span data-ttu-id="db790-109">You can choose to create an empty message with no values just "{}" and a license template will be created with all defaults.</span><span class="sxs-lookup"><span data-stu-id="db790-109">You can choose to create an empty message with no values just "{}" and a license template will be created with all defaults.</span></span> <span data-ttu-id="db790-110">The default works for most cases.</span><span class="sxs-lookup"><span data-stu-id="db790-110">The default works for most cases.</span></span> <span data-ttu-id="db790-111">For example, for MS based license delivery scenarios that should always be default.</span><span class="sxs-lookup"><span data-stu-id="db790-111">For example, for MS based license delivery scenarios that should always be default.</span></span> <span data-ttu-id="db790-112">If you do need to set the "provider" and "content_id" values, a provider must match Google's Widevine credentials.</span><span class="sxs-lookup"><span data-stu-id="db790-112">If you do need to set the "provider" and "content_id" values, a provider must match Google's Widevine credentials.</span></span>

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

## <a name="json-message"></a><span data-ttu-id="db790-113">JSON message</span><span class="sxs-lookup"><span data-stu-id="db790-113">JSON message</span></span>
| <span data-ttu-id="db790-114">Name</span><span class="sxs-lookup"><span data-stu-id="db790-114">Name</span></span> | <span data-ttu-id="db790-115">Value</span><span class="sxs-lookup"><span data-stu-id="db790-115">Value</span></span> | <span data-ttu-id="db790-116">Description</span><span class="sxs-lookup"><span data-stu-id="db790-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="db790-117">payload</span><span class="sxs-lookup"><span data-stu-id="db790-117">payload</span></span> |<span data-ttu-id="db790-118">Base64 encoded string</span><span class="sxs-lookup"><span data-stu-id="db790-118">Base64 encoded string</span></span> |<span data-ttu-id="db790-119">The license request sent by a client.</span><span class="sxs-lookup"><span data-stu-id="db790-119">The license request sent by a client.</span></span> |
| <span data-ttu-id="db790-120">content_id</span><span class="sxs-lookup"><span data-stu-id="db790-120">content_id</span></span> |<span data-ttu-id="db790-121">Base64 encoded string</span><span class="sxs-lookup"><span data-stu-id="db790-121">Base64 encoded string</span></span> |<span data-ttu-id="db790-122">Identifier used to derive KeyId(s) and Content Key(s) for each content_key_specs.track_type.</span><span class="sxs-lookup"><span data-stu-id="db790-122">Identifier used to derive KeyId(s) and Content Key(s) for each content_key_specs.track_type.</span></span> |
| <span data-ttu-id="db790-123">provider</span><span class="sxs-lookup"><span data-stu-id="db790-123">provider</span></span> |<span data-ttu-id="db790-124">string</span><span class="sxs-lookup"><span data-stu-id="db790-124">string</span></span> |<span data-ttu-id="db790-125">Used to look up content keys and policies.</span><span class="sxs-lookup"><span data-stu-id="db790-125">Used to look up content keys and policies.</span></span> <span data-ttu-id="db790-126">If MS key delivery is used for Widevine license delivery, this parameter is ignored.</span><span class="sxs-lookup"><span data-stu-id="db790-126">If MS key delivery is used for Widevine license delivery, this parameter is ignored.</span></span> |
| <span data-ttu-id="db790-127">policy_name</span><span class="sxs-lookup"><span data-stu-id="db790-127">policy_name</span></span> |<span data-ttu-id="db790-128">string</span><span class="sxs-lookup"><span data-stu-id="db790-128">string</span></span> |<span data-ttu-id="db790-129">Name of a previously registered policy.</span><span class="sxs-lookup"><span data-stu-id="db790-129">Name of a previously registered policy.</span></span> <span data-ttu-id="db790-130">Optional</span><span class="sxs-lookup"><span data-stu-id="db790-130">Optional</span></span> |
| <span data-ttu-id="db790-131">allowed_track_types</span><span class="sxs-lookup"><span data-stu-id="db790-131">allowed_track_types</span></span> |<span data-ttu-id="db790-132">enum</span><span class="sxs-lookup"><span data-stu-id="db790-132">enum</span></span> |<span data-ttu-id="db790-133">SD_ONLY or SD_HD.</span><span class="sxs-lookup"><span data-stu-id="db790-133">SD_ONLY or SD_HD.</span></span> <span data-ttu-id="db790-134">Controls which content keys should be included in a license</span><span class="sxs-lookup"><span data-stu-id="db790-134">Controls which content keys should be included in a license</span></span> |
| <span data-ttu-id="db790-135">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="db790-135">content_key_specs</span></span> |<span data-ttu-id="db790-136">array of JSON structures, see **Content Key Specs** below</span><span class="sxs-lookup"><span data-stu-id="db790-136">array of JSON structures, see **Content Key Specs** below</span></span> |<span data-ttu-id="db790-137">A finer grained control on what content keys to return.</span><span class="sxs-lookup"><span data-stu-id="db790-137">A finer grained control on what content keys to return.</span></span> <span data-ttu-id="db790-138">See Content Key Spec below for details.</span><span class="sxs-lookup"><span data-stu-id="db790-138">See Content Key Spec below for details.</span></span>  <span data-ttu-id="db790-139">Only one of allowed_track_types and content_key_specs can be specified.</span><span class="sxs-lookup"><span data-stu-id="db790-139">Only one of allowed_track_types and content_key_specs can be specified.</span></span> |
| <span data-ttu-id="db790-140">use_policy_overrides_exclusively</span><span class="sxs-lookup"><span data-stu-id="db790-140">use_policy_overrides_exclusively</span></span> |<span data-ttu-id="db790-141">boolean.</span><span class="sxs-lookup"><span data-stu-id="db790-141">boolean.</span></span> <span data-ttu-id="db790-142">true or false</span><span class="sxs-lookup"><span data-stu-id="db790-142">true or false</span></span> |<span data-ttu-id="db790-143">Use policy attributes specified by policy_overrides and omit all previously stored policy.</span><span class="sxs-lookup"><span data-stu-id="db790-143">Use policy attributes specified by policy_overrides and omit all previously stored policy.</span></span> |
| <span data-ttu-id="db790-144">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="db790-144">policy_overrides</span></span> |<span data-ttu-id="db790-145">JSON structure, see **Policy Overrides** below</span><span class="sxs-lookup"><span data-stu-id="db790-145">JSON structure, see **Policy Overrides** below</span></span> |<span data-ttu-id="db790-146">Policy settings for this license.</span><span class="sxs-lookup"><span data-stu-id="db790-146">Policy settings for this license.</span></span>  <span data-ttu-id="db790-147">In the event this asset has a pre-defined policy, these specified values will be used.</span><span class="sxs-lookup"><span data-stu-id="db790-147">In the event this asset has a pre-defined policy, these specified values will be used.</span></span> |
| <span data-ttu-id="db790-148">session_init</span><span class="sxs-lookup"><span data-stu-id="db790-148">session_init</span></span> |<span data-ttu-id="db790-149">JSON structure, see **Session Initialization** below</span><span class="sxs-lookup"><span data-stu-id="db790-149">JSON structure, see **Session Initialization** below</span></span> |<span data-ttu-id="db790-150">Optional data passed to license.</span><span class="sxs-lookup"><span data-stu-id="db790-150">Optional data passed to license.</span></span> |
| <span data-ttu-id="db790-151">parse_only</span><span class="sxs-lookup"><span data-stu-id="db790-151">parse_only</span></span> |<span data-ttu-id="db790-152">boolean.</span><span class="sxs-lookup"><span data-stu-id="db790-152">boolean.</span></span> <span data-ttu-id="db790-153">true or false</span><span class="sxs-lookup"><span data-stu-id="db790-153">true or false</span></span> |<span data-ttu-id="db790-154">The license request is parsed but no license is issued.</span><span class="sxs-lookup"><span data-stu-id="db790-154">The license request is parsed but no license is issued.</span></span> <span data-ttu-id="db790-155">However, values form the license request are returned in the response.</span><span class="sxs-lookup"><span data-stu-id="db790-155">However, values form the license request are returned in the response.</span></span> |

## <a name="content-key-specs"></a><span data-ttu-id="db790-156">Content Key Specs</span><span class="sxs-lookup"><span data-stu-id="db790-156">Content Key Specs</span></span>
<span data-ttu-id="db790-157">If a pre-existing policy exist, there is no need to specify any of the values in the Content Key Spec.  The pre-existing policy associated with this content will be used to determine the output protection such as HDCP and CGMS.</span><span class="sxs-lookup"><span data-stu-id="db790-157">If a pre-existing policy exist, there is no need to specify any of the values in the Content Key Spec.  The pre-existing policy associated with this content will be used to determine the output protection such as HDCP and CGMS.</span></span>  <span data-ttu-id="db790-158">If a pre-existing policy is not registered with the Widevine License Server, the content provider can inject the values into the license request.</span><span class="sxs-lookup"><span data-stu-id="db790-158">If a pre-existing policy is not registered with the Widevine License Server, the content provider can inject the values into the license request.</span></span>   

<span data-ttu-id="db790-159">Each content_key_specs must be specified for all tracks, regardless of the option use_policy_overrides_exclusively.</span><span class="sxs-lookup"><span data-stu-id="db790-159">Each content_key_specs must be specified for all tracks, regardless of the option use_policy_overrides_exclusively.</span></span> 

| <span data-ttu-id="db790-160">Name</span><span class="sxs-lookup"><span data-stu-id="db790-160">Name</span></span> | <span data-ttu-id="db790-161">Value</span><span class="sxs-lookup"><span data-stu-id="db790-161">Value</span></span> | <span data-ttu-id="db790-162">Description</span><span class="sxs-lookup"><span data-stu-id="db790-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="db790-163">content_key_specs.</span><span class="sxs-lookup"><span data-stu-id="db790-163">content_key_specs.</span></span> <span data-ttu-id="db790-164">track_type</span><span class="sxs-lookup"><span data-stu-id="db790-164">track_type</span></span> |<span data-ttu-id="db790-165">string</span><span class="sxs-lookup"><span data-stu-id="db790-165">string</span></span> |<span data-ttu-id="db790-166">A track type name.</span><span class="sxs-lookup"><span data-stu-id="db790-166">A track type name.</span></span> <span data-ttu-id="db790-167">If content_key_specs is specified in the license request, make sure to specify all track types explicitly.</span><span class="sxs-lookup"><span data-stu-id="db790-167">If content_key_specs is specified in the license request, make sure to specify all track types explicitly.</span></span> <span data-ttu-id="db790-168">Failure to do so will result in failure to playback past 10 seconds.</span><span class="sxs-lookup"><span data-stu-id="db790-168">Failure to do so will result in failure to playback past 10 seconds.</span></span> |
| <span data-ttu-id="db790-169">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="db790-169">content_key_specs</span></span>  <br/> <span data-ttu-id="db790-170">security_level</span><span class="sxs-lookup"><span data-stu-id="db790-170">security_level</span></span> |<span data-ttu-id="db790-171">uint32</span><span class="sxs-lookup"><span data-stu-id="db790-171">uint32</span></span> |<span data-ttu-id="db790-172">Defines client robustness requirements for playback.</span><span class="sxs-lookup"><span data-stu-id="db790-172">Defines client robustness requirements for playback.</span></span> <br/> <span data-ttu-id="db790-173">1 - Software-based whitebox crypto is required.</span><span class="sxs-lookup"><span data-stu-id="db790-173">1 - Software-based whitebox crypto is required.</span></span> <br/> <span data-ttu-id="db790-174">2 - Software crypto and an obfuscated decoder is required.</span><span class="sxs-lookup"><span data-stu-id="db790-174">2 - Software crypto and an obfuscated decoder is required.</span></span> <br/> <span data-ttu-id="db790-175">3 - The key material and crypto operations must be performed within a hardware backed trusted execution environment.</span><span class="sxs-lookup"><span data-stu-id="db790-175">3 - The key material and crypto operations must be performed within a hardware backed trusted execution environment.</span></span> <br/> <span data-ttu-id="db790-176">4 - The crypto and decoding of content must be performed within a hardware backed trusted execution environment.</span><span class="sxs-lookup"><span data-stu-id="db790-176">4 - The crypto and decoding of content must be performed within a hardware backed trusted execution environment.</span></span>  <br/> <span data-ttu-id="db790-177">5 - The crypto, decoding and all handling of the media (compressed and uncompressed) must be handled within a hardware backed trusted execution environment.</span><span class="sxs-lookup"><span data-stu-id="db790-177">5 - The crypto, decoding and all handling of the media (compressed and uncompressed) must be handled within a hardware backed trusted execution environment.</span></span> |
| <span data-ttu-id="db790-178">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="db790-178">content_key_specs</span></span> <br/> <span data-ttu-id="db790-179">required_output_protection.hdc</span><span class="sxs-lookup"><span data-stu-id="db790-179">required_output_protection.hdc</span></span> |<span data-ttu-id="db790-180">string - one of: HDCP_NONE, HDCP_V1, HDCP_V2</span><span class="sxs-lookup"><span data-stu-id="db790-180">string - one of: HDCP_NONE, HDCP_V1, HDCP_V2</span></span> |<span data-ttu-id="db790-181">Indicates whether HDCP is require</span><span class="sxs-lookup"><span data-stu-id="db790-181">Indicates whether HDCP is require</span></span> |
| <span data-ttu-id="db790-182">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="db790-182">content_key_specs</span></span> <br/><span data-ttu-id="db790-183">key</span><span class="sxs-lookup"><span data-stu-id="db790-183">key</span></span> |<span data-ttu-id="db790-184">Base64</span><span class="sxs-lookup"><span data-stu-id="db790-184">Base64</span></span> <br/><span data-ttu-id="db790-185">encoded string</span><span class="sxs-lookup"><span data-stu-id="db790-185">encoded string</span></span> |<span data-ttu-id="db790-186">Content key to use for this track. If specified, the track_type or key_id is required.</span><span class="sxs-lookup"><span data-stu-id="db790-186">Content key to use for this track. If specified, the track_type or key_id is required.</span></span>  <span data-ttu-id="db790-187">This option allows the content provider to inject the content key for this track instead of letting Widevine license server generate or lookup a key.</span><span class="sxs-lookup"><span data-stu-id="db790-187">This option allows the content provider to inject the content key for this track instead of letting Widevine license server generate or lookup a key.</span></span> |
| <span data-ttu-id="db790-188">content_key_specs.key_id</span><span class="sxs-lookup"><span data-stu-id="db790-188">content_key_specs.key_id</span></span> |<span data-ttu-id="db790-189">Base64 encoded string  binary, 16 bytes</span><span class="sxs-lookup"><span data-stu-id="db790-189">Base64 encoded string  binary, 16 bytes</span></span> |<span data-ttu-id="db790-190">Unique identifier for the key.</span><span class="sxs-lookup"><span data-stu-id="db790-190">Unique identifier for the key.</span></span> |

## <a name="policy-overrides"></a><span data-ttu-id="db790-191">Policy Overrides</span><span class="sxs-lookup"><span data-stu-id="db790-191">Policy Overrides</span></span>
| <span data-ttu-id="db790-192">Name</span><span class="sxs-lookup"><span data-stu-id="db790-192">Name</span></span> | <span data-ttu-id="db790-193">Value</span><span class="sxs-lookup"><span data-stu-id="db790-193">Value</span></span> | <span data-ttu-id="db790-194">Description</span><span class="sxs-lookup"><span data-stu-id="db790-194">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="db790-195">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="db790-195">policy_overrides.</span></span> <span data-ttu-id="db790-196">can_play</span><span class="sxs-lookup"><span data-stu-id="db790-196">can_play</span></span> |<span data-ttu-id="db790-197">boolean.</span><span class="sxs-lookup"><span data-stu-id="db790-197">boolean.</span></span> <span data-ttu-id="db790-198">true or false</span><span class="sxs-lookup"><span data-stu-id="db790-198">true or false</span></span> |<span data-ttu-id="db790-199">Indicates that playback of the content is allowed.</span><span class="sxs-lookup"><span data-stu-id="db790-199">Indicates that playback of the content is allowed.</span></span> <span data-ttu-id="db790-200">Default is false.</span><span class="sxs-lookup"><span data-stu-id="db790-200">Default is false.</span></span> |
| <span data-ttu-id="db790-201">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="db790-201">policy_overrides.</span></span> <span data-ttu-id="db790-202">can_persist</span><span class="sxs-lookup"><span data-stu-id="db790-202">can_persist</span></span> |<span data-ttu-id="db790-203">boolean.</span><span class="sxs-lookup"><span data-stu-id="db790-203">boolean.</span></span> <span data-ttu-id="db790-204">true or false</span><span class="sxs-lookup"><span data-stu-id="db790-204">true or false</span></span> |<span data-ttu-id="db790-205">Indicates that the license may be persisted to non-volatile storage for offline use.</span><span class="sxs-lookup"><span data-stu-id="db790-205">Indicates that the license may be persisted to non-volatile storage for offline use.</span></span> <span data-ttu-id="db790-206">Default is false.</span><span class="sxs-lookup"><span data-stu-id="db790-206">Default is false.</span></span> |
| <span data-ttu-id="db790-207">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="db790-207">policy_overrides.</span></span> <span data-ttu-id="db790-208">can_renew</span><span class="sxs-lookup"><span data-stu-id="db790-208">can_renew</span></span> |<span data-ttu-id="db790-209">boolean true or false</span><span class="sxs-lookup"><span data-stu-id="db790-209">boolean true or false</span></span> |<span data-ttu-id="db790-210">Indicates that renewal of this license is allowed.</span><span class="sxs-lookup"><span data-stu-id="db790-210">Indicates that renewal of this license is allowed.</span></span> <span data-ttu-id="db790-211">If true, the duration of the license can be extended by heartbeat.</span><span class="sxs-lookup"><span data-stu-id="db790-211">If true, the duration of the license can be extended by heartbeat.</span></span> <span data-ttu-id="db790-212">Default is false.</span><span class="sxs-lookup"><span data-stu-id="db790-212">Default is false.</span></span> |
| <span data-ttu-id="db790-213">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="db790-213">policy_overrides.</span></span> <span data-ttu-id="db790-214">license_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="db790-214">license_duration_seconds</span></span> |<span data-ttu-id="db790-215">int64</span><span class="sxs-lookup"><span data-stu-id="db790-215">int64</span></span> |<span data-ttu-id="db790-216">Indicates the time window for this specific license.</span><span class="sxs-lookup"><span data-stu-id="db790-216">Indicates the time window for this specific license.</span></span> <span data-ttu-id="db790-217">A value of 0 indicates that there is no limit to the duration.</span><span class="sxs-lookup"><span data-stu-id="db790-217">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="db790-218">Default is 0.</span><span class="sxs-lookup"><span data-stu-id="db790-218">Default is 0.</span></span> |
| <span data-ttu-id="db790-219">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="db790-219">policy_overrides.</span></span> <span data-ttu-id="db790-220">rental_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="db790-220">rental_duration_seconds</span></span> |<span data-ttu-id="db790-221">int64</span><span class="sxs-lookup"><span data-stu-id="db790-221">int64</span></span> |<span data-ttu-id="db790-222">Indicates the time window while playback is permitted.</span><span class="sxs-lookup"><span data-stu-id="db790-222">Indicates the time window while playback is permitted.</span></span> <span data-ttu-id="db790-223">A value of 0 indicates that there is no limit to the duration.</span><span class="sxs-lookup"><span data-stu-id="db790-223">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="db790-224">Default is 0.</span><span class="sxs-lookup"><span data-stu-id="db790-224">Default is 0.</span></span> |
| <span data-ttu-id="db790-225">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="db790-225">policy_overrides.</span></span> <span data-ttu-id="db790-226">playback_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="db790-226">playback_duration_seconds</span></span> |<span data-ttu-id="db790-227">int64</span><span class="sxs-lookup"><span data-stu-id="db790-227">int64</span></span> |<span data-ttu-id="db790-228">The viewing window of time once playback starts within the license duration.</span><span class="sxs-lookup"><span data-stu-id="db790-228">The viewing window of time once playback starts within the license duration.</span></span> <span data-ttu-id="db790-229">A value of 0 indicates that there is no limit to the duration.</span><span class="sxs-lookup"><span data-stu-id="db790-229">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="db790-230">Default is 0.</span><span class="sxs-lookup"><span data-stu-id="db790-230">Default is 0.</span></span> |
| <span data-ttu-id="db790-231">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="db790-231">policy_overrides.</span></span> <span data-ttu-id="db790-232">renewal_server_url</span><span class="sxs-lookup"><span data-stu-id="db790-232">renewal_server_url</span></span> |<span data-ttu-id="db790-233">string</span><span class="sxs-lookup"><span data-stu-id="db790-233">string</span></span> |<span data-ttu-id="db790-234">All heartbeat (renewal) requests for this license shall be directed to the specified URL.</span><span class="sxs-lookup"><span data-stu-id="db790-234">All heartbeat (renewal) requests for this license shall be directed to the specified URL.</span></span> <span data-ttu-id="db790-235">This field is only used if can_renew is true.</span><span class="sxs-lookup"><span data-stu-id="db790-235">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="db790-236">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="db790-236">policy_overrides.</span></span> <span data-ttu-id="db790-237">renewal_delay_seconds</span><span class="sxs-lookup"><span data-stu-id="db790-237">renewal_delay_seconds</span></span> |<span data-ttu-id="db790-238">int64</span><span class="sxs-lookup"><span data-stu-id="db790-238">int64</span></span> |<span data-ttu-id="db790-239">How many seconds after license_start_time, before renewal is first attempted.</span><span class="sxs-lookup"><span data-stu-id="db790-239">How many seconds after license_start_time, before renewal is first attempted.</span></span> <span data-ttu-id="db790-240">This field is only used if can_renew is true.</span><span class="sxs-lookup"><span data-stu-id="db790-240">This field is only used if can_renew is true.</span></span> <span data-ttu-id="db790-241">Default is 0</span><span class="sxs-lookup"><span data-stu-id="db790-241">Default is 0</span></span> |
| <span data-ttu-id="db790-242">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="db790-242">policy_overrides.</span></span> <span data-ttu-id="db790-243">renewal_retry_interval_seconds</span><span class="sxs-lookup"><span data-stu-id="db790-243">renewal_retry_interval_seconds</span></span> |<span data-ttu-id="db790-244">int64</span><span class="sxs-lookup"><span data-stu-id="db790-244">int64</span></span> |<span data-ttu-id="db790-245">Specifies the delay in seconds between subsequent license renewal requests, in case of failure.</span><span class="sxs-lookup"><span data-stu-id="db790-245">Specifies the delay in seconds between subsequent license renewal requests, in case of failure.</span></span> <span data-ttu-id="db790-246">This field is only used if can_renew is true.</span><span class="sxs-lookup"><span data-stu-id="db790-246">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="db790-247">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="db790-247">policy_overrides.</span></span> <span data-ttu-id="db790-248">renewal_recovery_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="db790-248">renewal_recovery_duration_seconds</span></span> |<span data-ttu-id="db790-249">int64</span><span class="sxs-lookup"><span data-stu-id="db790-249">int64</span></span> |<span data-ttu-id="db790-250">The window of time, in which playback is allowed to continue while renewal is attempted, yet unsuccessful due to backend problems with the license server.</span><span class="sxs-lookup"><span data-stu-id="db790-250">The window of time, in which playback is allowed to continue while renewal is attempted, yet unsuccessful due to backend problems with the license server.</span></span> <span data-ttu-id="db790-251">A value of 0 indicates that there is no limit to the duration.</span><span class="sxs-lookup"><span data-stu-id="db790-251">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="db790-252">This field is only used if can_renew is true.</span><span class="sxs-lookup"><span data-stu-id="db790-252">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="db790-253">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="db790-253">policy_overrides.</span></span> <span data-ttu-id="db790-254">renew_with_usage</span><span class="sxs-lookup"><span data-stu-id="db790-254">renew_with_usage</span></span> |<span data-ttu-id="db790-255">boolean true or false</span><span class="sxs-lookup"><span data-stu-id="db790-255">boolean true or false</span></span> |<span data-ttu-id="db790-256">Indicates that the license shall be sent for renewal when usage is started.</span><span class="sxs-lookup"><span data-stu-id="db790-256">Indicates that the license shall be sent for renewal when usage is started.</span></span> <span data-ttu-id="db790-257">This field is only used if can_renew is true.</span><span class="sxs-lookup"><span data-stu-id="db790-257">This field is only used if can_renew is true.</span></span> |

## <a name="session-initialization"></a><span data-ttu-id="db790-258">Session Initialization</span><span class="sxs-lookup"><span data-stu-id="db790-258">Session Initialization</span></span>
| <span data-ttu-id="db790-259">Name</span><span class="sxs-lookup"><span data-stu-id="db790-259">Name</span></span> | <span data-ttu-id="db790-260">Value</span><span class="sxs-lookup"><span data-stu-id="db790-260">Value</span></span> | <span data-ttu-id="db790-261">Description</span><span class="sxs-lookup"><span data-stu-id="db790-261">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="db790-262">provider_session_token</span><span class="sxs-lookup"><span data-stu-id="db790-262">provider_session_token</span></span> |<span data-ttu-id="db790-263">Base64 encoded string</span><span class="sxs-lookup"><span data-stu-id="db790-263">Base64 encoded string</span></span> |<span data-ttu-id="db790-264">This session token is passed back in the license and will exist in subsequent renewals.</span><span class="sxs-lookup"><span data-stu-id="db790-264">This session token is passed back in the license and will exist in subsequent renewals.</span></span>  <span data-ttu-id="db790-265">The session token will not persist beyond sessions.</span><span class="sxs-lookup"><span data-stu-id="db790-265">The session token will not persist beyond sessions.</span></span> |
| <span data-ttu-id="db790-266">provider_client_token</span><span class="sxs-lookup"><span data-stu-id="db790-266">provider_client_token</span></span> |<span data-ttu-id="db790-267">Base64 encoded string</span><span class="sxs-lookup"><span data-stu-id="db790-267">Base64 encoded string</span></span> |<span data-ttu-id="db790-268">Client token to send back in the license response.</span><span class="sxs-lookup"><span data-stu-id="db790-268">Client token to send back in the license response.</span></span>  <span data-ttu-id="db790-269">If the license request contains a client token, this value is ignored.</span><span class="sxs-lookup"><span data-stu-id="db790-269">If the license request contains a client token, this value is ignored.</span></span> <span data-ttu-id="db790-270">The client token will persist beyond license sessions.</span><span class="sxs-lookup"><span data-stu-id="db790-270">The client token will persist beyond license sessions.</span></span> |
| <span data-ttu-id="db790-271">override_provider_client_token</span><span class="sxs-lookup"><span data-stu-id="db790-271">override_provider_client_token</span></span> |<span data-ttu-id="db790-272">boolean.</span><span class="sxs-lookup"><span data-stu-id="db790-272">boolean.</span></span> <span data-ttu-id="db790-273">true or false</span><span class="sxs-lookup"><span data-stu-id="db790-273">true or false</span></span> |<span data-ttu-id="db790-274">If false and the license request contains a client token, use the token from the request even if a client token was specified in this structure.</span><span class="sxs-lookup"><span data-stu-id="db790-274">If false and the license request contains a client token, use the token from the request even if a client token was specified in this structure.</span></span>  <span data-ttu-id="db790-275">If true, always use the token specified in this structure.</span><span class="sxs-lookup"><span data-stu-id="db790-275">If true, always use the token specified in this structure.</span></span> |

## <a name="configure-your-widevine-licenses-using-net-types"></a><span data-ttu-id="db790-276">Configure your Widevine licenses using .NET types</span><span class="sxs-lookup"><span data-stu-id="db790-276">Configure your Widevine licenses using .NET types</span></span>
<span data-ttu-id="db790-277">Media Services provides .NET APIs that let you configure your Widevine licenses.</span><span class="sxs-lookup"><span data-stu-id="db790-277">Media Services provides .NET APIs that let you configure your Widevine licenses.</span></span> 

### <a name="classes-as-defined-in-the-media-services-net-sdk"></a><span data-ttu-id="db790-278">Classes as defined in the Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="db790-278">Classes as defined in the Media Services .NET SDK</span></span>
<span data-ttu-id="db790-279">The following are the definitions of these types.</span><span class="sxs-lookup"><span data-stu-id="db790-279">The following are the definitions of these types.</span></span>

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

### <a name="example"></a><span data-ttu-id="db790-280">Example</span><span class="sxs-lookup"><span data-stu-id="db790-280">Example</span></span>
<span data-ttu-id="db790-281">The following example shows how to use .NET APIs to configure  a simple Widevine license.</span><span class="sxs-lookup"><span data-stu-id="db790-281">The following example shows how to use .NET APIs to configure  a simple Widevine license.</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="db790-282">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="db790-282">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="db790-283">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="db790-283">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="db790-284">See also</span><span class="sxs-lookup"><span data-stu-id="db790-284">See also</span></span>
[<span data-ttu-id="db790-285">Using PlayReady and/or Widevine Dynamic Common Encryption</span><span class="sxs-lookup"><span data-stu-id="db790-285">Using PlayReady and/or Widevine Dynamic Common Encryption</span></span>](media-services-protect-with-drm.md)

